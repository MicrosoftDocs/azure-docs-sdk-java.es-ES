---
title: "Configuración de una aplicación Spring Boot Initializer para usar Redis Cache"
description: "Aprenda a configurar una aplicación de Spring Boot creada con Spring Initializr para usar Azure Redis Cache."
services: redis-cache
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
keywords: Spring, Spring Boot, Spring Framework, Spring Starter, Redis Cache
ms.assetid: 
ms.service: cache
ms.workload: na
ms.tgt_pltfrm: cache-redis
ms.devlang: java
ms.topic: article
ms.date: 11/01/2017
ms.author: robmcm;zhijzhao;yidon
ms.openlocfilehash: c5e9a9214762e014e463dd3277671fc56237d4a0
ms.sourcegitcommit: 613c1ffd2e0279fc7a96fca98aa1809563f52ee1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="how-to-configure-a-spring-boot-initializer-app-to-use-redis-cache"></a><span data-ttu-id="64fb2-104">Configuración de una aplicación Spring Boot Initializer para usar Redis Cache</span><span class="sxs-lookup"><span data-stu-id="64fb2-104">How to configure a Spring Boot Initializer app to use Redis Cache</span></span>

## <a name="overview"></a><span data-ttu-id="64fb2-105">Información general</span><span class="sxs-lookup"><span data-stu-id="64fb2-105">Overview</span></span>

<span data-ttu-id="64fb2-106">**[Spring Framework]** es una solución de código abierto que ayuda a los desarrolladores de Java a crear aplicaciones de nivel empresarial.</span><span class="sxs-lookup"><span data-stu-id="64fb2-106">The **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="64fb2-107">Uno de los proyectos más populares que se basa en esa plataforma es [Spring Boot], que proporciona un enfoque simplificado para crear aplicaciones de Java independientes.</span><span class="sxs-lookup"><span data-stu-id="64fb2-107">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="64fb2-108">Para ayudar a los desarrolladores a empezar con Spring Boot, puede encontrar varios paquetes de ejemplo de Spring Boot en <https://github.com/spring-guides/>.</span><span class="sxs-lookup"><span data-stu-id="64fb2-108">To help developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>.</span></span> <span data-ttu-id="64fb2-109">Además de elegir de la lista de proyectos básicos de Spring Boot, el **[Spring Initializr]** ayuda a los desarrolladores en los primeros pasos para crear aplicaciones de Spring Boot personalizadas.</span><span class="sxs-lookup"><span data-stu-id="64fb2-109">In addition to choosing from the list of basic Spring Boot projects, the **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>

<span data-ttu-id="64fb2-110">Este artículo le ayuda a crear una memoria caché en Redis mediante Azure Portal, después a utilizar **Spring Initializr** para crear una aplicación personalizada y, por último, a crear una aplicación web de Java que almacena y recupera datos mediante la memoria caché de Redis.</span><span class="sxs-lookup"><span data-stu-id="64fb2-110">This article walks you through creating a Redis cache using the Azure portal, then using the **Spring Initializr** to create a custom application, and then creating a Java web application that stores and retrieves data using your Redis cache.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="64fb2-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="64fb2-111">Prerequisites</span></span>

<span data-ttu-id="64fb2-112">Los siguientes requisitos previos son necesarios para seguir los pasos descritos en este artículo:</span><span class="sxs-lookup"><span data-stu-id="64fb2-112">The following prerequisites are required in order to follow the steps in this article:</span></span>

* <span data-ttu-id="64fb2-113">Una suscripción de Azure. Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN] o registrarse para obtener una [cuenta de Azure gratuita].</span><span class="sxs-lookup"><span data-stu-id="64fb2-113">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>

