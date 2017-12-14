---
title: "Implementación de una aplicación Spring Boot en Kubernetes en Azure Container Service"
description: "Este tutorial le guiará por los pasos necesarios para implementar una aplicación Spring Boot en un clúster de Kubernetes en Microsoft Azure."
services: container-service
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: java
ms.topic: article
ms.date: 12/01/2017
ms.author: asirveda;robmcm
ms.custom: mvc
ms.openlocfilehash: ee8d5fecc31df427645c1552e27996592eaf27af
ms.sourcegitcommit: fc48e038721e6910cb8b1f8951df765d517e504d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/06/2017
---
# <a name="deploy-a-spring-boot-application-on-a-kubernetes-cluster-in-the-azure-container-service"></a><span data-ttu-id="7edeb-103">Implementación de una aplicación de Spring Boot en un clúster de Kubernetes en Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="7edeb-103">Deploy a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>

<span data-ttu-id="7edeb-104">**[Kubernetes]** y **[cliente de Docker]** son soluciones de código abierto que ayudan a los desarrolladores a automatizar la implementación, el escalado y la administración de sus aplicaciones que se ejecutan en contenedores.</span><span class="sxs-lookup"><span data-stu-id="7edeb-104">**[Kubernetes]** and **[Docker]** are open-source solutions that help developers automate the deployment, scaling, and management of their applications  running in containers.</span></span>

<span data-ttu-id="7edeb-105">Este tutorial le guía en la combinación de estas dos populares tecnologías de código abierto para desarrollar e implementar una aplicación Spring Boot en Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="7edeb-105">This tutorial walks you though combining these two popular, open-source technologies to develop and deploy a Spring Boot application to Microsoft Azure.</span></span> <span data-ttu-id="7edeb-106">Concretamente, *[Spring Boot]* se usa para el desarrollo de aplicaciones, *[Kubernetes]* para la implementación de contenedores y [Azure Container Service (AKS)] para hospedar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7edeb-106">More specifically, you use *[Spring Boot]* for application development, *[Kubernetes]* for container deployment, and the [Azure Container Service (AKS)] to host your application.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="7edeb-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="7edeb-107">Prerequisites</span></span>

* <span data-ttu-id="7edeb-108">Una suscripción de Azure. Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN] o registrarse para obtener una [cuenta de Azure gratuita].</span><span class="sxs-lookup"><span data-stu-id="7edeb-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="7edeb-109">La [Interfaz de la línea de comandos (CLI) de Azure].</span><span class="sxs-lookup"><span data-stu-id="7edeb-109">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="7edeb-110">Un [kit para desarrolladores de Java (JDK)] actualizado.</span><span class="sxs-lookup"><span data-stu-id="7edeb-110">An up-to-date [Java Developer Kit (JDK)].</span></span>
* <span data-ttu-id="7edeb-111">La herramienta de compilación [Maven] de Apache (versión 3).</span><span class="sxs-lookup"><span data-stu-id="7edeb-111">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="7edeb-112">Un cliente [Git].</span><span class="sxs-lookup"><span data-stu-id="7edeb-112">A [Git] client.</span></span>
* <span data-ttu-id="7edeb-113">Un [cliente de Docker].</span><span class="sxs-lookup"><span data-stu-id="7edeb-113">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="7edeb-114">Dados los requisitos de virtualización de este tutorial, los pasos que se describen en este artículo no se pueden seguir en una máquina virtual; es preciso usar un equipo físico con características de virtualización habilitadas.</span><span class="sxs-lookup"><span data-stu-id="7edeb-114">Due to the virtualization requirements of this tutorial, you cannot follow the steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="create-the-spring-boot-on-docker-getting-started-web-app"></a><span data-ttu-id="7edeb-115">Creación de la aplicación web Spring Boot on Docker Getting Started</span><span class="sxs-lookup"><span data-stu-id="7edeb-115">Create the Spring Boot on Docker Getting Started web app</span></span>

