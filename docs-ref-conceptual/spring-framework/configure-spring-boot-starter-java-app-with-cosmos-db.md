---
title: Uso de la utilidad Spring Boot Starter con SQL API de Azure Cosmos DB
description: Aprenda a configurar una aplicación creada con Spring Boot Initializer con SQL API de Azure Cosmos DB.
services: cosmos-db
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 12/19/2018
ms.devlang: java
ms.service: cosmos-db
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: data-services
ms.openlocfilehash: 1d3ae6c12f32a3443f2783d0c88112746197f5be
ms.sourcegitcommit: f0f140b0862ca5338b1b7e5c33cec3e58a70b8fd
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/03/2019
ms.locfileid: "53991549"
---
# <a name="how-to-use-the-spring-boot-starter-with-the-azure-cosmos-db-sql-api"></a>Uso de la utilidad Spring Boot Starter con SQL API de Azure Cosmos DB

## <a name="overview"></a>Información general

Azure Cosmos DB es un servicio de base de datos de distribución global que permite a los desarrolladores trabajar con datos mediante diversas API estándar, como SQL, MongoDB, Graph y Table. Spring Boot Starter de Microsoft permite a los desarrolladores usar aplicaciones de Spring Boot que se integran fácilmente con Azure Cosmos DB mediante SQL API.

En este artículo se muestra cómo crear una base de datos de Azure Cosmos DB mediante Azure Portal, cómo usar **[Spring Initializr]** para crear una aplicación Java personalizada y, después, cómo agregar la funcionalidad de iniciador de Spring Boot a su aplicación personalizada para almacenar datos en Azure Cosmos DB y recuperarlos mediante SQL API.

## <a name="prerequisites"></a>Requisitos previos

Los siguientes requisitos previos son necesarios para seguir los pasos descritos en este artículo:

* Una suscripción de Azure. Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN] o registrarse para obtener una [cuenta de Azure gratuita].
* Un kit de desarrollo de Java (JDK) admitido Para más información sobre los JDK disponibles para desarrollar en Azure, consulte <https://aka.ms/azure-jdks>.
* [Apache Maven](http://maven.apache.org/), versión 3.0 o posterior.

## <a name="create-an-azure-cosmos-db-by-using-the-azure-portal"></a>Creación de una instancia de Azure Cosmos DB mediante Azure Portal

1. Vaya a Azure Portal en <https://portal.azure.com/> y haga clic en **+Crear un recurso**.

   ![Azure Portal][AZ01]

1. Haga clic en **Bases de datos** y luego haga clic en **Azure Cosmos DB**.

   ![Azure Portal][AZ02]

1. En la página **Azure Cosmos DB**, escriba la información siguiente:

   * Escriba un **identificador** único, que usará como el identificador URI para la base de datos. Por ejemplo, *wingtiptoysdata.documents.azure.com*.
   * Elija **SQL** como API.
   * Elija la **suscripción** que quiere usar para la base de datos.
   * Especifique si quiere crear un nuevo **grupo de recursos** para la base de datos o elija un grupo de recursos diferente.
   * Especifique la **ubicación** de la base de datos.
   
   Cuando haya especificado estas opciones, haga clic en **Crear** para crear la base de datos.

   ![Azure Portal][AZ03]

1. Cuando se ha creado la base de datos, se muestra en el **panel** de Azure, así como en las páginas **Todos los recursos** y **Azure Cosmos DB**. Puede hacer clic en la base de datos en cualquiera de esas ubicaciones para abrir la página de propiedades de la caché.

   ![Azure Portal][AZ04]

1. Cuando se muestre la página de propiedades de la base de datos, haga clic en **Claves de acceso** y copie el identificador URI y las claves de acceso de la base de datos; usará estos valores en su aplicación de Spring Boot.

   ![Azure Portal][AZ05]

## <a name="create-a-simple-spring-boot-application-with-the-spring-initializr"></a>Creación de una aplicación sencilla de Spring Boot con Spring Initializr

1. Vaya a <https://start.spring.io/>.

1. Especifique que quiere generar un proyecto de **Maven** con **Java**, escriba los nombres de **Group** (Grupo) y **Artifact** (Artefacto) de su aplicación, especifique su versión de **Spring Boot** y, luego, haga clic en el botón **Generate Project** (Generar proyecto).

   > [!IMPORTANT]
   >
   > Hubo varios cambios importantes en las API de la versión 2.0.n de Spring Boot, que se usarán para completar los pasos descritos en este artículo. Puede usar una de las versiones 1.5.n de Spring Boot para completar los pasos de este tutorial y se resaltarán las diferencias cuando sea necesario.
   >

   ![Opciones básicas de Spring Initializr][SI01]

   > [!NOTE]
   >
   > Spring Initializr usa los nombres de **Group** (Grupo) y **Artifact** (Artefacto) para crear el nombre del paquete, por ejemplo: *com.example.wintiptoysdata*.
   >

1. Cuando se le solicite, descargue el proyecto en una ruta de acceso del equipo local.

   ![Descarga del proyecto personalizado de Spring Boot][SI02]

1. Después de extraer los archivos en el sistema local, la aplicación sencilla de Spring Boot estará lista para editarla.

   ![Archivos de proyecto de Spring Boot personalizados][SI03]

## <a name="configure-your-spring-boot-app-to-use-the-azure-spring-boot-starter"></a>Configuración de la aplicación de Spring Boot para usar Azure Spring Boot Starter

1. Busque el archivo *pom.xml* en el directorio de la aplicación; por ejemplo:

   `C:\SpringBoot\wingtiptoysdata\pom.xml`

   O bien

   `/users/example/home/wingtiptoysdata/pom.xml`

   ![Guarde el archivo pom.xml.][PM01]

1. Abra el archivo *pom.xml* en un editor de texto y agregue las siguientes líneas a la lista de `<dependencies>`:

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-documentdb-spring-boot-starter</artifactId>
      <version>2.0.4</version>
   </dependency>
   ```

   ![Edición del archivo pom.xml][PM02]

   > [!IMPORTANT]
   >
   > Si usa una de las versiones 1.5.n de Spring Boot para completar este tutorial, deberá especificar la versión anterior del kit de inicio de Azure Cosmos DB; por ejemplo:
   >
   > ```xml
   > <dependency>
   >   <groupId>com.microsoft.azure</groupId>
   >   <artifactId>azure-documentdb-spring-boot-starter</artifactId>
   >   <version>0.1.4</version>
   > </dependency>
   > ```

1. Compruebe que la versión de Spring Boot es la que eligió al crear la aplicación con Spring Initializr; por ejemplo:

   ```xml
   <parent>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-parent</artifactId>
      <version>2.0.1.RELEASE</version>
      <relativePath/>
   </parent>
   ```

   > [!NOTE]
   >
   > Si usa una de las versiones 1.5.n de Spring Boot para completar este tutorial, deberá especificar la versión correcta; por ejemplo `<version>1.5.14.RELEASE</version>`.
   >

1. Guarde y cierre el archivo *pom.xml*.

## <a name="configure-your-spring-boot-app-to-use-your-azure-cosmos-db"></a>Configuración de la aplicación de Spring Boot para usar Azure Cosmos DB

1. Busque el archivo *application.properties* en el directorio *resources* de su aplicación; por ejemplo:

   `C:\SpringBoot\wingtiptoysdata\src\main\resources\application.properties`

   O bien

   `/users/example/home/wingtiptoysdata/src/main/resources/application.properties`

   ![Búsqueda del archivo application.properties][RE01]

1. Abra el archivo *application.properties* en un editor de texto y agréguele las siguientes líneas; a continuación, sustituya los valores de ejemplo por las propiedades adecuadas de su base de datos:

   ```yaml
   # Specify the DNS URI of your Azure Cosmos DB.
   azure.documentdb.uri=https://wingtiptoys.documents.azure.com:443/

   # Specify the access key for your database.
   azure.documentdb.key=57686f6120447564652c20426f6220526f636b73==

   # Specify the name of your database.
   azure.documentdb.database=wingtiptoysdata
   ```

   ![Edición del archivo application.properties][RE02]

1. Guarde y cierre el archivo *application.properties*.

## <a name="add-sample-code-to-implement-basic-database-functionality"></a>Adición de ejemplo de código para implementar funcionalidad básica de base de datos

En esta sección creará dos clases de Java para almacenar datos de usuario y, después, va a modificar la clase de aplicación principal para crear una instancia de la clase de usuario y guardarla en la base de datos.

### <a name="define-a-basic-class-for-storing-user-data"></a>Definición de una clase básica para almacenar datos de usuario

1. Cree un nuevo archivo llamado *User.java* en el mismo directorio que el archivo de Java de la aplicación principal.

1. Abra el archivo *User.java* en un editor de texto y agréguele las siguientes líneas para definir una clase de usuario genérica que almacene y recupere valores de la base de datos:

   ```java
   package com.example.wingtiptoysdata;

   // Define a generic User class.
   public class User {
      private String id;
      private String firstName;
      private String lastName;
   
      public User() {
      }
   
      public User(String id, String firstName, String lastName) {
         this.id = id;
         this.firstName = firstName;
         this.lastName = lastName;
      }
   
      public String getId() {
         return this.id;
      }
   
      public void setId(String id) {
         this.id = id;
      }
   
      public String getFirstName() {
         return firstName;
      }
   
      public void setFirstName(String firstName) {
         this.firstName = firstName;
      }
   
      public String getLastName() {
         return lastName;
      }
   
      public void setLastName(String lastName) {
         this.lastName = lastName;
      }
   
      @Override
      public String toString() {
         return String.format("User: %s %s %s", id, firstName, lastName);
      }
   }
   ```

1. Guarde y cierre el archivo *User.java*.

### <a name="define-a-data-repository-interface"></a>Definición de una interfaz del repositorio de datos

1. Cree un nuevo archivo llamado *UserRepository.java* en el mismo directorio que el archivo de Java de la aplicación principal.

1. Abra el archivo *UserRepository.java* en un editor de texto y agréguele las siguientes líneas para definir una interfaz de repositorio de usuario que extienda la interfaz predeterminada del repositorio de DocumentDB:

   ```java
   package com.example.wingtiptoysdata;
   
   import com.microsoft.azure.spring.data.documentdb.repository.DocumentDbRepository;
   import org.springframework.stereotype.Repository;
   
   @Repository
   public interface UserRepository extends DocumentDbRepository<User, String> { } 
   ```

1. Guarde y cierre el archivo *UserRepository.java*.

### <a name="modify-the-main-application-class"></a>Modificación de la clase de aplicación principal

1. Busque el archivo de Java de la aplicación principal en el directorio del paquete de la aplicación; por ejemplo:

   `C:\SpringBoot\wingtiptoysdata\src\main\java\com\example\wingtiptoysdata\WingtiptoysdataApplication.java`

   O bien

   `/users/example/home/wingtiptoysdata/src/main/java/com/example/wingtiptoysdata/WingtiptoysdataApplication.java`

   ![Búsqueda del archivo de Java de la aplicación][JV01]

1. Abra el archivo de Java de la aplicación principal en un editor de texto y agregue las siguientes líneas al archivo:

   ```java
   package com.example.wingtiptoysdata;

   // These imports are required for the application.
   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.boot.CommandLineRunner;

   // These imports are only used to create an ID for this example.
   import java.util.Date;
   import java.text.SimpleDateFormat;

   @SpringBootApplication
   public class wingtiptoysdataApplication implements CommandLineRunner {

      @Autowired
      private UserRepository repository;

      public static void main(String[] args) {
         // Execute the command line runner.
         SpringApplication.run(wingtiptoysdataApplication.class, args);
         System.exit(0);
      }

      public void run(String... args) throws Exception {
         // Create a simple date/time ID.
         SimpleDateFormat userId = new SimpleDateFormat("yyyyMMddHHmmssSSS");
         Date currentDate = new Date();

         // Create a new User class.
         final User testUser = new User(userId.format(currentDate), "Gena", "Soto");

         // For this example, remove all of the existing records.
         repository.deleteAll();

         // Save the User class to the Azure database.
         repository.save(testUser);
      
         // Retrieve the database record for the User class you just saved by ID.
         // final User result = repository.findOne(testUser.getId());
         final User result = repository.findById(testUser.getId()).get();

         // Display the results of the database record retrieval.
         System.out.printf("\n\n%s\n\n",result.toString());
      }
   }
   ```

   > [!IMPORTANT]
   >
   > Si usa una de las versiones 1.5.n de Spring Boot para completar este tutorial, deberá remplazar la sintaxis `final User result = repository.findById(testUser.getId()).get();` por `final User result = repository.findOne(testUser.getId());`.
   >

1. Guarde y cierre el archivo de Java de la aplicación principal.

## <a name="build-and-test-your-app"></a>Compilación y prueba de la aplicación

1. Abra un símbolo del sistema y cambie el directorio a la carpeta donde se encuentra el archivo *pom.xml*; por ejemplo:

   `cd C:\SpringBoot\wingtiptoysdata`

   O bien

   `cd /users/example/home/wingtiptoysdata`

1. Compile la aplicación de Spring Boot con Maven y ejecútela; por ejemplo:

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. La aplicación mostrará varios mensajes en tiempo de ejecución y mostrará un mensaje como el de los ejemplos siguientes, que indica que los valores se han almacenado y recuperado correctamente de la base de datos.

   ```
   User: 20170724025215132 Gena Soto
   ```

   ![Salida correcta de la aplicación][JV02]

1. OPCIONAL: Puede usar Azure Portal para ver el contenido de Azure Cosmos DB en la página de propiedades de la base de datos; para ello, haga clic en **Explorador de datos** y luego seleccione un elemento de la lista mostrada para ver el contenido.

   ![Uso del Explorador de documentos para ver los datos][JV03]

## <a name="next-steps"></a>Pasos siguientes

Para más información acerca de Spring y Azure, vaya al centro de documentación de Azure.

> [!div class="nextstepaction"]
> [Spring en Azure](/java/azure/spring-framework)

### <a name="additional-resources"></a>Recursos adicionales

Para más información sobre el uso de Azure Cosmos DB y Java, consulte los siguientes artículos:

* [Documentación sobre Azure Cosmos DB]

* [Azure Cosmos DB: Creación de una base de datos de documentos mediante Java y Azure Portal][Build a SQL API app with Java]

* [Spring Data para SQL API de Azure Cosmos DB]

Para obtener más información sobre el uso de aplicaciones de Spring Boot en Azure, consulte los siguientes artículos:

* [Spring Boot Document DB Starter para Azure]

* [Implementación de una aplicación de Spring Boot en Azure App Service](deploy-spring-boot-java-web-app-on-azure.md)

* [Ejecución de una aplicación de Spring Boot en un clúster de Kubernetes en Azure Container Service](deploy-spring-boot-java-app-on-kubernetes.md)

Para más información sobre el uso de Azure con Java, consulte [Azure para desarrolladores de Java] y [Working with Azure DevOps and Java] (Trabajo con Azure DevOps y Java).

**[Spring Framework]** es una solución de código abierto que ayuda a los desarrolladores de Java a crear aplicaciones de nivel empresarial. Uno de los proyectos más populares que se basa en esa plataforma es [Spring Boot], que proporciona un enfoque simplificado para crear aplicaciones de Java independientes. Para ayudar a los desarrolladores a empezar con Spring Boot, puede encontrar varios paquetes de ejemplo de Spring Boot en <https://github.com/spring-guides/>. Además de elegir de la lista de proyectos básicos de Spring Boot, el **[Spring Initializr]** ayuda a los desarrolladores en los primeros pasos para crear aplicaciones de Spring Boot personalizadas.

<!-- URL List -->

[Documentación sobre Azure Cosmos DB]: /azure/cosmos-db/
[Azure para desarrolladores de Java]: /java/azure/
[Build a SQL API app with Java]: /azure/cosmos-db/create-sql-api-java 
[Spring Data para SQL API de Azure Cosmos DB]: https://azure.microsoft.com/blog/spring-data-azure-cosmos-db-nosql-data-access-on-azure/
[Spring Boot Document DB Starter para Azure]:https://github.com/Microsoft/azure-spring-boot-starters/tree/master/azure-documentdb-spring-boot-starter-sample
[cuenta de Azure gratuita]: https://azure.microsoft.com/pricing/free-trial/
[Working with Azure DevOps and Java]: https://azure.microsoft.com/services/devops/java/ (Trabajo con Azure DevOps y Java)
[ventajas como suscriptor de MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[AZ01]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/AZ01.png
[AZ02]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/AZ02.png
[AZ03]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/AZ03.png
[AZ04]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/AZ04.png
[AZ05]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/AZ05.png

[SI01]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/SI01.png
[SI02]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/SI02.png
[SI03]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/SI03.png

[RE01]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/RE01.png
[RE02]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/RE02.png

[PM01]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/PM01.png
[PM02]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/PM02.png

[JV01]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/JV01.png
[JV02]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/JV02.png
[JV03]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/JV03.png
