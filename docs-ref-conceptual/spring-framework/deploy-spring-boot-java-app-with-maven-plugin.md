---
title: "Uso del complemento Maven de Azure Web Apps para implementar una aplicación de Spring Boot en Azure"
description: "Aprenda a usar el complemento Maven de Azure Web Apps para implementar una aplicación de Spring Boot en Azure."
services: app-service
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
keywords: Spring, Spring Boot, Spring Framework, Maven
ms.assetid: 
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: multiple
ms.devlang: java
ms.topic: article
ms.date: 10/11/2017
ms.author: robmcm;kevinzha
ms.openlocfilehash: 32781b3ee923f4d64d4e1a11df73f077281eee40
ms.sourcegitcommit: 7f8538e41c833deb69c300ad3431a431136a1f3e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/24/2017
---
# <a name="how-to-use-the-maven-plugin-for-azure-web-apps-to-deploy-a-spring-boot-app-to-azure"></a><span data-ttu-id="2c369-104">Uso del complemento Maven de Azure Web Apps para implementar una aplicación de Spring Boot en Azure</span><span class="sxs-lookup"><span data-stu-id="2c369-104">How to use the Maven Plugin for Azure Web Apps to deploy a Spring Boot app to Azure</span></span>

<span data-ttu-id="2c369-105">El [complemento Maven para Azure Web Apps](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) de [Apache Maven](http://maven.apache.org/) proporciona una perfecta integración de Azure App Service en proyectos de Maven y simplifica el proceso para que los desarrolladores implementen aplicaciones web en Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="2c369-105">The [Maven Plugin for Azure Web Apps](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) for [Apache Maven](http://maven.apache.org/) provides seamless integration of Azure App Service into Maven projects, and streamlines the process for developers to deploy web apps to Azure App Service.</span></span>

<span data-ttu-id="2c369-106">Este artículo muestra cómo utilizar el complemento Maven de Azure Web Apps para implementar una aplicación de Spring Boot de ejemplo en Azure App Services.</span><span class="sxs-lookup"><span data-stu-id="2c369-106">This article demonstrates using the Maven Plugin for Azure Web Apps to deploy a sample Spring Boot application to Azure App Services.</span></span>

> [!NOTE]
>
> <span data-ttu-id="2c369-107">El complemento Maven de Azure Web Apps está disponible actualmente como versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="2c369-107">The Maven Plugin for Azure Web Apps is currently available as a preview.</span></span> <span data-ttu-id="2c369-108">Por ahora, solo se admite la publicación FTP, aunque se van a agregar características adicionales en el futuro.</span><span class="sxs-lookup"><span data-stu-id="2c369-108">For now, only FTP publishing is supported, although additional features are planned for the future.</span></span>
>

## <a name="prerequisites"></a><span data-ttu-id="2c369-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="2c369-109">Prerequisites</span></span>

<span data-ttu-id="2c369-110">Para poder realizar los pasos de este tutorial, necesitará tener los siguientes requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="2c369-110">In order to complete the steps in this tutorial, you need to have the following prerequisites:</span></span>

* <span data-ttu-id="2c369-111">Una suscripción de Azure. Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN] o registrarse para obtener una [cuenta de Azure gratuita].</span><span class="sxs-lookup"><span data-stu-id="2c369-111">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="2c369-112">La [Interfaz de la línea de comandos (CLI) de Azure].</span><span class="sxs-lookup"><span data-stu-id="2c369-112">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="2c369-113">Un [kit de desarrollo de Java (JDK)] actualizado, versión 1.7 o posterior.</span><span class="sxs-lookup"><span data-stu-id="2c369-113">An up-to-date [Java Development Kit (JDK)], version 1.7 or later.</span></span>
* <span data-ttu-id="2c369-114">La herramienta de compilación [Maven] de Apache (versión 3).</span><span class="sxs-lookup"><span data-stu-id="2c369-114">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="2c369-115">Un cliente [Git].</span><span class="sxs-lookup"><span data-stu-id="2c369-115">A [Git] client.</span></span>

