---
title: "Implementación de una aplicación de Spring Boot en la nube con Azure App Service"
description: "Este tutorial guiará a los desarrolladores a través de los pasos necesarios para implementar una aplicación web inicial de Spring Boot en la nube con Azure App Service."
services: app-service
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 
ms.author: asirveda;robmcm
ms.date: 02/01/2018
ms.devlang: java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: adf779e2ba6ca73ea3a2406613f9622cc9ecbf99
ms.sourcegitcommit: 151aaa6ccc64d94ed67f03e846bab953bde15b4a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/03/2018
---
# <a name="deploy-a-spring-boot-application-to-the-cloud-with-azure-app-service"></a><span data-ttu-id="57cdb-103">Implementación de una aplicación de Spring Boot en la nube con Azure App Service</span><span class="sxs-lookup"><span data-stu-id="57cdb-103">Deploy a Spring Boot application to the cloud with Azure App Service</span></span>

<span data-ttu-id="57cdb-104">Este tutorial le ayudará a crear una aplicación web de ejemplo de [Spring Boot] y a implementarla en [Azure App Service].</span><span class="sxs-lookup"><span data-stu-id="57cdb-104">This tutorial will walk you though creating a sample [Spring Boot] Getting Started web app and deploying it to [Azure App Service].</span></span>

### <a name="prerequisites"></a><span data-ttu-id="57cdb-105">requisitos previos</span><span class="sxs-lookup"><span data-stu-id="57cdb-105">Prerequisites</span></span>

<span data-ttu-id="57cdb-106">Para poder realizar los pasos de este tutorial, necesitará tener lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="57cdb-106">In order to complete the steps in this tutorial, you need to have the following:</span></span>

* <span data-ttu-id="57cdb-107">Una suscripción de Azure. Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN] o registrarse para obtener una [cuenta de Azure gratuita].</span><span class="sxs-lookup"><span data-stu-id="57cdb-107">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="57cdb-108">Un [kit para desarrolladores de Java (JDK)] actualizado.</span><span class="sxs-lookup"><span data-stu-id="57cdb-108">An up-to-date [Java Developer Kit (JDK)].</span></span>
* <span data-ttu-id="57cdb-109">La herramienta de compilación [Maven] de Apache (versión 3).</span><span class="sxs-lookup"><span data-stu-id="57cdb-109">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="57cdb-110">Un cliente [Git].</span><span class="sxs-lookup"><span data-stu-id="57cdb-110">A [Git] client.</span></span>

## <a name="create-the-spring-boot-getting-started-web-app"></a><span data-ttu-id="57cdb-111">Creación de la aplicación web inicial de Spring Boot</span><span class="sxs-lookup"><span data-stu-id="57cdb-111">Create the Spring Boot Getting Started web app</span></span>

<span data-ttu-id="57cdb-112">Los siguientes pasos le guiarán por las fases necesarias para crear una aplicación web de Spring Boot sencilla y probarla de forma local.</span><span class="sxs-lookup"><span data-stu-id="57cdb-112">The following steps will walk you through the steps that are required to create a simple Spring Boot web application and test it locally.</span></span>

1. <span data-ttu-id="57cdb-113">Abra el símbolo del sistema, cree un directorio local para alojar la aplicación y cambie a dicho directorio, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="57cdb-113">Open a command-prompt and create a local directory to hold your application, and change to that directory; for example:</span></span>
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="57cdb-114">-- o --</span><span class="sxs-lookup"><span data-stu-id="57cdb-114">-- or --</span></span>
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="57cdb-115">Clone el proyecto de ejemplo [inicial de Spring Boot] en el directorio recién creado, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="57cdb-115">Clone the [Spring Boot Getting Started] sample project into the directory you just created; for example:</span></span>
   ```
   git clone https://github.com/spring-guides/gs-spring-boot.git
   ```

1. <span data-ttu-id="57cdb-116">Cambie de directorio al del proyecto finalizado, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="57cdb-116">Change directory to the completed project; for example:</span></span>
   ```
   cd gs-spring-boot
   cd complete
   ```

1. <span data-ttu-id="57cdb-117">Compile el archivo JAR con Maven, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="57cdb-117">Build the JAR file using Maven; for example:</span></span>
   ```
   mvn package
   ```

