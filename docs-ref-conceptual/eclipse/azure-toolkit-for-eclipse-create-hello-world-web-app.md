---
title: Creación de una aplicación web Hello World para Azure App Service mediante Eclipse
description: En este tutorial se muestra cómo utilizar el Kit de herramientas de Azure para Eclipse para crear una aplicación web Hello World para Azure.
services: app-service
keywords: java, eclipse, aplicación web, azure app service, hello world, guía de inicio rápido
documentationcenter: java
author: selvasingh
manager: routlaw
editor: ''
ms.assetid: 20d41e88-9eab-462e-8ee3-89da71e7a33f
ms.author: robmcm;asirveda
ms.date: 02/01/2018
ms.devlang: java
ms.service: app-service
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: 7e88298afaf0b4601d85d6063b7096c79e677421
ms.sourcegitcommit: 733115fe0a7b5109b511b4a32490f8264cf91217
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/15/2019
ms.locfileid: "65625855"
---
# <a name="create-a-hello-world-web-app-for-azure-app-service-using-eclipse"></a>Creación de una aplicación web Hello World para Azure App Service mediante Eclipse

Con el complemento de código abierto [Azure Toolkit for Eclipse](https://marketplace.eclipse.org/content/azure-toolkit-eclipse), crear e implementar una aplicación básica Hello World en Azure App Service como una aplicación web se puede llevar a cabo en unos minutos.

> [!NOTE]
>
> Si prefiere usar IntelliJ IDEA, consulte nuestro [tutorial similar para IntelliJ][intellij-hello-world].
>
>[!INCLUDE [quickstarts-free-trial-note](../includes/quickstarts-free-trial-note.md)]
>
> No se olvide de realizar una limpieza de los recursos después de completar este tutorial. En ese caso, la ejecución de esta guía no superará la cuota de la cuenta gratuita.
>

[!INCLUDE [azure-toolkit-for-intellij-basic-prerequisites](../includes/azure-toolkit-for-eclipse-basic-prerequisites.md)]

## <a name="installation-and-sign-in"></a>Instalación e inicio de sesión

1. Arrastre el botón siguiente al área de trabajo de Eclipse en ejecución para instalar el complemento Azure Toolkit for Eclipse ([otras opciones de instalación](azure-toolkit-for-eclipse-installation.md)).

    [![Arrastrar al área de trabajo de Eclipse* en ejecución. *Requiere el cliente de Marketplace de Eclipse](https://marketplace.eclipse.org/sites/all/themes/solstice/public/images/marketplace/btn-install.png)](http://marketplace.eclipse.org/marketplace-client-intro?mpc_install=1919278 "Arrastrar al área de trabajo de Eclipse* en ejecución. *Requiere el cliente de Marketplace de Eclipse")

1. Para iniciar sesión en la cuenta de Azure, haga clic en **Herramientas**, a continuación, haga clic en **Azure** y, a continuación, haga clic en **Iniciar sesión**.
   ![Menú de Eclipse para iniciar sesión en Azure][I01]

1. En la ventana **Inicio de sesión de Azure**, seleccione **Inicio de sesión de dispositivo** y, a continuación, haga clic en **Iniciar sesión** ([otras opciones de inicio de sesión](azure-toolkit-for-eclipse-sign-in-instructions.md)).

   ![Ventana Inicio de sesión de Azure con el inicio de sesión de dispositivo seleccionado][I02]

1. Haga clic en **Copiar y abrir** en el cuadro de diálogo **Inicio de sesión de dispositivo de Azure**.

   ![El cuadro de diálogo Inicio de sesión en Microsoft Azure][I03]

1. En el explorador, pegue el código del dispositivo (que se ha copiado al hacer clic en **Copiar y abrir** en el último paso) y, a continuación, haga clic en **Siguiente**.

   ![Explorador de inicio de sesión de dispositivo][I04]

1. Finalmente, en el cuadro de diálogo **Seleccionar suscripciones**, elija las suscripciones que desea usar y, luego, haga clic en **Aceptar**.

   ![Cuadro de diálogo Seleccionar suscripciones][I05]

## <a name="creating-web-app-project"></a>Creación del proyecto de aplicación web

1. Haga clic en **File** (Archivo), haga clic en **New** (Nuevo) y luego haga clic en **Dynamic Web Project** (Proyecto web dinámico). [Si no ve que **Dynamic Web Project** aparezca como disponible después de hacer clic en **File** (Archivo) y **New** (Nuevo), haga clic en **File** (Archivo), **New** (Nuevo), **Project...** (Proyecto...), expanda **Web**, haga clic en **Dynamic Web Project** (Proyecto web dinámica) y, finalmente, haga clic en **Next** (Siguiente).]

   ![Creación de un nuevo proyecto web dinámico][file-new-dynamic-web-project]

2. Para los fines de este tutorial, asigne el nombre **MyWebApp**al proyecto. La pantalla se parecerá a la siguiente:
   
   ![Propiedades de New Dynamic Web Project (Nuevo proyecto web dinámico)][dynamic-web-project-properties]

3. Haga clic en **Finalizar**

4. En la vista del explorador de proyectos de Eclipse, expanda **MyWebApp**. Haga clic con el botón derecho en **WebContent**, haga clic en **New** (Nuevo) y, después, en **JSP File** (Archivo JSP).

   ![Crear un archivo JSP nuevo][create-new-jsp-file]

5. En el cuadro de diálogo **New JSP File** (Nuevo archivo JSP), asigne un nombre del archivo **index.jsp**, conserve la carpeta principal como **MyWebApp/WebContent** y haga clic en **Next** (Siguiente).

   ![Cuadro de diálogo Nuevo archivo JSP][new-jsp-file-dialog]

6. Para este tutorial, en el cuadro de diálogo **Select JSP Template** (Seleccionar plantilla JSP), seleccione **New JSP File (html)** [Nuevo archivo JSP (html)] y haga clic en **Finish** (Finalizar).

   ![Seleccionar la plantilla JSP][select-jsp-template]

7. Cuando el archivo index.jsp se abra en Eclipse, agregue texto para que se muestre dinámicamente **Hello World!** dentro del elemento `<body>` existente. El contenido de `<body>` actualizado debe parecerse al siguiente ejemplo:
   
   ```jsp
   <body><b><% out.println("Hello World!"); %></b></body>
   ```

8. Guarde el archivo index.jsp.

## <a name="deploying-web-app-to-azure"></a>Implementación de la aplicación web en Azure

1. En la vista del explorador de proyectos de Eclipse, haga clic con el botón derecho en el proyecto, elija **Azure** y **Publish as Azure Web App** (Publicar como aplicación web de Azure).
   
   ![Publish as Azure Web App][publish-as-azure-web-app]

1. En el cuadro de diálogo **Deploy Web App** (Implementar aplicación web) que aparece, puede elegir una de las siguientes opciones:

   * Seleccione una aplicación web si ya existe una.

      ![Selección de la instancia de App Service][select-app-service]

   * Haga clic en **Create New Web App** (Crear aplicación web nueva).

      ![Creación de un elemento App Service][create-app-service]

      Especifique la información necesaria para la aplicación web en el cuadro de diálogo **Create App Service** (Crear servicio de aplicaciones) y haga clic en **Crear** (Ejecutar).

      Aquí puede configurar el entorno de tiempo de ejecución, la configuración de la aplicación, el plan de servicio y el grupo de recursos.

      ![Cuadro de diálogo Crear servicio de aplicaciones][create-app-service-dialog]

1. Seleccione la aplicación web y haga clic en **Deploy** (Implementar).

   ![Implementar instancia de App Service][deploy-app-service]

1. El kit de herramientas mostrará el estado **Publicado** en la pestaña **Registro de actividad de Azure** cuando se haya implementado correctamente la aplicación web, con un hipervínculo a la dirección URL de la aplicación web implementada.

   ![Estado de publicación][publish-status]

1. Puede buscar la aplicación web mediante el vínculo que se proporciona en el mensaje de estado.

   ![Búsqueda de la aplicación web][browse-web-app]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="cleaning-up-resources"></a>Limpieza de recursos

1. Después de publicar la aplicación web en Azure, puede administrarla; para ello, haga clic con el botón derecho en el explorador de Azure y seleccione una de las opciones del menú contextual. Por ejemplo, puede **Eliminar** la aplicación web aquí para limpiar los recursos de este tutorial.

   ![Administrar la instancia de App Service][manage-app-service]

## <a name="next-steps"></a>Pasos siguientes

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

Para obtener más información sobre cómo crear Azure Web Apps, consulte [Introducción a Web Apps].

<!-- URL List -->

[Azure Toolkit for Eclipse]: azure-toolkit-for-eclipse.md
[Azure Toolkit for IntelliJ]: ../intellij/azure-toolkit-for-intellij.md
[intellij-hello-world]: ../intellij/azure-toolkit-for-intellij-create-hello-world-web-app.md
[Introducción a Web Apps]: /azure/app-service/app-service-web-overview
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/
[Legacy Version]: azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version.md

<!-- IMG List -->
[I01]: media/azure-toolkit-for-eclipse-sign-in-instructions/I01.png
[I02]: media/azure-toolkit-for-eclipse-sign-in-instructions/I02.png
[I03]: media/azure-toolkit-for-eclipse-sign-in-instructions/I03.png
[I04]: media/azure-toolkit-for-eclipse-sign-in-instructions/I04.png
[I05]: media/azure-toolkit-for-eclipse-sign-in-instructions/I05.png

[browse-web-app]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/browse-web-app.png
[file-new-dynamic-web-project]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/file-new-dynamic-web-project.png
[dynamic-web-project-properties]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/dynamic-web-project-properties.png
[create-new-jsp-file]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/create-new-jsp-file.png
[new-jsp-file-dialog]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/new-jsp-file-dialog.png
[select-jsp-template]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/select-jsp-template.png
[publish-as-azure-web-app]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/publish-as-azure-web-app.png
[deploy-web-app-dialog]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/deploy-web-app-dialog.png
[select-app-service]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/select-app-service.png
[create-app-service-dialog]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/create-app-service-dialog.png
[publish-status]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/publish-status.png
[create-app-service]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/create-app-service.png
[deploy-app-service]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/deploy-app-service.png
[manage-app-service]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/manage-app-service.png