## <a name="clone-the-sample-spring-boot-web-app"></a><span data-ttu-id="2c369-116">Clonación de la aplicación web de Spring Boot de ejemplo</span><span class="sxs-lookup"><span data-stu-id="2c369-116">Clone the sample Spring Boot web app</span></span>

<span data-ttu-id="2c369-117">En esta sección, va a clonar una aplicación de Spring Boot terminada y a probarla de forma local.</span><span class="sxs-lookup"><span data-stu-id="2c369-117">In this section, you clone a completed Spring Boot application and test it locally.</span></span>

1. <span data-ttu-id="2c369-118">Abra el símbolo del sistema o una ventana de terminal y cree un directorio local para alojar la aplicación de Spring Boot, y cambie a dicho directorio, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2c369-118">Open a command prompt or terminal window and create a local directory to hold your Spring Boot application, and change to that directory; for example:</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="2c369-119">-- o --</span><span class="sxs-lookup"><span data-stu-id="2c369-119">-- or --</span></span>
   ```shell
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="2c369-120">Clone el proyecto de ejemplo [inicial de Spring Boot] en el directorio que creó, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2c369-120">Clone the [Spring Boot Getting Started] sample project into the directory you created; for example:</span></span>
   ```shell
   git clone https://github.com/microsoft/gs-spring-boot
   ```

1. <span data-ttu-id="2c369-121">Cambie de directorio al del proyecto finalizado, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2c369-121">Change directory to the completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot/complete
   ```

1. <span data-ttu-id="2c369-122">Compile el archivo JAR con Maven, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2c369-122">Build the JAR file using Maven; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="2c369-123">Cuándo se haya creado la aplicación web, iníciela con Maven. Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2c369-123">When the web app has been created, start the web app using Maven; for example:</span></span>
   ```shell
   mvn spring-boot:run
   ```

1. <span data-ttu-id="2c369-124">Pruebe la aplicación web. Para ello, navegue a ella localmente mediante un explorador web.</span><span class="sxs-lookup"><span data-stu-id="2c369-124">Test the web app by browsing to it locally using a web browser.</span></span> <span data-ttu-id="2c369-125">Por ejemplo, puede utilizar el siguiente comando si dispone de curl:</span><span class="sxs-lookup"><span data-stu-id="2c369-125">For example, you could use the following command if you have curl available:</span></span>
   ```shell
   curl http://localhost:8080
   ```

1. <span data-ttu-id="2c369-126">Debería aparecer el siguiente mensaje: **Greetings from Spring Boot!** (Saludos de Spring Boot).</span><span class="sxs-lookup"><span data-stu-id="2c369-126">You should see the following message displayed: **Greetings from Spring Boot!**</span></span>

## <a name="create-an-azure-service-principal"></a><span data-ttu-id="2c369-127">Creación de una entidad de servicio de Azure</span><span class="sxs-lookup"><span data-stu-id="2c369-127">Create an Azure service principal</span></span>

<span data-ttu-id="2c369-128">En esta sección, va a crear una entidad de servicio de Azure que usa el complemento Maven cuando implementa la aplicación web en Azure.</span><span class="sxs-lookup"><span data-stu-id="2c369-128">In this section, you create an Azure service principal that the Maven plugin uses when deploying your web app to Azure.</span></span>

1. <span data-ttu-id="2c369-129">Abra el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="2c369-129">Open a command prompt.</span></span>

1. <span data-ttu-id="2c369-130">Inicie sesión en la cuenta de Azure mediante la CLI de Azure:</span><span class="sxs-lookup"><span data-stu-id="2c369-130">Sign into your Azure account by using the Azure CLI:</span></span>
   ```shell
   az login
   ```
   <span data-ttu-id="2c369-131">Siga las instrucciones para completar el proceso de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="2c369-131">Follow the instructions to complete the sign-in process.</span></span>

