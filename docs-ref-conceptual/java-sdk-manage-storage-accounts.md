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
# <a name="manage-azure-storage-accounts-from-your-java-applications"></a><span data-ttu-id="8c920-103">Administración de cuentas de Azure Storage desde las aplicaciones Java</span><span class="sxs-lookup"><span data-stu-id="8c920-103">Manage Azure storage accounts from your Java applications</span></span>

<span data-ttu-id="8c920-104">[Este ejemplo](https://github.com/Azure-Samples/storage-java-manage-storage-accounts) crea una cuenta de [Azure Storage](https://docs.microsoft.com/azure/storage/storage-introduction) y trabaja con las claves de acceso de la cuenta mediante las [bibliotecas de administración para Java](https://github.com/Azure/azure-sdk-for-java).</span><span class="sxs-lookup"><span data-stu-id="8c920-104">[This sample](https://github.com/Azure-Samples/storage-java-manage-storage-accounts) creates an [Azure Storage](https://docs.microsoft.com/azure/storage/storage-introduction) account and works with the account access keys using the [Java management libraries](https://github.com/Azure/azure-sdk-for-java).</span></span> 

## <a name="run-the-sample"></a><span data-ttu-id="8c920-105">Ejecución del ejemplo</span><span class="sxs-lookup"><span data-stu-id="8c920-105">Run the sample</span></span>

<span data-ttu-id="8c920-106">Cree un [archivo de autenticación](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) y establezca una variable de entorno `AZURE_AUTH_LOCATION` con la ruta de acceso completa al archivo en el equipo.</span><span class="sxs-lookup"><span data-stu-id="8c920-106">Create an [authentication file](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) and set an environment variable `AZURE_AUTH_LOCATION` with the full path to the file on your computer.</span></span> <span data-ttu-id="8c920-107">A continuación, ejecute:</span><span class="sxs-lookup"><span data-stu-id="8c920-107">Then run:</span></span>

```
git clone https://github.com/Azure-Samples/storage-java-manage-storage-accounts.git
cd storage-java-manage-storage-accounts
mvn clean compile exec:java
```

<span data-ttu-id="8c920-108">Vea el [código completo del ejemplo en GitHub](https://github.com/Azure-Samples/storage-java-manage-storage-accounts).</span><span class="sxs-lookup"><span data-stu-id="8c920-108">View the [complete code sample on GitHub](https://github.com/Azure-Samples/storage-java-manage-storage-accounts).</span></span>

## <a name="authenticate-with-azure"></a><span data-ttu-id="8c920-109">Autenticación con Azure</span><span class="sxs-lookup"><span data-stu-id="8c920-109">Authenticate with Azure</span></span>

[!INCLUDE [auth-include](includes/java-auth-include.md)] 

## <a name="create-a-storage-account"></a><span data-ttu-id="8c920-110">Crear una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="8c920-110">Create a storage account</span></span>

```java
// create a new storage account
StorageAccount storageAccount = azure.storageAccounts().define(storageAccountName)
                    .withRegion(Region.US_EAST)
                    .withNewResourceGroup(rgName)
                    .create();
```

<span data-ttu-id="8c920-111">El nombre de almacenamiento proporcionado debe ser único entre todos los nombres de Azure y contener solo letras minúsculas y números.</span><span class="sxs-lookup"><span data-stu-id="8c920-111">The storage name provided must be unique across all names in Azure and contain only lowercase letters and numbers.</span></span> <span data-ttu-id="8c920-112">El rendimiento predeterminado y perfil de replicación utilizados para esta cuenta es [Standard_GRS](https://docs.microsoft.com/azure/storage/storage-redundancy#geo-redundant-storage).</span><span class="sxs-lookup"><span data-stu-id="8c920-112">The default performance and replication profile used for this account is [Standard_GRS](https://docs.microsoft.com/azure/storage/storage-redundancy#geo-redundant-storage).</span></span>

## <a name="list-keys-in-a-storage-account"></a><span data-ttu-id="8c920-113">Enumeración de las claves de una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="8c920-113">List keys in a storage account</span></span>
```java
// list the name and value for each access key in the storage account
List<StorageAccountKey> storageAccountKeys = storageAccount.getKeys();
for(StorageAccountKey key : storageAccountKeys)    {
    System.out.println("Key name: " + key.keyName() + " with value "+ key.value());
}
```

<span data-ttu-id="8c920-114">Se proporcionan dos claves por cada cuenta de Azure Storage, por lo que puede volver a generar una clave mientras sigue permitiendo el acceso al almacenamiento con la otra clave.</span><span class="sxs-lookup"><span data-stu-id="8c920-114">Two keys are provided in each Azure storage account so that you can regenerate one key while still allowing access to storage using the other key.</span></span>

## <a name="regenerate-a-key-in-a-storage-account"></a><span data-ttu-id="8c920-115">Regeneración de una clave en una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="8c920-115">Regenerate a key in a storage account</span></span>

```java
// regenerate the first key in a storage account and return an updated list of keys 
List<StorageAccountKey> updatedStorageAccountKeys =
    storageAccount.regenerateKey(storageAccountKeys.get(0).keyName());
```

<span data-ttu-id="8c920-116">Debe actualizar todos los recursos de Azure y las aplicaciones con la nueva clave después de generar una nueva.</span><span class="sxs-lookup"><span data-stu-id="8c920-116">You must update all Azure resources and applications with the new key after generating a new one.</span></span>

## <a name="list-all-storage-accounts-in-a-resource-group"></a><span data-ttu-id="8c920-117">Enumeración de todas las cuentas de almacenamiento en un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="8c920-117">List all storage accounts in a resource group</span></span>
```java
// get a list of accounts in a resource group , log info about each one
List<StorageAccount> accounts = azure.storageAccounts().listByResourceGroup(rgName);
for (StorageAccount sa : accounts) {
    System.out.println("Storage Account " + sa.name() + " created @ " + sa.creationTime());
}
```

<span data-ttu-id="8c920-118">[com.microsoft.azure.management.storage.StorageAccount](https://docs.microsoft.com/java/api/com.microsoft.azure.management.storage._storage_account) proporciona un conjunto de métodos útiles para inspeccionar la configuración de una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="8c920-118">[com.microsoft.azure.management.storage.StorageAccount](https://docs.microsoft.com/java/api/com.microsoft.azure.management.storage._storage_account) provides a set of useful methods to inspect the configuration of a storage account.</span></span>

## <a name="delete-a-storage-account"></a><span data-ttu-id="8c920-119">Eliminar una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="8c920-119">Delete a storage account</span></span>
```java
// delete by ID when you already have a storage account object
azure.storageAccounts().deleteById(storageAccount.id());

// delete by resource group and account name if you don't have an account object
azure.storageAccounts().deleteByResourceGroup(rgName,accountName);
```

> [!NOTE]
> <span data-ttu-id="8c920-120">No se pueden quitar cuentas de almacenamiento con imágenes de disco en uso conectadas a máquinas virtuales o discos en uso por otros artefactos con estos métodos.</span><span class="sxs-lookup"><span data-stu-id="8c920-120">Storage accounts with in-use disk images connected to virtual machines or disks in use by other artifacts may not remove with these methods.</span></span> <span data-ttu-id="8c920-121">Desconecte el almacenamiento de estos recursos antes de quitar la cuenta.</span><span class="sxs-lookup"><span data-stu-id="8c920-121">Detach the storage from these resources before removing the account.</span></span>

## <a name="sample-explanation"></a><span data-ttu-id="8c920-122">Explicación del ejemplo</span><span class="sxs-lookup"><span data-stu-id="8c920-122">Sample explanation</span></span>

<span data-ttu-id="8c920-123">[Código de ejemplo en GitHub](https://github.com/Azure-Samples/storage-java-manage-storage-accounts):</span><span class="sxs-lookup"><span data-stu-id="8c920-123">[The sample code on GitHub](https://github.com/Azure-Samples/storage-java-manage-storage-accounts):</span></span>

- <span data-ttu-id="8c920-124">crea una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="8c920-124">creates a storage account</span></span>
- <span data-ttu-id="8c920-125">lee y vuelve a generar las claves de acceso</span><span class="sxs-lookup"><span data-stu-id="8c920-125">reads and regenerates access keys</span></span>
- <span data-ttu-id="8c920-126">enumera todas las cuentas de almacenamiento de un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="8c920-126">lists all storage accounts in a resource group</span></span>
- <span data-ttu-id="8c920-127">elimina la cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="8c920-127">deletes the storage account</span></span> 

| <span data-ttu-id="8c920-128">Clase utilizada en el ejemplo</span><span class="sxs-lookup"><span data-stu-id="8c920-128">Class used in sample</span></span> | <span data-ttu-id="8c920-129">Notas</span><span class="sxs-lookup"><span data-stu-id="8c920-129">Notes</span></span>
|-------|-------|
| [<span data-ttu-id="8c920-130">StorageAccount</span><span class="sxs-lookup"><span data-stu-id="8c920-130">StorageAccount</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.storage._storage_account)  | <span data-ttu-id="8c920-131">Representación de una cuenta de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="8c920-131">Representation of an Azure storage account.</span></span> <span data-ttu-id="8c920-132">Use los métodos de la clase para obtener información acerca de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="8c920-132">Use the methods in the class to get information about the storage account.</span></span>
| [<span data-ttu-id="8c920-133">StorageAccountKey</span><span class="sxs-lookup"><span data-stu-id="8c920-133">StorageAccountKey</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.storage._storage_account_key) | <span data-ttu-id="8c920-134">`StorageAccount.getKeys()` devuelve las claves de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="8c920-134">`StorageAccount.getKeys()` returns the storage account keys.</span></span> <span data-ttu-id="8c920-135">Use los métodos `regenerateKey` de `StorageAccount` para actualizar las claves.</span><span class="sxs-lookup"><span data-stu-id="8c920-135">Use the `regenerateKey` methods in `StorageAccount` to update the keys.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8c920-136">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8c920-136">Next steps</span></span>

[!INCLUDE [next-steps](includes/java-next-steps.md)]