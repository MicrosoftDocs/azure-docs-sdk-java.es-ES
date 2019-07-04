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
ms.openlocfilehash: b133290d1f14429cbf36d6ed5a67d27e1a637593
ms.sourcegitcommit: 599405a9ce892d75073ef0776befa2fa22407b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2019
ms.locfileid: "67237597"
---
# <a name="deploy-a-spring-boot-jar-file-web-app-to-azure-app-service-on-linux"></a><span data-ttu-id="cd5ff-103">Implementación de una aplicación web de archivo JAR de Spring Boot en Azure App Service en Linux</span><span class="sxs-lookup"><span data-stu-id="cd5ff-103">Deploy a Spring Boot JAR file web app to Azure App Service on Linux</span></span>

<span data-ttu-id="cd5ff-104">En este artículo se muestra cómo usar el [complemento de Maven para Azure App Service Web Apps](/java/api/overview/azure/maven/azure-webapp-maven-plugin/readme) para implementar una aplicación de Spring Boot empaquetada como un archivo JAR de Java SE en [Azure App Service en Linux](/azure/app-service/containers/).</span><span class="sxs-lookup"><span data-stu-id="cd5ff-104">This article demonstrates using the [Maven Plugin for Azure App Service Web Apps](/java/api/overview/azure/maven/azure-webapp-maven-plugin/readme) to deploy a Spring Boot application packaged as a Java SE JAR to [Azure App Service on Linux](/azure/app-service/containers/).</span></span> <span data-ttu-id="cd5ff-105">Puede optar por la implementación de Java SE en lugar de [Tomcat y archivos WAR](/azure/app-service/containers/quickstart-java) cuando desee consolidar las dependencias, el entorno de ejecución y la configuración de la aplicación en un único artefacto implementable.</span><span class="sxs-lookup"><span data-stu-id="cd5ff-105">Choose Java SE deployment over [Tomcat and WAR files](/azure/app-service/containers/quickstart-java) when you want to consolidate your app's dependencies, runtime, and configuration into a single deployable artifact.</span></span>


<span data-ttu-id="cd5ff-106">Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de empezar.</span><span class="sxs-lookup"><span data-stu-id="cd5ff-106">If you don’t have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cd5ff-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="cd5ff-107">Prerequisites</span></span>

<span data-ttu-id="cd5ff-108">Para realizar los pasos de este tutorial, necesitará tener instalado y configurado lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="cd5ff-108">To complete the steps in this tutorial, you'll need to have the following installed and configured:</span></span>

