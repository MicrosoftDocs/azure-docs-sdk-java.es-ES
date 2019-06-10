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
# <a name="create-a-hello-world-web-app-for-azure-app-service-using-intellij"></a><span data-ttu-id="32f2e-104">Creación de una aplicación web Hello World para Azure App Service mediante IntelliJ</span><span class="sxs-lookup"><span data-stu-id="32f2e-104">Create a Hello World web app for Azure App Service using IntelliJ</span></span>

<span data-ttu-id="32f2e-105">Con el complemento de código abierto [Azure Toolkit for IntelliJ](https://plugins.jetbrains.com/plugin/8053), crear e implementar una aplicación básica Hello World en Azure App Service como una aplicación web se puede llevar a cabo en unos minutos.</span><span class="sxs-lookup"><span data-stu-id="32f2e-105">Using open sourced [Azure Toolkit for IntelliJ](https://plugins.jetbrains.com/plugin/8053) plugin, creating and deploying a basic Hello World application to Azure App Service as a web app can be done in a few minutes.</span></span>

> [!NOTE]
>
> <span data-ttu-id="32f2e-106">Si prefiere usar Eclipse, consulte nuestro [tutorial similar para Eclipse][eclipse-hello-world].</span><span class="sxs-lookup"><span data-stu-id="32f2e-106">If you prefer using Eclipse, check out our [similar tutorial for Eclipse][eclipse-hello-world].</span></span>
>
>[!INCLUDE [quickstarts-free-trial-note](../includes/quickstarts-free-trial-note.md)]
>
> <span data-ttu-id="32f2e-107">No se olvide de realizar una limpieza de los recursos después de completar este tutorial.</span><span class="sxs-lookup"><span data-stu-id="32f2e-107">Don't forget to clean up the resources after you complete this tutorial.</span></span> <span data-ttu-id="32f2e-108">En ese caso, la ejecución de esta guía no superará la cuota de la cuenta gratuita.</span><span class="sxs-lookup"><span data-stu-id="32f2e-108">In that case, running this guide will not exceed your free account quota.</span></span>
>

[!INCLUDE [azure-toolkit-for-intellij-basic-prerequisites](../includes/azure-toolkit-for-intellij-basic-prerequisites.md)]

## <a name="installation-and-sign-in"></a><span data-ttu-id="32f2e-109">Instalación e inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="32f2e-109">Installation and Sign-in</span></span>

1. <span data-ttu-id="32f2e-110">En el cuadro de diálogo de configuración y preferencias del IntelliJ IDEA (Ctrl+Alt+S), seleccione **Complementos**.</span><span class="sxs-lookup"><span data-stu-id="32f2e-110">In IntelliJ IDEA's Settings/Preferences dialog (Ctrl+Alt+S), select **Plugins**.</span></span> <span data-ttu-id="32f2e-111">A continuación, busque **Azure Toolkit for IntelliJ** en **Marketplace** y haga clic en **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="32f2e-111">Then, find the **Azure Toolkit for IntelliJ** in the **Marketplace** and click **Install**.</span></span> <span data-ttu-id="32f2e-112">Una vez instalado, haga clic en **Reiniciar** para activar el complemento.</span><span class="sxs-lookup"><span data-stu-id="32f2e-112">After installed, click **Restart** to activate the plugin.</span></span> 

   ![Complemento Azure Toolkit for IntelliJ en Marketplace][marketplace]

2. <span data-ttu-id="32f2e-114">Para iniciar sesión en la cuenta de Azure, abra **Azure Explorer** y, a continuación, haga clic en el icono **Inicio de sesión de Azure** en la barra de la parte superior (o en el menú IDEA **Herramientas/Azure/Inicio de sesión de Azure**).</span><span class="sxs-lookup"><span data-stu-id="32f2e-114">To sign in to your Azure account, open sidebar **Azure Explorer**, and then click the **Azure Sign In** icon in the bar on top (or from IDEA menu **Tools/Azure/Azure Sign in**).</span></span>

   ![El comando de inicio de sesión en Azure IntelliJ][I01]

3. <span data-ttu-id="32f2e-116">En la ventana **Inicio de sesión de Azure**, seleccione **Inicio de sesión de dispositivo** y, a continuación, haga clic en **Iniciar sesión** ([otras opciones de inicio de sesión](azure-toolkit-for-intellij-sign-in-instructions.md)).</span><span class="sxs-lookup"><span data-stu-id="32f2e-116">In the **Azure Sign In** window, select **Device Login**, and then click **Sign in** ([other sign in options](azure-toolkit-for-intellij-sign-in-instructions.md)).</span></span>

   ![Ventana Inicio de sesión de Azure con el inicio de sesión de dispositivo seleccionado][I02]

4. <span data-ttu-id="32f2e-118">Haga clic en **Copiar y abrir** en el cuadro de diálogo **Inicio de sesión de dispositivo de Azure**.</span><span class="sxs-lookup"><span data-stu-id="32f2e-118">Click **Copy&Open** in **Azure Device Login** dialog .</span></span>

   ![El cuadro de diálogo Inicio de sesión en Microsoft Azure][I03]

5. <span data-ttu-id="32f2e-120">En el explorador, pegue el código del dispositivo (que se ha copiado al hacer clic en **Copiar y abrir** en el último paso) y, a continuación, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="32f2e-120">In the browser, paste your device code (which has been copied when you click **Copy&Open** in last step) and then click **Next**.</span></span>

   ![Explorador de inicio de sesión de dispositivo][I04]

6. <span data-ttu-id="32f2e-122">En el cuadro de diálogo **Seleccionar suscripciones**, elija las suscripciones que desea usar y, luego, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="32f2e-122">In the **Select Subscriptions** dialog box, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![Cuadro de diálogo Seleccionar suscripciones][I05]

## <a name="creating-web-app-project"></a><span data-ttu-id="32f2e-124">Creación del proyecto de aplicación web</span><span class="sxs-lookup"><span data-stu-id="32f2e-124">Creating web app project</span></span>

1. <span data-ttu-id="32f2e-125">En IntelliJ, haga clic en el menú **File** (Archivo), luego en **New** (Nuevo) y, finalmente, en **Project** (Proyecto).</span><span class="sxs-lookup"><span data-stu-id="32f2e-125">In IntelliJ, click the **File** menu, then click **New**, and then click **Project**.</span></span>

   ![Creación de un proyecto][file-new-project]

2. <span data-ttu-id="32f2e-127">En el cuadro de diálogo **New Project** (Nuevo proyecto), seleccione **Maven**, **maven-archetype-webapp** y haga clic en **Next** (Siguiente).</span><span class="sxs-lookup"><span data-stu-id="32f2e-127">In the **New Project** dialog box, select **Maven**, then **maven-archetype-webapp**, and then click **Next**.</span></span>

   ![Elección de una aplicación web de arquetipo Maven][maven-archetype-webapp]

3. <span data-ttu-id="32f2e-129">Especifique **GroupId** y **ArtifactId** para la aplicación web y haga clic en **Next** (Siguiente).</span><span class="sxs-lookup"><span data-stu-id="32f2e-129">Specify the **GroupId** and **ArtifactId** for your web app, and then click **Next**.</span></span>

   ![Especificación de GroupId y ArtifactId][groupid-and-artifactid]

4. <span data-ttu-id="32f2e-131">Personalice la configuración de Maven o acepte los valores predeterminados y haga clic en **Next** (Siguiente).</span><span class="sxs-lookup"><span data-stu-id="32f2e-131">Customize any Maven settings or accept the defaults, and then click **Next**.</span></span>

   ![Especificación de la configuración de Maven][maven-options]

5. <span data-ttu-id="32f2e-133">Especifique el nombre y la ubicación del proyecto, y haga clic en **Finish**(Finalizar).</span><span class="sxs-lookup"><span data-stu-id="32f2e-133">Specify your project name and location, and then click **Finish**.</span></span>

   ![Especificación del nombre del proyecto][project-name]

6. <span data-ttu-id="32f2e-135">En la vista del explorador de proyectos, abra y edite el archivo **src/main/webapp/index.jsp** tal y como se indica a continuación y **guarde los cambios**:</span><span class="sxs-lookup"><span data-stu-id="32f2e-135">Under Project Explorer view, open and edit the file **src/main/webapp/index.jsp** as following and **save the changes**:</span></span>

   ```html
   <html>
    <body>
      <b><% out.println("Hello World!"); %></b>
    </body>
   </html>
   ```

   ![Edición de la página de índice][edit-index-page]

## <a name="deploying-web-app-to-azure"></a><span data-ttu-id="32f2e-137">Implementación de la aplicación web en Azure</span><span class="sxs-lookup"><span data-stu-id="32f2e-137">Deploying web app to Azure</span></span>

1. <span data-ttu-id="32f2e-138">En la vista del explorador de proyectos, haga clic con el botón derecho en el proyecto, expanda **Azure** y, a continuación, haga clic en **Implementar en Azure**.</span><span class="sxs-lookup"><span data-stu-id="32f2e-138">Under Project Explorer view, right-click your project, expand **Azure**, then click **Deploy to Azure**.</span></span>

   ![Menú Implementar en Azure][deploy-to-azure-menu]

1. <span data-ttu-id="32f2e-140">En el cuadro de diálogo Implementar en Azure, puede implementar directamente la aplicación como una aplicación web de Tomcat existente si ya tiene una; en caso contrario, se debe crear primero una nueva.</span><span class="sxs-lookup"><span data-stu-id="32f2e-140">In the Deploy to Azure dialog box, you can directly deploy the application to an existing Tomcat webapp if you already have one, otherwise you should create a new one first.</span></span>
   1. <span data-ttu-id="32f2e-141">Haga clic en el vínculo **No hay aplicación web disponible, haga clic para crear una nueva** para crear una nueva aplicación web, puede elegir **Crear nueva aplicación web** en la lista desplegable de aplicaciones web si hay aplicaciones web existentes en la suscripción.</span><span class="sxs-lookup"><span data-stu-id="32f2e-141">Click the link **No Available webapp, click to create a new one** to crete a new web app, you could choose **Create New WebApp** from WebApp dropdown if there are existing webapps in your subscription.</span></span>

      ![Cuadro de diálogo Implementar en Azure][deploy-to-azure-dialog]

   1. <span data-ttu-id="32f2e-143">En el cuadro de diálogo emergente, elija **TOMCAT 8.5-jre8** como contenedor web, especifique otra información necesaria y, a continuación, haga clic en **Aceptar** para crear la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="32f2e-143">In the pop-up dialog box, chose **TOMCAT 8.5-jre8** as Web Container and specify other required information, then click **OK** to create the webapp.</span></span>

      ![Creación de una aplicación web][create-new-web-app-dialog]

   1. <span data-ttu-id="32f2e-145">Elija la aplicación web en la lista desplegable de aplicaciones web y, a continuación, haga clic en **Ejecutar**. (Puede empezar desde aquí si desea implementar en una aplicación web existente)</span><span class="sxs-lookup"><span data-stu-id="32f2e-145">Choose the web app from WebApp drop down, and then click **Run**.(You could start from here if you want deploy to an existing webapp)</span></span>

      ![Implementación en una aplicación web existente][deploy-to-existing-webapp]

1. <span data-ttu-id="32f2e-147">El kit de herramientas mostrará un mensaje de estado cuando se haya implementado correctamente la aplicación web, con la dirección URL de la aplicación web implementada en caso correcto.</span><span class="sxs-lookup"><span data-stu-id="32f2e-147">The toolkit will display a status message when it has successfully deployed your web app, along with the URL of your deployed web app if succeed.</span></span>

   ![Implementación correcta][successfully-deployed]

1. <span data-ttu-id="32f2e-149">Puede buscar la aplicación web mediante el vínculo que se proporciona en el mensaje de estado.</span><span class="sxs-lookup"><span data-stu-id="32f2e-149">You can browse to your web app using the link provided in the status message.</span></span>

   ![Búsqueda de la aplicación web][browse-web-app]

## <a name="managing-deploy-configurations"></a><span data-ttu-id="32f2e-151">Administración de configuraciones de implementación</span><span class="sxs-lookup"><span data-stu-id="32f2e-151">Managing deploy configurations</span></span>

1. <span data-ttu-id="32f2e-152">Después de publicar la aplicación web, la configuración se guardará como valor predeterminado y podrá ejecutar la implementación al hacer clic en el icono de flecha verde de la barra de herramientas.</span><span class="sxs-lookup"><span data-stu-id="32f2e-152">After you have published your web app, your settings will be saved as the default, and you can run the deployment by clicking the green arrow icon on the toolbar.</span></span> <span data-ttu-id="32f2e-153">Para modificar esta configuración, haga clic en el menú desplegable de la aplicación web y, luego, en **Edit Configurations** (Editar configuraciones).</span><span class="sxs-lookup"><span data-stu-id="32f2e-153">You can modify your settings by clicking the drop-down menu for your web app and click **Edit Configurations**.</span></span>

   ![Menú Editar configuración][edit-configuration-menu]

1. <span data-ttu-id="32f2e-155">Cuando aparezca el cuadro de diálogo **Run/Debug Configurations** (Ejecutar/Depurar configuraciones), podrá modificar cualquiera de los valores predeterminados y hacer clic en **OK** (Aceptar).</span><span class="sxs-lookup"><span data-stu-id="32f2e-155">When the **Run/Debug Configurations** dialog box is displayed, you can modify any of the default settings, and then click **OK**.</span></span>

   ![Cuadro de diálogo Editar configuración][edit-configuration-dialog]

## <a name="cleaning-up-resources"></a><span data-ttu-id="32f2e-157">Limpieza de recursos</span><span class="sxs-lookup"><span data-stu-id="32f2e-157">Cleaning up resources</span></span>

1. <span data-ttu-id="32f2e-158">Eliminación de aplicaciones web en el Explorador de Azure</span><span class="sxs-lookup"><span data-stu-id="32f2e-158">Deleting Web Apps in Azure Explorer</span></span>

     ![Limpieza de recursos][clean-resources]

## <a name="next-steps"></a><span data-ttu-id="32f2e-160">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="32f2e-160">Next steps</span></span>

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

<span data-ttu-id="32f2e-161">Para obtener más información sobre cómo crear Azure Web Apps, consulte [Introducción a Web Apps].</span><span class="sxs-lookup"><span data-stu-id="32f2e-161">For additional information about creating Azure Web Apps, see the [Web Apps Overview].</span></span>

<!-- URL List -->

[Azure Toolkit for IntelliJ]: azure-toolkit-for-intellij.md
[Azure Toolkit for Eclipse]: ../eclipse/azure-toolkit-for-eclipse.md
[eclipse-hello-world]: ../eclipse/azure-toolkit-for-eclipse-create-hello-world-web-app.md
[Introducción a Web Apps]: /azure/app-service/app-service-web-overview
[Web Apps Overview]: /azure/app-service/app-service-web-overview
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
