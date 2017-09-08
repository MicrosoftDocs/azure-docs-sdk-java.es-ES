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
ms.openlocfilehash: 01fe31f2c59810f972875331d49ce5130755c8f2
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/28/2017
---
# <a name="azure-tools-for-java-developers"></a><span data-ttu-id="f4578-103">Herramientas para desarrolladores de Java de Azure</span><span class="sxs-lookup"><span data-stu-id="f4578-103">Azure tools for Java developers</span></span>

## <a name="client-and-management-libraries"></a><span data-ttu-id="f4578-104">Bibliotecas de cliente y de administración</span><span class="sxs-lookup"><span data-stu-id="f4578-104">Client and management libraries</span></span>

<span data-ttu-id="f4578-105">Conecte con los servicios y administre los recursos de Azure desde sus aplicaciones con las bibliotecas de Azure para Java.</span><span class="sxs-lookup"><span data-stu-id="f4578-105">Connect to services and manage Azure resources from your applications with the Azure libraries for Java.</span></span> <span data-ttu-id="f4578-106">Importe las bibliotecas de administración en los proyectos de Maven agregando esta dependencia al archivo *pom.xml* del proyecto.</span><span class="sxs-lookup"><span data-stu-id="f4578-106">Import the management libraries into your Maven projects by adding this dependency to your project *pom.xml*.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure</artifactId>
    <version>1.1.2</version>
</dependency>
```

<span data-ttu-id="f4578-107">Consulte la [lista completa de las bibliotecas](java-sdk-azure-install.md) y la [introducción](java-sdk-azure-get-started.md) a las bibliotecas de Azure para Java.</span><span class="sxs-lookup"><span data-stu-id="f4578-107">View the [complete list of libraries](java-sdk-azure-install.md) and [get started](java-sdk-azure-get-started.md) with the Azure libraries for Java.</span></span>

## <a name="eclipse-and-intellij-plugins"></a><span data-ttu-id="f4578-108">Complementos de Eclipse y IntelliJ</span><span class="sxs-lookup"><span data-stu-id="f4578-108">Eclipse and IntelliJ plugins</span></span>

<span data-ttu-id="f4578-109">Administre los recursos de Azure e implemente aplicaciones desde el IDE con los kits de herramientas de Azure para [Eclipse](https://docs.microsoft.com/azure/azure-toolkit-for-eclipse) e [IntelliJ](https://docs.microsoft.com/azure/azure-toolkit-for-intellij).</span><span class="sxs-lookup"><span data-stu-id="f4578-109">Manage Azure resources and deploy apps from your IDE with The Azure toolkits for [Eclipse](https://docs.microsoft.com/azure/azure-toolkit-for-eclipse) and [IntelliJ](https://docs.microsoft.com/azure/azure-toolkit-for-intellij).</span></span>   

![Kit de herramientas de IntelliJ que muestra el Explorador de Azure](media/intelliJ-azure-explorer.png)

[<span data-ttu-id="f4578-111">Introducción a Azure Toolkit for Eclipse](https://docs.microsoft.com/azure/app-service-web/app-service-web-eclipse-create-hello-world-web-app) | [Introducción a Azure Toolkit for IntelliJ</span><span class="sxs-lookup"><span data-stu-id="f4578-111">Get started with Azure Toolkit for Eclipse](https://docs.microsoft.com/azure/app-service-web/app-service-web-eclipse-create-hello-world-web-app) | [Get started with Azure Toolkit for IntelliJ</span></span>](https://docs.microsoft.com/azure/app-service-web/app-service-web-intellij-create-hello-world-web-app) 

## <a name="azure-cli-20"></a><span data-ttu-id="f4578-112">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="f4578-112">Azure CLI 2.0</span></span>

<span data-ttu-id="f4578-113">La CLI de Azure 2.0 proporciona una experiencia de línea de comandos para administrar los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="f4578-113">The Azure 2.0 CLI provides a command-line experience to manage Azure resources.</span></span> <span data-ttu-id="f4578-114">Puede usarla en el explorador con [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview) o puede [instalarla](https://docs.microsoft.com/cli/azure/install-azure-cli) en macOS, Linux y Windows y ejecutarla desde la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="f4578-114">You can use it in your browser with [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview), or you can [install](https://docs.microsoft.com/cli/azure/install-azure-cli) it on macOS, Linux, and Windows and run it from the command line.</span></span>

<span data-ttu-id="f4578-115">[Introducción a la CLI de Azure 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="f4578-115">[Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli).</span></span>

## <a name="azure-storage-explorer"></a><span data-ttu-id="f4578-116">Explorador de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="f4578-116">Azure Storage Explorer</span></span> 

<span data-ttu-id="f4578-117">Administre cuentas de Azure Storage, contenedores y blobs o archivos desde el escritorio.</span><span class="sxs-lookup"><span data-stu-id="f4578-117">Manage Azure storage accounts, containers, and blobs/files from your desktop.</span></span> <span data-ttu-id="f4578-118">El Explorador de Azure Storage está actualmente en versión preliminar y funciona en Windows, Mac OS y Linux.</span><span class="sxs-lookup"><span data-stu-id="f4578-118">Azure Storage Explorer is currently in Preview and works on Windows, macOS, and Linux.</span></span>

[<span data-ttu-id="f4578-119">Introducción al Explorador de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="f4578-119">Get started with Azure Storage Explorer</span></span>](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer)