---
title: Uso de la utilidad Spring Boot Starter con SQL API de Azure Cosmos DB
description: Aprenda a configurar una aplicación creada con Spring Boot Initializer con SQL API de Azure Cosmos DB.
services: cosmos-db
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: robmcm;yungez;kevinzha
ms.date: 02/01/2018
ms.devlang: java
ms.service: cosmos-db
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: data-services
ms.openlocfilehash: 85494fc310e2bb31cfe8636b5e866bb3f4856cd4
ms.sourcegitcommit: 3a746e8ae9ef0e6e82fccf9aca54eae8c9c1cdca
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2018
---
# <a name="how-to-use-the-spring-boot-starter-with-the-azure-cosmos-db-sql-api"></a><span data-ttu-id="8198e-103">Uso de la utilidad Spring Boot Starter con SQL API de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="8198e-103">How to use the Spring Boot Starter with the Azure Cosmos DB SQL API</span></span>

## <a name="overview"></a><span data-ttu-id="8198e-104">Información general</span><span class="sxs-lookup"><span data-stu-id="8198e-104">Overview</span></span>

<span data-ttu-id="8198e-105">Azure Cosmos DB es un servicio de base de datos de distribución global que permite a los desarrolladores trabajar con datos mediante diversas API estándar, como SQL, MongoDB, Graph y Table.</span><span class="sxs-lookup"><span data-stu-id="8198e-105">Azure Cosmos DB is a globally-distributed database service that allows developers to work with data using a variety of standard APIs, such as SQL, MongoDB, Graph, and Table APIs.</span></span> <span data-ttu-id="8198e-106">Spring Boot Starter de Microsoft permite a los desarrolladores usar aplicaciones de Spring Boot que se integran fácilmente con Azure Cosmos DB mediante SQL API.</span><span class="sxs-lookup"><span data-stu-id="8198e-106">Microsoft's Spring Boot Starter enables developers to use Spring Boot applications that easily integrate with Azure Cosmos DB by using the SQL API.</span></span>

<span data-ttu-id="8198e-107">En este artículo se muestra cómo crear una base de datos de Azure Cosmos DB mediante Azure Portal, cómo usar **[Spring Initializr]** para crear una aplicación Java personalizada y, después, cómo agregar la funcionalidad de iniciador de Spring Boot a su aplicación personalizada para almacenar datos en Azure Cosmos DB y recuperarlos mediante SQL API.</span><span class="sxs-lookup"><span data-stu-id="8198e-107">This article demonstrates creating an Azure Cosmos DB using the Azure portal, then using the **[Spring Initializr]** to create a custom java application, and then add the Spring Boot Starter functionality to your custom application to store data in and retrieve data from your Azure Cosmos DB by using the SQL API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8198e-108">requisitos previos</span><span class="sxs-lookup"><span data-stu-id="8198e-108">Prerequisites</span></span>

<span data-ttu-id="8198e-109">Los siguientes requisitos previos son necesarios para seguir los pasos descritos en este artículo:</span><span class="sxs-lookup"><span data-stu-id="8198e-109">The following prerequisites are required in order to follow the steps in this article:</span></span>

