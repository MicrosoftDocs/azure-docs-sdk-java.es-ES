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
# <a name="azure-storage-libraries-for-java"></a>Bibliotecas de Azure Storage para Java

## <a name="overview"></a>Información general

Lea y escriba datos de blobs (objeto), archivos y mensajes desde las aplicaciones Java con [Azure Storage](/azure/storage/storage-introduction).

Para empezar a trabajar con Azure Storage, consulte [Uso de Blob Storage desde Java](/azure/storage/blobs/storage-quickstart-blobs-java-v10).

## <a name="client-library"></a>Biblioteca de cliente

Use una clave compartida, un token de SAS o un token de OAuth de Azure Active Directory para la autorización con los servicios de Azure Storage. A continuación, use las clases y los métodos de las bibliotecas de cliente para trabajar con el almacenamiento de blobs, archivos o colas. 

[Agregue una dependencia](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) al archivo `pom.xml` de Maven para utilizar la biblioteca de cliente en el proyecto.   

**Dependencia para Blob service**:
```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-storage-blob</artifactId>
    <version>10.1.0</version>
</dependency>
```

**Dependencia para Queue service**:
```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-storage-queue</artifactId>
    <version>10.0.0-Preview</version>
</dependency>
```


### <a name="example"></a>Ejemplo

Escriba un archivo de imagen del sistema de archivos local en un nuevo blob en un contenedor de blobs de Azure Storage existente.


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
> [Explorar las API de cliente](/java/api/overview/azure/storage/client)

## <a name="management-api"></a>API de administración

Cree y administre cuentas y claves de conexión de Azure Storage con la API de administración.

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