1. <span data-ttu-id="2c369-132">Cree una entidad de servicio de Azure:</span><span class="sxs-lookup"><span data-stu-id="2c369-132">Create an Azure service principal:</span></span>
   ```shell
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   <span data-ttu-id="2c369-133">Donde `uuuuuuuu` es el nombre de usuario y `pppppppp` es la contraseña de la entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="2c369-133">Where `uuuuuuuu` is the user name and `pppppppp` is the password for the service principal.</span></span>

1. <span data-ttu-id="2c369-134">Azure responde con un archivo JSON que es similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="2c369-134">Azure responds with JSON that resembles the following example:</span></span>
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
   > <span data-ttu-id="2c369-135">Utilizará los valores de esta respuesta JSON al configurar el complemento para implementar la aplicación web en Azure.</span><span class="sxs-lookup"><span data-stu-id="2c369-135">You will use the values from this JSON response when you configure the Maven plugin to deploy your web app to Azure.</span></span> <span data-ttu-id="2c369-136">El `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, y `tttttttt` son valores de marcador de posición que se usan en este ejemplo para que sea más fácil asignar estos valores a sus respectivos elementos al configurar el archivo `settings.xml` de Maven en la sección siguiente.</span><span class="sxs-lookup"><span data-stu-id="2c369-136">The `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, and `tttttttt` are placeholder values, which are used in this example to make it easier to map these values to their respective elements when you configure your Maven `settings.xml` file in the next section.</span></span>
   >
   >

## <a name="configure-maven-to-use-your-azure-service-principal"></a><span data-ttu-id="2c369-137">Configurar Maven para usar la entidad de servicio de Azure</span><span class="sxs-lookup"><span data-stu-id="2c369-137">Configure Maven to use your Azure service principal</span></span>

<span data-ttu-id="2c369-138">En esta sección, utilice los valores de la entidad de servicio de Azure para configurar la autenticación que va a usar Maven al implementar la aplicación web en Azure.</span><span class="sxs-lookup"><span data-stu-id="2c369-138">In this section, you use the values from your Azure service principal to configure the authentication that Maven uses when deploying your web app to Azure.</span></span>

1. <span data-ttu-id="2c369-139">Abra el archivo `settings.xml` de Maven en un editor de texto; este archivo puede encontrarse en una ruta de acceso como la de los ejemplos siguientes:</span><span class="sxs-lookup"><span data-stu-id="2c369-139">Open your Maven `settings.xml` file in a text editor; this file might be in a path like the following examples:</span></span>
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. <span data-ttu-id="2c369-140">Agregue la configuración de la entidad de servicio de la sección anterior de este tutorial a la colección `<servers>` en el archivo *settings.xml*, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2c369-140">Add your Azure service principal settings from the previous section of this tutorial to the `<servers>` collection in the *settings.xml* file; for example:</span></span>

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
   <span data-ttu-id="2c369-141">Donde:</span><span class="sxs-lookup"><span data-stu-id="2c369-141">Where:</span></span>
   <span data-ttu-id="2c369-142">Elemento</span><span class="sxs-lookup"><span data-stu-id="2c369-142">Element</span></span> | <span data-ttu-id="2c369-143">Descripción</span><span class="sxs-lookup"><span data-stu-id="2c369-143">Description</span></span>
   ---|---|---
   `<id>` | <span data-ttu-id="2c369-144">Especifica un nombre único que Maven utiliza para buscar la configuración de seguridad al implementar la aplicación web en Azure.</span><span class="sxs-lookup"><span data-stu-id="2c369-144">Specifies a unique name which Maven uses to look up your security settings when you deploy your web app to Azure.</span></span>
   `<client>` | <span data-ttu-id="2c369-145">Contiene el valor `appId` de la entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="2c369-145">Contains the `appId` value from your service principal.</span></span>
   `<tenant>` | <span data-ttu-id="2c369-146">Contiene el valor `tenant` de la entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="2c369-146">Contains the `tenant` value from your service principal.</span></span>
   `<key>` | <span data-ttu-id="2c369-147">Contiene el valor `password` de la entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="2c369-147">Contains the `password` value from your service principal.</span></span>
   `<environment>` | <span data-ttu-id="2c369-148">Define el entorno en la nube de Azure de destino, que es `AZURE` en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="2c369-148">Defines the target Azure cloud environment, which is `AZURE` in this example.</span></span> <span data-ttu-id="2c369-149">(Una lista completa de los entornos está disponible en la documentación del [complemento Maven de Azure Web Apps])</span><span class="sxs-lookup"><span data-stu-id="2c369-149">(A full list of environments is available in the [Maven Plugin for Azure Web Apps] documentation)</span></span>

1. <span data-ttu-id="2c369-150">Guarde y cierre el archivo *settings.xml*.</span><span class="sxs-lookup"><span data-stu-id="2c369-150">Save and close the *settings.xml* file.</span></span>

## <a name="optional-customize-your-pomxml-before-deploying-your-web-app-to-azure"></a><span data-ttu-id="2c369-151">OPCIONAL: Personalice el archivo pom.xml antes de implementar la aplicación web en Azure</span><span class="sxs-lookup"><span data-stu-id="2c369-151">OPTIONAL: Customize your pom.xml before deploying your web app to Azure</span></span>

<span data-ttu-id="2c369-152">Abra el archivo `pom.xml` de la aplicación de Spring Boot en un editor de texto y, a continuación, busque el elemento `<plugin>` de `azure-webapp-maven-plugin`.</span><span class="sxs-lookup"><span data-stu-id="2c369-152">Open the `pom.xml` file for your Spring Boot application in a text editor, and then locate the `<plugin>` element for `azure-webapp-maven-plugin`.</span></span> <span data-ttu-id="2c369-153">Este elemento debe tener un aspecto similar al ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="2c369-153">This element should resemble the following example:</span></span>

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
         <appName>maven-web-app-${maven.build.timestamp}</appName>
         <region>westus</region>
         <javaVersion>1.8</javaVersion>
         <deploymentType>ftp</deploymentType>
         <resources>
            <resource>
               <directory>${project.basedir}/target</directory>
               <targetPath>/</targetPath>
               <includes>
                  <include>*.jar</include>
               </includes>
            </resource>
            <resource>
               <directory>${project.basedir}</directory>
               <targetPath>/</targetPath>
               <includes>
                  <include>web.config</include>
               </includes>
            </resource>
         </resources>
      </configuration>
   </plugin>
   ```

