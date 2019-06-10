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
# <a name="installing-the-azure-toolkit-for-intellij"></a>Instalación del kit de herramientas de Azure para IntelliJ

El kit de herramientas de Azure para IntelliJ ofrece plantillas y funciones que permiten crear, desarrollar, probar e implementar aplicaciones en la nube en Azure fácilmente con el entorno de desarrollo IntelliJ IDEA.

> [!NOTE] 
> 
> El kit de herramientas de Azure para IntelliJ es un proyecto de código abierto, cuyo código fuente está disponible con la licencia MIT del sitio del proyecto en GitHub en la siguiente dirección URL: 
> 
> <https://github.com/microsoft/azure-tools-for-java> 
> 

Hay dos métodos para instalar el Kit de herramientas de Azure para IntelliJ: mediante el cuadro de diálogo **Configuración** y mediante el menú **Configurar** en la pantalla Inicio. Ambos métodos de instalación se mostrarán en los pasos siguientes.

## <a name="prerequisites"></a>Requisitos previos

Azure Toolkit for IntelliJ requiere los siguientes componentes de software:

* Java Development Kit (JDK) 8+ instalado, por ejemplo: [OpenJDK](https://openjdk.java.net/) o el [JDK de Oracle](https://www.oracle.com/technetwork/java/javase/downloads/index.html)
* [IntelliJ IDEA](https://www.jetbrains.com/idea/download/) Ultimate Edition o Community Edition instalado

> [!NOTE]
> 
> La página [Azure Toolkit for IntelliJ](https://plugins.jetbrains.com/plugin/8053) en el repositorio de complementos de JetBrains muestra las compilaciones que son compatibles con el kit de herramientas.
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


## <a name="to-install-the-azure-toolkit-for-intellij-from-the-settings-dialog-box"></a>Para instalar el kit de herramientas de Azure para IntelliJ desde el cuadro de diálogo Configuración

1. Inicie IntelliJ IDEA.

1. Cuando se abra IntelliJ IDEA, haga clic en **File** (Archivo) y, después, en **Settings** (Configuración).
   
   ![Apertura del cuadro de diálogo Configuración de IntelliJ IDEA][01a]

1. En el cuadro de diálogo Settings (Configuración), haga clic en **Plugins** (Complementos) y, después, en **Browse repositories** (Explorar repositorios).
   
   ![Cuadro de diálogo Configuración de IntelliJ IDEA][02a]

1. En el cuadro de diálogo **Browse repositories** (Explorar repositorios), escriba "Azure" en el cuadro de búsqueda. Resalte **Azure Toolkit for IntelliJ** (Kit de herramientas de Azure para IntelliJ) y, después, haga clic en **Install** (Instalar).
   
   ![Búsqueda del kit de herramientas de Azure para IntelliJ][03]
   
   IntelliJ IDEA muestra el progreso de la instalación en un cuadro de diálogo.
   
   ![Progreso de la instalación][04]

1. Cuando se haya completado la instalación, haga clic en **Restart IntelliJ IDEA**(Reiniciar IntelliJ IDEA).
   
   ![Restart IntelliJ IDEA][05]

1. Haga clic en **Aceptar** para cerrar el cuadro de diálogo Configuración.
   
   ![Cierre del cuadro de diálogo Configuración de IntelliJ IDEA][06]

1. Cuando se le pregunte si desea reiniciar IntelliJ IDEA o posponer el reinicio, haga clic en **Reiniciar**.
   
1   ![Restart IntelliJ IDEA][07]

## <a name="to-install-the-azure-toolkit-for-intellij-from-the-start-screen"></a>Para instalar el kit de herramientas de Azure para IntelliJ desde la pantalla de inicio

1. Inicie IntelliJ IDEA.

1. Cuando aparezca la pantalla de inicio de IntelliJ IDEA, haga clic en **Configure** (Configurar) y, después, en **Plugins** (Complementos).
   
   ![Instalación de los complementos de IntelliJ IDEA][01b]

1. En el cuadro de diálogo **Plugins** (Complementos), haga clic en **Browse repositories** (Explorar repositorios).
   
   ![Exploración de los repositorios de complementos de IntelliJ IDEA][02b]

1. En el cuadro de diálogo **Browse repositories** (Explorar repositorios), escriba "Azure" en el cuadro de búsqueda. Resalte **Azure Toolkit for IntelliJ** (Kit de herramientas de Azure para IntelliJ) y, después, haga clic en **Install** (Instalar).
   
   ![Búsqueda del kit de herramientas de Azure para IntelliJ][03]
   
   IntelliJ IDEA mostrará el progreso de la instalación en un cuadro de diálogo.
   
   ![Progreso de la instalación][04]

1. Cuando se haya completado la instalación, haga clic en **Restart IntelliJ IDEA**(Reiniciar IntelliJ IDEA).
   
   ![Restart IntelliJ IDEA][05]

1. Cuando se le pregunte si desea reiniciar IntelliJ IDEA o posponer el reinicio, haga clic en **Reiniciar**.
   
   ![Restart IntelliJ IDEA][07]

## <a name="next-steps"></a>Pasos siguientes

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
