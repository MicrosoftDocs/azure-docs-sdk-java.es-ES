---
title: "Implementación de una aplicación de Spring Boot en Azure App Service"
description: "Este tutorial guiará a los desarrolladores a través de los pasos necesarios para implementar una aplicación web inicial de Spring Boot en Azure App Service."
services: app-service
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
keywords: Spring, Spring Boot, Spring Framework
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: java
ms.topic: article
ms.date: 10/11/2017
ms.author: asirveda;robmcm
ms.openlocfilehash: 5a0f13e1883c1de1adb72c450c55dcb38b1520b9
ms.sourcegitcommit: 7f8538e41c833deb69c300ad3431a431136a1f3e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/24/2017
---
# <a name="deploy-a-spring-boot-application-to-the-azure-app-service"></a>Implementación de una aplicación de Spring Boot en Azure App Service

**[Spring Framework]** es una solución de código abierto que ayuda a los desarrolladores de Java a crear aplicaciones a nivel empresarial. Uno de los proyectos más populares basados en esta plataforma es [Spring Boot], que ofrece un método simplificado para crear aplicaciones Java independientes.

Este tutorial le guiará a través de la creación de una aplicación web inicial de Spring Boot y su implementación en [Azure App Service].

### <a name="prerequisites"></a>Requisitos previos

Para poder realizar los pasos de este tutorial, necesitará tener lo siguiente:

* Una suscripción de Azure. Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN] o registrarse para obtener una [cuenta de Azure gratuita].
* Un [kit para desarrolladores de Java (JDK)] actualizado.
* La herramienta de compilación [Maven] de Apache (versión 3).
* Un cliente [Git].

## <a name="create-the-spring-boot-getting-started-web-app"></a>Creación de la aplicación web inicial de Spring Boot

Los siguientes pasos le guiarán por las fases necesarias para crear una aplicación web de Spring Boot sencilla y probarla de forma local.

1. Abra el símbolo del sistema, cree un directorio local para alojar la aplicación y cambie a dicho directorio, por ejemplo:
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   -- o --
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. Clone el proyecto de ejemplo [inicial de Spring Boot] en el directorio recién creado, por ejemplo:
   ```
   git clone https://github.com/spring-guides/gs-spring-boot.git
   ```

1. Cambie de directorio al del proyecto finalizado, por ejemplo:
   ```
   cd gs-spring-boot
   cd complete
   ```

1. Compile el archivo JAR con Maven, por ejemplo:
   ```
   mvn package
   ```

1. Una vez creada la aplicación web, cambie el directorio al del archivo JAR e inicie la aplicación web, por ejemplo:
   ```
   cd target
   java -jar gs-spring-boot-0.1.0.jar
   ```

1. Compruebe la aplicación web. Para ello, vaya a http://localhost:8080 con un explorador web, o bien utilice una sintaxis como la del siguiente ejemplo si tiene cURL disponible:
   ```
   curl http://localhost:8080
   ```

1. Debería aparecer el siguiente mensaje: **Greetings from Spring Boot!** (Saludos de Spring Boot).

   ![Buscar aplicación de ejemplo][SB01]

## <a name="create-an-azure-web-app-for-use-with-java"></a>Creación de una aplicación web de Azure para usarla con Java

Los siguientes pasos le guiarán por las diferentes fases de creación de una aplicación web de Azure, de ajuste de la configuración necesaria para Java y de configuración de las credenciales de FTP.

1. Vaya a [Azure Portal] e inicie sesión.

1. Una vez que haya iniciado sesión en la cuenta de Azure Portal, haga clic en el icono de menú de **App Services**:
   
   ![Portal de Azure][AZ01]

1. Cuando aparezca la página **App Services**, haga clic en **+ Agregar** para crear un nuevo elemento de App Service.

   ![Creación de un elemento App Service][AZ02]

1. Cuando aparezca la lista de plantillas de aplicaciones web, haga clic en el vínculo de la aplicación web básica de Microsoft.

   ![Plantillas de aplicaciones web][AZ03]

1. Cuando aparezca la página de información de plantillas de aplicaciones web, haga clic en **Crear**.

   ![Crear aplicación web][AZ04]

1. Proporcione un nombre único para la aplicación web y especifique cualquier configuración adicional. A continuación, seleccione **Crear**.

   ![Creación de configuración de aplicaciones web][AZ05]

1. Una vez creada la aplicación web, haga clic en el icono de menú de **App Services** y, a continuación, haga clic en la aplicación web recién creada:

   ![Lista de aplicaciones web][AZ06]

1. Cuando aparezca la aplicación web, especifique la versión de Java. Para ello, siga los siguientes pasos:

   a. Haga clic en el elemento de menú **Configuración de la aplicación**.

   b. Seleccione **Java 8** como versión de Java.

   c. Seleccione **Más reciente** como versión secundaria de Java.

   d. Seleccione **Newest Tomcat 8.5** como contenedor web. (Este contenedor en realidad no se usará. Azure usará el contenedor de la aplicación de Spring Boot).

   e. Haga clic en **Guardar**.

   ![Configuración de la aplicación][AZ07]

1. Especifique las credenciales de implementación de FTP. Para ello, siga los siguientes pasos:

   a. Haga clic en el elemento de menú **Credenciales de implementación**.

   b. Especifique el nombre de usuario y la contraseña.

   c. Haga clic en **Guardar**.

   ![Especificación de credenciales de implementación][AZ08]

1. Recupere la información de conexión del FTP. Para ello, siga los siguientes pasos:

   a. Haga clic en el elemento de menú **Credenciales de implementación**.

   b. Copie el nombre de usuario y la URL del FTP completos, y guárdelos para la siguiente sección del tutorial.

   ![URL y credenciales de FTP][AZ09]

