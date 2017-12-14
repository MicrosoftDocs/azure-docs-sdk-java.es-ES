---
title: "Cómo usar el iniciador de Spring Boot para Azure Active Directory"
description: "Aprenda a configurar una aplicación de Spring Boot Initializer con el iniciador de Azure Active Directory."
services: active-directory
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: multiple
ms.devlang: java
ms.topic: article
ms.date: 12/01/2017
ms.author: robmcm
ms.openlocfilehash: a999e33674ea01e776db10186e8af83ce157ef20
ms.sourcegitcommit: fc48e038721e6910cb8b1f8951df765d517e504d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/06/2017
---
# <a name="how-to-use-the-spring-boot-starter-for-azure-active-directory"></a><span data-ttu-id="abe95-103">Cómo usar el iniciador de Spring Boot para Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="abe95-103">How to use the Spring Boot Starter for Azure Active Directory</span></span>

## <a name="overview"></a><span data-ttu-id="abe95-104">Información general</span><span class="sxs-lookup"><span data-stu-id="abe95-104">Overview</span></span>

<span data-ttu-id="abe95-105">En este artículo se muestra cómo crear una aplicación con **[Spring Initializr]** que usa la funcionalidad Spring Boot Starter para Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="abe95-105">This article demonstrates creating an app with the **[Spring Initializr]** which the Spring Boot Starter for Azure Active Directory (Azure AD).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="abe95-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="abe95-106">Prerequisites</span></span>

<span data-ttu-id="abe95-107">Los siguientes requisitos previos son necesarios para seguir los pasos descritos en este artículo:</span><span class="sxs-lookup"><span data-stu-id="abe95-107">The following prerequisites are required in order to follow the steps in this article:</span></span>

