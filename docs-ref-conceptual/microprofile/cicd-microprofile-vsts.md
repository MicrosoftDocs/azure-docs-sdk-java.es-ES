---
title: CI/CD para aplicaciones de MicroProfile con Azure DevOps
description: Obtenga información sobre cómo configurar un ciclo de versión de CI/CD para implementar una aplicación de MicroProfile en una instancia de Azure Web App for Containers con Azure DevOps
services: Azure DevOps
documentationcenter: MicroProfile
author: ruyakubu
manager: brunoborges
editor: ruyakubu
ms.assetid: ''
ms.author: ruyakubu
ms.date: 09/14/2018
ms.devlang: Java
ms.service: Azure DevOps
ms.tgt_pltfrm: multiple
ms.topic: tutorial
ms.workload: web
ms.openlocfilehash: c2b6bf3370982d26d8d23fede370e0105a70b734
ms.sourcegitcommit: fd67d4088be2cad01c642b9ecf3f9475d9cb4f3c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/21/2018
ms.locfileid: "46506588"
---
# <a name="cicd-for-microprofile-applications-using-azure-devops"></a><span data-ttu-id="3f128-103">CI/CD para aplicaciones de MicroProfile con Azure DevOps</span><span class="sxs-lookup"><span data-stu-id="3f128-103">CI/CD for MicroProfile applications using Azure DevOps</span></span>

