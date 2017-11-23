---
title: "Ejecución de una aplicación web Hola mundo como contenedor de Linux con el kit de herramientas de Azure para IntelliJ"
description: "Aprenda a crear una aplicación web de Hola mundo básica en un contenedor de Linux y publicarla en Azure mediante el kit de herramientas de Azure para IntelliJ."
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 11/01/2017
ms.author: robmcm
ms.openlocfilehash: 2c0bfc581b5bb033f301d5a1e632377442821392
ms.sourcegitcommit: 613c1ffd2e0279fc7a96fca98aa1809563f52ee1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="run-a-hello-world-web-app-in-a-linux-container-by-using-the-azure-toolkit-for-intellij"></a><span data-ttu-id="d6edc-103">Ejecución de una aplicación web Hola mundo como contenedor de Linux con el kit de herramientas de Azure para IntelliJ</span><span class="sxs-lookup"><span data-stu-id="d6edc-103">Run a Hello World web app in a Linux container by using the Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="d6edc-104">Los contenedores de [cliente de Docker] son un método muy utilizado para implementar aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="d6edc-104">[Docker] containers are a widely used method for deploying web applications.</span></span> <span data-ttu-id="d6edc-105">Usando contenedores de Docker, los desarrolladores pueden consolidar todos sus archivos de proyecto y dependencias en un único paquete para implementarlo en un servidor.</span><span class="sxs-lookup"><span data-stu-id="d6edc-105">By using Docker containers, developers can consolidate all their project files and dependencies into a single package for deployment to a server.</span></span> <span data-ttu-id="d6edc-106">El kit de herramientas de Azure para IntelliJ simplifica este proceso para los desarrolladores de Java, ya que agrega características para implementar contenedores en Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="d6edc-106">The Azure Toolkit for IntelliJ simplifies this process for Java developers by adding features for to deploy containers to Microsoft Azure.</span></span>

<span data-ttu-id="d6edc-107">En este artículo se muestran los pasos necesarios para crear una aplicación web de Hola mundo básica y publicar la aplicación web en un contenedor de Linux en Azure mediante el kit de herramientas de Azure para IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="d6edc-107">This article demonstrates the steps that are required to create a basic Hello World web app and publish your web app in a Linux container to Azure by using the Azure Toolkit for IntelliJ.</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]
* <span data-ttu-id="d6edc-108">Un [cliente de Docker].</span><span class="sxs-lookup"><span data-stu-id="d6edc-108">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="d6edc-109">Para completar los pasos de este tutorial, debe configurar [cliente de Docker] para que exponga el demonio en el puerto 2375 sin TLS.</span><span class="sxs-lookup"><span data-stu-id="d6edc-109">To complete the steps in this tutorial, you need to configure [Docker] to expose the daemon on port 2375 without TLS.</span></span> <span data-ttu-id="d6edc-110">Puede configurar esta opción al instalar Docker o mediante el menú de configuración de Docker.</span><span class="sxs-lookup"><span data-stu-id="d6edc-110">You can configure this setting when installing Docker, or through the Docker settings menu.</span></span>
>
> ![Menú de configuración de Docker][docker-settings-menu]
>

## <a name="create-a-new-web-app-project"></a><span data-ttu-id="d6edc-112">Creación de un proyecto de aplicación web nuevo</span><span class="sxs-lookup"><span data-stu-id="d6edc-112">Create a new web app project</span></span>

