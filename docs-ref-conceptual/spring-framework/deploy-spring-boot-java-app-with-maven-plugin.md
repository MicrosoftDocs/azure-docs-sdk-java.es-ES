---
title: Implementación de una aplicación de archivo JAR de Spring Boot en la nube con Maven y Azure
description: Obtenga información acerca de cómo implementar una aplicación de Spring Boot en la nube con el complemento de Maven para Azure Web Apps para Linux.
services: app-service
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: brborges
ms.author: robmcm
ms.date: 12/19/2018
ms.devlang: java
ms.service: app-service
ms.topic: article
ms.openlocfilehash: 950b360eb525b0c6b97daad0798c27ded0582b8b
ms.sourcegitcommit: f0f140b0862ca5338b1b7e5c33cec3e58a70b8fd
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/03/2019
ms.locfileid: "53991349"
---
# <a name="deploy-a-spring-boot-jar-file-web-app-to-azure-app-service-on-linux"></a>Implementación de una aplicación web de archivo JAR de Spring Boot en Azure App Service en Linux

En este artículo se muestra cómo usar el [complemento de Maven para Azure App Service Web Apps](/java/api/overview/azure/maven/azure-webapp-maven-plugin/readme) para implementar una aplicación de Spring Boot empaquetada como un archivo JAR de Java SE en [Azure App Service en Linux](/azure/app-service/containers/). Puede optar por la implementación de Java SE en lugar de [Tomcat y archivos WAR](/azure/app-service/containers/quickstart-java) cuando desee consolidar las dependencias, el entorno de ejecución y la configuración de la aplicación en un único artefacto implementable.


Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de empezar.

## <a name="prerequisites"></a>Requisitos previos

Para realizar los pasos de este tutorial, necesitará tener instalado y configurado lo siguiente:

* La [CLI de Azure](/cli/azure/), ya sea localmente o con [Azure Cloud Shell](https://shell.azure.com).
* Un kit de desarrollo de Java (JDK) admitido Para más información sobre los JDK disponibles para desarrollar en Azure, consulte <https://aka.ms/azure-jdks>.
* [Maven](https://maven.apache.org/) de Apache, versión 3.
* Un cliente [Git](https://git-scm.com/downloads).

## <a name="install-and-sign-in-to-azure-cli"></a>Instalación e inicio de sesión en la CLI de Azure

La manera más sencilla y fácil de obtener el complemento Maven para implementar la aplicación de Spring Boot es con la [CLI de Azure](/cli/azure/).

Inicie sesión en la cuenta de Azure mediante la CLI de Azure:
   
   ```shell
   az login
   ```
   
Siga las instrucciones para completar el proceso de inicio de sesión.

## <a name="clone-the-sample-app"></a>Clonación de la aplicación de ejemplo

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

1. Debería ver el mensaje siguiente mostrado: **Greetings from Spring Boot!**

## <a name="configure-maven-plugin-for-azure-app-service"></a>Configuración del complemento de Maven para Azure App Service

En esta sección, configurará el proyecto de Spring Boot `pom.xml` para que Maven pueda implementar la aplicación en Azure App Service en Linux.

1. Abra `pom.xml` en un editor de código.

2. En la sección `<build>` del archivo pom.xml, agregue la siguiente entrada `<plugin>` dentro de la etiqueta `<plugins>`.

   ```xml
   <plugin>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-webapp-maven-plugin</artifactId>
    <version>1.4.0</version>
    <configuration>
      <deploymentType>jar</deploymentType>

      <!-- configure app to run on port 80, required by App Service -->
      <appSettings>
        <property> 
          <name>JAVA_OPTS</name> 
          <value>-Dserver.port=80</value> 
        </property> 
      </appSettings>

      <!-- Web App information -->
      <resourceGroup>${RESOURCEGROUP_NAME}</resourceGroup>
      <appName>${WEBAPP_NAME}</appName>
      <region>${REGION}</region>  

      <!-- Java Runtime Stack for Web App on Linux-->
      <linuxRuntime>jre8</linuxRuntime>
    </configuration>
   </plugin>
   ```

3. Actualice los siguientes marcadores de posición en la configuración del complemento:

| Marcador de posición | DESCRIPCIÓN |
| ----------- | ----------- |
| `RESOURCEGROUP_NAME` | Nombre del nuevo grupo de recursos en el que se va a crear la aplicación web. Al colocar todos los recursos de una aplicación en un grupo, puede administrarlos juntos. Por ejemplo, si elimina el grupo de recursos también se eliminarán todos los recursos asociados con la aplicación. Actualice este valor con un nombre único de un nuevo grupo de recursos, por ejemplo, *TestResources*. Este nombre lo utilizará para limpiar todos los recursos de Azure en una sección posterior. |
| `WEBAPP_NAME` | El nombre de la aplicación forma parte del nombre de host de la aplicación web si se ha implementado en Azure (WEBAPP_NAME.azurewebsites.net). Actualice este valor con un nombre único para la nueva aplicación web de Azure, que hospedará la aplicación Java, por ejemplo *contoso*. |
| `REGION` | Una región de Azure donde se hospeda la aplicación web, por ejemplo `westus2`. Puede obtener una lista de regiones en Cloud Shell o la CLI mediante el comando `az account list-locations`. |

Encontrará una lista completa de las opciones de configuración en la [Referencia del complemento de Maven en GitHub](https://github.com/Microsoft/azure-maven-plugins/tree/develop/azure-webapp-maven-plugin).

## <a name="deploy-the-app-to-azure"></a>Implementación de la aplicación en Azure

Una vez que haya configurado todas las opciones en las secciones anteriores de este artículo, estará listo para implementar la aplicación web en Azure. Para ello, siga estos pasos:

1. En el símbolo del sistema o la ventana de terminal que usó anteriormente, vuelva a compilar el archivo JAR con Maven si ha realizado algún cambio en el archivo *pom.xml*; por ejemplo:
   ```shell
   mvn clean package
   ```

1. Implemente la aplicación web en Azure mediante Maven; por ejemplo:
   ```shell
   mvn azure-webapp:deploy
   ```

Maven implementará la aplicación web en Azure; si la aplicación web o el plan de la aplicación web no existen, se crearán.

Cuando se haya implementado la web, podrá administrarla mediante [Azure Portal].

* La aplicación web aparecerá en **App Services**:

   ![Aplicación web en la lista de App Services de Azure Portal][AP01]

* Y la dirección URL de la aplicación web se mostrará en la sección de **información general** de la aplicación web:

   ![Determinar la dirección URL de la aplicación web][AP02]

Compruebe que la implementación se realizó correctamente mediante el mismo comando de cURL utilizado antes, utilizando la dirección URL de la aplicación web del portal en lugar de `localhost`. Debería ver el mensaje siguiente mostrado: **Greetings from Spring Boot!** 

## <a name="next-steps"></a>Pasos siguientes

Para más información acerca de Spring y Azure, vaya al centro de documentación de Azure.

> [!div class="nextstepaction"]
> [Spring en Azure](/java/azure/spring-framework)

### <a name="additional-resources"></a>Recursos adicionales

Para más información acerca de las diferentes tecnologías que se tratan en este artículo, consulte los artículos siguientes:

* [Complemento Maven de Azure Web Apps]

* [Uso del complemento Maven de Azure Web Apps para implementar una aplicación de Spring Boot en contenedor en Azure](deploy-containerized-spring-boot-java-app-with-maven-plugin.md)

* [Creación de una entidad de servicio de Azure con la CLI de Azure 2.0](/cli/azure/create-an-azure-service-principal-azure-cli)

* [Referencia de configuración de Maven](https://maven.apache.org/settings.html)

<!-- URL List -->

[Azure Command-Line Interface (CLI)]: /cli/azure/overview
[Azure for Java Developers]: /java/azure/
[Azure Portal]: https://portal.azure.com/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Working with Azure DevOps and Java]: /azure/devops/
[Maven]: http://maven.apache.org/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Primeros pasos de Spring Boot]: https://github.com/spring-guides/gs-spring-boot
[Spring Framework]: https://spring.io/
[Complemento Maven de Azure Web Apps]: /java/api/overview/azure/maven/azure-webapp-maven-plugin/readme

[Java Development Kit (JDK)]: https://aka.ms/azure-jdks
<!-- http://www.oracle.com/technetwork/java/javase/downloads/ -->

<!-- IMG List -->

[AP01]: ./media/deploy-spring-boot-java-app-with-maven-plugin/AP01.png
[AP02]: ./media/deploy-spring-boot-java-app-with-maven-plugin/AP02.png
