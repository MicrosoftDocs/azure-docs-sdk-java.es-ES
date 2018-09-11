---
title: Implementación de una aplicación de MicroProfile en la nube con Docker y Azure
description: Aprenda cómo implementar una aplicación de MicroProfile en la nube con Docker y Azure Container Instances.
services: container-instances;container-retistry
documentationcenter: java
author: brunoborges
manager: routlaw
editor: brunoborges
ms.assetid: ''
ms.author: brborges
ms.date: 07/30/2018
ms.devlang: java
ms.service: container-instances
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: 336af51bbdf5d2f843c3868ebc2358e128daaeaa
ms.sourcegitcommit: 280d13b43cef94177d95e03879a5919da234a23c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/31/2018
ms.locfileid: "43324331"
---
# <a name="deploy-a-microprofile-application-to-the-cloud-with-docker-and-azure"></a>Implementación de una aplicación de MicroProfile en la nube con Docker y Azure

En este artículo se muestra cómo empaquetar una aplicación de [MicroProfile.io] en un contenedor de Docker y ejecutarla en Azure Container Instances.

> [!NOTE]
>
> Este procedimiento funciona con cualquier implementación de MicroProfile.io siempre que la imagen del contenedor de Docker sea autoejecutable (es decir, que incluya el entorno de ejecución).

## <a name="prerequisites"></a>Requisitos previos

Para realizar los pasos de este tutorial, necesitará tener los siguientes requisitos previos:

* Si todavía no tiene una suscripción a Azure, puede registrarse para obtener una [cuenta de Azure gratuita].
* La [Interfaz de la línea de comandos (CLI) de Azure].
* Un [Kit de desarrollo de Java (JDK)] actualizado, versión 1.8 o posteriores.
* La herramienta de compilación [Maven] de Apache (versión 3 o posteriores).
* Un cliente [Git].

## <a name="microprofile-hello-azure-sample"></a>Ejemplo MicroProfile Hello Azure

