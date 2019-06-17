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
ms.openlocfilehash: f00afbdd09ce617f863ed758f4bdddcb40701e27
ms.sourcegitcommit: 5bbf64121a99019207ed8cca29280fc5183c7314
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/12/2019
ms.locfileid: "66840836"
---
# <a name="how-to-use-the-spring-boot-starter-with-the-azure-cosmos-db-sql-api"></a><span data-ttu-id="59089-103">Uso de la utilidad Spring Boot Starter con SQL API de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="59089-103">How to use the Spring Boot Starter with the Azure Cosmos DB SQL API</span></span>

## <a name="overview"></a><span data-ttu-id="59089-104">Información general</span><span class="sxs-lookup"><span data-stu-id="59089-104">Overview</span></span>

<span data-ttu-id="59089-105">Azure Cosmos DB es un servicio de base de datos de distribución global que permite a los desarrolladores trabajar con datos mediante diversas API estándar, como SQL, MongoDB, Graph y Table.</span><span class="sxs-lookup"><span data-stu-id="59089-105">Azure Cosmos DB is a globally-distributed database service that allows developers to work with data using a variety of standard APIs, such as SQL, MongoDB, Graph, and Table APIs.</span></span> <span data-ttu-id="59089-106">Spring Boot Starter de Microsoft permite a los desarrolladores usar aplicaciones de Spring Boot que se integran fácilmente con Azure Cosmos DB mediante SQL API.</span><span class="sxs-lookup"><span data-stu-id="59089-106">Microsoft's Spring Boot Starter enables developers to use Spring Boot applications that easily integrate with Azure Cosmos DB by using the SQL API.</span></span>

<span data-ttu-id="59089-107">En este artículo se muestra cómo crear una base de datos de Azure Cosmos DB mediante Azure Portal, cómo usar **[Spring Initializr]** para crear una aplicación Spring Boot personalizada y, después, cómo agregar el [iniciador de Spring Boot para Cosmos DB en Azure] a su aplicación personalizada para almacenar datos en Azure Cosmos DB y recuperarlos mediante Spring Data y SQL API de Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="59089-107">This article demonstrates creating an Azure Cosmos DB using the Azure portal, then using the **[Spring Initializr]** to create a custom Spring Boot application, and then add the [Spring Boot Cosmos DB Starter for Azure] to your custom application to store data in and retrieve data from your Azure Cosmos DB by using Spring Data and the Cosmos DB SQL API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="59089-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="59089-108">Prerequisites</span></span>

<span data-ttu-id="59089-109">Los siguientes requisitos previos son necesarios para seguir los pasos descritos en este artículo:</span><span class="sxs-lookup"><span data-stu-id="59089-109">The following prerequisites are required in order to follow the steps in this article:</span></span>

* <span data-ttu-id="59089-110">Una suscripción de Azure. Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN] o registrarse para obtener una [cuenta de Azure gratuita].</span><span class="sxs-lookup"><span data-stu-id="59089-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="59089-111">Un kit de desarrollo de Java (JDK) admitido</span><span class="sxs-lookup"><span data-stu-id="59089-111">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="59089-112">Para más información sobre los JDK disponibles para desarrollar en Azure, consulte <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="59089-112">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>

## <a name="create-an-azure-cosmos-db-by-using-the-azure-portal"></a><span data-ttu-id="59089-113">Creación de una instancia de Azure Cosmos DB mediante Azure Portal</span><span class="sxs-lookup"><span data-stu-id="59089-113">Create an Azure Cosmos DB by using the Azure portal</span></span>

1. <span data-ttu-id="59089-114">Vaya a Azure Portal en <https://portal.azure.com/> y haga clic en **+Crear un recurso**.</span><span class="sxs-lookup"><span data-stu-id="59089-114">Browse to the Azure portal at <https://portal.azure.com/> and click **+Create a resource**.</span></span>

   ![Portal de Azure][AZ01]

1. <span data-ttu-id="59089-116">Haga clic en **Bases de datos** y luego haga clic en **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="59089-116">Click **Databases**, and then click **Azure Cosmos DB**.</span></span>

   ![Portal de Azure][AZ02]

