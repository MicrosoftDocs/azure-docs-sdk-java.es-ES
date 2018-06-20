---
title: Implementación de una aplicación Spring Boot mediante el complemento Fabric8 para Maven
description: En este tutorial se le guiará por los pasos necesarios para implementar una aplicación Spring Boot en Microsoft Azure con el complemento Fabric8 para Apache Maven.
services: container-service
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: yuwzho;robmcm
ms.date: 02/01/2018
ms.devlang: java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: 396d0ecfb051109924f09ae8b5d9b8074e49c404
ms.sourcegitcommit: 151aaa6ccc64d94ed67f03e846bab953bde15b4a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/03/2018
ms.locfileid: "28954896"
---
# <a name="deploy-a-spring-boot-app-using-the-fabric8-maven-plugin"></a><span data-ttu-id="cfb79-103">Implementación de una aplicación Spring Boot mediante el complemento Fabric8 para Maven</span><span class="sxs-lookup"><span data-stu-id="cfb79-103">Deploy a Spring Boot app using the Fabric8 Maven Plugin</span></span>

<span data-ttu-id="cfb79-104">**[Fabric8]** es una solución de código abierto basada en **[Kubernetes]** que permite que los desarrolladores creen aplicaciones en los contenedores Linux.</span><span class="sxs-lookup"><span data-stu-id="cfb79-104">**[Fabric8]** is an open-source solution that is built on **[Kubernetes]**, which helps developers create applications in Linux containers.</span></span>

<span data-ttu-id="cfb79-105">En este tutorial se explica cómo usar el complemento Fabric8 para Maven para desarrollar e implementar una aplicación en un host Linux en [Azure Container Service (AKS)].</span><span class="sxs-lookup"><span data-stu-id="cfb79-105">This tutorial walks you through using the Fabric8 plugin for Maven to develop to deploy an application to a Linux host in the [Azure Container Service (AKS)].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cfb79-106">requisitos previos</span><span class="sxs-lookup"><span data-stu-id="cfb79-106">Prerequisites</span></span>

<span data-ttu-id="cfb79-107">Para realizar los pasos de este tutorial, necesitará tener los siguientes requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="cfb79-107">In order to complete the steps in this tutorial, you need to have the following prerequisites:</span></span>

* <span data-ttu-id="cfb79-108">Una suscripción de Azure. Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN] o registrarse para obtener una [cuenta de Azure gratuita].</span><span class="sxs-lookup"><span data-stu-id="cfb79-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="cfb79-109">La [Interfaz de la línea de comandos (CLI) de Azure].</span><span class="sxs-lookup"><span data-stu-id="cfb79-109">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="cfb79-110">Un [kit para desarrolladores de Java (JDK)] actualizado.</span><span class="sxs-lookup"><span data-stu-id="cfb79-110">An up-to-date [Java Developer Kit (JDK)].</span></span>
* <span data-ttu-id="cfb79-111">La herramienta de compilación [Maven] de Apache (versión 3).</span><span class="sxs-lookup"><span data-stu-id="cfb79-111">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="cfb79-112">Un cliente [Git].</span><span class="sxs-lookup"><span data-stu-id="cfb79-112">A [Git] client.</span></span>
* <span data-ttu-id="cfb79-113">Un [cliente de Docker].</span><span class="sxs-lookup"><span data-stu-id="cfb79-113">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="cfb79-114">Dados los requisitos de virtualización de este tutorial, los pasos que se describen en este artículo no se pueden seguir en una máquina virtual; es preciso usar un equipo físico con características de virtualización habilitadas.</span><span class="sxs-lookup"><span data-stu-id="cfb79-114">Due to the virtualization requirements of this tutorial, you cannot follow the steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="create-the-spring-boot-on-docker-getting-started-web-app"></a><span data-ttu-id="cfb79-115">Creación de la aplicación web Spring Boot on Docker Getting Started</span><span class="sxs-lookup"><span data-stu-id="cfb79-115">Create the Spring Boot on Docker Getting Started web app</span></span>

