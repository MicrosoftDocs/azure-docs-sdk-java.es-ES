---
title: "Uso del complemento Maven de Azure Web Apps para implementar una aplicación de Spring Boot en contenedor en Azure"
description: "Aprenda a usar el complemento Maven de Azure Web Apps para implementar una aplicación de Spring Boot en Azure."
services: app-service
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 
ms.author: robmcm;kevinzha
ms.date: 02/01/2018
ms.devlang: java
ms.service: app-service
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: 515cf350f32fc8252644e7022846cc2c9d264ed0
ms.sourcegitcommit: 151aaa6ccc64d94ed67f03e846bab953bde15b4a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/03/2018
---
# <a name="how-to-use-the-maven-plugin-for-azure-web-apps-to-deploy-a-containerized-spring-boot-app-to-azure"></a><span data-ttu-id="9cc3c-103">Uso del complemento Maven de Azure Web Apps para implementar una aplicación de Spring Boot en contenedor en Azure</span><span class="sxs-lookup"><span data-stu-id="9cc3c-103">How to use the Maven Plugin for Azure Web Apps to deploy a containerized Spring Boot app to Azure</span></span>

<span data-ttu-id="9cc3c-104">En este artículo se muestra cómo usar el [complemento Maven para Azure Web Apps](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) para implementar una aplicación de Spring Boot de ejemplo en un contenedor de Docker en Azure App Services.</span><span class="sxs-lookup"><span data-stu-id="9cc3c-104">This article demonstrates using the [Maven Plugin for Azure Web Apps](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) to deploy a sample Spring Boot application in a Docker container to Azure App Services.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="9cc3c-105">El complemento Maven para Azure Web Apps de [Apache Maven](http://maven.apache.org/) proporciona una perfecta integración de Azure App Service en proyectos de Maven y simplifica el proceso para que los desarrolladores implementen aplicaciones web en Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="9cc3c-105">The Maven Plugin for Azure Web Apps for [Apache Maven](http://maven.apache.org/) provides seamless integration of Azure App Service  into Maven projects, and streamlines the process for developers to deploy web apps to Azure App Service.</span></span>
> 
> <span data-ttu-id="9cc3c-106">El complemento Maven de Azure Web Apps está disponible actualmente como versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="9cc3c-106">The Maven Plugin for Azure Web Apps is currently available as a preview.</span></span> <span data-ttu-id="9cc3c-107">Por ahora, solo se admite la publicación FTP, aunque se van a agregar características adicionales en el futuro.</span><span class="sxs-lookup"><span data-stu-id="9cc3c-107">For now, only FTP publishing is supported, although additional features are planned for the future.</span></span>
> 

## <a name="prerequisites"></a><span data-ttu-id="9cc3c-108">requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9cc3c-108">Prerequisites</span></span>

<span data-ttu-id="9cc3c-109">Para realizar los pasos de este tutorial, necesitará tener los siguientes requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="9cc3c-109">In order to complete the steps in this tutorial, you need to have the following prerequisites:</span></span>

* <span data-ttu-id="9cc3c-110">Una suscripción de Azure. Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN] o registrarse para obtener una [cuenta de Azure gratuita].</span><span class="sxs-lookup"><span data-stu-id="9cc3c-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="9cc3c-111">La [Interfaz de la línea de comandos (CLI) de Azure].</span><span class="sxs-lookup"><span data-stu-id="9cc3c-111">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="9cc3c-112">Un [kit de desarrollo de Java (JDK)] actualizado, versión 1.7 o posterior.</span><span class="sxs-lookup"><span data-stu-id="9cc3c-112">An up-to-date [Java Development Kit (JDK)], version 1.7 or later.</span></span>
* <span data-ttu-id="9cc3c-113">La herramienta de compilación [Maven] de Apache (versión 3).</span><span class="sxs-lookup"><span data-stu-id="9cc3c-113">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="9cc3c-114">Un cliente [Git].</span><span class="sxs-lookup"><span data-stu-id="9cc3c-114">A [Git] client.</span></span>
* <span data-ttu-id="9cc3c-115">Un [cliente de Docker].</span><span class="sxs-lookup"><span data-stu-id="9cc3c-115">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="9cc3c-116">Dados los requisitos de virtualización de este tutorial, los pasos que se describen en este artículo no se pueden seguir en una máquina virtual; es preciso usar un equipo físico con características de virtualización habilitadas.</span><span class="sxs-lookup"><span data-stu-id="9cc3c-116">Due to the virtualization requirements of this tutorial, you cannot follow the steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="clone-the-sample-spring-boot-on-docker-web-app"></a><span data-ttu-id="9cc3c-117">Clonación de la aplicación de Spring Boot de ejemplo en la aplicación web de Docker</span><span class="sxs-lookup"><span data-stu-id="9cc3c-117">Clone the sample Spring Boot on Docker web app</span></span>

