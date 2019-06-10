---
title: Implementación de una aplicación web de Spring Boot en Azure App Service for Container
description: Este tutorial le guiará por los pasos necesarios para implementar una aplicación Spring Boot como una aplicación web de Linux en Microsoft Azure.
services: azure app service
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 12/19/2018
ms.devlang: java
ms.service: azure app service
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.custom: mvc
ms.openlocfilehash: 407b852e24ef88d2fb075bd064f1acf2b107ddc1
ms.sourcegitcommit: 394521c47ac9895d00d9f97535cc9d1e27d08fe9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/28/2019
ms.locfileid: "66270863"
---
# <a name="deploy-a-spring-boot-application-on-azure-app-service-for-container"></a><span data-ttu-id="b67cc-103">Implementación de una aplicación de Spring Boot en Azure App Service for Container</span><span class="sxs-lookup"><span data-stu-id="b67cc-103">Deploy a Spring Boot application on Azure App Service for Container</span></span>

<span data-ttu-id="b67cc-104">En este tutorial se explica cómo usar [Docker] para incluir su aplicación de [Spring Boot] en un contenedor e implementar su propia imagen de docker en un host Linux en [Azure App Service](https://docs.microsoft.com/azure/app-service/containers/app-service-linux-intro).</span><span class="sxs-lookup"><span data-stu-id="b67cc-104">This tutorial walks you through using [Docker] to containerize your [Spring Boot] application and deploy your own docker image to a Linux host in the [Azure App Service](https://docs.microsoft.com/azure/app-service/containers/app-service-linux-intro).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b67cc-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="b67cc-105">Prerequisites</span></span>

<span data-ttu-id="b67cc-106">Para realizar los pasos de este tutorial, necesitará tener los siguientes requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="b67cc-106">In order to complete the steps in this tutorial, you need to have the following prerequisites:</span></span>

* <span data-ttu-id="b67cc-107">Una suscripción de Azure. Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN] o registrarse para obtener una [cuenta de Azure gratuita].</span><span class="sxs-lookup"><span data-stu-id="b67cc-107">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="b67cc-108">La [Interfaz de la línea de comandos (CLI) de Azure].</span><span class="sxs-lookup"><span data-stu-id="b67cc-108">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="b67cc-109">Un kit de desarrollo de Java (JDK) admitido</span><span class="sxs-lookup"><span data-stu-id="b67cc-109">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="b67cc-110">Para más información sobre los JDK disponibles para desarrollar en Azure, consulte <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="b67cc-110">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="b67cc-111">La herramienta de compilación [Maven] de Apache (versión 3).</span><span class="sxs-lookup"><span data-stu-id="b67cc-111">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="b67cc-112">Un cliente [Git].</span><span class="sxs-lookup"><span data-stu-id="b67cc-112">A [Git] client.</span></span>
* <span data-ttu-id="b67cc-113">Un cliente de [Docker].</span><span class="sxs-lookup"><span data-stu-id="b67cc-113">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="b67cc-114">Dados los requisitos de virtualización de este tutorial, los pasos que se describen en este artículo no se pueden seguir en una máquina virtual; es preciso usar un equipo físico con características de virtualización habilitadas.</span><span class="sxs-lookup"><span data-stu-id="b67cc-114">Due to the virtualization requirements of this tutorial, you cannot follow the steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="create-the-spring-boot-on-docker-getting-started-web-app"></a><span data-ttu-id="b67cc-115">Creación de la aplicación web Spring Boot on Docker Getting Started</span><span class="sxs-lookup"><span data-stu-id="b67cc-115">Create the Spring Boot on Docker Getting Started web app</span></span>

<span data-ttu-id="b67cc-116">Los siguientes pasos le guiarán por las fases necesarias para crear una aplicación web de Spring Boot sencilla y probarla de forma local.</span><span class="sxs-lookup"><span data-stu-id="b67cc-116">The following steps walk you through the steps that are required to create a simple Spring Boot web application and test it locally.</span></span>