1. <span data-ttu-id="d6edc-113">Inicie IntelliJ e inicie sesión en su cuenta de Azure siguiendo los pasos del artículo [Instrucciones de inicio de sesión del kit de herramientas de Azure para IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="d6edc-113">Start IntelliJ and sign in to your Azure account using the steps in the [Sign In Instructions for the Azure Toolkit for IntelliJ] article.</span></span>

1. <span data-ttu-id="d6edc-114">Haga clic en el menú **File** (Archivo), en **New** (Nuevo) y en **Project** (Proyecto).</span><span class="sxs-lookup"><span data-stu-id="d6edc-114">Click the **File** menu, then click **New**, and then click **Project**.</span></span>
   
   ![Creación de un proyecto][file-new-project]

1. <span data-ttu-id="d6edc-116">En el cuadro de diálogo **New Project** (Nuevo proyecto), seleccione **Maven**, **maven-archetype-webapp** y haga clic en **Next** (Siguiente).</span><span class="sxs-lookup"><span data-stu-id="d6edc-116">In the **New Project** dialog box, select **Maven**, then **maven-archetype-webapp**, and then click **Next**.</span></span>
   
   ![Elección de una aplicación web de arquetipo Maven][maven-archetype-webapp]
   
1. <span data-ttu-id="d6edc-118">Especifique **GroupId** y **ArtifactId** para la aplicación web y haga clic en **Next** (Siguiente).</span><span class="sxs-lookup"><span data-stu-id="d6edc-118">Specify the **GroupId** and **ArtifactId** for your web app, and then click **Next**.</span></span>
   
   ![Especificación de GroupId y ArtifactId][groupid-and-artifactid]

1. <span data-ttu-id="d6edc-120">Personalice la configuración de Maven o acepte los valores predeterminados y haga clic en **Next** (Siguiente).</span><span class="sxs-lookup"><span data-stu-id="d6edc-120">Customize any Maven settings or accept the defaults, and then click **Next**.</span></span>
   
   ![Especificación de la configuración de Maven][maven-options]

1. <span data-ttu-id="d6edc-122">Especifique el nombre y la ubicación del proyecto, y haga clic en **Finish**(Finalizar).</span><span class="sxs-lookup"><span data-stu-id="d6edc-122">Specify your project name and location, and then click **Finish**.</span></span>
   
   ![Especificación del nombre del proyecto][project-name]

## <a name="create-an-azure-container-registry-to-use-as-a-private-docker-registry"></a><span data-ttu-id="d6edc-124">Creación de una instancia de Azure Container Registry para usarla como un registro de Docker privado</span><span class="sxs-lookup"><span data-stu-id="d6edc-124">Create an Azure Container Registry to use as a private Docker registry</span></span>

<span data-ttu-id="d6edc-125">Los siguientes pasos le muestran cómo usar Azure Portal para crear una instancia de Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="d6edc-125">The following steps walk you through using the Azure portal to create an Azure Container Registry.</span></span>

> [!NOTE]
>
> <span data-ttu-id="d6edc-126">Si quiere usar la CLI de Azure en lugar de Azure Portal, siga los pasos descritos en [Creación de un registro de contenedor privado de Docker con la CLI de Azure 2.0][Create Docker Registry using Azure CLI].</span><span class="sxs-lookup"><span data-stu-id="d6edc-126">If you want to use the Azure CLI instead of the Azure portal, follow the steps in [Create a private Docker container registry using the Azure CLI 2.0][Create Docker Registry using Azure CLI].</span></span>
>

1. <span data-ttu-id="d6edc-127">Vaya a [Azure Portal] e inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="d6edc-127">Browse to the [Azure portal] and sign in.</span></span>

   <span data-ttu-id="d6edc-128">Una vez que haya iniciado sesión en su cuenta en Azure Portal, puede seguir los pasos descritos en el artículo [Creación de un registro de contenedor privado de Docker con la CLI de Azure], que se vuelven a explicar en los pasos siguientes para mayor comodidad.</span><span class="sxs-lookup"><span data-stu-id="d6edc-128">Once you have signed in to your account on the Azure portal, you can follow the steps in the [Create a private Docker container registry using the Azure portal] article, which are paraphrased in the following steps for the sake of expediency.</span></span>

1. <span data-ttu-id="d6edc-129">Haga clic en el icono de menú **+ Nuevo**, en **Contenedores** y en **Azure Container Registry**.</span><span class="sxs-lookup"><span data-stu-id="d6edc-129">Click the menu icon for **+ New**, then click **Containers**, and then click **Azure Container Registry**.</span></span>
   
   ![Crear una instancia de Azure Container Registry][AR01]

1. <span data-ttu-id="d6edc-131">Cuando aparezca la página de información de la plantilla de Azure Container Registry, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="d6edc-131">When the information page for the Azure Container Registry template is displayed, click **Create**.</span></span> 

   ![Crear una instancia de Azure Container Registry][AR02]

1. <span data-ttu-id="d6edc-133">Cuando aparezca la página **Crear Registro de contenedor**, escriba su **Nombre del Registro** y **Grupo de recursos**, elija **Habilitar** para el **Usuario administrador** y haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="d6edc-133">When the **Create container registry** page is displayed, enter your **Registry name** and **Resource group**, choose **Enable** for the **Admin user**, and then click **Create**.</span></span>

   ![Configurar Azure Container Registry][AR03]

1. <span data-ttu-id="d6edc-135">Una vez que se haya creado el Registro de contenedor, desplácese hasta él en Azure Portal y haga clic en **Claves de acceso**.</span><span class="sxs-lookup"><span data-stu-id="d6edc-135">Once your container registry has been created, navigate to your container registry in the Azure portal, and then click **Access Keys**.</span></span> <span data-ttu-id="d6edc-136">Tome nota del nombre de usuario y la contraseña para usarlos en los pasos siguientes.</span><span class="sxs-lookup"><span data-stu-id="d6edc-136">Take note of the username and password for the next steps.</span></span>

   ![Claves de acceso de Azure Container Registry][AR04]

## <a name="deploy-your-web-app-in-a-docker-container"></a><span data-ttu-id="d6edc-138">Implementación de una aplicación web en un contenedor de Docker</span><span class="sxs-lookup"><span data-stu-id="d6edc-138">Deploy your web app in a Docker container</span></span>

1. <span data-ttu-id="d6edc-139">Haga clic con el botón derecho en el proyecto en Project Explorer, elija **Azure** y haga clic en **Add Docker Support** (Agregar compatibilidad con Docker).</span><span class="sxs-lookup"><span data-stu-id="d6edc-139">Right-click your project in the project explorer, choose **Azure**, and then click **Add Docker Support**.</span></span>

   <span data-ttu-id="d6edc-140">Se creará automáticamente un archivo de Docker con una configuración predeterminada.</span><span class="sxs-lookup"><span data-stu-id="d6edc-140">This will automatically create a Docker file with a default configuration.</span></span>

   ![Agregue compatibilidad con Docker][add-docker-support]

1. <span data-ttu-id="d6edc-142">Después de agregar compatibilidad con Docker, haga clic con el botón derecho en el proyecto en Project Explorer, elija **Azure** y haga clic en **Run on Web App (Linux)** [Ejecutar en aplicación web (Linux)].</span><span class="sxs-lookup"><span data-stu-id="d6edc-142">After you have added Docker support, right-click your project in the project explorer, choose **Azure**, and then click **Run on Web App (Linux)**.</span></span>

   ![Ejecutar en aplicación web (Linux)][run-on-web-app-linux]

1. <span data-ttu-id="d6edc-144">En el cuadro de diálogo **Run on Web App (Linux)** [Ejecutar en aplicación web (Linux)] que aparece, rellene la información necesaria:</span><span class="sxs-lookup"><span data-stu-id="d6edc-144">When the **Run on Web App (Linux)** dialog box is displayed, fill in the requisite information:</span></span>

   * <span data-ttu-id="d6edc-145">**Name** (Nombre): especifica el nombre descriptivo que se muestra en el kit de herramientas de Azure.</span><span class="sxs-lookup"><span data-stu-id="d6edc-145">**Name**: This specifies the friendly name which is displayed in the Azure Toolkit.</span></span> 

   * <span data-ttu-id="d6edc-146">**Server URL** (Dirección URL del servidor): especifica la dirección URL para el registro de contenedor de la sección anterior de este artículo; se suele utilizar la sintaxis siguiente: "*registro*.azurecr.io".</span><span class="sxs-lookup"><span data-stu-id="d6edc-146">**Server URL**: This specifies the URL for your container registry from the previous section of this article; typically this will use the following syntax: "*registry*.azurecr.io".</span></span> 

   * <span data-ttu-id="d6edc-147">**Username** (Nombre de usuario) y **Password** (Contraseña): especifica las claves de acceso para el registro de contenedor de la sección anterior de este artículo.</span><span class="sxs-lookup"><span data-stu-id="d6edc-147">**Username** and **Password**: Specifies the access keys for your container registry from the previous section of this article.</span></span> 

   * <span data-ttu-id="d6edc-148">**Image and tag** (Imagen y etiqueta): especifica el nombre de imagen de contenedor; se suele utilizar la sintaxis siguiente: "*registro*.azurecr.io/*nombreDeAplicación*:latest", donde:</span><span class="sxs-lookup"><span data-stu-id="d6edc-148">**Image and tag**: Specifies the container image name; typically this will use the following syntax: "*registry*.azurecr.io/*appname*:latest", where:</span></span> 
      * <span data-ttu-id="d6edc-149">*registro* es el registro de contenedor de la sección anterior de este artículo</span><span class="sxs-lookup"><span data-stu-id="d6edc-149">*registry* is your container registry from the previous section of this article</span></span> 
      * <span data-ttu-id="d6edc-150">*nombreDeAplicación* es el nombre de la aplicación web</span><span class="sxs-lookup"><span data-stu-id="d6edc-150">*appname* is the name of your web app</span></span> 

   * <span data-ttu-id="d6edc-151">**Use Existing Web App** (Usar la aplicación web existente) o **Create New Web App** (Crear aplicación web nueva): especifica si se implementa el contenedor en una aplicación web existente o se crea una aplicación web nueva.</span><span class="sxs-lookup"><span data-stu-id="d6edc-151">**Use Existing Web App** or **Create New Web App**: Specifies whether you will deploy your container to an existing web app or create a new web app.</span></span> 

   * <span data-ttu-id="d6edc-152">**Resource Group** (Grupo de recursos): especifica si va a utilizar un grupo de recursos existente o va a crear uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="d6edc-152">**Resource Group**: Specifies whether you will use an existing or create a new resource group.</span></span> 

   * <span data-ttu-id="d6edc-153">**App Service Plan** (Plan de App Service): especifica si va a utilizar un grupo de recursos existente o va a crear uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="d6edc-153">**App Service Plan**: Specifies whether you willuse an existing or create a new app service plan.</span></span> 

1. <span data-ttu-id="d6edc-154">Cuando haya terminado de configurar los valores enumerados anteriormente, haga clic en **Run** (Ejecutar).</span><span class="sxs-lookup"><span data-stu-id="d6edc-154">When you have finished configuring the settings listed above, click **Run**.</span></span>

   ![Crear aplicación web][create-web-app]

1. <span data-ttu-id="d6edc-156">Después de publicar la aplicación web, la configuración se guardará como valor predeterminado y podrá ejecutar la aplicación en Azure al hacer clic en el icono de flecha verde de la barra de herramientas.</span><span class="sxs-lookup"><span data-stu-id="d6edc-156">After you have published your web app, your settings will be saved as the default, and you can run your application on Azure by clicking the green arrow icon on the toolbar.</span></span> <span data-ttu-id="d6edc-157">Para modificar esta configuración, haga clic en el menú desplegable de la aplicación web y, luego, en **Edit Configurations** (Editar configuraciones).</span><span class="sxs-lookup"><span data-stu-id="d6edc-157">You can modify these settings by clicking the drop-down menu for your web app and click **Edit Configurations**.</span></span>

   ![Menú Editar configuración][edit-configuration-menu]

1. <span data-ttu-id="d6edc-159">Cuando aparezca el cuadro de diálogo **Run/Debug Configurations** (Ejecutar/Depurar configuraciones), podrá modificar cualquiera de los valores predeterminados y hacer clic en **OK** (Aceptar).</span><span class="sxs-lookup"><span data-stu-id="d6edc-159">When the **Run/Debug Configurations** dialog box is displayed, you can modify any of the default settings, and then click **OK**.</span></span>

   ![Cuadro de diálogo Editar configuración][edit-configuration-dialog]

## <a name="next-steps"></a><span data-ttu-id="d6edc-161">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d6edc-161">Next steps</span></span>

<span data-ttu-id="d6edc-162">Para ver más recursos de Docker, vaya al [sitio web oficial de Docker][cliente de Docker].</span><span class="sxs-lookup"><span data-stu-id="d6edc-162">For additional resources for Docker, see the official [Docker website][Docker].</span></span>

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

<!-- URL List -->

[Azure Portal]: https://portal.azure.com/
[Creación de un registro de contenedor privado de Docker con la CLI de Azure]: /azure/container-registry/container-registry-get-started-portal
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Create Docker Registry using Azure CLI]: /azure/container-registry/container-registry-get-started-azure-cli

[cliente de Docker]: https://www.docker.com/
[Configuring artifacts]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html

<!-- IMG List -->

[AR01]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/AR01.png
[AR02]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/AR02.png
[AR03]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/AR03.png
[AR04]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/AR04.png

[docker-settings-menu]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/docker-settings-menu.png
[file-new-project]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/file-new-project.png
[maven-archetype-webapp]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/maven-archetype-webapp.png
[groupid-and-artifactid]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/groupid-and-artifactid.png
[maven-options]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/maven-options.png
[project-name]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/project-name.png
[add-docker-support]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/add-docker-support.png
[run-on-web-app-linux]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/run-on-web-app-linux.png
[create-web-app]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/create-web-app.png
[edit-configuration-menu]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/edit-configuration-menu.png
[edit-configuration-dialog]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/edit-configuration-dialog.png
[successfully-deployed]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/successfully-deployed.png
