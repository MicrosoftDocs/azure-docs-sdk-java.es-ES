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
# <a name="how-to-use-the-spring-boot-starter-for-azure-active-directory"></a>Cómo usar el iniciador de Spring Boot para Azure Active Directory

## <a name="overview"></a>Información general

En este artículo se muestra cómo crear una aplicación con **[Spring Initializr]** que usa la funcionalidad Spring Boot Starter para Azure Active Directory (Azure AD).

## <a name="prerequisites"></a>requisitos previos

Los siguientes requisitos previos son necesarios para seguir los pasos descritos en este artículo:

* Una suscripción de Azure. Si todavía no la tiene, puede activar sus [Ventajas para suscriptores de MSDN] o registrarse para obtener una [cuenta de Azure gratuita].
* Un [kit de desarrollo de Java (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), versión 1.7 o posterior.
* [Apache Maven](http://maven.apache.org/), versión 3.0 o posterior.

## <a name="create-a-custom-application-using-the-spring-initializr"></a>Creación de una aplicación personalizada mediante Spring Initializr

1. Vaya a <https://start.spring.io/>.

1. Especifique que quiere generar un proyecto de **Maven** con **Java**, escriba los nombres de **Group** (Grupo) y **Artifact** (Artefacto) de su aplicación y luego haga clic en el vínculo **Switch to the full version** (Cambiar a la versión completa) de Spring Initializr.

   ![Especificar los nombres de grupo y artefacto][security-01]

1. Vaya a la sección **Core** y active la casilla **Security** (Seguridad); en la sección **Web**, active la casilla **Web**.

   ![Selección de los iniciadores Security y Web][security-02]

1. Vaya a la sección **Azure** y active la casilla **Azure Active Directory**.

   ![Seleccionar el iniciador Azure Active Directory][security-03]

1. Desplácese a la parte inferior de la página y haga clic en el botón **Generate Project** (Generar proyecto).

   ![Generación del proyecto de Spring Boot][security-04]

1. Cuando se le solicite, descargue el proyecto en una ruta de acceso del equipo local.

## <a name="create-and-configure-a-new-azure-active-directory-instance"></a>Creación y configuración de una nueva instancia de Azure Active Directory

### <a name="create-the-active-directory-instance"></a>Creación de la instancia de Active Directory

1. Inicie sesión en <https://portal.azure.com>.

1. Haga clic en **+Nuevo**, luego en **Seguridad e identidad** y, por último, en **Azure Active Directory**.

   ![Creación de una nueva instancia de Azure Active Directory][directory-01]

1. Rellene los campos **Nombre de la organización** y **Nombre de dominio inicial** y haga clic en **Crear**.

   ![Especificación de los nombres de Azure Active Directory][directory-02]

1. Seleccione la nueva instancia de Azure Active Directory en el menú desplegable, en la barra de herramientas superior de Azure Portal.

   ![Selección de la instancia de Azure Active Directory][directory-03]

1. Seleccione **Azure Active Directory** en el menú del portal, haga clic en **Propiedades** y copie el **Id. de directorio** que usará más adelante en este artículo.

   ![Copia del identificador de Azure Active Directory][directory-13]

### <a name="add-an-application-registration-for-your-spring-boot-app"></a>Adición de un registro de aplicación para la aplicación de Spring Boot

1. Seleccione **Azure Active Directory** en el menú del portal, haga clic en **Información general** y haga clic en **Registros de aplicaciones**.

   ![Adición de un nuevo registro de aplicaciones][directory-04]

1. Haga clic en **Nuevo registro de aplicaciones**, especifique el valor de **Nombre de la aplicación**, use http://localhost:8080 como **URL de inicio de sesión** y, por último, haga clic en **Crear**.

   ![Crear registro de aplicaciones][directory-05]

1. Haga clic en su registro de aplicaciones después de crearlo.

   ![Selección del registro de aplicaciones][directory-06]

1. Cuando se muestre la página del registro de aplicaciones, copie el valor de **Id. de aplicación** para más adelante y haga clic en **Configuración** y en **Claves**.

   ![Creación de las claves del registro de aplicaciones][directory-07]

1. Agregue una **Descripción** y especifique la **Duración** de la nueva clave y haga clic en **Guardar**; el valor de la clave se rellenará automáticamente al hacer clic en el icono **Guardar**, y tiene que copiar el valor de la clave para más adelante. (No podrá recuperar este valor más adelante).

   ![Especificación de los parámetros de clave del registro de aplicaciones][directory-08]

1. En la página principal del registro de aplicaciones, haga clic en **Configuración** y **Permisos necesarios**.

   ![Permisos necesarios del registro de aplicaciones][directory-09]

1. Haga clic en **Microsoft Azure Active Directory**.

   ![Selección de Microsoft Azure Active Directory][directory-10]

1. Active las casillas **Acceder al directorio como usuario con sesión iniciada** y **Iniciar sesión y leer el perfil del usuario**, y haga clic en **Guardar**.

   ![Habilitar los permisos de acceso][directory-11]

1. En la página **Permisos necesarios**, haga clic en **Conceder permisos** y responda **Sí** a la pregunta.

   ![Concesión de permisos de acceso][directory-12]

1. En la página principal del registro de aplicación, haga clic en **Configuración** y, a continuación, haga clic en **URL de respuesta**.

   ![Edición de las URL de respuesta][directory-14]

1. Escriba "http://localhost:8080/login/oauth2/code/azure" como nueva dirección URL de respuesta y haga clic en **Guardar**.

   ![Adición de una nueva URL de respuesta][directory-15]

## <a name="configure-and-compile-your-spring-boot-application"></a>Configuración y compilación de la aplicación de Spring Boot

1. Extraiga en un directorio los archivos del archivo de proyecto descargado.

2. Vaya a la carpeta principal del proyecto y abra el archivo *pom.xml* en un editor de texto.

3. Agregue las dependencias para la seguridad OAuth2 de Spring; por ejemplo:

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

4. Guarde y cierre el archivo *pom.xml*.

5. Vaya a la carpeta *src/main/resources* del proyecto y abra el archivo *application.properties* en un editor de texto.

6. Agrege la clave de la cuenta de almacenamiento utilizando los valores obtenidos anteriormente; por ejemplo:

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
   Donde:

   | . | DESCRIPCIÓN |
   |---|---|
   | `azure.activedirectory.tenant-id` | Contiene su **Id. de directorio** de Active Directory obtenido anteriormente. |
   | `spring.security.oauth2.client.registration.azure.client-id` | Contiene el **Id. de aplicación** del registro de aplicaciones que completó anteriormente. |
   | `spring.security.oauth2.client.registration.azure.client-secret` | Contiene el **Valor** de la clave del registro de aplicaciones que completó anteriormente. |
   | `azure.activedirectory.active-directory-groups` | Contiene una lista de los grupos de Active Directory que se usarán para la autenticación. |

   > [!NOTE]
   > 
   > Para obtener una lista completa de los valores disponibles en su archivo *application.properties*, consulte el [ejemplo de Azure Active Directory Spring Boot][AAD Spring Boot Sample] en GitHub.
   >

7. Guarde y cierre el archivo *application.properties*.

8. Cree una carpeta llamada *controller* en la carpeta src de Java para su aplicación; por ejemplo: *src/main/java/com/wingtiptoys/security/controller*.

9. Cree un archivo de Java nuevo llamado *HelloController.java* en la carpeta *controller* y ábralo en un editor de texto.

10. Escriba el código siguiente, guarde el archivo y ciérrelo:

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
   > El nombre del grupo que especifique para el método `@PreAuthorize("hasRole('')")` debe contener uno de los grupos que especificó en el campo `azure.activedirectory.active-directory-groups` del archivo *application.properties*.
   >

   > [!NOTE]
   > 
   > Puede especificar una configuración de autorización diferente para la asignación de solicitudes; por ejemplo:
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

11. Cree una carpeta llamada *security* en la carpeta src de Java para su aplicación; por ejemplo: *src/main/java/com/wingtiptoys/security/security*.

12. Cree un archivo Java nuevo llamado *WebSecurityConfig.java* en la carpeta *security* y ábralo en un editor de texto.

13. Escriba el código siguiente, guarde el archivo y ciérrelo:

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

## <a name="build-and-test-your-app"></a>Compilación y prueba de la aplicación

1. Abra un símbolo del sistema y cambie el directorio a la carpeta donde se encuentra el archivo *pom.xml* de su aplicación.

1. Compile la aplicación de Spring Boot con Maven y ejecútela; por ejemplo:

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

   ![Compilación de la aplicación][build-application]

1. Después de que Maven compile e inicie la aplicación, abra <http://localhost:8080> en un explorador web; se le pedirá un nombre de usuario y una contraseña.

   ![Inicio de sesión en su aplicación][application-login]

1. Cuando haya iniciado sesión correctamente, verá ver el texto de ejemplo "Hello World" desde el controlador.

   ![Inicio de sesión correcto][hello-world]

   > [!NOTE]
   > 
   > Las cuentas de usuario que no están autorizadas recibirán un mensaje **HTTP 403 No autorizado**.
   >

## <a name="next-steps"></a>Pasos siguientes

Para más información acerca de cómo usar Azure Active Directory, consulte los siguientes artículos:

* [Documentación de Azure Active Directory].

Para obtener más información sobre el uso de aplicaciones de Spring Boot en Azure, consulte los siguientes artículos:

* [Implementación de una aplicación de Spring Boot en Azure App Service](deploy-spring-boot-java-web-app-on-azure.md)

* [Ejecución de una aplicación de Spring Boot en un clúster de Kubernetes en Azure Container Service](deploy-spring-boot-java-app-on-kubernetes.md)

Para más información sobre el uso de Azure con Java, consulte [Azure para desarrolladores de Java] y [Herramientas de Java para Visual Studio Team Services] (Herramientas de Java para Visual Studio Team Services).

**[Spring Framework]** es una solución de código abierto que ayuda a los desarrolladores de Java a crear aplicaciones de nivel empresarial. Uno de los proyectos más populares que se basa en esa plataforma es [Spring Boot], que proporciona un enfoque simplificado para crear aplicaciones de Java independientes. Para ayudar a los desarrolladores a empezar con Spring Boot, puede encontrar varios paquetes de ejemplo de Spring Boot en <https://github.com/spring-guides/>. Además de elegir de la lista de proyectos básicos de Spring Boot, el **[Spring Initializr]** ayuda a los desarrolladores en los primeros pasos para crear aplicaciones de Spring Boot personalizadas.

Para obtener un ejemplo más detallado, consulte el [ejemplo de Spring Boot para Azure Active Directory][AAD Spring Boot Sample] en GitHub.

<!-- URL List -->

[Documentación de Azure Active Directory]: /azure/active-directory/
[Get started with Azure AD]: /azure/active-directory/get-started-azure-ad
[Azure para desarrolladores de Java]: https://docs.microsoft.com/java/azure/
[cuenta de Azure gratuita]: https://azure.microsoft.com/pricing/free-trial/
[Herramientas de Java para Visual Studio Team Services]: https://java.visualstudio.com/
[Ventajas para suscriptores de MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
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
