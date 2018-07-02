---
title: ''
description: En este tutorial se muestra cómo utilizar la versión 3.0.6 (o versiones anteriores) del Kit de herramientas de Azure para Eclipse para crear una aplicación web Hello World para Azure.
services: app-service
documentationcenter: java
author: selvasingh
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: robmcm;asirveda
ms.date: 02/01/2018
ms.devlang: java
ms.service: app-service
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: 896e7eff389bc7d3ac119d315c50aae505a381da
ms.sourcegitcommit: 5282a51bf31771671df01af5814df1d2b8e4620c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/28/2018
ms.locfileid: "37090808"
---
# <a name="create-a-hello-world-web-app-for-azure-using-the-legacy-toolkit-for-eclipse"></a>Creación de una aplicación web Hello World para Azure con el kit de herramientas heredado para Eclipse

En este tutorial se muestra cómo crear e implementar una aplicación básica Hello World en Azure como una aplicación web con la versión 3.0.6 (o versiones anteriores) del [Kit de herramientas de Azure para Eclipse].

> [!NOTE]
>
> Para ver la versión de este artículo que usa el [Kit de herramientas de Azure para IntelliJ], consulte [Creación de una aplicación web Hello World para Azure mediante IntelliJ][intellij-hello-world].
>

> [!IMPORTANT]
> 
> El Kit de herramientas de Azure para Eclipse se actualizó en agosto de 2017, con un flujo de trabajo diferente. En este artículo se muestra la creación de una aplicación web Hello World con la versión 3.0.6 (o posterior) del Kit de herramientas de Azure para Eclipse. Si está usando la versión 3.0.7 (o posterior) del Kit de herramientas, debe seguir los pasos descritos en [Creación de una aplicación web Hello World de Azure en Eclipse][Updated Version].
>

Cuando haya completado este tutorial, la aplicación se parecerá a la que se muestra en la siguiente ilustración al verla en un explorador web:

![Versión preliminar de la aplicación Hello World][01]

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="create-a-new-web-app-project"></a>Creación de un proyecto de aplicación web nuevo

1. Inicie Eclipse e inicie sesión en su cuenta de Azure siguiendo las instrucciones del artículo [Instrucciones de inicio de sesión del kit de herramientas de Azure para Eclipse][eclipse-sign-in-instructions].

1. Haga clic en **File** (Archivo), haga clic en **New** (Nuevo) y luego haga clic en **Dynamic Web Project** (Proyecto web dinámico). [Si no ve que **Dynamic Web Project** aparezca como disponible después de hacer clic en **File** (Archivo) y **New** (Nuevo), haga clic en **File** (Archivo), **New** (Nuevo), **Project...** (Proyecto...), expanda **Web**, haga clic en **Dynamic Web Project** (Proyecto web dinámica) y, finalmente, haga clic en **Next** (Siguiente).]

2. Para los fines de este tutorial, asigne el nombre **MyWebApp**al proyecto. La pantalla se parecerá a la siguiente:
   
   ![Creación de un nuevo proyecto web dinámico][02]

3. Haga clic en **Finalizar**

4. En la vista del **Explorador de proyectos** de Eclipse, expanda **MyWebApp**. Haga clic con el botón derecho en **WebContent**, haga clic en **New** (Nuevo) y, después, en **JSP File** (Archivo JSP).

5. En el cuadro de diálogo **New JSP File** (Nuevo archivo JSP), asigne un nombre del archivo **index.jsp**, conserve la carpeta principal como **MyWebApp/WebContent** y haga clic en **Next** (Siguiente).

6. Para este tutorial, en el cuadro de diálogo **Select JSP Template** (Seleccionar plantilla JSP), seleccione **New JSP File (html)** [Nuevo archivo JSP (html)] y haga clic en **Finish** (Finalizar).

7. Cuando el archivo index.jsp se abra en Eclipse, agregue texto para que se muestre dinámicamente **Hello World!** dentro del elemento `<body>` existente. El contenido de `<body>` actualizado debe parecerse al siguiente ejemplo:
   
   ```jsp
   <body><b><% out.println("Hello World!"); %></b></body>
   ```

8. Guarde el archivo index.jsp.

## <a name="deploy-your-web-app-to-azure"></a>Implementación de una aplicación web en Azure

