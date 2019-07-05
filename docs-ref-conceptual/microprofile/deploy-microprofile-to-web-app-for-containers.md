---
title: Implementación de un servicio de MicroProfile basado en Java en Azure Web Apps for Containers
description: Aprenda cómo implementar un servicio MicroProfile con Docker y Azure Web App for Containers
services: container-registry;app-service
documentationcenter: java
author: jonathangiles
manager: routlaw
editor: jonathangiles
ms.assetid: ''
ms.author: jogiles
ms.date: 09/07/2018
ms.devlang: java
ms.service: container-registry;app-service
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: 4ecfbf92bc30bc491c991e30111cce8375da7f1a
ms.sourcegitcommit: f8faa4a14c714e148c513fd46f119524f3897abf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2019
ms.locfileid: "67533600"
---
# <a name="deploy-a-java-based-microprofile-service-to-azure-web-app-for-containers"></a>Implementación de un servicio de MicroProfile basado en Java en Azure Web Apps for Containers

MicroProfile es una excelente manera de crear pequeñas aplicaciones de Java que se pueden implementar de forma rápida y sencilla en servicios como [Azure Web Apps for Containers](https://azure.microsoft.com/services/app-service/containers/). En este tutorial, crearemos un microservicio sencillo basado en MicroProfile que, a continuación, se incluirá en un contenedor de Docker implementado en una [instancia de registro de contenedor de Azure](https://azure.microsoft.com/services/container-registry/), y se hospedará en Azure Web App for Containers.

> [!NOTE]
> Este procedimiento funciona con cualquier implementación de MicroProfile.io siempre que la imagen del contenedor de Docker sea autoejecutable (es decir, la imagen incluye el entorno de ejecución).

En este ejemplo, se usa [Payara Micro](https://www.payara.fish/payara_micro) y [MicroProfile 1.3](https://microprofile.io/) para crear un pequeño archivo de requisitos de aplicación web (WAR) de Java de aproximadamente 5 000 bytes y, a continuación, se empaqueta en una imagen de Docker de aproximadamente 174 megabytes (MB). Esta imagen de Docker contiene todo lo necesario para realizar una implementación totalmente incluida en un contenedor de esta aplicación web.

No es necesario volver a implementar una imagen de Docker de 174 MB completa cada vez que cambie el código fuente, porque Docker carga solo las diferencias (que son mucho más pequeñas). Por lo tanto, el proceso de ejecución de una nueva versión de una aplicación de MicroProfile a través de una canalización de CI/CD sea eficaz y rápida, lo que reduce la fricción y permite una iteración rápida del desarrollo.

En este tutorial, primero vamos a crear y ejecutar el código localmente y, después, lo implementaremos como una aplicación web en Azure. En ambos casos, dependeremos de Docker para simplificar y normalizar nuestros esfuerzos. Antes de empezar, crearemos una instancia de registro de contenedor de Azure para almacenar los contenedores de Docker.

## <a name="create-an-azure-container-registry-instance"></a>Creación de una instancia de registro de contenedor de Azure

Puede usar [Azure Portal](http://portal.azure.com) para crear la instancia de registro de contenedor de Azure, pero hay otras opciones, como la CLI de Azure. Siga estos pasos para crear una nueva instancia de registro de contenedor de Azure:

1. Inicie sesión en [Azure Portal](http://portal.azure.com) y cree un nuevo recurso de Azure Container Registry. Proporcione un nombre de Registro (tenga en cuenta que este nombre se establecerá como la propiedad `docker.registry` en *pom.xml*). Cambie los valores predeterminados como desee y seleccione **Crear**.

1. En unos 30 segundos, cuando la instancia de registro de contenedor esté activa, selecciónela y, a continuación, en el panel izquierdo, seleccione el vínculo **Claves de acceso**. 

    No olvide habilitar la opción de configuración *admin user* para que pueda acceder a esta instancia de registro de contenedor desde sus máquinas, e insertar contenedores de Docker en ella. Al hacerlo, también permitirá el acceso desde la instancia de Azure Web App for Containers que va a configurar.

1. En el panel **Claves de acceso**, copie los valores **nombre de usuario** y **contraseña** y péguelos en el archivo *settings.xml* global de Maven. Para más información acerca de la configuración de Maven, visite el sitio web [Apache Maven Project](https://maven.apache.org/settings.html). 

   Como referencia, este es un ejemplo del archivo *${user.home}/.m2/settings.xml*:

    ```xml
    <settings xmlns="http://maven.apache.org/SETTINGS/1.0.0"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0
                          https://maven.apache.org/xsd/settings-1.0.0.xsd">
        <servers>
          <server>
            <id>jogilescr.azurecr.io</id>
            <username>jogilescr</username>
            <password>ojoirshois.this-isn't-real.hrihslirhlishrglih</password>
          </server>
        </servers>
    </settings>
    ```

Ahora que ha creado la instancia de registro de contenedor, puede compilar y ejecutar la aplicación MicroProfile localmente.

## <a name="create-your-microprofile-application"></a>Creación de la aplicación MicroProfile

Este código de ejemplo se basa en una aplicación de ejemplo que está disponible en GitHub. Escriba los siguientes comandos para clonar el código en su equipo:

```
git clone https://github.com/Azure-Samples/microprofile-docker-helloworld.git

cd microprofile-docker-helloworld
```

Este directorio contiene un archivo *pom.xml* que se usa para especificar el proyecto en el formato usado por la herramienta de compilación de Maven. Puede editar el archivo para que se adapte a sus propias necesidades. En concreto, las propiedades `docker.registry` y `docker.name` deben cambiarse a los valores `docker.registry` y `docker.name` creados cuando se configuró la instancia de registro de contenedor de Azure.

Otro archivo para tener en cuenta en este directorio es Dockerfile, que se reproduce a continuación:

```dockerfile
FROM payara/micro

ARG WAR_FILE
COPY target/${WAR_FILE} $DEPLOY_DIR

EXPOSE 8080
```

Dockerfile crea un nuevo contenedor de Docker que se basa en el contenedor de Docker Payara Micro. Copia el archivo WAR que se creó como parte del proceso de compilación. También expone el puerto 8080 para que pueda tener acceso al servicio una vez que esté en marcha en un contenedor de Docker.

Al abrir el directorio *src*, verá la clase `Application` que se reproduce aquí:

```java
package com.microsoft.azure.samples.microprofile.docker.helloworld;

import javax.ws.rs.ApplicationPath;

@ApplicationPath("/api")
public class Application extends javax.ws.rs.core.Application { }
```

La anotación *@ApplicationPath("/api")* especifica el punto de conexión base de este microservicio. Es decir, para todos los puntos de conexión, */api* precede al resto de la dirección URL que se necesita para acceder a cualquier punto de conexión REST específico.

Dentro del paquete *api*, hay una clase llamada `API` que contiene el código siguiente:

```java
package com.microsoft.azure.samples.microprofile.docker.helloworld.api;

import javax.enterprise.context.ApplicationScoped;
import javax.ws.rs.GET;
import javax.ws.rs.Path;
import javax.ws.rs.Produces;

import static javax.ws.rs.core.MediaType.TEXT_HTML;

@ApplicationScoped
@Path("/")
public class API {

    @GET
    @Path("/helloworld")
    @Produces(TEXT_HTML)
    public String info() {
        return "Hello, world!";
    }
}
```

Podemos usar la anotación *@Path("/helloworld")* para ver que este punto de conexión REST, cuando se combina con el valor de */api* especificado en la clase `Application`, será */api/helloworld*. Cuando se llama a este punto de conexión mediante una solicitud HTTP GET, puede ver que el método genera texto/html que, en realidad, es simplemente una cadena codificada de forma rígida "Hello, world!".

Hasta ahora, en este artículo hemos visto todo el código necesario para crear un microservicio utilizando MicroProfile. Ahora puede usar Maven para compilarlo, incluirlo en un contenedor de Docker y ejecutarlo localmente; para ello, siga estos pasos:

1. Ejecute `mvn clean package` y espere hasta que se complete.

1. Ejecute `docker run -it --rm -p 8080:8080 <docker.registry>/<docker.name>:latest`. Por ejemplo, *docker run -it --rm -p 8080:8080 jogilescr.azurecr.io/samples/docker-helloworld:latest*, donde *\<docker.registry>* es *jogilescr.azurecr.io* y *\<docker.name>* es *samples/docker-helloworld*.

1. Intente acceder a [http://localhost:8080/microprofile/api/helloworld](http://localhost:8080/microprofile/api/helloworld) y [http://localhost:8080/health](http://localhost:8080/health) en el explorador web. Si ve la respuesta "¡Hello, world!" esperada (y la información relacionada con el estado de mantenimiento del punto de conexión [/health](http://localhost:8080/health)), ha implementado correctamente la aplicación de MicroProfile en el equipo local.

## <a name="push-the-container-to-the-azure-container-registry-instance"></a>Inserción del contenedor en la instancia de registro de contenedor de Azure

Ahora que ha creado y ejecutado correctamente la aplicación de MicroProfile en la máquina local, el siguiente paso es insertar este contenedor en la instancia de registro de contenedor. 

> [!NOTE]
> Aunque en este artículo se usa una instancia de registro de contenedor de Azure, debería funcionar cualquier instancia de registro de contenedor, siempre y cuando el archivo *pom.xml* se edite para que apunte a la ubicación pertinente.

1. Ejecute `mvn clean package` para limpiar, compilar y crear una imagen de Docker local.
2. Para insertar el contenedor en la instancia de registro de contenedor de Azure, ejecute `mvn dockerfile:push`.

Ahora tiene la imagen de contenedor de Docker cargada en la instancia de registro de contenedor de Azure. Sin embargo, aún no se está ejecutando. Ahora debe implementarla en una instancia de Azure Web App for Containers. 

## <a name="create-an-azure-web-app-for-containers-instance"></a>Creación de una instancia de Azure Web App for Containers

1. En [Azure Portal](http://portal.azure.com), en el panel izquierdo, seleccione **Web y móvil** y haga lo siguiente:

   a. Especifique un nombre. El nombre se convertirá en la dirección URL pública de la aplicación web, por lo que es una buena idea elegir un nombre que pueda recordar fácilmente. Puede agregar un nombre de dominio personalizado más adelante, si lo desea.

   b. En la sección **Configurar contenedor**, en **Origen de imagen**, seleccione **Azure Container Registry** y, en la lista desplegable, seleccione la imagen correcta.

   c. No es necesario especificar ningún valor en el campo **Archivo de inicio**.

1. Después de crear la instancia, selecciónela y, a continuación, seleccione **Configuración de la aplicación**. En **Clave**, escriba **WEBSITES_PORT** y en **Valor**, escriba **8080**. Estas configuraciones indican a Azure qué puerto se expondrá en el contenedor y lo asignan al puerto 80 externamente.

1. (Opcional) Seleccione el vínculo **Contenedor de Docker** y habilite **Implementación continua**. Al hacerlo, cada vez que actualice la imagen de una instancia de registro de contenedor de Azure, se actualiza automáticamente en la instancia de Azure Web App for Containers.

1. Ahora podrá acceder a las instancias hospedadas en Azure en `http://<appname>.azurewebsites.net/microprofile/api/helloworld` y `http://<appname>.azurewebsites.net/health`.

## <a name="summary"></a>Resumen

En este tutorial, hemos recorrido el proceso para crear un microservicio de MicroProfile sencillo, incluirlo en un contenedor de Docker, y lo hemos publicado en Azure y ejecutado localmente. Puede ampliar su microservicio para que ofrezca otras funcionalidades adicionales útiles. Para más información, vaya a [MicroProfile.io](https://microprofile.io/).
