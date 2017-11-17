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
# <a name="create-a-basic-azure-web-app-in-intellij"></a><span data-ttu-id="98357-103">Creación de una aplicación web básica de Azure en IntelliJ</span><span class="sxs-lookup"><span data-stu-id="98357-103">Create a basic Azure web app in IntelliJ</span></span>

<span data-ttu-id="98357-104">En este tutorial se muestra cómo crear e implementar una aplicación básica Hola mundo en Azure como una aplicación web mediante el [Kit de herramientas de Azure para IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="98357-104">This tutorial shows how to create and deploy a basic Hello World application to Azure as a web app by using the [Azure Toolkit for IntelliJ].</span></span>

> [!NOTE]
> 
> <span data-ttu-id="98357-105">El Kit de herramientas de Azure para IntelliJ se actualizó en agosto de 2017, con un flujo de trabajo diferente.</span><span class="sxs-lookup"><span data-stu-id="98357-105">The Azure Toolkit for IntelliJ was updated in August 2017, with a different workflow.</span></span> <span data-ttu-id="98357-106">Con esto en mente, este artículo contiene dos secciones diferentes:</span><span class="sxs-lookup"><span data-stu-id="98357-106">With that in mind, this article contains two different sections:</span></span>
>
> * <span data-ttu-id="98357-107">En la primera sección se muestra la creación de una aplicación web de Hola mundo con la versión de agosto 2017 (o posterior) del Kit de herramientas de Azure para IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="98357-107">The first section illustrates creating a Hello World web app by using the August 2017 (or later) version of the Azure Toolkit for IntelliJ.</span></span>
>
> * <span data-ttu-id="98357-108">En la segunda sección de este artículo se muestra cómo crear una aplicación web de Hola mundo con la versión de abril de 2017 (o anterior) del kit de herramientas.</span><span class="sxs-lookup"><span data-stu-id="98357-108">The second section of this article demonstrates creating a Hello World web app by using the April 2017 (or earlier) version of the toolkit.</span></span>
> 

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="create-a-hello-world-web-app-by-using-the-version-307-or-later-toolkit"></a><span data-ttu-id="98357-109">Creación de una aplicación web de Hola mundo con la versión 3.0.7 o una posterior del kit de herramientas</span><span class="sxs-lookup"><span data-stu-id="98357-109">Create a Hello World web app by using the version 3.0.7 or later toolkit</span></span>

### <a name="create-a-new-web-app-project"></a><span data-ttu-id="98357-110">Creación de un proyecto de aplicación web nuevo</span><span class="sxs-lookup"><span data-stu-id="98357-110">Create a new web app project</span></span>

1. <span data-ttu-id="98357-111">Inicie IntelliJ e inicie sesión en su cuenta de Azure siguiendo los pasos del artículo [Instrucciones de inicio de sesión del kit de herramientas de Azure para IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="98357-111">Start IntelliJ and sign-in to your Azure account using the steps in the [Sign In Instructions for the Azure Toolkit for IntelliJ] article.</span></span>

1. <span data-ttu-id="98357-112">Haga clic en el menú **File** (Archivo), luego en **New** (Nuevo) y, finalmente, en **Project** (Proyecto).</span><span class="sxs-lookup"><span data-stu-id="98357-112">Click the **File** menu, then click **New**, and then click **Project**.</span></span>
   
   ![Creación de un proyecto][file-new-project]

1. <span data-ttu-id="98357-114">En el cuadro de diálogo **New Project** (Nuevo proyecto), seleccione **Maven**, **maven-archetype-webapp** y haga clic en **Next** (Siguiente).</span><span class="sxs-lookup"><span data-stu-id="98357-114">In the **New Project** dialog box, select **Maven**, then **maven-archetype-webapp**, and then click **Next**.</span></span>
   
   ![Elección de una aplicación web de arquetipo Maven][maven-archetype-webapp]
   
1. <span data-ttu-id="98357-116">Especifique **GroupId** y **ArtifactId** para la aplicación web y haga clic en **Next** (Siguiente).</span><span class="sxs-lookup"><span data-stu-id="98357-116">Specify the **GroupId** and **ArtifactId** for your web app, and then click **Next**.</span></span>
   
   ![Especificación de GroupId y ArtifactId][groupid-and-artifactid]

1. <span data-ttu-id="98357-118">Personalice la configuración de Maven o acepte los valores predeterminados y haga clic en **Next** (Siguiente).</span><span class="sxs-lookup"><span data-stu-id="98357-118">Customize any Maven settings or accept the defaults, and then click **Next**.</span></span>
   
   ![Especificación de la configuración de Maven][maven-options]

1. <span data-ttu-id="98357-120">Especifique el nombre y la ubicación del proyecto, y haga clic en **Finish**(Finalizar).</span><span class="sxs-lookup"><span data-stu-id="98357-120">Specify your project name and location, and then click **Finish**.</span></span>
   
   ![Especificación del nombre del proyecto][project-name]

1. <span data-ttu-id="98357-122">En la vista del explorador de proyectos de IntelliJ, expanda **src**, después, **main**, luego, **webapp** y, a continuación, haga doble clic en **index.jsp**.</span><span class="sxs-lookup"><span data-stu-id="98357-122">Within IntelliJ's Project Explorer view, expand **src**, then **main**, then **webapp**, and then double-click **index.jsp**.</span></span>
   
   ![Apertura de la página de índice][open-index-page]

1. <span data-ttu-id="98357-124">Cuando el archivo index.jsp se abra en IntelliJ, agregue texto para que se muestre dinámicamente **Hello World!**</span><span class="sxs-lookup"><span data-stu-id="98357-124">When your index.jsp file opens in IntelliJ, add in text to dynamically display **Hello World!**</span></span> <span data-ttu-id="98357-125">dentro del elemento `<body>` existente.</span><span class="sxs-lookup"><span data-stu-id="98357-125">within the existing `<body>` element.</span></span> <span data-ttu-id="98357-126">El contenido de `<body>` actualizado debe parecerse al siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="98357-126">Your updated `<body>` content should resemble the following example:</span></span>
   
   ```java
   <body><b><% out.println("Hello World!"); %></b></body>
   ``` 

   ![Edición de la página de índice][edit-index-page]

1. <span data-ttu-id="98357-128">Guarde el archivo index.jsp.</span><span class="sxs-lookup"><span data-stu-id="98357-128">Save index.jsp.</span></span>

### <a name="deploy-your-web-app-to-azure"></a><span data-ttu-id="98357-129">Implementación de una aplicación web en Azure</span><span class="sxs-lookup"><span data-stu-id="98357-129">Deploy your web app to Azure</span></span>

1. <span data-ttu-id="98357-130">En la vista del explorador de proyectos de IntelliJ, haga clic con el botón derecho en el proyecto, elija **Azure** y **Run on Web App** (Ejecutar en aplicación web).</span><span class="sxs-lookup"><span data-stu-id="98357-130">Within IntelliJ's Project Explorer view, right-click your project, choose **Azure**, and then choose **Run on Web App**.</span></span>
   
   ![Menú Run on Web App (Ejecutar en aplicación web)][run-on-web-app-menu]

1. <span data-ttu-id="98357-132">En el cuadro de diálogo Run on Web App (Ejecutar en aplicación web), puede elegir una de las siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="98357-132">In the Run on Web App dialog box, you can choose one of the following options:</span></span>

   * <span data-ttu-id="98357-133">Elija una aplicación web existente (si existe) y haga clic en **Run** (Ejecutar).</span><span class="sxs-lookup"><span data-stu-id="98357-133">Choose an existing web app (if one exists), and then click **Run**.</span></span>

      ![Cuadro de diálogo Run on Web App (Ejecutar en aplicación web)][run-on-web-app-dialog]

   * <span data-ttu-id="98357-135">Haga clic en **Create New Web App** (Crear aplicación web nueva).</span><span class="sxs-lookup"><span data-stu-id="98357-135">Click **Create New Web App**.</span></span> <span data-ttu-id="98357-136">Si decide crear una aplicación web, especifique la información necesaria para ella y haga clic en **Run** (Ejecutar).</span><span class="sxs-lookup"><span data-stu-id="98357-136">If you choose to create a new web app, specify the requisite information for your web app, and then click **Run**.</span></span>

      ![Creación de una aplicación web][create-new-web-app-dialog]

1. <span data-ttu-id="98357-138">El kit de herramientas mostrará un mensaje de estado cuando se haya implementado correctamente la aplicación web y la dirección URL de esta.</span><span class="sxs-lookup"><span data-stu-id="98357-138">The toolkit will display a status message when it has successfully deployed your web app, which will also display the URL of your deployed web app.</span></span>

   ![Implementación correcta][successfully-deployed]

1. <span data-ttu-id="98357-140">Puede buscar la aplicación web mediante el vínculo que se proporciona en el mensaje de estado.</span><span class="sxs-lookup"><span data-stu-id="98357-140">You can browse to your web app using the link provided in the status message.</span></span>

   ![Búsqueda de la aplicación web][browse-web-app]

1. <span data-ttu-id="98357-142">Después de publicar la aplicación web, la configuración se guardará como valor predeterminado y podrá ejecutar la aplicación en Azure al hacer clic en el icono de flecha verde de la barra de herramientas.</span><span class="sxs-lookup"><span data-stu-id="98357-142">After you have published your web app, your settings will be saved as the default, and you can run your application on Azure by clicking the green arrow icon on the toolbar.</span></span> <span data-ttu-id="98357-143">Para modificar esta configuración, haga clic en el menú desplegable de la aplicación web y, luego, en **Edit Configurations** (Editar configuraciones).</span><span class="sxs-lookup"><span data-stu-id="98357-143">You can modify your settings by clicking the drop-down menu for your web app and click **Edit Configurations**.</span></span>

   ![Menú Editar configuración][edit-configuration-menu]

1. <span data-ttu-id="98357-145">Cuando aparezca el cuadro de diálogo **Run/Debug Configurations** (Ejecutar/Depurar configuraciones), podrá modificar cualquiera de los valores predeterminados y hacer clic en **OK** (Aceptar).</span><span class="sxs-lookup"><span data-stu-id="98357-145">When the **Run/Debug Configurations** dialog box is displayed, you can modify any of the default settings, and then click **OK**.</span></span>

   ![Cuadro de diálogo Editar configuración][edit-configuration-dialog]

<hr />

## <a name="create-a-hello-world-web-app-by-using-the-version-306-or-earlier-toolkit"></a><span data-ttu-id="98357-147">Creación de una aplicación web Hola mundo con la versión 3.0.6 o un kit de herramientas anterior</span><span class="sxs-lookup"><span data-stu-id="98357-147">Create a Hello World web app by using the version 3.0.6 or earlier toolkit</span></span>

### <a name="create-a-new-web-app-project"></a><span data-ttu-id="98357-148">Creación de un proyecto de aplicación web nuevo</span><span class="sxs-lookup"><span data-stu-id="98357-148">Create a new web app project</span></span>

1. <span data-ttu-id="98357-149">Inicie IntelliJ y haga clic en **File** (Archivo), **New** (Nuevo) y, finalmente, en **Project** (Proyecto).</span><span class="sxs-lookup"><span data-stu-id="98357-149">Start IntelliJ and click the **File** menu, then click **New**, and then click **Project**.</span></span>
   
   ![Archivo Nuevo Proyecto][02]

2. <span data-ttu-id="98357-151">En el cuadro de diálogo **New Project** (Nuevo proyecto), seleccione **Java** y **Web Application** (Aplicación web) y, después, haga clic en **New** (Nuevo) para agregar un SDK del proyecto.</span><span class="sxs-lookup"><span data-stu-id="98357-151">In the **New Project** dialog box, select **Java**, then **Web Application**, and then click **New** to add a Project SDK.</span></span>
   
   ![Cuadro de diálogo Nuevo proyecto][03a]
   
3. <span data-ttu-id="98357-153">En el cuadro de diálogo Select Home Directory for JDK (Seleccionar directorio de inicio para JDK), seleccione la carpeta donde está instalado el JDK y, después, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="98357-153">In the Select Home Directory for JDK dialog box, select the folder where your JDK is installed, and then click **OK**.</span></span> <span data-ttu-id="98357-154">Haga clic en **Siguiente** en el cuadro de diálogo de nuevo proyecto para continuar.</span><span class="sxs-lookup"><span data-stu-id="98357-154">Click **Next** in the New Project dialog box to continue.</span></span>
   
   ![Especificación del directorio de inicio de JDK][03b]

4. <span data-ttu-id="98357-156">Para este tutorial, asigne al proyecto el nombre **Java-Web-App-On-Azure** y haga clic en **Finish** (Finalizar).</span><span class="sxs-lookup"><span data-stu-id="98357-156">For purposes of this tutorial, name the project **Java-Web-App-On-Azure**, and then click **Finish**.</span></span>
   
   ![Cuadro de diálogo Nuevo proyecto][04]

5. <span data-ttu-id="98357-158">En la vista del explorador de proyectos de IntelliJ, expanda **Java-Web-App-On-Azure**, después expanda **web** y, luego, haga doble clic en **index.jsp**.</span><span class="sxs-lookup"><span data-stu-id="98357-158">Within IntelliJ's Project Explorer view, expand **Java-Web-App-On-Azure**, then expand **web**, and then double-click **index.jsp**.</span></span>
   
   ![Abrir página de índice][05c]

6. <span data-ttu-id="98357-160">Cuando el archivo index.jsp se abra en IntelliJ, agregue texto para que se muestre dinámicamente **Hello World!**</span><span class="sxs-lookup"><span data-stu-id="98357-160">When your index.jsp file opens in IntelliJ, add in text to dynamically display **Hello World!**</span></span> <span data-ttu-id="98357-161">dentro del elemento `<body>` existente.</span><span class="sxs-lookup"><span data-stu-id="98357-161">within the existing `<body>` element.</span></span> <span data-ttu-id="98357-162">El contenido de `<body>` actualizado debe parecerse al siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="98357-162">Your updated `<body>` content should resemble the following example:</span></span>
   
   ```java
   <body><b><% out.println("Hello World!"); %></b></body>
   ```

7. <span data-ttu-id="98357-163">Guarde el archivo index.jsp.</span><span class="sxs-lookup"><span data-stu-id="98357-163">Save index.jsp.</span></span>

### <a name="deploy-your-web-app-to-azure"></a><span data-ttu-id="98357-164">Implementación de una aplicación web en Azure</span><span class="sxs-lookup"><span data-stu-id="98357-164">Deploy your web app to Azure</span></span>
<span data-ttu-id="98357-165">Existen varias maneras de implementar una aplicación web de Java en Azure.</span><span class="sxs-lookup"><span data-stu-id="98357-165">There are several ways by which you can deploy a Java web app to Azure.</span></span> <span data-ttu-id="98357-166">En este tutorial se describe una de las más sencillas: la aplicación se implementará en un contenedor de aplicaciones de Azure: no se necesita ningún tipo de proyecto especial ni herramientas adicionales.</span><span class="sxs-lookup"><span data-stu-id="98357-166">This tutorial describes one of the simplest: your application will be deployed to an Azure Web App Container - no special project type nor additional tools are needed.</span></span> <span data-ttu-id="98357-167">Azure facilitará el JDK y el software de contenedor web, así que no es necesario que cargue los suyos; lo único que necesita es su aplicación web de Java.</span><span class="sxs-lookup"><span data-stu-id="98357-167">The JDK and the web container software will be provided for you by Azure, so there is no need to upload your own; all you need is your Java Web App.</span></span> <span data-ttu-id="98357-168">Como resultado, el proceso de publicación de su aplicación tardará unos segundos y no minutos.</span><span class="sxs-lookup"><span data-stu-id="98357-168">As a result, the publishing process for your application will take seconds, not minutes.</span></span>

<span data-ttu-id="98357-169">Antes de publicar la aplicación, primero debe configurar el módulo.</span><span class="sxs-lookup"><span data-stu-id="98357-169">Before you publish your application, you first need to configure your module settings.</span></span> <span data-ttu-id="98357-170">Para ello, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="98357-170">To do so, use the following steps:</span></span>

1. <span data-ttu-id="98357-171">En el Explorador de proyectos de IntelliJ, haga clic con el botón derecho en el proyecto **Java-Web-App-On-Azure** .</span><span class="sxs-lookup"><span data-stu-id="98357-171">In IntelliJ's Project Explorer, right-click the **Java-Web-App-On-Azure** project.</span></span> <span data-ttu-id="98357-172">Cuando aparezca el menú contextual, haga clic en **Open Module Settings** (Abrir configuración del módulo).</span><span class="sxs-lookup"><span data-stu-id="98357-172">When the context menu appears, click **Open Module Settings**.</span></span>

   ![Abrir configuración del módulo][05a]

2. <span data-ttu-id="98357-174">Cuando se muestre el cuadro de diálogo Project Structure (Estructura de proyecto):</span><span class="sxs-lookup"><span data-stu-id="98357-174">When the Project Structure dialog box appears:</span></span>

   <span data-ttu-id="98357-175">a.</span><span class="sxs-lookup"><span data-stu-id="98357-175">a.</span></span> <span data-ttu-id="98357-176">Haga clic en **Artefactos** en la lista de **configuración del proyecto**.</span><span class="sxs-lookup"><span data-stu-id="98357-176">Click **Artifacts** in the list of **Project Settings**.</span></span>

   <span data-ttu-id="98357-177">b.</span><span class="sxs-lookup"><span data-stu-id="98357-177">b.</span></span> <span data-ttu-id="98357-178">Cambie el nombre del artefacto en el cuadro **Nombre** para que contenga un espacio en blanco o caracteres especiales; esto es necesario porque el nombre se usará en el identificador uniforme de recursos (URI).</span><span class="sxs-lookup"><span data-stu-id="98357-178">Change the artifact name in the **Name** box so that it doesn't contain whitespace or special characters; this is necessary since the name will be used in the Uniform Resource Identifier (URI).</span></span>

   <span data-ttu-id="98357-179">c.</span><span class="sxs-lookup"><span data-stu-id="98357-179">c.</span></span> <span data-ttu-id="98357-180">Cambiar el **tipo** a **Aplicación Web: archivo**.</span><span class="sxs-lookup"><span data-stu-id="98357-180">Change the **Type** to **Web Application: Archive**.</span></span>

   <span data-ttu-id="98357-181">d.</span><span class="sxs-lookup"><span data-stu-id="98357-181">d.</span></span> <span data-ttu-id="98357-182">Haga clic en **OK** (Aceptar) para cerrar el cuadro de diálogo Project Structure (Estructura del proyecto).</span><span class="sxs-lookup"><span data-stu-id="98357-182">Click **OK** to close the Project Structure dialog box.</span></span>

   ![Abrir configuración del módulo][05b]

<span data-ttu-id="98357-184">Cuando se ha configurado el módulo, puede publicar la aplicación en Azure mediante los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="98357-184">When you have configured your module settings, you can publish your application to Azure by using the following steps:</span></span>

1. <span data-ttu-id="98357-185">En el Explorador de proyectos de IntelliJ, haga clic con el botón derecho en el proyecto **Java-Web-App-On-Azure** .</span><span class="sxs-lookup"><span data-stu-id="98357-185">In IntelliJ's Project Explorer, right-click the **Java-Web-App-On-Azure** project.</span></span> <span data-ttu-id="98357-186">Cuando aparezca el menú contextual, seleccione **Azure** y, después, haga clic en **Publish as Azure Web App...** (Publicar como aplicación web de Azure)</span><span class="sxs-lookup"><span data-stu-id="98357-186">When the context menu appears, select **Azure**, and then click **Publish as Azure Web App...**</span></span>
   
   ![Menú contextual de publicación de Azure][06]

2. <span data-ttu-id="98357-188">Si aún no ha iniciado sesión en Azure desde IntelliJ, se le pedirá que lo haga.</span><span class="sxs-lookup"><span data-stu-id="98357-188">If you have not already signed in to Azure from IntelliJ, you will be prompted to sign in to your Azure account.</span></span> <span data-ttu-id="98357-189">(Si tiene varias cuentas de Azure, puede que algunos de los avisos que aparecen durante el proceso de inicio de sesión se muestren más de una vez, incluso si parecen iguales.</span><span class="sxs-lookup"><span data-stu-id="98357-189">(If you have multiple Azure accounts, some of the prompts during the sign-in process may be shown more than once, even if they appear to be the same.</span></span> <span data-ttu-id="98357-190">Cuando esto ocurra, siga la instrucciones de inicio de sesión).</span><span class="sxs-lookup"><span data-stu-id="98357-190">When this happens, continue to follow the sign-in instructions.)</span></span>
   
   ![Cuadro de diálogo de inicio de sesión de Azure][07]

3. <span data-ttu-id="98357-192">Cuando haya iniciado sesión correctamente en su cuenta de Azure, el cuadro de diálogo **Administrar suscripciones** mostrará una lista de suscripciones asociadas a sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="98357-192">After you have successfully signed in to your Azure account, the **Manage Subscriptions** dialog box will display a list of subscriptions that are associated with your credentials.</span></span> <span data-ttu-id="98357-193">Si aparecen varias suscripciones y quiere trabajar solo con un subconjunto específico de ellas, opcionalmente puede desactivar las que no utilice. Cuando haya seleccionado las suscripciones, haga clic en **Cerrar**.</span><span class="sxs-lookup"><span data-stu-id="98357-193">(If there are multiple subscriptions listed and you want to work with only a specific subset of them, you may optionally uncheck the subscriptions you don't want to use.) When you have selected your subscriptions, click **Close**.</span></span>
   
   ![Administrar suscripciones][08]

4. <span data-ttu-id="98357-195">Cuando aparezca el cuadro de diálogo **Deploy to Azure Web App Container** (Implementar en el contenedor de aplicaciones web de Azure), se mostrarán los contenedores de aplicaciones web creados anteriormente; si no ha creado ningún contenedor, la lista estará vacía.</span><span class="sxs-lookup"><span data-stu-id="98357-195">When the **Deploy to Azure Web App Container** dialog box appears, it will display any Web App containers that you have previously created; if you have not created any containers, the list will be empty.</span></span>
   
   ![Contenedores de aplicaciones][09]

5. <span data-ttu-id="98357-197">Si no ha creado un contenedor de aplicaciones web de Azure antes, o si quiere publicar la aplicación en un nuevo contenedor, siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="98357-197">If you have not created an Azure Web App Container before, or if you would like to publish your application to a new container, use the following steps.</span></span> <span data-ttu-id="98357-198">De lo contrario, seleccione un contenedor de aplicaciones web existente y vaya al paso 6 que encontrará a continuación.</span><span class="sxs-lookup"><span data-stu-id="98357-198">Otherwise, select an existing Web App Container and skip to step 6 below.</span></span>
   
   <span data-ttu-id="98357-199">a.</span><span class="sxs-lookup"><span data-stu-id="98357-199">a.</span></span> <span data-ttu-id="98357-200">Haga clic en el signo **+**.</span><span class="sxs-lookup"><span data-stu-id="98357-200">Click the **+** sign.</span></span>
      
      ![Agregar contenedor de aplicaciones][10]

   <span data-ttu-id="98357-202">b.</span><span class="sxs-lookup"><span data-stu-id="98357-202">b.</span></span> <span data-ttu-id="98357-203">Se mostrará el cuadro de diálogo **New Web App Container** (Nuevo contenedor de aplicaciones web), que se usará para los siguientes pasos.</span><span class="sxs-lookup"><span data-stu-id="98357-203">The **New Web App Container** dialog box will be displayed, which will be used for the next several steps.</span></span>
      
      ![Nuevo contenedor de aplicaciones][11a]
   
   <span data-ttu-id="98357-205">c.</span><span class="sxs-lookup"><span data-stu-id="98357-205">c.</span></span> <span data-ttu-id="98357-206">Escriba un valor para **Etiqueta DNS** para el contenedor de aplicaciones web; esta será la etiqueta DNS hoja de la dirección URL del host de la aplicación web en Azure.</span><span class="sxs-lookup"><span data-stu-id="98357-206">Enter a **DNS Label** for your Web App Container; this will form the leaf DNS label of the host URL for your web application in Azure.</span></span> <span data-ttu-id="98357-207">Tenga en cuenta que el nombre debe estar disponible y se ajusta a los requisitos de nomenclatura de las aplicaciones web de Azure.</span><span class="sxs-lookup"><span data-stu-id="98357-207">Note that the name must be available and conform to Azure Web App naming requirements.</span></span>

   <span data-ttu-id="98357-208">d.</span><span class="sxs-lookup"><span data-stu-id="98357-208">d.</span></span> <span data-ttu-id="98357-209">En el menú desplegable **Web Container** (Contenedor web), seleccione el software adecuado para su aplicación.</span><span class="sxs-lookup"><span data-stu-id="98357-209">In the **Web Container** drop-down menu, select the appropriate software for your application.</span></span>
      
      <span data-ttu-id="98357-210">Actualmente, puede elegir entre Tomcat 8, Tomcat 7 o Jetty 9.</span><span class="sxs-lookup"><span data-stu-id="98357-210">Currently, you can choose from Tomcat 8, Tomcat 7 or Jetty 9.</span></span> <span data-ttu-id="98357-211">Azure proporcionará una distribución reciente del software seleccionado y se ejecutará en una distribución reciente de JDK 8 creada por Oracle y proporcionada por Azure.</span><span class="sxs-lookup"><span data-stu-id="98357-211">A recent distribution of the selected software will be provided by Azure, and it will run on a recent distribution of JDK 8 created by Oracle and provided by Azure.</span></span>

   <span data-ttu-id="98357-212">e.</span><span class="sxs-lookup"><span data-stu-id="98357-212">e.</span></span> <span data-ttu-id="98357-213">En el menú desplegable **Suscripción** , seleccione la suscripción que quiere usar para esta implementación.</span><span class="sxs-lookup"><span data-stu-id="98357-213">In the **Subscription** drop-down menu, select the subscription you want to use for this deployment.</span></span>

   <span data-ttu-id="98357-214">f.</span><span class="sxs-lookup"><span data-stu-id="98357-214">f.</span></span> <span data-ttu-id="98357-215">En el menú desplegable **Grupo de recursos** , seleccione el grupo de recursos con el que desea asociar la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="98357-215">In the **Resource Group** drop-down menu, select the Resource Group with which you want to associate your Web App.</span></span> <span data-ttu-id="98357-216">Los grupos de recursos de Azure permiten agrupar recursos relacionados para que, por ejemplo, se puedan eliminar juntos.</span><span class="sxs-lookup"><span data-stu-id="98357-216">(Azure Resource Groups allow you to group related resources together so that, for example, they can be deleted together.)</span></span>
      
      <span data-ttu-id="98357-217">Puede seleccionar un grupo de recursos existente (si tiene alguno) y pasar al paso g a continuación o usar los siguientes pasos para crear un nuevo grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="98357-217">You can select an existing Resource Group (if you have any) and skip to step g below, or use the following steps to create a new Resource Group:</span></span>
      
      * <span data-ttu-id="98357-218">Seleccione **&lt;&lt; Crear nuevo grupo de recursos&gt;&gt;** en el menú desplegable **Grupo de recursos**.</span><span class="sxs-lookup"><span data-stu-id="98357-218">Select **&lt;&lt; Create new Resource Group &gt;&gt;** in the **Resource Group** drop-down menu.</span></span>
      * <span data-ttu-id="98357-219">Se muestra el cuadro de diálogo **Nuevo grupo de recursos** :</span><span class="sxs-lookup"><span data-stu-id="98357-219">The **New Resource Group** dialog box will be displayed:</span></span>
        
         ![Nuevo grupo de recursos][12]

      * <span data-ttu-id="98357-221">En el cuadro de texto **Nombre**, especifique un nombre para el nuevo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="98357-221">In the **Name** textbox, specify a name for your new Resource Group.</span></span>
      * <span data-ttu-id="98357-222">En el menú desplegable **Región**, seleccione la ubicación adecuada del centro de datos de Azure para el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="98357-222">In the **Region** drop-down menu, select the appropriate Azure data center location for your Resource Group.</span></span>
      * <span data-ttu-id="98357-223">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="98357-223">Click **OK**.</span></span>

   <span data-ttu-id="98357-224">g.</span><span class="sxs-lookup"><span data-stu-id="98357-224">g.</span></span> <span data-ttu-id="98357-225">En el menú desplegable **Plan del servicio de aplicaciones** se muestran los planes del servicio de aplicaciones que están asociados con el grupo de recursos seleccionado.</span><span class="sxs-lookup"><span data-stu-id="98357-225">The **App Service Plan** drop-down menu lists the app service plans that are associated with the Resource Group that you selected.</span></span> <span data-ttu-id="98357-226">(Un plan de App Service especifica información como la ubicación de la aplicación web, el plan de tarifa y el tamaño de la instancia de proceso.</span><span class="sxs-lookup"><span data-stu-id="98357-226">(An App Service Plan specifies information such as the location of your Web App, the pricing tier and the compute instance size.</span></span> <span data-ttu-id="98357-227">Un único plan de App Service se puede usar para varias aplicaciones web, motivo por el cual se mantiene independiente de una implementación específica de aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="98357-227">A single App Service Plan can be used for multiple Web Apps, which is why it is maintained separately from a specific Web App deployment.)</span></span>
      
      <span data-ttu-id="98357-228">Puede seleccionar un plan de plan de App Service existente (si tiene alguno) y pasar al paso h a continuación o usar los siguientes pasos para crear un nuevo plan:</span><span class="sxs-lookup"><span data-stu-id="98357-228">You can select an existing App Service Plan (if you have any) and skip to step h below, or use the following steps to create a new App Service Plan:</span></span>
      
      * <span data-ttu-id="98357-229">Seleccione **&lt;&lt; Crear nuevo plan de App Service&gt;&gt;** en el menú desplegable **Plan de App Service**.</span><span class="sxs-lookup"><span data-stu-id="98357-229">Select **&lt;&lt; Create new App Service Plan &gt;&gt;** in the **App Service Plan** drop-down menu.</span></span>
      * <span data-ttu-id="98357-230">Se muestra el cuadro de diálogo **Nuevo plan del servicio de aplicaciones** :</span><span class="sxs-lookup"><span data-stu-id="98357-230">The **New App Service Plan** dialog box will be displayed:</span></span>
        
         ![Nuevo plan de App Service][13]

      * <span data-ttu-id="98357-232">En el cuadro de texto **Nombre**, especifique un nombre para el nuevo plan de App Service.</span><span class="sxs-lookup"><span data-stu-id="98357-232">In the **Name** textbox, specify a name for your new App Service Plan.</span></span>
      * <span data-ttu-id="98357-233">En el menú desplegable **Ubicación**, seleccione la ubicación adecuada del centro de datos de Azure para el plan.</span><span class="sxs-lookup"><span data-stu-id="98357-233">In the **Location** drop-down menu, select the appropriate Azure data center location for the plan.</span></span>
      * <span data-ttu-id="98357-234">En el menú desplegable **Plan de tarifa**, seleccione la tarifa adecuada para el plan.</span><span class="sxs-lookup"><span data-stu-id="98357-234">In the **Pricing Tier** drop-down menu, select the appropriate pricing for the plan.</span></span> <span data-ttu-id="98357-235">Con fines de prueba, puede elegir **Gratis**.</span><span class="sxs-lookup"><span data-stu-id="98357-235">For testing purposes you can choose **Free**.</span></span>
      * <span data-ttu-id="98357-236">En el menú desplegable **Tamaño de instancia**, seleccione el tamaño de instancia adecuado para el plan.</span><span class="sxs-lookup"><span data-stu-id="98357-236">In the **Instance Size** drop-down menu, select the appropriate instance size for the plan.</span></span> <span data-ttu-id="98357-237">Con fines de prueba, puede elegir **Pequeño**.</span><span class="sxs-lookup"><span data-stu-id="98357-237">For testing purposes you can choose **Small**.</span></span>
      * <span data-ttu-id="98357-238">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="98357-238">Click **OK**.</span></span>

   <span data-ttu-id="98357-239">h.</span><span class="sxs-lookup"><span data-stu-id="98357-239">h.</span></span> <span data-ttu-id="98357-240">(Opcional) De manera predeterminada, Azure implementará automáticamente una distribución reciente de Java 8 como máquina virtual de Java en el contenedor de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="98357-240">(Optional) By default, a recent distribution of Java 8 will be automatically deployed as your JVM by Azure to your web app container.</span></span> <span data-ttu-id="98357-241">Sin embargo, puede seleccionar una versión y una distribución diferentes de la máquina virtual de Java.</span><span class="sxs-lookup"><span data-stu-id="98357-241">However, you can select a different version and distribution of the JVM.</span></span> <span data-ttu-id="98357-242">Para ello, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="98357-242">To do so, use the following steps:</span></span>
      
      * <span data-ttu-id="98357-243">Haga clic en la pestaña **JDK** en el cuadro de diálogo **New Web App Container** (Nuevo contenedor de aplicaciones web).</span><span class="sxs-lookup"><span data-stu-id="98357-243">Click the **JDK** tab in the **New Web App Container** dialog box.</span></span>
      * <span data-ttu-id="98357-244">Puede elegir una de las siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="98357-244">You can choose from one of the following options:</span></span>
        
         * <span data-ttu-id="98357-245">Implementar el JDK predeterminado que ofrece Azure</span><span class="sxs-lookup"><span data-stu-id="98357-245">Deploy the default JDK which is offered by Azure</span></span>
         * <span data-ttu-id="98357-246">Implementar un JDK de terceros de lista desplegable de JDK adicionales que están disponibles en Azure</span><span class="sxs-lookup"><span data-stu-id="98357-246">Deploy a 3rd party JDK from a drop-down list of additional JDKs which are available on Azure</span></span>
         * <span data-ttu-id="98357-247">Implementar un JDK personalizado, que debe estar empaquetado en un archivo ZIP y bien estar disponible públicamente o en su cuenta de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="98357-247">Deploy a custom JDK, which must be packaged as a ZIP file and either publicly available or in your Azure storage account</span></span>
        
      ![Pestaña JDK de nuevo contenedor de aplicaciones][11b]

   <span data-ttu-id="98357-249">i.</span><span class="sxs-lookup"><span data-stu-id="98357-249">i.</span></span> <span data-ttu-id="98357-250">Cuando haya completado todos los pasos anteriores, el cuadro de diálogo Nuevo contenedor de aplicaciones web debe parecerse al de la siguiente ilustración:</span><span class="sxs-lookup"><span data-stu-id="98357-250">Once you have completed all of the above steps, the New Web App Container dialog box should resemble the following illustration:</span></span>
      
      ![Nuevo contenedor de aplicaciones][14]
   
   <span data-ttu-id="98357-252">j.</span><span class="sxs-lookup"><span data-stu-id="98357-252">j.</span></span> <span data-ttu-id="98357-253">Haga clic en **Aceptar** para finalizar la creación de su nuevo contenedor de aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="98357-253">Click **OK** to complete the creation of your new Web App container.</span></span>
       
      <span data-ttu-id="98357-254">Espere unos segundos para que se actualice la lista de los contenedores de aplicaciones web y el contenedor recién creado ya debería estar seleccionado en la lista.</span><span class="sxs-lookup"><span data-stu-id="98357-254">Wait a few seconds for the list of the Web App containers to be refreshed, and your newly-created web app container should now be selected in the list.</span></span>

6. <span data-ttu-id="98357-255">Ya puede completar la implementación inicial de su aplicación web en Azure; haga clic en **Aceptar** para implementar la aplicación de Java en el contenedor de aplicación web seleccionado.</span><span class="sxs-lookup"><span data-stu-id="98357-255">You are now ready to complete the initial deployment of your Web App to Azure; click **OK** to deploy your Java application to the selected Web App container.</span></span> <span data-ttu-id="98357-256">De forma predeterminada, la aplicación se implementará como un subdirectorio del servidor de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="98357-256">By default, your application will be deployed as a subdirectory of the application server.</span></span> <span data-ttu-id="98357-257">Si desea que se implemente como aplicación raíz, active la casilla **Deploy to root** (Implementar en raíz) antes de hacer clic en **OK** (Aceptar).</span><span class="sxs-lookup"><span data-stu-id="98357-257">If you want it to be deployed as the root application, check the **Deploy to root** checkbox before clicking **OK**.</span></span>
   
   ![Implementar en Azure][15]

7. <span data-ttu-id="98357-259">A continuación, debería mostrarse la vista **Azure Activity Log** (Registro de actividad de Azure), que indicará el estado de implementación de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="98357-259">Next, you should see the **Azure Activity Log** view, which will indicate the deployment status of your Web App.</span></span>
   
   ![Indicador de progreso][16]
   
   <span data-ttu-id="98357-261">El proceso de implementación de la aplicación web en Azure debería tardar solo unos segundos en completarse.</span><span class="sxs-lookup"><span data-stu-id="98357-261">The process of deploying your Web App to Azure should take only a few seconds to complete.</span></span> <span data-ttu-id="98357-262">Cuando la aplicación esté lista, verá un vínculo denominado **Publicado** en la columna **Estado**.</span><span class="sxs-lookup"><span data-stu-id="98357-262">When your application is ready, you will see a link named **Published** in the **Status** column.</span></span> <span data-ttu-id="98357-263">Al hacer clic en el vínculo, se le llevará a la página principal de la aplicación web implementada. Por otro lado, puede utilizar los pasos de la sección siguiente para ir a la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="98357-263">When you click the link, it will take you to your deployed Web App's home page, or you can use the steps in the following section to browse to your web app.</span></span>

### <a name="browsing-to-your-web-app-on-azure"></a><span data-ttu-id="98357-264">Desplazamiento hasta su aplicación web en Azure</span><span class="sxs-lookup"><span data-stu-id="98357-264">Browsing to your Web App on Azure</span></span>
<span data-ttu-id="98357-265">Para ir a su aplicación web en Azure, puede usar la vista **Azure Explorer**.</span><span class="sxs-lookup"><span data-stu-id="98357-265">To browse to your Web App on Azure, you can use the **Azure Explorer** view.</span></span>

<span data-ttu-id="98357-266">Si la vista del **Explorador de Azure** no está abierta, puede abrirla haciendo clic en el menú **View** (Ver) de IntelliJ, luego haga clic en **Tool Windows** (Ventanas de herramientas) y, después, en **Service Explorer** (Explorador de servicios).</span><span class="sxs-lookup"><span data-stu-id="98357-266">If the **Azure Explorer** view is not already open, you can open it by clicking then **View** menu in IntelliJ, then click **Tool Windows**, and then click **Service Explorer**.</span></span> <span data-ttu-id="98357-267">Si anteriormente no ha iniciado sesión, se le pedirá que lo haga.</span><span class="sxs-lookup"><span data-stu-id="98357-267">If you have not previously logged in, it will prompt you to do so.</span></span>

<span data-ttu-id="98357-268">Cuando se muestre la vista **Azure Explorer** (Explorador de Azure), siga estos pasos para buscar la aplicación web:</span><span class="sxs-lookup"><span data-stu-id="98357-268">When the **Azure Explorer** view is displayed, follow these steps to browse to your Web App:</span></span> 

1. <span data-ttu-id="98357-269">Expanda el nodo **Azure** .</span><span class="sxs-lookup"><span data-stu-id="98357-269">Expand the **Azure** node.</span></span>
2. <span data-ttu-id="98357-270">Expanda el nodo **Aplicaciones web** .</span><span class="sxs-lookup"><span data-stu-id="98357-270">Expand the **Web Apps** node.</span></span> 
3. <span data-ttu-id="98357-271">Haga clic en la aplicación web deseada.</span><span class="sxs-lookup"><span data-stu-id="98357-271">Right-click the desired Web App.</span></span>
4. <span data-ttu-id="98357-272">Cuando aparezca el menú contextual, haga clic en **Abrir en el explorador**.</span><span class="sxs-lookup"><span data-stu-id="98357-272">When the context menu appears, click **Open in Browser**.</span></span>
   
   ![Examinar una aplicación web][17]

### <a name="updating-your-web-app"></a><span data-ttu-id="98357-274">Actualización de la aplicación web</span><span class="sxs-lookup"><span data-stu-id="98357-274">Updating your web app</span></span>
<span data-ttu-id="98357-275">Actualizar una aplicación web de Azure existente es un proceso rápido y sencillo, y tiene dos opciones para ello:</span><span class="sxs-lookup"><span data-stu-id="98357-275">Updating an existing running Azure Web App is a quick and easy process, and you have two options for updating:</span></span>

* <span data-ttu-id="98357-276">Puede actualizar la implementación de una aplicación web de Java existente.</span><span class="sxs-lookup"><span data-stu-id="98357-276">You can update the deployment of an existing Java Web App.</span></span>
* <span data-ttu-id="98357-277">Puede publicar una aplicación Java adicional en el mismo contenedor de aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="98357-277">You can publish an additional Java application to the same Web App Container.</span></span>

<span data-ttu-id="98357-278">En cualquier caso, el proceso es idéntico y tarda unos pocos segundos:</span><span class="sxs-lookup"><span data-stu-id="98357-278">In either case, the process is identical and takes only a few seconds:</span></span>

1. <span data-ttu-id="98357-279">En el Explorador de proyectos de IntelliJ, haga clic con el botón derecho en la aplicación Java que quiere actualizar o agregar a un contenedor de aplicaciones web existente.</span><span class="sxs-lookup"><span data-stu-id="98357-279">In the IntelliJ project explorer, right-click the Java application you want to update or add to an existing Web App Container.</span></span>
2. <span data-ttu-id="98357-280">Cuando aparezca el menú contextual, seleccione **Azure** y, después, haga clic en **Publish as Azure Web App...** (Publicar como aplicación web de Azure).</span><span class="sxs-lookup"><span data-stu-id="98357-280">When the context menu appears, select **Azure** and then **Publish as Azure Web App...**</span></span>
3. <span data-ttu-id="98357-281">Puesto que ya ha iniciado sesión anteriormente, verá una lista de contenedores de aplicaciones web existentes.</span><span class="sxs-lookup"><span data-stu-id="98357-281">Since you have already logged in previously, you will see a list of your existing Web App containers.</span></span> <span data-ttu-id="98357-282">Seleccione aquel en el que quiere publicar o volver a publicar la aplicación Java y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="98357-282">Select the one you want to publish or re-publish your Java application to and click **OK**.</span></span>

<span data-ttu-id="98357-283">Unos segundos más tarde, la vista **Azure Activity Log** (Registro de actividad de Azure) mostrará la implementación actualizada como **Published** (Publicado) y podrá comprobar la aplicación actualizada en un explorador web.</span><span class="sxs-lookup"><span data-stu-id="98357-283">A few seconds later, the **Azure Activity Log** view will show your updated deployment as **Published** and you will be able to verify your updated application in a web browser.</span></span>

### <a name="starting-stopping-or-restarting-an-existing-web-app"></a><span data-ttu-id="98357-284">Inicio, detención o reinicio de una aplicación web existente</span><span class="sxs-lookup"><span data-stu-id="98357-284">Starting, stopping, or restarting an existing web app</span></span>
<span data-ttu-id="98357-285">Para iniciar o detener un contenedor de aplicaciones web existente (junto con todas las aplicaciones Java implementadas en él), puede utilizar la vista **Azure Explorer** (Explorador de Azure).</span><span class="sxs-lookup"><span data-stu-id="98357-285">To start or stop an existing Azure Web App container, (including all the deployed Java applications in it), you can use the **Azure Explorer** view.</span></span>

<span data-ttu-id="98357-286">Si la vista del **Explorador de Azure** no está abierta, puede abrirla haciendo clic en el menú **View** (Ver) de IntelliJ, luego haga clic en **Tool Windows** (Ventanas de herramientas) y, después, en **Service Explorer** (Explorador de servicios).</span><span class="sxs-lookup"><span data-stu-id="98357-286">If the **Azure Explorer** view is not already open, you can open it by clicking then **View** menu in IntelliJ, then click **Tool Windows**, and then click **Service Explorer**.</span></span> <span data-ttu-id="98357-287">Si anteriormente no ha iniciado sesión, se le pedirá que lo haga.</span><span class="sxs-lookup"><span data-stu-id="98357-287">If you have not previously logged in, it will prompt you to do so.</span></span>

<span data-ttu-id="98357-288">Cuando se muestre la vista **Azure Explorer** (Explorador de Azure), siga estos pasos para iniciar o detener la aplicación web:</span><span class="sxs-lookup"><span data-stu-id="98357-288">When the **Azure Explorer** view is displayed, follow these steps to start or stop your Web App:</span></span> 

1. <span data-ttu-id="98357-289">Expanda el nodo **Azure** .</span><span class="sxs-lookup"><span data-stu-id="98357-289">Expand the **Azure** node.</span></span>
2. <span data-ttu-id="98357-290">Expanda el nodo **Aplicaciones web** .</span><span class="sxs-lookup"><span data-stu-id="98357-290">Expand the **Web Apps** node.</span></span> 
3. <span data-ttu-id="98357-291">Haga clic en la aplicación web deseada.</span><span class="sxs-lookup"><span data-stu-id="98357-291">Right-click the desired Web App.</span></span>
4. <span data-ttu-id="98357-292">Cuando aparezca el menú contextual, haga clic en **Iniciar**, **Detener** o **Reiniciar**.</span><span class="sxs-lookup"><span data-stu-id="98357-292">When the context menu appears, click **Start**, **Stop**, or **Restart**.</span></span> <span data-ttu-id="98357-293">Tenga en cuenta que las opciones de menú dependen del contexto, por lo que solo podrá detener una aplicación web que se encuentre en ejecución o iniciar una aplicación web que no se esté ejecutando en ese momento.</span><span class="sxs-lookup"><span data-stu-id="98357-293">Note that the menu choices are context-aware, so you can only stop a running web app or start a web app which is not currently running.</span></span>
   
   ![Detener aplicación web][18]

## <a name="next-steps"></a><span data-ttu-id="98357-295">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="98357-295">Next steps</span></span>

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<span data-ttu-id="98357-296">Para obtener más información sobre cómo crear aplicaciones web de Azure, consulte [Introducción a Aplicaciones web].</span><span class="sxs-lookup"><span data-stu-id="98357-296">For additional information about creating Azure Web Apps, see the [Web Apps Overview].</span></span>

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