Existen varias maneras de implementar una aplicación web de Java en Azure. En este tutorial se describe una de las más sencillas: la aplicación se implementará en un contenedor de aplicaciones de Azure: no se necesita ningún tipo de proyecto especial ni herramientas adicionales. Azure facilitará el JDK y el software de contenedor web, así que no es necesario que cargue los suyos; lo único que necesita es su aplicación web de Java. Como resultado, el proceso de publicación de su aplicación tardará unos segundos y no minutos.

1. En el Explorador de proyectos de Eclipse, haga clic con el botón derecho en **MyWebApp**.

2. En el menú contextual, seleccione **Azure** y, luego, haga clic en **Publish as Azure Web App...** (Publicar como aplicación web de Azure).
   
   ![Publish as Azure Web App][03]
   
   O bien, con el proyecto de aplicación web seleccionado en el Explorador de proyectos, puede hacer clic en el botón desplegable **Publish** (Publicar) de la barra de herramientas y seleccionar **Publish as Azure Web App** (Publicar como aplicación web de Azure) ahí:
   
   ![Publish as Azure Web App][14]

3. Si aún no ha iniciado sesión en Azure desde Eclipse, se le pedirá que inicie sesión en su cuenta de Azure:
   
   ![Cuadro de diálogo de inicio de sesión en Azure][04]
   
   Si tiene varias cuentas de Azure, puede que algunos de los avisos que aparecen durante el proceso de inicio de sesión se muestren más de una vez, incluso si parecen ser iguales. Cuando esto ocurra, siga la instrucciones de inicio de sesión.

4. Cuando haya iniciado sesión correctamente en su cuenta de Azure, el cuadro de diálogo **Manage Subscriptions** (Administrar suscripciones) mostrará una lista de suscripciones que están asociadas con sus credenciales. Si aparecen varias suscripciones y quiere trabajar solo con un subconjunto específico de ellas, opcionalmente puede desactivar las que no utilice. Cuando haya seleccionado las suscripciones, haga clic en **Cerrar**.
   
   ![Cuadro de diálogo Administrar suscripciones][05]

5. Cuando aparezca el cuadro de diálogo **Deploy to Azure Web App Container** (Implementar en el contenedor de aplicaciones web de Azure), se mostrarán los contenedores de aplicaciones web creados anteriormente; si no ha creado ningún contenedor, la lista estará vacía.
   
   ![Cuadro de diálogo de implementación en contenedor de Azure Web App][06]

