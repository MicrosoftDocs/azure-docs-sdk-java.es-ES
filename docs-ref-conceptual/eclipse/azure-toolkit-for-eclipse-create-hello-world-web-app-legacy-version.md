---
title: ''
description: En este tutorial se muestra cómo utilizar la versión 3.0.6 (o versiones anteriores) del Kit de herramientas de Azure para Eclipse para crear una aplicación web Hello World para Azure.
services: app-service
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 11/13/2018
ms.devlang: java
ms.service: app-service
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: b05dcd52f36524ab17652f83c6ced4006f874365
ms.sourcegitcommit: 8d0c59ae7c91adbb9be3c3e6d4a3429ffe51519d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/27/2018
ms.locfileid: "52338719"
---
# <a name="create-a-hello-world-web-app-for-azure-using-the-legacy-toolkit-for-eclipse"></a><span data-ttu-id="a51c7-102">Creación de una aplicación web Hello World para Azure con el kit de herramientas heredado para Eclipse</span><span class="sxs-lookup"><span data-stu-id="a51c7-102">Create a Hello World web app for Azure using the legacy toolkit for Eclipse</span></span>

<span data-ttu-id="a51c7-103">En este tutorial se muestra cómo crear e implementar una aplicación básica Hello World en Azure como una aplicación web con la versión 3.0.6 (o versiones anteriores) del [Kit de herramientas de Azure para Eclipse].</span><span class="sxs-lookup"><span data-stu-id="a51c7-103">This tutorial shows how to create and deploy a basic Hello World application to Azure as a web app by using version 3.0.6 (or earlier) of the [Azure Toolkit for Eclipse].</span></span>

> [!NOTE]
>
> <span data-ttu-id="a51c7-104">Para ver la versión de este artículo que usa el [Kit de herramientas de Azure para IntelliJ], consulte [Creación de una aplicación web Hello World para Azure mediante IntelliJ][intellij-hello-world].</span><span class="sxs-lookup"><span data-stu-id="a51c7-104">For a version of this article that uses the [Azure Toolkit for IntelliJ], see [Create a Hello World web app for Azure using IntelliJ][intellij-hello-world].</span></span>
>

> [!IMPORTANT]
> 
> <span data-ttu-id="a51c7-105">El Kit de herramientas de Azure para Eclipse se actualizó en agosto de 2017, con un flujo de trabajo diferente.</span><span class="sxs-lookup"><span data-stu-id="a51c7-105">The Azure Toolkit for Eclipse was updated in August 2017 with a different workflow.</span></span> <span data-ttu-id="a51c7-106">En este artículo se muestra la creación de una aplicación web Hello World con la versión 3.0.6 (o posterior) del Kit de herramientas de Azure para Eclipse.</span><span class="sxs-lookup"><span data-stu-id="a51c7-106">This article illustrates creating a Hello World web app by using version 3.0.6 (or earlier) of the Azure Toolkit for Eclipse.</span></span> <span data-ttu-id="a51c7-107">Si está usando la versión 3.0.7 (o posterior) del Kit de herramientas, debe seguir los pasos descritos en [Creación de una aplicación web Hello World de Azure en Eclipse][Updated Version].</span><span class="sxs-lookup"><span data-stu-id="a51c7-107">If you are using the version 3.0.7 (or later) of the toolkit, you will need to follow the steps in [Create a Hello World web app for Azure in Eclipse][Updated Version].</span></span>
>

<span data-ttu-id="a51c7-108">Cuando haya completado este tutorial, la aplicación se parecerá a la que se muestra en la siguiente ilustración al verla en un explorador web:</span><span class="sxs-lookup"><span data-stu-id="a51c7-108">When you have completed this tutorial, your application will look similar to the following illustration when you view it in a web browser:</span></span>

![Versión preliminar de la aplicación Hello World][01]

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="create-a-new-web-app-project"></a><span data-ttu-id="a51c7-110">Creación de un proyecto de aplicación web nuevo</span><span class="sxs-lookup"><span data-stu-id="a51c7-110">Create a new web app project</span></span>

1. <span data-ttu-id="a51c7-111">Inicie Eclipse e inicie sesión en su cuenta de Azure siguiendo las instrucciones del artículo [Instrucciones de inicio de sesión del kit de herramientas de Azure para Eclipse][eclipse-sign-in-instructions].</span><span class="sxs-lookup"><span data-stu-id="a51c7-111">Start Eclipse, and sign into your Azure account by using the instructions in the [Azure Sign In Instructions for the Azure Toolkit for Eclipse][eclipse-sign-in-instructions] article.</span></span>