* <span data-ttu-id="cd5ff-109">La [CLI de Azure](/cli/azure/), ya sea localmente o con [Azure Cloud Shell](https://shell.azure.com).</span><span class="sxs-lookup"><span data-stu-id="cd5ff-109">The [Azure CLI](/cli/azure/), either locally or through [Azure Cloud Shell](https://shell.azure.com).</span></span>
* <span data-ttu-id="cd5ff-110">Un kit de desarrollo de Java (JDK) admitido</span><span class="sxs-lookup"><span data-stu-id="cd5ff-110">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="cd5ff-111">Para más información sobre los JDK disponibles para desarrollar en Azure, consulte <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="cd5ff-111">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="cd5ff-112">[Maven](https://maven.apache.org/) de Apache, versión 3.</span><span class="sxs-lookup"><span data-stu-id="cd5ff-112">Apache's [Maven](https://maven.apache.org/), Version 3).</span></span>
* <span data-ttu-id="cd5ff-113">Un cliente [Git](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="cd5ff-113">A [Git](https://git-scm.com/downloads) client.</span></span>

## <a name="install-and-sign-in-to-azure-cli"></a><span data-ttu-id="cd5ff-114">Instalación e inicio de sesión en la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="cd5ff-114">Install and sign in to Azure CLI</span></span>

<span data-ttu-id="cd5ff-115">La manera más sencilla y fácil de obtener el complemento Maven para implementar la aplicación de Spring Boot es con la [CLI de Azure](/cli/azure/).</span><span class="sxs-lookup"><span data-stu-id="cd5ff-115">The simplest and easiest way to get the Maven Plugin deploying your Spring Boot application is by using [Azure CLI](/cli/azure/).</span></span>

<span data-ttu-id="cd5ff-116">Inicie sesión en la cuenta de Azure mediante la CLI de Azure:</span><span class="sxs-lookup"><span data-stu-id="cd5ff-116">Sign into your Azure account by using the Azure CLI:</span></span>
   
   ```shell
   az login
   ```
   
<span data-ttu-id="cd5ff-117">Siga las instrucciones para completar el proceso de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="cd5ff-117">Follow the instructions to complete the sign-in process.</span></span>

## <a name="clone-the-sample-app"></a><span data-ttu-id="cd5ff-118">Clonación de la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="cd5ff-118">Clone the sample app</span></span>

<span data-ttu-id="cd5ff-119">En esta sección, va a clonar una aplicación de Spring Boot terminada y a probarla de forma local.</span><span class="sxs-lookup"><span data-stu-id="cd5ff-119">In this section, you will clone a completed Spring Boot application and test it locally.</span></span>

1. <span data-ttu-id="cd5ff-120">Abra el símbolo del sistema o una ventana de terminal, cree un directorio local para alojar la aplicación de Spring Boot y cambie a dicho directorio, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="cd5ff-120">Open a command prompt or terminal window and create a local directory to hold your Spring Boot application, and change to that directory; for example:</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="cd5ff-121">-- o --</span><span class="sxs-lookup"><span data-stu-id="cd5ff-121">-- or --</span></span>
   ```shell
   md ~/SpringBoot
   cd ~/SpringBoot
   ```

1. <span data-ttu-id="cd5ff-122">Clone el proyecto de ejemplo [Primeros pasos de Spring Boot] en el directorio que creó, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="cd5ff-122">Clone the [Spring Boot Getting Started] sample project into the directory you created; for example:</span></span>
   ```shell
   git clone https://github.com/spring-guides/gs-spring-boot
   ```

1. <span data-ttu-id="cd5ff-123">Cambie de directorio al del proyecto finalizado, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="cd5ff-123">Change directory to the completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot/complete
   ```

1. <span data-ttu-id="cd5ff-124">Compile el archivo JAR con Maven, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="cd5ff-124">Build the JAR file using Maven; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="cd5ff-125">Cuándo se haya creado la aplicación web, iníciela con Maven. Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="cd5ff-125">When the web app has been created, start the web app using Maven; for example:</span></span>
   ```shell
   mvn spring-boot:run
   ```

1. <span data-ttu-id="cd5ff-126">Pruebe la aplicación web. Para ello, navegue a ella localmente mediante un explorador web.</span><span class="sxs-lookup"><span data-stu-id="cd5ff-126">Test the web app by browsing to it locally using a web browser.</span></span> <span data-ttu-id="cd5ff-127">Por ejemplo, puede utilizar el siguiente comando si dispone de curl:</span><span class="sxs-lookup"><span data-stu-id="cd5ff-127">For example, you could use the following command if you have curl available:</span></span>
   ```shell
   curl http://localhost:8080
   ```

1. <span data-ttu-id="cd5ff-128">Debería ver el mensaje siguiente mostrado: **Greetings from Spring Boot!**</span><span class="sxs-lookup"><span data-stu-id="cd5ff-128">You should see the following message displayed: **Greetings from Spring Boot!**</span></span>

## <a name="configure-maven-plugin-for-azure-app-service"></a><span data-ttu-id="cd5ff-129">Configuración del complemento de Maven para Azure App Service</span><span class="sxs-lookup"><span data-stu-id="cd5ff-129">Configure Maven Plugin for Azure App Service</span></span>

<span data-ttu-id="cd5ff-130">En esta sección, configurará el proyecto de Spring Boot `pom.xml` para que Maven pueda implementar la aplicación en Azure App Service en Linux.</span><span class="sxs-lookup"><span data-stu-id="cd5ff-130">In this section, you will configure the Spring Boot project `pom.xml` so that Maven can deploy the app to Azure App Service on Linux.</span></span>

1. <span data-ttu-id="cd5ff-131">Abra `pom.xml` en un editor de código.</span><span class="sxs-lookup"><span data-stu-id="cd5ff-131">Open `pom.xml` in a code editor.</span></span>

2. <span data-ttu-id="cd5ff-132">En la sección `<build>` del archivo pom.xml, agregue la siguiente entrada `<plugin>` dentro de la etiqueta `<plugins>`.</span><span class="sxs-lookup"><span data-stu-id="cd5ff-132">In the `<build>` section of the pom.xml, add the following `<plugin>` entry inside the `<plugins>` tag.</span></span>

   ```xml
   <plugin>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-webapp-maven-plugin</artifactId>
    <version>1.6.0</version>
   </plugin>
   ```

3. <span data-ttu-id="cd5ff-133">Después, puede configurar la implementación, ejecutar el comando `mvn azure-webapp:config` de Maven en el símbolo del sistema y usar el **número** para elegir estas opciones en el símbolo del sistema:</span><span class="sxs-lookup"><span data-stu-id="cd5ff-133">Then you can configure the deployment, run the maven command `mvn azure-webapp:config` in the Command Prompt and use the **number** to choose these options in the prompt:</span></span>
    * <span data-ttu-id="cd5ff-134">**OS**: linux</span><span class="sxs-lookup"><span data-stu-id="cd5ff-134">**OS**: linux</span></span>  
    * <span data-ttu-id="cd5ff-135">**javaVersion**: jre8</span><span class="sxs-lookup"><span data-stu-id="cd5ff-135">**javaVersion**: jre8</span></span>
    * <span data-ttu-id="cd5ff-136">**runtimeStack**: jre8</span><span class="sxs-lookup"><span data-stu-id="cd5ff-136">**runtimeStack**: jre8</span></span>

<span data-ttu-id="cd5ff-137">Cuando llegue al mensaje **Confirm (Y/N)** [Confirmar (S/N)], presione **y** y la configuración se realiza.</span><span class="sxs-lookup"><span data-stu-id="cd5ff-137">When you get the **Confirm (Y/N)** prompt, press **'y'** and the configuration is done.</span></span>

```cmd
~@Azure:~/gs-spring-boot/complete$ mvn azure-webapp:config
[INFO] Scanning for projects...
[INFO]
[INFO] -----------------< org.springframework:gs-spring-boot >-----------------
[INFO] Building gs-spring-boot 0.1.0
[INFO] --------------------------------[ jar ]---------------------------------
[INFO]
[INFO] --- azure-webapp-maven-plugin:1.6.0:config (default-cli) @ gs-spring-boot ---
[WARNING] The plugin may not work if you change the os of an existing webapp.
Define value for OS(Default: Linux):
1. linux [*]
2. windows
3. docker
Enter index to use:
Define value for javaVersion(Default: jre8):
1. jre8 [*]
2. java11
Enter index to use:
Define value for runtimeStack(Default: TOMCAT 8.5):
1. TOMCAT 9.0
2. jre8
3. TOMCAT 8.5 [*]
4. WILDFLY 14
Enter index to use: 2
Please confirm webapp properties
AppName : gs-spring-boot-1559091271202
ResourceGroup : gs-spring-boot-1559091271202-rg
Region : westeurope
PricingTier : Premium_P1V2
OS : Linux
RuntimeStack : JAVA 8-jre8
Deploy to slot : false
Confirm (Y/N)? : Y
```

4. <span data-ttu-id="cd5ff-138">Agregue la sección `<appSettings>` a la sección `<configuration>` de `<azure-webapp-maven-plugin>` para escuchar en el puerto *80*.</span><span class="sxs-lookup"><span data-stu-id="cd5ff-138">Add the `<appSettings>` section to the `<configuration>` section of `<azure-webapp-maven-plugin>` to listen on the *80* port.</span></span>

    ```xml
   <plugin>
       <groupId>com.microsoft.azure</groupId>
       <artifactId>azure-webapp-maven-plugin</artifactId>
       <version>1.6.0</version>
       <configuration>
          <schemaVersion>V2</schemaVersion>
          <resourceGroup>gs-spring-boot-1559091271202-rg</resourceGroup>
          <appName>gs-spring-boot-1559091271202</appName>
          <region>westeurope</region>
          <pricingTier>P1V2</pricingTier>

          <!-- Begin of App Settings  -->
          <appSettings>
             <property>
                   <name>JAVA_OPTS</name>
                   <value>-Dserver.port=80</value>
             </property>
          </appSettings>
          <!-- End of App Settings  -->
          ...
         </configuration>
   </plugin>
   ```

## <a name="deploy-the-app-to-azure"></a><span data-ttu-id="cd5ff-139">Implementación de la aplicación en Azure</span><span class="sxs-lookup"><span data-stu-id="cd5ff-139">Deploy the app to Azure</span></span>

<span data-ttu-id="cd5ff-140">Una vez que haya configurado todas las opciones en las secciones anteriores de este artículo, estará listo para implementar la aplicación web en Azure.</span><span class="sxs-lookup"><span data-stu-id="cd5ff-140">Once you have configured all of the settings in the preceding sections of this article, you are ready to deploy your web app to Azure.</span></span> <span data-ttu-id="cd5ff-141">Para ello, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="cd5ff-141">To do so, use the following steps:</span></span>

1. <span data-ttu-id="cd5ff-142">En el símbolo del sistema o la ventana de terminal que usó anteriormente, vuelva a compilar el archivo JAR con Maven si ha realizado algún cambio en el archivo *pom.xml*; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="cd5ff-142">From the command prompt or terminal window that you were using earlier, rebuild the JAR file using Maven if you made any changes to the *pom.xml* file; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="cd5ff-143">Implemente la aplicación web en Azure mediante Maven; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="cd5ff-143">Deploy your web app to Azure by using Maven; for example:</span></span>
   ```shell
   mvn azure-webapp:deploy
   ```

<span data-ttu-id="cd5ff-144">Maven implementará la aplicación web en Azure; si la aplicación web o el plan de la aplicación web no existen, se crearán.</span><span class="sxs-lookup"><span data-stu-id="cd5ff-144">Maven will deploy your web app to Azure; if the web app or web app plan does not already exist, it will be created for you.</span></span>

<span data-ttu-id="cd5ff-145">Cuando se haya implementado la web, podrá administrarla mediante [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="cd5ff-145">When your web has been deployed, you will be able to manage it through the [Azure portal].</span></span>

* <span data-ttu-id="cd5ff-146">La aplicación web aparecerá en **App Services**:</span><span class="sxs-lookup"><span data-stu-id="cd5ff-146">Your web app will be listed in **App Services**:</span></span>

   ![Aplicación web en la lista de App Services de Azure Portal][AP01]

* <span data-ttu-id="cd5ff-148">Y la dirección URL de la aplicación web se mostrará en la sección de **información general** de la aplicación web:</span><span class="sxs-lookup"><span data-stu-id="cd5ff-148">And the URL for your web app will be listed in the **Overview** for your web app:</span></span>

   ![Determinar la dirección URL de la aplicación web][AP02]

<span data-ttu-id="cd5ff-150">Compruebe que la implementación se realizó correctamente mediante el mismo comando de cURL utilizado antes, utilizando la dirección URL de la aplicación web del portal en lugar de `localhost`.</span><span class="sxs-lookup"><span data-stu-id="cd5ff-150">Verify that the deployment was successful by using the same cURL command as before, using your web app URL from the Portal instead of `localhost`.</span></span> <span data-ttu-id="cd5ff-151">Debería ver el mensaje siguiente mostrado: **Greetings from Spring Boot!**</span><span class="sxs-lookup"><span data-stu-id="cd5ff-151">You should see the following message displayed: **Greetings from Spring Boot!**</span></span> 

## <a name="next-steps"></a><span data-ttu-id="cd5ff-152">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cd5ff-152">Next steps</span></span>

<span data-ttu-id="cd5ff-153">Para más información acerca de Spring y Azure, vaya al centro de documentación de Azure.</span><span class="sxs-lookup"><span data-stu-id="cd5ff-153">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="cd5ff-154">Spring en Azure</span><span class="sxs-lookup"><span data-stu-id="cd5ff-154">Spring on Azure</span></span>](/java/azure/spring-framework)

### <a name="additional-resources"></a><span data-ttu-id="cd5ff-155">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="cd5ff-155">Additional Resources</span></span>

<span data-ttu-id="cd5ff-156">Para más información acerca de las diferentes tecnologías que se tratan en este artículo, consulte los artículos siguientes:</span><span class="sxs-lookup"><span data-stu-id="cd5ff-156">For more information about the various technologies discussed in this article, see the following articles:</span></span>

* <span data-ttu-id="cd5ff-157">[Complemento Maven de Azure Web Apps]</span><span class="sxs-lookup"><span data-stu-id="cd5ff-157">[Maven Plugin for Azure Web Apps]</span></span>

* [<span data-ttu-id="cd5ff-158">Uso del complemento Maven de Azure Web Apps para implementar una aplicación de Spring Boot en contenedor en Azure</span><span class="sxs-lookup"><span data-stu-id="cd5ff-158">How to use the Maven Plugin for Azure Web Apps to deploy a containerized Spring Boot app to Azure</span></span>](deploy-containerized-spring-boot-java-app-with-maven-plugin.md)

* [<span data-ttu-id="cd5ff-159">Creación de una entidad de servicio de Azure con la CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="cd5ff-159">Create an Azure service principal with Azure CLI 2.0</span></span>](/cli/azure/create-an-azure-service-principal-azure-cli)

* [<span data-ttu-id="cd5ff-160">Referencia de configuración de Maven</span><span class="sxs-lookup"><span data-stu-id="cd5ff-160">Maven Settings Reference</span></span>](https://maven.apache.org/settings.html)

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
