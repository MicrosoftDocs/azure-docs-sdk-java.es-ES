---
title: Implementación de una aplicación Spring Boot mediante el complemento Fabric8 para Maven
description: En este tutorial se le guiará por los pasos necesarios para implementar una aplicación Spring Boot en Microsoft Azure con el complemento Fabric8 para Apache Maven.
services: container-service
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: yuwzho;robmcm
ms.date: 02/01/2018
ms.devlang: java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: f05dca50f84b27f157892d63cda02286c6755795
ms.sourcegitcommit: 5282a51bf31771671df01af5814df1d2b8e4620c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/28/2018
ms.locfileid: "37090818"
---
# <a name="deploy-a-spring-boot-app-using-the-fabric8-maven-plugin"></a>Implementación de una aplicación Spring Boot mediante el complemento Fabric8 para Maven

**[Fabric8]** es una solución de código abierto basada en **[Kubernetes]** que permite que los desarrolladores creen aplicaciones en los contenedores Linux.

En este tutorial se explica cómo usar el complemento Fabric8 para Maven para desarrollar e implementar una aplicación en un host Linux en [Azure Container Service (AKS)].

## <a name="prerequisites"></a>requisitos previos

Para realizar los pasos de este tutorial, necesitará tener los siguientes requisitos previos:

* Una suscripción de Azure. Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN] o registrarse para obtener una [cuenta de Azure gratuita].
* La [Interfaz de la línea de comandos (CLI) de Azure].
* Un [kit para desarrolladores de Java (JDK)] actualizado.
* La herramienta de compilación [Maven] de Apache (versión 3).
* Un cliente [Git].
* Un [Docker].

> [!NOTE]
>
> Dados los requisitos de virtualización de este tutorial, los pasos que se describen en este artículo no se pueden seguir en una máquina virtual; es preciso usar un equipo físico con características de virtualización habilitadas.
>

## <a name="create-the-spring-boot-on-docker-getting-started-web-app"></a>Creación de la aplicación web Spring Boot on Docker Getting Started

Los siguientes pasos le guían a través de la creación de una aplicación web Spring Boot y la realización de pruebas de la misma de forma local.

1. Abra el símbolo del sistema, cree un directorio local para alojar la aplicación y cambie a dicho directorio, por ejemplo:
   ```shell
   md /home/GenaSoto/SpringBoot
   cd /home/GenaSoto/SpringBoot
   ```
   -- o --
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```

1. Clone el proyecto de ejemplo [Spring Boot on Docker Getting Started] en el directorio.
   ```shell
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. Cambie de directorio al del proyecto finalizado, por ejemplo:
   ```shell
   cd gs-spring-boot-docker/complete
   ```
   -- o --
   ```shell
   cd gs-spring-boot-docker\complete
   ```

1. Utilice Maven para compilar y ejecutar la aplicación de ejemplo.
   ```shell
   mvn clean package spring-boot:run
   ```

1. Para probar la aplicación web, vaya a `curl` o use el siguiente comando http://localhost:8080:
   ```shell
   curl http://localhost:8080
   ```

   Debería aparecer el siguiente mensaje: **Hello Docker World**.

   ![Examinar localmente la aplicación de ejemplo][SB01]


## <a name="install-the-kubernetes-command-line-interface-and-create-an-azure-resource-group-using-the-azure-cli"></a>Instalación de la interfaz de la línea de comandos de Kubernetes y creación de un grupo de recursos de Azure con la CLI de Azure

1. Abra el símbolo del sistema.

1. Escriba el comando siguiente para iniciar sesión en la cuenta de Azure:
   ```azurecli
   az login
   ```
   Siga las instrucciones para completar el proceso de inicio de sesión

   La CLI de Azure mostrará una lista de las cuentas, por ejemplo:

   ```json
   [
     {
       "cloudName": "AzureCloud",
       "id": "00000000-0000-0000-0000-000000000000",
       "isDefault": false,
       "name": "Windows Azure MSDN - Visual Studio Ultimate",
       "state": "Enabled",
       "tenantId": "00000000-0000-0000-0000-000000000000",
       "user": {
         "name": "Gena.Soto@wingtiptoys.com",
         "type": "user"
       }
     }
   ]
   ```

1. Si todavía no tiene instalada la interfaz de la línea de comandos de Kubernetes (`kubectl`), puede instalar con la CLI de Azure, por ejemplo:
   ```azurecli
   az acs kubernetes install-cli
   ```

   > [!NOTE]
   >
   > Los usuarios de Linux pueden tener anteceder este comando con `sudo`, ya que implementa la CLI de Kubernetes en `/usr/local/bin`.
   >
   > Si ya tiene instalado `kubectl` y la versión de `kubectl` es demasiado antigua, es posible que vea un mensaje de error similar al ejemplo siguiente cuando intente completar los pasos que aparecen más adelante en el artículo:
   >
   > ```
   > error: group map[autoscaling:0x0000000000 batch:0x0000000000 certificates.k8s.io
   > :0x0000000000 extensions:0x0000000000 storage.k8s.io:0x0000000000 apps:0x0000000
   > 000 authentication.k8s.io:0x0000000000 policy:0x0000000000 rbac.authorization.k8
   > s.io:0x0000000000 federation:0x0000000000 authorization.k8s.io:0x0000000000 comp
   > onentconfig:0x0000000000] is already registered
   > ```
   >
   > Si esto ocurre, deberá reinstalar `kubectl` para actualizar la versión.
   >

1. Cree un grupo de recursos para los recursos de Azure que se usarán en este tutorial, por ejemplo:
   ```azurecli
   az group create --name=wingtiptoys-kubernetes --location=westeurope
   ```
   Donde:  
      * *wingtiptoys-kubernetes* es un nombre único para el grupo de recursos  
      * *westeurope* es una ubicación geográfica adecuada para la aplicación  

   La CLI de Azure mostrará los resultados de la creación del grupo de recursos, por ejemplo:  

   ```json
   {
     "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/wingtiptoys-kubernetes",
     "location": "westeurope",
     "managedBy": null,
     "name": "wingtiptoys-kubernetes",
     "properties": {
       "provisioningState": "Succeeded"
     },
     "tags": null
   }
   ```


## <a name="create-a-kubernetes-cluster-using-the-azure-cli"></a>Creación de un clúster de Kubernetes mediante la CLI de Azure

1. Cree un clúster de Kubernetes en el grupo de recursos nuevo, por ejemplo:  
   ```azurecli 
   az acs create --orchestrator-type kubernetes --resource-group wingtiptoys-kubernetes --name wingtiptoys-cluster --generate-ssh-keys --dns-prefix=wingtiptoys
   ```
   Donde:  
      * *wingtiptoys-kubernetes* es el nombre del grupo de recursos que se mencionó anteriormente en el artículo  
      * *wingtiptoys-cluster* es un nombre único para el clúster de Kubernetes
      * *wingtiptoys* es un nombre DNS único para la aplicación

   La CLI de Azure mostrará los resultados de la creación del clúster, por ejemplo:  

   ```json
   {
     "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/wingtiptoys-kubernetes/providers/Microsoft.Resources/deployments/azurecli0000000000.00000000000",
     "name": "azurecli0000000000.00000000000",
     "properties": {
       "correlationId": "00000000-0000-0000-0000-000000000000",
       "debugSetting": null,
       "dependencies": [],
       "mode": "Incremental",
       "outputs": {
         "masterFQDN": {
           "type": "String",
           "value": "wingtiptoysmgmt.westeurope.cloudapp.azure.com"
         },
         "sshMaster0": {
           "type": "String",
           "value": "ssh azureuser@wingtiptoysmgmt.westeurope.cloudapp.azure.com -A -p 22"
         }
       },
       "parameters": {
         "clientSecret": {
           "type": "SecureString"
         }
       },
       "parametersLink": null,
       "providers": [
         {
           "id": null,
           "namespace": "Microsoft.ContainerService",
           "registrationState": null,
           "resourceTypes": [
             {
               "aliases": null,
               "apiVersions": null,
               "locations": [
                 "westeurope"
               ],
               "properties": null,
               "resourceType": "containerServices"
             }
           ]
         }
       ],
       "provisioningState": "Succeeded",
       "template": null,
       "templateLink": null,
       "timestamp": "2017-09-15T01:00:00.000000+00:00"
     },
     "resourceGroup": "wingtiptoys-kubernetes"
   }
   ```