1. <span data-ttu-id="a51c7-112">Haga clic en **File** (Archivo), haga clic en **New** (Nuevo) y luego haga clic en **Dynamic Web Project** (Proyecto web dinámico).</span><span class="sxs-lookup"><span data-stu-id="a51c7-112">Click **File**, click **New**, and then click **Dynamic Web Project**.</span></span> <span data-ttu-id="a51c7-113">[Si no ve que **Dynamic Web Project** aparezca como disponible después de hacer clic en **File** (Archivo) y **New** (Nuevo), haga clic en **File** (Archivo), **New** (Nuevo), **Project...** (Proyecto...), expanda **Web**, haga clic en **Dynamic Web Project** (Proyecto web dinámica) y, finalmente, haga clic en **Next** (Siguiente).]</span><span class="sxs-lookup"><span data-stu-id="a51c7-113">(If you don't see **Dynamic Web Project** listed as an available project after clicking **File** and **New**, then do the following: click **File**, click **New**, click **Project...**, expand **Web**, click **Dynamic Web Project**, and click **Next**.)</span></span>

2. <span data-ttu-id="a51c7-114">Para los fines de este tutorial, asigne el nombre **MyWebApp**al proyecto.</span><span class="sxs-lookup"><span data-stu-id="a51c7-114">For purposes of this tutorial, name the project **MyWebApp**.</span></span> <span data-ttu-id="a51c7-115">La pantalla se parecerá a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="a51c7-115">Your screen will appear similar to the following:</span></span>
   
   ![Creación de un nuevo proyecto web dinámico][02]

3. <span data-ttu-id="a51c7-117">Haga clic en **Finalizar**</span><span class="sxs-lookup"><span data-stu-id="a51c7-117">Click **Finish**.</span></span>

4. <span data-ttu-id="a51c7-118">En la vista del **Explorador de proyectos** de Eclipse, expanda **MyWebApp**.</span><span class="sxs-lookup"><span data-stu-id="a51c7-118">Within Eclipse's **Project Explorer** view, expand **MyWebApp**.</span></span> <span data-ttu-id="a51c7-119">Haga clic con el botón derecho en **WebContent**, haga clic en **New** (Nuevo) y, después, en **JSP File** (Archivo JSP).</span><span class="sxs-lookup"><span data-stu-id="a51c7-119">Right-click **WebContent**, click **New**, and then click **JSP File**.</span></span>

5. <span data-ttu-id="a51c7-120">En el cuadro de diálogo **New JSP File** (Nuevo archivo JSP), asigne un nombre del archivo **index.jsp**, conserve la carpeta principal como **MyWebApp/WebContent** y haga clic en **Next** (Siguiente).</span><span class="sxs-lookup"><span data-stu-id="a51c7-120">In the **New JSP File** dialog box, name the file **index.jsp**, keep the parent folder as **MyWebApp/WebContent**, and then click **Next**.</span></span>

6. <span data-ttu-id="a51c7-121">Para este tutorial, en el cuadro de diálogo **Select JSP Template** (Seleccionar plantilla JSP), seleccione **New JSP File (html)** [Nuevo archivo JSP (html)] y haga clic en **Finish** (Finalizar).</span><span class="sxs-lookup"><span data-stu-id="a51c7-121">In the **Select JSP Template** dialog box, for purposes of this tutorial select **New JSP File (html)**, and then click **Finish**.</span></span>

7. <span data-ttu-id="a51c7-122">Cuando el archivo index.jsp se abra en Eclipse, agregue texto para que se muestre dinámicamente **Hello World!**</span><span class="sxs-lookup"><span data-stu-id="a51c7-122">When your index.jsp file opens in Eclipse, add in text to dynamically display **Hello World!**</span></span> <span data-ttu-id="a51c7-123">dentro del elemento `<body>` existente.</span><span class="sxs-lookup"><span data-stu-id="a51c7-123">within the existing `<body>` element.</span></span> <span data-ttu-id="a51c7-124">El contenido de `<body>` actualizado debe parecerse al siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="a51c7-124">Your updated `<body>` content should resemble the following example:</span></span>
   
   ```jsp
   <body><b><% out.println("Hello World!"); %></b></body>
   ```

8. <span data-ttu-id="a51c7-125">Guarde el archivo index.jsp.</span><span class="sxs-lookup"><span data-stu-id="a51c7-125">Save index.jsp.</span></span>

## <a name="deploy-your-web-app-to-azure"></a><span data-ttu-id="a51c7-126">Implementación de una aplicación web en Azure</span><span class="sxs-lookup"><span data-stu-id="a51c7-126">Deploy your web app to Azure</span></span>

<span data-ttu-id="a51c7-127">Existen varias maneras de implementar una aplicación web de Java en Azure.</span><span class="sxs-lookup"><span data-stu-id="a51c7-127">There are several ways by which you can deploy a Java web application to Azure.</span></span> <span data-ttu-id="a51c7-128">En este tutorial se describe una de las más sencillas: la aplicación se implementará en un contenedor de aplicaciones de Azure: no se necesita ningún tipo de proyecto especial ni herramientas adicionales.</span><span class="sxs-lookup"><span data-stu-id="a51c7-128">This tutorial describes one of the simplest: your application will be deployed to an Azure Web App Container - no special project type nor additional tools are needed.</span></span> <span data-ttu-id="a51c7-129">Azure facilitará el JDK y el software de contenedor web, así que no es necesario que cargue los suyos; lo único que necesita es su aplicación web de Java.</span><span class="sxs-lookup"><span data-stu-id="a51c7-129">The JDK and the web container software will be provided for you by Azure, so there is no need to upload your own; all you need is your Java Web App.</span></span> <span data-ttu-id="a51c7-130">Como resultado, el proceso de publicación de su aplicación tardará unos segundos y no minutos.</span><span class="sxs-lookup"><span data-stu-id="a51c7-130">As a result, the publishing process for your application will take seconds, not minutes.</span></span>

1. <span data-ttu-id="a51c7-131">En el Explorador de proyectos de Eclipse, haga clic con el botón derecho en **MyWebApp**.</span><span class="sxs-lookup"><span data-stu-id="a51c7-131">In Eclipse's Project Explorer, right-click **MyWebApp**.</span></span>

2. <span data-ttu-id="a51c7-132">En el menú contextual, seleccione **Azure** y, luego, haga clic en **Publish as Azure Web App...** (Publicar como aplicación web de Azure).</span><span class="sxs-lookup"><span data-stu-id="a51c7-132">In the context menu, select **Azure**, then click **Publish as Azure Web App...**</span></span>
   
   ![Publish as Azure Web App][03]
   
   <span data-ttu-id="a51c7-134">O bien, con el proyecto de aplicación web seleccionado en el Explorador de proyectos, puede hacer clic en el botón desplegable **Publish** (Publicar) de la barra de herramientas y seleccionar **Publish as Azure Web App** (Publicar como aplicación web de Azure) ahí:</span><span class="sxs-lookup"><span data-stu-id="a51c7-134">Alternatively, while your web application project is selected in the Project Explorer, you can click the **Publish** dropdown button on the toolbar and select **Publish as Azure Web App** from there:</span></span>
   
   ![Publish as Azure Web App][14]

3. <span data-ttu-id="a51c7-136">Si aún no ha iniciado sesión en Azure desde Eclipse, se le pedirá que inicie sesión en su cuenta de Azure:</span><span class="sxs-lookup"><span data-stu-id="a51c7-136">If you have not already signed into Azure from Eclipse, you will be prompted to sign into your Azure account:</span></span>
   
   ![Cuadro de diálogo de inicio de sesión en Azure][04]
   
   <span data-ttu-id="a51c7-138">Si tiene varias cuentas de Azure, puede que algunos de los avisos que aparecen durante el proceso de inicio de sesión se muestren más de una vez, incluso si parecen ser iguales.</span><span class="sxs-lookup"><span data-stu-id="a51c7-138">If you have multiple Azure accounts, some of the prompts during the sign in process may be shown more than once, even if they appear to be the same.</span></span> <span data-ttu-id="a51c7-139">Cuando esto ocurra, siga la instrucciones de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="a51c7-139">When this happens, continue following the sign in instructions.</span></span>

4. <span data-ttu-id="a51c7-140">Cuando haya iniciado sesión correctamente en su cuenta de Azure, el cuadro de diálogo **Manage Subscriptions** (Administrar suscripciones) mostrará una lista de suscripciones que están asociadas con sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="a51c7-140">After you have successfully signed into your Azure account, the **Manage Subscriptions** dialog box will display a list of subscriptions that are associated with your credentials.</span></span> <span data-ttu-id="a51c7-141">Si aparecen varias suscripciones y quiere trabajar solo con un subconjunto específico de ellas, opcionalmente puede desactivar las que no utilice.</span><span class="sxs-lookup"><span data-stu-id="a51c7-141">If there are multiple subscriptions listed and you want to work with only a specific subset of them, you may optionally uncheck the ones you do want to use.</span></span> <span data-ttu-id="a51c7-142">Cuando haya seleccionado las suscripciones, haga clic en **Cerrar**.</span><span class="sxs-lookup"><span data-stu-id="a51c7-142">When you have selected your subscriptions, click **Close**.</span></span>
   
   ![Cuadro de diálogo Administrar suscripciones][05]

5. <span data-ttu-id="a51c7-144">Cuando aparezca el cuadro de diálogo **Deploy to Azure Web App Container** (Implementar en el contenedor de aplicaciones web de Azure), se mostrarán los contenedores de aplicaciones web creados anteriormente; si no ha creado ningún contenedor, la lista estará vacía.</span><span class="sxs-lookup"><span data-stu-id="a51c7-144">When the **Deploy to Azure Web App Container** dialog box appears, it will display any Web App containers that you have previously created; if you have not created any containers, the list will be empty.</span></span>
   
   ![Cuadro de diálogo de implementación en contenedor de Azure Web App][06]

6. <span data-ttu-id="a51c7-146">Si no ha creado un contenedor de aplicaciones web de Azure antes, o si quiere publicar la aplicación en un nuevo contenedor, siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="a51c7-146">If you have not created an Azure Web App Container before, or if you would like to publish your application to a new container, use the following steps.</span></span> <span data-ttu-id="a51c7-147">De lo contrario, seleccione un contenedor de aplicaciones web existente y vaya al paso 7 a continuación.</span><span class="sxs-lookup"><span data-stu-id="a51c7-147">Otherwise, select an existing Web App Container and skip to step 7 below.</span></span>
   
   <span data-ttu-id="a51c7-148"> a.</span><span class="sxs-lookup"><span data-stu-id="a51c7-148">a.</span></span> <span data-ttu-id="a51c7-149">Haga clic en **Nuevo...**</span><span class="sxs-lookup"><span data-stu-id="a51c7-149">Click **New...**</span></span>
      
      ![Cuadro de diálogo de implementación en contenedor de Azure Web App][15]

   <span data-ttu-id="a51c7-151">b.</span><span class="sxs-lookup"><span data-stu-id="a51c7-151">b.</span></span> <span data-ttu-id="a51c7-152">Se muestra el cuadro de diálogo **New Web App Container** (Nuevo contenedor de aplicaciones web):</span><span class="sxs-lookup"><span data-stu-id="a51c7-152">The **New Web App Container** dialog box will be displayed:</span></span>
      
      ![Cuadro de diálogo de implementación en nuevo contenedor de aplicación web][07a]

   <span data-ttu-id="a51c7-154">c.</span><span class="sxs-lookup"><span data-stu-id="a51c7-154">c.</span></span> <span data-ttu-id="a51c7-155">Escriba un valor para **Etiqueta DNS** para el contenedor de aplicaciones web; esta será la etiqueta DNS hoja de la dirección URL del host de la aplicación web en Azure.</span><span class="sxs-lookup"><span data-stu-id="a51c7-155">Enter a **DNS Label** for your Web App Container; this will form the leaf DNS label of the host URL for your web application in Azure.</span></span> <span data-ttu-id="a51c7-156">Tenga en cuenta que el nombre debe estar disponible y ajustarse a los requisitos de nomenclatura de las aplicaciones web de Azure.</span><span class="sxs-lookup"><span data-stu-id="a51c7-156">(Note that the name must be available and conform to Azure Web App naming requirements.)</span></span>

   <span data-ttu-id="a51c7-157">d.</span><span class="sxs-lookup"><span data-stu-id="a51c7-157">d.</span></span> <span data-ttu-id="a51c7-158">En el menú desplegable **Web Container** (Contenedor web), seleccione el software adecuado para su aplicación.</span><span class="sxs-lookup"><span data-stu-id="a51c7-158">In the **Web Container** drop-down menu, select the appropriate software for your application.</span></span>
      
      <span data-ttu-id="a51c7-159">Actualmente, puede elegir entre Tomcat 8, Tomcat 7 o Jetty 9.</span><span class="sxs-lookup"><span data-stu-id="a51c7-159">Currently, you can choose from Tomcat 8, Tomcat 7 or Jetty 9.</span></span> <span data-ttu-id="a51c7-160">Azure proporcionará una distribución reciente del software seleccionado y se ejecutará en una distribución reciente del JDK proporcionada por Azure.</span><span class="sxs-lookup"><span data-stu-id="a51c7-160">A recent distribution of the selected software will be provided by Azure, and it will run on a recent distribution of the JDK provided by Azure.</span></span>

   <span data-ttu-id="a51c7-161">e.</span><span class="sxs-lookup"><span data-stu-id="a51c7-161">e.</span></span> <span data-ttu-id="a51c7-162">En el menú desplegable **Suscripción** , seleccione la suscripción que quiere usar para esta implementación.</span><span class="sxs-lookup"><span data-stu-id="a51c7-162">In the **Subscription** drop-down menu, select the subscription you want to use for this deployment.</span></span>

   <span data-ttu-id="a51c7-163">f.</span><span class="sxs-lookup"><span data-stu-id="a51c7-163">f.</span></span> <span data-ttu-id="a51c7-164">En el menú desplegable **Grupo de recursos** , seleccione el grupo de recursos con el que desea asociar la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="a51c7-164">In the **Resource Group** drop-down menu, select the Resource Group with which you want to associate your Web App.</span></span> <span data-ttu-id="a51c7-165">Los grupos de recursos de Azure permiten agrupar recursos relacionados para que, por ejemplo, se puedan eliminar juntos.</span><span class="sxs-lookup"><span data-stu-id="a51c7-165">(Azure Resource Groups allow you to group related resources together so that, for example, they can be deleted together.)</span></span>
      
      <span data-ttu-id="a51c7-166">Puede seleccionar un grupo de recursos existente (si tiene alguno) y pasar al paso g a continuación o usar los siguientes pasos para crear un nuevo grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="a51c7-166">You can select an existing Resource Group (if you have any) and skip to step g below, or use the following these steps to create a new Resource Group:</span></span>
      
   * <span data-ttu-id="a51c7-167">Haga clic en **Nuevo...**</span><span class="sxs-lookup"><span data-stu-id="a51c7-167">Click **New...**</span></span>
   * <span data-ttu-id="a51c7-168">Se muestra el cuadro de diálogo **Nuevo grupo de recursos** :</span><span class="sxs-lookup"><span data-stu-id="a51c7-168">The **New Resource Group** dialog box will be displayed:</span></span>
        
       ![Cuadro de diálogo Nuevo grupo de recursos][08]
   * <span data-ttu-id="a51c7-170">En el cuadro de texto **Nombre** , especifique un nombre para el nuevo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="a51c7-170">In the the **Name** textbox, specify a name for your new Resource Group.</span></span>
   * <span data-ttu-id="a51c7-171">En el menú desplegable **Región** , seleccione la ubicación adecuada del centro de datos de Azure para su grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="a51c7-171">In the the **Region** drop-down menu, select the appropriate Azure data center location for your Resource Group.</span></span>
   * <span data-ttu-id="a51c7-172">OPCIONAL: De forma predeterminada, Azure implementará una distribución reciente de Java 8 automáticamente en el contenedor de la aplicación web como la máquina virtual de Java.</span><span class="sxs-lookup"><span data-stu-id="a51c7-172">OPTIONAL: By default, a recent distribution of Java 8 will be deployed by Azure automatically to your web app container as your JVM.</span></span> <span data-ttu-id="a51c7-173">Sin embargo, puede especificar una versión y una distribución diferentes de la máquina virtual de Java si así lo requiere la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="a51c7-173">However, you can specify a different version and distribution of the JVM if your Web App requires it.</span></span> <span data-ttu-id="a51c7-174">Para especificar el JDK de la aplicación web, haga clic en la pestaña **JDK** y seleccione una de las siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="a51c7-174">To specify the JDK for your Web App, click the **JDK** tab, and select one of the following options:</span></span>
     * <span data-ttu-id="a51c7-175">**Implementar el JDK predeterminado que ofrece el servicio Azure Web Apps**: esta opción implementará una distribución reciente de Java.</span><span class="sxs-lookup"><span data-stu-id="a51c7-175">**Deploy the default JDK offered by Azure Web Apps service**: This option will deploy a recent distribution of Java.</span></span>
     * <span data-ttu-id="a51c7-176">**Implementar un JDK de terceros disponible en Azure**: esta opción permite elegir en la lista el JDK que proporciona Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="a51c7-176">**Deploy a 3rd party JDK available on Azure**: This option allows you to choose from the list of JDKs which are provided by Microsoft Azure.</span></span>
     * <span data-ttu-id="a51c7-177">**Implementar mi propio JDK desde esta ubicación de descarga**: esta opción permite especificar su propia distribución JDK, que se debe empaquetar como un archivo ZIP y cargarse en una ubicación de descarga disponible públicamente o en una cuenta de Azure Storage a la que tenga acceso.</span><span class="sxs-lookup"><span data-stu-id="a51c7-177">**Deploy my own JDK from this download location**: This option allows you to specify your own JDK distribution, which must be packaged as a ZIP file and uploaded to either a publicly available download location or an Azure storage account for which you have access.</span></span>
          
       ![Cuadro de diálogo de implementación en nuevo contenedor de aplicación web][07b]

   <span data-ttu-id="a51c7-179">g.</span><span class="sxs-lookup"><span data-stu-id="a51c7-179">g.</span></span> <span data-ttu-id="a51c7-180">Haga clic en **OK**.</span><span class="sxs-lookup"><span data-stu-id="a51c7-180">Click **OK**.</span></span>

   <span data-ttu-id="a51c7-181">h.</span><span class="sxs-lookup"><span data-stu-id="a51c7-181">h.</span></span> <span data-ttu-id="a51c7-182">En el menú desplegable **Plan de App Service** se muestran los planes de App Service que están asociados con el grupo de recursos seleccionado.</span><span class="sxs-lookup"><span data-stu-id="a51c7-182">The **App Service Plan** drop-down menu lists the app service plans that are associated with the Resource Group that you selected.</span></span> <span data-ttu-id="a51c7-183">Los planes de App Service especifican información como la ubicación de la aplicación web, el plan de tarifas y el tamaño de la instancia de proceso.</span><span class="sxs-lookup"><span data-stu-id="a51c7-183">(App Service Plans specify information such as the location of your Web App, the pricing tier and the compute instance size.</span></span> <span data-ttu-id="a51c7-184">Un único plan de App Service se puede usar para varias Web Apps, motivo por el cual se mantiene independiente de una implementación específica de Web Apps.)</span><span class="sxs-lookup"><span data-stu-id="a51c7-184">A single App Service Plan can be used for multiple Web Apps, which is why it is maintained separately from a specific Web App deployment.)</span></span>
      
       You can select an existing App Service Plan (if you have any) and skip to step h below, or use the following these steps to create a new App Service Plan:
      
      * <span data-ttu-id="a51c7-185">Haga clic en **Nuevo...**</span><span class="sxs-lookup"><span data-stu-id="a51c7-185">Click **New...**</span></span>
      * <span data-ttu-id="a51c7-186">Se muestra el cuadro de diálogo **Nuevo plan de App Service** :</span><span class="sxs-lookup"><span data-stu-id="a51c7-186">The **New App Service Plan** dialog box will be displayed:</span></span>
        
          ![Cuadro de diálogo de nuevo plan de App Service][09]
      * <span data-ttu-id="a51c7-188">En el cuadro de texto **Nombre** , especifique un nombre para el nuevo plan.</span><span class="sxs-lookup"><span data-stu-id="a51c7-188">In the the **Name** textbox, specify a name for your new App Service Plan.</span></span>
      * <span data-ttu-id="a51c7-189">En el menú desplegable **Ubicación** , seleccione la ubicación adecuada del centro de datos de Azure para el plan.</span><span class="sxs-lookup"><span data-stu-id="a51c7-189">In the the **Location** drop-down menu, select the appropriate Azure data center location for the plan.</span></span>
      * <span data-ttu-id="a51c7-190">En el menú desplegable **Plan de tarifa** , seleccione la tarifa adecuada para el plan.</span><span class="sxs-lookup"><span data-stu-id="a51c7-190">In the the **Pricing Tier** drop-down menu, select the appropriate pricing for the plan.</span></span> <span data-ttu-id="a51c7-191">Con fines de prueba, puede elegir **Gratis**.</span><span class="sxs-lookup"><span data-stu-id="a51c7-191">For testing purposes you can choose **Free**.</span></span>
      * <span data-ttu-id="a51c7-192">En el menú desplegable **Tamaño de instancia** , seleccione el tamaño de instancia adecuado para el plan.</span><span class="sxs-lookup"><span data-stu-id="a51c7-192">In the the **Instance Size** drop-down menu, select the appropriate instance size for the plan.</span></span> <span data-ttu-id="a51c7-193">Con fines de prueba, puede elegir **Pequeño**.</span><span class="sxs-lookup"><span data-stu-id="a51c7-193">For testing purposes you can choose **Small**.</span></span>

   <span data-ttu-id="a51c7-194">i.</span><span class="sxs-lookup"><span data-stu-id="a51c7-194">i.</span></span> <span data-ttu-id="a51c7-195">Cuando haya completado todos los pasos anteriores, el cuadro de diálogo Nuevo contenedor de aplicaciones web debe parecerse al de la siguiente ilustración:</span><span class="sxs-lookup"><span data-stu-id="a51c7-195">Once you have completed all of the above steps, the New Web App Container dialog box should resemble the following illustration:</span></span>
      
      ![Cuadro de diálogo de implementación en nuevo contenedor de aplicación web][10]

   <span data-ttu-id="a51c7-197">j.</span><span class="sxs-lookup"><span data-stu-id="a51c7-197">j.</span></span> <span data-ttu-id="a51c7-198">Haga clic en **Aceptar** para finalizar la creación de su nuevo contenedor de aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="a51c7-198">Click **OK** to complete the creation of your new Web App container.</span></span>
       
      <span data-ttu-id="a51c7-199">Espere unos segundos para que se actualice la lista de los contenedores de aplicaciones web y el contenedor recién creado ya debería estar seleccionado en la lista.</span><span class="sxs-lookup"><span data-stu-id="a51c7-199">Wait a few seconds for the list of the Web App containers to be refreshed, and your newly-created web app container should now be selected in the list.</span></span>

