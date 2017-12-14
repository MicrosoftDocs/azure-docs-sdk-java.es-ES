---
title: "Uso del complemento Maven de Azure Web Apps para implementar una aplicación de Spring Boot de Azure Container Registry en Azure App Service"
description: "Este tutorial le guiará por los pasos para implementar una aplicación de Spring Boot de Azure Container Registry en Azure App Service mediante un complemento Maven."
services: container-registry
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: web
ms.tgt_pltfrm: multiple
ms.devlang: java
ms.topic: article
ms.date: 12/01/2017
ms.author: robmcm;kevinzha
ms.openlocfilehash: 7fa375ca805ddd037173f9dbd26b6631021e60a3
ms.sourcegitcommit: fc48e038721e6910cb8b1f8951df765d517e504d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/06/2017
---
# <a name="how-to-use-the-maven-plugin-for-azure-web-apps-to-deploy-a-spring-boot-app-in-azure-container-registry-to-azure-app-service"></a><span data-ttu-id="9f9e4-103">Uso del complemento Maven de Azure Web Apps para implementar una aplicación de Spring Boot de Azure Container Registry en Azure App Service</span><span class="sxs-lookup"><span data-stu-id="9f9e4-103">How to use the Maven Plugin for Azure Web Apps to deploy a Spring Boot app in Azure Container Registry to Azure App Service</span></span>

<span data-ttu-id="9f9e4-104">En este artículo se muestra cómo implementar una aplicación de [Spring Boot] de ejemplo en Azure Container Registry y cómo usar el complemento Maven para Azure Web Apps para implementar la aplicación en Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="9f9e4-104">This article demonstrates how to deploy a sample [Spring Boot] application to Azure Container Registry, and then use the Maven Plugin for Azure Web Apps to deploy your application to Azure App Service.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="9f9e4-105">El complemento Maven para Azure Web Apps de [Apache Maven](http://maven.apache.org/) proporciona una perfecta integración de Azure App Service en proyectos de Maven y simplifica el proceso para que los desarrolladores implementen aplicaciones web en Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="9f9e4-105">The Maven Plugin for Azure Web Apps for [Apache Maven](http://maven.apache.org/) provides seamless integration of Azure App Service  into Maven projects, and streamlines the process for developers to deploy web apps to Azure App Service.</span></span>
> 
> <span data-ttu-id="9f9e4-106">El complemento Maven de Azure Web Apps está disponible actualmente como versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="9f9e4-106">The Maven Plugin for Azure Web Apps is currently available as a preview.</span></span> <span data-ttu-id="9f9e4-107">Por ahora, solo se admite la publicación FTP, aunque se van a agregar características adicionales en el futuro.</span><span class="sxs-lookup"><span data-stu-id="9f9e4-107">For now, only FTP publishing is supported, although additional features are planned for the future.</span></span>
> 

## <a name="prerequisites"></a><span data-ttu-id="9f9e4-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9f9e4-108">Prerequisites</span></span>

<span data-ttu-id="9f9e4-109">Para poder realizar los pasos de este tutorial, necesitará tener los siguientes requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="9f9e4-109">In order to complete the steps in this tutorial, you need to have the following prerequisites:</span></span>

* <span data-ttu-id="9f9e4-110">Una suscripción de Azure. Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN] o registrarse para obtener una [cuenta de Azure gratuita].</span><span class="sxs-lookup"><span data-stu-id="9f9e4-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="9f9e4-111">La [Interfaz de la línea de comandos (CLI) de Azure].</span><span class="sxs-lookup"><span data-stu-id="9f9e4-111">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="9f9e4-112">Un [kit de desarrollo de Java (JDK)] actualizado, versión 1.7 o posterior.</span><span class="sxs-lookup"><span data-stu-id="9f9e4-112">An up-to-date [Java Development Kit (JDK)], version 1.7 or later.</span></span>
* <span data-ttu-id="9f9e4-113">La herramienta de compilación [Maven] de Apache (versión 3).</span><span class="sxs-lookup"><span data-stu-id="9f9e4-113">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="9f9e4-114">Un cliente [Git].</span><span class="sxs-lookup"><span data-stu-id="9f9e4-114">A [Git] client.</span></span>
* <span data-ttu-id="9f9e4-115">Un [cliente de Docker].</span><span class="sxs-lookup"><span data-stu-id="9f9e4-115">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="9f9e4-116">Dados los requisitos de virtualización de este tutorial, los pasos que se describen en este artículo no se pueden seguir en una máquina virtual; es preciso usar un equipo físico con características de virtualización habilitadas.</span><span class="sxs-lookup"><span data-stu-id="9f9e4-116">Due to the virtualization requirements of this tutorial, you cannot follow the steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="clone-the-sample-spring-boot-on-docker-web-app"></a><span data-ttu-id="9f9e4-117">Clonación de la aplicación de Spring Boot de ejemplo en la aplicación web de Docker</span><span class="sxs-lookup"><span data-stu-id="9f9e4-117">Clone the sample Spring Boot on Docker web app</span></span>