6. Si no ha creado un contenedor de aplicaciones web de Azure antes, o si quiere publicar la aplicación en un nuevo contenedor, siga estos pasos. De lo contrario, seleccione un contenedor de aplicaciones web existente y vaya al paso 7 a continuación.
   
   a. Haga clic en **Nuevo...**
      
      ![Cuadro de diálogo de implementación en contenedor de Azure Web App][15]

   b. Se muestra el cuadro de diálogo **New Web App Container** (Nuevo contenedor de aplicaciones web):
      
      ![Cuadro de diálogo de implementación en nuevo contenedor de aplicación web][07a]

   c. Escriba un valor para **Etiqueta DNS** para el contenedor de aplicaciones web; esta será la etiqueta DNS hoja de la dirección URL del host de la aplicación web en Azure. Tenga en cuenta que el nombre debe estar disponible y ajustarse a los requisitos de nomenclatura de las aplicaciones web de Azure.

   d. En el menú desplegable **Web Container** (Contenedor web), seleccione el software adecuado para su aplicación.
      
      Actualmente, puede elegir entre Tomcat 8, Tomcat 7 o Jetty 9. Azure proporcionará una distribución reciente del software seleccionado y se ejecutará en una distribución reciente de JDK 8 creada por Oracle y proporcionada por Azure.

   e. En el menú desplegable **Suscripción** , seleccione la suscripción que quiere usar para esta implementación.

   f. En el menú desplegable **Grupo de recursos** , seleccione el grupo de recursos con el que desea asociar la aplicación web. Los grupos de recursos de Azure permiten agrupar recursos relacionados para que, por ejemplo, se puedan eliminar juntos.
      
      Puede seleccionar un grupo de recursos existente (si tiene alguno) y pasar al paso g a continuación o usar los siguientes pasos para crear un nuevo grupo de recursos:
      
   * Haga clic en **Nuevo...**
   * Se muestra el cuadro de diálogo **Nuevo grupo de recursos** :
        
       ![Cuadro de diálogo Nuevo grupo de recursos][08]
   * En el cuadro de texto **Nombre** , especifique un nombre para el nuevo grupo de recursos.
   * En el menú desplegable **Región** , seleccione la ubicación adecuada del centro de datos de Azure para su grupo de recursos.
   * OPCIONAL: De forma predeterminada, Azure implementará una distribución reciente de Java 8 automáticamente en el contenedor de la aplicación web como la máquina virtual de Java. Sin embargo, puede especificar una versión y una distribución diferentes de la máquina virtual de Java si así lo requiere la aplicación web. Para especificar el JDK de la aplicación web, haga clic en la pestaña **JDK** y seleccione una de las siguientes opciones:
     * **Implementar el JDK predeterminado que ofrece el servicio Azure Web Apps**: esta opción implementará una distribución reciente de Java 8.
     * **Implementar un JDK de terceros disponible en Azure**: esta opción permite elegir en la lista el JDK que proporciona Microsoft Azure.
     * **Implementar mi propio JDK desde esta ubicación de descarga**: esta opción permite especificar su propia distribución JDK, que se debe empaquetar como un archivo ZIP y cargarse en una ubicación de descarga disponible públicamente o en una cuenta de Azure Storage a la que tenga acceso.
          
       ![Cuadro de diálogo de implementación en nuevo contenedor de aplicación web][07b]

   g. Haga clic en **OK**.

   h. En el menú desplegable **Plan de App Service** se muestran los planes de App Service que están asociados con el grupo de recursos seleccionado. Los planes de App Service especifican información como la ubicación de la aplicación web, el plan de tarifas y el tamaño de la instancia de proceso. Un único plan de App Service se puede usar para varias Web Apps, motivo por el cual se mantiene independiente de una implementación específica de Web Apps.)
      
       You can select an existing App Service Plan (if you have any) and skip to step h below, or use the following these steps to create a new App Service Plan:
      
      * Haga clic en **Nuevo...**
      * Se muestra el cuadro de diálogo **Nuevo plan de App Service** :
        
          ![Cuadro de diálogo de nuevo plan de App Service][09]
      * En el cuadro de texto **Nombre** , especifique un nombre para el nuevo plan.
      * En el menú desplegable **Ubicación** , seleccione la ubicación adecuada del centro de datos de Azure para el plan.
      * En el menú desplegable **Plan de tarifa** , seleccione la tarifa adecuada para el plan. Con fines de prueba, puede elegir **Gratis**.
      * En el menú desplegable **Tamaño de instancia** , seleccione el tamaño de instancia adecuado para el plan. Con fines de prueba, puede elegir **Pequeño**.

   i. Cuando haya completado todos los pasos anteriores, el cuadro de diálogo Nuevo contenedor de aplicaciones web debe parecerse al de la siguiente ilustración:
      
      ![Cuadro de diálogo de implementación en nuevo contenedor de aplicación web][10]

   j. Haga clic en **Aceptar** para finalizar la creación de su nuevo contenedor de aplicaciones web.
       
      Espere unos segundos para que se actualice la lista de los contenedores de aplicaciones web y el contenedor recién creado ya debería estar seleccionado en la lista.

7. Ahora está listo para terminar la implementación inicial de la aplicación web en Azure:
   
   ![Cuadro de diálogo de implementación en contenedor de Azure Web App][11]
   
   Haga clic en **Aceptar** para implementar su aplicación Java en el contenedor de aplicaciones web seleccionado.
   
   De forma predeterminada, la aplicación se implementará como un subdirectorio del servidor de aplicaciones. Si desea que se implemente como aplicación raíz, active la casilla **Deploy to root** (Implementar en raíz) antes de hacer clic en **OK** (Aceptar).

8. A continuación, debería mostrarse la vista **Azure Activity Log** (Registro de actividad de Azure), que indicará el estado de implementación de la aplicación web.
   
   ![Azure Activity Log][12]
   
   El proceso de implementación de la aplicación web en Azure debería tardar solo unos segundos en completarse. Cuando su aplicación esté lista, verá un vínculo denominado **Publicado** in the **Status** (Estado). Al hacer clic en el vínculo, irá a la página principal de la aplicación web implementada.