1. <span data-ttu-id="b67cc-117">Abra el símbolo del sistema, cree un directorio local para alojar la aplicación y cambie a dicho directorio, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="b67cc-117">Open a command-prompt and create a local directory to hold your application, and change to that directory; for example:</span></span>
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="b67cc-118">-- o --</span><span class="sxs-lookup"><span data-stu-id="b67cc-118">-- or --</span></span>
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="b67cc-119">Clone el proyecto de ejemplo [Spring Boot on Docker Getting Started] (inicial de Spring Boot en Docker) en el directorio que ha creado, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="b67cc-119">Clone the [Spring Boot on Docker Getting Started] sample project into the directory you created; for example:</span></span>
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. <span data-ttu-id="b67cc-120">Cambie de directorio al del proyecto finalizado, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="b67cc-120">Change directory to the completed project; for example:</span></span>
   ```
   cd gs-spring-boot-docker/complete
   ```

1. <span data-ttu-id="b67cc-121">Compile el archivo JAR con Maven, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="b67cc-121">Build the JAR file using Maven; for example:</span></span>
   ```
   mvn package
   ```

1. <span data-ttu-id="b67cc-122">Una vez creada la aplicación web, cambie el directorio al directorio `target` donde se encuentra el archivo JAR e inicie la aplicación web, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="b67cc-122">Once the web app has been created, change directory to the `target` directory where the JAR file is located and start the web app; for example:</span></span>
   ```
   cd target
   java -jar gs-spring-boot-docker-0.1.0.jar
   ```

1. <span data-ttu-id="b67cc-123">Pruebe la aplicación web. Para ello, navegue a ella localmente mediante un explorador web.</span><span class="sxs-lookup"><span data-stu-id="b67cc-123">Test the web app by browsing to it locally using a web browser.</span></span> <span data-ttu-id="b67cc-124">Por ejemplo, si tiene curl disponible y ha configurado el servidor Tomcat para que se ejecute en el puerto 80:</span><span class="sxs-lookup"><span data-stu-id="b67cc-124">For example, if you have curl available and you configured the Tomcat server to run on port 80:</span></span>
   ```
   curl http://localhost
   ```

1. <span data-ttu-id="b67cc-125">Debería ver el mensaje siguiente mostrado: **¡Hello Docker World!**</span><span class="sxs-lookup"><span data-stu-id="b67cc-125">You should see the following message displayed: **Hello Docker World!**</span></span>

   ![Examen local de aplicación de ejemplo][SB01]

## <a name="create-an-azure-container-registry-to-use-as-a-private-docker-registry"></a><span data-ttu-id="b67cc-127">Crear una instancia de Azure Container Registry para usarla como un Registro de Docker privado</span><span class="sxs-lookup"><span data-stu-id="b67cc-127">Create an Azure Container Registry to use as a Private Docker Registry</span></span>

<span data-ttu-id="b67cc-128">Los siguientes pasos le muestran cómo usar Azure Portal para crear una instancia de Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="b67cc-128">The following steps walk you through using the Azure portal to create an Azure Container Registry.</span></span>

