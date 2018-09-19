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
ms.openlocfilehash: 1eb0e7d7a718a1c106adebbf89011f6e3fa1504e
ms.sourcegitcommit: c2019ba6da6c7c28b17b5a85f89e49bb5e570ba4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2018
ms.locfileid: "44040253"
---
# <a name="deploy-a-java-based-microprofile-service-to-azure-web-app-for-containers"></a>Implementación de un servicio de MicroProfile basado en Java en Azure Web Apps for Containers

MicroProfile es una excelente manera de crear pequeñas aplicaciones de Java que se pueden implementar de forma rápida y sencilla en servicios como [Azure Web Apps for Containers](https://azure.microsoft.com/services/app-service/containers/). En este tutorial, crearemos un microservicio sencillo basado en MicroProfile que, a continuación, se incluirá en un contenedor de Docker implementado en un recurso de [Azure Container Registry](https://azure.microsoft.com/services/container-registry/), y se hospedará con Azure Web App for Containers.

> [!NOTE]
>
> Este procedimiento funciona con cualquier implementación de MicroProfile.io siempre que la imagen del contenedor de Docker sea autoejecutable (es decir, que incluya el entorno de ejecución).

Más concretamente, este ejemplo usa [Payara Micro](https://www.payara.fish/payara_micro) y [MicroProfile 1.3](https://microprofile.io/) para crear un pequeño archivo .war de Java (5,085 bytes en el equipo de autores) y, a continuación, lo empaqueta en una imagen de Docker (de unos 174 megabytes aproximadamente). Esta imagen de Docker contiene todo lo necesario para una implementación incluida totalmente en un contenedor de esta aplicación web.

Debido a la manera en que Docker funciona, suele ocurrir que no es necesario volver a implementar la imagen de Docker completa de 174 megabytes cada vez que se cambia el código fuente, porque Docker carga solo las diferencias (cuyo tamaño es significativamente más pequeño). Esto hace que el proceso de ejecución de una nueva versión de una aplicación de MicroProfile a través de una canalización de CI/CD sea eficaz y rápida, lo que reduce la fricción y permite una iteración rápida del desarrollo.

En este tutorial, primero vamos a crear y ejecutar el código localmente y, después, lo implementaremos como una aplicación web en Azure. En ambos casos, dependeremos de Docker para simplificar y normalizar nuestros esfuerzos. Antes de comenzar, crearemos un recurso de Azure Container Registry en la que almacenaremos los contenedores de Docker.

## <a name="creating-an-azure-container-registry"></a>Creación de un recurso de Azure Container Registry

Usaremos [Azure Portal](http://portal.azure.com) para crear el recurso de Azure Container Registry, pero tenga en cuenta que hay otras opciones, como la CLI de Azure. Siga estos pasos para crear un nuevo recurso de Azure Container Registry:

1. Inicie sesión en [Azure Portal](http://portal.azure.com) y cree un nuevo recurso de Azure Container Registry. Proporcione un nombre de registro (tenga en cuenta que este nombre se establecerá como la propiedad `docker.registry` en `pom.xml`). Cambie los valores predeterminados como desee y haga clic en "crear".

1. Una vez que activado el registro de contenedor (unos 30 segundos después de hacer clic en "crear"), haga clic en él y haga clic en el vínculo "Claves de acceso", en el área de menú de la izquierda. Aquí, deberá habilitar la opción "Usuario administrador" para poder acceder a este registro de contenedor desde nuestros equipos (para insertar contenedores de Docker en él), y también para habilitar el acceso desde la instancia de Azure Web App for Containers que vamos a instalar.

1. Cuando esté en el área "Claves de acceso", anote los valores `username` y `password`. Vamos a copiar y pegar estos valores en nuestro archivo `settings.xml` global de Maven (para más información sobre la configuración de Maven, consulte el sitio web de [Apache Maven Project](https://maven.apache.org/settings.html)). Como referencia, esta es una versión alterada del archivo `${user.home}/.m2/settings.xml` en el sistema de los autores:

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

Una vez completado, podemos continuar compilando y ejecutando nuestra aplicación de MicroProfile localmente.

## <a name="creating-our-microprofile-application"></a>Creación de nuestra aplicación MicroProfile

Este ejemplo se basa en una aplicación de ejemplo disponible en GitHub, por lo que vamos a clonarla y a recorrer el código. Siga estos pasos para obtener el código clonado en su equipo:

1. `git clone https://github.com/Azure-Samples/microprofile-docker-helloworld.git`
1. `cd microprofile-docker-helloworld`

En este directorio hay un archivo `pom.xml` que se usa para especificar el proyecto en el formato usado por la herramienta de compilación de Maven. Este archivo se puede editar para ajustarlo a sus necesidades. En concreto, las propiedades `docker.registry` y `docker.name` deben cambiarse a los valores `docker.registry` y `docker.name` creados cuando se configuró el recurso de Azure Container Registry.

Otro archivo para tener en cuenta en este directorio es Dockerfile, que se reproduce a continuación:

```dockerfile
FROM payara/micro

ARG WAR_FILE
COPY target/${WAR_FILE} $DEPLOY_DIR

EXPOSE 8080
```

Este archivo Dockerfile simplemente crea un nuevo contenedor de Docker basado en el contenedor de Docker de Payara Micro, y lo copia en el archivo .war creado como parte del proceso de compilación. También expone el puerto 8080 para poder tener acceso al servicio una vez que esté en marcha en un contenedor de Docker.

Si profundizamos en el directorio `src`, veremos la clase `Application` que se reproduce a continuación:

```java
package com.microsoft.azure.samples.microprofile.docker.helloworld;

import javax.ws.rs.ApplicationPath;

@ApplicationPath("/api")
public class Application extends javax.ws.rs.core.Application { }
```

La anotación `@ApplicationPath("/api")` especifica el punto de conexión de base para este microservicio; es decir, todos los extremos incluirán `/api` antes de la dirección URL necesaria para tener acceso a otros puntos de conexión REST específicos.

Dentro del paquete `api`, hay una clase llamada `API`, que contiene el código siguiente:

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

Podemos usar la anotación `@Path("/helloworld")` para ver que este punto de conexión REST, cuando se combina con el valor de `/api` especificado en la clase `Application`, será `/api/helloworld`. Cuando se llama a este punto de conexión mediante una solicitud HTTP GET, podemos ver que el método generará texto/html que, en realidad, es simplemente una cadena codificada de forma rígida "Hello, world!".

Ya hemos tratado todo el código necesario para crear un microservicio con MicroProfile. Ahora podemos usar Maven para compilarlo, incluirlo en un contenedor de Docker y ejecutarlo localmente. Para ello, siga estos pasos:

1. Ejecute `mvn clean package` y espere hasta que se complete correctamente.

1. Ejecute `docker run -it --rm -p 8080:8080 <docker.registry>/<docker.name>:latest`, por ejemplo, `docker run -it --rm -p 8080:8080 jogilescr.azurecr.io/samples/docker-helloworld:latest`, si su `docker.registry` es `jogilescr.azurecr.io` y `docker.name` es `samples/docker-helloworld`.

1. Intente acceder a [http://localhost:8080/microprofile/api/helloworld](http://localhost:8080/microprofile/api/helloworld) y [http://localhost:8080/health ](http://localhost:8080/health) en el explorador web. Si ve la respuesta "¡Hello, world!" esperada (y la información relacionada con el estado de mantenimiento del punto de conexión [/health](http://localhost:8080/health)), ha implementado correctamente la aplicación de MicroProfile en el equipo local.

## <a name="pushing-to-the-azure-container-registry"></a>Publicación en Azure Container Registry

Ahora que hemos creado y ejecutado correctamente nuestra aplicación de MicroProfile en la máquina local, el siguiente paso es insertar este contenedor en el registro de contenedor. En este tutorial usamos Azure Container Registry, pero funcionará cualquier registro de contenedor (siempre y cuando se edite el archivo `pom.xml` para que apunte a la ubicación correspondiente).

1. Ejecute `mvn clean package` para limpiar, compilar y crear una imagen de Docker local.
2. Ejecute `mvn dockerfile:push` para insertar el cambio en Azure Container Registry.

En esta fase, ya tiene la imagen de contenedor de Docker cargada en Azure Container Registry, pero no está aún en ejecución porque ahora tenemos que implementarla en una instancia de Azure Web App for Containers. Vamos a hacerlo ahora.

## <a name="creating-an-azure-web-app-for-containers-instance"></a>Creación de una instancia de Azure Web App for Containers

1. Vuelva a [Azure Portal](http://portal.azure.com) y cree una nueva instancia de Web App for Containers (en el encabezado "Web y móvil" del menú). Algunas sugerencias:

   1. El nombre que especifique aquí será la dirección URL pública de la aplicación web (aunque más adelante puede agregar un dominio personalizado si lo desea), por lo que es una buena idea elegir un nombre que pueda recordar fácilmente.

   1. Cuando llegue a la sección "Configurar contenedor", puede seleccionar "Azure Container Registry" en "Origen de imagen" y, a continuación, seleccione la imagen correcta en las listas desplegables.

   1. No es necesario especificar ningún valor en el campo de "Archivo de inicio".

1. Una vez creada la instancia (de nuevo, es muy rápido), haga clic en ella y, después, haga clic en el elemento de menú "Configuración de la aplicación". Aquí deberá agregar una nueva configuración de la aplicación, en la que la clave es `WEBSITES_PORT` y el valor es `8080`. Esto indica a Azure qué puerto desea exponer en el contenedor, y se asignará al puerto 80 externamente.

1. También puede hacer clic en el vínculo "Contenedor de Docker" y habilitar "Implementación continua" para que, cada vez que actualice la imagen de Azure Container Registry, se actualice automáticamente en la instancia de Azure Web App for Containers.

1. Debe poder acceder a las instancias de Azure hospedadas en `http://<appname>.azurewebsites.net/microprofile/api/helloworld` y `http://<appname>.azurewebsites.net/health`.

## <a name="summary"></a>Resumen

En este tutorial, hemos recorrido el proceso para crear un microservicio de MicroProfile sencillo, incluirlo en un contenedor de Docker, y lo hemos publicado en Azure y ejecutado localmente. La ampliación del microservicio para proporcionar funcionalidades más útiles queda fuera del ámbito de este tutorial, pero hay una gran cantidad de tutoriales y consejos sobre MicroProfile en Internet. Se recomienda [MicroProfile.io](https://microprofile.io/) para consultar más contenido.
