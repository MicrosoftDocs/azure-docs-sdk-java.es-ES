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
# <a name="azure-storage-libraries-for-java"></a>Bibliotecas de Azure Storage para Java

## <a name="overview"></a>Información general

Lea y escriba datos de blobs (objeto), archivos y mensajes desde las aplicaciones Java con [Azure Storage](/azure/storage/storage-introduction).

Para empezar a trabajar con Azure Storage, consulte [Uso de Blob Storage desde el SDK v7 para Java](/azure/storage/blobs/storage-quickstart-blobs-java).

## <a name="client-library"></a>Biblioteca de cliente

Use una clave compartida, un token de SAS o un token de OAuth de Azure Active Directory para la autorización con los servicios de Azure Storage. A continuación, use las clases y los métodos de las bibliotecas de cliente para trabajar con el almacenamiento de blobs, archivos o colas. 

[Agregue una dependencia](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) al archivo `pom.xml` de Maven para utilizar la biblioteca de cliente en el proyecto.   

**Dependencia del SDK v7 de Azure Storage**:
```XML
<!-- https://mvnrepository.com/artifact/com.microsoft.azure/azure-storage -->
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-storage</artifactId>
    <version>8.0.0</version>
</dependency>
```

### <a name="example"></a>Ejemplo

Escriba un archivo de imagen del sistema de archivos local en un nuevo blob en un contenedor de blobs de Azure Storage existente.


```java
// Parse the connection string and create a blob client to interact with Blob storage
CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);
CloudBlobClient blobClient = storageAccount.createCloudBlobClient();
CloudBlobContainer container = blobClient.getContainerReference("quickstartcontainer");

// Create the container if it does not exist with public access.
container.createIfNotExists(BlobContainerPublicAccessType.CONTAINER, new BlobRequestOptions(), new OperationContext());         
```

> [!div class="nextstepaction"]
> [Explorar las API de cliente](/java/api/overview/azure/storage/client)

## <a name="management-api"></a>API de administración

Cree y administre cuentas de Azure Storage y claves de conexión con la API de administración.

[Agregue una dependencia](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) al archivo `pom.xml` de Maven para utilizar la API de administración en el proyecto.  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-storage</artifactId>
    <version>1.3.0</version>
</dependency
```   

### <a name="example"></a>Ejemplo

Cree una nueva cuenta de Azure Storage en la suscripción y recupere sus claves de acceso.

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
> [Explorar las API de administración](/java/api/overview/azure/storage/management)


## <a name="samples"></a>Ejemplos

[SDK de Azure Storage para Java](https://github.com/azure/azure-storage-java)
[Lectura y escritura en objetos en el almacenamiento de blobs](https://github.com/Azure-Samples/storage-blobs-java-v10-quickstart)   
[Lectura y escritura de mensajes con colas](https://github.com/Azure-Samples/storage-queue-java-getting-started)   