> [!NOTE]
>
> <span data-ttu-id="b67cc-129">Si quiere usar la CLI de Azure en lugar de Azure Portal, siga los pasos descritos en [Creación de un registro de contenedor privado de Docker con la CLI de Azure 2.0](/azure/container-registry/container-registry-get-started-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="b67cc-129">If you want to use the Azure CLI instead of the Azure portal, follow the steps in [Create a private Docker container registry using the Azure CLI 2.0](/azure/container-registry/container-registry-get-started-azure-cli).</span></span>
>

1. <span data-ttu-id="b67cc-130">Vaya a [Azure Portal] e inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="b67cc-130">Browse to the [Azure portal] and sign in.</span></span>

   <span data-ttu-id="b67cc-131">Una vez que haya iniciado sesión en su cuenta en Azure Portal, puede seguir los pasos descritos en el artículo [Creación de un registro de contenedor privado de Docker con Azure Portal], que se vuelven a explicar en los pasos siguientes para mayor comodidad.</span><span class="sxs-lookup"><span data-stu-id="b67cc-131">Once you have signed in to your account on the Azure portal, you can follow the steps in the [Create a private Docker container registry using the Azure portal] article, which are paraphrased in the following steps for the sake of expediency.</span></span>

1. <span data-ttu-id="b67cc-132">Haga clic en el icono de menú **+ Nuevo**, en **Contenedores** y en **Azure Container Registry**.</span><span class="sxs-lookup"><span data-stu-id="b67cc-132">Click the menu icon for **+ New**, then click **Containers**, and then click **Azure Container Registry**.</span></span>
   
   ![Crear una instancia de Azure Container Registry][AR01]

1. <span data-ttu-id="b67cc-134">Cuando aparezca la página de información de la plantilla de Azure Container Registry, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="b67cc-134">When the information page for the Azure Container Registry template is displayed, click **Create**.</span></span> 

   ![Crear una instancia de Azure Container Registry][AR02]

1. <span data-ttu-id="b67cc-136">Cuando aparezca la página **Crear Registro de contenedor**, escriba su **Nombre del Registro** y **Grupo de recursos**, elija **Habilitar** para el **Usuario administrador** y haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="b67cc-136">When the **Create container registry** page is displayed, enter your **Registry name** and **Resource group**, choose **Enable** for the **Admin user**, and then click **Create**.</span></span>

   ![Configurar Azure Container Registry][AR03]

1. <span data-ttu-id="b67cc-138">Una vez que se haya creado el Registro de contenedor, desplácese hasta él en Azure Portal y haga clic en **Claves de acceso**.</span><span class="sxs-lookup"><span data-stu-id="b67cc-138">Once your container registry has been created, navigate to your container registry in the Azure portal, and then click **Access Keys**.</span></span> <span data-ttu-id="b67cc-139">Tome nota del nombre de usuario y la contraseña para usarlos en los pasos siguientes.</span><span class="sxs-lookup"><span data-stu-id="b67cc-139">Take note of the username and password for the next steps.</span></span>

   ![Claves de acceso de Azure Container Registry][AR04]

## <a name="configure-maven-to-use-your-azure-container-registry-access-keys"></a><span data-ttu-id="b67cc-141">Configurar Maven para que use las claves de acceso de Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="b67cc-141">Configure Maven to use your Azure Container Registry access keys</span></span>

1. <span data-ttu-id="b67cc-142">Vaya al directorio de proyecto completado de la aplicación Spring Boot (por ejemplo: "*C:\SpringBoot\gs-spring-boot-docker\complete*" o " */users/robert/SpringBoot/gs-spring-boot-docker/complete*") y abra el archivo *pom.xml* con un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="b67cc-142">Navigate to the completed project directory for your Spring Boot application, (for example: "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open the *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="b67cc-143">Actualice la colección `<properties>` del archivo *pom.xml* con la última versión de [jib-maven-plugin](https://github.com/GoogleContainerTools/jib/tree/master/jib-maven-plugin) y el valor del servidor de inicio de sesión y la configuración de acceso de Azure Container Registry de la sección anterior de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="b67cc-143">Update the `<properties>` collection in the *pom.xml* file with the latest version of [jib-maven-plugin](https://github.com/GoogleContainerTools/jib/tree/master/jib-maven-plugin) and login server value and access settings for your Azure Container Registry from the previous section of this tutorial.</span></span> <span data-ttu-id="b67cc-144">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="b67cc-144">For example:</span></span>

   ```xml
   <properties>
      <jib-maven-plugin.version>1.2.0</jib-maven-plugin.version>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
      <username>wingtiptoysregistry</username>
      <password>{put your Azure Container Registry access key here}</password>
   </properties>
   ```

1. <span data-ttu-id="b67cc-145">Agregue [jib-maven-plugin](https://github.com/GoogleContainerTools/jib/tree/master/jib-maven-plugin) a la colección `<plugins>` en el archivo *pom.xml*, especifique la imagen base en `<from>/<image>` y el nombre de la imagen final `<to>/<image>`, especifique el nombre de usuario y la contraseña de la sección anterior en `<to>/<auth>`.</span><span class="sxs-lookup"><span data-stu-id="b67cc-145">Add [jib-maven-plugin](https://github.com/GoogleContainerTools/jib/tree/master/jib-maven-plugin) to the `<plugins>` collection in the *pom.xml* file, specify the base image at `<from>/<image>` and  final image name `<to>/<image>`, specify the username and password from previous section at `<to>/<auth>`.</span></span> <span data-ttu-id="b67cc-146">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="b67cc-146">For example:</span></span>

   ```xml
   <plugin>
     <artifactId>jib-maven-plugin</artifactId>
     <groupId>com.google.cloud.tools</groupId>
     <version>${jib-maven-plugin.version}</version>
     <configuration>
        <from>
            <image>openjdk:8-jre-alpine</image>
        </from>
        <to>
            <image>${docker.image.prefix}/${project.artifactId}</image>
            <auth>
               <username>${username}</username>
               <password>${password}</password>
            </auth>
        </to>
     </configuration>
   </plugin>
   ```

1. <span data-ttu-id="b67cc-147">Navegue hasta el directorio de proyecto completado de la aplicación Spring Boot y ejecute el siguiente comando para recompilar la aplicación e insertar el contenedor en Azure Container Registry:</span><span class="sxs-lookup"><span data-stu-id="b67cc-147">Navigate to the completed project directory for your Spring Boot application and run the following command to rebuild the application and push the container to your Azure Container Registry:</span></span>

   ```cmd
   mvn compile jib:build
   ```

> [!NOTE]
>
> <span data-ttu-id="b67cc-148">Cuando usa Jib para insertar la imagen en Azure Container Registry, la imagen no seguirá el formato *Dockerfile*, consulte [este](https://cloudplatform.googleblog.com/2018/07/introducing-jib-build-java-docker-images-better.html) documento para más información.</span><span class="sxs-lookup"><span data-stu-id="b67cc-148">When you are using Jib to push your image to the Azure Container Registry, the image will not honor *Dockerfile*, see [this](https://cloudplatform.googleblog.com/2018/07/introducing-jib-build-java-docker-images-better.html) document for details.</span></span>
>

## <a name="create-a-web-app-on-linux-on-azure-app-service-using-your-container-image"></a><span data-ttu-id="b67cc-149">Crear una aplicación web en Linux en Azure App Service mediante la imagen de contenedor</span><span class="sxs-lookup"><span data-stu-id="b67cc-149">Create a web app on Linux on Azure App Service using your container image</span></span>

1. <span data-ttu-id="b67cc-150">Vaya a [Azure Portal] e inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="b67cc-150">Browse to the [Azure portal] and sign in.</span></span>

2. <span data-ttu-id="b67cc-151">Haga clic en el icono de menú **+ Crear un recurso**, a continuación, haga clic en **Web** y, a continuación, haga clic en **Web App for Containers**.</span><span class="sxs-lookup"><span data-stu-id="b67cc-151">Click the menu icon for **+ Create a resource**, then click **Web**, and then click **Web App for Containers**.</span></span>
   
   ![Crear una aplicación web en Azure Portal][LX01]

3. <span data-ttu-id="b67cc-153">Cuando aparezca la página **Aplicación web en Linux**, especifique la información siguiente:</span><span class="sxs-lookup"><span data-stu-id="b67cc-153">When the **Web App on Linux** page is displayed, enter the following information:</span></span>

   <span data-ttu-id="b67cc-154">a.</span><span class="sxs-lookup"><span data-stu-id="b67cc-154">a.</span></span> <span data-ttu-id="b67cc-155">Escriba un nombre único para el campo **Nombre de aplicación**, por ejemplo: "*wingtiptoyslinux*".</span><span class="sxs-lookup"><span data-stu-id="b67cc-155">Enter a unique name for the **App name**; for example: "*wingtiptoyslinux*"</span></span>

   <span data-ttu-id="b67cc-156">b.</span><span class="sxs-lookup"><span data-stu-id="b67cc-156">b.</span></span> <span data-ttu-id="b67cc-157">Seleccione su **Suscripción** en la lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="b67cc-157">Choose your **Subscription** from the drop-down list.</span></span>

   <span data-ttu-id="b67cc-158">c.</span><span class="sxs-lookup"><span data-stu-id="b67cc-158">c.</span></span> <span data-ttu-id="b67cc-159">Seleccione un **Grupo de recursos** existente o especifique un nombre para crear uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="b67cc-159">Choose an existing **Resource Group**, or specify a name to create a new resource group.</span></span>

   <span data-ttu-id="b67cc-160">d.</span><span class="sxs-lookup"><span data-stu-id="b67cc-160">d.</span></span> <span data-ttu-id="b67cc-161">Elija *Linux* como el **Sistema operativo**.</span><span class="sxs-lookup"><span data-stu-id="b67cc-161">Choose *Linux* as the **OS**.</span></span>

   <span data-ttu-id="b67cc-162">e.</span><span class="sxs-lookup"><span data-stu-id="b67cc-162">e.</span></span> <span data-ttu-id="b67cc-163">Haga clic en **Plan de App Service/Ubicación** y elija un plan de App Service existente o haga clic en **Crear nuevo** para crear un nuevo plan de App Service.</span><span class="sxs-lookup"><span data-stu-id="b67cc-163">Click **App Service plan/Location** and choose an existing app service plan, or click **Create new** to create a new app service plan.</span></span>

   <span data-ttu-id="b67cc-164">f.</span><span class="sxs-lookup"><span data-stu-id="b67cc-164">f.</span></span> <span data-ttu-id="b67cc-165">Haga clic en **Configurar contenedor** y especifique la información siguiente:</span><span class="sxs-lookup"><span data-stu-id="b67cc-165">Click **Configure container** and enter the following information:</span></span>

   * <span data-ttu-id="b67cc-166">Elija **Contenedor único** y **Azure Container Registry**.</span><span class="sxs-lookup"><span data-stu-id="b67cc-166">Choose **Single Container** and  **Azure Container Registry**.</span></span>

   * <span data-ttu-id="b67cc-167">**Registro**: Elija el nombre del contenedor creado anteriormente. Por ejemplo: "*wingtiptoysregistry*".</span><span class="sxs-lookup"><span data-stu-id="b67cc-167">**Registry**: Choose your container name created earlier; for example: "*wingtiptoysregistry*"</span></span>

   * <span data-ttu-id="b67cc-168">**Imagen**: elija el nombre de la imagen; por ejemplo: "*gs-spring-boot-docker*".</span><span class="sxs-lookup"><span data-stu-id="b67cc-168">**Image**: Choose the image name; for example: "*gs-spring-boot-docker*"</span></span>
   
   * <span data-ttu-id="b67cc-169">**Etiqueta**: elija la etiqueta de la imagen; por ejemplo: "*más reciente*".</span><span class="sxs-lookup"><span data-stu-id="b67cc-169">**Tag**: Choose the tag for the image; for example: "*latest*"</span></span>
   
   * <span data-ttu-id="b67cc-170">**Archivo de inicio**: déjela en blanco, ya que la imagen ya tiene el comando de inicio.</span><span class="sxs-lookup"><span data-stu-id="b67cc-170">**Startup File**: Keep it blank since the image already has the start up command</span></span>
   
   <span data-ttu-id="b67cc-171">e.</span><span class="sxs-lookup"><span data-stu-id="b67cc-171">e.</span></span> <span data-ttu-id="b67cc-172">Cuando haya especificado la información anterior, haga clic en **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="b67cc-172">Once you have entered all of the above information, click **Apply**.</span></span>

   ![Configurar aplicaciones web][LX02]

4. <span data-ttu-id="b67cc-174">Haga clic en **Create**(Crear).</span><span class="sxs-lookup"><span data-stu-id="b67cc-174">Click **Create**.</span></span>

> [!NOTE]
>
> <span data-ttu-id="b67cc-175">Azure asignará automáticamente las solicitudes de Internet al servidor Tomcat integrado que se ejecuta en los puertos estándar 80 u 8080.</span><span class="sxs-lookup"><span data-stu-id="b67cc-175">Azure will automatically map Internet requests to embedded Tomcat server that is running on the standard ports of 80 or 8080.</span></span> <span data-ttu-id="b67cc-176">Aun así, si ha configurado el servidor Tomcat integrado para que se ejecute en un puerto personalizado, debe agregar una variable de entorno a la aplicación web que defina el puerto del servidor Tomcat integrado.</span><span class="sxs-lookup"><span data-stu-id="b67cc-176">However, if you configured your embedded Tomcat server to run on a custom port, you need to add an environment variable to your web app that defines the port for your embedded Tomcat server.</span></span> <span data-ttu-id="b67cc-177">Para ello, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="b67cc-177">To do so, use the following steps:</span></span>
>
> 1. <span data-ttu-id="b67cc-178">Vaya a [Azure Portal] e inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="b67cc-178">Browse to the [Azure portal] and sign in.</span></span>
> 
> 2. <span data-ttu-id="b67cc-179">Haga clic en el icono de **App Services** y seleccione la aplicación web en la lista.</span><span class="sxs-lookup"><span data-stu-id="b67cc-179">Click the icon for **App Services**, and select your web app from the list.</span></span>
>
> 4. <span data-ttu-id="b67cc-180">Haga clic en **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="b67cc-180">Click **Configuration**.</span></span> <span data-ttu-id="b67cc-181">(Elemento 1 de la imagen siguiente).</span><span class="sxs-lookup"><span data-stu-id="b67cc-181">(Item #1 in the image below.)</span></span>
>
> 5. <span data-ttu-id="b67cc-182">En la sección **Configuración de la aplicación**, agregue un nuevo valor llamado **PORT** y especifique como valor su número de puerto personalizado.</span><span class="sxs-lookup"><span data-stu-id="b67cc-182">In the **Application settings** section, add a new setting named **PORT** and enter your custom port number for the value.</span></span> <span data-ttu-id="b67cc-183">(Elementos 2, 3 y 4 de la imagen siguiente).</span><span class="sxs-lookup"><span data-stu-id="b67cc-183">(Item #2, #3, #4 in the image below.)</span></span>
>
> 6. <span data-ttu-id="b67cc-184">Haga clic en **Save**(Guardar).</span><span class="sxs-lookup"><span data-stu-id="b67cc-184">Click **Save**.</span></span> <span data-ttu-id="b67cc-185">(Vea el elemento n.º 5 de la imagen siguiente).</span><span class="sxs-lookup"><span data-stu-id="b67cc-185">(Item #5 in the image below.)</span></span>
>
> ![Guardar un número de puerto personalizado en Azure Portal][LX03]
>

<!--
##  OPTIONAL: Configure the embedded Tomcat server to run on a different port

The embedded Tomcat server in the sample Spring Boot application is configured to run on port 8080 by default. However, if you want to run the embedded Tomcat server to run on a different port, such as port 80 for local testing, you can configure the port by using the following steps.

1. Go to the *resources* directory (or create the directory if it does not exist); for example:
   ```shell
   cd src/main/resources
   ```

1. Open the *application.yml* file in a text editor if it exists, or create a new YAML file if it does not exist.

1. Modify the **server** setting so that the server runs on port 80; for example:
   ```yaml
   server:
      port: 80
   ```

1. Save and close the *application.yml* file.
-->

## <a name="next-steps"></a><span data-ttu-id="b67cc-187">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b67cc-187">Next steps</span></span>

<span data-ttu-id="b67cc-188">Para más información acerca de Spring y Azure, vaya al centro de documentación de Azure.</span><span class="sxs-lookup"><span data-stu-id="b67cc-188">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b67cc-189">Spring en Azure</span><span class="sxs-lookup"><span data-stu-id="b67cc-189">Spring on Azure</span></span>](/java/azure/spring-framework)

### <a name="additional-resources"></a><span data-ttu-id="b67cc-190">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="b67cc-190">Additional Resources</span></span>

<span data-ttu-id="b67cc-191">Para obtener más información sobre el uso de aplicaciones de Spring Boot en Azure, consulte los siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="b67cc-191">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="b67cc-192">Implementación de una aplicación de Spring Boot en Azure App Service</span><span class="sxs-lookup"><span data-stu-id="b67cc-192">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)
* [<span data-ttu-id="b67cc-193">Implementación de una aplicación de Spring Boot en un clúster de Kubernetes en Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="b67cc-193">Deploy a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="b67cc-194">Para más información sobre el uso de Azure con Java, consulte [Azure para desarrolladores de Java] y [Working with Azure DevOps and Java] (Trabajo con Azure DevOps y Java).</span><span class="sxs-lookup"><span data-stu-id="b67cc-194">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Working with Azure DevOps and Java].</span></span>

<span data-ttu-id="b67cc-195">Para obtener más información sobre el proyecto de ejemplo Spring Boot en Docker, vea [Spring Boot on Docker Getting Started] (Introducción a Spring Boot en Docker).</span><span class="sxs-lookup"><span data-stu-id="b67cc-195">For further details about the Spring Boot on Docker sample project, see [Spring Boot on Docker Getting Started].</span></span>

<span data-ttu-id="b67cc-196">Para obtener ayuda para dar sus primeros pasos con sus propias aplicaciones de Spring Boot, consulte **Spring Initializr** en https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="b67cc-196">For help with getting started with your own Spring Boot applications, see the **Spring Initializr** at https://start.spring.io/.</span></span>

<span data-ttu-id="b67cc-197">Para más información sobre cómo empezar a crear una sencilla aplicación de Spring Boot, consulte Spring Initializr en https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="b67cc-197">For more information about getting started with creating a simple Spring Boot application, see the Spring Initializr at https://start.spring.io/.</span></span>

<span data-ttu-id="b67cc-198">Para ver más ejemplos de cómo usar imágenes de Docker personalizadas con Azure, consulte [Uso de una imagen personalizada de Docker para Web App on Linux de Azure].</span><span class="sxs-lookup"><span data-stu-id="b67cc-198">For additional examples for how to use custom Docker images with Azure, see [Using a custom Docker image for Azure Web App on Linux].</span></span>

<!-- URL List -->

[Interfaz de la línea de comandos (CLI) de Azure]: /cli/azure/overview
[Azure Command-Line Interface (CLI)]: /cli/azure/overview
[Azure Container Service (AKS)]: https://azure.microsoft.com/services/container-service/
[Azure para desarrolladores de Java]: /java/azure/
[Azure for Java Developers]: /java/azure/
[Azure Portal]: https://portal.azure.com/
[Azure portal]: https://portal.azure.com/
[Creación de un registro de contenedor privado de Docker con Azure Portal]: /azure/container-registry/container-registry-get-started-portal
[Create a private Docker container registry using the Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Uso de una imagen personalizada de Docker para Web App on Linux de Azure]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Using a custom Docker image for Azure Web App on Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[cuenta de Azure gratuita]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Working with Azure DevOps and Java]: /azure/devops/java/ (Trabajo con Azure DevOps y Java)
[Maven]: http://maven.apache.org/
[ventajas como suscriptor de MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot on Docker Getting Started]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/

[Java Development Kit (JDK)]: https://aka.ms/azure-jdks
<!-- http://www.oracle.com/technetwork/java/javase/downloads/ -->

<!-- IMG List -->

[SB01]: ./media/deploy-spring-boot-java-app-on-linux/SB01.png
[SB02]: ./media/deploy-spring-boot-java-app-on-linux/SB02.png

[AR01]: ./media/deploy-spring-boot-java-app-on-linux/AR01.png
[AR02]: ./media/deploy-spring-boot-java-app-on-linux/AR02.png
[AR03]: ./media/deploy-spring-boot-java-app-on-linux/AR03.png
[AR04]: ./media/deploy-spring-boot-java-app-on-linux/AR04.png

[LX01]: ./media/deploy-spring-boot-java-app-on-linux/LX01.png
[LX02]: ./media/deploy-spring-boot-java-app-on-linux/LX02.png
[LX03]: ./media/deploy-spring-boot-java-app-on-linux/LX03.png
