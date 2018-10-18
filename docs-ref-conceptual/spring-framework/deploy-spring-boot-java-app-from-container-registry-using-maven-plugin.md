---
title: Uso del complemento Maven de Azure Web Apps para implementar una aplicación de Spring Boot de Azure Container Registry en Azure App Service
description: Este tutorial le guiará por los pasos para implementar una aplicación de Spring Boot de Azure Container Registry en Azure App Service mediante un complemento Maven.
services: container-registry
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: robmcm;kevinzha
ms.date: 02/01/2018
ms.devlang: java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: e84960ebf79b89b2430924016a429518a935d086
ms.sourcegitcommit: 9d9e2fa97ebd95a699adcb58e82c3fc0882f0a24
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/15/2018
ms.locfileid: "49315939"
---
# <a name="how-to-use-the-maven-plugin-for-azure-web-apps-to-deploy-a-spring-boot-app-in-azure-container-registry-to-azure-app-service"></a>Uso del complemento Maven de Azure Web Apps para implementar una aplicación de Spring Boot de Azure Container Registry en Azure App Service

En este artículo se muestra cómo implementar una aplicación de [Spring Boot] de ejemplo en Azure Container Registry y cómo usar el complemento Maven para Azure Web Apps para implementar la aplicación en Azure App Service.

> [!NOTE]
> 
> El complemento Maven para Azure Web Apps de [Apache Maven](http://maven.apache.org/) proporciona una perfecta integración de Azure App Service en proyectos de Maven y simplifica el proceso para que los desarrolladores implementen aplicaciones web en Azure App Service.
> 
> El complemento Maven de Azure Web Apps está disponible actualmente como versión preliminar. Por ahora, solo se admite la publicación FTP, aunque se van a agregar características adicionales en el futuro.
> 

## <a name="prerequisites"></a>Requisitos previos

Para realizar los pasos de este tutorial, necesitará tener los siguientes requisitos previos:

* Una suscripción de Azure. Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN] o registrarse para obtener una [cuenta de Azure gratuita].
* La [Interfaz de la línea de comandos (CLI) de Azure].
* Un [kit de desarrollo de Java (JDK)] actualizado, versión 1.7 o posterior.
* La herramienta de compilación [Maven] de Apache (versión 3).
* Un cliente [Git].
* Un [Docker].

> [!NOTE]
>
> Dados los requisitos de virtualización de este tutorial, los pasos que se describen en este artículo no se pueden seguir en una máquina virtual; es preciso usar un equipo físico con características de virtualización habilitadas.
>

## <a name="clone-the-sample-spring-boot-on-docker-web-app"></a>Clonación de la aplicación de Spring Boot de ejemplo en la aplicación web de Docker

En esta sección, clone una aplicación de Spring Boot en contenedor y pruébela de forma local.

1. Abra el símbolo del sistema o una ventana de terminal, cree un directorio local para alojar la aplicación de Spring Boot y cambie a dicho directorio, por ejemplo:
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   -- o --
   ```shell
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. Clone el proyecto de ejemplo [Spring Boot on Docker Getting Started] en el directorio que ha creado, por ejemplo:
   ```shell
   git clone -b https://github.com/spring-guides/gs-spring-boot-docker
   ```

1. Cambie de directorio al del proyecto finalizado, por ejemplo:
   ```shell
   cd gs-spring-boot-docker/complete
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

1. Debería aparecer el siguiente mensaje: **Hello Docker World**

   ![Examen local de aplicación de ejemplo][SB01]

> [!NOTE]
>
> Cuando se usa Docker localmente, puede ver un error que indica que no se puede conectar a localhost en el puerto 2375. Si esto ocurre, debe habilitar el uso de Docker localmente sin TLS. Para ello, abra la configuración de Docker y compruebe que la opción **Expose Docker Daemon está establecida en TCP://localhost:2375 sin TLS**.
>
> ![Exponer Docker Daemon en el puerto TCP 2375 local][TL01]

## <a name="create-an-azure-service-principal"></a>Creación de una entidad de servicio de Azure

En esta sección, va a crear una entidad de servicio de Azure que usa el complemento Maven cuando implementa el contenedor en Azure.

1. Abra el símbolo del sistema.

2. Inicie sesión en la cuenta de Azure mediante la CLI de Azure:
   ```azurecli
   az login
   ```
   Siga las instrucciones para completar el proceso de inicio de sesión.