En este artículo, usaremos el ejemplo [MicroProfile Hello Azure](https://github.com/azure-samples/microprofile-hello-azure):

### <a name="clone-build-and-run-locally"></a>Clonación, compilación y ejecución local

```bash
$ git clone https://github.com/Azure-Samples/microprofile-hello-azure.git
$ mvn clean package
...
[INFO] BUILD SUCCESS
...
$ mvn payara-micro:start
...
[2018-07-30T13:34:51.553-0700] [] [INFO] [] [PayaraMicro] [tid: _ThreadID=1 _ThreadName=main] [timeMillis: 1532982891553] [levelValue: 800] Payara Micro  5.182 #badassmicrofish (build 303) ready in 10,304 (ms)
...
```

Para probar la aplicación, puede llamar a `curl` o visitarla mediante un [explorador](http://localhost:8080/api/hello):

```bash
$ curl http://localhost:8080/api/hello
Hello, Azure!
```

## <a name="deploy-to-azure"></a>Implementar en Azure

Ahora vamos a poner esta aplicación en la nube con los servicios [Azure Container Instances] y [Azure Container Registry].

### <a name="build-a-docker-image"></a>Compilación de una imagen de Docker

El proyecto de ejemplo ya incluye un archivo Dockerfile que se puede usar. No es necesario tener Docker instalado, porque usaremos la característica Azure Container Registry Build para compilar la imagen en la nube.

Para compilar la imagen y prepararla para ejecutarla en Azure, debe seguir estos pasos:

1. Instalación y inicio de sesión con la CLI de Azure
1. Crear un grupo de recursos de Azure
1. Creación de un recurso de Azure Container Registry (ACR)
1. Compilación de la imagen de Docker
1. Publicación de la imagen de Docker en el registro de contenedor creado anteriormente
1. (Opcionalmente) Compilación y publicación en ACR en un solo comando


#### <a name="set-up-azure-cli"></a>Configuración de la CLI de Azure

Asegúrese de que tiene una suscripción de Azure, la [CLI de Azure instalada](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest) y de que se ha autenticado en su cuenta:

```bash
az login
```

#### <a name="create-a-resource-group"></a>Creación de un grupo de recursos

```bash
export ARG=microprofileRG
export ADCL=eastus
az group create --name $ARG --location $ADCL
```

#### <a name="create-an-azure-container-registry-instance"></a>Crear una instancia de Azure Container Registry

Este comando creará un registro de contenedor globalmente único (esperamos) con un nombre básico y un número aleatorio.

```bash
export RANDINT=`date +"%m%d%y$RANDOM"`
export ACR=mydockerrepo$RANDINT
az acr create --name $ACR -g $ARG --sku Basic --admin-enabled
```

#### <a name="build-the-docker-image"></a>Compilación de la imagen de Docker

Aunque la imagen de Docker se puede compilar localmente con el propio Docker, quizás quiera considerar la posibilidad de compilarlo en la nube por algunas razones:

1. No es necesario instalar Docker localmente.
1. Es mucho más rápido porque la compilación se realizará en otro lugar (excepto el tiempo de carga de contexto).
1. Los procesos en la nube tienen un acceso a Internet más rápido, por lo que las descargas son más rápidas.
1. La imagen se coloca directamente en el registro de contenedor.

Por estas razones, vamos a compilar la imagen con la característica [Azure Container Registry Build]:

```bash
export IMG_NAME="mympapp:latest"
az acr build -r $ACR -t $IMG_NAME -g $ARG .
...
Build complete
Build ID: aa1 was successful after 1m2.674577892s
```

#### <a name="deploy-docker-image-from-azure-container-registry-acr-into-container-instances-aci"></a>Implementación de la imagen de Docker desde Azure Container Registry (ACR) en Azure Container Instances (ACI)

Ahora que la imagen está disponible en ACR, vamos a crear una instancia de ACI y a insertarla. Pero, primero, tenemos que asegurarnos de que podemos autenticarnos en el registro de contenedor:

```bash
export ACR_REPO=`az acr show --name $ACR -g $ARG --query loginServer -o tsv`
export ACR_PASS=`az acr credential show --name $ACR -g $ARG --query "passwords[0].value" -o tsv`
export ACI_INSTANCE=myapp`date +"%m%d%y$RANDOM"`

az container create --resource-group $ARG --name $ACR --image $ACR_REPO/$IMG_NAME --cpu 1 --memory 1 --registry-login-server $ACR_REPO --registry-username $ACR --registry-password $ACR_PASS --dns-name-label $ACI_INSTANCE --ports 8080
```

#### <a name="test-your-deployed-microprofile-application"></a>Prueba de la aplicación de MicroProfile implementada

La aplicación debe estar instalada y en ejecución. Para probarla en la línea de comandos, ejecute el siguiente comando:

```bash
curl http://$ACI_INSTANCE.$ADCL.azurecontainer.io:8080/api/hello
````

Felicidades. Ha compilado e implementado una aplicación de MicroProfile como un contenedor de Docker en Microsoft Azure.

## <a name="next-steps"></a>Pasos siguientes

Para más información acerca de las diferentes tecnologías que se tratan en este artículo, consulte los artículos siguientes:

* [Inicio de sesión en Azure desde la CLI de Azure](/azure/xplat-cli-connect)

<!-- URL List -->

[Azure Container Registry Build]: https://docs.microsoft.com/azure/container-registry/container-registry-build-overview
[MicroProfile.io]: https://microprofile.io
[Interfaz de la línea de comandos (CLI) de Azure]: /cli/azure/overview
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Azure portal]: https://portal.azure.com/
[cuenta de Azure gratuita]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Maven]: http://maven.apache.org/
[Kit de desarrollo de Java (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/index.html
[Azure Container Instances]: https://docs.microsoft.com/azure/container-instances/
[Azure Container Registry]:  https://docs.microsoft.com/azure/container-registry