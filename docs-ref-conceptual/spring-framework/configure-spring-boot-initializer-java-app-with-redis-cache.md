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
# <a name="how-to-configure-a-spring-boot-initializer-app-to-use-redis-cache"></a>Configuración de una aplicación Spring Boot Initializer para usar Redis Cache

## <a name="overview"></a>Información general

**[Spring Framework]** es una solución de código abierto que ayuda a los desarrolladores de Java a crear aplicaciones de nivel empresarial. Uno de los proyectos más populares que se basa en esa plataforma es [Spring Boot], que proporciona un enfoque simplificado para crear aplicaciones de Java independientes. Para ayudar a los desarrolladores a empezar con Spring Boot, puede encontrar varios paquetes de ejemplo de Spring Boot en <https://github.com/spring-guides/>. Además de elegir de la lista de proyectos básicos de Spring Boot, el **[Spring Initializr]** ayuda a los desarrolladores en los primeros pasos para crear aplicaciones de Spring Boot personalizadas.

Este artículo le ayuda a crear una memoria caché en Redis mediante Azure Portal, después a utilizar **Spring Initializr** para crear una aplicación personalizada y, por último, a crear una aplicación web de Java que almacena y recupera datos mediante la memoria caché de Redis.

## <a name="prerequisites"></a>Requisitos previos

Los siguientes requisitos previos son necesarios para seguir los pasos descritos en este artículo:

* Una suscripción de Azure. Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN] o registrarse para obtener una [cuenta de Azure gratuita].

* Un [kit de desarrollo de Java (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), versión 1.7 o posterior.

* [Apache Maven](http://maven.apache.org/), versión 3.0 o posterior.

## <a name="create-a-redis-cache-on-azure"></a>Crear una caché de Redis en Azure

1. Vaya a Azure Portal en <https://portal.azure.com/> y haga clic en el elemento **+Nuevo**.

   ![Portal de Azure][AZ01]

1. Haga clic en **Base de datos** y luego en **Redis Cache**.

   ![Azure Portal][AZ02]

1. En la página **Nueva caché en Redis**, especifique la información siguiente:

   * Escriba el **Nombre DNS** de su memoria caché.
   * Especifique la **suscripción**, **Grupo de recursos**, **Ubicación** y **Plan de tarifa**.
   * Para este tutorial, elija **Desbloquear puerto 6379**.

   > [!NOTE]
   >
   > Puede utilizar SSL con memorias caché de Redis, pero tendría que usar otro cliente Redis como Jedis. Para más información, consulte [Uso de Azure Redis Cache con Java][Redis Cache with Java].
   >

   Cuando haya especificado estas opciones, haga clic en **Crear** para crear la memoria caché.

   ![Azure Portal][AZ03]

1. Una vez completada la memoria caché, verá que aparece en su **Panel** de Azure, así como en las páginas **Todos los recursos** y **Cachés en Redis**. Puede hacer clic en la memoria caché en cualquiera de esas ubicaciones para abrir la página de propiedades de dicha memoria caché.

   ![Azure Portal][AZ04]

1. Cuando se muestre la página que contiene la lista de propiedades de la memoria caché, haga clic en **Claves de acceso** y copie las claves de acceso de la memoria caché.

   ![Azure Portal][AZ05]

## <a name="create-a-custom-application-using-the-spring-initializr"></a>Creación de una aplicación personalizada mediante Spring Initializr

1. Vaya a <https://start.spring.io/>.

1. Especifique que quiere generar un proyecto de **Maven** con **Java**, escriba los nombres de **Group** (Grupo) y **Artifact** (Artefacto) de su aplicación y luego haga clic en el vínculo **Switch to the full version** (Cambiar a la versión completa) de Spring Initializr.

   ![Opciones básicas de Spring Initializr][SI01]

   > [!NOTE]
   >
   > Spring Initializr usará los nombres de **Group** (Grupo) y **Artifact** (Artefacto) para crear el nombre del paquete, por ejemplo: *com.contoso.myazuredemo*.
   >

1. Desplácese hacia abajo hasta la sección **Web** y active la casilla **Web**, luego desplácese hacia abajo hasta la sección **NoSQL** y active la casilla **Redis**, después desplácese hasta la parte inferior de la página y haga clic en el botón **Generate Project** (Generar proyecto).

   ![Opciones completas de Spring Initializr][SI02]

1. Cuando se le solicite, descargue el proyecto en una ruta de acceso del equipo local.

   ![Descarga del proyecto personalizado de Spring Boot][SI03]

1. Después de extraer los archivos en el sistema local, la aplicación personalizada de Spring Boot estará lista para editarla.

   ![Archivos de proyecto personalizados de Spring Boot][SI04]

## <a name="configure-your-custom-spring-boot-to-use-your-redis-cache"></a>Configuración de su Spring Boot personalizada para usar Redis Cache

1. Busque el archivo *application.properties* en el directorio *resources* de la aplicación, o cree el archivo si todavía no existe.

   ![Localización del archivo application.properties][RE01]

1. Abra el archivo *application.properties* en un editor de texto y agréguele las siguientes líneas; luego, sustituya los valores de ejemplo por las propiedades adecuadas de la memoria caché:

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
   > Si utilizaba un cliente de Redis diferente como Jedis, que habilita SSL, debería especificar el puerto 6380 en el archivo *application.properties*. Por ejemplo:
   > 
   > ```yaml
   > spring.redis.host=myspringbootcache.redis.cache.windows.net
   > spring.redis.password=57686f6120447564652c2049495320526f636b73=
   > spring.redis.ssl=true
   > spring.redis.port=6380
   > ```
   > 
   > Para más información, consulte [Uso de Azure Redis Cache con Java][Redis Cache with Java]. 
   > 

1. Guarde y cierre el archivo *application.properties*.

1. Cree una carpeta denominada *controller* en la carpeta de origen para el paquete; por ejemplo:

   `C:\SpringBoot\myazuredemo\src\main\java\com\contoso\myazuredemo\controller`

   O bien

   `/users/example/home/myazuredemo/src/main/java/com/contoso/myazuredemo/controller`

1. Cree un archivo denominado *HelloController.java* en la carpeta *controller*. Abra el archivo en un editor de texto y agréguele el siguiente código:

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
   
   Necesitará reemplazar `com.contoso.myazuredemo` con el nombre del paquete para el proyecto.

1. Guarde y cierre el archivo *HelloController.java*.

1. Compile la aplicación de Spring Boot con Maven y ejecútela; por ejemplo:

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. Compruebe la aplicación web. Para ello, vaya a http://localhost:8080 con un explorador web, o bien utilice una sintaxis como la del siguiente ejemplo si tiene cURL disponible:

   ```shell
   curl http://localhost:8080
   ```

   Debe ver el mensaje "Hola mundo" del controlador de ejemplo mostrado, que se está recuperando dinámicamente de la memoria caché en Redis.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre el uso de aplicaciones de Spring Boot en Azure, consulte los siguientes artículos:

* [Implementación de una aplicación de Spring Boot en Azure App Service](deploy-spring-boot-java-web-app-on-azure.md)

* [Ejecución de una aplicación de Spring Boot en un clúster de Kubernetes en Azure Container Service](deploy-spring-boot-java-app-on-kubernetes.md)

Para obtener más información sobre el uso de Azure con Java, vea el [Centro para desarrolladores de Java de Azure] y [Java Tools for Visual Studio Team Services] (Herramientas de Java para Visual Studio Team Services).

Para más información sobre la introducción al uso de Redis Cache con Java en Azure, consulte [Uso de Azure Redis Cache con Java][Redis Cache with Java].

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
