---
title: Uso de Spring Data Gremlin Starter con SQL API de Azure Cosmos DB
description: Aprenda a configurar una aplicación creada con Spring Boot Initializer con SQL API de Azure Cosmos DB.
services: cosmos-db
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.date: 08/20/2018
ms.devlang: java
ms.service: cosmos-db
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: data-services
ms.openlocfilehash: 4e0138e3cc474b4c47d3bf492e696ec49ea3ef37
ms.sourcegitcommit: c2019ba6da6c7c28b17b5a85f89e49bb5e570ba4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2018
ms.locfileid: "44040273"
---
# <a name="how-to-use-the-spring-data-gremlin-starter-with-the-azure-cosmos-db-sql-api"></a><span data-ttu-id="ba40a-103">Uso de Spring Data Gremlin Starter con SQL API de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="ba40a-103">How to use the Spring Data Gremlin Starter with the Azure Cosmos DB SQL API</span></span>

## <a name="overview"></a><span data-ttu-id="ba40a-104">Información general</span><span class="sxs-lookup"><span data-stu-id="ba40a-104">Overview</span></span>

<span data-ttu-id="ba40a-105">Spring Data Gremlin Starter proporciona compatibilidad con Spring Data para el lenguaje de consultas Gremlin de Apache, que los desarrolladores pueden usar con cualquier almacén de datos compatibles con Gremlin.</span><span class="sxs-lookup"><span data-stu-id="ba40a-105">The Spring Data Gremlin Starter provides Spring Data support for the Gremlin query language from Apache, which developers can use with any Gremlin-compatible data store.</span></span>

<span data-ttu-id="ba40a-106">En este artículo se muestra cómo crear una base de datos de Azure Cosmos DB mediante Azure Portal para usarla con la API de Gremlin, cómo usar **[Spring Initializr]** para crear una aplicación Java personalizada y, después, cómo agregar la funcionalidad Spring Data Gremlin Starter a su aplicación personalizada para almacenar datos en Azure Cosmos DB y recuperarlos mediante Gremlin.</span><span class="sxs-lookup"><span data-stu-id="ba40a-106">This article demonstrates creating an Azure Cosmos DB by using the Azure portal for use with Gremlin API, then using the **[Spring Initializr]** to create a custom java application, and then add the Spring Data Gremlin Starter functionality to your custom application to store data in and retrieve data from your Azure Cosmos DB by using Gremlin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ba40a-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ba40a-107">Prerequisites</span></span>

<span data-ttu-id="ba40a-108">Los siguientes requisitos previos son necesarios para seguir los pasos descritos en este artículo:</span><span class="sxs-lookup"><span data-stu-id="ba40a-108">The following prerequisites are required in order to follow the steps in this article:</span></span>

* <span data-ttu-id="ba40a-109">Una suscripción de Azure. Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN] o registrarse para obtener una [cuenta de Azure gratuita].</span><span class="sxs-lookup"><span data-stu-id="ba40a-109">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="ba40a-110">Un [kit de desarrollo de Java (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), versión 1.7 o posterior.</span><span class="sxs-lookup"><span data-stu-id="ba40a-110">A [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 or later.</span></span>
* <span data-ttu-id="ba40a-111">[Apache Maven](http://maven.apache.org/), versión 3.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="ba40a-111">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

> [!IMPORTANT]
>
> <span data-ttu-id="ba40a-112">Se necesita Spring Boot versión 2.0 o posteriores para completar los pasos descritos en este artículo.</span><span class="sxs-lookup"><span data-stu-id="ba40a-112">Spring Boot version 2.0 or greater is required to complete the steps in this article.</span></span>
>

## <a name="create-an-azure-cosmos-db-using-the-azure-portal"></a><span data-ttu-id="ba40a-113">Creación de una base de datos de Azure Cosmos DB mediante Azure Portal</span><span class="sxs-lookup"><span data-stu-id="ba40a-113">Create an Azure Cosmos DB using the Azure portal</span></span>

### <a name="create-your-azure-cosmos-database-for-use-with-gremlin-api"></a><span data-ttu-id="ba40a-114">Creación de la base de datos de Azure Cosmos DB para su uso con la API de Gremlin</span><span class="sxs-lookup"><span data-stu-id="ba40a-114">Create your Azure Cosmos Database for use with Gremlin API</span></span>

1. <span data-ttu-id="ba40a-115">Vaya a Azure Portal en <https://portal.azure.com/> y haga clic en **+Crear un recurso**.</span><span class="sxs-lookup"><span data-stu-id="ba40a-115">Browse to the Azure portal at <https://portal.azure.com/> and click **+Create a resource**.</span></span>

   ![Creación de un recurso][AZ01]

1. <span data-ttu-id="ba40a-117">Haga clic en **Bases de datos** y luego haga clic en **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="ba40a-117">Click **Databases**, and then click **Azure Cosmos DB**.</span></span>

   ![Creación de una base de datos de Azure Cosmos DB][AZ02]

1. <span data-ttu-id="ba40a-119">En la página **Azure Cosmos DB**, escriba la información siguiente:</span><span class="sxs-lookup"><span data-stu-id="ba40a-119">On the **Azure Cosmos DB** page, enter the following information:</span></span>

   * <span data-ttu-id="ba40a-120">Escriba un **identificador** único, que usará como identificador URI de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="ba40a-120">Enter a unique **ID**, which you will use as part of the Gremlin URI for your database.</span></span> <span data-ttu-id="ba40a-121">Por ejemplo: si especificó **wingtiptoysdata** como valor de **ID**, el URI de Gremlin sería *wingtiptoysdata.gremlin.cosmosdb.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="ba40a-121">For example: if you entered **wingtiptoysdata** for the **ID**, the Gremlin URI would be *wingtiptoysdata.gremlin.cosmosdb.azure.com*.</span></span>
   * <span data-ttu-id="ba40a-122">Elija **Gremlin (Graph)** para la API.</span><span class="sxs-lookup"><span data-stu-id="ba40a-122">Choose **Gremlin (Graph)** for the API.</span></span>
   * <span data-ttu-id="ba40a-123">Elija la **suscripción** que quiere usar para la base de datos.</span><span class="sxs-lookup"><span data-stu-id="ba40a-123">Choose the **Subscription** you want to use for your database.</span></span>
   * <span data-ttu-id="ba40a-124">Especifique si quiere crear un nuevo **grupo de recursos** para la base de datos o elija un grupo de recursos diferente.</span><span class="sxs-lookup"><span data-stu-id="ba40a-124">Specify whether to create a new **Resource group** for your database, or choose an existing resource group.</span></span>
   * <span data-ttu-id="ba40a-125">Especifique la **ubicación** de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="ba40a-125">Specify the **Location** for your database.</span></span>
   
   <span data-ttu-id="ba40a-126">Cuando haya especificado estas opciones, haga clic en **Crear** para crear la base de datos.</span><span class="sxs-lookup"><span data-stu-id="ba40a-126">When you have specified these options, click **Create** to create your database.</span></span>

   ![Especificación de las opciones de Azure Cosmos DB][AZ03]

1. <span data-ttu-id="ba40a-128">Cuando se ha creado la base de datos, se muestra en el **panel** de Azure, así como en las páginas **Todos los recursos** y **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="ba40a-128">When your database has been created, it is listed on your Azure **Dashboard**, as well as under the **All Resources** and **Azure Cosmos DB** pages.</span></span> <span data-ttu-id="ba40a-129">Puede hacer clic en la base de datos en cualquiera de esas ubicaciones para abrir la página de propiedades de la caché.</span><span class="sxs-lookup"><span data-stu-id="ba40a-129">You can click on your database on any of those locations to open the properties page for your cache.</span></span>

   ![Todos los recursos][AZ04]

1. <span data-ttu-id="ba40a-131">Cuando se muestre la página de propiedades de la base de datos, haga clic en **Claves de acceso** y copie el identificador URI y las claves de acceso de la base de datos; usará estos valores en su aplicación de Spring Boot.</span><span class="sxs-lookup"><span data-stu-id="ba40a-131">When the properties page for your database is displayed, click **Access keys** and copy your URI and access keys for your database; you will use these values in your Spring Boot application.</span></span>

   ![Claves de acceso][AZ05]

### <a name="add-a-graph-to-your-azure-cosmos-database"></a><span data-ttu-id="ba40a-133">Adición de un gráfico a la base de datos de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="ba40a-133">Add a graph to your Azure Cosmos Database</span></span>

1. <span data-ttu-id="ba40a-134">Haga clic en **Explorador de datos** y después en **Nuevo grafo**.</span><span class="sxs-lookup"><span data-stu-id="ba40a-134">Click **Data Explorer**, and then click **New Graph**.</span></span>

   ![Nuevo grafo][AZ06]

1. <span data-ttu-id="ba40a-136">Cuando aparezca la página **Agregar grafo**, especifique la información siguiente:</span><span class="sxs-lookup"><span data-stu-id="ba40a-136">When the **Add Graph** is displayed, enter the following information:</span></span>

   * <span data-ttu-id="ba40a-137">Especifique un **Id. de base de datos** único para la base de datos.</span><span class="sxs-lookup"><span data-stu-id="ba40a-137">Specify a unique **Database id** for your database.</span></span>
   * <span data-ttu-id="ba40a-138">Especifique un **Id. de grafo** único para el grafo.</span><span class="sxs-lookup"><span data-stu-id="ba40a-138">Specify a unique **Graph id** for your graph.</span></span>
   * <span data-ttu-id="ba40a-139">Puede elegir especificar la **Capacidad de almacenamiento** o puede aceptar el valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="ba40a-139">You can choose to specify your **Storage capacity**, or you can accept the default.</span></span>
   * <span data-ttu-id="ba40a-140">Especifique el valor de **Rendimiento**; para este ejemplo, puede elegir 400 unidades de solicitud (RU).</span><span class="sxs-lookup"><span data-stu-id="ba40a-140">Specify your **Throughput**, and for this example you can choose 400 Request Units (RUs).</span></span>
   
   <span data-ttu-id="ba40a-141">Cuando haya especificado estas opciones, haga clic en **Crear** para crear el grafo.</span><span class="sxs-lookup"><span data-stu-id="ba40a-141">When you have specified these options, click **OK** to create your graph.</span></span>

   ![Agregar grafo][AZ07]

1. <span data-ttu-id="ba40a-143">Una vez creado el grafo, puede usar el **Explorador de datos** para verlo.</span><span class="sxs-lookup"><span data-stu-id="ba40a-143">After your graph has been created, you can use the **Data Explorer** to view it.</span></span>

   ![Visualización de las propiedades del grafo][AZ08]

## <a name="create-a-simple-spring-boot-application-with-the-spring-initializr"></a><span data-ttu-id="ba40a-145">Creación de una aplicación sencilla de Spring Boot con Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="ba40a-145">Create a simple Spring Boot application with the Spring Initializr</span></span>

1. <span data-ttu-id="ba40a-146">Vaya a <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="ba40a-146">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="ba40a-147">Especifique que quiere generar un proyecto de **Maven** con **Java**, escriba los nombres de **Group** (Grupo) y **Artifact** (Artefacto) de su aplicación, especifique en **Spring Boot** una versión que sea igual o posterior a 2.0 y, luego, haga clic en el botón **Generate Project** (Generar proyecto).</span><span class="sxs-lookup"><span data-stu-id="ba40a-147">Specify that you want to generate a **Maven** project with **Java**, enter the **Group** and **Artifact** names for your application, specify your **Spring Boot** version with a version that is equal to or greater than 2.0, and then click **Generate Project**.</span></span>

   ![Opciones básicas de Spring Initializr][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="ba40a-149">Spring Initializr usa los nombres de **Group** (Grupo) y **Artifact** (Artefacto) para crear el nombre del paquete, por ejemplo: \*com.example.wintiptoysdata.</span><span class="sxs-lookup"><span data-stu-id="ba40a-149">The Spring Initializr uses the **Group** and **Artifact** names to create the package name; for example: \*com.example.wintiptoysdata.</span></span>
   >

1. <span data-ttu-id="ba40a-150">Cuando se le solicite, descargue el proyecto en una ruta de acceso del equipo local.</span><span class="sxs-lookup"><span data-stu-id="ba40a-150">When prompted, download the project to a path on your local computer.</span></span>

   ![Descarga del proyecto personalizado de Spring Boot][SI02]

1. <span data-ttu-id="ba40a-152">Después de extraer los archivos en el sistema local, la aplicación sencilla de Spring Boot estará lista para editarla.</span><span class="sxs-lookup"><span data-stu-id="ba40a-152">After you have extracted the files on your local system, your simple Spring Boot application will be ready for editing.</span></span>

   ![Archivos de proyecto personalizados de Spring Boot][SI03]

## <a name="configure-your-spring-boot-app-to-use-the-spring-data-gremlin-starter"></a><span data-ttu-id="ba40a-154">Configuración de la aplicación de Spring Boot para usar Spring Data Gremlin Starter</span><span class="sxs-lookup"><span data-stu-id="ba40a-154">Configure your Spring Boot app to use the Spring Data Gremlin Starter</span></span>

1. <span data-ttu-id="ba40a-155">Busque el archivo *pom.xml* en el directorio de la aplicación; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="ba40a-155">Locate the *pom.xml* file in the directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoysdata\pom.xml`

   <span data-ttu-id="ba40a-156">O bien</span><span class="sxs-lookup"><span data-stu-id="ba40a-156">-or-</span></span>

   `/users/example/home/wingtiptoysdata/pom.xml`

   ![Guarde el archivo pom.xml.][PM01]

1. <span data-ttu-id="ba40a-158">Abra el archivo *pom.xml* en un editor de texto y agregue Spring Data Gremlin Starter a la lista `<dependencies>`:</span><span class="sxs-lookup"><span data-stu-id="ba40a-158">Open the *pom.xml* file in a text editor, and add the Spring Data Gremlin Starter to list of `<dependencies>`:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.spring.data.gremlin</groupId>
      <artifactId>spring-data-gremlin</artifactId>
      <version>2.0.0</version>
   </dependency>
   ```

   ![Edición del archivo pom.xml][PM02]

1. <span data-ttu-id="ba40a-160">Guarde y cierre el archivo *pom.xml*.</span><span class="sxs-lookup"><span data-stu-id="ba40a-160">Save and close the *pom.xml* file.</span></span>

## <a name="configure-your-spring-boot-app-to-use-your-azure-cosmos-db"></a><span data-ttu-id="ba40a-161">Configuración de la aplicación de Spring Boot para usar Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="ba40a-161">Configure your Spring Boot app to use your Azure Cosmos DB</span></span>

1. <span data-ttu-id="ba40a-162">Busque el directorio *resources* de la aplicación y cree un nuevo archivo llamado *application.yml*.</span><span class="sxs-lookup"><span data-stu-id="ba40a-162">Locate the *resources* directory of your app, and create a new file named *application.yml*.</span></span> <span data-ttu-id="ba40a-163">Por ejemplo: </span><span class="sxs-lookup"><span data-stu-id="ba40a-163">For example:</span></span>

   `C:\SpringBoot\wingtiptoysdata\src\main\resources\application.yml`

   <span data-ttu-id="ba40a-164">O bien</span><span class="sxs-lookup"><span data-stu-id="ba40a-164">-or-</span></span>

   `/users/example/home/wingtiptoysdata/src/main/resources/application.yml`

   ![Creación del archivo application.yml][RE01]

1.  <span data-ttu-id="ba40a-166">Abra el archivo *application.yml* en un editor de texto y agréguele las siguientes líneas; a continuación, sustituya los valores de ejemplo por las propiedades adecuadas de su base de datos:</span><span class="sxs-lookup"><span data-stu-id="ba40a-166">Open the *application.yml* file in a text editor, and add the following lines to the file, and replace the sample values with the appropriate properties for your database:</span></span>

   ```yaml
   gremlin:
      endpoint: wingtiptoys.gremlin.cosmosdb.azure.com
      port: 443
      username: /dbs/wingtiptoysdb/colls/wingtiptoysgraph
      password: 57686f6120447564652c20426f6220526f636b73==
      telemetryAllowed: false
   ```
   <span data-ttu-id="ba40a-167">Donde:</span><span class="sxs-lookup"><span data-stu-id="ba40a-167">Where:</span></span>
   | <span data-ttu-id="ba40a-168">Campo</span><span class="sxs-lookup"><span data-stu-id="ba40a-168">Field</span></span> | <span data-ttu-id="ba40a-169">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="ba40a-169">Description</span></span> |
   | ---|---|
   | `endpoint` | <span data-ttu-id="ba40a-170">Especifica el URI de Gremlin para la base de datos, que deriva del **ID** único que especificó al crear la base de datos de Azure Cosmos DB anteriormente en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="ba40a-170">Specifies the Gremlin URI for your database, which is derived from the unique **ID** that you specified when you created your Azure Cosmos DB earlier in this tutorial.</span></span> |
   | `port` | <span data-ttu-id="ba40a-171">Especifica el puerto TCP/IP, que debería ser **443** para HTTPS.</span><span class="sxs-lookup"><span data-stu-id="ba40a-171">Specifies the TCP/IP port, which should be **443** for HTTPS.</span></span> |
   | `username` | <span data-ttu-id="ba40a-172">Especifica los valores únicos **Id. de base de datos** e **Id. de grafo** que usó al agregar el grafo anteriormente en este tutorial; debe especificarse con la siguiente sintaxis: "/dbs/**{id. de base de datos}**/colls/**{id. de grafo}**".</span><span class="sxs-lookup"><span data-stu-id="ba40a-172">Specifies the unique **Database id** and **Graph id** that you used when you added your graph earlier in this tutorial; this must be entered using the following syntax: "/dbs/**{Database id}**/colls/**{Graph id}**".</span></span> |
   | `password` | <span data-ttu-id="ba40a-173">Especifica la **clave de acceso** principal o secundario que copió anteriormente en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="ba40a-173">Specifies either the primary or secondary **Access key** that you copied earlier in this tutorial.</span></span> |
   | `telemetryAllowed` | <span data-ttu-id="ba40a-174">Especifique **true** si desea habilitar los datos de telemetría; en caso contrario, **false**.</span><span class="sxs-lookup"><span data-stu-id="ba40a-174">Specify **true** if you want to enable telemetry; otherwise, **false**.</span></span>

1. <span data-ttu-id="ba40a-175">Guarde y cierre el archivo *application.yml*.</span><span class="sxs-lookup"><span data-stu-id="ba40a-175">Save and close the *application.yml* file.</span></span>

## <a name="add-sample-code-to-implement-basic-database-functionality"></a><span data-ttu-id="ba40a-176">Adición de ejemplo de código para implementar funcionalidad básica de base de datos</span><span class="sxs-lookup"><span data-stu-id="ba40a-176">Add sample code to implement basic database functionality</span></span>

<span data-ttu-id="ba40a-177">En esta sección, creará las clases de Java necesarias para almacenar datos en la base de datos.</span><span class="sxs-lookup"><span data-stu-id="ba40a-177">In this section, you create the necessary Java classes for storing data in your database.</span></span>

### <a name="modify-the-main-application-class"></a><span data-ttu-id="ba40a-178">Modificación de la clase de aplicación principal</span><span class="sxs-lookup"><span data-stu-id="ba40a-178">Modify the main application class</span></span>

1. <span data-ttu-id="ba40a-179">Busque el archivo de Java de la aplicación principal en el directorio del paquete de la aplicación; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="ba40a-179">Locate the main application Java file in the package directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoysdata\src\main\java\com\example\wingtiptoysdata\WingtiptoysdataApplication.java`

   <span data-ttu-id="ba40a-180">O bien</span><span class="sxs-lookup"><span data-stu-id="ba40a-180">-or-</span></span>

   `/users/example/home/wingtiptoysdata/src/main/java/com/example/wingtiptoysdata/WingtiptoysdataApplication.java`

   ![Búsqueda del archivo de Java de la aplicación][JV01]

1. <span data-ttu-id="ba40a-182">Abra el archivo de Java de la aplicación principal en un editor de texto y agregue las siguientes líneas al archivo:</span><span class="sxs-lookup"><span data-stu-id="ba40a-182">Open the main application Java file in a text editor, and add the following lines to the file:</span></span>

   ```java
   package com.example.wingtiptoysdata;
   
   // These imports are required for the application.
   import com.microsoft.spring.data.gremlin.common.GremlinFactory;
   import com.example.wingtiptoysdata.domain.Network;
   import com.example.wingtiptoysdata.domain.Person;
   import com.example.wingtiptoysdata.domain.Relation;
   import com.example.wingtiptoysdata.repository.NetworkRepository;
   import com.example.wingtiptoysdata.repository.PersonRepository;
   import com.example.wingtiptoysdata.repository.RelationRepository;
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;
   import javax.annotation.PostConstruct;
   import javax.annotation.PreDestroy;
   
   @SpringBootApplication
   public class WingtiptoysdataApplication {
   
       // Define several person classes to store personal data.
       private final Person person1 = new Person("01", "Nellie Hughes", "23");
       private final Person person2 = new Person("02", "Delmar Alfred", "34");
       private final Person person3 = new Person("03", "Kelley Hunter", "45");
       private final Person person4 = new Person("04", "Roscoe Guerin", "56");
       private final Person person5 = new Person("05", "Gracie Chavez", "67");
   
       // Define relationship classes to define the relationships between some of the persons.
       private final Relation relation1 = new Relation("0102", "siblings", person1, person2);
       private final Relation relation2 = new Relation("0203", "coworkers", person2, person3);
       private final Relation relation3 = new Relation("0301", "parent", person3, person1);
       private final Relation relation4 = new Relation("0302", "parent", person3, person2);
       private final Relation relation5 = new Relation("0501", "grandparent", person5, person1);
       private final Relation relation6 = new Relation("0502", "grandparent", person5, person2);
   
       // Define the network.
       private final Network network = new Network();
   
       // Autowire the repositories and factory.
       @Autowired
       private PersonRepository personRepo;
       @Autowired
       private RelationRepository relationRepo;
       @Autowired
       private NetworkRepository networkRepo;
       @Autowired
       private GremlinFactory factory;
   
       // Run the Spring application and exit.
    public static void main(String[] args) {
           SpringApplication.run(WingtiptoysdataApplication.class, args);
           System.exit(0);
    }
   
       // Perform post-construct operations.    
       @PostConstruct
       public void setup() {
           // Delete any existing data from the database.
           this.networkRepo.deleteAll();
   
           // Add the relationship classes as edges.
           this.network.getEdges().add(this.relation1);
           this.network.getEdges().add(this.relation2);
           this.network.getEdges().add(this.relation3);
           this.network.getEdges().add(this.relation4);
           this.network.getEdges().add(this.relation5);
           this.network.getEdges().add(this.relation6);
   
           // Add the person classes as vertices.
           this.network.getVertexes().add(this.person1);
           this.network.getVertexes().add(this.person2);
           this.network.getVertexes().add(this.person3);
           this.network.getVertexes().add(this.person4);
           this.network.getVertexes().add(this.person5);
   
           // Save the network.
           this.networkRepo.save(this.network);
       }
   }
   ```

1. <span data-ttu-id="ba40a-183">Guarde y cierre el archivo de Java de la aplicación principal.</span><span class="sxs-lookup"><span data-stu-id="ba40a-183">Save and close the main application Java file.</span></span>

### <a name="define-a-basic-class-for-storing-configuration-information"></a><span data-ttu-id="ba40a-184">Definición de una clase básica para almacenar información de configuración</span><span class="sxs-lookup"><span data-stu-id="ba40a-184">Define a basic class for storing configuration information</span></span>

1. <span data-ttu-id="ba40a-185">Cree una carpeta llamada *config* en el directorio del paquete de la aplicación; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="ba40a-185">Create a folder named *config* under the package directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoysdata\src\main\java\com\example\wingtiptoysdata\config`

   <span data-ttu-id="ba40a-186">O bien</span><span class="sxs-lookup"><span data-stu-id="ba40a-186">-or-</span></span>

   `/users/example/home/wingtiptoysdata/src/main/java/com/example/wingtiptoysdata/config`

1. <span data-ttu-id="ba40a-187">Cree un archivo Java nuevo llamado *UserRepositoryConfiguration.java* en el directorio *config*; a continuación, abra el archivo en un editor de texto y agregue las siguientes líneas:</span><span class="sxs-lookup"><span data-stu-id="ba40a-187">Create a new Java file named *UserRepositoryConfiguration.java* in the *config* directory, then open the file in a text editor, and add the following lines:</span></span>

   ```java
   package com.example.wingtiptoysdata.config;

   import com.microsoft.spring.data.gremlin.common.GremlinConfiguration;
   import com.microsoft.spring.data.gremlin.common.GremlinFactory;
   import com.microsoft.spring.data.gremlin.config.AbstractGremlinConfiguration;
   import com.microsoft.spring.data.gremlin.repository.config.EnableGremlinRepositories;
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.boot.context.properties.EnableConfigurationProperties;
   import org.springframework.context.annotation.Bean;
   import org.springframework.context.annotation.Configuration;
   import org.springframework.context.annotation.PropertySource;
   
   @Configuration
   @EnableGremlinRepositories(basePackages = "com.example.wingtiptoysdata.repository")
   @EnableConfigurationProperties(GremlinConfiguration.class)
   @PropertySource("classpath:application.yml")
   public class UserRepositoryConfiguration extends AbstractGremlinConfiguration {
   
       @Autowired
       private GremlinConfiguration config;
   
       @Override
       public GremlinConfiguration getGremlinConfiguration() {
           return this.config;
       }
   }
   ```

1. <span data-ttu-id="ba40a-188">Guarde y cierre el archivo *UserRepositoryConfiguration.java*.</span><span class="sxs-lookup"><span data-stu-id="ba40a-188">Save and close the *UserRepositoryConfiguration.java* file.</span></span>

### <a name="define-a-set-of-classes-that-define-the-elements-of-your-graph-database"></a><span data-ttu-id="ba40a-189">Definición del conjunto de clases que definen los elementos de la base de datos de grafos</span><span class="sxs-lookup"><span data-stu-id="ba40a-189">Define a set of classes that define the elements of your graph database</span></span>

1. <span data-ttu-id="ba40a-190">Cree una carpeta llamada *domain* en el directorio del paquete de la aplicación; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="ba40a-190">Create a folder named *domain* under the package directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoysdata\src\main\java\com\example\wingtiptoysdata\domain`

   <span data-ttu-id="ba40a-191">O bien</span><span class="sxs-lookup"><span data-stu-id="ba40a-191">-or-</span></span>

   `/users/example/home/wingtiptoysdata/src/main/java/com/example/wingtiptoysdata/domain`

1. <span data-ttu-id="ba40a-192">Cree un archivo Java nuevo llamado *Person.java* en el directorio *domain*; a continuación, abra el archivo en un editor de texto y agregue las siguientes líneas:</span><span class="sxs-lookup"><span data-stu-id="ba40a-192">Create a new Java file named *Person.java* in the *domain* directory, then open the file in a text editor and add the following lines:</span></span>

   ```java
   package com.example.wingtiptoysdata.domain;
   
   import com.microsoft.spring.data.gremlin.annotation.Vertex;
   import lombok.AllArgsConstructor;
   import lombok.Data;
   import lombok.NoArgsConstructor;
   import org.springframework.data.annotation.Id;
   
   @Data
   @Vertex
   @AllArgsConstructor
   @NoArgsConstructor
   public class Person {
   
       @Id
       private String id;
   
       private String name;
   
       private String age;
   }
   ```

1. <span data-ttu-id="ba40a-193">Guarde y cierre el archivo *Person.java*.</span><span class="sxs-lookup"><span data-stu-id="ba40a-193">Save and close the *Person.java* file.</span></span>

1. <span data-ttu-id="ba40a-194">Cree un archivo Java nuevo llamado *Relation.java* en el directorio *domain*; a continuación, abra el archivo en un editor de texto y agregue las siguientes líneas:</span><span class="sxs-lookup"><span data-stu-id="ba40a-194">Create a new Java file named *Relation.java* in the *domain* directory, then open the file in a text editor and add the following lines:</span></span>

   ```java
   package com.example.wingtiptoysdata.domain;
   
   import com.microsoft.spring.data.gremlin.annotation.Edge;
   import com.microsoft.spring.data.gremlin.annotation.EdgeFrom;
   import com.microsoft.spring.data.gremlin.annotation.EdgeTo;
   import lombok.AllArgsConstructor;
   import lombok.Data;
   import lombok.NoArgsConstructor;
   import org.springframework.data.annotation.Id;
   
   @Data
   @Edge
   @AllArgsConstructor
   @NoArgsConstructor
   public class Relation {
   
       @Id
       private String id;
   
       private String name;
   
       @EdgeFrom
       private Person personFrom;
   
       @EdgeTo
       private Person personTo;
   }
   ```

1. <span data-ttu-id="ba40a-195">Guarde y cierre el archivo *Relation.java*.</span><span class="sxs-lookup"><span data-stu-id="ba40a-195">Save and close the *Relation.java* file.</span></span>

1. <span data-ttu-id="ba40a-196">Cree un archivo Java nuevo llamado *Network.java* en el directorio *domain*; a continuación, abra el archivo en un editor de texto y agregue las siguientes líneas:</span><span class="sxs-lookup"><span data-stu-id="ba40a-196">Create a new Java file named *Network.java* in the *domain* directory, then open the file in a text editor and add the following lines:</span></span>

   ```java
   package com.example.wingtiptoysdata.domain;
   
   import com.microsoft.spring.data.gremlin.annotation.EdgeSet;
   import com.microsoft.spring.data.gremlin.annotation.Graph;
   import com.microsoft.spring.data.gremlin.annotation.VertexSet;
   import lombok.Getter;
   import org.springframework.data.annotation.Id;
   
   import java.util.ArrayList;
   import java.util.List;
   
   @Graph
   public class Network {
   
       @Id
       private String id;
   
       public Network() {
           this.edges = new ArrayList<Object>();
           this.vertexes = new ArrayList<Object>();
       }
   
       @EdgeSet
       @Getter
       private List<Object> edges;
   
       @VertexSet
       @Getter
       private List<Object> vertexes;
   }
   ```

1. <span data-ttu-id="ba40a-197">Guarde y cierre el archivo *Network.java*.</span><span class="sxs-lookup"><span data-stu-id="ba40a-197">Save and close the *Network.java* file.</span></span>

### <a name="define-a-set-of-classes-that-define-the-repositories-for-your-graph-database"></a><span data-ttu-id="ba40a-198">Definición del conjunto de clases que definen los repositorios de la base de datos de grafos</span><span class="sxs-lookup"><span data-stu-id="ba40a-198">Define a set of classes that define the repositories for your graph database</span></span>

1. <span data-ttu-id="ba40a-199">Cree una carpeta llamada *repository* en el directorio del paquete de la aplicación; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="ba40a-199">Create a folder named *repository* under the package directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoysdata\src\main\java\com\example\wingtiptoysdata\repository`

   <span data-ttu-id="ba40a-200">O bien</span><span class="sxs-lookup"><span data-stu-id="ba40a-200">-or-</span></span>

   `/users/example/home/wingtiptoysdata/src/main/java/com/example/wingtiptoysdata/repository`

1. <span data-ttu-id="ba40a-201">Cree un archivo Java nuevo llamado *NetworkRepository.java* en el directorio *repository*; a continuación, abra el archivo en un editor de texto y agregue las siguientes líneas:</span><span class="sxs-lookup"><span data-stu-id="ba40a-201">Create a new Java file named *NetworkRepository.java* in the *repository* directory, then open the file in a text editor and add the following lines:</span></span>

   ```java
   package com.example.wingtiptoysdata.repository;
   
   import com.microsoft.spring.data.gremlin.repository.GremlinRepository;
   import com.example.wingtiptoysdata.domain.Network;
   import org.springframework.stereotype.Repository;
   
   @Repository
   public interface NetworkRepository extends GremlinRepository<Network, String> {
   }
   ```

1. <span data-ttu-id="ba40a-202">Guarde y cierre el archivo *NetworkRepository.java*.</span><span class="sxs-lookup"><span data-stu-id="ba40a-202">Save and close the *NetworkRepository.java* file.</span></span>

1. <span data-ttu-id="ba40a-203">Cree un archivo Java nuevo llamado *PersonRepository.java* en el directorio *repository*; a continuación, abra el archivo en un editor de texto y agregue las siguientes líneas:</span><span class="sxs-lookup"><span data-stu-id="ba40a-203">Create a new Java file named *PersonRepository.java* in the *repository* directory, then open the file in a text editor and add the following lines:</span></span>

   ```java
   package com.example.wingtiptoysdata.repository;
   
   import com.microsoft.spring.data.gremlin.repository.GremlinRepository;
   import com.example.wingtiptoysdata.domain.Person;
   import org.springframework.stereotype.Repository;
   
   @Repository
   public interface PersonRepository extends GremlinRepository<Person, String> {
   }
   ```

1. <span data-ttu-id="ba40a-204">Guarde y cierre el archivo *PersonRepository.java*.</span><span class="sxs-lookup"><span data-stu-id="ba40a-204">Save and close the *PersonRepository.java* file.</span></span>

1. <span data-ttu-id="ba40a-205">Cree un archivo Java nuevo llamado *RelationRepository.java* en el directorio *repository*; a continuación, abra el archivo en un editor de texto y agregue las siguientes líneas:</span><span class="sxs-lookup"><span data-stu-id="ba40a-205">Create a new Java file named *RelationRepository.java* in the *repository* directory, then open the file in a text editor and add the following lines:</span></span>

   ```java
   package com.example.wingtiptoysdata.repository;
   
   import com.microsoft.spring.data.gremlin.repository.GremlinRepository;
   import com.example.wingtiptoysdata.domain.Relation;
   import org.springframework.stereotype.Repository;
   
   @Repository
   public interface RelationRepository extends GremlinRepository<Relation, String> {
   }
   ```

1. <span data-ttu-id="ba40a-206">Guarde y cierre el archivo *RelationRepository.java*.</span><span class="sxs-lookup"><span data-stu-id="ba40a-206">Save and close the *RelationRepository.java* file.</span></span>

## <a name="build-and-test-your-app"></a><span data-ttu-id="ba40a-207">Compilación y prueba de la aplicación</span><span class="sxs-lookup"><span data-stu-id="ba40a-207">Build and test your app</span></span>

1. <span data-ttu-id="ba40a-208">Abra un símbolo del sistema y cambie el directorio a la carpeta donde se encuentra el archivo *pom.xml*; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="ba40a-208">Open a command prompt and change directory to the folder where your *pom.xml* file is located; for example:</span></span>

   `cd C:\SpringBoot\wingtiptoysdata`

   <span data-ttu-id="ba40a-209">O bien</span><span class="sxs-lookup"><span data-stu-id="ba40a-209">-or-</span></span>

   `cd /users/example/home/wingtiptoysdata`

1. <span data-ttu-id="ba40a-210">Compile la aplicación de Spring Boot con Maven y ejecútela; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="ba40a-210">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. <span data-ttu-id="ba40a-211">La aplicación mostrará varios mensajes en tiempo de ejecución y, si no hay errores, puede usar Azure Portal para ver el contenido de su base de datos de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="ba40a-211">Your application will display several runtime messages, and if there were no errors, you can use the Azure portal to view the contents of your Azure Cosmos DB.</span></span> <span data-ttu-id="ba40a-212">Para ello, haga clic en el **Explorador de datos** en la página de propiedades de la base de datos, a continuación, haga clic en **Ejecutar consulta de Gremlin** y, a continuación, seleccione un elemento de la lista de resultados para ver los datos.</span><span class="sxs-lookup"><span data-stu-id="ba40a-212">To do so, click **Data Explorer** on the properties page for your database, then click **Execute Gremlin Query**, and then select an item from the list of results to view the data.</span></span>

   ![Uso del Explorador de documentos para ver los datos][JV03]

## <a name="next-steps"></a><span data-ttu-id="ba40a-214">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ba40a-214">Next steps</span></span>

<span data-ttu-id="ba40a-215">Consulte los siguientes artículos para más información sobre la compatibilidad de Azure para Gremlin y Graph API:</span><span class="sxs-lookup"><span data-stu-id="ba40a-215">For more information about Azure support for Gremlin and Graph API, see the following articles:</span></span>

* [<span data-ttu-id="ba40a-216">Introducción a Graph API de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="ba40a-216">Introduction to Azure Cosmos DB: Graph API</span></span>](https://docs.microsoft.com/azure/cosmos-db/graph-introduction)

* [<span data-ttu-id="ba40a-217">Compatibilidad de Azure Cosmos DB con grafos de Gremlin</span><span class="sxs-lookup"><span data-stu-id="ba40a-217">Azure Cosmos DB Gremlin graph support</span></span>](https://docs.microsoft.com/azure/cosmos-db/gremlin-support)

* [<span data-ttu-id="ba40a-218">Azure Cosmos DB: creación una base de datos de grafos mediante Java y Azure Portal</span><span class="sxs-lookup"><span data-stu-id="ba40a-218">Azure Cosmos DB: Create a graph database using Java and the Azure portal</span></span>](https://docs.microsoft.com/azure/cosmos-db/create-graph-java)

* [<span data-ttu-id="ba40a-219">Tutorial: Consulta de Graph API de Azure Cosmos DB mediante Gremlin</span><span class="sxs-lookup"><span data-stu-id="ba40a-219">Tutorial: Query Azure Cosmos DB Graph API by using Gremlin</span></span>](https://docs.microsoft.com/azure/cosmos-db/tutorial-query-graph)

* <span data-ttu-id="ba40a-220">[Spring Data Gremlin Starter]</span><span class="sxs-lookup"><span data-stu-id="ba40a-220">[Spring Data Gremlin Starter]</span></span>

<span data-ttu-id="ba40a-221">Para más información sobre el uso de Azure Cosmos DB y Java, consulte los siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="ba40a-221">For more information about using Azure Cosmos DB and Java, see the following articles:</span></span>

* <span data-ttu-id="ba40a-222">[Documentación sobre Azure Cosmos DB]</span><span class="sxs-lookup"><span data-stu-id="ba40a-222">[Azure Cosmos DB Documentation].</span></span>

* <span data-ttu-id="ba40a-223">[Azure Cosmos DB: creación una base de datos de documentos mediante Java y Azure Portal][Build a SQL API app with Java]</span><span class="sxs-lookup"><span data-stu-id="ba40a-223">[Azure Cosmos DB: Create a document database using Java and the Azure portal][Build a SQL API app with Java]</span></span>

* <span data-ttu-id="ba40a-224">[Spring Data para SQL API de Azure Cosmos DB]</span><span class="sxs-lookup"><span data-stu-id="ba40a-224">[Spring Data for Azure Cosmos DB SQL API]</span></span>

<span data-ttu-id="ba40a-225">Para obtener más información sobre el uso de aplicaciones de Spring Boot en Azure, consulte los siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="ba40a-225">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="ba40a-226">Implementación de una aplicación de Spring Boot en Azure App Service</span><span class="sxs-lookup"><span data-stu-id="ba40a-226">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)

* [<span data-ttu-id="ba40a-227">Ejecución de una aplicación de Spring Boot en un clúster de Kubernetes en Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="ba40a-227">Running a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="ba40a-228">Para más información sobre el uso de Azure con Java, consulte [Azure para desarrolladores de Java] y [Herramientas de Java para Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="ba40a-228">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="ba40a-229">**[Spring Framework]** es una solución de código abierto que ayuda a los desarrolladores de Java a crear aplicaciones de nivel empresarial.</span><span class="sxs-lookup"><span data-stu-id="ba40a-229">The **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="ba40a-230">Uno de los proyectos más populares que se basa en esa plataforma es [Spring Boot], que proporciona un enfoque simplificado para crear aplicaciones de Java independientes.</span><span class="sxs-lookup"><span data-stu-id="ba40a-230">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="ba40a-231">Para ayudar a los desarrolladores a empezar con Spring Boot, puede encontrar varios paquetes de ejemplo de Spring Boot en <https://github.com/spring-guides/>.</span><span class="sxs-lookup"><span data-stu-id="ba40a-231">To help developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>.</span></span> <span data-ttu-id="ba40a-232">Además de elegir de la lista de proyectos básicos de Spring Boot, el **[Spring Initializr]** ayuda a los desarrolladores en los primeros pasos para crear aplicaciones de Spring Boot personalizadas.</span><span class="sxs-lookup"><span data-stu-id="ba40a-232">In addition to choosing from the list of basic Spring Boot projects, the **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>


<!-- URL List -->

[Documentación sobre Azure Cosmos DB]: /azure/cosmos-db/
[Azure Cosmos DB Documentation]: /azure/cosmos-db/
[Azure para desarrolladores de Java]: https://docs.microsoft.com/java/azure/
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Build a SQL API app with Java]: https://docs.microsoft.com/azure/cosmos-db/create-sql-api-java 
[Spring Data para SQL API de Azure Cosmos DB]: https://azure.microsoft.com/blog/spring-data-azure-cosmos-db-nosql-data-access-on-azure/
[Spring Data for Azure Cosmos DB SQL API]: https://azure.microsoft.com/blog/spring-data-azure-cosmos-db-nosql-data-access-on-azure/
[Spring Data Gremlin Starter]: https://github.com/Microsoft/spring-data-gremlin
[cuenta de Azure gratuita]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Herramientas de Java para Visual Studio Team Services]: https://java.visualstudio.com/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[ventajas como suscriptor de MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[AZ01]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/AZ01.png
[AZ02]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/AZ02.png
[AZ03]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/AZ03.png
[AZ04]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/AZ04.png
[AZ05]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/AZ05.png
[AZ06]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/AZ06.png
[AZ07]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/AZ07.png
[AZ08]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/AZ08.png

[SI01]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/SI01.png
[SI02]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/SI02.png
[SI03]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/SI03.png

[RE01]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/RE01.png
[RE02]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/RE02.png

[PM01]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/PM01.png
[PM02]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/PM02.png

[JV01]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/JV01.png
[JV02]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/JV02.png
[JV03]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/JV03.png
