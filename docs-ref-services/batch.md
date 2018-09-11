---
title: Bibliotecas de Azure Batch para Java
description: Documentación de referencia de las bibliotecas de Batch para Java
keywords: Azure, Java, SDK, API, Batch, procesamiento, programación, larga ejecución
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 06/21/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: batch
ms.openlocfilehash: d8e7a6969bf35d98f03c5d3e335fbaf2f6b3a51d
ms.sourcegitcommit: 280d13b43cef94177d95e03879a5919da234a23c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/31/2018
ms.locfileid: "43324362"
---
# <a name="azure-batch-libraries-for-java"></a><span data-ttu-id="e3a18-104">Bibliotecas de Azure Batch para Java</span><span class="sxs-lookup"><span data-stu-id="e3a18-104">Azure Batch libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="e3a18-105">Información general</span><span class="sxs-lookup"><span data-stu-id="e3a18-105">Overview</span></span>

<span data-ttu-id="e3a18-106">[Azure Batch](/azure/batch/batch-technical-overview) permite ejecutar aplicaciones en paralelo a gran escala y de informática de alto rendimiento de manera eficaz en la nube.</span><span class="sxs-lookup"><span data-stu-id="e3a18-106">Run large-scale parallel and high-performance computing applications efficiently in the cloud with [Azure Batch](/azure/batch/batch-technical-overview).</span></span>   

<span data-ttu-id="e3a18-107">Para empezar a trabajar con Azure Batch, consulte [Creación de una cuenta de Batch con Azure Portal](/azure/batch/batch-account-create-portal).</span><span class="sxs-lookup"><span data-stu-id="e3a18-107">To get started with Azure Batch, see [Create a Batch account with the Azure portal](/azure/batch/batch-account-create-portal).</span></span>

## <a name="client-library"></a><span data-ttu-id="e3a18-108">Biblioteca de cliente</span><span class="sxs-lookup"><span data-stu-id="e3a18-108">Client library</span></span>

<span data-ttu-id="e3a18-109">Las bibliotecas de cliente de Azure Batch le permiten configurar nodos de cálculo y grupos, definir tareas y configurarlos para ejecutar trabajos y configurar un administrador de trabajos para controlar y supervisar la ejecución de trabajos.</span><span class="sxs-lookup"><span data-stu-id="e3a18-109">The Azure Batch client libraries let you configure compute nodes and pools, define tasks and configure them to run in jobs, and set up a job manager to control and monitor job execution.</span></span> <span data-ttu-id="e3a18-110">[Obtenga más información](/azure/batch/batch-api-basics) sobre el uso de estos objetos para ejecutar soluciones de proceso en paralelo a gran escala.</span><span class="sxs-lookup"><span data-stu-id="e3a18-110">[Learn more](/azure/batch/batch-api-basics) about using these objects to run large-scale parallel compute solutions.</span></span>

<span data-ttu-id="e3a18-111">[Agregue una dependencia](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) al archivo `pom.xml` de Maven para utilizar la biblioteca de cliente en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="e3a18-111">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span> <span data-ttu-id="e3a18-112">El código fuente de la biblioteca de cliente puede encontrarse en [GitHub](https://github.com/Azure/azure-batch-sdk-for-java).</span><span class="sxs-lookup"><span data-stu-id="e3a18-112">The client library source code can be found in [Github](https://github.com/Azure/azure-batch-sdk-for-java).</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-batch</artifactId>
    <version>4.0.0</version>
</dependency>
```   

### <a name="example"></a><span data-ttu-id="e3a18-113">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="e3a18-113">Example</span></span>

<span data-ttu-id="e3a18-114">Configure un grupo de nodos de proceso de Linux en una cuenta de Batch:</span><span class="sxs-lookup"><span data-stu-id="e3a18-114">Set up a pool of Linux compute nodes in a batch account:</span></span>

```java
// create the batch client for an account using its URI and keys
BatchClient client = BatchClient.open(new BatchSharedKeyCredentials("https://fabrikambatch.eastus.batch.azure.com", "fabrikambatch", batchKey));

// configure a pool of VMs to use 
VirtualMachineConfiguration configuration = new VirtualMachineConfiguration();
configuration.withNodeAgentSKUId("batch.node.ubuntu 16.04");
client.poolOperations().createPool(poolId, poolVMSize, configuration, poolVMCount);
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="e3a18-115">Explorar las API de cliente</span><span class="sxs-lookup"><span data-stu-id="e3a18-115">Explore the Client APIs</span></span>](/java/api/overview/azure/batch/client)


## <a name="management-api"></a><span data-ttu-id="e3a18-116">API de administración</span><span class="sxs-lookup"><span data-stu-id="e3a18-116">Management API</span></span>

<span data-ttu-id="e3a18-117">Use las bibliotecas de administración de Azure Batch para crear y eliminar cuentas de Batch, leer y volver a generar las claves de cuenta de Batch y administrar la cuenta de almacenamiento de Batch.</span><span class="sxs-lookup"><span data-stu-id="e3a18-117">Use the Azure Batch management libraries to create and delete batch accounts, read and regenerate batch account keys, and manage batch account storage.</span></span>

<span data-ttu-id="e3a18-118">[Agregue una dependencia](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) al archivo `pom.xml` de Maven para utilizar la API de administración en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="e3a18-118">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-batch</artifactId>
    <version>1.3.0</version>
</dependency>
```

### <a name="example"></a><span data-ttu-id="e3a18-119">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="e3a18-119">Example</span></span>

<span data-ttu-id="e3a18-120">Cree una cuenta de Azure Batch y configure una nueva aplicación y una cuenta de Azure Storage para ella.</span><span class="sxs-lookup"><span data-stu-id="e3a18-120">Create an Azure Batch account and configure a new application and Azure storage account for it.</span></span>

```java
BatchAccount batchAccount = azure.batchAccounts().define("newBatchAcct")
    .withRegion(Region.US_EAST)
    .withNewResourceGroup("myResourceGroup")
    .defineNewApplication("batchAppName")
        .defineNewApplicationPackage(applicationPackageName)
        .withAllowUpdates(true)
        .withDisplayName(applicationDisplayName)
        .attach()
    .withNewStorageAccount("batchStorageAcct")
    .create();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="e3a18-121">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="e3a18-121">Explore the Management APIs</span></span>](/java/api/overview/azure/batch/management)


## <a name="samples"></a><span data-ttu-id="e3a18-122">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="e3a18-122">Samples</span></span>

<span data-ttu-id="e3a18-123">[Administración de cuentas de Batch][1]</span><span class="sxs-lookup"><span data-stu-id="e3a18-123">[Manage Batch accounts][1]</span></span>   

<span data-ttu-id="e3a18-124">Ver más [código de Java de ejemplo para Azure Batch](https://azure.microsoft.com/resources/samples/?platform=java&term=batch) que puede usar en sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="e3a18-124">Explore more [sample Java code for Azure Batch](https://azure.microsoft.com/resources/samples/?platform=java&term=batch) you can use in your apps.</span></span>

[1]: https://github.com/Azure-Samples/batch-java-manage-batch-accounts