<span data-ttu-id="9cc3c-118">En esta sección, clone una aplicación de Spring Boot en contenedor y pruébela de forma local.</span><span class="sxs-lookup"><span data-stu-id="9cc3c-118">In this section, you clone a containerized Spring Boot application and test it locally.</span></span>

1. <span data-ttu-id="9cc3c-119">Abra el símbolo del sistema o una ventana de terminal, cree un directorio local para alojar la aplicación de Spring Boot y cambie a dicho directorio, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9cc3c-119">Open a command prompt or terminal window and create a local directory to hold your Spring Boot application, and change to that directory; for example:</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="9cc3c-120">-- o --</span><span class="sxs-lookup"><span data-stu-id="9cc3c-120">-- or --</span></span>
   ```shell
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="9cc3c-121">Clone el proyecto de ejemplo [inicial de Spring Boot en Docker] en el directorio que ha creado, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9cc3c-121">Clone the [Spring Boot on Docker Getting Started] sample project into the directory you created; for example:</span></span>
   ```shell
   git clone https://github.com/microsoft/gs-spring-boot-docker
   ```

1. <span data-ttu-id="9cc3c-122">Cambie de directorio al del proyecto finalizado, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9cc3c-122">Change directory to the completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot-docker/complete
   ```

1. <span data-ttu-id="9cc3c-123">Compile el archivo JAR con Maven, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9cc3c-123">Build the JAR file using Maven; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="9cc3c-124">Cuándo se haya creado la aplicación web, iníciela con Maven. Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9cc3c-124">When the web app has been created, start the web app using Maven; for example:</span></span>
   ```shell
   mvn spring-boot:run
   ```

1. <span data-ttu-id="9cc3c-125">Pruebe la aplicación web. Para ello, navegue a ella localmente mediante un explorador web.</span><span class="sxs-lookup"><span data-stu-id="9cc3c-125">Test the web app by browsing to it locally using a web browser.</span></span> <span data-ttu-id="9cc3c-126">Por ejemplo, puede utilizar el siguiente comando si dispone de curl:</span><span class="sxs-lookup"><span data-stu-id="9cc3c-126">For example, you could use the following command if you have curl available:</span></span>
   ```shell
   curl http://localhost:8080
   ```

1. <span data-ttu-id="9cc3c-127">Debería aparecer el siguiente mensaje: **Hello Docker World**</span><span class="sxs-lookup"><span data-stu-id="9cc3c-127">You should see the following message displayed: **Hello Docker World**</span></span>

## <a name="create-an-azure-service-principal"></a><span data-ttu-id="9cc3c-128">Creación de una entidad de servicio de Azure</span><span class="sxs-lookup"><span data-stu-id="9cc3c-128">Create an Azure service principal</span></span>

<span data-ttu-id="9cc3c-129">En esta sección, va a crear una entidad de servicio de Azure que usa el complemento Maven cuando implementa el contenedor en Azure.</span><span class="sxs-lookup"><span data-stu-id="9cc3c-129">In this section, you create an Azure service principal that the Maven plugin uses when deploying your container to Azure.</span></span>

1. <span data-ttu-id="9cc3c-130">Abra el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="9cc3c-130">Open a command prompt.</span></span>

1. <span data-ttu-id="9cc3c-131">Inicie sesión en la cuenta de Azure mediante la CLI de Azure:</span><span class="sxs-lookup"><span data-stu-id="9cc3c-131">Sign into your Azure account by using the Azure CLI:</span></span>
   ```shell
   az login
   ```
   <span data-ttu-id="9cc3c-132">Siga las instrucciones para completar el proceso de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="9cc3c-132">Follow the instructions to complete the sign-in process.</span></span>

