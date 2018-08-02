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
ms.openlocfilehash: 67381d68d23f98579a472aefbebaa929af622b8d
ms.sourcegitcommit: 49b17bbf34732512f836ee634818f1058147ff5c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
ms.locfileid: "31823598"
---
# <a name="azure-batch-libraries-for-java"></a>Bibliotecas de Azure Batch para Java

## <a name="overview"></a>Información general

[Azure Batch](/azure/batch/batch-technical-overview) permite ejecutar aplicaciones en paralelo a gran escala y de informática de alto rendimiento de manera eficaz en la nube.   

Para empezar a trabajar con Azure Batch, consulte [Creación de una cuenta de Batch con Azure Portal](/azure/batch/batch-account-create-portal).

## <a name="client-library"></a>Biblioteca de cliente

Las bibliotecas de cliente de Azure Batch le permiten configurar nodos de cálculo y grupos, definir tareas y configurarlos para ejecutar trabajos y configurar un administrador de trabajos para controlar y supervisar la ejecución de trabajos. [Obtenga más información](/azure/batch/batch-api-basics) sobre el uso de estos objetos para ejecutar soluciones de proceso en paralelo a gran escala.

[Agregue una dependencia](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) al archivo `pom.xml` de Maven para utilizar la biblioteca de cliente en el proyecto.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-batch</artifactId>
    <version>2.0.0</version>
</dependency>
```   

### <a name="example"></a>Ejemplo

Configure un grupo de nodos de proceso de Linux en una cuenta de Batch:

```java
// create the batch client for an account using its URI and keys
BatchClient client = BatchClient.open(new BatchSharedKeyCredentials("https://fabrikambatch.eastus.batch.azure.com", "fabrikambatch", batchKey));

// configure a pool of VMs to use 
VirtualMachineConfiguration configuration = new VirtualMachineConfiguration();
configuration.withNodeAgentSKUId("batch.node.ubuntu 16.04");
client.poolOperations().createPool(poolId, poolVMSize, configuration, poolVMCount);
```

> [!div class="nextstepaction"]
> [Explorar las API de cliente](/java/api/overview/azure/batch/client)


## <a name="management-api"></a>API de administración

Use las bibliotecas de administración de Azure Batch para crear y eliminar cuentas de Batch, leer y volver a generar las claves de cuenta de Batch y administrar la cuenta de almacenamiento de Batch.

[Agregue una dependencia](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) al archivo `pom.xml` de Maven para utilizar la API de administración en el proyecto.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-batch</artifactId>
    <version>1.3.0</version>
</dependency>
```

### <a name="example"></a>Ejemplo

Cree una cuenta de Azure Batch y configure una nueva aplicación y una cuenta de Azure Storage para ella.

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
> [Explorar las API de administración](/java/api/overview/azure/batch/management)


## <a name="samples"></a>Ejemplos

[Administración de cuentas de Batch][1]   

Ver más [código de Java de ejemplo para Azure Batch](https://azure.microsoft.com/resources/samples/?platform=java&term=batch) que puede usar en sus aplicaciones.

[1]: https://github.com/Azure-Samples/batch-java-manage-batch-accounts