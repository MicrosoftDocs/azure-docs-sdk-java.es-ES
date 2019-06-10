---
title: Implementación de una aplicación de Spring Boot en Kubernetes en Azure Kubernetes Service
description: Este tutorial le guiará por los pasos necesarios para implementar una aplicación Spring Boot en un clúster de Kubernetes en Microsoft Azure.
services: container-service
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 12/19/2018
ms.devlang: java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.custom: mvc
ms.openlocfilehash: 9ab781d27e8968ab867efc65f3ac422ac6253a6a
ms.sourcegitcommit: 394521c47ac9895d00d9f97535cc9d1e27d08fe9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/28/2019
ms.locfileid: "66270858"
---
# <a name="deploy-a-spring-boot-application-on-a-kubernetes-cluster-in-the-azure-kubernetes-service"></a>Implementación de una aplicación de Spring Boot en un clúster de Kubernetes en Azure Kubernetes Service

**[Kubernetes]** y **[Docker]** son soluciones de código abierto que ayudan a los desarrolladores a automatizar la implementación, el escalado y la administración de sus aplicaciones que se ejecutan en contenedores.

Este tutorial le indica cómo combinar estas dos populares tecnologías de código abierto para desarrollar e implementar una aplicación de Spring Boot en Microsoft Azure. Concretamente, *[Spring Boot]* se usa para el desarrollo de aplicaciones, *[Kubernetes]* para la implementación de contenedores y [Azure Kubernetes Service (AKS)] para hospedar la aplicación.

### <a name="prerequisites"></a>Requisitos previos

* Una suscripción de Azure. Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN] o registrarse para obtener una [cuenta de Azure gratuita].
* La [Interfaz de la línea de comandos (CLI) de Azure].
* Un kit de desarrollo de Java (JDK) admitido Para más información sobre los JDK disponibles para desarrollar en Azure, consulte <https://aka.ms/azure-jdks>.
* La herramienta de compilación [Maven] de Apache (versión 3).
* Un cliente [Git].
* Un cliente de [Docker].

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

1. Para probar la aplicación web, vaya a `curl` o use el siguiente comando `http://localhost:8080`:
   ```
   curl http://localhost:8080
   ```

1. Debería ver el mensaje siguiente mostrado: **Hello Docker World**

   ![Examen local de aplicación de ejemplo][SB01]

## <a name="create-an-azure-container-registry-using-the-azure-cli"></a>Creación de una instancia de Azure Container Registry mediante la CLI de Azure

1. Abra el símbolo del sistema.

1. Inicie sesión en una cuenta de Azure:
   ```azurecli
   az login
   ```

1. Elija la suscripción de Azure:
   ```azurecli
   az account set -s <YourSubscriptionID>
   ```

1. Cree un grupo de recursos para los recursos de Azure que se usan en este tutorial.
   ```azurecli
   az group create --name=wingtiptoys-kubernetes --location=eastus
   ```

1. Crear una instancia de Azure Container Registry en el grupo de recursos. El tutorial inserta la aplicación de ejemplo en forma de imagen Docker en este registro en los pasos posteriores. Reemplace `wingtiptoysregistry` por un nombre único para el registro.
   ```azurecli
   az acr create --resource-group wingtiptoys-kubernetes --location eastus \
    --name wingtiptoysregistry --sku Basic
   ```

## <a name="push-your-app-to-the-container-registry-via-jib"></a>Inserción de una aplicación en el registro de contenedor mediante Jib

1. Inicie sesión en Azure Container Registry desde la CLI de Azure.
   ```azurecli
   # set the default name for Azure Container Registry, otherwise you will need to specify the name in "az acr login"
   az configure --defaults acr=wingtiptoysregistry
   az acr login
   ```

1. Navegue hasta el directorio de proyecto completado de la aplicación Spring Boot (por ejemplo, "*C:\SpringBoot\gs-spring-boot-docker\complete*"o" */users/robert/SpringBoot/gs-spring-boot-docker/complete*") y abra el archivo *pom.xml* con un editor de texto.