<span data-ttu-id="cfb79-116">Los siguientes pasos le guían a través de la creación de una aplicación web Spring Boot y la realización de pruebas de la misma de forma local.</span><span class="sxs-lookup"><span data-stu-id="cfb79-116">The following steps walk you through building a Spring Boot web application and testing it locally.</span></span>

1. <span data-ttu-id="cfb79-117">Abra el símbolo del sistema, cree un directorio local para alojar la aplicación y cambie a dicho directorio, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="cfb79-117">Open a command-prompt and create a local directory to hold your application, and change to that directory; for example:</span></span>
   ```shell
   md /home/GenaSoto/SpringBoot
   cd /home/GenaSoto/SpringBoot
   ```
   <span data-ttu-id="cfb79-118">-- o --</span><span class="sxs-lookup"><span data-stu-id="cfb79-118">-- or --</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```

1. <span data-ttu-id="cfb79-119">Clone el proyecto de ejemplo [Spring Boot on Docker Getting Started] en el directorio.</span><span class="sxs-lookup"><span data-stu-id="cfb79-119">Clone the [Spring Boot on Docker Getting Started] sample project into the directory.</span></span>
   ```shell
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. <span data-ttu-id="cfb79-120">Cambie de directorio al del proyecto finalizado, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="cfb79-120">Change directory to the completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot-docker/complete
   ```
   <span data-ttu-id="cfb79-121">-- o --</span><span class="sxs-lookup"><span data-stu-id="cfb79-121">-- or --</span></span>
   ```shell
   cd gs-spring-boot-docker\complete
   ```

1. <span data-ttu-id="cfb79-122">Utilice Maven para compilar y ejecutar la aplicación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="cfb79-122">Use Maven to build and run the sample app.</span></span>
   ```shell
   mvn clean package spring-boot:run
   ```

1. <span data-ttu-id="cfb79-123">Pruebe la aplicación web examinando http://localhost:8080 o con el siguiente comando `curl`:</span><span class="sxs-lookup"><span data-stu-id="cfb79-123">Test the web app by browsing to http://localhost:8080, or with the following `curl` command:</span></span>
   ```shell
   curl http://localhost:8080
   ```

   <span data-ttu-id="cfb79-124">Debería aparecer el siguiente mensaje: **Hello Docker World**.</span><span class="sxs-lookup"><span data-stu-id="cfb79-124">You should see a **Hello Docker World** message displayed.</span></span>

   ![Examinar localmente la aplicación de ejemplo][SB01]


## <a name="install-the-kubernetes-command-line-interface-and-create-an-azure-resource-group-using-the-azure-cli"></a><span data-ttu-id="cfb79-126">Instalación de la interfaz de la línea de comandos de Kubernetes y creación de un grupo de recursos de Azure con la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="cfb79-126">Install the Kubernetes command-line interface and create an Azure resource group using the Azure CLI</span></span>

1. <span data-ttu-id="cfb79-127">Abra el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="cfb79-127">Open a command prompt.</span></span>

1. <span data-ttu-id="cfb79-128">Escriba el comando siguiente para iniciar sesión en la cuenta de Azure:</span><span class="sxs-lookup"><span data-stu-id="cfb79-128">Type the following command to log in to your Azure account:</span></span>
   ```azurecli
   az login
   ```
   <span data-ttu-id="cfb79-129">Siga las instrucciones para completar el proceso de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="cfb79-129">Follow the instructions to complete the login process</span></span>
   
   <span data-ttu-id="cfb79-130">La CLI de Azure mostrará una lista de las cuentas, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="cfb79-130">The Azure CLI will display a list of your accounts; for example:</span></span>

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

1. <span data-ttu-id="cfb79-131">Si todavía no tiene instalada la interfaz de la línea de comandos de Kubernetes (`kubectl`), puede instalar con la CLI de Azure, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="cfb79-131">If you do not already have the Kubernetes command-line interface (`kubectl`) installed, you can install using the Azure CLI; for example:</span></span>
   ```azurecli
   az acs kubernetes install-cli
   ```

   > [!NOTE]
   >
   > <span data-ttu-id="cfb79-132">Los usuarios de Linux pueden tener anteceder este comando con `sudo`, ya que implementa la CLI de Kubernetes en `/usr/local/bin`.</span><span class="sxs-lookup"><span data-stu-id="cfb79-132">Linux users may have to prefix this command with `sudo` since it deploys the Kubernetes CLI to `/usr/local/bin`.</span></span>
   >
   > <span data-ttu-id="cfb79-133">Si ya tiene instalado `kubectl` y la versión de `kubectl` es demasiado antigua, es posible que vea un mensaje de error similar al ejemplo siguiente cuando intente completar los pasos que aparecen más adelante en el artículo:</span><span class="sxs-lookup"><span data-stu-id="cfb79-133">If you already have `kubectl`) installed and your version of `kubectl` is too old, you may see an error message similar to the following example when you attempt to complete the steps listed later in this article:</span></span>
   >
   > ```
   > error: group map[autoscaling:0x0000000000 batch:0x0000000000 certificates.k8s.io
   > :0x0000000000 extensions:0x0000000000 storage.k8s.io:0x0000000000 apps:0x0000000
   > 000 authentication.k8s.io:0x0000000000 policy:0x0000000000 rbac.authorization.k8
   > s.io:0x0000000000 federation:0x0000000000 authorization.k8s.io:0x0000000000 comp
   > onentconfig:0x0000000000] is already registered
   > ```
   >
   > <span data-ttu-id="cfb79-134">Si esto ocurre, deberá reinstalar `kubectl` para actualizar la versión.</span><span class="sxs-lookup"><span data-stu-id="cfb79-134">If this happens, you will need to reinstall `kubectl` to update your version.</span></span>
   >

1. <span data-ttu-id="cfb79-135">Cree un grupo de recursos para los recursos de Azure que se usarán en este tutorial, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="cfb79-135">Create a resource group for the Azure resources that you will use in this tutorial; for example:</span></span>
   ```azurecli
   az group create --name=wingtiptoys-kubernetes --location=westeurope
   ```
   <span data-ttu-id="cfb79-136">Donde:</span><span class="sxs-lookup"><span data-stu-id="cfb79-136">Where:</span></span>  
      * <span data-ttu-id="cfb79-137">*wingtiptoys-kubernetes* es un nombre único para el grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="cfb79-137">*wingtiptoys-kubernetes* is a unique name for your resource group</span></span>  
      * <span data-ttu-id="cfb79-138">*westeurope* es una ubicación geográfica adecuada para la aplicación</span><span class="sxs-lookup"><span data-stu-id="cfb79-138">*westeurope* is an appropriate geographic location for your application</span></span>  

   <span data-ttu-id="cfb79-139">La CLI de Azure mostrará los resultados de la creación del grupo de recursos, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="cfb79-139">The Azure CLI will display the results of your resource group creation; for example:</span></span>  

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


## <a name="create-a-kubernetes-cluster-using-the-azure-cli"></a><span data-ttu-id="cfb79-140">Creación de un clúster de Kubernetes mediante la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="cfb79-140">Create a Kubernetes cluster using the Azure CLI</span></span>

1. <span data-ttu-id="cfb79-141">Cree un clúster de Kubernetes en el grupo de recursos nuevo, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="cfb79-141">Create a Kubernetes cluster in your new resource group; for example:</span></span>  
   ```azurecli 
   az acs create --orchestrator-type kubernetes --resource-group wingtiptoys-kubernetes --name wingtiptoys-cluster --generate-ssh-keys --dns-prefix=wingtiptoys
   ```
   <span data-ttu-id="cfb79-142">Donde:</span><span class="sxs-lookup"><span data-stu-id="cfb79-142">Where:</span></span>  
      * <span data-ttu-id="cfb79-143">*wingtiptoys-kubernetes* es el nombre del grupo de recursos que se mencionó anteriormente en el artículo</span><span class="sxs-lookup"><span data-stu-id="cfb79-143">*wingtiptoys-kubernetes* is the name of your resource group from earlier in this article</span></span>  
      * <span data-ttu-id="cfb79-144">*wingtiptoys-cluster* es un nombre único para el clúster de Kubernetes</span><span class="sxs-lookup"><span data-stu-id="cfb79-144">*wingtiptoys-cluster* is a unique name for your Kubernetes cluster</span></span>
      * <span data-ttu-id="cfb79-145">*wingtiptoys* es un nombre DNS único para la aplicación</span><span class="sxs-lookup"><span data-stu-id="cfb79-145">*wingtiptoys* is a unique name DNS name for your application</span></span>

   <span data-ttu-id="cfb79-146">La CLI de Azure mostrará los resultados de la creación del clúster, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="cfb79-146">The Azure CLI will display the results of your cluster creation; for example:</span></span>  

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

1. <span data-ttu-id="cfb79-147">Descargue las credenciales del clúster de Kubernetes nuevo, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="cfb79-147">Download your credentials for your new Kubernetes cluster; for example:</span></span>  
   ```azurecli 
   az acs kubernetes get-credentials --resource-group=wingtiptoys-kubernetes --name wingtiptoys-cluster
   ```

1. <span data-ttu-id="cfb79-148">Compruebe la conexión con el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="cfb79-148">Verify your connection with the following command:</span></span>
   ```shell 
   kubectl get nodes
   ```

   <span data-ttu-id="cfb79-149">Debería ver una lista de nodos y estados, como en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="cfb79-149">You should see a list of nodes and statuses like the following example:</span></span>

   ```shell
   NAME                    STATUS                     AGE       VERSION
   k8s-agent-00000000-0    Ready                      5h        v1.6.6
   k8s-agent-00000000-1    Ready                      5h        v1.6.6
   k8s-agent-00000000-2    Ready                      5h        v1.6.6
   k8s-master-00000000-0   Ready,SchedulingDisabled   5h        v1.6.6
   ```


## <a name="create-a-private-azure-container-registry-using-the-azure-cli"></a><span data-ttu-id="cfb79-150">Creación de un registro de contenedor privado de Azure con la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="cfb79-150">Create a private Azure container registry using the Azure CLI</span></span>

1. <span data-ttu-id="cfb79-151">Cree un registro de contenedor privado de Azure en el grupo de recursos para hospedar la imagen de Docker, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="cfb79-151">Create a private Azure container registry in your resource group to host your Docker image; for example:</span></span>
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoys-kubernetes --location westeurope --name wingtiptoysregistry --sku Basic
   ```
   <span data-ttu-id="cfb79-152">Donde:</span><span class="sxs-lookup"><span data-stu-id="cfb79-152">Where:</span></span>
   | <span data-ttu-id="cfb79-153">.</span><span class="sxs-lookup"><span data-stu-id="cfb79-153">Parameter</span></span> | <span data-ttu-id="cfb79-154">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="cfb79-154">Description</span></span> |
   |---|---|
   | `wingtiptoys-kubernetes` | <span data-ttu-id="cfb79-155">Especifica el nombre del grupo de recursos que se mencionó anteriormente en este artículo.</span><span class="sxs-lookup"><span data-stu-id="cfb79-155">Specifies the name of your resource group from earlier in this article.</span></span> |
   | `wingtiptoysregistry` | <span data-ttu-id="cfb79-156">Especifica un nombre único para el registro privado.</span><span class="sxs-lookup"><span data-stu-id="cfb79-156">Specifies a unique name for your private registry.</span></span> |
   | `westeurope` | <span data-ttu-id="cfb79-157">Especifica una ubicación geográfica adecuada para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="cfb79-157">Specifies an appropriate geographic location for your application.</span></span> |

   <span data-ttu-id="cfb79-158">La CLI de Azure mostrará los resultados de la creación del registro, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="cfb79-158">The Azure CLI will display the results of your registry creation; for example:</span></span>  

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

