---
title: "Creación de una aplicación web Hello World para Azure mediante IntelliJ"
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
ms.date: 11/15/2017
ms.author: robmcm;asirveda
ms.openlocfilehash: 900e64667bcc2eed79fe80954c118d54a9ef957f
ms.sourcegitcommit: 613c1ffd2e0279fc7a96fca98aa1809563f52ee1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="create-a-hello-world-web-app-for-azure-using-intellij"></a><span data-ttu-id="ab577-103">Creación de una aplicación web Hello World para Azure mediante IntelliJ</span><span class="sxs-lookup"><span data-stu-id="ab577-103">Create a Hello World web app for Azure using IntelliJ</span></span>

<span data-ttu-id="ab577-104">En este tutorial se muestra cómo crear e implementar una aplicación básica Hola mundo en Azure como una aplicación web mediante el [Kit de herramientas de Azure para IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="ab577-104">This tutorial shows how to create and deploy a basic Hello World application to Azure as a web app by using the [Azure Toolkit for IntelliJ].</span></span>

> [!NOTE]
>
> <span data-ttu-id="ab577-105">Para ver la versión de este artículo que usa el [Kit de herramientas de Azure para Eclipse], consulte [Creación de una aplicación web Hello World para Azure mediante Eclipse][eclipse-hello-world].</span><span class="sxs-lookup"><span data-stu-id="ab577-105">For a version of this article that uses the [Azure Toolkit for Eclipse], see [Create a Hello World web app for Azure using Eclipse][eclipse-hello-world].</span></span>
>

> [!IMPORTANT]
> 
> <span data-ttu-id="ab577-106">El Kit de herramientas de Azure para IntelliJ se actualizó en agosto de 2017, con un flujo de trabajo diferente.</span><span class="sxs-lookup"><span data-stu-id="ab577-106">The Azure Toolkit for IntelliJ was updated in August 2017 with a different workflow.</span></span> <span data-ttu-id="ab577-107">En este artículo se muestra la creación de una aplicación web Hello World con la versión 3.0.7 (o posterior) del Kit de herramientas de Azure para IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="ab577-107">This article illustrates creating a Hello World web app by using version 3.0.7 (or later) of the Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="ab577-108">Si está usando la versión 3.0.6 (o anterior) del kit de herramientas, debe seguir los pasos descritos en [Creación de una aplicación web Hello World de Azure en IntelliJ con el Kit de herramientas heredado][Legacy Version].</span><span class="sxs-lookup"><span data-stu-id="ab577-108">If you are using the version 3.0.6 (or earlier) of the toolkit, you will need to follow the steps in [Create a Hello World web app for Azure in IntelliJ using the legacy toolkit][Legacy Version].</span></span>
> 

<span data-ttu-id="ab577-109">Cuando haya completado este tutorial, la aplicación se parecerá a la que se muestra en la siguiente ilustración al verla en un explorador web:</span><span class="sxs-lookup"><span data-stu-id="ab577-109">When you have completed this tutorial, your application will look similar to the following illustration when you view it in a web browser:</span></span>

![Versión preliminar de la aplicación Hello World][browse-web-app]

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="create-a-new-web-app-project"></a><span data-ttu-id="ab577-111">Creación de un proyecto de aplicación web nuevo</span><span class="sxs-lookup"><span data-stu-id="ab577-111">Create a new web app project</span></span>

1. <span data-ttu-id="ab577-112">Inicie IntelliJ e inicie sesión en su cuenta de Azure siguiendo las instrucciones del artículo [Instrucciones de inicio de sesión del kit de herramientas de Azure para IntelliJ][intelliJ-sign-in-instructions].</span><span class="sxs-lookup"><span data-stu-id="ab577-112">Start IntelliJ, and sign into your Azure account by using the instructions in the [Azure Sign In Instructions for the Azure Toolkit for IntelliJ][intelliJ-sign-in-instructions] article.</span></span>

1. <span data-ttu-id="ab577-113">Haga clic en el menú **File** (Archivo), luego en **New** (Nuevo) y, finalmente, en **Project** (Proyecto).</span><span class="sxs-lookup"><span data-stu-id="ab577-113">Click the **File** menu, then click **New**, and then click **Project**.</span></span>
   
   ![Creación de un proyecto][file-new-project]

1. <span data-ttu-id="ab577-115">En el cuadro de diálogo **New Project** (Nuevo proyecto), seleccione **Maven**, **maven-archetype-webapp** y haga clic en **Next** (Siguiente).</span><span class="sxs-lookup"><span data-stu-id="ab577-115">In the **New Project** dialog box, select **Maven**, then **maven-archetype-webapp**, and then click **Next**.</span></span>
   
   ![Elección de una aplicación web de arquetipo Maven][maven-archetype-webapp]
   
1. <span data-ttu-id="ab577-117">Especifique **GroupId** y **ArtifactId** para la aplicación web y haga clic en **Next** (Siguiente).</span><span class="sxs-lookup"><span data-stu-id="ab577-117">Specify the **GroupId** and **ArtifactId** for your web app, and then click **Next**.</span></span>
   
   ![Especificación de GroupId y ArtifactId][groupid-and-artifactid]

1. <span data-ttu-id="ab577-119">Personalice la configuración de Maven o acepte los valores predeterminados y haga clic en **Next** (Siguiente).</span><span class="sxs-lookup"><span data-stu-id="ab577-119">Customize any Maven settings or accept the defaults, and then click **Next**.</span></span>
   
   ![Especificación de la configuración de Maven][maven-options]

1. <span data-ttu-id="ab577-121">Especifique el nombre y la ubicación del proyecto, y haga clic en **Finish**(Finalizar).</span><span class="sxs-lookup"><span data-stu-id="ab577-121">Specify your project name and location, and then click **Finish**.</span></span>
   
   ![Especificación del nombre del proyecto][project-name]

1. <span data-ttu-id="ab577-123">En la vista del explorador de proyectos de IntelliJ, expanda **src**, después, **main**, luego, **webapp** y, a continuación, haga doble clic en **index.jsp**.</span><span class="sxs-lookup"><span data-stu-id="ab577-123">Within IntelliJ's Project Explorer view, expand **src**, then **main**, then **webapp**, and then double-click **index.jsp**.</span></span>
   
   ![Apertura de la página de índice][open-index-page]

1. <span data-ttu-id="ab577-125">Cuando el archivo index.jsp se abra en IntelliJ, agregue texto para que se muestre dinámicamente **Hello World!**</span><span class="sxs-lookup"><span data-stu-id="ab577-125">When your index.jsp file opens in IntelliJ, add in text to dynamically display **Hello World!**</span></span> <span data-ttu-id="ab577-126">dentro del elemento `<body>` existente.</span><span class="sxs-lookup"><span data-stu-id="ab577-126">within the existing `<body>` element.</span></span> <span data-ttu-id="ab577-127">El contenido de `<body>` actualizado debe parecerse al siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="ab577-127">Your updated `<body>` content should resemble the following example:</span></span>
   
   ```java
   <body><b><% out.println("Hello World!"); %></b></body>
   ``` 

   ![Edición de la página de índice][edit-index-page]

1. <span data-ttu-id="ab577-129">Guarde el archivo index.jsp.</span><span class="sxs-lookup"><span data-stu-id="ab577-129">Save index.jsp.</span></span>

## <a name="deploy-your-web-app-to-azure"></a><span data-ttu-id="ab577-130">Implementación de una aplicación web en Azure</span><span class="sxs-lookup"><span data-stu-id="ab577-130">Deploy your web app to Azure</span></span>

1. <span data-ttu-id="ab577-131">En la vista del explorador de proyectos de IntelliJ, haga clic con el botón derecho en el proyecto, elija **Azure** y **Run on Web App** (Ejecutar en aplicación web).</span><span class="sxs-lookup"><span data-stu-id="ab577-131">Within IntelliJ's Project Explorer view, right-click your project, choose **Azure**, and then choose **Run on Web App**.</span></span>
   
   ![Menú Run on Web App (Ejecutar en aplicación web)][run-on-web-app-menu]

1. <span data-ttu-id="ab577-133">En el cuadro de diálogo Run on Web App (Ejecutar en aplicación web), puede elegir una de las siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="ab577-133">In the Run on Web App dialog box, you can choose one of the following options:</span></span>

   * <span data-ttu-id="ab577-134">Elija una aplicación web existente (si existe) y haga clic en **Run** (Ejecutar).</span><span class="sxs-lookup"><span data-stu-id="ab577-134">Choose an existing web app (if one exists), and then click **Run**.</span></span>

      ![Cuadro de diálogo Run on Web App (Ejecutar en aplicación web)][run-on-web-app-dialog]

   * <span data-ttu-id="ab577-136">Haga clic en **Create New Web App** (Crear aplicación web nueva).</span><span class="sxs-lookup"><span data-stu-id="ab577-136">Click **Create New Web App**.</span></span> <span data-ttu-id="ab577-137">Si decide crear una aplicación web, especifique la información necesaria para ella y haga clic en **Run** (Ejecutar).</span><span class="sxs-lookup"><span data-stu-id="ab577-137">If you choose to create a new web app, specify the requisite information for your web app, and then click **Run**.</span></span>

      ![Creación de una aplicación web][create-new-web-app-dialog]

1. <span data-ttu-id="ab577-139">El kit de herramientas mostrará un mensaje de estado cuando se haya implementado correctamente la aplicación web y la dirección URL de esta.</span><span class="sxs-lookup"><span data-stu-id="ab577-139">The toolkit will display a status message when it has successfully deployed your web app, which will also display the URL of your deployed web app.</span></span>

   ![Implementación correcta][successfully-deployed]

1. <span data-ttu-id="ab577-141">Puede buscar la aplicación web mediante el vínculo que se proporciona en el mensaje de estado.</span><span class="sxs-lookup"><span data-stu-id="ab577-141">You can browse to your web app using the link provided in the status message.</span></span>

   ![Búsqueda de la aplicación web][browse-web-app]

1. <span data-ttu-id="ab577-143">Después de publicar la aplicación web, la configuración se guardará como valor predeterminado y podrá ejecutar la aplicación en Azure al hacer clic en el icono de flecha verde de la barra de herramientas.</span><span class="sxs-lookup"><span data-stu-id="ab577-143">After you have published your web app, your settings will be saved as the default, and you can run your application on Azure by clicking the green arrow icon on the toolbar.</span></span> <span data-ttu-id="ab577-144">Para modificar esta configuración, haga clic en el menú desplegable de la aplicación web y, luego, en **Edit Configurations** (Editar configuraciones).</span><span class="sxs-lookup"><span data-stu-id="ab577-144">You can modify your settings by clicking the drop-down menu for your web app and click **Edit Configurations**.</span></span>

   ![Menú Editar configuración][edit-configuration-menu]

1. <span data-ttu-id="ab577-146">Cuando aparezca el cuadro de diálogo **Run/Debug Configurations** (Ejecutar/Depurar configuraciones), podrá modificar cualquiera de los valores predeterminados y hacer clic en **OK** (Aceptar).</span><span class="sxs-lookup"><span data-stu-id="ab577-146">When the **Run/Debug Configurations** dialog box is displayed, you can modify any of the default settings, and then click **OK**.</span></span>

   ![Cuadro de diálogo Editar configuración][edit-configuration-dialog]

## <a name="next-steps"></a><span data-ttu-id="ab577-148">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ab577-148">Next steps</span></span>

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

<span data-ttu-id="ab577-149">Para obtener más información sobre cómo crear Azure Web Apps, consulte [Introducción a Web Apps].</span><span class="sxs-lookup"><span data-stu-id="ab577-149">For additional information about creating Azure Web Apps, see the [Web Apps Overview].</span></span>

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