1. Actualice la colección `<properties>` del archivo *pom.xml* con el nombre de su registro de Azure Container Registry y la última versión de [jib-maven-plugin](https://github.com/GoogleContainerTools/jib/tree/master/jib-maven-plugin).

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <jib-maven-plugin.version>1.2.0</jib-maven-plugin.version>
      <java.version>1.8</java.version>
   </properties>
   ```

1. Actualice la colección `<plugins>` en el archivo *pom.xml* para que `<plugin>` contenga `jib-maven-plugin`.

   ```xml
   <plugin>
     <artifactId>jib-maven-plugin</artifactId>
     <groupId>com.google.cloud.tools</groupId>
     <version>${jib-maven-plugin.version}</version>
     <configuration>
        <from>
            <image>openjdk:8-jre-alpine</image>
        </from>
        <to>
            <image>${docker.image.prefix}/${project.artifactId}</image>
        </to>
     </configuration>
   </plugin>
   ```

1. Vaya al directorio de proyecto completado de la aplicación de Spring Boot y ejecute el siguiente comando para crear la imagen e insertarla en el registro:

   ```cmd
   mvn compile jib:build
   ```

> [!NOTE]
>
> Debido al problema de seguridad de la Cli de Azure y Azure Container Registry, la credencial creada mediante `az acr login` es válida durante una hora; si aparece el error *401 no autorizado*, puede ejecutar de nuevo el comando `az acr login -n <your registry name>` para volver a autenticar.
>

## <a name="create-a-kubernetes-cluster-on-aks-using-the-azure-cli"></a>Creación de un clúster de Kubernetes en AKS mediante la CLI de Azure

1. Cree un clúster de Kubernetes en Azure Kubernetes Service. El siguiente comando crea un clúster de *Kubernetes* en el grupo de recursos *wingtiptoys-kubernetes*, con *wingtiptoys-akscluster* como nombre de clúster y *wingtiptoys-kubernetes* como prefijo de DNS:
   ```azurecli
   az aks create --resource-group=wingtiptoys-kubernetes --name=wingtiptoys-akscluster \ 
    --dns-name-prefix=wingtiptoys-kubernetes --generate-ssh-keys
   ```
   Esta operación puede tardar un tiempo en completarse.

1. Cuando se usa Azure Container Registry (ACR) con Azure Kubernetes Service (AKS), debe conceder a Azure Kubernetes Service acceso de incorporación de cambios en Azure Container Registry. De forma predeterminada, Azure crea una entidad de servicio al crear Azure Kubernetes Service. Ejecute los siguientes scripts de Bash o Powershell para conceder a AKS acceso a ACR; consulte más información en [Autenticación con Azure Container Registry desde Azure Kubernetes Service (AKS)].

```bash
   # Get the id of the service principal configured for AKS
   CLIENT_ID=$(az aks show -g wingtiptoys-kubernetes -n wingtiptoys-akscluster --query "servicePrincipalProfile.clientId" --output tsv)
   
   # Get the ACR registry resource id
   ACR_ID=$(az acr show -g wingtiptoys-kubernetes -n wingtiptoysregistry --query "id" --output tsv)
   
   # Create role assignment
   az role assignment create --assignee $CLIENT_ID --role acrpull --scope $ACR_ID
```

  -- o --

```PowerShell
   # Get the id of the service principal configured for AKS
   $CLIENT_ID = az aks show -g wingtiptoys-kubernetes -n wingtiptoys-akscluster --query "servicePrincipalProfile.clientId" --output tsv
   
   # Get the ACR registry resource id
   $ACR_ID = az acr show -g wingtiptoys-kubernetes -n wingtiptoysregistry --query "id" --output tsv
   
   # Create role assignment
   az role assignment create --assignee $CLIENT_ID --role acrpull --scope $ACR_ID
```

1. Instale `kubectl` mediante la CLI de Azure. Los usuarios de Linux pueden tener anteceder este comando con `sudo`, ya que implementa la CLI de Kubernetes en `/usr/local/bin`.
   ```azurecli
   az aks install-cli
   ```

1. Descargar la información de configuración del clúster para que pueda administrar el clúster desde la interfaz web de Kubernetes y `kubectl`. 
   ```azurecli
   az aks get-credentials --resource-group=wingtiptoys-kubernetes --name=wingtiptoys-akscluster
   ```

## <a name="deploy-the-image-to-your-kubernetes-cluster"></a>Implementación de la imagen en un clúster de Kubernetes

Este tutorial implementa la aplicación mediante `kubectl` y, después, le permite explorar la implementación a través de la interfaz de web de Kubernetes.

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
   kubectl get services -o jsonpath={.items[*].status.loadBalancer.ingress[0].ip} --namespace=default
   ```

   ![Examen de la aplicación de ejemplo en Azure][SB02]



### <a name="deploy-with-the-kubernetes-web-interface"></a>Implementación con la interfaz web de Kubernetes

1. Abra el símbolo del sistema.

1. Abra el sitio web de configuración del clúster de Kubernetes en el explorador predeterminado:
   ```
   az aks browse --resource-group=wingtiptoys-kubernetes --name=wingtiptoys-akscluster
   ```

1. Cuando el sitio web para la configuración de Kubernetes se abra en el explorador, haga clic en el vínculo para **implementar una aplicación en contenedores**:

   ![Sitio web para la configuración de Kubernetes][KB01]

1. Cuando se muestra la página **Resource Creation** (Creación de recursos), especifique las opciones siguientes:

   a. Seleccione **CREATE AN APP** (Crear una aplicación).

   b. Escriba el nombre de la aplicación Spring Boot en **App name** (Nombre de aplicación); por ejemplo: "*gs-spring-boot-docker*".

   c. Escriba el servidor de inicio de sesión y la imagen del contenedor de anteriormente en **Container image** (Imagen del contenedor); por ejemplo: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*".

   d. Elija **External** (Externo) en **Service** (Servicio).

   e. Especifique los puertos interno y externo en los cuadros de texto **Port** (Puerto) y **Target port** (Puerto de destino).

   ![Sitio web para la configuración de Kubernetes][KB02]


1. Haga clic en **Deploy** (Implementar) para implementar el contenedor.

   ![Implementación de Kubernetes][KB05]

1. Una vez que la aplicación se haya implementado, verá la aplicación Spring Boot en **Services** (Servicios).

   ![Servicios de Kubernetes][KB06]

1. Si hace clic en el vínculo de **External endpoints** (Puntos de conexión externos), puede ver que la aplicación Spring Boot se ejecuta en Azure.

   ![Servicios de Kubernetes][KB07]

   ![Examen de la aplicación de ejemplo en Azure][SB02]

## <a name="next-steps"></a>Pasos siguientes

Para más información acerca de Spring y Azure, vaya al centro de documentación de Azure.

> [!div class="nextstepaction"]
> [Spring en Azure](/java/azure/spring-framework)

### <a name="additional-resources"></a>Recursos adicionales

Para más información acerca del uso de Spring Boot en Azure, consulte el siguiente artículo:

* [Implementación de una aplicación de Spring Boot en Azure App Service](deploy-spring-boot-java-web-app-on-azure.md)

Para más información sobre el uso de Azure con Java, consulte [Azure para desarrolladores de Java] y [Working with Azure DevOps and Java] (Trabajo con Azure DevOps y Java).

Para más información sobre cómo implementar una aplicación Java en Kubernetes con Visual Studio Code, consulte los [tutoriales de Visual Studio Code para Java].

Para más información acerca del proyecto de ejemplo Spring Boot on Docker, consulte [Spring Boot on Docker Getting Started].

Los vínculos siguientes proporcionan información adicional acerca de cómo crear aplicaciones Spring Boot:

* Para más información acerca de cómo crear una sencilla aplicación de Spring Boot, consulte Spring Initializr en https://start.spring.io/.

Los vínculos siguientes proporcionan información adicional acerca del uso de Kubernetes con Azure:

* [Introducción a los clústeres de Kubernetes en Azure Kubernetes Service](/azure/aks/intro-kubernetes)

Para más información acerca de cómo usar la interfaz de línea de comandos de Kubernetes, consulte la guía de usuario de **kubectl** en <https://kubernetes.io/docs/user-guide/kubectl/>.

El sitio web de Kubernetes tiene varios artículos que tratan el uso de imágenes en registros privados:

* [Configure Service Accounts for Pods] (Configurar cuentas de servicio para pods)
* [Espacios de nombres]
* [Pull an Image from a Private Registry] (Extraer una imagen de un registro privado)

Para ver más ejemplos de cómo usar imágenes de Docker personalizadas con Azure, consulte [Uso de una imagen personalizada de Docker para Web App on Linux de Azure].

Para obtener más información sobre la ejecución de forma iterativa y la depuración de contenedores directamente en Azure Kubernetes Service (AKS) con Azure Dev Spaces, consulte [Introducción a Azure Dev Spaces con Java].

<!-- URL List -->

[Interfaz de la línea de comandos (CLI) de Azure]: /cli/azure/overview
[Azure Kubernetes Service (AKS)]: https://azure.microsoft.com/services/kubernetes-service/
[Azure para desarrolladores de Java]: /java/azure/
[Azure portal]: https://portal.azure.com/
[Create a private Docker container registry using the Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Uso de una imagen personalizada de Docker para Web App on Linux de Azure]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[cuenta de Azure gratuita]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Working with Azure DevOps and Java]: /azure/devops/java/ (Trabajo con Azure DevOps y Java)
[Kubernetes]: https://kubernetes.io/
[Kubernetes Command-Line Interface (kubectl)]: https://kubernetes.io/docs/user-guide/kubectl-overview/
[Maven]: http://maven.apache.org/
[ventajas como suscriptor de MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot on Docker Getting Started]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/
[Configure Service Accounts for Pods]: https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/ (Configurar cuentas de servicio para pods)
[Espacios de nombres]: https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/
[Pull an Image from a Private Registry]: https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/ (Extraer una imagen de un registro privado)

[Java Development Kit (JDK)]: https://aka.ms/azure-jdks
<!-- http://www.oracle.com/technetwork/java/javase/downloads/ -->

<!-- Newly added -->
[Autenticación con Azure Container Registry desde Azure Kubernetes Service (AKS)]: /azure/container-registry/container-registry-auth-aks/
[Tutoriales de Visual Studio Code para Java]: https://code.visualstudio.com/docs/java/java-kubernetes/
[Introducción a Azure Dev Spaces con Java]: https://docs.microsoft.com/en-us/azure/dev-spaces/get-started-java
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
