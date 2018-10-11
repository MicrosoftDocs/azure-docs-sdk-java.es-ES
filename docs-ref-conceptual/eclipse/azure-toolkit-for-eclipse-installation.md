---
title: Instalación del kit de herramientas de Azure para Eclipse
description: Obtenga información acerca de cómo instalar el complemento del kit de herramientas de Azure para Eclipse para crear e implementar aplicaciones en la nube en Azure.
services: ''
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: 9e93ff6a-f42b-4d99-b55b-624136b4a730
ms.author: robmcm
ms.date: 02/01/2018
ms.devlang: Java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: d5f685fa62ad74c8b8cd842b3667f8161e7c5760
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/09/2018
ms.locfileid: "48893013"
---
# <a name="install-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="5272b-103">Instalación del kit de herramientas de Azure para Eclipse</span><span class="sxs-lookup"><span data-stu-id="5272b-103">Install the Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="5272b-104">El kit de herramientas de Azure para Eclipse ofrece plantillas y funciones que permiten crear, desarrollar, probar e implementar aplicaciones en la nube en Azure fácilmente desde el entorno de desarrollo Eclipse.</span><span class="sxs-lookup"><span data-stu-id="5272b-104">The Azure Toolkit for Eclipse provides templates and functionality that allow you to easily create, develop, test, and deploy cloud applications to Azure from the Eclipse development environment.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="5272b-105">El kit de herramientas de Azure para Eclipse es un proyecto de código abierto, cuyo código fuente está disponible con la licencia MIT del sitio del proyecto en GitHub en la siguiente dirección URL:</span><span class="sxs-lookup"><span data-stu-id="5272b-105">The Azure Toolkit for Eclipse is an Open Source project, whose source code is available under the MIT License from the project's site on GitHub at the following URL:</span></span> 
> 
> <https://github.com/microsoft/azure-tools-for-java> 
> 

<span data-ttu-id="5272b-106">En los pasos siguientes se muestra cómo instalar el Kit de herramientas de Azure para Eclipse.</span><span class="sxs-lookup"><span data-stu-id="5272b-106">The following steps show you how to install the Azure Toolkit for Eclipse.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="to-install-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="5272b-107">Para instalar el Kit de herramientas de Azure para Eclipse</span><span class="sxs-lookup"><span data-stu-id="5272b-107">To install the Azure Toolkit for Eclipse</span></span>

1. <span data-ttu-id="5272b-108">Inicie Eclipse.</span><span class="sxs-lookup"><span data-stu-id="5272b-108">Start Eclipse.</span></span>

1. <span data-ttu-id="5272b-109">Haga clic en el menú **Help** (Ayuda) y, a continuación, haga clic en **Install New Software** (Instalar nuevo software), como se muestra en la siguiente ilustración.</span><span class="sxs-lookup"><span data-stu-id="5272b-109">Click the **Help** menu, and then click **Install New Software**, as shown in the following illustration.</span></span>
   
   ![Instalación del Kit de herramientas de Azure para Eclipse][01]

1. <span data-ttu-id="5272b-111">En el cuadro de diálogo **Available Software** (Software disponible), en el cuadro de texto **Work with** (Trabajar con), escriba `http://dl.microsoft.com/eclipse/` seguido de la tecla **Intro**.</span><span class="sxs-lookup"><span data-stu-id="5272b-111">In the **Available Software** dialog, within the **Work with** text box, type `http://dl.microsoft.com/eclipse/` followed by the **Enter** key.</span></span>

1. <span data-ttu-id="5272b-112">En el panel **Nombre**, active **Kit de herramientas de Azure para Java** y desactive **Ponerse en contacto con todos los sitios de actualización durante la instalación para encontrar el software necesario**.</span><span class="sxs-lookup"><span data-stu-id="5272b-112">In the **Name** pane, check **Azure Toolkit for Java**, and uncheck **Contact all update sites during install to find required software**.</span></span> <span data-ttu-id="5272b-113">La pantalla debe parecerse a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="5272b-113">Your screen should appear similar to the following:</span></span>
   
   ![Instalación del Kit de herramientas de Azure para Eclipse][02]

