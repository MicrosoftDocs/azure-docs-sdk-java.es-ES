---
title: Bibliotecas de Azure Storage para Java
description: ''
keywords: Azure, Java, SDK, API, Storage
author: douge
ms.author: douge
manager: douge
ms.date: 10/19/2018
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: storage
ms.openlocfilehash: ee54e92ee0084cd2fc5e827764cfe094434ea784
ms.sourcegitcommit: 1c1412ad5d8960975c3fc7fd3d1948152ef651ef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/05/2019
ms.locfileid: "57335378"
---
# <a name="azure-storage-libraries-for-java"></a><span data-ttu-id="a828f-103">Bibliotecas de Azure Storage para Java</span><span class="sxs-lookup"><span data-stu-id="a828f-103">Azure Storage libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="a828f-104">Información general</span><span class="sxs-lookup"><span data-stu-id="a828f-104">Overview</span></span>

<span data-ttu-id="a828f-105">Lea y escriba datos de blobs (objeto), archivos y mensajes desde las aplicaciones Java con [Azure Storage](/azure/storage/storage-introduction).</span><span class="sxs-lookup"><span data-stu-id="a828f-105">Read and write blob (object) data, files, and messages from your Java applications with [Azure Storage](/azure/storage/storage-introduction).</span></span>

<span data-ttu-id="a828f-106">Para empezar a trabajar con Azure Storage, consulte [Uso de Blob Storage desde Java](/azure/storage/blobs/storage-quickstart-blobs-java-v10).</span><span class="sxs-lookup"><span data-stu-id="a828f-106">To get started with Azure Storage, see [How to use Blob storage from Java](/azure/storage/blobs/storage-quickstart-blobs-java-v10).</span></span>

## <a name="client-library"></a><span data-ttu-id="a828f-107">Biblioteca de cliente</span><span class="sxs-lookup"><span data-stu-id="a828f-107">Client library</span></span>

<span data-ttu-id="a828f-108">Use una clave compartida, un token de SAS o un token de OAuth de Azure Active Directory para la autorización con los servicios de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="a828f-108">Use a Shared Key, SAS token or an OAuth token from the Azure Active Directory to authorize with Azure Storage services.</span></span> <span data-ttu-id="a828f-109">A continuación, use las clases y los métodos de las bibliotecas de cliente para trabajar con el almacenamiento de blobs, archivos o colas.</span><span class="sxs-lookup"><span data-stu-id="a828f-109">Then use the client libraries' classes and methods to work with blob, file, or queue storage.</span></span> 

<span data-ttu-id="a828f-110">[Agregue una dependencia](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) al archivo `pom.xml` de Maven para utilizar la biblioteca de cliente en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="a828f-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>   

<span data-ttu-id="a828f-111">**Dependencia para Blob service**:</span><span class="sxs-lookup"><span data-stu-id="a828f-111">**Dependency for Blob service**:</span></span>
```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-storage-blob</artifactId>
    <version>10.1.0</version>
</dependency>
```

<span data-ttu-id="a828f-112">**Dependencia para Queue service**:</span><span class="sxs-lookup"><span data-stu-id="a828f-112">**Dependency for Queue service**:</span></span>
```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-storage-queue</artifactId>
    <version>10.0.0-Preview</version>
</dependency>
```


### <a name="example"></a><span data-ttu-id="a828f-113">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="a828f-113">Example</span></span>

<span data-ttu-id="a828f-114">Escriba un archivo de imagen del sistema de archivos local en un nuevo blob en un contenedor de blobs de Azure Storage existente.</span><span class="sxs-lookup"><span data-stu-id="a828f-114">Write an image file from the local file system into a new blob in an existing Azure Storage blob container.</span></span>


```java
// Retrieve the credentials and initialize SharedKeyCredentials
String accountName = System.getenv("AZURE_STORAGE_ACCOUNT");
String accountKey = System.getenv("AZURE_STORAGE_ACCESS_KEY");

// Create a BlockBlobURL to run operations on Block Blobs. Alternatively create a ServiceURL, or ContainerURL for operations on Blob service, and Blob containers
SharedKeyCredentials creds = new SharedKeyCredentials(accountName, accountKey);

// We are using a default pipeline here, you can learn more about it at https://github.com/Azure/azure-storage-java/wiki/Azure-Storage-Java-V10-Overview
final BlockBlobURL blobURL = new BlockBlobURL(
    new URL("https://" + accountName + ".blob.core.windows.net/mycontainer/myimage.jpg"), 
        StorageURL.createPipeline(creds, new PipelineOptions())
);

AsynchronousFileChannel fileChannel = AsynchronousFileChannel.open(Paths.get("myimage.jpg"));
TransferManager.uploadFileToBlockBlob(fileChannel, blobURL,0, null).blockingGet();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="a828f-115">Explorar las API de cliente</span><span class="sxs-lookup"><span data-stu-id="a828f-115">Explore the Client APIs</span></span>](/java/api/overview/azure/storage/client)

## <a name="management-api"></a><span data-ttu-id="a828f-116">API de administración</span><span class="sxs-lookup"><span data-stu-id="a828f-116">Management API</span></span>

<span data-ttu-id="a828f-117">Cree y administre cuentas y claves de conexión de Azure Storage con la API de administración.</span><span class="sxs-lookup"><span data-stu-id="a828f-117">Create and manage Azure Storage accounts and connection keys with the management API.</span></span>

<span data-ttu-id="a828f-118">[Agregue una dependencia](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) al archivo `pom.xml` de Maven para utilizar la API de administración en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="a828f-118">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-storage</artifactId>
    <version>1.3.0</version>
</dependency
```   

### <a name="example"></a><span data-ttu-id="a828f-119">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="a828f-119">Example</span></span>

<span data-ttu-id="a828f-120">Cree una nueva cuenta de Azure Storage en la suscripción y recupere sus claves de acceso.</span><span class="sxs-lookup"><span data-stu-id="a828f-120">Create a new Azure Storage account in your subscription and retrieve its access keys.</span></span>

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
> [<span data-ttu-id="a828f-121">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="a828f-121">Explore the Management APIs</span></span>](/java/api/overview/azure/storage/management)


## <a name="samples"></a><span data-ttu-id="a828f-122">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="a828f-122">Samples</span></span>

<span data-ttu-id="a828f-123">[SDK de Azure Storage para Java](https://github.com/azure/azure-storage-java)
[Lectura y escritura en objetos en el almacenamiento de blobs](https://github.com/Azure-Samples/storage-blobs-java-v10-quickstart) </span><span class="sxs-lookup"><span data-stu-id="a828f-123">[Azure Storage SDK for Java](https://github.com/azure/azure-storage-java)
[Read and write objects to blob storage](https://github.com/Azure-Samples/storage-blobs-java-v10-quickstart) </span></span>  
[<span data-ttu-id="a828f-124">Lectura y escritura de mensajes con colas</span><span class="sxs-lookup"><span data-stu-id="a828f-124">Read and write messages with queues</span></span>](https://github.com/Azure-Samples/storage-queue-java-getting-started)   
