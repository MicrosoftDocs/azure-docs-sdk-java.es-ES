---
title: Administración de conjuntos de escalado de máquinas virtuales con Java | Microsoft Docs
description: Código de ejemplo para administrar conjuntos de escalado de máquinas virtuales de Azure mediante Azure SDK para Java
author: rloutlaw
manager: douge
ms.assetid: b55923b7-d60a-460d-b77c-af5fac67f1cc
ms.devlang: java
ms.topic: article
ms.service: Azure
ms.technology: Azure
ms.date: 3/30/2017
ms.author: routlaw;asirveda
ms.openlocfilehash: ebc9657f9f148b89d9a3178547c50d5b7bbc86e0
ms.sourcegitcommit: 115f4c8ad07a11f17d79e9d945d63917836b11c8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "61593230"
---
# <a name="manage-azure-virtual-machine-scale-sets-from-your-java-applications"></a><span data-ttu-id="f9bd9-103">Administración de conjuntos de escalado de máquinas virtuales de Azure desde aplicaciones Java</span><span class="sxs-lookup"><span data-stu-id="f9bd9-103">Manage Azure virtual machine scale sets from your Java applications</span></span>

<span data-ttu-id="f9bd9-104">[Este ejemplo](https://github.com/Azure-Samples/compute-java-manage-virtual-machine-scale-sets) crea un [conjunto de escalado de máquinas virtuales](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-overview) mediante las [bibliotecas de administración de Java](https://github.com/Azure/azure-sdk-for-java).</span><span class="sxs-lookup"><span data-stu-id="f9bd9-104">[This sample](https://github.com/Azure-Samples/compute-java-manage-virtual-machine-scale-sets) creates a  [virtual machine scale set](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-overview) using the [Java management libraries](https://github.com/Azure/azure-sdk-for-java).</span></span> 

## <a name="run-the-sample"></a><span data-ttu-id="f9bd9-105">Ejecución del ejemplo</span><span class="sxs-lookup"><span data-stu-id="f9bd9-105">Run the sample</span></span>

<span data-ttu-id="f9bd9-106">Cree un [archivo de autenticación](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) y establezca una variable de entorno `AZURE_AUTH_LOCATION` con la ruta de acceso completa al archivo en el equipo.</span><span class="sxs-lookup"><span data-stu-id="f9bd9-106">Create an [authentication file](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) and set an environment variable `AZURE_AUTH_LOCATION` with the full path to the file on your computer.</span></span> <span data-ttu-id="f9bd9-107">A continuación, ejecute:</span><span class="sxs-lookup"><span data-stu-id="f9bd9-107">Then run:</span></span>

```
git clone https://github.com/Azure-Samples/compute-java-manage-virtual-machine-scale-sets.git
cd compute-java-manage-virtual-machine-scale-sets
mvn clean compile exec:java
```

<span data-ttu-id="f9bd9-108">Vea el [código completo del ejemplo en GitHub](https://github.com/Azure-Samples/compute-java-manage-virtual-machine-scale-sets/blob/master/src/main/java/com/microsoft/azure/management/compute/samples/ManageVirtualMachineScaleSet.java).</span><span class="sxs-lookup"><span data-stu-id="f9bd9-108">View the [complete code sample on GitHub](https://github.com/Azure-Samples/compute-java-manage-virtual-machine-scale-sets/blob/master/src/main/java/com/microsoft/azure/management/compute/samples/ManageVirtualMachineScaleSet.java).</span></span>

## <a name="authenticate-with-azure"></a><span data-ttu-id="f9bd9-109">Autenticación con Azure</span><span class="sxs-lookup"><span data-stu-id="f9bd9-109">Authenticate with Azure</span></span>

[!INCLUDE [auth-include](includes/java-auth-include.md)]

## <a name="create-a-virtual-network-for-the-scale-set"></a><span data-ttu-id="f9bd9-110">Creación de una red virtual para el conjunto de escalado</span><span class="sxs-lookup"><span data-stu-id="f9bd9-110">Create a virtual network for the scale set</span></span>

```java
Network network = azure.networks().define(vnetName)
                    .withRegion(region)
                    .withNewResourceGroup(rgName)
                    .withAddressSpace("172.16.0.0/16")
                    .defineSubnet("Front-end")
                    .withAddressPrefix("172.16.1.0/24")
                    .attach()
                    .create();
```

<span data-ttu-id="f9bd9-111">Configure una red virtual y un equilibrador de carga antes de crear la definición del conjunto de escalado.</span><span class="sxs-lookup"><span data-stu-id="f9bd9-111">Set up a virtual network and load balancer before creating the scale set definition.</span></span> <span data-ttu-id="f9bd9-112">El conjunto de escalado utiliza estos recursos para su configuración inicial.</span><span class="sxs-lookup"><span data-stu-id="f9bd9-112">The scale set uses these resources for its initial configuration.</span></span>

## <a name="create-a-load-balancer-to-distribute-load-across-the-scale-set"></a><span data-ttu-id="f9bd9-113">Creación de un equilibrador de carga para distribuir la carga en todo el conjunto de escalado</span><span class="sxs-lookup"><span data-stu-id="f9bd9-113">Create a load balancer to distribute load across the scale set</span></span>

```java
LoadBalancer loadBalancer1 = azure.loadBalancers().define(loadBalancerName1)
                    .withRegion(region)
                    .withExistingResourceGroup(rgName)
                    // assign a public IP address to the load balancer
                    .definePublicFrontend(frontendName)
                        .withExistingPublicIPAddress(publicIPAddress)
                        .attach()
                    // Add two backend address pools
                    .defineBackend(backendPoolName1)
                        .attach()
                    .defineBackend(backendPoolName2)
                        .attach()
                    // Add two health probes on 80 and 443
                    .defineHttpProbe(httpProbe)
                        .withRequestPath("/")
                        .withPort(80)
                        .attach()
                    .defineHttpProbe(httpsProbe)
                        .withRequestPath("/")
                        .withPort(443)
                        .attach()

                    // balance HTTP and HTTPs traffic
                    .defineLoadBalancingRule(httpLoadBalancingRule)
                        .withProtocol(TransportProtocol.TCP)
                        .withFrontend(frontendName)
                        .withFrontendPort(80)
                        .withProbe(httpProbe)
                        .withBackend(backendPoolName1)
                        .attach()
                    .defineLoadBalancingRule(httpsLoadBalancingRule)
                        .withProtocol(TransportProtocol.TCP)
                        .withFrontend(frontendName)
                        .withFrontendPort(443)
                        .withProbe(httpsProbe)
                        .withBackend(backendPoolName2)
                        .attach()

                    // Add NAT definitions to enable SSH and telnet to the VMs 
                    .defineInboundNatPool(natPool50XXto22)
                        .withProtocol(TransportProtocol.TCP)
                        .withFrontend(frontendName)
                        .withFrontendPortRange(5000, 5099)
                        .withBackendPort(22)
                        .attach()
                    .defineInboundNatPool(natPool60XXto23)
                        .withProtocol(TransportProtocol.TCP)
                        .withFrontend(frontendName)
                        .withFrontendPortRange(6000, 6099)
                        .withBackendPort(23)
                        .attach()
                    .create();
```

 <span data-ttu-id="f9bd9-114">El equilibrador de carga define dos grupos de direcciones de red de back-end: uno para equilibrar la carga a través de HTTP (`backendPoolName1`) y el otro para equilibrar la carga a través de HTTPS (`backendPoolName2`).</span><span class="sxs-lookup"><span data-stu-id="f9bd9-114">The load balancer defines two backend network address pools-one to balance load across HTTP (`backendPoolName1`) and the other to balance load across HTTPS (`backendPoolName2`).</span></span>  <span data-ttu-id="f9bd9-115">Los métodos `defineHttpProbe()` configuran [puntos de conexión de sondeo de mantenimiento](https://docs.microsoft.com/azure/load-balancer/load-balancer-custom-probe-overview) en los equilibradores de carga.</span><span class="sxs-lookup"><span data-stu-id="f9bd9-115">The `defineHttpProbe()` methods set up [health probe endpoints](https://docs.microsoft.com/azure/load-balancer/load-balancer-custom-probe-overview) on the load balancers.</span></span> <span data-ttu-id="f9bd9-116">Las reglas NAT exponen los puertos 22 y 23 de las máquinas virtuales del conjunto de escalado para acceso telnet y SSH.</span><span class="sxs-lookup"><span data-stu-id="f9bd9-116">NAT rules expose ports 22 and 23 on the scale set virtual machines for telnet and SSH access.</span></span>

## <a name="create-a-scale-set"></a><span data-ttu-id="f9bd9-117">Creación de un conjunto de escalado</span><span class="sxs-lookup"><span data-stu-id="f9bd9-117">Create a scale set</span></span>
 
```java
 // Create a virtual machine scale set with three virtual machines
 // And, install Apache Web servers on them
VirtualMachineScaleSet virtualMachineScaleSet = azure.virtualMachineScaleSets()
       .define(vmssName)
                .withRegion(region)
                .withExistingResourceGroup(rgName)
                .withSku(VirtualMachineScaleSetSkuTypes.STANDARD_D3_V2)
                .withExistingPrimaryNetworkSubnet(network, "Front-end")
                .withExistingPrimaryInternetFacingLoadBalancer(loadBalancer1)
                .withPrimaryInternetFacingLoadBalancerBackends(backendPoolName1, backendPoolName2)
                .withPrimaryInternetFacingLoadBalancerInboundNatPools(natPool50XXto22, natPool60XXto23)
                .withoutPrimaryInternalLoadBalancer()
                .withPopularLinuxImage(KnownLinuxVirtualMachineImage.UBUNTU_SERVER_16_04_LTS)
                .withRootUsername(userName)
                .withSsh(sshKey)
                .withNewDataDisk(100)
                .withNewDataDisk(100, 1, CachingTypes.READ_WRITE)
                .withNewDataDisk(100, 2, 
                     CachingTypes.READ_WRITE, StorageAccountTypes.STANDARD_LRS)
                .withCapacity(3)
                // Use a VM extension to install Apache Web servers
                .defineNewExtension("CustomScriptForLinux")
                    .withPublisher("Microsoft.OSTCExtensions")
                    .withType("CustomScriptForLinux")
                    .withVersion("1.4")
                    .withMinorVersionAutoUpgrade()
                    .withPublicSetting("fileUris", fileUris)
                    .withPublicSetting("commandToExecute", installCommand)
                    .attach()
                .create();
```

<span data-ttu-id="f9bd9-118">Use la definición de red virtual y la definición de equilibrador de carga creadas en el paso anterior para crear un conjunto de escalado con tres instancias de Linux (`withCapacity(3)`) y tres discos de datos de 100 GB cada uno.</span><span class="sxs-lookup"><span data-stu-id="f9bd9-118">Use the virtual network definition and load balancer definitions created in the previous step to create a scale set with three Linux instances (`withCapacity(3)`) and three 100GB data disks each.</span></span> <span data-ttu-id="f9bd9-119">La cadena del método `defineNewExtension()` instala el servidor web Apache en cada máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f9bd9-119">The `defineNewExtension()` method chain installs the Apache web server on each VM.</span></span>

## <a name="list-virtual-machine-scale-set-network-interfaces"></a><span data-ttu-id="f9bd9-120">Enumeración de las interfaces de red del conjunto de escalado de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="f9bd9-120">List virtual machine scale set network interfaces</span></span>

```java
// List network interfaces on the scale set and iterate through them
PagedList<VirtualMachineScaleSetNetworkInterface> vmssNics = 
     virtualMachineScaleSet.listNetworkInterfaces();
for (VirtualMachineScaleSetNetworkInterface vmssNic : vmssNics) {
    System.out.println(vmssNic.id());
}
```

## <a name="get-ssh-connection-strings-for-each-scale-set-virtual-machine"></a><span data-ttu-id="f9bd9-121">Obtención de las cadenas de conexión SSH para cada máquina virtual del conjunto de escalado</span><span class="sxs-lookup"><span data-stu-id="f9bd9-121">Get SSH connection strings for each scale set virtual machine</span></span>

```java
for (VirtualMachineScaleSetVM instance : virtualMachineScaleSet.virtualMachines().list()) {
    System.out.println("Scale set virtual machine instance #" + instance.instanceId());
    System.out.println(instance.id());
    PagedList<VirtualMachineScaleSetNetworkInterface> networkInterfaces = 
         instance.listNetworkInterfaces();
    // Pick the first NIC on the instance and use its primary IP address
    VirtualMachineScaleSetNetworkInterface networkInterface = networkInterfaces.get(0);
    for (VirtualMachineScaleSetNicIPConfiguration ipConfig : networkInterface.ipConfigurations().values()) {
        if (ipConfig.isPrimary()) {
            List<LoadBalancerInboundNatRule> natRules = ipConfig.listAssociatedLoadBalancerInboundNatRules();
            for (LoadBalancerInboundNatRule natRule : natRules) {
                // find rule matching the inbound SSH port on the backend for the IP address
                // and return the SSH connection string to that port on the load balancer
                if (natRule.backendPort() == 22) {
                    System.out.println("SSH connection string: " + userName + 
                        "@" + publicIPAddress.fqdn() + ":" + natRule.frontendPort());
                break;
                }
            }
            break;
        }
    }
}
```

<span data-ttu-id="f9bd9-122">El grupo NAT que creó anteriormente asigna los puertos SSH y telnet (22 y 23, respectivamente) de las máquinas virtuales a puertos del equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="f9bd9-122">The NAT pool created earlier mapped the SSH and telnet ports (22 and 23, respectively) on the virtual machines to ports on the load balancer.</span></span> <span data-ttu-id="f9bd9-123">Este código crea la cadena de conexión de SSH para cada máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f9bd9-123">This code builds the SSH connection string for each virtual machine.</span></span>

## <a name="stop-the-virtual-machine-scale-set"></a><span data-ttu-id="f9bd9-124">Detención del conjunto de escalado de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="f9bd9-124">Stop the virtual machine scale set</span></span>

```java
// stop (not deallocate) all scale set instances
virtualMachineScaleSet.powerOff();
```

<span data-ttu-id="f9bd9-125">Las máquinas virtuales detenidas siguen consumiendo recursos reservados.</span><span class="sxs-lookup"><span data-stu-id="f9bd9-125">Stopped virtual machines continue to consume reserved resources.</span></span> <span data-ttu-id="f9bd9-126">Use `deallocate()` para detener el sistema operativo en las máquinas virtuales y liberar sus recursos de proceso.</span><span class="sxs-lookup"><span data-stu-id="f9bd9-126">Use `deallocate()` to stop the operating system on the virtual machines and release their compute resources.</span></span>

## <a name="deallocate-the-virtual-machine-scale-set"></a><span data-ttu-id="f9bd9-127">Desasignación del conjunto de escalado de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="f9bd9-127">Deallocate the virtual machine scale set</span></span>

```java
// deallocate the virtual machine scale set
virtualMachineScaleSet.deallocate();
```

<span data-ttu-id="f9bd9-128">Deallocate() apaga el sistema operativo en las máquinas virtuales y libera los recursos de proceso y red (por ejemplo, direcciones IP) usados por las instancias del conjunto de escalado.</span><span class="sxs-lookup"><span data-stu-id="f9bd9-128">Deallocate() shuts down the operating system on the virtual machines and frees up the compute and network resources (such as IP addresses) used by the scale set instances.</span></span> <span data-ttu-id="f9bd9-129">Seguirá acumulando cargos de almacenamiento por los discos (incluido el sistema operativo) conectados a las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="f9bd9-129">You continue to accrue storage charges for any disks (including the OS) attached to the virtual machines.</span></span>

## <a name="start-a-virtual-machine-scale-set"></a><span data-ttu-id="f9bd9-130">Inicio de un conjunto de escalado de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="f9bd9-130">Start a virtual machine scale set</span></span>

```java
// start a deallocated or stopped virtual machine scale set
virtualMachineScaleSet.start();
```

## <a name="update-the-number-of-virtual-machines-instances-in-the-scale-set"></a><span data-ttu-id="f9bd9-131">Actualización del número de instancias de máquinas virtuales en el conjunto de escalado</span><span class="sxs-lookup"><span data-stu-id="f9bd9-131">Update the number of virtual machines instances in the scale set</span></span>
```java
// increase the number of virtual machine scale set instances from three to six
virtualMachineScaleSet.update()
                    .withCapacity(6)
                    .apply();
```

<span data-ttu-id="f9bd9-132">Escale el número de máquinas virtuales en el conjunto de escalado mediante `withCapacity()` y escale la capacidad de cada máquina virtual con `withSku()`.</span><span class="sxs-lookup"><span data-stu-id="f9bd9-132">Scale the number of virtual machines in the scale set using `withCapacity()` and scale the capacity of each virtual machine using `withSku()`.</span></span>

## <a name="sample-explanation"></a><span data-ttu-id="f9bd9-133">Explicación del ejemplo</span><span class="sxs-lookup"><span data-stu-id="f9bd9-133">Sample explanation</span></span>

<span data-ttu-id="f9bd9-134">[El código de ejemplo](https://github.com/Azure-Samples/compute-java-manage-virtual-machine-scale-sets/blob/master/src/main/java/com/microsoft/azure/management/compute/samples/ManageVirtualMachineScaleSet.java) crea primero una red virtual para la comunicación del conjunto de escalado y un equilibrador de carga para distribuir el tráfico entre las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="f9bd9-134">[The sample code](https://github.com/Azure-Samples/compute-java-manage-virtual-machine-scale-sets/blob/master/src/main/java/com/microsoft/azure/management/compute/samples/ManageVirtualMachineScaleSet.java) first creates a virtual network for the scale set to communicate across and a load balancer to distribute traffic across the virtual machines.</span></span> <span data-ttu-id="f9bd9-135">La cadena del método `azure.virtualMachineScaleSets().define()...create()` crea el conjunto de escalado con tres instancias de Linux que ejecutan el servidor web Apache.</span><span class="sxs-lookup"><span data-stu-id="f9bd9-135">The `azure.virtualMachineScaleSets().define()...create()` method chain creates the scale set with three Linux instances running the Apache web server.</span></span>    
   
| <span data-ttu-id="f9bd9-136">Clase utilizada en el ejemplo</span><span class="sxs-lookup"><span data-stu-id="f9bd9-136">Class used in sample</span></span> | <span data-ttu-id="f9bd9-137">Notas</span><span class="sxs-lookup"><span data-stu-id="f9bd9-137">Notes</span></span>
|-------|-------|
| [<span data-ttu-id="f9bd9-138">VirtualMachineScaleSet</span><span class="sxs-lookup"><span data-stu-id="f9bd9-138">VirtualMachineScaleSet</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._virtual_machine_scale_set) | <span data-ttu-id="f9bd9-139">Consultar, iniciar, detener, actualizar y eliminar todas las máquinas virtuales en el conjunto de escalado.</span><span class="sxs-lookup"><span data-stu-id="f9bd9-139">Query, start, stop, update and delete all virtual machines in the scale set.</span></span>
| [<span data-ttu-id="f9bd9-140">VirtualMachineScaleSetVM</span><span class="sxs-lookup"><span data-stu-id="f9bd9-140">VirtualMachineScaleSetVM</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._virtual_machine_scale_set_v_m) | <span data-ttu-id="f9bd9-141">Recuperado de `virtualMachineScaleSet.virtualMachines().get()` o `list()`, le permite consultar, iniciar, detener, configurar y eliminar máquinas virtuales en el conjunto de escalado.</span><span class="sxs-lookup"><span data-stu-id="f9bd9-141">Retrieved from `virtualMachineScaleSet.virtualMachines().get()` or `list()`, allows you to query, start, stop, configure and delete virtual machines in the scale set.</span></span>
| [<span data-ttu-id="f9bd9-142">VirtualMachineScaleSetNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="f9bd9-142">VirtualMachineScaleSetNetworkInterface</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.network._virtual_machine_scale_set_network_interface) | <span data-ttu-id="f9bd9-143">Devuelto desde `virtualMachineScaleSet.listNetworkInterfaces()`, es una representación de solo lectura de una interfaz de red en una máquina virtual en un conjunto de escalado.</span><span class="sxs-lookup"><span data-stu-id="f9bd9-143">Returned from `virtualMachineScaleSet.listNetworkInterfaces()`, read-only representation of a network interface on a virtual machine in a scale set.</span></span>
| [<span data-ttu-id="f9bd9-144">VirtualMachineScaleSetSkuTypes</span><span class="sxs-lookup"><span data-stu-id="f9bd9-144">VirtualMachineScaleSetSkuTypes</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._virtual_machine_scale_set_sku_types) | <span data-ttu-id="f9bd9-145">Clase de campos estáticos usados para establecer el [nivel del conjunto de escalado de máquinas virtuales](https://azure.microsoft.com/pricing/details/virtual-machine-scale-sets/linux/) que se utiliza para definir cuántos recursos pueden consumir los miembros del conjunto de escalado.</span><span class="sxs-lookup"><span data-stu-id="f9bd9-145">Class of static fields used to set the [virtual machine scale set tier](https://azure.microsoft.com/pricing/details/virtual-machine-scale-sets/linux/) used to define how much resources scale set members can consume.</span></span>
| [<span data-ttu-id="f9bd9-146">VirtualMachineScaleSetNicIpConfiguration</span><span class="sxs-lookup"><span data-stu-id="f9bd9-146">VirtualMachineScaleSetNicIpConfiguration</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.network._virtual_machine_scale_set_nic_i_p_configuration) | <span data-ttu-id="f9bd9-147">Se usa para consultar la configuración de IP asociada con una interfaz de red en una máquina virtual del conjunto de escalado.</span><span class="sxs-lookup"><span data-stu-id="f9bd9-147">Used to query the IP configuration associated with a network interface on a scale set virtual machine.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f9bd9-148">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f9bd9-148">Next steps</span></span>

[!INCLUDE [next-steps](includes/java-next-steps.md)]