<span data-ttu-id="7edeb-116">Los siguientes pasos le guían a través de la creación de una aplicación web Spring Boot y la realización de pruebas de la misma de forma local.</span><span class="sxs-lookup"><span data-stu-id="7edeb-116">The following steps walk you through building a Spring Boot web application and testing it locally.</span></span>

1. <span data-ttu-id="7edeb-117">Abra el símbolo del sistema, cree un directorio local para alojar la aplicación y cambie a dicho directorio, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="7edeb-117">Open a command-prompt and create a local directory to hold your application, and change to that directory; for example:</span></span>
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="7edeb-118">-- o --</span><span class="sxs-lookup"><span data-stu-id="7edeb-118">-- or --</span></span>
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="7edeb-119">Clone el proyecto de ejemplo [Spring Boot on Docker Getting Started] en el directorio.</span><span class="sxs-lookup"><span data-stu-id="7edeb-119">Clone the [Spring Boot on Docker Getting Started] sample project into the directory.</span></span>
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. <span data-ttu-id="7edeb-120">Cambie de directorio al del proyecto completado.</span><span class="sxs-lookup"><span data-stu-id="7edeb-120">Change directory to the completed project.</span></span>
   ```
   cd gs-spring-boot-docker
   cd complete
   ```

1. <span data-ttu-id="7edeb-121">Utilice Maven para compilar y ejecutar la aplicación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="7edeb-121">Use Maven to build and run the sample app.</span></span>
   ```
   mvn package spring-boot:run
   ```

1. <span data-ttu-id="7edeb-122">Pruebe la aplicación web examinando http://localhost:8080 o con el siguiente comando `curl`:</span><span class="sxs-lookup"><span data-stu-id="7edeb-122">Test the web app by browsing to http://localhost:8080, or with the following `curl` command:</span></span>
   ```
   curl http://localhost:8080
   ```

1. <span data-ttu-id="7edeb-123">Debería aparecer el siguiente mensaje: **Hello Docker World**</span><span class="sxs-lookup"><span data-stu-id="7edeb-123">You should see the following message displayed: **Hello Docker World**</span></span>

   ![Examen local de aplicación de ejemplo][SB01]

## <a name="create-an-azure-container-registry-using-the-azure-cli"></a><span data-ttu-id="7edeb-125">Creación de una instancia de Azure Container Registry mediante la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="7edeb-125">Create an Azure Container Registry using the Azure CLI</span></span>

1. <span data-ttu-id="7edeb-126">Abra el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="7edeb-126">Open a command prompt.</span></span>

1. <span data-ttu-id="7edeb-127">Inicie sesión en una cuenta de Azure:</span><span class="sxs-lookup"><span data-stu-id="7edeb-127">Log in to your Azure account:</span></span>
   ```azurecli
   az login
   ```

1. <span data-ttu-id="7edeb-128">Cree un grupo de recursos para los recursos de Azure que se usan en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="7edeb-128">Create a resource group for the Azure resources used in this tutorial.</span></span>
   ```azurecli
   az group create --name=wingtiptoys-kubernetes --location=eastus
   ```

