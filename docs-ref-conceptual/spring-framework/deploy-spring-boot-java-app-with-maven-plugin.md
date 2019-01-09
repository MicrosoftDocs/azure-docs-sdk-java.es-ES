---
title: Implementación de una aplicación de archivo JAR de Spring Boot en la nube con Maven y Azure
description: Obtenga información acerca de cómo implementar una aplicación de Spring Boot en la nube con el complemento de Maven para Azure Web Apps para Linux.
services: app-service
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: brborges
ms.author: robmcm
ms.date: 12/19/2018
ms.devlang: java
ms.service: app-service
ms.topic: article
ms.openlocfilehash: 950b360eb525b0c6b97daad0798c27ded0582b8b
ms.sourcegitcommit: f0f140b0862ca5338b1b7e5c33cec3e58a70b8fd
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/03/2019
ms.locfileid: "53991349"
---
# <a name="deploy-a-spring-boot-jar-file-web-app-to-azure-app-service-on-linux"></a><span data-ttu-id="bb255-103">Implementación de una aplicación web de archivo JAR de Spring Boot en Azure App Service en Linux</span><span class="sxs-lookup"><span data-stu-id="bb255-103">Deploy a Spring Boot JAR file web app to Azure App Service on Linux</span></span>

<span data-ttu-id="bb255-104">En este artículo se muestra cómo usar el [complemento de Maven para Azure App Service Web Apps](/java/api/overview/azure/maven/azure-webapp-maven-plugin/readme) para implementar una aplicación de Spring Boot empaquetada como un archivo JAR de Java SE en [Azure App Service en Linux](/azure/app-service/containers/).</span><span class="sxs-lookup"><span data-stu-id="bb255-104">This article demonstrates using the [Maven Plugin for Azure App Service Web Apps](/java/api/overview/azure/maven/azure-webapp-maven-plugin/readme) to deploy a Spring Boot application packaged as a Java SE JAR to [Azure App Service on Linux](/azure/app-service/containers/).</span></span> <span data-ttu-id="bb255-105">Puede optar por la implementación de Java SE en lugar de [Tomcat y archivos WAR](/azure/app-service/containers/quickstart-java) cuando desee consolidar las dependencias, el entorno de ejecución y la configuración de la aplicación en un único artefacto implementable.</span><span class="sxs-lookup"><span data-stu-id="bb255-105">Choose Java SE deployment over [Tomcat and WAR files](/azure/app-service/containers/quickstart-java) when you want to consolidate your app's dependencies, runtime, and configuration into a single deployable artifact.</span></span>


<span data-ttu-id="bb255-106">Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de empezar.</span><span class="sxs-lookup"><span data-stu-id="bb255-106">If you don’t have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bb255-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="bb255-107">Prerequisites</span></span>

<span data-ttu-id="bb255-108">Para realizar los pasos de este tutorial, necesitará tener instalado y configurado lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="bb255-108">To complete the steps in this tutorial, you'll need to have the following installed and configured:</span></span>