## <a name="updating-your-web-app"></a>Actualización de la aplicación web

Actualizar una aplicación web de Azure existente es un proceso rápido y sencillo, y tiene dos opciones para ello:

* Puede actualizar la implementación de una aplicación web de Java existente.
* Puede publicar una aplicación Java adicional en el mismo contenedor de aplicaciones web.

En cualquier caso, el proceso es idéntico y tarda unos pocos segundos:

1. En el Explorador de proyectos de Eclipse, haga clic con el botón derecho en la aplicación Java que quiere actualizar o agregar a un contenedor de aplicaciones web existente.

2. Cuando aparezca el menú contextual, seleccione **Azure** y, después, haga clic en **Publish as Azure Web App...** (Publicar como aplicación web de Azure).

3. Puesto que ya ha iniciado sesión anteriormente, verá una lista de contenedores de aplicaciones web existentes. Seleccione aquel en el que quiere publicar o volver a publicar la aplicación Java y haga clic en **Aceptar**.

Unos segundos más tarde, la vista **Azure Activity Log** (Registro de actividad de Azure) mostrará la implementación actualizada como **Published** (Publicado) y podrá comprobar la aplicación actualizada en un explorador web.

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a>Inicio, detención o reinicio de una aplicación web existente

Para iniciar o detener un contenedor de aplicaciones web existente (junto con todas las aplicaciones Java implementadas en él), puede utilizar la vista **Azure Explorer** (Explorador de Azure).

Si la vista **Azure Explorer** (Explorador de Azure) no está abierta, puede abrirla; para ello, haga clic en el menú **Window** (Ventana) en Eclipse, luego en **Show View** (Mostrar vista), **Other...** (Otra), **Azure** y, finalmente, en **Azure Explorer (Explorador de Azure)**. Si anteriormente no ha iniciado sesión, se le pedirá que lo haga.

Cuando se muestre la vista **Azure Explorer** (Explorador de Azure), siga estos pasos para iniciar o detener su aplicación web: 

1. Expanda el nodo **Azure** .

2. Expanda el nodo **Web Apps** . 

3. Haga clic en la aplicación web deseada.

4. Cuando aparezca el menú contextual, haga clic en **Iniciar**, **Detener** o **Reiniciar**. Tenga en cuenta que las opciones de menú dependen del contexto, por lo que solo podrá detener una aplicación web que se encuentre en ejecución o iniciar una aplicación web que no se esté ejecutando en ese momento.
   
   ![Detención de una aplicación web existente][13]

## <a name="next-steps"></a>Pasos siguientes

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

Para obtener más información sobre cómo crear Azure Web Apps, consulte [Introducción a Web Apps].

<!-- URL List -->

[kit de herramientas de Azure para Eclipse]: azure-toolkit-for-eclipse.md
[kit de herramientas de Azure para IntelliJ]: ../intellij/azure-toolkit-for-intellij.md
[intellij-hello-world]: ../intellij/azure-toolkit-for-intellij-create-hello-world-web-app.md
[Introducción a Web Apps]: /azure/app-service/app-service-web-overview
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/
[Updated Version]: azure-toolkit-for-eclipse-create-hello-world-web-app.md
[eclipse-sign-in-instructions]: azure-toolkit-for-eclipse-sign-in-instructions.md


<!-- IMG List -->

[01]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/01-Web-Page.png
[02]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/02-Dynamic-Web-Project.png
[03]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/03-Context-Menu.png
[04]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/04-Log-In-Dialog.png
[05]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/05-Manage-Subscriptions-Dialog.png
[06]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/06-Deploy-To-Azure-Web-Container.png
[07a]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/07a-New-Web-App-Container-Dialog.png
[07b]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/07b-New-Web-App-Container-Dialog.png
[08]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/08-New-Resource-Group-Dialog.png
[09]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/09-New-Service-Plan-Dialog.png
[10]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/10-Completed-Web-App-Container-Dialog.png
[11]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/11-Completed-Deploy-Dialog.png
[12]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/12-Activity-Log-View.png
[13]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/13-Azure-Explorer-Web-App.png
[14]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/14-publishDropdownButton.png
[15]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/15-New-Azure-Web-Container.png
