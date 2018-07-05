---
title: Cómo usar el iniciador de Spring Boot para Azure Active Directory
description: Aprenda a configurar una aplicación de Spring Boot Initializer con el iniciador de Azure Active Directory.
services: active-directory
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 06/20/2018
ms.devlang: java
ms.service: active-directory
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: identity
ms.openlocfilehash: adcbc78cc129daf589bf070741308e4024432e5d
ms.sourcegitcommit: 5282a51bf31771671df01af5814df1d2b8e4620c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/28/2018
ms.locfileid: "37090838"
---
# <a name="how-to-use-the-spring-boot-starter-for-azure-active-directory"></a><span data-ttu-id="cf45c-103">Cómo usar el iniciador de Spring Boot para Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cf45c-103">How to use the Spring Boot Starter for Azure Active Directory</span></span>

## <a name="overview"></a><span data-ttu-id="cf45c-104">Información general</span><span class="sxs-lookup"><span data-stu-id="cf45c-104">Overview</span></span>

<span data-ttu-id="cf45c-105">En este artículo se muestra cómo crear una aplicación con **[Spring Initializr]** que usa la funcionalidad Spring Boot Starter para Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cf45c-105">This article demonstrates creating an app with the **[Spring Initializr]** that uses the Spring Boot Starter for Azure Active Directory (Azure AD).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cf45c-106">requisitos previos</span><span class="sxs-lookup"><span data-stu-id="cf45c-106">Prerequisites</span></span>

<span data-ttu-id="cf45c-107">Los siguientes requisitos previos son necesarios para seguir los pasos descritos en este artículo:</span><span class="sxs-lookup"><span data-stu-id="cf45c-107">The following prerequisites are required in order to complete the steps in this article:</span></span>