<span data-ttu-id="2c369-154">Hay varios valores que se pueden modificar en el complemento Maven y hay una descripción detallada de cada uno de estos elementos disponible en la documentación del [complemento Maven de Azure Web Apps].</span><span class="sxs-lookup"><span data-stu-id="2c369-154">There are several values that you can modify for the Maven plugin, and a detailed description for each of these elements is available in the [Maven Plugin for Azure Web Apps] documentation.</span></span> <span data-ttu-id="2c369-155">Dicho esto, hay varios valores que merece la pena destacar en este artículo:</span><span class="sxs-lookup"><span data-stu-id="2c369-155">That being said, there are several values that are worth highlighting in this article:</span></span>

<span data-ttu-id="2c369-156">Elemento</span><span class="sxs-lookup"><span data-stu-id="2c369-156">Element</span></span> | <span data-ttu-id="2c369-157">Descripción</span><span class="sxs-lookup"><span data-stu-id="2c369-157">Description</span></span>
---|---|---
`<version>` | <span data-ttu-id="2c369-158">Especifica la versión del [complemento Maven de Azure Web Apps].</span><span class="sxs-lookup"><span data-stu-id="2c369-158">Specifies the version of the [Maven Plugin for Azure Web Apps].</span></span> <span data-ttu-id="2c369-159">Debe comprobar la versión que aparece en el [repositorio central de Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) para asegurarse de que está utilizando la versión más reciente.</span><span class="sxs-lookup"><span data-stu-id="2c369-159">You should check the version listed in the [Maven Central Respository](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) to ensure that you are using the latest version.</span></span>
`<authentication>` | <span data-ttu-id="2c369-160">Especifica la información de autenticación de Azure que, en este ejemplo, contiene un elemento `<serverId>` que contiene `azure-auth`; Maven utiliza ese valor para buscar los valores de la entidad de servicio de Azure en el archivo *settings.xml* que se definió en una sección anterior de este artículo.</span><span class="sxs-lookup"><span data-stu-id="2c369-160">Specifies the authentication information for Azure, which in this example contains a `<serverId>` element that contains `azure-auth`; Maven uses that value to look up the Azure service principal values in your Maven *settings.xml* file, which you defined in an earlier section of this article.</span></span>
`<resourceGroup>` | <span data-ttu-id="2c369-161">Especifica el grupo de recursos de destino, que es `maven-plugin` en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="2c369-161">Specifies the target resource group, which is `maven-plugin` in this example.</span></span> <span data-ttu-id="2c369-162">Se creará este grupo de recursos durante la implementación si todavía no existe.</span><span class="sxs-lookup"><span data-stu-id="2c369-162">The resource group is created during deployment if it does not already exist.</span></span>
`<appName>` | <span data-ttu-id="2c369-163">Especifica el nombre de destino de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="2c369-163">Specifies the target name for your web app.</span></span> <span data-ttu-id="2c369-164">En este ejemplo, el nombre de destino es `maven-web-app-${maven.build.timestamp}`, donde el sufijo `${maven.build.timestamp}` se anexa en este ejemplo para evitar conflictos.</span><span class="sxs-lookup"><span data-stu-id="2c369-164">In this example, the target name is `maven-web-app-${maven.build.timestamp}`, where the `${maven.build.timestamp}` suffix is appended in this example to avoid conflict.</span></span> <span data-ttu-id="2c369-165">(La marca de tiempo es opcional; puede especificar cualquier cadena única para el nombre de la aplicación).</span><span class="sxs-lookup"><span data-stu-id="2c369-165">(The timestamp is optional; you can specify any unique string for the app name.)</span></span>
`<region>` | <span data-ttu-id="2c369-166">Especifica la región de destino, que en este ejemplo es `westus`.</span><span class="sxs-lookup"><span data-stu-id="2c369-166">Specifies the target region, which in this example is `westus`.</span></span> <span data-ttu-id="2c369-167">(Puede encontrar una lista completa en la documentación del [complemento Maven de Azure Web Apps]).</span><span class="sxs-lookup"><span data-stu-id="2c369-167">(A full list is in the [Maven Plugin for Azure Web Apps] documentation.)</span></span>
`<javaVersion>` | <span data-ttu-id="2c369-168">Especifica la versión de tiempo de ejecución de Java para la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="2c369-168">Specifies the Java runtime version for your web app.</span></span> <span data-ttu-id="2c369-169">(Puede encontrar una lista completa en la documentación del [complemento Maven de Azure Web Apps]).</span><span class="sxs-lookup"><span data-stu-id="2c369-169">(A full list is in the [Maven Plugin for Azure Web Apps] documentation.)</span></span>
`<deploymentType>` | <span data-ttu-id="2c369-170">Especifica el tipo de implementación para la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="2c369-170">Specifies deployment type for your web app.</span></span> <span data-ttu-id="2c369-171">Por ahora, solo se admite `ftp`, aunque la compatibilidad con otros tipos de implementación está en la fase de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="2c369-171">For now, only `ftp` is supported, although support for other deployment types is in development.</span></span>
`<resources>` | <span data-ttu-id="2c369-172">Especifica los recursos y destinos que Maven usa al implementar la aplicación web en Azure.</span><span class="sxs-lookup"><span data-stu-id="2c369-172">Specifies resources and target destinations which Maven uses when deploying your web app to Azure.</span></span> <span data-ttu-id="2c369-173">En este ejemplo, dos elementos `<resource>` especifican que Maven implementará el archivo JAR de la aplicación web y el archivo *web.config* desde el proyecto de Spring Boot.</span><span class="sxs-lookup"><span data-stu-id="2c369-173">In this example, two `<resource>` elements specify that Maven will deploy the JAR file for your web app and the *web.config* file from the Spring Boot project.</span></span>

