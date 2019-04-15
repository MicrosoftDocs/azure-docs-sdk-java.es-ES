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
ms.date: 12/19/2018
ms.devlang: java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.custom: mvc
ms.openlocfilehash: 42bb030a916cc5aaf1e20242518a0a400b8baa88
ms.sourcegitcommit: 3b10fe30dcc83e4c2e4c94d5b55e37ddbaa23c7a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2019
ms.locfileid: "59071014"
---
# <a name="deploy-a-spring-boot-application-on-a-kubernetes-cluster-in-the-azure-kubernetes-service"></a><span data-ttu-id="c22ea-103">Implementación de una aplicación de Spring Boot en un clúster de Kubernetes en Azure Kubernetes Service</span><span class="sxs-lookup"><span data-stu-id="c22ea-103">Deploy a Spring Boot Application on a Kubernetes Cluster in the Azure Kubernetes Service</span></span>

<span data-ttu-id="c22ea-104">**[Kubernetes]** y **[Docker]** son soluciones de código abierto que ayudan a los desarrolladores a automatizar la implementación, el escalado y la administración de sus aplicaciones que se ejecutan en contenedores.</span><span class="sxs-lookup"><span data-stu-id="c22ea-104">**[Kubernetes]** and **[Docker]** are open-source solutions that help developers automate the deployment, scaling, and management of their applications running in containers.</span></span>

<span data-ttu-id="c22ea-105">Este tutorial le indica cómo combinar estas dos populares tecnologías de código abierto para desarrollar e implementar una aplicación de Spring Boot en Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="c22ea-105">This tutorial walks you through combining these two popular, open-source technologies to develop and deploy a Spring Boot application to Microsoft Azure.</span></span> <span data-ttu-id="c22ea-106">Concretamente, *[Spring Boot]* se usa para el desarrollo de aplicaciones, *[Kubernetes]* para la implementación de contenedores y [Azure Kubernetes Service (AKS)] para hospedar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c22ea-106">More specifically, you use *[Spring Boot]* for application development, *[Kubernetes]* for container deployment, and the [Azure Kubernetes Service (AKS)] to host your application.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="c22ea-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c22ea-107">Prerequisites</span></span>

* <span data-ttu-id="c22ea-108">Una suscripción de Azure. Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN] o registrarse para obtener una [cuenta de Azure gratuita].</span><span class="sxs-lookup"><span data-stu-id="c22ea-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="c22ea-109">La [Interfaz de la línea de comandos (CLI) de Azure].</span><span class="sxs-lookup"><span data-stu-id="c22ea-109">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="c22ea-110">Un kit de desarrollo de Java (JDK) admitido</span><span class="sxs-lookup"><span data-stu-id="c22ea-110">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="c22ea-111">Para más información sobre los JDK disponibles para desarrollar en Azure, consulte <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="c22ea-111">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="c22ea-112">La herramienta de compilación [Maven] de Apache (versión 3).</span><span class="sxs-lookup"><span data-stu-id="c22ea-112">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="c22ea-113">Un cliente [Git].</span><span class="sxs-lookup"><span data-stu-id="c22ea-113">A [Git] client.</span></span>
* <span data-ttu-id="c22ea-114">Un cliente de [Docker].</span><span class="sxs-lookup"><span data-stu-id="c22ea-114">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="c22ea-115">Dados los requisitos de virtualización de este tutorial, los pasos que se describen en este artículo no se pueden seguir en una máquina virtual; es preciso usar un equipo físico con características de virtualización habilitadas.</span><span class="sxs-lookup"><span data-stu-id="c22ea-115">Due to the virtualization requirements of this tutorial, you cannot follow the steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="create-the-spring-boot-on-docker-getting-started-web-app"></a><span data-ttu-id="c22ea-116">Creación de la aplicación web Spring Boot on Docker Getting Started</span><span class="sxs-lookup"><span data-stu-id="c22ea-116">Create the Spring Boot on Docker Getting Started web app</span></span>

<span data-ttu-id="c22ea-117">Los siguientes pasos le guían a través de la creación de una aplicación web Spring Boot y la realización de pruebas de la misma de forma local.</span><span class="sxs-lookup"><span data-stu-id="c22ea-117">The following steps walk you through building a Spring Boot web application and testing it locally.</span></span>

