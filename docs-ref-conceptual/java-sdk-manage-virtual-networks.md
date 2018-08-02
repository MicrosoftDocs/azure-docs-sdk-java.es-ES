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
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/28/2017
ms.locfileid: "21931091"
---
# <a name="create-and-manage-azure-virtual-networks-from-your-java-apps"></a>Creación y administración de redes virtuales de Azure desde las aplicaciones Java

[Este ejemplo](https://github.com/Azure-Samples/network-java-manage-virtual-network) crea una [red virtual](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) para aislar los recursos de Azure en un segmento de red que puede controlar.

## <a name="run-the-sample"></a>Ejecución del ejemplo

Cree un [archivo de autenticación](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) y establezca una variable de entorno `AZURE_AUTH_LOCATION` con la ruta de acceso completa al archivo en el equipo. A continuación, ejecute:

```
git clone https://github.com/Azure-Samples/network-java-manage-virtual-network.git
cd network-java-manage-virtual-network
mvn clean compile exec:java
```

Vea el [código completo del ejemplo en GitHub](https://github.com/Azure-Samples/network-java-manage-virtual-network/blob/master/src/main/java/com/microsoft/azure/management/network/samples/ManageVirtualNetwork.java).

## <a name="authenticate-with-azure"></a>Autenticación con Azure

[!INCLUDE [auth-include](includes/java-auth-include.md)]

## <a name="create-a-network-security-group-to-block-internet-traffic"></a>Creación de un grupo de seguridad de red para bloquear el tráfico de Internet

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

Esta [regla de seguridad de red](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg) bloquea el tráfico de Internet público entrante y saliente. Este grupo de seguridad de red no tiene efecto hasta que se aplica a una subred de la red virtual.

## <a name="create-a-virtual-network-with-two-subnets"></a>Creación de una red virtual con dos subredes

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

La subred de back-end deniega el acceso a Internet según las reglas definidas en el grupo de seguridad de red. La subred de front-end utiliza las [reglas predeterminadas](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg) que permiten el tráfico saliente a Internet.

## <a name="create-a-network-security-group-to-allow-inbound-http-traffic"></a>Creación de un grupo de seguridad de red para permitir el tráfico HTTP entrante
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

Esta regla de seguridad de red abre el tráfico entrante en el puerto 80 desde la red Internet pública y bloquea todo el tráfico saliente desde dentro de la red a la red Internet pública. 

## <a name="update-a-virtual-network"></a>Actualización de una red virtual
```java
// update the front end subnet to use the rules in the new network security group
virtualNetwork1.update()
          .updateSubnet(vnet1FrontEndSubnetName)
          .withExistingNetworkSecurityGroup(frontEndSubnetNsg)
          .parent()
          .apply();
```

Actualice la subred de front-end para permitir el tráfico HTTP entrante con la regla de seguridad de red creada en el paso anterior.

## <a name="create-a-virtual-machine-on-a-subnet"></a>Creación de una máquina virtual en una subred
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

`withExistingPrimaryNetwork()` y `withSubnet()` configuran la máquina virtual para que utilice la subred de front-end en la red virtual que creó en los pasos anteriores.

## <a name="list-virtual-networks-in-a-resource-group"></a>Enumeración de redes virtuales en un grupo de recursos
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

Puede enumerar e inspeccionar el objeto `Network` mediante la colección exterior o recorrer en iteración cada recurso secundario para cada red mediante el bucle for-each anidado, tal como se muestra en este ejemplo.

## <a name="delete-a-virtual-network"></a>Eliminar una red virtual
```java
// if you already have the virtual network object it is easiest to delete by ID
azure.networks().deleteById(virtualNetwork1.id());

// Delete by resource group and name if you don't have the VirtualMachine object
azure.networks().deleteByResourceGroup(rgName,vnetName1);
```

La eliminación de una red virtual elimina las subredes de la red, pero no elimina las reglas del grupo de seguridad de red aplicadas a las subredes. Esas definiciones se pueden volver a aplicar en otras subredes.

## <a name="sample-explanation"></a>Explicación del ejemplo

Este ejemplo crea una red virtual con dos subredes y con una máquina virtual en cada subred. La subred de back-end está desconectada de la red Internet pública. La subred de front-end acepta el tráfico HTTP entrante desde Internet. Ambas máquinas virtuales en la red virtual se comunican entre sí a través de las reglas del grupo de seguridad de red predeterminadas.

| Clase utilizada en el ejemplo | Notas
|-------|-------|
| [Red](https://docs.microsoft.com/java/api/com.microsoft.azure.management.network._network) | Representación en forma de objeto local de la red virtual creada a partir de `azure.networks().define()...create()`. Use el encadenamiento `update()...apply()` para actualizar una red virtual existente.
| [Subred](https://docs.microsoft.com/java/api/com.microsoft.azure.management.network._subnet) | Crear subredes en la red virtual al definir o actualizar la red mediante `withSubnet()`. Obtener representaciones de objeto de una subred con `Network.subnets().get()` o `Network.subnets().entrySet()`. Estos objetos tienen métodos para consultar las propiedades de la subred.
| [NetworkSecurityGroup](https://docs.microsoft.com/java/api/com.microsoft.azure.management.network._network_security_group) | Se crea mediante el encadenamiento `azure.networkSecurityGroups().define()...create()` y se aplica a las subredes mediante la actualización o creación de subredes en una red virtual. 

## <a name="next-steps"></a>Pasos siguientes

[!INCLUDE [next-steps](includes/java-next-steps.md)]