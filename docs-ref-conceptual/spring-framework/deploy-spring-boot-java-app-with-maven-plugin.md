---
title: Implementación de una aplicación de Spring Boot en la nube con Maven y Azure
description: Obtenga información acerca de cómo implementar una aplicación de Spring Boot en la nube con el complemento de Maven para Azure Web Apps.
services: app-service
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: brborges
ms.assetid: ''
ms.author: robmcm;kevinzha;brborges
ms.date: 06/01/2018
ms.devlang: java
ms.service: app-service
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: ca788354d26964bd9f1e21a0d3a8005ff65ce4bc
ms.sourcegitcommit: 280d13b43cef94177d95e03879a5919da234a23c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/31/2018
ms.locfileid: "43324351"
---
# <a name="deploy-a-spring-boot-app-to-the-cloud-using-the-maven-plugin-for-azure-app-service"></a><span data-ttu-id="86edf-103">Implementación de una aplicación de Spring Boot en la nube con el complemento de Maven para Azure App Service</span><span class="sxs-lookup"><span data-stu-id="86edf-103">Deploy a Spring Boot app to the cloud using the Maven Plugin for Azure App Service</span></span>

<span data-ttu-id="86edf-104">En este artículo se muestra cómo utilizar el complemento Maven de Azure App Service Web Apps para implementar una aplicación de Spring Boot de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="86edf-104">This article demonstrates using the Maven Plugin for Azure App Service Web Apps to deploy a sample Spring Boot application.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="86edf-105">El [complemento Maven para Azure App Service Web Apps](https://docs.microsoft.com/java/api/overview/azure/maven/azure-webapp-maven-plugin/readme) para [Apache Maven](http://maven.apache.org/) proporciona una perfecta integración de Azure App Service en proyectos de Maven y simplifica el proceso para que los desarrolladores implementen aplicaciones web en Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="86edf-105">The [Maven Plugin for Azure App Service Web Apps](https://docs.microsoft.com/java/api/overview/azure/maven/azure-webapp-maven-plugin/readme) for [Apache Maven](http://maven.apache.org/) provides seamless integration of Azure App Service into Maven projects, and streamlines the process for developers to deploy web apps to Azure App Service.</span></span>

<span data-ttu-id="86edf-106">Antes de usar el complemento Maven, obtenga en Maven Central la última versión disponible del complemento: [![Maven Central](https://img.shields.io/maven-central/v/com.microsoft.azure/azure-webapp-maven-plugin.svg)](http://search.maven.org/#search%7Cga%7C1%7Cg%3A%22com.microsoft.azure%22%20AND%20a%3A%22azure-webapp-maven-plugin%22)</span><span class="sxs-lookup"><span data-stu-id="86edf-106">Before using the Maven plugin, check on Maven Central for the latest available version of the plugin: [![Maven Central](https://img.shields.io/maven-central/v/com.microsoft.azure/azure-webapp-maven-plugin.svg)](http://search.maven.org/#search%7Cga%7C1%7Cg%3A%22com.microsoft.azure%22%20AND%20a%3A%22azure-webapp-maven-plugin%22)</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="86edf-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="86edf-107">Prerequisites</span></span>

<span data-ttu-id="86edf-108">Para realizar los pasos de este tutorial, necesitará tener los siguientes requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="86edf-108">In order to complete the steps in this tutorial, you will need to have the following prerequisites:</span></span>

* <span data-ttu-id="86edf-109">Si todavía no tiene una suscripción a Azure, puede registrarse para obtener una [cuenta de Azure gratuita].</span><span class="sxs-lookup"><span data-stu-id="86edf-109">An Azure subscription; if you don't already have an Azure subscription, you can sign up for a [free Azure account].</span></span>
* <span data-ttu-id="86edf-110">La [Interfaz de la línea de comandos (CLI) de Azure].</span><span class="sxs-lookup"><span data-stu-id="86edf-110">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="86edf-111">Un [kit de desarrollo de Java (JDK)] actualizado, versión 1.7 o posterior.</span><span class="sxs-lookup"><span data-stu-id="86edf-111">An up-to-date [Java Development Kit (JDK)], version 1.7 or later.</span></span>
* <span data-ttu-id="86edf-112">La herramienta de compilación [Maven] de Apache (versión 3).</span><span class="sxs-lookup"><span data-stu-id="86edf-112">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="86edf-113">Un cliente [Git].</span><span class="sxs-lookup"><span data-stu-id="86edf-113">A [Git] client.</span></span>

## <a name="clone-the-sample-spring-boot-web-app"></a><span data-ttu-id="86edf-114">Clonación de la aplicación web de Spring Boot de ejemplo</span><span class="sxs-lookup"><span data-stu-id="86edf-114">Clone the sample Spring Boot web app</span></span>

<span data-ttu-id="86edf-115">En esta sección, va a clonar una aplicación de Spring Boot terminada y a probarla de forma local.</span><span class="sxs-lookup"><span data-stu-id="86edf-115">In this section, you will clone a completed Spring Boot application and test it locally.</span></span>

1. <span data-ttu-id="86edf-116">Abra el símbolo del sistema o una ventana de terminal, cree un directorio local para alojar la aplicación de Spring Boot y cambie a dicho directorio, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="86edf-116">Open a command prompt or terminal window and create a local directory to hold your Spring Boot application, and change to that directory; for example:</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="86edf-117">-- o --</span><span class="sxs-lookup"><span data-stu-id="86edf-117">-- or --</span></span>
   ```shell
   md ~/SpringBoot
   cd ~/SpringBoot
   ```

1. <span data-ttu-id="86edf-118">Clone el proyecto de ejemplo [Primeros pasos de Spring Boot] en el directorio que creó, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="86edf-118">Clone the [Spring Boot Getting Started] sample project into the directory you created; for example:</span></span>
   ```shell
   git clone https://github.com/spring-guides/gs-spring-boot
   ```

1. <span data-ttu-id="86edf-119">Cambie de directorio al del proyecto finalizado, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="86edf-119">Change directory to the completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot/complete
   ```

1. <span data-ttu-id="86edf-120">Compile el archivo JAR con Maven, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="86edf-120">Build the JAR file using Maven; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="86edf-121">Cuándo se haya creado la aplicación web, iníciela con Maven. Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="86edf-121">When the web app has been created, start the web app using Maven; for example:</span></span>
   ```shell
   mvn spring-boot:run
   ```

1. <span data-ttu-id="86edf-122">Pruebe la aplicación web. Para ello, navegue a ella localmente mediante un explorador web.</span><span class="sxs-lookup"><span data-stu-id="86edf-122">Test the web app by browsing to it locally using a web browser.</span></span> <span data-ttu-id="86edf-123">Por ejemplo, puede utilizar el siguiente comando si dispone de curl:</span><span class="sxs-lookup"><span data-stu-id="86edf-123">For example, you could use the following command if you have curl available:</span></span>
   ```shell
   curl http://localhost:8080
   ```

1. <span data-ttu-id="86edf-124">Debería aparecer el siguiente mensaje: **Greetings from Spring Boot!** (Saludos de Spring Boot).</span><span class="sxs-lookup"><span data-stu-id="86edf-124">You should see the following message displayed: **Greetings from Spring Boot!**</span></span>

## <a name="adjust-project-for-war-based-deployment-on-azure-app-service"></a><span data-ttu-id="86edf-125">Ajuste del proyecto para una implementación basada en WAR en Azure App Service</span><span class="sxs-lookup"><span data-stu-id="86edf-125">Adjust project for WAR-based deployment on Azure App Service</span></span>

<span data-ttu-id="86edf-126">En esta sección, se ajustará rápidamente el proyecto de Spring Boot para implementarlo como un archivo WAR en Azure App Service, que proporciona Tomcat como sistema de tiempo de ejecución de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="86edf-126">In this section we will quickly adjust the Spring Boot project to be deployed as a WAR file on Azure App Service, which provides Tomcat as the runtime by default.</span></span> <span data-ttu-id="86edf-127">Para que funcione, hay que modificar dos archivos:</span><span class="sxs-lookup"><span data-stu-id="86edf-127">For this to work, there are two files to be modified:</span></span>

- <span data-ttu-id="86edf-128">El archivo `pom.xml` de Maven</span><span class="sxs-lookup"><span data-stu-id="86edf-128">The Maven `pom.xml` file</span></span>
- <span data-ttu-id="86edf-129">La clase `Application` de Java</span><span class="sxs-lookup"><span data-stu-id="86edf-129">The `Application` Java class</span></span>

<span data-ttu-id="86edf-130">Comencemos con la configuración de Maven:</span><span class="sxs-lookup"><span data-stu-id="86edf-130">Let's start with the Maven settings:</span></span>

1. <span data-ttu-id="86edf-131">Abra `pom.xml`</span><span class="sxs-lookup"><span data-stu-id="86edf-131">Open `pom.xml`</span></span>

1. <span data-ttu-id="86edf-132">Agregue `<packaging>war</packaging>` justo después de la definición `<artifactId>` en la parte superior:</span><span class="sxs-lookup"><span data-stu-id="86edf-132">Add `<packaging>war</packaging>` right after the `<artifactId>` definition at the top:</span></span>
   ```xml
    <modelVersion>4.0.0</modelVersion>
    <groupId>org.springframework</groupId>
    <artifactId>gs-spring-boot</artifactId>

    <packaging>war</packaging>
   ```

1. <span data-ttu-id="86edf-133">Agregue la siguiente dependencia:</span><span class="sxs-lookup"><span data-stu-id="86edf-133">Add the following dependency:</span></span>
   ```xml
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-tomcat</artifactId>
            <scope>provided</scope>
        </dependency>
   ```

<span data-ttu-id="86edf-134">Ahora, abra la clase `Application`, esperemos que después de que el IDE haya seleccionado las nuevas dependencias, y realice las siguientes modificaciones:</span><span class="sxs-lookup"><span data-stu-id="86edf-134">Now open the class `Application`, hopefully after your IDE has already picked up the new dependencies, and proceed with the following modifications:</span></span>

1. <span data-ttu-id="86edf-135">Haga que la clase Application sea una subclase de `SpringBootServletInitializer`:</span><span class="sxs-lookup"><span data-stu-id="86edf-135">Make class Application a subclass of `SpringBootServletInitializer`:</span></span>
   ```java
   @SpringBootApplication
   public class Application extends SpringBootServletInitializer {
     // ...
   }
   ```

1. <span data-ttu-id="86edf-136">Agregue el método siguiente a la clase Application:</span><span class="sxs-lookup"><span data-stu-id="86edf-136">Add the following method to the Application class:</span></span>
   ```java
       @Override
       protected SpringApplicationBuilder configure(SpringApplicationBuilder application) {
           return application.sources(Application.class);
       }
   ```
1. <span data-ttu-id="86edf-137">Organice las importaciones para asegurarse de que `SpringApplicationBuilder` y `SpringBootServletInitializer` se importan correctamente.</span><span class="sxs-lookup"><span data-stu-id="86edf-137">Organize your imports to ensure `SpringApplicationBuilder` and `SpringBootServletInitializer` are properly imported.</span></span>

<span data-ttu-id="86edf-138">La aplicación ahora está lista para implementarse en Tomcat y otros sistemas de tiempo de ejecución de servlet (por ejemplo, Jetty).</span><span class="sxs-lookup"><span data-stu-id="86edf-138">Your application is now ready to be deployed to Tomcat and any other Servlet runtime (e.g. Jetty).</span></span>

## <a name="add-the-maven-plugin-for-azure-app-service-web-apps"></a><span data-ttu-id="86edf-139">Adición del complemento Maven para Azure App Service Web Apps</span><span class="sxs-lookup"><span data-stu-id="86edf-139">Add the Maven Plugin for Azure App Service Web Apps</span></span>

<span data-ttu-id="86edf-140">En esta sección, agregaremos un complemento de Maven que automatizará toda la implementación de esta aplicación en Azure App Service Web Apps.</span><span class="sxs-lookup"><span data-stu-id="86edf-140">In this section, we will add a Maven plugin that will automate the entire deployment of this application into Azure App Service Web Apps.</span></span>

1. <span data-ttu-id="86edf-141">Abra `pom.xml` de nuevo.</span><span class="sxs-lookup"><span data-stu-id="86edf-141">Open `pom.xml` once again.</span></span>

1. <span data-ttu-id="86edf-142">Dentro de `<properties>`, establezca un formato de marca de tiempo personalizado con la propiedad `maven.build.timestamp.format`.</span><span class="sxs-lookup"><span data-stu-id="86edf-142">Inside `<properties>`, set a custom timestamp format with the property `maven.build.timestamp.format`.</span></span> <span data-ttu-id="86edf-143">Como Azure App Service crea una dirección URL pública para la aplicación, se usará esta configuración para generar el nombre de la implementación y evitar conflictos con las implementaciones activas de otros usuarios.</span><span class="sxs-lookup"><span data-stu-id="86edf-143">Because Azure App Service creates a public URL for your application, this setting will be used to generate the name of your deployment, and avoid conflict with other users' live deployments.</span></span>
   ```xml
    <properties>
        <java.version>1.8</java.version>
        <maven.build.timestamp.format>yyyyMMddHHmmssSSS</maven.build.timestamp.format>
    </properties>
   ```

1. <span data-ttu-id="86edf-144">En el elemento `<plugins>`, agregue lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="86edf-144">In the `<plugins>` element, add the following:</span></span>
   ```xml
    <plugin>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-webapp-maven-plugin</artifactId>
      <!-- Check latest version on Maven Central -->
      <version>1.1.0</version>
    </plugin>
   ```

<span data-ttu-id="86edf-145">Con esta configuración, el proyecto de Maven ya está listo para su implementación en vivo en Azure App Service Web Apps.</span><span class="sxs-lookup"><span data-stu-id="86edf-145">With these settings, your Maven project is now ready for live deployment to Azure App Service Web App.</span></span>

## <a name="install-and-log-in-to-azure-cli"></a><span data-ttu-id="86edf-146">Instalación y inicio de sesión en la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="86edf-146">Install and log in to Azure CLI</span></span>

<span data-ttu-id="86edf-147">La manera más sencilla y fácil de obtener el complemento Maven para implementar la aplicación de Spring Boot es con la [CLI de Azure](https://docs.microsoft.com/cli/azure/).</span><span class="sxs-lookup"><span data-stu-id="86edf-147">The simplest and easiest way to get the Maven Plugin deploying your Spring Boot application is by using [Azure CLI](https://docs.microsoft.com/cli/azure/).</span></span> <span data-ttu-id="86edf-148">Asegúrese de que la tiene instalada.</span><span class="sxs-lookup"><span data-stu-id="86edf-148">Make sure you have it installed.</span></span>

1. <span data-ttu-id="86edf-149">Inicie sesión en la cuenta de Azure mediante la CLI de Azure:</span><span class="sxs-lookup"><span data-stu-id="86edf-149">Sign into your Azure account by using the Azure CLI:</span></span>
   
   ```shell
   az login
   ```
   
   <span data-ttu-id="86edf-150">Siga las instrucciones para completar el proceso de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="86edf-150">Follow the instructions to complete the sign-in process.</span></span>

## <a name="optionally-customize-pomxml-before-deploying"></a><span data-ttu-id="86edf-151">También puede personalizar el archivo pom.xml antes de la implementación.</span><span class="sxs-lookup"><span data-stu-id="86edf-151">Optionally, customize pom.xml before deploying</span></span>

<span data-ttu-id="86edf-152">Abra el archivo `pom.xml` de la aplicación de Spring Boot en un editor de texto y, a continuación, busque el elemento `<plugin>` de `azure-webapp-maven-plugin`.</span><span class="sxs-lookup"><span data-stu-id="86edf-152">Open the `pom.xml` file for your Spring Boot application in a text editor, and then locate the `<plugin>` element for `azure-webapp-maven-plugin`.</span></span> <span data-ttu-id="86edf-153">Este elemento debe tener un aspecto similar al ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="86edf-153">This element should resemble the following example:</span></span>

   ```xml
  <plugins>
    <plugin>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-webapp-maven-plugin</artifactId>
      <!-- Check latest version on Maven Central -->
      <version>1.1.0</version>
      <configuration>
         <resourceGroup>maven-projects</resourceGroup>
         <appName>${project.artifactId}-${maven.build.timestamp}</appName>
         <region>westus</region>
         <javaVersion>1.8</javaVersion>
         <deploymentType>war</deploymentType>
      </configuration>
    </plugin>
  </plugins>
   ```

<span data-ttu-id="86edf-154">Hay varios valores que se pueden modificar en el complemento Maven; puede encontrar una descripción detallada de cada uno de estos elementos en la documentación del [complemento Maven de Azure Web Apps].</span><span class="sxs-lookup"><span data-stu-id="86edf-154">There are several values that you can modify for the Maven plugin, and a detailed description for each of these elements is available in the [Maven Plugin for Azure Web Apps] documentation.</span></span> <span data-ttu-id="86edf-155">Dicho esto, hay varios valores que merece la pena destacar en este artículo:</span><span class="sxs-lookup"><span data-stu-id="86edf-155">That being said, there are several values that are worth highlighting in this article:</span></span>

| <span data-ttu-id="86edf-156">Elemento</span><span class="sxs-lookup"><span data-stu-id="86edf-156">Element</span></span> | <span data-ttu-id="86edf-157">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="86edf-157">Description</span></span> |
|---|---|
| `<version>` | <span data-ttu-id="86edf-158">Especifica la versión del [complemento Maven de Azure Web Apps].</span><span class="sxs-lookup"><span data-stu-id="86edf-158">Specifies the version of the [Maven Plugin for Azure Web Apps].</span></span> <span data-ttu-id="86edf-159">Compruebe que la versión que aparece en el [repositorio central de Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) para asegurarse de que está utilizando la versión más reciente.</span><span class="sxs-lookup"><span data-stu-id="86edf-159">Verify the version listed in the [Maven Central Respository](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) to ensure that you are using the latest version.</span></span> |
| `<resourceGroup>` | <span data-ttu-id="86edf-160">Especifica el grupo de recursos de destino, que es `maven-plugin` en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="86edf-160">Specifies the target resource group, which is `maven-plugin` in this example.</span></span> <span data-ttu-id="86edf-161">Se creará este grupo de recursos durante la implementación si todavía no existe.</span><span class="sxs-lookup"><span data-stu-id="86edf-161">The resource group is created during deployment if it does not already exist.</span></span> |
| `<appName>` | <span data-ttu-id="86edf-162">Especifica el nombre de destino de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="86edf-162">Specifies the target name for your web app.</span></span> <span data-ttu-id="86edf-163">En este ejemplo, el nombre de destino es `maven-web-app-${maven.build.timestamp}`, donde el sufijo `${maven.build.timestamp}` se anexa en este ejemplo para evitar conflictos.</span><span class="sxs-lookup"><span data-stu-id="86edf-163">In this example, the target name is `maven-web-app-${maven.build.timestamp}`, where the `${maven.build.timestamp}` suffix is appended in this example to avoid conflict.</span></span> <span data-ttu-id="86edf-164">(La marca de tiempo es opcional; puede especificar cualquier cadena única para el nombre de la aplicación).</span><span class="sxs-lookup"><span data-stu-id="86edf-164">(The timestamp is optional; you can specify any unique string for the app name.)</span></span> |
| `<region>` | <span data-ttu-id="86edf-165">Especifica la región de destino, que en este ejemplo es `westus`.</span><span class="sxs-lookup"><span data-stu-id="86edf-165">Specifies the target region, which in this example is `westus`.</span></span> <span data-ttu-id="86edf-166">(Puede encontrar una lista completa en la documentación del [complemento Maven de Azure Web Apps]).</span><span class="sxs-lookup"><span data-stu-id="86edf-166">(A full list is in the [Maven Plugin for Azure Web Apps] documentation.)</span></span> |
| `<javaVersion>` | <span data-ttu-id="86edf-167">Especifica la versión de tiempo de ejecución de Java para la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="86edf-167">Specifies the Java runtime version for your web app.</span></span> <span data-ttu-id="86edf-168">(Puede encontrar una lista completa en la documentación del [complemento Maven de Azure Web Apps]).</span><span class="sxs-lookup"><span data-stu-id="86edf-168">(A full list is in the [Maven Plugin for Azure Web Apps] documentation.)</span></span> |
| `<deploymentType>` | <span data-ttu-id="86edf-169">Especifica el tipo de implementación para la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="86edf-169">Specifies deployment type for your web app.</span></span> <span data-ttu-id="86edf-170">El valor predeterminado es `war`.</span><span class="sxs-lookup"><span data-stu-id="86edf-170">Default is `war`.</span></span> |

## <a name="build-and-deploy-your-web-app-to-azure"></a><span data-ttu-id="86edf-171">Creación e implementación de una aplicación web en Azure</span><span class="sxs-lookup"><span data-stu-id="86edf-171">Build and deploy your web app to Azure</span></span>

<span data-ttu-id="86edf-172">Una vez que haya configurado todas las opciones en las secciones anteriores de este artículo, estará listo para implementar la aplicación web en Azure.</span><span class="sxs-lookup"><span data-stu-id="86edf-172">Once you have configured all of the settings in the preceding sections of this article, you are ready to deploy your web app to Azure.</span></span> <span data-ttu-id="86edf-173">Para ello, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="86edf-173">To do so, use the following steps:</span></span>

1. <span data-ttu-id="86edf-174">En el símbolo del sistema o la ventana de terminal que usó anteriormente, vuelva a compilar el archivo JAR con Maven si ha realizado algún cambio en el archivo *pom.xml*; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="86edf-174">From the command prompt or terminal window that you were using earlier, rebuild the JAR file using Maven if you made any changes to the *pom.xml* file; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="86edf-175">Implemente la aplicación web en Azure mediante Maven; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="86edf-175">Deploy your web app to Azure by using Maven; for example:</span></span>
   ```shell
   mvn azure-webapp:deploy
   ```

<span data-ttu-id="86edf-176">Maven implementará la aplicación web en Azure; si la aplicación web no existe, se creará.</span><span class="sxs-lookup"><span data-stu-id="86edf-176">Maven will deploy your web app to Azure; if the web app does not already exist, it will be created.</span></span>

<span data-ttu-id="86edf-177">Cuando se haya implementado la web, podrá administrarla mediante [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="86edf-177">When your web has been deployed, you will be able to manage it by using the [Azure portal].</span></span>

* <span data-ttu-id="86edf-178">La aplicación web aparecerá en **App Services**:</span><span class="sxs-lookup"><span data-stu-id="86edf-178">Your web app will be listed in **App Services**:</span></span>

   ![Aplicación web en la lista de App Services de Azure Portal][AP01]

* <span data-ttu-id="86edf-180">Y la dirección URL de la aplicación web se mostrará en la sección de **información general** de la aplicación web:</span><span class="sxs-lookup"><span data-stu-id="86edf-180">And the URL for your web app will be listed in the **Overview** for your web app:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="86edf-182">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="86edf-182">Next steps</span></span>

<span data-ttu-id="86edf-183">Para más información acerca de las diferentes tecnologías que se tratan en este artículo, consulte los artículos siguientes:</span><span class="sxs-lookup"><span data-stu-id="86edf-183">For more information about the various technologies discussed in this article, see the following articles:</span></span>

* <span data-ttu-id="86edf-184">[Complemento Maven de Azure Web Apps]</span><span class="sxs-lookup"><span data-stu-id="86edf-184">[Maven Plugin for Azure Web Apps]</span></span>

* [<span data-ttu-id="86edf-185">Inicio de sesión en Azure desde la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="86edf-185">Log in to Azure from the Azure CLI</span></span>](/azure/xplat-cli-connect)

* [<span data-ttu-id="86edf-186">Uso del complemento Maven de Azure Web Apps para implementar una aplicación de Spring Boot en contenedor en Azure</span><span class="sxs-lookup"><span data-stu-id="86edf-186">How to use the Maven Plugin for Azure Web Apps to deploy a containerized Spring Boot app to Azure</span></span>](deploy-containerized-spring-boot-java-app-with-maven-plugin.md)

* [<span data-ttu-id="86edf-187">Creación de una entidad de servicio de Azure con la CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="86edf-187">Create an Azure service principal with Azure CLI 2.0</span></span>](/cli/azure/create-an-azure-service-principal-azure-cli)

* [<span data-ttu-id="86edf-188">Referencia de configuración de Maven</span><span class="sxs-lookup"><span data-stu-id="86edf-188">Maven Settings Reference</span></span>](https://maven.apache.org/settings.html)

<!-- URL List -->

[Interfaz de la línea de comandos (CLI) de Azure]: /cli/azure/overview
[Azure Command-Line Interface (CLI)]: /cli/azure/overview
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Azure Portal]: https://portal.azure.com/
[Azure portal]: https://portal.azure.com/
[cuenta de Azure gratuita]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Primeros pasos de Spring Boot]: https://github.com/spring-guides/gs-spring-boot
[Spring Boot Getting Started]: https://github.com/spring-guides/gs-spring-boot
[Spring Framework]: https://spring.io/
[Complemento Maven de Azure Web Apps]: https://docs.microsoft.com/java/api/overview/azure/maven/azure-webapp-maven-plugin/readme
[Maven Plugin for Azure Web Apps]: https://docs.microsoft.com/java/api/overview/azure/maven/azure-webapp-maven-plugin/readme

<!-- IMG List -->

[AP01]: ./media/deploy-spring-boot-java-app-with-maven-plugin/AP01.png
[AP02]: ./media/deploy-spring-boot-java-app-with-maven-plugin/AP02.png