1. <span data-ttu-id="c22ea-118">Abra el símbolo del sistema, cree un directorio local para alojar la aplicación y cambie a dicho directorio, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c22ea-118">Open a command-prompt and create a local directory to hold your application, and change to that directory; for example:</span></span>
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="c22ea-119">-- o --</span><span class="sxs-lookup"><span data-stu-id="c22ea-119">-- or --</span></span>
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="c22ea-120">Clone el proyecto de ejemplo [Spring Boot on Docker Getting Started] en el directorio.</span><span class="sxs-lookup"><span data-stu-id="c22ea-120">Clone the [Spring Boot on Docker Getting Started] sample project into the directory.</span></span>
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. <span data-ttu-id="c22ea-121">Cambie de directorio al del proyecto completado.</span><span class="sxs-lookup"><span data-stu-id="c22ea-121">Change directory to the completed project.</span></span>
   ```
   cd gs-spring-boot-docker
   cd complete
   ```

1. <span data-ttu-id="c22ea-122">Utilice Maven para compilar y ejecutar la aplicación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="c22ea-122">Use Maven to build and run the sample app.</span></span>
   ```
   mvn package spring-boot:run
   ```

1. <span data-ttu-id="c22ea-123">Para probar la aplicación web, vaya a `curl` o use el siguiente comando `http://localhost:8080`:</span><span class="sxs-lookup"><span data-stu-id="c22ea-123">Test the web app by browsing to `http://localhost:8080`, or with the following `curl` command:</span></span>
   ```
   curl http://localhost:8080
   ```

1. <span data-ttu-id="c22ea-124">Debería ver el mensaje siguiente mostrado: **Hello Docker World**</span><span class="sxs-lookup"><span data-stu-id="c22ea-124">You should see the following message displayed: **Hello Docker World**</span></span>

   ![Examen local de aplicación de ejemplo][SB01]

## <a name="create-an-azure-container-registry-using-the-azure-cli"></a><span data-ttu-id="c22ea-126">Creación de una instancia de Azure Container Registry mediante la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="c22ea-126">Create an Azure Container Registry using the Azure CLI</span></span>

1. <span data-ttu-id="c22ea-127">Abra el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="c22ea-127">Open a command prompt.</span></span>

1. <span data-ttu-id="c22ea-128">Inicie sesión en una cuenta de Azure:</span><span class="sxs-lookup"><span data-stu-id="c22ea-128">Log in to your Azure account:</span></span>
   ```azurecli
   az login
   ```

1. <span data-ttu-id="c22ea-129">Elija la suscripción de Azure:</span><span class="sxs-lookup"><span data-stu-id="c22ea-129">Choose your Azure Subscription:</span></span>
   ```azurecli
   az account set -s <YourSubscriptionID>
   ```

1. <span data-ttu-id="c22ea-130">Cree un grupo de recursos para los recursos de Azure que se usan en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="c22ea-130">Create a resource group for the Azure resources used in this tutorial.</span></span>
   ```azurecli
   az group create --name=wingtiptoys-kubernetes --location=eastus
   ```

1. <span data-ttu-id="c22ea-131">Crear una instancia de Azure Container Registry en el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="c22ea-131">Create a private Azure container registry in the resource group.</span></span> <span data-ttu-id="c22ea-132">El tutorial inserta la aplicación de ejemplo en forma de imagen Docker en este registro en los pasos posteriores.</span><span class="sxs-lookup"><span data-stu-id="c22ea-132">The tutorial pushes the sample app as a Docker image to this registry in later steps.</span></span> <span data-ttu-id="c22ea-133">Reemplace `wingtiptoysregistry` por un nombre único para el registro.</span><span class="sxs-lookup"><span data-stu-id="c22ea-133">Replace `wingtiptoysregistry` with a unique name for your registry.</span></span>
   ```azurecli
   az acr create --resource-group wingtiptoys-kubernetes --location eastus \
    --name wingtiptoysregistry --sku Basic
   ```

## <a name="push-your-app-to-the-container-registry-via-jib"></a><span data-ttu-id="c22ea-134">Inserción de una aplicación en el registro de contenedor mediante Jib</span><span class="sxs-lookup"><span data-stu-id="c22ea-134">Push your app to the container registry via Jib</span></span>

