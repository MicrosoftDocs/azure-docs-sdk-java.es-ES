---
title: Implementación de una aplicación web Hola mundo en un contenedor Linux en la nube con el kit de herramientas de Azure para IntelliJ
description: Ejecución de una aplicación web Hola mundo en un contenedor Linux y su implementación en la nube con el kit de herramientas de Azure para IntelliJ.
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 12/20/2018
ms.devlang: Java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.openlocfilehash: fdff8dc2bd7a29473314d5c0bc99b7bcda369156
ms.sourcegitcommit: 54e7f077d694a5b1dd7fa6c8870b7d476af9829c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/02/2019
ms.locfileid: "55648729"
---
# <a name="deploy-a-hello-world-web-app-to-a-linux-container-in-the-cloud-using-the-azure-toolkit-for-intellij"></a><span data-ttu-id="19799-103">Implementación de una aplicación web Hola mundo en un contenedor Linux en la nube con el kit de herramientas de Azure para IntelliJ</span><span class="sxs-lookup"><span data-stu-id="19799-103">Deploy a Hello World web app to a Linux container in the cloud using the Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="19799-104">Los contenedores de [Docker] son un método muy utilizado para implementar aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="19799-104">[Docker] containers are a widely used method for deploying web applications.</span></span> <span data-ttu-id="19799-105">Usando contenedores de Docker, los desarrolladores pueden consolidar todos sus archivos de proyecto y dependencias en un único paquete para implementarlo en un servidor.</span><span class="sxs-lookup"><span data-stu-id="19799-105">By using Docker containers, developers can consolidate all their project files and dependencies into a single package for deployment to a server.</span></span> <span data-ttu-id="19799-106">El kit de herramientas de Azure para IntelliJ simplifica este proceso para los desarrolladores de Java, ya que agrega características para implementar contenedores en Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="19799-106">The Azure Toolkit for IntelliJ simplifies this process for Java developers by adding features for to deploy containers to Microsoft Azure.</span></span>

<span data-ttu-id="19799-107">En este artículo se muestran los pasos necesarios para crear una aplicación web de Hola mundo básica y publicar la aplicación web en un contenedor de Linux en Azure mediante el kit de herramientas de Azure para IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="19799-107">This article demonstrates the steps that are required to create a basic Hello World web app and publish your web app in a Linux container to Azure by using the Azure Toolkit for IntelliJ.</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]
* <span data-ttu-id="19799-108">Un cliente de [Docker].</span><span class="sxs-lookup"><span data-stu-id="19799-108">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="19799-109">Para completar los pasos de este tutorial, debe configurar [Docker] para que exponga el demonio en el puerto 2375 sin TLS.</span><span class="sxs-lookup"><span data-stu-id="19799-109">To complete the steps in this tutorial, you need to configure [Docker] to expose the daemon on port 2375 without TLS.</span></span> <span data-ttu-id="19799-110">Puede configurar esta opción al instalar Docker o mediante el menú de configuración de Docker.</span><span class="sxs-lookup"><span data-stu-id="19799-110">You can configure this setting when installing Docker, or through the Docker settings menu.</span></span>
>
> ![Menú de configuración de Docker][docker-settings-menu]
>

## <a name="create-a-new-web-app-project"></a><span data-ttu-id="19799-112">Creación de un proyecto de aplicación web nuevo</span><span class="sxs-lookup"><span data-stu-id="19799-112">Create a new web app project</span></span>

