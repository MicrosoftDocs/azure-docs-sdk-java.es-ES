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
# <a name="create-a-hello-world-web-app-for-azure-app-service-using-eclipse"></a><span data-ttu-id="134b2-104">Creación de una aplicación web Hello World para Azure App Service mediante Eclipse</span><span class="sxs-lookup"><span data-stu-id="134b2-104">Create a Hello World web app for Azure App Service using Eclipse</span></span>

<span data-ttu-id="134b2-105">Con el complemento de código abierto [Azure Toolkit for Eclipse](https://marketplace.eclipse.org/content/azure-toolkit-eclipse), crear e implementar una aplicación básica Hello World en Azure App Service como una aplicación web se puede llevar a cabo en unos minutos.</span><span class="sxs-lookup"><span data-stu-id="134b2-105">Using open sourced [Azure Toolkit for Eclipse](https://marketplace.eclipse.org/content/azure-toolkit-eclipse) plugin, creating and deploying a basic Hello World application to Azure App Service as a web app can be done in a few minutes.</span></span>

> [!NOTE]
>
> <span data-ttu-id="134b2-106">Si prefiere usar IntelliJ IDEA, consulte nuestro [tutorial similar para IntelliJ][intellij-hello-world].</span><span class="sxs-lookup"><span data-stu-id="134b2-106">If you prefer using IntelliJ IDEA, check out our [similar tutorial for IntelliJ][intellij-hello-world].</span></span>
>
>[!INCLUDE [quickstarts-free-trial-note](../includes/quickstarts-free-trial-note.md)]
>
> <span data-ttu-id="134b2-107">No se olvide de realizar una limpieza de los recursos después de completar este tutorial.</span><span class="sxs-lookup"><span data-stu-id="134b2-107">Don't forget to clean up the resources after you complete this tutorial.</span></span> <span data-ttu-id="134b2-108">En ese caso, la ejecución de esta guía no superará la cuota de la cuenta gratuita.</span><span class="sxs-lookup"><span data-stu-id="134b2-108">In that case, running this guide will not exceed your free account quota.</span></span>
>

[!INCLUDE [azure-toolkit-for-intellij-basic-prerequisites](../includes/azure-toolkit-for-eclipse-basic-prerequisites.md)]

## <a name="installation-and-sign-in"></a><span data-ttu-id="134b2-109">Instalación e inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="134b2-109">Installation and sign-in</span></span>

1. <span data-ttu-id="134b2-110">Arrastre el botón siguiente al área de trabajo de Eclipse en ejecución para instalar el complemento Azure Toolkit for Eclipse ([otras opciones de instalación](azure-toolkit-for-eclipse-installation.md)).</span><span class="sxs-lookup"><span data-stu-id="134b2-110">Drag the following button to your running Eclipse workspace to install the Azure Toolkit for Eclipse plugin ([other installation options](azure-toolkit-for-eclipse-installation.md)).</span></span>

    <span data-ttu-id="134b2-111">[![Arrastrar al área de trabajo de Eclipse* en ejecución. *Requiere el cliente de Marketplace de Eclipse](https://marketplace.eclipse.org/sites/all/themes/solstice/public/images/marketplace/btn-install.png)](http://marketplace.eclipse.org/marketplace-client-intro?mpc_install=1919278 "Arrastrar al área de trabajo de Eclipse* en ejecución. *Requiere el cliente de Marketplace de Eclipse")</span><span class="sxs-lookup"><span data-stu-id="134b2-111">[![Drag to your running Eclipse* workspace. *Requires Eclipse Marketplace Client](https://marketplace.eclipse.org/sites/all/themes/solstice/public/images/marketplace/btn-install.png)](http://marketplace.eclipse.org/marketplace-client-intro?mpc_install=1919278 "Drag to your running Eclipse* workspace. *Requires Eclipse Marketplace Client")</span></span>

1. <span data-ttu-id="134b2-112">Para iniciar sesión en la cuenta de Azure, haga clic en **Herramientas**, a continuación, haga clic en **Azure** y, a continuación, haga clic en **Iniciar sesión**.</span><span class="sxs-lookup"><span data-stu-id="134b2-112">To sign in to your Azure account, click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>
   <span data-ttu-id="134b2-113">![Menú de Eclipse para iniciar sesión en Azure][I01]</span><span class="sxs-lookup"><span data-stu-id="134b2-113">![Eclipse Menu for Azure Sign In][I01]</span></span>

1. <span data-ttu-id="134b2-114">En la ventana **Inicio de sesión de Azure**, seleccione **Inicio de sesión de dispositivo** y, a continuación, haga clic en **Iniciar sesión** ([otras opciones de inicio de sesión](azure-toolkit-for-eclipse-sign-in-instructions.md)).</span><span class="sxs-lookup"><span data-stu-id="134b2-114">In the **Azure Sign In** window, select **Device Login**, and then click **Sign in** ([other sign-in options](azure-toolkit-for-eclipse-sign-in-instructions.md)).</span></span>

   ![Ventana Inicio de sesión de Azure con el inicio de sesión de dispositivo seleccionado][I02]

1. <span data-ttu-id="134b2-116">Haga clic en **Copiar y abrir** en el cuadro de diálogo **Inicio de sesión de dispositivo de Azure**.</span><span class="sxs-lookup"><span data-stu-id="134b2-116">Click **Copy&Open** in **Azure Device Login** dialog .</span></span>

   ![El cuadro de diálogo Inicio de sesión en Microsoft Azure][I03]

1. <span data-ttu-id="134b2-118">En el explorador, pegue el código del dispositivo (que se ha copiado al hacer clic en **Copiar y abrir** en el último paso) y, a continuación, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="134b2-118">In the browser, paste your device code (which has been copied when you clicked **Copy&Open** in last step) and then click **Next**.</span></span>

   ![Explorador de inicio de sesión de dispositivo][I04]

1. <span data-ttu-id="134b2-120">Finalmente, en el cuadro de diálogo **Seleccionar suscripciones**, elija las suscripciones que desea usar y, luego, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="134b2-120">Finally, in the **Select Subscriptions** dialog box, select the subscriptions that you want to use, then click **OK**.</span></span>

   ![Cuadro de diálogo Seleccionar suscripciones][I05]

## <a name="creating-web-app-project"></a><span data-ttu-id="134b2-122">Creación del proyecto de aplicación web</span><span class="sxs-lookup"><span data-stu-id="134b2-122">Creating web app project</span></span>

1. <span data-ttu-id="134b2-123">Haga clic en **File** (Archivo), haga clic en **New** (Nuevo) y luego haga clic en **Dynamic Web Project** (Proyecto web dinámico).</span><span class="sxs-lookup"><span data-stu-id="134b2-123">Click **File**, click **New**, and then click **Dynamic Web Project**.</span></span> <span data-ttu-id="134b2-124">[Si no ve que **Dynamic Web Project** aparezca como disponible después de hacer clic en **File** (Archivo) y **New** (Nuevo), haga clic en **File** (Archivo), **New** (Nuevo), **Project...** (Proyecto...), expanda **Web**, haga clic en **Dynamic Web Project** (Proyecto web dinámica) y, finalmente, haga clic en **Next** (Siguiente).]</span><span class="sxs-lookup"><span data-stu-id="134b2-124">(If you don't see **Dynamic Web Project** listed as an available project after clicking **File** and **New**, then do the following: click **File**, click **New**, click **Project...**, expand **Web**, click **Dynamic Web Project**, and click **Next**.)</span></span>

   ![Creación de un nuevo proyecto web dinámico][file-new-dynamic-web-project]

2. <span data-ttu-id="134b2-126">Para los fines de este tutorial, asigne el nombre **MyWebApp**al proyecto.</span><span class="sxs-lookup"><span data-stu-id="134b2-126">For purposes of this tutorial, name the project **MyWebApp**.</span></span> <span data-ttu-id="134b2-127">La pantalla se parecerá a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="134b2-127">Your screen will appear similar to the following:</span></span>
   
   ![Propiedades de New Dynamic Web Project (Nuevo proyecto web dinámico)][dynamic-web-project-properties]

3. <span data-ttu-id="134b2-129">Haga clic en **Finalizar**</span><span class="sxs-lookup"><span data-stu-id="134b2-129">Click **Finish**.</span></span>

4. <span data-ttu-id="134b2-130">En la vista del explorador de proyectos de Eclipse, expanda **MyWebApp**.</span><span class="sxs-lookup"><span data-stu-id="134b2-130">Within Eclipse's Project Explorer view, expand **MyWebApp**.</span></span> <span data-ttu-id="134b2-131">Haga clic con el botón derecho en **WebContent**, haga clic en **New** (Nuevo) y, después, en **JSP File** (Archivo JSP).</span><span class="sxs-lookup"><span data-stu-id="134b2-131">Right-click **WebContent**, click **New**, and then click **JSP File**.</span></span>

   ![Crear un archivo JSP nuevo][create-new-jsp-file]

5. <span data-ttu-id="134b2-133">En el cuadro de diálogo **New JSP File** (Nuevo archivo JSP), asigne un nombre del archivo **index.jsp**, conserve la carpeta principal como **MyWebApp/WebContent** y haga clic en **Next** (Siguiente).</span><span class="sxs-lookup"><span data-stu-id="134b2-133">In the **New JSP File** dialog box, name the file **index.jsp**, keep the parent folder as **MyWebApp/WebContent**, and then click **Next**.</span></span>

   ![Cuadro de diálogo Nuevo archivo JSP][new-jsp-file-dialog]

6. <span data-ttu-id="134b2-135">Para este tutorial, en el cuadro de diálogo **Select JSP Template** (Seleccionar plantilla JSP), seleccione **New JSP File (html)** [Nuevo archivo JSP (html)] y haga clic en **Finish** (Finalizar).</span><span class="sxs-lookup"><span data-stu-id="134b2-135">In the **Select JSP Template** dialog box, for purposes of this tutorial select **New JSP File (html)**, and then click **Finish**.</span></span>

   ![Seleccionar la plantilla JSP][select-jsp-template]

7. <span data-ttu-id="134b2-137">Cuando el archivo index.jsp se abra en Eclipse, agregue texto para que se muestre dinámicamente **Hello World!**</span><span class="sxs-lookup"><span data-stu-id="134b2-137">When your index.jsp file opens in Eclipse, add in text to dynamically display **Hello World!**</span></span> <span data-ttu-id="134b2-138">dentro del elemento `<body>` existente.</span><span class="sxs-lookup"><span data-stu-id="134b2-138">within the existing `<body>` element.</span></span> <span data-ttu-id="134b2-139">El contenido de `<body>` actualizado debe parecerse al siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="134b2-139">Your updated `<body>` content should resemble the following example:</span></span>
   
   ```jsp
   <body><b><% out.println("Hello World!"); %></b></body>
   ```

8. <span data-ttu-id="134b2-140">Guarde el archivo index.jsp.</span><span class="sxs-lookup"><span data-stu-id="134b2-140">Save index.jsp.</span></span>

## <a name="deploying-web-app-to-azure"></a><span data-ttu-id="134b2-141">Implementación de la aplicación web en Azure</span><span class="sxs-lookup"><span data-stu-id="134b2-141">Deploying web app to Azure</span></span>

1. <span data-ttu-id="134b2-142">En la vista del explorador de proyectos de Eclipse, haga clic con el botón derecho en el proyecto, elija **Azure** y **Publish as Azure Web App** (Publicar como aplicación web de Azure).</span><span class="sxs-lookup"><span data-stu-id="134b2-142">Within Eclipse's Project Explorer view, right-click your project, choose **Azure**, and then choose **Publish as Azure Web App**.</span></span>
   
   ![Publish as Azure Web App][publish-as-azure-web-app]

1. <span data-ttu-id="134b2-144">En el cuadro de diálogo **Deploy Web App** (Implementar aplicación web) que aparece, puede elegir una de las siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="134b2-144">When the **Deploy Web App** dialog box appears, you can choose one of the following options:</span></span>

   * <span data-ttu-id="134b2-145">Seleccione una aplicación web si ya existe una.</span><span class="sxs-lookup"><span data-stu-id="134b2-145">Select an existing web app if one exists.</span></span>

      ![Selección de la instancia de App Service][select-app-service]

   * <span data-ttu-id="134b2-147">Haga clic en **Create New Web App** (Crear aplicación web nueva).</span><span class="sxs-lookup"><span data-stu-id="134b2-147">Click **Create New Web App**.</span></span>

      ![Creación de un elemento App Service][create-app-service]

      <span data-ttu-id="134b2-149">Especifique la información necesaria para la aplicación web en el cuadro de diálogo **Create App Service** (Crear servicio de aplicaciones) y haga clic en **Crear** (Ejecutar).</span><span class="sxs-lookup"><span data-stu-id="134b2-149">Specify the requisite information for your web app in the **Create App Service** dialog box, and then click **Create**.</span></span>

      <span data-ttu-id="134b2-150">Aquí puede configurar el entorno de tiempo de ejecución, la configuración de la aplicación, el plan de servicio y el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="134b2-150">Here you can configure the runtime environment, app settings, service plan and resource group.</span></span>

      ![Cuadro de diálogo Crear servicio de aplicaciones][create-app-service-dialog]

1. <span data-ttu-id="134b2-152">Seleccione la aplicación web y haga clic en **Deploy** (Implementar).</span><span class="sxs-lookup"><span data-stu-id="134b2-152">Select your web app and then click **Deploy**.</span></span>

   ![Implementar instancia de App Service][deploy-app-service]

1. <span data-ttu-id="134b2-154">El kit de herramientas mostrará el estado **Publicado** en la pestaña **Registro de actividad de Azure** cuando se haya implementado correctamente la aplicación web, con un hipervínculo a la dirección URL de la aplicación web implementada.</span><span class="sxs-lookup"><span data-stu-id="134b2-154">The toolkit will display a **Published** status under the **Azure Activity Log** tab when it has successfully deployed your web app, which is a hyperlink for the URL of your deployed web app.</span></span>

   ![Estado de publicación][publish-status]

1. <span data-ttu-id="134b2-156">Puede buscar la aplicación web mediante el vínculo que se proporciona en el mensaje de estado.</span><span class="sxs-lookup"><span data-stu-id="134b2-156">You can browse to your web app using the link provided in the status message.</span></span>

   ![Búsqueda de la aplicación web][browse-web-app]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="cleaning-up-resources"></a><span data-ttu-id="134b2-158">Limpieza de recursos</span><span class="sxs-lookup"><span data-stu-id="134b2-158">Cleaning up resources</span></span>

1. <span data-ttu-id="134b2-159">Después de publicar la aplicación web en Azure, puede administrarla; para ello, haga clic con el botón derecho en el explorador de Azure y seleccione una de las opciones del menú contextual.</span><span class="sxs-lookup"><span data-stu-id="134b2-159">After you have published your web app to Azure, you can manage it by right-clicking in Azure Explorer and selecting one of the options in the context menu.</span></span> <span data-ttu-id="134b2-160">Por ejemplo, puede **Eliminar** la aplicación web aquí para limpiar los recursos de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="134b2-160">For example, you can **Delete** your web app here to clean up the resource for this tutorial.</span></span>

   ![Administrar la instancia de App Service][manage-app-service]

## <a name="next-steps"></a><span data-ttu-id="134b2-162">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="134b2-162">Next steps</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<span data-ttu-id="134b2-163">Para obtener más información sobre cómo crear Azure Web Apps, consulte [Introducción a Web Apps].</span><span class="sxs-lookup"><span data-stu-id="134b2-163">For additional information about creating Azure Web Apps, see the [Web Apps Overview].</span></span>

<!-- URL List -->

[Azure Toolkit for Eclipse]: azure-toolkit-for-eclipse.md
[Azure Toolkit for IntelliJ]: ../intellij/azure-toolkit-for-intellij.md
[intellij-hello-world]: ../intellij/azure-toolkit-for-intellij-create-hello-world-web-app.md
[Introducción a Web Apps]: /azure/app-service/app-service-web-overview
[Web Apps Overview]: /azure/app-service/app-service-web-overview
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
