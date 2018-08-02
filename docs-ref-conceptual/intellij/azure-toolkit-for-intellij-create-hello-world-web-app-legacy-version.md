---
title: Creación de una aplicación web Hello World para Azure con el kit de herramientas heredado para IntelliJ
description: En este tutorial se muestra cómo utilizar la versión 3.0.6 (o versiones anteriores) del Kit de herramientas de Azure para IntelliJ para crear una aplicación web Hello World para Azure.
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
ms.openlocfilehash: efc1dffa248987772827bbe7bc0caa9f10a0b4ef
ms.sourcegitcommit: 5282a51bf31771671df01af5814df1d2b8e4620c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/28/2018
ms.locfileid: "37090788"
---
# <a name="create-a-hello-world-web-app-for-azure-using-the-legacy-toolkit-for-intellij"></a>Creación de una aplicación web Hello World para Azure con el kit de herramientas heredado para IntelliJ

En este tutorial se muestra cómo crear e implementar una aplicación básica Hola mundo en Azure como una aplicación web mediante la versión 3.0.6 (o versiones anteriores) del [Kit de herramientas de Azure para IntelliJ].

> [!NOTE]
>
> Para ver la versión de este artículo que usa el [Kit de herramientas de Azure para Eclipse], consulte [Creación de una aplicación web Hello World para Azure mediante Eclipse][eclipse-hello-world].
>

> [!IMPORTANT]
> 
> El Kit de herramientas de Azure para IntelliJ se actualizó en agosto de 2017, con un flujo de trabajo diferente. En este artículo se muestra la creación de una aplicación web Hello World con la versión 3.0.6 (o posterior) del Kit de herramientas de Azure para IntelliJ. Si está usando la versión 3.0.7 (o posterior) del Kit de herramientas, debe seguir los pasos descritos en [Creación de una aplicación web Hello World de Azure en IntelliJ][Updated Version].
>

Cuando haya completado este tutorial, la aplicación se parecerá a la que se muestra en la siguiente ilustración al verla en un explorador web:

![Versión preliminar de la aplicación Hello World][01]

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="create-a-new-web-app-project"></a>Creación de un proyecto de aplicación web nuevo

1. Inicie IntelliJ e inicie sesión en su cuenta de Azure siguiendo las instrucciones del artículo [Instrucciones de inicio de sesión del kit de herramientas de Azure para IntelliJ][intelliJ-sign-in-instructions].

1. Haga clic en el menú **File** (Archivo), luego en **New** (Nuevo) y, finalmente, en **Project** (Proyecto).
   
   ![Archivo Nuevo Proyecto][02]

2. En el cuadro de diálogo **New Project** (Nuevo proyecto), seleccione **Java** y **Web Application** (Aplicación web) y, después, haga clic en **New** (Nuevo) para agregar un SDK del proyecto.
   
   ![Cuadro de diálogo Nuevo proyecto][03a]
   
3. En el cuadro de diálogo Select Home Directory for JDK (Seleccionar directorio de inicio para JDK), seleccione la carpeta donde está instalado el JDK y, después, haga clic en **Aceptar**. Haga clic en **Siguiente** en el cuadro de diálogo de nuevo proyecto para continuar.
   
   ![Especificación del directorio de inicio de JDK][03b]

4. Para este tutorial, asigne al proyecto el nombre **Java-Web-App-On-Azure** y haga clic en **Finish** (Finalizar).
   
   ![Cuadro de diálogo Nuevo proyecto][04]

5. En la vista del explorador de proyectos de IntelliJ, expanda **Java-Web-App-On-Azure**, después expanda **web** y, luego, haga doble clic en **index.jsp**.
   
   ![Abrir página de índice][05c]

6. Cuando el archivo index.jsp se abra en IntelliJ, agregue texto para que se muestre dinámicamente **Hello World!** dentro del elemento `<body>` existente. El contenido de `<body>` actualizado debe parecerse al siguiente ejemplo:
   
   ```java
   <body><b><% out.println("Hello World!"); %></b></body>
   ```

7. Guarde el archivo index.jsp.

## <a name="deploy-your-web-app-to-azure"></a>Implementación de una aplicación web en Azure

Existen varias maneras de implementar una aplicación web de Java en Azure. En este tutorial se describe una de las más sencillas: la aplicación se implementará en un contenedor de aplicaciones de Azure: no se necesita ningún tipo de proyecto especial ni herramientas adicionales. Azure facilitará el JDK y el software de contenedor web, así que no es necesario que cargue los suyos; lo único que necesita es su aplicación web de Java. Como resultado, el proceso de publicación de su aplicación tardará unos segundos y no minutos.

Antes de publicar la aplicación, primero debe configurar el módulo. Para ello, siga estos pasos:

