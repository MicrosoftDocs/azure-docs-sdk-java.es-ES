---
title: Herramientas para desarrolladores de Java de Azure | Microsoft Docs
description: Integraciones de IDE, emuladores, exploradores de recursos e interfaces de línea de comandos para desarrolladores de Java que trabajan con Azure.
author: rloutlaw
manager: douge
ms.assetid: b55923b7-d60a-460d-b77c-af5fac67f1cc
ms.devlang: java
ms.topic: article
ms.service: Azure
ms.technology: Azure
ms.date: 11/13/2018
ms.author: routlaw
ms.openlocfilehash: 9e9828540ddc678f69eab11f5a61eef8bf8e916c
ms.sourcegitcommit: 8d0c59ae7c91adbb9be3c3e6d4a3429ffe51519d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/27/2018
ms.locfileid: "52339019"
---
# <a name="azure-tools-for-java-developers"></a><span data-ttu-id="93b7f-103">Herramientas para desarrolladores de Java de Azure</span><span class="sxs-lookup"><span data-stu-id="93b7f-103">Azure tools for Java developers</span></span>

## <a name="supported-jdk-runtimes"></a><span data-ttu-id="93b7f-104">Entornos de ejecución de JDK compatibles</span><span class="sxs-lookup"><span data-stu-id="93b7f-104">Supported JDK runtimes</span></span>

