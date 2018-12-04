---
title: Implementación de una aplicación de Spring Boot en Kubernetes en Azure Kubernetes Service
description: Este tutorial le guiará por los pasos necesarios para implementar una aplicación Spring Boot en un clúster de Kubernetes en Microsoft Azure.
services: container-service
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 11/21/2018
ms.devlang: java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.custom: mvc
ms.openlocfilehash: d5ebfb7fc7279c745f77848dae397509662f0c0d
ms.sourcegitcommit: 8d0c59ae7c91adbb9be3c3e6d4a3429ffe51519d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/27/2018
ms.locfileid: "52338729"
---
# <a name="deploy-a-spring-boot-application-on-a-kubernetes-cluster-in-the-azure-kubernetes-service"></a><span data-ttu-id="7208d-103">Implementación de una aplicación de Spring Boot en un clúster de Kubernetes en Azure Kubernetes Service</span><span class="sxs-lookup"><span data-stu-id="7208d-103">Deploy a Spring Boot Application on a Kubernetes Cluster in the Azure Kubernetes Service</span></span>

<span data-ttu-id="7208d-104">**[Kubernetes]** y **[Docker]** son soluciones de código abierto que ayudan a los desarrolladores a automatizar la implementación, el escalado y la administración de sus aplicaciones que se ejecutan en contenedores.</span><span class="sxs-lookup"><span data-stu-id="7208d-104">**[Kubernetes]** and **[Docker]** are open-source solutions that help developers automate the deployment, scaling, and management of their applications running in containers.</span></span>

<span data-ttu-id="7208d-105">Este tutorial le indica cómo combinar estas dos populares tecnologías de código abierto para desarrollar e implementar una aplicación de Spring Boot en Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="7208d-105">This tutorial walks you through combining these two popular, open-source technologies to develop and deploy a Spring Boot application to Microsoft Azure.</span></span> <span data-ttu-id="7208d-106">Concretamente, *[Spring Boot]* se usa para el desarrollo de aplicaciones, *[Kubernetes]* para la implementación de contenedores y [Azure Kubernetes Service (AKS)] para hospedar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7208d-106">More specifically, you use *[Spring Boot]* for application development, *[Kubernetes]* for container deployment, and the [Azure Kubernetes Service (AKS)] to host your application.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="7208d-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="7208d-107">Prerequisites</span></span>

* <span data-ttu-id="7208d-108">Una suscripción de Azure. Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN] o registrarse para obtener una [cuenta de Azure gratuita].</span><span class="sxs-lookup"><span data-stu-id="7208d-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="7208d-109">La [Interfaz de la línea de comandos (CLI) de Azure].</span><span class="sxs-lookup"><span data-stu-id="7208d-109">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="7208d-110">Un kit de desarrollo de Java (JDK) admitido</span><span class="sxs-lookup"><span data-stu-id="7208d-110">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="7208d-111">Para más información sobre los JDK disponibles para desarrollar en Azure, consulte <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="7208d-111">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="7208d-112">La herramienta de compilación [Maven] de Apache (versión 3).</span><span class="sxs-lookup"><span data-stu-id="7208d-112">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="7208d-113">Un cliente [Git].</span><span class="sxs-lookup"><span data-stu-id="7208d-113">A [Git] client.</span></span>
* <span data-ttu-id="7208d-114">Un [Docker].</span><span class="sxs-lookup"><span data-stu-id="7208d-114">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="7208d-115">Dados los requisitos de virtualización de este tutorial, los pasos que se describen en este artículo no se pueden seguir en una máquina virtual; es preciso usar un equipo físico con características de virtualización habilitadas.</span><span class="sxs-lookup"><span data-stu-id="7208d-115">Due to the virtualization requirements of this tutorial, you cannot follow the steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="create-the-spring-boot-on-docker-getting-started-web-app"></a><span data-ttu-id="7208d-116">Creación de la aplicación web Spring Boot on Docker Getting Started</span><span class="sxs-lookup"><span data-stu-id="7208d-116">Create the Spring Boot on Docker Getting Started web app</span></span>

<span data-ttu-id="7208d-117">Los siguientes pasos le guían a través de la creación de una aplicación web Spring Boot y la realización de pruebas de la misma de forma local.</span><span class="sxs-lookup"><span data-stu-id="7208d-117">The following steps walk you through building a Spring Boot web application and testing it locally.</span></span>