1. En el Explorador de proyectos de IntelliJ, haga clic con el botón derecho en el proyecto **Java-Web-App-On-Azure** . Cuando aparezca el menú contextual, haga clic en **Open Module Settings** (Abrir configuración del módulo).

   ![Abrir configuración del módulo][05a]

2. Cuando se muestre el cuadro de diálogo Project Structure (Estructura de proyecto):

   a. Haga clic en **Artefactos** en la lista de **configuración del proyecto**.

   b. Cambie el nombre del artefacto en el cuadro **Nombre** para que contenga un espacio en blanco o caracteres especiales; esto es necesario porque el nombre se usará en el identificador uniforme de recursos (URI).

   c. Cambiar el **tipo** a **Aplicación Web: archivo**.

   d. Haga clic en **OK** (Aceptar) para cerrar el cuadro de diálogo Project Structure (Estructura del proyecto).

   ![Abrir configuración del módulo][05b]

Cuando se ha configurado el módulo, puede publicar la aplicación en Azure mediante los pasos siguientes:

1. En el Explorador de proyectos de IntelliJ, haga clic con el botón derecho en el proyecto **Java-Web-App-On-Azure** . Cuando aparezca el menú contextual, seleccione **Azure** y, después, haga clic en **Publish as Azure Web App...** (Publicar como aplicación web de Azure)
   
   ![Menú contextual de publicación de Azure][06]

2. Si aún no ha iniciado sesión en Azure desde IntelliJ, se le pedirá que lo haga. (Si tiene varias cuentas de Azure, puede que algunos de los avisos que aparecen durante el proceso de inicio de sesión se muestren más de una vez, incluso si parecen iguales. Cuando esto ocurra, siga la instrucciones de inicio de sesión).
   
   ![Cuadro de diálogo de inicio de sesión de Azure][07]

3. Cuando haya iniciado sesión correctamente en su cuenta de Azure, el cuadro de diálogo **Administrar suscripciones** mostrará una lista de suscripciones asociadas a sus credenciales. Si aparecen varias suscripciones y quiere trabajar solo con un subconjunto específico de ellas, opcionalmente puede desactivar las que no utilice. Cuando haya seleccionado las suscripciones, haga clic en **Cerrar**.
   
   ![Administrar suscripciones][08]

4. Cuando aparezca el cuadro de diálogo **Deploy to Azure Web App Container** (Implementar en el contenedor de aplicaciones web de Azure), se mostrarán los contenedores de aplicaciones web creados anteriormente; si no ha creado ningún contenedor, la lista estará vacía.
   
   ![Contenedores de aplicaciones][09]

