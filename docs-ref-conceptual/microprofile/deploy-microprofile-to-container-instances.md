---
title: Implementación de una aplicación de MicroProfile en la nube con Docker y Azure
description: Aprenda cómo implementar una aplicación de MicroProfile en la nube con Docker y Azure Container Instances.
services: container-instances;container-registry
documentationcenter: java
author: brunoborges
manager: routlaw
editor: brunoborges
ms.assetid: ''
ms.author: brborges
ms.date: 11/21/2018
ms.devlang: java
ms.service: container-instances
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: 6ba12bb183969103676fa988199603df6cf36bba
ms.sourcegitcommit: f8faa4a14c714e148c513fd46f119524f3897abf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2019
ms.locfileid: "67533603"
---
# <a name="deploy-a-microprofile-app-to-the-cloud-by-using-docker-and-azure"></a>Implementación de una aplicación de MicroProfile en la nube con Docker y Azure

En este artículo se muestra cómo empaquetar una aplicación de [MicroProfile.io] en un contenedor de Docker y ejecutarla en Azure Container Instances.

> [!NOTE]
> Este procedimiento funciona con cualquier implementación de MicroProfile.io siempre que la imagen del contenedor de Docker sea autoejecutable (es decir, la imagen incluye el entorno de ejecución).

## <a name="prerequisites"></a>Requisitos previos

Para completar este tutorial, debe cumplir los siguientes requisitos previos:

* Una suscripción de Azure. Si todavía no dispone de una suscripción a Azure, puede registrarse para obtener una evaluación gratuita en una [cuenta de Azure gratuita].
* La [CLI de Azure] instalada.
* Un kit de desarrollo de Java (JDK) admitido Para más información acerca de los JDK que están disponibles para usar al desarrollar en Azure, consulte [Soporte técnico a largo plazo de Java para Azure y Azure Stack](https://aka.ms/azure-jdks).
* La herramienta de compilación [Apache Maven] (versión 3 o posteriores).
* Un cliente [Git].

## <a name="microprofile-hello-azure-sample"></a>Ejemplo MicroProfile Hello Azure

En este artículo, usaremos el ejemplo [MicroProfile Hello Azure](https://github.com/azure-samples/microprofile-hello-azure). Clónelo, compílelo y ejecútelo localmente con los siguientes comandos:

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

Para probar la aplicación, puede llamar a `curl` o usar un [explorador](http://localhost:8080/api/hello):

```bash
$ curl http://localhost:8080/api/hello
Hello, Azure!
```

## <a name="deploy-the-app-to-azure"></a>Implementación de la aplicación en Azure

Ahora vamos a poner esta aplicación en Azure con los servicios [Azure Container Instances] y [Azure Container Registry].

### <a name="build-a-docker-image"></a>Compilación de una imagen de Docker

El proyecto de ejemplo incluye un archivo Dockerfile que se puede usar. No es necesario tener Docker instalado, porque se usará la característica Build de Azure Container Registry para compilar la imagen en la nube.

Para compilar la imagen y prepararla para ejecutarla en Azure, haga lo siguiente:

1. Instale e inicie sesión en la CLI de Azure.
1. Cree un grupo de recursos de Azure.
1. Cree una instancia de registro de contenedor de Azure.
1. Compile una imagen de Docker.
1. Publique la imagen de Docker en la instancia de registro de contenedor creada previamente.
1. (Opcional) Genere y publique la imagen en la instancia de registro de contenedor en un solo comando.


#### <a name="set-up-the-azure-cli"></a>Configuración de la CLI de Azure

Asegúrese de que tiene una suscripción de Azure, que la [CLI de Azure](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest) está instalada y que se ha autenticado en su cuenta:

```bash
az login
```

#### <a name="create-a-resource-group"></a>Crear un grupo de recursos

```bash
export ARG=microprofileRG
export ADCL=eastus
az group create --name $ARG --location $ADCL
```

#### <a name="create-a-container-registry-instance"></a>Creación de una instancia de registro de contenedor

Este comando creará una instancia de registro de contenedor global único con un nombre básico y un número aleatorio.

```bash
export RANDINT=`date +"%m%d%y$RANDOM"`
export ACR=mydockerrepo$RANDINT
az acr create --name $ACR -g $ARG --sku Basic --admin-enabled
```

#### <a name="build-the-docker-image"></a>Compilación de la imagen de Docker

Aunque la imagen de Docker se puede compilar localmente con el propio Docker, quizás quiera considerar la posibilidad de compilarlo en la nube por algunas razones:

* No es necesario instalar Docker localmente.
* Es mucho más rápido porque la compilación se realizará en otro lugar (excepto el tiempo de carga de contexto).
* Los procesos en la nube tienen un acceso a Internet más rápido, por lo que las descargas son más rápidas.
* La imagen se coloca directamente en la instancia de registro de contenedor.

Por estas razones, la imagen se compila con la característica [Azure Container Registry Build]:

```bash
export IMG_NAME="mympapp:latest"
az acr build -r $ACR -t $IMG_NAME -g $ARG .
...
Build complete
Build ID: aa1 was successful after 1m2.674577892s
```

#### <a name="deploy-the-docker-image-from-the-azure-container-registry-instance-to-container-instances"></a>Implementación de la imagen de Docker desde la instancia de registro de contenedor de Azure en Azure Container Instances

Ahora que la imagen está disponible en la instancia de registro de contenedor, cree una instancia de contenedor e insértela en Container Instances. Pero primero, asegúrese de que puede autenticarse en la instancia de registro de contenedor:

```bash
export ACR_REPO=`az acr show --name $ACR -g $ARG --query loginServer -o tsv`
export ACR_PASS=`az acr credential show --name $ACR -g $ARG --query "passwords[0].value" -o tsv`
export ACI_INSTANCE=myapp`date +"%m%d%y$RANDOM"`

az container create --resource-group $ARG --name $ACR --image $ACR_REPO/$IMG_NAME --cpu 1 --memory 1 --registry-login-server $ACR_REPO --registry-username $ACR --registry-password $ACR_PASS --dns-name-label $ACI_INSTANCE --ports 8080
```

#### <a name="test-your-deployed-microprofile-application"></a>Prueba de la aplicación de MicroProfile implementada

La aplicación debe estar instalada y en ejecución. Para probarla en la interfaz de la línea de comandos, ejecute el siguiente comando:

```bash
curl http://$ACI_INSTANCE.$ADCL.azurecontainer.io:8080/api/hello
````

Felicidades. Ha compilado correctamente una aplicación de MicroProfile como un contenedor de Docker y la ha implementado en Microsoft Azure.

## <a name="next-steps"></a>Pasos siguientes

Para más información acerca de las diferentes tecnologías que se tratan en este artículo, consulte:

* [Inicio de sesión en Azure desde la CLI de Azure](/azure/xplat-cli-connect)

<!-- URL List -->

[Azure Container Registry Build]: https://docs.microsoft.com/azure/container-registry/container-registry-build-overview
[MicroProfile.io]: https://microprofile.io
[CLI de Azure]: /cli/azure/overview
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Azure portal]: https://portal.azure.com/
[cuenta de Azure gratuita]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Apache Maven]: http://maven.apache.org/
[Java Development Kit (JDK)]: https://aka.ms/azure-jdks
<!-- http://www.oracle.com/technetwork/java/javase/downloads/ -->
[Azure Container Instances]: https://docs.microsoft.com/azure/container-instances/
[Azure Container Registry]:  https://docs.microsoft.com/azure/container-registry