* <span data-ttu-id="64fb2-114">Un [kit de desarrollo de Java (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), versión 1.7 o posterior.</span><span class="sxs-lookup"><span data-stu-id="64fb2-114">A [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 or later.</span></span>

* <span data-ttu-id="64fb2-115">[Apache Maven](http://maven.apache.org/), versión 3.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="64fb2-115">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-a-redis-cache-on-azure"></a><span data-ttu-id="64fb2-116">Crear una caché de Redis en Azure</span><span class="sxs-lookup"><span data-stu-id="64fb2-116">Create a Redis cache on Azure</span></span>

1. <span data-ttu-id="64fb2-117">Vaya a Azure Portal en <https://portal.azure.com/> y haga clic en el elemento **+Nuevo**.</span><span class="sxs-lookup"><span data-stu-id="64fb2-117">Browse to the Azure portal at <https://portal.azure.com/> and click the item for **+New**.</span></span>

   ![Portal de Azure][AZ01]

1. <span data-ttu-id="64fb2-119">Haga clic en **Base de datos** y luego en **Redis Cache**.</span><span class="sxs-lookup"><span data-stu-id="64fb2-119">Click **Database**, and then click **Redis Cache**.</span></span>

   ![Azure Portal][AZ02]

1. <span data-ttu-id="64fb2-121">En la página **Nueva caché en Redis**, especifique la información siguiente:</span><span class="sxs-lookup"><span data-stu-id="64fb2-121">On the **New Redis Cache** page, specify the following information:</span></span>

   * <span data-ttu-id="64fb2-122">Escriba el **Nombre DNS** de su memoria caché.</span><span class="sxs-lookup"><span data-stu-id="64fb2-122">Enter the **DNS name** for your cache.</span></span>
   * <span data-ttu-id="64fb2-123">Especifique la **suscripción**, **Grupo de recursos**, **Ubicación** y **Plan de tarifa**.</span><span class="sxs-lookup"><span data-stu-id="64fb2-123">Specify your **Subscription**, **Resource group**, **Location**, and **Pricing tier**.</span></span>
   * <span data-ttu-id="64fb2-124">Para este tutorial, elija **Desbloquear puerto 6379**.</span><span class="sxs-lookup"><span data-stu-id="64fb2-124">For this tutorial, choose **Unblock port 6379**.</span></span>

   > [!NOTE]
   >
   > <span data-ttu-id="64fb2-125">Puede utilizar SSL con memorias caché de Redis, pero tendría que usar otro cliente Redis como Jedis.</span><span class="sxs-lookup"><span data-stu-id="64fb2-125">You can use SSL with Redis caches, but you would need to use a different Redis client like Jedis.</span></span> <span data-ttu-id="64fb2-126">Para más información, consulte [Uso de Azure Redis Cache con Java][Redis Cache with Java].</span><span class="sxs-lookup"><span data-stu-id="64fb2-126">For more information, see [How to use Azure Redis Cache with Java][Redis Cache with Java].</span></span>
   >

   <span data-ttu-id="64fb2-127">Cuando haya especificado estas opciones, haga clic en **Crear** para crear la memoria caché.</span><span class="sxs-lookup"><span data-stu-id="64fb2-127">When you have specified these options, click **Create** to create your cache.</span></span>

   ![Azure Portal][AZ03]

1. <span data-ttu-id="64fb2-129">Una vez completada la memoria caché, verá que aparece en su **Panel** de Azure, así como en las páginas **Todos los recursos** y **Cachés en Redis**.</span><span class="sxs-lookup"><span data-stu-id="64fb2-129">Once your cache has been completed, you will see it listed on your Azure **Dashboard**, as well as under the **All Resources**, and **Redis Caches** pages.</span></span> <span data-ttu-id="64fb2-130">Puede hacer clic en la memoria caché en cualquiera de esas ubicaciones para abrir la página de propiedades de dicha memoria caché.</span><span class="sxs-lookup"><span data-stu-id="64fb2-130">You can click on your cache on any of those locations to open the properties page for your cache.</span></span>

   ![Azure Portal][AZ04]

1. <span data-ttu-id="64fb2-132">Cuando se muestre la página que contiene la lista de propiedades de la memoria caché, haga clic en **Claves de acceso** y copie las claves de acceso de la memoria caché.</span><span class="sxs-lookup"><span data-stu-id="64fb2-132">When the page that contains the list of properties for your cache is displayed, click **Access keys** and copy your access keys for your cache.</span></span>

   ![Azure Portal][AZ05]

## <a name="create-a-custom-application-using-the-spring-initializr"></a><span data-ttu-id="64fb2-134">Creación de una aplicación personalizada mediante Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="64fb2-134">Create a custom application using the Spring Initializr</span></span>

1. <span data-ttu-id="64fb2-135">Vaya a <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="64fb2-135">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="64fb2-136">Especifique que quiere generar un proyecto de **Maven** con **Java**, escriba los nombres de **Group** (Grupo) y **Artifact** (Artefacto) de su aplicación y luego haga clic en el vínculo **Switch to the full version** (Cambiar a la versión completa) de Spring Initializr.</span><span class="sxs-lookup"><span data-stu-id="64fb2-136">Specify that you want to generate a **Maven** project with **Java**, enter the **Group** and **Aritifact** names for your application, and then click the link to **Switch to the full version** of the Spring Initializr.</span></span>

   ![Opciones básicas de Spring Initializr][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="64fb2-138">Spring Initializr usará los nombres de **Group** (Grupo) y **Artifact** (Artefacto) para crear el nombre del paquete, por ejemplo: *com.contoso.myazuredemo*.</span><span class="sxs-lookup"><span data-stu-id="64fb2-138">The Spring Initializr will use the **Group** and **Aritifact** names to create the package name; for example: *com.contoso.myazuredemo*.</span></span>
   >

1. <span data-ttu-id="64fb2-139">Desplácese hacia abajo hasta la sección **Web** y active la casilla **Web**, luego desplácese hacia abajo hasta la sección **NoSQL** y active la casilla **Redis**, después desplácese hasta la parte inferior de la página y haga clic en el botón **Generate Project** (Generar proyecto).</span><span class="sxs-lookup"><span data-stu-id="64fb2-139">Scroll down to the **Web** section and check the box for **Web**, then scroll down to the **NoSQL** section and check the box for **Redis**, then scroll to the bottom of the page and click the button to **Generate Project**.</span></span>

   ![Opciones completas de Spring Initializr][SI02]

1. <span data-ttu-id="64fb2-141">Cuando se le solicite, descargue el proyecto en una ruta de acceso del equipo local.</span><span class="sxs-lookup"><span data-stu-id="64fb2-141">When prompted, download the project to a path on your local computer.</span></span>

   ![Descarga del proyecto personalizado de Spring Boot][SI03]

1. <span data-ttu-id="64fb2-143">Después de extraer los archivos en el sistema local, la aplicación personalizada de Spring Boot estará lista para editarla.</span><span class="sxs-lookup"><span data-stu-id="64fb2-143">After you have extracted the files on your local system, your custom Spring Boot application will be ready for editing.</span></span>

   ![Archivos de proyecto personalizados de Spring Boot][SI04]

## <a name="configure-your-custom-spring-boot-to-use-your-redis-cache"></a><span data-ttu-id="64fb2-145">Configuración de su Spring Boot personalizada para usar Redis Cache</span><span class="sxs-lookup"><span data-stu-id="64fb2-145">Configure your custom Spring Boot to use your Redis Cache</span></span>

1. <span data-ttu-id="64fb2-146">Busque el archivo *application.properties* en el directorio *resources* de la aplicación, o cree el archivo si todavía no existe.</span><span class="sxs-lookup"><span data-stu-id="64fb2-146">Locate the *application.properties* file in the *resources* directory of your app, or create the file if it does not already exist.</span></span>

   ![Localización del archivo application.properties][RE01]

1. <span data-ttu-id="64fb2-148">Abra el archivo *application.properties* en un editor de texto y agréguele las siguientes líneas; luego, sustituya los valores de ejemplo por las propiedades adecuadas de la memoria caché:</span><span class="sxs-lookup"><span data-stu-id="64fb2-148">Open the *application.properties* file in a text editor, and add the following lines to the file, and replace the sample values with the appropriate properties from your cache:</span></span>

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
   > <span data-ttu-id="64fb2-150">Si utilizaba un cliente de Redis diferente como Jedis, que habilita SSL, debería especificar el puerto 6380 en el archivo *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="64fb2-150">If you were using a different Redis client like Jedis that enables SSL, you would specify port 6380 in your *application.properties* file.</span></span> <span data-ttu-id="64fb2-151">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="64fb2-151">For example:</span></span>
   > 
   > ```yaml
   > spring.redis.host=myspringbootcache.redis.cache.windows.net
   > spring.redis.password=57686f6120447564652c2049495320526f636b73=
   > spring.redis.ssl=true
   > spring.redis.port=6380
   > ```
   > 
   > <span data-ttu-id="64fb2-152">Para más información, consulte [Uso de Azure Redis Cache con Java][Redis Cache with Java].</span><span class="sxs-lookup"><span data-stu-id="64fb2-152">For more information, see [How to use Azure Redis Cache with Java][Redis Cache with Java].</span></span> 
   > 

1. <span data-ttu-id="64fb2-153">Guarde y cierre el archivo *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="64fb2-153">Save and close the *application.properties* file.</span></span>

1. <span data-ttu-id="64fb2-154">Cree una carpeta denominada *controller* en la carpeta de origen para el paquete; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="64fb2-154">Create a folder named *controller* under the source folder for your package; for example:</span></span>

   `C:\SpringBoot\myazuredemo\src\main\java\com\contoso\myazuredemo\controller`

   <span data-ttu-id="64fb2-155">O bien</span><span class="sxs-lookup"><span data-stu-id="64fb2-155">-or-</span></span>

   `/users/example/home/myazuredemo/src/main/java/com/contoso/myazuredemo/controller`

1. <span data-ttu-id="64fb2-156">Cree un archivo denominado *HelloController.java* en la carpeta *controller*.</span><span class="sxs-lookup"><span data-stu-id="64fb2-156">Create a new file named *HelloController.java* in the *controller* folder.</span></span> <span data-ttu-id="64fb2-157">Abra el archivo en un editor de texto y agréguele el siguiente código:</span><span class="sxs-lookup"><span data-stu-id="64fb2-157">Open the file in a text editor and add the following code to it:</span></span>

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
   
   <span data-ttu-id="64fb2-158">Necesitará reemplazar `com.contoso.myazuredemo` con el nombre del paquete para el proyecto.</span><span class="sxs-lookup"><span data-stu-id="64fb2-158">Where you will need to replace `com.contoso.myazuredemo` with the package name for your project.</span></span>

1. <span data-ttu-id="64fb2-159">Guarde y cierre el archivo *HelloController.java*.</span><span class="sxs-lookup"><span data-stu-id="64fb2-159">Save and close the *HelloController.java* file.</span></span>

1. <span data-ttu-id="64fb2-160">Compile la aplicación de Spring Boot con Maven y ejecútela; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="64fb2-160">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. <span data-ttu-id="64fb2-161">Compruebe la aplicación web. Para ello, vaya a http://localhost:8080 con un explorador web, o bien utilice una sintaxis como la del siguiente ejemplo si tiene cURL disponible:</span><span class="sxs-lookup"><span data-stu-id="64fb2-161">Test the web app by browsing to http://localhost:8080 using a web browser, or use the syntax like the following example if you have curl available:</span></span>

   ```shell
   curl http://localhost:8080
   ```

   <span data-ttu-id="64fb2-162">Debe ver el mensaje "Hola mundo"</span><span class="sxs-lookup"><span data-stu-id="64fb2-162">You should see the "Hello World!"</span></span> <span data-ttu-id="64fb2-163">del controlador de ejemplo mostrado, que se está recuperando dinámicamente de la memoria caché en Redis.</span><span class="sxs-lookup"><span data-stu-id="64fb2-163">message from your sample controller displayed, which is being retrieved dynamically from your Redis cache.</span></span>

## <a name="next-steps"></a><span data-ttu-id="64fb2-164">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="64fb2-164">Next steps</span></span>

<span data-ttu-id="64fb2-165">Para obtener más información sobre el uso de aplicaciones de Spring Boot en Azure, consulte los siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="64fb2-165">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="64fb2-166">Implementación de una aplicación de Spring Boot en Azure App Service</span><span class="sxs-lookup"><span data-stu-id="64fb2-166">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)

* [<span data-ttu-id="64fb2-167">Ejecución de una aplicación de Spring Boot en un clúster de Kubernetes en Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="64fb2-167">Running a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="64fb2-168">Para obtener más información sobre el uso de Azure con Java, vea el [Centro para desarrolladores de Java de Azure] y [Java Tools for Visual Studio Team Services] (Herramientas de Java para Visual Studio Team Services).</span><span class="sxs-lookup"><span data-stu-id="64fb2-168">For more information about using Azure with Java, see the [Azure Java Developer Center] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="64fb2-169">Para más información sobre la introducción al uso de Redis Cache con Java en Azure, consulte [Uso de Azure Redis Cache con Java][Redis Cache with Java].</span><span class="sxs-lookup"><span data-stu-id="64fb2-169">For more information about getting started using Redis Cache with Java on Azure, see [How to use Azure Redis Cache with Java][Redis Cache with Java].</span></span>

<!-- URL List -->

[Centro para desarrolladores de Java de Azure]: https://azure.microsoft.com/develop/java/
[cuenta de Azure gratuita]: https://azure.microsoft.com/pricing/free-trial/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[ventajas como suscriptor de MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
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