1. <span data-ttu-id="7208d-118">Abra el símbolo del sistema, cree un directorio local para alojar la aplicación y cambie a dicho directorio, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="7208d-118">Open a command-prompt and create a local directory to hold your application, and change to that directory; for example:</span></span>
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="7208d-119">-- o --</span><span class="sxs-lookup"><span data-stu-id="7208d-119">-- or --</span></span>
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="7208d-120">Clone el proyecto de ejemplo [Spring Boot on Docker Getting Started] en el directorio.</span><span class="sxs-lookup"><span data-stu-id="7208d-120">Clone the [Spring Boot on Docker Getting Started] sample project into the directory.</span></span>
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. <span data-ttu-id="7208d-121">Cambie de directorio al del proyecto completado.</span><span class="sxs-lookup"><span data-stu-id="7208d-121">Change directory to the completed project.</span></span>
   ```
   cd gs-spring-boot-docker
   cd complete
   ```

1. <span data-ttu-id="7208d-122">Utilice Maven para compilar y ejecutar la aplicación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="7208d-122">Use Maven to build and run the sample app.</span></span>
   ```
   mvn package spring-boot:run
   ```

1. <span data-ttu-id="7208d-123">Para probar la aplicación web, vaya a `curl` o use el siguiente comando `http://localhost:8080`:</span><span class="sxs-lookup"><span data-stu-id="7208d-123">Test the web app by browsing to `http://localhost:8080`, or with the following `curl` command:</span></span>
   ```
   curl http://localhost:8080
   ```

1. <span data-ttu-id="7208d-124">Debería aparecer el siguiente mensaje: **Hello Docker World**</span><span class="sxs-lookup"><span data-stu-id="7208d-124">You should see the following message displayed: **Hello Docker World**</span></span>

   ![Examen local de aplicación de ejemplo][SB01]

## <a name="create-an-azure-container-registry-using-the-azure-cli"></a><span data-ttu-id="7208d-126">Creación de una instancia de Azure Container Registry mediante la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="7208d-126">Create an Azure Container Registry using the Azure CLI</span></span>

1. <span data-ttu-id="7208d-127">Abra el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="7208d-127">Open a command prompt.</span></span>

1. <span data-ttu-id="7208d-128">Inicie sesión en una cuenta de Azure:</span><span class="sxs-lookup"><span data-stu-id="7208d-128">Log in to your Azure account:</span></span>
   ```azurecli
   az login
   ```

1. <span data-ttu-id="7208d-129">Elija la suscripción de Azure:</span><span class="sxs-lookup"><span data-stu-id="7208d-129">Choose your Azure Subscription:</span></span>
   ```azurecli
   az account set -s <YourSubscriptionID>
   ```

1. <span data-ttu-id="7208d-130">Cree un grupo de recursos para los recursos de Azure que se usan en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="7208d-130">Create a resource group for the Azure resources used in this tutorial.</span></span>
   ```azurecli
   az group create --name=wingtiptoys-kubernetes --location=eastus
   ```

1. <span data-ttu-id="7208d-131">Crear una instancia de Azure Container Registry en el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="7208d-131">Create a private Azure container registry in the resource group.</span></span> <span data-ttu-id="7208d-132">El tutorial inserta la aplicación de ejemplo en forma de imagen Docker en este registro en los pasos posteriores.</span><span class="sxs-lookup"><span data-stu-id="7208d-132">The tutorial pushes the sample app as a Docker image to this registry in later steps.</span></span> <span data-ttu-id="7208d-133">Reemplace `wingtiptoysregistry` por un nombre único para el registro.</span><span class="sxs-lookup"><span data-stu-id="7208d-133">Replace `wingtiptoysregistry` with a unique name for your registry.</span></span>
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoys-kubernetes--location eastus \
    --name wingtiptoysregistry --sku Basic
   ```

## <a name="push-your-app-to-the-container-registry"></a><span data-ttu-id="7208d-134">Inserción de una aplicación en el registro de contenedor</span><span class="sxs-lookup"><span data-stu-id="7208d-134">Push your app to the container registry</span></span>

1. <span data-ttu-id="7208d-135">Navegue hasta el directorio de configuración de la instalación de Maven (valor predeterminado ~/.m2/ o C:\Users\username\.m2) y abra el archivo *settings.xml* con un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="7208d-135">Navigate to the configuration directory for your Maven installation (default ~/.m2/ or C:\Users\username\.m2) and open the *settings.xml* file with a text editor.</span></span>

1. <span data-ttu-id="7208d-136">Recupere la contraseña del registro de contenedor de la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="7208d-136">Retrieve the password for your container registry from the Azure CLI.</span></span>
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```

   ```json
   {
     "name": "password",
     "value": "AbCdEfGhIjKlMnOpQrStUvWxYz"
   }
   ```

