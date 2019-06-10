---
title: Instalación del kit de herramientas de Azure para IntelliJ
description: Obtenga información acerca de cómo instalar el complemento del kit de herramientas de Azure para IntelliJ para crear e implementar aplicaciones en la nube en Azure.
services: ''
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: c6817c7b-f28c-4c06-8216-41c7a8117de3
ms.author: robmcm
ms.date: 02/01/2018
ms.devlang: Java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: 86cef07873ae7a2ba75aab1044fe4d241cd5b13e
ms.sourcegitcommit: 394521c47ac9895d00d9f97535cc9d1e27d08fe9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/28/2019
ms.locfileid: "66270872"
---
# <a name="installing-the-azure-toolkit-for-intellij"></a><span data-ttu-id="c67c3-103">Instalación del kit de herramientas de Azure para IntelliJ</span><span class="sxs-lookup"><span data-stu-id="c67c3-103">Installing the Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="c67c3-104">El kit de herramientas de Azure para IntelliJ ofrece plantillas y funciones que permiten crear, desarrollar, probar e implementar aplicaciones en la nube en Azure fácilmente con el entorno de desarrollo IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="c67c3-104">The Azure Toolkit for IntelliJ provides templates and functionality that allow you to easily create, develop, test, and deploy cloud application to Azure using the IntelliJ IDEA development environment.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="c67c3-105">El kit de herramientas de Azure para IntelliJ es un proyecto de código abierto, cuyo código fuente está disponible con la licencia MIT del sitio del proyecto en GitHub en la siguiente dirección URL:</span><span class="sxs-lookup"><span data-stu-id="c67c3-105">The Azure Toolkit for IntelliJ is an Open Source project, whose source code is available under the MIT License from the project's site on GitHub at the following URL:</span></span> 
> 
> <https://github.com/microsoft/azure-tools-for-java> 
> 

<span data-ttu-id="c67c3-106">Hay dos métodos para instalar el Kit de herramientas de Azure para IntelliJ: mediante el cuadro de diálogo **Configuración** y mediante el menú **Configurar** en la pantalla Inicio.</span><span class="sxs-lookup"><span data-stu-id="c67c3-106">There are two methods of installing the Azure Toolkit for IntelliJ: by using the **Settings** dialog box, and by using the **Configure** menu on the start screen.</span></span> <span data-ttu-id="c67c3-107">Ambos métodos de instalación se mostrarán en los pasos siguientes.</span><span class="sxs-lookup"><span data-stu-id="c67c3-107">Both installation methods will be demonstrated in the following steps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c67c3-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c67c3-108">Prerequisites</span></span>

<span data-ttu-id="c67c3-109">Azure Toolkit for IntelliJ requiere los siguientes componentes de software:</span><span class="sxs-lookup"><span data-stu-id="c67c3-109">The Azure Toolkit for IntelliJ requires to the following software components:</span></span>

