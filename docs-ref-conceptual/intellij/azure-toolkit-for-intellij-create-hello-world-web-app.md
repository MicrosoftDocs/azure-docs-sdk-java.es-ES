---
title: "Creación de una aplicación web Hello World para Azure mediante IntelliJ"
description: "En este tutorial se muestra cómo utilizar el Kit de herramientas de Azure para IntelliJ para crear una aplicación web Hello World para Azure."
services: app-service
documentationcenter: java
author: selvasingh
manager: routlaw
editor: 
ms.assetid: 75ce7b36-e3ae-491d-8305-4b42ce37db4e
ms.author: robmcm;asirveda
ms.date: 02/01/2018
ms.devlang: java
ms.service: app-service
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: cc68e16a6940a1f0f2b08f0b63c90c58ec6dbc4e
ms.sourcegitcommit: 151aaa6ccc64d94ed67f03e846bab953bde15b4a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/03/2018
---
# <a name="create-a-hello-world-web-app-for-azure-using-intellij"></a>Creación de una aplicación web Hello World para Azure mediante IntelliJ

En este tutorial se muestra cómo crear e implementar una aplicación básica Hola mundo en Azure como una aplicación web mediante el [Kit de herramientas de Azure para IntelliJ].

> [!NOTE]
>
> Para ver la versión de este artículo que usa el [Kit de herramientas de Azure para Eclipse], consulte [Creación de una aplicación web Hello World para Azure mediante Eclipse][eclipse-hello-world].
>

> [!IMPORTANT]
> 
> El Kit de herramientas de Azure para IntelliJ se actualizó en agosto de 2017, con un flujo de trabajo diferente. En este artículo se muestra la creación de una aplicación web Hello World con la versión 3.0.7 (o posterior) del Kit de herramientas de Azure para IntelliJ. Si está usando la versión 3.0.6 (o anterior) del kit de herramientas, debe seguir los pasos descritos en [Creación de una aplicación web Hello World de Azure en IntelliJ con el Kit de herramientas heredado][Legacy Version].
> 

Cuando haya completado este tutorial, la aplicación se parecerá a la que se muestra en la siguiente ilustración al verla en un explorador web:

![Versión preliminar de la aplicación Hello World][browse-web-app]

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="create-a-new-web-app-project"></a>Creación de un proyecto de aplicación web nuevo

1. Inicie IntelliJ e inicie sesión en su cuenta de Azure siguiendo las instrucciones del artículo [Instrucciones de inicio de sesión del kit de herramientas de Azure para IntelliJ][intelliJ-sign-in-instructions].

1. Haga clic en el menú **File** (Archivo), luego en **New** (Nuevo) y, finalmente, en **Project** (Proyecto).
   
   ![Creación de un proyecto][file-new-project]

1. En el cuadro de diálogo **New Project** (Nuevo proyecto), seleccione **Maven**, **maven-archetype-webapp** y haga clic en **Next** (Siguiente).
   
   ![Elección de una aplicación web de arquetipo Maven][maven-archetype-webapp]
   
1. Especifique **GroupId** y **ArtifactId** para la aplicación web y haga clic en **Next** (Siguiente).
   
   ![Especificación de GroupId y ArtifactId][groupid-and-artifactid]

1. Personalice la configuración de Maven o acepte los valores predeterminados y haga clic en **Next** (Siguiente).
   
   ![Especificación de la configuración de Maven][maven-options]

1. Especifique el nombre y la ubicación del proyecto, y haga clic en **Finish**(Finalizar).
   
   ![Especificación del nombre del proyecto][project-name]

1. En la vista del explorador de proyectos de IntelliJ, expanda **src**, después, **main**, luego, **webapp** y, a continuación, haga doble clic en **index.jsp**.
   
   ![Apertura de la página de índice][open-index-page]

