---
title: Administración de redes virtuales de Azure con Java | Microsoft Docs
description: Código de ejemplo para administrar redes virtuales de Azure desde el código de Java
author: rloutlaw
manager: douge
ms.assetid: 92736911-3df6-46e7-b751-25bb36bf89b9
ms.devlang: java
ms.topic: article
ms.service: Azure
ms.technology: Azure
ms.date: 3/30/2017
ms.author: routlaw;asirveda
ms.openlocfilehash: 3d21cdd890912c1fc58fc65a79ba972b8327edeb
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/09/2018
ms.locfileid: "48892546"
---
# <a name="create-and-manage-azure-virtual-networks-from-your-java-apps"></a><span data-ttu-id="e5d46-103">Creación y administración de redes virtuales de Azure desde las aplicaciones Java</span><span class="sxs-lookup"><span data-stu-id="e5d46-103">Create and manage Azure virtual networks from your Java apps</span></span>

<span data-ttu-id="e5d46-104">[Este ejemplo](https://github.com/Azure-Samples/network-java-manage-virtual-network) crea una [red virtual](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) para aislar los recursos de Azure en un segmento de red que puede controlar.</span><span class="sxs-lookup"><span data-stu-id="e5d46-104">[This sample](https://github.com/Azure-Samples/network-java-manage-virtual-network) creates a [virtual network](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) to isolate your Azure resources on network segment you control.</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="e5d46-105">Ejecución del ejemplo</span><span class="sxs-lookup"><span data-stu-id="e5d46-105">Run the sample</span></span>

<span data-ttu-id="e5d46-106">Cree un [archivo de autenticación](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) y establezca una variable de entorno `AZURE_AUTH_LOCATION` con la ruta de acceso completa al archivo en el equipo.</span><span class="sxs-lookup"><span data-stu-id="e5d46-106">Create an [authentication file](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) and set an environment variable `AZURE_AUTH_LOCATION` with the full path to the file on your computer.</span></span> <span data-ttu-id="e5d46-107">A continuación, ejecute:</span><span class="sxs-lookup"><span data-stu-id="e5d46-107">Then run:</span></span>

```
git clone https://github.com/Azure-Samples/network-java-manage-virtual-network.git
cd network-java-manage-virtual-network
mvn clean compile exec:java
```

<span data-ttu-id="e5d46-108">Vea el [código completo del ejemplo en GitHub](https://github.com/Azure-Samples/network-java-manage-virtual-network/blob/master/src/main/java/com/microsoft/azure/management/network/samples/ManageVirtualNetwork.java).</span><span class="sxs-lookup"><span data-stu-id="e5d46-108">View the [complete code sample on GitHub](https://github.com/Azure-Samples/network-java-manage-virtual-network/blob/master/src/main/java/com/microsoft/azure/management/network/samples/ManageVirtualNetwork.java).</span></span>

## <a name="authenticate-with-azure"></a><span data-ttu-id="e5d46-109">Autenticación con Azure</span><span class="sxs-lookup"><span data-stu-id="e5d46-109">Authenticate with Azure</span></span>

[!INCLUDE [auth-include](includes/java-auth-include.md)]

## <a name="create-a-network-security-group-to-block-internet-traffic"></a><span data-ttu-id="e5d46-110">Creación de un grupo de seguridad de red para bloquear el tráfico de Internet</span><span class="sxs-lookup"><span data-stu-id="e5d46-110">Create a network security group to block Internet traffic</span></span>

```java
// this NSG definition block traffic to and from the public Internet
NetworkSecurityGroup backEndSubnetNsg = azure.networkSecurityGroups()
              .define(vnet1BackEndSubnetNsgName)
                    .withRegion(Region.US_EAST)
                    .withNewResourceGroup(rgName)
                    .defineRule("DenyInternetInComing")
                        .denyInbound()
                        .fromAddress("INTERNET")
                        .fromAnyPort()
                        .toAnyAddress()
                        .toAnyPort()
                        .withAnyProtocol()
                        .attach()
                    .defineRule("DenyInternetOutGoing")
                        .denyOutbound()
                        .fromAnyAddress()
                        .fromAnyPort()
                        .toAddress("INTERNET")
                        .toAnyPort()
                        .withAnyProtocol()
                        .attach()
                    .create();
```

<span data-ttu-id="e5d46-111">Esta [regla de seguridad de red](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg) bloquea el tráfico de Internet público entrante y saliente.</span><span class="sxs-lookup"><span data-stu-id="e5d46-111">This [network security rule](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg) blocks both inbound and outbound public Internet traffic.</span></span> <span data-ttu-id="e5d46-112">Este grupo de seguridad de red no tiene efecto hasta que se aplica a una subred de la red virtual.</span><span class="sxs-lookup"><span data-stu-id="e5d46-112">This network security group will not have an effect until applied to a subnet in your virtual network.</span></span>

## <a name="create-a-virtual-network-with-two-subnets"></a><span data-ttu-id="e5d46-113">Creación de una red virtual con dos subredes</span><span class="sxs-lookup"><span data-stu-id="e5d46-113">Create a virtual network with two subnets</span></span>

```java
// create the a virtual network with two subnets
// assign the backend subnet a rule blocking public internet traffic
Network virtualNetwork1 = azure.networks().define(vnetName1)
                    .withRegion(Region.US_EAST)
                    .withExistingResourceGroup(rgName)
                    .withAddressSpace("192.168.0.0/16")
                    .withSubnet(vnet1FrontEndSubnetName, "192.168.1.0/24")
                    .defineSubnet(vnet1BackEndSubnetName)
                        .withAddressPrefix("192.168.2.0/24")
                        .withExistingNetworkSecurityGroup(backEndSubnetNsg)
                        .attach()
                    .create();
```

<span data-ttu-id="e5d46-114">La subred de back-end deniega el acceso a Internet según las reglas definidas en el grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="e5d46-114">The backend subnet denies Internet access usingfollowing the rules set in the network security group.</span></span> <span data-ttu-id="e5d46-115">La subred de front-end utiliza las [reglas predeterminadas](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg) que permiten el tráfico saliente a Internet.</span><span class="sxs-lookup"><span data-stu-id="e5d46-115">The front end subnet uses the [default rules](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg) which allow outbound traffic to the Internet.</span></span>

## <a name="create-a-network-security-group-to-allow-inbound-http-traffic"></a><span data-ttu-id="e5d46-116">Creación de un grupo de seguridad de red para permitir el tráfico HTTP entrante</span><span class="sxs-lookup"><span data-stu-id="e5d46-116">Create a network security group to allow inbound HTTP traffic</span></span>
```java
// create a rule that allows inbound HTTP and blocks outbound Internet traffic
NetworkSecurityGroup frontEndSubnetNsg = azure.networkSecurityGroups()
               .define(vnet1FrontEndSubnetNsgName)
                    .withRegion(Region.US_EAST)
                    .withExistingResourceGroup(rgName)
                    .defineRule("AllowHttpInComing")
                        .allowInbound()
                        .fromAddress("INTERNET")
                        .fromAnyPort()
                        .toAnyAddress()
                        .toPort(80)
                        .withProtocol(SecurityRuleProtocol.TCP)
                        .attach()
                    .defineRule("DenyInternetOutGoing")
                        .denyOutbound()
                        .fromAnyAddress()
                        .fromAnyPort()
                        .toAddress("INTERNET")
                        .toAnyPort()
                        .withAnyProtocol()
                        .attach()
                    .create();
```

<span data-ttu-id="e5d46-117">Esta regla de seguridad de red abre el tráfico entrante en el puerto 80 desde la red Internet pública y bloquea todo el tráfico saliente desde dentro de la red a la red Internet pública.</span><span class="sxs-lookup"><span data-stu-id="e5d46-117">This network security rule opens up inbound traffic on port 80 from the public Internet, and blocks all outbound traffic from inside the network to the public Internet.</span></span> 

## <a name="update-a-virtual-network"></a><span data-ttu-id="e5d46-118">Actualización de una red virtual</span><span class="sxs-lookup"><span data-stu-id="e5d46-118">Update a virtual network</span></span>
```java
// update the front end subnet to use the rules in the new network security group
virtualNetwork1.update()
          .updateSubnet(vnet1FrontEndSubnetName)
          .withExistingNetworkSecurityGroup(frontEndSubnetNsg)
          .parent()
          .apply();
```

<span data-ttu-id="e5d46-119">Actualice la subred de front-end para permitir el tráfico HTTP entrante con la regla de seguridad de red creada en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="e5d46-119">Update the front end subnet to allow inbound HTTP traffic using the network security rule created in the previous step.</span></span>

## <a name="create-a-virtual-machine-on-a-subnet"></a><span data-ttu-id="e5d46-120">Creación de una máquina virtual en una subred</span><span class="sxs-lookup"><span data-stu-id="e5d46-120">Create a virtual machine on a subnet</span></span>
```java
// attach the new VM to the front end subnet on the virtual network
VirtualMachine frontEndVM = azure.virtualMachines().define(frontEndVmName)
                    .withRegion(Region.US_EAST)
                    .withExistingResourceGroup(rgName)
                    .withExistingPrimaryNetwork(virtualNetwork1) 
                    .withSubnet(vnet1FrontEndSubnetName)
                    .withPrimaryPrivateIpAddressDynamic()
                    .withNewPrimaryPublicIpAddress(publicIpAddressLeafDnsForFrontEndVm)
                    .withPopularLinuxImage(KnownLinuxVirtualMachineImage.UBUNTU_SERVER_16_04_LTS)
                    .withRootUsername(userName)
                    .withSsh(sshKey)
                    .withSize(VirtualMachineSizeTypes.STANDARD_D3_V2)
                    .create();
```

<span data-ttu-id="e5d46-121">`withExistingPrimaryNetwork()` y `withSubnet()` configuran la máquina virtual para que utilice la subred de front-end en la red virtual que creó en los pasos anteriores.</span><span class="sxs-lookup"><span data-stu-id="e5d46-121">`withExistingPrimaryNetwork()` and `withSubnet()` configure the virtual machine to use the front-end subnet on the virtual network created in the previous steps.</span></span>

## <a name="list-virtual-networks-in-a-resource-group"></a><span data-ttu-id="e5d46-122">Enumeración de redes virtuales en un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="e5d46-122">List virtual networks in a resource group</span></span>
```java
// iterate over every virtual network in the resource group 
for (Network virtualNetwork : azure.networks().listByResourceGroup(rgName)) {
    // for each subnet on the virtual network, log the network address prefix 
    for (Map.Entry<String, Subnet> entry : virtualNetwork.subnets().entrySet()) {
        String subnetName = entry.getKey();
        Subnet subnet = entry.getValue();
        System.out.println("Address prefix for subnet " + subnetName + 
             " is " + subnet.addressPrefix());
    }
}
```       

<span data-ttu-id="e5d46-123">Puede enumerar e inspeccionar el objeto `Network` mediante la colección exterior o recorrer en iteración cada recurso secundario para cada red mediante el bucle for-each anidado, tal como se muestra en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="e5d46-123">You can list and inspect `Network` object using the outer collection or iterate through each child resource for each network using the nested for-each loop as seen in this example.</span></span>

## <a name="delete-a-virtual-network"></a><span data-ttu-id="e5d46-124">Eliminar una red virtual</span><span class="sxs-lookup"><span data-stu-id="e5d46-124">Delete a virtual network</span></span>
```java
// if you already have the virtual network object it is easiest to delete by ID
azure.networks().deleteById(virtualNetwork1.id());

// Delete by resource group and name if you don't have the VirtualMachine object
azure.networks().deleteByResourceGroup(rgName,vnetName1);
```

<span data-ttu-id="e5d46-125">La eliminación de una red virtual elimina las subredes de la red, pero no elimina las reglas del grupo de seguridad de red aplicadas a las subredes.</span><span class="sxs-lookup"><span data-stu-id="e5d46-125">Removing a virtual network deletes the subnets on the network but does not delete the network security group rules applied to the subnets.</span></span> <span data-ttu-id="e5d46-126">Esas definiciones se pueden volver a aplicar en otras subredes.</span><span class="sxs-lookup"><span data-stu-id="e5d46-126">Those definitions can be reapplied to other subnets.</span></span>

## <a name="sample-explanation"></a><span data-ttu-id="e5d46-127">Explicación del ejemplo</span><span class="sxs-lookup"><span data-stu-id="e5d46-127">Sample explanation</span></span>

<span data-ttu-id="e5d46-128">Este ejemplo crea una red virtual con dos subredes y con una máquina virtual en cada subred.</span><span class="sxs-lookup"><span data-stu-id="e5d46-128">This sample creates a virtual network with two subnets and with one virtual machine on each subnet.</span></span> <span data-ttu-id="e5d46-129">La subred de back-end está desconectada de la red Internet pública.</span><span class="sxs-lookup"><span data-stu-id="e5d46-129">The back subnet is cut off from the public Internet.</span></span> <span data-ttu-id="e5d46-130">La subred de front-end acepta el tráfico HTTP entrante desde Internet.</span><span class="sxs-lookup"><span data-stu-id="e5d46-130">The front-facing subnet accepts inbound HTTP traffic from the Internet.</span></span> <span data-ttu-id="e5d46-131">Ambas máquinas virtuales en la red virtual se comunican entre sí a través de las reglas del grupo de seguridad de red predeterminadas.</span><span class="sxs-lookup"><span data-stu-id="e5d46-131">Both virtual machines in the virtual network communicate with each other through the default network security group rules.</span></span>

| <span data-ttu-id="e5d46-132">Clase utilizada en el ejemplo</span><span class="sxs-lookup"><span data-stu-id="e5d46-132">Class used in sample</span></span> | <span data-ttu-id="e5d46-133">Notas</span><span class="sxs-lookup"><span data-stu-id="e5d46-133">Notes</span></span>
|-------|-------|
| [<span data-ttu-id="e5d46-134">Red</span><span class="sxs-lookup"><span data-stu-id="e5d46-134">Network</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.network._network) | <span data-ttu-id="e5d46-135">Representación en forma de objeto local de la red virtual creada a partir de `azure.networks().define()...create()`.</span><span class="sxs-lookup"><span data-stu-id="e5d46-135">Local object representation of the virtual network created from `azure.networks().define()...create()` .</span></span> <span data-ttu-id="e5d46-136">Use el encadenamiento `update()...apply()` para actualizar una red virtual existente.</span><span class="sxs-lookup"><span data-stu-id="e5d46-136">Use the `update()...apply()` fluent chain to update an existing virtual network.</span></span>
| [<span data-ttu-id="e5d46-137">Subred</span><span class="sxs-lookup"><span data-stu-id="e5d46-137">Subnet</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.network._subnet) | <span data-ttu-id="e5d46-138">Crear subredes en la red virtual al definir o actualizar la red mediante `withSubnet()`.</span><span class="sxs-lookup"><span data-stu-id="e5d46-138">Create subnets on the virtual network when defining or updating the network using `withSubnet()`.</span></span> <span data-ttu-id="e5d46-139">Obtener representaciones de objeto de una subred con `Network.subnets().get()` o `Network.subnets().entrySet()`.</span><span class="sxs-lookup"><span data-stu-id="e5d46-139">Get object representations of a subnet from `Network.subnets().get()` or `Network.subnets().entrySet()`.</span></span> <span data-ttu-id="e5d46-140">Estos objetos tienen métodos para consultar las propiedades de la subred.</span><span class="sxs-lookup"><span data-stu-id="e5d46-140">These objects have methods to query subnet properties.</span></span>
| [<span data-ttu-id="e5d46-141">NetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="e5d46-141">NetworkSecurityGroup</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.network._network_security_group) | <span data-ttu-id="e5d46-142">Se crea mediante el encadenamiento `azure.networkSecurityGroups().define()...create()` y se aplica a las subredes mediante la actualización o creación de subredes en una red virtual.</span><span class="sxs-lookup"><span data-stu-id="e5d46-142">Created using the `azure.networkSecurityGroups().define()...create()` fluent chain and then applied to subnets through the updating or creating subnets in a virtual network.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="e5d46-143">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e5d46-143">Next steps</span></span>

[!INCLUDE [next-steps](includes/java-next-steps.md)]