1. <span data-ttu-id="9cc3c-133">Cree una entidad de servicio de Azure:</span><span class="sxs-lookup"><span data-stu-id="9cc3c-133">Create an Azure service principal:</span></span>
   ```shell
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   <span data-ttu-id="9cc3c-134">Donde:</span><span class="sxs-lookup"><span data-stu-id="9cc3c-134">Where:</span></span>
   | <span data-ttu-id="9cc3c-135">.</span><span class="sxs-lookup"><span data-stu-id="9cc3c-135">Parameter</span></span> | <span data-ttu-id="9cc3c-136">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="9cc3c-136">Description</span></span> |
   |---|---|
   | `uuuuuuuu` | <span data-ttu-id="9cc3c-137">Especifica el nombre de usuario para la entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="9cc3c-137">Specifies the user name for the service principal.</span></span> |
   | `pppppppp` | <span data-ttu-id="9cc3c-138">Especifica la contraseña de la entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="9cc3c-138">Specifies the password for the service principal.</span></span> |

1. <span data-ttu-id="9cc3c-139">Azure responde con un archivo JSON que es similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="9cc3c-139">Azure responds with JSON that resembles the following example:</span></span>
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
   > <span data-ttu-id="9cc3c-140">Utilizará los valores de esta respuesta JSON al configurar el complemento de Maven para implementar el contenedor en Azure.</span><span class="sxs-lookup"><span data-stu-id="9cc3c-140">You will use the values from this JSON response when you configure the Maven plugin to deploy your container to Azure.</span></span> <span data-ttu-id="9cc3c-141">`aaaaaaaa`, `uuuuuuuu`, `pppppppp` y `tttttttt` son valores de marcador de posición que se usan en este ejemplo para que sea más fácil asignar estos valores a sus respectivos elementos al configurar el archivo `settings.xml` de Maven en la sección siguiente.</span><span class="sxs-lookup"><span data-stu-id="9cc3c-141">The `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, and `tttttttt` are placeholder values, which are used in this example to make it easier to map these values to their respective elements when you configure your Maven `settings.xml` file in the next section.</span></span>
   >
   >

## <a name="configure-maven-to-use-your-azure-service-principal"></a><span data-ttu-id="9cc3c-142">Configurar Maven para usar la entidad de servicio de Azure</span><span class="sxs-lookup"><span data-stu-id="9cc3c-142">Configure Maven to use your Azure service principal</span></span>

<span data-ttu-id="9cc3c-143">En esta sección, utilice los valores de la entidad de servicio de Azure para configurar la autenticación que va a usar Maven al implementar el contenedor en Azure.</span><span class="sxs-lookup"><span data-stu-id="9cc3c-143">In this section, you use the values from your Azure service principal to configure the authentication that Maven will use when deploying your container to Azure.</span></span>

1. <span data-ttu-id="9cc3c-144">Abra el archivo `settings.xml` de Maven en un editor de texto; este archivo puede encontrarse en una ruta de acceso como la de los ejemplos siguientes:</span><span class="sxs-lookup"><span data-stu-id="9cc3c-144">Open your Maven `settings.xml` file in a text editor; this file might be in a path like the following examples:</span></span>
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. <span data-ttu-id="9cc3c-145">Agregue la configuración de la entidad de servicio de la sección anterior de este tutorial a la colección `<servers>` en el archivo *settings.xml*, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9cc3c-145">Add your Azure service principal settings from the previous section of this tutorial to the `<servers>` collection in the *settings.xml* file; for example:</span></span>

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
   <span data-ttu-id="9cc3c-146">Donde:</span><span class="sxs-lookup"><span data-stu-id="9cc3c-146">Where:</span></span>
   | <span data-ttu-id="9cc3c-147">Elemento</span><span class="sxs-lookup"><span data-stu-id="9cc3c-147">Element</span></span> | <span data-ttu-id="9cc3c-148">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="9cc3c-148">Description</span></span> |
   |---|---|
   | `<id>` | <span data-ttu-id="9cc3c-149">Especifica un nombre único que Maven utiliza para buscar la configuración de seguridad al implementar la aplicación web en Azure.</span><span class="sxs-lookup"><span data-stu-id="9cc3c-149">Specifies a unique name which Maven uses to look up your security settings when you deploy your web app to Azure.</span></span> |
   | `<client>` | <span data-ttu-id="9cc3c-150">Contiene el valor `appId` de la entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="9cc3c-150">Contains the `appId` value from your service principal.</span></span> |
   | `<tenant>` | <span data-ttu-id="9cc3c-151">Contiene el valor `tenant` de la entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="9cc3c-151">Contains the `tenant` value from your service principal.</span></span> |
   | `<key>` | <span data-ttu-id="9cc3c-152">Contiene el valor `password` de la entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="9cc3c-152">Contains the `password` value from your service principal.</span></span> |
   | `<environment>` | <span data-ttu-id="9cc3c-153">Define el entorno en la nube de Azure de destino, que es `AZURE` en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="9cc3c-153">Defines the target Azure cloud environment, which is `AZURE` in this example.</span></span> <span data-ttu-id="9cc3c-154">(Una lista completa de los entornos está disponible en la documentación del [complemento Maven de Azure Web Apps]).</span><span class="sxs-lookup"><span data-stu-id="9cc3c-154">(A full list of environments is available in the [Maven Plugin for Azure Web Apps] documentation)</span></span> |

