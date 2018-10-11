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
ms.openlocfilehash: 0f3df5c8cf3c83c1ce9a4ca32c753b5fc39ab1df
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/09/2018
ms.locfileid: "48892886"
---
# <a name="installing-the-azure-toolkit-for-intellij"></a><span data-ttu-id="f4427-103">Instalación del kit de herramientas de Azure para IntelliJ</span><span class="sxs-lookup"><span data-stu-id="f4427-103">Installing the Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="f4427-104">El kit de herramientas de Azure para IntelliJ ofrece plantillas y funciones que permiten crear, desarrollar, probar e implementar aplicaciones en la nube en Azure fácilmente con el entorno de desarrollo IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="f4427-104">The Azure Toolkit for IntelliJ provides templates and functionality that allow you to easily create, develop, test, and deploy cloud application to Azure using the IntelliJ IDEA development environment.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="f4427-105">El kit de herramientas de Azure para IntelliJ es un proyecto de código abierto, cuyo código fuente está disponible con la licencia MIT del sitio del proyecto en GitHub en la siguiente dirección URL:</span><span class="sxs-lookup"><span data-stu-id="f4427-105">The Azure Toolkit for IntelliJ is an Open Source project, whose source code is available under the MIT License from the project's site on GitHub at the following URL:</span></span> 
> 
> <https://github.com/microsoft/azure-tools-for-java> 
> 

<span data-ttu-id="f4427-106">Hay dos métodos para instalar el Kit de herramientas de Azure para IntelliJ: mediante el cuadro de diálogo **Configuración** y mediante el menú **Configurar** en la pantalla Inicio.</span><span class="sxs-lookup"><span data-stu-id="f4427-106">There are two methods of installing the Azure Toolkit for IntelliJ: by using the **Settings** dialog box, and by using the **Configure** menu on the start screen.</span></span> <span data-ttu-id="f4427-107">Ambos métodos de instalación se mostrarán en los pasos siguientes.</span><span class="sxs-lookup"><span data-stu-id="f4427-107">Both installation methods will be demonstrated in the following steps.</span></span>

