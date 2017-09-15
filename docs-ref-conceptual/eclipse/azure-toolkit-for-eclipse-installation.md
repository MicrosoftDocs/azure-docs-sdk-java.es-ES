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
ms.date: 09/11/2017
ms.author: robmcm
ms.openlocfilehash: 59a8bfb6ab4db8ea8c6c9025ca3ced8a13192628
ms.sourcegitcommit: 256044d7cbce16dcb8dc4e195d0f63c10cb44d4e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/13/2017
---
# <a name="installing-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="d90d1-103">Instalación del Kit de herramientas de Azure para Eclipse</span><span class="sxs-lookup"><span data-stu-id="d90d1-103">Installing the Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="d90d1-104">El kit de herramientas de Azure para Eclipse ofrece plantillas y funciones que permiten crear, desarrollar, probar e implementar aplicaciones de Azure fácilmente con el entorno de desarrollo de Eclipse.</span><span class="sxs-lookup"><span data-stu-id="d90d1-104">The Azure Toolkit for Eclipse provides templates and functionality that allow you to easily create, develop, test, and deploy Azure applications using the Eclipse development environment.</span></span> <span data-ttu-id="d90d1-105">El kit de herramientas de Azure para Eclipse es un proyecto de código abierto.</span><span class="sxs-lookup"><span data-stu-id="d90d1-105">The Azure Toolkit for Eclipse is an Open Source project.</span></span> <span data-ttu-id="d90d1-106">El código fuente está disponible bajo la licencia MIT en <https://github.com/microsoft/azure-tools-for-java>.</span><span class="sxs-lookup"><span data-stu-id="d90d1-106">The source code is available under the MIT License from <https://github.com/microsoft/azure-tools-for-java>.</span></span>

<span data-ttu-id="d90d1-107">En los pasos siguientes se muestra cómo instalar el Kit de herramientas de Azure para Eclipse.</span><span class="sxs-lookup"><span data-stu-id="d90d1-107">The following steps show you how to install the Azure Toolkit for Eclipse.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="to-install-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="d90d1-108">Para instalar el Kit de herramientas de Azure para Eclipse</span><span class="sxs-lookup"><span data-stu-id="d90d1-108">To install the Azure Toolkit for Eclipse</span></span>

1. <span data-ttu-id="d90d1-109">Inicie Eclipse.</span><span class="sxs-lookup"><span data-stu-id="d90d1-109">Start Eclipse.</span></span>

1. <span data-ttu-id="d90d1-110">Haga clic en el menú **Help** (Ayuda) y, a continuación, haga clic en **Install New Software** (Instalar nuevo software), como se muestra en la siguiente ilustración.</span><span class="sxs-lookup"><span data-stu-id="d90d1-110">Click the **Help** menu, and then click **Install New Software**, as shown in the following illustration.</span></span>
   
   ![Instalación del Kit de herramientas de Azure para Eclipse][01]

1. <span data-ttu-id="d90d1-112">En el cuadro de diálogo **Available Software** (Software disponible), en el cuadro de texto **Work with** (Trabajar con), escriba `http://dl.microsoft.com/eclipse/` seguido de la tecla **Intro**.</span><span class="sxs-lookup"><span data-stu-id="d90d1-112">In the **Available Software** dialog, within the **Work with** text box, type `http://dl.microsoft.com/eclipse/` followed by the **Enter** key.</span></span>

1. <span data-ttu-id="d90d1-113">En el panel **Nombre**, active **Kit de herramientas de Azure para Eclipse**, y desactive **Ponerse en contacto con todos los sitios de actualización durante la instalación para encontrar el software necesario**.</span><span class="sxs-lookup"><span data-stu-id="d90d1-113">In the **Name** pane, check **Azure Toolkit for Eclipse**, and uncheck **Contact all update sites during install to find required software**.</span></span> <span data-ttu-id="d90d1-114">La pantalla debe parecerse a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="d90d1-114">Your screen should appear similar to the following:</span></span>
   
   ![Instalación del Kit de herramientas de Azure para Eclipse][02]

