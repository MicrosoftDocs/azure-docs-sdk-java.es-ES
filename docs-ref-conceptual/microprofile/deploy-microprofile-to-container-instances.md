---
title: Implementación de una aplicación de MicroProfile en la nube con Docker y Azure
description: Aprenda cómo implementar una aplicación de MicroProfile en la nube con Docker y Azure Container Instances.
services: container-instances;container-registry
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
ms.openlocfilehash: 6ba12bb183969103676fa988199603df6cf36bba
ms.sourcegitcommit: f8faa4a14c714e148c513fd46f119524f3897abf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2019
ms.locfileid: "67533603"
---
# <a name="deploy-a-microprofile-app-to-the-cloud-by-using-docker-and-azure"></a><span data-ttu-id="1bb70-103">Implementación de una aplicación de MicroProfile en la nube con Docker y Azure</span><span class="sxs-lookup"><span data-stu-id="1bb70-103">Deploy a MicroProfile app to the cloud by using Docker and Azure</span></span>

<span data-ttu-id="1bb70-104">En este artículo se muestra cómo empaquetar una aplicación de [MicroProfile.io] en un contenedor de Docker y ejecutarla en Azure Container Instances.</span><span class="sxs-lookup"><span data-stu-id="1bb70-104">This article demonstrates how to pack a [MicroProfile.io] application in a Docker container and run it on Azure Container Instances.</span></span>

> [!NOTE]
> <span data-ttu-id="1bb70-105">Este procedimiento funciona con cualquier implementación de MicroProfile.io siempre que la imagen del contenedor de Docker sea autoejecutable (es decir, la imagen incluye el entorno de ejecución).</span><span class="sxs-lookup"><span data-stu-id="1bb70-105">This procedure works with any implementation of MicroProfile.io, as long as the Docker container image is self-executable (that is, the image includes the runtime).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1bb70-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="1bb70-106">Prerequisites</span></span>

<span data-ttu-id="1bb70-107">Para completar este tutorial, debe cumplir los siguientes requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="1bb70-107">To complete this tutorial, you need the following prerequisites:</span></span>

