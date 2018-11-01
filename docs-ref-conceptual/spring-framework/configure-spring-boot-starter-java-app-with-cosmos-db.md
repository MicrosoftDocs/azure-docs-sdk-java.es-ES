---
title: Uso de la utilidad Spring Boot Starter con SQL API de Azure Cosmos DB
description: Aprenda a configurar una aplicación creada con Spring Boot Initializer con SQL API de Azure Cosmos DB.
services: cosmos-db
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 08/10/2018
ms.devlang: java
ms.service: cosmos-db
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: data-services
ms.openlocfilehash: aa753692b1a3f342a47a07d3bb0cd4e90558a0f8
ms.sourcegitcommit: a168dc8c2396b6c4749abef03debb1f69298da38
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/01/2018
ms.locfileid: "50747016"
---
# <a name="how-to-use-the-spring-boot-starter-with-the-azure-cosmos-db-sql-api"></a><span data-ttu-id="7e07d-103">Uso de la utilidad Spring Boot Starter con SQL API de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="7e07d-103">How to use the Spring Boot Starter with the Azure Cosmos DB SQL API</span></span>

## <a name="overview"></a><span data-ttu-id="7e07d-104">Información general</span><span class="sxs-lookup"><span data-stu-id="7e07d-104">Overview</span></span>

<span data-ttu-id="7e07d-105">Azure Cosmos DB es un servicio de base de datos de distribución global que permite a los desarrolladores trabajar con datos mediante diversas API estándar, como SQL, MongoDB, Graph y Table.</span><span class="sxs-lookup"><span data-stu-id="7e07d-105">Azure Cosmos DB is a globally-distributed database service that allows developers to work with data using a variety of standard APIs, such as SQL, MongoDB, Graph, and Table APIs.</span></span> <span data-ttu-id="7e07d-106">Spring Boot Starter de Microsoft permite a los desarrolladores usar aplicaciones de Spring Boot que se integran fácilmente con Azure Cosmos DB mediante SQL API.</span><span class="sxs-lookup"><span data-stu-id="7e07d-106">Microsoft's Spring Boot Starter enables developers to use Spring Boot applications that easily integrate with Azure Cosmos DB by using the SQL API.</span></span>

<span data-ttu-id="7e07d-107">En este artículo se muestra cómo crear una base de datos de Azure Cosmos DB mediante Azure Portal, cómo usar **[Spring Initializr]** para crear una aplicación Java personalizada y, después, cómo agregar la funcionalidad de iniciador de Spring Boot a su aplicación personalizada para almacenar datos en Azure Cosmos DB y recuperarlos mediante SQL API.</span><span class="sxs-lookup"><span data-stu-id="7e07d-107">This article demonstrates creating an Azure Cosmos DB using the Azure portal, then using the **[Spring Initializr]** to create a custom java application, and then add the Spring Boot Starter functionality to your custom application to store data in and retrieve data from your Azure Cosmos DB by using the SQL API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7e07d-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="7e07d-108">Prerequisites</span></span>

<span data-ttu-id="7e07d-109">Los siguientes requisitos previos son necesarios para seguir los pasos descritos en este artículo:</span><span class="sxs-lookup"><span data-stu-id="7e07d-109">The following prerequisites are required in order to follow the steps in this article:</span></span>

