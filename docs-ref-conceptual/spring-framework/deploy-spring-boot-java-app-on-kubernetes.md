---
title: "Implementación de una aplicación Spring Boot en Kubernetes en Azure Container Service"
description: "Este tutorial le guiará por los pasos necesarios para implementar una aplicación Spring Boot en un clúster de Kubernetes en Microsoft Azure."
services: container-service
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
keywords: Spring, Spring Boot, Spring Framework, Kubernetes
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: java
ms.topic: article
ms.date: 10/11/2017
ms.author: asirveda;robmcm
ms.custom: mvc
ms.openlocfilehash: 44c20e9084d53fa366137fc191726aaa4be177f2
ms.sourcegitcommit: 7f8538e41c833deb69c300ad3431a431136a1f3e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/24/2017
---
# <a name="deploy-a-spring-boot-application-on-a-kubernetes-cluster-in-the-azure-container-service"></a>Implementación de una aplicación de Spring Boot en un clúster de Kubernetes en Azure Container Service

**[Spring Framework]** es un popular marco de código abierto que ayuda a los desarrolladores de Java a crear aplicaciones de API, móviles y web. Este tutorial utiliza una aplicación de ejemplo creada mediante [Spring arranque], un enfoque basado en la convención para usar Spring para empezar a trabajar rápidamente.

**[Kubernetes]** y **[cliente de Docker]** son soluciones de código abierto que ayudan a los desarrolladores a automatizar la implementación, el escalado y la administración de sus aplicaciones que se ejecutan en contenedores.

Este tutorial le guía en la combinación de estas dos populares tecnologías de código abierto para desarrollar e implementar una aplicación Spring Boot en Microsoft Azure. Más en concreto, *[Spring arranque]* se usa para el desarrollo de aplicaciones, *[Kubernetes]* para la implementación de contenedores y [Azure Container Service (ACS)] para hospedar su aplicación.

### <a name="prerequisites"></a>Requisitos previos

* Una suscripción de Azure. Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN] o registrarse para obtener una [cuenta de Azure gratuita].
* La [Interfaz de la línea de comandos (CLI) de Azure].
* Un [kit para desarrolladores de Java (JDK)] actualizado.
* La herramienta de compilación [Maven] de Apache (versión 3).
* Un cliente [Git].
* Un [cliente de Docker].

> [!NOTE]
>
> Dados los requisitos de virtualización de este tutorial, los pasos que se describen en este artículo no se pueden seguir en una máquina virtual; es preciso usar un equipo físico con características de virtualización habilitadas.
>

## <a name="create-the-spring-boot-on-docker-getting-started-web-app"></a>Creación de la aplicación web Spring Boot on Docker Getting Started

Los siguientes pasos le guían a través de la creación de una aplicación web Spring Boot y la realización de pruebas de la misma de forma local.

1. Abra el símbolo del sistema, cree un directorio local para alojar la aplicación y cambie a dicho directorio, por ejemplo:
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   -- o --
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. Clone el proyecto de ejemplo [Spring Boot on Docker Getting Started] en el directorio.
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. Cambie de directorio al del proyecto completado.
   ```
   cd gs-spring-boot-docker
   cd complete
   ```

1. Utilice Maven para compilar y ejecutar la aplicación de ejemplo.
   ```
   mvn package spring-boot:run
   ```

1. Pruebe la aplicación web examinando http://localhost:8080 o con el siguiente comando `curl`:
   ```
   curl http://localhost:8080
   ```

1. Debería aparecer el siguiente mensaje: **Hello Docker World**

   ![Examen local de aplicación de ejemplo][SB01]

## <a name="create-an-azure-container-registry-using-the-azure-cli"></a>Creación de una instancia de Azure Container Registry mediante la CLI de Azure

1. Abra el símbolo del sistema.

1. Inicie sesión en una cuenta de Azure:
   ```azurecli
   az login
   ```

1. Cree un grupo de recursos para los recursos de Azure que se usan en este tutorial.
   ```azurecli
   az group create --name=wingtiptoys-kubernetes --location=eastus
   ```

