---
title: Configuración de una aplicación de Spring Boot Initializr para usar Azure Redis Cache
description: Configure una aplicación de Spring Boot creada con Spring Initializr para usar Redis en la nube con Azure Redis Cache.
services: redis-cache
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 12/19/2018
ms.devlang: java
ms.service: cache
ms.tgt_pltfrm: cache-redis
ms.topic: article
ms.workload: na
ms.openlocfilehash: 4b720cf4639a12c6dd8cc5040107c1b52de6f642
ms.sourcegitcommit: f0f140b0862ca5338b1b7e5c33cec3e58a70b8fd
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/03/2019
ms.locfileid: "53991409"
---
# <a name="configure-a-spring-boot-initializer-app-to-use-redis-in-the-cloud-with-azure-redis-cache"></a><span data-ttu-id="9a65a-103">Configuración de una aplicación de Spring Boot Initializr para usar Redis en la nube con Azure Redis Cache</span><span class="sxs-lookup"><span data-stu-id="9a65a-103">Configure a Spring Boot Initializer app to use Redis in the cloud with Azure Redis Cache</span></span>

<span data-ttu-id="9a65a-104">Este artículo le ayuda a crear una memoria caché en Redis en la nube mediante Azure Portal, después a utilizar **[Spring Initializr]** para crear una aplicación personalizada y, por último, a crear una aplicación web de Java que almacena y recupera datos mediante la memoria caché en Redis.</span><span class="sxs-lookup"><span data-stu-id="9a65a-104">This article walks you through creating a Redis cache in the cloud using the Azure portal, then using the **[Spring Initializr]** to create a custom application, and then creating a Java web application that stores and retrieves data using your Redis cache.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9a65a-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9a65a-105">Prerequisites</span></span>

<span data-ttu-id="9a65a-106">Los siguientes requisitos previos son necesarios para seguir los pasos descritos en este artículo:</span><span class="sxs-lookup"><span data-stu-id="9a65a-106">The following prerequisites are required in order to complete the steps in this article:</span></span>