1. <span data-ttu-id="7208d-137">Agregue el identificador y la contraseña de Azure Container Registry a una nueva colección `<server>` del archivo *settings.xml*.</span><span class="sxs-lookup"><span data-stu-id="7208d-137">Add your Azure Container Registry id and password to a new `<server>` collection in the *settings.xml* file.</span></span>
<span data-ttu-id="7208d-138">`id` y `username` son el nombre del registro.</span><span class="sxs-lookup"><span data-stu-id="7208d-138">The `id` and `username` are the name of the registry.</span></span> <span data-ttu-id="7208d-139">Use el valor `password` del comando anterior (sin comillas).</span><span class="sxs-lookup"><span data-stu-id="7208d-139">Use the `password` value from the previous command (without quotes).</span></span>

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

1. <span data-ttu-id="7208d-140">Navegue hasta el directorio de proyecto completado de la aplicación Spring Boot (por ejemplo, "*C:\SpringBoot\gs-spring-boot-docker\complete*"o"*/users/robert/SpringBoot/gs-spring-boot-docker/complete*") y abra el archivo *pom.xml* con un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="7208d-140">Navigate to the completed project directory for your Spring Boot application (for example, "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open the *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="7208d-141">Actualice la colección `<properties>` del archivo *pom.xml* con el valor del servidor de inicio de sesión de Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="7208d-141">Update the `<properties>` collection in the *pom.xml* file with the login server value for your Azure Container Registry.</span></span>

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

1. <span data-ttu-id="7208d-142">Actualice la colección `<plugins>` del archivo *pom.xml* de modo que `<plugin>` contiene la dirección del servidor de inicio de sesión y el nombre de registro de Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="7208d-142">Update the `<plugins>` collection in the *pom.xml* file so that the `<plugin>` contains the login server address and registry name for your Azure Container Registry.</span></span>

   ```xml
   <plugin>
      <groupId>com.spotify</groupId>
      <artifactId>docker-maven-plugin</artifactId>
      <version>0.4.11</version>
      <configuration>
         <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
         <buildArgs>
            <JAR_FILE>target/${project.build.finalName}.jar</JAR_FILE>
         </buildArgs>
         <baseImage>java</baseImage>
         <entryPoint>["java", "-jar", "/${project.build.finalName}.jar"]</entryPoint>
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

1. <span data-ttu-id="7208d-143">Navegue hasta el directorio de proyecto completado de la aplicación Spring Boot y ejecute el siguiente comando para crear el contenedor Docker e insertar la imagen en el registro:</span><span class="sxs-lookup"><span data-stu-id="7208d-143">Navigate to the completed project directory for your Spring Boot application and run the following command to build the Docker container and push the image to the registry:</span></span>

   ```
   mvn package docker:build -DpushImage
   ```

> [!NOTE]
>
>  <span data-ttu-id="7208d-144">Cuando Maven inserta la imagen en Azure, puede recibir un mensaje de error similar a uno de los siguientes:</span><span class="sxs-lookup"><span data-stu-id="7208d-144">You may receive an error message that is similar to one of the following when Maven pushes the image to Azure:</span></span>
>
> * `[ERROR] Failed to execute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: no basic auth credentials`
>
> * `[ERROR] Failed to execute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: Incomplete Docker registry authorization credentials. Please provide all of username, password, and email or none.`
>
> <span data-ttu-id="7208d-145">Si aparece este error, inicie sesión en Azure desde la línea de comandos de Docker.</span><span class="sxs-lookup"><span data-stu-id="7208d-145">If you get this error, log in to Azure from the Docker command line.</span></span>
>
> `docker login -u wingtiptoysregistry -p "AbCdEfGhIjKlMnOpQrStUvWxYz" wingtiptoysregistry.azurecr.io`
>
> <span data-ttu-id="7208d-146">Después, inserte el contenedor:</span><span class="sxs-lookup"><span data-stu-id="7208d-146">Then push your container:</span></span>
>
> `docker push wingtiptoysregistry.azurecr.io/gs-spring-boot-docker`

## <a name="create-a-kubernetes-cluster-on-aks-using-the-azure-cli"></a><span data-ttu-id="7208d-147">Creación de un clúster de Kubernetes en AKS mediante la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="7208d-147">Create a Kubernetes Cluster on AKS using the Azure CLI</span></span>

1. <span data-ttu-id="7208d-148">Cree un clúster de Kubernetes en Azure Kubernetes Service.</span><span class="sxs-lookup"><span data-stu-id="7208d-148">Create a Kubernetes cluster in Azure Kubernetes Service.</span></span> <span data-ttu-id="7208d-149">El siguiente comando crea un clúster de *Kubernetes* en el grupo de recursos *wingtiptoys-kubernetes*, con *wingtiptoys-akscluster* como nombre de clúster y *wingtiptoys-kubernetes* como prefijo de DNS:</span><span class="sxs-lookup"><span data-stu-id="7208d-149">The following command creates a *kubernetes* cluster in the *wingtiptoys-kubernetes* resource group, with *wingtiptoys-akscluster* as the cluster name, and *wingtiptoys-kubernetes* as the DNS prefix:</span></span>
   ```azurecli
   az aks create --resource-group=wingtiptoys-kubernetes --name=wingtiptoys-akscluster \ 
    --dns-name-prefix=wingtiptoys-kubernetes --generate-ssh-keys
   ```
   <span data-ttu-id="7208d-150">Esta operación puede tardar un tiempo en completarse.</span><span class="sxs-lookup"><span data-stu-id="7208d-150">This command may take a while to complete.</span></span>

1. <span data-ttu-id="7208d-151">Cuando se usa Azure Container Registry (ACR) con Azure Kubernetes Service (AKS), es preciso establecer un mecanismo de autenticación.</span><span class="sxs-lookup"><span data-stu-id="7208d-151">When you're using Azure Container Registry (ACR) with Azure Kubernetes Service (AKS), an authentication mechanism needs to be established.</span></span> <span data-ttu-id="7208d-152">Siga los pasos descritos en [Autenticación con Azure Container Registry desde Azure Kubernetes Service] para conceder a AKS acceso a ACR.</span><span class="sxs-lookup"><span data-stu-id="7208d-152">Follow the steps in [Authenticate with Azure Container Registry from Azure Kubernetes Service] to grant AKS access to ACR.</span></span>


1. <span data-ttu-id="7208d-153">Instale `kubectl` mediante la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="7208d-153">Install `kubectl` using the Azure CLI.</span></span> <span data-ttu-id="7208d-154">Los usuarios de Linux pueden tener anteceder este comando con `sudo`, ya que implementa la CLI de Kubernetes en `/usr/local/bin`.</span><span class="sxs-lookup"><span data-stu-id="7208d-154">Linux users may have to prefix this command with `sudo` since it deploys the Kubernetes CLI to `/usr/local/bin`.</span></span>
   ```azurecli
   az aks install-cli
   ```

1. <span data-ttu-id="7208d-155">Descargar la información de configuración del clúster para que pueda administrar el clúster desde la interfaz web de Kubernetes y `kubectl`.</span><span class="sxs-lookup"><span data-stu-id="7208d-155">Download the cluster configuration information so you can manage your cluster from the Kubernetes web interface and `kubectl`.</span></span> 
   ```azurecli
   az aks get-credentials --resource-group=wingtiptoys-kubernetes --name=wingtiptoys-akscluster
   ```

## <a name="deploy-the-image-to-your-kubernetes-cluster"></a><span data-ttu-id="7208d-156">Implementación de la imagen en un clúster de Kubernetes</span><span class="sxs-lookup"><span data-stu-id="7208d-156">Deploy the image to your Kubernetes cluster</span></span>

<span data-ttu-id="7208d-157">Este tutorial implementa la aplicación mediante `kubectl` y, después, le permite explorar la implementación a través de la interfaz de web de Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="7208d-157">This tutorial deploys the app using `kubectl`, then allow you to explore the deployment through the Kubernetes web interface.</span></span>

### <a name="deploy-with-the-kubernetes-web-interface"></a><span data-ttu-id="7208d-158">Implementación con la interfaz web de Kubernetes</span><span class="sxs-lookup"><span data-stu-id="7208d-158">Deploy with the Kubernetes web interface</span></span>

1. <span data-ttu-id="7208d-159">Abra el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="7208d-159">Open a command prompt.</span></span>

1. <span data-ttu-id="7208d-160">Abra el sitio web de configuración del clúster de Kubernetes en el explorador predeterminado:</span><span class="sxs-lookup"><span data-stu-id="7208d-160">Open the configuration website for your Kubernetes cluster in your default browser:</span></span>
   ```
   az aks browse --resource-group=wingtiptoys-kubernetes --name=wingtiptoys-akscluster
   ```

1. <span data-ttu-id="7208d-161">Cuando el sitio web para la configuración de Kubernetes se abra en el explorador, haga clic en el vínculo para **implementar una aplicación en contenedores**:</span><span class="sxs-lookup"><span data-stu-id="7208d-161">When the Kubernetes configuration website opens in your browser, click the link to **deploy a containerized app**:</span></span>

   ![Sitio web para la configuración de Kubernetes][KB01]

1. <span data-ttu-id="7208d-163">Cuando se muestra la página **Resource Creation** (Creación de recursos), especifique las opciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="7208d-163">When the **Resource Creation** page is displayed, specify the following options:</span></span>

   <span data-ttu-id="7208d-164"> a.</span><span class="sxs-lookup"><span data-stu-id="7208d-164">a.</span></span> <span data-ttu-id="7208d-165">Seleccione **CREATE AN APP** (Crear una aplicación).</span><span class="sxs-lookup"><span data-stu-id="7208d-165">Select **CREATE AN APP**.</span></span>

   <span data-ttu-id="7208d-166">b.</span><span class="sxs-lookup"><span data-stu-id="7208d-166">b.</span></span> <span data-ttu-id="7208d-167">Escriba el nombre de la aplicación Spring Boot en **App name** (Nombre de aplicación); por ejemplo: "*gs-spring-boot-docker*".</span><span class="sxs-lookup"><span data-stu-id="7208d-167">Enter your Spring Boot application name for the **App name**; for example: "*gs-spring-boot-docker*".</span></span>

   <span data-ttu-id="7208d-168">c.</span><span class="sxs-lookup"><span data-stu-id="7208d-168">c.</span></span> <span data-ttu-id="7208d-169">Escriba el servidor de inicio de sesión y la imagen del contenedor de anteriormente en **Container image** (Imagen del contenedor); por ejemplo: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*".</span><span class="sxs-lookup"><span data-stu-id="7208d-169">Enter your login server and container image from earlier for the **Container image**; for example: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*".</span></span>

   <span data-ttu-id="7208d-170">d.</span><span class="sxs-lookup"><span data-stu-id="7208d-170">d.</span></span> <span data-ttu-id="7208d-171">Elija **External** (Externo) en **Service** (Servicio).</span><span class="sxs-lookup"><span data-stu-id="7208d-171">Choose **External** for the **Service**.</span></span>

   <span data-ttu-id="7208d-172">e.</span><span class="sxs-lookup"><span data-stu-id="7208d-172">e.</span></span> <span data-ttu-id="7208d-173">Especifique los puertos interno y externo en los cuadros de texto **Port** (Puerto) y **Target port** (Puerto de destino).</span><span class="sxs-lookup"><span data-stu-id="7208d-173">Specify your external and internal ports in the **Port** and **Target port** text boxes.</span></span>

   ![Sitio web para la configuración de Kubernetes][KB02]


1. <span data-ttu-id="7208d-175">Haga clic en **Deploy** (Implementar) para implementar el contenedor.</span><span class="sxs-lookup"><span data-stu-id="7208d-175">Click **Deploy** to deploy the container.</span></span>

   ![Implementación de Kubernetes][KB05]

1. <span data-ttu-id="7208d-177">Una vez que la aplicación se haya implementado, verá la aplicación Spring Boot en **Services** (Servicios).</span><span class="sxs-lookup"><span data-stu-id="7208d-177">Once your application has been deployed, you will see your Spring Boot application listed under **Services**.</span></span>

   ![Servicios de Kubernetes][KB06]

1. <span data-ttu-id="7208d-179">Si hace clic en el vínculo de **External endpoints** (Puntos de conexión externos), puede ver que la aplicación Spring Boot se ejecuta en Azure.</span><span class="sxs-lookup"><span data-stu-id="7208d-179">If you click the link for **External endpoints**, you can see your Spring Boot application running on Azure.</span></span>

   ![Servicios de Kubernetes][KB07]

   ![Examen de la aplicación de ejemplo en Azure][SB02]


### <a name="deploy-with-kubectl"></a><span data-ttu-id="7208d-182">Implementación con kubectl</span><span class="sxs-lookup"><span data-stu-id="7208d-182">Deploy with kubectl</span></span>

1. <span data-ttu-id="7208d-183">Abra el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="7208d-183">Open a command prompt.</span></span>

1. <span data-ttu-id="7208d-184">Ejecute el contenedor en el clúster de Kubernetes mediante el comando `kubectl run`.</span><span class="sxs-lookup"><span data-stu-id="7208d-184">Run your container in the Kubernetes cluster by using the `kubectl run` command.</span></span> <span data-ttu-id="7208d-185">Proporcione un nombre de servicio para la aplicación en Kubernetes y el nombre de la imagen completa.</span><span class="sxs-lookup"><span data-stu-id="7208d-185">Give a service name for your app in Kubernetes and the full image name.</span></span> <span data-ttu-id="7208d-186">Por ejemplo: </span><span class="sxs-lookup"><span data-stu-id="7208d-186">For example:</span></span>
   ```
   kubectl run gs-spring-boot-docker --image=wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest
   ```
   <span data-ttu-id="7208d-187">En este comando:</span><span class="sxs-lookup"><span data-stu-id="7208d-187">In this command:</span></span>

   * <span data-ttu-id="7208d-188">El nombre del contenedor `gs-spring-boot-docker` se especifica inmediatamente después del comando `run`</span><span class="sxs-lookup"><span data-stu-id="7208d-188">The container name `gs-spring-boot-docker` is specified immediately after the `run` command</span></span>

   * <span data-ttu-id="7208d-189">El parámetro `--image` especifica la combinación de servidor de inicio de sesión y nombre de imagen como `wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest`</span><span class="sxs-lookup"><span data-stu-id="7208d-189">The `--image` parameter specifies the combined login server and image name as `wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest`</span></span>

1. <span data-ttu-id="7208d-190">Exponga externamente el clúster Kubernetes mediante el comando `kubectl expose`.</span><span class="sxs-lookup"><span data-stu-id="7208d-190">Expose your Kubernetes cluster externally by using the `kubectl expose` command.</span></span> <span data-ttu-id="7208d-191">Especifique el nombre del servicio, el puerto TCP de acceso público utilizado para acceder a la aplicación y el puerto de destino interno en que escucha la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7208d-191">Specify your service name, the public-facing TCP port used to access the app, and the internal target port your app listens on.</span></span> <span data-ttu-id="7208d-192">Por ejemplo: </span><span class="sxs-lookup"><span data-stu-id="7208d-192">For example:</span></span>
   ```
   kubectl expose deployment gs-spring-boot-docker --type=LoadBalancer --port=80 --target-port=8080
   ```
   <span data-ttu-id="7208d-193">En este comando:</span><span class="sxs-lookup"><span data-stu-id="7208d-193">In this command:</span></span>

   * <span data-ttu-id="7208d-194">El nombre del contenedor `gs-spring-boot-docker` se especifica inmediatamente después del comando `expose deployment`</span><span class="sxs-lookup"><span data-stu-id="7208d-194">The container name `gs-spring-boot-docker` is specified immediately after the `expose deployment` command</span></span>

   * <span data-ttu-id="7208d-195">El parámetro `--type` especifica que el clúster utiliza equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="7208d-195">The `--type` parameter specifies that the cluster uses load balancer</span></span>

   * <span data-ttu-id="7208d-196">El parámetro `--port` especifica el puerto TCP de acceso público, el 80.</span><span class="sxs-lookup"><span data-stu-id="7208d-196">The `--port` parameter specifies the public-facing TCP port of 80.</span></span> <span data-ttu-id="7208d-197">El acceso a la aplicación se realiza a través de este puerto.</span><span class="sxs-lookup"><span data-stu-id="7208d-197">You access the app on this port.</span></span>

   * <span data-ttu-id="7208d-198">El parámetro `--target-port` especifica el puerto TCP interno, el 8080.</span><span class="sxs-lookup"><span data-stu-id="7208d-198">The `--target-port` parameter specifies the internal TCP port of 8080.</span></span> <span data-ttu-id="7208d-199">El equilibrador de carga reenvía las solicitudes a la aplicación en este puerto.</span><span class="sxs-lookup"><span data-stu-id="7208d-199">The load balancer forwards requests to your app on this port.</span></span>

1. <span data-ttu-id="7208d-200">Una vez que la aplicación se implementa en el clúster, consulte la dirección IP externa y ábrala en el explorador web:</span><span class="sxs-lookup"><span data-stu-id="7208d-200">Once the app is deployed to the cluster, query the external IP address and open it in your web browser:</span></span>

   ```
   kubectl get services -o jsonpath={.items[*].status.loadBalancer.ingress[0].ip} --namespace=${namespace}
   ```

   ![Examen de la aplicación de ejemplo en Azure][SB02]


## <a name="next-steps"></a><span data-ttu-id="7208d-202">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7208d-202">Next steps</span></span>

<span data-ttu-id="7208d-203">Para más información acerca del uso de Spring Boot en Azure, consulte los siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="7208d-203">For more information about using Spring Boot on Azure, see the following articles:</span></span>

* [<span data-ttu-id="7208d-204">Implementación de una aplicación de Spring Boot en Azure App Service</span><span class="sxs-lookup"><span data-stu-id="7208d-204">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)
* [<span data-ttu-id="7208d-205">Implementación de una aplicación de Spring Boot en Linux en Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="7208d-205">Deploy a Spring Boot application on Linux in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-linux.md)

<span data-ttu-id="7208d-206">Para más información sobre el uso de Azure con Java, consulte [Azure para desarrolladores de Java] y [Herramientas de Java para Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="7208d-206">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="7208d-207"><!-- Newly added --> Para más información sobre cómo implementar una aplicación Java en Kubernetes con Visual Studio Code, consulte los [tutoriales de Visual Studio Code para Java].</span><span class="sxs-lookup"><span data-stu-id="7208d-207"><!-- Newly added --> For more information about deploying a Java application to Kubernetes with Visual Studio Code, see [Visual Studio Code Java Tutorials].</span></span>

<span data-ttu-id="7208d-208">Para más información acerca del proyecto de ejemplo Spring Boot on Docker, consulte [Spring Boot on Docker Getting Started].</span><span class="sxs-lookup"><span data-stu-id="7208d-208">For more information about the Spring Boot on Docker sample project, see [Spring Boot on Docker Getting Started].</span></span>

<span data-ttu-id="7208d-209">Los vínculos siguientes proporcionan información adicional acerca de cómo crear aplicaciones Spring Boot:</span><span class="sxs-lookup"><span data-stu-id="7208d-209">The following links provide additional information about creating Spring Boot applications:</span></span>

* <span data-ttu-id="7208d-210">Para más información acerca de cómo crear una sencilla aplicación de Spring Boot, consulte Spring Initializr en https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="7208d-210">For more information about creating a simple Spring Boot application, see the Spring Initializr at https://start.spring.io/.</span></span>

<span data-ttu-id="7208d-211">Los vínculos siguientes proporcionan información adicional acerca del uso de Kubernetes con Azure:</span><span class="sxs-lookup"><span data-stu-id="7208d-211">The following links provide additional information about using Kubernetes with Azure:</span></span>

* [<span data-ttu-id="7208d-212">Introducción a los clústeres de Kubernetes en Azure Kubernetes Service</span><span class="sxs-lookup"><span data-stu-id="7208d-212">Get started with a Kubernetes cluster in Azure Kubernetes Service</span></span>](https://docs.microsoft.com/azure/aks/intro-kubernetes)

<span data-ttu-id="7208d-213">Para más información acerca de cómo usar la interfaz de línea de comandos de Kubernetes, consulte la guía de usuario de **kubectl** en <https://kubernetes.io/docs/user-guide/kubectl/>.</span><span class="sxs-lookup"><span data-stu-id="7208d-213">More information about using Kubernetes command-line interface is available in the **kubectl** user guide at <https://kubernetes.io/docs/user-guide/kubectl/>.</span></span>

<span data-ttu-id="7208d-214">El sitio web de Kubernetes tiene varios artículos que tratan el uso de imágenes en registros privados:</span><span class="sxs-lookup"><span data-stu-id="7208d-214">The Kubernetes website has several articles that discuss using images in private registries:</span></span>

* <span data-ttu-id="7208d-215">[Configure Service Accounts for Pods] (Configurar cuentas de servicio para pods)</span><span class="sxs-lookup"><span data-stu-id="7208d-215">[Configuring Service Accounts for Pods]</span></span>
* <span data-ttu-id="7208d-216">[Espacios de nombres]</span><span class="sxs-lookup"><span data-stu-id="7208d-216">[Namespaces]</span></span>
* <span data-ttu-id="7208d-217">[Pull an Image from a Private Registry] (Extraer una imagen de un registro privado)</span><span class="sxs-lookup"><span data-stu-id="7208d-217">[Pulling an Image from a Private Registry]</span></span>

<span data-ttu-id="7208d-218">Para ver más ejemplos de cómo usar imágenes de Docker personalizadas con Azure, consulte [Uso de una imagen personalizada de Docker para Web App on Linux de Azure].</span><span class="sxs-lookup"><span data-stu-id="7208d-218">For additional examples for how to use custom Docker images with Azure, see [Using a custom Docker image for Azure Web App on Linux].</span></span>

<!-- URL List -->

[Interfaz de la línea de comandos (CLI) de Azure]: /cli/azure/overview
[Azure Command-Line Interface (CLI)]: /cli/azure/overview
[Azure Kubernetes Service (AKS)]: https://azure.microsoft.com/services/kubernetes-service/
[Azure para desarrolladores de Java]: https://docs.microsoft.com/java/azure/
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Azure portal]: https://portal.azure.com/
[Create a private Docker container registry using the Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Uso de una imagen personalizada de Docker para Web App on Linux de Azure]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Using a custom Docker image for Azure Web App on Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[cuenta de Azure gratuita]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Herramientas de Java para Visual Studio Team Services]: https://java.visualstudio.com/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Kubernetes]: https://kubernetes.io/
[Kubernetes Command-Line Interface (kubectl)]: https://kubernetes.io/docs/user-guide/kubectl-overview/
[Maven]: http://maven.apache.org/
[ventajas como suscriptor de MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot on Docker Getting Started]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/
[Configure Service Accounts for Pods]: https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/ (Configurar cuentas de servicio para pods)
[Configuring Service Accounts for Pods]: https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/
[Espacios de nombres]: https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/
[Namespaces]: https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/
[Pull an Image from a Private Registry]: https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/ (Extraer una imagen de un registro privado)
[Pulling an Image from a Private Registry]: https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/

[Java Development Kit (JDK)]: https://aka.ms/azure-jdks
<!-- http://www.oracle.com/technetwork/java/javase/downloads/ -->

<!-- Newly added -->
[Autenticación con Azure Container Registry desde Azure Kubernetes Service]: https://docs.microsoft.com/azure/container-registry/container-registry-auth-aks/
[Authenticate with Azure Container Registry from Azure Kubernetes Service]: https://docs.microsoft.com/azure/container-registry/container-registry-auth-aks/
[Tutoriales de Visual Studio Code para Java]: https://code.visualstudio.com/docs/java/java-kubernetes/
[Visual Studio Code Java Tutorials]: https://code.visualstudio.com/docs/java/java-kubernetes/

<!-- IMG List -->

[SB01]: ./media/deploy-spring-boot-java-app-on-kubernetes/SB01.png
[SB02]: ./media/deploy-spring-boot-java-app-on-kubernetes/SB02.png

[AR01]: ./media/deploy-spring-boot-java-app-on-kubernetes/AR01.png
[AR02]: ./media/deploy-spring-boot-java-app-on-kubernetes/AR02.png
[AR03]: ./media/deploy-spring-boot-java-app-on-kubernetes/AR03.png
[AR04]: ./media/deploy-spring-boot-java-app-on-kubernetes/AR04.png

[KB01]: ./media/deploy-spring-boot-java-app-on-kubernetes/KB01.png
[KB02]: ./media/deploy-spring-boot-java-app-on-kubernetes/KB02.png
[KB03]: ./media/deploy-spring-boot-java-app-on-kubernetes/KB03.png
[KB04]: ./media/deploy-spring-boot-java-app-on-kubernetes/KB04.png
[KB05]: ./media/deploy-spring-boot-java-app-on-kubernetes/KB05.png
[KB06]: ./media/deploy-spring-boot-java-app-on-kubernetes/KB06.png
[KB07]: ./media/deploy-spring-boot-java-app-on-kubernetes/KB07.png