<span data-ttu-id="9f9e4-118">En esta sección, clone una aplicación de Spring Boot en contenedor y pruébela de forma local.</span><span class="sxs-lookup"><span data-stu-id="9f9e4-118">In this section, you clone a containerized Spring Boot application and test it locally.</span></span>

1. <span data-ttu-id="9f9e4-119">Abra el símbolo del sistema o una ventana de terminal y cree un directorio local para alojar la aplicación de Spring Boot, y cambie a dicho directorio, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9f9e4-119">Open a command prompt or terminal window and create a local directory to hold your Spring Boot application, and change to that directory; for example:</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="9f9e4-120">-- o --</span><span class="sxs-lookup"><span data-stu-id="9f9e4-120">-- or --</span></span>
   ```shell
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="9f9e4-121">Clone el proyecto de ejemplo [inicial de Spring Boot en Docker] en el directorio que ha creado, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9f9e4-121">Clone the [Spring Boot on Docker Getting Started] sample project into the directory you created; for example:</span></span>
   ```shell
   git clone -b private-registry https://github.com/Microsoft/gs-spring-boot-docker
   ```

1. <span data-ttu-id="9f9e4-122">Cambie de directorio al del proyecto finalizado, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9f9e4-122">Change directory to the completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot-docker/complete
   ```

1. <span data-ttu-id="9f9e4-123">Compile el archivo JAR con Maven, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9f9e4-123">Build the JAR file using Maven; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="9f9e4-124">Cuándo se haya creado la aplicación web, iníciela con Maven. Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9f9e4-124">When the web app has been created, start the web app using Maven; for example:</span></span>
   ```shell
   mvn spring-boot:run
   ```

1. <span data-ttu-id="9f9e4-125">Pruebe la aplicación web. Para ello, navegue a ella localmente mediante un explorador web.</span><span class="sxs-lookup"><span data-stu-id="9f9e4-125">Test the web app by browsing to it locally using a web browser.</span></span> <span data-ttu-id="9f9e4-126">Por ejemplo, puede utilizar el siguiente comando si dispone de curl:</span><span class="sxs-lookup"><span data-stu-id="9f9e4-126">For example, you could use the following command if you have curl available:</span></span>
   ```shell
   curl http://localhost:8080
   ```

1. <span data-ttu-id="9f9e4-127">Debería aparecer el siguiente mensaje: **Hello Docker World**</span><span class="sxs-lookup"><span data-stu-id="9f9e4-127">You should see the following message displayed: **Hello Docker World**</span></span>

   ![Examen local de aplicación de ejemplo][SB01]

> [!NOTE]
>
> <span data-ttu-id="9f9e4-129">Cuando se usa Docker localmente, puede ver un error que indica que no se puede conectar a localhost en el puerto 2375.</span><span class="sxs-lookup"><span data-stu-id="9f9e4-129">When you are using Docker locally, you may see an error which states that you cannot connect to localhost on port 2375.</span></span> <span data-ttu-id="9f9e4-130">Si esto ocurre, debe habilitar el uso de Docker localmente sin TLS.</span><span class="sxs-lookup"><span data-stu-id="9f9e4-130">If this happens, you may need to enable using Docker locally without TLS.</span></span> <span data-ttu-id="9f9e4-131">Para ello, abra la configuración de Docker y compruebe que la opción **Expose Docker Daemon está establecida en TCP://localhost:2375 sin TLS**.</span><span class="sxs-lookup"><span data-stu-id="9f9e4-131">To do so, open your Docker settings and check the option to **Expose daemon on TCP://localhost:2375 without TLS**.</span></span>
>
> ![Exponer Docker Daemon en el puerto TCP 2375 local][TL01]

## <a name="create-an-azure-service-principal"></a><span data-ttu-id="9f9e4-133">Creación de una entidad de servicio de Azure</span><span class="sxs-lookup"><span data-stu-id="9f9e4-133">Create an Azure service principal</span></span>

<span data-ttu-id="9f9e4-134">En esta sección, va a crear una entidad de servicio de Azure que usa el complemento Maven cuando implementa el contenedor en Azure.</span><span class="sxs-lookup"><span data-stu-id="9f9e4-134">In this section, you create an Azure service principal that the Maven plugin uses when deploying your container to Azure.</span></span>

1. <span data-ttu-id="9f9e4-135">Abra el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="9f9e4-135">Open a command prompt.</span></span>

