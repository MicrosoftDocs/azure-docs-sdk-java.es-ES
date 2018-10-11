---
title: Administración de máquinas virtuales de Azure con Java | Microsoft Docs
description: Código de ejemplo para administrar máquinas virtuales de Azure mediante el SDK de Azure para Java
author: rloutlaw
manager: douge
ms.assetid: 88629aee-6279-433e-a08b-4f8e290446d0
ms.devlang: java
ms.topic: article
ms.service: Azure
ms.technology: Azure
ms.date: 3/30/2017
ms.author: routlaw;asirveda
ms.openlocfilehash: e3048b3317477f4b1fb8edf93e4bebad6b7fafce
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/09/2018
ms.locfileid: "48893616"
---
# <a name="manage-azure-virtual-machines-from-your-java-applications"></a>Administración de máquinas virtuales de Azure desde las aplicaciones Java

[Este ejemplo](https://github.com/Azure-Samples/compute-java-manage-vm/) utiliza las [bibliotecas de administración de Azure para Java](https://github.com/Azure/azure-sdk-for-java) para crear y trabajar con máquinas virtuales de Azure.

## <a name="run-the-sample"></a>Ejecución del ejemplo

Cree un [archivo de autenticación](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) y establezca una variable de entorno `AZURE_AUTH_LOCATION` con la ruta de acceso completa al archivo en el equipo. A continuación, ejecute:

```
git clone https://github.com/Azure-Samples/compute-java-manage-vm.git
cd compute-java-manage-vm
mvn clean compile exec:java
```

Vea el [código completo del ejemplo en GitHub](https://github.com/Azure-Samples/compute-java-manage-vm/blob/master/src/main/java/com/microsoft/azure/management/compute/samples/ManageVirtualMachine.java).

## <a name="authenticate-with-azure"></a>Autenticación con Azure

[!INCLUDE [auth-include](includes/java-auth-include.md)]

## <a name="create-a-windows-virtual-machine"></a>Creación de una máquina virtual Windows

```java
// Prepare a data disk for VM
Disk dataDisk = azure.disks().define(SdkContext.randomResourceName("dsk", 30))
            .withRegion(region)
            .withNewResourceGroup(rgName)
            .withData()
            .withSizeInGB(50)
            .create();

// create the windows virtual machine with the data disk            
VirtualMachine windowsVM = azure.virtualMachines().define(windowsVmName)
            .withRegion(region)
            .withNewResourceGroup(rgName)
            .withNewPrimaryNetwork("10.0.0.0/28")
            .withPrimaryPrivateIpAddressDynamic()
            .withoutPrimaryPublicIpAddress()
            .withPopularWindowsImage(KnownWindowsVirtualMachineImage.WINDOWS_SERVER_2012_R2_DATACENTER)
            .withAdminUsername(userName)
            .withAdminPassword(password)
            .withNewDataDisk(10)
            .withNewDataDisk(dataDiskCreatable)
            .withExistingDataDisk(dataDisk)
            .withSize(VirtualMachineSizeTypes.STANDARD_D3_V2)
            .create();
```

Este código:   

0. Define un objeto Creatable `Disk` con un tamaño de 50 GB y un nombre aleatorio para su uso con una máquina virtual.
0. Usa la cadena `azure.virtualMachines().define()..create()` para crear la máquina virtual con Windows Server 2012. La API crea el objeto `Disk` definido en el paso anterior al mismo tiempo que la máquina virtual. También se conecta un disco de datos de 10 GB a la máquina virtual mediante `withNewDataDisk(10)`.

Obtenga más información sobre el uso de [objetos Creatable<T>](java-sdk-azure-concepts.md#Creatables) para definir representaciones locales de recursos y crearlos justo cuando otros recursos de Azure los necesiten.

## <a name="stop-start-and-restart-a-virtual-machine"></a>Detener, iniciar y reiniciar una máquina virtual

```java
// look up a virtual machine by its ID and then restart, stop, and start it
azureVM = azure.getVirtualMachine.getById(windowsVM.id());

azureVM.restart();
azureVM.powerOff();
azureVM.start();
```

`powerOff()` detiene el sistema operativo de la máquina virtual pero no desasigna sus recursos.

## <a name="add-a-virtual-machine-to-an-existing-network"></a>Agregación de una máquina virtual a una red existente

```java
// Get the virtual network the current virtual machine is using
Network network = windowsVM.getPrimaryNetworkInterface().primaryIPConfiguration().getNetwork();

// Create a Linux VM in the same subnet
VirtualMachine linuxVM = azure.virtualMachines().define(linuxVmName)
           .withRegion(region)
           .withExistingResourceGroup(rgName)
           .withExistingPrimaryNetwork(network)
           .withSubnet("subnet1") // default subnet name when no name specified at creation
           .withPrimaryPrivateIPAddressDynamic()
           .withoutPrimaryPublicIPAddress()
           .withPopularLinuxImage(KnownLinuxVirtualMachineImage.UBUNTU_SERVER_16_04_LTS)
           .withRootUsername(userName)
           .withRootPassword(password)
           .withSize(VirtualMachineSizeTypes.STANDARD_D3_V2)
           .create();
```

Use `withPopularLinuxImage` para definir una máquina virtual Linux en lugar de Windows.


## <a name="list-virtual-machines"></a>Enumeración de máquinas virtuales

```java
// get a list of VMs in the same resource group as an existing VM
String resourceGroupName = windowsVM.resourceGroupName();
PagedList<VirtualMachine> resourceGroupVMs = azure.virtualMachines()
        .listByResourceGroup(resourceGroupName); 

// for each vitual machine in the resource group, log their name and plan
for (VirtualMachine virtualMachine : azure.virtualMachines().listByResourceGroup(resourceGroupName)) {
    System.out.println("VM " + virtualMachine.computerName() + 
        " has plan " + virtualMachine.plan());
}
```

Enumere todas las máquinas virtuales de una suscripción con `azure.virtualMachines().list()` y recorra en iteración la asignación devuelta por `tags()` para administrar colecciones etiquetadas de máquinas virtuales en grupos de recursos.

## <a name="update-a-virtual-machine"></a>Actualización de una máquina virtual

```java
// add a 10GB data disk to the virtual machine
windowsVM.update()
     .withNewDataDisk(10)
     .apply();
```

Actualice la configuración de la máquina virtual con `update()...apply()` y los mismos métodos usados para configurar la máquina virtual cuando se creó mediante `define()...create()`.

## <a name="delete-a-virtual-machine"></a>Eliminación de una máquina virtual

```java
// delete by ID if you already are working with the VM object
azure.virtualMachines().deleteById(windowsVM.id());

// delete by resource group and name
azure.virtualMachines().deleteByResourceGroup(rgName,windowsVmName);
```

## <a name="sample-explanation"></a>Explicación del ejemplo

[El código de ejemplo](https://github.com/Azure-Samples/compute-java-manage-vm/blob/master/src/main/java/com/microsoft/azure/management/compute/samples/ManageVirtualMachine.java) crea una máquina virtual Windows con un disco de datos de 50 GB. El ejemplo, a continuación, crea un segundo disco de datos de 10 GB y lo asocia a esta máquina virtual Windows.
Después, el ejemplo crea una máquina virtual Linux en la misma red virtual que la máquina virtual Windows.

El ejemplo registra información acerca de ambas máquinas virtuales y las elimina antes de finalizar.

| Clase utilizada en el ejemplo | Notas
|-------|-------|
| [VirtualMachine](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._virtual_machine) | Consulte las propiedades de las máquinas virtuales y administre su estado. Recuperadas en forma de lista con `azure.virtualMachines().list()` o por nombre o identificador `azure.virtualMachines().getByResourceGroup()`
| [VirtualMachineSizeTypes](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._virtual_machine_size_types) | Clase con valores estáticos que se corresponden con las [opciones de tamaño de máquina virtual](https://azure.microsoft.com/pricing/details/virtual-machines/linux/); la usa el método `withSize()` para definir los recursos asignados a la máquina virtual.
| [Disco](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._disk) | Cree un disco para almacenar datos con `withData()` o con una imagen de sistema operativo, con el método `withLinux` o `withWindows` correspondiente al definir el disco. Conecte discos a las máquinas virtuales en el momento de creación (`using withNewDataDisk` o `withExistingDataDisk`) o después con `update()..apply()` en el objeto VirtualMachine.
| [DiskSkuTypes](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._disk_sku_types) | Clase con valores estáticos para definir un disco con un plan de almacenamiento estándar o [premium](https://docs.microsoft.com/azure/storage/storage-premium-storage).
| [KnownLinuxVirtualMachineImage](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._known_linux_virtual_machine_image) | Clase con un conjunto de opciones de máquina virtual Linux para su uso con el método `withPopularLinuxImage()` al definir una máquina virtual.
| [KnownWindowsVirtualMachineImage](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._known_windows_virtual_machine_image) | Clase con un conjunto de opciones de imagen de máquina virtual Windows para su uso con el método `withPopularWindowsImage()` al definir una máquina virtual.

## <a name="next-steps"></a>Pasos siguientes

[!INCLUDE [next-steps](includes/java-next-steps.md)]