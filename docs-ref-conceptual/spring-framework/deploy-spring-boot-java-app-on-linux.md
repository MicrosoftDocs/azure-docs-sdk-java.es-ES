---
title: Implementación de una aplicación web Spring Boot en Linux en Azure Container Service
description: Este tutorial le guiará por los pasos necesarios para implementar una aplicación Spring Boot como una aplicación web de Linux en Microsoft Azure.
services: container-service
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: asirveda;robmcm
ms.date: 02/01/2018
ms.devlang: java
ms.service: container-service
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.custom: mvc
ms.openlocfilehash: c3a10a0d6029ba31b13f82907311d9182f98acb6
ms.sourcegitcommit: 151aaa6ccc64d94ed67f03e846bab953bde15b4a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/03/2018
ms.locfileid: "28954756"
---
# <a name="deploy-a-spring-boot-application-on-linux-in-the-azure-container-service"></a><span data-ttu-id="37516-103">Implementación de una aplicación de Spring Boot en Linux en Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="37516-103">Deploy a Spring Boot application on Linux in the Azure Container Service</span></span>

<span data-ttu-id="37516-104">En este tutorial se explica cómo usar [cliente de Docker] para desarrollar e implementar una aplicación de [Spring Boot] en un host Linux en [Azure Container Service (AKS)].</span><span class="sxs-lookup"><span data-stu-id="37516-104">This tutorial walks you through using [Docker] to develop and deploy a [Spring Boot] application to a Linux host in the [Azure Container Service (AKS)].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="37516-105">requisitos previos</span><span class="sxs-lookup"><span data-stu-id="37516-105">Prerequisites</span></span>

<span data-ttu-id="37516-106">Para realizar los pasos de este tutorial, necesitará tener los siguientes requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="37516-106">In order to complete the steps in this tutorial, you need to have the following prerequisites:</span></span>

* <span data-ttu-id="37516-107">Una suscripción de Azure. Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN] o registrarse para obtener una [cuenta de Azure gratuita].</span><span class="sxs-lookup"><span data-stu-id="37516-107">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="37516-108">La [Interfaz de la línea de comandos (CLI) de Azure].</span><span class="sxs-lookup"><span data-stu-id="37516-108">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="37516-109">Un [kit para desarrolladores de Java (JDK)] actualizado.</span><span class="sxs-lookup"><span data-stu-id="37516-109">An up-to-date [Java Developer Kit (JDK)].</span></span>
* <span data-ttu-id="37516-110">La herramienta de compilación [Maven] de Apache (versión 3).</span><span class="sxs-lookup"><span data-stu-id="37516-110">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="37516-111">Un cliente [Git].</span><span class="sxs-lookup"><span data-stu-id="37516-111">A [Git] client.</span></span>
* <span data-ttu-id="37516-112">Un [cliente de Docker].</span><span class="sxs-lookup"><span data-stu-id="37516-112">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="37516-113">Dados los requisitos de virtualización de este tutorial, los pasos que se describen en este artículo no se pueden seguir en una máquina virtual; es preciso usar un equipo físico con características de virtualización habilitadas.</span><span class="sxs-lookup"><span data-stu-id="37516-113">Due to the virtualization requirements of this tutorial, you cannot follow the steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="create-the-spring-boot-on-docker-getting-started-web-app"></a><span data-ttu-id="37516-114">Creación de la aplicación web Spring Boot on Docker Getting Started</span><span class="sxs-lookup"><span data-stu-id="37516-114">Create the Spring Boot on Docker Getting Started web app</span></span>

<span data-ttu-id="37516-115">Los siguientes pasos le guiarán por las fases necesarias para crear una aplicación web de Spring Boot sencilla y probarla de forma local.</span><span class="sxs-lookup"><span data-stu-id="37516-115">The following steps walk you through the steps that are required to create a simple Spring Boot web application and test it locally.</span></span>

