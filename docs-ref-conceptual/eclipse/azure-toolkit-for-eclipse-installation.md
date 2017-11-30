---
title: "Instalación del Kit de herramientas de Azure para Eclipse"
description: "Descubra cómo instalar el kit de herramientas de Azure para Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 9e93ff6a-f42b-4d99-b55b-624136b4a730
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 11/01/2017
ms.author: robmcm
ms.openlocfilehash: 1f06b02a4c0b23d98ecd394d42f41f7148b6c8e8
ms.sourcegitcommit: 062e07cbd42cda74f02c82b933ce90da646a50a0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="installing-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="23add-103">Instalación del Kit de herramientas de Azure para Eclipse</span><span class="sxs-lookup"><span data-stu-id="23add-103">Installing the Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="23add-104">El kit de herramientas de Azure para Eclipse ofrece plantillas y funciones que permiten crear, desarrollar, probar e implementar aplicaciones de Azure fácilmente con el entorno de desarrollo de Eclipse.</span><span class="sxs-lookup"><span data-stu-id="23add-104">The Azure Toolkit for Eclipse provides templates and functionality that allow you to easily create, develop, test, and deploy Azure applications using the Eclipse development environment.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="23add-105">El kit de herramientas de Azure para Eclipse es un proyecto de código abierto, cuyo código fuente está disponible con la licencia MIT del sitio del proyecto en GitHub en la siguiente dirección URL:</span><span class="sxs-lookup"><span data-stu-id="23add-105">The Azure Toolkit for Eclipse is an Open Source project, whose source code is available under the MIT License from the project's site on GitHub at the following URL:</span></span> 
> 
> <span data-ttu-id="23add-106"><https://github.com/microsoft/azure-tools-for-java></span><span class="sxs-lookup"><span data-stu-id="23add-106"><https://github.com/microsoft/azure-tools-for-java></span></span> 
> 

<span data-ttu-id="23add-107">En los pasos siguientes se muestra cómo instalar el Kit de herramientas de Azure para Eclipse.</span><span class="sxs-lookup"><span data-stu-id="23add-107">The following steps show you how to install the Azure Toolkit for Eclipse.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="to-install-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="23add-108">Para instalar el Kit de herramientas de Azure para Eclipse</span><span class="sxs-lookup"><span data-stu-id="23add-108">To install the Azure Toolkit for Eclipse</span></span>

1. <span data-ttu-id="23add-109">Inicie Eclipse.</span><span class="sxs-lookup"><span data-stu-id="23add-109">Start Eclipse.</span></span>

1. <span data-ttu-id="23add-110">Haga clic en el menú **Help** (Ayuda) y, a continuación, haga clic en **Install New Software** (Instalar nuevo software), como se muestra en la siguiente ilustración.</span><span class="sxs-lookup"><span data-stu-id="23add-110">Click the **Help** menu, and then click **Install New Software**, as shown in the following illustration.</span></span>
   
   ![Instalación del Kit de herramientas de Azure para Eclipse][01]

1. <span data-ttu-id="23add-112">En el cuadro de diálogo **Available Software** (Software disponible), en el cuadro de texto **Work with** (Trabajar con), escriba `http://dl.microsoft.com/eclipse/` seguido de la tecla **Intro**.</span><span class="sxs-lookup"><span data-stu-id="23add-112">In the **Available Software** dialog, within the **Work with** text box, type `http://dl.microsoft.com/eclipse/` followed by the **Enter** key.</span></span>

1. <span data-ttu-id="23add-113">En el panel **Nombre**, active **Kit de herramientas de Azure para Eclipse**, y desactive **Ponerse en contacto con todos los sitios de actualización durante la instalación para encontrar el software necesario**.</span><span class="sxs-lookup"><span data-stu-id="23add-113">In the **Name** pane, check **Azure Toolkit for Eclipse**, and uncheck **Contact all update sites during install to find required software**.</span></span> <span data-ttu-id="23add-114">La pantalla debe parecerse a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="23add-114">Your screen should appear similar to the following:</span></span>
   
   ![Instalación del Kit de herramientas de Azure para Eclipse][02]

