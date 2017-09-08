---
title: Bibliotecas de Azure Virtual Machines para Java
description: 
keywords: "Azure, Java, SDK, API, proceso, máquinas virtuales"
author: douge
ms.author: douge
manager: douge
ms.date: 05/17/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: compute
ms.openlocfilehash: 58016d4eef7d6548b2bd5302abcebf78f9cd7bcf
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/28/2017
---
# <a name="azure-virtual-machine-libraries"></a><span data-ttu-id="ebcdc-103">Bibliotecas de Azure Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="ebcdc-103">Azure virtual machine libraries</span></span>

## <a name="overview"></a><span data-ttu-id="ebcdc-104">Información general</span><span class="sxs-lookup"><span data-stu-id="ebcdc-104">Overview</span></span>

<span data-ttu-id="ebcdc-105">Recursos informáticos bajo demanda y escalables que se ejecutan en Linux o Windows.</span><span class="sxs-lookup"><span data-stu-id="ebcdc-105">On-demand, scalable computing resources running Linux or Windows.</span></span>

<span data-ttu-id="ebcdc-106">Para empezar a trabajar con Azure Virtual Machines, consulte [Creación de una máquina virtual Linux con Azure Portal](/azure/virtual-machines/linux/quick-create-portal).</span><span class="sxs-lookup"><span data-stu-id="ebcdc-106">To get started with Azure virtual machines, see [Create a Linux virtual machine with the Azure portal](/azure/virtual-machines/linux/quick-create-portal).</span></span>

## <a name="management-api"></a><span data-ttu-id="ebcdc-107">API de administración</span><span class="sxs-lookup"><span data-stu-id="ebcdc-107">Management API</span></span>

<span data-ttu-id="ebcdc-108">Cree, configure y escale horizontalmente máquinas virtuales Windows y Linux de Azure desde código con la API de administración.</span><span class="sxs-lookup"><span data-stu-id="ebcdc-108">Create, configure, and scale out Windows and Linux virtual machines in Azure from your code with the management API.</span></span>

<span data-ttu-id="ebcdc-109">[Agregue una dependencia](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) al archivo `pom.xml` de Maven para utilizar la API de administración en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="ebcdc-109">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-compute</artifactId>
    <version>1.1.2</version>
</dependency>
```   


## <a name="example"></a><span data-ttu-id="ebcdc-110">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="ebcdc-110">Example</span></span>

<span data-ttu-id="ebcdc-111">Cree una nueva máquina virtual Linux en un nuevo grupo de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="ebcdc-111">Create a new Linux virtual machine in a new Azure resource group.</span></span>

```java
VirtualMachine newLinuxVm = azure.virtualMachines().define(linuxVmName)
            .withRegion(Region.US_EAST)
            .withNewResourceGroup("myResourceGroup")
            .withNewPrimaryNetwork("10.0.0.0/28")
            .withPrimaryPrivateIpAddressDynamic()
            .withoutPrimaryPublicIpAddress()
            .withPopularLinuxImage(KnownLinuxVirtualMachineImage.UBUNTU_SERVER_16_04_LTS)
            .withRootUsername(userName)
            .withSshKey(key)
            .withSize(VirtualMachineSizeTypes.STANDARD_D3_V2)
            .create();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="ebcdc-112">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="ebcdc-112">Explore the Management APIs</span></span>](/java/api/overview/azure/virtualmachines/managementapi)


## <a name="samples"></a><span data-ttu-id="ebcdc-113">Muestras</span><span class="sxs-lookup"><span data-stu-id="ebcdc-113">Samples</span></span>

<span data-ttu-id="ebcdc-114">[Administración de máquinas virtuales][1] </span><span class="sxs-lookup"><span data-stu-id="ebcdc-114">[Manage virtual machines][1] </span></span>  
<span data-ttu-id="ebcdc-115">[Administración de redes virtuales][6] </span><span class="sxs-lookup"><span data-stu-id="ebcdc-115">[Manage virtual networks][6] </span></span>  
<span data-ttu-id="ebcdc-116">[Creación de una máquina virtual desde una imagen personalizada][2] </span><span class="sxs-lookup"><span data-stu-id="ebcdc-116">[Create a virtual machine from a custom image][2] </span></span>  
<span data-ttu-id="ebcdc-117">[Creación de máquinas virtuales en varias regiones en paralelo][5]  </span><span class="sxs-lookup"><span data-stu-id="ebcdc-117">[Create virtual machines across regions in parallel][5]  </span></span>  
<span data-ttu-id="ebcdc-118">[Creación de un conjunto de escalado de máquinas virtuales con un equilibrador de carga][7]</span><span class="sxs-lookup"><span data-stu-id="ebcdc-118">[Create a virtual machine scale set with a load balancer][7]</span></span>    

[1]: ../docs-ref-conceptual/java-sdk-manage-virtual-machines.md
[2]: https://azure.microsoft.com/resources/samples/managed-disk-java-create-virtual-machine-using-custom-image/
[5]: ../docs-ref-conceptual/java-sdk-virtual-machines-in-parallel.md
[6]: ../docs-ref-conceptual/java-sdk-manage-virtual-networks.md
[7]: ../docs-ref-conceptual/java-sdk-manage-vm-scalesets.md

<span data-ttu-id="ebcdc-119">Ver más [código de Java de ejemplo para Azure Virtual Machines](https://azure.microsoft.com/resources/samples/?platform=java&term=VM) que puede usar en las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="ebcdc-119">Explore more [sample Java code for Azure virtual machines](https://azure.microsoft.com/resources/samples/?platform=java&term=VM) you can use in your apps.</span></span>