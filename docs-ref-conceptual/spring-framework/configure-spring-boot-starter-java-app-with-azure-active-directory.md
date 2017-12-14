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
# <a name="how-to-use-the-spring-boot-starter-for-azure-active-directory"></a>Cómo usar el iniciador de Spring Boot para Azure Active Directory

## <a name="overview"></a>Información general

En este artículo se muestra cómo crear una aplicación con **[Spring Initializr]** que usa la funcionalidad Spring Boot Starter para Azure Active Directory (Azure AD).

## <a name="prerequisites"></a>Requisitos previos

Los siguientes requisitos previos son necesarios para seguir los pasos descritos en este artículo:

* Una suscripción de Azure. Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN] o registrarse para obtener una [cuenta de Azure gratuita].
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

### <a name="add-an-application-registration-for-your-spring-boot-app"></a>Adición de un registro de aplicación para la aplicación de Spring Boot

1. Seleccione **Azure Active Directory** en el menú del portal, haga clic en **Información general** y haga clic en **Registros de aplicaciones**.

   ![Adición de un nuevo registro de aplicaciones][directory-04]

1. Haga clic en **Nuevo registro de aplicaciones**, especifique el **Nombre** de la aplicación, use http://localhost:8080 como **URL de inicio de sesión** y, por último, haga clic en **Crear**.

   ![Crear registro de aplicaciones][directory-05]

1. Haga clic en su registro de aplicaciones después de crearlo.

   ![Selección del registro de aplicaciones][directory-06]

1. Cuando se muestre la página del registro de aplicaciones, copie el valor de **Id. de aplicación** para más adelante y haga clic en **Claves**.

   ![Creación de las claves del registro de aplicaciones][directory-07]

1. Agregue una **Descripción** y especifique la **Duración** de la nueva clave y haga clic en **Guardar**; el valor de la clave se rellenará automáticamente al hacer clic en el icono **Guardar**, y tiene que copiar el valor de la clave para más adelante. (No podrá recuperar este valor más adelante).

   ![Especificación de los parámetros de clave del registro de aplicaciones][directory-08]

1. En la página principal del registro de aplicaciones, haga clic en **Permisos necesarios**.

   ![Permisos necesarios del registro de aplicaciones][directory-09]

1. Haga clic en **Microsoft Azure Active Directory**.

   ![Selección de Microsoft Azure Active Directory][directory-10]

1. Active las casillas **Acceder al directorio como usuario con sesión iniciada** y **Iniciar sesión y leer el perfil del usuario**, y haga clic en **Guardar**.

   ![Habilitar los permisos de acceso][directory-11]

1. En la página **Permisos necesarios**, haga clic en **Conceder permisos** y responda **Sí** a la pregunta.

   ![Concesión de permisos de acceso][directory-12]

## <a name="configure-and-compile-your-spring-boot-application"></a>Configuración y compilación de la aplicación de Spring Boot

1. Extraiga en un directorio los archivos del archivo de proyecto descargado.

1. Vaya a la carpeta principal del proyecto y abra el archivo *pom.xml* en un editor de texto.

1. Agregue la dependencia para la seguridad OAuth2 de Spring; por ejemplo:

   ```xml
   <dependency>
      <groupId>org.springframework.security.oauth</groupId>
      <artifactId>spring-security-oauth2</artifactId>
   </dependency>
   ```

1. Guarde y cierre el archivo *pom.xml*.

1. Vaya a la carpeta *src/main/resources* del proyecto y abra el archivo *application.properties* en un editor de texto.

1. Agrege la clave de la cuenta de almacenamiento utilizando los valores obtenidos anteriormente; por ejemplo:

   ```yaml
   # Specifies your Active Directory Application ID:
   azure.activedirectory.clientId=11111111-1111-1111-1111-1111111111111111

   # Specifies your secret key:
   azure.activedirectory.clientSecret=AbCdEfGhIjKlMnOpQrStUvWxYz==

   # Specifies the list of Active Directory groups to use for authentication:
   azure.activedirectory.activeDirectoryGroups=Users
   ```
   Donde:
   Parámetro | Descripción
   ---|---|---
   `azure.activedirectory.clientId` | Contiene el **Id. de aplicación** obtenido anteriormente.
   `azure.activedirectory.clientSecret` | Contiene la clave del registro de aplicaciones que completó anteriormente.
   `azure.activedirectory.activeDirectoryGroups` | Contiene una lista de los grupos de Active Directory que se usarán para la autenticación.


1. Guarde y cierre el archivo *application.properties*.

1. Cree una carpeta llamada *controller* en la carpeta src de Java para su aplicación; por ejemplo: *src/main/java/com/wingtiptoys/security/controller*.

1. Cree un archivo de Java nuevo llamado *HelloController.java* en la carpeta *controller* y ábralo en un editor de texto.

1. Escriba el código siguiente, guarde el archivo y ciérrelo:

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

1. Cree una carpeta llamada *security* en la carpeta src de Java para su aplicación; por ejemplo: *src/main/java/com/wingtiptoys/security/security*.

1. Cree un archivo Java nuevo llamado *WebSecurityConfig.java* en la carpeta *security* y ábralo en un editor de texto.

1. Escriba el código siguiente, guarde el archivo y ciérrelo:

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

## <a name="build-and-test-your-app"></a>Compilación y prueba de la aplicación

1. Abra un símbolo del sistema y cambie el directorio a la carpeta donde se encuentra el archivo *pom.xml* de su aplicación.

1. Compile la aplicación de Spring Boot con Maven y ejecútela; por ejemplo:

   ```shell
   mvn clean package
   ```

   ![][build-application]

1. Compile la aplicación de Spring Boot con Maven y ejecútela; por ejemplo:

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```



1. Después de que Maven haya compilado e iniciado la aplicación, abra <http://localhost:8080> en un explorador web.

## <a name="next-steps"></a>Pasos siguientes

Para más información acerca de cómo usar Azure Active Directory, consulte los siguientes artículos:

* [Documentación de Azure Active Directory].

Para obtener más información sobre el uso de aplicaciones de Spring Boot en Azure, consulte los siguientes artículos:

* [Implementación de una aplicación de Spring Boot en Azure App Service](deploy-spring-boot-java-web-app-on-azure.md)

* [Ejecución de una aplicación de Spring Boot en un clúster de Kubernetes en Azure Container Service](deploy-spring-boot-java-app-on-kubernetes.md)

Para más información sobre el uso de Azure con Java, consulte [Azure para desarrolladores de Java] y [Java Tools for Visual Studio Team Services] (Herramientas de Java para Visual Studio Team Services).

**[Spring Framework]** es una solución de código abierto que ayuda a los desarrolladores de Java a crear aplicaciones de nivel empresarial. Uno de los proyectos más populares que se basa en esa plataforma es [Spring Boot], que proporciona un enfoque simplificado para crear aplicaciones de Java independientes. Para ayudar a los desarrolladores a empezar con Spring Boot, puede encontrar varios paquetes de ejemplo de Spring Boot en <https://github.com/spring-guides/>. Además de elegir de la lista de proyectos básicos de Spring Boot, el **[Spring Initializr]** ayuda a los desarrolladores en los primeros pasos para crear aplicaciones de Spring Boot personalizadas.

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