1. Descargue las credenciales del clúster de Kubernetes nuevo, por ejemplo:  
   ```azurecli 
   az acs kubernetes get-credentials --resource-group=wingtiptoys-kubernetes --name wingtiptoys-cluster
   ```

1. Compruebe la conexión con el comando siguiente:
   ```shell 
   kubectl get nodes
   ```

   Debería ver una lista de nodos y estados, como en el ejemplo siguiente:

   ```shell
   NAME                    STATUS                     AGE       VERSION
   k8s-agent-00000000-0    Ready                      5h        v1.6.6
   k8s-agent-00000000-1    Ready                      5h        v1.6.6
   k8s-agent-00000000-2    Ready                      5h        v1.6.6
   k8s-master-00000000-0   Ready,SchedulingDisabled   5h        v1.6.6
   ```


## <a name="create-a-private-azure-container-registry-using-the-azure-cli"></a>Creación de un registro de contenedor privado de Azure con la CLI de Azure

1. Cree un registro de contenedor privado de Azure en el grupo de recursos para hospedar la imagen de Docker, por ejemplo:
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoys-kubernetes --location westeurope --name wingtiptoysregistry --sku Basic
   ```
   Donde:

   | . | DESCRIPCIÓN |
   |---|---|
   | `wingtiptoys-kubernetes` | Especifica el nombre del grupo de recursos que se mencionó anteriormente en este artículo. |
   | `wingtiptoysregistry` | Especifica un nombre único para el registro privado. |
   | `westeurope` | Especifica una ubicación geográfica adecuada para la aplicación. |

   La CLI de Azure mostrará los resultados de la creación del registro, por ejemplo:  

   ```json
   {
     "adminUserEnabled": true,
     "creationDate": "2017-09-15T01:00:00.000000+00:00",
     "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/wingtiptoys-kubernetes/providers/Microsoft.ContainerRegistry/registries/wingtiptoysregistry",
     "location": "westeurope",
     "loginServer": "wingtiptoysregistry.azurecr.io",
     "name": "wingtiptoysregistry",
     "provisioningState": "Succeeded",
     "resourceGroup": "wingtiptoys-kubernetes",
     "sku": {
       "name": "Basic",
       "tier": "Basic"
     },
     "storageAccount": {
       "name": "wingtiptoysregistr000000"
     },
     "tags": {},
     "type": "Microsoft.ContainerRegistry/registries"
   }
   ```

2. Recupere la contraseña del registro de contenedor de la CLI de Azure.
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```

   La CLI de Azure mostrará la contraseña del registro, por ejemplo:  

   ```json
   {
     "name": "password",
     "value": "AbCdEfGhIjKlMnOpQrStUvWxYz"
   }
   ```

3. Navegue hasta el directorio de configuración de la instalación de Maven (valor predeterminado ~/.m2/ o C:\Users\username\.m2) y abra el archivo *settings.xml* con un editor de texto.

4. Agregue la dirección URL de Azure Container Registry, el nombre de usuario y la contraseña a una colección nueva de `<server>` en el archivo *settings.xml*.
   `id` y `username` son el nombre del registro. Use el valor `password` del comando anterior (sin comillas).

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry.azurecr.io</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

5. Navegue hasta el directorio de proyecto completado de la aplicación Spring Boot (por ejemplo, "*C:\SpringBoot\gs-spring-boot-docker\complete*" o "*/home/GenaSoto/SpringBoot/gs-spring-boot-docker/complete*") y abra el archivo *pom.xml* con un editor de texto.

6. Actualice la colección `<properties>` del archivo *pom.xml* con el valor del servidor de inicio de sesión de Azure Container Registry.

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

7. Actualice la colección `<plugins>` del archivo *pom.xml* de modo que `<plugin>` contiene la dirección del servidor de inicio de sesión y el nombre de registro de Azure Container Registry.

   ```xml
   <plugin>
     <groupId>com.spotify</groupId>
     <artifactId>dockerfile-maven-plugin</artifactId>
     <version>1.3.4</version>
     <configuration>
       <repository>${docker.image.prefix}/${project.artifactId}</repository>
       <serverId>${docker.image.prefix}</serverId>
       <registryUrl>https://${docker.image.prefix}</registryUrl>
     </configuration>
   </plugin>
   ```

