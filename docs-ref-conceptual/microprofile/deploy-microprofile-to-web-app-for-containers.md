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
# <a name="deploy-a-java-based-microprofile-service-to-azure-web-app-for-containers"></a><span data-ttu-id="0908e-103">Implementación de un servicio de MicroProfile basado en Java en Azure Web Apps for Containers</span><span class="sxs-lookup"><span data-stu-id="0908e-103">Deploy a Java-based MicroProfile service to Azure Web App for Containers</span></span>

<span data-ttu-id="0908e-104">MicroProfile es una excelente manera de crear pequeñas aplicaciones de Java que se pueden implementar de forma rápida y sencilla en servicios como [Azure Web Apps for Containers](https://azure.microsoft.com/services/app-service/containers/).</span><span class="sxs-lookup"><span data-stu-id="0908e-104">MicroProfile is a great way to build exceedingly tiny Java applications that can be quickly and easily deployed to services such as [Azure Web App for Containers](https://azure.microsoft.com/services/app-service/containers/).</span></span> <span data-ttu-id="0908e-105">En este tutorial, crearemos un microservicio sencillo basado en MicroProfile que, a continuación, se incluirá en un contenedor de Docker implementado en un recurso de [Azure Container Registry](https://azure.microsoft.com/services/container-registry/), y se hospedará con Azure Web App for Containers.</span><span class="sxs-lookup"><span data-stu-id="0908e-105">In this tutorial we will create a simple MicroProfile-based microservice that is then containerized into a Docker container, deployed into an [Azure Container Registry](https://azure.microsoft.com/services/container-registry/), and then hosted using Azure Web App for Containers.</span></span>

> [!NOTE]
>
> <span data-ttu-id="0908e-106">Este procedimiento funciona con cualquier implementación de MicroProfile.io siempre que la imagen del contenedor de Docker sea autoejecutable (es decir, que incluya el entorno de ejecución).</span><span class="sxs-lookup"><span data-stu-id="0908e-106">This procedure works with any implementation of MicroProfile.io as long the Docker container image is self-executable (i.e. includes the runtime).</span></span>

<span data-ttu-id="0908e-107">Más concretamente, este ejemplo usa [Payara Micro](https://www.payara.fish/payara_micro) y [MicroProfile 1.3](https://microprofile.io/) para crear un pequeño archivo .war de Java (5,085 bytes en el equipo de autores) y, a continuación, lo empaqueta en una imagen de Docker (de unos 174 megabytes aproximadamente).</span><span class="sxs-lookup"><span data-stu-id="0908e-107">More concretely, this sample makes use of [Payara Micro](https://www.payara.fish/payara_micro) and [MicroProfile 1.3](https://microprofile.io/) to create a tiny Java war file (5,085 bytes on the authors machine), and then packages it up into a Docker image (which is approximately 174 megabytes).</span></span> <span data-ttu-id="0908e-108">Esta imagen de Docker contiene todo lo necesario para una implementación incluida totalmente en un contenedor de esta aplicación web.</span><span class="sxs-lookup"><span data-stu-id="0908e-108">This Docker image contains everything necessary for a fully-containerised deployment of this webapp.</span></span>

<span data-ttu-id="0908e-109">Debido a la manera en que Docker funciona, suele ocurrir que no es necesario volver a implementar la imagen de Docker completa de 174 megabytes cada vez que se cambia el código fuente, porque Docker carga solo las diferencias (cuyo tamaño es significativamente más pequeño).</span><span class="sxs-lookup"><span data-stu-id="0908e-109">Because of the way Docker works, it is often the case that the entire 174 megabyte Docker image does not need to be redeployed whenever the application source code is changed, as Docker will only upload the differences (which is significantly smaller).</span></span> <span data-ttu-id="0908e-110">Esto hace que el proceso de ejecución de una nueva versión de una aplicación de MicroProfile a través de una canalización de CI/CD sea eficaz y rápida, lo que reduce la fricción y permite una iteración rápida del desarrollo.</span><span class="sxs-lookup"><span data-stu-id="0908e-110">This makes the process of executing a new release of a MicroProfile application via a CI/CD pipeline extremely efficient and quick, reducing friction and enabling rapid development iteration.</span></span>

<span data-ttu-id="0908e-111">En este tutorial, primero vamos a crear y ejecutar el código localmente y, después, lo implementaremos como una aplicación web en Azure.</span><span class="sxs-lookup"><span data-stu-id="0908e-111">We will work through this tutorial firstly by creating and running the code locally, and then we will deploy this as a web app on Azure.</span></span> <span data-ttu-id="0908e-112">En ambos casos, dependeremos de Docker para simplificar y normalizar nuestros esfuerzos.</span><span class="sxs-lookup"><span data-stu-id="0908e-112">In both cases we will depend on Docker to simplify and standardize our efforts.</span></span> <span data-ttu-id="0908e-113">Antes de comenzar, crearemos un recurso de Azure Container Registry en la que almacenaremos los contenedores de Docker.</span><span class="sxs-lookup"><span data-stu-id="0908e-113">Before we begin, we will create an Azure Container Registry to store our Docker containers in.</span></span>

## <a name="creating-an-azure-container-registry"></a><span data-ttu-id="0908e-114">Creación de un recurso de Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="0908e-114">Creating an Azure Container Registry</span></span>

<span data-ttu-id="0908e-115">Usaremos [Azure Portal](http://portal.azure.com) para crear el recurso de Azure Container Registry, pero tenga en cuenta que hay otras opciones, como la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="0908e-115">We will use the [Azure Portal](http://portal.azure.com) for creating the Azure Container Registry, but note that there are alternate choices such as the Azure CLI.</span></span> <span data-ttu-id="0908e-116">Siga estos pasos para crear un nuevo recurso de Azure Container Registry:</span><span class="sxs-lookup"><span data-stu-id="0908e-116">Follow the steps below to create a new Azure Container Registry:</span></span>

1. <span data-ttu-id="0908e-117">Inicie sesión en [Azure Portal](http://portal.azure.com) y cree un nuevo recurso de Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="0908e-117">Log in to the [Azure Portal](http://portal.azure.com) and create a new Azure Container Registry resource.</span></span> <span data-ttu-id="0908e-118">Proporcione un nombre de registro (tenga en cuenta que este nombre se establecerá como la propiedad `docker.registry` en `pom.xml`).</span><span class="sxs-lookup"><span data-stu-id="0908e-118">Provide a registry name (note that this is the name that should be set as the `docker.registry` property in `pom.xml`).</span></span> <span data-ttu-id="0908e-119">Cambie los valores predeterminados como desee y haga clic en "crear".</span><span class="sxs-lookup"><span data-stu-id="0908e-119">Change the defaults as you wish, and then click 'create'.</span></span>

1. <span data-ttu-id="0908e-120">Una vez que activado el registro de contenedor (unos 30 segundos después de hacer clic en "crear"), haga clic en él y haga clic en el vínculo "Claves de acceso", en el área de menú de la izquierda.</span><span class="sxs-lookup"><span data-stu-id="0908e-120">Once the container registry is live (which is about 30 seconds after clicking 'create'), click on the container registry, and click on the 'Access keys' link in the left-menu area.</span></span> <span data-ttu-id="0908e-121">Aquí, deberá habilitar la opción "Usuario administrador" para poder acceder a este registro de contenedor desde nuestros equipos (para insertar contenedores de Docker en él), y también para habilitar el acceso desde la instancia de Azure Web App for Containers que vamos a instalar.</span><span class="sxs-lookup"><span data-stu-id="0908e-121">In here, you need to enable the 'admin user' setting, so that this container registry can be accessed from our machines (to push docker containers into), and also to enable access from the Azure Web Apps for Containers instance we will setup soon.</span></span>

1. <span data-ttu-id="0908e-122">Cuando esté en el área "Claves de acceso", anote los valores `username` y `password`.</span><span class="sxs-lookup"><span data-stu-id="0908e-122">Whilst you are in the 'Access keys' area, note the `username` and `password` values.</span></span> <span data-ttu-id="0908e-123">Vamos a copiar y pegar estos valores en nuestro archivo `settings.xml` global de Maven (para más información sobre la configuración de Maven, consulte el sitio web de [Apache Maven Project](https://maven.apache.org/settings.html)).</span><span class="sxs-lookup"><span data-stu-id="0908e-123">We will copy / paste these into our global Maven `settings.xml` file  (for more information on Maven settings, refer to the [Apache Maven Project](https://maven.apache.org/settings.html) website).</span></span> <span data-ttu-id="0908e-124">Como referencia, esta es una versión alterada del archivo `${user.home}/.m2/settings.xml` en el sistema de los autores:</span><span class="sxs-lookup"><span data-stu-id="0908e-124">For reference, here is an obfuscated version of the `${user.home}/.m2/settings.xml` file on the authors system:</span></span>

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

<span data-ttu-id="0908e-125">Una vez completado, podemos continuar compilando y ejecutando nuestra aplicación de MicroProfile localmente.</span><span class="sxs-lookup"><span data-stu-id="0908e-125">Now that this is complete, we can move on with building and running our MicroProfile application locally.</span></span>

## <a name="creating-our-microprofile-application"></a><span data-ttu-id="0908e-126">Creación de nuestra aplicación MicroProfile</span><span class="sxs-lookup"><span data-stu-id="0908e-126">Creating our MicroProfile application</span></span>

<span data-ttu-id="0908e-127">Este ejemplo se basa en una aplicación de ejemplo disponible en GitHub, por lo que vamos a clonarla y a recorrer el código.</span><span class="sxs-lookup"><span data-stu-id="0908e-127">This example is based on a sample application available on GitHub, so we will clone that and then step through the code.</span></span> <span data-ttu-id="0908e-128">Siga estos pasos para obtener el código clonado en su equipo:</span><span class="sxs-lookup"><span data-stu-id="0908e-128">Follow the steps below to get the code cloned onto your machine:</span></span>

1. `git clone https://github.com/Azure-Samples/microprofile-docker-helloworld.git`
1. `cd microprofile-docker-helloworld`

<span data-ttu-id="0908e-129">En este directorio hay un archivo `pom.xml` que se usa para especificar el proyecto en el formato usado por la herramienta de compilación de Maven.</span><span class="sxs-lookup"><span data-stu-id="0908e-129">In this directory there is a `pom.xml` file that is used to specify the project in the format used by the Maven build tool.</span></span> <span data-ttu-id="0908e-130">Este archivo se puede editar para ajustarlo a sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="0908e-130">This file can be edited to suit your own needs.</span></span> <span data-ttu-id="0908e-131">En concreto, las propiedades `docker.registry` y `docker.name` deben cambiarse a los valores `docker.registry` y `docker.name` creados cuando se configuró el recurso de Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="0908e-131">In particular, the `docker.registry` and `docker.name` properties should be changed to the `docker.registry` and `docker.name` created when the Azure Container Registry was setup.</span></span>

<span data-ttu-id="0908e-132">Otro archivo para tener en cuenta en este directorio es Dockerfile, que se reproduce a continuación:</span><span class="sxs-lookup"><span data-stu-id="0908e-132">Another file of note in this directory is the Dockerfile, which is reproduced below:</span></span>

```dockerfile
FROM payara/micro

ARG WAR_FILE
COPY target/${WAR_FILE} $DEPLOY_DIR

EXPOSE 8080
```

<span data-ttu-id="0908e-133">Este archivo Dockerfile simplemente crea un nuevo contenedor de Docker basado en el contenedor de Docker de Payara Micro, y lo copia en el archivo .war creado como parte del proceso de compilación.</span><span class="sxs-lookup"><span data-stu-id="0908e-133">This Dockerfile simply creates a new Docker container based on the Payara Micro Docker Container, and copies in the .war file that is created as part of our build process.</span></span> <span data-ttu-id="0908e-134">También expone el puerto 8080 para poder tener acceso al servicio una vez que esté en marcha en un contenedor de Docker.</span><span class="sxs-lookup"><span data-stu-id="0908e-134">It also exposes port 8080 so that we may access the service once it is up and running within a Docker container.</span></span>

<span data-ttu-id="0908e-135">Si profundizamos en el directorio `src`, veremos la clase `Application` que se reproduce a continuación:</span><span class="sxs-lookup"><span data-stu-id="0908e-135">Diving into the `src` directory, we will eventually discover the `Application` class reproduced below:</span></span>

```java
package com.microsoft.azure.samples.microprofile.docker.helloworld;

import javax.ws.rs.ApplicationPath;

@ApplicationPath("/api")
public class Application extends javax.ws.rs.core.Application { }
```

<span data-ttu-id="0908e-136">La anotación `@ApplicationPath("/api")` especifica el punto de conexión de base para este microservicio; es decir, todos los extremos incluirán `/api` antes de la dirección URL necesaria para tener acceso a otros puntos de conexión REST específicos.</span><span class="sxs-lookup"><span data-stu-id="0908e-136">The `@ApplicationPath("/api")` annotation specifies the base endpoint for this microservice - that is, that all endpoints will have `/api` preceed the rest of the URL required to access any specific REST endpoint.</span></span>

<span data-ttu-id="0908e-137">Dentro del paquete `api`, hay una clase llamada `API`, que contiene el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="0908e-137">Inside the `api` package is a class named `API`, which contains the following code:</span></span>

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

<span data-ttu-id="0908e-138">Podemos usar la anotación `@Path("/helloworld")` para ver que este punto de conexión REST, cuando se combina con el valor de `/api` especificado en la clase `Application`, será `/api/helloworld`.</span><span class="sxs-lookup"><span data-stu-id="0908e-138">Through the use of the `@Path("/helloworld")` annotation, we can see that this REST endpoint, when combined with the `/api` specified in the `Application` class, will be `/api/helloworld`.</span></span> <span data-ttu-id="0908e-139">Cuando se llama a este punto de conexión mediante una solicitud HTTP GET, podemos ver que el método generará texto/html que, en realidad, es simplemente una cadena codificada de forma rígida "Hello, world!".</span><span class="sxs-lookup"><span data-stu-id="0908e-139">When this endpoint is called using an HTTP GET request, we can see that the method will produce text/html, and in fact it is simply a hard-coded string "Hello, world!".</span></span>

<span data-ttu-id="0908e-140">Ya hemos tratado todo el código necesario para crear un microservicio con MicroProfile.</span><span class="sxs-lookup"><span data-stu-id="0908e-140">We have now covered all the code required to create a microservice using MicroProfile.</span></span> <span data-ttu-id="0908e-141">Ahora podemos usar Maven para compilarlo, incluirlo en un contenedor de Docker y ejecutarlo localmente.</span><span class="sxs-lookup"><span data-stu-id="0908e-141">We can now use Maven to build it, containerize it into a Docker container, and run it locally.</span></span> <span data-ttu-id="0908e-142">Para ello, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="0908e-142">We can do that with the following steps:</span></span>

1. <span data-ttu-id="0908e-143">Ejecute `mvn clean package` y espere hasta que se complete correctamente.</span><span class="sxs-lookup"><span data-stu-id="0908e-143">Run `mvn clean package` and wait until it successfully completes.</span></span>

1. <span data-ttu-id="0908e-144">Ejecute `docker run -it --rm -p 8080:8080 <docker.registry>/<docker.name>:latest`, por ejemplo, `docker run -it --rm -p 8080:8080 jogilescr.azurecr.io/samples/docker-helloworld:latest`, si su `docker.registry` es `jogilescr.azurecr.io` y `docker.name` es `samples/docker-helloworld`.</span><span class="sxs-lookup"><span data-stu-id="0908e-144">Run `docker run -it --rm -p 8080:8080 <docker.registry>/<docker.name>:latest`, for example, `docker run -it --rm -p 8080:8080 jogilescr.azurecr.io/samples/docker-helloworld:latest`, if your `docker.registry` is `jogilescr.azurecr.io` and `docker.name` is `samples/docker-helloworld`.</span></span>

1. <span data-ttu-id="0908e-145">Intente acceder a [http://localhost:8080/microprofile/api/helloworld](http://localhost:8080/microprofile/api/helloworld) y [http://localhost:8080/health ](http://localhost:8080/health) en el explorador web.</span><span class="sxs-lookup"><span data-stu-id="0908e-145">Try accessing [http://localhost:8080/microprofile/api/helloworld](http://localhost:8080/microprofile/api/helloworld) and [http://localhost:8080/health](http://localhost:8080/health) in your web browser.</span></span> <span data-ttu-id="0908e-146">Si ve la respuesta "¡Hello, world!"</span><span class="sxs-lookup"><span data-stu-id="0908e-146">If you see the expected "Hello, world!"</span></span> <span data-ttu-id="0908e-147">esperada (y la información relacionada con el estado de mantenimiento del punto de conexión [/health](http://localhost:8080/health)), ha implementado correctamente la aplicación de MicroProfile en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="0908e-147">response (and health-related information for the [/health](http://localhost:8080/health) endpoint), you have successfully deployed the MicroProfile application on your local machine.</span></span>

## <a name="pushing-to-the-azure-container-registry"></a><span data-ttu-id="0908e-148">Publicación en Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="0908e-148">Pushing to the Azure Container Registry</span></span>

<span data-ttu-id="0908e-149">Ahora que hemos creado y ejecutado correctamente nuestra aplicación de MicroProfile en la máquina local, el siguiente paso es insertar este contenedor en el registro de contenedor.</span><span class="sxs-lookup"><span data-stu-id="0908e-149">Now that we have successfully built and run our MicroProfile application on our local machine, the next step is to push this container into our container registry.</span></span> <span data-ttu-id="0908e-150">En este tutorial usamos Azure Container Registry, pero funcionará cualquier registro de contenedor (siempre y cuando se edite el archivo `pom.xml` para que apunte a la ubicación correspondiente).</span><span class="sxs-lookup"><span data-stu-id="0908e-150">In this tutorial we are using the Azure Container Registry, but any container registry will work (as long as the `pom.xml` file is edited to point to the relevant location).</span></span>

1. <span data-ttu-id="0908e-151">Ejecute `mvn clean package` para limpiar, compilar y crear una imagen de Docker local.</span><span class="sxs-lookup"><span data-stu-id="0908e-151">Run `mvn clean package` to clean, compile, and create a local docker image.</span></span>
2. <span data-ttu-id="0908e-152">Ejecute `mvn dockerfile:push` para insertar el cambio en Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="0908e-152">Run `mvn dockerfile:push` to push to the Azure Container Registry.</span></span>

<span data-ttu-id="0908e-153">En esta fase, ya tiene la imagen de contenedor de Docker cargada en Azure Container Registry, pero no está aún en ejecución porque ahora tenemos que implementarla en una instancia de Azure Web App for Containers.</span><span class="sxs-lookup"><span data-stu-id="0908e-153">At this stage you now have your docker container image uploaded to the Azure Container Registry, but it is not yet running as we now have to deploy it into an Azure Web App for Containers instance.</span></span> <span data-ttu-id="0908e-154">Vamos a hacerlo ahora.</span><span class="sxs-lookup"><span data-stu-id="0908e-154">We will now do that.</span></span>

## <a name="creating-an-azure-web-app-for-containers-instance"></a><span data-ttu-id="0908e-155">Creación de una instancia de Azure Web App for Containers</span><span class="sxs-lookup"><span data-stu-id="0908e-155">Creating an Azure Web App for Containers instance</span></span>

1. <span data-ttu-id="0908e-156">Vuelva a [Azure Portal](http://portal.azure.com) y cree una nueva instancia de Web App for Containers (en el encabezado "Web y móvil" del menú).</span><span class="sxs-lookup"><span data-stu-id="0908e-156">Return to the [Azure Portal](http://portal.azure.com) and create a new Web App for Containers instance (located under the 'Web + Mobile' heading in the menu).</span></span> <span data-ttu-id="0908e-157">Algunas sugerencias:</span><span class="sxs-lookup"><span data-stu-id="0908e-157">A few pointers:</span></span>

   1. <span data-ttu-id="0908e-158">El nombre que especifique aquí será la dirección URL pública de la aplicación web (aunque más adelante puede agregar un dominio personalizado si lo desea), por lo que es una buena idea elegir un nombre que pueda recordar fácilmente.</span><span class="sxs-lookup"><span data-stu-id="0908e-158">The name you specify here will be the public URL of the web app (although a custom domain can be added later if desired), so it is a good idea to pick a name that you can easily remember.</span></span>

   1. <span data-ttu-id="0908e-159">Cuando llegue a la sección "Configurar contenedor", puede seleccionar "Azure Container Registry" en "Origen de imagen" y, a continuación, seleccione la imagen correcta en las listas desplegables.</span><span class="sxs-lookup"><span data-stu-id="0908e-159">When you get to the 'Configure container' section, you can select 'Azure Container Registry' for the 'Image source', and then select the correct image from the drop-down lists.</span></span>

   1. <span data-ttu-id="0908e-160">No es necesario especificar ningún valor en el campo de "Archivo de inicio".</span><span class="sxs-lookup"><span data-stu-id="0908e-160">You do not need to specify any value in the 'Startup File' field.</span></span>

1. <span data-ttu-id="0908e-161">Una vez creada la instancia (de nuevo, es muy rápido), haga clic en ella y, después, haga clic en el elemento de menú "Configuración de la aplicación".</span><span class="sxs-lookup"><span data-stu-id="0908e-161">Once the instance is created (again, it is very quick), click on it and then click on the 'Application Settings' menu item.</span></span> <span data-ttu-id="0908e-162">Aquí deberá agregar una nueva configuración de la aplicación, en la que la clave es `WEBSITES_PORT` y el valor es `8080`.</span><span class="sxs-lookup"><span data-stu-id="0908e-162">In here you need to add a new application setting, where the key is `WEBSITES_PORT` and the value is `8080`.</span></span> <span data-ttu-id="0908e-163">Esto indica a Azure qué puerto desea exponer en el contenedor, y se asignará al puerto 80 externamente.</span><span class="sxs-lookup"><span data-stu-id="0908e-163">This tells Azure which port you want to expose in the container, and it will be mapped to port 80 externally.</span></span>

1. <span data-ttu-id="0908e-164">También puede hacer clic en el vínculo "Contenedor de Docker" y habilitar "Implementación continua" para que, cada vez que actualice la imagen de Azure Container Registry, se actualice automáticamente en la instancia de Azure Web App for Containers.</span><span class="sxs-lookup"><span data-stu-id="0908e-164">Optionally, click on the 'Docker Container' link, and enable 'Continuous Deployment', so that whenever you update the Azure Container Registry image it is automatically updated in the Azure Web App for Containers instance.</span></span>

1. <span data-ttu-id="0908e-165">Debe poder acceder a las instancias de Azure hospedadas en `http://<appname>.azurewebsites.net/microprofile/api/helloworld` y `http://<appname>.azurewebsites.net/health`.</span><span class="sxs-lookup"><span data-stu-id="0908e-165">You should be able to access the Azure-hosted instances at `http://<appname>.azurewebsites.net/microprofile/api/helloworld` and `http://<appname>.azurewebsites.net/health`.</span></span>

## <a name="summary"></a><span data-ttu-id="0908e-166">Resumen</span><span class="sxs-lookup"><span data-stu-id="0908e-166">Summary</span></span>

<span data-ttu-id="0908e-167">En este tutorial, hemos recorrido el proceso para crear un microservicio de MicroProfile sencillo, incluirlo en un contenedor de Docker, y lo hemos publicado en Azure y ejecutado localmente.</span><span class="sxs-lookup"><span data-stu-id="0908e-167">Through this tutorial we have stepped through the process of creating a simple MicroProfile-based microservice, containerized it into a Docker container, and we have run it locally and published it to Azure.</span></span> <span data-ttu-id="0908e-168">La ampliación del microservicio para proporcionar funcionalidades más útiles queda fuera del ámbito de este tutorial, pero hay una gran cantidad de tutoriales y consejos sobre MicroProfile en Internet. Se recomienda [MicroProfile.io](https://microprofile.io/) para consultar más contenido.</span><span class="sxs-lookup"><span data-stu-id="0908e-168">Extending our microservice to provide more useful functionality is outside the scope of this tutorial, but there is a wealth of tutorials and advice on MicroProfile on the internet, and readers are encouraged to review [MicroProfile.io](https://microprofile.io/) for more content.</span></span>
