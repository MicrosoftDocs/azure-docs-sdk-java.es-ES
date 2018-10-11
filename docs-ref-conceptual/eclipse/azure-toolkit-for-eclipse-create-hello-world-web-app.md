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
ms.openlocfilehash: 5e025c90c2619ec72ffddf5815fd49c3ac59c00f
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/09/2018
ms.locfileid: "48893096"
---
# <a name="create-a-hello-world-web-app-for-azure-using-eclipse"></a><span data-ttu-id="a095a-103">Creación de una aplicación web Hello World para Azure mediante Eclipse</span><span class="sxs-lookup"><span data-stu-id="a095a-103">Create a Hello World web app for Azure using Eclipse</span></span>

<span data-ttu-id="a095a-104">En este tutorial se muestra cómo crear e implementar una aplicación básica Hello World en Azure como una aplicación web mediante el [Kit de herramientas de Azure para Eclipse].</span><span class="sxs-lookup"><span data-stu-id="a095a-104">This tutorial shows how to create and deploy a basic Hello World application to Azure as a web app by using the [Azure Toolkit for Eclipse].</span></span>

> [!NOTE]
>
> <span data-ttu-id="a095a-105">Para ver la versión de este artículo que usa el [Kit de herramientas de Azure para IntelliJ], consulte [Creación de una aplicación web Hello World para Azure mediante IntelliJ][intellij-hello-world].</span><span class="sxs-lookup"><span data-stu-id="a095a-105">For a version of this article that uses the [Azure Toolkit for IntelliJ], see [Create a Hello World web app for Azure using IntelliJ][intellij-hello-world].</span></span>
>

> [!IMPORTANT]
> 
> <span data-ttu-id="a095a-106">El Kit de herramientas de Azure para Eclipse se actualizó en agosto de 2017, con un flujo de trabajo diferente.</span><span class="sxs-lookup"><span data-stu-id="a095a-106">The Azure Toolkit for Eclipse was updated in August 2017 with a different workflow.</span></span> <span data-ttu-id="a095a-107">En este artículo se muestra la creación de una aplicación web Hello World con la versión 3.0.7 (o posterior) del Kit de herramientas de Azure para Eclipse.</span><span class="sxs-lookup"><span data-stu-id="a095a-107">This article illustrates creating a Hello World web app by using version 3.0.7 (or later) of the Azure Toolkit for Eclipse.</span></span> <span data-ttu-id="a095a-108">Si está usando la versión 3.0.6 (o versiones anteriores) del kit de herramientas, debe seguir los pasos descritos en [Creación de una aplicación web Hello World de Azure en Eclipse con el Kit de herramientas heredado][Legacy Version].</span><span class="sxs-lookup"><span data-stu-id="a095a-108">If you are using the version 3.0.6 (or earlier) of the toolkit, you will need to follow the steps in [Create a Hello World web app for Azure in Eclipse using the legacy toolkit][Legacy Version].</span></span>
> 

<span data-ttu-id="a095a-109">Cuando haya completado este tutorial, la aplicación se parecerá a la que se muestra en la siguiente ilustración al verla en un explorador web:</span><span class="sxs-lookup"><span data-stu-id="a095a-109">When you have completed this tutorial, your application will look similar to the following illustration when you view it in a web browser:</span></span>

![Versión preliminar de la aplicación Hello World][browse-web-app]

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="create-a-new-web-app-project"></a><span data-ttu-id="a095a-111">Creación de un proyecto de aplicación web nuevo</span><span class="sxs-lookup"><span data-stu-id="a095a-111">Create a new web app project</span></span>

1. <span data-ttu-id="a095a-112">Inicie Eclipse e inicie sesión en su cuenta de Azure siguiendo las instrucciones del artículo [Azure Sign In Instructions for the Azure Toolkit for Eclipse][eclipse-sign-in-instructions].</span><span class="sxs-lookup"><span data-stu-id="a095a-112">Start Eclipse, and sign into your Azure account by using the instructions in the [Azure Sign In Instructions for the Azure Toolkit for Eclipse][eclipse-sign-in-instructions] article.</span></span>

