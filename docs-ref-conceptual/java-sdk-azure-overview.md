---
title: Bibliotecas de Azure para Java
description: Introducción a la administración de Azure y las bibliotecas de servicio para Java
keywords: Azure, Java, SDK, API
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 04/16/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: multiple
ms.assetid: 9aaf22a2-382a-4b13-a8e3-0e467d607207
ms.openlocfilehash: 22a337e928085475e905a271f991147729d97671
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/28/2017
ms.locfileid: "21930881"
---
# <a name="azure-libraries-for-java"></a><span data-ttu-id="904d3-104">Bibliotecas de Azure para Java</span><span class="sxs-lookup"><span data-stu-id="904d3-104">Azure libraries for Java</span></span>

<span data-ttu-id="904d3-105">Las bibliotecas de Azure para Java le ayudarán a administrar recursos de Azure y conectarse a los servicios desde el código de aplicación.</span><span class="sxs-lookup"><span data-stu-id="904d3-105">The Azure libraries for Java help you manage Azure resources and connect to services from your application code.</span></span> <span data-ttu-id="904d3-106">Las bibliotecas están disponibles como [importaciones de Maven](java-sdk-azure-install.md) para su uso en los proyectos de Java.</span><span class="sxs-lookup"><span data-stu-id="904d3-106">The libraries are available as [Maven imports](java-sdk-azure-install.md) for use in your Java projects.</span></span> 

## <a name="manage-azure-resources"></a><span data-ttu-id="904d3-107">Administración de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="904d3-107">Manage Azure resources</span></span>

<span data-ttu-id="904d3-108">Cree y administre recursos de Azure desde las aplicaciones Java mediante las [bibliotecas de administración de Azure para Java](java-sdk-azure-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="904d3-108">Create and manage Azure resources from your Java applications using the [Azure management libraries for Java](java-sdk-azure-get-started.md).</span></span> <span data-ttu-id="904d3-109">Utilice estas bibliotecas para crear sus propios servicios y herramientas de automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="904d3-109">Use these libraries to build your own Azure automation tools and services.</span></span> 

<span data-ttu-id="904d3-110">Por ejemplo, para crear una máquina virtual Linux escribiría el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="904d3-110">For example, to create a Linux VM you would write the following code:</span></span>

```java
VirtualMachine linuxVM = azure.virtualMachines().define("myAzureVM")
           .withRegion(region)
           .withExistingResourceGroup("sampleResourceGroup")
           .withNewPrimaryNetwork("10.0.0.0/28")
           .withPrimaryPrivateIpAddressDynamic()
           .withoutPrimaryPublicIpAddress()
           .withPopularLinuxImage(KnownLinuxVirtualMachineImage.UBUNTU_SERVER_16_04_LTS)
           .withRootUsername(userName)
           .withSsh(key)
           .withUnmanagedStorage()
           .withSize(VirtualMachineSizeTypes.STANDARD_D3_V2)
           .create();
 ```

<span data-ttu-id="904d3-111">Revise las [instrucciones de instalación](java-sdk-azure-install.md) para obtener una lista completa de las bibliotecas y cómo importarlas en los proyectos y, a continuación, consulte el artículo de [Introducción](java-sdk-azure-get-started.md) para configurar la autenticación y ejecutar código de ejemplo en su propia suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="904d3-111">Review the [install instructions](java-sdk-azure-install.md) for a full list of the libraries and how to import them into your projects and then read the [get started article](java-sdk-azure-get-started.md) to set up your authentication and run sample code against your own Azure subscription.</span></span> 

## <a name="connect-to-azure-services"></a><span data-ttu-id="904d3-112">Conexión a los servicios de Azure</span><span class="sxs-lookup"><span data-stu-id="904d3-112">Connect to Azure services</span></span>

<span data-ttu-id="904d3-113">Además de utilizar las bibliotecas de Java para crear y administrar recursos en Azure, también puede utilizarlas para conectarse y usar esos recursos en las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="904d3-113">In addition to using Java libraries to create and manage resources within Azure, you can also use Java libraries to connect  and use those resources in your apps.</span></span> <span data-ttu-id="904d3-114">Por ejemplo, puede actualizar una tabla de SQL Database o almacenar archivos en Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="904d3-114">For example, you might update a table SQL Database or store files in Azure Storage.</span></span> <span data-ttu-id="904d3-115">Seleccione la biblioteca que necesita para un servicio determinado en la [lista completa de bibliotecas](java-sdk-azure-install.md) y visite el [Centro para desarrolladores de Java](https://azure.microsoft.com/develop/java/) para ver tutoriales y código de ejemplo para obtener ayuda con ellos en las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="904d3-115">Select the library you need for a particular service from the [complete list of libraries](java-sdk-azure-install.md) and visit the [Java developer center](https://azure.microsoft.com/develop/java/) for tutorials and sample code for help using them in your apps.</span></span>

<span data-ttu-id="904d3-116">Por ejemplo, para imprimir el contenido de cada blob en un contenedor de Azure Storage:</span><span class="sxs-lookup"><span data-stu-id="904d3-116">For example, to print out the contents of every blob in an Azure storage container:</span></span>

```java
// get the container from the blob client
CloudBlobContainer container = blobClient.getContainerReference("blobcontainer");

// For each item in the container
for (ListBlobItem blobItem : container.listBlobs()) {
    // If the item is a blob, not a virtual directory
    if (blobItem instanceof CloudBlockBlob) {
        // Download the text
        CloudBlockBlob retrievedBlob = (CloudBlockBlob) blobItem;
        System.out.println(retrievedBlob.downloadText());
    }
}
```

## <a name="sample-code-and-reference"></a><span data-ttu-id="904d3-117">Código de ejemplo y referencia</span><span class="sxs-lookup"><span data-stu-id="904d3-117">Sample code and reference</span></span>

<span data-ttu-id="904d3-118">Los ejemplos siguientes incluyen las tareas comunes de automatización con las bibliotecas de administración de Azure para Java y tienen código listo para usar en sus propias aplicaciones:</span><span class="sxs-lookup"><span data-stu-id="904d3-118">The following samples cover common automation tasks with the Azure management libraries for Java and have code ready to use in your own apps:</span></span>

- [<span data-ttu-id="904d3-119">Máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="904d3-119">Virtual machines</span></span>](java-sdk-azure-virtual-machine-samples.md)
- [<span data-ttu-id="904d3-120">Aplicaciones web</span><span class="sxs-lookup"><span data-stu-id="904d3-120">Web apps</span></span>](java-sdk-azure-web-apps-samples.md)
- [<span data-ttu-id="904d3-121">SQL Database</span><span class="sxs-lookup"><span data-stu-id="904d3-121">SQL Database</span></span>](java-sdk-azure-sql-database-samples.md)
   
<span data-ttu-id="904d3-122">Hay disponible una [referencia](https://docs.microsoft.com/java/api) para todos los paquetes tanto del servicio como de las bibliotecas de administración.</span><span class="sxs-lookup"><span data-stu-id="904d3-122">A [reference](https://docs.microsoft.com/java/api) is available for all packages in both the service and management libraries.</span></span> <span data-ttu-id="904d3-123">Las nuevas características, cambios importantes e instrucciones de migración desde versiones anteriores están disponibles en las [notas de la versión](java-sdk-azure-release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="904d3-123">New features, breaking changes, and migration instructions from previous versions are available in the [release notes](java-sdk-azure-release-notes.md).</span></span>