3. Cree una entidad de servicio de Azure:
   ```azurecli
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   Donde:

   | Parámetro  |                    DESCRIPCIÓN                     |
   |------------|----------------------------------------------------|
   | `uuuuuuuu` | Especifica el nombre de usuario para la entidad de servicio. |
   | `pppppppp` | Especifica la contraseña de la entidad de servicio.  |


4. Azure responde con un archivo JSON que es similar al siguiente:
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
   > Utilizará los valores de esta respuesta JSON al configurar el complemento de Maven para implementar el contenedor en Azure. `aaaaaaaa`, `uuuuuuuu`, `pppppppp` y `tttttttt` son valores de marcador de posición que se usan en este ejemplo para que sea más fácil asignar estos valores a sus respectivos elementos al configurar el archivo `settings.xml` de Maven en la sección siguiente.
   >
   >

## <a name="create-an-azure-container-registry-using-the-azure-cli"></a>Creación de una instancia de Azure Container Registry mediante la CLI de Azure

1. Abra el símbolo del sistema.

1. Inicie sesión en una cuenta de Azure:
   ```azurecli
   az login
   ```

1. Cree un grupo de recursos para los recursos de Azure que se usan en este artículo:
   ```azurecli
   az group create --name=wingtiptoysresources --location=westus
   ```
   Reemplace `wingtiptoysresources` en este ejemplo por un nombre único para el grupo de recursos.

1. Cree una instancia de Azure Container Registry en el grupo de recursos de la aplicación de Spring Boot: 
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoysresources --location westus --name wingtiptoysregistry --sku Basic
   ```
   Reemplace `wingtiptoysregistry` en este ejemplo por un nombre único para el registro de contenedor.

1. Recupere la contraseña del registro de contenedor:
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```
   Azure responderá con la contraseña; por ejemplo:
   ```json
   {
      "name": "password",
      "value": "xxxxxxxxxx"
   }
   ```

## <a name="add-your-azure-container-registry-and-azure-service-principal-to-your-maven-settings"></a>Agregue el registro de contenedor y la entidad de servicio de Azure a la configuración de Maven

1. Abra el archivo `settings.xml` de Maven en un editor de texto; este archivo puede encontrarse en una ruta de acceso como la de los ejemplos siguientes:
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

2. Agregue la configuración de acceso de Azure Container Registry de la sección anterior de este artículo a la colección `<servers>` en el archivo *settings.xml*, por ejemplo:

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>xxxxxxxxxx</password>
      </server>
   </servers>
   ```
   Donde:

   |   Elemento    |                                 DESCRIPCIÓN                                  |
   |--------------|------------------------------------------------------------------------------|
   |    `<id>`    |         Contiene el nombre del registro de contenedor privado de Azure.          |
   | `<username>` |         Contiene el nombre del registro de contenedor privado de Azure.          |
   | `<password>` | Contiene la contraseña que recuperó en la sección anterior de este artículo. |


3. Agregue la configuración de la entidad de servicio de una sección anterior de este artículo a la colección `<servers>` en el archivo *settings.xml*, por ejemplo:

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

   |     Elemento     |                                                                                   DESCRIPCIÓN                                                                                   |
   |-----------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   |     `<id>`      |                                Especifica un nombre único que Maven utiliza para buscar la configuración de seguridad al implementar la aplicación web en Azure.                                |
   |   `<client>`    |                                                             Contiene el valor `appId` de la entidad de servicio.                                                             |
   |   `<tenant>`    |                                                            Contiene el valor `tenant` de la entidad de servicio.                                                             |
   |     `<key>`     |                                                           Contiene el valor `password` de la entidad de servicio.                                                            |
   | `<environment>` | Define el entorno en la nube de Azure de destino, que es `AZURE` en este ejemplo. (Una lista completa de los entornos está disponible en la documentación del [complemento Maven de Azure Web Apps]). |


4. Guarde y cierre el archivo *settings.xml*.

## <a name="build-your-docker-container-image-and-push-it-to-your-azure-container-registry"></a>Creación de la imagen de contenedor de Docker e inserción de esta en el registro de contenedor de Azure

1. Vaya al directorio de proyecto completado de la aplicación Spring Boot (por ejemplo, "*C:\SpringBoot\gs-spring-boot-docker\complete*" o "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*") y abra el archivo *pom.xml* con un editor de texto.