1. <span data-ttu-id="c22ea-135">Inicie sesión en Azure Container Registry desde la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="c22ea-135">Log in to your Azure Container Registry from the Azure CLI.</span></span>
   ```azurecli
   # set the default name for Azure Container Registry, otherwise you will need to specify the name in "az acr login"
   az configure --defaults acr=wingtiptoysregistry
   az acr login
   ```

1. <span data-ttu-id="c22ea-136">Navegue hasta el directorio de proyecto completado de la aplicación Spring Boot (por ejemplo, "*C:\SpringBoot\gs-spring-boot-docker\complete*"o"*/users/robert/SpringBoot/gs-spring-boot-docker/complete*") y abra el archivo *pom.xml* con un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="c22ea-136">Navigate to the completed project directory for your Spring Boot application (for example, "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open the *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="c22ea-137">Actualice la colección `<properties>` del archivo *pom.xml* con el nombre de su registro de Azure Container Registry y la última versión de [jib-maven-plugin](https://github.com/GoogleContainerTools/jib/tree/master/jib-maven-plugin).</span><span class="sxs-lookup"><span data-stu-id="c22ea-137">Update the `<properties>` collection in the *pom.xml* file with the registry name for your Azure Container Registry and the latest version of [jib-maven-plugin](https://github.com/GoogleContainerTools/jib/tree/master/jib-maven-plugin).</span></span>

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <jib-maven-plugin.version>1.0.2</jib-maven-plugin.version>
      <java.version>1.8</java.version>
   </properties>
   ```

1. <span data-ttu-id="c22ea-138">Actualice la colección `<plugins>` en el archivo *pom.xml* para que `<plugin>` contenga `jib-maven-plugin`.</span><span class="sxs-lookup"><span data-stu-id="c22ea-138">Update the `<plugins>` collection in the *pom.xml* file so that the `<plugin>` contains the `jib-maven-plugin`.</span></span>

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
        </to>
     </configuration>
   </plugin>
   ```

1. <span data-ttu-id="c22ea-139">Vaya al directorio de proyecto completado de la aplicación de Spring Boot y ejecute el siguiente comando para crear la imagen e insertarla en el registro:</span><span class="sxs-lookup"><span data-stu-id="c22ea-139">Navigate to the completed project directory for your Spring Boot application and run the following command to build the image and push the image to the registry:</span></span>

   ```
   mvn compile jib:build
   ```

## <a name="create-a-kubernetes-cluster-on-aks-using-the-azure-cli"></a><span data-ttu-id="c22ea-140">Creación de un clúster de Kubernetes en AKS mediante la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="c22ea-140">Create a Kubernetes Cluster on AKS using the Azure CLI</span></span>

1. <span data-ttu-id="c22ea-141">Cree un clúster de Kubernetes en Azure Kubernetes Service.</span><span class="sxs-lookup"><span data-stu-id="c22ea-141">Create a Kubernetes cluster in Azure Kubernetes Service.</span></span> <span data-ttu-id="c22ea-142">El siguiente comando crea un clúster de *Kubernetes* en el grupo de recursos *wingtiptoys-kubernetes*, con *wingtiptoys-akscluster* como nombre de clúster y *wingtiptoys-kubernetes* como prefijo de DNS:</span><span class="sxs-lookup"><span data-stu-id="c22ea-142">The following command creates a *kubernetes* cluster in the *wingtiptoys-kubernetes* resource group, with *wingtiptoys-akscluster* as the cluster name, and *wingtiptoys-kubernetes* as the DNS prefix:</span></span>
   ```azurecli
   az aks create --resource-group=wingtiptoys-kubernetes --name=wingtiptoys-akscluster \ 
    --dns-name-prefix=wingtiptoys-kubernetes --generate-ssh-keys
   ```
   <span data-ttu-id="c22ea-143">Esta operación puede tardar un tiempo en completarse.</span><span class="sxs-lookup"><span data-stu-id="c22ea-143">This command may take a while to complete.</span></span>

1. <span data-ttu-id="c22ea-144">Cuando se usa Azure Container Registry (ACR) con Azure Kubernetes Service (AKS), debe conceder a Azure Kubernetes Service acceso de incorporación de cambios en Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="c22ea-144">When you're using Azure Container Registry (ACR) with Azure Kubernetes Service (AKS), you need to grant Azure Kubernetes Service pull access to Azure Container Registry.</span></span> <span data-ttu-id="c22ea-145">De forma predeterminada, Azure crea una entidad de servicio al crear Azure Kubernetes Service.</span><span class="sxs-lookup"><span data-stu-id="c22ea-145">Azure creates a default service principal when you are creating Azure Kubernetes Service.</span></span> <span data-ttu-id="c22ea-146">Ejecute los siguientes scripts de Bash o Powershell para conceder a AKS acceso a ACR; consulte más información en [Autenticación con Azure Container Registry desde Azure Kubernetes Service (AKS)].</span><span class="sxs-lookup"><span data-stu-id="c22ea-146">Please run the following scripts in bash or Powershell to grant AKS access to ACR, see more details at [Authenticate with Azure Container Registry from Azure Kubernetes Service].</span></span>

```bash
   # Get the id of the service principal configured for AKS
   CLIENT_ID=$(az aks show -g wingtiptoys-kubernetes -n wingtiptoys-akscluster --query "servicePrincipalProfile.clientId" --output tsv)
   
   # Get the ACR registry resource id
   ACR_ID=$(az acr show -g wingtiptoys-kubernetes -n wingtiptoysregistry --query "id" --output tsv)
   
   # Create role assignment
   az role assignment create --assignee $CLIENT_ID --role acrpull --scope $ACR_ID
```

  <span data-ttu-id="c22ea-147">-- o --</span><span class="sxs-lookup"><span data-stu-id="c22ea-147">-- or --</span></span>

```PowerShell
   # Get the id of the service principal configured for AKS
   $CLIENT_ID = az aks show -g wingtiptoys-kubernetes -n wingtiptoys-akscluster --query "servicePrincipalProfile.clientId" --output tsv
   
   # Get the ACR registry resource id
   $ACR_ID = az acr show -g wingtiptoys-kubernetes -n wingtiptoysregistry --query "id" --output tsv
   
   # Create role assignment
   az role assignment create --assignee $CLIENT_ID --role acrpull --scope $ACR_ID
```

1. <span data-ttu-id="c22ea-148">Instale `kubectl` mediante la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="c22ea-148">Install `kubectl` using the Azure CLI.</span></span> <span data-ttu-id="c22ea-149">Los usuarios de Linux pueden tener anteceder este comando con `sudo`, ya que implementa la CLI de Kubernetes en `/usr/local/bin`.</span><span class="sxs-lookup"><span data-stu-id="c22ea-149">Linux users may have to prefix this command with `sudo` since it deploys the Kubernetes CLI to `/usr/local/bin`.</span></span>
   ```azurecli
   az aks install-cli
   ```

1. <span data-ttu-id="c22ea-150">Descargar la información de configuración del clúster para que pueda administrar el clúster desde la interfaz web de Kubernetes y `kubectl`.</span><span class="sxs-lookup"><span data-stu-id="c22ea-150">Download the cluster configuration information so you can manage your cluster from the Kubernetes web interface and `kubectl`.</span></span> 
   ```azurecli
   az aks get-credentials --resource-group=wingtiptoys-kubernetes --name=wingtiptoys-akscluster
   ```

## <a name="deploy-the-image-to-your-kubernetes-cluster"></a><span data-ttu-id="c22ea-151">Implementación de la imagen en un clúster de Kubernetes</span><span class="sxs-lookup"><span data-stu-id="c22ea-151">Deploy the image to your Kubernetes cluster</span></span>

<span data-ttu-id="c22ea-152">Este tutorial implementa la aplicación mediante `kubectl` y, después, le permite explorar la implementación a través de la interfaz de web de Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="c22ea-152">This tutorial deploys the app using `kubectl`, then allow you to explore the deployment through the Kubernetes web interface.</span></span>

### <a name="deploy-with-kubectl"></a><span data-ttu-id="c22ea-153">Implementación con kubectl</span><span class="sxs-lookup"><span data-stu-id="c22ea-153">Deploy with kubectl</span></span>

1. <span data-ttu-id="c22ea-154">Abra el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="c22ea-154">Open a command prompt.</span></span>

1. <span data-ttu-id="c22ea-155">Ejecute el contenedor en el clúster de Kubernetes mediante el comando `kubectl run`.</span><span class="sxs-lookup"><span data-stu-id="c22ea-155">Run your container in the Kubernetes cluster by using the `kubectl run` command.</span></span> <span data-ttu-id="c22ea-156">Proporcione un nombre de servicio para la aplicación en Kubernetes y el nombre de la imagen completa.</span><span class="sxs-lookup"><span data-stu-id="c22ea-156">Give a service name for your app in Kubernetes and the full image name.</span></span> <span data-ttu-id="c22ea-157">Por ejemplo: </span><span class="sxs-lookup"><span data-stu-id="c22ea-157">For example:</span></span>
   ```
   kubectl run gs-spring-boot-docker --image=wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest
   ```
   <span data-ttu-id="c22ea-158">En este comando:</span><span class="sxs-lookup"><span data-stu-id="c22ea-158">In this command:</span></span>

   * <span data-ttu-id="c22ea-159">El nombre del contenedor `gs-spring-boot-docker` se especifica inmediatamente después del comando `run`</span><span class="sxs-lookup"><span data-stu-id="c22ea-159">The container name `gs-spring-boot-docker` is specified immediately after the `run` command</span></span>

   * <span data-ttu-id="c22ea-160">El parámetro `--image` especifica la combinación de servidor de inicio de sesión y nombre de imagen como `wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest`</span><span class="sxs-lookup"><span data-stu-id="c22ea-160">The `--image` parameter specifies the combined login server and image name as `wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest`</span></span>

1. <span data-ttu-id="c22ea-161">Exponga externamente el clúster Kubernetes mediante el comando `kubectl expose`.</span><span class="sxs-lookup"><span data-stu-id="c22ea-161">Expose your Kubernetes cluster externally by using the `kubectl expose` command.</span></span> <span data-ttu-id="c22ea-162">Especifique el nombre del servicio, el puerto TCP de acceso público utilizado para acceder a la aplicación y el puerto de destino interno en que escucha la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c22ea-162">Specify your service name, the public-facing TCP port used to access the app, and the internal target port your app listens on.</span></span> <span data-ttu-id="c22ea-163">Por ejemplo: </span><span class="sxs-lookup"><span data-stu-id="c22ea-163">For example:</span></span>
   ```
   kubectl expose deployment gs-spring-boot-docker --type=LoadBalancer --port=80 --target-port=8080
   ```
   <span data-ttu-id="c22ea-164">En este comando:</span><span class="sxs-lookup"><span data-stu-id="c22ea-164">In this command:</span></span>

   * <span data-ttu-id="c22ea-165">El nombre del contenedor `gs-spring-boot-docker` se especifica inmediatamente después del comando `expose deployment`</span><span class="sxs-lookup"><span data-stu-id="c22ea-165">The container name `gs-spring-boot-docker` is specified immediately after the `expose deployment` command</span></span>

   * <span data-ttu-id="c22ea-166">El parámetro `--type` especifica que el clúster utiliza equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="c22ea-166">The `--type` parameter specifies that the cluster uses load balancer</span></span>

   * <span data-ttu-id="c22ea-167">El parámetro `--port` especifica el puerto TCP de acceso público, el 80.</span><span class="sxs-lookup"><span data-stu-id="c22ea-167">The `--port` parameter specifies the public-facing TCP port of 80.</span></span> <span data-ttu-id="c22ea-168">El acceso a la aplicación se realiza a través de este puerto.</span><span class="sxs-lookup"><span data-stu-id="c22ea-168">You access the app on this port.</span></span>

   * <span data-ttu-id="c22ea-169">El parámetro `--target-port` especifica el puerto TCP interno, el 8080.</span><span class="sxs-lookup"><span data-stu-id="c22ea-169">The `--target-port` parameter specifies the internal TCP port of 8080.</span></span> <span data-ttu-id="c22ea-170">El equilibrador de carga reenvía las solicitudes a la aplicación en este puerto.</span><span class="sxs-lookup"><span data-stu-id="c22ea-170">The load balancer forwards requests to your app on this port.</span></span>

1. <span data-ttu-id="c22ea-171">Una vez que la aplicación se implementa en el clúster, consulte la dirección IP externa y ábrala en el explorador web:</span><span class="sxs-lookup"><span data-stu-id="c22ea-171">Once the app is deployed to the cluster, query the external IP address and open it in your web browser:</span></span>

   ```
   kubectl get services -o jsonpath={.items[*].status.loadBalancer.ingress[0].ip} --namespace=default
   ```

   ![Examen de la aplicación de ejemplo en Azure][SB02]



### <a name="deploy-with-the-kubernetes-web-interface"></a><span data-ttu-id="c22ea-173">Implementación con la interfaz web de Kubernetes</span><span class="sxs-lookup"><span data-stu-id="c22ea-173">Deploy with the Kubernetes web interface</span></span>

1. <span data-ttu-id="c22ea-174">Abra el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="c22ea-174">Open a command prompt.</span></span>

1. <span data-ttu-id="c22ea-175">Abra el sitio web de configuración del clúster de Kubernetes en el explorador predeterminado:</span><span class="sxs-lookup"><span data-stu-id="c22ea-175">Open the configuration website for your Kubernetes cluster in your default browser:</span></span>
   ```
   az aks browse --resource-group=wingtiptoys-kubernetes --name=wingtiptoys-akscluster
   ```

1. <span data-ttu-id="c22ea-176">Cuando el sitio web para la configuración de Kubernetes se abra en el explorador, haga clic en el vínculo para **implementar una aplicación en contenedores**:</span><span class="sxs-lookup"><span data-stu-id="c22ea-176">When the Kubernetes configuration website opens in your browser, click the link to **deploy a containerized app**:</span></span>

   ![Sitio web para la configuración de Kubernetes][KB01]

1. <span data-ttu-id="c22ea-178">Cuando se muestra la página **Resource Creation** (Creación de recursos), especifique las opciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="c22ea-178">When the **Resource Creation** page is displayed, specify the following options:</span></span>

   <span data-ttu-id="c22ea-179">a.</span><span class="sxs-lookup"><span data-stu-id="c22ea-179">a.</span></span> <span data-ttu-id="c22ea-180">Seleccione **CREATE AN APP** (Crear una aplicación).</span><span class="sxs-lookup"><span data-stu-id="c22ea-180">Select **CREATE AN APP**.</span></span>

   <span data-ttu-id="c22ea-181">b.</span><span class="sxs-lookup"><span data-stu-id="c22ea-181">b.</span></span> <span data-ttu-id="c22ea-182">Escriba el nombre de la aplicación Spring Boot en **App name** (Nombre de aplicación); por ejemplo: "*gs-spring-boot-docker*".</span><span class="sxs-lookup"><span data-stu-id="c22ea-182">Enter your Spring Boot application name for the **App name**; for example: "*gs-spring-boot-docker*".</span></span>

   <span data-ttu-id="c22ea-183">c.</span><span class="sxs-lookup"><span data-stu-id="c22ea-183">c.</span></span> <span data-ttu-id="c22ea-184">Escriba el servidor de inicio de sesión y la imagen del contenedor de anteriormente en **Container image** (Imagen del contenedor); por ejemplo: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*".</span><span class="sxs-lookup"><span data-stu-id="c22ea-184">Enter your login server and container image from earlier for the **Container image**; for example: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*".</span></span>

   <span data-ttu-id="c22ea-185">d.</span><span class="sxs-lookup"><span data-stu-id="c22ea-185">d.</span></span> <span data-ttu-id="c22ea-186">Elija **External** (Externo) en **Service** (Servicio).</span><span class="sxs-lookup"><span data-stu-id="c22ea-186">Choose **External** for the **Service**.</span></span>

   <span data-ttu-id="c22ea-187">e.</span><span class="sxs-lookup"><span data-stu-id="c22ea-187">e.</span></span> <span data-ttu-id="c22ea-188">Especifique los puertos interno y externo en los cuadros de texto **Port** (Puerto) y **Target port** (Puerto de destino).</span><span class="sxs-lookup"><span data-stu-id="c22ea-188">Specify your external and internal ports in the **Port** and **Target port** text boxes.</span></span>

   ![Sitio web para la configuración de Kubernetes][KB02]


1. <span data-ttu-id="c22ea-190">Haga clic en **Deploy** (Implementar) para implementar el contenedor.</span><span class="sxs-lookup"><span data-stu-id="c22ea-190">Click **Deploy** to deploy the container.</span></span>

   ![Implementación de Kubernetes][KB05]

1. <span data-ttu-id="c22ea-192">Una vez que la aplicación se haya implementado, verá la aplicación Spring Boot en **Services** (Servicios).</span><span class="sxs-lookup"><span data-stu-id="c22ea-192">Once your application has been deployed, you will see your Spring Boot application listed under **Services**.</span></span>

   ![Servicios de Kubernetes][KB06]

1. <span data-ttu-id="c22ea-194">Si hace clic en el vínculo de **External endpoints** (Puntos de conexión externos), puede ver que la aplicación Spring Boot se ejecuta en Azure.</span><span class="sxs-lookup"><span data-stu-id="c22ea-194">If you click the link for **External endpoints**, you can see your Spring Boot application running on Azure.</span></span>

   ![Servicios de Kubernetes][KB07]

   ![Examen de la aplicación de ejemplo en Azure][SB02]

## <a name="next-steps"></a><span data-ttu-id="c22ea-197">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c22ea-197">Next steps</span></span>

<span data-ttu-id="c22ea-198">Para más información acerca de Spring y Azure, vaya al centro de documentación de Azure.</span><span class="sxs-lookup"><span data-stu-id="c22ea-198">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c22ea-199">Spring en Azure</span><span class="sxs-lookup"><span data-stu-id="c22ea-199">Spring on Azure</span></span>](/java/azure/spring-framework)

### <a name="additional-resources"></a><span data-ttu-id="c22ea-200">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="c22ea-200">Additional Resources</span></span>

<span data-ttu-id="c22ea-201">Para más información acerca del uso de Spring Boot en Azure, consulte el siguiente artículo:</span><span class="sxs-lookup"><span data-stu-id="c22ea-201">For more information about using Spring Boot on Azure, see the following article:</span></span>

* [<span data-ttu-id="c22ea-202">Implementación de una aplicación de Spring Boot en Azure App Service</span><span class="sxs-lookup"><span data-stu-id="c22ea-202">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)

<span data-ttu-id="c22ea-203">Para más información sobre el uso de Azure con Java, consulte [Azure para desarrolladores de Java] y [Working with Azure DevOps and Java] (Trabajo con Azure DevOps y Java).</span><span class="sxs-lookup"><span data-stu-id="c22ea-203">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Working with Azure DevOps and Java].</span></span>

