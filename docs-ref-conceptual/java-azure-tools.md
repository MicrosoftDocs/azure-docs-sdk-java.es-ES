---
title: Herramientas para desarrolladores de Java de Azure | Microsoft Docs
description: "Integraciones de IDE, emuladores, exploradores de recursos e interfaces de línea de comandos para desarrolladores de Java que trabajan con Azure."
author: rloutlaw
manager: douge
ms.assetid: b55923b7-d60a-460d-b77c-af5fac67f1cc
ms.devlang: java
ms.topic: article
ms.service: Azure
ms.technology: Azure
ms.date: 4/10/2017
ms.author: routlaw;asirveda
ms.openlocfilehash: ce0b003cc7c48c8690f4236547ddec36e6ea9d53
ms.sourcegitcommit: ae39830d5a54fedceac78d8df1718e77741e03fa
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/09/2017
---
# <a name="azure-tools-for-java-developers"></a>Herramientas para desarrolladores de Java de Azure

## <a name="client-and-management-libraries"></a>Bibliotecas de cliente y de administración

Conecte con los servicios y administre los recursos de Azure desde sus aplicaciones con las bibliotecas de Azure para Java. Importe las bibliotecas de administración en los proyectos de Maven agregando esta dependencia al archivo *pom.xml* del proyecto.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure</artifactId>
    <version>1.2.1</version>
</dependency>
```

Consulte la [lista completa de las bibliotecas](java-sdk-azure-install.md) y la [introducción](java-sdk-azure-get-started.md) a las bibliotecas de Azure para Java.

## <a name="eclipse-and-intellij-plugins"></a>Complementos de Eclipse y IntelliJ

Administre los recursos de Azure e implemente aplicaciones desde el IDE con los kits de herramientas de Azure para [Eclipse](eclipse/azure-toolkit-for-eclipse.md) e [IntelliJ](intellij/azure-toolkit-for-intellij.md).   

![Kit de herramientas de IntelliJ que muestra el Explorador de Azure](media/intelliJ-azure-explorer.png)

[Introducción a Azure Toolkit for Eclipse](https://docs.microsoft.com/azure/app-service-web/app-service-web-eclipse-create-hello-world-web-app) | [Introducción a Azure Toolkit for IntelliJ](https://docs.microsoft.com/azure/app-service-web/app-service-web-intellij-create-hello-world-web-app) 

## <a name="azure-cli-20"></a>CLI de Azure 2.0

La CLI de Azure 2.0 proporciona una experiencia de línea de comandos para administrar los recursos de Azure. Puede usarla en el explorador con [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview) o puede [instalarla](https://docs.microsoft.com/cli/azure/install-azure-cli) en macOS, Linux y Windows y ejecutarla desde la línea de comandos.

[Introducción a la CLI de Azure 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli).

## <a name="azure-storage-explorer"></a>Explorador de Azure Storage 

Administre cuentas de Azure Storage, contenedores y blobs o archivos desde el escritorio. El Explorador de Azure Storage está actualmente en versión preliminar y funciona en Windows, Mac OS y Linux.

[Introducción al Explorador de almacenamiento de Azure](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer)