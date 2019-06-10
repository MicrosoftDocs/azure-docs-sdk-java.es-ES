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
# <a name="use-docker-with-a-jdk-for-azure"></a>Uso de Docker con un JDK para Azure 

Las imágenes predefinidas de Docker para Java 7, 8 y 11 están disponibles en [Docker Hub](https://hub.docker.com/_/microsoft-java-se).

Están disponibles en Docker Hub imágenes de contenedor de Docker certificadas para el JDK, JRE y JRE desatendido en varias imágenes de sistema operativo base:

* [JDK](https://hub.docker.com/_/microsoft-java-jdk)
* [JRE](https://hub.docker.com/_/microsoft-java-jre)
* [JRE desatendido](https://hub.docker.com/_/microsoft-java-jre-headless)

## <a name="running-a-docker-image"></a>Ejecución de una imagen de Docker

Se pueden ejecutar imágenes de Docker mediante la sintaxis `$ docker run mcr.microsoft.com/java/jdk:tag java` tal como se muestra en el ejemplo siguiente.

```cli
docker run mcr.microsoft.com/java/jdk:8u212-zulu-alpine java -version 
```

## <a name="creating-a-docker-image"></a>Creación de una imagen de Docker

Puede crear una imagen mediante imágenes de Docker Hub oficiales de Microsoft, como se muestra en los ejemplos siguientes.

### <a name="create-a-docker-file"></a>Creación de un archivo de Docker

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

### <a name="build-a-docker-image"></a>Compilación de una imagen de Docker

```cli
docker build -t hello-world
```

### <a name="run-the-new-image"></a>Ejecución de la nueva imagen

```cli
docker run hello-world
```

Verá la salida siguiente:

```output
Hello World - From Microsoft Azure !!!
```
