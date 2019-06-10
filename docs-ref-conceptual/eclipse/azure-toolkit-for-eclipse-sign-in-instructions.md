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
ms.openlocfilehash: b4b13de38913ae6e7ae2bb09210ac742efc9d0ad
ms.sourcegitcommit: d18d9dce22b7f7af178f756bd341433d24e3c3b5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2019
ms.locfileid: "66575312"
---
# <a name="sign-in-instructions-for-the-azure-toolkit-for-eclipse"></a>Instrucciones de inicio de sesión del kit de herramientas de Azure para Eclipse

El kit de herramientas de Azure para Eclipse proporciona dos métodos para iniciar sesión en su cuenta de Azure:

  - [Iniciar sesión en su cuenta de Azure mediante el inicio de sesión de dispositivo](#sign-in-to-your-azure-account-by-device-login)
  - [Iniciar sesión en su cuenta de Azure mediante entidad de servicio](#sign-in-to-your-azure-account-by-service-principal)

También se proporcionan métodos de [**Cierre de sesión**](#sign-out-of-your-azure-account).

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="sign-in-to-your-azure-account-by-device-login"></a>Inicio de sesión en su cuenta de Azure mediante el inicio de sesión de dispositivo

Para iniciar sesión en Azure mediante el inicio de sesión de dispositivo, haga lo siguiente:

1. Abra el proyecto con Eclipse.

2. Haga clic en **Herramientas** y, luego, en **Azure**y en **Iniciar sesión**.
   ![Menú de Eclipse para iniciar sesión en Azure][I01]

3. En la ventana **Inicio de sesión de Azure**, seleccione **Inicio de sesión de dispositivo** y, luego, haga clic en **Iniciar sesión**.

   ![Ventana Inicio de sesión de Azure con el inicio de sesión de dispositivo seleccionado][I02]

4. Haga clic en **Copiar y abrir** en el cuadro de diálogo **Inicio de sesión de dispositivo de Azure**.

   ![El cuadro de diálogo Inicio de sesión en Microsoft Azure][I03]

> [!NOTE]
>
> Si no se abre el explorador, configure Eclipse para utilizar un explorador externo, como Internet Explorer, Firefox o Chrome:
>
> 1. En Eclipse, abra Preferencias -> General -> Explorador web -> Usar un explorador web externo
>
> 2. Seleccione el explorador que prefiera utilizar
>

5. En el explorador, pegue el código del dispositivo (que se ha copiado al hacer clic en **Copiar y abrir** en el último paso) y, a continuación, haga clic en **Siguiente**.

   ![Explorador de inicio de sesión de dispositivo][I04]

6. Finalmente, en el cuadro de diálogo **Seleccionar suscripciones**, elija las suscripciones que desea usar y, luego, haga clic en **Aceptar**.

   ![Cuadro de diálogo Seleccionar suscripciones][I05]

## <a name="sign-in-to-your-azure-account-by-service-principal"></a>Inicio de sesión en su cuenta de Azure mediante entidad de servicio

Los siguientes pasos lo guiarán por el proceso de creación de un archivo de credenciales que contiene los datos de entidades de servicio. Cuando finalice este proceso, Eclipse usará el archivo de credenciales para iniciar sesión automáticamente en Azure cuando abra el proyecto.

1. Abra el proyecto con Eclipse.

2. Haga clic en **Herramientas** y, luego, en **Azure**y en **Iniciar sesión**.
   ![Comando de inicio de sesión en Azure de Eclipse][A01]

3. En la ventana **Iniciar sesión de Azure**, seleccione **Entidad de servicio**. Si aún no tiene el archivo de autenticación de la entidad de servicio, haga clic en **Nuevo** para crear uno. En caso contrario, haga clic en **Examinar** para abrirlo y vaya al paso 8.

   ![Ventana de inicio de sesión de Azure con la entidad de servicio seleccionada][A02]

4. Haga clic en **Copiar y abrir** en el cuadro de diálogo **Inicio de sesión de dispositivo de Azure**.

   ![El cuadro de diálogo Inicio de sesión en Microsoft Azure][A08]

> [!NOTE]
>
> Si no se abre el explorador, configure Eclipse para utilizar un explorador externo, como Internet Explorer o Chrome:
>
> 1. En Eclipse, abra Preferencias -> General -> Explorador web -> Usar un explorador web externo.
>
> 2. Seleccione el explorador que prefiera utilizar.
>

5. En el explorador, pegue el código del dispositivo (que se ha copiado al hacer clic en **Copiar y abrir** en el último paso) y, a continuación, haga clic en **Siguiente**.

   ![Explorador de inicio de sesión de dispositivo][A03]

6. En la ventana **Create authentication files** (Crear archivos de autenticación), seleccione las suscripciones que desea utilizar, elija el directorio de destino y, luego, haga clic en **Iniciar**.

   ![La ventana Create authentication files (Crear archivos de autenticación)][A04]

7. En el cuadro de diálogo **Estado de creación de entidades de servicio**, una vez que se hayan creado correctamente los archivos, haga clic en **Aceptar**.

   ![El cuadro de diálogo Service Principal Creation Status (Estado de creación de entidades de servicio)][A05]

8. La dirección del archivo creado se rellenará automáticamente en la ventana **Inicio de sesión de Azure**. Ahora, haga clic en **Iniciar sesión**.

   ![Cuadro de diálogo Inicio de sesión en Microsoft Azure][A06]

9. Finalmente, en el cuadro de diálogo **Seleccionar suscripciones**, elija las suscripciones que desea usar y, luego, haga clic en **Aceptar**.

   ![Cuadro de diálogo Seleccionar suscripciones][A07]

## <a name="sign-out-of-your-azure-account"></a>Cierre de sesión en la cuenta de Azure

Después de haber configurado la cuenta con los pasos anteriores, iniciará sesión automáticamente cada vez que inicie Eclipse. Sin embargo, si desea cerrar sesión de su cuenta de Azure, siga estos pasos.

1. En Eclipse, haga clic en **Herramientas** y, luego, en **Azure** y en **Cerrar sesión**.

   ![Menú de Eclipse para cerrar sesión en Azure][L01]

2. Cuando se muestre el cuadro de diálogo **Cierre de sesión en Microsoft Azure** , haga clic en **Sí**.

   ![Cuadro de diálogo Cerrar sesión][L02]

## <a name="next-steps"></a>Pasos siguientes

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<!-- URL List -->


<!-- IMG List -->

[I01]: media/azure-toolkit-for-eclipse-sign-in-instructions/I01.png
[I02]: media/azure-toolkit-for-eclipse-sign-in-instructions/I02.png
[I03]: media/azure-toolkit-for-eclipse-sign-in-instructions/I03.png
[I04]: media/azure-toolkit-for-eclipse-sign-in-instructions/I04.png
[I05]: media/azure-toolkit-for-eclipse-sign-in-instructions/I05.png

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
