---
title: "Uso del complemento Maven de Azure Web Apps para implementar una aplicación de Spring Boot en Azure"
description: "Aprenda a usar el complemento Maven de Azure Web Apps para implementar una aplicación de Spring Boot en Azure."
services: app-service
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
keywords: Spring, Spring Boot, Spring Framework, Maven
ms.assetid: 
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: multiple
ms.devlang: java
ms.topic: article
ms.date: 11/01/2017
ms.author: robmcm;kevinzha
ms.openlocfilehash: 9711a14d7b671cb672f54b92415544378c90fd88
ms.sourcegitcommit: 613c1ffd2e0279fc7a96fca98aa1809563f52ee1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="how-to-use-the-maven-plugin-for-azure-web-apps-to-deploy-a-spring-boot-app-to-azure"></a>Uso del complemento Maven de Azure Web Apps para implementar una aplicación de Spring Boot en Azure

El [complemento Maven para Azure Web Apps](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) de [Apache Maven](http://maven.apache.org/) proporciona una perfecta integración de Azure App Service en proyectos de Maven y simplifica el proceso para que los desarrolladores implementen aplicaciones web en Azure App Service.

Este artículo muestra cómo utilizar el complemento Maven de Azure Web Apps para implementar una aplicación de Spring Boot de ejemplo en Azure App Services.

> [!NOTE]
>
> El complemento Maven de Azure Web Apps está disponible actualmente como versión preliminar. Por ahora, solo se admite la publicación FTP, aunque se van a agregar características adicionales en el futuro.
>

## <a name="prerequisites"></a>Requisitos previos

Para poder realizar los pasos de este tutorial, necesitará tener los siguientes requisitos previos:

* Una suscripción de Azure. Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN] o registrarse para obtener una [cuenta de Azure gratuita].
* La [Interfaz de la línea de comandos (CLI) de Azure].
* Un [kit de desarrollo de Java (JDK)] actualizado, versión 1.7 o posterior.
* La herramienta de compilación [Maven] de Apache (versión 3).
* Un cliente [Git].

## <a name="clone-the-sample-spring-boot-web-app"></a>Clonación de la aplicación web de Spring Boot de ejemplo

En esta sección, va a clonar una aplicación de Spring Boot terminada y a probarla de forma local.

1. Abra el símbolo del sistema o una ventana de terminal y cree un directorio local para alojar la aplicación de Spring Boot, y cambie a dicho directorio, por ejemplo:
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   -- o --
   ```shell
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. Clone el proyecto de ejemplo [inicial de Spring Boot] en el directorio que creó, por ejemplo:
   ```shell
   git clone https://github.com/microsoft/gs-spring-boot
   ```

1. Cambie de directorio al del proyecto finalizado, por ejemplo:
   ```shell
   cd gs-spring-boot/complete
   ```

1. Compile el archivo JAR con Maven, por ejemplo:
   ```shell
   mvn clean package
   ```

1. Cuándo se haya creado la aplicación web, iníciela con Maven. Por ejemplo:
   ```shell
   mvn spring-boot:run
   ```

1. Pruebe la aplicación web. Para ello, navegue a ella localmente mediante un explorador web. Por ejemplo, puede utilizar el siguiente comando si dispone de curl:
   ```shell
   curl http://localhost:8080
   ```

1. Debería aparecer el siguiente mensaje: **Greetings from Spring Boot!** (Saludos de Spring Boot).

## <a name="create-an-azure-service-principal"></a>Creación de una entidad de servicio de Azure

En esta sección, va a crear una entidad de servicio de Azure que usa el complemento Maven cuando implementa la aplicación web en Azure.

1. Abra el símbolo del sistema.

1. Inicie sesión en la cuenta de Azure mediante la CLI de Azure:
   ```shell
   az login
   ```
   Siga las instrucciones para completar el proceso de inicio de sesión.

1. Cree una entidad de servicio de Azure:
   ```shell
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   Donde `uuuuuuuu` es el nombre de usuario y `pppppppp` es la contraseña de la entidad de servicio.

