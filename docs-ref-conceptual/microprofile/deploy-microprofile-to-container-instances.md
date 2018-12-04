---
title: Implementación de una aplicación de MicroProfile en la nube con Docker y Azure
description: Aprenda cómo implementar una aplicación de MicroProfile en la nube con Docker y Azure Container Instances.
services: container-instances;container-retistry
documentationcenter: java
author: brunoborges
manager: routlaw
editor: brunoborges
ms.assetid: ''
ms.author: brborges
ms.date: 11/21/2018
ms.devlang: java
ms.service: container-instances
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: 22870b7ba32f115e7270c63d1bf42cbfc6531d7e
ms.sourcegitcommit: 8d0c59ae7c91adbb9be3c3e6d4a3429ffe51519d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/27/2018
ms.locfileid: "52338789"
---
# <a name="deploy-a-microprofile-application-to-the-cloud-with-docker-and-azure"></a><span data-ttu-id="6a8b8-103">Implementación de una aplicación de MicroProfile en la nube con Docker y Azure</span><span class="sxs-lookup"><span data-stu-id="6a8b8-103">Deploy a MicroProfile application to the cloud with Docker and Azure</span></span>

<span data-ttu-id="6a8b8-104">En este artículo se muestra cómo empaquetar una aplicación de [MicroProfile.io] en un contenedor de Docker y ejecutarla en Azure Container Instances.</span><span class="sxs-lookup"><span data-stu-id="6a8b8-104">This article demonstrates how to pack a [MicroProfile.io] application in a Docker container and run it on Azure Container Instances.</span></span>

> [!NOTE]
>
> <span data-ttu-id="6a8b8-105">Este procedimiento funciona con cualquier implementación de MicroProfile.io siempre que la imagen del contenedor de Docker sea autoejecutable (es decir, que incluya el entorno de ejecución).</span><span class="sxs-lookup"><span data-stu-id="6a8b8-105">This procedure works with any implementation of MicroProfile.io as long the Docker container image is self-executable (i.e. includes the runtime).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6a8b8-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="6a8b8-106">Prerequisites</span></span>

<span data-ttu-id="6a8b8-107">Para realizar los pasos de este tutorial, necesitará tener los siguientes requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="6a8b8-107">In order to complete the steps in this tutorial, you will need to have the following prerequisites:</span></span>

* <span data-ttu-id="6a8b8-108">Si todavía no tiene una suscripción a Azure, puede registrarse para obtener una [cuenta de Azure gratuita].</span><span class="sxs-lookup"><span data-stu-id="6a8b8-108">An Azure subscription; if you don't already have an Azure subscription, you can sign up for a [free Azure account].</span></span>
* <span data-ttu-id="6a8b8-109">La [Interfaz de la línea de comandos (CLI) de Azure].</span><span class="sxs-lookup"><span data-stu-id="6a8b8-109">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="6a8b8-110">Un kit de desarrollo de Java (JDK) admitido</span><span class="sxs-lookup"><span data-stu-id="6a8b8-110">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="6a8b8-111">Para más información sobre los JDK disponibles para desarrollar en Azure, consulte <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="6a8b8-111">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="6a8b8-112">La herramienta de compilación [Maven] de Apache (versión 3 o posteriores).</span><span class="sxs-lookup"><span data-stu-id="6a8b8-112">Apache's [Maven] build tool (version 3+).</span></span>
* <span data-ttu-id="6a8b8-113">Un cliente [Git].</span><span class="sxs-lookup"><span data-stu-id="6a8b8-113">A [Git] client.</span></span>

## <a name="microprofile-hello-azure-sample"></a><span data-ttu-id="6a8b8-114">Ejemplo MicroProfile Hello Azure</span><span class="sxs-lookup"><span data-stu-id="6a8b8-114">MicroProfile Hello Azure sample</span></span>

