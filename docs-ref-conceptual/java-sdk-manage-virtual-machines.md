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
ms.openlocfilehash: 388b68bfb0fdac70efed5ad5d0f7c957ce915449
ms.sourcegitcommit: 115f4c8ad07a11f17d79e9d945d63917836b11c8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "61592570"
---
# <a name="manage-azure-virtual-machines-from-your-java-applications"></a><span data-ttu-id="932f6-103">Administración de máquinas virtuales de Azure desde las aplicaciones Java</span><span class="sxs-lookup"><span data-stu-id="932f6-103">Manage Azure virtual machines from your Java applications</span></span>

<span data-ttu-id="932f6-104">[Este ejemplo](https://github.com/Azure-Samples/compute-java-manage-vm/) utiliza las [bibliotecas de administración de Azure para Java](https://github.com/Azure/azure-sdk-for-java) para crear y trabajar con máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="932f6-104">[This sample](https://github.com/Azure-Samples/compute-java-manage-vm/) uses the [Azure management libraries for Java](https://github.com/Azure/azure-sdk-for-java) to create and work with Azure virtual machines.</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="932f6-105">Ejecución del ejemplo</span><span class="sxs-lookup"><span data-stu-id="932f6-105">Run the sample</span></span>

<span data-ttu-id="932f6-106">Cree un [archivo de autenticación](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) y establezca una variable de entorno `AZURE_AUTH_LOCATION` con la ruta de acceso completa al archivo en el equipo.</span><span class="sxs-lookup"><span data-stu-id="932f6-106">Create an [authentication file](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) and set an environment variable `AZURE_AUTH_LOCATION` with the full path to the file on your computer.</span></span> <span data-ttu-id="932f6-107">A continuación, ejecute:</span><span class="sxs-lookup"><span data-stu-id="932f6-107">Then run:</span></span>

```
git clone https://github.com/Azure-Samples/compute-java-manage-vm.git
cd compute-java-manage-vm
mvn clean compile exec:java
```

<span data-ttu-id="932f6-108">Vea el [código completo del ejemplo en GitHub](https://github.com/Azure-Samples/compute-java-manage-vm/blob/master/src/main/java/com/microsoft/azure/management/compute/samples/ManageVirtualMachine.java).</span><span class="sxs-lookup"><span data-stu-id="932f6-108">View the [complete code sample on GitHub](https://github.com/Azure-Samples/compute-java-manage-vm/blob/master/src/main/java/com/microsoft/azure/management/compute/samples/ManageVirtualMachine.java).</span></span>

## <a name="authenticate-with-azure"></a><span data-ttu-id="932f6-109">Autenticación con Azure</span><span class="sxs-lookup"><span data-stu-id="932f6-109">Authenticate with Azure</span></span>

[!INCLUDE [auth-include](includes/java-auth-include.md)]

## <a name="create-a-windows-virtual-machine"></a><span data-ttu-id="932f6-110">Creación de una máquina virtual Windows</span><span class="sxs-lookup"><span data-stu-id="932f6-110">Create a Windows virtual machine</span></span>

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

<span data-ttu-id="932f6-111">Este código:</span><span class="sxs-lookup"><span data-stu-id="932f6-111">This code:</span></span>   

0. <span data-ttu-id="932f6-112">Define un objeto Creatable `Disk` con un tamaño de 50 GB y un nombre aleatorio para su uso con una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="932f6-112">Defines a `Disk` Creatable with a 50GB size and random name for use with a virtual machine.</span></span>
0. <span data-ttu-id="932f6-113">Usa la cadena `azure.virtualMachines().define()..create()` para crear la máquina virtual con Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="932f6-113">Uses the `azure.virtualMachines().define()..create()` chain to create the Windows Server 2012 virtual machine.</span></span> <span data-ttu-id="932f6-114">La API crea el objeto `Disk` definido en el paso anterior al mismo tiempo que la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="932f6-114">The API creates the `Disk` defined in the previous step the same time as the virtual machine.</span></span> <span data-ttu-id="932f6-115">También se conecta un disco de datos de 10 GB a la máquina virtual mediante `withNewDataDisk(10)`.</span><span class="sxs-lookup"><span data-stu-id="932f6-115">A 10GB data disk is also attached to the virtual machine through `withNewDataDisk(10)`.</span></span>

<span data-ttu-id="932f6-116">Obtenga más información sobre el uso de [objetos Creatable<T>](java-sdk-azure-concepts.md#Creatables) para definir representaciones locales de recursos y crearlos justo cuando otros recursos de Azure los necesiten.</span><span class="sxs-lookup"><span data-stu-id="932f6-116">Learn more about using [Creatable<T> objects](java-sdk-azure-concepts.md#Creatables) to define local representations of resources and create them just as other Azure resources need them.</span></span>

## <a name="stop-start-and-restart-a-virtual-machine"></a><span data-ttu-id="932f6-117">Detener, iniciar y reiniciar una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="932f6-117">Stop, start, and restart a virtual machine</span></span>

```java
// look up a virtual machine by its ID and then restart, stop, and start it
azureVM = azure.getVirtualMachine.getById(windowsVM.id());

azureVM.restart();
azureVM.powerOff();
azureVM.start();
```

<span data-ttu-id="932f6-118">`powerOff()` detiene el sistema operativo de la máquina virtual pero no desasigna sus recursos.</span><span class="sxs-lookup"><span data-stu-id="932f6-118">`powerOff()` stops the virtual machine operating system but does not deallocate its resources.</span></span>

## <a name="add-a-virtual-machine-to-an-existing-network"></a><span data-ttu-id="932f6-119">Agregación de una máquina virtual a una red existente</span><span class="sxs-lookup"><span data-stu-id="932f6-119">Add a virtual machine to an existing network</span></span>

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

<span data-ttu-id="932f6-120">Use `withPopularLinuxImage` para definir una máquina virtual Linux en lugar de Windows.</span><span class="sxs-lookup"><span data-stu-id="932f6-120">Use `withPopularLinuxImage` to define a Linux VM instead of a Windows one.</span></span>


## <a name="list-virtual-machines"></a><span data-ttu-id="932f6-121">Enumeración de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="932f6-121">List virtual machines</span></span>

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

<span data-ttu-id="932f6-122">Enumere todas las máquinas virtuales de una suscripción con `azure.virtualMachines().list()` y recorra en iteración la asignación devuelta por `tags()` para administrar colecciones etiquetadas de máquinas virtuales en grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="932f6-122">List all virtual machines for a subscription using `azure.virtualMachines().list()` and iterate through the Map returned by `tags()` to manage tagged collections of virtual machines across resource groups.</span></span>

## <a name="update-a-virtual-machine"></a><span data-ttu-id="932f6-123">Actualización de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="932f6-123">Update a virtual machine</span></span>

```java
// add a 10GB data disk to the virtual machine
windowsVM.update()
     .withNewDataDisk(10)
     .apply();
```

<span data-ttu-id="932f6-124">Actualice la configuración de la máquina virtual con `update()...apply()` y los mismos métodos usados para configurar la máquina virtual cuando se creó mediante `define()...create()`.</span><span class="sxs-lookup"><span data-stu-id="932f6-124">Update the virtual machine configuration using `update()...apply()` and the same methods used to configure the virtual machine when created through `define()...create()`.</span></span>

## <a name="delete-a-virtual-machine"></a><span data-ttu-id="932f6-125">Eliminación de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="932f6-125">Delete a virtual machine</span></span>

```java
// delete by ID if you already are working with the VM object
azure.virtualMachines().deleteById(windowsVM.id());

// delete by resource group and name
azure.virtualMachines().deleteByResourceGroup(rgName,windowsVmName);
```

## <a name="sample-explanation"></a><span data-ttu-id="932f6-126">Explicación del ejemplo</span><span class="sxs-lookup"><span data-stu-id="932f6-126">Sample explanation</span></span>

<span data-ttu-id="932f6-127">[El código de ejemplo](https://github.com/Azure-Samples/compute-java-manage-vm/blob/master/src/main/java/com/microsoft/azure/management/compute/samples/ManageVirtualMachine.java) crea una máquina virtual Windows con un disco de datos de 50 GB.</span><span class="sxs-lookup"><span data-stu-id="932f6-127">[The sample code](https://github.com/Azure-Samples/compute-java-manage-vm/blob/master/src/main/java/com/microsoft/azure/management/compute/samples/ManageVirtualMachine.java) creates a Windows virtual machine with a 50GB data disk.</span></span> <span data-ttu-id="932f6-128">El ejemplo, a continuación, crea un segundo disco de datos de 10 GB y lo asocia a esta máquina virtual Windows.</span><span class="sxs-lookup"><span data-stu-id="932f6-128">The sample then creates a second 10GB data disk and attaches it to this Windows virtual machine.</span></span>
<span data-ttu-id="932f6-129">Después, el ejemplo crea una máquina virtual Linux en la misma red virtual que la máquina virtual Windows.</span><span class="sxs-lookup"><span data-stu-id="932f6-129">Then the sample creates a Linux virtual machine in the same virtual network as the Windows virtual machine.</span></span>

<span data-ttu-id="932f6-130">El ejemplo registra información acerca de ambas máquinas virtuales y las elimina antes de finalizar.</span><span class="sxs-lookup"><span data-stu-id="932f6-130">The sample logs information about both virtual machines and deletes them both before completing.</span></span>

| <span data-ttu-id="932f6-131">Clase utilizada en el ejemplo</span><span class="sxs-lookup"><span data-stu-id="932f6-131">Class used in sample</span></span> | <span data-ttu-id="932f6-132">Notas</span><span class="sxs-lookup"><span data-stu-id="932f6-132">Notes</span></span>
|-------|-------|
| [<span data-ttu-id="932f6-133">VirtualMachine</span><span class="sxs-lookup"><span data-stu-id="932f6-133">VirtualMachine</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._virtual_machine) | <span data-ttu-id="932f6-134">Consulte las propiedades de las máquinas virtuales y administre su estado.</span><span class="sxs-lookup"><span data-stu-id="932f6-134">Query properties and manage state of virtual machines.</span></span> <span data-ttu-id="932f6-135">Recuperadas en forma de lista con `azure.virtualMachines().list()` o por nombre o identificador `azure.virtualMachines().getByResourceGroup()`</span><span class="sxs-lookup"><span data-stu-id="932f6-135">Retrieved in list form  with`azure.virtualMachines().list()` or by name or ID `azure.virtualMachines().getByResourceGroup()`</span></span>
| [<span data-ttu-id="932f6-136">VirtualMachineSizeTypes</span><span class="sxs-lookup"><span data-stu-id="932f6-136">VirtualMachineSizeTypes</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._virtual_machine_size_types) | <span data-ttu-id="932f6-137">Clase con valores estáticos que se corresponden con las [opciones de tamaño de máquina virtual](https://azure.microsoft.com/pricing/details/virtual-machines/linux/); la usa el método `withSize()` para definir los recursos asignados a la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="932f6-137">Class with static values that map to [virtual machine size options](https://azure.microsoft.com/pricing/details/virtual-machines/linux/), used by the `withSize()` method to define the resources allocated to the VM.</span></span>
| [<span data-ttu-id="932f6-138">Disco</span><span class="sxs-lookup"><span data-stu-id="932f6-138">Disk</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._disk) | <span data-ttu-id="932f6-139">Cree un disco para almacenar datos con `withData()` o con una imagen de sistema operativo, con el método `withLinux` o `withWindows` correspondiente al definir el disco.</span><span class="sxs-lookup"><span data-stu-id="932f6-139">Create a disk to store data using `withData()` or operating system image using the appropriate `withLinux` or `withWindows` method when defining the disk.</span></span> <span data-ttu-id="932f6-140">Conecte discos a las máquinas virtuales en el momento de creación (`using withNewDataDisk` o `withExistingDataDisk`) o después con `update()..apply()` en el objeto VirtualMachine.</span><span class="sxs-lookup"><span data-stu-id="932f6-140">Attach disks to virtual machines either at the time of creation (`using withNewDataDisk` or `withExistingDataDisk`) or after creation by `update()..apply()` on the VirtualMachine object.</span></span>
| [<span data-ttu-id="932f6-141">DiskSkuTypes</span><span class="sxs-lookup"><span data-stu-id="932f6-141">DiskSkuTypes</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._disk_sku_types) | <span data-ttu-id="932f6-142">Clase con valores estáticos para definir un disco con un plan de almacenamiento estándar o [premium](https://docs.microsoft.com/azure/storage/storage-premium-storage).</span><span class="sxs-lookup"><span data-stu-id="932f6-142">Class with static values to define a disk with a standard or [premium](https://docs.microsoft.com/azure/storage/storage-premium-storage) storage plan.</span></span>
| [<span data-ttu-id="932f6-143">KnownLinuxVirtualMachineImage</span><span class="sxs-lookup"><span data-stu-id="932f6-143">KnownLinuxVirtualMachineImage</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._known_linux_virtual_machine_image) | <span data-ttu-id="932f6-144">Clase con un conjunto de opciones de máquina virtual Linux para su uso con el método `withPopularLinuxImage()` al definir una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="932f6-144">Class with a set of Linux virtual machine options for use with the `withPopularLinuxImage()` method when defining a virtual machine.</span></span>
| [<span data-ttu-id="932f6-145">KnownWindowsVirtualMachineImage</span><span class="sxs-lookup"><span data-stu-id="932f6-145">KnownWindowsVirtualMachineImage</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._known_windows_virtual_machine_image) | <span data-ttu-id="932f6-146">Clase con un conjunto de opciones de imagen de máquina virtual Windows para su uso con el método `withPopularWindowsImage()` al definir una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="932f6-146">Class with a set of Windows virtual machine image options for use with the `withPopularWindowsImage()` method when defining a virtual machine.</span></span>

## <a name="next-steps"></a><span data-ttu-id="932f6-147">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="932f6-147">Next steps</span></span>

[!INCLUDE [next-steps](includes/java-next-steps.md)]