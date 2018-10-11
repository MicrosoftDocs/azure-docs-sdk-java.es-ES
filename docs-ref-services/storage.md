---
title: Bibliotecas de Azure Storage para Java
description: ''
keywords: Azure, Java, SDK, API, Storage
author: douge
ms.author: douge
manager: douge
ms.date: 02/07/2018
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: storage
ms.openlocfilehash: ec06e79374176b5a4795d27c5fbbb2260e65cd8c
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/09/2018
ms.locfileid: "48893596"
---
# <a name="azure-storage-libraries-for-java"></a><span data-ttu-id="8d099-103">Bibliotecas de Azure Storage para Java</span><span class="sxs-lookup"><span data-stu-id="8d099-103">Azure Storage libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="8d099-104">Información general</span><span class="sxs-lookup"><span data-stu-id="8d099-104">Overview</span></span>

<span data-ttu-id="8d099-105">Lea y escriba archivos, datos de blob (objeto), pares de clave-valor y mensajes desde las aplicaciones Java con [Azure Storage](/azure/storage/storage-introduction).</span><span class="sxs-lookup"><span data-stu-id="8d099-105">Read and write files, blob (object) data, key-value pairs, and messages from your Java applications with [Azure Storage](/azure/storage/storage-introduction).</span></span>

<span data-ttu-id="8d099-106">Para empezar a trabajar con Azure Storage, consulte [Uso de Blob Storage desde Java](/azure/storage/storage-java-how-to-use-blob-storage).</span><span class="sxs-lookup"><span data-stu-id="8d099-106">To get started with Azure Storage, see [How to use Blob storage from Java](/azure/storage/storage-java-how-to-use-blob-storage).</span></span>

## <a name="client-library"></a><span data-ttu-id="8d099-107">Biblioteca de cliente</span><span class="sxs-lookup"><span data-stu-id="8d099-107">Client library</span></span>

<span data-ttu-id="8d099-108">Use [cadenas de conexión](/azure/storage/storage-create-storage-account#manage-your-storage-account) para conectarse a una cuenta de Azure Storage y, a continuación, use las clases y los métodos de las bibliotecas de cliente para trabajar con almacenamiento de blobs, tablas, archivos o colas.</span><span class="sxs-lookup"><span data-stu-id="8d099-108">Use [connection strings](/azure/storage/storage-create-storage-account#manage-your-storage-account) to connect to an Azure Storage account, then use the client libraries' classes and methods to work with blob, table, file, or queue storage.</span></span> 

<span data-ttu-id="8d099-109">[Agregue una dependencia](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) al archivo `pom.xml` de Maven para utilizar la biblioteca de cliente en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="8d099-109">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>   

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-storage</artifactId>
    <version>7.0.0</version>
</dependency>
```   

### <a name="example"></a><span data-ttu-id="8d099-110">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="8d099-110">Example</span></span>

<span data-ttu-id="8d099-111">Escriba un archivo de imagen a partir del sistema de archivos local en un nuevo blob en un contenedor de blobs de Azure Storage existente.</span><span class="sxs-lookup"><span data-stu-id="8d099-111">Write a image file from the local file system into a new blob in an existing Azure Storage blob container.</span></span>


```java
String storageConnectionString = "DefaultEndpointsProtocol=https;" + 
"AccountName=fabrikamblobstorage;" + 
"AccountKey=keyvalue;EndpointSuffix=core.windows.net";

CloudStorageAccount account = CloudStorageAccount.parse(storageConnectionString);
CloudBlobClient serviceClient = account.createCloudBlobClient();
CloudBlobContainer container = serviceClient.getContainerReference(blobContainer);

// write a blob from a local filesystem path to the container as logo.png
CloudBlockBlob blob = container.getBlockBlobReference("logo.png");
blob.uploadFromFile("/Users/raisa/fabrikam.png");
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="8d099-112">Explorar las API de cliente</span><span class="sxs-lookup"><span data-stu-id="8d099-112">Explore the Client APIs</span></span>](/java/api/overview/azure/storage/client)

## <a name="management-api"></a><span data-ttu-id="8d099-113">API de administración</span><span class="sxs-lookup"><span data-stu-id="8d099-113">Management API</span></span>

<span data-ttu-id="8d099-114">Cree y administre cuentas de Azure Storage y claves de conexión con la API de administración.</span><span class="sxs-lookup"><span data-stu-id="8d099-114">Crete and manage Azure Storage accounts and connection keys with the management API.</span></span>

<span data-ttu-id="8d099-115">[Agregue una dependencia](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) al archivo `pom.xml` de Maven para utilizar la API de administración en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="8d099-115">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-storage</artifactId>
    <version>1.3.0</version>
</dependency
```   

### <a name="example"></a><span data-ttu-id="8d099-116">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="8d099-116">Example</span></span>

<span data-ttu-id="8d099-117">Cree una nueva cuenta de Azure Storage en la suscripción y recupere sus claves de acceso.</span><span class="sxs-lookup"><span data-stu-id="8d099-117">Create a new Azure Storage account in your subscription and retrieve its access keys.</span></span>

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
> [<span data-ttu-id="8d099-118">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="8d099-118">Explore the Management APIs</span></span>](/java/api/overview/azure/storage/management)


## <a name="samples"></a><span data-ttu-id="8d099-119">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="8d099-119">Samples</span></span>

<span data-ttu-id="8d099-120">[Administración de cuentas de Azure Storage](../docs-ref-conceptual/java-sdk-manage-storage-accounts.md)  </span><span class="sxs-lookup"><span data-stu-id="8d099-120">[Manage Azure Storage accounts](../docs-ref-conceptual/java-sdk-manage-storage-accounts.md)  </span></span>  
<span data-ttu-id="8d099-121">[Leer y escribir objetos en almacenamiento de blobs](https://github.com/Azure-Samples/storage-blob-java-getting-started) </span><span class="sxs-lookup"><span data-stu-id="8d099-121">[Read and write objects to blob storage](https://github.com/Azure-Samples/storage-blob-java-getting-started) </span></span>  
<span data-ttu-id="8d099-122">[Leer y escribir mensajes con colas](https://github.com/Azure-Samples/storage-queue-java-getting-started) </span><span class="sxs-lookup"><span data-stu-id="8d099-122">[Read and write messages with queues](https://github.com/Azure-Samples/storage-queue-java-getting-started) </span></span>  
[<span data-ttu-id="8d099-123">Leer archivos de almacenamiento de blobs en una aplicación web</span><span class="sxs-lookup"><span data-stu-id="8d099-123">Read files from blob storage in a web app</span></span>](https://github.com/Azure-Samples/app-service-java-manage-storage-connections-for-web-apps-on-linux)

<span data-ttu-id="8d099-124">Ver más [código de Java de ejemplo para Azure Storage](https://azure.microsoft.com/resources/samples/?platform=java&term=storage) que puede usar en sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="8d099-124">Explore more [sample Java code for Azure Storage](https://azure.microsoft.com/resources/samples/?platform=java&term=storage) you can use in your apps.</span></span>