7. <span data-ttu-id="a51c7-200">Ahora está listo para terminar la implementación inicial de la aplicación web en Azure:</span><span class="sxs-lookup"><span data-stu-id="a51c7-200">You are now ready to complete the initial deployment of your Web App to Azure:</span></span>
   
   ![Cuadro de diálogo de implementación en contenedor de Azure Web App][11]
   
   <span data-ttu-id="a51c7-202">Haga clic en **Aceptar** para implementar su aplicación Java en el contenedor de aplicaciones web seleccionado.</span><span class="sxs-lookup"><span data-stu-id="a51c7-202">Click **OK** to deploy your Java application to the selected Web App container.</span></span>
   
   <span data-ttu-id="a51c7-203">De forma predeterminada, la aplicación se implementará como un subdirectorio del servidor de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="a51c7-203">By default, your application will be deployed as a subdirectory of the application server.</span></span> <span data-ttu-id="a51c7-204">Si desea que se implemente como aplicación raíz, active la casilla **Deploy to root** (Implementar en raíz) antes de hacer clic en **OK** (Aceptar).</span><span class="sxs-lookup"><span data-stu-id="a51c7-204">If you want it to be deployed as the root application, check the **Deploy to root** checkbox before clicking **OK**.</span></span>

8. <span data-ttu-id="a51c7-205">A continuación, debería mostrarse la vista **Azure Activity Log** (Registro de actividad de Azure), que indicará el estado de implementación de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="a51c7-205">Next, you should see the **Azure Activity Log** view, which will indicate the deployment status of your Web App.</span></span>
   
   ![Azure Activity Log][12]
   
   <span data-ttu-id="a51c7-207">El proceso de implementación de la aplicación web en Azure debería tardar solo unos segundos en completarse.</span><span class="sxs-lookup"><span data-stu-id="a51c7-207">The process of deploying your Web App to Azure should take only a few seconds to complete.</span></span> <span data-ttu-id="a51c7-208">Cuando su aplicación esté lista, verá un vínculo denominado **Publicado** in the **Status** (Estado).</span><span class="sxs-lookup"><span data-stu-id="a51c7-208">When your application ready, you will see a link named **Published** in the **Status** column.</span></span> <span data-ttu-id="a51c7-209">Al hacer clic en el vínculo, irá a la página principal de la aplicación web implementada.</span><span class="sxs-lookup"><span data-stu-id="a51c7-209">When you click the link, it will take you to your deployed Web App's home page.</span></span>