* <span data-ttu-id="bb255-109">La [CLI de Azure](/cli/azure/), ya sea localmente o con [Azure Cloud Shell](https://shell.azure.com).</span><span class="sxs-lookup"><span data-stu-id="bb255-109">The [Azure CLI](/cli/azure/), either locally or through [Azure Cloud Shell](https://shell.azure.com).</span></span>
* <span data-ttu-id="bb255-110">Un kit de desarrollo de Java (JDK) admitido</span><span class="sxs-lookup"><span data-stu-id="bb255-110">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="bb255-111">Para más información sobre los JDK disponibles para desarrollar en Azure, consulte <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="bb255-111">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="bb255-112">[Maven](https://maven.apache.org/) de Apache, versión 3.</span><span class="sxs-lookup"><span data-stu-id="bb255-112">Apache's [Maven](https://maven.apache.org/), Version 3).</span></span>
* <span data-ttu-id="bb255-113">Un cliente [Git](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="bb255-113">A [Git](https://git-scm.com/downloads) client.</span></span>

## <a name="install-and-sign-in-to-azure-cli"></a><span data-ttu-id="bb255-114">Instalación e inicio de sesión en la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="bb255-114">Install and sign in to Azure CLI</span></span>

<span data-ttu-id="bb255-115">La manera más sencilla y fácil de obtener el complemento Maven para implementar la aplicación de Spring Boot es con la [CLI de Azure](/cli/azure/).</span><span class="sxs-lookup"><span data-stu-id="bb255-115">The simplest and easiest way to get the Maven Plugin deploying your Spring Boot application is by using [Azure CLI](/cli/azure/).</span></span>

<span data-ttu-id="bb255-116">Inicie sesión en la cuenta de Azure mediante la CLI de Azure:</span><span class="sxs-lookup"><span data-stu-id="bb255-116">Sign into your Azure account by using the Azure CLI:</span></span>
   
   ```shell
   az login
   ```
   
<span data-ttu-id="bb255-117">Siga las instrucciones para completar el proceso de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="bb255-117">Follow the instructions to complete the sign-in process.</span></span>

## <a name="clone-the-sample-app"></a><span data-ttu-id="bb255-118">Clonación de la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="bb255-118">Clone the sample app</span></span>

<span data-ttu-id="bb255-119">En esta sección, va a clonar una aplicación de Spring Boot terminada y a probarla de forma local.</span><span class="sxs-lookup"><span data-stu-id="bb255-119">In this section, you will clone a completed Spring Boot application and test it locally.</span></span>

1. <span data-ttu-id="bb255-120">Abra el símbolo del sistema o una ventana de terminal, cree un directorio local para alojar la aplicación de Spring Boot y cambie a dicho directorio, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="bb255-120">Open a command prompt or terminal window and create a local directory to hold your Spring Boot application, and change to that directory; for example:</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="bb255-121">-- o --</span><span class="sxs-lookup"><span data-stu-id="bb255-121">-- or --</span></span>
   ```shell
   md ~/SpringBoot
   cd ~/SpringBoot
   ```

1. <span data-ttu-id="bb255-122">Clone el proyecto de ejemplo [Primeros pasos de Spring Boot] en el directorio que creó, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="bb255-122">Clone the [Spring Boot Getting Started] sample project into the directory you created; for example:</span></span>
   ```shell
   git clone https://github.com/spring-guides/gs-spring-boot
   ```

1. <span data-ttu-id="bb255-123">Cambie de directorio al del proyecto finalizado, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="bb255-123">Change directory to the completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot/complete
   ```

1. <span data-ttu-id="bb255-124">Compile el archivo JAR con Maven, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="bb255-124">Build the JAR file using Maven; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="bb255-125">Cuándo se haya creado la aplicación web, iníciela con Maven. Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="bb255-125">When the web app has been created, start the web app using Maven; for example:</span></span>
   ```shell
   mvn spring-boot:run
   ```

1. <span data-ttu-id="bb255-126">Pruebe la aplicación web. Para ello, navegue a ella localmente mediante un explorador web.</span><span class="sxs-lookup"><span data-stu-id="bb255-126">Test the web app by browsing to it locally using a web browser.</span></span> <span data-ttu-id="bb255-127">Por ejemplo, puede utilizar el siguiente comando si dispone de curl:</span><span class="sxs-lookup"><span data-stu-id="bb255-127">For example, you could use the following command if you have curl available:</span></span>
   ```shell
   curl http://localhost:8080
   ```

1. <span data-ttu-id="bb255-128">Debería ver el mensaje siguiente mostrado: **Greetings from Spring Boot!**</span><span class="sxs-lookup"><span data-stu-id="bb255-128">You should see the following message displayed: **Greetings from Spring Boot!**</span></span>

## <a name="configure-maven-plugin-for-azure-app-service"></a><span data-ttu-id="bb255-129">Configuración del complemento de Maven para Azure App Service</span><span class="sxs-lookup"><span data-stu-id="bb255-129">Configure Maven Plugin for Azure App Service</span></span>

<span data-ttu-id="bb255-130">En esta sección, configurará el proyecto de Spring Boot `pom.xml` para que Maven pueda implementar la aplicación en Azure App Service en Linux.</span><span class="sxs-lookup"><span data-stu-id="bb255-130">In this section, you will configure the Spring Boot project `pom.xml` so that Maven can deploy the app to Azure App Service on Linux.</span></span>

1. <span data-ttu-id="bb255-131">Abra `pom.xml` en un editor de código.</span><span class="sxs-lookup"><span data-stu-id="bb255-131">Open `pom.xml` in a code editor.</span></span>

2. <span data-ttu-id="bb255-132">En la sección `<build>` del archivo pom.xml, agregue la siguiente entrada `<plugin>` dentro de la etiqueta `<plugins>`.</span><span class="sxs-lookup"><span data-stu-id="bb255-132">In the `<build>` section of the pom.xml, add the following `<plugin>` entry inside the `<plugins>` tag.</span></span>

   ```xml
   <plugin>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-webapp-maven-plugin</artifactId>
    <version>1.4.0</version>
    <configuration>
      <deploymentType>jar</deploymentType>

      <!-- configure app to run on port 80, required by App Service -->
      <appSettings>
        <property> 
          <name>JAVA_OPTS</name> 
          <value>-Dserver.port=80</value> 
        </property> 
      </appSettings>

      <!-- Web App information -->
      <resourceGroup>${RESOURCEGROUP_NAME}</resourceGroup>
      <appName>${WEBAPP_NAME}</appName>
      <region>${REGION}</region>  

      <!-- Java Runtime Stack for Web App on Linux-->
      <linuxRuntime>jre8</linuxRuntime>
    </configuration>
   </plugin>
   ```

3. <span data-ttu-id="bb255-133">Actualice los siguientes marcadores de posición en la configuración del complemento:</span><span class="sxs-lookup"><span data-stu-id="bb255-133">Update the following placeholders in the plugin configuration:</span></span>

| <span data-ttu-id="bb255-134">Marcador de posición</span><span class="sxs-lookup"><span data-stu-id="bb255-134">Placeholder</span></span> | <span data-ttu-id="bb255-135">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="bb255-135">Description</span></span> |
| ----------- | ----------- |
| `RESOURCEGROUP_NAME` | <span data-ttu-id="bb255-136">Nombre del nuevo grupo de recursos en el que se va a crear la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="bb255-136">Name for the new resource group in which to create your web app.</span></span> <span data-ttu-id="bb255-137">Al colocar todos los recursos de una aplicación en un grupo, puede administrarlos juntos.</span><span class="sxs-lookup"><span data-stu-id="bb255-137">By putting all the resources for an app in a group, you can manage them together.</span></span> <span data-ttu-id="bb255-138">Por ejemplo, si elimina el grupo de recursos también se eliminarán todos los recursos asociados con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="bb255-138">For example, deleting the resource group would delete all resources associated with the app.</span></span> <span data-ttu-id="bb255-139">Actualice este valor con un nombre único de un nuevo grupo de recursos, por ejemplo, *TestResources*.</span><span class="sxs-lookup"><span data-stu-id="bb255-139">Update this value with a unique new resource group name, for example, *TestResources*.</span></span> <span data-ttu-id="bb255-140">Este nombre lo utilizará para limpiar todos los recursos de Azure en una sección posterior.</span><span class="sxs-lookup"><span data-stu-id="bb255-140">You will use this resource group name to clean up all Azure resources in a later section.</span></span> |
| `WEBAPP_NAME` | <span data-ttu-id="bb255-141">El nombre de la aplicación forma parte del nombre de host de la aplicación web si se ha implementado en Azure (WEBAPP_NAME.azurewebsites.net).</span><span class="sxs-lookup"><span data-stu-id="bb255-141">The app name will be part the host name for the web app when deployed to Azure (WEBAPP_NAME.azurewebsites.net).</span></span> <span data-ttu-id="bb255-142">Actualice este valor con un nombre único para la nueva aplicación web de Azure, que hospedará la aplicación Java, por ejemplo *contoso*.</span><span class="sxs-lookup"><span data-stu-id="bb255-142">Update this value with a unique name for the new Azure web app, which will host your Java app, for example *contoso*.</span></span> |
| `REGION` | <span data-ttu-id="bb255-143">Una región de Azure donde se hospeda la aplicación web, por ejemplo `westus2`.</span><span class="sxs-lookup"><span data-stu-id="bb255-143">An Azure region where the web app is hosted, for example `westus2`.</span></span> <span data-ttu-id="bb255-144">Puede obtener una lista de regiones en Cloud Shell o la CLI mediante el comando `az account list-locations`.</span><span class="sxs-lookup"><span data-stu-id="bb255-144">You can get a list of regions from the Cloud Shell or CLI using the `az account list-locations` command.</span></span> |

<span data-ttu-id="bb255-145">Encontrará una lista completa de las opciones de configuración en la [Referencia del complemento de Maven en GitHub](https://github.com/Microsoft/azure-maven-plugins/tree/develop/azure-webapp-maven-plugin).</span><span class="sxs-lookup"><span data-stu-id="bb255-145">A full list of configuration options can be found in the [Maven plugin reference on GitHub](https://github.com/Microsoft/azure-maven-plugins/tree/develop/azure-webapp-maven-plugin).</span></span>

## <a name="deploy-the-app-to-azure"></a><span data-ttu-id="bb255-146">Implementación de la aplicación en Azure</span><span class="sxs-lookup"><span data-stu-id="bb255-146">Deploy the app to Azure</span></span>

<span data-ttu-id="bb255-147">Una vez que haya configurado todas las opciones en las secciones anteriores de este artículo, estará listo para implementar la aplicación web en Azure.</span><span class="sxs-lookup"><span data-stu-id="bb255-147">Once you have configured all of the settings in the preceding sections of this article, you are ready to deploy your web app to Azure.</span></span> <span data-ttu-id="bb255-148">Para ello, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="bb255-148">To do so, use the following steps:</span></span>

1. <span data-ttu-id="bb255-149">En el símbolo del sistema o la ventana de terminal que usó anteriormente, vuelva a compilar el archivo JAR con Maven si ha realizado algún cambio en el archivo *pom.xml*; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="bb255-149">From the command prompt or terminal window that you were using earlier, rebuild the JAR file using Maven if you made any changes to the *pom.xml* file; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="bb255-150">Implemente la aplicación web en Azure mediante Maven; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="bb255-150">Deploy your web app to Azure by using Maven; for example:</span></span>
   ```shell
   mvn azure-webapp:deploy
   ```

<span data-ttu-id="bb255-151">Maven implementará la aplicación web en Azure; si la aplicación web o el plan de la aplicación web no existen, se crearán.</span><span class="sxs-lookup"><span data-stu-id="bb255-151">Maven will deploy your web app to Azure; if the web app or web app plan does not already exist, it will be created for you.</span></span>

<span data-ttu-id="bb255-152">Cuando se haya implementado la web, podrá administrarla mediante [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="bb255-152">When your web has been deployed, you will be able to manage it through the [Azure portal].</span></span>

* <span data-ttu-id="bb255-153">La aplicación web aparecerá en **App Services**:</span><span class="sxs-lookup"><span data-stu-id="bb255-153">Your web app will be listed in **App Services**:</span></span>

   ![Aplicación web en la lista de App Services de Azure Portal][AP01]

* <span data-ttu-id="bb255-155">Y la dirección URL de la aplicación web se mostrará en la sección de **información general** de la aplicación web:</span><span class="sxs-lookup"><span data-stu-id="bb255-155">And the URL for your web app will be listed in the **Overview** for your web app:</span></span>

   ![Determinar la dirección URL de la aplicación web][AP02]

<span data-ttu-id="bb255-157">Compruebe que la implementación se realizó correctamente mediante el mismo comando de cURL utilizado antes, utilizando la dirección URL de la aplicación web del portal en lugar de `localhost`.</span><span class="sxs-lookup"><span data-stu-id="bb255-157">Verify that the deployment was successful by using the same cURL command as before, using your web app URL from the Portal instead of `localhost`.</span></span> <span data-ttu-id="bb255-158">Debería ver el mensaje siguiente mostrado: **Greetings from Spring Boot!**</span><span class="sxs-lookup"><span data-stu-id="bb255-158">You should see the following message displayed: **Greetings from Spring Boot!**</span></span> 

## <a name="next-steps"></a><span data-ttu-id="bb255-159">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bb255-159">Next steps</span></span>

<span data-ttu-id="bb255-160">Para más información acerca de Spring y Azure, vaya al centro de documentación de Azure.</span><span class="sxs-lookup"><span data-stu-id="bb255-160">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="bb255-161">Spring en Azure</span><span class="sxs-lookup"><span data-stu-id="bb255-161">Spring on Azure</span></span>](/java/azure/spring-framework)

### <a name="additional-resources"></a><span data-ttu-id="bb255-162">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="bb255-162">Additional Resources</span></span>

<span data-ttu-id="bb255-163">Para más información acerca de las diferentes tecnologías que se tratan en este artículo, consulte los artículos siguientes:</span><span class="sxs-lookup"><span data-stu-id="bb255-163">For more information about the various technologies discussed in this article, see the following articles:</span></span>

* <span data-ttu-id="bb255-164">[Complemento Maven de Azure Web Apps]</span><span class="sxs-lookup"><span data-stu-id="bb255-164">[Maven Plugin for Azure Web Apps]</span></span>

* [<span data-ttu-id="bb255-165">Uso del complemento Maven de Azure Web Apps para implementar una aplicación de Spring Boot en contenedor en Azure</span><span class="sxs-lookup"><span data-stu-id="bb255-165">How to use the Maven Plugin for Azure Web Apps to deploy a containerized Spring Boot app to Azure</span></span>](deploy-containerized-spring-boot-java-app-with-maven-plugin.md)

* [<span data-ttu-id="bb255-166">Creación de una entidad de servicio de Azure con la CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="bb255-166">Create an Azure service principal with Azure CLI 2.0</span></span>](/cli/azure/create-an-azure-service-principal-azure-cli)

* [<span data-ttu-id="bb255-167">Referencia de configuración de Maven</span><span class="sxs-lookup"><span data-stu-id="bb255-167">Maven Settings Reference</span></span>](https://maven.apache.org/settings.html)

<!-- URL List -->

[Azure Command-Line Interface (CLI)]: /cli/azure/overview
[Azure for Java Developers]: /java/azure/
[Azure Portal]: https://portal.azure.com/
[Azure portal]: https://portal.azure.com/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Working with Azure DevOps and Java]: /azure/devops/
[Maven]: http://maven.apache.org/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Primeros pasos de Spring Boot]: https://github.com/spring-guides/gs-spring-boot
[Spring Boot Getting Started]: https://github.com/spring-guides/gs-spring-boot
[Spring Framework]: https://spring.io/
[Complemento Maven de Azure Web Apps]: /java/api/overview/azure/maven/azure-webapp-maven-plugin/readme
[Maven Plugin for Azure Web Apps]: /java/api/overview/azure/maven/azure-webapp-maven-plugin/readme

[Java Development Kit (JDK)]: https://aka.ms/azure-jdks
<!-- http://www.oracle.com/technetwork/java/javase/downloads/ -->

<!-- IMG List -->

[AP01]: ./media/deploy-spring-boot-java-app-with-maven-plugin/AP01.png
[AP02]: ./media/deploy-spring-boot-java-app-with-maven-plugin/AP02.png
