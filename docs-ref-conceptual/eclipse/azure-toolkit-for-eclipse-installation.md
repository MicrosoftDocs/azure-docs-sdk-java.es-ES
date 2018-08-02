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
ms.sourcegitcommit: 798f4d4199d3be9fc5c9f8bf7a754d7393de31ae
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/08/2018
ms.locfileid: "33887755"
---
# <a name="install-the-azure-toolkit-for-eclipse"></a>Instalación del kit de herramientas de Azure para Eclipse

El kit de herramientas de Azure para Eclipse ofrece plantillas y funciones que permiten crear, desarrollar, probar e implementar aplicaciones en la nube en Azure fácilmente desde el entorno de desarrollo Eclipse.

> [!NOTE] 
> 
> El kit de herramientas de Azure para Eclipse es un proyecto de código abierto, cuyo código fuente está disponible con la licencia MIT del sitio del proyecto en GitHub en la siguiente dirección URL: 
> 
> <https://github.com/microsoft/azure-tools-for-java> 
> 

En los pasos siguientes se muestra cómo instalar el Kit de herramientas de Azure para Eclipse.

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="to-install-the-azure-toolkit-for-eclipse"></a>Para instalar el Kit de herramientas de Azure para Eclipse

1. Inicie Eclipse.

1. Haga clic en el menú **Help** (Ayuda) y, a continuación, haga clic en **Install New Software** (Instalar nuevo software), como se muestra en la siguiente ilustración.
   
   ![Instalación del Kit de herramientas de Azure para Eclipse][01]

1. En el cuadro de diálogo **Available Software** (Software disponible), en el cuadro de texto **Work with** (Trabajar con), escriba `http://dl.microsoft.com/eclipse/` seguido de la tecla **Intro**.

1. En el panel **Nombre**, active **Kit de herramientas de Azure para Java** y desactive **Ponerse en contacto con todos los sitios de actualización durante la instalación para encontrar el software necesario**. La pantalla debe parecerse a la siguiente:
   
   ![Instalación del Kit de herramientas de Azure para Eclipse][02]

1. Si expande **Azure Toolkit for Eclipse**, verá una lista de los componentes que se instalarán; por ejemplo:

   | Característica | DESCRIPCIÓN | 
   |---|---| 
   | **Complemento de Application Insights para Java** | Permite usar los servicios de análisis y registro de telemetría de Azure para sus aplicaciones e instancias de servidor. | 
   | **Complemento común de Azure** | Proporciona la funcionalidad habitual necesaria para otros componentes del kit de herramientas. | 
   | **Herramientas de Azure Container para Eclipse** | Permite crear e implementar un artefacto .WAR como un contenedor de Docker en una máquina de Docker. | 
   | **Azure Containers for Eclipse** | Permite implementar un artefacto .WAR o .JAR como un contenedor Docker en una máquina virtual de Azure. | 
   | **Explorador de Azure para Eclipse** | Proporciona una interfaz de tipo explorador para administrar los recursos de Azure. | 
   | **Microsoft JDBC Driver 6.1 para SQL Server** | Proporciona JDBC API para SQL Server y Microsoft Azure SQL Database para Java Platform Enterprise Edition 8. | 
   | **Paquete para bibliotecas de Microsoft Azure para Java** | Proporciona las API para acceder a los servicios de Microsoft Azure, como Storage, Service Bus, Service Runtime, etc. | 

1. Haga clic en **Next**. (Si se producen retrasos inusuales al instalar el kit de herramientas, asegúrese de que la opción **Ponerse en contacto con todos los sitios de actualización durante la instalación para encontrar el software necesario** está desactivada.)

1. En el cuadro de diálogo **Install Details** (Detalles de instalación), haga clic en **Next** (Siguiente).
   
   ![Revisión de los detalles de la instalación][03]

1. En el cuadro de diálogo **Revisar licencias** , revise los términos de los contratos de licencia. Si acepta los términos de los contratos de licencia, haga clic en **I accept the terms of the license agreements** (Acepto los términos de los contratos de licencia) y luego haga clic en **Finish** (Finalizar). (En los pasos restantes se supone que acepta los términos de los contratos de licencia. Si no acepta los términos de los contratos de licencia, salga del proceso de instalación.)
   
   ![Revisar licencias][04]
   
   Eclipse descargará e instalará los paquetes necesarios.
   
   ![Progreso de la instalación][05]

1. Si se le solicita que reinicie Eclipse para completar la instalación, haga clic en **Sí**.
   
   ![Reinicio del símbolo del sistema][06]

## <a name="next-steps"></a>Pasos siguientes

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
