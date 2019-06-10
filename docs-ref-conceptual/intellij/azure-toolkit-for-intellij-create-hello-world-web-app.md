---
title: Creación de una aplicación web Hello World para Azure App Service mediante IntelliJ
description: En este tutorial se muestra cómo utilizar el Kit de herramientas de Azure para IntelliJ para crear una aplicación web Hello World para Azure.
services: app-service
keywords: java, intellij, aplicación web, azure app service, hello world, guía de inicio rápido
documentationcenter: java
author: selvasingh
manager: routlaw
editor: ''
ms.assetid: 75ce7b36-e3ae-491d-8305-4b42ce37db4e
ms.author: robmcm;asirveda
ms.date: 02/01/2018
ms.devlang: java
ms.service: app-service
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: ae0749ce1ddab971f1a83e2e5e58492fd8ccb287
ms.sourcegitcommit: 733115fe0a7b5109b511b4a32490f8264cf91217
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/15/2019
ms.locfileid: "65626121"
---
# <a name="create-a-hello-world-web-app-for-azure-app-service-using-intellij"></a>Creación de una aplicación web Hello World para Azure App Service mediante IntelliJ

Con el complemento de código abierto [Azure Toolkit for IntelliJ](https://plugins.jetbrains.com/plugin/8053), crear e implementar una aplicación básica Hello World en Azure App Service como una aplicación web se puede llevar a cabo en unos minutos.

> [!NOTE]
>
> Si prefiere usar Eclipse, consulte nuestro [tutorial similar para Eclipse][eclipse-hello-world].
>
>[!INCLUDE [quickstarts-free-trial-note](../includes/quickstarts-free-trial-note.md)]
>
> No se olvide de realizar una limpieza de los recursos después de completar este tutorial. En ese caso, la ejecución de esta guía no superará la cuota de la cuenta gratuita.
>

[!INCLUDE [azure-toolkit-for-intellij-basic-prerequisites](../includes/azure-toolkit-for-intellij-basic-prerequisites.md)]

## <a name="installation-and-sign-in"></a>Instalación e inicio de sesión

1. En el cuadro de diálogo de configuración y preferencias del IntelliJ IDEA (Ctrl+Alt+S), seleccione **Complementos**. A continuación, busque **Azure Toolkit for IntelliJ** en **Marketplace** y haga clic en **Instalar**. Una vez instalado, haga clic en **Reiniciar** para activar el complemento. 

   ![Complemento Azure Toolkit for IntelliJ en Marketplace][marketplace]

2. Para iniciar sesión en la cuenta de Azure, abra **Azure Explorer** y, a continuación, haga clic en el icono **Inicio de sesión de Azure** en la barra de la parte superior (o en el menú IDEA **Herramientas/Azure/Inicio de sesión de Azure**).

   ![El comando de inicio de sesión en Azure IntelliJ][I01]

3. En la ventana **Inicio de sesión de Azure**, seleccione **Inicio de sesión de dispositivo** y, a continuación, haga clic en **Iniciar sesión** ([otras opciones de inicio de sesión](azure-toolkit-for-intellij-sign-in-instructions.md)).

   ![Ventana Inicio de sesión de Azure con el inicio de sesión de dispositivo seleccionado][I02]

4. Haga clic en **Copiar y abrir** en el cuadro de diálogo **Inicio de sesión de dispositivo de Azure**.

   ![El cuadro de diálogo Inicio de sesión en Microsoft Azure][I03]

5. En el explorador, pegue el código del dispositivo (que se ha copiado al hacer clic en **Copiar y abrir** en el último paso) y, a continuación, haga clic en **Siguiente**.

   ![Explorador de inicio de sesión de dispositivo][I04]

6. En el cuadro de diálogo **Seleccionar suscripciones**, elija las suscripciones que desea usar y, luego, haga clic en **Aceptar**.

   ![Cuadro de diálogo Seleccionar suscripciones][I05]

## <a name="creating-web-app-project"></a>Creación del proyecto de aplicación web

1. En IntelliJ, haga clic en el menú **File** (Archivo), luego en **New** (Nuevo) y, finalmente, en **Project** (Proyecto).

   ![Creación de un proyecto][file-new-project]

2. En el cuadro de diálogo **New Project** (Nuevo proyecto), seleccione **Maven**, **maven-archetype-webapp** y haga clic en **Next** (Siguiente).

   ![Elección de una aplicación web de arquetipo Maven][maven-archetype-webapp]

3. Especifique **GroupId** y **ArtifactId** para la aplicación web y haga clic en **Next** (Siguiente).

   ![Especificación de GroupId y ArtifactId][groupid-and-artifactid]

4. Personalice la configuración de Maven o acepte los valores predeterminados y haga clic en **Next** (Siguiente).

   ![Especificación de la configuración de Maven][maven-options]

5. Especifique el nombre y la ubicación del proyecto, y haga clic en **Finish**(Finalizar).

   ![Especificación del nombre del proyecto][project-name]

6. En la vista del explorador de proyectos, abra y edite el archivo **src/main/webapp/index.jsp** tal y como se indica a continuación y **guarde los cambios**:

   ```html
   <html>
    <body>
      <b><% out.println("Hello World!"); %></b>
    </body>
   </html>
   ```

   ![Edición de la página de índice][edit-index-page]

## <a name="deploying-web-app-to-azure"></a>Implementación de la aplicación web en Azure

1. En la vista del explorador de proyectos, haga clic con el botón derecho en el proyecto, expanda **Azure** y, a continuación, haga clic en **Implementar en Azure**.

   ![Menú Implementar en Azure][deploy-to-azure-menu]

1. En el cuadro de diálogo Implementar en Azure, puede implementar directamente la aplicación como una aplicación web de Tomcat existente si ya tiene una; en caso contrario, se debe crear primero una nueva.
   1. Haga clic en el vínculo **No hay aplicación web disponible, haga clic para crear una nueva** para crear una nueva aplicación web, puede elegir **Crear nueva aplicación web** en la lista desplegable de aplicaciones web si hay aplicaciones web existentes en la suscripción.

      ![Cuadro de diálogo Implementar en Azure][deploy-to-azure-dialog]

   1. En el cuadro de diálogo emergente, elija **TOMCAT 8.5-jre8** como contenedor web, especifique otra información necesaria y, a continuación, haga clic en **Aceptar** para crear la aplicación web.

      ![Creación de una aplicación web][create-new-web-app-dialog]

   1. Elija la aplicación web en la lista desplegable de aplicaciones web y, a continuación, haga clic en **Ejecutar**. (Puede empezar desde aquí si desea implementar en una aplicación web existente)

      ![Implementación en una aplicación web existente][deploy-to-existing-webapp]

1. El kit de herramientas mostrará un mensaje de estado cuando se haya implementado correctamente la aplicación web, con la dirección URL de la aplicación web implementada en caso correcto.

   ![Implementación correcta][successfully-deployed]

1. Puede buscar la aplicación web mediante el vínculo que se proporciona en el mensaje de estado.

   ![Búsqueda de la aplicación web][browse-web-app]

## <a name="managing-deploy-configurations"></a>Administración de configuraciones de implementación

1. Después de publicar la aplicación web, la configuración se guardará como valor predeterminado y podrá ejecutar la implementación al hacer clic en el icono de flecha verde de la barra de herramientas. Para modificar esta configuración, haga clic en el menú desplegable de la aplicación web y, luego, en **Edit Configurations** (Editar configuraciones).

   ![Menú Editar configuración][edit-configuration-menu]

1. Cuando aparezca el cuadro de diálogo **Run/Debug Configurations** (Ejecutar/Depurar configuraciones), podrá modificar cualquiera de los valores predeterminados y hacer clic en **OK** (Aceptar).

   ![Cuadro de diálogo Editar configuración][edit-configuration-dialog]

## <a name="cleaning-up-resources"></a>Limpieza de recursos

1. Eliminación de aplicaciones web en el Explorador de Azure

     ![Limpieza de recursos][clean-resources]

## <a name="next-steps"></a>Pasos siguientes

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

Para obtener más información sobre cómo crear Azure Web Apps, consulte [Introducción a Web Apps].

<!-- URL List -->

[Azure Toolkit for IntelliJ]: azure-toolkit-for-intellij.md
[Azure Toolkit for Eclipse]: ../eclipse/azure-toolkit-for-eclipse.md
[eclipse-hello-world]: ../eclipse/azure-toolkit-for-eclipse-create-hello-world-web-app.md
[Introducción a Web Apps]: /azure/app-service/app-service-web-overview
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/
[Legacy Version]: azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version.md
[intelliJ-sign-in-instructions]: azure-toolkit-for-intellij-sign-in-instructions.md

<!-- IMG List -->
[marketplace]:./media/azure-toolkit-for-intellij-create-hello-world-web-app/marketplace.png
[file-new-project]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/file-new-project.png
[maven-archetype-webapp]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/maven-archetype-webapp.png
[groupid-and-artifactid]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/groupid-and-artifactid.png
[maven-options]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/maven-options.png
[project-name]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/project-name.png
[open-index-page]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/open-index-page.png
[edit-index-page]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/edit-index-page.png
[deploy-to-azure-menu]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/run-on-web-app-menu.png
[deploy-to-azure-dialog]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/run-on-web-app-dialog.png
[deploy-to-existing-webapp]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/deploy-to-existing-webapp.png
[create-new-web-app-dialog]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/create-new-web-app-dialog.png
[successfully-deployed]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/successfully-deployed.png
[browse-web-app]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/browse-web-app.png
[edit-configuration-menu]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/edit-configuration-menu.png
[edit-configuration-dialog]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/edit-configuration-dialog.png
[clean-resources]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/clean-resource.png
[I01]: media/azure-toolkit-for-intellij-sign-in-instructions/I01.png
[I02]: media/azure-toolkit-for-intellij-sign-in-instructions/I02.png
[I03]: media/azure-toolkit-for-intellij-sign-in-instructions/I03.png
[I04]: media/azure-toolkit-for-intellij-sign-in-instructions/I04.png
[I05]: media/azure-toolkit-for-intellij-sign-in-instructions/I05.png