## <a name="build-and-deploy-your-web-app-to-azure"></a><span data-ttu-id="2c369-174">Creación e implementación de una aplicación web en Azure</span><span class="sxs-lookup"><span data-stu-id="2c369-174">Build and deploy your web app to Azure</span></span>

<span data-ttu-id="2c369-175">Una vez haya configurado todas las opciones en las secciones anteriores de este artículo, está listo para implementar la aplicación web en Azure.</span><span class="sxs-lookup"><span data-stu-id="2c369-175">Once you have configured all of the settings in the preceding sections of this article, you are ready to deploy your web app to Azure.</span></span> <span data-ttu-id="2c369-176">Para ello, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="2c369-176">To do so, use the following steps:</span></span>

1. <span data-ttu-id="2c369-177">En el símbolo del sistema o la ventana de terminal que usó anteriormente, vuelva a compilar el archivo JAR con Maven si ha realizado algún cambio en el archivo *pom.xml*; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2c369-177">From the command prompt or terminal window that you were using earlier, rebuild the JAR file using Maven if you made any changes to the *pom.xml* file; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="2c369-178">Implemente la aplicación web en Azure mediante Maven; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2c369-178">Deploy your web app to Azure by using Maven; for example:</span></span>
   ```shell
   mvn azure-webapp:deploy
   ```