1. <span data-ttu-id="7edeb-129">Crear una instancia de Azure Container Registry en el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="7edeb-129">Create a private Azure container registry in the resource group.</span></span> <span data-ttu-id="7edeb-130">El tutorial inserta la aplicación de ejemplo en forma de imagen Docker en este registro en los pasos posteriores.</span><span class="sxs-lookup"><span data-stu-id="7edeb-130">The tutorial pushes the sample app as a Docker image to this registry in later steps.</span></span> <span data-ttu-id="7edeb-131">Reemplace `wingtiptoysregistry` por un nombre único para el registro.</span><span class="sxs-lookup"><span data-stu-id="7edeb-131">Replace `wingtiptoysregistry` with a unique name for your registry.</span></span>
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoys-kubernetes--location eastus \
    --name wingtiptoysregistry --sku Basic
   ```

## <a name="push-your-app-to-the-container-registry"></a><span data-ttu-id="7edeb-132">Inserción de una aplicación en el registro de contenedor</span><span class="sxs-lookup"><span data-stu-id="7edeb-132">Push your app to the container registry</span></span>

1. <span data-ttu-id="7edeb-133">Navegue hasta el directorio de configuración de la instalación de Maven (valor predeterminado ~/.m2/ o C:\Users\username\.m2) y abra el archivo *settings.xml* con un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="7edeb-133">Navigate to the configuration directory for your Maven installation (default ~/.m2/ or C:\Users\username\.m2) and open the *settings.xml* file with a text editor.</span></span>

1. <span data-ttu-id="7edeb-134">Recupere la contraseña del registro de contenedor de la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="7edeb-134">Retrieve the password for your container registry from the Azure CLI.</span></span>
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```

   ```json
   {
  "name": "password",
  "value": "AbCdEfGhIjKlMnOpQrStUvWxYz"
   }
   ```

1. <span data-ttu-id="7edeb-135">Agregue el identificador y la contraseña de Azure Container Registry a una nueva colección `<server>` del archivo *settings.xml*.</span><span class="sxs-lookup"><span data-stu-id="7edeb-135">Add your Azure Container Registry id and password to a new `<server>` collection in the *settings.xml* file.</span></span>
<span data-ttu-id="7edeb-136">`id` y `username` son el nombre del registro.</span><span class="sxs-lookup"><span data-stu-id="7edeb-136">The `id` and `username` are the name of the registry.</span></span> <span data-ttu-id="7edeb-137">Use el valor `password` del comando anterior (sin comillas).</span><span class="sxs-lookup"><span data-stu-id="7edeb-137">Use the `password` value from the previous command (without quotes).</span></span>

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

