---
title: Implementación de una aplicación de Spring Boot en la nube con Maven y Azure
description: Obtenga información acerca de cómo implementar una aplicación de Spring Boot en la nube con el complemento de Maven para Azure Web Apps.
services: app-service
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: brborges
ms.assetid: ''
ms.author: robmcm;kevinzha;brborges
ms.date: 06/01/2018
ms.devlang: java
ms.service: app-service
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: 3610312ed17301131967bd2c047c86656de070e7
ms.sourcegitcommit: f313c14e92f38c54a3a583270ee85cc928cd39d7
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2018
ms.locfileid: "34689428"
---
# <a name="deploy-a-spring-boot-app-to-the-cloud-using-the-maven-plugin-for-azure-app-service"></a>Implementación de una aplicación de Spring Boot en la nube con el complemento de Maven para Azure App Service

En este artículo se muestra cómo utilizar el complemento Maven de Azure App Service Web Apps para implementar una aplicación de Spring Boot de ejemplo.

> [!NOTE]
> 
> El [complemento Maven para Azure App Service Web Apps](https://docs.microsoft.com/java/api/overview/azure/maven/azure-webapp-maven-plugin/readme) para [Apache Maven](http://maven.apache.org/) proporciona una perfecta integración de Azure App Service en proyectos de Maven y simplifica el proceso para que los desarrolladores implementen aplicaciones web en Azure App Service.

Antes de usar el complemento Maven, obtenga en Maven Central la última versión disponible del complemento: [![Maven Central](https://img.shields.io/maven-central/v/com.microsoft.azure/azure-webapp-maven-plugin.svg)](http://search.maven.org/#search%7Cga%7C1%7Cg%3A%22com.microsoft.azure%22%20AND%20a%3A%22azure-webapp-maven-plugin%22) 

## <a name="prerequisites"></a>requisitos previos

Para realizar los pasos de este tutorial, necesitará tener los siguientes requisitos previos:

* Si todavía no tiene una suscripción a Azure, puede registrarse para obtener una [cuenta de Azure gratuita].
* La [Interfaz de la línea de comandos (CLI) de Azure].
* Un [kit de desarrollo de Java (JDK)] actualizado, versión 1.7 o posterior.
* La herramienta de compilación [Maven] de Apache (versión 3).
* Un cliente [Git].

## <a name="clone-the-sample-spring-boot-web-app"></a>Clonación de la aplicación web de Spring Boot de ejemplo

En esta sección, va a clonar una aplicación de Spring Boot terminada y a probarla de forma local.

1. Abra el símbolo del sistema o una ventana de terminal, cree un directorio local para alojar la aplicación de Spring Boot y cambie a dicho directorio, por ejemplo:
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   -- o --
   ```shell
   md ~/SpringBoot
   cd ~/SpringBoot
   ```

1. Clone el proyecto de ejemplo [Primeros pasos de Spring Boot] en el directorio que creó, por ejemplo:
   ```shell
   git clone https://github.com/spring-guides/gs-spring-boot
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

## <a name="adjust-project-for-war-based-deployment-on-azure-app-service"></a>Ajuste del proyecto para una implementación basada en WAR en Azure App Service

En esta sección, se ajustará rápidamente el proyecto de Spring Boot para implementarlo como un archivo WAR en Azure App Service, que proporciona Tomcat como sistema de tiempo de ejecución de forma predeterminada. Para que funcione, hay que modificar dos archivos:

- El archivo `pom.xml` de Maven
- La clase `Application` de Java

Comencemos con la configuración de Maven:

1. Abra `pom.xml`

1. Agregue `<packaging>war</packaging>` justo después de la definición `<artifactId>` en la parte superior:
   ```xml
    <modelVersion>4.0.0</modelVersion>
    <groupId>org.springframework</groupId>
    <artifactId>gs-spring-boot</artifactId>

    <packaging>war</packaging>
   ```

1. Agregue la siguiente dependencia:
   ```xml
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-tomcat</artifactId>
            <scope>provided</scope>
        </dependency>
   ```

Ahora, abra la clase `Application`, esperemos que después de que el IDE haya seleccionado las nuevas dependencias, y realice las siguientes modificaciones:

1. Haga que la clase Application sea una subclase de `SpringBootServletInitializer`:
   ```java
   @SpringBootApplication
   public class Application extends SpringBootServletInitializer {
     // ...
   }
   ```

1. Agregue el método siguiente a la clase Application:
   ```java
       @Override
       protected SpringApplicationBuilder configure(SpringApplicationBuilder application) {
           return application.sources(Application.class);
       }
   ```

La aplicación ahora está lista para implementarse en Tomcat y otros sistemas de tiempo de ejecución de servlet (por ejemplo, Jetty).

## <a name="add-the-maven-plugin-for-azure-app-service-web-apps"></a>Adición del complemento Maven para Azure App Service Web Apps

En esta sección, agregaremos un complemento de Maven que automatizará toda la implementación de esta aplicación en Azure App Service Web Apps.

1. Abra `pom.xml` de nuevo.

1. Dentro de `<properties>`, establezca un formato de marca de tiempo personalizado con la propiedad `maven.build.timestamp.format`. Como Azure App Service crea una dirección URL pública para la aplicación, se usará esta configuración para generar el nombre de la implementación y evitar conflictos con las implementaciones activas de otros usuarios.
   ```xml
    <properties>
        <java.version>1.8</java.version>
        <maven.build.timestamp.format>yyyyMMddHHmmssSSS</maven.build.timestamp.format>
    </properties>
   ```

1. En el elemento `<plugins>`, agregue lo siguiente:
   ```xml
    <plugin>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-webapp-maven-plugin</artifactId>
      <!-- Check latest version on Maven Central -->
      <version>1.1.0</version>
    </plugin>
   ```

Con esta configuración, el proyecto de Maven ya está listo para su implementación en vivo en Azure App Service Web Apps.

## <a name="install-and-log-in-to-azure-cli"></a>Instalación y inicio de sesión en la CLI de Azure

La manera más sencilla y fácil de obtener el complemento Maven para implementar la aplicación de Spring Boot es con la [CLI de Azure](https://docs.microsoft.com/cli/azure/). Asegúrese de que la tiene instalada.

1. Inicie sesión en la cuenta de Azure mediante la CLI de Azure:
   ```shell
   az login
   ```
   Siga las instrucciones para completar el proceso de inicio de sesión.

## <a name="optionally-customize-pomxml-before-deploying"></a>También puede personalizar el archivo pom.xml antes de la implementación.

Abra el archivo `pom.xml` de la aplicación de Spring Boot en un editor de texto y, a continuación, busque el elemento `<plugin>` de `azure-webapp-maven-plugin`. Este elemento debe tener un aspecto similar al ejemplo siguiente:

   ```xml
  <plugins>
    <plugin>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-webapp-maven-plugin</artifactId>
      <!-- Check latest version on Maven Central -->
      <version>1.1.0</version>
      <configuration>
         <resourceGroup>maven-projects</resourceGroup>
         <appName>${project.artifactId}-${maven.build.timestamp}</appName>
         <region>westus</region>
         <javaVersion>1.8</javaVersion>
         <deploymentType>war</deploymentType>
      </configuration>
    </plugin>
  </plugins>
   ```

Hay varios valores que se pueden modificar en el complemento Maven; puede encontrar una descripción detallada de cada uno de estos elementos en la documentación del [complemento Maven de Azure Web Apps]. Dicho esto, hay varios valores que merece la pena destacar en este artículo:

| Elemento | DESCRIPCIÓN |
|---|---|
| `<version>` | Especifica la versión del [complemento Maven de Azure Web Apps]. Compruebe que la versión que aparece en el [repositorio central de Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) para asegurarse de que está utilizando la versión más reciente. |
| `<resourceGroup>` | Especifica el grupo de recursos de destino, que es `maven-plugin` en este ejemplo. Se creará este grupo de recursos durante la implementación si todavía no existe. |
| `<appName>` | Especifica el nombre de destino de la aplicación web. En este ejemplo, el nombre de destino es `maven-web-app-${maven.build.timestamp}`, donde el sufijo `${maven.build.timestamp}` se anexa en este ejemplo para evitar conflictos. (La marca de tiempo es opcional; puede especificar cualquier cadena única para el nombre de la aplicación). |
| `<region>` | Especifica la región de destino, que en este ejemplo es `westus`. (Puede encontrar una lista completa en la documentación del [complemento Maven de Azure Web Apps]). |
| `<javaVersion>` | Especifica la versión de tiempo de ejecución de Java para la aplicación web. (Puede encontrar una lista completa en la documentación del [complemento Maven de Azure Web Apps]). |
| `<deploymentType>` | Especifica el tipo de implementación para la aplicación web. El valor predeterminado es `war`. |

## <a name="build-and-deploy-your-web-app-to-azure"></a>Creación e implementación de una aplicación web en Azure

Una vez que haya configurado todas las opciones en las secciones anteriores de este artículo, estará listo para implementar la aplicación web en Azure. Para ello, siga estos pasos:

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

* [Complemento Maven de Azure Web Apps]

* [Inicio de sesión en Azure desde la CLI de Azure](/azure/xplat-cli-connect)

* [Uso del complemento Maven de Azure Web Apps para implementar una aplicación de Spring Boot en contenedor en Azure](deploy-containerized-spring-boot-java-app-with-maven-plugin.md)

* [Creación de una entidad de servicio de Azure con la CLI de Azure 2.0](/cli/azure/create-an-azure-service-principal-azure-cli)

* [Referencia de configuración de Maven](https://maven.apache.org/settings.html)

<!-- URL List -->

[Interfaz de la línea de comandos (CLI) de Azure]: /cli/azure/overview
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Azure Portal]: https://portal.azure.com/
[cuenta de Azure gratuita]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Primeros pasos de Spring Boot]: https://github.com/spring-guides/gs-spring-boot
[Spring Framework]: https://spring.io/
[Complemento Maven de Azure Web Apps]: https://docs.microsoft.com/java/api/overview/azure/maven/azure-webapp-maven-plugin/readme

<!-- IMG List -->

[AP01]: ./media/deploy-spring-boot-java-app-with-maven-plugin/AP01.png
[AP02]: ./media/deploy-spring-boot-java-app-with-maven-plugin/AP02.png