* <span data-ttu-id="8198e-110">Una suscripción de Azure. Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN] o registrarse para obtener una [cuenta de Azure gratuita].</span><span class="sxs-lookup"><span data-stu-id="8198e-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="8198e-111">Un [kit de desarrollo de Java (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), versión 1.7 o posterior.</span><span class="sxs-lookup"><span data-stu-id="8198e-111">A [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 or later.</span></span>
* <span data-ttu-id="8198e-112">[Apache Maven](http://maven.apache.org/), versión 3.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="8198e-112">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-an-azure-cosmos-db-by-using-the-azure-portal"></a><span data-ttu-id="8198e-113">Creación de una instancia de Azure Cosmos DB mediante Azure Portal</span><span class="sxs-lookup"><span data-stu-id="8198e-113">Create an Azure Cosmos DB by using the Azure portal</span></span>

1. <span data-ttu-id="8198e-114">Vaya a Azure Portal en <https://portal.azure.com/> y haga clic en **+Nuevo**.</span><span class="sxs-lookup"><span data-stu-id="8198e-114">Browse to the Azure portal at <https://portal.azure.com/> and click **+New**.</span></span>

   ![Azure Portal][AZ01]

1. <span data-ttu-id="8198e-116">Haga clic en **Bases de datos** y luego haga clic en **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="8198e-116">Click **Databases**, and then click **Azure Cosmos DB**.</span></span>

   ![Azure Portal][AZ02]

1. <span data-ttu-id="8198e-118">En la página **Azure Cosmos DB**, escriba la información siguiente:</span><span class="sxs-lookup"><span data-stu-id="8198e-118">On the **Azure Cosmos DB** page, enter the following information:</span></span>

   * <span data-ttu-id="8198e-119">Escriba un **identificador** único, que usará como el identificador URI para la base de datos.</span><span class="sxs-lookup"><span data-stu-id="8198e-119">Enter a unique **ID**, which you will use as the URI for your database.</span></span> <span data-ttu-id="8198e-120">Por ejemplo, *wingtiptoysdata.documents.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="8198e-120">For example: *wingtiptoysdata.documents.azure.com*.</span></span>
   * <span data-ttu-id="8198e-121">Elija **SQL (DocumentDB)** para la API.</span><span class="sxs-lookup"><span data-stu-id="8198e-121">Choose **SQL (Document DB)** for the API.</span></span>
   * <span data-ttu-id="8198e-122">Elija la **suscripción** que quiere usar para la base de datos.</span><span class="sxs-lookup"><span data-stu-id="8198e-122">Choose the **Subscription** you want to use for your database.</span></span>
   * <span data-ttu-id="8198e-123">Especifique si quiere crear un nuevo **grupo de recursos** para la base de datos o elija un grupo de recursos diferente.</span><span class="sxs-lookup"><span data-stu-id="8198e-123">Specify whether to create a new **Resource group** for your database, or choose an existing resource group.</span></span>
   * <span data-ttu-id="8198e-124">Especifique la **ubicación** de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="8198e-124">Specify the **Location** for your database.</span></span>
   
   <span data-ttu-id="8198e-125">Cuando haya especificado estas opciones, haga clic en **Crear** para crear la base de datos.</span><span class="sxs-lookup"><span data-stu-id="8198e-125">When you have specified these options, click **Create** to create your database.</span></span>

   ![Azure Portal][AZ03]

1. <span data-ttu-id="8198e-127">Cuando se ha creado la base de datos, se muestra en el **panel** de Azure, así como en las páginas **Todos los recursos** y **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="8198e-127">When your database has been created, it is listed on your Azure **Dashboard**, as well as under the **All Resources** and **Azure Cosmos DB** pages.</span></span> <span data-ttu-id="8198e-128">Puede hacer clic en la base de datos en cualquiera de esas ubicaciones para abrir la página de propiedades de la caché.</span><span class="sxs-lookup"><span data-stu-id="8198e-128">You can click on your database on any of those locations to open the properties page for your cache.</span></span>

   ![Azure Portal][AZ04]

1. <span data-ttu-id="8198e-130">Cuando se muestre la página de propiedades de la base de datos, haga clic en **Claves de acceso** y copie el identificador URI y las claves de acceso de la base de datos; usará estos valores en su aplicación de Spring Boot.</span><span class="sxs-lookup"><span data-stu-id="8198e-130">When the properties page for your database is displayed, click **Access keys** and copy your URI and access keys for your database; you will use these values in your Spring Boot application.</span></span>

   ![Azure Portal][AZ05]

## <a name="create-a-simple-spring-boot-application-with-the-spring-initializr"></a><span data-ttu-id="8198e-132">Creación de una aplicación sencilla de Spring Boot con Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="8198e-132">Create a simple Spring Boot application with the Spring Initializr</span></span>

1. <span data-ttu-id="8198e-133">Vaya a <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="8198e-133">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="8198e-134">Especifique que quiere generar un proyecto de **Maven** con **Java**, escriba los nombres de **Group** (Grupo) y **Artifact** (Artefacto) de su aplicación y luego haga clic en el botón **Generate Project** (Generar proyecto).</span><span class="sxs-lookup"><span data-stu-id="8198e-134">Specify that you want to generate a **Maven** project with **Java**, enter the **Group** and **Artifact** names for your application, and then click the button to **Generate Project**.</span></span>

   ![Opciones básicas de Basic Spring Initializr][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="8198e-136">Spring Initializr usa los nombres de **Group** (Grupo) y **Artifact** (Artefacto) para crear el nombre del paquete, por ejemplo: *com.example.wintiptoys*.</span><span class="sxs-lookup"><span data-stu-id="8198e-136">The Spring Initializr uses the **Group** and **Artifact** names to create the package name; for example: *com.example.wintiptoys*.</span></span>
   >

1. <span data-ttu-id="8198e-137">Cuando se le solicite, descargue el proyecto en una ruta del equipo local.</span><span class="sxs-lookup"><span data-stu-id="8198e-137">When prompted, download the project to a path on your local computer.</span></span>

   ![Descarga del proyecto personalizado de Spring Boot][SI02]

1. <span data-ttu-id="8198e-139">Después de extraer los archivos en el sistema local, la aplicación sencilla de Spring Boot estará lista para editarla.</span><span class="sxs-lookup"><span data-stu-id="8198e-139">After you have extracted the files on your local system, your simple Spring Boot application will be ready for editing.</span></span>

   ![Archivos de proyecto de Spring Boot personalizados][SI03]

## <a name="configure-your-spring-boot-app-to-use-the-azure-spring-boot-starter"></a><span data-ttu-id="8198e-141">Configuración de la aplicación de Spring Boot para usar Azure Spring Boot Starter</span><span class="sxs-lookup"><span data-stu-id="8198e-141">Configure your Spring Boot app to use the Azure Spring Boot Starter</span></span>

1. <span data-ttu-id="8198e-142">Busque el archivo *pom.xml* en el directorio de la aplicación; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="8198e-142">Locate the *pom.xml* file in the directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoys\pom.xml`

   <span data-ttu-id="8198e-143">O bien</span><span class="sxs-lookup"><span data-stu-id="8198e-143">-or-</span></span>

   `/users/example/home/wingtiptoys/pom.xml`

   ![Guarde el archivo pom.xml.][PM01]

1. <span data-ttu-id="8198e-145">Abra el archivo *pom.xml* en un editor de texto y agregue las siguientes líneas a la lista de `<dependencies>`:</span><span class="sxs-lookup"><span data-stu-id="8198e-145">Open the *pom.xml* file in a text editor, and add the following lines to list of `<dependencies>`:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-documentdb-spring-boot-starter</artifactId>
      <version>0.1.4</version>
   </dependency>
   ```

   ![Edición del archivo pom.xml][PM02]

1. <span data-ttu-id="8198e-147">Guarde y cierre el archivo *pom.xml*.</span><span class="sxs-lookup"><span data-stu-id="8198e-147">Save and close the *pom.xml* file.</span></span>

## <a name="configure-your-spring-boot-app-to-use-your-azure-cosmos-db"></a><span data-ttu-id="8198e-148">Configuración de la aplicación de Spring Boot para usar Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="8198e-148">Configure your Spring Boot app to use your Azure Cosmos DB</span></span>

1. <span data-ttu-id="8198e-149">Busque el archivo *application.properties* en el directorio *resources* de su aplicación; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="8198e-149">Locate the *application.properties* file in the *resources* directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoys\src\main\resources\application.properties`

   <span data-ttu-id="8198e-150">O bien</span><span class="sxs-lookup"><span data-stu-id="8198e-150">-or-</span></span>

   `/users/example/home/wingtiptoys/src/main/resources/application.properties`

   ![Búsqueda del archivo application.properties][RE01]

1. <span data-ttu-id="8198e-152">Abra el archivo *application.properties* en un editor de texto y agréguele las siguientes líneas; a continuación, sustituya los valores de ejemplo por las propiedades adecuadas de su base de datos:</span><span class="sxs-lookup"><span data-stu-id="8198e-152">Open the *application.properties* file in a text editor, and add the following lines to the file, and replace the sample values with the appropriate properties for your database:</span></span>

   ```yaml
   # Specify the DNS URI of your Azure Cosmos DB.
   azure.documentdb.uri=https://wingtiptoys.documents.azure.com:443/

   # Specify the access key for your database.
   azure.documentdb.key=57686f6120447564652c20426f6220526f636b73==

   # Specify the name of your database.
   azure.documentdb.database=wingtiptoysdata
   ```

   ![Edición del archivo application.properties][RE02]

1. <span data-ttu-id="8198e-154">Guarde y cierre el archivo *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="8198e-154">Save and close the *application.properties* file.</span></span>

## <a name="add-sample-code-to-implement-basic-database-functionality"></a><span data-ttu-id="8198e-155">Adición de ejemplo de código para implementar funcionalidad básica de base de datos</span><span class="sxs-lookup"><span data-stu-id="8198e-155">Add sample code to implement basic database functionality</span></span>

<span data-ttu-id="8198e-156">En esta sección creará dos clases de Java para almacenar datos de usuario y, después, va a modificar la clase de aplicación principal para crear una instancia de la clase de usuario y guardarla en la base de datos.</span><span class="sxs-lookup"><span data-stu-id="8198e-156">In this section you create two Java classes for storing user data, and then you modify your main application class to create an instance of the user class and save it to your database.</span></span>

### <a name="define-a-basic-class-for-storing-user-data"></a><span data-ttu-id="8198e-157">Definición de una clase básica para almacenar datos de usuario</span><span class="sxs-lookup"><span data-stu-id="8198e-157">Define a basic class for storing user data</span></span>

1. <span data-ttu-id="8198e-158">Cree un nuevo archivo llamado *User.java* en el mismo directorio que el archivo de Java de la aplicación principal.</span><span class="sxs-lookup"><span data-stu-id="8198e-158">Create a new file named *User.java* in the same directory as your main application Java file.</span></span>

1. <span data-ttu-id="8198e-159">Abra el archivo *User.java* en un editor de texto y agréguele las siguientes líneas para definir una clase de usuario genérica que almacene y recupere valores de la base de datos:</span><span class="sxs-lookup"><span data-stu-id="8198e-159">Open the *User.java* file in a text editor, and add the following lines to the file to define a generic user class that stores and retrieve values in your database:</span></span>

   ```java
   package com.example.wingtiptoys;

   public class User {
      private String id;
      private String firstName;
      private String lastName;
 
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
         return String.format("User: %s %s", firstName, lastName);
      }
   }
   ```

1. <span data-ttu-id="8198e-160">Guarde y cierre el archivo *User.java*.</span><span class="sxs-lookup"><span data-stu-id="8198e-160">Save and close the *User.java* file.</span></span>

### <a name="define-a-data-repository-interface"></a><span data-ttu-id="8198e-161">Definición de una interfaz del repositorio de datos</span><span class="sxs-lookup"><span data-stu-id="8198e-161">Define a data repository interface</span></span>

1. <span data-ttu-id="8198e-162">Cree un nuevo archivo llamado *UserRepository.java* en el mismo directorio que el archivo de Java de la aplicación principal.</span><span class="sxs-lookup"><span data-stu-id="8198e-162">Create a new file named *UserRepository.java* in the same directory as your main application Java file.</span></span>

1. <span data-ttu-id="8198e-163">Abra el archivo *UserRepository.java* en un editor de texto y agréguele las siguientes líneas para definir una interfaz de repositorio de usuario que extienda la interfaz predeterminada del repositorio de DocumentDB:</span><span class="sxs-lookup"><span data-stu-id="8198e-163">Open the *UserRepository.java* file in a text editor, and add the following lines to the file to define a user repository interface that extends the default DocumentDB repository interface:</span></span>

   ```java
   package com.example.wingtiptoys;

   import com.microsoft.azure.spring.data.documentdb.repository.DocumentDbRepository;
   import org.springframework.stereotype.Repository;

   @Repository
   public interface UserRepository extends DocumentDbRepository<User, String> {}   
   ```

1. <span data-ttu-id="8198e-164">Guarde y cierre el archivo *UserRepository.java*.</span><span class="sxs-lookup"><span data-stu-id="8198e-164">Save and close the *UserRepository.java* file.</span></span>

### <a name="modify-the-main-application-class"></a><span data-ttu-id="8198e-165">Modificación de la clase de aplicación principal</span><span class="sxs-lookup"><span data-stu-id="8198e-165">Modify the main application class</span></span>

1. <span data-ttu-id="8198e-166">Busque el archivo de Java de la aplicación principal en el directorio del paquete de la aplicación; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="8198e-166">Locate the main application Java file in the package directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoys\src\main\java\com\example\wingtiptoys\WingtiptoysApplication.java`

   <span data-ttu-id="8198e-167">O bien</span><span class="sxs-lookup"><span data-stu-id="8198e-167">-or-</span></span>

   `/users/example/home/wingtiptoys/src/main/java/com/example/wingtiptoys/WingtiptoysApplication.java`

   ![Búsqueda del archivo de Java de la aplicación][JV01]

1. <span data-ttu-id="8198e-169">Abra el archivo de Java de la aplicación principal en un editor de texto y agregue las siguientes líneas al archivo:</span><span class="sxs-lookup"><span data-stu-id="8198e-169">Open the main application Java file in a text editor, and add the following lines to the file:</span></span>

   ```java
   package com.example.wingtiptoys;

   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.boot.CommandLineRunner;

   @SpringBootApplication
   public class WingtiptoysApplication implements CommandLineRunner {

      @Autowired
      private UserRepository repository;
    
      public static void main(String[] args) {
         SpringApplication.run(WingtiptoysApplication.class, args);
      }

      public void run(String... var1) throws Exception {
         final User testUser = new User("testId", "testFirstName", "testLastName");

         repository.deleteAll();
         repository.save(testUser);

         final User result = repository.findOne(testUser.getId());

         System.out.printf("\n\n%s\n\n",result.toString());
      }
   }
   ```

1. <span data-ttu-id="8198e-170">Guarde y cierre el archivo de Java de la aplicación principal.</span><span class="sxs-lookup"><span data-stu-id="8198e-170">Save and close the main application Java file.</span></span>

## <a name="build-and-test-your-app"></a><span data-ttu-id="8198e-171">Compilación y prueba de la aplicación</span><span class="sxs-lookup"><span data-stu-id="8198e-171">Build and test your app</span></span>

1. <span data-ttu-id="8198e-172">Abra un símbolo del sistema y cambie el directorio a la carpeta donde se encuentra el archivo *pom.xml*; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="8198e-172">Open a command prompt and change directory to the folder where your *pom.xml* file is located; for example:</span></span>

   `cd C:\SpringBoot\wingtiptoys`

   <span data-ttu-id="8198e-173">O bien</span><span class="sxs-lookup"><span data-stu-id="8198e-173">-or-</span></span>

   `cd /users/example/home/wingtiptoys`

1. <span data-ttu-id="8198e-174">Compile la aplicación de Spring Boot con Maven y ejecútela; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="8198e-174">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn package
   java -jar target/wingtiptoys-0.0.1-SNAPSHOT.jar
   ```

1. <span data-ttu-id="8198e-175">La aplicación mostrará varios mensajes de tiempo de ejecución y verá el mensaje `User: testFirstName testLastName` que indica que los valores se han almacenado y recuperado correctamente de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="8198e-175">Your application will display several runtime messages, and you should see the message `User: testFirstName testLastName` displayed to indicate that values have been successfully stored and retrieved from your database.</span></span>

   ![Salida correcta de la aplicación][JV02]

1. <span data-ttu-id="8198e-177">OPCIONAL: Puede usar Azure Portal para ver el contenido de Azure Cosmos DB en la página de propiedades de la base de datos; para ello, haga clic en **Explorador de documentos** y luego seleccione un elemento de la lista mostrada para ver el contenido.</span><span class="sxs-lookup"><span data-stu-id="8198e-177">OPTIONAL: You can use the Azure portal to view the contents of your Azure Cosmos DB from the properties page for your database by clicking  **Document Explorer**, and then selecting and item from the displayed list to view the contents.</span></span>

   ![Uso del Explorador de documentos para ver los datos][JV03]

## <a name="next-steps"></a><span data-ttu-id="8198e-179">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8198e-179">Next steps</span></span>

<span data-ttu-id="8198e-180">Para más información sobre el uso de Azure Cosmos DB y Java, consulte los siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="8198e-180">For more information about using Azure Cosmos DB and Java, see the following articles:</span></span>

* <span data-ttu-id="8198e-181">[Documentación sobre Azure Cosmos DB]</span><span class="sxs-lookup"><span data-stu-id="8198e-181">[Azure Cosmos DB Documentation].</span></span>

* <span data-ttu-id="8198e-182">[Azure Cosmos DB: creación una base de datos de documentos mediante Java y Azure Portal][Build a SQL API app with Java]</span><span class="sxs-lookup"><span data-stu-id="8198e-182">[Azure Cosmos DB: Create a document database using Java and the Azure portal][Build a SQL API app with Java]</span></span>

<span data-ttu-id="8198e-183">Para obtener más información sobre el uso de aplicaciones de Spring Boot en Azure, consulte los siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="8198e-183">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* <span data-ttu-id="8198e-184">[Spring Boot DocumenDB Starter for Azure](https://github.com/Microsoft/azure-spring-boot-starters/tree/master/azure-documentdb-spring-boot-starter-sample) (Spring Boot DocumenDB Starter para Azure)</span><span class="sxs-lookup"><span data-stu-id="8198e-184">[Spring Boot DocumenDB Starter for Azure](https://github.com/Microsoft/azure-spring-boot-starters/tree/master/azure-documentdb-spring-boot-starter-sample)</span></span>

* [<span data-ttu-id="8198e-185">Implementación de una aplicación de Spring Boot en Azure App Service</span><span class="sxs-lookup"><span data-stu-id="8198e-185">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)

* [<span data-ttu-id="8198e-186">Ejecución de una aplicación de Spring Boot en un clúster de Kubernetes en Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="8198e-186">Running a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="8198e-187">Para más información sobre el uso de Azure con Java, consulte [Azure para desarrolladores de Java] y [Java Tools for Visual Studio Team Services] (Herramientas de Java para Visual Studio Team Services).</span><span class="sxs-lookup"><span data-stu-id="8198e-187">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="8198e-188">**[Spring Framework]** es una solución de código abierto que ayuda a los desarrolladores de Java a crear aplicaciones de nivel empresarial.</span><span class="sxs-lookup"><span data-stu-id="8198e-188">The **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="8198e-189">Uno de los proyectos más populares que se basa en esa plataforma es [Spring Boot], que proporciona un enfoque simplificado para crear aplicaciones de Java independientes.</span><span class="sxs-lookup"><span data-stu-id="8198e-189">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="8198e-190">Para ayudar a los desarrolladores a empezar con Spring Boot, puede encontrar varios paquetes de ejemplo de Spring Boot en <https://github.com/spring-guides/>.</span><span class="sxs-lookup"><span data-stu-id="8198e-190">To help developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>.</span></span> <span data-ttu-id="8198e-191">Además de elegir de la lista de proyectos básicos de Spring Boot, el **[Spring Initializr]** ayuda a los desarrolladores en los primeros pasos para crear aplicaciones de Spring Boot personalizadas.</span><span class="sxs-lookup"><span data-stu-id="8198e-191">In addition to choosing from the list of basic Spring Boot projects, the **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>

<!-- URL List -->

[Documentación sobre Azure Cosmos DB]: /azure/cosmos-db/
[Azure Cosmos DB Documentation]: /azure/cosmos-db/
[Azure para desarrolladores de Java]: https://docs.microsoft.com/java/azure/
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Build a SQL API app with Java]: https://docs.microsoft.com/azure/cosmos-db/create-sql-api-java 
[cuenta de Azure gratuita]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[ventajas como suscriptor de MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
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
