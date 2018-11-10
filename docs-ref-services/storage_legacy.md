---
title: Bibliotecas de Azure Storage para Java
description: ''
keywords: Azure, Java, SDK, API, Storage
author: douge
ms.author: seguler
manager: dineshm
ms.date: 10/29/2018
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: storage
ms.openlocfilehash: 68a5fdbf8e2fbfe83f9ea09112d64488e0c11d08
ms.sourcegitcommit: 66f3dd4bdb09712b73c9194e23028567c0c4ee3f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/30/2018
ms.locfileid: "50235256"
---
# <a name="azure-storage-libraries-for-java"></a><span data-ttu-id="4f637-103">Bibliotecas de Azure Storage para Java</span><span class="sxs-lookup"><span data-stu-id="4f637-103">Azure Storage libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="4f637-104">Información general</span><span class="sxs-lookup"><span data-stu-id="4f637-104">Overview</span></span>

<span data-ttu-id="4f637-105">Lea y escriba datos de blobs (objeto), archivos y mensajes desde las aplicaciones Java con [Azure Storage](/azure/storage/storage-introduction).</span><span class="sxs-lookup"><span data-stu-id="4f637-105">Read and write blob (object) data, files, and messages from your Java applications with [Azure Storage](/azure/storage/storage-introduction).</span></span>

<span data-ttu-id="4f637-106">Para empezar a trabajar con Azure Storage, consulte [Uso de Blob Storage desde el SDK v7 para Java](/azure/storage/blobs/storage-quickstart-blobs-java).</span><span class="sxs-lookup"><span data-stu-id="4f637-106">To get started with Azure Storage, see [How to use Blob storage from Java SDK v7](/azure/storage/blobs/storage-quickstart-blobs-java).</span></span>

## <a name="client-library"></a><span data-ttu-id="4f637-107">Biblioteca de cliente</span><span class="sxs-lookup"><span data-stu-id="4f637-107">Client library</span></span>

<span data-ttu-id="4f637-108">Use una clave compartida, un token de SAS o un token de OAuth de Azure Active Directory para la autorización con los servicios de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="4f637-108">Use a Shared Key, SAS token or an OAuth token from the Azure Active Directory to authorize with Azure Storage services.</span></span> <span data-ttu-id="4f637-109">A continuación, use las clases y los métodos de las bibliotecas de cliente para trabajar con el almacenamiento de blobs, archivos o colas.</span><span class="sxs-lookup"><span data-stu-id="4f637-109">Then use the client libraries' classes and methods to work with blob, file, or queue storage.</span></span> 

<span data-ttu-id="4f637-110">[Agregue una dependencia](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) al archivo `pom.xml` de Maven para utilizar la biblioteca de cliente en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="4f637-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>   

<span data-ttu-id="4f637-111">**Dependencia del SDK v7 de Azure Storage**:</span><span class="sxs-lookup"><span data-stu-id="4f637-111">**Dependency for the legacy Azure Storage SDK v7**:</span></span>
```XML
<!-- https://mvnrepository.com/artifact/com.microsoft.azure/azure-storage -->
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-storage</artifactId>
    <version>8.0.0</version>
</dependency>
```

### <a name="example"></a><span data-ttu-id="4f637-112">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="4f637-112">Example</span></span>

<span data-ttu-id="4f637-113">Escriba un archivo de imagen del sistema de archivos local en un nuevo blob en un contenedor de blobs de Azure Storage existente.</span><span class="sxs-lookup"><span data-stu-id="4f637-113">Write an image file from the local file system into a new blob in an existing Azure Storage blob container.</span></span>


```java
// Parse the connection string and create a blob client to interact with Blob storage
CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);
CloudBlobClient blobClient = storageAccount.createCloudBlobClient();
CloudBlobContainer container = blobClient.getContainerReference("quickstartcontainer");

// Create the container if it does not exist with public access.
container.createIfNotExists(BlobContainerPublicAccessType.CONTAINER, new BlobRequestOptions(), new OperationContext());         
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="4f637-114">Explorar las API de cliente</span><span class="sxs-lookup"><span data-stu-id="4f637-114">Explore the Client APIs</span></span>](/java/api/overview/azure/storage/client)

## <a name="management-api"></a><span data-ttu-id="4f637-115">API de administración</span><span class="sxs-lookup"><span data-stu-id="4f637-115">Management API</span></span>

<span data-ttu-id="4f637-116">Cree y administre cuentas de Azure Storage y claves de conexión con la API de administración.</span><span class="sxs-lookup"><span data-stu-id="4f637-116">Crete and manage Azure Storage accounts and connection keys with the management API.</span></span>

<span data-ttu-id="4f637-117">[Agregue una dependencia](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) al archivo `pom.xml` de Maven para utilizar la API de administración en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="4f637-117">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-storage</artifactId>
    <version>1.3.0</version>
</dependency
```   

### <a name="example"></a><span data-ttu-id="4f637-118">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="4f637-118">Example</span></span>

<span data-ttu-id="4f637-119">Cree una nueva cuenta de Azure Storage en la suscripción y recupere sus claves de acceso.</span><span class="sxs-lookup"><span data-stu-id="4f637-119">Create a new Azure Storage account in your subscription and retrieve its access keys.</span></span>

```java
StorageAccount storageAccount = azure.storageAccounts().define(storageAccountName)
        .withRegion(Region.US_EAST)
        .withNewResourceGroup(rgName)
        .create();

// get a list of storage account keys related to the account
List<StorageAccountKey> storageAccountKeys = storageAccount.getKeys();
for(StorageAccountKey key : storageAccountKeys)    {
    System.out.println("Key name: " + key.keyName() + " with value "+ key.value());
}
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="4f637-120">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="4f637-120">Explore the Management APIs</span></span>](/java/api/overview/azure/storage/management)


## <a name="samples"></a><span data-ttu-id="4f637-121">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="4f637-121">Samples</span></span>

<span data-ttu-id="4f637-122">[SDK de Azure Storage para Java](https://github.com/azure/azure-storage-java)
[Lectura y escritura en objetos en el almacenamiento de blobs](https://github.com/Azure-Samples/storage-blobs-java-v10-quickstart) </span><span class="sxs-lookup"><span data-stu-id="4f637-122">[Azure Storage SDK for Java](https://github.com/azure/azure-storage-java)
[Read and write objects to blob storage](https://github.com/Azure-Samples/storage-blobs-java-v10-quickstart) </span></span>  
[<span data-ttu-id="4f637-123">Lectura y escritura de mensajes con colas</span><span class="sxs-lookup"><span data-stu-id="4f637-123">Read and write messages with queues</span></span>](https://github.com/Azure-Samples/storage-queue-java-getting-started)   
