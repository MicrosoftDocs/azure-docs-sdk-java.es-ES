---
title: "Creación de una aplicación web básica de Azure en IntelliJ"
description: "En este tutorial se muestra cómo utilizar el Kit de herramientas de Azure para IntelliJ para crear una aplicación web Hello World para Azure."
services: app-service
documentationcenter: java
author: selvasingh
manager: routlaw
editor: 
ms.assetid: 75ce7b36-e3ae-491d-8305-4b42ce37db4e
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: multiple
ms.devlang: java
ms.topic: article
ms.date: 10/19/2017
ms.author: robmcm;asirveda
ms.openlocfilehash: 323ce74f2d4dad10460a0c2bc0fb59f2bbdbbf3c
ms.sourcegitcommit: 7f8538e41c833deb69c300ad3431a431136a1f3e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/24/2017
---
# <a name="create-a-basic-azure-web-app-in-intellij"></a>Creación de una aplicación web básica de Azure en IntelliJ

En este tutorial se muestra cómo crear e implementar una aplicación básica Hola mundo en Azure como una aplicación web mediante el [Kit de herramientas de Azure para IntelliJ].

> [!NOTE]
> 
> El Kit de herramientas de Azure para IntelliJ se actualizó en agosto de 2017, con un flujo de trabajo diferente. Con esto en mente, este artículo contiene dos secciones diferentes:
>
> * En la primera sección se muestra la creación de una aplicación web de Hola mundo con la versión de agosto 2017 (o posterior) del Kit de herramientas de Azure para IntelliJ.
>
> * En la segunda sección de este artículo se muestra cómo crear una aplicación web de Hola mundo con la versión de abril de 2017 (o anterior) del kit de herramientas.
> 

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="create-a-hello-world-web-app-by-using-the-version-307-or-later-toolkit"></a>Creación de una aplicación web de Hola mundo con la versión 3.0.7 o una posterior del kit de herramientas

### <a name="create-a-new-web-app-project"></a>Creación de un proyecto de aplicación web nuevo

1. Inicie IntelliJ e inicie sesión en su cuenta de Azure siguiendo los pasos del artículo [Instrucciones de inicio de sesión del kit de herramientas de Azure para IntelliJ].

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

### <a name="deploy-your-web-app-to-azure"></a>Implementación de una aplicación web en Azure

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

<hr />

## <a name="create-a-hello-world-web-app-by-using-the-version-306-or-earlier-toolkit"></a>Creación de una aplicación web Hola mundo con la versión 3.0.6 o un kit de herramientas anterior

### <a name="create-a-new-web-app-project"></a>Creación de un proyecto de aplicación web nuevo

1. Inicie IntelliJ y haga clic en **File** (Archivo), **New** (Nuevo) y, finalmente, en **Project** (Proyecto).
   
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