1. <span data-ttu-id="57cdb-118">Una vez creada la aplicación web, cambie el directorio al del archivo JAR e inicie la aplicación web, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="57cdb-118">Once the web app has been created, change directory to the JAR file and start the web app; for example:</span></span>
   ```
   cd target
   java -jar gs-spring-boot-0.1.0.jar
   ```

1. <span data-ttu-id="57cdb-119">Compruebe la aplicación web. Para ello, vaya a http://localhost:8080 con un explorador web, o bien utilice una sintaxis como la del siguiente ejemplo si tiene cURL disponible:</span><span class="sxs-lookup"><span data-stu-id="57cdb-119">Test the web app by browsing to http://localhost:8080 using a web browser, or use the syntax like the following example if you have curl available:</span></span>
   ```
   curl http://localhost:8080
   ```

1. <span data-ttu-id="57cdb-120">Debería aparecer el siguiente mensaje: **Greetings from Spring Boot!** (Saludos de Spring Boot).</span><span class="sxs-lookup"><span data-stu-id="57cdb-120">You should see the following message displayed: **Greetings from Spring Boot!**</span></span>

   ![Buscar aplicación de ejemplo][SB01]

## <a name="create-an-azure-web-app-for-use-with-java"></a><span data-ttu-id="57cdb-122">Creación de una aplicación web de Azure para usarla con Java</span><span class="sxs-lookup"><span data-stu-id="57cdb-122">Create an Azure web app for use with Java</span></span>

<span data-ttu-id="57cdb-123">Los siguientes pasos le guiarán por las diferentes fases de creación de una aplicación web de Azure, de ajuste de la configuración necesaria para Java y de configuración de las credenciales de FTP.</span><span class="sxs-lookup"><span data-stu-id="57cdb-123">The following steps will walk you through the steps to create an Azure Web App, configure the required settings for Java, and configure your FTP credentials.</span></span>

1. <span data-ttu-id="57cdb-124">Vaya a [Azure Portal] e inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="57cdb-124">Browse to the [Azure portal] and log in.</span></span>

1. <span data-ttu-id="57cdb-125">Una vez que haya iniciado sesión en la cuenta de Azure Portal, haga clic en el icono de menú de **App Services**:</span><span class="sxs-lookup"><span data-stu-id="57cdb-125">Once you have logged into your account on the Azure portal, click the menu icon for **App Services**:</span></span>
   
   ![Azure Portal][AZ01]

1. <span data-ttu-id="57cdb-127">Cuando aparezca la página **App Services**, haga clic en **+ Agregar** para crear un nuevo elemento de App Service.</span><span class="sxs-lookup"><span data-stu-id="57cdb-127">When the **App Services** page is displayed, click **+ Add** to create a new App Service.</span></span>

   ![Creación de un elemento App Service][AZ02]

1. <span data-ttu-id="57cdb-129">Cuando aparezca la lista de plantillas de aplicaciones web, haga clic en el vínculo de la aplicación web básica de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="57cdb-129">When the list of web app templates is displayed, click the link for the basic Microsoft Web App.</span></span>

   ![Plantillas de aplicaciones web][AZ03]

1. <span data-ttu-id="57cdb-131">Cuando aparezca la página de información de plantillas de aplicaciones web, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="57cdb-131">When the information page for the Web App template is displayed, click **Create**.</span></span>

   ![Crear aplicación web][AZ04]

1. <span data-ttu-id="57cdb-133">Proporcione un nombre único para la aplicación web y especifique cualquier configuración adicional. A continuación, seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="57cdb-133">Provide a unique name for your web app and specify any additional settings, and then **Create**.</span></span>

   ![Creación de configuración de aplicaciones web][AZ05]

1. <span data-ttu-id="57cdb-135">Una vez creada la aplicación web, haga clic en el icono de menú de **App Services** y, a continuación, haga clic en la aplicación web recién creada:</span><span class="sxs-lookup"><span data-stu-id="57cdb-135">Once your web app has been created, click the menu icon for **App Services**, and then click your newly-created web app:</span></span>

   ![Lista de Web Apps][AZ06]

