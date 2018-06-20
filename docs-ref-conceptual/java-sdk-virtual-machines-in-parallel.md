---
title: Creación de máquinas virtuales en varias regiones en paralelo | Microsoft Docs
description: Código de ejemplo para crear máquinas virtuales en diferentes regiones de Azure en paralelo mediante el SDK de Azure para Java
author: rloutlaw
manager: douge
ms.assetid: e5a36699-2d96-4571-84f9-a6af13f3c067
ms.service: Azure
ms.devlang: java
ms.topic: article
ms.date: 03/30/2017
ms.author: routlaw;asirveda
ms.openlocfilehash: e20feb555c3a360eceae60c1569af9a00a5cd027
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/28/2017
ms.locfileid: "21931201"
---
# <a name="create-virtual-machines-across-multiple-regions-from-your-java-applications"></a>Creación de máquinas virtuales en varias regiones desde las aplicaciones Java

[Este ejemplo](https://github.com/Azure-Samples/compute-java-create-virtual-machines-across-regions-in-parallel) crea máquinas virtuales en paralelo en diferentes regiones de Azure mediante las [bibliotecas de administración de Azure para Java](https://github.com/Azure/azure-sdk-for-java).

> [!IMPORTANT]
> El ejemplo crea un total de 48 máquinas virtuales que ejecutan Ubuntu 16.04 LTS de [tamaño STANDARD_DS3_V2](http://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-sizes) en cuatro regiones. El código de ejemplo elimina estas máquinas virtuales antes de salir. No olvide [comprobar los límites de servicio y la cuota](http://docs.microsoft.com/azure/azure-subscription-service-limits) antes de ejecutar este ejemplo con el número predeterminado de máquinas virtuales.

## <a name="run-the-sample"></a>Ejecución del ejemplo

Cree un [archivo de autenticación](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) y establezca una variable de entorno `AZURE_AUTH_LOCATION` con la ruta de acceso completa al archivo en el equipo. A continuación, ejecute:

```
git clone https://github.com/Azure-Samples/compute-java-create-virtual-machines-across-regions-in-parallel.git
cd compute-java-create-virtual-machines-across-regions-in-parallel
mvn clean compile exec:java
```

Vea el [código completo del ejemplo en GitHub](https://github.com/Azure-Samples/compute-java-create-virtual-machines-across-regions-in-parallel/blob/master/src/main/java/com/microsoft/azure/management/compute/samples/CreateVirtualMachinesInParallel.java).

## <a name="authenticate-with-azure"></a>Autenticación con Azure

[!INCLUDE [auth-include](includes/java-auth-include.md)]

## <a name="set-locations-and-counts-for-the-virtual-machines"></a>Establecimiento de las ubicaciones y los recuentos de las máquinas virtuales

```java
// use a Map to define how where and how many VMs to create 
Map<Region, Integer> virtualMachinesByLocation = new HashMap<Region, Integer>();

// create 12 virtual machines in four regions
virtualMachinesByLocation.put(Region.US_EAST, 12);
virtualMachinesByLocation.put(Region.US_SOUTH_CENTRAL, 12);
virtualMachinesByLocation.put(Region.US_WEST, 12);
virtualMachinesByLocation.put(Region.US_NORTH_CENTRAL, 12);
```

Esta `Map` se usa más adelante en el ejemplo para establecer la distribución de las máquinas virtuales en todo el mundo.

## <a name="create-a-resource-group"></a>Crear un grupo de recursos 

```java
// logically associate the resources in the sample into a randomly named resource group
final String rgName = SdkContext.randomResourceName("rgCOPD", 24);
ResourceGroup resourceGroup = azure.resourceGroups().define(rgName)
                .withRegion(Region.US_EAST)
                .create();
```

Cada recurso en el ejemplo está administrado por este grupo de recursos. Esto facilita la limpieza de los recursos más adelante eliminando el grupo de recursos.

## <a name="define-the-virtual-machines"></a>Definición de las máquinas virtuales
```java
// list to store the VirtualMachine definitions
List<Creatable<VirtualMachine>> creatableVirtualMachines = new ArrayList<>();
    
// outer loop: iterate through each region included in the map
for (Map.Entry<Region, Integer> entry : virtualMachinesByLocation.entrySet()) {
    Region region = entry.getKey();
    Integer vmCount = entry.getValue();

    // Define one virtual network Creatable per region for the VMs to share
    String networkName = SdkContext.randomResourceName("vnetCOPD-", 20);
    Creatable<Network> networkCreatable = azure.networks().define(networkName)
           .withRegion(region)
           .withExistingResourceGroup(resourceGroup)
           .withAddressSpace("172.16.0.0/16");

    // Define one storage account Creatable per region for storing VM disks
    String storageAccountName = SdkContext.randomResourceName("stgcopd", 20);
    Creatable<StorageAccount> storageAccountCreatable = azure.storageAccounts()
        .define(storageAccountName)
              .withRegion(region)
              .withExistingResourceGroup(resourceGroup);

    // generate a common prefix for every VM name
    String linuxVMNamePrefix = SdkContext.randomResourceName("vm-", 15);

    // inner loop: iterate once for every VM instance in the region
    for (int i = 1; i <= vmCount; i++) {

        // Create one public IP address Creatable for each VM
        Creatable<PublicIpAddress> publicIpAddressCreatable = azure.publicIpAddresses()
             .define(String.format("%s-%d", linuxVMNamePrefix, i))
             .withRegion(region)
             .withExistingResourceGroup(resourceGroup)
             .withLeafDomainLabel(SdkContext.randomResourceName("pip", 10));

        publicIpCreatableKeys.add(publicIpAddressCreatable.key());

        // Create one virtual machine Creatable 
        Creatable<VirtualMachine> virtualMachineCreatable = azure.virtualMachines()
             .define(String.format("%s-%d", linuxVMNamePrefix, i))
             .withRegion(region)
             .withExistingResourceGroup(resourceGroup)
             .withNewPrimaryNetwork(networkCreatable)
             .withPrimaryPrivateIpAddressDynamic()
             .withNewPrimaryPublicIpAddress(publicIpAddressCreatable)
             .withPopularLinuxImage(KnownLinuxVirtualMachineImage.UBUNTU_SERVER_16_04_LTS)
             .withRootUsername(userName)
             .withSsh(sshKey)
             .withSize(VirtualMachineSizeTypes.STANDARD_DS3_V2)
             .withNewStorageAccount(storageAccountCreatable);
        // add the virtual machine Creatable to the list     
        creatableVirtualMachines.add(virtualMachineCreatable); 
     }
}
```

El bucle `for` exterior anterior recorre en iteración cada región y define una red virtual Creatable y una cuenta de almacenamiento Creatable para que las usen todas las máquinas virtuales en dicha región. Más información sobre el uso de objetos [Creatable](java-sdk-azure-concepts.md#Creatables) para crear recursos cuando se necesitan con las bibliotecas de administración.

El bucle `for` obtiene una dirección IP pública Creatable para la máquina virtual y, a continuación, define una máquina virtual Creatable utilizando los objetos Creatable para la red virtual, la cuenta de almacenamiento y la dirección IP pública que ha definido previamente.  A continuación, esta máquina virtual Creatable se agrega a la lista `creatableVirtualMachines`.

## <a name="create-the-virtual-machines"></a>Creación de las máquinas virtuales

```java
// create all virtual machines defined in the list, return all Creatable objects used
// including networks, public IP addresses, and storage accounts
CreatedResources<VirtualMachine> virtualMachines = azure.virtualMachines().create(creatableVirtualMachines);

// list the IDs of each virtual machine created 
for (VirtualMachine virtualMachine : virtualMachines.values()) {
    System.out.println(virtualMachine.id());
}

// call createdRelatedResource(key) to get the resources used to define the virtual machines. 
// Save the key at the time you define the Creatable to use CreatedResources like this
for (String publicIpCreatableKey : publicIpCreatableKeys) {
    PublicIPAddress pip = 
         (PublicIPAddress) virtualMachines.createdRelatedResource(publicIpCreatableKey);
}
```

La llamada a `azure.virtualMachines().create(creatableVirtualMachines)` crea todas las máquinas virtuales definidas en la lista `creatableVirtualMachines` en paralelo a través de las regiones.

Utilice el objeto `CreatedResources<VirtualMachine>` devuelto para tener acceso a los recursos creados en la suscripción de Azure mediante el método `create()`, no solo el tipo `VirtualMachine` devuelto. Convierta el valor devuelto por `createdRelatedResources()` al tipo correcto. 

Más información sobre cómo trabajar con `Creatable<T>` y `CreatedResources` en el [artículo de conceptos de la biblioteca](java-sdk-azure-concepts.md).

## <a name="delete-the-resource-group"></a>Eliminar el grupo de recursos 

```java
// finally block deletes the resource group before the code exits
// deleting a resource group deletes all resources created in it
finally {
    try {
        System.out.println("Deleting Resource Group: " + rgName);
        azure.resourceGroups().deleteByName(rgName);
        System.out.println("Deleted Resource Group: " + rgName);
    } catch (NullPointerException npe) {
        System.out.println("Did not create any resources in Azure. No clean up is necessary");
    } catch (Exception g) {
        g.printStackTrace();
    }
}
```

Este bloque elimina los recursos creados en el ejemplo antes de que finalice el ejemplo.

## <a name="sample-explanation"></a>Explicación del ejemplo

Vea el código completo del ejemplo en [GitHub](https://github.com/Azure-Samples/compute-java-create-virtual-machines-across-regions-in-parallel).

El ejemplo usa objetos `Creatable` para definir una cuenta de almacenamiento y una red virtual para cada región que hospeda las máquinas virtuales. Después, se definen los objetos `Creatable` para la dirección IP pública de cada máquina virtual. El ejemplo define las máquinas virtuales mediante estos objetos `Creatable` y agrega la definición de la máquina virtual a la lista `virtualMachineCreatable`.

Después de que el código agrega cada definición de máquina virtual a la lista, `azure.virtualMachines().create(creatableVirtualMachines)` crea cada máquina virtual en paralelo en Azure.

El código de ejemplo, a continuación, obtiene las direcciones IP de todas las máquinas virtuales creadas desde el objeto CreatedResources devuelto para crear una instancia de [Traffic Manager](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview) para distribuir la carga entre las máquinas virtuales. 

El bloque `finally` elimina los recursos de la suscripción de Azure incluso si se produce un error.

| Clase utilizada en el ejemplo | Notas
|-------|-------|
| [VirtualMachine](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._virtual_machine) | Consulte las propiedades de las máquinas virtuales y administre su estado. Recuperadas en forma de lista de `azure.virtualMachines().list()` o por nombre o identificador `azure.virtualMachines().getByResourceGroup()`
| [VirtualMachineSizeTypes](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._virtual_machine_size_types) | Valores estáticos que se asignan a [opciones de tamaño de máquina virtual](https://azure.microsoft.com/pricing/details/virtual-machines/linux/) para su uso como parámetro para `withSize()` al definir una máquina virtual.
| [PublicIpAddress](https://docs.microsoft.com/java/api/com.microsoft.azure.management.network._public_i_p_address) | Se define, pero no se crea inmediatamente, para cada máquina virtual a través de `azure.publicIpAddresses().define()`. Almacene la clave de cada `Creatable` y recupérela más adelante mediante `createdRelatedResource()`.
| [KnownLinuxVirtualMachineImage](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._known_linux_virtual_machine_image) | Conjunto de opciones de máquina virtual Linux usado como parámetro del método `withPopularLinuxImage()` al definir una máquina virtual.
| [Red](https://docs.microsoft.com/java/api/com.microsoft.azure.management.network._network) | El ejemplo define una red virtual para cada región a través de `azure.networks().define()`. 

## <a name="next-steps"></a>Pasos siguientes

[!INCLUDE [next-steps](includes/java-next-steps.md)]