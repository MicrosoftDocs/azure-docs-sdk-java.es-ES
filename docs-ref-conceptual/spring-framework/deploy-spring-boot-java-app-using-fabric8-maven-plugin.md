---
title: "Implementación de una aplicación Spring Boot mediante el complemento Fabric8 para Maven"
description: "En este tutorial se le guiará por los pasos necesarios para implementar una aplicación Spring Boot en Microsoft Azure con el complemento Fabric8 para Apache Maven."
services: container-service
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
keywords: Spring, Spring Boot, Spring Framework, Maven
ms.assetid: 
ms.service: container-service
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: java
ms.topic: article
ms.date: 10/11/2017
ms.author: yuwzho;robmcm
ms.custom: 
ms.openlocfilehash: 4a1ed7f4bfe7f3fe9483e5822912035eded72887
ms.sourcegitcommit: 7f8538e41c833deb69c300ad3431a431136a1f3e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/24/2017
---
# <a name="deploy-a-spring-boot-app-using-the-fabric8-maven-plugin"></a><span data-ttu-id="61b70-104">Implementación de una aplicación Spring Boot mediante el complemento Fabric8 para Maven</span><span class="sxs-lookup"><span data-stu-id="61b70-104">Deploy a Spring Boot app using the Fabric8 Maven Plugin</span></span>

<span data-ttu-id="61b70-105">**[Fabric8]** es una solución de código abierto basada en **[Kubernetes]** que permite que los desarrolladores creen aplicaciones en los contenedores Linux.</span><span class="sxs-lookup"><span data-stu-id="61b70-105">**[Fabric8]** is an open-source solution that is built on **[Kubernetes]**, which helps developers create applications in Linux containers.</span></span>

<span data-ttu-id="61b70-106">En este tutorial se explica cómo usar el complemento Fabric8 para Maven para desarrollar e implementar una aplicación en un host Linux en [Azure Container Service (ACS)].</span><span class="sxs-lookup"><span data-stu-id="61b70-106">This tutorial walks you through using the Fabric8 plugin for Maven to develop to deploy an application to a Linux host in the [Azure Container Service (ACS)].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="61b70-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="61b70-107">Prerequisites</span></span>

<span data-ttu-id="61b70-108">Para poder realizar los pasos de este tutorial, necesitará tener los siguientes requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="61b70-108">In order to complete the steps in this tutorial, you need to have the following prerequisites:</span></span>

* <span data-ttu-id="61b70-109">Una suscripción de Azure. Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN] o registrarse para obtener una [cuenta de Azure gratuita].</span><span class="sxs-lookup"><span data-stu-id="61b70-109">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="61b70-110">La [Interfaz de la línea de comandos (CLI) de Azure].</span><span class="sxs-lookup"><span data-stu-id="61b70-110">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="61b70-111">Un [kit para desarrolladores de Java (JDK)] actualizado.</span><span class="sxs-lookup"><span data-stu-id="61b70-111">An up-to-date [Java Developer Kit (JDK)].</span></span>
* <span data-ttu-id="61b70-112">La herramienta de compilación [Maven] de Apache (versión 3).</span><span class="sxs-lookup"><span data-stu-id="61b70-112">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="61b70-113">Un cliente [Git].</span><span class="sxs-lookup"><span data-stu-id="61b70-113">A [Git] client.</span></span>
* <span data-ttu-id="61b70-114">Un [cliente de Docker].</span><span class="sxs-lookup"><span data-stu-id="61b70-114">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="61b70-115">Dados los requisitos de virtualización de este tutorial, los pasos que se describen en este artículo no se pueden seguir en una máquina virtual; es preciso usar un equipo físico con características de virtualización habilitadas.</span><span class="sxs-lookup"><span data-stu-id="61b70-115">Due to the virtualization requirements of this tutorial, you cannot follow the steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="create-the-spring-boot-on-docker-getting-started-web-app"></a><span data-ttu-id="61b70-116">Creación de la aplicación web Spring Boot on Docker Getting Started</span><span class="sxs-lookup"><span data-stu-id="61b70-116">Create the Spring Boot on Docker Getting Started web app</span></span>

<span data-ttu-id="61b70-117">Los siguientes pasos le guían a través de la creación de una aplicación web Spring Boot y la realización de pruebas de la misma de forma local.</span><span class="sxs-lookup"><span data-stu-id="61b70-117">The following steps walk you through building a Spring Boot web application and testing it locally.</span></span>