1. <span data-ttu-id="57cdb-137">Cuando aparezca la aplicación web, especifique la versión de Java. Para ello, siga los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="57cdb-137">When your web app is displayed, specify the Java version by using the following steps:</span></span>

   <span data-ttu-id="57cdb-138">a.</span><span class="sxs-lookup"><span data-stu-id="57cdb-138">a.</span></span> <span data-ttu-id="57cdb-139">Haga clic en el elemento de menú **Configuración de la aplicación**.</span><span class="sxs-lookup"><span data-stu-id="57cdb-139">Click the **Application Settings** menu item.</span></span>

   <span data-ttu-id="57cdb-140">b.</span><span class="sxs-lookup"><span data-stu-id="57cdb-140">b.</span></span> <span data-ttu-id="57cdb-141">Seleccione **Java 8** como versión de Java.</span><span class="sxs-lookup"><span data-stu-id="57cdb-141">Choose **Java 8** for the Java version.</span></span>

   <span data-ttu-id="57cdb-142">c.</span><span class="sxs-lookup"><span data-stu-id="57cdb-142">c.</span></span> <span data-ttu-id="57cdb-143">Seleccione **Más reciente** como versión secundaria de Java.</span><span class="sxs-lookup"><span data-stu-id="57cdb-143">Choose **Newest** for the minor Java version.</span></span>

   <span data-ttu-id="57cdb-144">d.</span><span class="sxs-lookup"><span data-stu-id="57cdb-144">d.</span></span> <span data-ttu-id="57cdb-145">Seleccione **Newest Tomcat 8.5** como contenedor web.</span><span class="sxs-lookup"><span data-stu-id="57cdb-145">Choose **Newest Tomcat 8.5** for the web container.</span></span> <span data-ttu-id="57cdb-146">(Este contenedor en realidad no se usará. Azure usará el contenedor de la aplicación de Spring Boot).</span><span class="sxs-lookup"><span data-stu-id="57cdb-146">(This container will not actually be used; Azure will use the container from your Spring Boot application.)</span></span>

   <span data-ttu-id="57cdb-147">e.</span><span class="sxs-lookup"><span data-stu-id="57cdb-147">e.</span></span> <span data-ttu-id="57cdb-148">Haga clic en **Save**(Guardar).</span><span class="sxs-lookup"><span data-stu-id="57cdb-148">Click **Save**.</span></span>

   ![Configuración de la aplicación][AZ07]

1. <span data-ttu-id="57cdb-150">Especifique las credenciales de implementación de FTP. Para ello, siga los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="57cdb-150">Specify your FTP deployment credentials by using the following steps:</span></span>

   <span data-ttu-id="57cdb-151">a.</span><span class="sxs-lookup"><span data-stu-id="57cdb-151">a.</span></span> <span data-ttu-id="57cdb-152">Haga clic en el elemento de menú **Credenciales de implementación**.</span><span class="sxs-lookup"><span data-stu-id="57cdb-152">Click the **Deployment Credentials** menu item.</span></span>

   <span data-ttu-id="57cdb-153">b.</span><span class="sxs-lookup"><span data-stu-id="57cdb-153">b.</span></span> <span data-ttu-id="57cdb-154">Especifique el nombre de usuario y la contraseña.</span><span class="sxs-lookup"><span data-stu-id="57cdb-154">Specify your username and password.</span></span>

   <span data-ttu-id="57cdb-155">c.</span><span class="sxs-lookup"><span data-stu-id="57cdb-155">c.</span></span> <span data-ttu-id="57cdb-156">Haga clic en **Save**(Guardar).</span><span class="sxs-lookup"><span data-stu-id="57cdb-156">Click **Save**.</span></span>

   ![Especificación de credenciales de implementación][AZ08]

1. <span data-ttu-id="57cdb-158">Recupere la información de conexión del FTP. Para ello, siga los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="57cdb-158">Retrieve your FTP connection information by using the following steps:</span></span>

   <span data-ttu-id="57cdb-159">a.</span><span class="sxs-lookup"><span data-stu-id="57cdb-159">a.</span></span> <span data-ttu-id="57cdb-160">Haga clic en el elemento de menú **Credenciales de implementación**.</span><span class="sxs-lookup"><span data-stu-id="57cdb-160">Click the **Deployment Credentials** menu item.</span></span>

   <span data-ttu-id="57cdb-161">b.</span><span class="sxs-lookup"><span data-stu-id="57cdb-161">b.</span></span> <span data-ttu-id="57cdb-162">Copie el nombre de usuario y la URL del FTP completos, y guárdelos para la siguiente sección del tutorial.</span><span class="sxs-lookup"><span data-stu-id="57cdb-162">Copy your full FTP username and URL and save them for the next section of this tutorial.</span></span>

   ![URL y credenciales de FTP][AZ09]