8. Navegue hasta el directorio de proyecto completado de la aplicación Spring Boot y ejecute el comando Maven siguiente para compilar el contenedor Docker e insertar la imagen en el registro:

   ```shell
   mvn package dockerfile:build -DpushImage
   ```

   Maven mostrará los resultados de la compilación, por ejemplo:  

   ```shell
   [INFO] ----------------------------------------------------
   [INFO] BUILD SUCCESS
   [INFO] ----------------------------------------------------
   [INFO] Total time: 38.113 s
   [INFO] Finished at: 2017-09-15T02:00:00-07:00
   [INFO] Final Memory: 47M/338M
   [INFO] ----------------------------------------------------
   ```


## <a name="configure-your-spring-boot-app-to-use-the-fabric8-maven-plugin"></a>Configuración de la aplicación Spring Boot para usar el complemento Fabric8 para Maven

1. Navegue hasta el directorio de proyecto completado de la aplicación Spring Boot (por ejemplo, "*C:\SpringBoot\gs-spring-boot-docker\complete*" o "*/home/GenaSoto/SpringBoot/gs-spring-boot-docker/complete*") y abra el archivo *pom.xml* con un editor de texto.

1. Actualice la colección de `<plugins>` en el archivo *pom.xml* para agregar el complemento Fabric8 para Maven:

   ```xml
   <plugin>
     <groupId>io.fabric8</groupId>
     <artifactId>fabric8-maven-plugin</artifactId>
     <version>3.5.30</version>
     <configuration>
       <ignoreServices>false</ignoreServices>
       <registry>${docker.image.prefix}</registry>
     </configuration>
   </plugin>
   ```

1. Navegue al directorio de origen principal de la aplicación Spring Boot (por ejemplo, "*C:\SpringBoot\gs-spring-boot-docker\complete\src\main*" o "*/home/GenaSoto/SpringBoot/gs-spring-boot-docker/complete/src/main*") y cree una carpeta nueva denominada "*fabric8*".

1. Cree tres archivos de fragmentos YAML en la carpeta *fabric8* nueva:

   a. Cree un archivo denominado **deployment.yml** con el contenido siguiente:
      ```yaml
      apiVersion: extensions/v1beta1
      kind: Deployment
      metadata:
        name: ${project.artifactId}
        labels:
          run: gs-spring-boot-docker
      spec:
        replicas: 1
        selector:
          matchLabels:
            run: gs-spring-boot-docker
        strategy:
          rollingUpdate:
            maxSurge: 1
            maxUnavailable: 1
          type: RollingUpdate
        template:
          metadata:
            labels:
              run: gs-spring-boot-docker
          spec:
            containers:
            - image: ${docker.image.prefix}/${project.artifactId}:latest
              name: gs-spring-boot-docker
              imagePullPolicy: Always
              ports:
              - containerPort: 8080
            imagePullSecrets:
              - name: mysecrets
      ```

   b. Cree un archivo denominado **secrets.yml** con el contenido siguiente:
      ```yaml
      apiVersion: v1
      kind: Secret
      metadata:
        name: mysecrets
        namespace: default
        annotations:
          maven.fabric8.io/dockerServerId:  ${docker.image.prefix}
      type: kubernetes.io/dockercfg
      ```

   c. Cree un archivo denominado **service.yml** con el contenido siguiente:
      ```yaml
      apiVersion: v1
      kind: Service
      metadata:
        name: ${project.artifactId}
        labels:
          expose: "true"
      spec:
        ports:
        - port: 80
          targetPort: 8080
        type: LoadBalancer
      ```

1. Ejecute el comando Maven siguiente para compilar el archivo de lista de recursos de Kubernetes:

   ```shell
   mvn fabric8:resource
   ```

   Este comando combina todos los archivos YAML de recursos de Kubernetes de la carpeta *src/main/fabric8* en un archivo YAML que contiene una lista de recursos de Kubernetes, que se puede aplicar directamente al clúster de Kubernetes o exportar a un gráfico de Helm.

   Maven mostrará los resultados de la compilación, por ejemplo:  

   ```shell
   [INFO] ----------------------------------------------------
   [INFO] BUILD SUCCESS
   [INFO] ----------------------------------------------------
   [INFO] Total time: 16.744 s
   [INFO] Finished at: 2017-09-15T02:35:00-07:00
   [INFO] Final Memory: 30M/290M
   [INFO] ----------------------------------------------------
   ```