* <span data-ttu-id="7e07d-110">Una suscripción de Azure. Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN] o registrarse para obtener una [cuenta de Azure gratuita].</span><span class="sxs-lookup"><span data-stu-id="7e07d-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="7e07d-111">Un [kit de desarrollo de Java (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), versión 1.7 o posterior.</span><span class="sxs-lookup"><span data-stu-id="7e07d-111">A [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 or later.</span></span>
* <span data-ttu-id="7e07d-112">[Apache Maven](http://maven.apache.org/), versión 3.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="7e07d-112">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-an-azure-cosmos-db-by-using-the-azure-portal"></a><span data-ttu-id="7e07d-113">Creación de una instancia de Azure Cosmos DB mediante Azure Portal</span><span class="sxs-lookup"><span data-stu-id="7e07d-113">Create an Azure Cosmos DB by using the Azure portal</span></span>

1. <span data-ttu-id="7e07d-114">Vaya a Azure Portal en <https://portal.azure.com/> y haga clic en **+Crear un recurso**.</span><span class="sxs-lookup"><span data-stu-id="7e07d-114">Browse to the Azure portal at <https://portal.azure.com/> and click **+Create a resource**.</span></span>

   ![Azure Portal][AZ01]

1. <span data-ttu-id="7e07d-116">Haga clic en **Bases de datos** y luego haga clic en **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="7e07d-116">Click **Databases**, and then click **Azure Cosmos DB**.</span></span>

   ![Azure Portal][AZ02]

1. <span data-ttu-id="7e07d-118">En la página **Azure Cosmos DB**, escriba la información siguiente:</span><span class="sxs-lookup"><span data-stu-id="7e07d-118">On the **Azure Cosmos DB** page, enter the following information:</span></span>

   * <span data-ttu-id="7e07d-119">Escriba un **identificador** único, que usará como el identificador URI para la base de datos.</span><span class="sxs-lookup"><span data-stu-id="7e07d-119">Enter a unique **ID**, which you will use as the URI for your database.</span></span> <span data-ttu-id="7e07d-120">Por ejemplo, *wingtiptoysdata.documents.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="7e07d-120">For example: *wingtiptoysdata.documents.azure.com*.</span></span>
   * <span data-ttu-id="7e07d-121">Elija **SQL** como API.</span><span class="sxs-lookup"><span data-stu-id="7e07d-121">Choose **SQL** for the API.</span></span>
   * <span data-ttu-id="7e07d-122">Elija la **suscripción** que quiere usar para la base de datos.</span><span class="sxs-lookup"><span data-stu-id="7e07d-122">Choose the **Subscription** you want to use for your database.</span></span>
   * <span data-ttu-id="7e07d-123">Especifique si quiere crear un nuevo **grupo de recursos** para la base de datos o elija un grupo de recursos diferente.</span><span class="sxs-lookup"><span data-stu-id="7e07d-123">Specify whether to create a new **Resource group** for your database, or choose an existing resource group.</span></span>
   * <span data-ttu-id="7e07d-124">Especifique la **ubicación** de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="7e07d-124">Specify the **Location** for your database.</span></span>
   
   <span data-ttu-id="7e07d-125">Cuando haya especificado estas opciones, haga clic en **Crear** para crear la base de datos.</span><span class="sxs-lookup"><span data-stu-id="7e07d-125">When you have specified these options, click **Create** to create your database.</span></span>

   ![Azure Portal][AZ03]

1. <span data-ttu-id="7e07d-127">Cuando se ha creado la base de datos, se muestra en el **panel** de Azure, así como en las páginas **Todos los recursos** y **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="7e07d-127">When your database has been created, it is listed on your Azure **Dashboard**, as well as under the **All Resources** and **Azure Cosmos DB** pages.</span></span> <span data-ttu-id="7e07d-128">Puede hacer clic en la base de datos en cualquiera de esas ubicaciones para abrir la página de propiedades de la caché.</span><span class="sxs-lookup"><span data-stu-id="7e07d-128">You can click on your database on any of those locations to open the properties page for your cache.</span></span>

   ![Azure Portal][AZ04]

1. <span data-ttu-id="7e07d-130">Cuando se muestre la página de propiedades de la base de datos, haga clic en **Claves de acceso** y copie el identificador URI y las claves de acceso de la base de datos; usará estos valores en su aplicación de Spring Boot.</span><span class="sxs-lookup"><span data-stu-id="7e07d-130">When the properties page for your database is displayed, click **Access keys** and copy your URI and access keys for your database; you will use these values in your Spring Boot application.</span></span>

   ![Azure Portal][AZ05]

## <a name="create-a-simple-spring-boot-application-with-the-spring-initializr"></a><span data-ttu-id="7e07d-132">Creación de una aplicación sencilla de Spring Boot con Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="7e07d-132">Create a simple Spring Boot application with the Spring Initializr</span></span>

1. <span data-ttu-id="7e07d-133">Vaya a <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="7e07d-133">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="7e07d-134">Especifique que quiere generar un proyecto de **Maven** con **Java**, escriba los nombres de **Group** (Grupo) y **Artifact** (Artefacto) de su aplicación, especifique su versión de **Spring Boot** y, luego, haga clic en el botón **Generate Project** (Generar proyecto).</span><span class="sxs-lookup"><span data-stu-id="7e07d-134">Specify that you want to generate a **Maven** project with **Java**, enter the **Group** and **Artifact** names for your application, specify your **Spring Boot** version, and then click the button to **Generate Project**.</span></span>

   > [!IMPORTANT]
   >
   > <span data-ttu-id="7e07d-135">Hubo varios cambios importantes en las API de la versión 2.0.n de Spring Boot, que se usarán para completar los pasos descritos en este artículo.</span><span class="sxs-lookup"><span data-stu-id="7e07d-135">There were several breaking changes to the APIs in Spring Boot version 2.0.n, which will be used to complete the steps in this article.</span></span> <span data-ttu-id="7e07d-136">Puede usar una de las versiones 1.5.n de Spring Boot para completar los pasos de este tutorial y se resaltarán las diferencias cuando sea necesario.</span><span class="sxs-lookup"><span data-stu-id="7e07d-136">You can still use one of the Spring Boot 1.5.n versions to complete the steps in this tutorial, and the differences will be highlighted when necessary.</span></span>
   >

   ![Opciones básicas de Spring Initializr][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="7e07d-138">Spring Initializr usa los nombres de **Group** (Grupo) y **Artifact** (Artefacto) para crear el nombre del paquete, por ejemplo: *com.example.wintiptoysdata*.</span><span class="sxs-lookup"><span data-stu-id="7e07d-138">The Spring Initializr uses the **Group** and **Artifact** names to create the package name; for example: *com.example.wintiptoysdata*.</span></span>
   >

1. <span data-ttu-id="7e07d-139">Cuando se le solicite, descargue el proyecto en una ruta de acceso del equipo local.</span><span class="sxs-lookup"><span data-stu-id="7e07d-139">When prompted, download the project to a path on your local computer.</span></span>

   ![Descarga del proyecto personalizado de Spring Boot][SI02]

1. <span data-ttu-id="7e07d-141">Después de extraer los archivos en el sistema local, la aplicación sencilla de Spring Boot estará lista para editarla.</span><span class="sxs-lookup"><span data-stu-id="7e07d-141">After you have extracted the files on your local system, your simple Spring Boot application will be ready for editing.</span></span>

   ![Archivos de proyecto de Spring Boot personalizados][SI03]

## <a name="configure-your-spring-boot-app-to-use-the-azure-spring-boot-starter"></a><span data-ttu-id="7e07d-143">Configuración de la aplicación de Spring Boot para usar Azure Spring Boot Starter</span><span class="sxs-lookup"><span data-stu-id="7e07d-143">Configure your Spring Boot app to use the Azure Spring Boot Starter</span></span>

1. <span data-ttu-id="7e07d-144">Busque el archivo *pom.xml* en el directorio de la aplicación; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="7e07d-144">Locate the *pom.xml* file in the directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoysdata\pom.xml`

   <span data-ttu-id="7e07d-145">O bien</span><span class="sxs-lookup"><span data-stu-id="7e07d-145">-or-</span></span>

   `/users/example/home/wingtiptoysdata/pom.xml`

   ![Guarde el archivo pom.xml.][PM01]

1. <span data-ttu-id="7e07d-147">Abra el archivo *pom.xml* en un editor de texto y agregue las siguientes líneas a la lista de `<dependencies>`:</span><span class="sxs-lookup"><span data-stu-id="7e07d-147">Open the *pom.xml* file in a text editor, and add the following lines to list of `<dependencies>`:</span></span>

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
   > <span data-ttu-id="7e07d-149">Si usa una de las versiones 1.5.n de Spring Boot para completar este tutorial, deberá especificar la versión anterior del kit de inicio de Azure Cosmos DB; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="7e07d-149">If you are using one of Spring Boot 1.5.n versions to complete this tutorial, you will need to specify the older version of the Azure Cosmos DB starter; for example:</span></span>
   >
   > ```xml
   > <dependency>
   >   <groupId>com.microsoft.azure</groupId>
   >   <artifactId>azure-documentdb-spring-boot-starter</artifactId>
   >   <version>0.1.4</version>
   > </dependency>
   > ```

1. <span data-ttu-id="7e07d-150">Compruebe que la versión de Spring Boot es la que eligió al crear la aplicación con Spring Initializr; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="7e07d-150">Verify that the Spring Boot version is the version that you chose when you created your application with the Spring Initializr; for example:</span></span>

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
   > <span data-ttu-id="7e07d-151">Si usa una de las versiones 1.5.n de Spring Boot para completar este tutorial, deberá especificar la versión correcta; por ejemplo `<version>1.5.14.RELEASE</version>`.</span><span class="sxs-lookup"><span data-stu-id="7e07d-151">If you are using one of Spring Boot 1.5.n versions to complete this tutorial, you will need to verify the correct version; for example: `<version>1.5.14.RELEASE</version>`.</span></span>
   >

1. <span data-ttu-id="7e07d-152">Guarde y cierre el archivo *pom.xml*.</span><span class="sxs-lookup"><span data-stu-id="7e07d-152">Save and close the *pom.xml* file.</span></span>

## <a name="configure-your-spring-boot-app-to-use-your-azure-cosmos-db"></a><span data-ttu-id="7e07d-153">Configuración de la aplicación de Spring Boot para usar Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="7e07d-153">Configure your Spring Boot app to use your Azure Cosmos DB</span></span>

1. <span data-ttu-id="7e07d-154">Busque el archivo *application.properties* en el directorio *resources* de su aplicación; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="7e07d-154">Locate the *application.properties* file in the *resources* directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoysdata\src\main\resources\application.properties`

   <span data-ttu-id="7e07d-155">O bien</span><span class="sxs-lookup"><span data-stu-id="7e07d-155">-or-</span></span>

   `/users/example/home/wingtiptoysdata/src/main/resources/application.properties`

   ![Búsqueda del archivo application.properties][RE01]

1. <span data-ttu-id="7e07d-157">Abra el archivo *application.properties* en un editor de texto y agréguele las siguientes líneas; a continuación, sustituya los valores de ejemplo por las propiedades adecuadas de su base de datos:</span><span class="sxs-lookup"><span data-stu-id="7e07d-157">Open the *application.properties* file in a text editor, and add the following lines to the file, and replace the sample values with the appropriate properties for your database:</span></span>

   ```yaml
   # Specify the DNS URI of your Azure Cosmos DB.
   azure.documentdb.uri=https://wingtiptoys.documents.azure.com:443/

   # Specify the access key for your database.
   azure.documentdb.key=57686f6120447564652c20426f6220526f636b73==

   # Specify the name of your database.
   azure.documentdb.database=wingtiptoysdata
   ```

   ![Edición del archivo application.properties][RE02]

1. <span data-ttu-id="7e07d-159">Guarde y cierre el archivo *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="7e07d-159">Save and close the *application.properties* file.</span></span>

## <a name="add-sample-code-to-implement-basic-database-functionality"></a><span data-ttu-id="7e07d-160">Adición de ejemplo de código para implementar funcionalidad básica de base de datos</span><span class="sxs-lookup"><span data-stu-id="7e07d-160">Add sample code to implement basic database functionality</span></span>

<span data-ttu-id="7e07d-161">En esta sección creará dos clases de Java para almacenar datos de usuario y, después, va a modificar la clase de aplicación principal para crear una instancia de la clase de usuario y guardarla en la base de datos.</span><span class="sxs-lookup"><span data-stu-id="7e07d-161">In this section you create two Java classes for storing user data, and then you modify your main application class to create an instance of the user class and save it to your database.</span></span>

### <a name="define-a-basic-class-for-storing-user-data"></a><span data-ttu-id="7e07d-162">Definición de una clase básica para almacenar datos de usuario</span><span class="sxs-lookup"><span data-stu-id="7e07d-162">Define a basic class for storing user data</span></span>

1. <span data-ttu-id="7e07d-163">Cree un nuevo archivo llamado *User.java* en el mismo directorio que el archivo de Java de la aplicación principal.</span><span class="sxs-lookup"><span data-stu-id="7e07d-163">Create a new file named *User.java* in the same directory as your main application Java file.</span></span>

1. <span data-ttu-id="7e07d-164">Abra el archivo *User.java* en un editor de texto y agréguele las siguientes líneas para definir una clase de usuario genérica que almacene y recupere valores de la base de datos:</span><span class="sxs-lookup"><span data-stu-id="7e07d-164">Open the *User.java* file in a text editor, and add the following lines to the file to define a generic user class that stores and retrieve values in your database:</span></span>

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

1. <span data-ttu-id="7e07d-165">Guarde y cierre el archivo *User.java*.</span><span class="sxs-lookup"><span data-stu-id="7e07d-165">Save and close the *User.java* file.</span></span>

### <a name="define-a-data-repository-interface"></a><span data-ttu-id="7e07d-166">Definición de una interfaz del repositorio de datos</span><span class="sxs-lookup"><span data-stu-id="7e07d-166">Define a data repository interface</span></span>

1. <span data-ttu-id="7e07d-167">Cree un nuevo archivo llamado *UserRepository.java* en el mismo directorio que el archivo de Java de la aplicación principal.</span><span class="sxs-lookup"><span data-stu-id="7e07d-167">Create a new file named *UserRepository.java* in the same directory as your main application Java file.</span></span>

1. <span data-ttu-id="7e07d-168">Abra el archivo *UserRepository.java* en un editor de texto y agréguele las siguientes líneas para definir una interfaz de repositorio de usuario que extienda la interfaz predeterminada del repositorio de DocumentDB:</span><span class="sxs-lookup"><span data-stu-id="7e07d-168">Open the *UserRepository.java* file in a text editor, and add the following lines to the file to define a user repository interface that extends the default DocumentDB repository interface:</span></span>

   ```java
   package com.example.wingtiptoysdata;
   
   import com.microsoft.azure.spring.data.documentdb.repository.DocumentDbRepository;
   import org.springframework.stereotype.Repository;
   
   @Repository
   public interface UserRepository extends DocumentDbRepository<User, String> { } 
   ```

1. <span data-ttu-id="7e07d-169">Guarde y cierre el archivo *UserRepository.java*.</span><span class="sxs-lookup"><span data-stu-id="7e07d-169">Save and close the *UserRepository.java* file.</span></span>

### <a name="modify-the-main-application-class"></a><span data-ttu-id="7e07d-170">Modificación de la clase de aplicación principal</span><span class="sxs-lookup"><span data-stu-id="7e07d-170">Modify the main application class</span></span>

1. <span data-ttu-id="7e07d-171">Busque el archivo de Java de la aplicación principal en el directorio del paquete de la aplicación; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="7e07d-171">Locate the main application Java file in the package directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoysdata\src\main\java\com\example\wingtiptoysdata\WingtiptoysdataApplication.java`

   <span data-ttu-id="7e07d-172">O bien</span><span class="sxs-lookup"><span data-stu-id="7e07d-172">-or-</span></span>

   `/users/example/home/wingtiptoysdata/src/main/java/com/example/wingtiptoysdata/WingtiptoysdataApplication.java`

   ![Búsqueda del archivo de Java de la aplicación][JV01]

1. <span data-ttu-id="7e07d-174">Abra el archivo de Java de la aplicación principal en un editor de texto y agregue las siguientes líneas al archivo:</span><span class="sxs-lookup"><span data-stu-id="7e07d-174">Open the main application Java file in a text editor, and add the following lines to the file:</span></span>

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
   > <span data-ttu-id="7e07d-175">Si usa una de las versiones 1.5.n de Spring Boot para completar este tutorial, deberá remplazar la sintaxis `final User result = repository.findById(testUser.getId()).get();` por `final User result = repository.findOne(testUser.getId());`.</span><span class="sxs-lookup"><span data-stu-id="7e07d-175">If you are using one of Spring Boot 1.5.n versions to complete this tutorial, you will need to replace the `final User result = repository.findById(testUser.getId()).get();` syntax with `final User result = repository.findOne(testUser.getId());`.</span></span>
   >

1. <span data-ttu-id="7e07d-176">Guarde y cierre el archivo de Java de la aplicación principal.</span><span class="sxs-lookup"><span data-stu-id="7e07d-176">Save and close the main application Java file.</span></span>

## <a name="build-and-test-your-app"></a><span data-ttu-id="7e07d-177">Compilación y prueba de la aplicación</span><span class="sxs-lookup"><span data-stu-id="7e07d-177">Build and test your app</span></span>

1. <span data-ttu-id="7e07d-178">Abra un símbolo del sistema y cambie el directorio a la carpeta donde se encuentra el archivo *pom.xml*; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="7e07d-178">Open a command prompt and change directory to the folder where your *pom.xml* file is located; for example:</span></span>

   `cd C:\SpringBoot\wingtiptoysdata`

   <span data-ttu-id="7e07d-179">O bien</span><span class="sxs-lookup"><span data-stu-id="7e07d-179">-or-</span></span>

   `cd /users/example/home/wingtiptoysdata`

1. <span data-ttu-id="7e07d-180">Compile la aplicación de Spring Boot con Maven y ejecútela; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="7e07d-180">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. <span data-ttu-id="7e07d-181">La aplicación mostrará varios mensajes en tiempo de ejecución y mostrará un mensaje como el de los ejemplos siguientes, que indica que los valores se han almacenado y recuperado correctamente de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="7e07d-181">Your application will display several runtime messages, and it will display a message like the following examples to indicate that values have been successfully stored and retrieved from your database.</span></span>

   ```
   User: 20170724025215132 Gena Soto
   ```

   ![Salida correcta de la aplicación][JV02]

1. <span data-ttu-id="7e07d-183">OPCIONAL: Puede usar Azure Portal para ver el contenido de Azure Cosmos DB en la página de propiedades de la base de datos; para ello, haga clic en **Explorador de datos** y luego seleccione un elemento de la lista mostrada para ver el contenido.</span><span class="sxs-lookup"><span data-stu-id="7e07d-183">OPTIONAL: You can use the Azure portal to view the contents of your Azure Cosmos DB from the properties page for your database by clicking  **Data Explorer**, and then selecting and item from the displayed list to view the contents.</span></span>

   ![Uso del Explorador de documentos para ver los datos][JV03]

## <a name="next-steps"></a><span data-ttu-id="7e07d-185">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7e07d-185">Next steps</span></span>

<span data-ttu-id="7e07d-186">Para más información sobre el uso de Azure Cosmos DB y Java, consulte los siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="7e07d-186">For more information about using Azure Cosmos DB and Java, see the following articles:</span></span>

* <span data-ttu-id="7e07d-187">[Documentación sobre Azure Cosmos DB]</span><span class="sxs-lookup"><span data-stu-id="7e07d-187">[Azure Cosmos DB Documentation].</span></span>

* <span data-ttu-id="7e07d-188">[Azure Cosmos DB: creación una base de datos de documentos mediante Java y Azure Portal][Build a SQL API app with Java]</span><span class="sxs-lookup"><span data-stu-id="7e07d-188">[Azure Cosmos DB: Create a document database using Java and the Azure portal][Build a SQL API app with Java]</span></span>

* <span data-ttu-id="7e07d-189">[Spring Data para SQL API de Azure Cosmos DB]</span><span class="sxs-lookup"><span data-stu-id="7e07d-189">[Spring Data for Azure Cosmos DB SQL API]</span></span>

<span data-ttu-id="7e07d-190">Para obtener más información sobre el uso de aplicaciones de Spring Boot en Azure, consulte los siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="7e07d-190">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* <span data-ttu-id="7e07d-191">[Spring Boot Document DB Starter para Azure]</span><span class="sxs-lookup"><span data-stu-id="7e07d-191">[Spring Boot Document DB Starter for Azure]</span></span>

* [<span data-ttu-id="7e07d-192">Implementación de una aplicación de Spring Boot en Azure App Service</span><span class="sxs-lookup"><span data-stu-id="7e07d-192">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)

* [<span data-ttu-id="7e07d-193">Ejecución de una aplicación de Spring Boot en un clúster de Kubernetes en Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="7e07d-193">Running a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="7e07d-194">Para más información sobre el uso de Azure con Java, consulte [Azure para desarrolladores de Java] y [Herramientas de Java para Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="7e07d-194">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="7e07d-195">**[Spring Framework]** es una solución de código abierto que ayuda a los desarrolladores de Java a crear aplicaciones de nivel empresarial.</span><span class="sxs-lookup"><span data-stu-id="7e07d-195">The **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="7e07d-196">Uno de los proyectos más populares que se basa en esa plataforma es [Spring Boot], que proporciona un enfoque simplificado para crear aplicaciones de Java independientes.</span><span class="sxs-lookup"><span data-stu-id="7e07d-196">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="7e07d-197">Para ayudar a los desarrolladores a empezar con Spring Boot, puede encontrar varios paquetes de ejemplo de Spring Boot en <https://github.com/spring-guides/>.</span><span class="sxs-lookup"><span data-stu-id="7e07d-197">To help developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>.</span></span> <span data-ttu-id="7e07d-198">Además de elegir de la lista de proyectos básicos de Spring Boot, el **[Spring Initializr]** ayuda a los desarrolladores en los primeros pasos para crear aplicaciones de Spring Boot personalizadas.</span><span class="sxs-lookup"><span data-stu-id="7e07d-198">In addition to choosing from the list of basic Spring Boot projects, the **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>

<!-- URL List -->

[Documentación sobre Azure Cosmos DB]: /azure/cosmos-db/
[Azure Cosmos DB Documentation]: /azure/cosmos-db/
[Azure para desarrolladores de Java]: https://docs.microsoft.com/java/azure/
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Build a SQL API app with Java]: https://docs.microsoft.com/azure/cosmos-db/create-sql-api-java 
[Spring Data para SQL API de Azure Cosmos DB]: https://azure.microsoft.com/blog/spring-data-azure-cosmos-db-nosql-data-access-on-azure/
[Spring Data for Azure Cosmos DB SQL API]: https://azure.microsoft.com/blog/spring-data-azure-cosmos-db-nosql-data-access-on-azure/
[Spring Boot Document DB Starter para Azure]:https://github.com/Microsoft/azure-spring-boot-starters/tree/master/azure-documentdb-spring-boot-starter-sample
[Spring Boot Document DB Starter for Azure]:https://github.com/Microsoft/azure-spring-boot-starters/tree/master/azure-documentdb-spring-boot-starter-sample
[cuenta de Azure gratuita]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Herramientas de Java para Visual Studio Team Services]: https://azure.microsoft.com/services/devops/java/
[Java Tools for Visual Studio Team Services]: https://azure.microsoft.com/services/devops/java/
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