2. Actualice la colección `<properties>` del archivo *pom.xml* con el valor del servidor de inicio de sesión de Azure Container Registry de la sección anterior de este tutorial, por ejemplo:

   ```xml
   <properties>
      <azure.containerRegistry>wingtiptoysregistry</azure.containerRegistry>
      <docker.image.prefix>${azure.containerRegistry}.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
      <maven.build.timestamp.format>yyyyMMddHHmmssSSS</maven.build.timestamp.format>
   </properties>
   ```
   Donde:

   |           Elemento           |                                                                       DESCRIPCIÓN                                                                       |
   |-----------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------|
   | `<azure.containerRegistry>` |                                              Especifica el nombre del registro de contenedor privado de Azure.                                               |
   |   `<docker.image.prefix>`   | Especifica la dirección URL del registro de contenedor privado de Azure, que se crea agregando ".azurecr.io" al nombre del registro de contenedor privado. |


3. Compruebe que `<plugin>` del complemento de Docker del archivo *pom.xml* contiene las propiedades correctas de dirección del servidor de inicio de sesión y nombre de registro del paso anterior de este tutorial. Por ejemplo: 

   ```xml
   <plugin>
      <groupId>com.spotify</groupId>
      <artifactId>docker-maven-plugin</artifactId>
      <version>0.4.11</version>
      <configuration>
         <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
         <registryUrl>https://${docker.image.prefix}</registryUrl>
         <serverId>${azure.containerRegistry}</serverId>
         <dockerDirectory>src/main/docker</dockerDirectory>
         <resources>
            <resource>
               <targetPath>/</targetPath>
               <directory>${project.build.directory}</directory>
               <include>${project.build.finalName}.jar</include>
            </resource>
         </resources>
      </configuration>
   </plugin>
   ```
   Donde:

   |     Elemento     |                                       DESCRIPCIÓN                                       |
   |-----------------|-----------------------------------------------------------------------------------------|
   |  `<serverId>`   |  Especifica la propiedad que contiene el nombre del registro de contenedor privado de Azure.   |
   | `<registryUrl>` | Especifica la propiedad que contiene la dirección URL del registro de contenedor privado de Azure. |


4. Navegue hasta el directorio de proyecto completado de la aplicación de Spring Boot y ejecute el siguiente comando para recompilar la aplicación e insertar el contenedor en la instancia de Azure Container Registry:

   ```
   mvn package docker:build -DpushImage 
   ```

5. OPCIONAL: Vaya a [Azure Portal] y compruebe que hay una imagen de contenedor de Docker denominada **gs-spring-arranque-docker** en el registro de contenedor.

   ![Comprobar contenedor en Azure Portal][CR01]