1. <span data-ttu-id="a095a-113">Haga clic en **File** (Archivo), haga clic en **New** (Nuevo) y luego haga clic en **Dynamic Web Project** (Proyecto web dinámico).</span><span class="sxs-lookup"><span data-stu-id="a095a-113">Click **File**, click **New**, and then click **Dynamic Web Project**.</span></span> <span data-ttu-id="a095a-114">[Si no ve que **Dynamic Web Project** aparezca como disponible después de hacer clic en **File** (Archivo) y **New** (Nuevo), haga clic en **File** (Archivo), **New** (Nuevo), **Project...** (Proyecto...), expanda **Web**, haga clic en **Dynamic Web Project** (Proyecto web dinámica) y, finalmente, haga clic en **Next** (Siguiente).]</span><span class="sxs-lookup"><span data-stu-id="a095a-114">(If you don't see **Dynamic Web Project** listed as an available project after clicking **File** and **New**, then do the following: click **File**, click **New**, click **Project...**, expand **Web**, click **Dynamic Web Project**, and click **Next**.)</span></span>

   ![Creación de un nuevo proyecto web dinámico][file-new-dynamic-web-project]

2. <span data-ttu-id="a095a-116">Para los fines de este tutorial, asigne el nombre **MyWebApp**al proyecto.</span><span class="sxs-lookup"><span data-stu-id="a095a-116">For purposes of this tutorial, name the project **MyWebApp**.</span></span> <span data-ttu-id="a095a-117">La pantalla se parecerá a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="a095a-117">Your screen will appear similar to the following:</span></span>
   
   ![Propiedades de New Dynamic Web Project (Nuevo proyecto web dinámico)][dynamic-web-project-properties]

3. <span data-ttu-id="a095a-119">Haga clic en **Finalizar**</span><span class="sxs-lookup"><span data-stu-id="a095a-119">Click **Finish**.</span></span>

4. <span data-ttu-id="a095a-120">En la vista del explorador de proyectos de Eclipse, expanda **MyWebApp**.</span><span class="sxs-lookup"><span data-stu-id="a095a-120">Within Eclipse's Project Explorer view, expand **MyWebApp**.</span></span> <span data-ttu-id="a095a-121">Haga clic con el botón derecho en **WebContent**, haga clic en **New** (Nuevo) y, después, en **JSP File** (Archivo JSP).</span><span class="sxs-lookup"><span data-stu-id="a095a-121">Right-click **WebContent**, click **New**, and then click **JSP File**.</span></span>

   ![Crear un archivo JSP nuevo][create-new-jsp-file]

5. <span data-ttu-id="a095a-123">En el cuadro de diálogo **New JSP File** (Nuevo archivo JSP), asigne un nombre del archivo **index.jsp**, conserve la carpeta principal como **MyWebApp/WebContent** y haga clic en **Next** (Siguiente).</span><span class="sxs-lookup"><span data-stu-id="a095a-123">In the **New JSP File** dialog box, name the file **index.jsp**, keep the parent folder as **MyWebApp/WebContent**, and then click **Next**.</span></span>

   ![Cuadro de diálogo Nuevo archivo JSP][new-jsp-file-dialog]

6. <span data-ttu-id="a095a-125">Para este tutorial, en el cuadro de diálogo **Select JSP Template** (Seleccionar plantilla JSP), seleccione **New JSP File (html)** [Nuevo archivo JSP (html)] y haga clic en **Finish** (Finalizar).</span><span class="sxs-lookup"><span data-stu-id="a095a-125">In the **Select JSP Template** dialog box, for purposes of this tutorial select **New JSP File (html)**, and then click **Finish**.</span></span>

   ![Seleccionar la plantilla JSP][select-jsp-template]

7. <span data-ttu-id="a095a-127">Cuando el archivo index.jsp se abra en Eclipse, agregue texto para que se muestre dinámicamente **Hello World!**</span><span class="sxs-lookup"><span data-stu-id="a095a-127">When your index.jsp file opens in Eclipse, add in text to dynamically display **Hello World!**</span></span> <span data-ttu-id="a095a-128">dentro del elemento `<body>` existente.</span><span class="sxs-lookup"><span data-stu-id="a095a-128">within the existing `<body>` element.</span></span> <span data-ttu-id="a095a-129">El contenido de `<body>` actualizado debe parecerse al siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="a095a-129">Your updated `<body>` content should resemble the following example:</span></span>
   
   ```jsp
   <body><b><% out.println("Hello World!"); %></b></body>
   ```

8. <span data-ttu-id="a095a-130">Guarde el archivo index.jsp.</span><span class="sxs-lookup"><span data-stu-id="a095a-130">Save index.jsp.</span></span>

## <a name="deploy-your-web-app-to-azure"></a><span data-ttu-id="a095a-131">Implementación de una aplicación web en Azure</span><span class="sxs-lookup"><span data-stu-id="a095a-131">Deploy your web app to Azure</span></span>

1. <span data-ttu-id="a095a-132">En la vista del explorador de proyectos de Eclipse, haga clic con el botón derecho en el proyecto, elija **Azure** y **Publish as Azure Web App** (Publicar como aplicación web de Azure).</span><span class="sxs-lookup"><span data-stu-id="a095a-132">Within Eclipse's Project Explorer view, right-click your project, choose **Azure**, and then choose **Publish as Azure Web App**.</span></span>
   
   ![Publish as Azure Web App][publish-as-azure-web-app]

1. <span data-ttu-id="a095a-134">En el cuadro de diálogo **Deploy Web App** (Implementar aplicación web) que aparece, puede elegir una de las siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="a095a-134">When the **Deploy Web App** dialog box appears, you can choose one of the following options:</span></span>

   * <span data-ttu-id="a095a-135">Seleccione una aplicación web si ya existe una.</span><span class="sxs-lookup"><span data-stu-id="a095a-135">Select an existing web app if one exists.</span></span>

      ![Selección de la instancia de App Service][select-app-service]

   * <span data-ttu-id="a095a-137">Haga clic en **Create New Web App** (Crear aplicación web nueva).</span><span class="sxs-lookup"><span data-stu-id="a095a-137">Click **Create New Web App**.</span></span>

      ![Creación de un elemento App Service][create-app-service]

      <span data-ttu-id="a095a-139">Especifique la información necesaria para la aplicación web en el cuadro de diálogo **Create App Service** (Crear servicio de aplicaciones) y haga clic en **Crear** (Ejecutar).</span><span class="sxs-lookup"><span data-stu-id="a095a-139">Specify the requisite information for your web app in the **Create App Service** dialog box, and then click **Create**.</span></span>

      ![Cuadro de diálogo Crear servicio de aplicaciones][create-app-service-dialog]

1. <span data-ttu-id="a095a-141">Seleccione la aplicación web y haga clic en **Deploy** (Implementar).</span><span class="sxs-lookup"><span data-stu-id="a095a-141">Select your web app and then click **Deploy**.</span></span>

   ![Implementar instancia de App Service][deploy-app-service]

1. <span data-ttu-id="a095a-143">El kit de herramientas mostrará el estado **Publicado** en la pestaña **Registro de actividad de Azure** cuando se haya implementado correctamente la aplicación web, con un hipervínculo a la dirección URL de la aplicación web implementada.</span><span class="sxs-lookup"><span data-stu-id="a095a-143">The toolkit will display a **Published** status under the **Azure Activity Log** tab when it has successfully deployed your web app, which is a hyperlink for the URL of your deployed web app.</span></span>

   ![Estado de publicación][publish-status]

1. <span data-ttu-id="a095a-145">Puede buscar la aplicación web mediante el vínculo que se proporciona en el mensaje de estado.</span><span class="sxs-lookup"><span data-stu-id="a095a-145">You can browse to your web app using the link provided in the status message.</span></span>

   ![Búsqueda de la aplicación web][browse-web-app]

1. <span data-ttu-id="a095a-147">Después de publicar su sitio web en Azure, puede administrar la aplicación; para ello, haga clic con el botón derecho y seleccione una de las opciones del menú contextual.</span><span class="sxs-lookup"><span data-stu-id="a095a-147">After you have published your web to Azure, you can manage your app by right-clicking on it and selecting one of the options on the context menu.</span></span> <span data-ttu-id="a095a-148">Estas opciones son: **Start** (Iniciar), **Stop** (Detener) o **Delete** (Eliminar).</span><span class="sxs-lookup"><span data-stu-id="a095a-148">For example, you can **Start**, **Stop**, or **Delete** your web app.</span></span>

   ![Administrar la instancia de App Service][manage-app-service]

## <a name="next-steps"></a><span data-ttu-id="a095a-150">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a095a-150">Next steps</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<span data-ttu-id="a095a-151">Para obtener más información sobre cómo crear Azure Web Apps, consulte [Introducción a Web Apps].</span><span class="sxs-lookup"><span data-stu-id="a095a-151">For additional information about creating Azure Web Apps, see the [Web Apps Overview].</span></span>

<!-- URL List -->

[Kit de herramientas de Azure para Eclipse]: azure-toolkit-for-eclipse.md
[Azure Toolkit for Eclipse]: azure-toolkit-for-eclipse.md
[kit de herramientas de Azure para IntelliJ]: ../intellij/azure-toolkit-for-intellij.md
[Azure Toolkit for IntelliJ]: ../intellij/azure-toolkit-for-intellij.md
[intellij-hello-world]: ../intellij/azure-toolkit-for-intellij-create-hello-world-web-app.md
[Introducción a Web Apps]: /azure/app-service/app-service-web-overview
[Web Apps Overview]: /azure/app-service/app-service-web-overview
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