5. Si no ha creado un contenedor de aplicaciones web de Azure antes, o si quiere publicar la aplicación en un nuevo contenedor, siga estos pasos. De lo contrario, seleccione un contenedor de aplicaciones web existente y vaya al paso 6 que encontrará a continuación.
   
   a. Haga clic en el signo **+**.
      
      ![Agregar contenedor de aplicaciones][10]

   b. Se mostrará el cuadro de diálogo **New Web App Container** (Nuevo contenedor de aplicaciones web), que se usará para los siguientes pasos.
      
      ![Nuevo contenedor de aplicaciones][11a]
   
   c. Escriba un valor para **Etiqueta DNS** para el contenedor de aplicaciones web; esta será la etiqueta DNS hoja de la dirección URL del host de la aplicación web en Azure. Tenga en cuenta que el nombre debe estar disponible y se ajusta a los requisitos de nomenclatura de las aplicaciones web de Azure.

   d. En el menú desplegable **Web Container** (Contenedor web), seleccione el software adecuado para su aplicación.
      
      Actualmente, puede elegir entre Tomcat 8, Tomcat 7 o Jetty 9. Azure proporcionará una distribución reciente del software seleccionado y se ejecutará en una distribución reciente de JDK 8 creada por Oracle y proporcionada por Azure.

   e. En el menú desplegable **Suscripción** , seleccione la suscripción que quiere usar para esta implementación.

   f. En el menú desplegable **Grupo de recursos** , seleccione el grupo de recursos con el que desea asociar la aplicación web. Los grupos de recursos de Azure permiten agrupar recursos relacionados para que, por ejemplo, se puedan eliminar juntos.
      
      Puede seleccionar un grupo de recursos existente (si tiene alguno) y pasar al paso g a continuación o usar los siguientes pasos para crear un nuevo grupo de recursos:
      
      * Seleccione **&lt;&lt; Crear nuevo grupo de recursos&gt;&gt;** en el menú desplegable **Grupo de recursos**.
      * Se muestra el cuadro de diálogo **Nuevo grupo de recursos** :
        
         ![Nuevo grupo de recursos][12]

      * En el cuadro de texto **Nombre**, especifique un nombre para el nuevo grupo de recursos.
      * En el menú desplegable **Región**, seleccione la ubicación adecuada del centro de datos de Azure para el grupo de recursos.
      * Haga clic en **OK**.

   g. En el menú desplegable **Plan de App Service** se muestran los planes de App Service que están asociados con el grupo de recursos seleccionado. (Un plan de App Service especifica información como la ubicación de la aplicación web, el plan de tarifa y el tamaño de la instancia de proceso. Un único plan de App Service se puede usar para varias Web Apps, motivo por el cual se mantiene independiente de una implementación específica de Web Apps.)
      
      Puede seleccionar un plan de plan de App Service existente (si tiene alguno) y pasar al paso h a continuación o usar los siguientes pasos para crear un nuevo plan:
      
      * Seleccione **&lt;&lt; Crear nuevo plan de App Service&gt;&gt;** en el menú desplegable **Plan de App Service**.
      * Se muestra el cuadro de diálogo **Nuevo plan de App Service** :
        
         ![Nuevo plan de App Service][13]

      * En el cuadro de texto **Nombre**, especifique un nombre para el nuevo plan de App Service.
      * En el menú desplegable **Ubicación**, seleccione la ubicación adecuada del centro de datos de Azure para el plan.
      * En el menú desplegable **Plan de tarifa**, seleccione la tarifa adecuada para el plan. Con fines de prueba, puede elegir **Gratis**.
      * En el menú desplegable **Tamaño de instancia**, seleccione el tamaño de instancia adecuado para el plan. Con fines de prueba, puede elegir **Pequeño**.
      * Haga clic en **OK**.

   h. (Opcional) De manera predeterminada, Azure implementará automáticamente una distribución reciente de Java 8 como máquina virtual de Java en el contenedor de la aplicación. Sin embargo, puede seleccionar una versión y una distribución diferentes de la máquina virtual de Java. Para ello, siga estos pasos:
      
   * Haga clic en la pestaña **JDK** en el cuadro de diálogo **New Web App Container** (Nuevo contenedor de aplicaciones web).
   * Puede elegir una de las siguientes opciones:
        
      * Implementar el JDK predeterminado que ofrece Azure
      * Implementar un JDK de terceros de lista desplegable de JDK adicionales que están disponibles en Azure
      * Implementar un JDK personalizado, que debe estar empaquetado en un archivo ZIP y bien estar disponible públicamente o en su cuenta de Azure Storage
        
     ![Pestaña JDK de nuevo contenedor de aplicaciones][11b]

   i. Cuando haya completado todos los pasos anteriores, el cuadro de diálogo Nuevo contenedor de aplicaciones web debe parecerse al de la siguiente ilustración:
      
      ![Nuevo contenedor de aplicaciones][14]
   
   j. Haga clic en **Aceptar** para finalizar la creación de su nuevo contenedor de aplicaciones web.
       
      Espere unos segundos para que se actualice la lista de los contenedores de aplicaciones web y el contenedor recién creado ya debería estar seleccionado en la lista.

6. Ya puede completar la implementación inicial de su aplicación web en Azure; haga clic en **Aceptar** para implementar la aplicación de Java en el contenedor de aplicación web seleccionado. De forma predeterminada, la aplicación se implementará como un subdirectorio del servidor de aplicaciones. Si desea que se implemente como aplicación raíz, active la casilla **Deploy to root** (Implementar en raíz) antes de hacer clic en **OK** (Aceptar).
   
   ![Implementar en Azure][15]

7. A continuación, debería mostrarse la vista **Azure Activity Log** (Registro de actividad de Azure), que indicará el estado de implementación de la aplicación web.
   
   ![Indicador de progreso][16]
   
   El proceso de implementación de la aplicación web en Azure debería tardar solo unos segundos en completarse. Cuando la aplicación esté lista, verá un vínculo denominado **Publicado** en la columna **Estado**. Al hacer clic en el vínculo, se le llevará a la página principal de la aplicación web implementada. Por otro lado, puede utilizar los pasos de la sección siguiente para ir a la aplicación web.

## <a name="browsing-to-your-web-app-on-azure"></a>Desplazamiento hasta su aplicación web en Azure

Para ir a su aplicación web en Azure, puede usar la vista **Azure Explorer**.

Si la vista del **Explorador de Azure** no está abierta, puede abrirla haciendo clic en el menú **View** (Ver) de IntelliJ, luego haga clic en **Tool Windows** (Ventanas de herramientas) y, después, en **Service Explorer** (Explorador de servicios). Si anteriormente no ha iniciado sesión, se le pedirá que lo haga.