<span data-ttu-id="2c369-179">Maven implementará la aplicación web en Azure; si la aplicación web no existe, se creará.</span><span class="sxs-lookup"><span data-stu-id="2c369-179">Maven will deploy your web app to Azure; if the web app does not already exist, it will be created.</span></span>

<span data-ttu-id="2c369-180">Cuando se haya implementado la web, podrá administrarla mediante [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="2c369-180">When your web has been deployed, you will be able to manage it by using the [Azure portal].</span></span>

* <span data-ttu-id="2c369-181">La aplicación web aparecerá en **App Services**:</span><span class="sxs-lookup"><span data-stu-id="2c369-181">Your web app will be listed in **App Services**:</span></span>

   ![Aplicación web en la lista de App Services de Azure Portal][AP01]

* <span data-ttu-id="2c369-183">Y la dirección URL de la aplicación web se mostrará en la sección de **información general** de la aplicación web:</span><span class="sxs-lookup"><span data-stu-id="2c369-183">And the URL for your web app will be listed in the **Overview** for your web app:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="2c369-185">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2c369-185">Next steps</span></span>

<span data-ttu-id="2c369-186">Para más información acerca de las diferentes tecnologías que se tratan en este artículo, consulte los artículos siguientes:</span><span class="sxs-lookup"><span data-stu-id="2c369-186">For more information about the various technologies discussed in this article, see the following articles:</span></span>

* <span data-ttu-id="2c369-187">[complemento Maven de Azure Web Apps]</span><span class="sxs-lookup"><span data-stu-id="2c369-187">[Maven Plugin for Azure Web Apps]</span></span>

* [<span data-ttu-id="2c369-188">Inicio de sesión en Azure desde la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="2c369-188">Log in to Azure from the Azure CLI</span></span>](/azure/xplat-cli-connect)

* [<span data-ttu-id="2c369-189">Uso del complemento Maven de Azure Web Apps para implementar una aplicación de Spring Boot en contenedor en Azure</span><span class="sxs-lookup"><span data-stu-id="2c369-189">How to use the Maven Plugin for Azure Web Apps to deploy a containerized Spring Boot app to Azure</span></span>](deploy-containerized-spring-boot-java-app-with-maven-plugin.md)

* [<span data-ttu-id="2c369-190">Creación de una entidad de servicio de Azure con la CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="2c369-190">Create an Azure service principal with Azure CLI 2.0</span></span>](/cli/azure/create-an-azure-service-principal-azure-cli)

* [<span data-ttu-id="2c369-191">Referencia de configuración de Maven</span><span class="sxs-lookup"><span data-stu-id="2c369-191">Maven Settings Reference</span></span>](https://maven.apache.org/settings.html)

<!-- URL List -->

[Interfaz de la línea de comandos (CLI) de Azure]: /cli/azure/overview
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[Azure Portal]: https://portal.azure.com/
[cuenta de Azure gratuita]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[ventajas como suscriptor de MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[inicial de Spring Boot]: https://github.com/microsoft/gs-spring-boot
[Spring Framework]: https://spring.io/
[complemento Maven de Azure Web Apps]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin

<!-- IMG List -->

[AP01]: ./media/deploy-spring-boot-java-app-with-maven-plugin/AP01.png
[AP02]: ./media/deploy-spring-boot-java-app-with-maven-plugin/AP02.png