## <a name="updating-your-web-app"></a><span data-ttu-id="a51c7-210">Actualización de la aplicación web</span><span class="sxs-lookup"><span data-stu-id="a51c7-210">Updating your web app</span></span>

<span data-ttu-id="a51c7-211">Actualizar una aplicación web de Azure existente es un proceso rápido y sencillo, y tiene dos opciones para ello:</span><span class="sxs-lookup"><span data-stu-id="a51c7-211">Updating an existing running Azure Web App is a quick and easy process, and you have two options for updating:</span></span>

* <span data-ttu-id="a51c7-212">Puede actualizar la implementación de una aplicación web de Java existente.</span><span class="sxs-lookup"><span data-stu-id="a51c7-212">You can update the deployment of an existing Java Web App.</span></span>
* <span data-ttu-id="a51c7-213">Puede publicar una aplicación Java adicional en el mismo contenedor de aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="a51c7-213">You can publish an additional Java application to the same Web App Container.</span></span>

<span data-ttu-id="a51c7-214">En cualquier caso, el proceso es idéntico y tarda unos pocos segundos:</span><span class="sxs-lookup"><span data-stu-id="a51c7-214">In either case, the process is identical and takes only a few seconds:</span></span>

1. <span data-ttu-id="a51c7-215">En el Explorador de proyectos de Eclipse, haga clic con el botón derecho en la aplicación Java que quiere actualizar o agregar a un contenedor de aplicaciones web existente.</span><span class="sxs-lookup"><span data-stu-id="a51c7-215">In the Eclipse project explorer, right-click the Java application you want to update or add to an existing Web App Container.</span></span>