1. Ejecute el comando Maven siguiente para aplicar el archivo de lista de recursos en el clúster de Kubernetes:

   ```shell
   mvn fabric8:apply
   ```

   Maven mostrará los resultados de la compilación, por ejemplo:  

   ```shell
   [INFO] ----------------------------------------------------
   [INFO] BUILD SUCCESS
   [INFO] ----------------------------------------------------
   [INFO] Total time: 14.814 s
   [INFO] Finished at: 2017-09-15T02:41:00-07:00
   [INFO] Final Memory: 35M/288M
   [INFO] ----------------------------------------------------
   ```

1. Una vez que la aplicación se implemente en el clúster, consulte la dirección IP externa con la aplicación `kubectl`, por ejemplo:
   ```shell
   kubectl get svc -w
   ```

   `kubectl` mostrará las direcciones IP internas y externas, por ejemplo:

   ```shell
   NAME                    CLUSTER-IP   EXTERNAL-IP   PORT(S)        AGE
   kubernetes              10.0.0.1     <none>        443/TCP        19h
   gs-spring-boot-docker   10.0.242.8   13.65.196.3   80:31215/TCP   3m
   ```

   Puede usar la dirección IP externa para abrir la aplicación en un explorador web.

   ![Examinar externamente la aplicación de ejemplo][SB02]

## <a name="delete-your-kubernetes-cluster"></a>Eliminación del clúster de Kubernetes

Cuando ya no se necesita el clúster de Kubernetes, puede usar el comando `az group delete` para quitar el grupo de recursos, con lo que se quitarán todos los recursos relacionados, por ejemplo:

   ```azurecli
   az group delete --name wingtiptoys-kubernetes --yes --no-wait
   ```

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre el uso de aplicaciones de Spring Boot en Azure, consulte los siguientes artículos:

* [Implementación de una aplicación de Spring Boot en Azure App Service](deploy-spring-boot-java-web-app-on-azure.md)
* [Implementación de una aplicación de Spring Boot en Linux en Azure Container Service](deploy-spring-boot-java-app-on-linux.md)
* [Implementación de una aplicación de Spring Boot en un clúster de Kubernetes en Azure Container Service](deploy-spring-boot-java-app-on-kubernetes.md)

Para más información sobre el uso de Azure con Java, consulte [Azure para desarrolladores de Java] y [Herramientas de Java para Visual Studio Team Services] (Herramientas de Java para Visual Studio Team Services).

Para obtener más información sobre el proyecto de ejemplo Spring Boot en Docker, vea [Spring Boot on Docker Getting Started] (Introducción a Spring Boot en Docker).

Para obtener ayuda para dar sus primeros pasos con sus propias aplicaciones de Spring Boot, consulte **Spring Initializr** en <https://start.spring.io/>.

Para más información sobre cómo empezar a crear una sencilla aplicación de Spring Boot, consulte Spring Initializr en <https://start.spring.io/>.

Para ver más ejemplos de cómo usar imágenes de Docker personalizadas con Azure, consulte [Uso de una imagen personalizada de Docker para Web App on Linux de Azure].

<!-- URL List -->

[Interfaz de la línea de comandos (CLI) de Azure]: /cli/azure/overview
[Azure Container Service (AKS)]: https://azure.microsoft.com/services/container-service/
[Azure para desarrolladores de Java]: https://docs.microsoft.com/java/azure/
[Azure portal]: https://portal.azure.com/
[Create a private Docker container registry using the Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Uso de una imagen personalizada de Docker para Web App on Linux de Azure]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[Fabric8]: https://fabric8.io/
[cuenta de Azure gratuita]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Kit para desarrolladores de Java (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Herramientas de Java para Visual Studio Team Services]: https://java.visualstudio.com/
[Kubernetes]: https://kubernetes.io/
[Maven]: http://maven.apache.org/
[ventajas como suscriptor de MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot on Docker Getting Started]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[SB01]: ./media/deploy-spring-boot-java-app-using-fabric8-maven-plugin/SB01.png
[SB02]: ./media/deploy-spring-boot-java-app-using-fabric8-maven-plugin/SB02.png