<span data-ttu-id="93b7f-105">Los desarrolladores Java que trabajan con Azure y Azure Stack pueden crear y ejecutar aplicaciones Java 7, 8 y 11 de producción con [compilaciones de Azul Systems Zulu Enterprise de OpenJDK](https://www.azul.com/downloads/azure-only/zulu/) sin incurrir en costos de soporte técnico adicionales.</span><span class="sxs-lookup"><span data-stu-id="93b7f-105">Java developers on Azure and Azure Stack can build and run production Java 7,8, and 11 applications using [Azul Systems Zulu Enterprise builds of OpenJDK](https://www.azul.com/downloads/azure-only/zulu/) without incurring additional support costs.</span></span> <span data-ttu-id="93b7f-106">Si actualmente ejecuta aplicaciones Java con otros JDK, plantéese cambiar a Zulu en Azure con soporte técnico y mantenimiento gratuitos.</span><span class="sxs-lookup"><span data-stu-id="93b7f-106">If you’re currently running Java apps with other JDKs, consider migrating to Zulu on Azure for free support and maintenance.</span></span> 

<span data-ttu-id="93b7f-107">Para más información sobre los JDK disponibles para desarrollar en Azure, consulte <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="93b7f-107">For more information about the supported JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>

## <a name="eclipse-and-intellij-plugins"></a><span data-ttu-id="93b7f-108">Complementos de Eclipse y IntelliJ</span><span class="sxs-lookup"><span data-stu-id="93b7f-108">Eclipse and IntelliJ plugins</span></span>

<span data-ttu-id="93b7f-109">Administre los recursos de Azure e implemente aplicaciones desde el IDE con los kits de herramientas de Azure para [Eclipse](eclipse/azure-toolkit-for-eclipse.md) e [IntelliJ](intellij/azure-toolkit-for-intellij.md).</span><span class="sxs-lookup"><span data-stu-id="93b7f-109">Manage Azure resources and deploy apps from your IDE with The Azure toolkits for [Eclipse](eclipse/azure-toolkit-for-eclipse.md) and [IntelliJ](intellij/azure-toolkit-for-intellij.md).</span></span>   

![Kit de herramientas de IntelliJ que muestra el Explorador de Azure](media/intelliJ-azure-explorer.png)

<span data-ttu-id="93b7f-111">[Introducción a Azure Toolkit for Eclipse](https://docs.microsoft.com/azure/app-service-web/app-service-web-eclipse-create-hello-world-web-app) | [Introducción a Azure Toolkit for IntelliJ](https://docs.microsoft.com/azure/app-service-web/app-service-web-intellij-create-hello-world-web-app)</span><span class="sxs-lookup"><span data-stu-id="93b7f-111">[Get started with Azure Toolkit for Eclipse](https://docs.microsoft.com/azure/app-service-web/app-service-web-eclipse-create-hello-world-web-app) | [Get started with Azure Toolkit for IntelliJ](https://docs.microsoft.com/azure/app-service-web/app-service-web-intellij-create-hello-world-web-app)</span></span> 

## <a name="visual-studio-code"></a><span data-ttu-id="93b7f-112">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="93b7f-112">Visual Studio Code</span></span>

<span data-ttu-id="93b7f-113">[VS Code](https://code.visualstudio.com/) es un editor de código ligero pero eficaz, disponible para MacOS, Windows y Linux.</span><span class="sxs-lookup"><span data-stu-id="93b7f-113">[VS Code](https://code.visualstudio.com/) is a lightweight but powerful code editor available for MacOS, Windows, and Linux.</span></span> <span data-ttu-id="93b7f-114">VS Code admite un flujo de trabajo de desarrollo con Java sencillo y moderno, mediante un conjunto de extensiones que proporcionan compatibilidad para proyectos, finalización del código, búsqueda de errores, depuración y navegación.</span><span class="sxs-lookup"><span data-stu-id="93b7f-114">VS Code supports a simple, modern Java development workflow through a set of extensions that provide project support, code completion, debugging, linting, and navigation.</span></span>

<span data-ttu-id="93b7f-115">[Introducción a VS Code y Java](https://code.visualstudio.com/docs/java)
[Paquete de extensiones de Java para VS Code](https://code.visualstudio.com/docs/java/extensions)</span><span class="sxs-lookup"><span data-stu-id="93b7f-115">[Get Started with VS Code and Java](https://code.visualstudio.com/docs/java)
[Java extension pack for VS Code](https://code.visualstudio.com/docs/java/extensions)</span></span>  

## <a name="azure-cli-20"></a><span data-ttu-id="93b7f-116">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="93b7f-116">Azure CLI 2.0</span></span>

<span data-ttu-id="93b7f-117">La CLI de Azure 2.0 proporciona una experiencia de línea de comandos para administrar los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="93b7f-117">The Azure 2.0 CLI provides a command-line experience to manage Azure resources.</span></span> <span data-ttu-id="93b7f-118">Puede usarla en el explorador con [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview) o puede [instalarla](https://docs.microsoft.com/cli/azure/install-azure-cli) en macOS, Linux y Windows y ejecutarla desde la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="93b7f-118">You can use it in your browser with [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview), or you can [install](https://docs.microsoft.com/cli/azure/install-azure-cli) it on macOS, Linux, and Windows and run it from the command line.</span></span>

<span data-ttu-id="93b7f-119">[Introducción a la CLI de Azure 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="93b7f-119">[Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli).</span></span>

## <a name="azure-storage-explorer"></a><span data-ttu-id="93b7f-120">Explorador de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="93b7f-120">Azure Storage Explorer</span></span> 

<span data-ttu-id="93b7f-121">Administre cuentas de Azure Storage, contenedores y blobs o archivos desde el escritorio.</span><span class="sxs-lookup"><span data-stu-id="93b7f-121">Manage Azure storage accounts, containers, and blobs/files from your desktop.</span></span> <span data-ttu-id="93b7f-122">El Explorador de Azure Storage está actualmente en versión preliminar y funciona en Windows, Mac OS y Linux.</span><span class="sxs-lookup"><span data-stu-id="93b7f-122">Azure Storage Explorer is currently in Preview and works on Windows, macOS, and Linux.</span></span>

[<span data-ttu-id="93b7f-123">Introducción al Explorador de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="93b7f-123">Get started with Azure Storage Explorer</span></span>](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer)