<span data-ttu-id="3f128-104">Este tutorial muestra cómo pueden los desarrolladores de Java EE configurar fácilmente un ciclo de versión de CI/CD para implementar sus aplicaciones de [MicroProfile](http://microprofile.io) en Azure Web App for Containers con Azure DevOps (anteriormente conocido como VSTS).</span><span class="sxs-lookup"><span data-stu-id="3f128-104">This tutorial will show how Java EE developers can easily setup a CI/CD release cycle to deploy their [MicroProfile](http://microprofile.io) applications to an Azure Web App for Containers using Azure DevOps (formally known as VSTS).</span></span>  <span data-ttu-id="3f128-105">En este ejemplo, vamos a usar una aplicación de MicroProfile que usa [Payara Micro](https://www.payara.fish/payara_micro) como imagen base.</span><span class="sxs-lookup"><span data-stu-id="3f128-105">In this example, we’ll be using a MicroProfile application that uses a [Payara Micro](https://www.payara.fish/payara_micro) as a base image.</span></span>   

```Dockerfile
FROM payara/micro:5.182
COPY target/*.war $DEPLOY_DIR/ROOT.war
EXPOSE 8080
```
<span data-ttu-id="3f128-106">El proceso de inclusión en contenedores de Azure DevOps se inicia con la creación de una imagen de Docker y la inserción de la imagen de contenedor en Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="3f128-106">We will start the Azure DevOps containerize process by building a Docker image and pushing the container image to an Azure Container Register.</span></span>  <span data-ttu-id="3f128-107">A continuación, se completará con una canalización de versión de Azure DevOps para implementar la imagen de contenedor en una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="3f128-107">Then complete with a Azure DevOps release pipeline to deploy the container image to a Web App.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3f128-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="3f128-108">Prerequisites</span></span>
- <span data-ttu-id="3f128-109">Copie y guarde la dirección URL de Git desde [Github](https://github.com/Azure-Samples/microprofile-hello-azure).</span><span class="sxs-lookup"><span data-stu-id="3f128-109">Copy and save the Git url from [Github](https://github.com/Azure-Samples/microprofile-hello-azure)</span></span>
- <span data-ttu-id="3f128-110">Regístrese o inicie sesión en su cuenta de [Azure DevOps](https://dev.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3f128-110">Register or Log into your [Azure DevOps](https://dev.azure.com) account</span></span>
- <span data-ttu-id="3f128-111">Cree un nuevo [proyecto de Azure DevOps](https://docs.microsoft.com/en-us/vsts/organizations/projects/create-project?view=vsts&tabs=new-nav) y use la dirección URL de Git anterior para **importar un repositorio**.</span><span class="sxs-lookup"><span data-stu-id="3f128-111">Create a new [Azure DevOps project](https://docs.microsoft.com/en-us/vsts/organizations/projects/create-project?view=vsts&tabs=new-nav) and use the above Git url to **import a repository**</span></span>
- <span data-ttu-id="3f128-112">Cree una instancia de [Azure Container Registry](https://azure.microsoft.com/en-us/services/container-registry) (ACR).</span><span class="sxs-lookup"><span data-stu-id="3f128-112">Create an [Azure Container Registry](https://azure.microsoft.com/en-us/services/container-registry) (ACR)</span></span>
- <span data-ttu-id="3f128-113">Cree una instancia de Azure Web App for Containers.</span><span class="sxs-lookup"><span data-stu-id="3f128-113">Create an Azure Web App for Container</span></span>
> [!NOTE]
>
> <span data-ttu-id="3f128-114">Seleccione "Inicio rápido" en la configuración del contenedor al aprovisionar la instancia de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="3f128-114">Select "Quickstart" in the Container Settings when provisioning the Web App instance</span></span>


## <a name="create-a-build-definition"></a><span data-ttu-id="3f128-115">Creación de una definición de compilación</span><span class="sxs-lookup"><span data-stu-id="3f128-115">Create a Build definition</span></span>

<span data-ttu-id="3f128-116">La definición de compilación de Azure DevOps ejecuta automáticamente todas las tareas de la compilación cada vez que hay una confirmación en el código fuente de la aplicación de Java EE.</span><span class="sxs-lookup"><span data-stu-id="3f128-116">The build definition in Azure DevOps automatically executes all the tasks in the build each time there’s a commit in Java EE application source application.</span></span>  <span data-ttu-id="3f128-117">En este ejemplo, Azure DevOps usa Maven para compilar el proyecto de MicroProfile de Java.</span><span class="sxs-lookup"><span data-stu-id="3f128-117">In this example, Azure DevOps will use Maven to build the Java MicroProfile project.</span></span>

1. <span data-ttu-id="3f128-118">Haga clic en la pestaña "Compilación y versión" en la parte superior de la página del proyecto de Azure DevOps.</span><span class="sxs-lookup"><span data-stu-id="3f128-118">Click on the "Build and Release" tab on top your Azure DevOps project page.</span></span>  <span data-ttu-id="3f128-119">A continuación, seleccione el vínculo **Compilaciones**.</span><span class="sxs-lookup"><span data-stu-id="3f128-119">Then, select the **Builds** link</span></span> 

<img src="media/VSTS/Buid-and-Release1.png">

2. <span data-ttu-id="3f128-120">Haga clic en el botón **Nueva canalización** y, a continuación, en **Continuar** para comenzar a definir las tareas de compilación.</span><span class="sxs-lookup"><span data-stu-id="3f128-120">Click on the **New Pipeline** button, and then **Continue** to start defining your build tasks</span></span>
3. <span data-ttu-id="3f128-121">Seleccione "Maven" en la lista de plantillas y haga clic en el botón **Aplicar** para compilar el proyecto de Java.</span><span class="sxs-lookup"><span data-stu-id="3f128-121">Select "Maven" from the list of templates, then click on the **Apply** button to build your Java project</span></span>
4. <span data-ttu-id="3f128-122">Use el menú desplegable del campo Grupo de agentes para seleccionar la opción **Hosted Linux Preview**.</span><span class="sxs-lookup"><span data-stu-id="3f128-122">Use the drop-down menu for the Agent pool field to select **Hosted Linux Preview** option.</span></span>
> [!NOTE]
>
> <span data-ttu-id="3f128-123">Esto informa a Azure DevOps sobre qué servidor de compilación se va a utilizar.</span><span class="sxs-lookup"><span data-stu-id="3f128-123">This informs Azure DevOps which build server to use.</span></span>  <span data-ttu-id="3f128-124">Puede usar un servidor de compilación personalizado privado.</span><span class="sxs-lookup"><span data-stu-id="3f128-124">You can use your private customized build server</span></span>

5. <span data-ttu-id="3f128-125">Para configurar la compilación para la integración continua, seleccione la pestaña **Desencadenadores** y active la casilla de verificación **Habilitar la integración continua**.</span><span class="sxs-lookup"><span data-stu-id="3f128-125">To configure your build for continuous integration, select the **Triggers** tab and check the **Enable continuous integration** checkbox.</span></span>  

<img src="media/VSTS/Build-Triggers2.png"> 
 
6. <span data-ttu-id="3f128-126">Seleccione la pestaña **Tareas** para volver a la página principal de la canalización de compilación.</span><span class="sxs-lookup"><span data-stu-id="3f128-126">Select the **Tasks** tab to return back to the main build pipeline page</span></span>
7. <span data-ttu-id="3f128-127">Use el menú desplegable **Guardar y poner en cola** para seleccionar la opción **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="3f128-127">Use the **Save & queue** drop-down menu to select the **Save** option</span></span>
 

## <a name="create-a-docker-build-image"></a><span data-ttu-id="3f128-128">Creación de una imagen de compilación de Docker</span><span class="sxs-lookup"><span data-stu-id="3f128-128">Create a Docker Build Image</span></span>

<span data-ttu-id="3f128-129">En esta tarea, Azure DevOps usa un Dockerfile con una imagen base de Payara Micro para crear una imagen de Docker.</span><span class="sxs-lookup"><span data-stu-id="3f128-129">In this task, Azure DevOps uses a Dockerfile with a base image from Payara Micro to create a Docker image.</span></span>  

1. <span data-ttu-id="3f128-130">Seleccione la pestaña **Tareas** para volver a la página principal de la canalización de compilación.</span><span class="sxs-lookup"><span data-stu-id="3f128-130">Select the **Tasks** tab to return back to the main build pipeline page</span></span>
2. <span data-ttu-id="3f128-131">Haga clic en el icono **+** para agregar la nueva tarea a la definición de compilación.</span><span class="sxs-lookup"><span data-stu-id="3f128-131">Click on the **+** icon to add new task to the build definition</span></span>
 
<img src="media/VSTS/Tasks-add4.png">
 
3. <span data-ttu-id="3f128-132">Seleccione "Docker" en la lista de plantillas y haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="3f128-132">Select "Docker" from the list of templates, then click on the **Add** button</span></span>
4. <span data-ttu-id="3f128-133">Escriba un nombre descriptivo para el campo **Nombre para mostrar**.</span><span class="sxs-lookup"><span data-stu-id="3f128-133">Enter a description name for the **Display name** field</span></span>
5. <span data-ttu-id="3f128-134">Compruebe que está seleccionado **Azure Container Registry** en el menú desplegable **Tipo de registro de contenedor**.</span><span class="sxs-lookup"><span data-stu-id="3f128-134">Verify that **Azure Container Registry** is selected in the drop-down menu for **Container registry type**.</span></span>
> [!NOTE]
>
>  <span data-ttu-id="3f128-135">Si usa Docker Hub u otro registro, seleccione "Registro de contenedor" en su lugar.</span><span class="sxs-lookup"><span data-stu-id="3f128-135">If you are using Docker Hub or another registry, select "Container Registry" instead.</span></span>  <span data-ttu-id="3f128-136">A continuación, haga clic en el botón "+ Nuevo" para proporcionar las credenciales y la información de conexión.</span><span class="sxs-lookup"><span data-stu-id="3f128-136">Then click on the "+ New" button to provide the credentials and connection information for it.</span></span> <span data-ttu-id="3f128-137">A continuación, vaya a la sección Comandos para continuar.</span><span class="sxs-lookup"><span data-stu-id="3f128-137">Then skip to the Commands section to continue.</span></span>

6. <span data-ttu-id="3f128-138">Utilice el menú desplegable **Suscripción de Azure** para seleccionar el identificador de suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="3f128-138">Use the **Azure subscription** drop-down menu to select your azure subscription ID.</span></span>  <span data-ttu-id="3f128-139">A continuación, haga clic en el botón **Autorizar**</span><span class="sxs-lookup"><span data-stu-id="3f128-139">Then click on the **Authorize** button</span></span>
7. <span data-ttu-id="3f128-140">En el menú desplegable **Registro de contenedor de Azure**, seleccione el nombre del registro que creó en Azure.</span><span class="sxs-lookup"><span data-stu-id="3f128-140">In the **Azure container registry** drop-down menu, select registry name you created in Azure.</span></span>
8. <span data-ttu-id="3f128-141">Compruebe que está seleccionada la opción **Compilar** en el menú desplegable **Comando**.</span><span class="sxs-lookup"><span data-stu-id="3f128-141">Verify that **build** option is selected in the **Command** drop-down menu.</span></span>
9. <span data-ttu-id="3f128-142">Para el campo **Dockerfile**, haga clic en el icono de la ruta de acceso junto al cuadro de texto para seleccionar el archivo Dockerfile del proyecto de Github.</span><span class="sxs-lookup"><span data-stu-id="3f128-142">For the **Dockerfile**, click on the path navigation icon next to the textbox to select the Dockerfile from the github project.</span></span>  <span data-ttu-id="3f128-143">A continuación, haga clic en el botón **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="3f128-143">Then click the **OK** button.</span></span>

<img src="media/VSTS/Dockerfile5.png">

10. <span data-ttu-id="3f128-144">En **Nombre de la imagen**, active la casilla de verificación **Incluir última etiqueta**.</span><span class="sxs-lookup"><span data-stu-id="3f128-144">Under the **Image name**, check the **Include latest tag** checkbox.</span></span> 
11. <span data-ttu-id="3f128-145">Use el menú desplegable **Guardar y poner en cola** para seleccionar la opción **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="3f128-145">Use the **Save & queue** drop-down menu to select the **Save** option.</span></span>

## <a name="push-docker-image-to-acr"></a><span data-ttu-id="3f128-146">Inserción de una imagen de Docker en ACR</span><span class="sxs-lookup"><span data-stu-id="3f128-146">Push Docker Image to ACR</span></span>

<span data-ttu-id="3f128-147">En esta tarea, Azure DevOps insertará la imagen de Docker en la instancia de Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="3f128-147">In this task, Azure DevOps will push the docker image to your Azure Container Registry.</span></span>  <span data-ttu-id="3f128-148">Se usará para ejecutar la aplicación de MicroProfile API como una aplicación web de Java en contenedores.</span><span class="sxs-lookup"><span data-stu-id="3f128-148">This will be used to run the MicroProfile API application as a containerized Java web app.</span></span>

1. <span data-ttu-id="3f128-149">Puesto que estamos usando Docker en Azure DevOps, repita los pasos 1 a 7 anteriores de la sección **Creación de una imagen de compilación de Docker** para crear una nueva plantilla de Docker.</span><span class="sxs-lookup"><span data-stu-id="3f128-149">Since we are using Docker in Azure DevOps, create a new Docker template by repeating steps 1 - 7 above in the **Create a Docker Build Image** section.</span></span>
2. <span data-ttu-id="3f128-150">Seleccione **Insertar** en el menú desplegable **Comando**.</span><span class="sxs-lookup"><span data-stu-id="3f128-150">Select **push** in the **Command** drop-down menu.</span></span>
3. <span data-ttu-id="3f128-151">Haga clic en la pestaña **Guardar y poner en cola** y, a continuación, seleccione la opción **Guardar y poner en cola**.</span><span class="sxs-lookup"><span data-stu-id="3f128-151">Click on the **Save & queue** tab, then select **Save & queue** option.</span></span>
4. <span data-ttu-id="3f128-152">Compruebe que está seleccionado **Hosted Linux Preview** en Grupo de agentes en la ventana emergente.</span><span class="sxs-lookup"><span data-stu-id="3f128-152">Verify that the **Hosted Linux Preview** is select for the Agent pool on the pop-up window.</span></span>  <span data-ttu-id="3f128-153">A continuación, haga clic en el botón **Guardar y poner en cola**.</span><span class="sxs-lookup"><span data-stu-id="3f128-153">Then click on the **Save & queue** button.</span></span>
5. <span data-ttu-id="3f128-154">Haga clic en el número de compilación para comprobar que la canalización de compilación para el proyecto de Java ha finalizado correctamente.</span><span class="sxs-lookup"><span data-stu-id="3f128-154">Click on the build number to verify that the build pipeline for the Java project completed successfully.</span></span>

<img src="media/VSTS/Build-Number6.png">
 

## <a name="create-a-release-definition-for-a-java-app"></a><span data-ttu-id="3f128-155">Creación de una definición de versión para una aplicación de Java</span><span class="sxs-lookup"><span data-stu-id="3f128-155">Create a release definition for a Java app</span></span>

<span data-ttu-id="3f128-156">La canalización de versión de Azure DevOps desencadena automáticamente la implementación de los artefactos de compilación en un entorno de destino, como por ejemplo Azure, tan pronto como el proceso de compilación finaliza correctamente.</span><span class="sxs-lookup"><span data-stu-id="3f128-156">The release pipeline in Azure DevOps automatically triggers the deployment of build artifacts to a target environment like Azure as soon as the Build process completes successfully.</span></span>   <span data-ttu-id="3f128-157">La canalización de versión se puede crear para los entornos de desarrollo, prueba, ensayo o producción.</span><span class="sxs-lookup"><span data-stu-id="3f128-157">The release pipeline can be created for dev, test, staging or production environments.</span></span>

1. <span data-ttu-id="3f128-158">Haga clic en la pestaña "Compilación y versión" en la parte superior de la página del proyecto de Azure DevOps.</span><span class="sxs-lookup"><span data-stu-id="3f128-158">Click on the "Build and release" tab on top your Azure DevOps project page.</span></span>  <span data-ttu-id="3f128-159">A continuación, seleccione el vínculo **Versiones**.</span><span class="sxs-lookup"><span data-stu-id="3f128-159">Then, select the **Releases** link.</span></span>

<img src="media/VSTS/Release-new-pipeline7.png">
 
2. <span data-ttu-id="3f128-160">Haga clic en el botón "Nueva canalización\*\*.</span><span class="sxs-lookup"><span data-stu-id="3f128-160">Click on the "New pipeline\*\* button</span></span>
3. <span data-ttu-id="3f128-161">Seleccione **Implementar una aplicación de Java en Azure App Service** en la lista de plantillas y, a continuación, haga clic en el botón **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="3f128-161">Select the **Deploy a Java app to Azure App Service** in the list of templates, then click on the **Apply** button.</span></span>

<img src="media/VSTS/deploy-java-template8.png">
 
4. <span data-ttu-id="3f128-162">Establezca un **Nombre de fase** (por ejemplo, desarrollo, prueba, ensayo o producción).</span><span class="sxs-lookup"><span data-stu-id="3f128-162">Set a **Stage name** (e.g Dev, Test, Staging or Production).</span></span>  <span data-ttu-id="3f128-163">A continuación, haga clic en el botón **X** para cerrar la ventana emergente.</span><span class="sxs-lookup"><span data-stu-id="3f128-163">Then click on the **X** button to close the pop-up window</span></span>
5. <span data-ttu-id="3f128-164">Haga clic en el botón **+ Agregar** en la sección Artefactos.</span><span class="sxs-lookup"><span data-stu-id="3f128-164">Click on the **+ Add** button in the Artifacts section.</span></span>  <span data-ttu-id="3f128-165">Esto vinculará los artefactos de la definición de compilación con esta definición de versión.</span><span class="sxs-lookup"><span data-stu-id="3f128-165">This will link artifacts from the build definition to this release definition.</span></span>  
6. <span data-ttu-id="3f128-166">Use el menú desplegable **Origen (canalización de compilación)** para seleccionar la definición de compilación.</span><span class="sxs-lookup"><span data-stu-id="3f128-166">Use the drop-down menu for the **Source (build pipeline)** to select your build definition.</span></span> <span data-ttu-id="3f128-167">A continuación, haga clic en el botón **Agregar** para continuar.</span><span class="sxs-lookup"><span data-stu-id="3f128-167">Then click the **Add** button to continue.</span></span>

<img src="media/VSTS/add-artifact9.png">
 
7. <span data-ttu-id="3f128-168">Haga clic en la pestaña **Tareas** de la canalización.</span><span class="sxs-lookup"><span data-stu-id="3f128-168">Click on the **Tasks** tab on the pipeline.</span></span>  <span data-ttu-id="3f128-169">A continuación, seleccione el nombre de fase.</span><span class="sxs-lookup"><span data-stu-id="3f128-169">Then, select your stage name.</span></span>
 
<img src="media/VSTS/release-stage10.png">

8. <span data-ttu-id="3f128-170">Utilice el menú desplegable **Suscripción de Azure** para seleccionar el identificador de suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="3f128-170">Use the **Azure subscription** drop-down menu to select your azure subscription ID.</span></span>
9. <span data-ttu-id="3f128-171">Seleccione **Aplicación Linux** en el menú desplegable **Tipo de aplicación**</span><span class="sxs-lookup"><span data-stu-id="3f128-171">Select **Linux App** from the **App type** drop-down menu</span></span>
10. <span data-ttu-id="3f128-172">Seleccione el nombre de la instancia de Web App for Containers que creó anteriormente en el menú desplegable **Nombre de App Service**.</span><span class="sxs-lookup"><span data-stu-id="3f128-172">Select the name of the Web App for Container instance you created above in the **App service name** drop-down menu</span></span>
11. <span data-ttu-id="3f128-173">Escriba el nombre de la instancia de Azure Container Registry en el campo **Registro o espacio de nombres**.</span><span class="sxs-lookup"><span data-stu-id="3f128-173">Enter the name of your azure container registry in the **Registry or Namespaces** field.</span></span>  <span data-ttu-id="3f128-174">Por ejemplo, **myregistry.azure.io**</span><span class="sxs-lookup"><span data-stu-id="3f128-174">E.g **myregistry.azure.io**</span></span>
12. <span data-ttu-id="3f128-175">Escriba el nombre del registro en el campo **Repositorio**.</span><span class="sxs-lookup"><span data-stu-id="3f128-175">Enter the registry name in the **Repository** field</span></span>
13. <span data-ttu-id="3f128-176">Haga clic en **Implementar Azure App Service**.</span><span class="sxs-lookup"><span data-stu-id="3f128-176">Click on **Deploy Azure App Service**.</span></span>  <span data-ttu-id="3f128-177">Escriba la etiqueta de la imagen de contenedor en el cuadro de texto **Etiqueta**.</span><span class="sxs-lookup"><span data-stu-id="3f128-177">Enter the tag for the container image in the **Tag** textbox</span></span> 
14. <span data-ttu-id="3f128-178">Haga clic en **Ejecutar en el agente**.</span><span class="sxs-lookup"><span data-stu-id="3f128-178">Click on **Run on agent**.</span></span>  <span data-ttu-id="3f128-179">Seleccione **Hosted Linux Preview** en el menú desplegable Grupo de agentes.</span><span class="sxs-lookup"><span data-stu-id="3f128-179">Select **Hosted Linux Preview** in the Agent pool drop-down menu</span></span> 

## <a name="setup-environment-variables"></a><span data-ttu-id="3f128-180">Configuración de las variables de entorno</span><span class="sxs-lookup"><span data-stu-id="3f128-180">Setup Environment Variables</span></span>

1. <span data-ttu-id="3f128-181">Haga clic en la pestaña **Variables**.  A continuación, haga clic en el botón **+ Agregar** para definir las variables de entorno.</span><span class="sxs-lookup"><span data-stu-id="3f128-181">Click on the **Variables** tab.  Then click on the **+ Add** button to define your environment variables</span></span>
2. <span data-ttu-id="3f128-182">Agregue el nombre de variable y sus valores para la dirección URL del registro de contenedor, el nombre de usuario y la contraseña.</span><span class="sxs-lookup"><span data-stu-id="3f128-182">Add the variable name and values for your container registry url, username and password.</span></span>   <span data-ttu-id="3f128-183">Por seguridad, haga clic en el icono de candado para mantener oculto el valor de la contraseña.</span><span class="sxs-lookup"><span data-stu-id="3f128-183">For security, click on the lock icon to keep the password value hidden.</span></span>

<span data-ttu-id="3f128-184">Por ejemplo: </span><span class="sxs-lookup"><span data-stu-id="3f128-184">For example:</span></span>
- <span data-ttu-id="3f128-185">registry.password</span><span class="sxs-lookup"><span data-stu-id="3f128-185">registry.password</span></span>
- <span data-ttu-id="3f128-186">registry.url</span><span class="sxs-lookup"><span data-stu-id="3f128-186">registry.url</span></span>
- <span data-ttu-id="3f128-187">registry.username</span><span class="sxs-lookup"><span data-stu-id="3f128-187">registry.username</span></span>

<img src="media/VSTS/environment-variables12.png">

3. <span data-ttu-id="3f128-188">Haga clic en la pestaña **Tareas** para volver a la página principal de la definición de canalización de versión</span><span class="sxs-lookup"><span data-stu-id="3f128-188">Click on the **Tasks** tab to return to the main release pipeline definition page</span></span>
4. <span data-ttu-id="3f128-189">Haga clic en **Implementar Azure App Service**.</span><span class="sxs-lookup"><span data-stu-id="3f128-189">Click on **Deploy Azure App Service**.</span></span> 
5. <span data-ttu-id="3f128-190">Expanda la sección **Configuración y opciones de la aplicación** y, a continuación, haga clic en la ruta de navegación del campo **Configuración de la aplicación** para agregar las variables de entorno para la conexión al registro de contenedor durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="3f128-190">Expand the **Application and Configuration Settings** section, then click on the navigation path for the **App Settings** field to add environments variable to connect to the container registry during deployment.</span></span>
6. <span data-ttu-id="3f128-191">Haga clic en el botón \*\* + Agregar\*\* para definir la siguiente configuración de la aplicación y asignar las variables de entorno.</span><span class="sxs-lookup"><span data-stu-id="3f128-191">Click on the \*\* + Add\*\* button to define the following app settings and assign the environment variables</span></span>
- <span data-ttu-id="3f128-192">DOCKER_REGISTRY_SERVER_PASSWORD = $(registry.password)</span><span class="sxs-lookup"><span data-stu-id="3f128-192">DOCKER_REGISTRY_SERVER_PASSWORD = $(registry.password)</span></span>
- <span data-ttu-id="3f128-193">DOCKER_REGISTRY_SERVER_URL = $(registry.url)</span><span class="sxs-lookup"><span data-stu-id="3f128-193">DOCKER_REGISTRY_SERVER_URL = $(registry.url)</span></span>
- <span data-ttu-id="3f128-194">DOCKER_REGISTRY_SERVER_USERNAME = $(registry.username)</span><span class="sxs-lookup"><span data-stu-id="3f128-194">DOCKER_REGISTRY_SERVER_USERNAME = $(registry.username)</span></span>

<img src="media/VSTS/environment-variables14.png">
 
7. <span data-ttu-id="3f128-195">Haga clic en el botón **Aceptar** para continuar.</span><span class="sxs-lookup"><span data-stu-id="3f128-195">Click on the **OK** button to continue</span></span>

## <a name="setup-continious-deployment--deploy-java-application"></a><span data-ttu-id="3f128-196">Configuración de la implementación continua e implementación de la aplicación de Java</span><span class="sxs-lookup"><span data-stu-id="3f128-196">Setup Continious Deployment & Deploy Java Application</span></span>

1. <span data-ttu-id="3f128-197">Para habilitar la implementación continua, haga clic en la pestaña **Canalizaciones**.</span><span class="sxs-lookup"><span data-stu-id="3f128-197">To enable continuous deployment, click the **Pipelines** tab</span></span>
2. <span data-ttu-id="3f128-198">En la sección Artefactos, haga clic en el icono de rayo que aparece.</span><span class="sxs-lookup"><span data-stu-id="3f128-198">In the Artifacts section, click on the lightening icon.</span></span>  <span data-ttu-id="3f128-199">A continuación, establezca el **Desencadenador de implementación continua** en habilitado.</span><span class="sxs-lookup"><span data-stu-id="3f128-199">Then set the **Continuous deployment trigger** to Enabled.</span></span>

<img src="media/VSTS/release-enable-CD.png">
 
3. <span data-ttu-id="3f128-200">Haga clic en el botón **Guardar** y, a continuación, en el botón **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="3f128-200">Click on the **Save** button, then the **OK** button</span></span> 
4. <span data-ttu-id="3f128-201">Haga clic en el menú desplegable **+ Versión** y, a continuación, seleccione el vínculo **Crear una versión**.</span><span class="sxs-lookup"><span data-stu-id="3f128-201">Click on the **+ Release** drop-down menu, then select **Create a release** link</span></span>
5. <span data-ttu-id="3f128-202">Use el menú desplegable **Fases para un cambio de desencadenador de automático a manual** para seleccionar la casilla de verificación del nombre de fase.</span><span class="sxs-lookup"><span data-stu-id="3f128-202">Use the **Stages for a trigger change from automated to manual** drop-down menu to select the checkbox for your stage name</span></span>
6. <span data-ttu-id="3f128-203">Haga clic en el botón **Crear** para continuar.</span><span class="sxs-lookup"><span data-stu-id="3f128-203">Click the **Create** button to continue</span></span>
7. <span data-ttu-id="3f128-204">Haga clic en el número de versión.</span><span class="sxs-lookup"><span data-stu-id="3f128-204">Click on the release number.</span></span>  <span data-ttu-id="3f128-205">A continuación, mantenga el cursor del mouse sobre el nombre de fase y haga clic en el botón **Implementar**.</span><span class="sxs-lookup"><span data-stu-id="3f128-205">Then hover your mouse cursor over the stage name and click on the **Deploy** button</span></span>
8. <span data-ttu-id="3f128-206">A continuación, haga clic en el botón **Implementar** en la ventana emergente para iniciar el proceso de implementación en Azure.</span><span class="sxs-lookup"><span data-stu-id="3f128-206">The click on the **Deploy** button on the pop-up window to start the deployment process to Azure</span></span>


## <a name="test-the-java-web-application"></a><span data-ttu-id="3f128-207">Prueba de la aplicación web de Java</span><span class="sxs-lookup"><span data-stu-id="3f128-207">Test the Java Web Application</span></span>
1. <span data-ttu-id="3f128-208">Ejecute la dirección URL de la aplicación web en el explorador web:</span><span class="sxs-lookup"><span data-stu-id="3f128-208">Run the web app url in web browser:</span></span>  
<span data-ttu-id="3f128-209">https://{nombre-de-app-service}.azurewebsites.net/api/hello</span><span class="sxs-lookup"><span data-stu-id="3f128-209">https://{your-app-service-name}.azurewebsites.net/api/hello</span></span>

 
<img src="media/VSTS/web-app16.png">

2. <span data-ttu-id="3f128-210">En la página web debe aparecer **Hello Azure!**</span><span class="sxs-lookup"><span data-stu-id="3f128-210">The web page should say **Hello Azure!**</span></span>
 
<img src="media/VSTS/web-api17.png">