1. <span data-ttu-id="61b70-118">Abra el símbolo del sistema, cree un directorio local para alojar la aplicación y cambie a dicho directorio, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="61b70-118">Open a command-prompt and create a local directory to hold your application, and change to that directory; for example:</span></span>
   ```shell
   md /home/GenaSoto/SpringBoot
   cd /home/GenaSoto/SpringBoot
   ```
   <span data-ttu-id="61b70-119">-- o --</span><span class="sxs-lookup"><span data-stu-id="61b70-119">-- or --</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```

1. <span data-ttu-id="61b70-120">Clone el proyecto de ejemplo [Spring Boot on Docker Getting Started] en el directorio.</span><span class="sxs-lookup"><span data-stu-id="61b70-120">Clone the [Spring Boot on Docker Getting Started] sample project into the directory.</span></span>
   ```shell
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. <span data-ttu-id="61b70-121">Cambie de directorio al del proyecto finalizado, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="61b70-121">Change directory to the completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot-docker/complete
   ```
   <span data-ttu-id="61b70-122">-- o --</span><span class="sxs-lookup"><span data-stu-id="61b70-122">-- or --</span></span>
   ```shell
   cd gs-spring-boot-docker\complete
   ```

1. <span data-ttu-id="61b70-123">Utilice Maven para compilar y ejecutar la aplicación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="61b70-123">Use Maven to build and run the sample app.</span></span>
   ```shell
   mvn clean package spring-boot:run
   ```

1. <span data-ttu-id="61b70-124">Pruebe la aplicación web examinando http://localhost:8080 o con el siguiente comando `curl`:</span><span class="sxs-lookup"><span data-stu-id="61b70-124">Test the web app by browsing to http://localhost:8080, or with the following `curl` command:</span></span>
   ```shell
   curl http://localhost:8080
   ```

   <span data-ttu-id="61b70-125">Debería aparecer el siguiente mensaje: **Hello Docker World**.</span><span class="sxs-lookup"><span data-stu-id="61b70-125">You should see a **Hello Docker World** message displayed.</span></span>

   ![Examinar localmente la aplicación de ejemplo][SB01]


## <a name="install-the-kubernetes-command-line-interface-and-create-an-azure-resource-group-using-the-azure-cli"></a><span data-ttu-id="61b70-127">Instalación de la interfaz de la línea de comandos de Kubernetes y creación de un grupo de recursos de Azure con la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="61b70-127">Install the Kubernetes command-line interface and create an Azure resource group using the Azure CLI</span></span>

1. <span data-ttu-id="61b70-128">Abra el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="61b70-128">Open a command prompt.</span></span>

1. <span data-ttu-id="61b70-129">Escriba el comando siguiente para iniciar sesión en la cuenta de Azure:</span><span class="sxs-lookup"><span data-stu-id="61b70-129">Type the following command to log in to your Azure account:</span></span>
   ```azurecli
   az login
   ```
   <span data-ttu-id="61b70-130">Siga las instrucciones para completar el proceso de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="61b70-130">Follow the instructions to complete the login process</span></span>
   
   <span data-ttu-id="61b70-131">La CLI de Azure mostrará una lista de las cuentas, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="61b70-131">The Azure CLI will display a list of your accounts; for example:</span></span>

   ```json
   [
     {
       "cloudName": "AzureCloud",
       "id": "00000000-0000-0000-0000-000000000000",
       "isDefault": false,
       "name": "Windows Azure MSDN - Visual Studio Ultimate",
       "state": "Enabled",
       "tenantId": "00000000-0000-0000-0000-000000000000",
       "user": {
         "name": "Gena.Soto@wingtiptoys.com",
         "type": "user"
       }
     }
   ]
   ```

1. <span data-ttu-id="61b70-132">Si todavía no tiene instalada la interfaz de la línea de comandos de Kubernetes (`kubectl`), puede instalar con la CLI de Azure, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="61b70-132">If you do not already have the Kubernetes command-line interface (`kubectl`) installed, you can install using the Azure CLI; for example:</span></span>
   ```azurecli
   az acs kubernetes install-cli
   ```

   > [!NOTE]
   >
   > <span data-ttu-id="61b70-133">Los usuarios de Linux pueden tener anteceder este comando con `sudo`, ya que implementa la CLI de Kubernetes en `/usr/local/bin`.</span><span class="sxs-lookup"><span data-stu-id="61b70-133">Linux users may have to prefix this command with `sudo` since it deploys the Kubernetes CLI to `/usr/local/bin`.</span></span>
   >
   > <span data-ttu-id="61b70-134">Si ya tiene instalado `kubectl` y la versión de `kubectl` es demasiado antigua, es posible que vea un mensaje de error similar al ejemplo siguiente cuando intente completar los pasos que aparecen más adelante en el artículo:</span><span class="sxs-lookup"><span data-stu-id="61b70-134">If you already have `kubectl`) installed and your version of `kubectl` is too old, you may see an error message similar to the following example when you attempt to complete the steps listed later in this article:</span></span>
   >
   > ```
   > error: group map[autoscaling:0x0000000000 batch:0x0000000000 certificates.k8s.io
   > :0x0000000000 extensions:0x0000000000 storage.k8s.io:0x0000000000 apps:0x0000000
   > 000 authentication.k8s.io:0x0000000000 policy:0x0000000000 rbac.authorization.k8
   > s.io:0x0000000000 federation:0x0000000000 authorization.k8s.io:0x0000000000 comp
   > onentconfig:0x0000000000] is already registered
   > ```
   >
   > <span data-ttu-id="61b70-135">Si esto ocurre, deberá reinstalar `kubectl` para actualizar la versión.</span><span class="sxs-lookup"><span data-stu-id="61b70-135">If this happens, you will need to reinstall `kubectl` to update your version.</span></span>
   >

1. <span data-ttu-id="61b70-136">Cree un grupo de recursos para los recursos de Azure que se usarán en este tutorial, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="61b70-136">Create a resource group for the Azure resources that you will use in this tutorial; for example:</span></span>
   ```azurecli
   az group create --name=wingtiptoys-kubernetes --location=westeurope
   ```
   <span data-ttu-id="61b70-137">Donde:</span><span class="sxs-lookup"><span data-stu-id="61b70-137">Where:</span></span>  
      * <span data-ttu-id="61b70-138">*wingtiptoys-kubernetes* es un nombre único para el grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="61b70-138">*wingtiptoys-kubernetes* is a unique name for your resource group</span></span>  
      * <span data-ttu-id="61b70-139">*westeurope* es una ubicación geográfica adecuada para la aplicación</span><span class="sxs-lookup"><span data-stu-id="61b70-139">*westeurope* is an appropriate geographic location for your application</span></span>  

   <span data-ttu-id="61b70-140">La CLI de Azure mostrará los resultados de la creación del grupo de recursos, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="61b70-140">The Azure CLI will display the results of your resource group creation; for example:</span></span>  

   ```json
   {
     "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/wingtiptoys-kubernetes",
     "location": "westeurope",
     "managedBy": null,
     "name": "wingtiptoys-kubernetes",
     "properties": {
       "provisioningState": "Succeeded"
     },
     "tags": null
   }
   ```


## <a name="create-a-kubernetes-cluster-using-the-azure-cli"></a><span data-ttu-id="61b70-141">Creación de un clúster de Kubernetes mediante la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="61b70-141">Create a Kubernetes cluster using the Azure CLI</span></span>

1. <span data-ttu-id="61b70-142">Cree un clúster de Kubernetes en el grupo de recursos nuevo, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="61b70-142">Create a Kubernetes cluster in your new resource group; for example:</span></span>  
   ```azurecli 
   az acs create --orchestrator-type kubernetes --resource-group wingtiptoys-kubernetes --name wingtiptoys-cluster --generate-ssh-keys --dns-prefix=wingtiptoys
   ```
   <span data-ttu-id="61b70-143">Donde:</span><span class="sxs-lookup"><span data-stu-id="61b70-143">Where:</span></span>  
      * <span data-ttu-id="61b70-144">*wingtiptoys-kubernetes* es el nombre del grupo de recursos que se mencionó anteriormente en el artículo</span><span class="sxs-lookup"><span data-stu-id="61b70-144">*wingtiptoys-kubernetes* is the name of your resource group from earlier in this article</span></span>  
      * <span data-ttu-id="61b70-145">*wingtiptoys-cluster* es un nombre único para el clúster de Kubernetes</span><span class="sxs-lookup"><span data-stu-id="61b70-145">*wingtiptoys-cluster* is a unique name for your Kubernetes cluster</span></span>
      * <span data-ttu-id="61b70-146">*wingtiptoys* es un nombre DNS único para la aplicación</span><span class="sxs-lookup"><span data-stu-id="61b70-146">*wingtiptoys* is a unique name DNS name for your application</span></span>

   <span data-ttu-id="61b70-147">La CLI de Azure mostrará los resultados de la creación del clúster, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="61b70-147">The Azure CLI will display the results of your cluster creation; for example:</span></span>  

   ```json
   {
     "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/wingtiptoys-kubernetes/providers/Microsoft.Resources/deployments/azurecli0000000000.00000000000",
     "name": "azurecli0000000000.00000000000",
     "properties": {
       "correlationId": "00000000-0000-0000-0000-000000000000",
       "debugSetting": null,
       "dependencies": [],
       "mode": "Incremental",
       "outputs": {
         "masterFQDN": {
           "type": "String",
           "value": "wingtiptoysmgmt.westeurope.cloudapp.azure.com"
         },
         "sshMaster0": {
           "type": "String",
           "value": "ssh azureuser@wingtiptoysmgmt.westeurope.cloudapp.azure.com -A -p 22"
         }
       },
       "parameters": {
         "clientSecret": {
           "type": "SecureString"
         }
       },
       "parametersLink": null,
       "providers": [
         {
           "id": null,
           "namespace": "Microsoft.ContainerService",
           "registrationState": null,
           "resourceTypes": [
             {
               "aliases": null,
               "apiVersions": null,
               "locations": [
                 "westeurope"
               ],
               "properties": null,
               "resourceType": "containerServices"
             }
           ]
         }
       ],
       "provisioningState": "Succeeded",
       "template": null,
       "templateLink": null,
       "timestamp": "2017-09-15T01:00:00.000000+00:00"
     },
     "resourceGroup": "wingtiptoys-kubernetes"
   }
   ```

1. <span data-ttu-id="61b70-148">Descargue las credenciales del clúster de Kubernetes nuevo, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="61b70-148">Download your credentials for your new Kubernetes cluster; for example:</span></span>  
   ```azurecli 
   az acs kubernetes get-credentials --resource-group=wingtiptoys-kubernetes --name wingtiptoys-cluster
   ```

1. <span data-ttu-id="61b70-149">Compruebe la conexión con el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="61b70-149">Verify your connection with the following command:</span></span>
   ```shell 
   kubectl get nodes
   ```

   <span data-ttu-id="61b70-150">Debería ver una lista de nodos y estados, como en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="61b70-150">You should see a list of nodes and statuses like the following example:</span></span>

   ```shell
   NAME                    STATUS                     AGE       VERSION
   k8s-agent-00000000-0    Ready                      5h        v1.6.6
   k8s-agent-00000000-1    Ready                      5h        v1.6.6
   k8s-agent-00000000-2    Ready                      5h        v1.6.6
   k8s-master-00000000-0   Ready,SchedulingDisabled   5h        v1.6.6
   ```


## <a name="create-a-private-azure-container-registry-using-the-azure-cli"></a><span data-ttu-id="61b70-151">Creación de un registro de contenedor privado de Azure con la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="61b70-151">Create a private Azure container registry using the Azure CLI</span></span>

1. <span data-ttu-id="61b70-152">Cree un registro de contenedor privado de Azure en el grupo de recursos para hospedar la imagen de Docker, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="61b70-152">Create a private Azure container registry in your resource group to host your Docker image; for example:</span></span>
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoys-kubernetes --location westeurope --name wingtiptoysregistry --sku Basic
   ```
   <span data-ttu-id="61b70-153">Donde:</span><span class="sxs-lookup"><span data-stu-id="61b70-153">Where:</span></span>  
      * <span data-ttu-id="61b70-154">*wingtiptoys-kubernetes* es el nombre del grupo de recursos que se mencionó anteriormente en el artículo</span><span class="sxs-lookup"><span data-stu-id="61b70-154">*wingtiptoys-kubernetes* is the name of your resource group from earlier in this article</span></span>  
      * <span data-ttu-id="61b70-155">*wingtiptoysregistry* es un nombre único para el registro privado</span><span class="sxs-lookup"><span data-stu-id="61b70-155">*wingtiptoysregistry* is a unique name for your private registry</span></span>
      * <span data-ttu-id="61b70-156">*westeurope* es una ubicación geográfica adecuada para la aplicación</span><span class="sxs-lookup"><span data-stu-id="61b70-156">*westeurope* is an appropriate geographic location for your application</span></span>  

   <span data-ttu-id="61b70-157">La CLI de Azure mostrará los resultados de la creación del registro, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="61b70-157">The Azure CLI will display the results of your registry creation; for example:</span></span>  

   ```json
   {
     "adminUserEnabled": true,
     "creationDate": "2017-09-15T01:00:00.000000+00:00",
     "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/wingtiptoys-kubernetes/providers/Microsoft.ContainerRegistry/registries/wingtiptoysregistry",
     "location": "westeurope",
     "loginServer": "wingtiptoysregistry.azurecr.io",
     "name": "wingtiptoysregistry",
     "provisioningState": "Succeeded",
     "resourceGroup": "wingtiptoys-kubernetes",
     "sku": {
       "name": "Basic",
       "tier": "Basic"
     },
     "storageAccount": {
       "name": "wingtiptoysregistr000000"
     },
     "tags": {},
     "type": "Microsoft.ContainerRegistry/registries"
   }
   ```