* <span data-ttu-id="cf45c-108">Una suscripción de Azure. Si todavía no la tiene, puede activar sus [Ventajas para suscriptores de MSDN] o registrarse para obtener una [cuenta de Azure gratuita].</span><span class="sxs-lookup"><span data-stu-id="cf45c-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="cf45c-109">Un [kit de desarrollo de Java (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), versión 1.7 o posterior.</span><span class="sxs-lookup"><span data-stu-id="cf45c-109">A [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 or later.</span></span>
* <span data-ttu-id="cf45c-110">[Apache Maven](http://maven.apache.org/), versión 3.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="cf45c-110">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-a-custom-application-using-the-spring-initializr"></a><span data-ttu-id="cf45c-111">Creación de una aplicación personalizada mediante Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="cf45c-111">Create a custom application using the Spring Initializr</span></span>

1. <span data-ttu-id="cf45c-112">Vaya a <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="cf45c-112">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="cf45c-113">Especifique que quiere generar un proyecto de **Maven** con **Java**, escriba los nombres de **Group** (Grupo) y **Artifact** (Artefacto) de su aplicación y luego haga clic en el vínculo **Switch to the full version** (Cambiar a la versión completa) de Spring Initializr.</span><span class="sxs-lookup"><span data-stu-id="cf45c-113">Specify that you want to generate a **Maven** project with **Java**, enter the **Group** and **Aritifact** names for your application, and then click the link to **Switch to the full version** of the Spring Initializr.</span></span>

   ![Especificar los nombres de grupo y artefacto][security-01]

1. <span data-ttu-id="cf45c-115">Vaya a la sección **Core** y active la casilla **Security** (Seguridad); en la sección **Web**, active la casilla **Web**.</span><span class="sxs-lookup"><span data-stu-id="cf45c-115">Scroll down to the **Core** section and check the box for **Security**, and in the **Web** section check the box for **Web**.</span></span>

   ![Selección de los iniciadores Security y Web][security-02]

1. <span data-ttu-id="cf45c-117">Vaya a la sección **Azure** y active la casilla **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="cf45c-117">Scroll down to the **Azure** section and check the box for **Azure Active Directory**.</span></span>

   ![Seleccionar el iniciador Azure Active Directory][security-03]

1. <span data-ttu-id="cf45c-119">Desplácese a la parte inferior de la página y haga clic en el botón **Generate Project** (Generar proyecto).</span><span class="sxs-lookup"><span data-stu-id="cf45c-119">Scroll to the bottom of the page and click the button to **Generate Project**.</span></span>

   ![Generación del proyecto de Spring Boot][security-04]

1. <span data-ttu-id="cf45c-121">Cuando se le solicite, descargue el proyecto en una ruta de acceso del equipo local.</span><span class="sxs-lookup"><span data-stu-id="cf45c-121">When prompted, download the project to a path on your local computer.</span></span>

## <a name="create-and-configure-a-new-azure-active-directory-instance"></a><span data-ttu-id="cf45c-122">Creación y configuración de una nueva instancia de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cf45c-122">Create and configure a new Azure Active Directory instance</span></span>

### <a name="create-the-active-directory-instance"></a><span data-ttu-id="cf45c-123">Creación de la instancia de Active Directory</span><span class="sxs-lookup"><span data-stu-id="cf45c-123">Create the Active Directory instance</span></span>

1. <span data-ttu-id="cf45c-124">Inicie sesión en <https://portal.azure.com>.</span><span class="sxs-lookup"><span data-stu-id="cf45c-124">Log into <https://portal.azure.com>.</span></span>

1. <span data-ttu-id="cf45c-125">Haga clic en **+Nuevo**, luego en **Seguridad e identidad** y, por último, en **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="cf45c-125">Click **+New**, then **Security + Identity**, and then **Azure Active Directory**.</span></span>

   ![Creación de una nueva instancia de Azure Active Directory][directory-01]

1. <span data-ttu-id="cf45c-127">Rellene los campos **Nombre de la organización** y **Nombre de dominio inicial** y haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="cf45c-127">Enter your **Organization name** and your **Initial domain name**, and then click **Create**.</span></span>

   ![Especificación de los nombres de Azure Active Directory][directory-02]

1. <span data-ttu-id="cf45c-129">Seleccione la nueva instancia de Azure Active Directory en el menú desplegable, en la barra de herramientas superior de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="cf45c-129">Select your new Azure Active Directory from the drop-down menu on the top toolbar of the Azure portal.</span></span>

   ![Selección de la instancia de Azure Active Directory][directory-03]

1. <span data-ttu-id="cf45c-131">Seleccione **Azure Active Directory** en el menú del portal, haga clic en **Propiedades** y copie el **Id. de directorio** que usará más adelante en este artículo.</span><span class="sxs-lookup"><span data-stu-id="cf45c-131">Select **Azure Active Directory** from the portal menu, click **Properties**, and copy the **Directory ID** - you will use that later in this article.</span></span>

   ![Copia del identificador de Azure Active Directory][directory-13]

### <a name="add-an-application-registration-for-your-spring-boot-app"></a><span data-ttu-id="cf45c-133">Adición de un registro de aplicación para la aplicación de Spring Boot</span><span class="sxs-lookup"><span data-stu-id="cf45c-133">Add an application registration for your Spring Boot app</span></span>

1. <span data-ttu-id="cf45c-134">Seleccione **Azure Active Directory** en el menú del portal, haga clic en **Información general** y haga clic en **Registros de aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="cf45c-134">Select **Azure Active Directory** from the portal menu, click **Overview**, and then click **App registrations**.</span></span>

   ![Adición de un nuevo registro de aplicaciones][directory-04]

1. <span data-ttu-id="cf45c-136">Haga clic en **Nuevo registro de aplicaciones**, especifique el valor de **Nombre de la aplicación**, use http://localhost:8080 como **URL de inicio de sesión** y, por último, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="cf45c-136">Click **New application registration**, specify your application **Name**, use http://localhost:8080 for the **Sign-on URL**, and then click **Create**.</span></span>

   ![Crear registro de aplicaciones][directory-05]

1. <span data-ttu-id="cf45c-138">Haga clic en su registro de aplicaciones después de crearlo.</span><span class="sxs-lookup"><span data-stu-id="cf45c-138">Click your application registration after it has been created.</span></span>

   ![Selección del registro de aplicaciones][directory-06]

1. <span data-ttu-id="cf45c-140">Cuando se muestre la página del registro de aplicaciones, copie el valor de **Id. de aplicación** para más adelante y haga clic en **Configuración** y en **Claves**.</span><span class="sxs-lookup"><span data-stu-id="cf45c-140">When the page for your app registration, copy your **Application ID** for later use, then click **Settings**, and then click **Keys**.</span></span>

   ![Creación de las claves del registro de aplicaciones][directory-07]

1. <span data-ttu-id="cf45c-142">Agregue una **Descripción** y especifique la **Duración** de la nueva clave y haga clic en **Guardar**; el valor de la clave se rellenará automáticamente al hacer clic en el icono **Guardar**, y tiene que copiar el valor de la clave para más adelante.</span><span class="sxs-lookup"><span data-stu-id="cf45c-142">Add a **Description** and specify the **Duration** for a new key and click **Save**; the value for the key will be automatically filled in when you click the **Save** icon, and you need to copy down the value of the key for later.</span></span> <span data-ttu-id="cf45c-143">(No podrá recuperar este valor más adelante).</span><span class="sxs-lookup"><span data-stu-id="cf45c-143">(You will not be able to retrieve this value later.)</span></span>

   ![Especificación de los parámetros de clave del registro de aplicaciones][directory-08]

1. <span data-ttu-id="cf45c-145">En la página principal del registro de aplicaciones, haga clic en **Configuración** y **Permisos necesarios**.</span><span class="sxs-lookup"><span data-stu-id="cf45c-145">From the main page for your app registration, click **Settings**, and then click **Required permissions**.</span></span>

   ![Permisos necesarios del registro de aplicaciones][directory-09]

1. <span data-ttu-id="cf45c-147">Haga clic en **Microsoft Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="cf45c-147">Click **Windows Azure Active Directory**.</span></span>

   ![Selección de Microsoft Azure Active Directory][directory-10]

1. <span data-ttu-id="cf45c-149">Active las casillas **Acceder al directorio como usuario con sesión iniciada** y **Iniciar sesión y leer el perfil del usuario**, y haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="cf45c-149">Check the boxes for **Access the directory as the signed-in user** and **Sign in and read user profile**, and then click **Save**.</span></span>

   ![Habilitar los permisos de acceso][directory-11]

1. <span data-ttu-id="cf45c-151">En la página **Permisos necesarios**, haga clic en **Conceder permisos** y responda **Sí** a la pregunta.</span><span class="sxs-lookup"><span data-stu-id="cf45c-151">On the **Required permissions** page, click **Grant Permissions**, and click **Yes** when prompted.</span></span>

   ![Concesión de permisos de acceso][directory-12]

1. <span data-ttu-id="cf45c-153">En la página principal del registro de aplicación, haga clic en **Configuración** y, a continuación, haga clic en **URL de respuesta**.</span><span class="sxs-lookup"><span data-stu-id="cf45c-153">From the main page for your app registration, click **Settings**, and then click **Reply URLs**.</span></span>

   ![Edición de las URL de respuesta][directory-14]

1. <span data-ttu-id="cf45c-155">Escriba "http://localhost:8080/login/oauth2/code/azure" como nueva dirección URL de respuesta y haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="cf45c-155">Enter "http://localhost:8080/login/oauth2/code/azure" as a new reply URL, and then click **Save**.</span></span>

   ![Adición de una nueva URL de respuesta][directory-15]

## <a name="configure-and-compile-your-spring-boot-application"></a><span data-ttu-id="cf45c-157">Configuración y compilación de la aplicación de Spring Boot</span><span class="sxs-lookup"><span data-stu-id="cf45c-157">Configure and compile your Spring Boot application</span></span>

1. <span data-ttu-id="cf45c-158">Extraiga en un directorio los archivos del archivo de proyecto descargado.</span><span class="sxs-lookup"><span data-stu-id="cf45c-158">Extract the files from the downloaded project archive into a directory.</span></span>

2. <span data-ttu-id="cf45c-159">Vaya a la carpeta principal del proyecto y abra el archivo *pom.xml* en un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="cf45c-159">Navigate to the parent folder in your project and open the *pom.xml* file in a text editor.</span></span>

3. <span data-ttu-id="cf45c-160">Agregue las dependencias para la seguridad OAuth2 de Spring; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="cf45c-160">Add the dependencies for Spring OAuth2 security; for example:</span></span>

   ```xml
   <dependency>
      <groupId>org.springframework.security</groupId>
      <artifactId>spring-security-oauth2-client</artifactId>
   </dependency>
   <dependency>
      <groupId>org.springframework.security</groupId>
      <artifactId>spring-security-oauth2-jose</artifactId>
   </dependency>
   ```

4. <span data-ttu-id="cf45c-161">Guarde y cierre el archivo *pom.xml*.</span><span class="sxs-lookup"><span data-stu-id="cf45c-161">Save and close the *pom.xml* file.</span></span>

5. <span data-ttu-id="cf45c-162">Vaya a la carpeta *src/main/resources* del proyecto y abra el archivo *application.properties* en un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="cf45c-162">Navigate to the *src/main/resources* folder in your project and open the *application.properties* file in a text editor.</span></span>

6. <span data-ttu-id="cf45c-163">Agrege la clave de la cuenta de almacenamiento utilizando los valores obtenidos anteriormente; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="cf45c-163">Add the key for your storage account using the values from earlier; for example:</span></span>

   ```yaml
   # Specifies your Active Directory ID:
   azure.activedirectory.tenant-id=22222222-2222-2222-2222-222222222222

   # Specifies your App Registration's Application ID:
   spring.security.oauth2.client.registration.azure.client-id=11111111-1111-1111-1111-1111111111111111

   # Specifies your App Registration's secret key:
   spring.security.oauth2.client.registration.azure.client-secret=AbCdEfGhIjKlMnOpQrStUvWxYz==

   # Specifies the list of Active Directory groups to use for authentication:
   azure.activedirectory.active-directory-groups=Users
   ```
   <span data-ttu-id="cf45c-164">Donde:</span><span class="sxs-lookup"><span data-stu-id="cf45c-164">Where:</span></span>

   | <span data-ttu-id="cf45c-165">.</span><span class="sxs-lookup"><span data-stu-id="cf45c-165">Parameter</span></span> | <span data-ttu-id="cf45c-166">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="cf45c-166">Description</span></span> |
   |---|---|
   | `azure.activedirectory.tenant-id` | <span data-ttu-id="cf45c-167">Contiene su **Id. de directorio** de Active Directory obtenido anteriormente.</span><span class="sxs-lookup"><span data-stu-id="cf45c-167">Contains your Active Directory's **Directory ID** from earlier.</span></span> |
   | `spring.security.oauth2.client.registration.azure.client-id` | <span data-ttu-id="cf45c-168">Contiene el **Id. de aplicación** del registro de aplicaciones que completó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="cf45c-168">Contains the **Application ID** from your app registration that you completed earlier.</span></span> |
   | `spring.security.oauth2.client.registration.azure.client-secret` | <span data-ttu-id="cf45c-169">Contiene el **Valor** de la clave del registro de aplicaciones que completó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="cf45c-169">Contains the **Value** from your app registration key that you completed earlier.</span></span> |
   | `azure.activedirectory.active-directory-groups` | <span data-ttu-id="cf45c-170">Contiene una lista de los grupos de Active Directory que se usarán para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="cf45c-170">Contains a list of Active Directory groups to use for authentication.</span></span> |

   > [!NOTE]
   > 
   > <span data-ttu-id="cf45c-171">Para obtener una lista completa de los valores disponibles en su archivo *application.properties*, consulte el [ejemplo de Azure Active Directory Spring Boot][AAD Spring Boot Sample] en GitHub.</span><span class="sxs-lookup"><span data-stu-id="cf45c-171">For a full list of values that are available in your *application.properties* file, see  the [Azure Active Directory Spring Boot Sample][AAD Spring Boot Sample] on GitHub.</span></span>
   >

7. <span data-ttu-id="cf45c-172">Guarde y cierre el archivo *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="cf45c-172">Save and close the *application.properties* file.</span></span>

8. <span data-ttu-id="cf45c-173">Cree una carpeta llamada *controller* en la carpeta src de Java para su aplicación; por ejemplo: *src/main/java/com/wingtiptoys/security/controller*.</span><span class="sxs-lookup"><span data-stu-id="cf45c-173">Create a folder named *controller* in the Java source folder for your application; for example: *src/main/java/com/wingtiptoys/security/controller*.</span></span>

9. <span data-ttu-id="cf45c-174">Cree un archivo de Java nuevo llamado *HelloController.java* en la carpeta *controller* y ábralo en un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="cf45c-174">Create a new Java file named *HelloController.java* in the *controller* folder and open it in a text editor.</span></span>

10. <span data-ttu-id="cf45c-175">Escriba el código siguiente, guarde el archivo y ciérrelo:</span><span class="sxs-lookup"><span data-stu-id="cf45c-175">Enter the following code, then save and close the file:</span></span>

   ```java
   package com.wingtiptoys.security;

   import org.springframework.web.bind.annotation.RequestMapping;
   import org.springframework.web.bind.annotation.RestController;
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.security.access.prepost.PreAuthorize;
   import org.springframework.security.oauth2.client.OAuth2AuthorizedClient;
   import org.springframework.security.oauth2.client.authentication.OAuth2AuthenticationToken;
   import org.springframework.ui.Model;

   @RestController
   public class HelloController {
      @Autowired
      @PreAuthorize("hasRole('Users')")
      @RequestMapping("/")
      public String helloWorld() {
         return "Hello World!";
      }
   }
   ```
   > [!NOTE]
   > 
   > <span data-ttu-id="cf45c-176">El nombre del grupo que especifique para el método `@PreAuthorize("hasRole('')")` debe contener uno de los grupos que especificó en el campo `azure.activedirectory.active-directory-groups` del archivo *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="cf45c-176">The group name that you specify for the `@PreAuthorize("hasRole('')")` method must contain one of the groups that you specified in the `azure.activedirectory.active-directory-groups` field of your *application.properties* file.</span></span>
   >

   > [!NOTE]
   > 
   > <span data-ttu-id="cf45c-177">Puede especificar una configuración de autorización diferente para la asignación de solicitudes; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="cf45c-177">You can specify different authorization settings for different request mappings; for example:</span></span>
   >
   > ``` java
   > public class HelloController {
   >    @Autowired
   >    @PreAuthorize("hasRole('Users')")
   >    @RequestMapping("/")
   >    public String helloWorld() {
   >       return "Hello Users!";
   >    }
   >    @PreAuthorize("hasRole('Group1')")
   >    @RequestMapping("/Group1")
   >    public String groupOne() {
   >       return "Hello Group 1 Users!";
   >    }
   >    @PreAuthorize("hasRole('Group2')")
   >    @RequestMapping("/Group2")
   >    public String groupTwo() {
   >       return "Hello Group 2 Users!";
   >    }
   > }
   > ```
   >    

11. <span data-ttu-id="cf45c-178">Cree una carpeta llamada *security* en la carpeta src de Java para su aplicación; por ejemplo: *src/main/java/com/wingtiptoys/security/security*.</span><span class="sxs-lookup"><span data-stu-id="cf45c-178">Create a folder named *security* in the Java source folder for your application; for example: *src/main/java/com/wingtiptoys/security/security*.</span></span>

12. <span data-ttu-id="cf45c-179">Cree un archivo Java nuevo llamado *WebSecurityConfig.java* en la carpeta *security* y ábralo en un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="cf45c-179">Create a new Java file named *WebSecurityConfig.java* in the *security* folder and open it in a text editor.</span></span>

13. <span data-ttu-id="cf45c-180">Escriba el código siguiente, guarde el archivo y ciérrelo:</span><span class="sxs-lookup"><span data-stu-id="cf45c-180">Enter the following code, then save and close the file:</span></span>

    ```java
    package com.wingtiptoys.security;

    import org.springframework.beans.factory.annotation.Autowired;
    import org.springframework.security.config.annotation.method.configuration.EnableGlobalMethodSecurity;
    import org.springframework.security.config.annotation.web.builders.HttpSecurity;
    import org.springframework.security.config.annotation.web.configuration.EnableWebSecurity;
    import org.springframework.security.config.annotation.web.configuration.WebSecurityConfigurerAdapter;
    import org.springframework.security.oauth2.client.oidc.userinfo.OidcUserRequest;
    import org.springframework.security.oauth2.client.userinfo.OAuth2UserService;
    import org.springframework.security.oauth2.core.oidc.user.OidcUser;

    @EnableWebSecurity
    @EnableGlobalMethodSecurity(prePostEnabled = true)
    public class WebSecurityConfig extends WebSecurityConfigurerAdapter {
        @Autowired
        private OAuth2UserService<OidcUserRequest, OidcUser> oidcUserService;

        @Override
        protected void configure(HttpSecurity http) throws Exception {
            http
                .authorizeRequests()
                .anyRequest().authenticated()
                .and()
                .oauth2Login()
                .userInfoEndpoint()
                .oidcUserService(oidcUserService);
        }
    }
    ```

## <a name="build-and-test-your-app"></a><span data-ttu-id="cf45c-181">Compilación y prueba de la aplicación</span><span class="sxs-lookup"><span data-stu-id="cf45c-181">Build and test your app</span></span>

1. <span data-ttu-id="cf45c-182">Abra un símbolo del sistema y cambie el directorio a la carpeta donde se encuentra el archivo *pom.xml* de su aplicación.</span><span class="sxs-lookup"><span data-stu-id="cf45c-182">Open a command prompt and change directory to the folder where your app's *pom.xml* file is located.</span></span>

1. <span data-ttu-id="cf45c-183">Compile la aplicación de Spring Boot con Maven y ejecútela; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="cf45c-183">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

   ![Compilación de la aplicación][build-application]

1. <span data-ttu-id="cf45c-185">Después de que Maven compile e inicie la aplicación, abra <http://localhost:8080> en un explorador web; se le pedirá un nombre de usuario y una contraseña.</span><span class="sxs-lookup"><span data-stu-id="cf45c-185">After your application is built and started by Maven, open <http://localhost:8080> in a web browser; you should be prompted for a user name and password.</span></span>

   ![Inicio de sesión en su aplicación][application-login]

1. <span data-ttu-id="cf45c-187">Cuando haya iniciado sesión correctamente, verá ver el texto de ejemplo "Hello World" desde el controlador.</span><span class="sxs-lookup"><span data-stu-id="cf45c-187">After you have logged in successfully, you should see the sample "Hello World" text from the controller.</span></span>

   ![Inicio de sesión correcto][hello-world]

   > [!NOTE]
   > 
   > <span data-ttu-id="cf45c-189">Las cuentas de usuario que no están autorizadas recibirán un mensaje **HTTP 403 No autorizado**.</span><span class="sxs-lookup"><span data-stu-id="cf45c-189">User accounts which are not authorized will receive an **HTTP 403 Unauthorized** message.</span></span>
   >

## <a name="next-steps"></a><span data-ttu-id="cf45c-190">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cf45c-190">Next steps</span></span>

<span data-ttu-id="cf45c-191">Para más información acerca de cómo usar Azure Active Directory, consulte los siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="cf45c-191">For more information about using Azure Active Directory, see the following articles:</span></span>

* <span data-ttu-id="cf45c-192">[Documentación de Azure Active Directory].</span><span class="sxs-lookup"><span data-stu-id="cf45c-192">[Azure Active Directory Documentation].</span></span>

<span data-ttu-id="cf45c-193">Para obtener más información sobre el uso de aplicaciones de Spring Boot en Azure, consulte los siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="cf45c-193">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="cf45c-194">Implementación de una aplicación de Spring Boot en Azure App Service</span><span class="sxs-lookup"><span data-stu-id="cf45c-194">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)

