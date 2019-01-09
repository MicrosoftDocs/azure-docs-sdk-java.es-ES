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
ms.date: 12/19/2018
ms.devlang: java
ms.service: active-directory
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: identity
ms.openlocfilehash: b3d97917deffa75bfab5f0d9ded64affd90139e1
ms.sourcegitcommit: f0f140b0862ca5338b1b7e5c33cec3e58a70b8fd
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/03/2019
ms.locfileid: "53991399"
---
# <a name="tutorial-secure-a-java-web-app-using-the-spring-boot-starter-for-azure-active-directory"></a>Tutorial: Protección de una aplicación web de Java con la utilidad Spring Boot Starter para Azure Active Directory

## <a name="overview"></a>Información general

En este artículo, se muestra cómo crear una aplicación de Java con **[Spring Initializr]**, que usa la funcionalidad Spring Boot Starter para Azure Active Directory (Azure AD).

En este tutorial, aprenderá a:

> [!div class="checklist"]
> * Crear una aplicación de Java mediante Spring Initializr
> * Configurar Azure Active Directory
> * Proteger la aplicación con las clases y anotaciones de Spring Boot
> * Compilar y probar la aplicación de Java

Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de empezar.

## <a name="prerequisites"></a>Requisitos previos

Los siguientes requisitos previos son necesarios para seguir los pasos descritos en este artículo:

* Un kit de desarrollo de Java (JDK) admitido Para más información sobre los JDK disponibles para desarrollar en Azure, consulte <https://aka.ms/azure-jdks>.
* [Apache Maven](http://maven.apache.org/), versión 3.0 o posterior.

## <a name="create-an-app-using-spring-initializr"></a>Creación de una aplicación con Spring Initialzr

1. Vaya a <https://start.spring.io/>.

1. Especifique que desea generar un proyecto de **Maven** con **Java**, escriba los nombres de **Group** (Grupo) y **Artifact** (Artefacto) de su aplicación y luego haga clic en el vínculo **Switch to the full version** (Cambiar a la versión completa) de Spring Initializr.

   ![Especificar los nombres de grupo y artefacto][create-spring-app-01]

1. Vaya a la sección **Core** y active la casilla **Security** (Seguridad) y, en la sección **Web**, active la casilla **Web**. Después, baje a la sección **Azure** y active la casilla **Azure Active Directory**.

   ![Selección de los iniciadores Security, Web y Azure Active Directory][create-spring-app-02]

1. Desplácese a la parte inferior o superior de la página y haga clic en el botón **Generate Project** (Generar proyecto).

   ![Generación del proyecto de Spring Boot][create-spring-app-03]

1. Cuando se le solicite, descargue el proyecto en una ruta de acceso del equipo local.

## <a name="create-azure-active-directory-instance"></a>Creación de una instancia de Azure Active Directory

### <a name="create-the-active-directory-instance"></a>Creación de la instancia de Active Directory

1. Inicie sesión en <https://portal.azure.com>.

1. Haga clic en **+Crear un recurso**, luego en **Identidad** y, por último, en **Azure Active Directory**.

   ![Creación de una nueva instancia de Azure Active Directory][create-directory-01]

1. Rellene los campos **Nombre de la organización** y **Nombre de dominio inicial**. Copie la dirección URL completa del directorio; se usará para agregar cuentas de usuario más adelante en este tutorial. (Por ejemplo, `wingtiptoysdirectory.onmicrosoft.com`). Cuando haya terminado, haga clic en **Crear**.

   ![Especificación de los nombres de Azure Active Directory][create-directory-02]

1. Seleccione el nombre de cuenta en la parte superior derecha de la barra de herramientas de Azure Portal y haga clic en **Cambiar directorio**.

   ![Seleccione el nombre de su cuenta de Azure.][create-directory-03]

1. Seleccione la nueva instancia de Azure Active Directory en el menú desplegable.

   ![Selección de la instancia de Azure Active Directory][create-directory-04]

1. Seleccione **Azure Active Directory** en el menú del portal, haga clic en **Propiedades** y copie el **Id. de directorio**; este valor se usará más adelante para configurar el archivo *application.properties* más adelante en este tutorial.

   ![Copia del identificador de Azure Active Directory][create-directory-05]

### <a name="add-an-application-registration-for-your-spring-boot-app"></a>Adición de un registro de aplicación para la aplicación de Spring Boot

1. Seleccione **Azure Active Directory** en el menú del portal, haga clic en **Registros de aplicaciones** y haga clic en **Nuevos registros de aplicaciones**.

   ![Adición de un nuevo registro de aplicaciones][create-app-registration-01]

2. Especifique el valor de **Nombre** de la aplicación, use http://localhost:8080 como **URL de inicio de sesión** y, por último, haga clic en **Crear**.

   ![Crear registro de aplicaciones][create-app-registration-02]

4. Cuando aparezca la página para registrar la aplicación, copie su **Id. de aplicación**; usará este valor para configurar el archivo *application.properties* más adelante en este tutorial. Haga clic en **Configuración** y después en **Claves**.

   ![Creación de las claves del registro de aplicaciones][create-app-registration-03]

5. Agregue una **Descripción**, especifique la **Duración** de la nueva clave y haga clic en **Guardar**; el valor de la clave se rellenará automáticamente al hacer clic en el icono **Guardar**, y tendrá que copiar el valor de la clave para configurar el archivo *application.properties* más adelante en este tutorial. (No podrá recuperar este valor más adelante).

   ![Especificación de los parámetros de clave del registro de aplicaciones][create-app-registration-04]

6. En la página principal del registro de aplicaciones, haga clic en **Configuración** y **Permisos necesarios**.

   ![Permisos necesarios del registro de aplicaciones][create-app-registration-05]

7. Haga clic en **Microsoft Azure Active Directory**.

   ![Selección de Microsoft Azure Active Directory][create-app-registration-06]

8. Active las casillas **Acceder al directorio como usuario con sesión iniciada** y **Iniciar sesión y leer el perfil del usuario**, y haga clic en **Guardar**.

   ![Habilitar los permisos de acceso][create-app-registration-07]

9. En la página **Permisos necesarios**, haga clic en **Conceder permisos** y responda **Sí** a la pregunta.

   ![Concesión de permisos de acceso][create-app-registration-08]

10. En la página principal del registro de aplicación, haga clic en **Configuración** y, a continuación, haga clic en **URL de respuesta**.

    ![Edición de las URL de respuesta][create-app-registration-09]

11. Escriba "<http://localhost:8080/login/oauth2/code/azure>" como nueva dirección URL de respuesta y haga clic en **Guardar**.

    ![Adición de una nueva URL de respuesta][create-app-registration-10]

12. En la página principal para el registro de aplicación, haga clic en **Manifiesto**, establezca el valor del parámetro `oauth2AllowImplicitFlow` en `true` y, a continuación, haga clic en **Guardar**.

    ![Configuración del manifiesto de aplicación][create-app-registration-11]

    > [!NOTE]
    > 
    > Para más información acerca del parámetro `oauth2AllowImplicitFlow` y otras opciones de configuración de la aplicación, consulte [Manifiesto de aplicación de Azure Active Directory][AAD app manifest]. 
    >

### <a name="add-a-user-account-to-your-directory-and-add-that-account-to-a-group"></a>Adición de una cuenta de usuario al directorio y adición de esa cuenta a un grupo

1. En la página **Información general** de Active Directory, haga clic en **Todos los usuarios** y en **Nuevo usuario**.

   ![Agregar una nueva cuenta de usuario][create-user-01]

1. Cuando se muestre el panel **Usuario**, escriba **Nombre** y el **Nombre de usuario**.

   ![Especificar la información de la cuenta de usuario][create-user-02]

   > [!NOTE]
   > 
   > Al escribir el nombre de usuario, debe especificar la misma dirección URL del directorio que usamos anteriormente en este tutorial; por ejemplo:
   >
   > `wingtipuser@wingtiptoysdirectory.onmicrosoft.com`
   > 

1. Haga clic en **Grupos**, seleccione los grupos que usará para autorización en la aplicación y, a continuación, haga clic en **Seleccionar**. (Para este tutorial, agregue la cuenta al grupo _Usuarios_).

   ![Seleccionar los grupos del usuario][create-user-03]

1. Haga clic en **Mostrar contraseña** y copie la contraseña; se usará para iniciar sesión en la aplicación más adelante en este tutorial. Cuando haya copiado la contraseña, haga clic en **Crear** para agregar la nueva cuenta de usuario al directorio.

   ![Mostrar la contraseña][create-user-04]

## <a name="configure-and-compile-your-app"></a>Configuración y compilación de la aplicación

1. Extraiga los archivos del proyecto que creó y descargó en un directorio anteriormente en este tutorial.

1. Vaya a la carpeta principal del proyecto y abra el archivo del proyecto de Maven `pom.xml` en un editor de texto.

1. Agregue las dependencias para la seguridad OAuth2 de Spring a `pom.xml`:

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

1. Guarde y cierre el archivo *pom.xml*.

1. Vaya a la carpeta *src/main/resources* del proyecto y abra el archivo *application.properties* en un editor de texto.

1. Especifique la configuración del registro de su aplicación con los valores que creó anteriormente; por ejemplo:

   ```yaml
   # Specifies your Active Directory ID:
   azure.activedirectory.tenant-id=22222222-2222-2222-2222-222222222222

   # Specifies your App Registration's Application ID:
   spring.security.oauth2.client.registration.azure.client-id=11111111-1111-1111-1111-1111111111111111

   # Specifies your App Registration's secret key:
   spring.security.oauth2.client.registration.azure.client-secret=AbCdEfGhIjKlMnOpQrStUvWxYz==

   # Specifies the list of Active Directory groups to use for authorization:
   azure.activedirectory.active-directory-groups=Users
   ```
   Donde:

   | Parámetro | DESCRIPCIÓN |
   |---|---|
   | `azure.activedirectory.tenant-id` | Contiene su **Id. de directorio** de Active Directory obtenido anteriormente. |
   | `spring.security.oauth2.client.registration.azure.client-id` | Contiene el **Id. de aplicación** del registro de aplicaciones que completó anteriormente. |
   | `spring.security.oauth2.client.registration.azure.client-secret` | Contiene el **Valor** de la clave del registro de aplicaciones que completó anteriormente. |
   | `azure.activedirectory.active-directory-groups` | Contiene una lista de los grupos de Active Directory que se usarán para la autorización. |

   > [!NOTE]
   > 
   > Para obtener una lista completa de los valores disponibles en su archivo *application.properties*, consulte el [ejemplo de Azure Active Directory Spring Boot][AAD Spring Boot Sample] en GitHub.
   >

1. Guarde y cierre el archivo *application.properties*.

1. Cree una carpeta llamada *controller* en la carpeta src de Java para su aplicación; por ejemplo: *src/main/java/com/wingtiptoys/security/controller*.

1. Cree un archivo de Java nuevo llamado *HelloController.java* en la carpeta *controller* y ábralo en un editor de texto.

1. Escriba el código siguiente, guarde el archivo y ciérrelo:

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
   > Puede especificar una configuración de autorización diferente para diferentes asignaciones de solicitudes; por ejemplo:
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

1. Cree una carpeta llamada *security* en la carpeta src de Java para su aplicación; por ejemplo: *src/main/java/com/wingtiptoys/security/security*.

1. Cree un archivo Java nuevo llamado *WebSecurityConfig.java* en la carpeta *security* y ábralo en un editor de texto.

1. Escriba el código siguiente, guarde el archivo y ciérrelo:

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

   > [!NOTE]
   > 
   > Se le pedirá que cambie su contraseña si es el primer inicio de sesión de una cuenta de usuario nueva.
   > 
   > ![Cambiar la contraseña][update-password]
   > 

1. Cuando haya iniciado sesión correctamente, verá ver el texto de ejemplo "Hello World" desde el controlador.

   ![Inicio de sesión correcto][hello-world]

   > [!NOTE]
   > 
   > Las cuentas de usuario que no están autorizadas recibirán un mensaje **HTTP 403 No autorizado**.
   >

## <a name="summary"></a>Resumen

En este tutorial, ha creado una nueva aplicación web de Java mediante el iniciador de Azure Active Directory, ha configurado un nuevo inquilino de Azure AD y ha registrado una nueva aplicación en él; después, ha configurado la aplicación para que use las clases y anotaciones de Spring para proteger la aplicación web.

## <a name="next-steps"></a>Pasos siguientes

Para más información acerca de Spring y Azure, vaya al centro de documentación de Azure.

> [!div class="nextstepaction"]
> [Spring en Azure](/java/azure/spring-framework)

<!-- URL List -->

[Azure Active Directory Documentation]: /azure/active-directory/
[AAD app manifest]: /azure/active-directory/develop/active-directory-application-manifest
[Get started with Azure AD]: /azure/active-directory/get-started-azure-ad
[Azure for Java Developers]: /java/azure/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Working with Azure DevOps and Java]: /azure/devops/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/
[AAD Spring Boot Sample]: https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-active-directory-spring-boot-backend-sample

<!-- IMG List -->

[create-spring-app-01]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-spring-app-01.png
[create-spring-app-02]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-spring-app-02.png
[create-spring-app-03]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-spring-app-03.png

[create-directory-01]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-directory-01.png
[create-directory-02]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-directory-02.png
[create-directory-03]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-directory-03.png
[create-directory-04]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-directory-04.png
[create-directory-05]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-directory-05.png

[create-app-registration-01]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-app-registration-01.png
[create-app-registration-02]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-app-registration-02.png
[create-app-registration-03]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-app-registration-03.png
[create-app-registration-04]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-app-registration-04.png
[create-app-registration-05]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-app-registration-05.png
[create-app-registration-06]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-app-registration-06.png
[create-app-registration-07]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-app-registration-07.png
[create-app-registration-08]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-app-registration-08.png
[create-app-registration-09]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-app-registration-09.png
[create-app-registration-10]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-app-registration-10.png
[create-app-registration-11]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-app-registration-11.png

[create-user-01]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-user-01.png
[create-user-02]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-user-02.png
[create-user-03]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-user-03.png
[create-user-04]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-user-04.png

[application-login]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/application-login.png
[build-application]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/build-application.png
[hello-world]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/hello-world.png
[update-password]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/update-password.png