1. <span data-ttu-id="61b70-158">Recupere la contraseña del registro de contenedor de la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="61b70-158">Retrieve the password for your container registry from the Azure CLI.</span></span>
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```

   <span data-ttu-id="61b70-159">La CLI de Azure mostrará la contraseña del registro, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="61b70-159">The Azure CLI will display the password for your registry; for example:</span></span>  

   ```json
   {
     "name": "password",
     "value": "AbCdEfGhIjKlMnOpQrStUvWxYz"
   }
   ```

1. <span data-ttu-id="61b70-160">Navegue hasta el directorio de configuración de la instalación de Maven (valor predeterminado ~/.m2/ o C:\Users\username\.m2) y abra el archivo *settings.xml* con un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="61b70-160">Navigate to the configuration directory for your Maven installation (default ~/.m2/ or C:\Users\username\.m2) and open the *settings.xml* file with a text editor.</span></span>

1. <span data-ttu-id="61b70-161">Agregue la dirección URL de Azure Container Registry, el nombre de usuario y la contraseña a una colección nueva de `<server>` en el archivo *settings.xml*.</span><span class="sxs-lookup"><span data-stu-id="61b70-161">Add your Azure Container Registry URL, username and password to a new `<server>` collection in the *settings.xml* file.</span></span>
<span data-ttu-id="61b70-162">`id` y `username` son el nombre del registro.</span><span class="sxs-lookup"><span data-stu-id="61b70-162">The `id` and `username` are the name of the registry.</span></span> <span data-ttu-id="61b70-163">Use el valor `password` del comando anterior (sin comillas).</span><span class="sxs-lookup"><span data-stu-id="61b70-163">Use the `password` value from the previous command (without quotes).</span></span>

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry.azurecr.io</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

1. <span data-ttu-id="61b70-164">Navegue hasta el directorio de proyecto completado de la aplicación Spring Boot (por ejemplo, "*C:\SpringBoot\gs-spring-boot-docker\complete*" o "*/home/GenaSoto/SpringBoot/gs-spring-boot-docker/complete*") y abra el archivo *pom.xml* con un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="61b70-164">Navigate to the completed project directory for your Spring Boot application (for example, "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/home/GenaSoto/SpringBoot/gs-spring-boot-docker/complete*"), and open the *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="61b70-165">Actualice la colección `<properties>` del archivo *pom.xml* con el valor del servidor de inicio de sesión de Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="61b70-165">Update the `<properties>` collection in the *pom.xml* file with the login server value for your Azure Container Registry.</span></span>

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

1. <span data-ttu-id="61b70-166">Actualice la colección `<plugins>` del archivo *pom.xml* de modo que `<plugin>` contiene la dirección del servidor de inicio de sesión y el nombre de registro de Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="61b70-166">Update the `<plugins>` collection in the *pom.xml* file so that the `<plugin>` contains the login server address and registry name for your Azure Container Registry.</span></span>

   ```xml
   <plugin>
     <groupId>com.spotify</groupId>
     <artifactId>dockerfile-maven-plugin</artifactId>
     <version>1.3.4</version>
     <configuration>
       <repository>${docker.image.prefix}/${project.artifactId}</repository>
       <serverId>${docker.image.prefix}</serverId>
       <registryUrl>https://${docker.image.prefix}</registryUrl>
     </configuration>
   </plugin>
   ```

1. <span data-ttu-id="61b70-167">Navegue hasta el directorio de proyecto completado de la aplicación Spring Boot y ejecute el comando Maven siguiente para compilar el contenedor Docker e insertar la imagen en el registro:</span><span class="sxs-lookup"><span data-stu-id="61b70-167">Navigate to the completed project directory for your Spring Boot application, and run the following Maven command to build the Docker container and push the image to your registry:</span></span>

   ```shell
   mvn package dockerfile:build -DpushImage
   ```

   <span data-ttu-id="61b70-168">Maven mostrará los resultados de la compilación, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="61b70-168">Maven will display the results of your build; for example:</span></span>  

   ```shell
   [INFO] ----------------------------------------------------
   [INFO] BUILD SUCCESS
   [INFO] ----------------------------------------------------
   [INFO] Total time: 38.113 s
   [INFO] Finished at: 2017-09-15T02:00:00-07:00
   [INFO] Final Memory: 47M/338M
   [INFO] ----------------------------------------------------
   ```


## <a name="configure-your-spring-boot-app-to-use-the-fabric8-maven-plugin"></a><span data-ttu-id="61b70-169">Configuración de la aplicación Spring Boot para usar el complemento Fabric8 para Maven</span><span class="sxs-lookup"><span data-stu-id="61b70-169">Configure your Spring Boot app to use the Fabric8 Maven plugin</span></span>

1. <span data-ttu-id="61b70-170">Navegue hasta el directorio de proyecto completado de la aplicación Spring Boot (por ejemplo, "*C:\SpringBoot\gs-spring-boot-docker\complete*" o "*/home/GenaSoto/SpringBoot/gs-spring-boot-docker/complete*") y abra el archivo *pom.xml* con un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="61b70-170">Navigate to the completed project directory for your Spring Boot application, (for example: "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/home/GenaSoto/SpringBoot/gs-spring-boot-docker/complete*"), and open the *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="61b70-171">Actualice la colección de `<plugins>` en el archivo *pom.xml* para agregar el complemento Fabric8 para Maven:</span><span class="sxs-lookup"><span data-stu-id="61b70-171">Update the `<plugins>` collection in the *pom.xml* file to add the Fabric8 Maven plugin:</span></span>

   ```xml
   <plugin>
     <groupId>io.fabric8</groupId>
     <artifactId>fabric8-maven-plugin</artifactId>
     <version>3.5.30</version>
     <configuration>
       <ignoreServices>false</ignoreServices>
       <registry>${docker.image.prefix}</registry>
     </configuration>
   </plugin>
   ```

1. <span data-ttu-id="61b70-172">Navegue al directorio de origen principal de la aplicación Spring Boot (por ejemplo, "*C:\SpringBoot\gs-spring-boot-docker\complete\src\main*" o "*/home/GenaSoto/SpringBoot/gs-spring-boot-docker/complete/src/main*") y cree una carpeta nueva denominada "*fabric8*".</span><span class="sxs-lookup"><span data-stu-id="61b70-172">Navigate to the main source directory for your Spring Boot application, (for example: "*C:\SpringBoot\gs-spring-boot-docker\complete\src\main*" or "*/home/GenaSoto/SpringBoot/gs-spring-boot-docker/complete/src/main*"), and create a new folder named "*fabric8*".</span></span>

1. <span data-ttu-id="61b70-173">Cree tres archivos de fragmentos YAML en la carpeta *fabric8* nueva:</span><span class="sxs-lookup"><span data-stu-id="61b70-173">Create three YAML fragment files in the new *fabric8* folder:</span></span>

   <span data-ttu-id="61b70-174">a.</span><span class="sxs-lookup"><span data-stu-id="61b70-174">a.</span></span> <span data-ttu-id="61b70-175">Cree un archivo denominado **deployment.yml** con el contenido siguiente:</span><span class="sxs-lookup"><span data-stu-id="61b70-175">Create a file named **deployment.yml** with the following contents:</span></span>
      ```yaml
      apiVersion: extensions/v1beta1
      kind: Deployment
      metadata:
        name: ${project.artifactId}
        labels:
          run: gs-spring-boot-docker
      spec:
        replicas: 1
        selector:
          matchLabels:
            run: gs-spring-boot-docker
        strategy:
          rollingUpdate:
            maxSurge: 1
            maxUnavailable: 1
          type: RollingUpdate
        template:
          metadata:
            labels:
              run: gs-spring-boot-docker
          spec:
            containers:
            - image: ${docker.image.prefix}/${project.artifactId}:latest
              name: gs-spring-boot-docker
              imagePullPolicy: Always
              ports:
              - containerPort: 8080
            imagePullSecrets:
              - name: mysecrets
      ```

   <span data-ttu-id="61b70-176">b.</span><span class="sxs-lookup"><span data-stu-id="61b70-176">b.</span></span> <span data-ttu-id="61b70-177">Cree un archivo denominado **secrets.yml** con el contenido siguiente:</span><span class="sxs-lookup"><span data-stu-id="61b70-177">Create a file named **secrets.yml** with the following contents:</span></span>
      ```yaml
      apiVersion: v1
      kind: Secret
      metadata:
        name: mysecrets
        namespace: default
        annotations:
          maven.fabric8.io/dockerServerId:  ${docker.image.prefix}
      type: kubernetes.io/dockercfg
      ```

   <span data-ttu-id="61b70-178">c.</span><span class="sxs-lookup"><span data-stu-id="61b70-178">c.</span></span> <span data-ttu-id="61b70-179">Cree un archivo denominado **service.yml** con el contenido siguiente:</span><span class="sxs-lookup"><span data-stu-id="61b70-179">Create a file named **service.yml** with the following contents:</span></span>
      ```yaml
      apiVersion: v1
      kind: Service
      metadata:
        name: ${project.artifactId}
        labels:
          expose: "true"
      spec:
        ports:
        - port: 80
          targetPort: 8080
        type: LoadBalancer
      ```

1. <span data-ttu-id="61b70-180">Ejecute el comando Maven siguiente para compilar el archivo de lista de recursos de Kubernetes:</span><span class="sxs-lookup"><span data-stu-id="61b70-180">Run the following Maven command to build the Kubernetes resource list file:</span></span>

   ```shell
   mvn fabric8:resource
   ```

   <span data-ttu-id="61b70-181">Este comando combina todos los archivos YAML de recursos de Kubernetes de la carpeta *src/main/fabric8* en un archivo YAML que contiene una lista de recursos de Kubernetes, que se puede aplicar directamente al clúster de Kubernetes o exportar a un gráfico de Helm.</span><span class="sxs-lookup"><span data-stu-id="61b70-181">This command merges all Kubernetes resource yaml files under the *src/main/fabric8* folder to a YAML file that contains a Kubernetes resource list, which can be applied to Kubernetes cluster directly or export to a helm chart.</span></span>

   <span data-ttu-id="61b70-182">Maven mostrará los resultados de la compilación, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="61b70-182">Maven will display the results of your build; for example:</span></span>  

   ```shell
   [INFO] ----------------------------------------------------
   [INFO] BUILD SUCCESS
   [INFO] ----------------------------------------------------
   [INFO] Total time: 16.744 s
   [INFO] Finished at: 2017-09-15T02:35:00-07:00
   [INFO] Final Memory: 30M/290M
   [INFO] ----------------------------------------------------
   ```

1. <span data-ttu-id="61b70-183">Ejecute el comando Maven siguiente para aplicar el archivo de lista de recursos en el clúster de Kubernetes:</span><span class="sxs-lookup"><span data-stu-id="61b70-183">Run the following Maven command to apply the resource list file to your Kubernetes cluster:</span></span>

   ```shell
   mvn fabric8:apply
   ```

   <span data-ttu-id="61b70-184">Maven mostrará los resultados de la compilación, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="61b70-184">Maven will display the results of your build; for example:</span></span>  

   ```shell
   [INFO] ----------------------------------------------------
   [INFO] BUILD SUCCESS
   [INFO] ----------------------------------------------------
   [INFO] Total time: 14.814 s
   [INFO] Finished at: 2017-09-15T02:41:00-07:00
   [INFO] Final Memory: 35M/288M
   [INFO] ----------------------------------------------------
   ```

1. <span data-ttu-id="61b70-185">Una vez que la aplicación se implemente en el clúster, consulte la dirección IP externa con la aplicación `kubectl`, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="61b70-185">Once the app is deployed to the cluster, query the external IP address using the `kubectl` application; for example:</span></span>
   ```shell
   kubectl get svc -w
   ```

   <span data-ttu-id="61b70-186">`kubectl` mostrará las direcciones IP internas y externas, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="61b70-186">`kubectl` will display your internal and external IP addresses; for example:</span></span>
   
   ```shell
   NAME                    CLUSTER-IP   EXTERNAL-IP   PORT(S)        AGE
   kubernetes              10.0.0.1     <none>        443/TCP        19h
   gs-spring-boot-docker   10.0.242.8   13.65.196.3   80:31215/TCP   3m
   ```
   
   <span data-ttu-id="61b70-187">Puede usar la dirección IP externa para abrir la aplicación en un explorador web.</span><span class="sxs-lookup"><span data-stu-id="61b70-187">You can use the external IP address to open your application in a web browser.</span></span>

   ![Examinar externamente la aplicación de ejemplo][SB02]

## <a name="delete-your-kubernetes-cluster"></a><span data-ttu-id="61b70-189">Eliminación del clúster de Kubernetes</span><span class="sxs-lookup"><span data-stu-id="61b70-189">Delete your Kubernetes cluster</span></span>

<span data-ttu-id="61b70-190">Cuando ya no se necesita el clúster de Kubernetes, puede usar el comando `az group delete` para quitar el grupo de recursos, con lo que se quitarán todos los recursos relacionados, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="61b70-190">When your Kubernetes cluster is no longer needed, you can use the `az group delete` command to remove the resource group, which will remove all of its related resources; for example:</span></span>

   ```azurecli
   az group delete --name wingtiptoys-kubernetes --yes --no-wait
   ```

## <a name="next-steps"></a><span data-ttu-id="61b70-191">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="61b70-191">Next steps</span></span>

<span data-ttu-id="61b70-192">Para obtener más información sobre el uso de aplicaciones de Spring Boot en Azure, consulte los siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="61b70-192">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="61b70-193">Implementación de una aplicación de Spring Boot en Azure App Service</span><span class="sxs-lookup"><span data-stu-id="61b70-193">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)
* [<span data-ttu-id="61b70-194">Implementación de una aplicación de Spring Boot en Linux en Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="61b70-194">Deploy a Spring Boot application on Linux in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-linux.md)
* [<span data-ttu-id="61b70-195">Implementación de una aplicación de Spring Boot en un clúster de Kubernetes en Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="61b70-195">Deploy a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="61b70-196">Para obtener más información sobre el uso de Azure con Java, vea el [Centro para desarrolladores de Java de Azure] y [Java Tools for Visual Studio Team Services] (Herramientas de Java para Visual Studio Team Services).</span><span class="sxs-lookup"><span data-stu-id="61b70-196">For more information about using Azure with Java, see the [Azure Java Developer Center] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="61b70-197">Para obtener más información sobre el proyecto de ejemplo Spring Boot en Docker, vea [Spring Boot on Docker Getting Started] (Introducción a Spring Boot en Docker).</span><span class="sxs-lookup"><span data-stu-id="61b70-197">For further details about the Spring Boot on Docker sample project, see [Spring Boot on Docker Getting Started].</span></span>

<span data-ttu-id="61b70-198">Para obtener ayuda para dar sus primeros pasos con sus propias aplicaciones Spring Boot, consulte **Spring Initializr** en <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="61b70-198">For help with getting started with your own Spring Boot applications, see the **Spring Initializr** at <https://start.spring.io/>.</span></span>

<span data-ttu-id="61b70-199">Para más información sobre cómo empezar a crear una aplicación Spring Boot sencilla, consulte Spring Initializr en <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="61b70-199">For more information about getting started with creating a simple Spring Boot application, see the Spring Initializr at <https://start.spring.io/>.</span></span>

<span data-ttu-id="61b70-200">Para ver más ejemplos de cómo usar imágenes de Docker personalizadas con Azure, consulte [Uso de una imagen personalizada de Docker para Web App on Linux de Azure].</span><span class="sxs-lookup"><span data-stu-id="61b70-200">For additional examples for how to use custom Docker images with Azure, see [Using a custom Docker image for Azure Web App on Linux].</span></span>

<!-- URL List -->

[Interfaz de la línea de comandos (CLI) de Azure]: /cli/azure/overview
[Azure Container Service (ACS)]: https://azure.microsoft.com/services/container-service/
[Centro para desarrolladores de Java de Azure]: https://azure.microsoft.com/develop/java/
[Azure portal]: https://portal.azure.com/
[Create a private Docker container registry using the Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Uso de una imagen personalizada de Docker para Web App on Linux de Azure]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[cliente de Docker]: https://www.docker.com/
[Fabric8]: https://fabric8.io/
[cuenta de Azure gratuita]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[kit para desarrolladores de Java (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Kubernetes]: https://kubernetes.io/
[Maven]: http://maven.apache.org/
[ventajas como suscriptor de MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot on Docker Getting Started]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[SB01]: ./media/deploy-spring-boot-java-app-using-fabric8-maven-plugin/SB01.png
[SB02]: ./media/deploy-spring-boot-java-app-using-fabric8-maven-plugin/SB02.png