### <a name="deploy-your-web-app-to-azure"></a>Implementación de una aplicación web en Azure
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
      * Haga clic en **Aceptar**.

   g. En el menú desplegable **Plan del servicio de aplicaciones** se muestran los planes del servicio de aplicaciones que están asociados con el grupo de recursos seleccionado. (Un plan de App Service especifica información como la ubicación de la aplicación web, el plan de tarifa y el tamaño de la instancia de proceso. Un único plan de App Service se puede usar para varias aplicaciones web, motivo por el cual se mantiene independiente de una implementación específica de aplicaciones web.
      
      Puede seleccionar un plan de plan de App Service existente (si tiene alguno) y pasar al paso h a continuación o usar los siguientes pasos para crear un nuevo plan:
      
      * Seleccione **&lt;&lt; Crear nuevo plan de App Service&gt;&gt;** en el menú desplegable **Plan de App Service**.
      * Se muestra el cuadro de diálogo **Nuevo plan del servicio de aplicaciones** :
        
         ![Nuevo plan de App Service][13]

      * En el cuadro de texto **Nombre**, especifique un nombre para el nuevo plan de App Service.
      * En el menú desplegable **Ubicación**, seleccione la ubicación adecuada del centro de datos de Azure para el plan.
      * En el menú desplegable **Plan de tarifa**, seleccione la tarifa adecuada para el plan. Con fines de prueba, puede elegir **Gratis**.
      * En el menú desplegable **Tamaño de instancia**, seleccione el tamaño de instancia adecuado para el plan. Con fines de prueba, puede elegir **Pequeño**.
      * Haga clic en **Aceptar**.

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

### <a name="browsing-to-your-web-app-on-azure"></a>Desplazamiento hasta su aplicación web en Azure
Para ir a su aplicación web en Azure, puede usar la vista **Azure Explorer**.

Si la vista del **Explorador de Azure** no está abierta, puede abrirla haciendo clic en el menú **View** (Ver) de IntelliJ, luego haga clic en **Tool Windows** (Ventanas de herramientas) y, después, en **Service Explorer** (Explorador de servicios). Si anteriormente no ha iniciado sesión, se le pedirá que lo haga.

Cuando se muestre la vista **Azure Explorer** (Explorador de Azure), siga estos pasos para buscar la aplicación web: 

1. Expanda el nodo **Azure** .
2. Expanda el nodo **Aplicaciones web** . 
3. Haga clic en la aplicación web deseada.
4. Cuando aparezca el menú contextual, haga clic en **Abrir en el explorador**.
   
   ![Examinar una aplicación web][17]

### <a name="updating-your-web-app"></a>Actualización de la aplicación web
Actualizar una aplicación web de Azure existente es un proceso rápido y sencillo, y tiene dos opciones para ello:

* Puede actualizar la implementación de una aplicación web de Java existente.
* Puede publicar una aplicación Java adicional en el mismo contenedor de aplicaciones web.

En cualquier caso, el proceso es idéntico y tarda unos pocos segundos:

1. En el Explorador de proyectos de IntelliJ, haga clic con el botón derecho en la aplicación Java que quiere actualizar o agregar a un contenedor de aplicaciones web existente.
2. Cuando aparezca el menú contextual, seleccione **Azure** y, después, haga clic en **Publish as Azure Web App...** (Publicar como aplicación web de Azure).
3. Puesto que ya ha iniciado sesión anteriormente, verá una lista de contenedores de aplicaciones web existentes. Seleccione aquel en el que quiere publicar o volver a publicar la aplicación Java y haga clic en **Aceptar**.

Unos segundos más tarde, la vista **Azure Activity Log** (Registro de actividad de Azure) mostrará la implementación actualizada como **Published** (Publicado) y podrá comprobar la aplicación actualizada en un explorador web.

### <a name="starting-stopping-or-restarting-an-existing-web-app"></a>Inicio, detención o reinicio de una aplicación web existente
Para iniciar o detener un contenedor de aplicaciones web existente (junto con todas las aplicaciones Java implementadas en él), puede utilizar la vista **Azure Explorer** (Explorador de Azure).

Si la vista del **Explorador de Azure** no está abierta, puede abrirla haciendo clic en el menú **View** (Ver) de IntelliJ, luego haga clic en **Tool Windows** (Ventanas de herramientas) y, después, en **Service Explorer** (Explorador de servicios). Si anteriormente no ha iniciado sesión, se le pedirá que lo haga.

Cuando se muestre la vista **Azure Explorer** (Explorador de Azure), siga estos pasos para iniciar o detener la aplicación web: 

1. Expanda el nodo **Azure** .
2. Expanda el nodo **Aplicaciones web** . 
3. Haga clic en la aplicación web deseada.
4. Cuando aparezca el menú contextual, haga clic en **Iniciar**, **Detener** o **Reiniciar**. Tenga en cuenta que las opciones de menú dependen del contexto, por lo que solo podrá detener una aplicación web que se encuentre en ejecución o iniciar una aplicación web que no se esté ejecutando en ese momento.
   
   ![Detener aplicación web][18]

## <a name="next-steps"></a>Pasos siguientes

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

Para obtener más información sobre cómo crear aplicaciones web de Azure, consulte [Introducción a Aplicaciones web].

<!-- URL List -->

[Kit de herramientas de Azure para IntelliJ]: azure-toolkit-for-intellij.md
[Introducción a Aplicaciones web]: /azure/app-service/app-service-web-overview
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/

<!-- IMG List -->

[01]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/01-Web-Page.png
[02]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/02-File-New-Project.png
[03a]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/03-New-Project-Dialog.png
[03b]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/03-New-Project-SDK-Dialog.png
[04]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/04-New-Project-Dialog.png
[05a]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/05-Open-Module-Settings.png
[05b]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/05-Project-Structure-Dialog.png
[05c]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/05-Open-Index-Page.png
[06]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/06-Azure-Publish-Context-Menu.png
[07]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/07-Azure-Log-In-Dialog.png
[08]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/08-Manage-Subscriptions.png
[09]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/09-App-Containers.png
[10]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/10-Add-App-Container.png
[11a]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/11-New-App-Container.png
[11b]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/11-New-App-Container-JDK-Tab.png
[12]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/12-New-Resource-Group.png
[13]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/13-New-App-Service-Plan.png
[14]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/14-New-App-Container.png
[15]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/15-Deploy-To-Azure.png
[16]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/16-Progress-Indicator.png
[17]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/17-Browse-Web-App.png
[18]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/18-Stop-Web-App.png

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