1. Crear una instancia de Azure Container Registry en el grupo de recursos. El tutorial inserta la aplicación de ejemplo en forma de imagen Docker en este registro en los pasos posteriores. Reemplace `wingtiptoysregistry` por un nombre único para el registro.
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoys-kubernetes--location eastus \
    --name wingtiptoysregistry --sku Basic
   ```

## <a name="push-your-app-to-the-container-registry"></a>Inserción de una aplicación en el registro de contenedor

1. Navegue hasta el directorio de configuración de la instalación de Maven (valor predeterminado ~/.m2/ o C:\Users\username\.m2) y abra el archivo *settings.xml* con un editor de texto.

1. Recupere la contraseña del registro de contenedor de la CLI de Azure.
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```

   ```json
   {
  "name": "password",
  "value": "AbCdEfGhIjKlMnOpQrStUvWxYz"
   }
   ```

1. Agregue el identificador y la contraseña de Azure Container Registry a una nueva colección `<server>` del archivo *settings.xml*.
`id` y `username` son el nombre del registro. Use el valor `password` del comando anterior (sin comillas).

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

1. Navegue hasta el directorio de proyecto completado de la aplicación Spring Boot (por ejemplo, "*C:\SpringBoot\gs-spring-boot-docker\complete*"o"*/users/robert/SpringBoot/gs-spring-boot-docker/complete*") y abra el archivo *pom.xml* con un editor de texto.

1. Actualice la colección `<properties>` del archivo *pom.xml* con el valor del servidor de inicio de sesión de Azure Container Registry.

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

1. Actualice la colección `<plugins>` del archivo *pom.xml* de modo que `<plugin>` contiene la dirección del servidor de inicio de sesión y el nombre de registro de Azure Container Registry.

   ```xml
   <plugin>
      <groupId>com.spotify</groupId>
      <artifactId>docker-maven-plugin</artifactId>
      <version>0.4.11</version>
      <configuration>
         <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
         <dockerDirectory>src/main/docker</dockerDirectory>
         <resources>
            <resource>
               <targetPath>/</targetPath>
               <directory>${project.build.directory}</directory>
               <include>${project.build.finalName}.jar</include>
            </resource>
         </resources>
         <serverId>wingtiptoysregistry</serverId>
         <registryUrl>https://wingtiptoysregistry.azurecr.io</registryUrl>
      </configuration>
   </plugin>
   ```

1. Navegue hasta el directorio de proyecto completado de la aplicación Spring Boot y ejecute el siguiente comando para crear el contenedor Docker e insertar la imagen en el registro:

   ```
   mvn package docker:build -DpushImage
   ```

> [!NOTE]
>
>  Cuando Maven inserta la imagen en Azure, puede recibir un mensaje de error similar a uno de los siguientes:
>
> * `[ERROR] Failed to execute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: no basic auth credentials`
>
> * `[ERROR] Failed to execute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: Incomplete Docker registry authorization credentials. Please provide all of username, password, and email or none.`
>
> Si aparece este error, inicie sesión en Azure desde la línea de comandos de Docker.
>
> `docker login -u wingtiptoysregistry -p "AbCdEfGhIjKlMnOpQrStUvWxYz" wingtiptoysregistry.azurecr.io`
>
> Después, inserte el contenedor:
>
> `docker push wingtiptoysregistry.azurecr.io/gs-spring-boot-docker`

## <a name="create-a-kubernetes-cluster-on-acs-using-the-azure-cli"></a>Creación de un clúster de Kubernetes en ACS mediante la CLI de Azure

1. Cree un clúster de Kubernetes en Azure Container Service. El siguiente comando crea un clúster de *Kubernetes* en el grupo de recursos *wingtiptoys-kubernetes*, con *wingtiptoys-objeto containerservice* como nombre de clúster y *wingtiptoys-kubernetes* como prefijo de DNS:
   ```azurecli
   az acs create --orchestrator-type=kubernetes --resource-group=wingtiptoys-kubernetes \ 
    --name=wingtiptoys-containerservice --dns-prefix=wingtiptoys-kubernetes
   ```
   Esta operación puede tardar un tiempo en completarse.

1. Instale `kubectl` mediante la CLI de Azure. Los usuarios de Linux pueden tener anteceder este comando con `sudo`, ya que implementa la CLI de Kubernetes en `/usr/local/bin`.
   ```azurecli
   az acs kubernetes install-cli
   ```

1. Descargar la información de configuración del clúster para que pueda administrar el clúster desde la interfaz web de Kubernetes y `kubectl`. 
   ```azurecli
   az acs kubernetes get-credentials --resource-group=wingtiptoys-kubernetes  \ 
    --name=wingtiptoys-containerservice
   ```