1. <span data-ttu-id="19799-113">Inicie IntelliJ e inicie sesión en la cuenta de Azure siguiendo los pasos del artículo [Instrucciones de inicio de sesión del kit de herramientas de Azure para IntelliJ](https://docs.microsoft.com/java/azure/intellij/azure-toolkit-for-intellij-sign-in-instructions).</span><span class="sxs-lookup"><span data-stu-id="19799-113">Start IntelliJ and sign in to your Azure account using the steps in the [Sign In Instructions for the Azure Toolkit for IntelliJ](https://docs.microsoft.com/java/azure/intellij/azure-toolkit-for-intellij-sign-in-instructions) article.</span></span>

1. <span data-ttu-id="19799-114">Haga clic en el menú **File** (Archivo), luego en **New** (Nuevo) y, finalmente, en **Project** (Proyecto).</span><span class="sxs-lookup"><span data-stu-id="19799-114">Click the **File** menu, then click **New**, and then click **Project**.</span></span>
   
   ![Creación de un proyecto][file-new-project]

1. <span data-ttu-id="19799-116">En el cuadro de diálogo **New Project** (Nuevo proyecto), seleccione **Maven**, **maven-archetype-webapp** y haga clic en **Next** (Siguiente).</span><span class="sxs-lookup"><span data-stu-id="19799-116">In the **New Project** dialog box, select **Maven**, then **maven-archetype-webapp**, and then click **Next**.</span></span>
   
   ![Elección de una aplicación web de arquetipo Maven][maven-archetype-webapp]
   
1. <span data-ttu-id="19799-118">Especifique **GroupId** y **ArtifactId** para la aplicación web y haga clic en **Next** (Siguiente).</span><span class="sxs-lookup"><span data-stu-id="19799-118">Specify the **GroupId** and **ArtifactId** for your web app, and then click **Next**.</span></span>
   
   ![Especificación de GroupId y ArtifactId][groupid-and-artifactid]

1. <span data-ttu-id="19799-120">Personalice la configuración de Maven o acepte los valores predeterminados y haga clic en **Next** (Siguiente).</span><span class="sxs-lookup"><span data-stu-id="19799-120">Customize any Maven settings or accept the defaults, and then click **Next**.</span></span>
   
   ![Especificación de la configuración de Maven][maven-options]

1. <span data-ttu-id="19799-122">Especifique el nombre y la ubicación del proyecto, y haga clic en **Finish**(Finalizar).</span><span class="sxs-lookup"><span data-stu-id="19799-122">Specify your project name and location, and then click **Finish**.</span></span>
   
   ![Especificación del nombre del proyecto][project-name]

## <a name="create-an-azure-container-registry-to-use-as-a-private-docker-registry"></a><span data-ttu-id="19799-124">Creación de una instancia de Azure Container Registry para usarla como un registro de Docker privado</span><span class="sxs-lookup"><span data-stu-id="19799-124">Create an Azure Container Registry to use as a private Docker registry</span></span>

<span data-ttu-id="19799-125">Los siguientes pasos le muestran cómo usar Azure Portal para crear una instancia de Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="19799-125">The following steps walk you through using the Azure portal to create an Azure Container Registry.</span></span>

> [!NOTE]
>
> <span data-ttu-id="19799-126">Si quiere usar la CLI de Azure en lugar de Azure Portal, siga los pasos descritos en [Creación de un registro de contenedor privado de Docker con la CLI de Azure 2.0][Create Docker Registry using Azure CLI].</span><span class="sxs-lookup"><span data-stu-id="19799-126">If you want to use the Azure CLI instead of the Azure portal, follow the steps in [Create a private Docker container registry using the Azure CLI 2.0][Create Docker Registry using Azure CLI].</span></span>
>

1. <span data-ttu-id="19799-127">Vaya a [Azure Portal] e inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="19799-127">Browse to the [Azure portal] and sign in.</span></span>

   <span data-ttu-id="19799-128">Una vez que haya iniciado sesión en su cuenta en Azure Portal, puede seguir los pasos descritos en el artículo [Creación de un registro de contenedor privado de Docker con Azure Portal], que se vuelven a explicar en los pasos siguientes para mayor comodidad.</span><span class="sxs-lookup"><span data-stu-id="19799-128">Once you have signed in to your account on the Azure portal, you can follow the steps in the [Create a private Docker container registry using the Azure portal] article, which are paraphrased in the following steps for the sake of expediency.</span></span>

1. <span data-ttu-id="19799-129">Haga clic en el icono de menú **+ Crear un recurso**, en **Contenedores** y en **Container Registry**.</span><span class="sxs-lookup"><span data-stu-id="19799-129">Click the menu icon for **+ Create a resource**, then click **Containers**, and then click **Container Registry**.</span></span>
   
   ![Crear una instancia de Azure Container Registry][create-container-registry-01]

1. <span data-ttu-id="19799-131">Cuando aparezca la página **Crear Registro de contenedor**, escriba su **Nombre del Registro** y **Grupo de recursos**, elija **Habilitar** para el **Usuario administrador** y haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="19799-131">When the **Create container registry** page is displayed, enter your **Registry name** and **Resource group**, choose **Enable** for the **Admin user**, and then click **Create**.</span></span>

   ![Configurar Azure Container Registry][create-container-registry-02]

## <a name="deploy-your-web-app-in-a-docker-container"></a><span data-ttu-id="19799-133">Implementación de una aplicación web en un contenedor de Docker</span><span class="sxs-lookup"><span data-stu-id="19799-133">Deploy your web app in a Docker container</span></span>

1. <span data-ttu-id="19799-134">Haga clic con el botón derecho en el proyecto en Project Explorer, elija **Azure** y haga clic en **Add Docker Support** (Agregar compatibilidad con Docker).</span><span class="sxs-lookup"><span data-stu-id="19799-134">Right-click your project in the project explorer, choose **Azure**, and then click **Add Docker Support**.</span></span>

   <span data-ttu-id="19799-135">Se creará automáticamente un archivo de Docker con una configuración predeterminada.</span><span class="sxs-lookup"><span data-stu-id="19799-135">This will automatically create a Docker file with a default configuration.</span></span>

   ![Agregue compatibilidad con Docker][add-docker-support]

1. <span data-ttu-id="19799-137">Después de agregar compatibilidad con Docker, haga clic con el botón derecho en el proyecto en Project Explorer, elija **Azure** y haga clic en **Run on Web App for Containers** (Ejecutar en Web App for Containers).</span><span class="sxs-lookup"><span data-stu-id="19799-137">After you have added Docker support, right-click your project in the project explorer, choose **Azure**, and then click **Run on Web App for Containers**.</span></span>

   ![Ejecutar en Web App for Containers][run-on-web-app-for-containers]

1. <span data-ttu-id="19799-139">En el cuadro de diálogo **Run on Web App for Containers** (Ejecutar en Web App for Containers) que aparece, rellene la información necesaria:</span><span class="sxs-lookup"><span data-stu-id="19799-139">When the **Run on Web App for Containers** dialog box is displayed, fill in the requisite information:</span></span>

   * <span data-ttu-id="19799-140">**Name** (Nombre): especifica el nombre descriptivo que se muestra en el kit de herramientas de Azure.</span><span class="sxs-lookup"><span data-stu-id="19799-140">**Name**: This specifies the friendly name which is displayed in the Azure Toolkit.</span></span> 

   * <span data-ttu-id="19799-141">**Container Registry** (Registro de contenedor): En el menú desplegable, elija el registro de contenedor que creó en la sección anterior de este artículo.</span><span class="sxs-lookup"><span data-stu-id="19799-141">**Container Registry**: Choose the container registry from the drop-down menu that you created in the previous section of this article.</span></span> <span data-ttu-id="19799-142">Los campos **Server URL** (URL del servidor), **Username** (Nombre de usuario) y **Password** (Contraseña) se rellenarán automáticamente.</span><span class="sxs-lookup"><span data-stu-id="19799-142">The fields for **Server URL**, **Username**, and **Password** will be automatically populated.</span></span>

   * <span data-ttu-id="19799-143">**Image and tag** (Imagen y etiqueta): especifica el nombre de la imagen de contenedor; se suele utilizar la sintaxis siguiente: "*registro*.azurecr.io/*nombreDeAplicación*:latest", donde:</span><span class="sxs-lookup"><span data-stu-id="19799-143">**Image and tag**: Specifies the container image name; typically this will use the following syntax: "*registry*.azurecr.io/*appname*:latest", where:</span></span> 
      * <span data-ttu-id="19799-144">*registro* es el registro de contenedor de la sección anterior de este artículo</span><span class="sxs-lookup"><span data-stu-id="19799-144">*registry* is your container registry from the previous section of this article</span></span> 
      * <span data-ttu-id="19799-145">*nombreDeAplicación* es el nombre de la aplicación web</span><span class="sxs-lookup"><span data-stu-id="19799-145">*appname* is the name of your web app</span></span> 

   * <span data-ttu-id="19799-146">**Use Existing Web App** (Usar aplicación web existente) o **Create New Web App** (Crear aplicación web nueva): especifica si el contenedor se implementará en una aplicación web existente o se creará una aplicación web nueva.</span><span class="sxs-lookup"><span data-stu-id="19799-146">**Use Existing Web App** or **Create New Web App**: Specifies whether you will deploy your container to an existing web app or create a new web app.</span></span> <span data-ttu-id="19799-147">Con el **nombre de aplicación** que especifique se creará la dirección URL de la aplicación web; por ejemplo: *wingtiptoys.azurewebsites.net*.</span><span class="sxs-lookup"><span data-stu-id="19799-147">The **App name** that you specify will create the URL for your web app; for example: *wingtiptoys.azurewebsites.net*.</span></span>

   * <span data-ttu-id="19799-148">**Resource Group** (Grupo de recursos): especifica si va a utilizar un grupo de recursos existente o va a crear uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="19799-148">**Resource Group**: Specifies whether you will use an existing or create a new resource group.</span></span> 

   * <span data-ttu-id="19799-149">**App Service Plan** (Plan de App Service): especifica si va a utilizar un plan de App Service existente o va a crear uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="19799-149">**App Service Plan**: Specifies whether you will use an existing or create a new app service plan.</span></span> 

   ![Ejecutar en Web App for Containers][run-on-web-app-linux]

1. <span data-ttu-id="19799-151">Cuando haya terminado de configurar los valores enumerados anteriormente, haga clic en **Run** (Ejecutar).</span><span class="sxs-lookup"><span data-stu-id="19799-151">When you have finished configuring the settings listed above, click **Run**.</span></span> <span data-ttu-id="19799-152">Cuando la aplicación web se ha implementado correctamente, se muestra el estado en la ventana **Ejecutar**.</span><span class="sxs-lookup"><span data-stu-id="19799-152">When your web app has been successfully deployed, the status will be displayed in the **Run** window.</span></span>

   ![La aplicación web se implementó correctamente][successfully-deployed]

1. <span data-ttu-id="19799-154">Una vez publicada la aplicación web, puede ir a la dirección URL que especificó anteriormente para ella. Por ejemplo: *wingtiptoys.azurewebsites.net*.</span><span class="sxs-lookup"><span data-stu-id="19799-154">After your web app has been published, you can browse to the URL that specifed earlier for your web app; for example: *wingtiptoys.azurewebsites.net*.</span></span>

   ![Ir a la aplicación web][browsing-to-web-app]

## <a name="optional-modify-your-web-app-publish-settings"></a><span data-ttu-id="19799-156">Opcional: Modificación de la configuración de publicación de la aplicación web</span><span class="sxs-lookup"><span data-stu-id="19799-156">Optional: Modify your web app publish settings</span></span>

1. <span data-ttu-id="19799-157">Después de publicar la aplicación web, la configuración se guardará como valor predeterminado y podrá ejecutar la aplicación en Azure al hacer clic en el icono de flecha verde de la barra de herramientas.</span><span class="sxs-lookup"><span data-stu-id="19799-157">After you have published your web app, your settings will be saved as the default, and you can run your application on Azure by clicking the green arrow icon on the toolbar.</span></span> <span data-ttu-id="19799-158">Para modificar esta configuración, haga clic en el menú desplegable de la aplicación web y, luego, en **Edit Configurations** (Editar configuraciones).</span><span class="sxs-lookup"><span data-stu-id="19799-158">You can modify these settings by clicking the drop-down menu for your web app and click **Edit Configurations**.</span></span>

   ![Menú Editar configuración][edit-configuration-menu]

1. <span data-ttu-id="19799-160">Cuando aparezca el cuadro de diálogo **Run/Debug Configurations** (Ejecutar/Depurar configuraciones), podrá modificar cualquiera de los valores predeterminados y hacer clic en **OK** (Aceptar).</span><span class="sxs-lookup"><span data-stu-id="19799-160">When the **Run/Debug Configurations** dialog box is displayed, you can modify any of the default settings, and then click **OK**.</span></span>

   ![Cuadro de diálogo Editar configuración][edit-configuration-dialog]

## <a name="next-steps"></a><span data-ttu-id="19799-162">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="19799-162">Next steps</span></span>

<span data-ttu-id="19799-163">Para ver más recursos de Docker, vaya al [sitio web oficial de Docker][Docker].</span><span class="sxs-lookup"><span data-stu-id="19799-163">For additional resources for Docker, see the official [Docker website][Docker].</span></span>

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

<!-- URL List -->

[Azure Portal]: https://portal.azure.com/
[Azure portal]: https://portal.azure.com/
[Creación de un registro de contenedor privado de Docker con Azure Portal]: /azure/container-registry/container-registry-get-started-portal
[Create a private Docker container registry using the Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Create Docker Registry using Azure CLI]: /azure/container-registry/container-registry-get-started-azure-cli

[Docker]: https://www.docker.com/
[Configuring artifacts]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html

<!-- IMG List -->

[add-docker-support]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/add-docker-support.png
[browsing-to-web-app]:  media/azure-toolkit-for-intellij-hello-world-web-app-linux/browsing-to-web-app.png
[create-container-registry-01]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/create-container-registry-01.png
[create-container-registry-02]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/create-container-registry-02.png
[docker-settings-menu]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/docker-settings-menu.png
[edit-configuration-dialog]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/edit-configuration-dialog.png
[edit-configuration-menu]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/edit-configuration-menu.png
[file-new-project]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/file-new-project.png
[groupid-and-artifactid]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/groupid-and-artifactid.png
[maven-archetype-webapp]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/maven-archetype-webapp.png
[maven-options]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/maven-options.png
[project-name]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/project-name.png
[run-on-web-app-for-containers]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/run-on-web-app-for-containers.png
[run-on-web-app-linux]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/run-on-web-app-linux.png
[successfully-deployed]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/successfully-deployed.png