1. <span data-ttu-id="cfb79-159">Recupere la contraseña del registro de contenedor de la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="cfb79-159">Retrieve the password for your container registry from the Azure CLI.</span></span>
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```

   <span data-ttu-id="cfb79-160">La CLI de Azure mostrará la contraseña del registro, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="cfb79-160">The Azure CLI will display the password for your registry; for example:</span></span>  

   ```json
   {
     "name": "password",
     "value": "AbCdEfGhIjKlMnOpQrStUvWxYz"
   }
   ```

1. <span data-ttu-id="cfb79-161">Navegue hasta el directorio de configuración de la instalación de Maven (valor predeterminado ~/.m2/ o C:\Users\username\.m2) y abra el archivo *settings.xml* con un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="cfb79-161">Navigate to the configuration directory for your Maven installation (default ~/.m2/ or C:\Users\username\.m2) and open the *settings.xml* file with a text editor.</span></span>

1. <span data-ttu-id="cfb79-162">Agregue la dirección URL de Azure Container Registry, el nombre de usuario y la contraseña a una colección nueva de `<server>` en el archivo *settings.xml*.</span><span class="sxs-lookup"><span data-stu-id="cfb79-162">Add your Azure Container Registry URL, username and password to a new `<server>` collection in the *settings.xml* file.</span></span>
<span data-ttu-id="cfb79-163">`id` y `username` son el nombre del registro.</span><span class="sxs-lookup"><span data-stu-id="cfb79-163">The `id` and `username` are the name of the registry.</span></span> <span data-ttu-id="cfb79-164">Use el valor `password` del comando anterior (sin comillas).</span><span class="sxs-lookup"><span data-stu-id="cfb79-164">Use the `password` value from the previous command (without quotes).</span></span>

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry.azurecr.io</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

1. <span data-ttu-id="cfb79-165">Navegue hasta el directorio de proyecto completado de la aplicación Spring Boot (por ejemplo, "*C:\SpringBoot\gs-spring-boot-docker\complete*" o "*/home/GenaSoto/SpringBoot/gs-spring-boot-docker/complete*") y abra el archivo *pom.xml* con un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="cfb79-165">Navigate to the completed project directory for your Spring Boot application (for example, "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/home/GenaSoto/SpringBoot/gs-spring-boot-docker/complete*"), and open the *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="cfb79-166">Actualice la colección `<properties>` del archivo *pom.xml* con el valor del servidor de inicio de sesión de Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="cfb79-166">Update the `<properties>` collection in the *pom.xml* file with the login server value for your Azure Container Registry.</span></span>

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

1. <span data-ttu-id="cfb79-167">Actualice la colección `<plugins>` del archivo *pom.xml* de modo que `<plugin>` contiene la dirección del servidor de inicio de sesión y el nombre de registro de Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="cfb79-167">Update the `<plugins>` collection in the *pom.xml* file so that the `<plugin>` contains the login server address and registry name for your Azure Container Registry.</span></span>

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

1. <span data-ttu-id="cfb79-168">Navegue hasta el directorio de proyecto completado de la aplicación Spring Boot y ejecute el comando Maven siguiente para compilar el contenedor Docker e insertar la imagen en el registro:</span><span class="sxs-lookup"><span data-stu-id="cfb79-168">Navigate to the completed project directory for your Spring Boot application, and run the following Maven command to build the Docker container and push the image to your registry:</span></span>

   ```shell
   mvn package dockerfile:build -DpushImage
   ```

   <span data-ttu-id="cfb79-169">Maven mostrará los resultados de la compilación, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="cfb79-169">Maven will display the results of your build; for example:</span></span>  

   ```shell
   [INFO] ----------------------------------------------------
   [INFO] BUILD SUCCESS
   [INFO] ----------------------------------------------------
   [INFO] Total time: 38.113 s
   [INFO] Finished at: 2017-09-15T02:00:00-07:00
   [INFO] Final Memory: 47M/338M
   [INFO] ----------------------------------------------------
   ```


## <a name="configure-your-spring-boot-app-to-use-the-fabric8-maven-plugin"></a><span data-ttu-id="cfb79-170">Configuración de la aplicación Spring Boot para usar el complemento Fabric8 para Maven</span><span class="sxs-lookup"><span data-stu-id="cfb79-170">Configure your Spring Boot app to use the Fabric8 Maven plugin</span></span>

1. <span data-ttu-id="cfb79-171">Navegue hasta el directorio de proyecto completado de la aplicación Spring Boot (por ejemplo, "*C:\SpringBoot\gs-spring-boot-docker\complete*" o "*/home/GenaSoto/SpringBoot/gs-spring-boot-docker/complete*") y abra el archivo *pom.xml* con un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="cfb79-171">Navigate to the completed project directory for your Spring Boot application, (for example: "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/home/GenaSoto/SpringBoot/gs-spring-boot-docker/complete*"), and open the *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="cfb79-172">Actualice la colección de `<plugins>` en el archivo *pom.xml* para agregar el complemento Fabric8 para Maven:</span><span class="sxs-lookup"><span data-stu-id="cfb79-172">Update the `<plugins>` collection in the *pom.xml* file to add the Fabric8 Maven plugin:</span></span>

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

1. <span data-ttu-id="cfb79-173">Navegue al directorio de origen principal de la aplicación Spring Boot (por ejemplo, "*C:\SpringBoot\gs-spring-boot-docker\complete\src\main*" o "*/home/GenaSoto/SpringBoot/gs-spring-boot-docker/complete/src/main*") y cree una carpeta nueva denominada "*fabric8*".</span><span class="sxs-lookup"><span data-stu-id="cfb79-173">Navigate to the main source directory for your Spring Boot application, (for example: "*C:\SpringBoot\gs-spring-boot-docker\complete\src\main*" or "*/home/GenaSoto/SpringBoot/gs-spring-boot-docker/complete/src/main*"), and create a new folder named "*fabric8*".</span></span>

1. <span data-ttu-id="cfb79-174">Cree tres archivos de fragmentos YAML en la carpeta *fabric8* nueva:</span><span class="sxs-lookup"><span data-stu-id="cfb79-174">Create three YAML fragment files in the new *fabric8* folder:</span></span>

   <span data-ttu-id="cfb79-175">a.</span><span class="sxs-lookup"><span data-stu-id="cfb79-175">a.</span></span> <span data-ttu-id="cfb79-176">Cree un archivo denominado **deployment.yml** con el contenido siguiente:</span><span class="sxs-lookup"><span data-stu-id="cfb79-176">Create a file named **deployment.yml** with the following contents:</span></span>
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

   <span data-ttu-id="cfb79-177">b.</span><span class="sxs-lookup"><span data-stu-id="cfb79-177">b.</span></span> <span data-ttu-id="cfb79-178">Cree un archivo denominado **secrets.yml** con el contenido siguiente:</span><span class="sxs-lookup"><span data-stu-id="cfb79-178">Create a file named **secrets.yml** with the following contents:</span></span>
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

   <span data-ttu-id="cfb79-179">c.</span><span class="sxs-lookup"><span data-stu-id="cfb79-179">c.</span></span> <span data-ttu-id="cfb79-180">Cree un archivo denominado **service.yml** con el contenido siguiente:</span><span class="sxs-lookup"><span data-stu-id="cfb79-180">Create a file named **service.yml** with the following contents:</span></span>
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

1. <span data-ttu-id="cfb79-181">Ejecute el comando Maven siguiente para compilar el archivo de lista de recursos de Kubernetes:</span><span class="sxs-lookup"><span data-stu-id="cfb79-181">Run the following Maven command to build the Kubernetes resource list file:</span></span>

   ```shell
   mvn fabric8:resource
   ```

   <span data-ttu-id="cfb79-182">Este comando combina todos los archivos YAML de recursos de Kubernetes de la carpeta *src/main/fabric8* en un archivo YAML que contiene una lista de recursos de Kubernetes, que se puede aplicar directamente al clúster de Kubernetes o exportar a un gráfico de Helm.</span><span class="sxs-lookup"><span data-stu-id="cfb79-182">This command merges all Kubernetes resource yaml files under the *src/main/fabric8* folder to a YAML file that contains a Kubernetes resource list, which can be applied to Kubernetes cluster directly or export to a helm chart.</span></span>

   <span data-ttu-id="cfb79-183">Maven mostrará los resultados de la compilación, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="cfb79-183">Maven will display the results of your build; for example:</span></span>  

   ```shell
   [INFO] ----------------------------------------------------
   [INFO] BUILD SUCCESS
   [INFO] ----------------------------------------------------
   [INFO] Total time: 16.744 s
   [INFO] Finished at: 2017-09-15T02:35:00-07:00
   [INFO] Final Memory: 30M/290M
   [INFO] ----------------------------------------------------
   ```

1. <span data-ttu-id="cfb79-184">Ejecute el comando Maven siguiente para aplicar el archivo de lista de recursos en el clúster de Kubernetes:</span><span class="sxs-lookup"><span data-stu-id="cfb79-184">Run the following Maven command to apply the resource list file to your Kubernetes cluster:</span></span>

   ```shell
   mvn fabric8:apply
   ```

   <span data-ttu-id="cfb79-185">Maven mostrará los resultados de la compilación, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="cfb79-185">Maven will display the results of your build; for example:</span></span>  

   ```shell
   [INFO] ----------------------------------------------------
   [INFO] BUILD SUCCESS
   [INFO] ----------------------------------------------------
   [INFO] Total time: 14.814 s
   [INFO] Finished at: 2017-09-15T02:41:00-07:00
   [INFO] Final Memory: 35M/288M
   [INFO] ----------------------------------------------------
   ```

1. <span data-ttu-id="cfb79-186">Una vez que la aplicación se implemente en el clúster, consulte la dirección IP externa con la aplicación `kubectl`, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="cfb79-186">Once the app is deployed to the cluster, query the external IP address using the `kubectl` application; for example:</span></span>
   ```shell
   kubectl get svc -w
   ```

   <span data-ttu-id="cfb79-187">`kubectl` mostrará las direcciones IP internas y externas, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="cfb79-187">`kubectl` will display your internal and external IP addresses; for example:</span></span>
   
   ```shell
   NAME                    CLUSTER-IP   EXTERNAL-IP   PORT(S)        AGE
   kubernetes              10.0.0.1     <none>        443/TCP        19h
   gs-spring-boot-docker   10.0.242.8   13.65.196.3   80:31215/TCP   3m
   ```
   
   <span data-ttu-id="cfb79-188">Puede usar la dirección IP externa para abrir la aplicación en un explorador web.</span><span class="sxs-lookup"><span data-stu-id="cfb79-188">You can use the external IP address to open your application in a web browser.</span></span>

   ![Examinar externamente la aplicación de ejemplo][SB02]

## <a name="delete-your-kubernetes-cluster"></a><span data-ttu-id="cfb79-190">Eliminación del clúster de Kubernetes</span><span class="sxs-lookup"><span data-stu-id="cfb79-190">Delete your Kubernetes cluster</span></span>

<span data-ttu-id="cfb79-191">Cuando ya no se necesita el clúster de Kubernetes, puede usar el comando `az group delete` para quitar el grupo de recursos, con lo que se quitarán todos los recursos relacionados, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="cfb79-191">When your Kubernetes cluster is no longer needed, you can use the `az group delete` command to remove the resource group, which will remove all of its related resources; for example:</span></span>

   ```azurecli
   az group delete --name wingtiptoys-kubernetes --yes --no-wait
   ```

## <a name="next-steps"></a><span data-ttu-id="cfb79-192">pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cfb79-192">Next steps</span></span>

<span data-ttu-id="cfb79-193">Para obtener más información sobre el uso de aplicaciones de Spring Boot en Azure, consulte los siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="cfb79-193">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="cfb79-194">Implementación de una aplicación de Spring Boot en Azure App Service</span><span class="sxs-lookup"><span data-stu-id="cfb79-194">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)
* [<span data-ttu-id="cfb79-195">Implementación de una aplicación de Spring Boot en Linux en Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="cfb79-195">Deploy a Spring Boot application on Linux in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-linux.md)
* [<span data-ttu-id="cfb79-196">Implementación de una aplicación de Spring Boot en un clúster de Kubernetes en Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="cfb79-196">Deploy a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="cfb79-197">Para más información sobre el uso de Azure con Java, consulte [Azure para desarrolladores de Java] y [Java Tools for Visual Studio Team Services] (Herramientas de Java para Visual Studio Team Services).</span><span class="sxs-lookup"><span data-stu-id="cfb79-197">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="cfb79-198">Para obtener más información sobre el proyecto de ejemplo Spring Boot en Docker, vea [Spring Boot on Docker Getting Started] (Introducción a Spring Boot en Docker).</span><span class="sxs-lookup"><span data-stu-id="cfb79-198">For further details about the Spring Boot on Docker sample project, see [Spring Boot on Docker Getting Started].</span></span>

<span data-ttu-id="cfb79-199">Para obtener ayuda para dar sus primeros pasos con sus propias aplicaciones Spring Boot, consulte **Spring Initializr** en <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="cfb79-199">For help with getting started with your own Spring Boot applications, see the **Spring Initializr** at <https://start.spring.io/>.</span></span>

<span data-ttu-id="cfb79-200">Para más información sobre cómo empezar a crear una aplicación Spring Boot sencilla, consulte Spring Initializr en <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="cfb79-200">For more information about getting started with creating a simple Spring Boot application, see the Spring Initializr at <https://start.spring.io/>.</span></span>

<span data-ttu-id="cfb79-201">Para ver más ejemplos de cómo usar imágenes de Docker personalizadas con Azure, consulte [Uso de una imagen personalizada de Docker para Web App on Linux de Azure].</span><span class="sxs-lookup"><span data-stu-id="cfb79-201">For additional examples for how to use custom Docker images with Azure, see [Using a custom Docker image for Azure Web App on Linux].</span></span>

<!-- URL List -->

[Interfaz de la línea de comandos (CLI) de Azure]: /cli/azure/overview
[Azure Command-Line Interface (CLI)]: /cli/azure/overview
[Azure Container Service (AKS)]: https://azure.microsoft.com/services/container-service/
[Azure para desarrolladores de Java]: https://docs.microsoft.com/java/azure/
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Azure portal]: https://portal.azure.com/
[Create a private Docker container registry using the Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Uso de una imagen personalizada de Docker para Web App on Linux de Azure]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Using a custom Docker image for Azure Web App on Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[cliente de Docker]: https://www.docker.com/
[Docker]: https://www.docker.com/
[Fabric8]: https://fabric8.io/
[cuenta de Azure gratuita]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[kit para desarrolladores de Java (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Kubernetes]: https://kubernetes.io/
[Maven]: http://maven.apache.org/
[ventajas como suscriptor de MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot on Docker Getting Started]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[SB01]: ./media/deploy-spring-boot-java-app-using-fabric8-maven-plugin/SB01.png
[SB02]: ./media/deploy-spring-boot-java-app-using-fabric8-maven-plugin/SB02.png