1. <span data-ttu-id="9cc3c-155">Guarde y cierre el archivo *settings.xml*.</span><span class="sxs-lookup"><span data-stu-id="9cc3c-155">Save and close the *settings.xml* file.</span></span>

## <a name="optional-deploy-your-local-docker-file-to-docker-hub"></a><span data-ttu-id="9cc3c-156">OPCIONAL: Implemente el archivo local de Docker en Docker Hub</span><span class="sxs-lookup"><span data-stu-id="9cc3c-156">OPTIONAL: Deploy your local Docker file to Docker Hub</span></span>

<span data-ttu-id="9cc3c-157">Si tiene una cuenta de Docker, puede generar la imagen de contenedor de Docker localmente e insertarla en Docker Hub.</span><span class="sxs-lookup"><span data-stu-id="9cc3c-157">If you have a Docker account, you can build your Docker container image locally and push it to Docker Hub.</span></span> <span data-ttu-id="9cc3c-158">Para ello, siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="9cc3c-158">To do so, use the following steps.</span></span>

1. <span data-ttu-id="9cc3c-159">Abra el archivo `pom.xml` de la aplicación de Spring Boot en un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="9cc3c-159">Open the `pom.xml` file for your Spring Boot application in a text editor.</span></span>

1. <span data-ttu-id="9cc3c-160">Busque el elemento secundario `<imageName>` del elemento `<containerSettings>`.</span><span class="sxs-lookup"><span data-stu-id="9cc3c-160">Locate the `<imageName>` child element of the `<containerSettings>` element.</span></span>

1. <span data-ttu-id="9cc3c-161">Actualice el valor `${docker.image.prefix}` con el nombre de la cuenta de Docker:</span><span class="sxs-lookup"><span data-stu-id="9cc3c-161">Update the `${docker.image.prefix}` value with your Docker account name:</span></span>
   ```xml
   <containerSettings>
      <imageName>mydockeraccountname/${project.artifactId}</imageName>
   </containerSettings>
   ```

1. <span data-ttu-id="9cc3c-162">Elija uno de los siguientes métodos de implementación:</span><span class="sxs-lookup"><span data-stu-id="9cc3c-162">Choose one of the following deployment methods:</span></span>

   * <span data-ttu-id="9cc3c-163">Cree la imagen de contenedor localmente con Maven y, a continuación, use Docker para insertar el contenedor en Docker Hub:</span><span class="sxs-lookup"><span data-stu-id="9cc3c-163">Build your container image locally with Maven, and then use Docker to push your container to Docker Hub:</span></span>
      ```shell
      mvn clean package docker:build
      docker push
      ```
   
   * <span data-ttu-id="9cc3c-164">Si tiene el [complemento de Docker para Maven] instalado, puede generar automáticamente la imagen del contenedor en Docker Hub mediante el parámetro `-DpushImage`:</span><span class="sxs-lookup"><span data-stu-id="9cc3c-164">If you have the [Docker plugin for Maven] installed, you can automatically build and your container image to Docker Hub by using the `-DpushImage` parameter:</span></span>
      ```shell
      mvn clean package docker:build -DpushImage
      ```

