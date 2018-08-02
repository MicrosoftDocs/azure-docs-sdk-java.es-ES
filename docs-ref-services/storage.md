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
ms.sourcegitcommit: 49b17bbf34732512f836ee634818f1058147ff5c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
ms.locfileid: "31823658"
---
# <a name="azure-storage-libraries-for-java"></a>Bibliotecas de Azure Storage para Java

## <a name="overview"></a>Información general

Lea y escriba archivos, datos de blob (objeto), pares de clave-valor y mensajes desde las aplicaciones Java con [Azure Storage](/azure/storage/storage-introduction).

Para empezar a trabajar con Azure Storage, consulte [Uso de Blob Storage desde Java](/azure/storage/storage-java-how-to-use-blob-storage).

## <a name="client-library"></a>Biblioteca de cliente

Use [cadenas de conexión](/azure/storage/storage-create-storage-account#manage-your-storage-account) para conectarse a una cuenta de Azure Storage y, a continuación, use las clases y los métodos de las bibliotecas de cliente para trabajar con almacenamiento de blobs, tablas, archivos o colas. 

[Agregue una dependencia](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) al archivo `pom.xml` de Maven para utilizar la biblioteca de cliente en el proyecto.   

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-storage</artifactId>
    <version>7.0.0</version>
</dependency>
```   

### <a name="example"></a>Ejemplo

Escriba un archivo de imagen a partir del sistema de archivos local en un nuevo blob en un contenedor de blobs de Azure Storage existente.


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

[Administración de cuentas de Azure Storage](../docs-ref-conceptual/java-sdk-manage-storage-accounts.md)    
[Leer y escribir objetos en almacenamiento de blobs](https://github.com/Azure-Samples/storage-blob-java-getting-started)   
[Leer y escribir mensajes con colas](https://github.com/Azure-Samples/storage-queue-java-getting-started)   
[Leer archivos de almacenamiento de blobs en una aplicación web](https://github.com/Azure-Samples/app-service-java-manage-storage-connections-for-web-apps-on-linux)

Ver más [código de Java de ejemplo para Azure Storage](https://azure.microsoft.com/resources/samples/?platform=java&term=storage) que puede usar en sus aplicaciones.
