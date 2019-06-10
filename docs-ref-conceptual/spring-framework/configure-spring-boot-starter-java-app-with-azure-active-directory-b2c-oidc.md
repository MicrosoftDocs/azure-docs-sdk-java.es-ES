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
# <a name="tutorial-secure-a-java-web-app-using-the-spring-boot-starter-for-azure-active-directory-b2c"></a>Tutorial: Protección de una aplicación web de Java con Spring Boot Starter para Azure Active Directory B2C.

## <a name="overview"></a>Información general

En este artículo se muestra cómo crear una aplicación de Java con [Spring Initializr](https://start.spring.io/), que usa Spring Boot Starter para Azure Active Directory (Azure AD).

En este tutorial, aprenderá a:

> [!div class="checklist"]
> * Crear una aplicación de Java mediante Spring Initializr
> * Configurar Azure Active Directory B2C
> * Proteger la aplicación con las clases y anotaciones de Spring Boot
> * Compilar y probar la aplicación de Java

Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de empezar.

## <a name="prerequisites"></a>Requisitos previos

Los siguientes requisitos previos son necesarios para seguir los pasos descritos en este artículo:

* Un kit de desarrollo de Java (JDK) admitido Para más información sobre los JDK disponibles para desarrollar en Azure, consulte <https://aka.ms/azure-jdks>.
* [Apache Maven](http://maven.apache.org/), versión 3.0 o posterior.

## <a name="create-an-app-using-spring-initializr"></a>Creación de una aplicación con Spring Initialzr

1. Vaya a <https://start.spring.io/>.

2. Especifique que desea generar un proyecto de **Maven** con **Java**, escriba los nombres de **Grupo** y **Artefacto** de la aplicación y, a continuación, seleccione el módulo **Web** y **Seguridad** de Spring Initializr.

   ![Especificar los nombres de grupo y artefacto](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/SI.png)


3. Haga clic en `Generate Project` y, cuando se le solicite, descargue el proyecto en una ruta de acceso del equipo local.

## <a name="create-azure-active-directory-instance"></a>Creación de una instancia de Azure Active Directory

### <a name="create-the-active-directory-instance"></a>Creación de la instancia de Active Directory

1. Inicie sesión en <https://portal.azure.com>.

2. Haga clic en **+Crear un recurso**, luego en **Identidad** y, por último, en **Azure Active Directory B2C**.

   ![Creación de una nueva instancia de Azure Active Directory B2C](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/AZ1.png)

3. Escriba el **Nombre de la organización** y el **Nombre de dominio inicial**, registre el **nombre de dominio** como su `${your-tenant-name}` y haga clic en **Crear**.

   ![Obtención del nombre del inquilino de B2C](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/AZ5.png)

4. Seleccione el nombre de cuenta en la parte superior derecha de la barra de herramientas de Azure Portal y haga clic en **Cambiar directorio**.

   ![Selección de la instancia de Azure Active Directory](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/AZ2.png)

5. Seleccione la nueva instancia de Azure Active Directory en el menú desplegable.

   ![Selección de la instancia de Azure Active Directory](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/AZ3.png)

6. Busque `b2c` y haga clic en el servicio `Azure AD B2C`.

   ![Búsqueda de la instancia de Azure Active Directory B2C](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/AZ4.png)

### <a name="add-an-application-registration-for-your-spring-boot-app"></a>Adición de un registro de aplicación para la aplicación de Spring Boot

1. Seleccione **Azure AD B2C** desde el menú del portal, haga clic en **Aplicaciones** y, a continuación, haga clic en **Agregar**.

   ![Adición de un nuevo registro de aplicaciones](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/B2C1.png)

2. Especifique el **Nombre** de la aplicación, agregue `http://localhost:8080/home` a la **Dirección URL de respuesta**, registre el **Identificador de aplicación** como su `${your-client-id}` y, a continuación, haga clic en **Guardar**.

   ![Agregar dirección URL de respuesta de la aplicación](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/B2C2.png)

3. Seleccione **Claves** en la aplicación, haga clic en **Generar clave** para generar `${your-client-secret}` y, a continuación, haga clic en **Guardar**.

4. Seleccione **Flujos de usuario** a la izquierda y, a continuación, **haga clic en** **Nuevo flujo de usuario**.

   ![Creación del flujo de usuario](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/B2C3.png)

5. Elija **Registrarse** o en **Edición de perfiles** y **Restablecimiento de contraseña** para crear flujos de usuario, respectivamente. Especifique el **Nombre** del flujo de usuario y los **Atributos y notificaciones de usuario** y haga clic en **Crear**.

   ![Configuración del flujo de usuario](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/B2C4.png)

## <a name="configure-and-compile-your-app"></a>Configuración y compilación de la aplicación

1. Extraiga los archivos del proyecto que creó y descargó en un directorio anteriormente en este tutorial.

2. Vaya a la carpeta principal del proyecto y abra el archivo del proyecto de Maven `pom.xml` en un editor de texto.

3. Agregue las dependencias para la seguridad OAuth2 de Spring a `pom.xml`:

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

4. Guarde y cierre el archivo *pom.xml*.

5. Vaya a la carpeta *src/main/resources* del proyecto y abra el archivo *application.yml* en un editor de texto.

6. Especifique la configuración del registro de su aplicación con los valores que creó anteriormente; por ejemplo:

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
   Donde:

   | Parámetro | DESCRIPCIÓN |
   |---|---|
   | `azure.activedirectory.b2c.tenant` | Contiene el valor de `${your-tenant-name` de AD B2C anterior. |
   | `azure.activedirectory.b2c.client-id` | Contiene el valor de `${your-client-id}` de la aplicación que completó anteriormente. |
   | `azure.activedirectory.b2c.client-secret` | Contiene el valor de `${your-client-secret}` de la aplicación que completó anteriormente. |
   | `azure.activedirectory.b2c.reply-url` | Contiene uno de los valores de **Dirección URL de respuesta** de la aplicación que se completaron anteriormente. |
   | `azure.activedirectory.b2c.logout-success-url` | Especifique la dirección URL cuando se cierra la sesión de la aplicación correctamente. |
   | `azure.activedirectory.b2c.user-flows` | Contiene el nombre de los flujos de usuario que se completaron anteriormente.

   > [!NOTE]
   > 
   > Para obtener una lista completa de los valores disponibles en el archivo *application.yml*, consulte el [Ejemplo de Spring Boot de Azure Active Directory B2C][Ejemplo de Spring Boot de AAD B2C] en GitHub.
   >

7. Guarde y cierre el archivo *application.yml*.

8. Cree una carpeta llamada *controller* en la carpeta de fuentes de Java de la aplicación.

9. Cree un archivo de Java nuevo llamado *HelloController.java* en la carpeta *controller* y ábralo en un editor de texto.

10. Escriba el código siguiente, guarde el archivo y ciérrelo:

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

11. Cree una carpeta llamada *security* en la carpeta de fuentes de Java de la aplicación.

12. Cree un archivo Java nuevo llamado *WebSecurityConfig.java* en la carpeta *security* y ábralo en un editor de texto.

13. Escriba el código siguiente, guarde el archivo y ciérrelo:

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
14. Copie `greeting.html` y `home.html` desde [Ejemplo de Spring Boot de Azure AD B2C](https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-active-directory-b2c-oidc-spring-boot-sample/src/main/resources/templates) y reemplace `${your-profile-edit-user-flow}` y `${your-password-reset-user-flow}` por el nombre de flujo de usuario respectivamente que se completaron anteriormente.

## <a name="build-and-test-your-app"></a>Compilación y prueba de la aplicación

1. Abra un símbolo del sistema y cambie el directorio a la carpeta donde se encuentra el archivo *pom.xml* de su aplicación.

2. Compile la aplicación de Spring Boot con Maven y ejecútela; por ejemplo:

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

3. Después de que Maven compile e inicie la aplicación, abra <http://localhost:8080/> en un explorador web; se le redirigirá a la página de inicio de sesión.

   ![Página de inicio de sesión](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/LO1.png)

4. Haga clic en el vínculo con el nombre del flujo de usuario `${your-sign-up-or-in}`, que le debería redirigir a Azure AD B2C para iniciar el proceso de autenticación.

   ![Inicio de sesión de Azure AD B2C](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/LO2.png)

4. Una vez que haya iniciado sesión correctamente, debería ver el ejemplo `home page` desde el explorador,

   ![Inicio de sesión correcto](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/LO3.png)

## <a name="summary"></a>Resumen

En este tutorial, ha creado una nueva aplicación web de Java mediante el iniciador de Azure Active Directory B2C, ha configurado un nuevo inquilino de Azure AD B2C y ha registrado una nueva aplicación en él; después, ha configurado la aplicación para que use las clases y anotaciones de Spring para proteger la aplicación web.

## <a name="next-steps"></a>Pasos siguientes

Para más información acerca de Spring y Azure, vaya al centro de documentación de Azure.

> [!div class="nextstepaction"]
> [Spring en Azure](/java/azure/spring-framework)