1. <span data-ttu-id="59089-118">En la página **Azure Cosmos DB**, escriba la información siguiente:</span><span class="sxs-lookup"><span data-stu-id="59089-118">On the **Azure Cosmos DB** page, enter the following information:</span></span>

   * <span data-ttu-id="59089-119">Elija la **suscripción** que quiere usar para la base de datos.</span><span class="sxs-lookup"><span data-stu-id="59089-119">Choose the **Subscription** you want to use for your database.</span></span>
   * <span data-ttu-id="59089-120">Especifique si quiere crear un nuevo **grupo de recursos** para la base de datos o elija un grupo de recursos diferente.</span><span class="sxs-lookup"><span data-stu-id="59089-120">Specify whether to create a new **Resource group** for your database, or choose an existing resource group.</span></span>
   * <span data-ttu-id="59089-121">Escriba un **Nombre de cuenta** único, que usará como el URI de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="59089-121">Enter a unique **Account Name**, which you will use as the URI for your database.</span></span> <span data-ttu-id="59089-122">Por ejemplo: *wingtiptoysdata*.</span><span class="sxs-lookup"><span data-stu-id="59089-122">For example: *wingtiptoysdata*.</span></span>
   * <span data-ttu-id="59089-123">Elija **Core (SQL)** como API.</span><span class="sxs-lookup"><span data-stu-id="59089-123">Choose **Core (SQL)** for the API.</span></span>
   * <span data-ttu-id="59089-124">Especifique la **ubicación** de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="59089-124">Specify the **Location** for your database.</span></span>

   <span data-ttu-id="59089-125">Cuando haya especificado estas opciones, haga clic en **Revisar y crear** para crear la base de datos.</span><span class="sxs-lookup"><span data-stu-id="59089-125">When you have specified these options, click **Review + create** to create your database.</span></span>

   ![Portal de Azure][AZ03]

1. <span data-ttu-id="59089-127">Cuando se ha creado la base de datos, se muestra en el **panel** de Azure, así como en las páginas **Todos los recursos** y **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="59089-127">When your database has been created, it is listed on your Azure **Dashboard**, as well as under the **All Resources** and **Azure Cosmos DB** pages.</span></span> <span data-ttu-id="59089-128">Puede hacer clic en la base de datos en cualquiera de esas ubicaciones para abrir la página de propiedades de la caché.</span><span class="sxs-lookup"><span data-stu-id="59089-128">You can click on your database on any of those locations to open the properties page for your cache.</span></span>

   ![Portal de Azure][AZ04]

1. <span data-ttu-id="59089-130">Cuando se muestre la página de propiedades de la base de datos, haga clic en **Claves** y copie el identificador URI y las claves de acceso de la base de datos; usará estos valores en su aplicación de Spring Boot.</span><span class="sxs-lookup"><span data-stu-id="59089-130">When the properties page for your database is displayed, click **Keys** and copy your URI and access keys for your database; you will use these values in your Spring Boot application.</span></span>

   ![Portal de Azure][AZ05]

## <a name="create-a-simple-spring-boot-application-with-the-spring-initializr"></a><span data-ttu-id="59089-132">Creación de una aplicación sencilla de Spring Boot con Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="59089-132">Create a simple Spring Boot application with the Spring Initializr</span></span>