* <span data-ttu-id="abe95-108">Una suscripción de Azure. Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN] o registrarse para obtener una [cuenta de Azure gratuita].</span><span class="sxs-lookup"><span data-stu-id="abe95-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="abe95-109">Un [kit de desarrollo de Java (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), versión 1.7 o posterior.</span><span class="sxs-lookup"><span data-stu-id="abe95-109">A [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 or later.</span></span>
* <span data-ttu-id="abe95-110">[Apache Maven](http://maven.apache.org/), versión 3.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="abe95-110">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-a-custom-application-using-the-spring-initializr"></a><span data-ttu-id="abe95-111">Creación de una aplicación personalizada mediante Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="abe95-111">Create a custom application using the Spring Initializr</span></span>

1. <span data-ttu-id="abe95-112">Vaya a <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="abe95-112">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="abe95-113">Especifique que quiere generar un proyecto de **Maven** con **Java**, escriba los nombres de **Group** (Grupo) y **Artifact** (Artefacto) de su aplicación y luego haga clic en el vínculo **Switch to the full version** (Cambiar a la versión completa) de Spring Initializr.</span><span class="sxs-lookup"><span data-stu-id="abe95-113">Specify that you want to generate a **Maven** project with **Java**, enter the **Group** and **Aritifact** names for your application, and then click the link to **Switch to the full version** of the Spring Initializr.</span></span>

   ![Especificar los nombres de grupo y artefacto][security-01]

1. <span data-ttu-id="abe95-115">Vaya a la sección **Core** y active la casilla **Security** (Seguridad); en la sección **Web**, active la casilla **Web**.</span><span class="sxs-lookup"><span data-stu-id="abe95-115">Scroll down to the **Core** section and check the box for **Security**, and in the **Web** section check the box for **Web**.</span></span>

   ![Selección de los iniciadores Security y Web][security-02]

1. <span data-ttu-id="abe95-117">Vaya a la sección **Azure** y active la casilla **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="abe95-117">Scroll down to the **Azure** section and check the box for **Azure Active Directory**.</span></span>

   ![Seleccionar el iniciador Azure Active Directory][security-03]

1. <span data-ttu-id="abe95-119">Desplácese a la parte inferior de la página y haga clic en el botón **Generate Project** (Generar proyecto).</span><span class="sxs-lookup"><span data-stu-id="abe95-119">Scroll to the bottom of the page and click the button to **Generate Project**.</span></span>

   ![Generación del proyecto de Spring Boot][security-04]

1. <span data-ttu-id="abe95-121">Cuando se le solicite, descargue el proyecto en una ruta de acceso del equipo local.</span><span class="sxs-lookup"><span data-stu-id="abe95-121">When prompted, download the project to a path on your local computer.</span></span>

## <a name="create-and-configure-a-new-azure-active-directory-instance"></a><span data-ttu-id="abe95-122">Creación y configuración de una nueva instancia de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="abe95-122">Create and configure a new Azure Active Directory instance</span></span>

### <a name="create-the-active-directory-instance"></a><span data-ttu-id="abe95-123">Creación de la instancia de Active Directory</span><span class="sxs-lookup"><span data-stu-id="abe95-123">Create the Active Directory instance</span></span>

1. <span data-ttu-id="abe95-124">Inicie sesión en <https://portal.azure.com>.</span><span class="sxs-lookup"><span data-stu-id="abe95-124">Log into <https://portal.azure.com>.</span></span>

1. <span data-ttu-id="abe95-125">Haga clic en **+Nuevo**, luego en **Seguridad e identidad** y, por último, en **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="abe95-125">Click **+New**, then **Security + Identity**, and then **Azure Active Directory**.</span></span>

   ![Creación de una nueva instancia de Azure Active Directory][directory-01]

1. <span data-ttu-id="abe95-127">Rellene los campos **Nombre de la organización** y **Nombre de dominio inicial** y haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="abe95-127">Enter your **Organization name** and your **Initial domain name**, and then click **Create**.</span></span>

   ![Especificación de los nombres de Azure Active Directory][directory-02]

1. <span data-ttu-id="abe95-129">Seleccione la nueva instancia de Azure Active Directory en el menú desplegable, en la barra de herramientas superior de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="abe95-129">Select your new Azure Active Directory from the drop-down menu on the top toolbar of the Azure portal.</span></span>

   ![Selección de la instancia de Azure Active Directory][directory-03]

### <a name="add-an-application-registration-for-your-spring-boot-app"></a><span data-ttu-id="abe95-131">Adición de un registro de aplicación para la aplicación de Spring Boot</span><span class="sxs-lookup"><span data-stu-id="abe95-131">Add an application registration for your Spring Boot app</span></span>

1. <span data-ttu-id="abe95-132">Seleccione **Azure Active Directory** en el menú del portal, haga clic en **Información general** y haga clic en **Registros de aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="abe95-132">Select **Azure Active Directory** from the portal menu, click **Overview**, and then click **App registrations**.</span></span>

   ![Adición de un nuevo registro de aplicaciones][directory-04]

1. <span data-ttu-id="abe95-134">Haga clic en **Nuevo registro de aplicaciones**, especifique el **Nombre** de la aplicación, use http://localhost:8080 como **URL de inicio de sesión** y, por último, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="abe95-134">Click **New application registration**, specify your application **Name**, use http://localhost:8080 for the **Sign-on URL**, and then click **Create**.</span></span>

   ![Crear registro de aplicaciones][directory-05]

1. <span data-ttu-id="abe95-136">Haga clic en su registro de aplicaciones después de crearlo.</span><span class="sxs-lookup"><span data-stu-id="abe95-136">Click your application registration after it has been created.</span></span>

   ![Selección del registro de aplicaciones][directory-06]

1. <span data-ttu-id="abe95-138">Cuando se muestre la página del registro de aplicaciones, copie el valor de **Id. de aplicación** para más adelante y haga clic en **Claves**.</span><span class="sxs-lookup"><span data-stu-id="abe95-138">When the page for your app registration, copy your **Application ID** for later, then click **Keys**.</span></span>

   ![Creación de las claves del registro de aplicaciones][directory-07]

1. <span data-ttu-id="abe95-140">Agregue una **Descripción** y especifique la **Duración** de la nueva clave y haga clic en **Guardar**; el valor de la clave se rellenará automáticamente al hacer clic en el icono **Guardar**, y tiene que copiar el valor de la clave para más adelante.</span><span class="sxs-lookup"><span data-stu-id="abe95-140">Add a **Description** and specify the **Duration** for a new key and click **Save**; the value for the key will be automatically filled in when you click the **Save** icon, and you need to copy down the value of the key for later.</span></span> <span data-ttu-id="abe95-141">(No podrá recuperar este valor más adelante).</span><span class="sxs-lookup"><span data-stu-id="abe95-141">(You will not be able to retrieve this value later.)</span></span>

   ![Especificación de los parámetros de clave del registro de aplicaciones][directory-08]

1. <span data-ttu-id="abe95-143">En la página principal del registro de aplicaciones, haga clic en **Permisos necesarios**.</span><span class="sxs-lookup"><span data-stu-id="abe95-143">From the main page for your app registration, click **Required permissions**.</span></span>

   ![Permisos necesarios del registro de aplicaciones][directory-09]

1. <span data-ttu-id="abe95-145">Haga clic en **Microsoft Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="abe95-145">Click **Windows Azure Active Directory**.</span></span>

   ![Selección de Microsoft Azure Active Directory][directory-10]

1. <span data-ttu-id="abe95-147">Active las casillas **Acceder al directorio como usuario con sesión iniciada** y **Iniciar sesión y leer el perfil del usuario**, y haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="abe95-147">Check the boxes for **Access the directory as the signed-in user** and **Sign in and read user profile**, and then click **Save**.</span></span>

   ![Habilitar los permisos de acceso][directory-11]

1. <span data-ttu-id="abe95-149">En la página **Permisos necesarios**, haga clic en **Conceder permisos** y responda **Sí** a la pregunta.</span><span class="sxs-lookup"><span data-stu-id="abe95-149">On the **Required permissions** page, click **Grant Permissions**, and click **Yes** when prompted.</span></span>

   ![Concesión de permisos de acceso][directory-12]

## <a name="configure-and-compile-your-spring-boot-application"></a><span data-ttu-id="abe95-151">Configuración y compilación de la aplicación de Spring Boot</span><span class="sxs-lookup"><span data-stu-id="abe95-151">Configure and compile your Spring Boot application</span></span>

1. <span data-ttu-id="abe95-152">Extraiga en un directorio los archivos del archivo de proyecto descargado.</span><span class="sxs-lookup"><span data-stu-id="abe95-152">Extract the files from the downloaded project archive into a directory.</span></span>

1. <span data-ttu-id="abe95-153">Vaya a la carpeta principal del proyecto y abra el archivo *pom.xml* en un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="abe95-153">Navigate to the parent folder in your project and open the *pom.xml* file in a text editor.</span></span>

1. <span data-ttu-id="abe95-154">Agregue la dependencia para la seguridad OAuth2 de Spring; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="abe95-154">Add the dependency for Spring OAuth2 security; for example:</span></span>

   ```xml
   <dependency>
      <groupId>org.springframework.security.oauth</groupId>
      <artifactId>spring-security-oauth2</artifactId>
   </dependency>
   ```

1. <span data-ttu-id="abe95-155">Guarde y cierre el archivo *pom.xml*.</span><span class="sxs-lookup"><span data-stu-id="abe95-155">Save and close the  the *pom.xml* file.</span></span>

1. <span data-ttu-id="abe95-156">Vaya a la carpeta *src/main/resources* del proyecto y abra el archivo *application.properties* en un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="abe95-156">Navigate to the *src/main/resources* folder in your project and open the *application.properties* file in a text editor.</span></span>

1. <span data-ttu-id="abe95-157">Agrege la clave de la cuenta de almacenamiento utilizando los valores obtenidos anteriormente; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="abe95-157">Add the key for your storage account using the values from earlier; for example:</span></span>

   ```yaml
   # Specifies your Active Directory Application ID:
   azure.activedirectory.clientId=11111111-1111-1111-1111-1111111111111111

   # Specifies your secret key:
   azure.activedirectory.clientSecret=AbCdEfGhIjKlMnOpQrStUvWxYz==

   # Specifies the list of Active Directory groups to use for authentication:
   azure.activedirectory.activeDirectoryGroups=Users
   ```
   <span data-ttu-id="abe95-158">Donde:</span><span class="sxs-lookup"><span data-stu-id="abe95-158">Where:</span></span>
   <span data-ttu-id="abe95-159">Parámetro</span><span class="sxs-lookup"><span data-stu-id="abe95-159">Parameter</span></span> | <span data-ttu-id="abe95-160">Descripción</span><span class="sxs-lookup"><span data-stu-id="abe95-160">Description</span></span>
   ---|---|---
   `azure.activedirectory.clientId` | <span data-ttu-id="abe95-161">Contiene el **Id. de aplicación** obtenido anteriormente.</span><span class="sxs-lookup"><span data-stu-id="abe95-161">Contains your **Application ID** from earlier.</span></span>
   `azure.activedirectory.clientSecret` | <span data-ttu-id="abe95-162">Contiene la clave del registro de aplicaciones que completó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="abe95-162">Contains the key value from your app registration which you completed earlier.</span></span>
   `azure.activedirectory.activeDirectoryGroups` | <span data-ttu-id="abe95-163">Contiene una lista de los grupos de Active Directory que se usarán para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="abe95-163">Contains a list of Active Directory groups to use for authentication.</span></span>


1. <span data-ttu-id="abe95-164">Guarde y cierre el archivo *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="abe95-164">Save and close the  the *application.properties* file.</span></span>

1. <span data-ttu-id="abe95-165">Cree una carpeta llamada *controller* en la carpeta src de Java para su aplicación; por ejemplo: *src/main/java/com/wingtiptoys/security/controller*.</span><span class="sxs-lookup"><span data-stu-id="abe95-165">Create a folder named *controller* in the Java source folder for your application; for example: *src/main/java/com/wingtiptoys/security/controller*.</span></span>

1. <span data-ttu-id="abe95-166">Cree un archivo de Java nuevo llamado *HelloController.java* en la carpeta *controller* y ábralo en un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="abe95-166">Create a new Java file named *HelloController.java* in the *controller* folder and open it in a text editor.</span></span>

1. <span data-ttu-id="abe95-167">Escriba el código siguiente, guarde el archivo y ciérrelo:</span><span class="sxs-lookup"><span data-stu-id="abe95-167">Enter the following code, then save and close the file:</span></span>

   ```java
   package com.wingtiptoys.security;
   
   import org.springframework.web.bind.annotation.RequestMapping;
   import org.springframework.web.bind.annotation.RestController;
   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;
   
   import org.springframework.security.access.prepost.PreAuthorize;
   import org.springframework.security.web.authentication.preauth.PreAuthenticatedAuthenticationToken;
   
   @RestController
   public class HelloController {
      @PreAuthorize("hasRole('Users')")
      @RequestMapping("/")
      public String hello() {
         return "Hello World!";
      }
   }
   ```

1. <span data-ttu-id="abe95-168">Cree una carpeta llamada *security* en la carpeta src de Java para su aplicación; por ejemplo: *src/main/java/com/wingtiptoys/security/security*.</span><span class="sxs-lookup"><span data-stu-id="abe95-168">Create a folder named *security* in the Java source folder for your application; for example: *src/main/java/com/wingtiptoys/security/security*.</span></span>

1. <span data-ttu-id="abe95-169">Cree un archivo Java nuevo llamado *WebSecurityConfig.java* en la carpeta *security* y ábralo en un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="abe95-169">Create a new Java file named *WebSecurityConfig.java* in the *security* folder and open it in a text editor.</span></span>

1. <span data-ttu-id="abe95-170">Escriba el código siguiente, guarde el archivo y ciérrelo:</span><span class="sxs-lookup"><span data-stu-id="abe95-170">Enter the following code, then save and close the file:</span></span>

   ```java
   package com.wingtiptoys.security;

   import com.microsoft.azure.spring.autoconfigure.aad.AADAuthenticationFilter;
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.boot.autoconfigure.security.oauth2.client.EnableOAuth2Sso;
   import org.springframework.security.config.annotation.method.configuration.EnableGlobalMethodSecurity;
   import org.springframework.security.config.annotation.web.builders.HttpSecurity;
   import org.springframework.security.config.annotation.web.configuration.WebSecurityConfigurerAdapter;
   import org.springframework.security.web.authentication.UsernamePasswordAuthenticationFilter;
   import org.springframework.security.web.csrf.CookieCsrfTokenRepository;
   
   @EnableOAuth2Sso
   @EnableGlobalMethodSecurity(securedEnabled = true, prePostEnabled = true)
   
   public class WebSecurityConfig extends WebSecurityConfigurerAdapter {
      @Autowired
      private AADAuthenticationFilter aadAuthFilter;
      @Override
      protected void configure(HttpSecurity http) throws Exception {
         http.authorizeRequests().anyRequest().permitAll();
         http.addFilterBefore(aadAuthFilter, UsernamePasswordAuthenticationFilter.class);
      }
   }
   ```

## <a name="build-and-test-your-app"></a><span data-ttu-id="abe95-171">Compilación y prueba de la aplicación</span><span class="sxs-lookup"><span data-stu-id="abe95-171">Build and test your app</span></span>

1. <span data-ttu-id="abe95-172">Abra un símbolo del sistema y cambie el directorio a la carpeta donde se encuentra el archivo *pom.xml* de su aplicación.</span><span class="sxs-lookup"><span data-stu-id="abe95-172">Open a command prompt and change directory to the folder where your app's *pom.xml* file is located.</span></span>

1. <span data-ttu-id="abe95-173">Compile la aplicación de Spring Boot con Maven y ejecútela; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="abe95-173">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   ```

   ![][build-application]

1. <span data-ttu-id="abe95-174">Compile la aplicación de Spring Boot con Maven y ejecútela; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="abe95-174">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```



1. <span data-ttu-id="abe95-175">Después de que Maven haya compilado e iniciado la aplicación, abra <http://localhost:8080> en un explorador web.</span><span class="sxs-lookup"><span data-stu-id="abe95-175">After your application is built and started by Maven, open <http://localhost:8080> in a web browser.</span></span>

## <a name="next-steps"></a><span data-ttu-id="abe95-176">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="abe95-176">Next steps</span></span>

<span data-ttu-id="abe95-177">Para más información acerca de cómo usar Azure Active Directory, consulte los siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="abe95-177">For more information about using Azure Active Directory, see the following articles:</span></span>

* <span data-ttu-id="abe95-178">[Documentación de Azure Active Directory].</span><span class="sxs-lookup"><span data-stu-id="abe95-178">[Azure Active Directory Documentation].</span></span>

<span data-ttu-id="abe95-179">Para obtener más información sobre el uso de aplicaciones de Spring Boot en Azure, consulte los siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="abe95-179">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="abe95-180">Implementación de una aplicación de Spring Boot en Azure App Service</span><span class="sxs-lookup"><span data-stu-id="abe95-180">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)

