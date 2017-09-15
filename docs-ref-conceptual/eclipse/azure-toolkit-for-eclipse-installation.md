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
# <a name="installing-the-azure-toolkit-for-eclipse"></a>Instalación del Kit de herramientas de Azure para Eclipse

El kit de herramientas de Azure para Eclipse ofrece plantillas y funciones que permiten crear, desarrollar, probar e implementar aplicaciones de Azure fácilmente con el entorno de desarrollo de Eclipse. El kit de herramientas de Azure para Eclipse es un proyecto de código abierto. El código fuente está disponible bajo la licencia MIT en <https://github.com/microsoft/azure-tools-for-java>.

En los pasos siguientes se muestra cómo instalar el Kit de herramientas de Azure para Eclipse.

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="to-install-the-azure-toolkit-for-eclipse"></a>Para instalar el Kit de herramientas de Azure para Eclipse

1. Inicie Eclipse.

1. Haga clic en el menú **Help** (Ayuda) y, a continuación, haga clic en **Install New Software** (Instalar nuevo software), como se muestra en la siguiente ilustración.
   
   ![Instalación del Kit de herramientas de Azure para Eclipse][01]

1. En el cuadro de diálogo **Available Software** (Software disponible), en el cuadro de texto **Work with** (Trabajar con), escriba `http://dl.microsoft.com/eclipse/` seguido de la tecla **Intro**.

1. En el panel **Nombre**, active **Kit de herramientas de Azure para Eclipse**, y desactive **Ponerse en contacto con todos los sitios de actualización durante la instalación para encontrar el software necesario**. La pantalla debe parecerse a la siguiente:
   
   ![Instalación del Kit de herramientas de Azure para Eclipse][02]

1. Si expande el **kit de herramientas de Azure para Eclipse**, verá una lista de elementos como la del siguiente ejemplo:
   
   * **Complemento de Application Insights para Java**: este componente permite usar los servicios de análisis y registro de telemetría de Azure para sus aplicaciones e instancias de servidor.
   * **Filtro de Azure Access Control Service**: este componente proporciona compatibilidad para autenticar a los usuarios de aplicaciones con ACS de Azure, lo que permite poner en práctica escenarios de inicio de sesión único y externalizar la lógica de identidades de la aplicación.
   * **Complemento común de Azure**: este componente proporciona la funcionalidad habitual necesaria para otros componentes del kit de herramientas.
   * **Explorador de Azure para Eclipse**: este componente proporciona la funcionalidad habitual necesaria para otros componentes del kit de herramientas.
   * **Complemento de Azure para Eclipse con Java**: este componente respalda el desarrollo de proyectos que lo ayudan a crear, probar e implementar aplicaciones de Java para la nube de Microsoft Azure en Eclipse y mediante la línea de comandos.
   * **Complemento de Azure Web Apps con Java**: este componente permite implementar aplicaciones web de Java en los contenedores de aplicaciones web de Microsoft Azure.
   * **Microsoft JDBC Driver 4.2 para SQL Server**: este componente proporciona la API de JDBC API para SQL Server y Microsoft Azure SQL Database para Java Platform Enterprise Edition 8.
   * **Paquete para bibliotecas de cliente Apache Qpid de JMS**: este componente ofrece el componente de cliente JMS del proyecto de Apache Qpid para habilitar su aplicación para que use la mensajería de AMQP en Microsoft Azure.
   * **Paquete para bibliotecas de Microsoft Azure para Java**: este componente proporciona las API para acceder a los servicios de Microsoft Azure, como almacenamiento, service bus, runtime de servicio, etc.

1. Haga clic en **Siguiente**. (Si se producen retrasos inusuales al instalar el kit de herramientas, asegúrese de que la opción **Ponerse en contacto con todos los sitios de actualización durante la instalación para encontrar el software necesario** está desactivada.)

1. En el cuadro de diálogo **Install Details** (Detalles de instalación), haga clic en **Next** (Siguiente).
   
   ![Revisión de los detalles de la instalación][03]

1. En el cuadro de diálogo **Revisar licencias** , revise los términos de los contratos de licencia. Si acepta los términos de los contratos de licencia, haga clic en **I accept the terms of the license agreements** (Acepto los términos de los contratos de licencia) y luego haga clic en **Finish** (Finalizar). (En los pasos restantes se supone que acepta los términos de los contratos de licencia. Si no acepta los términos de los contratos de licencia, salga del proceso de instalación.)
   
   ![Revisar licencias][04]
   
   Eclipse descargará e instalará los paquetes necesarios.
   
   ![Progreso de la instalación][05]

1. Si se le solicita que reinicie Eclipse para completar la instalación, haga clic en **Sí**.
   
   ![Reinicio del símbolo del sistema][06]

## <a name="next-steps"></a>Pasos siguientes

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