1. <span data-ttu-id="9f9e4-136">Inicie sesión en la cuenta de Azure mediante la CLI de Azure:</span><span class="sxs-lookup"><span data-stu-id="9f9e4-136">Sign into your Azure account by using the Azure CLI:</span></span>
   ```azurecli
   az login
   ```
   <span data-ttu-id="9f9e4-137">Siga las instrucciones para completar el proceso de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="9f9e4-137">Follow the instructions to complete the sign-in process.</span></span>

1. <span data-ttu-id="9f9e4-138">Cree una entidad de servicio de Azure:</span><span class="sxs-lookup"><span data-stu-id="9f9e4-138">Create an Azure service principal:</span></span>
   ```azurecli
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   <span data-ttu-id="9f9e4-139">Donde `uuuuuuuu` es el nombre de usuario y `pppppppp` es la contraseña de la entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="9f9e4-139">Where `uuuuuuuu` is the user name and `pppppppp` is the password for the service principal.</span></span>

1. <span data-ttu-id="9f9e4-140">Azure responde con un archivo JSON que es similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="9f9e4-140">Azure responds with JSON that resembles the following example:</span></span>
   ```json
   {
      "appId": "aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa",
      "displayName": "uuuuuuuu",
      "name": "http://uuuuuuuu",
      "password": "pppppppp",
      "tenant": "tttttttt-tttt-tttt-tttt-tttttttttttt"
   }
   ```

   > [!NOTE]
   >
   > <span data-ttu-id="9f9e4-141">Utilizará los valores de esta respuesta JSON al configurar el complemento de Maven para implementar el contenedor en Azure.</span><span class="sxs-lookup"><span data-stu-id="9f9e4-141">You will use the values from this JSON response when you configure the Maven plugin to deploy your container to Azure.</span></span> <span data-ttu-id="9f9e4-142">El `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, y `tttttttt` son valores de marcador de posición que se usan en este ejemplo para que sea más fácil asignar estos valores a sus respectivos elementos al configurar el archivo `settings.xml` de Maven en la sección siguiente.</span><span class="sxs-lookup"><span data-stu-id="9f9e4-142">The `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, and `tttttttt` are placeholder values, which are used in this example to make it easier to map these values to their respective elements when you configure your Maven `settings.xml` file in the next section.</span></span>
   >
   >

## <a name="create-an-azure-container-registry-using-the-azure-cli"></a><span data-ttu-id="9f9e4-143">Creación de una instancia de Azure Container Registry mediante la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="9f9e4-143">Create an Azure Container Registry using the Azure CLI</span></span>

1. <span data-ttu-id="9f9e4-144">Abra el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="9f9e4-144">Open a command prompt.</span></span>

1. <span data-ttu-id="9f9e4-145">Inicie sesión en una cuenta de Azure:</span><span class="sxs-lookup"><span data-stu-id="9f9e4-145">Log in to your Azure account:</span></span>
   ```azurecli
   az login
   ```

1. <span data-ttu-id="9f9e4-146">Cree un grupo de recursos para los recursos de Azure que se usan en este artículo:</span><span class="sxs-lookup"><span data-stu-id="9f9e4-146">Create a resource group for the Azure resources you will use in this article:</span></span>
   ```azurecli
   az group create --name=wingtiptoysresources --location=westus
   ```
   <span data-ttu-id="9f9e4-147">Reemplace `wingtiptoysresources` en este ejemplo por un nombre único para el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="9f9e4-147">Replace `wingtiptoysresources` in this example with a unique name for your resource group.</span></span>

1. <span data-ttu-id="9f9e4-148">Cree una instancia de Azure Container Registry en el grupo de recursos de la aplicación de Spring Boot:</span><span class="sxs-lookup"><span data-stu-id="9f9e4-148">Create a private Azure container registry in the resource group for your Spring Boot app:</span></span> 
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoysresources --location westus --name wingtiptoysregistry --sku Basic
   ```
   <span data-ttu-id="9f9e4-149">Reemplace `wingtiptoysregistry` en este ejemplo por un nombre único para el registro de contenedor.</span><span class="sxs-lookup"><span data-stu-id="9f9e4-149">Replace `wingtiptoysregistry` in this example with a unique name for your container registry.</span></span>