* <span data-ttu-id="1bb70-108">Una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="1bb70-108">An Azure subscription.</span></span> <span data-ttu-id="1bb70-109">Si todavía no dispone de una suscripción a Azure, puede registrarse para obtener una evaluación gratuita en una [cuenta de Azure gratuita].</span><span class="sxs-lookup"><span data-stu-id="1bb70-109">If you don't already have an Azure subscription, you can sign up for a [free Azure account].</span></span>
* <span data-ttu-id="1bb70-110">La [CLI de Azure] instalada.</span><span class="sxs-lookup"><span data-stu-id="1bb70-110">The [Azure CLI], installed.</span></span>
* <span data-ttu-id="1bb70-111">Un kit de desarrollo de Java (JDK) admitido</span><span class="sxs-lookup"><span data-stu-id="1bb70-111">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="1bb70-112">Para más información acerca de los JDK que están disponibles para usar al desarrollar en Azure, consulte [Soporte técnico a largo plazo de Java para Azure y Azure Stack](https://aka.ms/azure-jdks).</span><span class="sxs-lookup"><span data-stu-id="1bb70-112">For more information about the JDKs that are available to use when you develop on Azure, see [Java long-term support for Azure and Azure Stack](https://aka.ms/azure-jdks).</span></span>
* <span data-ttu-id="1bb70-113">La herramienta de compilación [Apache Maven] (versión 3 o posteriores).</span><span class="sxs-lookup"><span data-stu-id="1bb70-113">The [Apache Maven] build tool (version 3 or later).</span></span>
* <span data-ttu-id="1bb70-114">Un cliente [Git].</span><span class="sxs-lookup"><span data-stu-id="1bb70-114">A [Git] client.</span></span>

## <a name="microprofile-hello-azure-sample"></a><span data-ttu-id="1bb70-115">Ejemplo MicroProfile Hello Azure</span><span class="sxs-lookup"><span data-stu-id="1bb70-115">MicroProfile Hello Azure sample</span></span>

<span data-ttu-id="1bb70-116">En este artículo, usaremos el ejemplo [MicroProfile Hello Azure](https://github.com/azure-samples/microprofile-hello-azure).</span><span class="sxs-lookup"><span data-stu-id="1bb70-116">In this article, you use the [MicroProfile Hello Azure](https://github.com/azure-samples/microprofile-hello-azure) sample.</span></span> <span data-ttu-id="1bb70-117">Clónelo, compílelo y ejecútelo localmente con los siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="1bb70-117">Clone, build, and run it locally by using the following commands:</span></span>

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

<span data-ttu-id="1bb70-118">Para probar la aplicación, puede llamar a `curl` o usar un [explorador](http://localhost:8080/api/hello):</span><span class="sxs-lookup"><span data-stu-id="1bb70-118">You can test the application by calling `curl` or by using a [browser](http://localhost:8080/api/hello):</span></span>

```bash
$ curl http://localhost:8080/api/hello
Hello, Azure!
```

## <a name="deploy-the-app-to-azure"></a><span data-ttu-id="1bb70-119">Implementación de la aplicación en Azure</span><span class="sxs-lookup"><span data-stu-id="1bb70-119">Deploy the app to Azure</span></span>

<span data-ttu-id="1bb70-120">Ahora vamos a poner esta aplicación en Azure con los servicios [Azure Container Instances] y [Azure Container Registry].</span><span class="sxs-lookup"><span data-stu-id="1bb70-120">Now bring this application to Azure by using the [Azure Container Instances] and [Azure Container Registry] services.</span></span>

### <a name="build-a-docker-image"></a><span data-ttu-id="1bb70-121">Compilación de una imagen de Docker</span><span class="sxs-lookup"><span data-stu-id="1bb70-121">Build a Docker image</span></span>

<span data-ttu-id="1bb70-122">El proyecto de ejemplo incluye un archivo Dockerfile que se puede usar.</span><span class="sxs-lookup"><span data-stu-id="1bb70-122">The sample project provides a Dockerfile that you can use.</span></span> <span data-ttu-id="1bb70-123">No es necesario tener Docker instalado, porque se usará la característica Build de Azure Container Registry para compilar la imagen en la nube.</span><span class="sxs-lookup"><span data-stu-id="1bb70-123">You don't need to have Docker installed, though, because you'll use the Azure Container Registry Build feature to build the image in the cloud.</span></span>

<span data-ttu-id="1bb70-124">Para compilar la imagen y prepararla para ejecutarla en Azure, haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="1bb70-124">To build the image and prepare to run it on Azure, do the following:</span></span>

1. <span data-ttu-id="1bb70-125">Instale e inicie sesión en la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="1bb70-125">Install and sign in to the Azure CLI.</span></span>
1. <span data-ttu-id="1bb70-126">Cree un grupo de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="1bb70-126">Create an Azure resource group.</span></span>
1. <span data-ttu-id="1bb70-127">Cree una instancia de registro de contenedor de Azure.</span><span class="sxs-lookup"><span data-stu-id="1bb70-127">Create an Azure container registry instance.</span></span>
1. <span data-ttu-id="1bb70-128">Compile una imagen de Docker.</span><span class="sxs-lookup"><span data-stu-id="1bb70-128">Build a Docker image.</span></span>
1. <span data-ttu-id="1bb70-129">Publique la imagen de Docker en la instancia de registro de contenedor creada previamente.</span><span class="sxs-lookup"><span data-stu-id="1bb70-129">Publish the Docker image to the previously created container registry instance.</span></span>
1. <span data-ttu-id="1bb70-130">(Opcional) Genere y publique la imagen en la instancia de registro de contenedor en un solo comando.</span><span class="sxs-lookup"><span data-stu-id="1bb70-130">(Optional) Build and publish the image to the container registry instance in one command.</span></span>


#### <a name="set-up-the-azure-cli"></a><span data-ttu-id="1bb70-131">Configuración de la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="1bb70-131">Set up the Azure CLI</span></span>

<span data-ttu-id="1bb70-132">Asegúrese de que tiene una suscripción de Azure, que la [CLI de Azure](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest) está instalada y que se ha autenticado en su cuenta:</span><span class="sxs-lookup"><span data-stu-id="1bb70-132">Make sure that you have an Azure subscription, that you've installed [the Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest), and that you're authenticated to your account:</span></span>

```bash
az login
```

#### <a name="create-a-resource-group"></a><span data-ttu-id="1bb70-133">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="1bb70-133">Create a resource group</span></span>

```bash
export ARG=microprofileRG
export ADCL=eastus
az group create --name $ARG --location $ADCL
```

#### <a name="create-a-container-registry-instance"></a><span data-ttu-id="1bb70-134">Creación de una instancia de registro de contenedor</span><span class="sxs-lookup"><span data-stu-id="1bb70-134">Create a container registry instance</span></span>

<span data-ttu-id="1bb70-135">Este comando creará una instancia de registro de contenedor global único con un nombre básico y un número aleatorio.</span><span class="sxs-lookup"><span data-stu-id="1bb70-135">This command should create a globally unique container registry instance with a basic name and a random number.</span></span>

```bash
export RANDINT=`date +"%m%d%y$RANDOM"`
export ACR=mydockerrepo$RANDINT
az acr create --name $ACR -g $ARG --sku Basic --admin-enabled
```

#### <a name="build-the-docker-image"></a><span data-ttu-id="1bb70-136">Compilación de la imagen de Docker</span><span class="sxs-lookup"><span data-stu-id="1bb70-136">Build the Docker image</span></span>

<span data-ttu-id="1bb70-137">Aunque la imagen de Docker se puede compilar localmente con el propio Docker, quizás quiera considerar la posibilidad de compilarlo en la nube por algunas razones:</span><span class="sxs-lookup"><span data-stu-id="1bb70-137">Although you can easily build the Docker image locally by using Docker itself, you might consider building it in the cloud for few reasons:</span></span>

* <span data-ttu-id="1bb70-138">No es necesario instalar Docker localmente.</span><span class="sxs-lookup"><span data-stu-id="1bb70-138">You don't have to install Docker locally.</span></span>
* <span data-ttu-id="1bb70-139">Es mucho más rápido porque la compilación se realizará en otro lugar (excepto el tiempo de carga de contexto).</span><span class="sxs-lookup"><span data-stu-id="1bb70-139">It's much faster, because the build happens elsewhere (except for context upload time).</span></span>
* <span data-ttu-id="1bb70-140">Los procesos en la nube tienen un acceso a Internet más rápido, por lo que las descargas son más rápidas.</span><span class="sxs-lookup"><span data-stu-id="1bb70-140">The process in the cloud has faster access to the internet and, therefore, faster downloads.</span></span>
* <span data-ttu-id="1bb70-141">La imagen se coloca directamente en la instancia de registro de contenedor.</span><span class="sxs-lookup"><span data-stu-id="1bb70-141">The image goes directly into the container registry instance.</span></span>

<span data-ttu-id="1bb70-142">Por estas razones, la imagen se compila con la característica [Azure Container Registry Build]:</span><span class="sxs-lookup"><span data-stu-id="1bb70-142">For these reasons, you build the image by using the [Azure Container Registry Build] feature:</span></span>

```bash
export IMG_NAME="mympapp:latest"
az acr build -r $ACR -t $IMG_NAME -g $ARG .
...
Build complete
Build ID: aa1 was successful after 1m2.674577892s
```

#### <a name="deploy-the-docker-image-from-the-azure-container-registry-instance-to-container-instances"></a><span data-ttu-id="1bb70-143">Implementación de la imagen de Docker desde la instancia de registro de contenedor de Azure en Azure Container Instances</span><span class="sxs-lookup"><span data-stu-id="1bb70-143">Deploy the Docker image from the Azure container registry instance to Container Instances</span></span>

<span data-ttu-id="1bb70-144">Ahora que la imagen está disponible en la instancia de registro de contenedor, cree una instancia de contenedor e insértela en Container Instances.</span><span class="sxs-lookup"><span data-stu-id="1bb70-144">Now that the image is available on your container registry instance, push and instantiate a container instance on Container Instances.</span></span> <span data-ttu-id="1bb70-145">Pero primero, asegúrese de que puede autenticarse en la instancia de registro de contenedor:</span><span class="sxs-lookup"><span data-stu-id="1bb70-145">But first, make sure that you can authenticate into the container registry instance:</span></span>

```bash
export ACR_REPO=`az acr show --name $ACR -g $ARG --query loginServer -o tsv`
export ACR_PASS=`az acr credential show --name $ACR -g $ARG --query "passwords[0].value" -o tsv`
export ACI_INSTANCE=myapp`date +"%m%d%y$RANDOM"`

az container create --resource-group $ARG --name $ACR --image $ACR_REPO/$IMG_NAME --cpu 1 --memory 1 --registry-login-server $ACR_REPO --registry-username $ACR --registry-password $ACR_PASS --dns-name-label $ACI_INSTANCE --ports 8080
```

#### <a name="test-your-deployed-microprofile-application"></a><span data-ttu-id="1bb70-146">Prueba de la aplicación de MicroProfile implementada</span><span class="sxs-lookup"><span data-stu-id="1bb70-146">Test your deployed MicroProfile application</span></span>

<span data-ttu-id="1bb70-147">La aplicación debe estar instalada y en ejecución.</span><span class="sxs-lookup"><span data-stu-id="1bb70-147">Your application should now be up and running.</span></span> <span data-ttu-id="1bb70-148">Para probarla en la interfaz de la línea de comandos, ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="1bb70-148">To test it from the command-line interface, use the following command:</span></span>

```bash
curl http://$ACI_INSTANCE.$ADCL.azurecontainer.io:8080/api/hello
````

<span data-ttu-id="1bb70-149">Felicidades.</span><span class="sxs-lookup"><span data-stu-id="1bb70-149">Congratulations!</span></span> <span data-ttu-id="1bb70-150">Ha compilado correctamente una aplicación de MicroProfile como un contenedor de Docker y la ha implementado en Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="1bb70-150">You've successfully built a MicroProfile application as a Docker container and deployed it to Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1bb70-151">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1bb70-151">Next steps</span></span>

<span data-ttu-id="1bb70-152">Para más información acerca de las diferentes tecnologías que se tratan en este artículo, consulte:</span><span class="sxs-lookup"><span data-stu-id="1bb70-152">For more information about the various technologies discussed in this article, see:</span></span>

* [<span data-ttu-id="1bb70-153">Inicio de sesión en Azure desde la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="1bb70-153">Sign in to Azure from the Azure CLI</span></span>](/azure/xplat-cli-connect)

<!-- URL List -->

[Azure Container Registry Build]: https://docs.microsoft.com/azure/container-registry/container-registry-build-overview
[MicroProfile.io]: https://microprofile.io
[CLI de Azure]: /cli/azure/overview
[Azure CLI]: /cli/azure/overview
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Azure portal]: https://portal.azure.com/
[cuenta de Azure gratuita]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Apache Maven]: http://maven.apache.org/
[Java Development Kit (JDK)]: https://aka.ms/azure-jdks
<!-- http://www.oracle.com/technetwork/java/javase/downloads/ -->
[Azure Container Instances]: https://docs.microsoft.com/azure/container-instances/
[Azure Container Registry]:  https://docs.microsoft.com/azure/container-registry
