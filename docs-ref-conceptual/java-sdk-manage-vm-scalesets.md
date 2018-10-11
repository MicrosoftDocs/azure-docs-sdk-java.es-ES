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
ms.openlocfilehash: 4653726b387369c18942b6c11392f15b9f0351f3
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/09/2018
ms.locfileid: "48893496"
---
# <a name="manage-azure-virtual-machine-scale-sets-from-your-java-applications"></a>Administración de conjuntos de escalado de máquinas virtuales de Azure desde aplicaciones Java

[Este ejemplo](https://github.com/Azure-Samples/compute-java-manage-virtual-machine-scale-sets) crea un [conjunto de escalado de máquinas virtuales](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-overview) mediante las [bibliotecas de administración de Java](https://github.com/Azure/azure-sdk-for-java). 

## <a name="run-the-sample"></a>Ejecución del ejemplo

Cree un [archivo de autenticación](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) y establezca una variable de entorno `AZURE_AUTH_LOCATION` con la ruta de acceso completa al archivo en el equipo. A continuación, ejecute:

```
git clone https://github.com/Azure-Samples/compute-java-manage-virtual-machine-scale-sets.git
cd compute-java-manage-virtual-machine-scale-sets
mvn clean compile exec:java
```

Vea el [código completo del ejemplo en GitHub](https://github.com/Azure-Samples/compute-java-manage-virtual-machine-scale-sets/blob/master/src/main/java/com/microsoft/azure/management/compute/samples/ManageVirtualMachineScaleSet.java).

## <a name="authenticate-with-azure"></a>Autenticación con Azure

[!INCLUDE [auth-include](includes/java-auth-include.md)]

## <a name="create-a-virtual-network-for-the-scale-set"></a>Creación de una red virtual para el conjunto de escalado

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

Configure una red virtual y un equilibrador de carga antes de crear la definición del conjunto de escalado. El conjunto de escalado utiliza estos recursos para su configuración inicial.

## <a name="create-a-load-balancer-to-distribute-load-across-the-scale-set"></a>Creación de un equilibrador de carga para distribuir la carga en todo el conjunto de escalado

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

 El equilibrador de carga define dos grupos de direcciones de red de back-end: uno para equilibrar la carga a través de HTTP (`backendPoolName1`) y el otro para equilibrar la carga a través de HTTPS (`backendPoolName2`).  Los métodos `defineHttpProbe()` configuran [puntos de conexión de sondeo de mantenimiento](https://docs.microsoft.com/azure/load-balancer/load-balancer-custom-probe-overview) en los equilibradores de carga. Las reglas NAT exponen los puertos 22 y 23 de las máquinas virtuales del conjunto de escalado para acceso telnet y SSH.

## <a name="create-a-scale-set"></a>Creación de un conjunto de escalado
 
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

Use la definición de red virtual y la definición de equilibrador de carga creadas en el paso anterior para crear un conjunto de escalado con tres instancias de Linux (`withCapacity(3)`) y tres discos de datos de 100 GB cada uno. La cadena del método `defineNewExtension()` instala el servidor web Apache en cada máquina virtual.

## <a name="list-virtual-machine-scale-set-network-interfaces"></a>Enumeración de las interfaces de red del conjunto de escalado de máquinas virtuales

```java
// List network interfaces on the scale set and iterate through them
PagedList<VirtualMachineScaleSetNetworkInterface> vmssNics = 
     virtualMachineScaleSet.listNetworkInterfaces();
for (VirtualMachineScaleSetNetworkInterface vmssNic : vmssNics) {
    System.out.println(vmssNic.id());
}
```

## <a name="get-ssh-connection-strings-for-each-scale-set-virtual-machine"></a>Obtención de las cadenas de conexión SSH para cada máquina virtual del conjunto de escalado

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

El grupo NAT que creó anteriormente asigna los puertos SSH y telnet (22 y 23, respectivamente) de las máquinas virtuales a puertos del equilibrador de carga. Este código crea la cadena de conexión de SSH para cada máquina virtual.

## <a name="stop-the-virtual-machine-scale-set"></a>Detención del conjunto de escalado de máquinas virtuales

```java
// stop (not deallocate) all scale set instances
virtualMachineScaleSet.powerOff();
```

Las máquinas virtuales detenidas siguen consumiendo recursos reservados. Use `deallocate()` para detener el sistema operativo en las máquinas virtuales y liberar sus recursos de proceso.

## <a name="deallocate-the-virtual-machine-scale-set"></a>Desasignación del conjunto de escalado de máquinas virtuales

```java
// deallocate the virtual machine scale set
virtualMachineScaleSet.deallocate();
```

Deallocate() apaga el sistema operativo en las máquinas virtuales y libera los recursos de proceso y red (por ejemplo, direcciones IP) usados por las instancias del conjunto de escalado. Seguirá acumulando cargos de almacenamiento por los discos (incluido el sistema operativo) conectados a las máquinas virtuales.

## <a name="start-a-virtual-machine-scale-set"></a>Inicio de un conjunto de escalado de máquinas virtuales

```java
// start a deallocated or stopped virtual machine scale set
virtualMachineScaleSet.start();
```

## <a name="update-the-number-of-virtual-machines-instances-in-the-scale-set"></a>Actualización del número de instancias de máquinas virtuales en el conjunto de escalado
```java
// increase the number of virtual machine scale set instances from three to six
virtualMachineScaleSet.update()
                    .withCapacity(6)
                    .apply();
```

Escale el número de máquinas virtuales en el conjunto de escalado mediante `withCapacity()` y escale la capacidad de cada máquina virtual con `withSku()`.

## <a name="sample-explanation"></a>Explicación del ejemplo

[El código de ejemplo](https://github.com/Azure-Samples/compute-java-manage-virtual-machine-scale-sets/blob/master/src/main/java/com/microsoft/azure/management/compute/samples/ManageVirtualMachineScaleSet.java) crea primero una red virtual para la comunicación del conjunto de escalado y un equilibrador de carga para distribuir el tráfico entre las máquinas virtuales. La cadena del método `azure.virtualMachineScaleSets().define()...create()` crea el conjunto de escalado con tres instancias de Linux que ejecutan el servidor web Apache.    
   
| Clase utilizada en el ejemplo | Notas
|-------|-------|
| [VirtualMachineScaleSet](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._virtual_machine_scale_set) | Consultar, iniciar, detener, actualizar y eliminar todas las máquinas virtuales en el conjunto de escalado.
| [VirtualMachineScaleSetVM](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._virtual_machine_scale_set_v_m) | Recuperado de `virtualMachineScaleSet.virtualMachines().get()` o `list()`, le permite consultar, iniciar, detener, configurar y eliminar máquinas virtuales en el conjunto de escalado.
| [VirtualMachineScaleSetNetworkInterface](https://docs.microsoft.com/java/api/com.microsoft.azure.management.network._virtual_machine_scale_set_network_interface) | Devuelto desde `virtualMachineScaleSet.listNetworkInterfaces()`, es una representación de solo lectura de una interfaz de red en una máquina virtual en un conjunto de escalado.
| [VirtualMachineScaleSetSkuTypes](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._virtual_machine_scale_set_sku_types) | Clase de campos estáticos usados para establecer el [nivel del conjunto de escalado de máquinas virtuales](https://azure.microsoft.com/pricing/details/virtual-machine-scale-sets/linux/) que se utiliza para definir cuántos recursos pueden consumir los miembros del conjunto de escalado.
| [VirtualMachineScaleSetNicIpConfiguration](https://docs.microsoft.com/java/api/com.microsoft.azure.management.network._virtual_machine_scale_set_nic_i_p_configuration) | Se usa para consultar la configuración de IP asociada con una interfaz de red en una máquina virtual del conjunto de escalado.

## <a name="next-steps"></a>Pasos siguientes

[!INCLUDE [next-steps](includes/java-next-steps.md)]