1. Azure responde con un archivo JSON que es similar al siguiente:
   ```json
   {
      "appId": "aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa",
      "displayName": "uuuuuuuu",
      "name": "http://uuuuuuuu",
      "password": "pppppppp",
      "tenant": "tttttttt-tttt-tttt-tttt-tttttttttttt"
   }
   ```

   > [!NOTE]
   >
   > Utilizará los valores de esta respuesta JSON al configurar el complemento para implementar la aplicación web en Azure. El `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, y `tttttttt` son valores de marcador de posición que se usan en este ejemplo para que sea más fácil asignar estos valores a sus respectivos elementos al configurar el archivo `settings.xml` de Maven en la sección siguiente.
   >
   >

## <a name="configure-maven-to-use-your-azure-service-principal"></a>Configurar Maven para usar la entidad de servicio de Azure

En esta sección, utilice los valores de la entidad de servicio de Azure para configurar la autenticación que va a usar Maven al implementar la aplicación web en Azure.

1. Abra el archivo `settings.xml` de Maven en un editor de texto; este archivo puede encontrarse en una ruta de acceso como la de los ejemplos siguientes:
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. Agregue la configuración de la entidad de servicio de la sección anterior de este tutorial a la colección `<servers>` en el archivo *settings.xml*, por ejemplo:

   ```xml
   <servers>
      <server>
        <id>azure-auth</id>
         <configuration>
            <client>aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa</client>
            <tenant>tttttttt-tttt-tttt-tttt-tttttttttttt</tenant>
            <key>pppppppp</key>
            <environment>AZURE</environment>
         </configuration>
      </server>
   </servers>
   ```
   Donde:
   Elemento | Descripción
   ---|---|---
   `<id>` | Especifica un nombre único que Maven utiliza para buscar la configuración de seguridad al implementar la aplicación web en Azure.
   `<client>` | Contiene el valor `appId` de la entidad de servicio.
   `<tenant>` | Contiene el valor `tenant` de la entidad de servicio.
   `<key>` | Contiene el valor `password` de la entidad de servicio.
   `<environment>` | Define el entorno en la nube de Azure de destino, que es `AZURE` en este ejemplo. (Una lista completa de los entornos está disponible en la documentación del [complemento Maven de Azure Web Apps])

1. Guarde y cierre el archivo *settings.xml*.

## <a name="optional-customize-your-pomxml-before-deploying-your-web-app-to-azure"></a>OPCIONAL: Personalice el archivo pom.xml antes de implementar la aplicación web en Azure

Abra el archivo `pom.xml` de la aplicación de Spring Boot en un editor de texto y, a continuación, busque el elemento `<plugin>` de `azure-webapp-maven-plugin`. Este elemento debe tener un aspecto similar al ejemplo siguiente:

   ```xml
   <plugin>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-webapp-maven-plugin</artifactId>
      <version>0.1.3</version>
      <configuration>
         <authentication>
            <serverId>azure-auth</serverId>
         </authentication>
         <resourceGroup>maven-plugin</resourceGroup>
         <appName>maven-web-app-${maven.build.timestamp}</appName>
         <region>westus</region>
         <javaVersion>1.8</javaVersion>
         <deploymentType>ftp</deploymentType>
         <resources>
            <resource>
               <directory>${project.basedir}/target</directory>
               <targetPath>/</targetPath>
               <includes>
                  <include>*.jar</include>
               </includes>
            </resource>
            <resource>
               <directory>${project.basedir}</directory>
               <targetPath>/</targetPath>
               <includes>
                  <include>web.config</include>
               </includes>
            </resource>
         </resources>
      </configuration>
   </plugin>
   ```

Hay varios valores que se pueden modificar en el complemento Maven y hay una descripción detallada de cada uno de estos elementos disponible en la documentación del [complemento Maven de Azure Web Apps]. Dicho esto, hay varios valores que merece la pena destacar en este artículo:

Elemento | Descripción
---|---|---
`<version>` | Especifica la versión del [complemento Maven de Azure Web Apps]. Debe comprobar la versión que aparece en el [repositorio central de Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) para asegurarse de que está utilizando la versión más reciente.
`<authentication>` | Especifica la información de autenticación de Azure que, en este ejemplo, contiene un elemento `<serverId>` que contiene `azure-auth`; Maven utiliza ese valor para buscar los valores de la entidad de servicio de Azure en el archivo *settings.xml* que se definió en una sección anterior de este artículo.
`<resourceGroup>` | Especifica el grupo de recursos de destino, que es `maven-plugin` en este ejemplo. Se creará este grupo de recursos durante la implementación si todavía no existe.
`<appName>` | Especifica el nombre de destino de la aplicación web. En este ejemplo, el nombre de destino es `maven-web-app-${maven.build.timestamp}`, donde el sufijo `${maven.build.timestamp}` se anexa en este ejemplo para evitar conflictos. (La marca de tiempo es opcional; puede especificar cualquier cadena única para el nombre de la aplicación).
`<region>` | Especifica la región de destino, que en este ejemplo es `westus`. (Puede encontrar una lista completa en la documentación del [complemento Maven de Azure Web Apps]).
`<javaVersion>` | Especifica la versión de tiempo de ejecución de Java para la aplicación web. (Puede encontrar una lista completa en la documentación del [complemento Maven de Azure Web Apps]).
`<deploymentType>` | Especifica el tipo de implementación para la aplicación web. Por ahora, solo se admite `ftp`, aunque la compatibilidad con otros tipos de implementación está en la fase de desarrollo.
`<resources>` | Especifica los recursos y destinos que Maven usa al implementar la aplicación web en Azure. En este ejemplo, dos elementos `<resource>` especifican que Maven implementará el archivo JAR de la aplicación web y el archivo *web.config* desde el proyecto de Spring Boot.

## <a name="build-and-deploy-your-web-app-to-azure"></a>Creación e implementación de una aplicación web en Azure

Una vez haya configurado todas las opciones en las secciones anteriores de este artículo, está listo para implementar la aplicación web en Azure. Para ello, siga estos pasos:

1. En el símbolo del sistema o la ventana de terminal que usó anteriormente, vuelva a compilar el archivo JAR con Maven si ha realizado algún cambio en el archivo *pom.xml*; por ejemplo:
   ```shell
   mvn clean package
   ```

1. Implemente la aplicación web en Azure mediante Maven; por ejemplo:
   ```shell
   mvn azure-webapp:deploy
   ```

Maven implementará la aplicación web en Azure; si la aplicación web no existe, se creará.

Cuando se haya implementado la web, podrá administrarla mediante [Azure Portal].

* La aplicación web aparecerá en **App Services**:

   ![Aplicación web en la lista de App Services de Azure Portal][AP01]

* Y la dirección URL de la aplicación web se mostrará en la sección de **información general** de la aplicación web:

   ![Determinar la dirección URL de la aplicación web][AP02]

<!--
##  OPTIONAL: Configure the embedded Tomcat server to run on a different port

The embedded Tomcat server in the sample Spring Boot application is configured to run on port 8080 by default. However, if you want to run the embedded Tomcat server to run on a different port, such as port 80 for local testing, you can configure the port by using the following steps.

1. Go to the *resources* directory (or create the directory if it does not exist); for example:
   ```shell
   cd src/main/resources
   ```

1. Open the *application.yml* file in a text editor if it exists, or create a new YAML file if it does not exist.

1. Modify the **server** setting so that the server runs on port 80; for example:
   ```yaml
   server:
      port: 80
   ```

1. Save and close the *application.yml* file.
-->

## <a name="next-steps"></a>Pasos siguientes

Para más información acerca de las diferentes tecnologías que se tratan en este artículo, consulte los artículos siguientes:

* [complemento Maven de Azure Web Apps]

* [Inicio de sesión en Azure desde la CLI de Azure](/azure/xplat-cli-connect)

* [Uso del complemento Maven de Azure Web Apps para implementar una aplicación de Spring Boot en contenedor en Azure](deploy-containerized-spring-boot-java-app-with-maven-plugin.md)

* [Creación de una entidad de servicio de Azure con la CLI de Azure 2.0](/cli/azure/create-an-azure-service-principal-azure-cli)

* [Referencia de configuración de Maven](https://maven.apache.org/settings.html)

<!-- URL List -->

[Interfaz de la línea de comandos (CLI) de Azure]: /cli/azure/overview
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[Azure Portal]: https://portal.azure.com/
[cuenta de Azure gratuita]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[ventajas como suscriptor de MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[inicial de Spring Boot]: https://github.com/microsoft/gs-spring-boot
[Spring Framework]: https://spring.io/
[complemento Maven de Azure Web Apps]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin

<!-- IMG List -->

[AP01]: ./media/deploy-spring-boot-java-app-with-maven-plugin/AP01.png
[AP02]: ./media/deploy-spring-boot-java-app-with-maven-plugin/AP02.png
