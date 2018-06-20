---
title: Administración de cuentas de Azure Storage con Java | Microsoft Docs
description: Código de ejemplo para administrar cuentas de Azure Storage mediante el SDK de Azure para Java
author: rloutlaw
manager: douge
ms.assetid: 49be8b66-3b56-4c10-8f14-9d326d815cb4
ms.devlang: java
ms.topic: article
ms.service: Azure
ms.technology: Azure
ms.date: 3/30/2017
ms.author: routlaw;asirveda
ms.openlocfilehash: 5945164b2b04e1fa9169590a71f6c5f9f45842d6
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/28/2017
ms.locfileid: "21931061"
---
# <a name="manage-azure-storage-accounts-from-your-java-applications"></a>Administración de cuentas de Azure Storage desde las aplicaciones Java

[Este ejemplo](https://github.com/Azure-Samples/storage-java-manage-storage-accounts) crea una cuenta de [Azure Storage](https://docs.microsoft.com/azure/storage/storage-introduction) y trabaja con las claves de acceso de la cuenta mediante las [bibliotecas de administración para Java](https://github.com/Azure/azure-sdk-for-java). 

## <a name="run-the-sample"></a>Ejecución del ejemplo

Cree un [archivo de autenticación](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) y establezca una variable de entorno `AZURE_AUTH_LOCATION` con la ruta de acceso completa al archivo en el equipo. A continuación, ejecute:

```
git clone https://github.com/Azure-Samples/storage-java-manage-storage-accounts.git
cd storage-java-manage-storage-accounts
mvn clean compile exec:java
```

Vea el [código completo del ejemplo en GitHub](https://github.com/Azure-Samples/storage-java-manage-storage-accounts).

## <a name="authenticate-with-azure"></a>Autenticación con Azure

[!INCLUDE [auth-include](includes/java-auth-include.md)] 

## <a name="create-a-storage-account"></a>Crear una cuenta de almacenamiento

```java
// create a new storage account
StorageAccount storageAccount = azure.storageAccounts().define(storageAccountName)
                    .withRegion(Region.US_EAST)
                    .withNewResourceGroup(rgName)
                    .create();
```

El nombre de almacenamiento proporcionado debe ser único entre todos los nombres de Azure y contener solo letras minúsculas y números. El rendimiento predeterminado y perfil de replicación utilizados para esta cuenta es [Standard_GRS](https://docs.microsoft.com/azure/storage/storage-redundancy#geo-redundant-storage).

## <a name="list-keys-in-a-storage-account"></a>Enumeración de las claves de una cuenta de almacenamiento
```java
// list the name and value for each access key in the storage account
List<StorageAccountKey> storageAccountKeys = storageAccount.getKeys();
for(StorageAccountKey key : storageAccountKeys)    {
    System.out.println("Key name: " + key.keyName() + " with value "+ key.value());
}
```

Se proporcionan dos claves por cada cuenta de Azure Storage, por lo que puede volver a generar una clave mientras sigue permitiendo el acceso al almacenamiento con la otra clave.

## <a name="regenerate-a-key-in-a-storage-account"></a>Regeneración de una clave en una cuenta de almacenamiento

```java
// regenerate the first key in a storage account and return an updated list of keys 
List<StorageAccountKey> updatedStorageAccountKeys =
    storageAccount.regenerateKey(storageAccountKeys.get(0).keyName());
```

Debe actualizar todos los recursos de Azure y las aplicaciones con la nueva clave después de generar una nueva.

## <a name="list-all-storage-accounts-in-a-resource-group"></a>Enumeración de todas las cuentas de almacenamiento en un grupo de recursos
```java
// get a list of accounts in a resource group , log info about each one
List<StorageAccount> accounts = azure.storageAccounts().listByResourceGroup(rgName);
for (StorageAccount sa : accounts) {
    System.out.println("Storage Account " + sa.name() + " created @ " + sa.creationTime());
}
```

[com.microsoft.azure.management.storage.StorageAccount](https://docs.microsoft.com/java/api/com.microsoft.azure.management.storage._storage_account) proporciona un conjunto de métodos útiles para inspeccionar la configuración de una cuenta de almacenamiento.

## <a name="delete-a-storage-account"></a>Eliminar una cuenta de almacenamiento
```java
// delete by ID when you already have a storage account object
azure.storageAccounts().deleteById(storageAccount.id());

// delete by resource group and account name if you don't have an account object
azure.storageAccounts().deleteByResourceGroup(rgName,accountName);
```

> [!NOTE]
> No se pueden quitar cuentas de almacenamiento con imágenes de disco en uso conectadas a máquinas virtuales o discos en uso por otros artefactos con estos métodos. Desconecte el almacenamiento de estos recursos antes de quitar la cuenta.

## <a name="sample-explanation"></a>Explicación del ejemplo

[Código de ejemplo en GitHub](https://github.com/Azure-Samples/storage-java-manage-storage-accounts):

- crea una cuenta de almacenamiento
- lee y vuelve a generar las claves de acceso
- enumera todas las cuentas de almacenamiento de un grupo de recursos
- elimina la cuenta de almacenamiento 

| Clase utilizada en el ejemplo | Notas
|-------|-------|
| [StorageAccount](https://docs.microsoft.com/java/api/com.microsoft.azure.management.storage._storage_account)  | Representación de una cuenta de Azure Storage. Use los métodos de la clase para obtener información acerca de la cuenta de almacenamiento.
| [StorageAccountKey](https://docs.microsoft.com/java/api/com.microsoft.azure.management.storage._storage_account_key) | `StorageAccount.getKeys()` devuelve las claves de la cuenta de almacenamiento. Use los métodos `regenerateKey` de `StorageAccount` para actualizar las claves.

## <a name="next-steps"></a>Pasos siguientes

[!INCLUDE [next-steps](includes/java-next-steps.md)]