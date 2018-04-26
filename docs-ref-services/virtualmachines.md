---
title: Bibliotecas de Azure Virtual Machines para Java
description: ''
keywords: Azure, Java, SDK, API, Compute, Virtual Machines
author: douge
ms.author: douge
manager: douge
ms.date: 05/17/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: compute
ms.openlocfilehash: a54bc40e1d28ba6ee1d8b0638cb259adbb69d78d
ms.sourcegitcommit: 49b17bbf34732512f836ee634818f1058147ff5c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="azure-virtual-machine-libraries"></a><span data-ttu-id="66b65-103">Bibliotecas de Azure Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="66b65-103">Azure virtual machine libraries</span></span>

## <a name="overview"></a><span data-ttu-id="66b65-104">Información general</span><span class="sxs-lookup"><span data-stu-id="66b65-104">Overview</span></span>

<span data-ttu-id="66b65-105">Recursos informáticos bajo demanda y escalables que se ejecutan en Linux o Windows.</span><span class="sxs-lookup"><span data-stu-id="66b65-105">On-demand, scalable computing resources running Linux or Windows.</span></span>

<span data-ttu-id="66b65-106">Para empezar a trabajar con Azure Virtual Machines, consulte [Creación de una máquina virtual Linux con Azure Portal](/azure/virtual-machines/linux/quick-create-portal).</span><span class="sxs-lookup"><span data-stu-id="66b65-106">To get started with Azure virtual machines, see [Create a Linux virtual machine with the Azure portal](/azure/virtual-machines/linux/quick-create-portal).</span></span>

## <a name="management-api"></a><span data-ttu-id="66b65-107">API de administración</span><span class="sxs-lookup"><span data-stu-id="66b65-107">Management API</span></span>

<span data-ttu-id="66b65-108">Cree, configure y escale horizontalmente máquinas virtuales Windows y Linux de Azure desde código con la API de administración.</span><span class="sxs-lookup"><span data-stu-id="66b65-108">Create, configure, and scale out Windows and Linux virtual machines in Azure from your code with the management API.</span></span>

<span data-ttu-id="66b65-109">[Agregue una dependencia](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) al archivo `pom.xml` de Maven para utilizar la API de administración en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="66b65-109">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-compute</artifactId>
    <version>1.3.0</version>
</dependency>
```   


## <a name="example"></a><span data-ttu-id="66b65-110">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="66b65-110">Example</span></span>

<span data-ttu-id="66b65-111">Cree una nueva máquina virtual Linux en un nuevo grupo de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="66b65-111">Create a new Linux virtual machine in a new Azure resource group.</span></span>

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
> [<span data-ttu-id="66b65-112">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="66b65-112">Explore the Management APIs</span></span>](/java/api/overview/azure/virtualmachines/management)


## <a name="samples"></a><span data-ttu-id="66b65-113">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="66b65-113">Samples</span></span>

<span data-ttu-id="66b65-114">[Administración de máquinas virtuales][1] </span><span class="sxs-lookup"><span data-stu-id="66b65-114">[Manage virtual machines][1] </span></span>  
<span data-ttu-id="66b65-115">[Administración de redes virtuales][6] </span><span class="sxs-lookup"><span data-stu-id="66b65-115">[Manage virtual networks][6] </span></span>  
<span data-ttu-id="66b65-116">[Creación de una máquina virtual desde una imagen personalizada][2] </span><span class="sxs-lookup"><span data-stu-id="66b65-116">[Create a virtual machine from a custom image][2] </span></span>  
<span data-ttu-id="66b65-117">[Creación de máquinas virtuales en varias regiones en paralelo][5]  </span><span class="sxs-lookup"><span data-stu-id="66b65-117">[Create virtual machines across regions in parallel][5]  </span></span>  
<span data-ttu-id="66b65-118">[Creación de un conjunto de escalado de máquinas virtuales con un equilibrador de carga][7]</span><span class="sxs-lookup"><span data-stu-id="66b65-118">[Create a virtual machine scale set with a load balancer][7]</span></span>    

[1]: ../docs-ref-conceptual/java-sdk-manage-virtual-machines.md
[2]: https://azure.microsoft.com/resources/samples/managed-disk-java-create-virtual-machine-using-custom-image/
[5]: ../docs-ref-conceptual/java-sdk-virtual-machines-in-parallel.md
[6]: ../docs-ref-conceptual/java-sdk-manage-virtual-networks.md
[7]: ../docs-ref-conceptual/java-sdk-manage-vm-scalesets.md

<span data-ttu-id="66b65-119">Ver más [código de Java de ejemplo para Azure Virtual Machines](https://azure.microsoft.com/resources/samples/?platform=java&term=VM) que puede usar en las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="66b65-119">Explore more [sample Java code for Azure virtual machines](https://azure.microsoft.com/resources/samples/?platform=java&term=VM) you can use in your apps.</span></span>