1. <span data-ttu-id="37516-116">Abra el símbolo del sistema, cree un directorio local para alojar la aplicación y cambie a dicho directorio, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="37516-116">Open a command-prompt and create a local directory to hold your application, and change to that directory; for example:</span></span>
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="37516-117">-- o --</span><span class="sxs-lookup"><span data-stu-id="37516-117">-- or --</span></span>
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="37516-118">Clone el proyecto de ejemplo [inicial de Spring Boot en Docker] en el directorio que ha creado, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="37516-118">Clone the [Spring Boot on Docker Getting Started] sample project into the directory you created; for example:</span></span>
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. <span data-ttu-id="37516-119">Cambie de directorio al del proyecto finalizado, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="37516-119">Change directory to the completed project; for example:</span></span>
   ```
   cd gs-spring-boot-docker/complete
   ```

1. <span data-ttu-id="37516-120">Compile el archivo JAR con Maven, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="37516-120">Build the JAR file using Maven; for example:</span></span>
   ```
   mvn package
   ```

1. <span data-ttu-id="37516-121">Una vez creada la aplicación web, cambie el directorio al directorio `target` donde se encuentra el archivo JAR e inicie la aplicación web, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="37516-121">Once the web app has been created, change directory to the `target` directory where the JAR file is located and start the web app; for example:</span></span>
   ```
   cd target
   java -jar gs-spring-boot-docker-0.1.0.jar
   ```

1. <span data-ttu-id="37516-122">Pruebe la aplicación web. Para ello, navegue a ella localmente mediante un explorador web.</span><span class="sxs-lookup"><span data-stu-id="37516-122">Test the web app by browsing to it locally using a web browser.</span></span> <span data-ttu-id="37516-123">Por ejemplo, si tiene curl disponible y ha configurado el servidor Tomcat para que se ejecute en el puerto 80:</span><span class="sxs-lookup"><span data-stu-id="37516-123">For example, if you have curl available and you configured the Tomcat server to run on port 80:</span></span>
   ```
   curl http://localhost
   ```

1. <span data-ttu-id="37516-124">Debería aparecer el siguiente mensaje: **Hello Docker World!**</span><span class="sxs-lookup"><span data-stu-id="37516-124">You should see the following message displayed: **Hello Docker World!**</span></span>

   ![Examen local de aplicación de ejemplo][SB01]

## <a name="create-an-azure-container-registry-to-use-as-a-private-docker-registry"></a><span data-ttu-id="37516-126">Crear una instancia de Azure Container Registry para usarla como un Registro de Docker privado</span><span class="sxs-lookup"><span data-stu-id="37516-126">Create an Azure Container Registry to use as a Private Docker Registry</span></span>

<span data-ttu-id="37516-127">Los siguientes pasos le muestran cómo usar Azure Portal para crear una instancia de Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="37516-127">The following steps walk you through using the Azure portal to create an Azure Container Registry.</span></span>