1. <span data-ttu-id="9f9e4-150">Recupere la contraseña del registro de contenedor:</span><span class="sxs-lookup"><span data-stu-id="9f9e4-150">Retrieve the password for your container registry:</span></span>
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```
   <span data-ttu-id="9f9e4-151">Azure responderá con la contraseña; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9f9e4-151">Azure will respond with your password; for example:</span></span>
   ```json
   {
      "name": "password",
      "value": "xxxxxxxxxx"
   }
   ```

## <a name="add-your-azure-container-registry-and-azure-service-principal-to-your-maven-settings"></a><span data-ttu-id="9f9e4-152">Agregue el registro de contenedor y la entidad de servicio de Azure a la configuración de Maven</span><span class="sxs-lookup"><span data-stu-id="9f9e4-152">Add your Azure container registry and Azure service principal to your Maven settings</span></span>

1. <span data-ttu-id="9f9e4-153">Abra el archivo `settings.xml` de Maven en un editor de texto; este archivo puede encontrarse en una ruta de acceso como la de los ejemplos siguientes:</span><span class="sxs-lookup"><span data-stu-id="9f9e4-153">Open your Maven `settings.xml` file in a text editor; this file might be in a path like the following examples:</span></span>
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. <span data-ttu-id="9f9e4-154">Agregue la configuración de acceso de Azure Container Registry de la sección anterior de este artículo a la colección `<servers>` en el archivo *settings.xml*, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9f9e4-154">Add your Azure Container Registry access settings from the previous section of this article to the `<servers>` collection in the *settings.xml* file; for example:</span></span>

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>xxxxxxxxxx</password>
      </server>
   </servers>
   ```
   <span data-ttu-id="9f9e4-155">Donde:</span><span class="sxs-lookup"><span data-stu-id="9f9e4-155">Where:</span></span>
   <span data-ttu-id="9f9e4-156">Elemento</span><span class="sxs-lookup"><span data-stu-id="9f9e4-156">Element</span></span> | <span data-ttu-id="9f9e4-157">Descripción</span><span class="sxs-lookup"><span data-stu-id="9f9e4-157">Description</span></span>
   ---|---|---
   `<id>` | <span data-ttu-id="9f9e4-158">Contiene el nombre del registro de contenedor privado de Azure.</span><span class="sxs-lookup"><span data-stu-id="9f9e4-158">Contains the name of your private Azure container registry.</span></span>
   `<username>` | <span data-ttu-id="9f9e4-159">Contiene el nombre del registro de contenedor privado de Azure.</span><span class="sxs-lookup"><span data-stu-id="9f9e4-159">Contains the name of your private Azure container registry.</span></span>
   `<password>` | <span data-ttu-id="9f9e4-160">Contiene la contraseña que recuperó en la sección anterior de este artículo.</span><span class="sxs-lookup"><span data-stu-id="9f9e4-160">Contains the password you retrieved in the previous section of this article.</span></span>

1. <span data-ttu-id="9f9e4-161">Agregue la configuración de la entidad de servicio de una sección anterior de este artículo a la colección `<servers>` en el archivo *settings.xml*, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9f9e4-161">Add your Azure service principal settings from an earlier section of this article to the `<servers>` collection in the *settings.xml* file; for example:</span></span>

   ```xml
   <servers>
      <server>
        <id>azure-auth</id>
         <configuration>
            <client>aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa</client>
            <tenant>tttttttt-tttt-tttt-tttt-tttttttttttt</tenant>
            <key>pppppppp</key>
            <environment>AZURE</environment>
         </configuration>
      </server>
   </servers>
   ```
   <span data-ttu-id="9f9e4-162">Donde:</span><span class="sxs-lookup"><span data-stu-id="9f9e4-162">Where:</span></span>
   <span data-ttu-id="9f9e4-163">Elemento</span><span class="sxs-lookup"><span data-stu-id="9f9e4-163">Element</span></span> | <span data-ttu-id="9f9e4-164">Descripción</span><span class="sxs-lookup"><span data-stu-id="9f9e4-164">Description</span></span>
   ---|---|---
   `<id>` | <span data-ttu-id="9f9e4-165">Especifica un nombre único que Maven utiliza para buscar la configuración de seguridad al implementar la aplicación web en Azure.</span><span class="sxs-lookup"><span data-stu-id="9f9e4-165">Specifies a unique name which Maven uses to look up your security settings when you deploy your web app to Azure.</span></span>
   `<client>` | <span data-ttu-id="9f9e4-166">Contiene el valor `appId` de la entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="9f9e4-166">Contains the `appId` value from your service principal.</span></span>
   `<tenant>` | <span data-ttu-id="9f9e4-167">Contiene el valor `tenant` de la entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="9f9e4-167">Contains the `tenant` value from your service principal.</span></span>
   `<key>` | <span data-ttu-id="9f9e4-168">Contiene el valor `password` de la entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="9f9e4-168">Contains the `password` value from your service principal.</span></span>
   `<environment>` | <span data-ttu-id="9f9e4-169">Define el entorno en la nube de Azure de destino, que es `AZURE` en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="9f9e4-169">Defines the target Azure cloud environment, which is `AZURE` in this example.</span></span> <span data-ttu-id="9f9e4-170">(Una lista completa de los entornos está disponible en la documentación del [complemento Maven de Azure Web Apps])</span><span class="sxs-lookup"><span data-stu-id="9f9e4-170">(A full list of environments is available in the [Maven Plugin for Azure Web Apps] documentation)</span></span>