2. <span data-ttu-id="a51c7-216">Cuando aparezca el menú contextual, seleccione **Azure** y, después, haga clic en **Publish as Azure Web App...** (Publicar como aplicación web de Azure).</span><span class="sxs-lookup"><span data-stu-id="a51c7-216">When the context menu appears, select **Azure** and then **Publish as Azure Web App...**</span></span>

3. <span data-ttu-id="a51c7-217">Puesto que ya ha iniciado sesión anteriormente, verá una lista de contenedores de aplicaciones web existentes.</span><span class="sxs-lookup"><span data-stu-id="a51c7-217">Since you have already logged in previously, you will see a list of your existing Web App containers.</span></span> <span data-ttu-id="a51c7-218">Seleccione aquel en el que quiere publicar o volver a publicar la aplicación Java y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="a51c7-218">Select the one you want to publish or re-publish your Java application to and click **OK**.</span></span>

<span data-ttu-id="a51c7-219">Unos segundos más tarde, la vista **Azure Activity Log** (Registro de actividad de Azure) mostrará la implementación actualizada como **Published** (Publicado) y podrá comprobar la aplicación actualizada en un explorador web.</span><span class="sxs-lookup"><span data-stu-id="a51c7-219">A few seconds later, the **Azure Activity Log** view will show your updated deployment as **Published** and you will be able to verify your updated application in a web browser.</span></span>

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a><span data-ttu-id="a51c7-220">Inicio, detención o reinicio de una aplicación web existente</span><span class="sxs-lookup"><span data-stu-id="a51c7-220">Starting, stopping, or restarting an existing web app</span></span>