* [<span data-ttu-id="abe95-181">Ejecución de una aplicación de Spring Boot en un clúster de Kubernetes en Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="abe95-181">Running a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="abe95-182">Para más información sobre el uso de Azure con Java, consulte [Azure para desarrolladores de Java] y [Java Tools for Visual Studio Team Services] (Herramientas de Java para Visual Studio Team Services).</span><span class="sxs-lookup"><span data-stu-id="abe95-182">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="abe95-183">**[Spring Framework]** es una solución de código abierto que ayuda a los desarrolladores de Java a crear aplicaciones de nivel empresarial.</span><span class="sxs-lookup"><span data-stu-id="abe95-183">The **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="abe95-184">Uno de los proyectos más populares que se basa en esa plataforma es [Spring Boot], que proporciona un enfoque simplificado para crear aplicaciones de Java independientes.</span><span class="sxs-lookup"><span data-stu-id="abe95-184">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="abe95-185">Para ayudar a los desarrolladores a empezar con Spring Boot, puede encontrar varios paquetes de ejemplo de Spring Boot en <https://github.com/spring-guides/>.</span><span class="sxs-lookup"><span data-stu-id="abe95-185">To help developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>.</span></span> <span data-ttu-id="abe95-186">Además de elegir de la lista de proyectos básicos de Spring Boot, el **[Spring Initializr]** ayuda a los desarrolladores en los primeros pasos para crear aplicaciones de Spring Boot personalizadas.</span><span class="sxs-lookup"><span data-stu-id="abe95-186">In addition to choosing from the list of basic Spring Boot projects, the **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>

<!-- URL List -->

[Documentación de Azure Active Directory]: /azure/active-directory/
[Get started with Azure AD]: /azure/active-directory/get-started-azure-ad
[Azure para desarrolladores de Java]: https://docs.microsoft.com/java/azure/
[cuenta de Azure gratuita]: https://azure.microsoft.com/pricing/free-trial/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[ventajas como suscriptor de MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[security-01]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/security-01.png
[security-02]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/security-02.png
[security-03]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/security-03.png
[security-04]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/security-04.png

[directory-01]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-01.png
[directory-02]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-02.png
[directory-03]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-03.png
[directory-04]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-04.png
[directory-05]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-05.png
[directory-06]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-06.png
[directory-07]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-07.png
[directory-08]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-08.png
[directory-09]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-09.png
[directory-10]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-10.png
[directory-11]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-11.png
[directory-12]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-12.png

[build-application]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/build-application.png