1. Cuando el archivo index.jsp se abra en IntelliJ, agregue texto para que se muestre dinámicamente **Hello World!** dentro del elemento `<body>` existente. El contenido de `<body>` actualizado debe parecerse al siguiente ejemplo:
   
   ```java
   <body><b><% out.println("Hello World!"); %></b></body>
   ``` 

   ![Edición de la página de índice][edit-index-page]

1. Guarde el archivo index.jsp.

## <a name="deploy-your-web-app-to-azure"></a>Implementación de una aplicación web en Azure

1. En la vista del explorador de proyectos de IntelliJ, haga clic con el botón derecho en el proyecto, elija **Azure** y **Run on Web App** (Ejecutar en aplicación web).
   
   ![Menú Run on Web App (Ejecutar en aplicación web)][run-on-web-app-menu]

1. En el cuadro de diálogo Run on Web App (Ejecutar en aplicación web), puede elegir una de las siguientes opciones:

   * Elija una aplicación web existente (si existe) y haga clic en **Run** (Ejecutar).

      ![Cuadro de diálogo Run on Web App (Ejecutar en aplicación web)][run-on-web-app-dialog]

   * Haga clic en **Create New Web App** (Crear aplicación web nueva). Si decide crear una aplicación web, especifique la información necesaria para ella y haga clic en **Run** (Ejecutar).

      ![Creación de una aplicación web][create-new-web-app-dialog]

1. El kit de herramientas mostrará un mensaje de estado cuando se haya implementado correctamente la aplicación web y la dirección URL de esta.

   ![Implementación correcta][successfully-deployed]

1. Puede buscar la aplicación web mediante el vínculo que se proporciona en el mensaje de estado.

   ![Búsqueda de la aplicación web][browse-web-app]

1. Después de publicar la aplicación web, la configuración se guardará como valor predeterminado y podrá ejecutar la aplicación en Azure al hacer clic en el icono de flecha verde de la barra de herramientas. Para modificar esta configuración, haga clic en el menú desplegable de la aplicación web y, luego, en **Edit Configurations** (Editar configuraciones).

   ![Menú Editar configuración][edit-configuration-menu]

1. Cuando aparezca el cuadro de diálogo **Run/Debug Configurations** (Ejecutar/Depurar configuraciones), podrá modificar cualquiera de los valores predeterminados y hacer clic en **OK** (Aceptar).

   ![Cuadro de diálogo Editar configuración][edit-configuration-dialog]

## <a name="next-steps"></a>pasos siguientes

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

Para obtener más información sobre cómo crear Azure Web Apps, consulte [Introducción a Web Apps].

<!-- URL List -->

[Kit de herramientas de Azure para IntelliJ]: azure-toolkit-for-intellij.md
[Kit de herramientas de Azure para Eclipse]: ../eclipse/azure-toolkit-for-eclipse.md
[eclipse-hello-world]: ../eclipse/azure-toolkit-for-eclipse-create-hello-world-web-app.md
[Introducción a Web Apps]: /azure/app-service/app-service-web-overview
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/
[Legacy Version]: azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version.md
[intelliJ-sign-in-instructions]: azure-toolkit-for-intellij-sign-in-instructions.md

<!-- IMG List -->

[file-new-project]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/file-new-project.png
[maven-archetype-webapp]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/maven-archetype-webapp.png
[groupid-and-artifactid]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/groupid-and-artifactid.png
[maven-options]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/maven-options.png
[project-name]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/project-name.png
[open-index-page]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/open-index-page.png
[edit-index-page]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/edit-index-page.png
[run-on-web-app-menu]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/run-on-web-app-menu.png
[run-on-web-app-dialog]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/run-on-web-app-dialog.png
[create-new-web-app-dialog]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/create-new-web-app-dialog.png
[successfully-deployed]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/successfully-deployed.png
[browse-web-app]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/browse-web-app.png
[edit-configuration-menu]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/edit-configuration-menu.png
[edit-configuration-dialog]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/edit-configuration-dialog.png