1. <span data-ttu-id="23add-116">Si expande **Azure Toolkit for Eclipse**, verá una lista de los componentes que se instalarán; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="23add-116">If you expand **Azure Toolkit for Eclipse**, you will see a list of components that will be installed; for example:</span></span>

   | <span data-ttu-id="23add-117">Característica</span><span class="sxs-lookup"><span data-stu-id="23add-117">Feature</span></span> | <span data-ttu-id="23add-118">Descripción</span><span class="sxs-lookup"><span data-stu-id="23add-118">Description</span></span> | 
   |---|---| 
   | <span data-ttu-id="23add-119">**Complemento de Application Insights para Java**</span><span class="sxs-lookup"><span data-stu-id="23add-119">**Application Insights Plugin for Java**</span></span> | <span data-ttu-id="23add-120">Permite usar los servicios de análisis y registro de telemetría de Azure para sus aplicaciones e instancias de servidor.</span><span class="sxs-lookup"><span data-stu-id="23add-120">Allows you to use Azure's telemetry logging and analysis services for your applications and server instances.</span></span> | 
   | <span data-ttu-id="23add-121">**Complemento común de Azure**</span><span class="sxs-lookup"><span data-stu-id="23add-121">**Azure Common Plugin**</span></span> | <span data-ttu-id="23add-122">Proporciona la funcionalidad habitual necesaria para otros componentes del kit de herramientas.</span><span class="sxs-lookup"><span data-stu-id="23add-122">provides the common functionality needed by other toolkit components.</span></span> | 
   | <span data-ttu-id="23add-123">**Herramientas de Azure Container para Eclipse**</span><span class="sxs-lookup"><span data-stu-id="23add-123">**Azure Container Tools for Eclipse**</span></span> | <span data-ttu-id="23add-124">Permite crear e implementar un artefacto .WAR como un contenedor de Docker en una máquina de Docker.</span><span class="sxs-lookup"><span data-stu-id="23add-124">Enables you to build and deploy a .WAR as a Docker container to a docker machine.</span></span> | 
   | <span data-ttu-id="23add-125">**Azure Containers for Eclipse**</span><span class="sxs-lookup"><span data-stu-id="23add-125">**Azure Containers for Eclipse**</span></span> | <span data-ttu-id="23add-126">Permite implementar un artefacto .WAR o .JAR como un contenedor Docker en una máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="23add-126">Enables you to deploy a .WAR or .JAR artifact as a Docker container to an Azure virtual machine.</span></span> | 
   | <span data-ttu-id="23add-127">**Explorador de Azure para Eclipse**</span><span class="sxs-lookup"><span data-stu-id="23add-127">**Azure Explorer for Eclipse**</span></span> | <span data-ttu-id="23add-128">Proporciona una interfaz de tipo explorador para administrar los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="23add-128">Provides an explorer-style interface for managing your Azure resources.</span></span> | 
   | <span data-ttu-id="23add-129">**Microsoft JDBC Driver 6.1 para SQL Server**</span><span class="sxs-lookup"><span data-stu-id="23add-129">**Microsoft JDBC Driver 6.1 for SQL Server**</span></span> | <span data-ttu-id="23add-130">Proporciona JDBC API para SQL Server y Microsoft Azure SQL Database para Java Platform Enterprise Edition 8.</span><span class="sxs-lookup"><span data-stu-id="23add-130">Provides JDBC API for SQL Server and Microsoft Azure SQL Database for Java Platform Enterprise Edition 8.</span></span> | 
   | <span data-ttu-id="23add-131">**Paquete para bibliotecas de Microsoft Azure para Java**</span><span class="sxs-lookup"><span data-stu-id="23add-131">**Package for Microsoft Azure Libraries for Java**</span></span> | <span data-ttu-id="23add-132">Proporciona las API para acceder a los servicios de Microsoft Azure, como Storage, Service Bus, Service Runtime, etc.</span><span class="sxs-lookup"><span data-stu-id="23add-132">Provides APIs for accessing Microsoft Azure services, such as storage, service bus, service runtime, etc.</span></span> | 

1. <span data-ttu-id="23add-133">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="23add-133">Click **Next**.</span></span> <span data-ttu-id="23add-134">(Si se producen retrasos inusuales al instalar el kit de herramientas, asegúrese de que la opción **Ponerse en contacto con todos los sitios de actualización durante la instalación para encontrar el software necesario** está desactivada.)</span><span class="sxs-lookup"><span data-stu-id="23add-134">(If you experience unusual delays when installing the toolkit, ensure that **Contact all update sites during install to find required software** is unchecked.)</span></span>

1. <span data-ttu-id="23add-135">En el cuadro de diálogo **Install Details** (Detalles de instalación), haga clic en **Next** (Siguiente).</span><span class="sxs-lookup"><span data-stu-id="23add-135">In the **Install Details** dialog, click **Next**.</span></span>
   
   ![Revisión de los detalles de la instalación][03]

1. <span data-ttu-id="23add-137">En el cuadro de diálogo **Revisar licencias** , revise los términos de los contratos de licencia.</span><span class="sxs-lookup"><span data-stu-id="23add-137">In the **Review Licenses** dialog, review the terms of the license agreements.</span></span> <span data-ttu-id="23add-138">Si acepta los términos de los contratos de licencia, haga clic en **I accept the terms of the license agreements** (Acepto los términos de los contratos de licencia) y luego haga clic en **Finish** (Finalizar).</span><span class="sxs-lookup"><span data-stu-id="23add-138">If you accept the terms of the license agreements, click **I accept the terms of the license agreements** and then click **Finish**.</span></span> <span data-ttu-id="23add-139">(En los pasos restantes se supone que acepta los términos de los contratos de licencia.</span><span class="sxs-lookup"><span data-stu-id="23add-139">(The remaining steps assume you do accept the terms of the license agreements.</span></span> <span data-ttu-id="23add-140">Si no acepta los términos de los contratos de licencia, salga del proceso de instalación.)</span><span class="sxs-lookup"><span data-stu-id="23add-140">If you do not accept the terms of the license agreements, exit the installation process.)</span></span>
   
   ![Revisar licencias][04]
   
   <span data-ttu-id="23add-142">Eclipse descargará e instalará los paquetes necesarios.</span><span class="sxs-lookup"><span data-stu-id="23add-142">Eclipse will download and install the requisite packages.</span></span>
   
   ![Progreso de la instalación][05]

1. <span data-ttu-id="23add-144">Si se le solicita que reinicie Eclipse para completar la instalación, haga clic en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="23add-144">If prompted to restart Eclipse to complete installation, click **Yes**.</span></span>
   
   ![Reinicio del símbolo del sistema][06]

## <a name="next-steps"></a><span data-ttu-id="23add-146">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="23add-146">Next steps</span></span>

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