1. <span data-ttu-id="7edeb-138">Navegue hasta el directorio de proyecto completado de la aplicación Spring Boot (por ejemplo, "*C:\SpringBoot\gs-spring-boot-docker\complete*"o"*/users/robert/SpringBoot/gs-spring-boot-docker/complete*") y abra el archivo *pom.xml* con un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="7edeb-138">Navigate to the completed project directory for your Spring Boot application (for example, "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open the *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="7edeb-139">Actualice la colección `<properties>` del archivo *pom.xml* con el valor del servidor de inicio de sesión de Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="7edeb-139">Update the `<properties>` collection in the *pom.xml* file with the login server value for your Azure Container Registry.</span></span>

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

1. <span data-ttu-id="7edeb-140">Actualice la colección `<plugins>` del archivo *pom.xml* de modo que `<plugin>` contiene la dirección del servidor de inicio de sesión y el nombre de registro de Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="7edeb-140">Update the `<plugins>` collection in the *pom.xml* file so that the `<plugin>` contains the login server address and registry name for your Azure Container Registry.</span></span>

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

1. <span data-ttu-id="7edeb-141">Navegue hasta el directorio de proyecto completado de la aplicación Spring Boot y ejecute el siguiente comando para crear el contenedor Docker e insertar la imagen en el registro:</span><span class="sxs-lookup"><span data-stu-id="7edeb-141">Navigate to the completed project directory for your Spring Boot application and run the following command to build the Docker container and push the image to the registry:</span></span>

   ```
   mvn package docker:build -DpushImage
   ```

> [!NOTE]
>
>  <span data-ttu-id="7edeb-142">Cuando Maven inserta la imagen en Azure, puede recibir un mensaje de error similar a uno de los siguientes:</span><span class="sxs-lookup"><span data-stu-id="7edeb-142">You may receive an error message that is similar to one of the following when Maven pushes the image to Azure:</span></span>
>
> * `[ERROR] Failed to execute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: no basic auth credentials`
>
> * `[ERROR] Failed to execute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: Incomplete Docker registry authorization credentials. Please provide all of username, password, and email or none.`
>
> <span data-ttu-id="7edeb-143">Si aparece este error, inicie sesión en Azure desde la línea de comandos de Docker.</span><span class="sxs-lookup"><span data-stu-id="7edeb-143">If you get this error, log in to Azure from the Docker command line.</span></span>
>
> `docker login -u wingtiptoysregistry -p "AbCdEfGhIjKlMnOpQrStUvWxYz" wingtiptoysregistry.azurecr.io`
>
> <span data-ttu-id="7edeb-144">Después, inserte el contenedor:</span><span class="sxs-lookup"><span data-stu-id="7edeb-144">Then push your container:</span></span>
>
> `docker push wingtiptoysregistry.azurecr.io/gs-spring-boot-docker`

## <a name="create-a-kubernetes-cluster-on-aks-using-the-azure-cli"></a><span data-ttu-id="7edeb-145">Creación de un clúster de Kubernetes en AKS mediante la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="7edeb-145">Create a Kubernetes Cluster on AKS using the Azure CLI</span></span>

1. <span data-ttu-id="7edeb-146">Cree un clúster de Kubernetes en Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="7edeb-146">Create a Kubernetes cluster in Azure Container Service.</span></span> <span data-ttu-id="7edeb-147">El siguiente comando crea un clúster de *Kubernetes* en el grupo de recursos *wingtiptoys-kubernetes*, con *wingtiptoys-objeto containerservice* como nombre de clúster y *wingtiptoys-kubernetes* como prefijo de DNS:</span><span class="sxs-lookup"><span data-stu-id="7edeb-147">The following command creates a *kubernetes* cluster in the *wingtiptoys-kubernetes* resource group, with *wingtiptoys-containerservice* as the cluster name, and *wingtiptoys-kubernetes* as the DNS prefix:</span></span>
   ```azurecli
   az acs create --orchestrator-type=kubernetes --resource-group=wingtiptoys-kubernetes \ 
    --name=wingtiptoys-containerservice --dns-prefix=wingtiptoys-kubernetes
   ```
   <span data-ttu-id="7edeb-148">Esta operación puede tardar un tiempo en completarse.</span><span class="sxs-lookup"><span data-stu-id="7edeb-148">This command may take a while to complete.</span></span>

1. <span data-ttu-id="7edeb-149">Instale `kubectl` mediante la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="7edeb-149">Install `kubectl` using the Azure CLI.</span></span> <span data-ttu-id="7edeb-150">Los usuarios de Linux pueden tener anteceder este comando con `sudo`, ya que implementa la CLI de Kubernetes en `/usr/local/bin`.</span><span class="sxs-lookup"><span data-stu-id="7edeb-150">Linux users may have to prefix this command with `sudo` since it deploys the Kubernetes CLI to `/usr/local/bin`.</span></span>
   ```azurecli
   az acs kubernetes install-cli
   ```

1. <span data-ttu-id="7edeb-151">Descargar la información de configuración del clúster para que pueda administrar el clúster desde la interfaz web de Kubernetes y `kubectl`.</span><span class="sxs-lookup"><span data-stu-id="7edeb-151">Download the cluster configuration information so you can manage your cluster from the Kubernetes web interface and `kubectl`.</span></span> 
   ```azurecli
   az acs kubernetes get-credentials --resource-group=wingtiptoys-kubernetes  \ 
    --name=wingtiptoys-containerservice
   ```

## <a name="deploy-the-image-to-your-kubernetes-cluster"></a><span data-ttu-id="7edeb-152">Implementación de la imagen en un clúster de Kubernetes</span><span class="sxs-lookup"><span data-stu-id="7edeb-152">Deploy the image to your Kubernetes cluster</span></span>

<span data-ttu-id="7edeb-153">Este tutorial implementa la aplicación mediante `kubectl` y, después, le permite explorar la implementación a través de la interfaz de web de Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="7edeb-153">This tutorial deploys the app using `kubectl`, then allow you to explore the deployment through the Kubernetes web interface.</span></span>

### <a name="deploy-with-the-kubernetes-web-interface"></a><span data-ttu-id="7edeb-154">Implementación con la interfaz web de Kubernetes</span><span class="sxs-lookup"><span data-stu-id="7edeb-154">Deploy with the Kubernetes web interface</span></span>

1. <span data-ttu-id="7edeb-155">Abra el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="7edeb-155">Open a command prompt.</span></span>

1. <span data-ttu-id="7edeb-156">Abra el sitio web de configuración del clúster de Kubernetes en el explorador predeterminado:</span><span class="sxs-lookup"><span data-stu-id="7edeb-156">Open the configuration website for your Kubernetes cluster in your default browser:</span></span>
   ```
   az acs kubernetes browse --resource-group=wingtiptoys-kubernetes --name=wingtiptoys-containerservice
   ```

1. <span data-ttu-id="7edeb-157">Cuando el sitio web para la configuración de Kubernetes se abra en el explorador, haga clic en el vínculo para **implementar una aplicación en contenedores**:</span><span class="sxs-lookup"><span data-stu-id="7edeb-157">When the Kubernetes configuration website opens in your browser, click the link to **deploy a containerized app**:</span></span>

   ![Sitio web para la configuración de Kubernetes][KB01]

1. <span data-ttu-id="7edeb-159">Cuando se muestra la página **Deploy a containerized app** (Implementar una aplicación en contenedor), especifique las opciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="7edeb-159">When the **Deploy a containerized app** page is displayed, specify the following options:</span></span>

   <span data-ttu-id="7edeb-160">a.</span><span class="sxs-lookup"><span data-stu-id="7edeb-160">a.</span></span> <span data-ttu-id="7edeb-161">Seleccione **Specify app details below** (Especificar detalles de la aplicación a continuación).</span><span class="sxs-lookup"><span data-stu-id="7edeb-161">Select **Specify app details below**.</span></span>

   <span data-ttu-id="7edeb-162">b.</span><span class="sxs-lookup"><span data-stu-id="7edeb-162">b.</span></span> <span data-ttu-id="7edeb-163">Escriba el nombre de la aplicación Spring Boot en **App name** (Nombre de aplicación); por ejemplo: "*gs-spring-boot-docker*".</span><span class="sxs-lookup"><span data-stu-id="7edeb-163">Enter your Spring Boot application name for the **App name**; for example: "*gs-spring-boot-docker*".</span></span>

   <span data-ttu-id="7edeb-164">c.</span><span class="sxs-lookup"><span data-stu-id="7edeb-164">c.</span></span> <span data-ttu-id="7edeb-165">Escriba el servidor de inicio de sesión y la imagen del contenedor de anteriormente en **Container image** (Imagen del contenedor); por ejemplo: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*".</span><span class="sxs-lookup"><span data-stu-id="7edeb-165">Enter your login server and container image from earlier for the **Container image**; for example: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*".</span></span>

   <span data-ttu-id="7edeb-166">d.</span><span class="sxs-lookup"><span data-stu-id="7edeb-166">d.</span></span> <span data-ttu-id="7edeb-167">Elija **External** (Externo) en **Service** (Servicio).</span><span class="sxs-lookup"><span data-stu-id="7edeb-167">Choose **External** for the **Service**.</span></span>

   <span data-ttu-id="7edeb-168">e.</span><span class="sxs-lookup"><span data-stu-id="7edeb-168">e.</span></span> <span data-ttu-id="7edeb-169">Especifique los puertos interno y externo en los cuadros de texto **Port** (Puerto) y **Target port** (Puerto de destino).</span><span class="sxs-lookup"><span data-stu-id="7edeb-169">Specify your external and internal ports in the **Port** and **Target port** text boxes.</span></span>

   ![Sitio web para la configuración de Kubernetes][KB02]


1. <span data-ttu-id="7edeb-171">Haga clic en **Deploy** (Implementar) para implementar el contenedor.</span><span class="sxs-lookup"><span data-stu-id="7edeb-171">Click **Deploy** to deploy the container.</span></span>

   ![Implementar un contenedor][KB05]

1. <span data-ttu-id="7edeb-173">Una vez que la aplicación se haya implementado, verá la aplicación Spring Boot en **Services** (Servicios).</span><span class="sxs-lookup"><span data-stu-id="7edeb-173">Once your application has been deployed, you will see your Spring Boot application listed under **Services**.</span></span>

   ![Servicios de Kubernetes][KB06]

1. <span data-ttu-id="7edeb-175">Si hace clic en el vínculo de **External endpoints** (Puntos de conexión externos), puede ver que la aplicación Spring Boot se ejecuta en Azure.</span><span class="sxs-lookup"><span data-stu-id="7edeb-175">If you click the link for **External endpoints**, you can see your Spring Boot application running on Azure.</span></span>

   ![Servicios de Kubernetes][KB07]

   ![Examen de la aplicación de ejemplo en Azure][SB02]


### <a name="deploy-with-kubectl"></a><span data-ttu-id="7edeb-178">Implementación con kubectl</span><span class="sxs-lookup"><span data-stu-id="7edeb-178">Deploy with kubectl</span></span>

1. <span data-ttu-id="7edeb-179">Abra el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="7edeb-179">Open a command prompt.</span></span>

1. <span data-ttu-id="7edeb-180">Ejecute el contenedor en el clúster de Kubernetes mediante el comando `kubectl run`.</span><span class="sxs-lookup"><span data-stu-id="7edeb-180">Run your container in the Kubernetes cluster by using the `kubectl run` command.</span></span> <span data-ttu-id="7edeb-181">Proporcione un nombre de servicio para la aplicación en Kubernetes y el nombre de la imagen completa.</span><span class="sxs-lookup"><span data-stu-id="7edeb-181">Give a service name for your app in Kubernetes and the full image name.</span></span> <span data-ttu-id="7edeb-182">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="7edeb-182">For example:</span></span>
   ```
   kubectl run gs-spring-boot-docker --image=wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest
   ```
   <span data-ttu-id="7edeb-183">En este comando:</span><span class="sxs-lookup"><span data-stu-id="7edeb-183">In this command:</span></span>

   * <span data-ttu-id="7edeb-184">El nombre del contenedor `gs-spring-boot-docker` se especifica inmediatamente después del comando `run`</span><span class="sxs-lookup"><span data-stu-id="7edeb-184">The container name `gs-spring-boot-docker` is specified immediately after the `run` command</span></span>

   * <span data-ttu-id="7edeb-185">El parámetro `--image` especifica la combinación de servidor de inicio de sesión y nombre de imagen como `wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest`</span><span class="sxs-lookup"><span data-stu-id="7edeb-185">The `--image` parameter specifies the combined login server and image name as `wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest`</span></span>

1. <span data-ttu-id="7edeb-186">Exponga externamente el clúster Kubernetes mediante el comando `kubectl expose`.</span><span class="sxs-lookup"><span data-stu-id="7edeb-186">Expose your Kubernetes cluster externally by using the `kubectl expose` command.</span></span> <span data-ttu-id="7edeb-187">Especifique el nombre del servicio, el puerto TCP de acceso público utilizado para acceder a la aplicación y el puerto de destino interno en que escucha la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7edeb-187">Specify your service name, the public-facing TCP port used to access the app, and the internal target port your app listens on.</span></span> <span data-ttu-id="7edeb-188">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="7edeb-188">For example:</span></span>
   ```
   kubectl expose deployment gs-spring-boot-docker --type=LoadBalancer --port=80 --target-port=8080
   ```
   <span data-ttu-id="7edeb-189">En este comando:</span><span class="sxs-lookup"><span data-stu-id="7edeb-189">In this command:</span></span>

   * <span data-ttu-id="7edeb-190">El nombre del contenedor `gs-spring-boot-docker` se especifica inmediatamente después del comando `expose deployment`</span><span class="sxs-lookup"><span data-stu-id="7edeb-190">The container name `gs-spring-boot-docker` is specified immediately after the `expose deployment` command</span></span>

   * <span data-ttu-id="7edeb-191">El parámetro `--type` especifica que el clúster utiliza equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="7edeb-191">The `--type` parameter specifies that the cluster uses load balancer</span></span>

   * <span data-ttu-id="7edeb-192">El parámetro `--port` especifica el puerto TCP de acceso público, el 80.</span><span class="sxs-lookup"><span data-stu-id="7edeb-192">The `--port` parameter specifies the public-facing TCP port of 80.</span></span> <span data-ttu-id="7edeb-193">El acceso a la aplicación se realiza a través de este puerto.</span><span class="sxs-lookup"><span data-stu-id="7edeb-193">You access the app on this port.</span></span>

   * <span data-ttu-id="7edeb-194">El parámetro `--target-port` especifica el puerto TCP interno, el 8080.</span><span class="sxs-lookup"><span data-stu-id="7edeb-194">The `--target-port` parameter specifies the internal TCP port of 8080.</span></span> <span data-ttu-id="7edeb-195">El equilibrador de carga reenvía las solicitudes a la aplicación en este puerto.</span><span class="sxs-lookup"><span data-stu-id="7edeb-195">The load balancer forwards requests to your app on this port.</span></span>

1. <span data-ttu-id="7edeb-196">Una vez que la aplicación se implementa en el clúster, consulte la dirección IP externa y ábrala en el explorador web:</span><span class="sxs-lookup"><span data-stu-id="7edeb-196">Once the app is deployed to the cluster, query the external IP address and open it in your web browser:</span></span>

   ```
   kubectl get services -o jsonpath={.items[*].status.loadBalancer.ingress[0].ip} --namespace=${namespace}
   ```

   ![Examen de la aplicación de ejemplo en Azure][SB02]


## <a name="next-steps"></a><span data-ttu-id="7edeb-198">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7edeb-198">Next steps</span></span>

<span data-ttu-id="7edeb-199">Para más información acerca del uso de Spring Boot en Azure, consulte los siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="7edeb-199">For more information about using Spring Boot on Azure, see the following articles:</span></span>

* [<span data-ttu-id="7edeb-200">Implementación de una aplicación de Spring Boot en Azure App Service</span><span class="sxs-lookup"><span data-stu-id="7edeb-200">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)
* [<span data-ttu-id="7edeb-201">Implementación de una aplicación de Spring Boot en Linux en Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="7edeb-201">Deploy a Spring Boot application on Linux in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-linux.md)

<span data-ttu-id="7edeb-202">Para más información sobre el uso de Azure con Java, consulte [Azure para desarrolladores de Java] y [Java Tools for Visual Studio Team Services] (Herramientas de Java para Visual Studio Team Services).</span><span class="sxs-lookup"><span data-stu-id="7edeb-202">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="7edeb-203">Para más información acerca del proyecto de ejemplo Spring Boot on Docker, consulte [Spring Boot on Docker Getting Started].</span><span class="sxs-lookup"><span data-stu-id="7edeb-203">For more information about the Spring Boot on Docker sample project, see [Spring Boot on Docker Getting Started].</span></span>

<span data-ttu-id="7edeb-204">Los vínculos siguientes proporcionan información adicional acerca de cómo crear aplicaciones Spring Boot:</span><span class="sxs-lookup"><span data-stu-id="7edeb-204">The following links provide additional information about creating Spring Boot applications:</span></span>

* <span data-ttu-id="7edeb-205">Para más información acerca de cómo crear una sencilla aplicación Spring Boot, consulte Initializr Spring en https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="7edeb-205">For more information about creating a simple Spring Boot application, see the Spring Initializr at https://start.spring.io/.</span></span>

<span data-ttu-id="7edeb-206">Los vínculos siguientes proporcionan información adicional acerca del uso de Kubernetes con Azure:</span><span class="sxs-lookup"><span data-stu-id="7edeb-206">The following links provide additional information about using Kubernetes with Azure:</span></span>

* [<span data-ttu-id="7edeb-207">Implementación de un clúster de Kubernetes para los contenedores de Linux</span><span class="sxs-lookup"><span data-stu-id="7edeb-207">Get started with a Kubernetes cluster in Container Service</span></span>](https://docs.microsoft.com/azure/container-service/container-service-kubernetes-walkthrough)
* [<span data-ttu-id="7edeb-208">Uso de la interfaz de usuario web de Kubernetes con Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="7edeb-208">Using the Kubernetes web UI with Azure Container Service</span></span>](https://docs.microsoft.com/azure/container-service/container-service-kubernetes-ui)

<span data-ttu-id="7edeb-209">Para más información acerca del uso de la interfaz de línea de comandos de Kubernetes, consulte la guía de usuario de **kubectl** en <https://kubernetes.io/docs/user-guide/kubectl/>.</span><span class="sxs-lookup"><span data-stu-id="7edeb-209">More information about using Kubernetes command-line interface is available in the **kubectl** user guide at <https://kubernetes.io/docs/user-guide/kubectl/>.</span></span>

<span data-ttu-id="7edeb-210">El sitio web de Kubernetes tiene varios artículos que tratan el uso de imágenes en registros privados:</span><span class="sxs-lookup"><span data-stu-id="7edeb-210">The Kubernetes website has several articles that discuss using images in private registries:</span></span>

* <span data-ttu-id="7edeb-211">[Configure Service Accounts for Pods] (Configurar cuentas de servicio para pods)</span><span class="sxs-lookup"><span data-stu-id="7edeb-211">[Configuring Service Accounts for Pods]</span></span>
* <span data-ttu-id="7edeb-212">[Espacios de nombres]</span><span class="sxs-lookup"><span data-stu-id="7edeb-212">[Namespaces]</span></span>
* <span data-ttu-id="7edeb-213">[Pull an Image from a Private Registry] (Extraer una imagen de un registro privado)</span><span class="sxs-lookup"><span data-stu-id="7edeb-213">[Pulling an Image from a Private Registry]</span></span>

<span data-ttu-id="7edeb-214">Para ver más ejemplos de cómo usar imágenes de Docker personalizadas con Azure, consulte [Uso de una imagen personalizada de Docker para Web App on Linux de Azure].</span><span class="sxs-lookup"><span data-stu-id="7edeb-214">For additional examples for how to use custom Docker images with Azure, see [Using a custom Docker image for Azure Web App on Linux].</span></span>

<!-- URL List -->

[Interfaz de la línea de comandos (CLI) de Azure]: /cli/azure/overview
[Azure Container Service (AKS)]: https://azure.microsoft.com/services/container-service/
[Azure para desarrolladores de Java]: https://docs.microsoft.com/java/azure/
[Azure portal]: https://portal.azure.com/
[Create a private Docker container registry using the Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Uso de una imagen personalizada de Docker para Web App on Linux de Azure]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[cliente de Docker]: https://www.docker.com/
[cuenta de Azure gratuita]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[kit para desarrolladores de Java (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Kubernetes]: https://kubernetes.io/
[Kubernetes Command-Line Interface (kubectl)]: https://kubernetes.io/docs/user-guide/kubectl-overview/
[Maven]: http://maven.apache.org/
[ventajas como suscriptor de MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot on Docker Getting Started]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/
[Configure Service Accounts for Pods]: https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/ (Configurar cuentas de servicio para pods)
[Espacios de nombres]: https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/
[Pull an Image from a Private Registry]: https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/ (Extraer una imagen de un registro privado)

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