* [<span data-ttu-id="cf45c-195">Ejecución de una aplicación de Spring Boot en un clúster de Kubernetes en Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="cf45c-195">Running a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="cf45c-196">Para más información sobre el uso de Azure con Java, consulte [Azure para desarrolladores de Java] y [Herramientas de Java para Visual Studio Team Services] (Herramientas de Java para Visual Studio Team Services).</span><span class="sxs-lookup"><span data-stu-id="cf45c-196">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="cf45c-197">**[Spring Framework]** es una solución de código abierto que ayuda a los desarrolladores de Java a crear aplicaciones de nivel empresarial.</span><span class="sxs-lookup"><span data-stu-id="cf45c-197">The **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="cf45c-198">Uno de los proyectos más populares que se basa en esa plataforma es [Spring Boot], que proporciona un enfoque simplificado para crear aplicaciones de Java independientes.</span><span class="sxs-lookup"><span data-stu-id="cf45c-198">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="cf45c-199">Para ayudar a los desarrolladores a empezar con Spring Boot, puede encontrar varios paquetes de ejemplo de Spring Boot en <https://github.com/spring-guides/>.</span><span class="sxs-lookup"><span data-stu-id="cf45c-199">To help developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>.</span></span> <span data-ttu-id="cf45c-200">Además de elegir de la lista de proyectos básicos de Spring Boot, el **[Spring Initializr]** ayuda a los desarrolladores en los primeros pasos para crear aplicaciones de Spring Boot personalizadas.</span><span class="sxs-lookup"><span data-stu-id="cf45c-200">In addition to choosing from the list of basic Spring Boot projects, the **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>

<span data-ttu-id="cf45c-201">Para obtener un ejemplo más detallado, consulte el [ejemplo de Spring Boot para Azure Active Directory][AAD Spring Boot Sample] en GitHub.</span><span class="sxs-lookup"><span data-stu-id="cf45c-201">For a more-detailed sample, see the [Azure Active Directory Spring Boot Sample][AAD Spring Boot Sample] on GitHub.</span></span>

<!-- URL List -->

[Documentación de Azure Active Directory]: /azure/active-directory/
[Azure Active Directory Documentation]: /azure/active-directory/
[Get started with Azure AD]: /azure/active-directory/get-started-azure-ad
[Azure para desarrolladores de Java]: https://docs.microsoft.com/java/azure/
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[cuenta de Azure gratuita]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Herramientas de Java para Visual Studio Team Services]: https://java.visualstudio.com/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Ventajas para suscriptores de MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/
[AAD Spring Boot Sample]: https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-active-directory-spring-boot-backend-sample

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
[directory-13]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-13.png
[directory-14]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-14.png
[directory-15]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-15.png

[build-application]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/build-application.png
[application-login]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/application-login.png
[hello-world]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/hello-world.png