* <span data-ttu-id="c67c3-110">Java Development Kit (JDK) 8+ instalado, por ejemplo: [OpenJDK](https://openjdk.java.net/) o el [JDK de Oracle](https://www.oracle.com/technetwork/java/javase/downloads/index.html)</span><span class="sxs-lookup"><span data-stu-id="c67c3-110">An Java Development Kit (JDK) 8+ installed, for example: [OpenJDK](https://openjdk.java.net/) or [Oracle JDK](https://www.oracle.com/technetwork/java/javase/downloads/index.html)</span></span>
* <span data-ttu-id="c67c3-111">[IntelliJ IDEA](https://www.jetbrains.com/idea/download/) Ultimate Edition o Community Edition instalado</span><span class="sxs-lookup"><span data-stu-id="c67c3-111">An [IntelliJ IDEA](https://www.jetbrains.com/idea/download/) Ultimate Edition or Community Edition installed</span></span>

> [!NOTE]
> 
> <span data-ttu-id="c67c3-112">La página [Azure Toolkit for IntelliJ](https://plugins.jetbrains.com/plugin/8053) en el repositorio de complementos de JetBrains muestra las compilaciones que son compatibles con el kit de herramientas.</span><span class="sxs-lookup"><span data-stu-id="c67c3-112">The [Azure Toolkit for IntelliJ](https://plugins.jetbrains.com/plugin/8053) page at the JetBrains Plugin Repository lists the builds that are compatible with the toolkit.</span></span>
> 

<!--
> [!IMPORTANT]
> 
> If you are using the Azure Toolkit for IntelliJ on Windows, the toolkit requires installing the Azure SDK 2.9.6 or later in order to use the Azure emulator. You have two options for installing the Azure SDK:
> 
> * You can download and install the Azure SDK by using the [Web Platform Installer (WebPI)](http://go.microsoft.com/fwlink/?LinkID=252838).
> * If you do not have the Azure SDK installed when you create your first Azure deployment project, you will be prompted to automatically download install the requisite version of the Azure SDK.
> 
> Note that the Azure SDK is only required on Windows.
> 
-->


## <a name="to-install-the-azure-toolkit-for-intellij-from-the-settings-dialog-box"></a><span data-ttu-id="c67c3-113">Para instalar el kit de herramientas de Azure para IntelliJ desde el cuadro de diálogo Configuración</span><span class="sxs-lookup"><span data-stu-id="c67c3-113">To install the Azure Toolkit for IntelliJ from the settings dialog box</span></span>

1. <span data-ttu-id="c67c3-114">Inicie IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="c67c3-114">Start IntelliJ IDEA.</span></span>

1. <span data-ttu-id="c67c3-115">Cuando se abra IntelliJ IDEA, haga clic en **File** (Archivo) y, después, en **Settings** (Configuración).</span><span class="sxs-lookup"><span data-stu-id="c67c3-115">When the IntelliJ IDEA opens, click **File**, then click **Settings**.</span></span>
   
   ![Apertura del cuadro de diálogo Configuración de IntelliJ IDEA][01a]

1. <span data-ttu-id="c67c3-117">En el cuadro de diálogo Settings (Configuración), haga clic en **Plugins** (Complementos) y, después, en **Browse repositories** (Explorar repositorios).</span><span class="sxs-lookup"><span data-stu-id="c67c3-117">In the Settings dialog box, click **Plugins**, and then click **Browse repositories**.</span></span>
   
   ![Cuadro de diálogo Configuración de IntelliJ IDEA][02a]

1. <span data-ttu-id="c67c3-119">En el cuadro de diálogo **Browse repositories** (Explorar repositorios), escriba "Azure" en el cuadro de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="c67c3-119">In the **Browse Repositories** dialog box, type "Azure" in the search box.</span></span> <span data-ttu-id="c67c3-120">Resalte **Azure Toolkit for IntelliJ** (Kit de herramientas de Azure para IntelliJ) y, después, haga clic en **Install** (Instalar).</span><span class="sxs-lookup"><span data-stu-id="c67c3-120">Highlight **Azure Toolkit for IntelliJ**, and then click **Install**.</span></span>
   
   ![Búsqueda del kit de herramientas de Azure para IntelliJ][03]
   
   <span data-ttu-id="c67c3-122">IntelliJ IDEA muestra el progreso de la instalación en un cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c67c3-122">IntelliJ IDEA displays the installation progress in a dialog box.</span></span>
   
   ![Progreso de la instalación][04]

1. <span data-ttu-id="c67c3-124">Cuando se haya completado la instalación, haga clic en **Restart IntelliJ IDEA**(Reiniciar IntelliJ IDEA).</span><span class="sxs-lookup"><span data-stu-id="c67c3-124">When the installation has completed, click **Restart IntelliJ IDEA**.</span></span>
   
   ![Restart IntelliJ IDEA][05]

1. <span data-ttu-id="c67c3-126">Haga clic en **Aceptar** para cerrar el cuadro de diálogo Configuración.</span><span class="sxs-lookup"><span data-stu-id="c67c3-126">Click **OK** to close the Settings dialog box.</span></span>
   
   ![Cierre del cuadro de diálogo Configuración de IntelliJ IDEA][06]

1. <span data-ttu-id="c67c3-128">Cuando se le pregunte si desea reiniciar IntelliJ IDEA o posponer el reinicio, haga clic en **Reiniciar**.</span><span class="sxs-lookup"><span data-stu-id="c67c3-128">When prompted to restart IntelliJ IDEA or postpone, click **Restart**.</span></span>
   
<span data-ttu-id="c67c3-129">1</span><span class="sxs-lookup"><span data-stu-id="c67c3-129">1</span></span>   ![Restart IntelliJ IDEA][07]

## <a name="to-install-the-azure-toolkit-for-intellij-from-the-start-screen"></a><span data-ttu-id="c67c3-131">Para instalar el kit de herramientas de Azure para IntelliJ desde la pantalla de inicio</span><span class="sxs-lookup"><span data-stu-id="c67c3-131">To install the Azure Toolkit for IntelliJ from the start screen</span></span>

1. <span data-ttu-id="c67c3-132">Inicie IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="c67c3-132">Start IntelliJ IDEA.</span></span>

1. <span data-ttu-id="c67c3-133">Cuando aparezca la pantalla de inicio de IntelliJ IDEA, haga clic en **Configure** (Configurar) y, después, en **Plugins** (Complementos).</span><span class="sxs-lookup"><span data-stu-id="c67c3-133">When the IntelliJ IDEA start screen appears, click **Configure**, then click **Plugins**.</span></span>
   
   ![Instalación de los complementos de IntelliJ IDEA][01b]

1. <span data-ttu-id="c67c3-135">En el cuadro de diálogo **Plugins** (Complementos), haga clic en **Browse repositories** (Explorar repositorios).</span><span class="sxs-lookup"><span data-stu-id="c67c3-135">In the **Plugins** dialog box, click **Browse repositories**.</span></span>
   
   ![Exploración de los repositorios de complementos de IntelliJ IDEA][02b]

1. <span data-ttu-id="c67c3-137">En el cuadro de diálogo **Browse repositories** (Explorar repositorios), escriba "Azure" en el cuadro de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="c67c3-137">In the **Browse Repositories** dialog box, type "Azure" in the search box.</span></span> <span data-ttu-id="c67c3-138">Resalte **Azure Toolkit for IntelliJ** (Kit de herramientas de Azure para IntelliJ) y, después, haga clic en **Install** (Instalar).</span><span class="sxs-lookup"><span data-stu-id="c67c3-138">Highlight **Azure Toolkit for IntelliJ**, and then click **Install**.</span></span>
   
   ![Búsqueda del kit de herramientas de Azure para IntelliJ][03]
   
   <span data-ttu-id="c67c3-140">IntelliJ IDEA mostrará el progreso de la instalación en un cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c67c3-140">IntelliJ IDEA will display the installation progress in a dialog box.</span></span>
   
   ![Progreso de la instalación][04]

1. <span data-ttu-id="c67c3-142">Cuando se haya completado la instalación, haga clic en **Restart IntelliJ IDEA**(Reiniciar IntelliJ IDEA).</span><span class="sxs-lookup"><span data-stu-id="c67c3-142">When the installation has completed, click **Restart IntelliJ IDEA**.</span></span>
   
   ![Restart IntelliJ IDEA][05]

1. <span data-ttu-id="c67c3-144">Cuando se le pregunte si desea reiniciar IntelliJ IDEA o posponer el reinicio, haga clic en **Reiniciar**.</span><span class="sxs-lookup"><span data-stu-id="c67c3-144">When prompted to restart IntelliJ IDEA or postpone, click **Restart**.</span></span>
   
   ![Restart IntelliJ IDEA][07]

## <a name="next-steps"></a><span data-ttu-id="c67c3-146">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c67c3-146">Next steps</span></span>

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

<!-- URL List -->

<!-- IMG List -->

[01a]: media/azure-toolkit-for-intellij-installation/01-intellij-file-settings.png
[01b]: media/azure-toolkit-for-intellij-installation/01-intellij-configure-dropdown.png
[02a]: media/azure-toolkit-for-intellij-installation/02-intellij-settings-dialog.png
[02b]: media/azure-toolkit-for-intellij-installation/02-intellij-plugins-dialog.png
[03]: media/azure-toolkit-for-intellij-installation/03-intellij-browse-repositories.png
[04]: media/azure-toolkit-for-intellij-installation/04-install-progress.png
[05]: media/azure-toolkit-for-intellij-installation/05-restart-intellij.png
[06]: media/azure-toolkit-for-intellij-installation/06-intellij-settings-dialog.png
[07]: media/azure-toolkit-for-intellij-installation/07-restart-intellij.png