## <a name="deploy-your-spring-boot-web-app-to-azure"></a><span data-ttu-id="57cdb-164">Implementación de la aplicación web de Spring Boot en Azure</span><span class="sxs-lookup"><span data-stu-id="57cdb-164">Deploy your Spring Boot web app to Azure</span></span>

<span data-ttu-id="57cdb-165">Los siguientes pasos le guiarán por las fases necesarias para implementar la aplicación web de Spring Boot en Azure.</span><span class="sxs-lookup"><span data-stu-id="57cdb-165">The following steps will walk you through the steps to deploy your Spring Boot web app to Azure.</span></span>

1. <span data-ttu-id="57cdb-166">Abra un editor de texto, como el Bloc de notas de Windows, y pegue el siguiente texto en un nuevo documento. A continuación, guarde el archivo como *web.config*:</span><span class="sxs-lookup"><span data-stu-id="57cdb-166">Open a text editor such as Windows Notepad and paste the following text into a new document, then save the file as *web.config*:</span></span>
   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <configuration>
     <system.webServer>
       <handlers>
         <add name="httpPlatformHandler" path="*" verb="*" modules="httpPlatformHandler" resourceType="Unspecified" />
       </handlers>
       <httpPlatform processPath="%JAVA_HOME%\bin\java.exe"
           arguments="-Djava.net.preferIPv4Stack=true -Dserver.port=%HTTP_PLATFORM_PORT% -jar &quot;%HOME%\site\wwwroot\gs-spring-boot-0.1.0.jar&quot;">
       </httpPlatform>
     </system.webServer>
   </configuration>
   ```

1. <span data-ttu-id="57cdb-167">Después de guardar el archivo *web.config* en el sistema, conéctese a la aplicación web a través de FTP con la URL, el nombre de usuario y la contraseña de la sección anterior de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="57cdb-167">After you have saved the *web.config* file to your system, connect to your web app via FTP using the URL, username, and password from the preceding section of this tutorial.</span></span> <span data-ttu-id="57cdb-168">Por ejemplo: </span><span class="sxs-lookup"><span data-stu-id="57cdb-168">For example:</span></span>
   ```
   ftp
   open waws-prod-sn0-000.ftp.azurewebsites.windows.net
   user wingtiptoys-springboot\wingtiptoysuser
   pass ********
   ```

1. <span data-ttu-id="57cdb-169">Cambie el directorio remoto a la carpeta raíz de la aplicación web (que se encuentra en */sitio/wwwRaíz*) y, a continuación, copie el archivo JAR de la aplicación de Spring Boot y el archivo *web.config* anterior.</span><span class="sxs-lookup"><span data-stu-id="57cdb-169">Change the remote directory to the root folder of your web app, (which is at */site/wwwroot*), then copy the JAR file from your Spring Boot application and the *web.config* from earlier.</span></span> <span data-ttu-id="57cdb-170">Por ejemplo: </span><span class="sxs-lookup"><span data-stu-id="57cdb-170">For example:</span></span>
   ```
   cd site/wwwroot
   put gs-spring-boot-0.1.0.jar
   put web.config
   ```

1. <span data-ttu-id="57cdb-171">Una vez implementados los archivos JAR y *web.config* en la aplicación web, debe reiniciar esta con Azure Portal:</span><span class="sxs-lookup"><span data-stu-id="57cdb-171">After you have deployed your JAR and *web.config* files to your web app, you need to restart your web app using the Azure portal:</span></span>

   ![Reinicio de la aplicación web][AZ10]

1. <span data-ttu-id="57cdb-173">Compruebe la aplicación web. Para ello, acceda a la URL de la aplicación con un explorador web, o bien utilice una sintaxis como la del siguiente ejemplo si tiene cURL disponible:</span><span class="sxs-lookup"><span data-stu-id="57cdb-173">Test the web app by browsing to your web app's URL using a web browser, or use the syntax like the following example if you have curl available:</span></span>
   ```
   curl http://wingtiptoys-springboot.azurewebsites.net/
   ```

1. <span data-ttu-id="57cdb-174">Debería aparecer el siguiente mensaje: **Greetings from Spring Boot!** (Saludos de Spring Boot).</span><span class="sxs-lookup"><span data-stu-id="57cdb-174">You should see the following message displayed: **Greetings from Spring Boot!**</span></span>

   ![Buscar aplicación de ejemplo][SB02]

## <a name="next-steps"></a><span data-ttu-id="57cdb-176">pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="57cdb-176">Next steps</span></span>

<span data-ttu-id="57cdb-177">Para obtener más información sobre el uso de aplicaciones de Spring Boot en Azure, consulte los siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="57cdb-177">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="57cdb-178">Implementación de una aplicación de Spring Boot en Linux en Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="57cdb-178">Deploy a Spring Boot Application on Linux in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-linux.md)

* [<span data-ttu-id="57cdb-179">Implementación de una aplicación de Spring Boot en un clúster de Kubernetes en Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="57cdb-179">Deploy a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="57cdb-180">Para más información sobre el uso de Azure con Java, consulte [Azure para desarrolladores de Java] y [Java Tools for Visual Studio Team Services] (Herramientas de Java para Visual Studio Team Services).</span><span class="sxs-lookup"><span data-stu-id="57cdb-180">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="57cdb-181">Para obtener más información sobre la implementación de aplicaciones web en Azure mediante FTP, consulte [Implementación de la aplicación en Azure App Service mediante FTP/S].</span><span class="sxs-lookup"><span data-stu-id="57cdb-181">For additional information about depoying web apps to Azure using FTP, see [Deploy your app to Azure App Service using FTP/S].</span></span>

<span data-ttu-id="57cdb-182">Para obtener más información sobre el proyecto de ejemplo de Spring Boot, consulte [inicial de Spring Boot].</span><span class="sxs-lookup"><span data-stu-id="57cdb-182">For further details about the Spring Boot sample project, see [Spring Boot Getting Started].</span></span>

<span data-ttu-id="57cdb-183">Para obtener ayuda para dar sus primeros pasos con sus propias aplicaciones de Spring Boot, consulte **Spring Initializr** en https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="57cdb-183">For help with getting started with your own Spring Boot applications, see the **Spring Initializr** at https://start.spring.io/.</span></span>

<span data-ttu-id="57cdb-184">Para obtener más información sobre configuración de valores adicionales para la aplicación web, consulte [Configuración de aplicaciones web en Azure App Service].</span><span class="sxs-lookup"><span data-stu-id="57cdb-184">For more information about configuring additional settings for your web app, see [Configure web apps in Azure App Service].</span></span>

<!-- URL List -->

[Azure App Service]: https://azure.microsoft.com/services/app-service/
[Azure Container Service]: https://azure.microsoft.com/services/container-service/
[Azure para desarrolladores de Java]: https://docs.microsoft.com/java/azure/
[Azure Portal]: https://portal.azure.com/
[Configuración de aplicaciones web en Azure App Service]: /azure/app-service/web-sites-configure
[Implementación de la aplicación en Azure App Service mediante FTP/S]: https://docs.microsoft.com/azure/app-service/app-service-deploy-ftp
[cuenta de Azure gratuita]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[kit para desarrolladores de Java (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[ventajas como suscriptor de MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[inicial de Spring Boot]: https://github.com/spring-guides/gs-spring-boot
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[SB01]: ./media/deploy-spring-boot-java-web-app-on-azure/SB01.png
[SB02]: ./media/deploy-spring-boot-java-web-app-on-azure/SB02.png

[AZ01]: ./media/deploy-spring-boot-java-web-app-on-azure/AZ01.png
[AZ02]: ./media/deploy-spring-boot-java-web-app-on-azure/AZ02.png
[AZ03]: ./media/deploy-spring-boot-java-web-app-on-azure/AZ03.png
[AZ04]: ./media/deploy-spring-boot-java-web-app-on-azure/AZ04.png
[AZ05]: ./media/deploy-spring-boot-java-web-app-on-azure/AZ05.png
[AZ06]: ./media/deploy-spring-boot-java-web-app-on-azure/AZ06.png
[AZ07]: ./media/deploy-spring-boot-java-web-app-on-azure/AZ07.png
[AZ08]: ./media/deploy-spring-boot-java-web-app-on-azure/AZ08.png
[AZ09]: ./media/deploy-spring-boot-java-web-app-on-azure/AZ09.png
[AZ10]: ./media/deploy-spring-boot-java-web-app-on-azure/AZ10.png
