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
ms.openlocfilehash: 818e37291fa47f99cb161c63a86062bddbf6248c
ms.sourcegitcommit: 4d52e47073fb0b3ac40a2689daea186bad5b1ef5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/23/2018
ms.locfileid: "49799941"
---
# <a name="cicd-for-microprofile-applications-using-azure-devops"></a><span data-ttu-id="988fd-103">CI/CD para aplicaciones de MicroProfile con Azure DevOps</span><span class="sxs-lookup"><span data-stu-id="988fd-103">CI/CD for MicroProfile applications using Azure DevOps</span></span>

<span data-ttu-id="988fd-104">Este tutorial muestra cómo pueden los desarrolladores de Java EE configurar fácilmente un ciclo de versión de CI/CD para implementar sus aplicaciones de [MicroProfile](http://microprofile.io) en Azure Web App for Containers con Azure DevOps (anteriormente conocido como VSTS).</span><span class="sxs-lookup"><span data-stu-id="988fd-104">This tutorial will show how Java EE developers can easily setup a CI/CD release cycle to deploy their [MicroProfile](http://microprofile.io) applications to an Azure Web App for Containers using Azure DevOps (formally known as VSTS).</span></span>  <span data-ttu-id="988fd-105">En este ejemplo, vamos a usar una aplicación de MicroProfile que usa [Payara Micro](https://www.payara.fish/payara_micro) como imagen base.</span><span class="sxs-lookup"><span data-stu-id="988fd-105">In this example, we’ll be using a MicroProfile application that uses a [Payara Micro](https://www.payara.fish/payara_micro) as a base image.</span></span>   

```Dockerfile
FROM payara/micro:5.182
COPY target/*.war $DEPLOY_DIR/ROOT.war
EXPOSE 8080
```
<span data-ttu-id="988fd-106">El proceso de inclusión en contenedores de Azure DevOps se inicia con la creación de una imagen de Docker y la inserción de la imagen de contenedor en Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="988fd-106">We will start the Azure DevOps containerize process by building a Docker image and pushing the container image to an Azure Container Register.</span></span>  <span data-ttu-id="988fd-107">A continuación, se completará con una canalización de versión de Azure DevOps para implementar la imagen de contenedor en una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="988fd-107">Then complete with a Azure DevOps release pipeline to deploy the container image to a Web App.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="988fd-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="988fd-108">Prerequisites</span></span>
- <span data-ttu-id="988fd-109">Copie y guarde la dirección URL de Git desde [Github](https://github.com/Azure-Samples/microprofile-hello-azure).</span><span class="sxs-lookup"><span data-stu-id="988fd-109">Copy and save the Git url from [Github](https://github.com/Azure-Samples/microprofile-hello-azure)</span></span>
- <span data-ttu-id="988fd-110">Regístrese o inicie sesión en su cuenta de [Azure DevOps](https://dev.azure.com).</span><span class="sxs-lookup"><span data-stu-id="988fd-110">Register or Log into your [Azure DevOps](https://dev.azure.com) account</span></span>
- <span data-ttu-id="988fd-111">Cree un nuevo [proyecto de Azure DevOps](https://docs.microsoft.com/en-us/vsts/organizations/projects/create-project?view=vsts&tabs=new-nav) y use la dirección URL de Git anterior para **importar un repositorio**.</span><span class="sxs-lookup"><span data-stu-id="988fd-111">Create a new [Azure DevOps project](https://docs.microsoft.com/en-us/vsts/organizations/projects/create-project?view=vsts&tabs=new-nav) and use the above Git url to **import a repository**</span></span>
- <span data-ttu-id="988fd-112">Cree una instancia de [Azure Container Registry](https://azure.microsoft.com/en-us/services/container-registry) (ACR).</span><span class="sxs-lookup"><span data-stu-id="988fd-112">Create an [Azure Container Registry](https://azure.microsoft.com/en-us/services/container-registry) (ACR)</span></span>
- <span data-ttu-id="988fd-113">Cree una instancia de Azure Web App for Containers.</span><span class="sxs-lookup"><span data-stu-id="988fd-113">Create an Azure Web App for Container</span></span>
  > [!NOTE]
  >
  > <span data-ttu-id="988fd-114">Seleccione "Inicio rápido" en la configuración del contenedor al aprovisionar la instancia de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="988fd-114">Select "Quickstart" in the Container Settings when provisioning the Web App instance</span></span>


## <a name="create-a-build-definition"></a><span data-ttu-id="988fd-115">Creación de una definición de compilación</span><span class="sxs-lookup"><span data-stu-id="988fd-115">Create a Build definition</span></span>

<span data-ttu-id="988fd-116">La definición de compilación de Azure DevOps ejecuta automáticamente todas las tareas de la compilación cada vez que hay una confirmación en el código fuente de la aplicación de Java EE.</span><span class="sxs-lookup"><span data-stu-id="988fd-116">The build definition in Azure DevOps automatically executes all the tasks in the build each time there’s a commit in Java EE application source application.</span></span>  <span data-ttu-id="988fd-117">En este ejemplo, Azure DevOps usa Maven para compilar el proyecto de MicroProfile de Java.</span><span class="sxs-lookup"><span data-stu-id="988fd-117">In this example, Azure DevOps will use Maven to build the Java MicroProfile project.</span></span>

1. <span data-ttu-id="988fd-118">Haga clic en la pestaña "Compilación y versión" en la parte superior de la página del proyecto de Azure DevOps.</span><span class="sxs-lookup"><span data-stu-id="988fd-118">Click on the "Build and Release" tab on top your Azure DevOps project page.</span></span>  <span data-ttu-id="988fd-119">A continuación, seleccione el vínculo **Compilaciones**.</span><span class="sxs-lookup"><span data-stu-id="988fd-119">Then, select the **Builds** link</span></span> 

<img src="media/VSTS/Buid-and-Release1.png">

2. <span data-ttu-id="988fd-120">Haga clic en el botón **Nueva canalización** y, a continuación, en **Continuar** para comenzar a definir las tareas de compilación.</span><span class="sxs-lookup"><span data-stu-id="988fd-120">Click on the **New Pipeline** button, and then **Continue** to start defining your build tasks</span></span>
3. <span data-ttu-id="988fd-121">Seleccione "Maven" en la lista de plantillas y haga clic en el botón **Aplicar** para compilar el proyecto de Java.</span><span class="sxs-lookup"><span data-stu-id="988fd-121">Select "Maven" from the list of templates, then click on the **Apply** button to build your Java project</span></span>
4. <span data-ttu-id="988fd-122">Use el menú desplegable del campo Grupo de agentes para seleccionar la opción **Hosted Linux Preview**.</span><span class="sxs-lookup"><span data-stu-id="988fd-122">Use the drop-down menu for the Agent pool field to select **Hosted Linux Preview** option.</span></span>
   > [!NOTE]
   >
   > <span data-ttu-id="988fd-123">Esto informa a Azure DevOps sobre qué servidor de compilación se va a utilizar.</span><span class="sxs-lookup"><span data-stu-id="988fd-123">This informs Azure DevOps which build server to use.</span></span>  <span data-ttu-id="988fd-124">Puede usar un servidor de compilación personalizado privado.</span><span class="sxs-lookup"><span data-stu-id="988fd-124">You can use your private customized build server</span></span>

5. <span data-ttu-id="988fd-125">Para configurar la compilación para la integración continua, seleccione la pestaña **Desencadenadores** y active la casilla de verificación **Habilitar la integración continua**.</span><span class="sxs-lookup"><span data-stu-id="988fd-125">To configure your build for continuous integration, select the **Triggers** tab and check the **Enable continuous integration** checkbox.</span></span>  

<img src="media/VSTS/Build-Triggers2.png"> 

6. <span data-ttu-id="988fd-126">Seleccione la pestaña <strong>Tareas</strong> para volver a la página principal de la canalización de compilación.</span><span class="sxs-lookup"><span data-stu-id="988fd-126">Select the <strong>Tasks</strong> tab to return back to the main build pipeline page</span></span>
7. <span data-ttu-id="988fd-127">Use el menú desplegable <strong>Guardar y poner en cola&amp;</strong> y seleccione la opción <strong>Guardar</strong>.</span><span class="sxs-lookup"><span data-stu-id="988fd-127">Use the <strong>Save &amp; queue</strong> drop-down menu to select the <strong>Save</strong> option</span></span>


## <a name="create-a-docker-build-image"></a><span data-ttu-id="988fd-128">Creación de una imagen de compilación de Docker</span><span class="sxs-lookup"><span data-stu-id="988fd-128">Create a Docker Build Image</span></span>

<span data-ttu-id="988fd-129">En esta tarea, Azure DevOps usa un Dockerfile con una imagen base de Payara Micro para crear una imagen de Docker.</span><span class="sxs-lookup"><span data-stu-id="988fd-129">In this task, Azure DevOps uses a Dockerfile with a base image from Payara Micro to create a Docker image.</span></span>  

1. <span data-ttu-id="988fd-130">Seleccione la pestaña **Tareas** para volver a la página principal de la canalización de compilación.</span><span class="sxs-lookup"><span data-stu-id="988fd-130">Select the **Tasks** tab to return back to the main build pipeline page</span></span>
2. <span data-ttu-id="988fd-131">Haga clic en el icono **+** para agregar la nueva tarea a la definición de compilación.</span><span class="sxs-lookup"><span data-stu-id="988fd-131">Click on the **+** icon to add new task to the build definition</span></span>

<img src="media/VSTS/Tasks-add4.png">

3. <span data-ttu-id="988fd-132">Seleccione &quot;Docker&quot; en la lista de plantillas y haga clic en el botón <strong>Agregar</strong>.</span><span class="sxs-lookup"><span data-stu-id="988fd-132">Select &quot;Docker&quot; from the list of templates, then click on the <strong>Add</strong> button</span></span>
4. <span data-ttu-id="988fd-133">Escriba un nombre descriptivo para el campo <strong>Nombre para mostrar</strong>.</span><span class="sxs-lookup"><span data-stu-id="988fd-133">Enter a description name for the <strong>Display name</strong> field</span></span>
5. <span data-ttu-id="988fd-134">Compruebe que está seleccionado <strong>Azure Container Registry</strong> en el menú desplegable <strong>Tipo de registro de contenedor</strong>.</span><span class="sxs-lookup"><span data-stu-id="988fd-134">Verify that <strong>Azure Container Registry</strong> is selected in the drop-down menu for <strong>Container registry type</strong>.</span></span>
<span data-ttu-id="988fd-135">&gt;</span><span class="sxs-lookup"><span data-stu-id="988fd-135">&gt;</span></span> [!NOTE]
<span data-ttu-id="988fd-136">&gt; &gt; Si usa Docker Hub u otro registro, seleccione &quot;Registro de contenedor&quot; en su lugar.</span><span class="sxs-lookup"><span data-stu-id="988fd-136">&gt; &gt;  If you are using Docker Hub or another registry, select &quot;Container Registry&quot; instead.</span></span>  <span data-ttu-id="988fd-137">A continuación, haga clic en el botón &quot;+ Nuevo&quot; para proporcionar las credenciales y la información de conexión.</span><span class="sxs-lookup"><span data-stu-id="988fd-137">Then click on the &quot;+ New&quot; button to provide the credentials and connection information for it.</span></span> <span data-ttu-id="988fd-138">A continuación, vaya a la sección Comandos para continuar.</span><span class="sxs-lookup"><span data-stu-id="988fd-138">Then skip to the Commands section to continue.</span></span>

6. <span data-ttu-id="988fd-139">Utilice el menú desplegable **Suscripción de Azure** para seleccionar el identificador de suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="988fd-139">Use the **Azure subscription** drop-down menu to select your azure subscription ID.</span></span>  <span data-ttu-id="988fd-140">A continuación, haga clic en el botón **Autorizar**</span><span class="sxs-lookup"><span data-stu-id="988fd-140">Then click on the **Authorize** button</span></span>
7. <span data-ttu-id="988fd-141">En el menú desplegable **Registro de contenedor de Azure**, seleccione el nombre del registro que creó en Azure.</span><span class="sxs-lookup"><span data-stu-id="988fd-141">In the **Azure container registry** drop-down menu, select registry name you created in Azure.</span></span>
8. <span data-ttu-id="988fd-142">Compruebe que está seleccionada la opción **Compilar** en el menú desplegable **Comando**.</span><span class="sxs-lookup"><span data-stu-id="988fd-142">Verify that **build** option is selected in the **Command** drop-down menu.</span></span>
9. <span data-ttu-id="988fd-143">Para el campo **Dockerfile**, haga clic en el icono de la ruta de acceso junto al cuadro de texto para seleccionar el archivo Dockerfile del proyecto de Github.</span><span class="sxs-lookup"><span data-stu-id="988fd-143">For the **Dockerfile**, click on the path navigation icon next to the textbox to select the Dockerfile from the github project.</span></span>  <span data-ttu-id="988fd-144">A continuación, haga clic en el botón **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="988fd-144">Then click the **OK** button.</span></span>

<img src="media/VSTS/Dockerfile5.png">

10. <span data-ttu-id="988fd-145">En **Nombre de la imagen**, active la casilla de verificación **Incluir última etiqueta**.</span><span class="sxs-lookup"><span data-stu-id="988fd-145">Under the **Image name**, check the **Include latest tag** checkbox.</span></span> 
11. <span data-ttu-id="988fd-146">Use el menú desplegable **Guardar y poner en cola** para seleccionar la opción **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="988fd-146">Use the **Save & queue** drop-down menu to select the **Save** option.</span></span>

## <a name="push-docker-image-to-acr"></a><span data-ttu-id="988fd-147">Inserción de una imagen de Docker en ACR</span><span class="sxs-lookup"><span data-stu-id="988fd-147">Push Docker Image to ACR</span></span>

<span data-ttu-id="988fd-148">En esta tarea, Azure DevOps insertará la imagen de Docker en la instancia de Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="988fd-148">In this task, Azure DevOps will push the docker image to your Azure Container Registry.</span></span>  <span data-ttu-id="988fd-149">Se usará para ejecutar la aplicación de MicroProfile API como una aplicación web de Java en contenedores.</span><span class="sxs-lookup"><span data-stu-id="988fd-149">This will be used to run the MicroProfile API application as a containerized Java web app.</span></span>

1. <span data-ttu-id="988fd-150">Puesto que estamos usando Docker en Azure DevOps, repita los pasos 1 a 7 anteriores de la sección **Creación de una imagen de compilación de Docker** para crear una nueva plantilla de Docker.</span><span class="sxs-lookup"><span data-stu-id="988fd-150">Since we are using Docker in Azure DevOps, create a new Docker template by repeating steps 1 - 7 above in the **Create a Docker Build Image** section.</span></span>
2. <span data-ttu-id="988fd-151">Seleccione **Insertar** en el menú desplegable **Comando**.</span><span class="sxs-lookup"><span data-stu-id="988fd-151">Select **push** in the **Command** drop-down menu.</span></span>
3. <span data-ttu-id="988fd-152">Haga clic en la pestaña **Guardar y poner en cola** y, a continuación, seleccione la opción **Guardar y poner en cola**.</span><span class="sxs-lookup"><span data-stu-id="988fd-152">Click on the **Save & queue** tab, then select **Save & queue** option.</span></span>
4. <span data-ttu-id="988fd-153">Compruebe que está seleccionado **Hosted Linux Preview** en Grupo de agentes en la ventana emergente.</span><span class="sxs-lookup"><span data-stu-id="988fd-153">Verify that the **Hosted Linux Preview** is select for the Agent pool on the pop-up window.</span></span>  <span data-ttu-id="988fd-154">A continuación, haga clic en el botón **Guardar y poner en cola**.</span><span class="sxs-lookup"><span data-stu-id="988fd-154">Then click on the **Save & queue** button.</span></span>
5. <span data-ttu-id="988fd-155">Haga clic en el número de compilación para comprobar que la canalización de compilación para el proyecto de Java ha finalizado correctamente.</span><span class="sxs-lookup"><span data-stu-id="988fd-155">Click on the build number to verify that the build pipeline for the Java project completed successfully.</span></span>

<img src="media/VSTS/Build-Number6.png">


## <a name="create-a-release-definition-for-a-java-app"></a><span data-ttu-id="988fd-156">Creación de una definición de versión para una aplicación de Java</span><span class="sxs-lookup"><span data-stu-id="988fd-156">Create a release definition for a Java app</span></span>

<span data-ttu-id="988fd-157">La canalización de versión de Azure DevOps desencadena automáticamente la implementación de los artefactos de compilación en un entorno de destino, como por ejemplo Azure, tan pronto como el proceso de compilación finaliza correctamente.</span><span class="sxs-lookup"><span data-stu-id="988fd-157">The release pipeline in Azure DevOps automatically triggers the deployment of build artifacts to a target environment like Azure as soon as the Build process completes successfully.</span></span>   <span data-ttu-id="988fd-158">La canalización de versión se puede crear para los entornos de desarrollo, prueba, ensayo o producción.</span><span class="sxs-lookup"><span data-stu-id="988fd-158">The release pipeline can be created for dev, test, staging or production environments.</span></span>

1. <span data-ttu-id="988fd-159">Haga clic en la pestaña "Compilación y versión" en la parte superior de la página del proyecto de Azure DevOps.</span><span class="sxs-lookup"><span data-stu-id="988fd-159">Click on the "Build and release" tab on top your Azure DevOps project page.</span></span>  <span data-ttu-id="988fd-160">A continuación, seleccione el vínculo **Versiones**.</span><span class="sxs-lookup"><span data-stu-id="988fd-160">Then, select the **Releases** link.</span></span>

<img src="media/VSTS/Release-new-pipeline7.png">

2. <span data-ttu-id="988fd-161">Haga clic en el botón &quot;Nueva canalización\*\*</span><span class="sxs-lookup"><span data-stu-id="988fd-161">Click on the &quot;New pipeline\*\* button</span></span>
3. <span data-ttu-id="988fd-162">Seleccione <strong>Implementar una aplicación de Java en Azure App Service</strong> en la lista de plantillas y, a continuación, haga clic en el botón <strong>Aplicar</strong>.</span><span class="sxs-lookup"><span data-stu-id="988fd-162">Select the <strong>Deploy a Java app to Azure App Service</strong> in the list of templates, then click on the <strong>Apply</strong> button.</span></span>

<img src="media/VSTS/deploy-java-template8.png">

4. <span data-ttu-id="988fd-163">Establezca un <strong>Nombre de fase</strong> (por ejemplo, desarrollo, prueba, ensayo o producción).</span><span class="sxs-lookup"><span data-stu-id="988fd-163">Set a <strong>Stage name</strong> (e.g Dev, Test, Staging or Production).</span></span>  <span data-ttu-id="988fd-164">A continuación, haga clic en el botón <strong>X</strong> para cerrar la ventana emergente.</span><span class="sxs-lookup"><span data-stu-id="988fd-164">Then click on the <strong>X</strong> button to close the pop-up window</span></span>
5. <span data-ttu-id="988fd-165">Haga clic en el botón <strong>+ Agregar</strong> en la sección Artefactos.</span><span class="sxs-lookup"><span data-stu-id="988fd-165">Click on the <strong>+ Add</strong> button in the Artifacts section.</span></span>  <span data-ttu-id="988fd-166">Esto vinculará los artefactos de la definición de compilación con esta definición de versión.</span><span class="sxs-lookup"><span data-stu-id="988fd-166">This will link artifacts from the build definition to this release definition.</span></span><br/><span data-ttu-id="988fd-167">6. Use el menú desplegable <strong>Origen (canalización de compilación)</strong> para seleccionar la definición de compilación.</span><span class="sxs-lookup"><span data-stu-id="988fd-167">6. Use the drop-down menu for the <strong>Source (build pipeline)</strong> to select your build definition.</span></span> <span data-ttu-id="988fd-168">A continuación, haga clic en el botón <strong>Agregar</strong> para continuar.</span><span class="sxs-lookup"><span data-stu-id="988fd-168">Then click the <strong>Add</strong> button to continue.</span></span>

<img src="media/VSTS/add-artifact9.png">

7. <span data-ttu-id="988fd-169">Haga clic en la pestaña <strong>Tareas</strong> de la canalización.</span><span class="sxs-lookup"><span data-stu-id="988fd-169">Click on the <strong>Tasks</strong> tab on the pipeline.</span></span>  <span data-ttu-id="988fd-170">A continuación, seleccione el nombre de fase.</span><span class="sxs-lookup"><span data-stu-id="988fd-170">Then, select your stage name.</span></span>

<img src="media/VSTS/release-stage10.png">

8. <span data-ttu-id="988fd-171">Utilice el menú desplegable **Suscripción de Azure** para seleccionar el identificador de suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="988fd-171">Use the **Azure subscription** drop-down menu to select your azure subscription ID.</span></span>
9. <span data-ttu-id="988fd-172">Seleccione **Aplicación Linux** en el menú desplegable **Tipo de aplicación**</span><span class="sxs-lookup"><span data-stu-id="988fd-172">Select **Linux App** from the **App type** drop-down menu</span></span>
10. <span data-ttu-id="988fd-173">Seleccione el nombre de la instancia de Web App for Containers que creó anteriormente en el menú desplegable **Nombre de App Service**.</span><span class="sxs-lookup"><span data-stu-id="988fd-173">Select the name of the Web App for Container instance you created above in the **App service name** drop-down menu</span></span>
11. <span data-ttu-id="988fd-174">Escriba el nombre de la instancia de Azure Container Registry en el campo **Registro o espacio de nombres**.</span><span class="sxs-lookup"><span data-stu-id="988fd-174">Enter the name of your azure container registry in the **Registry or Namespaces** field.</span></span>  <span data-ttu-id="988fd-175">Por ejemplo, **myregistry.azure.io**</span><span class="sxs-lookup"><span data-stu-id="988fd-175">E.g **myregistry.azure.io**</span></span>
12. <span data-ttu-id="988fd-176">Escriba el nombre del registro en el campo **Repositorio**.</span><span class="sxs-lookup"><span data-stu-id="988fd-176">Enter the registry name in the **Repository** field</span></span>
13. <span data-ttu-id="988fd-177">Haga clic en **Implementar Azure App Service**.</span><span class="sxs-lookup"><span data-stu-id="988fd-177">Click on **Deploy Azure App Service**.</span></span>  <span data-ttu-id="988fd-178">Escriba la etiqueta de la imagen de contenedor en el cuadro de texto **Etiqueta**.</span><span class="sxs-lookup"><span data-stu-id="988fd-178">Enter the tag for the container image in the **Tag** textbox</span></span> 
14. <span data-ttu-id="988fd-179">Haga clic en **Ejecutar en el agente**.</span><span class="sxs-lookup"><span data-stu-id="988fd-179">Click on **Run on agent**.</span></span>  <span data-ttu-id="988fd-180">Seleccione **Hosted Linux Preview** en el menú desplegable Grupo de agentes.</span><span class="sxs-lookup"><span data-stu-id="988fd-180">Select **Hosted Linux Preview** in the Agent pool drop-down menu</span></span> 

## <a name="setup-environment-variables"></a><span data-ttu-id="988fd-181">Configuración de las variables de entorno</span><span class="sxs-lookup"><span data-stu-id="988fd-181">Setup Environment Variables</span></span>

1. <span data-ttu-id="988fd-182">Haga clic en la pestaña **Variables**.  A continuación, haga clic en el botón **+ Agregar** para definir las variables de entorno.</span><span class="sxs-lookup"><span data-stu-id="988fd-182">Click on the **Variables** tab.  Then click on the **+ Add** button to define your environment variables</span></span>
2. <span data-ttu-id="988fd-183">Agregue el nombre de variable y sus valores para la dirección URL del registro de contenedor, el nombre de usuario y la contraseña.</span><span class="sxs-lookup"><span data-stu-id="988fd-183">Add the variable name and values for your container registry url, username and password.</span></span>   <span data-ttu-id="988fd-184">Por seguridad, haga clic en el icono de candado para mantener oculto el valor de la contraseña.</span><span class="sxs-lookup"><span data-stu-id="988fd-184">For security, click on the lock icon to keep the password value hidden.</span></span>

<span data-ttu-id="988fd-185">Por ejemplo: </span><span class="sxs-lookup"><span data-stu-id="988fd-185">For example:</span></span>
- <span data-ttu-id="988fd-186">registry.password</span><span class="sxs-lookup"><span data-stu-id="988fd-186">registry.password</span></span>
- <span data-ttu-id="988fd-187">registry.url</span><span class="sxs-lookup"><span data-stu-id="988fd-187">registry.url</span></span>
- <span data-ttu-id="988fd-188">registry.username</span><span class="sxs-lookup"><span data-stu-id="988fd-188">registry.username</span></span>

<img src="media/VSTS/environment-variables12.png">

3. <span data-ttu-id="988fd-189">Haga clic en la pestaña **Tareas** para volver a la página principal de la definición de canalización de versión</span><span class="sxs-lookup"><span data-stu-id="988fd-189">Click on the **Tasks** tab to return to the main release pipeline definition page</span></span>
4. <span data-ttu-id="988fd-190">Haga clic en **Implementar Azure App Service**.</span><span class="sxs-lookup"><span data-stu-id="988fd-190">Click on **Deploy Azure App Service**.</span></span> 
5. <span data-ttu-id="988fd-191">Expanda la sección **Configuración y opciones de la aplicación** y, a continuación, haga clic en la ruta de navegación del campo **Configuración de la aplicación** para agregar las variables de entorno para la conexión al registro de contenedor durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="988fd-191">Expand the **Application and Configuration Settings** section, then click on the navigation path for the **App Settings** field to add environments variable to connect to the container registry during deployment.</span></span>
6. <span data-ttu-id="988fd-192">Haga clic en el botón \*\* + Agregar\*\* para definir la siguiente configuración de la aplicación y asignar las variables de entorno.</span><span class="sxs-lookup"><span data-stu-id="988fd-192">Click on the \*\* + Add\*\* button to define the following app settings and assign the environment variables</span></span>
7. <span data-ttu-id="988fd-193">DOCKER_REGISTRY_SERVER_PASSWORD = $(registry.password)</span><span class="sxs-lookup"><span data-stu-id="988fd-193">DOCKER_REGISTRY_SERVER_PASSWORD = $(registry.password)</span></span>
8. <span data-ttu-id="988fd-194">DOCKER_REGISTRY_SERVER_URL = $(registry.url)</span><span class="sxs-lookup"><span data-stu-id="988fd-194">DOCKER_REGISTRY_SERVER_URL = $(registry.url)</span></span>
9. <span data-ttu-id="988fd-195">DOCKER_REGISTRY_SERVER_USERNAME = $(registry.username)</span><span class="sxs-lookup"><span data-stu-id="988fd-195">DOCKER_REGISTRY_SERVER_USERNAME = $(registry.username)</span></span>

<img src="media/VSTS/environment-variables14.png">

7. <span data-ttu-id="988fd-196">Haga clic en el botón <strong>Aceptar</strong> para continuar.</span><span class="sxs-lookup"><span data-stu-id="988fd-196">Click on the <strong>OK</strong> button to continue</span></span>

## <a name="setup-continious-deployment--deploy-java-application"></a><span data-ttu-id="988fd-197">Configuración de la implementación continua e implementación de la aplicación de Java</span><span class="sxs-lookup"><span data-stu-id="988fd-197">Setup Continious Deployment & Deploy Java Application</span></span>

1. <span data-ttu-id="988fd-198">Para habilitar la implementación continua, haga clic en la pestaña **Canalizaciones**.</span><span class="sxs-lookup"><span data-stu-id="988fd-198">To enable continuous deployment, click the **Pipelines** tab</span></span>
2. <span data-ttu-id="988fd-199">En la sección Artefactos, haga clic en el icono de rayo que aparece.</span><span class="sxs-lookup"><span data-stu-id="988fd-199">In the Artifacts section, click on the lightening icon.</span></span>  <span data-ttu-id="988fd-200">A continuación, establezca el **Desencadenador de implementación continua** en habilitado.</span><span class="sxs-lookup"><span data-stu-id="988fd-200">Then set the **Continuous deployment trigger** to Enabled.</span></span>

<img src="media/VSTS/release-enable-CD.png">

3. <span data-ttu-id="988fd-201">Haga clic en el botón <strong>Guardar</strong> y, a continuación, en el botón <strong>Aceptar</strong>.</span><span class="sxs-lookup"><span data-stu-id="988fd-201">Click on the <strong>Save</strong> button, then the <strong>OK</strong> button</span></span> 
4. <span data-ttu-id="988fd-202">Haga clic en el menú desplegable <strong>+ Versión</strong> y, a continuación, seleccione el vínculo <strong>Crear una versión</strong>.</span><span class="sxs-lookup"><span data-stu-id="988fd-202">Click on the <strong>+ Release</strong> drop-down menu, then select <strong>Create a release</strong> link</span></span>
5. <span data-ttu-id="988fd-203">Use el menú desplegable <strong>Fases para un cambio de desencadenador de automático a manual</strong> para seleccionar la casilla de verificación del nombre de fase.</span><span class="sxs-lookup"><span data-stu-id="988fd-203">Use the <strong>Stages for a trigger change from automated to manual</strong> drop-down menu to select the checkbox for your stage name</span></span>
6. <span data-ttu-id="988fd-204">Haga clic en el botón <strong>Crear</strong> para continuar.</span><span class="sxs-lookup"><span data-stu-id="988fd-204">Click the <strong>Create</strong> button to continue</span></span>
7. <span data-ttu-id="988fd-205">Haga clic en el número de versión.</span><span class="sxs-lookup"><span data-stu-id="988fd-205">Click on the release number.</span></span>  <span data-ttu-id="988fd-206">A continuación, mantenga el cursor del mouse sobre el nombre de fase y haga clic en el botón <strong>Implementar</strong>.</span><span class="sxs-lookup"><span data-stu-id="988fd-206">Then hover your mouse cursor over the stage name and click on the <strong>Deploy</strong> button</span></span>
8. <span data-ttu-id="988fd-207">A continuación, haga clic en el botón <strong>Implementar</strong> en la ventana emergente para iniciar el proceso de implementación en Azure.</span><span class="sxs-lookup"><span data-stu-id="988fd-207">The click on the <strong>Deploy</strong> button on the pop-up window to start the deployment process to Azure</span></span>


## <a name="test-the-java-web-application"></a><span data-ttu-id="988fd-208">Prueba de la aplicación web de Java</span><span class="sxs-lookup"><span data-stu-id="988fd-208">Test the Java Web Application</span></span>
1. <span data-ttu-id="988fd-209">Ejecute la dirección URL de la aplicación web en el explorador web:</span><span class="sxs-lookup"><span data-stu-id="988fd-209">Run the web app url in web browser:</span></span>  
   <span data-ttu-id="988fd-210">https://{nombre-de-app-service}.azurewebsites.net/api/hello</span><span class="sxs-lookup"><span data-stu-id="988fd-210">https://{your-app-service-name}.azurewebsites.net/api/hello</span></span>


<img src="media/VSTS/web-app16.png">

2. <span data-ttu-id="988fd-211">En la página web debe aparecer **Hello Azure!**</span><span class="sxs-lookup"><span data-stu-id="988fd-211">The web page should say **Hello Azure!**</span></span>

<img src="media/VSTS/web-api17.png">