## <a name="optional-customize-your-pomxml-before-deploying-your-container-to-azure"></a><span data-ttu-id="9cc3c-165">OPCIONAL: Personalice el archivo pom.xml antes de implementar el contenedor en Azure</span><span class="sxs-lookup"><span data-stu-id="9cc3c-165">OPTIONAL: Customize your pom.xml before deploying your container to Azure</span></span>

<span data-ttu-id="9cc3c-166">Abra el archivo `pom.xml` de la aplicación de Spring Boot en un editor de texto y, a continuación, busque el elemento `<plugin>` de `azure-webapp-maven-plugin`.</span><span class="sxs-lookup"><span data-stu-id="9cc3c-166">Open the `pom.xml` file for your Spring Boot application in a text editor, and then locate the `<plugin>` element for `azure-webapp-maven-plugin`.</span></span> <span data-ttu-id="9cc3c-167">Este elemento debe tener un aspecto similar al ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="9cc3c-167">This element should resemble the following example:</span></span>

   ```xml
   <plugin>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-webapp-maven-plugin</artifactId>
      <version>0.1.3</version>
      <configuration>
         <authentication>
            <serverId>azure-auth</serverId>
         </authentication>
         <resourceGroup>maven-plugin</resourceGroup>
         <appName>maven-linux-app-${maven.build.timestamp}</appName>
         <region>westus</region>
         <containerSettings>
            <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
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

<span data-ttu-id="9cc3c-168">Hay varios valores que se pueden modificar en el complemento Maven; puede encontrar una descripción detallada de cada uno de estos elementos en la documentación del [complemento Maven de Azure Web Apps].</span><span class="sxs-lookup"><span data-stu-id="9cc3c-168">There are several values that you can modify for the Maven plugin, and a detailed description for each of these elements is available in the [Maven Plugin for Azure Web Apps] documentation.</span></span> <span data-ttu-id="9cc3c-169">Dicho esto, hay varios valores que merece la pena destacar en este artículo:</span><span class="sxs-lookup"><span data-stu-id="9cc3c-169">That being said, there are several values that are worth highlighting in this article:</span></span>

| <span data-ttu-id="9cc3c-170">Elemento</span><span class="sxs-lookup"><span data-stu-id="9cc3c-170">Element</span></span> | <span data-ttu-id="9cc3c-171">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="9cc3c-171">Description</span></span> |
|---|---|
| `<version>` | <span data-ttu-id="9cc3c-172">Especifica la versión del [complemento Maven de Azure Web Apps].</span><span class="sxs-lookup"><span data-stu-id="9cc3c-172">Specifies the version of the [Maven Plugin for Azure Web Apps].</span></span> <span data-ttu-id="9cc3c-173">Debe comprobar la versión que aparece en el [repositorio central de Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) para asegurarse de que está utilizando la versión más reciente.</span><span class="sxs-lookup"><span data-stu-id="9cc3c-173">You should check the version listed in the [Maven Central Respository](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) to ensure that you are using the latest version.</span></span> |
| `<authentication>` | <span data-ttu-id="9cc3c-174">Especifica la información de autenticación de Azure que, en este ejemplo, incluye un elemento `<serverId>` que contiene `azure-auth`; Maven utiliza ese valor para buscar los valores de la entidad de servicio de Azure en el archivo *settings.xml* que se definió en una sección anterior de este artículo.</span><span class="sxs-lookup"><span data-stu-id="9cc3c-174">Specifies the authentication information for Azure, which in this example contains a `<serverId>` element that contains `azure-auth`; Maven uses that value to look up the Azure service principal values in your Maven *settings.xml* file, which you defined in an earlier section of this article.</span></span> |
| `<resourceGroup>` | <span data-ttu-id="9cc3c-175">Especifica el grupo de recursos de destino, que es `maven-plugin` en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="9cc3c-175">Specifies the target resource group, which is `maven-plugin` in this example.</span></span> <span data-ttu-id="9cc3c-176">Se creará este grupo de recursos durante la implementación si todavía no existe.</span><span class="sxs-lookup"><span data-stu-id="9cc3c-176">The resource group will be created during deployment if it does not already exist.</span></span> |
| `<appName>` | <span data-ttu-id="9cc3c-177">Especifica el nombre de destino de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="9cc3c-177">Specifies the target name for your web app.</span></span> <span data-ttu-id="9cc3c-178">En este ejemplo, el nombre de destino es `maven-linux-app-${maven.build.timestamp}`, donde el sufijo `${maven.build.timestamp}` se anexa en este ejemplo para evitar conflictos.</span><span class="sxs-lookup"><span data-stu-id="9cc3c-178">In this example, the target name is `maven-linux-app-${maven.build.timestamp}`, where the `${maven.build.timestamp}` suffix is appended in this example to avoid conflict.</span></span> <span data-ttu-id="9cc3c-179">(La marca de tiempo es opcional; puede especificar cualquier cadena única para el nombre de la aplicación).</span><span class="sxs-lookup"><span data-stu-id="9cc3c-179">(The timestamp is optional; you can specify any unique string for the app name.)</span></span> |
| `<region>` | <span data-ttu-id="9cc3c-180">Especifica la región de destino, que en este ejemplo es `westus`.</span><span class="sxs-lookup"><span data-stu-id="9cc3c-180">Specifies the target region, which in this example is `westus`.</span></span> <span data-ttu-id="9cc3c-181">(Puede encontrar una lista completa en la documentación del [complemento Maven de Azure Web Apps]).</span><span class="sxs-lookup"><span data-stu-id="9cc3c-181">(A full list is in the [Maven Plugin for Azure Web Apps] documentation.)</span></span> |
| `<appSettings>` | <span data-ttu-id="9cc3c-182">Especifica los valores únicos de Maven que se deben usar durante la implementación de la aplicación web en Azure.</span><span class="sxs-lookup"><span data-stu-id="9cc3c-182">Specifies any unique settings for Maven to use when deploying your web app to Azure.</span></span> <span data-ttu-id="9cc3c-183">En este ejemplo, un elemento `<property>` contiene un par nombre/valor de elementos secundarios que especifican el puerto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9cc3c-183">In this example, a `<property>` element contains a name/value pair of child elements that specify the port for your app.</span></span> |

> [!NOTE]
>
> <span data-ttu-id="9cc3c-184">Las opciones para cambiar el número de puerto en este ejemplo solo son necesarias si va a usar un puerto distinto al predeterminado.</span><span class="sxs-lookup"><span data-stu-id="9cc3c-184">The settings to change the port number in this example are only necessary when you are changing the port from the default.</span></span>
>

## <a name="build-and-deploy-your-container-to-azure"></a><span data-ttu-id="9cc3c-185">Compilar e implementar el contenedor en Azure</span><span class="sxs-lookup"><span data-stu-id="9cc3c-185">Build and deploy your container to Azure</span></span>

<span data-ttu-id="9cc3c-186">Una vez haya configurado todas las opciones en las secciones anteriores de este artículo, está listo para implementar el contenedor en Azure.</span><span class="sxs-lookup"><span data-stu-id="9cc3c-186">Once you have configured all of the settings in the preceding sections of this article, you are ready to deploy your container to Azure.</span></span> <span data-ttu-id="9cc3c-187">Para ello, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="9cc3c-187">To do so, use the following steps:</span></span>

1. <span data-ttu-id="9cc3c-188">En el símbolo del sistema o la ventana de terminal que usó anteriormente, vuelva a compilar el archivo JAR con Maven si ha realizado algún cambio en el archivo *pom.xml*; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9cc3c-188">From the command prompt or terminal window that you were using earlier, rebuild the JAR file using Maven if you made any changes to the *pom.xml* file; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="9cc3c-189">Implemente la aplicación web en Azure mediante Maven; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9cc3c-189">Deploy your web app to Azure by using Maven; for example:</span></span>
   ```shell
   mvn azure-webapp:deploy
   ```

<span data-ttu-id="9cc3c-190">Maven implementará la aplicación web en Azure; si la aplicación web no existe, se creará.</span><span class="sxs-lookup"><span data-stu-id="9cc3c-190">Maven will deploy your web app to Azure; if the web app does not already exist, it will be created.</span></span>

> [!NOTE]
>
> <span data-ttu-id="9cc3c-191">Si la región que especifique en el elemento `<region>` del archivo *pom.xml* no tiene suficientes servidores disponibles al iniciar la implementación, aparecerá un error parecido al del siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9cc3c-191">If the region which you specify in the `<region>` element of your *pom.xml* file does not have enough servers available when you start your deployment, you might see an error similar to the following example:</span></span>
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
> <span data-ttu-id="9cc3c-192">Si esto ocurre, puede especificar otra región y volver a ejecutar el comando Maven para implementar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9cc3c-192">If this happens, you can specify another region and re-run the Maven command to deploy your application.</span></span>
>
>

<span data-ttu-id="9cc3c-193">Cuando se haya implementado la web, podrá administrarla mediante [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="9cc3c-193">When your web has been deployed, you will be able to manage it by using the [Azure portal].</span></span>

* <span data-ttu-id="9cc3c-194">La aplicación web aparecerá en **App Services**:</span><span class="sxs-lookup"><span data-stu-id="9cc3c-194">Your web app will be listed in **App Services**:</span></span>

   ![Aplicación web en la lista de App Services de Azure Portal][AP01]

* <span data-ttu-id="9cc3c-196">Y la dirección URL de la aplicación web se mostrará en la sección de **información general** de la aplicación web:</span><span class="sxs-lookup"><span data-stu-id="9cc3c-196">And the URL for your web app will be listed in the **Overview** for your web app:</span></span>

   ![Determinar la dirección URL de la aplicación web][AP02]

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

## <a name="next-steps"></a><span data-ttu-id="9cc3c-198">pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9cc3c-198">Next steps</span></span>

<span data-ttu-id="9cc3c-199">Para más información acerca de las diferentes tecnologías que se tratan en este artículo, consulte los artículos siguientes:</span><span class="sxs-lookup"><span data-stu-id="9cc3c-199">For more information about the various technologies discussed in this article, see the following articles:</span></span>

* <span data-ttu-id="9cc3c-200">[complemento Maven de Azure Web Apps]</span><span class="sxs-lookup"><span data-stu-id="9cc3c-200">[Maven Plugin for Azure Web Apps]</span></span>

* [<span data-ttu-id="9cc3c-201">Inicio de sesión en Azure desde la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="9cc3c-201">Log in to Azure from the Azure CLI</span></span>](/azure/xplat-cli-connect)

* [<span data-ttu-id="9cc3c-202">Uso del complemento Maven de Azure Web Apps para implementar una aplicación de Spring Boot en Azure App Service </span><span class="sxs-lookup"><span data-stu-id="9cc3c-202">How to use the Maven Plugin for Azure Web Apps to deploy a Spring Boot app to Azure App Service </span></span>](deploy-spring-boot-java-app-with-maven-plugin.md)

* [<span data-ttu-id="9cc3c-203">Creación de una entidad de servicio de Azure con la CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="9cc3c-203">Create an Azure service principal with Azure CLI 2.0</span></span>](/cli/azure/create-an-azure-service-principal-azure-cli)

* [<span data-ttu-id="9cc3c-204">Referencia de configuración de Maven</span><span class="sxs-lookup"><span data-stu-id="9cc3c-204">Maven Settings Reference</span></span>](https://maven.apache.org/settings.html)

* <span data-ttu-id="9cc3c-205">[complemento de Docker para Maven]</span><span class="sxs-lookup"><span data-stu-id="9cc3c-205">[Docker plugin for Maven]</span></span>

<!-- URL List -->

[Interfaz de la línea de comandos (CLI) de Azure]: /cli/azure/overview
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Azure Portal]: https://portal.azure.com/
[cliente de Docker]: https://www.docker.com/
[complemento de Docker para Maven]: https://github.com/spotify/docker-maven-plugin
[cuenta de Azure gratuita]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[ventajas como suscriptor de MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[inicial de Spring Boot en Docker]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/
[complemento Maven de Azure Web Apps]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin

<!-- IMG List -->

[AP01]: ./media/deploy-containerized-spring-boot-java-app-with-maven-plugin/AP01.png
[AP02]: ./media/deploy-containerized-spring-boot-java-app-with-maven-plugin/AP02.png
