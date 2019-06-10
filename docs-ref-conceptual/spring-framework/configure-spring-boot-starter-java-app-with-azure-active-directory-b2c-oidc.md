---
title: Cómo usar Spring Boot Starter para Azure Active Directory B2C
description: Aprenda a configurar una aplicación de Spring Boot Initializer con el iniciador de Azure Active Directory B2C.
services: active-directory-b2c
documentationcenter: java
author: panli
manager: kevinzha
editor: panli
ms.assetid: ''
ms.author: panli
ms.date: 02/28/2019
ms.devlang: java
ms.service: active-directory-b2c
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: identity
ms.openlocfilehash: 21aa6c812a519d686356851a57f00688d9a24fa4
ms.sourcegitcommit: 733115fe0a7b5109b511b4a32490f8264cf91217
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/15/2019
ms.locfileid: "65625709"
---
# <a name="tutorial-secure-a-java-web-app-using-the-spring-boot-starter-for-azure-active-directory-b2c"></a><span data-ttu-id="fb451-103">Tutorial: Protección de una aplicación web de Java con Spring Boot Starter para Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="fb451-103">Tutorial: Secure a Java web app using the Spring Boot Starter for Azure Active Directory B2C.</span></span>

## <a name="overview"></a><span data-ttu-id="fb451-104">Información general</span><span class="sxs-lookup"><span data-stu-id="fb451-104">Overview</span></span>