<span data-ttu-id="c22ea-204">Para más información sobre cómo implementar una aplicación Java en Kubernetes con Visual Studio Code, consulte los [tutoriales de Visual Studio Code para Java].</span><span class="sxs-lookup"><span data-stu-id="c22ea-204">For more information about deploying a Java application to Kubernetes with Visual Studio Code, see [Visual Studio Code Java Tutorials].</span></span>

<span data-ttu-id="c22ea-205">Para más información acerca del proyecto de ejemplo Spring Boot on Docker, consulte [Spring Boot on Docker Getting Started].</span><span class="sxs-lookup"><span data-stu-id="c22ea-205">For more information about the Spring Boot on Docker sample project, see [Spring Boot on Docker Getting Started].</span></span>

<span data-ttu-id="c22ea-206">Los vínculos siguientes proporcionan información adicional acerca de cómo crear aplicaciones Spring Boot:</span><span class="sxs-lookup"><span data-stu-id="c22ea-206">The following links provide additional information about creating Spring Boot applications:</span></span>

* <span data-ttu-id="c22ea-207">Para más información acerca de cómo crear una sencilla aplicación de Spring Boot, consulte Spring Initializr en https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="c22ea-207">For more information about creating a simple Spring Boot application, see the Spring Initializr at https://start.spring.io/.</span></span>