[!INCLUDE [azure-toolkit-for-IntelliJ-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="to-install-the-azure-toolkit-for-intellij-from-the-settings-dialog-box"></a><span data-ttu-id="f4427-108">Para instalar el kit de herramientas de Azure para IntelliJ desde el cuadro de diálogo Configuración</span><span class="sxs-lookup"><span data-stu-id="f4427-108">To install the Azure Toolkit for IntelliJ from the settings dialog box</span></span>

1. <span data-ttu-id="f4427-109">Inicie IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="f4427-109">Start IntelliJ IDEA.</span></span>

1. <span data-ttu-id="f4427-110">Cuando se abra IntelliJ IDEA, haga clic en **File** (Archivo) y, después, en **Settings** (Configuración).</span><span class="sxs-lookup"><span data-stu-id="f4427-110">When the IntelliJ IDEA opens, click **File**, then click **Settings**.</span></span>
   
   ![Apertura del cuadro de diálogo Configuración de IntelliJ IDEA][01a]

1. <span data-ttu-id="f4427-112">En el cuadro de diálogo Settings (Configuración), haga clic en **Plugins** (Complementos) y, después, en **Browse repositories** (Explorar repositorios).</span><span class="sxs-lookup"><span data-stu-id="f4427-112">In the Settings dialog box, click **Plugins**, and then click **Browse repositories**.</span></span>
   
   ![Cuadro de diálogo Configuración de IntelliJ IDEA][02a]

1. <span data-ttu-id="f4427-114">En el cuadro de diálogo **Browse repositories** (Explorar repositorios), escriba "Azure" en el cuadro de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="f4427-114">In the **Browse Repositories** dialog box, type "Azure" in the search box.</span></span> <span data-ttu-id="f4427-115">Resalte **Azure Toolkit for IntelliJ** (Kit de herramientas de Azure para IntelliJ) y, después, haga clic en **Install** (Instalar).</span><span class="sxs-lookup"><span data-stu-id="f4427-115">Highlight **Azure Toolkit for IntelliJ**, and then click **Install**.</span></span>
   
   ![Búsqueda del kit de herramientas de Azure para IntelliJ][03]
   
   <span data-ttu-id="f4427-117">IntelliJ IDEA muestra el progreso de la instalación en un cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f4427-117">IntelliJ IDEA displays the installation progress in a dialog box.</span></span>
   
   ![Progreso de la instalación][04]

1. <span data-ttu-id="f4427-119">Cuando se haya completado la instalación, haga clic en **Restart IntelliJ IDEA**(Reiniciar IntelliJ IDEA).</span><span class="sxs-lookup"><span data-stu-id="f4427-119">When the installation has completed, click **Restart IntelliJ IDEA**.</span></span>
   
   ![Restart IntelliJ IDEA][05]

1. <span data-ttu-id="f4427-121">Haga clic en **Aceptar** para cerrar el cuadro de diálogo Configuración.</span><span class="sxs-lookup"><span data-stu-id="f4427-121">Click **OK** to close the Settings dialog box.</span></span>
   
   ![Cierre del cuadro de diálogo Configuración de IntelliJ IDEA][06]

1. <span data-ttu-id="f4427-123">Cuando se le pregunte si desea reiniciar IntelliJ IDEA o posponer el reinicio, haga clic en **Reiniciar**.</span><span class="sxs-lookup"><span data-stu-id="f4427-123">When prompted to restart IntelliJ IDEA or postpone, click **Restart**.</span></span>
   
<span data-ttu-id="f4427-124">1</span><span class="sxs-lookup"><span data-stu-id="f4427-124">1</span></span>   ![Restart IntelliJ IDEA][07]

## <a name="to-install-the-azure-toolkit-for-intellij-from-the-start-screen"></a><span data-ttu-id="f4427-126">Para instalar el kit de herramientas de Azure para IntelliJ desde la pantalla de inicio</span><span class="sxs-lookup"><span data-stu-id="f4427-126">To install the Azure Toolkit for IntelliJ from the start screen</span></span>

1. <span data-ttu-id="f4427-127">Inicie IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="f4427-127">Start IntelliJ IDEA.</span></span>

1. <span data-ttu-id="f4427-128">Cuando aparezca la pantalla de inicio de IntelliJ IDEA, haga clic en **Configure** (Configurar) y, después, en **Plugins** (Complementos).</span><span class="sxs-lookup"><span data-stu-id="f4427-128">When the IntelliJ IDEA start screen appears, click **Configure**, then click **Plugins**.</span></span>
   
   ![Instalación de los complementos de IntelliJ IDEA][01b]

1. <span data-ttu-id="f4427-130">En el cuadro de diálogo **Plugins** (Complementos), haga clic en **Browse repositories** (Explorar repositorios).</span><span class="sxs-lookup"><span data-stu-id="f4427-130">In the **Plugins** dialog box, click **Browse repositories**.</span></span>
   
   ![Exploración de los repositorios de complementos de IntelliJ IDEA][02b]

1. <span data-ttu-id="f4427-132">En el cuadro de diálogo **Browse repositories** (Explorar repositorios), escriba "Azure" en el cuadro de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="f4427-132">In the **Browse Repositories** dialog box, type "Azure" in the search box.</span></span> <span data-ttu-id="f4427-133">Resalte **Azure Toolkit for IntelliJ** (Kit de herramientas de Azure para IntelliJ) y, después, haga clic en **Install** (Instalar).</span><span class="sxs-lookup"><span data-stu-id="f4427-133">Highlight **Azure Toolkit for IntelliJ**, and then click **Install**.</span></span>
   
   ![Búsqueda del kit de herramientas de Azure para IntelliJ][03]
   
   <span data-ttu-id="f4427-135">IntelliJ IDEA mostrará el progreso de la instalación en un cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f4427-135">IntelliJ IDEA will display the installation progress in a dialog box.</span></span>
   
   ![Progreso de la instalación][04]

1. <span data-ttu-id="f4427-137">Cuando se haya completado la instalación, haga clic en **Restart IntelliJ IDEA**(Reiniciar IntelliJ IDEA).</span><span class="sxs-lookup"><span data-stu-id="f4427-137">When the installation has completed, click **Restart IntelliJ IDEA**.</span></span>
   
   ![Restart IntelliJ IDEA][05]

1. <span data-ttu-id="f4427-139">Cuando se le pregunte si desea reiniciar IntelliJ IDEA o posponer el reinicio, haga clic en **Reiniciar**.</span><span class="sxs-lookup"><span data-stu-id="f4427-139">When prompted to restart IntelliJ IDEA or postpone, click **Restart**.</span></span>
   
   ![Restart IntelliJ IDEA][07]

## <a name="next-steps"></a><span data-ttu-id="f4427-141">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f4427-141">Next steps</span></span>

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