## <a name="deploy-your-spring-boot-web-app-to-azure"></a>Implementación de la aplicación web de Spring Boot en Azure

Los siguientes pasos le guiarán por las fases necesarias para implementar la aplicación web de Spring Boot en Azure.

1. Abra un editor de texto, como el Bloc de notas de Windows, y pegue el siguiente texto en un nuevo documento. A continuación, guarde el archivo como *web.config*:
   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <configuration>
     <system.webServer>
       <handlers>
         <add name="httpPlatformHandler" path="*" verb="*" modules="httpPlatformHandler" resourceType="Unspecified" />
       </handlers>
       <httpPlatform processPath="%JAVA_HOME%\bin\java.exe"
           arguments="-Djava.net.preferIPv4Stack=true -Dserver.port=%HTTP_PLATFORM_PORT% -jar &quot;%HOME%\site\wwwroot\gs-spring-boot-0.1.0.jar&quot;">
       </httpPlatform>
     </system.webServer>
   </configuration>
   ```

1. Después de guardar el archivo *web.config* en el sistema, conéctese a la aplicación web a través de FTP con la URL, el nombre de usuario y la contraseña de la sección anterior de este tutorial. Por ejemplo:
   ```
   ftp
   open waws-prod-sn0-000.ftp.azurewebsites.windows.net
   user wingtiptoys-springboot\wingtiptoysuser
   pass ********
   ```

1. Cambie el directorio remoto a la carpeta raíz de la aplicación web (que se encuentra en */sitio/wwwRaíz*) y, a continuación, copie el archivo JAR de la aplicación de Spring Boot y el archivo *web.config* anterior. Por ejemplo:
   ```
   cd site/wwwroot
   put gs-spring-boot-0.1.0.jar
   put web.config
   ```

1. Una vez implementados los archivos JAR y *web.config* en la aplicación web, debe reiniciar esta con Azure Portal:

   ![][AZ10]

1. Compruebe la aplicación web. Para ello, acceda a la URL de la aplicación con un explorador web, o bien utilice una sintaxis como la del siguiente ejemplo si tiene cURL disponible:
   ```
   curl http://wingtiptoys-springboot.azurewebsites.net/
   ```

1. Debería aparecer el siguiente mensaje: **Greetings from Spring Boot!** (Saludos de Spring Boot).

   ![Buscar aplicación de ejemplo][SB02]

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre el uso de aplicaciones de Spring Boot en Azure, consulte los siguientes artículos:

* [Implementación de una aplicación de Spring Boot en Linux en Azure Container Service](deploy-spring-boot-java-app-on-linux.md)

* [Implementación de una aplicación de Spring Boot en un clúster de Kubernetes en Azure Container Service](deploy-spring-boot-java-app-on-kubernetes.md)

Para obtener más información sobre el uso de Azure con Java, vea el [Centro para desarrolladores de Java de Azure] y [Java Tools for Visual Studio Team Services] (Herramientas de Java para Visual Studio Team Services).

Para obtener más información sobre la implementación de aplicaciones web en Azure mediante FTP, consulte [Implementación de la aplicación en Azure App Service mediante FTP/S].

Para obtener más información sobre el proyecto de ejemplo de Spring Boot, consulte [inicial de Spring Boot].

Para obtener ayuda para dar sus primeros pasos con sus propias aplicaciones de Spring Boot, consulte **Spring Initializr** en https://start.spring.io/.

Para obtener más información sobre configuración de valores adicionales para la aplicación web, consulte [Configuración de aplicaciones web en Azure App Service].

<!-- URL List -->

[Azure App Service]: https://azure.microsoft.com/services/app-service/
[Azure Container Service]: https://azure.microsoft.com/services/container-service/
[Centro para desarrolladores de Java de Azure]: https://azure.microsoft.com/develop/java/
[Azure Portal]: https://portal.azure.com/
[Configuración de aplicaciones web en Azure App Service]: /azure/app-service/web-sites-configure
[Implementación de la aplicación en Azure App Service mediante FTP/S]: https://docs.microsoft.com/azure/app-service/app-service-deploy-ftp
[cuenta de Azure gratuita]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[kit para desarrolladores de Java (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[ventajas como suscriptor de MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[inicial de Spring Boot]: https://github.com/spring-guides/gs-spring-boot
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[SB01]: ./media/deploy-spring-boot-java-web-app-on-azure/SB01.png
[SB02]: ./media/deploy-spring-boot-java-web-app-on-azure/SB02.png

[AZ01]: ./media/deploy-spring-boot-java-web-app-on-azure/AZ01.png
[AZ02]: ./media/deploy-spring-boot-java-web-app-on-azure/AZ02.png
[AZ03]: ./media/deploy-spring-boot-java-web-app-on-azure/AZ03.png
[AZ04]: ./media/deploy-spring-boot-java-web-app-on-azure/AZ04.png
[AZ05]: ./media/deploy-spring-boot-java-web-app-on-azure/AZ05.png
[AZ06]: ./media/deploy-spring-boot-java-web-app-on-azure/AZ06.png
[AZ07]: ./media/deploy-spring-boot-java-web-app-on-azure/AZ07.png
[AZ08]: ./media/deploy-spring-boot-java-web-app-on-azure/AZ08.png
[AZ09]: ./media/deploy-spring-boot-java-web-app-on-azure/AZ09.png
[AZ10]: ./media/deploy-spring-boot-java-web-app-on-azure/AZ10.png
