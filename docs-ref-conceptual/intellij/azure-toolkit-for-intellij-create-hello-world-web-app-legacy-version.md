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
ms.openlocfilehash: ebe98a604b52dc9a4b5a47cbf65a4c68a5c86fe3
ms.sourcegitcommit: 151aaa6ccc64d94ed67f03e846bab953bde15b4a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/03/2018
ms.locfileid: "28954786"
---
# <a name="create-a-hello-world-web-app-for-azure-using-the-legacy-toolkit-for-intellij"></a><span data-ttu-id="07130-103">Creación de una aplicación web Hello World para Azure con el kit de herramientas heredado para IntelliJ</span><span class="sxs-lookup"><span data-stu-id="07130-103">Create a Hello World web app for Azure using the legacy toolkit for IntelliJ</span></span>

<span data-ttu-id="07130-104">En este tutorial se muestra cómo crear e implementar una aplicación básica Hola mundo en Azure como una aplicación web mediante la versión 3.0.6 (o versiones anteriores) del [Kit de herramientas de Azure para IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="07130-104">This tutorial shows how to create and deploy a basic Hello World application to Azure as a web app by using version 3.0.6 (or earlier) of the [Azure Toolkit for IntelliJ].</span></span>

> [!NOTE]
>
> <span data-ttu-id="07130-105">Para ver la versión de este artículo que usa el [Kit de herramientas de Azure para Eclipse], consulte [Creación de una aplicación web Hello World para Azure mediante Eclipse][eclipse-hello-world].</span><span class="sxs-lookup"><span data-stu-id="07130-105">For a version of this article that uses the [Azure Toolkit for Eclipse], see [Create a Hello World web app for Azure using Eclipse][eclipse-hello-world].</span></span>
>

> [!IMPORTANT]
> 
> <span data-ttu-id="07130-106">El Kit de herramientas de Azure para IntelliJ se actualizó en agosto de 2017, con un flujo de trabajo diferente.</span><span class="sxs-lookup"><span data-stu-id="07130-106">The Azure Toolkit for IntelliJ was updated in August 2017 with a different workflow.</span></span> <span data-ttu-id="07130-107">En este artículo se muestra la creación de una aplicación web Hello World con la versión 3.0.6 (o posterior) del Kit de herramientas de Azure para IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="07130-107">This article illustrates creating a Hello World web app by using version 3.0.6 (or earlier) of the Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="07130-108">Si está usando la versión 3.0.7 (o posterior) del Kit de herramientas, debe seguir los pasos descritos en [Creación de una aplicación web Hello World de Azure en IntelliJ][Updated Version].</span><span class="sxs-lookup"><span data-stu-id="07130-108">If you are using the version 3.0.7 (or later) of the toolkit, you will need to follow the steps in [Create a Hello World web app for Azure in IntelliJ][Updated Version].</span></span>
>

<span data-ttu-id="07130-109">Cuando haya completado este tutorial, la aplicación se parecerá a la que se muestra en la siguiente ilustración al verla en un explorador web:</span><span class="sxs-lookup"><span data-stu-id="07130-109">When you have completed this tutorial, your application will look similar to the following illustration when you view it in a web browser:</span></span>

![Versión preliminar de la aplicación Hello World][01]

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="create-a-new-web-app-project"></a><span data-ttu-id="07130-111">Creación de un proyecto de aplicación web nuevo</span><span class="sxs-lookup"><span data-stu-id="07130-111">Create a new web app project</span></span>

1. <span data-ttu-id="07130-112">Inicie IntelliJ e inicie sesión en su cuenta de Azure siguiendo las instrucciones del artículo [Instrucciones de inicio de sesión del kit de herramientas de Azure para IntelliJ][intelliJ-sign-in-instructions].</span><span class="sxs-lookup"><span data-stu-id="07130-112">Start IntelliJ, and sign into your Azure account by using the instructions in the [Azure Sign In Instructions for the Azure Toolkit for IntelliJ][intelliJ-sign-in-instructions] article.</span></span>

1. <span data-ttu-id="07130-113">Haga clic en el menú **File** (Archivo), luego en **New** (Nuevo) y, finalmente, en **Project** (Proyecto).</span><span class="sxs-lookup"><span data-stu-id="07130-113">Click the **File** menu, then click **New**, and then click **Project**.</span></span>
   
   ![Archivo Nuevo Proyecto][02]

2. <span data-ttu-id="07130-115">En el cuadro de diálogo **New Project** (Nuevo proyecto), seleccione **Java** y **Web Application** (Aplicación web) y, después, haga clic en **New** (Nuevo) para agregar un SDK del proyecto.</span><span class="sxs-lookup"><span data-stu-id="07130-115">In the **New Project** dialog box, select **Java**, then **Web Application**, and then click **New** to add a Project SDK.</span></span>
   
   ![Cuadro de diálogo Nuevo proyecto][03a]
   
3. <span data-ttu-id="07130-117">En el cuadro de diálogo Select Home Directory for JDK (Seleccionar directorio de inicio para JDK), seleccione la carpeta donde está instalado el JDK y, después, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="07130-117">In the Select Home Directory for JDK dialog box, select the folder where your JDK is installed, and then click **OK**.</span></span> <span data-ttu-id="07130-118">Haga clic en **Siguiente** en el cuadro de diálogo de nuevo proyecto para continuar.</span><span class="sxs-lookup"><span data-stu-id="07130-118">Click **Next** in the New Project dialog box to continue.</span></span>
   
   ![Especificación del directorio de inicio de JDK][03b]

4. <span data-ttu-id="07130-120">Para este tutorial, asigne al proyecto el nombre **Java-Web-App-On-Azure** y haga clic en **Finish** (Finalizar).</span><span class="sxs-lookup"><span data-stu-id="07130-120">For purposes of this tutorial, name the project **Java-Web-App-On-Azure**, and then click **Finish**.</span></span>
   
   ![Cuadro de diálogo Nuevo proyecto][04]

5. <span data-ttu-id="07130-122">En la vista del explorador de proyectos de IntelliJ, expanda **Java-Web-App-On-Azure**, después expanda **web** y, luego, haga doble clic en **index.jsp**.</span><span class="sxs-lookup"><span data-stu-id="07130-122">Within IntelliJ's Project Explorer view, expand **Java-Web-App-On-Azure**, then expand **web**, and then double-click **index.jsp**.</span></span>
   
   ![Abrir página de índice][05c]

6. <span data-ttu-id="07130-124">Cuando el archivo index.jsp se abra en IntelliJ, agregue texto para que se muestre dinámicamente **Hello World!**</span><span class="sxs-lookup"><span data-stu-id="07130-124">When your index.jsp file opens in IntelliJ, add in text to dynamically display **Hello World!**</span></span> <span data-ttu-id="07130-125">dentro del elemento `<body>` existente.</span><span class="sxs-lookup"><span data-stu-id="07130-125">within the existing `<body>` element.</span></span> <span data-ttu-id="07130-126">El contenido de `<body>` actualizado debe parecerse al siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="07130-126">Your updated `<body>` content should resemble the following example:</span></span>
   
   ```java
   <body><b><% out.println("Hello World!"); %></b></body>
   ```

7. <span data-ttu-id="07130-127">Guarde el archivo index.jsp.</span><span class="sxs-lookup"><span data-stu-id="07130-127">Save index.jsp.</span></span>

## <a name="deploy-your-web-app-to-azure"></a><span data-ttu-id="07130-128">Implementación de una aplicación web en Azure</span><span class="sxs-lookup"><span data-stu-id="07130-128">Deploy your web app to Azure</span></span>

<span data-ttu-id="07130-129">Existen varias maneras de implementar una aplicación web de Java en Azure.</span><span class="sxs-lookup"><span data-stu-id="07130-129">There are several ways by which you can deploy a Java web app to Azure.</span></span> <span data-ttu-id="07130-130">En este tutorial se describe una de las más sencillas: la aplicación se implementará en un contenedor de aplicaciones de Azure: no se necesita ningún tipo de proyecto especial ni herramientas adicionales.</span><span class="sxs-lookup"><span data-stu-id="07130-130">This tutorial describes one of the simplest: your application will be deployed to an Azure Web App Container - no special project type nor additional tools are needed.</span></span> <span data-ttu-id="07130-131">Azure facilitará el JDK y el software de contenedor web, así que no es necesario que cargue los suyos; lo único que necesita es su aplicación web de Java.</span><span class="sxs-lookup"><span data-stu-id="07130-131">The JDK and the web container software will be provided for you by Azure, so there is no need to upload your own; all you need is your Java Web App.</span></span> <span data-ttu-id="07130-132">Como resultado, el proceso de publicación de su aplicación tardará unos segundos y no minutos.</span><span class="sxs-lookup"><span data-stu-id="07130-132">As a result, the publishing process for your application will take seconds, not minutes.</span></span>

<span data-ttu-id="07130-133">Antes de publicar la aplicación, primero debe configurar el módulo.</span><span class="sxs-lookup"><span data-stu-id="07130-133">Before you publish your application, you first need to configure your module settings.</span></span> <span data-ttu-id="07130-134">Para ello, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="07130-134">To do so, use the following steps:</span></span>

1. <span data-ttu-id="07130-135">En el Explorador de proyectos de IntelliJ, haga clic con el botón derecho en el proyecto **Java-Web-App-On-Azure** .</span><span class="sxs-lookup"><span data-stu-id="07130-135">In IntelliJ's Project Explorer, right-click the **Java-Web-App-On-Azure** project.</span></span> <span data-ttu-id="07130-136">Cuando aparezca el menú contextual, haga clic en **Open Module Settings** (Abrir configuración del módulo).</span><span class="sxs-lookup"><span data-stu-id="07130-136">When the context menu appears, click **Open Module Settings**.</span></span>

   ![Abrir configuración del módulo][05a]

2. <span data-ttu-id="07130-138">Cuando se muestre el cuadro de diálogo Project Structure (Estructura de proyecto):</span><span class="sxs-lookup"><span data-stu-id="07130-138">When the Project Structure dialog box appears:</span></span>

   <span data-ttu-id="07130-139">a.</span><span class="sxs-lookup"><span data-stu-id="07130-139">a.</span></span> <span data-ttu-id="07130-140">Haga clic en **Artefactos** en la lista de **configuración del proyecto**.</span><span class="sxs-lookup"><span data-stu-id="07130-140">Click **Artifacts** in the list of **Project Settings**.</span></span>

   <span data-ttu-id="07130-141">b.</span><span class="sxs-lookup"><span data-stu-id="07130-141">b.</span></span> <span data-ttu-id="07130-142">Cambie el nombre del artefacto en el cuadro **Nombre** para que contenga un espacio en blanco o caracteres especiales; esto es necesario porque el nombre se usará en el identificador uniforme de recursos (URI).</span><span class="sxs-lookup"><span data-stu-id="07130-142">Change the artifact name in the **Name** box so that it doesn't contain whitespace or special characters; this is necessary since the name will be used in the Uniform Resource Identifier (URI).</span></span>

   <span data-ttu-id="07130-143">c.</span><span class="sxs-lookup"><span data-stu-id="07130-143">c.</span></span> <span data-ttu-id="07130-144">Cambiar el **tipo** a **Aplicación Web: archivo**.</span><span class="sxs-lookup"><span data-stu-id="07130-144">Change the **Type** to **Web Application: Archive**.</span></span>

   <span data-ttu-id="07130-145">d.</span><span class="sxs-lookup"><span data-stu-id="07130-145">d.</span></span> <span data-ttu-id="07130-146">Haga clic en **OK** (Aceptar) para cerrar el cuadro de diálogo Project Structure (Estructura del proyecto).</span><span class="sxs-lookup"><span data-stu-id="07130-146">Click **OK** to close the Project Structure dialog box.</span></span>

   ![Abrir configuración del módulo][05b]

<span data-ttu-id="07130-148">Cuando se ha configurado el módulo, puede publicar la aplicación en Azure mediante los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="07130-148">When you have configured your module settings, you can publish your application to Azure by using the following steps:</span></span>

1. <span data-ttu-id="07130-149">En el Explorador de proyectos de IntelliJ, haga clic con el botón derecho en el proyecto **Java-Web-App-On-Azure** .</span><span class="sxs-lookup"><span data-stu-id="07130-149">In IntelliJ's Project Explorer, right-click the **Java-Web-App-On-Azure** project.</span></span> <span data-ttu-id="07130-150">Cuando aparezca el menú contextual, seleccione **Azure** y, después, haga clic en **Publish as Azure Web App...** (Publicar como aplicación web de Azure)</span><span class="sxs-lookup"><span data-stu-id="07130-150">When the context menu appears, select **Azure**, and then click **Publish as Azure Web App...**</span></span>
   
   ![Menú contextual de publicación de Azure][06]

2. <span data-ttu-id="07130-152">Si aún no ha iniciado sesión en Azure desde IntelliJ, se le pedirá que lo haga.</span><span class="sxs-lookup"><span data-stu-id="07130-152">If you have not already signed in to Azure from IntelliJ, you will be prompted to sign in to your Azure account.</span></span> <span data-ttu-id="07130-153">(Si tiene varias cuentas de Azure, puede que algunos de los avisos que aparecen durante el proceso de inicio de sesión se muestren más de una vez, incluso si parecen iguales.</span><span class="sxs-lookup"><span data-stu-id="07130-153">(If you have multiple Azure accounts, some of the prompts during the sign-in process may be shown more than once, even if they appear to be the same.</span></span> <span data-ttu-id="07130-154">Cuando esto ocurra, siga la instrucciones de inicio de sesión).</span><span class="sxs-lookup"><span data-stu-id="07130-154">When this happens, continue to follow the sign-in instructions.)</span></span>
   
   ![Cuadro de diálogo de inicio de sesión de Azure][07]

3. <span data-ttu-id="07130-156">Cuando haya iniciado sesión correctamente en su cuenta de Azure, el cuadro de diálogo **Administrar suscripciones** mostrará una lista de suscripciones asociadas a sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="07130-156">After you have successfully signed in to your Azure account, the **Manage Subscriptions** dialog box will display a list of subscriptions that are associated with your credentials.</span></span> <span data-ttu-id="07130-157">Si aparecen varias suscripciones y quiere trabajar solo con un subconjunto específico de ellas, opcionalmente puede desactivar las que no utilice. Cuando haya seleccionado las suscripciones, haga clic en **Cerrar**.</span><span class="sxs-lookup"><span data-stu-id="07130-157">(If there are multiple subscriptions listed and you want to work with only a specific subset of them, you may optionally uncheck the subscriptions you don't want to use.) When you have selected your subscriptions, click **Close**.</span></span>
   
   ![Administrar suscripciones][08]

4. <span data-ttu-id="07130-159">Cuando aparezca el cuadro de diálogo **Deploy to Azure Web App Container** (Implementar en el contenedor de aplicaciones web de Azure), se mostrarán los contenedores de aplicaciones web creados anteriormente; si no ha creado ningún contenedor, la lista estará vacía.</span><span class="sxs-lookup"><span data-stu-id="07130-159">When the **Deploy to Azure Web App Container** dialog box appears, it will display any Web App containers that you have previously created; if you have not created any containers, the list will be empty.</span></span>
   
   ![Contenedores de aplicaciones][09]

5. <span data-ttu-id="07130-161">Si no ha creado un contenedor de aplicaciones web de Azure antes, o si quiere publicar la aplicación en un nuevo contenedor, siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="07130-161">If you have not created an Azure Web App Container before, or if you would like to publish your application to a new container, use the following steps.</span></span> <span data-ttu-id="07130-162">De lo contrario, seleccione un contenedor de aplicaciones web existente y vaya al paso 6 que encontrará a continuación.</span><span class="sxs-lookup"><span data-stu-id="07130-162">Otherwise, select an existing Web App Container and skip to step 6 below.</span></span>
   
   <span data-ttu-id="07130-163">a.</span><span class="sxs-lookup"><span data-stu-id="07130-163">a.</span></span> <span data-ttu-id="07130-164">Haga clic en el signo **+**.</span><span class="sxs-lookup"><span data-stu-id="07130-164">Click the **+** sign.</span></span>
      
      ![Agregar contenedor de aplicaciones][10]

   <span data-ttu-id="07130-166">b.</span><span class="sxs-lookup"><span data-stu-id="07130-166">b.</span></span> <span data-ttu-id="07130-167">Se mostrará el cuadro de diálogo **New Web App Container** (Nuevo contenedor de aplicaciones web), que se usará para los siguientes pasos.</span><span class="sxs-lookup"><span data-stu-id="07130-167">The **New Web App Container** dialog box will be displayed, which will be used for the next several steps.</span></span>
      
      ![Nuevo contenedor de aplicaciones][11a]
   
   <span data-ttu-id="07130-169">c.</span><span class="sxs-lookup"><span data-stu-id="07130-169">c.</span></span> <span data-ttu-id="07130-170">Escriba un valor para **Etiqueta DNS** para el contenedor de aplicaciones web; esta será la etiqueta DNS hoja de la dirección URL del host de la aplicación web en Azure.</span><span class="sxs-lookup"><span data-stu-id="07130-170">Enter a **DNS Label** for your Web App Container; this will form the leaf DNS label of the host URL for your web application in Azure.</span></span> <span data-ttu-id="07130-171">Tenga en cuenta que el nombre debe estar disponible y se ajusta a los requisitos de nomenclatura de las aplicaciones web de Azure.</span><span class="sxs-lookup"><span data-stu-id="07130-171">Note that the name must be available and conform to Azure Web App naming requirements.</span></span>

   <span data-ttu-id="07130-172">d.</span><span class="sxs-lookup"><span data-stu-id="07130-172">d.</span></span> <span data-ttu-id="07130-173">En el menú desplegable **Web Container** (Contenedor web), seleccione el software adecuado para su aplicación.</span><span class="sxs-lookup"><span data-stu-id="07130-173">In the **Web Container** drop-down menu, select the appropriate software for your application.</span></span>
      
      <span data-ttu-id="07130-174">Actualmente, puede elegir entre Tomcat 8, Tomcat 7 o Jetty 9.</span><span class="sxs-lookup"><span data-stu-id="07130-174">Currently, you can choose from Tomcat 8, Tomcat 7 or Jetty 9.</span></span> <span data-ttu-id="07130-175">Azure proporcionará una distribución reciente del software seleccionado y se ejecutará en una distribución reciente de JDK 8 creada por Oracle y proporcionada por Azure.</span><span class="sxs-lookup"><span data-stu-id="07130-175">A recent distribution of the selected software will be provided by Azure, and it will run on a recent distribution of JDK 8 created by Oracle and provided by Azure.</span></span>

   <span data-ttu-id="07130-176">e.</span><span class="sxs-lookup"><span data-stu-id="07130-176">e.</span></span> <span data-ttu-id="07130-177">En el menú desplegable **Suscripción** , seleccione la suscripción que quiere usar para esta implementación.</span><span class="sxs-lookup"><span data-stu-id="07130-177">In the **Subscription** drop-down menu, select the subscription you want to use for this deployment.</span></span>

   <span data-ttu-id="07130-178">f.</span><span class="sxs-lookup"><span data-stu-id="07130-178">f.</span></span> <span data-ttu-id="07130-179">En el menú desplegable **Grupo de recursos** , seleccione el grupo de recursos con el que desea asociar la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="07130-179">In the **Resource Group** drop-down menu, select the Resource Group with which you want to associate your Web App.</span></span> <span data-ttu-id="07130-180">Los grupos de recursos de Azure permiten agrupar recursos relacionados para que, por ejemplo, se puedan eliminar juntos.</span><span class="sxs-lookup"><span data-stu-id="07130-180">(Azure Resource Groups allow you to group related resources together so that, for example, they can be deleted together.)</span></span>
      
      <span data-ttu-id="07130-181">Puede seleccionar un grupo de recursos existente (si tiene alguno) y pasar al paso g a continuación o usar los siguientes pasos para crear un nuevo grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="07130-181">You can select an existing Resource Group (if you have any) and skip to step g below, or use the following steps to create a new Resource Group:</span></span>
      
      * <span data-ttu-id="07130-182">Seleccione **&lt;&lt; Crear nuevo grupo de recursos&gt;&gt;** en el menú desplegable **Grupo de recursos**.</span><span class="sxs-lookup"><span data-stu-id="07130-182">Select **&lt;&lt; Create new Resource Group &gt;&gt;** in the **Resource Group** drop-down menu.</span></span>
      * <span data-ttu-id="07130-183">Se muestra el cuadro de diálogo **Nuevo grupo de recursos** :</span><span class="sxs-lookup"><span data-stu-id="07130-183">The **New Resource Group** dialog box will be displayed:</span></span>
        
         ![Nuevo grupo de recursos][12]

      * <span data-ttu-id="07130-185">En el cuadro de texto **Nombre**, especifique un nombre para el nuevo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="07130-185">In the **Name** textbox, specify a name for your new Resource Group.</span></span>
      * <span data-ttu-id="07130-186">En el menú desplegable **Región**, seleccione la ubicación adecuada del centro de datos de Azure para el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="07130-186">In the **Region** drop-down menu, select the appropriate Azure data center location for your Resource Group.</span></span>
      * <span data-ttu-id="07130-187">Haga clic en **OK**.</span><span class="sxs-lookup"><span data-stu-id="07130-187">Click **OK**.</span></span>

   <span data-ttu-id="07130-188">g.</span><span class="sxs-lookup"><span data-stu-id="07130-188">g.</span></span> <span data-ttu-id="07130-189">En el menú desplegable **Plan de App Service** se muestran los planes de App Service que están asociados con el grupo de recursos seleccionado.</span><span class="sxs-lookup"><span data-stu-id="07130-189">The **App Service Plan** drop-down menu lists the app service plans that are associated with the Resource Group that you selected.</span></span> <span data-ttu-id="07130-190">(Un plan de App Service especifica información como la ubicación de la aplicación web, el plan de tarifa y el tamaño de la instancia de proceso.</span><span class="sxs-lookup"><span data-stu-id="07130-190">(An App Service Plan specifies information such as the location of your Web App, the pricing tier and the compute instance size.</span></span> <span data-ttu-id="07130-191">Un único plan de App Service se puede usar para varias Web Apps, motivo por el cual se mantiene independiente de una implementación específica de Web Apps.)</span><span class="sxs-lookup"><span data-stu-id="07130-191">A single App Service Plan can be used for multiple Web Apps, which is why it is maintained separately from a specific Web App deployment.)</span></span>
      
      <span data-ttu-id="07130-192">Puede seleccionar un plan de plan de App Service existente (si tiene alguno) y pasar al paso h a continuación o usar los siguientes pasos para crear un nuevo plan:</span><span class="sxs-lookup"><span data-stu-id="07130-192">You can select an existing App Service Plan (if you have any) and skip to step h below, or use the following steps to create a new App Service Plan:</span></span>
      
      * <span data-ttu-id="07130-193">Seleccione **&lt;&lt; Crear nuevo plan de App Service&gt;&gt;** en el menú desplegable **Plan de App Service**.</span><span class="sxs-lookup"><span data-stu-id="07130-193">Select **&lt;&lt; Create new App Service Plan &gt;&gt;** in the **App Service Plan** drop-down menu.</span></span>
      * <span data-ttu-id="07130-194">Se muestra el cuadro de diálogo **Nuevo plan de App Service** :</span><span class="sxs-lookup"><span data-stu-id="07130-194">The **New App Service Plan** dialog box will be displayed:</span></span>
        
         ![Nuevo plan de App Service][13]

      * <span data-ttu-id="07130-196">En el cuadro de texto **Nombre**, especifique un nombre para el nuevo plan de App Service.</span><span class="sxs-lookup"><span data-stu-id="07130-196">In the **Name** textbox, specify a name for your new App Service Plan.</span></span>
      * <span data-ttu-id="07130-197">En el menú desplegable **Ubicación**, seleccione la ubicación adecuada del centro de datos de Azure para el plan.</span><span class="sxs-lookup"><span data-stu-id="07130-197">In the **Location** drop-down menu, select the appropriate Azure data center location for the plan.</span></span>
      * <span data-ttu-id="07130-198">En el menú desplegable **Plan de tarifa**, seleccione la tarifa adecuada para el plan.</span><span class="sxs-lookup"><span data-stu-id="07130-198">In the **Pricing Tier** drop-down menu, select the appropriate pricing for the plan.</span></span> <span data-ttu-id="07130-199">Con fines de prueba, puede elegir **Gratis**.</span><span class="sxs-lookup"><span data-stu-id="07130-199">For testing purposes you can choose **Free**.</span></span>
      * <span data-ttu-id="07130-200">En el menú desplegable **Tamaño de instancia**, seleccione el tamaño de instancia adecuado para el plan.</span><span class="sxs-lookup"><span data-stu-id="07130-200">In the **Instance Size** drop-down menu, select the appropriate instance size for the plan.</span></span> <span data-ttu-id="07130-201">Con fines de prueba, puede elegir **Pequeño**.</span><span class="sxs-lookup"><span data-stu-id="07130-201">For testing purposes you can choose **Small**.</span></span>
      * <span data-ttu-id="07130-202">Haga clic en **OK**.</span><span class="sxs-lookup"><span data-stu-id="07130-202">Click **OK**.</span></span>

   <span data-ttu-id="07130-203">h.</span><span class="sxs-lookup"><span data-stu-id="07130-203">h.</span></span> <span data-ttu-id="07130-204">(Opcional) De manera predeterminada, Azure implementará automáticamente una distribución reciente de Java 8 como máquina virtual de Java en el contenedor de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="07130-204">(Optional) By default, a recent distribution of Java 8 will be automatically deployed as your JVM by Azure to your web app container.</span></span> <span data-ttu-id="07130-205">Sin embargo, puede seleccionar una versión y una distribución diferentes de la máquina virtual de Java.</span><span class="sxs-lookup"><span data-stu-id="07130-205">However, you can select a different version and distribution of the JVM.</span></span> <span data-ttu-id="07130-206">Para ello, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="07130-206">To do so, use the following steps:</span></span>
      
      * <span data-ttu-id="07130-207">Haga clic en la pestaña **JDK** en el cuadro de diálogo **New Web App Container** (Nuevo contenedor de aplicaciones web).</span><span class="sxs-lookup"><span data-stu-id="07130-207">Click the **JDK** tab in the **New Web App Container** dialog box.</span></span>
      * <span data-ttu-id="07130-208">Puede elegir una de las siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="07130-208">You can choose from one of the following options:</span></span>
        
         * <span data-ttu-id="07130-209">Implementar el JDK predeterminado que ofrece Azure</span><span class="sxs-lookup"><span data-stu-id="07130-209">Deploy the default JDK which is offered by Azure</span></span>
         * <span data-ttu-id="07130-210">Implementar un JDK de terceros de lista desplegable de JDK adicionales que están disponibles en Azure</span><span class="sxs-lookup"><span data-stu-id="07130-210">Deploy a 3rd party JDK from a drop-down list of additional JDKs which are available on Azure</span></span>
         * <span data-ttu-id="07130-211">Implementar un JDK personalizado, que debe estar empaquetado en un archivo ZIP y bien estar disponible públicamente o en su cuenta de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="07130-211">Deploy a custom JDK, which must be packaged as a ZIP file and either publicly available or in your Azure storage account</span></span>
        
      ![Pestaña JDK de nuevo contenedor de aplicaciones][11b]

   <span data-ttu-id="07130-213">i.</span><span class="sxs-lookup"><span data-stu-id="07130-213">i.</span></span> <span data-ttu-id="07130-214">Cuando haya completado todos los pasos anteriores, el cuadro de diálogo Nuevo contenedor de aplicaciones web debe parecerse al de la siguiente ilustración:</span><span class="sxs-lookup"><span data-stu-id="07130-214">Once you have completed all of the above steps, the New Web App Container dialog box should resemble the following illustration:</span></span>
      
      ![Nuevo contenedor de aplicaciones][14]
   
   <span data-ttu-id="07130-216">j.</span><span class="sxs-lookup"><span data-stu-id="07130-216">j.</span></span> <span data-ttu-id="07130-217">Haga clic en **Aceptar** para finalizar la creación de su nuevo contenedor de aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="07130-217">Click **OK** to complete the creation of your new Web App container.</span></span>
       
      <span data-ttu-id="07130-218">Espere unos segundos para que se actualice la lista de los contenedores de aplicaciones web y el contenedor recién creado ya debería estar seleccionado en la lista.</span><span class="sxs-lookup"><span data-stu-id="07130-218">Wait a few seconds for the list of the Web App containers to be refreshed, and your newly-created web app container should now be selected in the list.</span></span>

6. <span data-ttu-id="07130-219">Ya puede completar la implementación inicial de su aplicación web en Azure; haga clic en **Aceptar** para implementar la aplicación de Java en el contenedor de aplicación web seleccionado.</span><span class="sxs-lookup"><span data-stu-id="07130-219">You are now ready to complete the initial deployment of your Web App to Azure; click **OK** to deploy your Java application to the selected Web App container.</span></span> <span data-ttu-id="07130-220">De forma predeterminada, la aplicación se implementará como un subdirectorio del servidor de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="07130-220">By default, your application will be deployed as a subdirectory of the application server.</span></span> <span data-ttu-id="07130-221">Si desea que se implemente como aplicación raíz, active la casilla **Deploy to root** (Implementar en raíz) antes de hacer clic en **OK** (Aceptar).</span><span class="sxs-lookup"><span data-stu-id="07130-221">If you want it to be deployed as the root application, check the **Deploy to root** checkbox before clicking **OK**.</span></span>
   
   ![Implementar en Azure][15]

7. <span data-ttu-id="07130-223">A continuación, debería mostrarse la vista **Azure Activity Log** (Registro de actividad de Azure), que indicará el estado de implementación de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="07130-223">Next, you should see the **Azure Activity Log** view, which will indicate the deployment status of your Web App.</span></span>
   
   ![Indicador de progreso][16]
   
   <span data-ttu-id="07130-225">El proceso de implementación de la aplicación web en Azure debería tardar solo unos segundos en completarse.</span><span class="sxs-lookup"><span data-stu-id="07130-225">The process of deploying your Web App to Azure should take only a few seconds to complete.</span></span> <span data-ttu-id="07130-226">Cuando la aplicación esté lista, verá un vínculo denominado **Publicado** en la columna **Estado**.</span><span class="sxs-lookup"><span data-stu-id="07130-226">When your application is ready, you will see a link named **Published** in the **Status** column.</span></span> <span data-ttu-id="07130-227">Al hacer clic en el vínculo, se le llevará a la página principal de la aplicación web implementada. Por otro lado, puede utilizar los pasos de la sección siguiente para ir a la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="07130-227">When you click the link, it will take you to your deployed Web App's home page, or you can use the steps in the following section to browse to your web app.</span></span>

## <a name="browsing-to-your-web-app-on-azure"></a><span data-ttu-id="07130-228">Desplazamiento hasta su aplicación web en Azure</span><span class="sxs-lookup"><span data-stu-id="07130-228">Browsing to your Web App on Azure</span></span>

<span data-ttu-id="07130-229">Para ir a su aplicación web en Azure, puede usar la vista **Azure Explorer**.</span><span class="sxs-lookup"><span data-stu-id="07130-229">To browse to your Web App on Azure, you can use the **Azure Explorer** view.</span></span>

<span data-ttu-id="07130-230">Si la vista del **Explorador de Azure** no está abierta, puede abrirla haciendo clic en el menú **View** (Ver) de IntelliJ, luego haga clic en **Tool Windows** (Ventanas de herramientas) y, después, en **Service Explorer** (Explorador de servicios).</span><span class="sxs-lookup"><span data-stu-id="07130-230">If the **Azure Explorer** view is not already open, you can open it by clicking then **View** menu in IntelliJ, then click **Tool Windows**, and then click **Service Explorer**.</span></span> <span data-ttu-id="07130-231">Si anteriormente no ha iniciado sesión, se le pedirá que lo haga.</span><span class="sxs-lookup"><span data-stu-id="07130-231">If you have not previously logged in, it will prompt you to do so.</span></span>

<span data-ttu-id="07130-232">Cuando se muestre la vista **Azure Explorer** (Explorador de Azure), siga estos pasos para buscar la aplicación web:</span><span class="sxs-lookup"><span data-stu-id="07130-232">When the **Azure Explorer** view is displayed, follow these steps to browse to your Web App:</span></span> 

1. <span data-ttu-id="07130-233">Expanda el nodo **Azure** .</span><span class="sxs-lookup"><span data-stu-id="07130-233">Expand the **Azure** node.</span></span>
2. <span data-ttu-id="07130-234">Expanda el nodo **Web Apps** .</span><span class="sxs-lookup"><span data-stu-id="07130-234">Expand the **Web Apps** node.</span></span> 
3. <span data-ttu-id="07130-235">Haga clic en la aplicación web deseada.</span><span class="sxs-lookup"><span data-stu-id="07130-235">Right-click the desired Web App.</span></span>
4. <span data-ttu-id="07130-236">Cuando aparezca el menú contextual, haga clic en **Abrir en el explorador**.</span><span class="sxs-lookup"><span data-stu-id="07130-236">When the context menu appears, click **Open in Browser**.</span></span>
   
   ![Examinar una aplicación web][17]

## <a name="updating-your-web-app"></a><span data-ttu-id="07130-238">Actualización de la aplicación web</span><span class="sxs-lookup"><span data-stu-id="07130-238">Updating your web app</span></span>

<span data-ttu-id="07130-239">Actualizar una aplicación web de Azure existente es un proceso rápido y sencillo, y tiene dos opciones para ello:</span><span class="sxs-lookup"><span data-stu-id="07130-239">Updating an existing running Azure Web App is a quick and easy process, and you have two options for updating:</span></span>

* <span data-ttu-id="07130-240">Puede actualizar la implementación de una aplicación web de Java existente.</span><span class="sxs-lookup"><span data-stu-id="07130-240">You can update the deployment of an existing Java Web App.</span></span>
* <span data-ttu-id="07130-241">Puede publicar una aplicación Java adicional en el mismo contenedor de aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="07130-241">You can publish an additional Java application to the same Web App Container.</span></span>

<span data-ttu-id="07130-242">En cualquier caso, el proceso es idéntico y tarda unos pocos segundos:</span><span class="sxs-lookup"><span data-stu-id="07130-242">In either case, the process is identical and takes only a few seconds:</span></span>

1. <span data-ttu-id="07130-243">En el Explorador de proyectos de IntelliJ, haga clic con el botón derecho en la aplicación Java que quiere actualizar o agregar a un contenedor de aplicaciones web existente.</span><span class="sxs-lookup"><span data-stu-id="07130-243">In the IntelliJ project explorer, right-click the Java application you want to update or add to an existing Web App Container.</span></span>
2. <span data-ttu-id="07130-244">Cuando aparezca el menú contextual, seleccione **Azure** y, después, haga clic en **Publish as Azure Web App...** (Publicar como aplicación web de Azure).</span><span class="sxs-lookup"><span data-stu-id="07130-244">When the context menu appears, select **Azure** and then **Publish as Azure Web App...**</span></span>
3. <span data-ttu-id="07130-245">Puesto que ya ha iniciado sesión anteriormente, verá una lista de contenedores de aplicaciones web existentes.</span><span class="sxs-lookup"><span data-stu-id="07130-245">Since you have already logged in previously, you will see a list of your existing Web App containers.</span></span> <span data-ttu-id="07130-246">Seleccione aquel en el que quiere publicar o volver a publicar la aplicación Java y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="07130-246">Select the one you want to publish or re-publish your Java application to and click **OK**.</span></span>

<span data-ttu-id="07130-247">Unos segundos más tarde, la vista **Azure Activity Log** (Registro de actividad de Azure) mostrará la implementación actualizada como **Published** (Publicado) y podrá comprobar la aplicación actualizada en un explorador web.</span><span class="sxs-lookup"><span data-stu-id="07130-247">A few seconds later, the **Azure Activity Log** view will show your updated deployment as **Published** and you will be able to verify your updated application in a web browser.</span></span>

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a><span data-ttu-id="07130-248">Inicio, detención o reinicio de una aplicación web existente</span><span class="sxs-lookup"><span data-stu-id="07130-248">Starting, stopping, or restarting an existing web app</span></span>

<span data-ttu-id="07130-249">Para iniciar o detener un contenedor de aplicaciones web existente (junto con todas las aplicaciones Java implementadas en él), puede utilizar la vista **Azure Explorer** (Explorador de Azure).</span><span class="sxs-lookup"><span data-stu-id="07130-249">To start or stop an existing Azure Web App container, (including all the deployed Java applications in it), you can use the **Azure Explorer** view.</span></span>

<span data-ttu-id="07130-250">Si la vista del **Explorador de Azure** no está abierta, puede abrirla haciendo clic en el menú **View** (Ver) de IntelliJ, luego haga clic en **Tool Windows** (Ventanas de herramientas) y, después, en **Service Explorer** (Explorador de servicios).</span><span class="sxs-lookup"><span data-stu-id="07130-250">If the **Azure Explorer** view is not already open, you can open it by clicking then **View** menu in IntelliJ, then click **Tool Windows**, and then click **Service Explorer**.</span></span> <span data-ttu-id="07130-251">Si anteriormente no ha iniciado sesión, se le pedirá que lo haga.</span><span class="sxs-lookup"><span data-stu-id="07130-251">If you have not previously logged in, it will prompt you to do so.</span></span>

<span data-ttu-id="07130-252">Cuando se muestre la vista **Azure Explorer** (Explorador de Azure), siga estos pasos para iniciar o detener la aplicación web:</span><span class="sxs-lookup"><span data-stu-id="07130-252">When the **Azure Explorer** view is displayed, follow these steps to start or stop your Web App:</span></span> 

1. <span data-ttu-id="07130-253">Expanda el nodo **Azure** .</span><span class="sxs-lookup"><span data-stu-id="07130-253">Expand the **Azure** node.</span></span>
2. <span data-ttu-id="07130-254">Expanda el nodo **Web Apps** .</span><span class="sxs-lookup"><span data-stu-id="07130-254">Expand the **Web Apps** node.</span></span> 
3. <span data-ttu-id="07130-255">Haga clic en la aplicación web deseada.</span><span class="sxs-lookup"><span data-stu-id="07130-255">Right-click the desired Web App.</span></span>
4. <span data-ttu-id="07130-256">Cuando aparezca el menú contextual, haga clic en **Iniciar**, **Detener** o **Reiniciar**.</span><span class="sxs-lookup"><span data-stu-id="07130-256">When the context menu appears, click **Start**, **Stop**, or **Restart**.</span></span> <span data-ttu-id="07130-257">Tenga en cuenta que las opciones de menú dependen del contexto, por lo que solo podrá detener una aplicación web que se encuentre en ejecución o iniciar una aplicación web que no se esté ejecutando en ese momento.</span><span class="sxs-lookup"><span data-stu-id="07130-257">Note that the menu choices are context-aware, so you can only stop a running web app or start a web app which is not currently running.</span></span>
   
   ![Detener aplicación web][18]

## <a name="next-steps"></a><span data-ttu-id="07130-259">pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="07130-259">Next steps</span></span>

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

<span data-ttu-id="07130-260">Para obtener más información sobre cómo crear Azure Web Apps, consulte [Introducción a Web Apps].</span><span class="sxs-lookup"><span data-stu-id="07130-260">For additional information about creating Azure Web Apps, see the [Web Apps Overview].</span></span>

<!-- URL List -->

[Kit de herramientas de Azure para IntelliJ]: azure-toolkit-for-intellij.md
[Azure Toolkit for IntelliJ]: azure-toolkit-for-intellij.md
[Kit de herramientas de Azure para Eclipse]: ../eclipse/azure-toolkit-for-eclipse.md
[Azure Toolkit for Eclipse]: ../eclipse/azure-toolkit-for-eclipse.md
[eclipse-hello-world]: ../eclipse/azure-toolkit-for-eclipse-create-hello-world-web-app.md
[Introducción a Web Apps]: /azure/app-service/app-service-web-overview
[Web Apps Overview]: /azure/app-service/app-service-web-overview
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