<span data-ttu-id="6a8b8-115">En este artículo, usaremos el ejemplo [MicroProfile Hello Azure](https://github.com/azure-samples/microprofile-hello-azure):</span><span class="sxs-lookup"><span data-stu-id="6a8b8-115">For this article, we will use the [MicroProfile Hello Azure](https://github.com/azure-samples/microprofile-hello-azure) sample:</span></span>

### <a name="clone-build-and-run-locally"></a><span data-ttu-id="6a8b8-116">Clonación, compilación y ejecución local</span><span class="sxs-lookup"><span data-stu-id="6a8b8-116">Clone, build, and run locally</span></span>

```bash
$ git clone https://github.com/Azure-Samples/microprofile-hello-azure.git
$ mvn clean package
...
[INFO] BUILD SUCCESS
...
$ mvn payara-micro:start
...
[2018-07-30T13:34:51.553-0700] [] [INFO] [] [PayaraMicro] [tid: _ThreadID=1 _ThreadName=main] [timeMillis: 1532982891553] [levelValue: 800] Payara Micro  5.182 #badassmicrofish (build 303) ready in 10,304 (ms)
...
```

<span data-ttu-id="6a8b8-117">Para probar la aplicación, puede llamar a `curl` o visitarla mediante un [explorador](http://localhost:8080/api/hello):</span><span class="sxs-lookup"><span data-stu-id="6a8b8-117">You can test the application by calling `curl` or visiting through a [browser](http://localhost:8080/api/hello):</span></span>

```bash
$ curl http://localhost:8080/api/hello
Hello, Azure!
```

## <a name="deploy-to-azure"></a><span data-ttu-id="6a8b8-118">Implementar en Azure</span><span class="sxs-lookup"><span data-stu-id="6a8b8-118">Deploy to Azure</span></span>

<span data-ttu-id="6a8b8-119">Ahora vamos a poner esta aplicación en la nube con los servicios [Azure Container Instances] y [Azure Container Registry].</span><span class="sxs-lookup"><span data-stu-id="6a8b8-119">Now let's bring this application to the cloud using [Azure Container Instances] and [Azure Container Registry] services.</span></span>

### <a name="build-a-docker-image"></a><span data-ttu-id="6a8b8-120">Compilación de una imagen de Docker</span><span class="sxs-lookup"><span data-stu-id="6a8b8-120">Build a Docker image</span></span>

<span data-ttu-id="6a8b8-121">El proyecto de ejemplo ya incluye un archivo Dockerfile que se puede usar.</span><span class="sxs-lookup"><span data-stu-id="6a8b8-121">The sample project already provides a Dockerfile you can use.</span></span> <span data-ttu-id="6a8b8-122">No es necesario tener Docker instalado, porque usaremos la característica Azure Container Registry Build para compilar la imagen en la nube.</span><span class="sxs-lookup"><span data-stu-id="6a8b8-122">You don't need Docker installed though, as we will use Azure Container Registry Build feature to build the image in the cloud.</span></span>

<span data-ttu-id="6a8b8-123">Para compilar la imagen y prepararla para ejecutarla en Azure, debe seguir estos pasos:</span><span class="sxs-lookup"><span data-stu-id="6a8b8-123">To build the image and be ready to run on Azure, you will have to follow these steps:</span></span>

1. <span data-ttu-id="6a8b8-124">Instalación y inicio de sesión con la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="6a8b8-124">Install and log in with Azure CLI</span></span>
1. <span data-ttu-id="6a8b8-125">Crear un grupo de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="6a8b8-125">Create an Azure Resource Group</span></span>
1. <span data-ttu-id="6a8b8-126">Creación de un recurso de Azure Container Registry (ACR)</span><span class="sxs-lookup"><span data-stu-id="6a8b8-126">Create an Azure Container Registry (ACR)</span></span>
1. <span data-ttu-id="6a8b8-127">Compilación de la imagen de Docker</span><span class="sxs-lookup"><span data-stu-id="6a8b8-127">Build the Docker image</span></span>
1. <span data-ttu-id="6a8b8-128">Publicación de la imagen de Docker en el registro de contenedor creado anteriormente</span><span class="sxs-lookup"><span data-stu-id="6a8b8-128">Publish the Docker image to the ACR created before</span></span>
1. <span data-ttu-id="6a8b8-129">(Opcionalmente) Compilación y publicación en ACR en un solo comando</span><span class="sxs-lookup"><span data-stu-id="6a8b8-129">(Optionally) Build and publish to ACR in one command</span></span>


#### <a name="set-up-azure-cli"></a><span data-ttu-id="6a8b8-130">Configuración de la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="6a8b8-130">Set up Azure CLI</span></span>

<span data-ttu-id="6a8b8-131">Asegúrese de que tiene una suscripción de Azure, la [CLI de Azure instalada](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest) y de que se ha autenticado en su cuenta:</span><span class="sxs-lookup"><span data-stu-id="6a8b8-131">Make sure you have an Azure subscription, [Azure CLI installed](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest), and that you are authenticated to your account:</span></span>

```bash
az login
```

#### <a name="create-a-resource-group"></a><span data-ttu-id="6a8b8-132">Creación de un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="6a8b8-132">Create a Resource Group</span></span>

```bash
export ARG=microprofileRG
export ADCL=eastus
az group create --name $ARG --location $ADCL
```

#### <a name="create-an-azure-container-registry-instance"></a><span data-ttu-id="6a8b8-133">Crear una instancia de Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="6a8b8-133">Create an Azure Container Registry instance</span></span>

<span data-ttu-id="6a8b8-134">Este comando creará un registro de contenedor globalmente único (esperamos) con un nombre básico y un número aleatorio.</span><span class="sxs-lookup"><span data-stu-id="6a8b8-134">This command will create a globally unique (hopefully) container registry using a basic name with a random number.</span></span>

```bash
export RANDINT=`date +"%m%d%y$RANDOM"`
export ACR=mydockerrepo$RANDINT
az acr create --name $ACR -g $ARG --sku Basic --admin-enabled
```

#### <a name="build-the-docker-image"></a><span data-ttu-id="6a8b8-135">Compilación de la imagen de Docker</span><span class="sxs-lookup"><span data-stu-id="6a8b8-135">Build the Docker image</span></span>

<span data-ttu-id="6a8b8-136">Aunque la imagen de Docker se puede compilar localmente con el propio Docker, quizás quiera considerar la posibilidad de compilarlo en la nube por algunas razones:</span><span class="sxs-lookup"><span data-stu-id="6a8b8-136">While you can easily build the Docker image locally using Docker itself, you may want to consider building it in the Cloud for few reasons:</span></span>

1. <span data-ttu-id="6a8b8-137">No es necesario instalar Docker localmente.</span><span class="sxs-lookup"><span data-stu-id="6a8b8-137">No need to install Docker locally</span></span>
1. <span data-ttu-id="6a8b8-138">Es mucho más rápido porque la compilación se realizará en otro lugar (excepto el tiempo de carga de contexto).</span><span class="sxs-lookup"><span data-stu-id="6a8b8-138">Much faster since build will happen elsewhere (except for context upload time)</span></span>
1. <span data-ttu-id="6a8b8-139">Los procesos en la nube tienen un acceso a Internet más rápido, por lo que las descargas son más rápidas.</span><span class="sxs-lookup"><span data-stu-id="6a8b8-139">Process in the Cloud has access to faster Internet, therefore faster downloads</span></span>
1. <span data-ttu-id="6a8b8-140">La imagen se coloca directamente en el registro de contenedor.</span><span class="sxs-lookup"><span data-stu-id="6a8b8-140">Image goes directly into the Container Registry</span></span>

<span data-ttu-id="6a8b8-141">Por estas razones, vamos a compilar la imagen con la característica [Azure Container Registry Build]:</span><span class="sxs-lookup"><span data-stu-id="6a8b8-141">Because of these reasons, we will build the image using the [Azure Container Registry Build] feature:</span></span>

```bash
export IMG_NAME="mympapp:latest"
az acr build -r $ACR -t $IMG_NAME -g $ARG .
...
Build complete
Build ID: aa1 was successful after 1m2.674577892s
```

#### <a name="deploy-docker-image-from-azure-container-registry-acr-into-container-instances-aci"></a><span data-ttu-id="6a8b8-142">Implementación de la imagen de Docker desde Azure Container Registry (ACR) en Azure Container Instances (ACI)</span><span class="sxs-lookup"><span data-stu-id="6a8b8-142">Deploy Docker Image from Azure Container Registry (ACR) into Container Instances (ACI)</span></span>

<span data-ttu-id="6a8b8-143">Ahora que la imagen está disponible en ACR, vamos a crear una instancia de ACI y a insertarla.</span><span class="sxs-lookup"><span data-stu-id="6a8b8-143">Now that the image is available on your ACR, let's push and instanciate a container instance on ACI.</span></span> <span data-ttu-id="6a8b8-144">Pero, primero, tenemos que asegurarnos de que podemos autenticarnos en el registro de contenedor:</span><span class="sxs-lookup"><span data-stu-id="6a8b8-144">But first, we need to make sure we can authenticate into the ACR:</span></span>

```bash
export ACR_REPO=`az acr show --name $ACR -g $ARG --query loginServer -o tsv`
export ACR_PASS=`az acr credential show --name $ACR -g $ARG --query "passwords[0].value" -o tsv`
export ACI_INSTANCE=myapp`date +"%m%d%y$RANDOM"`

az container create --resource-group $ARG --name $ACR --image $ACR_REPO/$IMG_NAME --cpu 1 --memory 1 --registry-login-server $ACR_REPO --registry-username $ACR --registry-password $ACR_PASS --dns-name-label $ACI_INSTANCE --ports 8080
```

#### <a name="test-your-deployed-microprofile-application"></a><span data-ttu-id="6a8b8-145">Prueba de la aplicación de MicroProfile implementada</span><span class="sxs-lookup"><span data-stu-id="6a8b8-145">Test Your Deployed MicroProfile Application</span></span>

<span data-ttu-id="6a8b8-146">La aplicación debe estar instalada y en ejecución.</span><span class="sxs-lookup"><span data-stu-id="6a8b8-146">Your application should now be up and running.</span></span> <span data-ttu-id="6a8b8-147">Para probarla en la línea de comandos, ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="6a8b8-147">To test it from the command-line, try the following command:</span></span>

```bash
curl http://$ACI_INSTANCE.$ADCL.azurecontainer.io:8080/api/hello
````

<span data-ttu-id="6a8b8-148">Felicidades.</span><span class="sxs-lookup"><span data-stu-id="6a8b8-148">Congratulations!</span></span> <span data-ttu-id="6a8b8-149">Ha compilado e implementado una aplicación de MicroProfile como un contenedor de Docker en Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="6a8b8-149">You have successfuly built and deployed a MicroProfile application as a Docker container onto Microsoft Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6a8b8-150">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6a8b8-150">Next steps</span></span>

<span data-ttu-id="6a8b8-151">Para más información acerca de las diferentes tecnologías que se tratan en este artículo, consulte los artículos siguientes:</span><span class="sxs-lookup"><span data-stu-id="6a8b8-151">For more information about the various technologies discussed in this article, see the following articles:</span></span>

* [<span data-ttu-id="6a8b8-152">Inicio de sesión en Azure desde la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="6a8b8-152">Log in to Azure from the Azure CLI</span></span>](/azure/xplat-cli-connect)

<!-- URL List -->

[Azure Container Registry Build]: https://docs.microsoft.com/azure/container-registry/container-registry-build-overview
[MicroProfile.io]: https://microprofile.io
[Interfaz de la línea de comandos (CLI) de Azure]: /cli/azure/overview
[Azure Command-Line Interface (CLI)]: /cli/azure/overview
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Azure portal]: https://portal.azure.com/
[cuenta de Azure gratuita]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Maven]: http://maven.apache.org/
[Java Development Kit (JDK)]: https://aka.ms/azure-jdks
<!-- http://www.oracle.com/technetwork/java/javase/downloads/ -->
[Azure Container Instances]: https://docs.microsoft.com/azure/container-instances/
[Azure Container Registry]:  https://docs.microsoft.com/azure/container-registry