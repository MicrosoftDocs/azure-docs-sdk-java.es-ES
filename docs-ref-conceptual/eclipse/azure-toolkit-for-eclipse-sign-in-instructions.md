---
title: Instrucciones de inicio de sesión del kit de herramientas de Azure para Eclipse
description: Obtenga información sobre cómo iniciar sesión en Microsoft Azure utilizando el Kit de herramientas de Azure para Eclipse.
services: ''
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 02/01/2018
ms.devlang: Java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: 79f6cfd3b21d68c131a3f0052d86e4bcb3254e55
ms.sourcegitcommit: 115f4c8ad07a11f17d79e9d945d63917836b11c8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "61591070"
---
# <a name="azure-sign-in-instructions-for-the-azure-toolkit-for-eclipse"></a>Instrucciones de inicio de sesión del kit de herramientas de Azure para Eclipse

El kit de herramientas de Azure para Eclipse proporciona dos métodos para iniciar sesión en su cuenta de Azure:

  * **Automatizado**: al utilizar este método, se creará un archivo de credenciales que contiene los datos de entidades de seguridad de servicio. Después, podrá utilizar el archivo de credenciales para iniciar sesión automáticamente en su cuenta de Azure.
  * **Interactivo**: al usar este método, deberá especificar sus credenciales de Azure cada vez que inicie sesión en su cuenta de Azure.

Los pasos descritos en las secciones siguientes explican cómo utilizar cada método.

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="signing-into-your-azure-account-automatically-and-creating-a-credentials-file-to-use-in-the-future"></a>Inicio de sesión en su cuenta de Azure de forma automática y creación de un archivo de credenciales para utilizarlo en el futuro

Los siguientes pasos lo guiarán por el proceso de creación de un archivo de credenciales que contiene los datos de entidades de seguridad de servicio. Cuando finalice estos pasos, Eclipse usará automáticamente el archivo de credenciales para iniciar sesión automáticamente en Azure cada vez que abra el proyecto.

1. Abra el proyecto con Eclipse.

1. Haga clic en **Herramientas** y, luego, en **Azure**y en **Iniciar sesión**.

   ![Menú de Eclipse para iniciar sesión en Azure][A01]

1. Cuando se muestra el cuadro de diálogo **Inicio de sesión en Microsoft Azure**, seleccione **Automatizado** y, luego, haga clic en **Nuevo**.

   ![Cuadro de diálogo Iniciar sesión][A02]

1. Cuando se muestre el cuadro de diálogo **Inicio de sesión en Microsoft Azure**, escriba sus credenciales de Azure y, luego, haga clic en **Iniciar sesión**.

   ![Cuadro de diálogo Inicio de sesión en Microsoft Azure][A03]

1. Cuando se muestre el cuadro de diálogo **Create authentication files** (Crear archivos de autenticación), seleccione las suscripciones que desea utilizar, elija el directorio de destino y, luego, haga clic en **Iniciar**.

   ![Cuadro de diálogo Inicio de sesión en Microsoft Azure][A04]

1. Se mostrará el cuadro de diálogo **Service Principal Creation Status** (Estado de creación de entidades de servicio) y, una vez que se hayan creado correctamente los archivos, haga clic en **Aceptar**.

   ![Cuadro de diálogo Service Principal Creation Status (Estado de creación de entidades de servicio)][A05]

1. Cuando se muestre el cuadro de diálogo **Inicio de sesión en Microsoft Azure** , haga clic en **Iniciar sesión**.

   ![Cuadro de diálogo Inicio de sesión en Microsoft Azure][A06]

1. Cuando se muestre el cuadro de diálogo **Seleccionar suscripciones**, seleccione las suscripciones que desea usar y, luego, haga clic en **Aceptar**.

   ![Cuadro de diálogo Seleccionar suscripciones][A07]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-automatically"></a>Cierre de sesión de la cuenta de Azure al iniciar sesión de forma automática

Después de haber configurado los pasos en la sección anterior, el kit de herramientas de Azure cerrará automáticamente la sesión de su cuenta de Azure cada vez que reinicie Eclipse. Sin embargo, para cerrar la sesión de su cuenta de Azure e impedir que el kit de herramientas de Azure inicie sesión automáticamente, siga estos pasos.

1. En Eclipse, haga clic en **Herramientas** y, luego, en **Azure** y en **Cerrar sesión**.

   ![Menú de Eclipse para cerrar sesión en Azure][L01]

1. Cuando se muestre el cuadro de diálogo **Cierre de sesión en Microsoft Azure** , haga clic en **Sí**.

   ![Cuadro de diálogo Cerrar sesión][L03]

## <a name="signing-into-your-azure-account-automatically-using-a-credentials-file-which-you-have-already-created"></a>Inicio de sesión en su cuenta de Azure de forma automática y uso de un archivo de credenciales existente