<span data-ttu-id="c22ea-208">Los vínculos siguientes proporcionan información adicional acerca del uso de Kubernetes con Azure:</span><span class="sxs-lookup"><span data-stu-id="c22ea-208">The following links provide additional information about using Kubernetes with Azure:</span></span>

* [<span data-ttu-id="c22ea-209">Introducción a los clústeres de Kubernetes en Azure Kubernetes Service</span><span class="sxs-lookup"><span data-stu-id="c22ea-209">Get started with a Kubernetes cluster in Azure Kubernetes Service</span></span>](/azure/aks/intro-kubernetes)

<span data-ttu-id="c22ea-210">Para más información acerca de cómo usar la interfaz de línea de comandos de Kubernetes, consulte la guía de usuario de **kubectl** en <https://kubernetes.io/docs/user-guide/kubectl/>.</span><span class="sxs-lookup"><span data-stu-id="c22ea-210">More information about using Kubernetes command-line interface is available in the **kubectl** user guide at <https://kubernetes.io/docs/user-guide/kubectl/>.</span></span>

<span data-ttu-id="c22ea-211">El sitio web de Kubernetes tiene varios artículos que tratan el uso de imágenes en registros privados:</span><span class="sxs-lookup"><span data-stu-id="c22ea-211">The Kubernetes website has several articles that discuss using images in private registries:</span></span>