1. <span data-ttu-id="d90d1-116">Si expande el **kit de herramientas de Azure para Eclipse**, verá una lista de elementos como la del siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="d90d1-116">If you expand the **Azure Toolkit for Eclipse**, you will see a list of items like following example:</span></span>
   
   * <span data-ttu-id="d90d1-117">**Complemento de Application Insights para Java**: este componente permite usar los servicios de análisis y registro de telemetría de Azure para sus aplicaciones e instancias de servidor.</span><span class="sxs-lookup"><span data-stu-id="d90d1-117">**Application Insights Plugin for Java**: This component allows you to use Azure's telemetry logging and analysis services for your applications and server instances.</span></span>
   * <span data-ttu-id="d90d1-118">**Filtro de Azure Access Control Service**: este componente proporciona compatibilidad para autenticar a los usuarios de aplicaciones con ACS de Azure, lo que permite poner en práctica escenarios de inicio de sesión único y externalizar la lógica de identidades de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d90d1-118">**Azure Access Control Services Filter**: This component provides support for authenticating application users with Azure ACS, enabling single sign-on scenarios and externalizing identity logic from the application.</span></span>
   * <span data-ttu-id="d90d1-119">**Complemento común de Azure**: este componente proporciona la funcionalidad habitual necesaria para otros componentes del kit de herramientas.</span><span class="sxs-lookup"><span data-stu-id="d90d1-119">**Azure Common Plugin**: This component provides the common functionality needed by other toolkit components.</span></span>
   * <span data-ttu-id="d90d1-120">**Explorador de Azure para Eclipse**: este componente proporciona la funcionalidad habitual necesaria para otros componentes del kit de herramientas.</span><span class="sxs-lookup"><span data-stu-id="d90d1-120">**Azure Explorer for Eclipse**: This component provides the common functionality needed by other toolkit components.</span></span>
   * <span data-ttu-id="d90d1-121">**Complemento de Azure para Eclipse con Java**: este componente respalda el desarrollo de proyectos que lo ayudan a crear, probar e implementar aplicaciones de Java para la nube de Microsoft Azure en Eclipse y mediante la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="d90d1-121">**Azure Plugin for Eclipse with Java**: This component provides support for developing projects that help build, test and deploy Java applications for the Microsoft Azure cloud in Eclipse and via command line.</span></span>
   * <span data-ttu-id="d90d1-122">**Complemento de Azure Web Apps con Java**: este componente permite implementar aplicaciones web de Java en los contenedores de aplicaciones web de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="d90d1-122">**Azure Web Apps Plugin with Java**: This component provides support for deploying Java web applications to Microsoft Azure Web App containers.</span></span>
   * <span data-ttu-id="d90d1-123">**Microsoft JDBC Driver 4.2 para SQL Server**: este componente proporciona la API de JDBC API para SQL Server y Microsoft Azure SQL Database para Java Platform Enterprise Edition 8.</span><span class="sxs-lookup"><span data-stu-id="d90d1-123">**Microsoft JDBC Driver 4.2 for SQL Server**: This component provides JDBC API for SQL Server and Microsoft Azure SQL Database for Java Platform Enterprise Edition 8.</span></span>
   * <span data-ttu-id="d90d1-124">**Paquete para bibliotecas de cliente Apache Qpid de JMS**: este componente ofrece el componente de cliente JMS del proyecto de Apache Qpid para habilitar su aplicación para que use la mensajería de AMQP en Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="d90d1-124">**Package for Apache Qpid Client Libraries for JMS**: This component provides the JMS client component from the Apache Qpid project to enable your application to use AMQP messaging in Microsoft Azure.</span></span>
   * <span data-ttu-id="d90d1-125">**Paquete para bibliotecas de Microsoft Azure para Java**: este componente proporciona las API para acceder a los servicios de Microsoft Azure, como almacenamiento, service bus, runtime de servicio, etc.</span><span class="sxs-lookup"><span data-stu-id="d90d1-125">**Package for Microsoft Azure Libraries for Java**: This component provides APIs for accessing Microsoft Azure services, such as storage, service bus, service runtime, etc.</span></span>

1. <span data-ttu-id="d90d1-126">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="d90d1-126">Click **Next**.</span></span> <span data-ttu-id="d90d1-127">(Si se producen retrasos inusuales al instalar el kit de herramientas, asegúrese de que la opción **Ponerse en contacto con todos los sitios de actualización durante la instalación para encontrar el software necesario** está desactivada.)</span><span class="sxs-lookup"><span data-stu-id="d90d1-127">(If you experience unusual delays when installing the toolkit, ensure that **Contact all update sites during install to find required software** is unchecked.)</span></span>

1. <span data-ttu-id="d90d1-128">En el cuadro de diálogo **Install Details** (Detalles de instalación), haga clic en **Next** (Siguiente).</span><span class="sxs-lookup"><span data-stu-id="d90d1-128">In the **Install Details** dialog, click **Next**.</span></span>
   
   ![Revisión de los detalles de la instalación][03]

1. <span data-ttu-id="d90d1-130">En el cuadro de diálogo **Revisar licencias** , revise los términos de los contratos de licencia.</span><span class="sxs-lookup"><span data-stu-id="d90d1-130">In the **Review Licenses** dialog, review the terms of the license agreements.</span></span> <span data-ttu-id="d90d1-131">Si acepta los términos de los contratos de licencia, haga clic en **I accept the terms of the license agreements** (Acepto los términos de los contratos de licencia) y luego haga clic en **Finish** (Finalizar).</span><span class="sxs-lookup"><span data-stu-id="d90d1-131">If you accept the terms of the license agreements, click **I accept the terms of the license agreements** and then click **Finish**.</span></span> <span data-ttu-id="d90d1-132">(En los pasos restantes se supone que acepta los términos de los contratos de licencia.</span><span class="sxs-lookup"><span data-stu-id="d90d1-132">(The remaining steps assume you do accept the terms of the license agreements.</span></span> <span data-ttu-id="d90d1-133">Si no acepta los términos de los contratos de licencia, salga del proceso de instalación.)</span><span class="sxs-lookup"><span data-stu-id="d90d1-133">If you do not accept the terms of the license agreements, exit the installation process.)</span></span>
   
   ![Revisar licencias][04]
   
   <span data-ttu-id="d90d1-135">Eclipse descargará e instalará los paquetes necesarios.</span><span class="sxs-lookup"><span data-stu-id="d90d1-135">Eclipse will download and install the requisite packages.</span></span>
   
   ![Progreso de la instalación][05]

1. <span data-ttu-id="d90d1-137">Si se le solicita que reinicie Eclipse para completar la instalación, haga clic en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="d90d1-137">If prompted to restart Eclipse to complete installation, click **Yes**.</span></span>
   
   ![Reinicio del símbolo del sistema][06]

## <a name="next-steps"></a><span data-ttu-id="d90d1-139">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d90d1-139">Next steps</span></span>

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<!-- URL List -->

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690946.aspx -->

<!-- IMG List -->

[01]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-01.png
[02]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-02.png
[03]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-03.png
[04]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-04.png
[05]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-05.png
[06]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-06.png