1. <span data-ttu-id="9f9e4-171">Guarde y cierre el archivo *settings.xml*.</span><span class="sxs-lookup"><span data-stu-id="9f9e4-171">Save and close the *settings.xml* file.</span></span>

## <a name="build-your-docker-container-image-and-push-it-to-your-azure-container-registry"></a><span data-ttu-id="9f9e4-172">Creación de la imagen de contenedor de Docker e inserción de esta en el registro de contenedor de Azure</span><span class="sxs-lookup"><span data-stu-id="9f9e4-172">Build your Docker container image and push it to your Azure container registry</span></span>

1. <span data-ttu-id="9f9e4-173">Vaya al directorio de proyecto completado de la aplicación Spring Boot (por ejemplo, "*C:\SpringBoot\gs-spring-boot-docker\complete*" o "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*") y abra el archivo *pom.xml* con un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="9f9e4-173">Navigate to the completed project directory for your Spring Boot application, (e.g. "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open the *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="9f9e4-174">Actualice la colección `<properties>` del archivo *pom.xml* con el valor del servidor de inicio de sesión de Azure Container Registry de la sección anterior de este tutorial, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9f9e4-174">Update the `<properties>` collection in the *pom.xml* file with the login server value for your Azure Container Registry from the previous section of this tutorial; for example:</span></span>

   ```xml
   <properties>
      <azure.containerRegistry>wingtiptoysregistry</azure.containerRegistry>
      <docker.image.prefix>${azure.containerRegistry}.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
      <maven.build.timestamp.format>yyyyMMddHHmmssSSS</maven.build.timestamp.format>
   </properties>
   ```
   <span data-ttu-id="9f9e4-175">Donde:</span><span class="sxs-lookup"><span data-stu-id="9f9e4-175">Where:</span></span>
   <span data-ttu-id="9f9e4-176">Elemento</span><span class="sxs-lookup"><span data-stu-id="9f9e4-176">Element</span></span> | <span data-ttu-id="9f9e4-177">Descripción</span><span class="sxs-lookup"><span data-stu-id="9f9e4-177">Description</span></span>
   ---|---|---
   `<azure.containerRegistry>` | <span data-ttu-id="9f9e4-178">Especifica el nombre del registro de contenedor privado de Azure.</span><span class="sxs-lookup"><span data-stu-id="9f9e4-178">Specifies the name of your private Azure container registry.</span></span>
   `<docker.image.prefix>` | <span data-ttu-id="9f9e4-179">Especifica la dirección URL del registro de contenedor privado de Azure, que se crea agregando ".azurecr.io" al nombre del registro de contenedor privado.</span><span class="sxs-lookup"><span data-stu-id="9f9e4-179">Specifies the URL of your private Azure container registry, which is derived by appending ".azurecr.io" to the name of your private container registry.</span></span>

1. <span data-ttu-id="9f9e4-180">Compruebe que `<plugin>` del complemento de Docker del archivo *pom.xml* contiene las propiedades correctas de dirección del servidor de inicio de sesión y nombre de registro del paso anterior de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="9f9e4-180">Verify that `<plugin>` for the Docker plugin in your *pom.xml* file contains the correct properties for the login server address and registry name from the previous step in this tutorial.</span></span> <span data-ttu-id="9f9e4-181">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9f9e4-181">For example:</span></span>

   ```xml
   <plugin>
      <groupId>com.spotify</groupId>
      <artifactId>docker-maven-plugin</artifactId>
      <version>0.4.11</version>
      <configuration>
         <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
         <registryUrl>https://${docker.image.prefix}</registryUrl>
         <serverId>${azure.containerRegistry}</serverId>
         <dockerDirectory>src/main/docker</dockerDirectory>
         <resources>
            <resource>
               <targetPath>/</targetPath>
               <directory>${project.build.directory}</directory>
               <include>${project.build.finalName}.jar</include>
            </resource>
         </resources>
      </configuration>
   </plugin>
   ```
   <span data-ttu-id="9f9e4-182">Donde:</span><span class="sxs-lookup"><span data-stu-id="9f9e4-182">Where:</span></span>
   <span data-ttu-id="9f9e4-183">Elemento</span><span class="sxs-lookup"><span data-stu-id="9f9e4-183">Element</span></span> | <span data-ttu-id="9f9e4-184">Descripción</span><span class="sxs-lookup"><span data-stu-id="9f9e4-184">Description</span></span>
   ---|---|---
   `<serverId>` | <span data-ttu-id="9f9e4-185">Especifica la propiedad que contiene el nombre del registro de contenedor privado de Azure.</span><span class="sxs-lookup"><span data-stu-id="9f9e4-185">Specifies the property which contains name of your private Azure container registry.</span></span>
   `<registryUrl>` | <span data-ttu-id="9f9e4-186">Especifica la propiedad que contiene la dirección URL del registro de contenedor privado de Azure.</span><span class="sxs-lookup"><span data-stu-id="9f9e4-186">Specifies the property which contains the URL of your private Azure container registry.</span></span>

1. <span data-ttu-id="9f9e4-187">Navegue hasta el directorio de proyecto completado de la aplicación de Spring Boot y ejecute el siguiente comando para recompilar la aplicación e insertar el contenedor en la instancia de Azure Container Registry:</span><span class="sxs-lookup"><span data-stu-id="9f9e4-187">Navigate to the completed project directory for your Spring Boot application and run the following command to rebuild the application and push the container to your Azure container registry:</span></span>

   ```
   mvn package docker:build -DpushImage 
   ```

1. <span data-ttu-id="9f9e4-188">OPCIONAL: Vaya a [Azure Portal] y compruebe que hay una imagen de contenedor de Docker denominada **gs-spring-arranque-docker** en el registro de contenedor.</span><span class="sxs-lookup"><span data-stu-id="9f9e4-188">OPTIONAL: Browse to the [Azure portal] and verify that there is Docker container image named **gs-spring-boot-docker** in your container registry.</span></span>

   ![Comprobar contenedor en Azure Portal][CR01]

## <a name="customize-your-pomxml-then-build-and-deploy-your-container-to-azure"></a><span data-ttu-id="9f9e4-190">Personalización del archivo pom.xml y compilación e implementación posterior del contenedor en Azure</span><span class="sxs-lookup"><span data-stu-id="9f9e4-190">Customize your pom.xml, then build and deploy your container to Azure</span></span>

<span data-ttu-id="9f9e4-191">Abra el archivo `pom.xml` de la aplicación de Spring Boot en un editor de texto y, a continuación, busque el elemento `<plugin>` de `azure-webapp-maven-plugin`.</span><span class="sxs-lookup"><span data-stu-id="9f9e4-191">Open the `pom.xml` file for your Spring Boot application in a text editor, and then locate the `<plugin>` element for `azure-webapp-maven-plugin`.</span></span> <span data-ttu-id="9f9e4-192">Este elemento debe tener un aspecto similar al ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="9f9e4-192">This element should resemble the following example:</span></span>

   ```xml
   <plugin>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-webapp-maven-plugin</artifactId>
      <version>0.1.3</version>
      <configuration>
         <authentication>
            <serverId>azure-auth</serverId>
         </authentication>
         <resourceGroup>wingtiptoysresources</resourceGroup>
         <appName>maven-linux-app-${maven.build.timestamp}</appName>
         <region>westus</region>
         <containerSettings>
            <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
            <registryUrl>https://${docker.image.prefix}</registryUrl>
            <serverId>${azure.containerRegistry}</serverId>
         </containerSettings>
         <appSettings>
            <property>
               <name>PORT</name>
               <value>8080</value>
            </property>
         </appSettings>
      </configuration>
   </plugin>
   ```

<span data-ttu-id="9f9e4-193">Hay varios valores que se pueden modificar en el complemento Maven y hay una descripción detallada de cada uno de estos elementos disponible en la documentación del [complemento Maven de Azure Web Apps].</span><span class="sxs-lookup"><span data-stu-id="9f9e4-193">There are several values that you can modify for the Maven plugin, and a detailed description for each of these elements is available in the [Maven Plugin for Azure Web Apps] documentation.</span></span> <span data-ttu-id="9f9e4-194">Dicho esto, hay varios valores que merece la pena destacar en este artículo:</span><span class="sxs-lookup"><span data-stu-id="9f9e4-194">That being said, there are several values that are worth highlighting in this article:</span></span>

<span data-ttu-id="9f9e4-195">Elemento</span><span class="sxs-lookup"><span data-stu-id="9f9e4-195">Element</span></span> | <span data-ttu-id="9f9e4-196">Descripción</span><span class="sxs-lookup"><span data-stu-id="9f9e4-196">Description</span></span>
---|---|---
`<version>` | <span data-ttu-id="9f9e4-197">Especifica la versión del [complemento Maven de Azure Web Apps].</span><span class="sxs-lookup"><span data-stu-id="9f9e4-197">Specifies the version of the [Maven Plugin for Azure Web Apps].</span></span> <span data-ttu-id="9f9e4-198">Debe comprobar la versión que aparece en el [repositorio central de Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) para asegurarse de que está utilizando la versión más reciente.</span><span class="sxs-lookup"><span data-stu-id="9f9e4-198">You should check the version listed in the [Maven Central Respository](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) to ensure that you are using the latest version.</span></span>
`<authentication>` | <span data-ttu-id="9f9e4-199">Especifica la información de autenticación de Azure que, en este ejemplo, contiene un elemento `<serverId>` que contiene `azure-auth`; Maven utiliza ese valor para buscar los valores de la entidad de servicio de Azure en el archivo *settings.xml* que se definió en una sección anterior de este artículo.</span><span class="sxs-lookup"><span data-stu-id="9f9e4-199">Specifies the authentication information for Azure, which in this example contains a `<serverId>` element that contains `azure-auth`; Maven uses that value to look up the Azure service principal values in your Maven *settings.xml* file, which you defined in an earlier section of this article.</span></span>
`<resourceGroup>` | <span data-ttu-id="9f9e4-200">Especifica el grupo de recursos de destino, que es `wingtiptoysresources` en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="9f9e4-200">Specifies the target resource group, which is `wingtiptoysresources` in this example.</span></span> <span data-ttu-id="9f9e4-201">Se creará este grupo de recursos durante la implementación si todavía no existe.</span><span class="sxs-lookup"><span data-stu-id="9f9e4-201">The resource group will be created during deployment if it does not already exist.</span></span>
`<appName>` | <span data-ttu-id="9f9e4-202">Especifica el nombre de destino de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="9f9e4-202">Specifies the target name for your web app.</span></span> <span data-ttu-id="9f9e4-203">En este ejemplo, el nombre de destino es `maven-linux-app-${maven.build.timestamp}`, donde el sufijo `${maven.build.timestamp}` se anexa en este ejemplo para evitar conflictos.</span><span class="sxs-lookup"><span data-stu-id="9f9e4-203">In this example, the target name is `maven-linux-app-${maven.build.timestamp}`, where the `${maven.build.timestamp}` suffix is appended in this example to avoid conflict.</span></span> <span data-ttu-id="9f9e4-204">(La marca de tiempo es opcional; puede especificar cualquier cadena única para el nombre de la aplicación).</span><span class="sxs-lookup"><span data-stu-id="9f9e4-204">(The timestamp is optional; you can specify any unique string for the app name.)</span></span>
`<region>` | <span data-ttu-id="9f9e4-205">Especifica la región de destino, que en este ejemplo es `westus`.</span><span class="sxs-lookup"><span data-stu-id="9f9e4-205">Specifies the target region, which in this example is `westus`.</span></span> <span data-ttu-id="9f9e4-206">(Puede encontrar una lista completa en la documentación del [complemento Maven de Azure Web Apps]).</span><span class="sxs-lookup"><span data-stu-id="9f9e4-206">(A full list is in the [Maven Plugin for Azure Web Apps] documentation.)</span></span>
`<containerSettings>` | <span data-ttu-id="9f9e4-207">Especifica las propiedades que contienen el nombre y la dirección URL del contenedor.</span><span class="sxs-lookup"><span data-stu-id="9f9e4-207">Specifies the properties which contain the name and URL of your container.</span></span>
`<appSettings>` | <span data-ttu-id="9f9e4-208">Especifica los valores únicos de Maven que se deben usar durante la implementación de la aplicación web en Azure.</span><span class="sxs-lookup"><span data-stu-id="9f9e4-208">Specifies any unique settings for Maven to use when deploying your web app to Azure.</span></span> <span data-ttu-id="9f9e4-209">En este ejemplo, un elemento `<property>` contiene un par nombre/valor de elementos secundarios que especifican el puerto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9f9e4-209">In this example, a `<property>` element contains a name/value pair of child elements that specify the port for your app.</span></span>

> [!NOTE]
>
> <span data-ttu-id="9f9e4-210">Las opciones para cambiar el número de puerto en este ejemplo solo son necesarias si va a usar un puerto distinto al predeterminado.</span><span class="sxs-lookup"><span data-stu-id="9f9e4-210">The settings to change the port number in this example are only necessary when you are changing the port from the default.</span></span>
>

1. <span data-ttu-id="9f9e4-211">En el símbolo del sistema o la ventana de terminal que usó anteriormente, vuelva a compilar el archivo JAR con Maven si ha realizado algún cambio en el archivo *pom.xml*; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9f9e4-211">From the command prompt or terminal window that you were using earlier, rebuild the JAR file using Maven if you made any changes to the *pom.xml* file; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="9f9e4-212">Implemente la aplicación web en Azure mediante Maven; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9f9e4-212">Deploy your web app to Azure by using Maven; for example:</span></span>
   ```shell
   mvn azure-webapp:deploy
   ```

<span data-ttu-id="9f9e4-213">Maven implementará la aplicación web en Azure; si la aplicación web no existe, se creará.</span><span class="sxs-lookup"><span data-stu-id="9f9e4-213">Maven will deploy your web app to Azure; if the web app does not already exist, it will be created.</span></span>

> [!NOTE]
>
> <span data-ttu-id="9f9e4-214">Si la región que especifique en el elemento `<region>` del archivo *pom.xml* no tiene suficientes servidores disponibles al iniciar la implementación, aparecerá un error parecido al del siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9f9e4-214">If the region which you specify in the `<region>` element of your *pom.xml* file does not have enough servers available when you start your deployment, you might see an error similar to the following example:</span></span>
>
> ```
> [INFO] Start deploying to Web App maven-linux-app-20170804...
> [INFO] ------------------------------------------------------------------------
> [INFO] BUILD FAILURE
> [INFO] ------------------------------------------------------------------------
> [INFO] Total time: 31.059 s
> [INFO] Finished at: 2017-08-04T12:15:47-07:00
> [INFO] Final Memory: 51M/279M
> [INFO] ------------------------------------------------------------------------
> [ERROR] Failed to execute goal com.microsoft.azure:azure-webapp-maven-plugin:0.1.3:deploy (default-cli) on project gs-spring-boot-docker: null: MojoExecutionException: CloudException: OnError while emitting onNext value: retrofit2.Response.class
> ```
>
> <span data-ttu-id="9f9e4-215">Si esto ocurre, puede especificar otra región y volver a ejecutar el comando Maven para implementar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9f9e4-215">If this happens, you can specify another region and re-run the Maven command to deploy your application.</span></span>
>
>

<span data-ttu-id="9f9e4-216">Cuando se haya implementado la web, podrá administrarla mediante [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="9f9e4-216">When your web has been deployed, you will be able to manage it by using the [Azure portal].</span></span>

* <span data-ttu-id="9f9e4-217">La aplicación web aparecerá en **App Services**:</span><span class="sxs-lookup"><span data-stu-id="9f9e4-217">Your web app will be listed in **App Services**:</span></span>

   ![Aplicación web en la lista de App Services de Azure Portal][AP01]

* <span data-ttu-id="9f9e4-219">Y la dirección URL de la aplicación web se mostrará en la sección de **información general** de la aplicación web:</span><span class="sxs-lookup"><span data-stu-id="9f9e4-219">And the URL for your web app will be listed in the **Overview** for your web app:</span></span>

   ![Determinar la dirección URL de la aplicación web][AP02]

## <a name="next-steps"></a><span data-ttu-id="9f9e4-221">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9f9e4-221">Next steps</span></span>

<span data-ttu-id="9f9e4-222">Para más información acerca de las diferentes tecnologías que se tratan en este artículo, consulte los artículos siguientes:</span><span class="sxs-lookup"><span data-stu-id="9f9e4-222">For more information about the various technologies discussed in this article, see the following articles:</span></span>

* <span data-ttu-id="9f9e4-223">[complemento Maven de Azure Web Apps]</span><span class="sxs-lookup"><span data-stu-id="9f9e4-223">[Maven Plugin for Azure Web Apps]</span></span>

* [<span data-ttu-id="9f9e4-224">Inicio de sesión en Azure desde la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="9f9e4-224">Log in to Azure from the Azure CLI</span></span>](/azure/xplat-cli-connect)

* [<span data-ttu-id="9f9e4-225">Creación de una entidad de servicio de Azure con la CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="9f9e4-225">Create an Azure service principal with Azure CLI 2.0</span></span>](/cli/azure/create-an-azure-service-principal-azure-cli)

* [<span data-ttu-id="9f9e4-226">Referencia de configuración de Maven</span><span class="sxs-lookup"><span data-stu-id="9f9e4-226">Maven Settings Reference</span></span>](https://maven.apache.org/settings.html)

* <span data-ttu-id="9f9e4-227">[Complemento Docker para Maven]</span><span class="sxs-lookup"><span data-stu-id="9f9e4-227">[Docker plugin for Maven]</span></span>

<!-- URL List -->

[Interfaz de la línea de comandos (CLI) de Azure]: /cli/azure/overview
[Azure Container Service (AKS)]: https://azure.microsoft.com/services/container-service/
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Azure Portal]: https://portal.azure.com/
[complemento Maven de Azure Web Apps]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin
[Create a private Docker container registry using the Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Using a custom Docker image for Azure Web App on Linux]: /azure/app-service/containers/tutorial-custom-docker-image
[cliente de Docker]: https://www.docker.com/
[Complemento Docker para Maven]: https://github.com/spotify/docker-maven-plugin
[cuenta de Azure gratuita]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[ventajas como suscriptor de MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[inicial de Spring Boot en Docker]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[SB01]: ./media/deploy-spring-boot-java-app-from-container-registry-using-maven-plugin/SB01.png
[CR01]: ./media/deploy-spring-boot-java-app-from-container-registry-using-maven-plugin/CR01.png
[AP01]: ./media/deploy-spring-boot-java-app-from-container-registry-using-maven-plugin/AP01.png
[AP02]: ./media/deploy-spring-boot-java-app-from-container-registry-using-maven-plugin/AP02.png
[TL01]: ./media/deploy-spring-boot-java-app-from-container-registry-using-maven-plugin/TL01.png