* <span data-ttu-id="c22ea-212">[Configure Service Accounts for Pods] (Configurar cuentas de servicio para pods)</span><span class="sxs-lookup"><span data-stu-id="c22ea-212">[Configuring Service Accounts for Pods]</span></span>
* <span data-ttu-id="c22ea-213">[Espacios de nombres]</span><span class="sxs-lookup"><span data-stu-id="c22ea-213">[Namespaces]</span></span>
* <span data-ttu-id="c22ea-214">[Pull an Image from a Private Registry] (Extraer una imagen de un registro privado)</span><span class="sxs-lookup"><span data-stu-id="c22ea-214">[Pulling an Image from a Private Registry]</span></span>

<span data-ttu-id="c22ea-215">Para ver más ejemplos de cómo usar imágenes de Docker personalizadas con Azure, consulte [Uso de una imagen personalizada de Docker para Web App on Linux de Azure].</span><span class="sxs-lookup"><span data-stu-id="c22ea-215">For additional examples for how to use custom Docker images with Azure, see [Using a custom Docker image for Azure Web App on Linux].</span></span>

<span data-ttu-id="c22ea-216">Para obtener más información sobre la ejecución de forma iterativa y la depuración de contenedores directamente en Azure Kubernetes Service (AKS) con Azure Dev Spaces, consulte [Introducción a Azure Dev Spaces con Java].</span><span class="sxs-lookup"><span data-stu-id="c22ea-216">For more information about iteratively running and debugging containers directly in Azure Kubernetes Service (AKS) with Azure Dev Spaces, see [Get started on Azure Dev Spaces with Java]</span></span>

