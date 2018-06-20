---
title: Bibliotecas de Azure para Java
description: Introducción a la administración de Azure y las bibliotecas de servicio para Java
keywords: Azure, Java, SDK, API
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 04/16/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: multiple
ms.assetid: 9aaf22a2-382a-4b13-a8e3-0e467d607207
ms.openlocfilehash: 22a337e928085475e905a271f991147729d97671
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/28/2017
ms.locfileid: "21930881"
---
# <a name="azure-libraries-for-java"></a>Bibliotecas de Azure para Java

Las bibliotecas de Azure para Java le ayudarán a administrar recursos de Azure y conectarse a los servicios desde el código de aplicación. Las bibliotecas están disponibles como [importaciones de Maven](java-sdk-azure-install.md) para su uso en los proyectos de Java. 

## <a name="manage-azure-resources"></a>Administración de recursos de Azure

Cree y administre recursos de Azure desde las aplicaciones Java mediante las [bibliotecas de administración de Azure para Java](java-sdk-azure-get-started.md). Utilice estas bibliotecas para crear sus propios servicios y herramientas de automatización de Azure. 

Por ejemplo, para crear una máquina virtual Linux escribiría el código siguiente:

```java
VirtualMachine linuxVM = azure.virtualMachines().define("myAzureVM")
           .withRegion(region)
           .withExistingResourceGroup("sampleResourceGroup")
           .withNewPrimaryNetwork("10.0.0.0/28")
           .withPrimaryPrivateIpAddressDynamic()
           .withoutPrimaryPublicIpAddress()
           .withPopularLinuxImage(KnownLinuxVirtualMachineImage.UBUNTU_SERVER_16_04_LTS)
           .withRootUsername(userName)
           .withSsh(key)
           .withUnmanagedStorage()
           .withSize(VirtualMachineSizeTypes.STANDARD_D3_V2)
           .create();
 ```

Revise las [instrucciones de instalación](java-sdk-azure-install.md) para obtener una lista completa de las bibliotecas y cómo importarlas en los proyectos y, a continuación, consulte el artículo de [Introducción](java-sdk-azure-get-started.md) para configurar la autenticación y ejecutar código de ejemplo en su propia suscripción de Azure. 

## <a name="connect-to-azure-services"></a>Conexión a los servicios de Azure

Además de utilizar las bibliotecas de Java para crear y administrar recursos en Azure, también puede utilizarlas para conectarse y usar esos recursos en las aplicaciones. Por ejemplo, puede actualizar una tabla de SQL Database o almacenar archivos en Azure Storage. Seleccione la biblioteca que necesita para un servicio determinado en la [lista completa de bibliotecas](java-sdk-azure-install.md) y visite el [Centro para desarrolladores de Java](https://azure.microsoft.com/develop/java/) para ver tutoriales y código de ejemplo para obtener ayuda con ellos en las aplicaciones.

Por ejemplo, para imprimir el contenido de cada blob en un contenedor de Azure Storage:

```java
// get the container from the blob client
CloudBlobContainer container = blobClient.getContainerReference("blobcontainer");

// For each item in the container
for (ListBlobItem blobItem : container.listBlobs()) {
    // If the item is a blob, not a virtual directory
    if (blobItem instanceof CloudBlockBlob) {
        // Download the text
        CloudBlockBlob retrievedBlob = (CloudBlockBlob) blobItem;
        System.out.println(retrievedBlob.downloadText());
    }
}
```

## <a name="sample-code-and-reference"></a>Código de ejemplo y referencia

Los ejemplos siguientes incluyen las tareas comunes de automatización con las bibliotecas de administración de Azure para Java y tienen código listo para usar en sus propias aplicaciones:

- [Máquinas virtuales](java-sdk-azure-virtual-machine-samples.md)
- [Aplicaciones web](java-sdk-azure-web-apps-samples.md)
- [SQL Database](java-sdk-azure-sql-database-samples.md)
   
Hay disponible una [referencia](https://docs.microsoft.com/java/api) para todos los paquetes tanto del servicio como de las bibliotecas de administración. Las nuevas características, cambios importantes e instrucciones de migración desde versiones anteriores están disponibles en las [notas de la versión](java-sdk-azure-release-notes.md).