<span data-ttu-id="fb451-105">En este artículo se muestra cómo crear una aplicación de Java con [Spring Initializr](https://start.spring.io/), que usa Spring Boot Starter para Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fb451-105">This article demonstrates creating a Java app with the [Spring Initializr](https://start.spring.io/) that uses the Spring Boot Starter for Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fb451-106">En este tutorial, aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="fb451-106">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="fb451-107">Crear una aplicación de Java mediante Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="fb451-107">Create a Java application using the Spring Initializr</span></span>
> * <span data-ttu-id="fb451-108">Configurar Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="fb451-108">Configure Azure Active Directory B2C</span></span>
> * <span data-ttu-id="fb451-109">Proteger la aplicación con las clases y anotaciones de Spring Boot</span><span class="sxs-lookup"><span data-stu-id="fb451-109">Secure the application with Spring Boot classes and annotations</span></span>
> * <span data-ttu-id="fb451-110">Compilar y probar la aplicación de Java</span><span class="sxs-lookup"><span data-stu-id="fb451-110">Build and test your Java application</span></span>

<span data-ttu-id="fb451-111">Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de empezar.</span><span class="sxs-lookup"><span data-stu-id="fb451-111">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fb451-112">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="fb451-112">Prerequisites</span></span>

<span data-ttu-id="fb451-113">Los siguientes requisitos previos son necesarios para seguir los pasos descritos en este artículo:</span><span class="sxs-lookup"><span data-stu-id="fb451-113">The following prerequisites are required in order to complete the steps in this article:</span></span>

* <span data-ttu-id="fb451-114">Un kit de desarrollo de Java (JDK) admitido</span><span class="sxs-lookup"><span data-stu-id="fb451-114">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="fb451-115">Para más información sobre los JDK disponibles para desarrollar en Azure, consulte <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="fb451-115">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="fb451-116">[Apache Maven](http://maven.apache.org/), versión 3.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="fb451-116">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-an-app-using-spring-initializr"></a><span data-ttu-id="fb451-117">Creación de una aplicación con Spring Initialzr</span><span class="sxs-lookup"><span data-stu-id="fb451-117">Create an app using Spring Initializr</span></span>

1. <span data-ttu-id="fb451-118">Vaya a <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="fb451-118">Browse to <https://start.spring.io/>.</span></span>

2. <span data-ttu-id="fb451-119">Especifique que desea generar un proyecto de **Maven** con **Java**, escriba los nombres de **Grupo** y **Artefacto** de la aplicación y, a continuación, seleccione el módulo **Web** y **Seguridad** de Spring Initializr.</span><span class="sxs-lookup"><span data-stu-id="fb451-119">Specify that you want to generate a **Maven** project with **Java**, enter the **Group** and **Artifact** names for your application, and then select the **Web** and **Security** module of the Spring Initializr.</span></span>

   ![Especificar los nombres de grupo y artefacto](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/SI.png)


3. <span data-ttu-id="fb451-121">Haga clic en `Generate Project` y, cuando se le solicite, descargue el proyecto en una ruta de acceso del equipo local.</span><span class="sxs-lookup"><span data-stu-id="fb451-121">Click `Generate Project`, download the project to a path on your local computer when prompted.</span></span>

## <a name="create-azure-active-directory-instance"></a><span data-ttu-id="fb451-122">Creación de una instancia de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fb451-122">Create Azure Active Directory instance</span></span>

### <a name="create-the-active-directory-instance"></a><span data-ttu-id="fb451-123">Creación de la instancia de Active Directory</span><span class="sxs-lookup"><span data-stu-id="fb451-123">Create the Active Directory instance</span></span>

1. <span data-ttu-id="fb451-124">Inicie sesión en <https://portal.azure.com>.</span><span class="sxs-lookup"><span data-stu-id="fb451-124">Log into <https://portal.azure.com>.</span></span>

2. <span data-ttu-id="fb451-125">Haga clic en **+Crear un recurso**, luego en **Identidad** y, por último, en **Azure Active Directory B2C**.</span><span class="sxs-lookup"><span data-stu-id="fb451-125">Click **+Create a resource**, then **Identity**, and then **Azure Active Directory B2C**.</span></span>

   ![Creación de una nueva instancia de Azure Active Directory B2C](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/AZ1.png)

3. <span data-ttu-id="fb451-127">Escriba el **Nombre de la organización** y el **Nombre de dominio inicial**, registre el **nombre de dominio** como su `${your-tenant-name}` y haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="fb451-127">Enter your **Organization name** and your **Initial domain name**, record the **domain name** as your `${your-tenant-name}` and click **Create**.</span></span>

   ![Obtención del nombre del inquilino de B2C](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/AZ5.png)

4. <span data-ttu-id="fb451-129">Seleccione el nombre de cuenta en la parte superior derecha de la barra de herramientas de Azure Portal y haga clic en **Cambiar directorio**.</span><span class="sxs-lookup"><span data-stu-id="fb451-129">Select your account name on the top-right of the Azure portal toolbar, then click **Switch directory**.</span></span>

   ![Selección de la instancia de Azure Active Directory](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/AZ2.png)

5. <span data-ttu-id="fb451-131">Seleccione la nueva instancia de Azure Active Directory en el menú desplegable.</span><span class="sxs-lookup"><span data-stu-id="fb451-131">Select your new Azure Active Directory from the drop-down menu.</span></span>

   ![Selección de la instancia de Azure Active Directory](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/AZ3.png)

6. <span data-ttu-id="fb451-133">Busque `b2c` y haga clic en el servicio `Azure AD B2C`.</span><span class="sxs-lookup"><span data-stu-id="fb451-133">Search `b2c` and click `Azure AD B2C` service.</span></span>

   ![Búsqueda de la instancia de Azure Active Directory B2C](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/AZ4.png)

### <a name="add-an-application-registration-for-your-spring-boot-app"></a><span data-ttu-id="fb451-135">Adición de un registro de aplicación para la aplicación de Spring Boot</span><span class="sxs-lookup"><span data-stu-id="fb451-135">Add an application registration for your Spring Boot app</span></span>

1. <span data-ttu-id="fb451-136">Seleccione **Azure AD B2C** desde el menú del portal, haga clic en **Aplicaciones** y, a continuación, haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="fb451-136">Select **Azure AD B2C** from the portal menu, click **Applications**, and then click **Add**.</span></span>

   ![Adición de un nuevo registro de aplicaciones](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/B2C1.png)

2. <span data-ttu-id="fb451-138">Especifique el **Nombre** de la aplicación, agregue `http://localhost:8080/home` a la **Dirección URL de respuesta**, registre el **Identificador de aplicación** como su `${your-client-id}` y, a continuación, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="fb451-138">Specify your application **Name**, add `http://localhost:8080/home` for the **Reply URL**, record the **Application ID** as your `${your-client-id}` and then click **Save**.</span></span>

   ![Agregar dirección URL de respuesta de la aplicación](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/B2C2.png)

3. <span data-ttu-id="fb451-140">Seleccione **Claves** en la aplicación, haga clic en **Generar clave** para generar `${your-client-secret}` y, a continuación, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="fb451-140">Select **Keys** from your application, click **Generate key** to generate `${your-client-secret}` and then **Save**.</span></span>

4. <span data-ttu-id="fb451-141">Seleccione **Flujos de usuario** a la izquierda y, a continuación, **haga clic en** **Nuevo flujo de usuario**.</span><span class="sxs-lookup"><span data-stu-id="fb451-141">Select **User flows** on your left, and then **Click** \*\*New user flow \*\*.</span></span>

   ![Creación del flujo de usuario](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/B2C3.png)

5. <span data-ttu-id="fb451-143">Elija **Registrarse** o en **Edición de perfiles** y **Restablecimiento de contraseña** para crear flujos de usuario, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="fb451-143">Choose **Sign up or in**, **Profile editing** and **Password reset** to create user flows respectively.</span></span> <span data-ttu-id="fb451-144">Especifique el **Nombre** del flujo de usuario y los **Atributos y notificaciones de usuario** y haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="fb451-144">Specify your user flow **Name** and **User attributes and claims**, click **Create**.</span></span>

   ![Configuración del flujo de usuario](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/B2C4.png)

## <a name="configure-and-compile-your-app"></a><span data-ttu-id="fb451-146">Configuración y compilación de la aplicación</span><span class="sxs-lookup"><span data-stu-id="fb451-146">Configure and compile your app</span></span>

1. <span data-ttu-id="fb451-147">Extraiga los archivos del proyecto que creó y descargó en un directorio anteriormente en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="fb451-147">Extract the files from the project archive you created and downloaded earlier in this tutorial into a directory.</span></span>

2. <span data-ttu-id="fb451-148">Vaya a la carpeta principal del proyecto y abra el archivo del proyecto de Maven `pom.xml` en un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="fb451-148">Navigate to the parent folder for your project, and open the `pom.xml` Maven project file in a text editor.</span></span>

3. <span data-ttu-id="fb451-149">Agregue las dependencias para la seguridad OAuth2 de Spring a `pom.xml`:</span><span class="sxs-lookup"><span data-stu-id="fb451-149">Add the dependencies for Spring OAuth2 security to the `pom.xml`:</span></span>

   ```xml
   <dependency>
       <groupId>com.microsoft.azure</groupId>
       <artifactId>azure-active-directory-b2c-spring-boot-starter</artifactId>
       <version>2.1.6.M2</version>
   </dependency>
   <dependency>
       <groupId>org.springframework.boot</groupId>
       <artifactId>spring-boot-starter-thymeleaf</artifactId>
   </dependency>
   <dependency>
       <groupId>org.thymeleaf.extras</groupId>
       <artifactId>thymeleaf-extras-springsecurity5</artifactId>
   </dependency>
   ```

4. <span data-ttu-id="fb451-150">Guarde y cierre el archivo *pom.xml*.</span><span class="sxs-lookup"><span data-stu-id="fb451-150">Save and close the *pom.xml* file.</span></span>

5. <span data-ttu-id="fb451-151">Vaya a la carpeta *src/main/resources* del proyecto y abra el archivo *application.yml* en un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="fb451-151">Navigate to the *src/main/resources* folder in your project and open the *application.yml* file in a text editor.</span></span>

6. <span data-ttu-id="fb451-152">Especifique la configuración del registro de su aplicación con los valores que creó anteriormente; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="fb451-152">Specify the settings for your app registration using the values you created earlier; for example:</span></span>

   ```yaml
   azure:
     activedirectory:
       b2c:
         tenant: ${your-tenant-name}
         client-id: ${your-client-id}
         client-secret: ${your-client-secret}
         reply-url: ${your-reply-url-from-aad} # should be absolute url.
         logout-success-url: ${you-logout-success-url}
         user-flows:
           sign-up-or-sign-in: ${your-sign-up-or-in-user-flow}
           profile-edit: ${your-profile-edit-user-flow}     # optional
           password-reset: ${your-password-reset-user-flow} # optional
   ```
   <span data-ttu-id="fb451-153">Donde:</span><span class="sxs-lookup"><span data-stu-id="fb451-153">Where:</span></span>

   | <span data-ttu-id="fb451-154">Parámetro</span><span class="sxs-lookup"><span data-stu-id="fb451-154">Parameter</span></span> | <span data-ttu-id="fb451-155">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="fb451-155">Description</span></span> |
   |---|---|
   | `azure.activedirectory.b2c.tenant` | <span data-ttu-id="fb451-156">Contiene el valor de `${your-tenant-name` de AD B2C anterior.</span><span class="sxs-lookup"><span data-stu-id="fb451-156">Contains your AD B2C's `${your-tenant-name` from earlier.</span></span> |
   | `azure.activedirectory.b2c.client-id` | <span data-ttu-id="fb451-157">Contiene el valor de `${your-client-id}` de la aplicación que completó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="fb451-157">Contains the `${your-client-id}` from your application that you completed earlier.</span></span> |
   | `azure.activedirectory.b2c.client-secret` | <span data-ttu-id="fb451-158">Contiene el valor de `${your-client-secret}` de la aplicación que completó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="fb451-158">Contains the `${your-client-secret}` from your application that you completed earlier.</span></span> |
   | `azure.activedirectory.b2c.reply-url` | <span data-ttu-id="fb451-159">Contiene uno de los valores de **Dirección URL de respuesta** de la aplicación que se completaron anteriormente.</span><span class="sxs-lookup"><span data-stu-id="fb451-159">Contains one of the **Reply URL** from your application that you completed earlier.</span></span> |
   | `azure.activedirectory.b2c.logout-success-url` | <span data-ttu-id="fb451-160">Especifique la dirección URL cuando se cierra la sesión de la aplicación correctamente.</span><span class="sxs-lookup"><span data-stu-id="fb451-160">Specify the URL when your application logout successfully.</span></span> |
   | `azure.activedirectory.b2c.user-flows` | <span data-ttu-id="fb451-161">Contiene el nombre de los flujos de usuario que se completaron anteriormente.</span><span class="sxs-lookup"><span data-stu-id="fb451-161">Contains the name of the user flows that you completed earlier.</span></span>

   > [!NOTE]
   > 
   > <span data-ttu-id="fb451-162">Para obtener una lista completa de los valores disponibles en el archivo *application.yml*, consulte el [Ejemplo de Spring Boot de Azure Active Directory B2C][Ejemplo de Spring Boot de AAD B2C] en GitHub.</span><span class="sxs-lookup"><span data-stu-id="fb451-162">For a full list of values that are available in your *application.yml* file, see the [Azure Active Directory B2C Spring Boot Sample][AAD B2C Spring Boot Sample] on GitHub.</span></span>
   >

7. <span data-ttu-id="fb451-163">Guarde y cierre el archivo *application.yml*.</span><span class="sxs-lookup"><span data-stu-id="fb451-163">Save and close the *application.yml* file.</span></span>

8. <span data-ttu-id="fb451-164">Cree una carpeta llamada *controller* en la carpeta de fuentes de Java de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="fb451-164">Create a folder named *controller* in the Java source folder for your application.</span></span>

9. <span data-ttu-id="fb451-165">Cree un archivo de Java nuevo llamado *HelloController.java* en la carpeta *controller* y ábralo en un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="fb451-165">Create a new Java file named *HelloController.java* in the *controller* folder and open it in a text editor.</span></span>

10. <span data-ttu-id="fb451-166">Escriba el código siguiente, guarde el archivo y ciérrelo:</span><span class="sxs-lookup"><span data-stu-id="fb451-166">Enter the following code, then save and close the file:</span></span>

    ```java
    package sample.aad.controller;
    
    import org.springframework.security.oauth2.client.authentication.OAuth2AuthenticationToken;
    import org.springframework.security.oauth2.core.user.OAuth2User;
    import org.springframework.stereotype.Controller;
    import org.springframework.ui.Model;
    import org.springframework.web.bind.annotation.GetMapping;
    
    @Controller
    public class WebController {
    
        private void initializeModel(Model model, OAuth2AuthenticationToken token) {
            if (token != null) {
                final OAuth2User user = token.getPrincipal();
    
                model.addAttribute("grant_type", user.getAuthorities());
                model.addAllAttributes(user.getAttributes());
            }
        }
    
        @GetMapping(value = "/")
        public String index(Model model, OAuth2AuthenticationToken token) {
            initializeModel(model, token);
    
            return "home";
        }
    
        @GetMapping(value = "/greeting")
        public String greeting(Model model, OAuth2AuthenticationToken token) {
            initializeModel(model, token);
    
            return "greeting";
        }
    
        @GetMapping(value = "/home")
        public String home(Model model, OAuth2AuthenticationToken token) {
            initializeModel(model, token);
    
            return "home";
        }
    }
    ```

11. <span data-ttu-id="fb451-167">Cree una carpeta llamada *security* en la carpeta de fuentes de Java de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="fb451-167">Create a folder named *security* in the Java source folder for your application.</span></span>

12. <span data-ttu-id="fb451-168">Cree un archivo Java nuevo llamado *WebSecurityConfig.java* en la carpeta *security* y ábralo en un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="fb451-168">Create a new Java file named *WebSecurityConfig.java* in the *security* folder and open it in a text editor.</span></span>

13. <span data-ttu-id="fb451-169">Escriba el código siguiente, guarde el archivo y ciérrelo:</span><span class="sxs-lookup"><span data-stu-id="fb451-169">Enter the following code, then save and close the file:</span></span>

    ```java
    package sample.aad.security;
    
    import com.microsoft.azure.spring.autoconfigure.b2c.AADB2COidcLoginConfigurer;
    import org.springframework.security.config.annotation.web.builders.HttpSecurity;
    import org.springframework.security.config.annotation.web.configuration.EnableWebSecurity;
    import org.springframework.security.config.annotation.web.configuration.WebSecurityConfigurerAdapter;
    
    @EnableWebSecurity
    public class WebSecurityConfiguration extends WebSecurityConfigurerAdapter {
    
        private final AADB2COidcLoginConfigurer configurer;
    
        public WebSecurityConfiguration(AADB2COidcLoginConfigurer configurer) {
            this.configurer = configurer;
        }
    
        @Override
        protected void configure(HttpSecurity http) throws Exception {
            http
                    .authorizeRequests()
                    .anyRequest()
                    .authenticated()
                    .and()
                    .apply(configurer)
            ;
        }
    }
    ```
14. <span data-ttu-id="fb451-170">Copie `greeting.html` y `home.html` desde [Ejemplo de Spring Boot de Azure AD B2C](https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-active-directory-b2c-oidc-spring-boot-sample/src/main/resources/templates) y reemplace `${your-profile-edit-user-flow}` y `${your-password-reset-user-flow}` por el nombre de flujo de usuario respectivamente que se completaron anteriormente.</span><span class="sxs-lookup"><span data-stu-id="fb451-170">Copy the `greeting.html` and `home.html` from [Azure AD B2C Spring Boot Sample](https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-active-directory-b2c-oidc-spring-boot-sample/src/main/resources/templates), and replace the `${your-profile-edit-user-flow}` and `${your-password-reset-user-flow}` with your user flow name respectively that completed earlier.</span></span>

## <a name="build-and-test-your-app"></a><span data-ttu-id="fb451-171">Compilación y prueba de la aplicación</span><span class="sxs-lookup"><span data-stu-id="fb451-171">Build and test your app</span></span>

1. <span data-ttu-id="fb451-172">Abra un símbolo del sistema y cambie el directorio a la carpeta donde se encuentra el archivo *pom.xml* de su aplicación.</span><span class="sxs-lookup"><span data-stu-id="fb451-172">Open a command prompt and change directory to the folder where your app's *pom.xml* file is located.</span></span>

2. <span data-ttu-id="fb451-173">Compile la aplicación de Spring Boot con Maven y ejecútela; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="fb451-173">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

3. <span data-ttu-id="fb451-174">Después de que Maven compile e inicie la aplicación, abra <http://localhost:8080/> en un explorador web; se le redirigirá a la página de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="fb451-174">After your application is built and started by Maven, open <http://localhost:8080/> in a web browser; you should be redirected to login page.</span></span>

   ![Página de inicio de sesión](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/LO1.png)

4. <span data-ttu-id="fb451-176">Haga clic en el vínculo con el nombre del flujo de usuario `${your-sign-up-or-in}`, que le debería redirigir a Azure AD B2C para iniciar el proceso de autenticación.</span><span class="sxs-lookup"><span data-stu-id="fb451-176">Click linke with name of `${your-sign-up-or-in}` user flow, you should be rediected Azure AD B2C to start the authentication process.</span></span>

   ![Inicio de sesión de Azure AD B2C](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/LO2.png)

4. <span data-ttu-id="fb451-178">Una vez que haya iniciado sesión correctamente, debería ver el ejemplo `home page` desde el explorador,</span><span class="sxs-lookup"><span data-stu-id="fb451-178">After you have logged in successfully, you should see the sample `home page` from the browser,</span></span>

   ![Inicio de sesión correcto](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/LO3.png)

## <a name="summary"></a><span data-ttu-id="fb451-180">Resumen</span><span class="sxs-lookup"><span data-stu-id="fb451-180">Summary</span></span>

<span data-ttu-id="fb451-181">En este tutorial, ha creado una nueva aplicación web de Java mediante el iniciador de Azure Active Directory B2C, ha configurado un nuevo inquilino de Azure AD B2C y ha registrado una nueva aplicación en él; después, ha configurado la aplicación para que use las clases y anotaciones de Spring para proteger la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="fb451-181">In this tutorial, you created a new Java web application using the Azure Active Directory B2C starter, configured a new Azure AD B2C tenant and registered a new application in it, and then configured your application to use the Spring annotations and classes to protect the web app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fb451-182">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fb451-182">Next steps</span></span>

<span data-ttu-id="fb451-183">Para más información acerca de Spring y Azure, vaya al centro de documentación de Azure.</span><span class="sxs-lookup"><span data-stu-id="fb451-183">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="fb451-184">Spring en Azure</span><span class="sxs-lookup"><span data-stu-id="fb451-184">Spring on Azure</span></span>](/java/azure/spring-framework)