<!-- URL List -->

[Interfaz de la línea de comandos (CLI) de Azure]: /cli/azure/overview
[Azure Command-Line Interface (CLI)]: /cli/azure/overview
[Azure Kubernetes Service (AKS)]: https://azure.microsoft.com/services/kubernetes-service/
[Azure para desarrolladores de Java]: /java/azure/
[Azure for Java Developers]: /java/azure/
[Azure portal]: https://portal.azure.com/
[Create a private Docker container registry using the Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Uso de una imagen personalizada de Docker para Web App on Linux de Azure]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Using a custom Docker image for Azure Web App on Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[cuenta de Azure gratuita]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Working with Azure DevOps and Java]: /azure/devops/java/ (Trabajo con Azure DevOps y Java)
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
[Autenticación con Azure Container Registry desde Azure Kubernetes Service (AKS)]: /azure/container-registry/container-registry-auth-aks/
[Authenticate with Azure Container Registry from Azure Kubernetes Service]: /azure/container-registry/container-registry-auth-aks/
[Tutoriales de Visual Studio Code para Java]: https://code.visualstudio.com/docs/java/java-kubernetes/
[Visual Studio Code Java Tutorials]: https://code.visualstudio.com/docs/java/java-kubernetes/
[Introducción a Azure Dev Spaces con Java]: https://docs.microsoft.com/en-us/azure/dev-spaces/get-started-java
[Get started on Azure Dev Spaces with Java]: https://docs.microsoft.com/en-us/azure/dev-spaces/get-started-java
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