## <a name="customize-your-pomxml-then-build-and-deploy-your-container-to-azure"></a>Personalización del archivo pom.xml y compilación e implementación posterior del contenedor en Azure

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
         <resourceGroup>wingtiptoysresources</resourceGroup>
         <appName>maven-linux-app-${maven.build.timestamp}</appName>
         <region>westus</region>
         <containerSettings>
            <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
            <registryUrl>https://${docker.image.prefix}</registryUrl>
            <serverId>${azure.containerRegistry}</serverId>
         </containerSettings>
         <appSettings>
            <property>
               <name>PORT</name>
               <value>8080</value>
            </property>
         </appSettings>
      </configuration>
   </plugin>
   ```

Hay varios valores que se pueden modificar en el complemento Maven; puede encontrar una descripción detallada de cada uno de estos elementos en la documentación del [complemento Maven de Azure Web Apps]. Dicho esto, hay varios valores que merece la pena destacar en este artículo:

| Elemento | DESCRIPCIÓN |
|---|---|
| `<version>` | Especifica la versión del [complemento Maven de Azure Web Apps]. Debe comprobar la versión que aparece en el [repositorio central de Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) para asegurarse de que está utilizando la versión más reciente. |
| `<authentication>` | Especifica la información de autenticación de Azure que, en este ejemplo, incluye un elemento `<serverId>` que contiene `azure-auth`; Maven utiliza ese valor para buscar los valores de la entidad de servicio de Azure en el archivo *settings.xml* que se definió en una sección anterior de este artículo. |
| `<resourceGroup>` | Especifica el grupo de recursos de destino, que es `wingtiptoysresources` en este ejemplo. Se creará este grupo de recursos durante la implementación si todavía no existe. |
| `<appName>` | Especifica el nombre de destino de la aplicación web. En este ejemplo, el nombre de destino es `maven-linux-app-${maven.build.timestamp}`, donde el sufijo `${maven.build.timestamp}` se anexa en este ejemplo para evitar conflictos. (La marca de tiempo es opcional; puede especificar cualquier cadena única para el nombre de la aplicación). |
| `<region>` | Especifica la región de destino, que en este ejemplo es `westus`. (Puede encontrar una lista completa en la documentación del [complemento Maven de Azure Web Apps]). |
| `<containerSettings>` | Especifica las propiedades que contienen el nombre y la dirección URL del contenedor. |
| `<appSettings>` | Especifica los valores únicos de Maven que se deben usar durante la implementación de la aplicación web en Azure. En este ejemplo, un elemento `<property>` contiene un par nombre/valor de elementos secundarios que especifican el puerto de la aplicación. |

> [!NOTE]
>
> Las opciones para cambiar el número de puerto en este ejemplo solo son necesarias si va a usar un puerto distinto al predeterminado.
>

1. En el símbolo del sistema o la ventana de terminal que usó anteriormente, vuelva a compilar el archivo JAR con Maven si ha realizado algún cambio en el archivo *pom.xml*; por ejemplo:
   ```shell
   mvn clean package
   ```

1. Implemente la aplicación web en Azure mediante Maven; por ejemplo:
   ```shell
   mvn azure-webapp:deploy
   ```

Maven implementará la aplicación web en Azure; si la aplicación web no existe, se creará.

> [!NOTE]
>
> Si la región que especifique en el elemento `<region>` del archivo *pom.xml* no tiene suficientes servidores disponibles al iniciar la implementación, aparecerá un error parecido al del siguiente ejemplo:
>
> ```
> [INFO] Start deploying to Web App maven-linux-app-20170804...
> [INFO] ------------------------------------------------------------------------
> [INFO] BUILD FAILURE
> [INFO] ------------------------------------------------------------------------
> [INFO] Total time: 31.059 s
> [INFO] Finished at: 2017-08-04T12:15:47-07:00
> [INFO] Final Memory: 51M/279M
> [INFO] ------------------------------------------------------------------------
> [ERROR] Failed to execute goal com.microsoft.azure:azure-webapp-maven-plugin:0.1.3:deploy (default-cli) on project gs-spring-boot-docker: null: MojoExecutionException: CloudException: OnError while emitting onNext value: retrofit2.Response.class
> ```
>
> Si esto ocurre, puede especificar otra región y volver a ejecutar el comando Maven para implementar la aplicación.
>
>

Cuando se haya implementado la web, podrá administrarla mediante [Azure Portal].

* La aplicación web aparecerá en **App Services**:

   ![Aplicación web en la lista de App Services de Azure Portal][AP01]

* Y la dirección URL de la aplicación web se mostrará en la sección de **información general** de la aplicación web:

   ![Determinar la dirección URL de la aplicación web][AP02]

## <a name="next-steps"></a>Pasos siguientes

Para más información acerca de las diferentes tecnologías que se tratan en este artículo, consulte los artículos siguientes:

* [Complemento Maven de Azure Web Apps]

* [Inicio de sesión en Azure desde la CLI de Azure](/azure/xplat-cli-connect)

* [Creación de una entidad de servicio de Azure con la CLI de Azure 2.0](/cli/azure/create-an-azure-service-principal-azure-cli)

* [Referencia de configuración de Maven](https://maven.apache.org/settings.html)

* [Complemento Docker para Maven]

<!-- URL List -->

[Interfaz de la línea de comandos (CLI) de Azure]: /cli/azure/overview
[Azure Container Service (AKS)]: https://azure.microsoft.com/services/container-service/
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Azure Portal]: https://portal.azure.com/
[Complemento Maven de Azure Web Apps]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin
[Create a private Docker container registry using the Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Using a custom Docker image for Azure Web App on Linux]: /azure/app-service/containers/tutorial-custom-docker-image
[Docker]: https://www.docker.com/
[Complemento Docker para Maven]: https://github.com/spotify/docker-maven-plugin
[cuenta de Azure gratuita]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[ventajas como suscriptor de MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot on Docker Getting Started]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[SB01]: ./media/deploy-spring-boot-java-app-from-container-registry-using-maven-plugin/SB01.png
[CR01]: ./media/deploy-spring-boot-java-app-from-container-registry-using-maven-plugin/CR01.png
[AP01]: ./media/deploy-spring-boot-java-app-from-container-registry-using-maven-plugin/AP01.png
[AP02]: ./media/deploy-spring-boot-java-app-from-container-registry-using-maven-plugin/AP02.png
[TL01]: ./media/deploy-spring-boot-java-app-from-container-registry-using-maven-plugin/TL01.png
