---
title: Uso de imágenes de Docker con un JDK para el desarrollo de Java en Azure
description: ''
author: bmitchell287
manager: douge
ms.author: brendm
ms.date: 4/9/2019
ms.devlang: java
ms.topic: conceptual
ms.openlocfilehash: ee8df2a08b23d090965cb42e2c15b934d4785e7c
ms.sourcegitcommit: 03379369346974c6e80f86e7129b885112b5c1a9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/29/2019
ms.locfileid: "64910230"
---
# <a name="use-docker-with-a-jdk-for-azure"></a><span data-ttu-id="a54a9-102">Uso de Docker con un JDK para Azure</span><span class="sxs-lookup"><span data-stu-id="a54a9-102">Use Docker with a JDK for Azure</span></span> 

<span data-ttu-id="a54a9-103">Las imágenes predefinidas de Docker para Java 7, 8 y 11 están disponibles en [Docker Hub](https://hub.docker.com/_/microsoft-java-se).</span><span class="sxs-lookup"><span data-stu-id="a54a9-103">Pre-built Docker images for Java 7, 8, and 11 are available through [Docker Hub](https://hub.docker.com/_/microsoft-java-se).</span></span>

<span data-ttu-id="a54a9-104">Están disponibles en Docker Hub imágenes de contenedor de Docker certificadas para el JDK, JRE y JRE desatendido en varias imágenes de sistema operativo base:</span><span class="sxs-lookup"><span data-stu-id="a54a9-104">Certified Docker container images for Zulu JDK, JRE, and JRE-headless on multiple base OS images are available at Docker Hub:</span></span>

* [<span data-ttu-id="a54a9-105">JDK</span><span class="sxs-lookup"><span data-stu-id="a54a9-105">JDK</span></span>](https://hub.docker.com/_/microsoft-java-jdk)
* [<span data-ttu-id="a54a9-106">JRE</span><span class="sxs-lookup"><span data-stu-id="a54a9-106">JRE</span></span>](https://hub.docker.com/_/microsoft-java-jre)
* [<span data-ttu-id="a54a9-107">JRE desatendido</span><span class="sxs-lookup"><span data-stu-id="a54a9-107">JRE-headless</span></span>](https://hub.docker.com/_/microsoft-java-jre-headless)

## <a name="running-a-docker-image"></a><span data-ttu-id="a54a9-108">Ejecución de una imagen de Docker</span><span class="sxs-lookup"><span data-stu-id="a54a9-108">Running a Docker image</span></span>

<span data-ttu-id="a54a9-109">Se pueden ejecutar imágenes de Docker mediante la sintaxis `$ docker run mcr.microsoft.com/java/jdk:tag java` tal como se muestra en el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="a54a9-109">Docker images can be run using the syntax `$ docker run mcr.microsoft.com/java/jdk:tag java` as shown in the following example.</span></span>

```cli
docker run mcr.microsoft.com/java/jdk:8u212-zulu-alpine java -version 
```

## <a name="creating-a-docker-image"></a><span data-ttu-id="a54a9-110">Creación de una imagen de Docker</span><span class="sxs-lookup"><span data-stu-id="a54a9-110">Creating a Docker image</span></span>

<span data-ttu-id="a54a9-111">Puede crear una imagen mediante imágenes de Docker Hub oficiales de Microsoft, como se muestra en los ejemplos siguientes.</span><span class="sxs-lookup"><span data-stu-id="a54a9-111">You can create an image using Microsoft's official Docker Hub images as shown in the following examples.</span></span>

### <a name="create-a-docker-file"></a><span data-ttu-id="a54a9-112">Creación de un archivo de Docker</span><span class="sxs-lookup"><span data-stu-id="a54a9-112">Create a Docker file</span></span>

```cli
FROM mcr.microsoft.com/java/jdk:8u212-zulu-alpine 
  
RUN echo $' \
  
public class HelloWorld { \
   public static void main(String[] args) { \
      // Prints "Hello, World" in the terminal window. \
      System.out.println("Hello, World - From Microsoft Azure !!!"); \
   } \
}' > HelloWorld.java
  
RUN javac HelloWorld.java
  
CMD ["java", "HelloWorld"]
```

### <a name="build-a-docker-image"></a><span data-ttu-id="a54a9-113">Compilación de una imagen de Docker</span><span class="sxs-lookup"><span data-stu-id="a54a9-113">Build a Docker image</span></span>

```cli
docker build -t hello-world
```

### <a name="run-the-new-image"></a><span data-ttu-id="a54a9-114">Ejecución de la nueva imagen</span><span class="sxs-lookup"><span data-stu-id="a54a9-114">Run the new image</span></span>

```cli
docker run hello-world
```

<span data-ttu-id="a54a9-115">Verá la salida siguiente:</span><span class="sxs-lookup"><span data-stu-id="a54a9-115">You will see the following output:</span></span>

```output
Hello World - From Microsoft Azure !!!
```