<span data-ttu-id="a51c7-221">Para iniciar o detener un contenedor de aplicaciones web existente (junto con todas las aplicaciones Java implementadas en él), puede utilizar la vista **Azure Explorer** (Explorador de Azure).</span><span class="sxs-lookup"><span data-stu-id="a51c7-221">To start or stop an existing Azure Web App container, (including all the deployed Java applications in it), you can use the **Azure Explorer** view.</span></span>

<span data-ttu-id="a51c7-222">Si la vista **Azure Explorer** (Explorador de Azure) no está abierta, puede abrirla; para ello, haga clic en el menú **Window** (Ventana) en Eclipse, luego en **Show View** (Mostrar vista), **Other...** (Otra), **Azure** y, finalmente, en **Azure Explorer (Explorador de Azure)**.</span><span class="sxs-lookup"><span data-stu-id="a51c7-222">If the **Azure Explorer** view is not already open, you can open it by clicking then **Window** menu in Eclipse, then click **Show View**, then **Other...**, then **Azure**, and then click **Azure Explorer**.</span></span> <span data-ttu-id="a51c7-223">Si anteriormente no ha iniciado sesión, se le pedirá que lo haga.</span><span class="sxs-lookup"><span data-stu-id="a51c7-223">If you have not previously logged in, it will prompt you to do so.</span></span>