## <a name="deploy-the-image-to-your-kubernetes-cluster"></a>Implementación de la imagen en un clúster de Kubernetes

Este tutorial implementa la aplicación mediante `kubectl` y, después, le permite explorar la implementación a través de la interfaz de web de Kubernetes.

### <a name="deploy-with-the-kubernetes-web-interface"></a>Implementación con la interfaz web de Kubernetes

1. Abra el símbolo del sistema.

1. Abra el sitio web de configuración del clúster de Kubernetes en el explorador predeterminado:
   ```
   az acs kubernetes browse --resource-group=wingtiptoys-kubernetes --name=wingtiptoys-containerservice
   ```

1. Cuando el sitio web para la configuración de Kubernetes se abra en el explorador, haga clic en el vínculo para **implementar una aplicación en contenedores**:

   ![Sitio web para la configuración de Kubernetes][KB01]

1. Cuando se muestra la página **Deploy a containerized app** (Implementar una aplicación en contenedor), especifique las opciones siguientes:

   a. Seleccione **Specify app details below** (Especificar detalles de la aplicación a continuación).

   b. Escriba el nombre de la aplicación Spring Boot en **App name** (Nombre de aplicación); por ejemplo: "*gs-spring-boot-docker*".

   c. Escriba el servidor de inicio de sesión y la imagen del contenedor de anteriormente en **Container image** (Imagen del contenedor); por ejemplo: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*".

   d. Elija **External** (Externo) en **Service** (Servicio).

   e. Especifique los puertos interno y externo en los cuadros de texto **Port** (Puerto) y **Target port** (Puerto de destino).

   ![Sitio web para la configuración de Kubernetes][KB02]


1. Haga clic en **Deploy** (Implementar) para implementar el contenedor.

   ![Implementar un contenedor][KB05]

1. Una vez que la aplicación se haya implementado, verá la aplicación Spring Boot en **Services** (Servicios).

   ![Servicios de Kubernetes][KB06]

1. Si hace clic en el vínculo de **External endpoints** (Puntos de conexión externos), puede ver que la aplicación Spring Boot se ejecuta en Azure.

   ![Servicios de Kubernetes][KB07]

   ![Examen de la aplicación de ejemplo en Azure][SB02]


### <a name="deploy-with-kubectl"></a>Implementación con kubectl

1. Abra el símbolo del sistema.

1. Ejecute el contenedor en el clúster de Kubernetes mediante el comando `kubectl run`. Proporcione un nombre de servicio para la aplicación en Kubernetes y el nombre de la imagen completa. Por ejemplo:
   ```
   kubectl run gs-spring-boot-docker --image=wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest
   ```
   En este comando:

   * El nombre del contenedor `gs-spring-boot-docker` se especifica inmediatamente después del comando `run`

   * El parámetro `--image` especifica la combinación de servidor de inicio de sesión y nombre de imagen como `wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest`

1. Exponga externamente el clúster Kubernetes mediante el comando `kubectl expose`. Especifique el nombre del servicio, el puerto TCP de acceso público utilizado para acceder a la aplicación y el puerto de destino interno en que escucha la aplicación. Por ejemplo:
   ```
   kubectl expose deployment gs-spring-boot-docker --type=LoadBalancer --port=80 --target-port=8080
   ```
   En este comando:

   * El nombre del contenedor `gs-spring-boot-docker` se especifica inmediatamente después del comando `expose deployment`

   * El parámetro `--type` especifica que el clúster utiliza equilibrador de carga

   * El parámetro `--port` especifica el puerto TCP de acceso público, el 80. El acceso a la aplicación se realiza a través de este puerto.

   * El parámetro `--target-port` especifica el puerto TCP interno, el 8080. El equilibrador de carga reenvía las solicitudes a la aplicación en este puerto.

1. Una vez que la aplicación se implementa en el clúster, consulte la dirección IP externa y ábrala en el explorador web:

   ```
   kubectl get services -o jsonpath={.items[*].status.loadBalancer.ingress[0].ip} --namespace=${namespace}
   ```

   ![Examen de la aplicación de ejemplo en Azure][SB02]


## <a name="next-steps"></a>Pasos siguientes

Para más información acerca del uso de Spring Boot en Azure, consulte los siguientes artículos:

* [Implementación de una aplicación de Spring Boot en Azure App Service](deploy-spring-boot-java-web-app-on-azure.md)
* [Implementación de una aplicación de Spring Boot en Linux en Azure Container Service](deploy-spring-boot-java-app-on-linux.md)

Para obtener más información sobre el uso de Azure con Java, vea el [Centro para desarrolladores de Java de Azure] y [Java Tools for Visual Studio Team Services] (Herramientas de Java para Visual Studio Team Services).

Para más información acerca del proyecto de ejemplo Spring Boot on Docker, consulte [Spring Boot on Docker Getting Started].

Los vínculos siguientes proporcionan información adicional acerca de cómo crear aplicaciones Spring Boot:

* Para más información acerca de cómo crear una sencilla aplicación Spring Boot, consulte Initializr Spring en https://start.spring.io/.

Los vínculos siguientes proporcionan información adicional acerca del uso de Kubernetes con Azure:

* [Implementación de un clúster de Kubernetes para los contenedores de Linux](https://docs.microsoft.com/azure/container-service/container-service-kubernetes-walkthrough)
* [Uso de la interfaz de usuario web de Kubernetes con Azure Container Service](https://docs.microsoft.com/azure/container-service/container-service-kubernetes-ui)

Para más información acerca del uso de la interfaz de línea de comandos de Kubernetes, consulte la guía de usuario de **kubectl** en <https://kubernetes.io/docs/user-guide/kubectl/>.

El sitio web de Kubernetes tiene varios artículos que tratan el uso de imágenes en registros privados:

* [Configure Service Accounts for Pods] (Configurar cuentas de servicio para pods)
* [Espacios de nombres]
* [Pull an Image from a Private Registry] (Extraer una imagen de un registro privado)

Para ver más ejemplos de cómo usar imágenes de Docker personalizadas con Azure, consulte [Uso de una imagen personalizada de Docker para Web App on Linux de Azure].

<!-- URL List -->

[Interfaz de la línea de comandos (CLI) de Azure]: /cli/azure/overview
[Azure Container Service (ACS)]: https://azure.microsoft.com/services/container-service/
[Centro para desarrolladores de Java de Azure]: https://azure.microsoft.com/develop/java/
[Azure portal]: https://portal.azure.com/
[Create a private Docker container registry using the Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Uso de una imagen personalizada de Docker para Web App on Linux de Azure]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[cliente de Docker]: https://www.docker.com/
[cuenta de Azure gratuita]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[kit para desarrolladores de Java (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Kubernetes]: https://kubernetes.io/
[Kubernetes Command-Line Interface (kubectl)]: https://kubernetes.io/docs/user-guide/kubectl-overview/
[Maven]: http://maven.apache.org/
[ventajas como suscriptor de MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring arranque]: http://projects.spring.io/spring-boot/
[Spring Boot on Docker Getting Started]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/
[Configure Service Accounts for Pods]: https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/ (Configurar cuentas de servicio para pods)
[Espacios de nombres]: https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/
[Pull an Image from a Private Registry]: https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/ (Extraer una imagen de un registro privado)

<!-- IMG List -->

[SB01]: ./media/deploy-spring-boot-java-app-on-kubernetes/SB01.png
[SB02]: ./media/deploy-spring-boot-java-app-on-kubernetes/SB02.png

[AR01]: ./media/deploy-spring-boot-java-app-on-kubernetes/AR01.png
[AR02]: ./media/deploy-spring-boot-java-app-on-kubernetes/AR02.png
[AR03]: ./media/deploy-spring-boot-java-app-on-kubernetes/AR03.png
[AR04]: ./media/deploy-spring-boot-java-app-on-kubernetes/AR04.png

[KB01]: ./media/deploy-spring-boot-java-app-on-kubernetes/KB01.png
[KB02]: ./media/deploy-spring-boot-java-app-on-kubernetes/KB02.png
[KB03]: ./media/deploy-spring-boot-java-app-on-kubernetes/KB03.png
[KB04]: ./media/deploy-spring-boot-java-app-on-kubernetes/KB04.png
[KB05]: ./media/deploy-spring-boot-java-app-on-kubernetes/KB05.png
[KB06]: ./media/deploy-spring-boot-java-app-on-kubernetes/KB06.png
[KB07]: ./media/deploy-spring-boot-java-app-on-kubernetes/KB07.png