* <span data-ttu-id="9a65a-107">Una suscripción de Azure. Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN] o registrarse para obtener una [cuenta de Azure gratuita].</span><span class="sxs-lookup"><span data-stu-id="9a65a-107">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="9a65a-108">Un kit de desarrollo de Java (JDK) admitido</span><span class="sxs-lookup"><span data-stu-id="9a65a-108">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="9a65a-109">Para más información sobre los JDK disponibles para desarrollar en Azure, consulte <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="9a65a-109">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="9a65a-110">[Apache Maven](http://maven.apache.org/), versión 3.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="9a65a-110">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-a-custom-application-using-the-spring-initializr"></a><span data-ttu-id="9a65a-111">Creación de una aplicación personalizada mediante Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="9a65a-111">Create a custom application using the Spring Initializr</span></span>

1. <span data-ttu-id="9a65a-112">Vaya a <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="9a65a-112">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="9a65a-113">Especifique que quiere generar un proyecto de **Maven** con **Java**, escriba los nombres de **Group** (Grupo) y **Artifact** (Artefacto) de su aplicación y luego haga clic en el vínculo **Switch to the full version** (Cambiar a la versión completa) de Spring Initializr.</span><span class="sxs-lookup"><span data-stu-id="9a65a-113">Specify that you want to generate a **Maven** project with **Java**, enter the **Group** and **Aritifact** names for your application, and then click the link to **Switch to the full version** of the Spring Initializr.</span></span>

   ![Opciones básicas de Spring Initializr][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="9a65a-115">Spring Initializr usará los nombres de **Group** (Grupo) y **Artifact** (Artefacto) para crear el nombre del paquete, por ejemplo: *com.contoso.myazuredemo*.</span><span class="sxs-lookup"><span data-stu-id="9a65a-115">The Spring Initializr will use the **Group** and **Aritifact** names to create the package name; for example: *com.contoso.myazuredemo*.</span></span>
   >

1. <span data-ttu-id="9a65a-116">Desplácese hacia abajo hasta la sección **Web** y active la casilla **Web**, luego desplácese hacia abajo hasta la sección **NoSQL** y active la casilla **Redis**, después desplácese hasta la parte inferior de la página y haga clic en el botón **Generate Project** (Generar proyecto).</span><span class="sxs-lookup"><span data-stu-id="9a65a-116">Scroll down to the **Web** section and check the box for **Web**, then scroll down to the **NoSQL** section and check the box for **Redis**, then scroll to the bottom of the page and click the button to **Generate Project**.</span></span>

   ![Opciones completas de Spring Initializr][SI02]

1. <span data-ttu-id="9a65a-118">Cuando se le solicite, descargue el proyecto en una ruta de acceso del equipo local.</span><span class="sxs-lookup"><span data-stu-id="9a65a-118">When prompted, download the project to a path on your local computer.</span></span>

   ![Descarga del proyecto personalizado de Spring Boot][SI03]

1. <span data-ttu-id="9a65a-120">Después de extraer los archivos en el sistema local, la aplicación personalizada de Spring Boot estará lista para editarla.</span><span class="sxs-lookup"><span data-stu-id="9a65a-120">After you have extracted the files on your local system, your custom Spring Boot application will be ready for editing.</span></span>

   ![Archivos de proyecto personalizados de Spring Boot][SI04]

## <a name="create-a-redis-cache-on-azure"></a><span data-ttu-id="9a65a-122">Crear una caché de Redis en Azure</span><span class="sxs-lookup"><span data-stu-id="9a65a-122">Create a Redis cache on Azure</span></span>

1. <span data-ttu-id="9a65a-123">Vaya a Azure Portal en <https://portal.azure.com/> y haga clic en **+Nuevo**.</span><span class="sxs-lookup"><span data-stu-id="9a65a-123">Browse to the Azure portal at <https://portal.azure.com/> and click **+New**.</span></span>

   ![Azure Portal][AZ01]

1. <span data-ttu-id="9a65a-125">Haga clic en **Base de datos** y luego en **Redis Cache**.</span><span class="sxs-lookup"><span data-stu-id="9a65a-125">Click **Database**, and then click **Redis Cache**.</span></span>

   ![Azure Portal][AZ02]

1. <span data-ttu-id="9a65a-127">En la página **Nueva caché en Redis**, especifique la información siguiente:</span><span class="sxs-lookup"><span data-stu-id="9a65a-127">On the **New Redis Cache** page, specify the following information:</span></span>

   * <span data-ttu-id="9a65a-128">Escriba el **Nombre DNS** de su memoria caché.</span><span class="sxs-lookup"><span data-stu-id="9a65a-128">Enter the **DNS name** for your cache.</span></span>
   * <span data-ttu-id="9a65a-129">Especifique la **suscripción**, **Grupo de recursos**, **Ubicación** y **Plan de tarifa**.</span><span class="sxs-lookup"><span data-stu-id="9a65a-129">Specify your **Subscription**, **Resource group**, **Location**, and **Pricing tier**.</span></span>
   * <span data-ttu-id="9a65a-130">Para este tutorial, elija **Desbloquear puerto 6379**.</span><span class="sxs-lookup"><span data-stu-id="9a65a-130">For this tutorial, choose **Unblock port 6379**.</span></span>

   > [!NOTE]
   >
   > <span data-ttu-id="9a65a-131">Puede utilizar SSL con memorias caché de Redis, pero tendría que usar otro cliente Redis como Jedis.</span><span class="sxs-lookup"><span data-stu-id="9a65a-131">You can use SSL with Redis caches, but you would need to use a different Redis client like Jedis.</span></span> <span data-ttu-id="9a65a-132">Para más información, consulte [Uso de Azure Redis Cache con Java][Redis Cache with Java].</span><span class="sxs-lookup"><span data-stu-id="9a65a-132">For more information, see [How to use Azure Redis Cache with Java][Redis Cache with Java].</span></span>
   >

   <span data-ttu-id="9a65a-133">Cuando haya especificado estas opciones, haga clic en **Crear** para crear la memoria caché.</span><span class="sxs-lookup"><span data-stu-id="9a65a-133">When you have specified these options, click **Create** to create your cache.</span></span>

   ![Azure Portal][AZ03]

1. <span data-ttu-id="9a65a-135">Una vez completada la memoria caché, verá que aparece en su **Panel** de Azure, así como en las páginas **Todos los recursos** y **Cachés en Redis**.</span><span class="sxs-lookup"><span data-stu-id="9a65a-135">Once your cache has been completed, you will see it listed on your Azure **Dashboard**, as well as under the **All Resources**, and **Redis Caches** pages.</span></span> <span data-ttu-id="9a65a-136">Puede hacer clic en la memoria caché en cualquiera de esas ubicaciones para abrir la página de propiedades de dicha memoria caché.</span><span class="sxs-lookup"><span data-stu-id="9a65a-136">You can click on your cache on any of those locations to open the properties page for your cache.</span></span>

   ![Azure Portal][AZ04]

1. <span data-ttu-id="9a65a-138">Cuando se muestre la página que contiene la lista de propiedades de la memoria caché, haga clic en **Claves de acceso** y copie las claves de acceso de la memoria caché.</span><span class="sxs-lookup"><span data-stu-id="9a65a-138">When the page that contains the list of properties for your cache is displayed, click **Access keys** and copy your access keys for your cache.</span></span>

   ![Azure Portal][AZ05]

## <a name="configure-your-custom-spring-boot-to-use-your-redis-cache"></a><span data-ttu-id="9a65a-140">Configuración de su Spring Boot personalizada para usar Redis Cache</span><span class="sxs-lookup"><span data-stu-id="9a65a-140">Configure your custom Spring Boot to use your Redis Cache</span></span>

1. <span data-ttu-id="9a65a-141">Busque el archivo *application.properties* en el directorio *resources* de la aplicación, o cree el archivo si todavía no existe.</span><span class="sxs-lookup"><span data-stu-id="9a65a-141">Locate the *application.properties* file in the *resources* directory of your app, or create the file if it does not already exist.</span></span>

   ![Localización del archivo application.properties][RE01]

1. <span data-ttu-id="9a65a-143">Abra el archivo *application.properties* en un editor de texto y agréguele las siguientes líneas; luego, sustituya los valores de ejemplo por las propiedades adecuadas de la memoria caché:</span><span class="sxs-lookup"><span data-stu-id="9a65a-143">Open the *application.properties* file in a text editor, and add the following lines to the file, and replace the sample values with the appropriate properties from your cache:</span></span>

   ```yaml
   # Specify the DNS URI of your Redis cache.
   spring.redis.host=myspringbootcache.redis.cache.windows.net

   # Specify the port for your Redis cache.
   spring.redis.port=6379

   # Specify the access key for your Redis cache.
   spring.redis.password=57686f6120447564652c2049495320526f636b73=
   ```

   ![Edición del archivo application.properties][RE02]

   > [!NOTE] 
   > 
   > <span data-ttu-id="9a65a-145">Si utilizaba un cliente de Redis diferente como Jedis, que habilita SSL, debería especificar que va a utilizar SSL en el archivo *application.properties* y usar el puerto 6380.</span><span class="sxs-lookup"><span data-stu-id="9a65a-145">If you were using a different Redis client like Jedis that enables SSL, you would specify that you want to use SSL in your *application.properties* file and use port 6380.</span></span> <span data-ttu-id="9a65a-146">Por ejemplo: </span><span class="sxs-lookup"><span data-stu-id="9a65a-146">For example:</span></span>
   > 
   > ```yaml
   > # Specify the DNS URI of your Redis cache.
   > spring.redis.host=myspringbootcache.redis.cache.windows.net
   > # Specify the access key for your Redis cache.
   > spring.redis.password=57686f6120447564652c2049495320526f636b73=
   > # Specify that you want to use SSL.
   > spring.redis.ssl=true
   > # Specify the SSL port for your Redis cache.
   > spring.redis.port=6380
   > ```
   > 
   > <span data-ttu-id="9a65a-147">Para más información, consulte [Uso de Azure Redis Cache con Java][Redis Cache with Java].</span><span class="sxs-lookup"><span data-stu-id="9a65a-147">For more information, see [How to use Azure Redis Cache with Java][Redis Cache with Java].</span></span> 
   > 

1. <span data-ttu-id="9a65a-148">Guarde y cierre el archivo *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="9a65a-148">Save and close the *application.properties* file.</span></span>

1. <span data-ttu-id="9a65a-149">Cree una carpeta denominada *controller* en la carpeta de origen para el paquete; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9a65a-149">Create a folder named *controller* under the source folder for your package; for example:</span></span>

   `C:\SpringBoot\myazuredemo\src\main\java\com\contoso\myazuredemo\controller`

   <span data-ttu-id="9a65a-150">O bien</span><span class="sxs-lookup"><span data-stu-id="9a65a-150">-or-</span></span>

   `/users/example/home/myazuredemo/src/main/java/com/contoso/myazuredemo/controller`

1. <span data-ttu-id="9a65a-151">Cree un archivo denominado *HelloController.java* en la carpeta *controller*.</span><span class="sxs-lookup"><span data-stu-id="9a65a-151">Create a new file named *HelloController.java* in the *controller* folder.</span></span> <span data-ttu-id="9a65a-152">Abra el archivo en un editor de texto y agréguele el siguiente código:</span><span class="sxs-lookup"><span data-stu-id="9a65a-152">Open the file in a text editor and add the following code to it:</span></span>

   ```java
   package com.contoso.myazuredemo;

   import org.springframework.web.bind.annotation.RequestMapping;
   import org.springframework.web.bind.annotation.RestController;
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;
   import org.springframework.data.redis.core.StringRedisTemplate;
   import org.springframework.data.redis.core.ValueOperations;

   @RestController
   public class HelloController {
   
      @Autowired
      private StringRedisTemplate template;

      @RequestMapping("/")
      // Define the Hello World controller.
      public String hello() {
      
         ValueOperations<String, String> ops = this.template.opsForValue();

         // Add a Hello World string to your cache.
         String key = "greeting";
         if (!this.template.hasKey(key)) {
             ops.set(key, "Hello World!");
         }

         // Return the string from your cache.
         return ops.get(key);
      }
   }
   ```
   
   <span data-ttu-id="9a65a-153">Necesitará reemplazar `com.contoso.myazuredemo` con el nombre del paquete para el proyecto.</span><span class="sxs-lookup"><span data-stu-id="9a65a-153">Where you will need to replace `com.contoso.myazuredemo` with the package name for your project.</span></span>

1. <span data-ttu-id="9a65a-154">Guarde y cierre el archivo *HelloController.java*.</span><span class="sxs-lookup"><span data-stu-id="9a65a-154">Save and close the *HelloController.java* file.</span></span>

1. <span data-ttu-id="9a65a-155">Compile la aplicación de Spring Boot con Maven y ejecútela; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9a65a-155">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. <span data-ttu-id="9a65a-156">Pruebe la aplicación web. Para ello, vaya a http://localhost:8080 con un explorador web, o bien utilice una sintaxis como la del siguiente ejemplo si tiene cURL disponible:</span><span class="sxs-lookup"><span data-stu-id="9a65a-156">Test the web app by browsing to http://localhost:8080 using a web browser, or use the syntax like the following example if you have curl available:</span></span>

   ```shell
   curl http://localhost:8080
   ```

   <span data-ttu-id="9a65a-157">Debe ver el mensaje "Hola mundo"</span><span class="sxs-lookup"><span data-stu-id="9a65a-157">You should see the "Hello World!"</span></span> <span data-ttu-id="9a65a-158">del controlador de ejemplo mostrado, que se está recuperando dinámicamente de la memoria caché en Redis.</span><span class="sxs-lookup"><span data-stu-id="9a65a-158">message from your sample controller displayed, which is being retrieved dynamically from your Redis cache.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9a65a-159">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9a65a-159">Next steps</span></span>

<span data-ttu-id="9a65a-160">Para más información acerca de Spring y Azure, vaya al centro de documentación de Azure.</span><span class="sxs-lookup"><span data-stu-id="9a65a-160">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9a65a-161">Spring en Azure</span><span class="sxs-lookup"><span data-stu-id="9a65a-161">Spring on Azure</span></span>](/java/azure/spring-framework)

### <a name="additional-resources"></a><span data-ttu-id="9a65a-162">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="9a65a-162">Additional Resources</span></span>

<span data-ttu-id="9a65a-163">Para obtener más información sobre el uso de aplicaciones de Spring Boot en Azure, consulte los siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="9a65a-163">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="9a65a-164">Implementación de una aplicación de Spring Boot en Azure App Service</span><span class="sxs-lookup"><span data-stu-id="9a65a-164">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)

* [<span data-ttu-id="9a65a-165">Ejecución de una aplicación de Spring Boot en un clúster de Kubernetes en Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="9a65a-165">Running a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="9a65a-166">Para más información sobre el uso de Azure con Java, consulte [Azure para desarrolladores de Java] y [Working with Azure DevOps and Java] (Trabajo con Azure DevOps y Java).</span><span class="sxs-lookup"><span data-stu-id="9a65a-166">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Working with Azure DevOps and Java].</span></span>

<span data-ttu-id="9a65a-167">Para más información sobre la introducción al uso de Redis Cache con Java en Azure, consulte [Uso de Azure Redis Cache con Java][Redis Cache with Java].</span><span class="sxs-lookup"><span data-stu-id="9a65a-167">For more information about getting started using Redis Cache with Java on Azure, see [How to use Azure Redis Cache with Java][Redis Cache with Java].</span></span>

<span data-ttu-id="9a65a-168">**[Spring Framework]** es una solución de código abierto que ayuda a los desarrolladores de Java a crear aplicaciones de nivel empresarial.</span><span class="sxs-lookup"><span data-stu-id="9a65a-168">The **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="9a65a-169">Uno de los proyectos más populares que se basa en esa plataforma es [Spring Boot], que proporciona un enfoque simplificado para crear aplicaciones de Java independientes.</span><span class="sxs-lookup"><span data-stu-id="9a65a-169">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="9a65a-170">Para ayudar a los desarrolladores a empezar con Spring Boot, puede encontrar varios paquetes de ejemplo de Spring Boot en <https://github.com/spring-guides/>.</span><span class="sxs-lookup"><span data-stu-id="9a65a-170">To help developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>.</span></span> <span data-ttu-id="9a65a-171">Además de elegir de la lista de proyectos básicos de Spring Boot, el **[Spring Initializr]** ayuda a los desarrolladores en los primeros pasos para crear aplicaciones de Spring Boot personalizadas.</span><span class="sxs-lookup"><span data-stu-id="9a65a-171">In addition to choosing from the list of basic Spring Boot projects, the **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>

<!-- URL List -->

[Azure para desarrolladores de Java]: /java/azure/
[Azure for Java Developers]: /java/azure/
[cuenta de Azure gratuita]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Working with Azure DevOps and Java]: /azure/devops/java/ (Trabajo con Azure DevOps y Java)
[ventajas como suscriptor de MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/
[Redis Cache with Java]: /azure/redis-cache/cache-java-get-started

<!-- IMG List -->

[AZ01]: ./media/configure-spring-boot-initializer-java-app-with-redis-cache/AZ01.png
[AZ02]: ./media/configure-spring-boot-initializer-java-app-with-redis-cache/AZ02.png
[AZ03]: ./media/configure-spring-boot-initializer-java-app-with-redis-cache/AZ03.png
[AZ04]: ./media/configure-spring-boot-initializer-java-app-with-redis-cache/AZ04.png
[AZ05]: ./media/configure-spring-boot-initializer-java-app-with-redis-cache/AZ05.png

[SI01]: ./media/configure-spring-boot-initializer-java-app-with-redis-cache/SI01.png
[SI02]: ./media/configure-spring-boot-initializer-java-app-with-redis-cache/SI02.png
[SI03]: ./media/configure-spring-boot-initializer-java-app-with-redis-cache/SI03.png
[SI04]: ./media/configure-spring-boot-initializer-java-app-with-redis-cache/SI04.png

[RE01]: ./media/configure-spring-boot-initializer-java-app-with-redis-cache/RE01.png
[RE02]: ./media/configure-spring-boot-initializer-java-app-with-redis-cache/RE02.png