Si cierra la sesión de Azure al utilizar Eclipse, debe volver a configurar el kit de herramientas de Azure para Eclipse con el fin de usar un archivo de credenciales ya creado antes de poder iniciar sesión automáticamente en su cuenta de Azure. Los siguientes pasos lo guiarán a través del proceso de configuración del kit de herramientas de Azure para usar un archivo de credenciales existente.

1. Abra el proyecto con Eclipse.

1. Haga clic en **Herramientas** y, luego, en **Azure**y en **Iniciar sesión**.

   ![Menú de Eclipse para iniciar sesión en Azure][A01]

1. Cuando se muestra el cuadro de diálogo **Inicio de sesión en Microsoft Azure**, seleccione **Automatizado** y, luego, haga clic en **Examinar**.

   ![Cuadro de diálogo Iniciar sesión][A02]

1. Cuando se muestra el cuadro de diálogo **Select Authentication File** (Seleccionar archivo de autenticación), elija un archivo de credenciales que creó anteriormente y, luego, haga clic en **Open** (Abrir).

   ![Cuadro de diálogo Iniciar sesión][A08]

1. Cuando se muestre el cuadro de diálogo **Inicio de sesión en Microsoft Azure**, haga clic en **Iniciar sesión**.

   ![Cuadro de diálogo Inicio de sesión en Microsoft Azure][A06]

1. Cuando se muestre el cuadro de diálogo **Seleccionar suscripciones**, seleccione las suscripciones que desea usar y, luego, haga clic en **Aceptar**.

   ![Cuadro de diálogo Seleccionar suscripciones][A07]

## <a name="signing-into-your-azure-account-interactively"></a>Inicio de sesión en la cuenta de Azure de forma interactiva

En los pasos siguientes se explica cómo iniciar sesión en Azure especificando manualmente las credenciales de Azure.

1. Abra el proyecto con Eclipse.

1. Haga clic en **Herramientas** y, luego, en **Azure**y en **Iniciar sesión**.

   ![Menú de Eclipse para iniciar sesión en Azure][I01]

1. Cuando se muestra el cuadro de diálogo **Inicio de sesión en Microsoft Azure**, seleccione **Interactivo** y, luego, haga clic en **Iniciar sesión**.

   ![Cuadro de diálogo Iniciar sesión][I02]

1. Cuando se muestre el cuadro de diálogo **Inicio de sesión en Microsoft Azure**, escriba sus credenciales de Azure y, luego, haga clic en **Iniciar sesión**.

   ![Cuadro de diálogo Inicio de sesión en Microsoft Azure][I03]

1. Cuando se muestre el cuadro de diálogo **Seleccionar suscripciones**, seleccione las suscripciones que desea usar y, luego, haga clic en **Aceptar**.

   ![Cuadro de diálogo Seleccionar suscripciones][I04]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-interactively"></a>Cierre de sesión de la cuenta de Azure al iniciar sesión de forma interactiva

Después de haber configurado los pasos en la sección anterior, se cerrará automáticamente la sesión de su cuenta de Azure cada vez que reinicie Eclipse. Sin embargo, si desea cerrar sesión de su cuenta de Azure sin tener que reiniciar Eclipse, siga estos pasos.

1. En Eclipse, haga clic en **Herramientas** y, luego, en **Azure** y en **Cerrar sesión**.

   ![Menú de Eclipse para cerrar sesión en Azure][L01]

1. Cuando se muestre el cuadro de diálogo **Cierre de sesión en Microsoft Azure** , haga clic en **Sí**.

   ![Cuadro de diálogo Cerrar sesión][L02]

## <a name="next-steps"></a>Pasos siguientes

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<!-- URL List -->


<!-- IMG List -->

[I01]: media/azure-toolkit-for-eclipse-sign-in-instructions/I01.png
[I02]: media/azure-toolkit-for-eclipse-sign-in-instructions/I02.png
[I03]: media/azure-toolkit-for-eclipse-sign-in-instructions/I03.png
[I04]: media/azure-toolkit-for-eclipse-sign-in-instructions/I04.png

[A01]: media/azure-toolkit-for-eclipse-sign-in-instructions/A01.png
[A02]: media/azure-toolkit-for-eclipse-sign-in-instructions/A02.png
[A03]: media/azure-toolkit-for-eclipse-sign-in-instructions/A03.png
[A04]: media/azure-toolkit-for-eclipse-sign-in-instructions/A04.png
[A05]: media/azure-toolkit-for-eclipse-sign-in-instructions/A05.png
[A06]: media/azure-toolkit-for-eclipse-sign-in-instructions/A06.png
[A07]: media/azure-toolkit-for-eclipse-sign-in-instructions/A07.png
[A08]: media/azure-toolkit-for-eclipse-sign-in-instructions/A08.png

[L01]: media/azure-toolkit-for-eclipse-sign-in-instructions/L01.png
[L02]: media/azure-toolkit-for-eclipse-sign-in-instructions/L02.png
[L03]: media/azure-toolkit-for-eclipse-sign-in-instructions/L03.png
