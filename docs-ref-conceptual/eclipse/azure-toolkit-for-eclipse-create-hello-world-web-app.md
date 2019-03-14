---
title: Creación de una aplicación web Hello World para Azure mediante Eclipse
description: En este tutorial se muestra cómo utilizar el Kit de herramientas de Azure para Eclipse para crear una aplicación web Hello World para Azure.
services: app-service
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
ms.openlocfilehash: c98f966eb17e3fbde877451c8f8fefb21e6bf686
ms.sourcegitcommit: dca98b953fa3149fb2e6aa49e27e843b6df0c6c2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/12/2019
ms.locfileid: "57786894"
---
# <a name="create-a-hello-world-web-app-for-azure-using-eclipse"></a>Creación de una aplicación web Hello World para Azure mediante Eclipse

En este tutorial se muestra cómo crear e implementar una aplicación básica Hello World en Azure como una aplicación web mediante el [Kit de herramientas de Azure para Eclipse].

> [!NOTE]
>
> Para ver la versión de este artículo que usa el [Kit de herramientas de Azure para IntelliJ], consulte [Creación de una aplicación web Hello World para Azure mediante IntelliJ][intellij-hello-world].
>

> [!IMPORTANT]
> 
> El Kit de herramientas de Azure para Eclipse se actualizó en agosto de 2017, con un flujo de trabajo diferente. En este artículo se muestra la creación de una aplicación web Hello World con la versión 3.0.7 (o posterior) del Kit de herramientas de Azure para Eclipse. Si está usando la versión 3.0.6 (o versiones anteriores) del kit de herramientas, debe seguir los pasos descritos en [Creación de una aplicación web Hello World de Azure en Eclipse con el Kit de herramientas heredado][Legacy Version].
> 

Cuando haya completado este tutorial, la aplicación se parecerá a la que se muestra en la siguiente ilustración al verla en un explorador web:

![Versión preliminar de la aplicación Hello World][browse-web-app]

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="create-a-new-web-app-project"></a>Creación de un proyecto de aplicación web nuevo

1. Inicie Eclipse e inicie sesión en su cuenta de Azure siguiendo las instrucciones del artículo [Azure Sign In Instructions for the Azure Toolkit for Eclipse][eclipse-sign-in-instructions].

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

## <a name="deploy-your-web-app-to-azure"></a>Implementación de una aplicación web en Azure

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

1. Después de publicar su sitio web en Azure, puede administrar la aplicación; para ello, haga clic con el botón derecho y seleccione una de las opciones del menú contextual. Estas opciones son: **Start** (Iniciar), **Stop** (Detener) o **Delete** (Eliminar).

   ![Administrar la instancia de App Service][manage-app-service]

## <a name="next-steps"></a>Pasos siguientes

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

Para obtener más información sobre cómo crear Azure Web Apps, consulte [Introducción a Web Apps].

<!-- URL List -->

[Kit de herramientas de Azure para Eclipse]: azure-toolkit-for-eclipse.md
[kit de herramientas de Azure para IntelliJ]: ../intellij/azure-toolkit-for-intellij.md
[intellij-hello-world]: ../intellij/azure-toolkit-for-intellij-create-hello-world-web-app.md
[Introducción a Web Apps]: /azure/app-service/app-service-web-overview
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/
[Legacy Version]: azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version.md

<!-- IMG List -->

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