<span data-ttu-id="a51c7-224">Cuando se muestre la vista **Azure Explorer** (Explorador de Azure), siga estos pasos para iniciar o detener su aplicación web:</span><span class="sxs-lookup"><span data-stu-id="a51c7-224">When the **Azure Explorer** view is displayed, use follow these steps to start or stop your Web App:</span></span> 

1. <span data-ttu-id="a51c7-225">Expanda el nodo **Azure** .</span><span class="sxs-lookup"><span data-stu-id="a51c7-225">Expand the **Azure** node.</span></span>

2. <span data-ttu-id="a51c7-226">Expanda el nodo **Web Apps** .</span><span class="sxs-lookup"><span data-stu-id="a51c7-226">Expand the **Web Apps** node.</span></span> 

3. <span data-ttu-id="a51c7-227">Haga clic en la aplicación web deseada.</span><span class="sxs-lookup"><span data-stu-id="a51c7-227">Right-click the desired Web App.</span></span>

4. <span data-ttu-id="a51c7-228">Cuando aparezca el menú contextual, haga clic en **Iniciar**, **Detener** o **Reiniciar**.</span><span class="sxs-lookup"><span data-stu-id="a51c7-228">When the context menu appears, click **Start**, **Stop**, or **Restart**.</span></span> <span data-ttu-id="a51c7-229">Tenga en cuenta que las opciones de menú dependen del contexto, por lo que solo podrá detener una aplicación web que se encuentre en ejecución o iniciar una aplicación web que no se esté ejecutando en ese momento.</span><span class="sxs-lookup"><span data-stu-id="a51c7-229">Note that the menu choices are context-aware, so you can only stop a running web app or start a web app which is not currently running.</span></span>
   
   ![Detención de una aplicación web existente][13]

## <a name="next-steps"></a><span data-ttu-id="a51c7-231">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a51c7-231">Next steps</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<span data-ttu-id="a51c7-232">Para obtener más información sobre cómo crear Azure Web Apps, consulte [Introducción a Web Apps].</span><span class="sxs-lookup"><span data-stu-id="a51c7-232">For additional information about creating Azure Web Apps, see the [Web Apps Overview].</span></span>

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
