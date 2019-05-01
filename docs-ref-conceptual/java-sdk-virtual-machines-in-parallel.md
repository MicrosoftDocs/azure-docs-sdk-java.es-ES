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
ms.openlocfilehash: 497ea5c4e2efd73335f05f90b700fb70e2809de6
ms.sourcegitcommit: 115f4c8ad07a11f17d79e9d945d63917836b11c8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "61592523"
---
# <a name="create-virtual-machines-across-multiple-regions-from-your-java-applications"></a><span data-ttu-id="f9d00-103">Creación de máquinas virtuales en varias regiones desde las aplicaciones Java</span><span class="sxs-lookup"><span data-stu-id="f9d00-103">Create virtual machines across multiple regions from your Java applications</span></span>

<span data-ttu-id="f9d00-104">[Este ejemplo](https://github.com/Azure-Samples/compute-java-create-virtual-machines-across-regions-in-parallel) crea máquinas virtuales en paralelo en diferentes regiones de Azure mediante las [bibliotecas de administración de Azure para Java](https://github.com/Azure/azure-sdk-for-java).</span><span class="sxs-lookup"><span data-stu-id="f9d00-104">[This sample](https://github.com/Azure-Samples/compute-java-create-virtual-machines-across-regions-in-parallel) creates virtual machines in parallel across different Azure regions using the [Azure management libraries for Java](https://github.com/Azure/azure-sdk-for-java).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f9d00-105">El ejemplo crea un total de 48 máquinas virtuales que ejecutan Ubuntu 16.04 LTS de [tamaño STANDARD_DS3_V2](http://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-sizes) en cuatro regiones.</span><span class="sxs-lookup"><span data-stu-id="f9d00-105">The sample creates a total of 48 VMs running Ubuntu 16.04 LTS of [size STANDARD_DS3_V2](http://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-sizes) across four regions.</span></span> <span data-ttu-id="f9d00-106">El código de ejemplo elimina estas máquinas virtuales antes de salir.</span><span class="sxs-lookup"><span data-stu-id="f9d00-106">The sample code deletes these virtual machines before exiting.</span></span> <span data-ttu-id="f9d00-107">No olvide [comprobar los límites de servicio y la cuota](http://docs.microsoft.com/azure/azure-subscription-service-limits) antes de ejecutar este ejemplo con el número predeterminado de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="f9d00-107">Make sure to [check your service limits and quota](http://docs.microsoft.com/azure/azure-subscription-service-limits) before running this sample with the default number of VMs.</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="f9d00-108">Ejecución del ejemplo</span><span class="sxs-lookup"><span data-stu-id="f9d00-108">Run the sample</span></span>

<span data-ttu-id="f9d00-109">Cree un [archivo de autenticación](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) y establezca una variable de entorno `AZURE_AUTH_LOCATION` con la ruta de acceso completa al archivo en el equipo.</span><span class="sxs-lookup"><span data-stu-id="f9d00-109">Create an [authentication file](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) and set an environment variable `AZURE_AUTH_LOCATION` with the full path to the file on your computer.</span></span> <span data-ttu-id="f9d00-110">A continuación, ejecute:</span><span class="sxs-lookup"><span data-stu-id="f9d00-110">Then run:</span></span>

```
git clone https://github.com/Azure-Samples/compute-java-create-virtual-machines-across-regions-in-parallel.git
cd compute-java-create-virtual-machines-across-regions-in-parallel
mvn clean compile exec:java
```

<span data-ttu-id="f9d00-111">Vea el [código completo del ejemplo en GitHub](https://github.com/Azure-Samples/compute-java-create-virtual-machines-across-regions-in-parallel/blob/master/src/main/java/com/microsoft/azure/management/compute/samples/CreateVirtualMachinesInParallel.java).</span><span class="sxs-lookup"><span data-stu-id="f9d00-111">View the [complete code sample on GitHub](https://github.com/Azure-Samples/compute-java-create-virtual-machines-across-regions-in-parallel/blob/master/src/main/java/com/microsoft/azure/management/compute/samples/CreateVirtualMachinesInParallel.java).</span></span>

## <a name="authenticate-with-azure"></a><span data-ttu-id="f9d00-112">Autenticación con Azure</span><span class="sxs-lookup"><span data-stu-id="f9d00-112">Authenticate with Azure</span></span>

[!INCLUDE [auth-include](includes/java-auth-include.md)]

## <a name="set-locations-and-counts-for-the-virtual-machines"></a><span data-ttu-id="f9d00-113">Establecimiento de las ubicaciones y los recuentos de las máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="f9d00-113">Set locations and counts for the virtual machines</span></span>

```java
// use a Map to define how where and how many VMs to create 
Map<Region, Integer> virtualMachinesByLocation = new HashMap<Region, Integer>();

// create 12 virtual machines in four regions
virtualMachinesByLocation.put(Region.US_EAST, 12);
virtualMachinesByLocation.put(Region.US_SOUTH_CENTRAL, 12);
virtualMachinesByLocation.put(Region.US_WEST, 12);
virtualMachinesByLocation.put(Region.US_NORTH_CENTRAL, 12);
```

<span data-ttu-id="f9d00-114">Esta `Map` se usa más adelante en el ejemplo para establecer la distribución de las máquinas virtuales en todo el mundo.</span><span class="sxs-lookup"><span data-stu-id="f9d00-114">This `Map` is used later in the sample to set the distrubtion of the VMs worldwide.</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="f9d00-115">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="f9d00-115">Create a resource group</span></span> 

```java
// logically associate the resources in the sample into a randomly named resource group
final String rgName = SdkContext.randomResourceName("rgCOPD", 24);
ResourceGroup resourceGroup = azure.resourceGroups().define(rgName)
                .withRegion(Region.US_EAST)
                .create();
```

<span data-ttu-id="f9d00-116">Cada recurso en el ejemplo está administrado por este grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="f9d00-116">Each resource in the sample is managed by this resource group.</span></span> <span data-ttu-id="f9d00-117">Esto facilita la limpieza de los recursos más adelante eliminando el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="f9d00-117">This makes the resources easy to clean up later by deleting the resource group.</span></span>

## <a name="define-the-virtual-machines"></a><span data-ttu-id="f9d00-118">Definición de las máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="f9d00-118">Define the virtual machines</span></span>
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

<span data-ttu-id="f9d00-119">El bucle `for` exterior anterior recorre en iteración cada región y define una red virtual Creatable y una cuenta de almacenamiento Creatable para que las usen todas las máquinas virtuales en dicha región.</span><span class="sxs-lookup"><span data-stu-id="f9d00-119">The outer `for` loop above iterates through each region, defining a virtual network Creatable and storage account Creatable for use by all virtual machines in that region.</span></span> <span data-ttu-id="f9d00-120">Más información sobre el uso de objetos [Creatable](java-sdk-azure-concepts.md#Creatables) para crear recursos cuando se necesitan con las bibliotecas de administración.</span><span class="sxs-lookup"><span data-stu-id="f9d00-120">Learn more about using [Creatables](java-sdk-azure-concepts.md#Creatables) to create resources only as needed when using the management libraries.</span></span>

<span data-ttu-id="f9d00-121">El bucle `for` obtiene una dirección IP pública Creatable para la máquina virtual y, a continuación, define una máquina virtual Creatable utilizando los objetos Creatable para la red virtual, la cuenta de almacenamiento y la dirección IP pública que ha definido previamente.</span><span class="sxs-lookup"><span data-stu-id="f9d00-121">The inner `for` loop gets a public IP address Creatable for the virtual machine and then defines a virtual machine Creatable using the Creatables for the virtual network, storage account, and public IP address defined previously.</span></span>  <span data-ttu-id="f9d00-122">A continuación, esta máquina virtual Creatable se agrega a la lista `creatableVirtualMachines`.</span><span class="sxs-lookup"><span data-stu-id="f9d00-122">This VirtualMachine Creatable is then added to the `creatableVirtualMachines` list.</span></span>

## <a name="create-the-virtual-machines"></a><span data-ttu-id="f9d00-123">Creación de las máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="f9d00-123">Create the virtual machines</span></span>

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

<span data-ttu-id="f9d00-124">La llamada a `azure.virtualMachines().create(creatableVirtualMachines)` crea todas las máquinas virtuales definidas en la lista `creatableVirtualMachines` en paralelo a través de las regiones.</span><span class="sxs-lookup"><span data-stu-id="f9d00-124">The `azure.virtualMachines().create(creatableVirtualMachines)` call creates all of the virtual machines defined in the `creatableVirtualMachines` List in parallel across the regions.</span></span>

<span data-ttu-id="f9d00-125">Utilice el objeto `CreatedResources<VirtualMachine>` devuelto para tener acceso a los recursos creados en la suscripción de Azure mediante el método `create()`, no solo el tipo `VirtualMachine` devuelto.</span><span class="sxs-lookup"><span data-stu-id="f9d00-125">Use the returned `CreatedResources<VirtualMachine>` object to access any resources created in the Azure subscription during the the `create()` method, not just the returned `VirtualMachine` type.</span></span> <span data-ttu-id="f9d00-126">Convierta el valor devuelto por `createdRelatedResources()` al tipo correcto.</span><span class="sxs-lookup"><span data-stu-id="f9d00-126">Cast the returned value from `createdRelatedResources()` to the correct type.</span></span> 

<span data-ttu-id="f9d00-127">Más información sobre cómo trabajar con `Creatable<T>` y `CreatedResources` en el [artículo de conceptos de la biblioteca](java-sdk-azure-concepts.md).</span><span class="sxs-lookup"><span data-stu-id="f9d00-127">Learn more about working with `Creatable<T>` and `CreatedResources` in our [library concepts article](java-sdk-azure-concepts.md).</span></span>

## <a name="delete-the-resource-group"></a><span data-ttu-id="f9d00-128">Eliminar el grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="f9d00-128">Delete the resource group</span></span> 

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

<span data-ttu-id="f9d00-129">Este bloque elimina los recursos creados en el ejemplo antes de que finalice el ejemplo.</span><span class="sxs-lookup"><span data-stu-id="f9d00-129">This block deletes resources created in the sample before the sample exits.</span></span>

## <a name="sample-explanation"></a><span data-ttu-id="f9d00-130">Explicación del ejemplo</span><span class="sxs-lookup"><span data-stu-id="f9d00-130">Sample explanation</span></span>

<span data-ttu-id="f9d00-131">Vea el código completo del ejemplo en [GitHub](https://github.com/Azure-Samples/compute-java-create-virtual-machines-across-regions-in-parallel).</span><span class="sxs-lookup"><span data-stu-id="f9d00-131">View the complete sample code on [Github](https://github.com/Azure-Samples/compute-java-create-virtual-machines-across-regions-in-parallel).</span></span>

<span data-ttu-id="f9d00-132">El ejemplo usa objetos `Creatable` para definir una cuenta de almacenamiento y una red virtual para cada región que hospeda las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="f9d00-132">The sample uses `Creatable` objects to define a virtual network and storage account for each region hosting the virtual machines.</span></span> <span data-ttu-id="f9d00-133">Después, se definen los objetos `Creatable` para la dirección IP pública de cada máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f9d00-133">`Creatable` objects are then defined for the public IP address for each virtual machine.</span></span> <span data-ttu-id="f9d00-134">El ejemplo define las máquinas virtuales mediante estos objetos `Creatable` y agrega la definición de la máquina virtual a la lista `virtualMachineCreatable`.</span><span class="sxs-lookup"><span data-stu-id="f9d00-134">The sample defines the virtual machines using these `Creatable` objects, and sample adds the VM definition to the `virtualMachineCreatable` list.</span></span>

<span data-ttu-id="f9d00-135">Después de que el código agrega cada definición de máquina virtual a la lista, `azure.virtualMachines().create(creatableVirtualMachines)` crea cada máquina virtual en paralelo en Azure.</span><span class="sxs-lookup"><span data-stu-id="f9d00-135">After the code adds every virtual machine definition to the list, `azure.virtualMachines().create(creatableVirtualMachines)` creates each virtual machine in parallel in Azure.</span></span>

<span data-ttu-id="f9d00-136">El código de ejemplo, a continuación, obtiene las direcciones IP de todas las máquinas virtuales creadas desde el objeto CreatedResources devuelto para crear una instancia de [Traffic Manager](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview) para distribuir la carga entre las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="f9d00-136">The sample code then gets the IP addresses for all of the created virtual machines from the returned CreatedResources object to create a [Traffic Manager](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview) to distribute load across the virtual machines.</span></span> 

<span data-ttu-id="f9d00-137">El bloque `finally` elimina los recursos de la suscripción de Azure incluso si se produce un error.</span><span class="sxs-lookup"><span data-stu-id="f9d00-137">The `finally` block deletes the resources from your Azure subscription even in the case of an error.</span></span>

| <span data-ttu-id="f9d00-138">Clase utilizada en el ejemplo</span><span class="sxs-lookup"><span data-stu-id="f9d00-138">Class used in sample</span></span> | <span data-ttu-id="f9d00-139">Notas</span><span class="sxs-lookup"><span data-stu-id="f9d00-139">Notes</span></span>
|-------|-------|
| [<span data-ttu-id="f9d00-140">VirtualMachine</span><span class="sxs-lookup"><span data-stu-id="f9d00-140">VirtualMachine</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._virtual_machine) | <span data-ttu-id="f9d00-141">Consulte las propiedades de las máquinas virtuales y administre su estado.</span><span class="sxs-lookup"><span data-stu-id="f9d00-141">Query properties and manage state of virtual machines.</span></span> <span data-ttu-id="f9d00-142">Recuperadas en forma de lista de `azure.virtualMachines().list()` o por nombre o identificador `azure.virtualMachines().getByResourceGroup()`</span><span class="sxs-lookup"><span data-stu-id="f9d00-142">Retrieved in list form from `azure.virtualMachines().list()` or by name or ID `azure.virtualMachines().getByResourceGroup()`</span></span>
| [<span data-ttu-id="f9d00-143">VirtualMachineSizeTypes</span><span class="sxs-lookup"><span data-stu-id="f9d00-143">VirtualMachineSizeTypes</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._virtual_machine_size_types) | <span data-ttu-id="f9d00-144">Valores estáticos que se asignan a [opciones de tamaño de máquina virtual](https://azure.microsoft.com/pricing/details/virtual-machines/linux/) para su uso como parámetro para `withSize()` al definir una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f9d00-144">Static values that map to [virtual machine size options](https://azure.microsoft.com/pricing/details/virtual-machines/linux/) for use as a parameter to `withSize()` when defining a virtual machine.</span></span>
| [<span data-ttu-id="f9d00-145">PublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="f9d00-145">PublicIpAddress</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.network._public_i_p_address) | <span data-ttu-id="f9d00-146">Se define, pero no se crea inmediatamente, para cada máquina virtual a través de `azure.publicIpAddresses().define()`.</span><span class="sxs-lookup"><span data-stu-id="f9d00-146">Defined, but not immediately created, for each virtual machine through `azure.publicIpAddresses().define()`.</span></span> <span data-ttu-id="f9d00-147">Almacene la clave de cada `Creatable` y recupérela más adelante mediante `createdRelatedResource()`.</span><span class="sxs-lookup"><span data-stu-id="f9d00-147">Store the key for each `Creatable` and retrieve later through `createdRelatedResource()`</span></span>
| [<span data-ttu-id="f9d00-148">KnownLinuxVirtualMachineImage</span><span class="sxs-lookup"><span data-stu-id="f9d00-148">KnownLinuxVirtualMachineImage</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._known_linux_virtual_machine_image) | <span data-ttu-id="f9d00-149">Conjunto de opciones de máquina virtual Linux usado como parámetro del método `withPopularLinuxImage()` al definir una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f9d00-149">Set of Linux virtual machine options used as a parameter to `withPopularLinuxImage()` method when defining a virtual machine.</span></span>
| [<span data-ttu-id="f9d00-150">Red</span><span class="sxs-lookup"><span data-stu-id="f9d00-150">Network</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.network._network) | <span data-ttu-id="f9d00-151">El ejemplo define una red virtual para cada región a través de `azure.networks().define()`.</span><span class="sxs-lookup"><span data-stu-id="f9d00-151">The sample defines one virtual network for each region through  `azure.networks().define()` .</span></span> 

## <a name="next-steps"></a><span data-ttu-id="f9d00-152">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f9d00-152">Next steps</span></span>

[!INCLUDE [next-steps](includes/java-next-steps.md)]