Cuando se muestre la vista **Azure Explorer** (Explorador de Azure), siga estos pasos para buscar la aplicación web: 

1. Expanda el nodo **Azure** .
2. Expanda el nodo **Web Apps** . 
3. Haga clic en la aplicación web deseada.
4. Cuando aparezca el menú contextual, haga clic en **Abrir en el explorador**.
   
   ![Examinar una aplicación web][17]

## <a name="updating-your-web-app"></a>Actualización de la aplicación web

Actualizar una aplicación web de Azure existente es un proceso rápido y sencillo, y tiene dos opciones para ello:

* Puede actualizar la implementación de una aplicación web de Java existente.
* Puede publicar una aplicación Java adicional en el mismo contenedor de aplicaciones web.

En cualquier caso, el proceso es idéntico y tarda unos pocos segundos:

1. En el Explorador de proyectos de IntelliJ, haga clic con el botón derecho en la aplicación Java que quiere actualizar o agregar a un contenedor de aplicaciones web existente.
2. Cuando aparezca el menú contextual, seleccione **Azure** y, después, haga clic en **Publish as Azure Web App...** (Publicar como aplicación web de Azure).
3. Puesto que ya ha iniciado sesión anteriormente, verá una lista de contenedores de aplicaciones web existentes. Seleccione aquel en el que quiere publicar o volver a publicar la aplicación Java y haga clic en **Aceptar**.

Unos segundos más tarde, la vista **Azure Activity Log** (Registro de actividad de Azure) mostrará la implementación actualizada como **Published** (Publicado) y podrá comprobar la aplicación actualizada en un explorador web.

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a>Inicio, detención o reinicio de una aplicación web existente

Para iniciar o detener un contenedor de aplicaciones web existente (junto con todas las aplicaciones Java implementadas en él), puede utilizar la vista **Azure Explorer** (Explorador de Azure).

Si la vista del **Explorador de Azure** no está abierta, puede abrirla haciendo clic en el menú **View** (Ver) de IntelliJ, luego haga clic en **Tool Windows** (Ventanas de herramientas) y, después, en **Service Explorer** (Explorador de servicios). Si anteriormente no ha iniciado sesión, se le pedirá que lo haga.

Cuando se muestre la vista **Azure Explorer** (Explorador de Azure), siga estos pasos para iniciar o detener la aplicación web: 

1. Expanda el nodo **Azure** .
2. Expanda el nodo **Web Apps** . 
3. Haga clic en la aplicación web deseada.
4. Cuando aparezca el menú contextual, haga clic en **Iniciar**, **Detener** o **Reiniciar**. Tenga en cuenta que las opciones de menú dependen del contexto, por lo que solo podrá detener una aplicación web que se encuentre en ejecución o iniciar una aplicación web que no se esté ejecutando en ese momento.
   
   ![Detener aplicación web][18]

## <a name="next-steps"></a>Pasos siguientes

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

Para obtener más información sobre cómo crear Azure Web Apps, consulte [Introducción a Web Apps].

<!-- URL List -->

[kit de herramientas de Azure para IntelliJ]: azure-toolkit-for-intellij.md
[kit de herramientas de Azure para Eclipse]: ../eclipse/azure-toolkit-for-eclipse.md
[eclipse-hello-world]: ../eclipse/azure-toolkit-for-eclipse-create-hello-world-web-app.md
[Introducción a Web Apps]: /azure/app-service/app-service-web-overview
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/
[Updated Version]: azure-toolkit-for-intellij-create-hello-world-web-app.md
[intelliJ-sign-in-instructions]: azure-toolkit-for-intellij-sign-in-instructions.md

<!-- IMG List -->

[01]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/01-Web-Page.png
[02]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/02-File-New-Project.png
[03a]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/03-New-Project-Dialog.png
[03b]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/03-New-Project-SDK-Dialog.png
[04]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/04-New-Project-Dialog.png
[05a]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/05-Open-Module-Settings.png
[05b]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/05-Project-Structure-Dialog.png
[05c]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/05-Open-Index-Page.png
[06]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/06-Azure-Publish-Context-Menu.png
[07]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/07-Azure-Log-In-Dialog.png
[08]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/08-Manage-Subscriptions.png
[09]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/09-App-Containers.png
[10]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/10-Add-App-Container.png
[11a]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/11-New-App-Container.png
[11b]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/11-New-App-Container-JDK-Tab.png
[12]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/12-New-Resource-Group.png
[13]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/13-New-App-Service-Plan.png
[14]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/14-New-App-Container.png
[15]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/15-Deploy-To-Azure.png
[16]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/16-Progress-Indicator.png
[17]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/17-Browse-Web-App.png
[18]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/18-Stop-Web-App.png