1. <span data-ttu-id="59089-133">Vaya a <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="59089-133">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="59089-134">Especifique que quiere generar un **Proyecto de Maven** con **Java**, indique la versión de **Spring Boot**, escriba los nombres de **Group** (Grupo) y **Artifact** (Artefacto) para la aplicación, agregue **Azure Support** (Compatibilidad con Azure) en las dependencias y, a continuación, haga clic en el botón **Generate Project** (Generar proyecto).</span><span class="sxs-lookup"><span data-stu-id="59089-134">Specify that you want to generate a **Maven Project** with **Java**, specify your **Spring Boot** version, enter the **Group** and **Artifact** names for your application, add **Azure Support** in the dependencies, and then click the button to **Generate Project**.</span></span>

   ![Opciones básicas de Spring Initializr][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="59089-136">Spring Initializr usa los nombres de **Group** (Grupo) y **Artifact** (Artefacto) para crear el nombre del paquete, por ejemplo: *com.example.wintiptoysdata*.</span><span class="sxs-lookup"><span data-stu-id="59089-136">The Spring Initializr uses the **Group** and **Artifact** names to create the package name; for example: *com.example.wintiptoysdata*.</span></span>
   >

1. <span data-ttu-id="59089-137">Cuando se le pida, descargue el proyecto en una ruta de acceso del equipo local y extraiga los archivos.</span><span class="sxs-lookup"><span data-stu-id="59089-137">When prompted, download the project to a path on your local computer and extract the files.</span></span>

   ![Extracción del proyecto personalizado de Spring Boot][SI02]

1. <span data-ttu-id="59089-139">Después de extraer los archivos en el sistema local, la aplicación sencilla de Spring Boot estará lista para editarla.</span><span class="sxs-lookup"><span data-stu-id="59089-139">After you have extracted the files on your local system, your simple Spring Boot application will be ready for editing.</span></span>

   ![Archivos de proyecto personalizados de Spring Boot][SI03]

## <a name="configure-your-spring-boot-application-to-use-the-azure-spring-boot-starter"></a><span data-ttu-id="59089-141">Configuración de la aplicación de Spring Boot para usar Azure Spring Boot Starter</span><span class="sxs-lookup"><span data-stu-id="59089-141">Configure your Spring Boot application to use the Azure Spring Boot Starter</span></span>

1. <span data-ttu-id="59089-142">Busque el archivo *pom.xml* en el directorio de la aplicación; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="59089-142">Locate the *pom.xml* file in the directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoysdata\pom.xml`

   <span data-ttu-id="59089-143">O bien</span><span class="sxs-lookup"><span data-stu-id="59089-143">-or-</span></span>

   `/users/example/home/wingtiptoysdata/pom.xml`

   ![Guarde el archivo pom.xml.][PM01]

1. <span data-ttu-id="59089-145">Abra el archivo *pom.xml* en un editor de texto y agregue las siguientes líneas a la lista de `<dependencies>`:</span><span class="sxs-lookup"><span data-stu-id="59089-145">Open the *pom.xml* file in a text editor, and add the following lines to list of `<dependencies>`:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-cosmosdb-spring-boot-starter</artifactId>
   </dependency>
   ```

   ![Edición del archivo pom.xml][PM02]

1. <span data-ttu-id="59089-147">Compruebe que la versión de Spring Boot es la que eligió al crear la aplicación con Spring Initializr; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="59089-147">Verify that the Spring Boot version is the version that you chose when you created your application with the Spring Initializr; for example:</span></span>

   ```xml
   <parent>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-parent</artifactId>
      <version>2.1.5.RELEASE</version>
      <relativePath/>
   </parent>
   ```

1. <span data-ttu-id="59089-148">Compruebe que usa la versión de los [iniciadores de Spring Boot para Azure](https://github.com/microsoft/azure-spring-boot) más reciente, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="59089-148">Verify that you use the most recent [Azure Spring Boot starters](https://github.com/microsoft/azure-spring-boot) version, for example:</span></span>

   ```xml
   <azure.version>2.1.6</azure.version>
   ```

1. <span data-ttu-id="59089-149">Guarde y cierre el archivo *pom.xml*.</span><span class="sxs-lookup"><span data-stu-id="59089-149">Save and close the *pom.xml* file.</span></span>

## <a name="configure-your-spring-boot-application-to-use-your-azure-cosmos-db"></a><span data-ttu-id="59089-150">Configuración de la aplicación de Spring Boot para usar su base de datos de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="59089-150">Configure your Spring Boot application to use your Azure Cosmos DB</span></span>

1. <span data-ttu-id="59089-151">Busque el archivo *application.properties* en el directorio *resources* de su aplicación; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="59089-151">Locate the *application.properties* file in the *resources* directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoysdata\src\main\resources\application.properties`

   <span data-ttu-id="59089-152">O bien</span><span class="sxs-lookup"><span data-stu-id="59089-152">-or-</span></span>

   `/users/example/home/wingtiptoysdata/src/main/resources/application.properties`

   ![Búsqueda del archivo application.properties][RE01]

1. <span data-ttu-id="59089-154">Abra el archivo *application.properties* en un editor de texto y agréguele las siguientes líneas; a continuación, sustituya los valores de ejemplo por las propiedades adecuadas de su base de datos:</span><span class="sxs-lookup"><span data-stu-id="59089-154">Open the *application.properties* file in a text editor, and add the following lines to the file, and replace the sample values with the appropriate properties for your database:</span></span>

   ```yaml
   # Specify the DNS URI of your Azure Cosmos DB.
   azure.cosmosdb.uri=https://wingtiptoys.documents.azure.com:443/

   # Specify the access key for your database.
   azure.cosmosdb.key=57686f6120447564652c20426f6220526f636b73==

   # Specify the name of your database.
   azure.cosmosdb.database=wingtiptoysdata
   ```

   ![Edición del archivo application.properties][RE02]

1. <span data-ttu-id="59089-156">Guarde y cierre el archivo *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="59089-156">Save and close the *application.properties* file.</span></span>

## <a name="add-sample-code-to-implement-basic-database-functionality"></a><span data-ttu-id="59089-157">Adición de ejemplo de código para implementar funcionalidad básica de base de datos</span><span class="sxs-lookup"><span data-stu-id="59089-157">Add sample code to implement basic database functionality</span></span>

<span data-ttu-id="59089-158">En esta sección, creará dos clases de Java para almacenar datos de usuario y, después, va a modificar la clase de aplicación principal para crear una instancia de la clase *User* y guardarla en la base de datos.</span><span class="sxs-lookup"><span data-stu-id="59089-158">In this section you create two Java classes for storing user data, and then you modify your main application class to create an instance of the *User* class and save it to your database.</span></span>

### <a name="define-a-base-class-for-storing-user-data"></a><span data-ttu-id="59089-159">Definición de una clase base para almacenar datos de usuario</span><span class="sxs-lookup"><span data-stu-id="59089-159">Define a base class for storing user data</span></span>

1. <span data-ttu-id="59089-160">Cree un nuevo archivo llamado *User.java* en el mismo directorio que el archivo de Java de la aplicación principal.</span><span class="sxs-lookup"><span data-stu-id="59089-160">Create a new file named *User.java* in the same directory as your main application Java file.</span></span>

1. <span data-ttu-id="59089-161">Abra el archivo *User.java* en un editor de texto y agréguele las siguientes líneas para definir una clase de usuario genérica que almacene y recupere valores de la base de datos:</span><span class="sxs-lookup"><span data-stu-id="59089-161">Open the *User.java* file in a text editor, and add the following lines to the file to define a generic user class that stores and retrieve values in your database:</span></span>

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

1. <span data-ttu-id="59089-162">Guarde y cierre el archivo *User.java*.</span><span class="sxs-lookup"><span data-stu-id="59089-162">Save and close the *User.java* file.</span></span>

### <a name="define-a-data-repository-interface"></a><span data-ttu-id="59089-163">Definición de una interfaz del repositorio de datos</span><span class="sxs-lookup"><span data-stu-id="59089-163">Define a data repository interface</span></span>

1. <span data-ttu-id="59089-164">Cree un nuevo archivo llamado *UserRepository.java* en el mismo directorio que el archivo de Java de la aplicación principal.</span><span class="sxs-lookup"><span data-stu-id="59089-164">Create a new file named *UserRepository.java* in the same directory as your main application Java file.</span></span>

1. <span data-ttu-id="59089-165">Abra el archivo *UserRepository.java* en un editor de texto y agréguele las siguientes líneas para definir una interfaz de repositorio de usuario que extienda la interfaz predeterminada del repositorio de DocumentDB:</span><span class="sxs-lookup"><span data-stu-id="59089-165">Open the *UserRepository.java* file in a text editor, and add the following lines to the file to define a user repository interface that extends the default DocumentDB repository interface:</span></span>

   ```java
   package com.example.wingtiptoysdata;

   import com.microsoft.azure.spring.data.cosmosdb.repository.DocumentDbRepository;
   import org.springframework.stereotype.Repository;

   @Repository
   public interface UserRepository extends DocumentDbRepository<User, String> { }
   ```

1. <span data-ttu-id="59089-166">Guarde y cierre el archivo *UserRepository.java*.</span><span class="sxs-lookup"><span data-stu-id="59089-166">Save and close the *UserRepository.java* file.</span></span>

### <a name="modify-the-main-application-class"></a><span data-ttu-id="59089-167">Modificación de la clase de aplicación principal</span><span class="sxs-lookup"><span data-stu-id="59089-167">Modify the main application class</span></span>

1. <span data-ttu-id="59089-168">Busque el archivo de Java de la aplicación principal en el directorio del paquete de la aplicación; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="59089-168">Locate the main application Java file in the package directory of your application, for example:</span></span>

   `C:\SpringBoot\wingtiptoysdata\src\main\java\com\example\wingtiptoysdata\WingtiptoysdataApplication.java`

   <span data-ttu-id="59089-169">O bien</span><span class="sxs-lookup"><span data-stu-id="59089-169">-or-</span></span>

   `/users/example/home/wingtiptoysdata/src/main/java/com/example/wingtiptoysdata/WingtiptoysdataApplication.java`

   ![Búsqueda del archivo de Java de la aplicación][JV01]

1. <span data-ttu-id="59089-171">Abra el archivo de Java de la aplicación principal en un editor de texto y agregue las siguientes líneas al archivo:</span><span class="sxs-lookup"><span data-stu-id="59089-171">Open the main application Java file in a text editor, and add the following lines to the file:</span></span>

   ```java
    package com.example.wingtiptoysdata;

    import org.springframework.boot.CommandLineRunner;
    import org.springframework.boot.SpringApplication;
    import org.springframework.boot.autoconfigure.SpringBootApplication;

    import java.util.Optional;
    import java.util.UUID;

    @SpringBootApplication
    public class WingtiptoysdataApplication implements CommandLineRunner {

        private final UserRepository repository;

        public WingtiptoysdataApplication(UserRepository repository) {
            this.repository = repository;
        }

        public static void main(String[] args) {
            // Execute the command line runner.
            SpringApplication.run(WingtiptoysdataApplication.class, args);
            System.exit(0);
        }

        public void run(String... args) throws Exception {
            // Create a unique identifier.
            String uuid = UUID.randomUUID().toString();

            // Create a new User class.
            final User testUser = new User(uuid, "John", "Doe");

            // For this example, remove all of the existing records.
            repository.deleteAll();

            // Save the User class to the Azure database.
            repository.save(testUser);

            // Retrieve the database record for the User class you just saved by ID.
            Optional<User> result = repository.findById(testUser.getId());

            // Display the results of the database record retrieval.
            System.out.println("\nSaved user is: " + result + "\n")
        }
    }
   ```

1. <span data-ttu-id="59089-172">Guarde y cierre el archivo de Java de la aplicación principal.</span><span class="sxs-lookup"><span data-stu-id="59089-172">Save and close the main application Java file.</span></span>

## <a name="build-and-test-your-app"></a><span data-ttu-id="59089-173">Compilación y prueba de la aplicación</span><span class="sxs-lookup"><span data-stu-id="59089-173">Build and test your app</span></span>

1. <span data-ttu-id="59089-174">Abra un símbolo del sistema y cambie el directorio a la carpeta donde se encuentra el archivo *pom.xml*; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="59089-174">Open a command prompt and change directory to the folder where your *pom.xml* file is located; for example:</span></span>

   `cd C:\SpringBoot\wingtiptoysdata`

   <span data-ttu-id="59089-175">O bien</span><span class="sxs-lookup"><span data-stu-id="59089-175">-or-</span></span>

   `cd /users/example/home/wingtiptoysdata`

1. <span data-ttu-id="59089-176">Compile la aplicación de Spring Boot con Maven y ejecútela; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="59089-176">Build your Spring Boot application with Maven and run it, for example:</span></span>

   ```shell
   mvnw clean spring-boot:run
   ```

1. <span data-ttu-id="59089-177">La aplicación mostrará varios mensajes en tiempo de ejecución y mostrará un mensaje como el de los ejemplos siguientes, que indica que los valores se han almacenado y recuperado correctamente de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="59089-177">Your application will display several runtime messages, and it will display a message like the following examples to indicate that values have been successfully stored and retrieved from your database.</span></span>

   ```shell
   Saved user is: Optional[User: 24093cb5-55fe-4d2c-b459-cb8bafdd39fe John Doe]
   ```

   ![Salida correcta de la aplicación][JV02]

1. <span data-ttu-id="59089-179">OPCIONAL: Puede usar Azure Portal para ver el contenido de Azure Cosmos DB en la página de propiedades de la base de datos; para ello, haga clic en **Explorador de datos** y luego seleccione un elemento de la lista mostrada para ver el contenido.</span><span class="sxs-lookup"><span data-stu-id="59089-179">OPTIONAL: You can use the Azure portal to view the contents of your Azure Cosmos DB from the properties page for your database by clicking  **Data Explorer**, and then selecting and item from the displayed list to view the contents.</span></span>

   ![Uso del Explorador de documentos para ver los datos][JV03]

## <a name="next-steps"></a><span data-ttu-id="59089-181">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="59089-181">Next steps</span></span>

<span data-ttu-id="59089-182">Para más información acerca de Spring y Azure, vaya al centro de documentación de Azure.</span><span class="sxs-lookup"><span data-stu-id="59089-182">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="59089-183">Spring en Azure</span><span class="sxs-lookup"><span data-stu-id="59089-183">Spring on Azure</span></span>](/java/azure/spring-framework)

### <a name="additional-resources"></a><span data-ttu-id="59089-184">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="59089-184">Additional Resources</span></span>

<span data-ttu-id="59089-185">Para más información sobre el uso de Azure Cosmos DB y Java, consulte los siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="59089-185">For more information about using Azure Cosmos DB and Java, see the following articles:</span></span>

* <span data-ttu-id="59089-186">[Documentación sobre Azure Cosmos DB]</span><span class="sxs-lookup"><span data-stu-id="59089-186">[Azure Cosmos DB Documentation].</span></span>

* <span data-ttu-id="59089-187">[Azure Cosmos DB: Creación de una base de datos de documentos mediante Java y Azure Portal][Build a SQL API app with Java]</span><span class="sxs-lookup"><span data-stu-id="59089-187">[Azure Cosmos DB: Create a document database using Java and the Azure portal][Build a SQL API app with Java]</span></span>

* <span data-ttu-id="59089-188">[Spring Data para SQL API de Azure Cosmos DB]</span><span class="sxs-lookup"><span data-stu-id="59089-188">[Spring Data for Azure Cosmos DB SQL API]</span></span>

<span data-ttu-id="59089-189">Para obtener más información sobre el uso de aplicaciones de Spring Boot en Azure, consulte los siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="59089-189">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* <span data-ttu-id="59089-190">[Iniciador de Spring Boot para Cosmos DB en Azure]</span><span class="sxs-lookup"><span data-stu-id="59089-190">[Spring Boot Cosmos DB Starter for Azure]</span></span>

* [<span data-ttu-id="59089-191">Implementación de una aplicación de Spring Boot en Azure App Service</span><span class="sxs-lookup"><span data-stu-id="59089-191">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)

* [<span data-ttu-id="59089-192">Ejecución de una aplicación de Spring Boot en un clúster de Kubernetes en Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="59089-192">Running a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="59089-193">Para más información sobre el uso de Azure con Java, consulte [Azure para desarrolladores de Java] y [Working with Azure DevOps and Java] (Trabajo con Azure DevOps y Java).</span><span class="sxs-lookup"><span data-stu-id="59089-193">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Working with Azure DevOps and Java].</span></span>

<span data-ttu-id="59089-194">**[Spring Framework]** es una solución de código abierto que ayuda a los desarrolladores de Java a crear aplicaciones de nivel empresarial.</span><span class="sxs-lookup"><span data-stu-id="59089-194">The **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="59089-195">Uno de los proyectos más populares que se basa en esa plataforma es [Spring Boot], que proporciona un enfoque simplificado para crear aplicaciones de Java independientes.</span><span class="sxs-lookup"><span data-stu-id="59089-195">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="59089-196">Para ayudar a los desarrolladores a empezar con Spring Boot, puede encontrar varios paquetes de ejemplo de Spring Boot en <https://github.com/spring-guides/>.</span><span class="sxs-lookup"><span data-stu-id="59089-196">To help developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>.</span></span> <span data-ttu-id="59089-197">Además de elegir de la lista de proyectos básicos de Spring Boot, el **[Spring Initializr]** ayuda a los desarrolladores en los primeros pasos para crear aplicaciones de Spring Boot personalizadas.</span><span class="sxs-lookup"><span data-stu-id="59089-197">In addition to choosing from the list of basic Spring Boot projects, the **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>

<!-- URL List -->

[Documentación sobre Azure Cosmos DB]: /azure/cosmos-db/
[Azure Cosmos DB Documentation]: /azure/cosmos-db/
[Azure para desarrolladores de Java]: /java/azure/
[Azure for Java Developers]: /java/azure/
[Build a SQL API app with Java]: /azure/cosmos-db/create-sql-api-java 
[Spring Data para SQL API de Azure Cosmos DB]: https://azure.microsoft.com/blog/spring-data-azure-cosmos-db-nosql-data-access-on-azure/
[Spring Data for Azure Cosmos DB SQL API]: https://azure.microsoft.com/blog/spring-data-azure-cosmos-db-nosql-data-access-on-azure/
[Iniciador de Spring Boot para Cosmos DB en Azure]: https://github.com/microsoft/azure-spring-boot/tree/master/azure-spring-boot-starters/azure-cosmosdb-spring-boot-starter
[Spring Boot Cosmos DB Starter for Azure]: https://github.com/microsoft/azure-spring-boot/tree/master/azure-spring-boot-starters/azure-cosmosdb-spring-boot-starter
[cuenta de Azure gratuita]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Working with Azure DevOps and Java]: https://azure.microsoft.com/services/devops/java/ (Trabajo con Azure DevOps y Java)
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