1. <span data-ttu-id="5272b-115">Si expande **Azure Toolkit for Eclipse**, verá una lista de los componentes que se instalarán; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="5272b-115">If you expand **Azure Toolkit for Eclipse**, you will see a list of components that will be installed; for example:</span></span>

   | <span data-ttu-id="5272b-116">Característica</span><span class="sxs-lookup"><span data-stu-id="5272b-116">Feature</span></span> | <span data-ttu-id="5272b-117">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="5272b-117">Description</span></span> | 
   |---|---| 
   | <span data-ttu-id="5272b-118">**Complemento de Application Insights para Java**</span><span class="sxs-lookup"><span data-stu-id="5272b-118">**Application Insights Plugin for Java**</span></span> | <span data-ttu-id="5272b-119">Permite usar los servicios de análisis y registro de telemetría de Azure para sus aplicaciones e instancias de servidor.</span><span class="sxs-lookup"><span data-stu-id="5272b-119">Allows you to use Azure's telemetry logging and analysis services for your applications and server instances.</span></span> | 
   | <span data-ttu-id="5272b-120">**Complemento común de Azure**</span><span class="sxs-lookup"><span data-stu-id="5272b-120">**Azure Common Plugin**</span></span> | <span data-ttu-id="5272b-121">Proporciona la funcionalidad habitual necesaria para otros componentes del kit de herramientas.</span><span class="sxs-lookup"><span data-stu-id="5272b-121">provides the common functionality needed by other toolkit components.</span></span> | 
   | <span data-ttu-id="5272b-122">**Herramientas de Azure Container para Eclipse**</span><span class="sxs-lookup"><span data-stu-id="5272b-122">**Azure Container Tools for Eclipse**</span></span> | <span data-ttu-id="5272b-123">Permite crear e implementar un artefacto .WAR como un contenedor de Docker en una máquina de Docker.</span><span class="sxs-lookup"><span data-stu-id="5272b-123">Enables you to build and deploy a .WAR as a Docker container to a docker machine.</span></span> | 
   | <span data-ttu-id="5272b-124">**Azure Containers for Eclipse**</span><span class="sxs-lookup"><span data-stu-id="5272b-124">**Azure Containers for Eclipse**</span></span> | <span data-ttu-id="5272b-125">Permite implementar un artefacto .WAR o .JAR como un contenedor Docker en una máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="5272b-125">Enables you to deploy a .WAR or .JAR artifact as a Docker container to an Azure virtual machine.</span></span> | 
   | <span data-ttu-id="5272b-126">**Explorador de Azure para Eclipse**</span><span class="sxs-lookup"><span data-stu-id="5272b-126">**Azure Explorer for Eclipse**</span></span> | <span data-ttu-id="5272b-127">Proporciona una interfaz de tipo explorador para administrar los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="5272b-127">Provides an explorer-style interface for managing your Azure resources.</span></span> | 
   | <span data-ttu-id="5272b-128">**Microsoft JDBC Driver 6.1 para SQL Server**</span><span class="sxs-lookup"><span data-stu-id="5272b-128">**Microsoft JDBC Driver 6.1 for SQL Server**</span></span> | <span data-ttu-id="5272b-129">Proporciona JDBC API para SQL Server y Microsoft Azure SQL Database para Java Platform Enterprise Edition 8.</span><span class="sxs-lookup"><span data-stu-id="5272b-129">Provides JDBC API for SQL Server and Microsoft Azure SQL Database for Java Platform Enterprise Edition 8.</span></span> | 
   | <span data-ttu-id="5272b-130">**Paquete para bibliotecas de Microsoft Azure para Java**</span><span class="sxs-lookup"><span data-stu-id="5272b-130">**Package for Microsoft Azure Libraries for Java**</span></span> | <span data-ttu-id="5272b-131">Proporciona las API para acceder a los servicios de Microsoft Azure, como Storage, Service Bus, Service Runtime, etc.</span><span class="sxs-lookup"><span data-stu-id="5272b-131">Provides APIs for accessing Microsoft Azure services, such as storage, service bus, service runtime, etc.</span></span> | 

1. <span data-ttu-id="5272b-132">Haga clic en **Next**.</span><span class="sxs-lookup"><span data-stu-id="5272b-132">Click **Next**.</span></span> <span data-ttu-id="5272b-133">(Si se producen retrasos inusuales al instalar el kit de herramientas, asegúrese de que la opción **Ponerse en contacto con todos los sitios de actualización durante la instalación para encontrar el software necesario** está desactivada.)</span><span class="sxs-lookup"><span data-stu-id="5272b-133">(If you experience unusual delays when installing the toolkit, ensure that **Contact all update sites during install to find required software** is unchecked.)</span></span>

1. <span data-ttu-id="5272b-134">En el cuadro de diálogo **Install Details** (Detalles de instalación), haga clic en **Next** (Siguiente).</span><span class="sxs-lookup"><span data-stu-id="5272b-134">In the **Install Details** dialog, click **Next**.</span></span>
   
   ![Revisión de los detalles de la instalación][03]

1. <span data-ttu-id="5272b-136">En el cuadro de diálogo **Revisar licencias** , revise los términos de los contratos de licencia.</span><span class="sxs-lookup"><span data-stu-id="5272b-136">In the **Review Licenses** dialog, review the terms of the license agreements.</span></span> <span data-ttu-id="5272b-137">Si acepta los términos de los contratos de licencia, haga clic en **I accept the terms of the license agreements** (Acepto los términos de los contratos de licencia) y luego haga clic en **Finish** (Finalizar).</span><span class="sxs-lookup"><span data-stu-id="5272b-137">If you accept the terms of the license agreements, click **I accept the terms of the license agreements** and then click **Finish**.</span></span> <span data-ttu-id="5272b-138">(En los pasos restantes se supone que acepta los términos de los contratos de licencia.</span><span class="sxs-lookup"><span data-stu-id="5272b-138">(The remaining steps assume you do accept the terms of the license agreements.</span></span> <span data-ttu-id="5272b-139">Si no acepta los términos de los contratos de licencia, salga del proceso de instalación.)</span><span class="sxs-lookup"><span data-stu-id="5272b-139">If you do not accept the terms of the license agreements, exit the installation process.)</span></span>
   
   ![Revisar licencias][04]
   
   <span data-ttu-id="5272b-141">Eclipse descargará e instalará los paquetes necesarios.</span><span class="sxs-lookup"><span data-stu-id="5272b-141">Eclipse will download and install the requisite packages.</span></span>
   
   ![Progreso de la instalación][05]

1. <span data-ttu-id="5272b-143">Si se le solicita que reinicie Eclipse para completar la instalación, haga clic en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="5272b-143">If prompted to restart Eclipse to complete installation, click **Yes**.</span></span>
   
   ![Reinicio del símbolo del sistema][06]

## <a name="next-steps"></a><span data-ttu-id="5272b-145">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5272b-145">Next steps</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<!-- URL List -->

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690946.aspx -->

<!-- IMG List -->

[01]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-01.png
[02]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-02.png
[03]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-03.png
[04]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-04.png
[05]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-05.png
[06]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-06.png