> [!NOTE]
>
> <span data-ttu-id="37516-128">Si quiere usar la CLI de Azure en lugar de Azure Portal, siga los pasos descritos en [Creación de un registro de contenedor privado de Docker con la CLI de Azure 2.0](/azure/container-registry/container-registry-get-started-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="37516-128">If you want to use the Azure CLI instead of the Azure portal, follow the steps in [Create a private Docker container registry using the Azure CLI 2.0](/azure/container-registry/container-registry-get-started-azure-cli).</span></span>
>

1. <span data-ttu-id="37516-129">Vaya a [Azure Portal] e inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="37516-129">Browse to the [Azure portal] and sign in.</span></span>

   <span data-ttu-id="37516-130">Una vez que haya iniciado sesión en su cuenta en Azure Portal, puede seguir los pasos descritos en el artículo [Creación de un registro de contenedor privado de Docker con la CLI de Azure], que se vuelven a explicar en los pasos siguientes para mayor comodidad.</span><span class="sxs-lookup"><span data-stu-id="37516-130">Once you have signed in to your account on the Azure portal, you can follow the steps in the [Create a private Docker container registry using the Azure portal] article, which are paraphrased in the following steps for the sake of expediency.</span></span>

1. <span data-ttu-id="37516-131">Haga clic en el icono de menú **+ Nuevo**, en **Contenedores** y en **Azure Container Registry**.</span><span class="sxs-lookup"><span data-stu-id="37516-131">Click the menu icon for **+ New**, then click **Containers**, and then click **Azure Container Registry**.</span></span>
   
   ![Crear una instancia de Azure Container Registry][AR01]

1. <span data-ttu-id="37516-133">Cuando aparezca la página de información de la plantilla de Azure Container Registry, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="37516-133">When the information page for the Azure Container Registry template is displayed, click **Create**.</span></span> 

   ![Crear una instancia de Azure Container Registry][AR02]

1. <span data-ttu-id="37516-135">Cuando aparezca la página **Crear Registro de contenedor**, escriba su **Nombre del Registro** y **Grupo de recursos**, elija **Habilitar** para el **Usuario administrador** y haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="37516-135">When the **Create container registry** page is displayed, enter your **Registry name** and **Resource group**, choose **Enable** for the **Admin user**, and then click **Create**.</span></span>

   ![Configurar Azure Container Registry][AR03]

1. <span data-ttu-id="37516-137">Una vez que se haya creado el Registro de contenedor, desplácese hasta él en Azure Portal y haga clic en **Claves de acceso**.</span><span class="sxs-lookup"><span data-stu-id="37516-137">Once your container registry has been created, navigate to your container registry in the Azure portal, and then click **Access Keys**.</span></span> <span data-ttu-id="37516-138">Tome nota del nombre de usuario y la contraseña para usarlos en los pasos siguientes.</span><span class="sxs-lookup"><span data-stu-id="37516-138">Take note of the username and password for the next steps.</span></span>

   ![Claves de acceso de Azure Container Registry][AR04]

## <a name="configure-maven-to-use-your-azure-container-registry-access-keys"></a><span data-ttu-id="37516-140">Configurar Maven para que use las claves de acceso de Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="37516-140">Configure Maven to use your Azure Container Registry access keys</span></span>

1. <span data-ttu-id="37516-141">Navegue hasta el directorio de configuración de la instalación de Maven y abra el archivo *settings.xml* con un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="37516-141">Navigate to the configuration directory for your Maven installation and open the *settings.xml* file with a text editor.</span></span>

1. <span data-ttu-id="37516-142">Agregue la configuración de acceso de Azure Container Registry de la sección anterior de este tutorial a la colección `<servers>` en el archivo *settings.xml*, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="37516-142">Add your Azure Container Registry access settings from the previous section of this tutorial to the `<servers>` collection in the *settings.xml* file; for example:</span></span>

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

1. <span data-ttu-id="37516-143">Navegue hasta el directorio de proyecto completado de la aplicación Spring Boot (por ejemplo, "*C:\SpringBoot\gs-spring-boot-docker\complete*"o"*/users/robert/SpringBoot/gs-spring-boot-docker/complete*") y abra el archivo *pom.xml* con un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="37516-143">Navigate to the completed project directory for your Spring Boot application, (for example: "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open the *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="37516-144">Actualice la colección `<properties>` del archivo *pom.xml* con el valor del servidor de inicio de sesión de Azure Container Registry de la sección anterior de este tutorial, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="37516-144">Update the `<properties>` collection in the *pom.xml* file with the login server value for your Azure Container Registry from the previous section of this tutorial; for example:</span></span>

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

1. <span data-ttu-id="37516-145">Actualice la colección `<plugins>` del archivo *pom.xml* de modo que `<plugin>` contenga la dirección del servidor de inicio de sesión y el nombre de Registro de Azure Container Registry de la sección anterior de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="37516-145">Update the `<plugins>` collection in the *pom.xml* file so that the `<plugin>` contains the login server address and registry name for your Azure Container Registry from the previous section of this tutorial.</span></span> <span data-ttu-id="37516-146">Por ejemplo: </span><span class="sxs-lookup"><span data-stu-id="37516-146">For example:</span></span>

   ```xml
   <plugin>
      <groupId>com.spotify</groupId>
      <artifactId>docker-maven-plugin</artifactId>
      <version>0.4.11</version>
      <configuration>
         <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
         <dockerDirectory>src/main/docker</dockerDirectory>
         <resources>
            <resource>
               <targetPath>/</targetPath>
               <directory>${project.build.directory}</directory>
               <include>${project.build.finalName}.jar</include>
            </resource>
         </resources>
         <serverId>wingtiptoysregistry</serverId>
         <registryUrl>https://wingtiptoysregistry.azurecr.io</registryUrl>
      </configuration>
   </plugin>
   ```

1. <span data-ttu-id="37516-147">Navegue hasta el directorio de proyecto completado de la aplicación Spring Boot y ejecute el siguiente comando para recompilar la aplicación e insertar el contenedor en Azure Container Registry:</span><span class="sxs-lookup"><span data-stu-id="37516-147">Navigate to the completed project directory for your Spring Boot application and run the following command to rebuild the application and push the container to your Azure Container Registry:</span></span>

   ```
   mvn package docker:build -DpushImage 
   ```

> [!NOTE]
>
> <span data-ttu-id="37516-148">Cuando inserte el contenedor de Docker en Azure, podría recibir un mensaje de error similar a uno de los siguientes, incluso si el contenedor de Docker se ha creado correctamente:</span><span class="sxs-lookup"><span data-stu-id="37516-148">When you are pushing your Docker container to Azure, you may receive an error message that is similar to one of the following even though your Docker container was created successfully:</span></span>
>
> * `[ERROR] Failed to execute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: no basic auth credentials`
>
> * `[ERROR] Failed to execute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: Incomplete Docker registry authorization credentials. Please provide all of username, password, and email or none.`
>
> <span data-ttu-id="37516-149">Si esto ocurre, es posible que deba iniciar sesión en la cuenta de Azure desde la línea de comandos de Docker, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="37516-149">If this happens, you may need to sign in to your Azure account from the Docker command line; for example:</span></span>
>
> `docker login -u wingtiptoysregistry -p "AbCdEfGhIjKlMnOpQrStUvWxYz" wingtiptoysregistry.azurecr.io`
>
> <span data-ttu-id="37516-150">Después, puede insertar el contenedor desde la línea de comandos, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="37516-150">You can then push your container from the command line; for example:</span></span>
>
> `docker push wingtiptoysregistry.azurecr.io/gs-spring-boot-docker`
>

## <a name="create-a-web-app-on-linux-on-azure-app-service-using-your-container-image"></a><span data-ttu-id="37516-151">Crear una aplicación web en Linux en Azure App Service mediante la imagen de contenedor</span><span class="sxs-lookup"><span data-stu-id="37516-151">Create a web app on Linux on Azure App Service using your container image</span></span>

1. <span data-ttu-id="37516-152">Vaya a [Azure Portal] e inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="37516-152">Browse to the [Azure portal] and sign in.</span></span>

1. <span data-ttu-id="37516-153">Haga clic en el icono de menú **+ Nuevo**, en **Web y móvil** y en **Web App on Linux** (Aplicación web en Linux).</span><span class="sxs-lookup"><span data-stu-id="37516-153">Click the menu icon for **+ New**, then click **Web + Mobile**, and then click **Web App on Linux**.</span></span>
   
   ![Crear una aplicación web en Azure Portal][LX01]

1. <span data-ttu-id="37516-155">Cuando aparezca la página **Aplicación web en Linux**, especifique la información siguiente:</span><span class="sxs-lookup"><span data-stu-id="37516-155">When the **Web App on Linux** page is displayed, enter the following information:</span></span>

   <span data-ttu-id="37516-156">a.</span><span class="sxs-lookup"><span data-stu-id="37516-156">a.</span></span> <span data-ttu-id="37516-157">Escriba un nombre único para el **Nombre de la aplicación**, por ejemplo: "*wingtiptoyslinux*".</span><span class="sxs-lookup"><span data-stu-id="37516-157">Enter a unique name for the **App name**; for example: "*wingtiptoyslinux*."</span></span>

   <span data-ttu-id="37516-158">b.</span><span class="sxs-lookup"><span data-stu-id="37516-158">b.</span></span> <span data-ttu-id="37516-159">Seleccione su **Suscripción** en la lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="37516-159">Choose your **Subscription** from the drop-down list.</span></span>

   <span data-ttu-id="37516-160">c.</span><span class="sxs-lookup"><span data-stu-id="37516-160">c.</span></span> <span data-ttu-id="37516-161">Seleccione un **Grupo de recursos** existente o especifique un nombre para crear uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="37516-161">Choose an existing **Resource Group**, or specify a name to create a new resource group.</span></span>

   <span data-ttu-id="37516-162">d.</span><span class="sxs-lookup"><span data-stu-id="37516-162">d.</span></span> <span data-ttu-id="37516-163">Haga clic en **Configurar contenedor** y especifique la información siguiente:</span><span class="sxs-lookup"><span data-stu-id="37516-163">Click **Configure container** and enter the following information:</span></span>

      * <span data-ttu-id="37516-164">Seleccione **Registro privado**.</span><span class="sxs-lookup"><span data-stu-id="37516-164">Choose **Private registry**.</span></span>

      * <span data-ttu-id="37516-165">**Imagen y etiqueta opcional**: especifique el nombre del contenedor del ejemplo anterior, por ejemplo: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*".</span><span class="sxs-lookup"><span data-stu-id="37516-165">**Image and optional tag**: Specify your container name from earlier; for example: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*"</span></span>

      * <span data-ttu-id="37516-166">**Dirección URL del servidor**: especifique la dirección URL del Registro del ejemplo anterior, por ejemplo: "*https://wingtiptoysregistry.azurecr.io*".</span><span class="sxs-lookup"><span data-stu-id="37516-166">**Server URL**: Specify your registry URL from earlier; for example: "*https://wingtiptoysregistry.azurecr.io*"</span></span>

      * <span data-ttu-id="37516-167">**Nombre de usuario de inicio de sesión** y **Contraseña**: especifique las credenciales de inicio de sesión de las **Claves de acceso** que ha usado en los pasos anteriores.</span><span class="sxs-lookup"><span data-stu-id="37516-167">**Login username** and **Password**: Specify your login credentials from your **Access Keys** that you used in previous steps.</span></span>
   
   <span data-ttu-id="37516-168">e.</span><span class="sxs-lookup"><span data-stu-id="37516-168">e.</span></span> <span data-ttu-id="37516-169">Cuando haya especificado la información anterior, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="37516-169">Once you have entered all of the above information, click **OK**.</span></span>

   ![Configurar aplicaciones web][LX02]

1. <span data-ttu-id="37516-171">Haga clic en **Create**(Crear).</span><span class="sxs-lookup"><span data-stu-id="37516-171">Click **Create**.</span></span>

> [!NOTE]
>
> <span data-ttu-id="37516-172">Azure asignará automáticamente las solicitudes de Internet al servidor Tomcat integrado que se ejecuta en los puertos estándar 80 u 8080.</span><span class="sxs-lookup"><span data-stu-id="37516-172">Azure will automatically map Internet requests to embedded Tomcat server that is running on the standard ports of 80 or 8080.</span></span> <span data-ttu-id="37516-173">Aun así, si ha configurado el servidor Tomcat integrado para que se ejecute en un puerto personalizado, debe agregar una variable de entorno a la aplicación web que defina el puerto del servidor Tomcat integrado.</span><span class="sxs-lookup"><span data-stu-id="37516-173">However, if you configured your embedded Tomcat server to run on a custom port, you need to add an environment variable to your web app that defines the port for your embedded Tomcat server.</span></span> <span data-ttu-id="37516-174">Para ello, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="37516-174">To do so, use the following steps:</span></span>
>
> 1. <span data-ttu-id="37516-175">Vaya a [Azure Portal] e inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="37516-175">Browse to the [Azure portal] and sign in.</span></span>
> 
> 2. <span data-ttu-id="37516-176">Haga clic en el icono de **App Services**.</span><span class="sxs-lookup"><span data-stu-id="37516-176">Click the icon for **App Services**.</span></span> <span data-ttu-id="37516-177">(Vea el elemento n.º 1 de la imagen siguiente).</span><span class="sxs-lookup"><span data-stu-id="37516-177">(See item #1 in the image below.)</span></span>
>
> 3. <span data-ttu-id="37516-178">Seleccione la aplicación web en la lista.</span><span class="sxs-lookup"><span data-stu-id="37516-178">Select your web app from the list.</span></span> <span data-ttu-id="37516-179">(Vea el elemento n.º 2 de la imagen siguiente).</span><span class="sxs-lookup"><span data-stu-id="37516-179">(Item #2 in the image below.)</span></span>
>
> 4. <span data-ttu-id="37516-180">Haga clic en **Configuración de la aplicación**.</span><span class="sxs-lookup"><span data-stu-id="37516-180">Click **Application Settings**.</span></span> <span data-ttu-id="37516-181">(Vea el elemento n.º 3 de la imagen siguiente).</span><span class="sxs-lookup"><span data-stu-id="37516-181">(Item #3 in the image below.)</span></span>
>
> 5. <span data-ttu-id="37516-182">En la sección **Configuración de la aplicación**, agregue una nueva variable de entorno denominada **PORT** y especifique como valor su número de puerto personalizado.</span><span class="sxs-lookup"><span data-stu-id="37516-182">In the **App settings** section, add a new environment variable named **PORT** and enter your custom port number for the value.</span></span> <span data-ttu-id="37516-183">(Vea el elemento n.º 4 de la imagen siguiente).</span><span class="sxs-lookup"><span data-stu-id="37516-183">(Item #4 in the image below.)</span></span>
>
> 6. <span data-ttu-id="37516-184">Haga clic en **Save**(Guardar).</span><span class="sxs-lookup"><span data-stu-id="37516-184">Click **Save**.</span></span> <span data-ttu-id="37516-185">(Vea el elemento n.º 5 de la imagen siguiente).</span><span class="sxs-lookup"><span data-stu-id="37516-185">(Item #5 in the image below.)</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="37516-187">pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="37516-187">Next steps</span></span>

<span data-ttu-id="37516-188">Para obtener más información sobre el uso de aplicaciones de Spring Boot en Azure, consulte los siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="37516-188">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="37516-189">Implementación de una aplicación de Spring Boot en Azure App Service</span><span class="sxs-lookup"><span data-stu-id="37516-189">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)
* [<span data-ttu-id="37516-190">Implementación de una aplicación de Spring Boot en un clúster de Kubernetes en Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="37516-190">Deploy a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="37516-191">Para más información sobre el uso de Azure con Java, consulte [Azure para desarrolladores de Java] y [Java Tools for Visual Studio Team Services] (Herramientas de Java para Visual Studio Team Services).</span><span class="sxs-lookup"><span data-stu-id="37516-191">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="37516-192">Para obtener más información sobre el proyecto de ejemplo Spring Boot en Docker, vea [inicial de Spring Boot en Docker] (Introducción a Spring Boot en Docker).</span><span class="sxs-lookup"><span data-stu-id="37516-192">For further details about the Spring Boot on Docker sample project, see [Spring Boot on Docker Getting Started].</span></span>

<span data-ttu-id="37516-193">Para obtener ayuda para dar sus primeros pasos con sus propias aplicaciones de Spring Boot, consulte **Spring Initializr** en https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="37516-193">For help with getting started with your own Spring Boot applications, see the **Spring Initializr** at https://start.spring.io/.</span></span>

<span data-ttu-id="37516-194">Para obtener más información sobre cómo empezar a crear una sencilla aplicación Spring Boot, vea Spring Initializr en https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="37516-194">For more information about getting started with creating a simple Spring Boot application, see the Spring Initializr at https://start.spring.io/.</span></span>

<span data-ttu-id="37516-195">Para ver más ejemplos de cómo usar imágenes de Docker personalizadas con Azure, consulte [Uso de una imagen personalizada de Docker para Web App on Linux de Azure].</span><span class="sxs-lookup"><span data-stu-id="37516-195">For additional examples for how to use custom Docker images with Azure, see [Using a custom Docker image for Azure Web App on Linux].</span></span>

<!-- URL List -->

[Interfaz de la línea de comandos (CLI) de Azure]: /cli/azure/overview
[Azure Command-Line Interface (CLI)]: /cli/azure/overview
[Azure Container Service (AKS)]: https://azure.microsoft.com/services/container-service/
[Azure para desarrolladores de Java]: https://docs.microsoft.com/java/azure/
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Azure Portal]: https://portal.azure.com/
[Azure portal]: https://portal.azure.com/
[Creación de un registro de contenedor privado de Docker con la CLI de Azure]: /azure/container-registry/container-registry-get-started-portal
[Create a private Docker container registry using the Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Uso de una imagen personalizada de Docker para Web App on Linux de Azure]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Using a custom Docker image for Azure Web App on Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[cliente de Docker]: https://www.docker.com/
[Docker]: https://www.docker.com/
[cuenta de Azure gratuita]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[kit para desarrolladores de Java (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[ventajas como suscriptor de MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[inicial de Spring Boot en Docker]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Boot on Docker Getting Started]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/

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
