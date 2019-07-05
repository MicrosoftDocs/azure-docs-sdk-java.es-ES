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
# <a name="deploy-a-java-based-microprofile-service-to-azure-web-app-for-containers"></a><span data-ttu-id="d5b6f-103">Implementación de un servicio de MicroProfile basado en Java en Azure Web Apps for Containers</span><span class="sxs-lookup"><span data-stu-id="d5b6f-103">Deploy a Java-based MicroProfile service to Azure Web App for Containers</span></span>

<span data-ttu-id="d5b6f-104">MicroProfile es una excelente manera de crear pequeñas aplicaciones de Java que se pueden implementar de forma rápida y sencilla en servicios como [Azure Web Apps for Containers](https://azure.microsoft.com/services/app-service/containers/).</span><span class="sxs-lookup"><span data-stu-id="d5b6f-104">MicroProfile is a great way to build exceedingly small Java applications that you can quickly and easily deploy to services such as [Azure Web App for Containers](https://azure.microsoft.com/services/app-service/containers/).</span></span> <span data-ttu-id="d5b6f-105">En este tutorial, crearemos un microservicio sencillo basado en MicroProfile que, a continuación, se incluirá en un contenedor de Docker implementado en una [instancia de registro de contenedor de Azure](https://azure.microsoft.com/services/container-registry/), y se hospedará en Azure Web App for Containers.</span><span class="sxs-lookup"><span data-stu-id="d5b6f-105">In this tutorial, you create a simple, MicroProfile-based microservice that you containerize into a Docker container, deploy to an [Azure container registry instance](https://azure.microsoft.com/services/container-registry/), and then host by using Azure Web App for Containers.</span></span>

> [!NOTE]
> <span data-ttu-id="d5b6f-106">Este procedimiento funciona con cualquier implementación de MicroProfile.io siempre que la imagen del contenedor de Docker sea autoejecutable (es decir, la imagen incluye el entorno de ejecución).</span><span class="sxs-lookup"><span data-stu-id="d5b6f-106">This procedure works with any implementation of MicroProfile.io, as long the Docker container image is self-executable (that is, the image includes the runtime).</span></span>

<span data-ttu-id="d5b6f-107">En este ejemplo, se usa [Payara Micro](https://www.payara.fish/payara_micro) y [MicroProfile 1.3](https://microprofile.io/) para crear un pequeño archivo de requisitos de aplicación web (WAR) de Java de aproximadamente 5 000 bytes y, a continuación, se empaqueta en una imagen de Docker de aproximadamente 174 megabytes (MB).</span><span class="sxs-lookup"><span data-stu-id="d5b6f-107">In this sample, you use [Payara Micro](https://www.payara.fish/payara_micro) and [MicroProfile 1.3](https://microprofile.io/) to create a small (approximately 5,000 bytes) Java web application requirement (WAR) file, and then package it into a Docker image of approximately 174 megabytes (MB).</span></span> <span data-ttu-id="d5b6f-108">Esta imagen de Docker contiene todo lo necesario para realizar una implementación totalmente incluida en un contenedor de esta aplicación web.</span><span class="sxs-lookup"><span data-stu-id="d5b6f-108">The Docker image contains everything necessary for a fully containerized deployment of the web app.</span></span>

<span data-ttu-id="d5b6f-109">No es necesario volver a implementar una imagen de Docker de 174 MB completa cada vez que cambie el código fuente, porque Docker carga solo las diferencias (que son mucho más pequeñas).</span><span class="sxs-lookup"><span data-stu-id="d5b6f-109">An entire 174 MB Docker image doesn't need to be redeployed whenever the application source code is changed, because Docker uploads only the differences (which are significantly smaller).</span></span> <span data-ttu-id="d5b6f-110">Por lo tanto, el proceso de ejecución de una nueva versión de una aplicación de MicroProfile a través de una canalización de CI/CD sea eficaz y rápida, lo que reduce la fricción y permite una iteración rápida del desarrollo.</span><span class="sxs-lookup"><span data-stu-id="d5b6f-110">Consequently, the process of executing a new release of a MicroProfile application via a CI/CD pipeline is extremely efficient and quick, reducing friction and enabling rapid development iteration.</span></span>

<span data-ttu-id="d5b6f-111">En este tutorial, primero vamos a crear y ejecutar el código localmente y, después, lo implementaremos como una aplicación web en Azure.</span><span class="sxs-lookup"><span data-stu-id="d5b6f-111">You'll work through this tutorial by first creating and running the code locally and then deploying it as a web app on Azure.</span></span> <span data-ttu-id="d5b6f-112">En ambos casos, dependeremos de Docker para simplificar y normalizar nuestros esfuerzos.</span><span class="sxs-lookup"><span data-stu-id="d5b6f-112">In both phases, you can depend on Docker to simplify and standardize your efforts.</span></span> <span data-ttu-id="d5b6f-113">Antes de empezar, crearemos una instancia de registro de contenedor de Azure para almacenar los contenedores de Docker.</span><span class="sxs-lookup"><span data-stu-id="d5b6f-113">Before you begin, you'll create an Azure container registry instance for storing your Docker containers.</span></span>

## <a name="create-an-azure-container-registry-instance"></a><span data-ttu-id="d5b6f-114">Creación de una instancia de registro de contenedor de Azure</span><span class="sxs-lookup"><span data-stu-id="d5b6f-114">Create an Azure container registry instance</span></span>

<span data-ttu-id="d5b6f-115">Puede usar [Azure Portal](http://portal.azure.com) para crear la instancia de registro de contenedor de Azure, pero hay otras opciones, como la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="d5b6f-115">You can use the [Azure portal](http://portal.azure.com) to create the Azure container registry instance, but there are other choices also, such as the Azure CLI.</span></span> <span data-ttu-id="d5b6f-116">Siga estos pasos para crear una nueva instancia de registro de contenedor de Azure:</span><span class="sxs-lookup"><span data-stu-id="d5b6f-116">To create a new Azure container registry instance, do the following:</span></span>

1. <span data-ttu-id="d5b6f-117">Inicie sesión en [Azure Portal](http://portal.azure.com) y cree un nuevo recurso de Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="d5b6f-117">Sign in to the [Azure portal](http://portal.azure.com) and create a new Azure container registry resource.</span></span> <span data-ttu-id="d5b6f-118">Proporcione un nombre de Registro (tenga en cuenta que este nombre se establecerá como la propiedad `docker.registry` en *pom.xml*).</span><span class="sxs-lookup"><span data-stu-id="d5b6f-118">Provide a registry name (this name should be set as the `docker.registry` property in the *pom.xml* file).</span></span> <span data-ttu-id="d5b6f-119">Cambie los valores predeterminados como desee y seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="d5b6f-119">Change the defaults as you want, and then select **Create**.</span></span>

1. <span data-ttu-id="d5b6f-120">En unos 30 segundos, cuando la instancia de registro de contenedor esté activa, selecciónela y, a continuación, en el panel izquierdo, seleccione el vínculo **Claves de acceso**.</span><span class="sxs-lookup"><span data-stu-id="d5b6f-120">In about 30 seconds, when the container registry instance is live, select the container registry instance and then, in the left pane, select the **Access keys** link.</span></span> 

    <span data-ttu-id="d5b6f-121">No olvide habilitar la opción de configuración *admin user* para que pueda acceder a esta instancia de registro de contenedor desde sus máquinas, e insertar contenedores de Docker en ella.</span><span class="sxs-lookup"><span data-stu-id="d5b6f-121">Be sure to enable the *admin user* setting, so that you can access this container registry instance from your machines and push Docker containers into it.</span></span> <span data-ttu-id="d5b6f-122">Al hacerlo, también permitirá el acceso desde la instancia de Azure Web App for Containers que va a configurar.</span><span class="sxs-lookup"><span data-stu-id="d5b6f-122">Doing so also enables access from the Azure Web App for Containers instance that you'll set up soon.</span></span>

1. <span data-ttu-id="d5b6f-123">En el panel **Claves de acceso**, copie los valores **nombre de usuario** y **contraseña** y péguelos en el archivo *settings.xml* global de Maven.</span><span class="sxs-lookup"><span data-stu-id="d5b6f-123">In the **Access keys** pane, copy the **username** and **password** values and paste them into your global Maven *settings.xml* file.</span></span> <span data-ttu-id="d5b6f-124">Para más información acerca de la configuración de Maven, visite el sitio web [Apache Maven Project](https://maven.apache.org/settings.html).</span><span class="sxs-lookup"><span data-stu-id="d5b6f-124">For more information about Maven settings, go to the [Apache Maven Project](https://maven.apache.org/settings.html) website.</span></span> 

   <span data-ttu-id="d5b6f-125">Como referencia, este es un ejemplo del archivo *${user.home}/.m2/settings.xml*:</span><span class="sxs-lookup"><span data-stu-id="d5b6f-125">For your reference, here's an example of the *${user.home}/.m2/settings.xml* file:</span></span>

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

<span data-ttu-id="d5b6f-126">Ahora que ha creado la instancia de registro de contenedor, puede compilar y ejecutar la aplicación MicroProfile localmente.</span><span class="sxs-lookup"><span data-stu-id="d5b6f-126">Now that you've created your container registry instance, you can move on to building and running your MicroProfile application locally.</span></span>

## <a name="create-your-microprofile-application"></a><span data-ttu-id="d5b6f-127">Creación de la aplicación MicroProfile</span><span class="sxs-lookup"><span data-stu-id="d5b6f-127">Create your MicroProfile application</span></span>

<span data-ttu-id="d5b6f-128">Este código de ejemplo se basa en una aplicación de ejemplo que está disponible en GitHub.</span><span class="sxs-lookup"><span data-stu-id="d5b6f-128">This example code is based on a sample application that's available on GitHub.</span></span> <span data-ttu-id="d5b6f-129">Escriba los siguientes comandos para clonar el código en su equipo:</span><span class="sxs-lookup"><span data-stu-id="d5b6f-129">To clone the code onto your machine, enter the following commands:</span></span>

```
git clone https://github.com/Azure-Samples/microprofile-docker-helloworld.git

cd microprofile-docker-helloworld
```

<span data-ttu-id="d5b6f-130">Este directorio contiene un archivo *pom.xml* que se usa para especificar el proyecto en el formato usado por la herramienta de compilación de Maven.</span><span class="sxs-lookup"><span data-stu-id="d5b6f-130">This directory contains a *pom.xml* file that you use to specify the project in the format that's used by the Maven build tool.</span></span> <span data-ttu-id="d5b6f-131">Puede editar el archivo para que se adapte a sus propias necesidades.</span><span class="sxs-lookup"><span data-stu-id="d5b6f-131">You can edit the file to suit your own needs.</span></span> <span data-ttu-id="d5b6f-132">En concreto, las propiedades `docker.registry` y `docker.name` deben cambiarse a los valores `docker.registry` y `docker.name` creados cuando se configuró la instancia de registro de contenedor de Azure.</span><span class="sxs-lookup"><span data-stu-id="d5b6f-132">In particular, the `docker.registry` and `docker.name` properties should be changed to the `docker.registry` and `docker.name` properties that were created when you set up the Azure container registry instance.</span></span>

<span data-ttu-id="d5b6f-133">Otro archivo para tener en cuenta en este directorio es Dockerfile, que se reproduce a continuación:</span><span class="sxs-lookup"><span data-stu-id="d5b6f-133">Another file of note in this directory is the Dockerfile, which is reproduced below:</span></span>

```dockerfile
FROM payara/micro

ARG WAR_FILE
COPY target/${WAR_FILE} $DEPLOY_DIR

EXPOSE 8080
```

<span data-ttu-id="d5b6f-134">Dockerfile crea un nuevo contenedor de Docker que se basa en el contenedor de Docker Payara Micro.</span><span class="sxs-lookup"><span data-stu-id="d5b6f-134">The Dockerfile creates a new Docker container that's based on the Payara Micro Docker Container.</span></span> <span data-ttu-id="d5b6f-135">Copia el archivo WAR que se creó como parte del proceso de compilación.</span><span class="sxs-lookup"><span data-stu-id="d5b6f-135">It copies in the WAR file that was created as part of your build process.</span></span> <span data-ttu-id="d5b6f-136">También expone el puerto 8080 para que pueda tener acceso al servicio una vez que esté en marcha en un contenedor de Docker.</span><span class="sxs-lookup"><span data-stu-id="d5b6f-136">It also exposes port 8080 so that you can access the service after it's up and running within a Docker container.</span></span>

<span data-ttu-id="d5b6f-137">Al abrir el directorio *src*, verá la clase `Application` que se reproduce aquí:</span><span class="sxs-lookup"><span data-stu-id="d5b6f-137">When you open the *src* directory, you'll eventually discover the `Application` class that's reproduced here:</span></span>

```java
package com.microsoft.azure.samples.microprofile.docker.helloworld;

import javax.ws.rs.ApplicationPath;

@ApplicationPath("/api")
public class Application extends javax.ws.rs.core.Application { }
```

<span data-ttu-id="d5b6f-138">La anotación *@ApplicationPath("/api")* especifica el punto de conexión base de este microservicio.</span><span class="sxs-lookup"><span data-stu-id="d5b6f-138">The *@ApplicationPath("/api")* annotation specifies the base endpoint for this microservice.</span></span> <span data-ttu-id="d5b6f-139">Es decir, para todos los puntos de conexión, */api* precede al resto de la dirección URL que se necesita para acceder a cualquier punto de conexión REST específico.</span><span class="sxs-lookup"><span data-stu-id="d5b6f-139">That is, for all endpoints, */api* precedes the rest of the URL that's required to access any specific REST endpoint.</span></span>

<span data-ttu-id="d5b6f-140">Dentro del paquete *api*, hay una clase llamada `API` que contiene el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="d5b6f-140">Inside the *api* package is a class named `API`, which contains the following code:</span></span>

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

<span data-ttu-id="d5b6f-141">Podemos usar la anotación *@Path("/helloworld")* para ver que este punto de conexión REST, cuando se combina con el valor de */api* especificado en la clase `Application`, será */api/helloworld*.</span><span class="sxs-lookup"><span data-stu-id="d5b6f-141">Through the use of the *@Path("/helloworld")* annotation, you can see that this REST endpoint, when it's combined with the */api* that's specified in the `Application` class, will be */api/helloworld*.</span></span> <span data-ttu-id="d5b6f-142">Cuando se llama a este punto de conexión mediante una solicitud HTTP GET, puede ver que el método genera texto/html que, en realidad, es simplemente una cadena codificada de forma rígida "Hello, world!".</span><span class="sxs-lookup"><span data-stu-id="d5b6f-142">When you call this endpoint by using an HTTP GET request, you can see that the method produces text/html and, in fact, it's simply a hard-coded string, "Hello, world!"</span></span>

<span data-ttu-id="d5b6f-143">Hasta ahora, en este artículo hemos visto todo el código necesario para crear un microservicio utilizando MicroProfile.</span><span class="sxs-lookup"><span data-stu-id="d5b6f-143">So far, this article has covered all the code that's required for you to create a microservice by using MicroProfile.</span></span> <span data-ttu-id="d5b6f-144">Ahora puede usar Maven para compilarlo, incluirlo en un contenedor de Docker y ejecutarlo localmente; para ello, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="d5b6f-144">You can now use Maven to build it, containerize it into a Docker container, and run it locally by doing the following:</span></span>

1. <span data-ttu-id="d5b6f-145">Ejecute `mvn clean package` y espere hasta que se complete.</span><span class="sxs-lookup"><span data-stu-id="d5b6f-145">Run `mvn clean package`, and wait until it is complete.</span></span>

1. <span data-ttu-id="d5b6f-146">Ejecute `docker run -it --rm -p 8080:8080 <docker.registry>/<docker.name>:latest`.</span><span class="sxs-lookup"><span data-stu-id="d5b6f-146">Run `docker run -it --rm -p 8080:8080 <docker.registry>/<docker.name>:latest`.</span></span> <span data-ttu-id="d5b6f-147">Por ejemplo, *docker run -it --rm -p 8080:8080 jogilescr.azurecr.io/samples/docker-helloworld:latest*, donde *\<docker.registry>* es *jogilescr.azurecr.io* y *\<docker.name>* es *samples/docker-helloworld*.</span><span class="sxs-lookup"><span data-stu-id="d5b6f-147">For example, *docker run -it --rm -p 8080:8080 jogilescr.azurecr.io/samples/docker-helloworld:latest*, where *\<docker.registry>* is *jogilescr.azurecr.io* and *\<docker.name>* is *samples/docker-helloworld*.</span></span>

1. <span data-ttu-id="d5b6f-148">Intente acceder a [http://localhost:8080/microprofile/api/helloworld](http://localhost:8080/microprofile/api/helloworld) y [http://localhost:8080/health](http://localhost:8080/health) en el explorador web.</span><span class="sxs-lookup"><span data-stu-id="d5b6f-148">Try to access [http://localhost:8080/microprofile/api/helloworld](http://localhost:8080/microprofile/api/helloworld) and [http://localhost:8080/health](http://localhost:8080/health) in your web browser.</span></span> <span data-ttu-id="d5b6f-149">Si ve la respuesta "¡Hello, world!"</span><span class="sxs-lookup"><span data-stu-id="d5b6f-149">If you see the expected "Hello, world!"</span></span> <span data-ttu-id="d5b6f-150">esperada (y la información relacionada con el estado de mantenimiento del punto de conexión [/health](http://localhost:8080/health)), ha implementado correctamente la aplicación de MicroProfile en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="d5b6f-150">response (and health-related information for the [/health](http://localhost:8080/health) endpoint), you've successfully deployed the MicroProfile application on your local machine.</span></span>

## <a name="push-the-container-to-the-azure-container-registry-instance"></a><span data-ttu-id="d5b6f-151">Inserción del contenedor en la instancia de registro de contenedor de Azure</span><span class="sxs-lookup"><span data-stu-id="d5b6f-151">Push the container to the Azure container registry instance</span></span>

<span data-ttu-id="d5b6f-152">Ahora que ha creado y ejecutado correctamente la aplicación de MicroProfile en la máquina local, el siguiente paso es insertar este contenedor en la instancia de registro de contenedor.</span><span class="sxs-lookup"><span data-stu-id="d5b6f-152">Now that you've successfully built and run your MicroProfile application on your local machine, push this container to your container registry instance.</span></span> 

> [!NOTE]
> <span data-ttu-id="d5b6f-153">Aunque en este artículo se usa una instancia de registro de contenedor de Azure, debería funcionar cualquier instancia de registro de contenedor, siempre y cuando el archivo *pom.xml* se edite para que apunte a la ubicación pertinente.</span><span class="sxs-lookup"><span data-stu-id="d5b6f-153">Although this article uses an Azure container registry instance, any container registry instance should work, as long as the *pom.xml* file is edited to point to the relevant location.</span></span>

1. <span data-ttu-id="d5b6f-154">Ejecute `mvn clean package` para limpiar, compilar y crear una imagen de Docker local.</span><span class="sxs-lookup"><span data-stu-id="d5b6f-154">To clean, compile, and create a local Docker image, run `mvn clean package`.</span></span>
2. <span data-ttu-id="d5b6f-155">Para insertar el contenedor en la instancia de registro de contenedor de Azure, ejecute `mvn dockerfile:push`.</span><span class="sxs-lookup"><span data-stu-id="d5b6f-155">To push the container to the Azure container registry instance, run `mvn dockerfile:push`.</span></span>

<span data-ttu-id="d5b6f-156">Ahora tiene la imagen de contenedor de Docker cargada en la instancia de registro de contenedor de Azure.</span><span class="sxs-lookup"><span data-stu-id="d5b6f-156">You now have your Docker container image uploaded to the Azure container registry instance.</span></span> <span data-ttu-id="d5b6f-157">Sin embargo, aún no se está ejecutando.</span><span class="sxs-lookup"><span data-stu-id="d5b6f-157">However, it's not yet running.</span></span> <span data-ttu-id="d5b6f-158">Ahora debe implementarla en una instancia de Azure Web App for Containers.</span><span class="sxs-lookup"><span data-stu-id="d5b6f-158">You now have to deploy it to an Azure Web App for Containers instance.</span></span> 

## <a name="create-an-azure-web-app-for-containers-instance"></a><span data-ttu-id="d5b6f-159">Creación de una instancia de Azure Web App for Containers</span><span class="sxs-lookup"><span data-stu-id="d5b6f-159">Create an Azure Web App for Containers instance</span></span>

1. <span data-ttu-id="d5b6f-160">En [Azure Portal](http://portal.azure.com), en el panel izquierdo, seleccione **Web y móvil** y haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="d5b6f-160">In the [Azure portal](http://portal.azure.com), in the left pane, select **Web + Mobile**, and then do the following:</span></span>

   <span data-ttu-id="d5b6f-161">a.</span><span class="sxs-lookup"><span data-stu-id="d5b6f-161">a.</span></span> <span data-ttu-id="d5b6f-162">Especifique un nombre.</span><span class="sxs-lookup"><span data-stu-id="d5b6f-162">Specify a name.</span></span> <span data-ttu-id="d5b6f-163">El nombre se convertirá en la dirección URL pública de la aplicación web, por lo que es una buena idea elegir un nombre que pueda recordar fácilmente.</span><span class="sxs-lookup"><span data-stu-id="d5b6f-163">The name will become the public URL of the web app, so it's a good idea to pick a name that you can easily remember.</span></span> <span data-ttu-id="d5b6f-164">Puede agregar un nombre de dominio personalizado más adelante, si lo desea.</span><span class="sxs-lookup"><span data-stu-id="d5b6f-164">You can add a custom domain name later, if you want.</span></span>

   <span data-ttu-id="d5b6f-165">b.</span><span class="sxs-lookup"><span data-stu-id="d5b6f-165">b.</span></span> <span data-ttu-id="d5b6f-166">En la sección **Configurar contenedor**, en **Origen de imagen**, seleccione **Azure Container Registry** y, en la lista desplegable, seleccione la imagen correcta.</span><span class="sxs-lookup"><span data-stu-id="d5b6f-166">In the **Configure container** section, under **Image source**, select **Azure Container Registry** and then, in the drop-down list, select the correct image.</span></span>

   <span data-ttu-id="d5b6f-167">c.</span><span class="sxs-lookup"><span data-stu-id="d5b6f-167">c.</span></span> <span data-ttu-id="d5b6f-168">No es necesario especificar ningún valor en el campo **Archivo de inicio**.</span><span class="sxs-lookup"><span data-stu-id="d5b6f-168">You don't need to specify a value in the **Startup File** field.</span></span>

1. <span data-ttu-id="d5b6f-169">Después de crear la instancia, selecciónela y, a continuación, seleccione **Configuración de la aplicación**.</span><span class="sxs-lookup"><span data-stu-id="d5b6f-169">After you've created the instance, select it, and then select **Application Settings**.</span></span> <span data-ttu-id="d5b6f-170">En **Clave**, escriba **WEBSITES_PORT** y en **Valor**, escriba **8080**.</span><span class="sxs-lookup"><span data-stu-id="d5b6f-170">For **Key**, enter **WEBSITES_PORT**, and for **Value**, enter **8080**.</span></span> <span data-ttu-id="d5b6f-171">Estas configuraciones indican a Azure qué puerto se expondrá en el contenedor y lo asignan al puerto 80 externamente.</span><span class="sxs-lookup"><span data-stu-id="d5b6f-171">These settings tell Azure which port to expose in the container and to map it to port 80 externally.</span></span>

1. <span data-ttu-id="d5b6f-172">(Opcional) Seleccione el vínculo **Contenedor de Docker** y habilite **Implementación continua**.</span><span class="sxs-lookup"><span data-stu-id="d5b6f-172">(Optional) Select the **Docker Container** link, and then enable **Continuous Deployment**.</span></span> <span data-ttu-id="d5b6f-173">Al hacerlo, cada vez que actualice la imagen de una instancia de registro de contenedor de Azure, se actualiza automáticamente en la instancia de Azure Web App for Containers.</span><span class="sxs-lookup"><span data-stu-id="d5b6f-173">By doing so, whenever you update the Azure container registry instance image, it's automatically updated in the Azure Web App for Containers instance.</span></span>

1. <span data-ttu-id="d5b6f-174">Ahora podrá acceder a las instancias hospedadas en Azure en `http://<appname>.azurewebsites.net/microprofile/api/helloworld` y `http://<appname>.azurewebsites.net/health`.</span><span class="sxs-lookup"><span data-stu-id="d5b6f-174">You should now be able to access the Azure-hosted instances at `http://<appname>.azurewebsites.net/microprofile/api/helloworld` and `http://<appname>.azurewebsites.net/health`.</span></span>

## <a name="summary"></a><span data-ttu-id="d5b6f-175">Resumen</span><span class="sxs-lookup"><span data-stu-id="d5b6f-175">Summary</span></span>

<span data-ttu-id="d5b6f-176">En este tutorial, hemos recorrido el proceso para crear un microservicio de MicroProfile sencillo, incluirlo en un contenedor de Docker, y lo hemos publicado en Azure y ejecutado localmente.</span><span class="sxs-lookup"><span data-stu-id="d5b6f-176">In this tutorial, you've stepped through the process of creating a simple MicroProfile-based microservice, containerized it into a Docker container, run it locally, and published it to Azure.</span></span> <span data-ttu-id="d5b6f-177">Puede ampliar su microservicio para que ofrezca otras funcionalidades adicionales útiles.</span><span class="sxs-lookup"><span data-stu-id="d5b6f-177">You can extend your microservice to provide additional useful functionality.</span></span> <span data-ttu-id="d5b6f-178">Para más información, vaya a [MicroProfile.io](https://microprofile.io/).</span><span class="sxs-lookup"><span data-stu-id="d5b6f-178">For more information, go to [MicroProfile.io](https://microprofile.io/).</span></span>
