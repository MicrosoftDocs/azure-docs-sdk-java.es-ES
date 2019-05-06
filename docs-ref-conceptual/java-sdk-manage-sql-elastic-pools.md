---
title: Administración de grupos elásticos de Azure SQL Database con Java | Microsoft Docs
description: Código de ejemplo para crear y configurar bases de datos de Azure SQL mediante el SDK de Azure para Java
author: rloutlaw
manager: douge
ms.assetid: 9b461de8-46bc-4650-8e9e-59531f4e2a53
ms.topic: article
ms.service: Azure
ms.devlang: java
ms.technology: Azure
ms.date: 3/30/2017
ms.author: routlaw;asirveda
ms.openlocfilehash: 59d2601ef21b91a364887fe0548cb95023c79b5e
ms.sourcegitcommit: 115f4c8ad07a11f17d79e9d945d63917836b11c8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "61592690"
---
# <a name="manage-azure-sql-databases-in-elastic-pools-from-your-java-applications"></a><span data-ttu-id="41cf0-103">Administración de bases de datos de Azure SQL en grupos elásticos desde las aplicaciones Java</span><span class="sxs-lookup"><span data-stu-id="41cf0-103">Manage Azure SQL databases in elastic pools from your Java applications</span></span>

<span data-ttu-id="41cf0-104">[Este ejemplo](https://github.com/Azure-Samples/sql-database-java-manage-sql-dbs-in-elastic-pool) crea un servidor de SQL Database con un [grupo elástico](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-pool) para administrar y escalar los recursos para múltiples bases de datos en un único plan.</span><span class="sxs-lookup"><span data-stu-id="41cf0-104">[This sample](https://github.com/Azure-Samples/sql-database-java-manage-sql-dbs-in-elastic-pool) creates a SQL database server with an [elastic pool](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-pool) to manage and scale resources for mulitple databases in a single plan.</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="41cf0-105">Ejecución del ejemplo</span><span class="sxs-lookup"><span data-stu-id="41cf0-105">Run the sample</span></span>

<span data-ttu-id="41cf0-106">Cree un [archivo de autenticación](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) y establezca una variable de entorno `AZURE_AUTH_LOCATION` con la ruta de acceso completa al archivo en el equipo.</span><span class="sxs-lookup"><span data-stu-id="41cf0-106">Create an [authentication file](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) and set an environment variable `AZURE_AUTH_LOCATION` with the full path to the file on your computer.</span></span> <span data-ttu-id="41cf0-107">A continuación, ejecute:</span><span class="sxs-lookup"><span data-stu-id="41cf0-107">Then run:</span></span>

```
git clone https://github.com/Azure-Samples/sql-database-java-manage-sql-dbs-in-elastic-pool
cd sql-database-java-manage-sql-dbs-in-elastic-pool
mvn clean compile exec:java
```

[<span data-ttu-id="41cf0-108">Ver el código completo del ejemplo en GitHub</span><span class="sxs-lookup"><span data-stu-id="41cf0-108">View the complete code sample on GitHub</span></span>](https://github.com/Azure-Samples/sql-database-java-manage-sql-dbs-in-elastic-pool)

## <a name="authenticate-with-azure"></a><span data-ttu-id="41cf0-109">Autenticación con Azure</span><span class="sxs-lookup"><span data-stu-id="41cf0-109">Authenticate with Azure</span></span>

[!INCLUDE [auth-include](includes/java-auth-include.md)]

## <a name="create-a-sql-database-server-with-an-elastic-pool"></a><span data-ttu-id="41cf0-110">Creación de un servidor de SQL Database con un grupo elástico</span><span class="sxs-lookup"><span data-stu-id="41cf0-110">Create a SQL database server with an elastic pool</span></span>

```java
SqlServer sqlServer = azure.sqlServers().define(sqlServerName)
                    .withRegion(Region.US_EAST)
                    .withNewResourceGroup(rgName)
                    .withAdministratorLogin(administratorLogin)
                    .withAdministratorPassword(administratorPassword)
                    // Use ElasticPoolEditions.STANDARD as the edition
                    // and create two databases
                    .withNewElasticPool(elasticPoolName, ElasticPoolEditions.STANDARD, 
                        database1Name, database2Name)
                    .create();
```

<span data-ttu-id="41cf0-111">Consulte la [referencia de la clase ElasticPoolEditions](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._elastic_pool_editions) para los valores actuales de edición.</span><span class="sxs-lookup"><span data-stu-id="41cf0-111">See the [ElasticPoolEditions class reference](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._elastic_pool_editions) for current edition values.</span></span> <span data-ttu-id="41cf0-112">Revise la [documentación de grupos elásticos de bases de datos SQL](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-pool) para comparar las características de los recursos de la edición.</span><span class="sxs-lookup"><span data-stu-id="41cf0-112">Review the [SQL database elastic pool documentation](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-pool) to compare edition resource characteristics.</span></span> 

## <a name="change-database-transaction-unit-dtu-settings-in-an-elastic-pool"></a><span data-ttu-id="41cf0-113">Cambio de la configuración de la unidad de transmisión de datos (DTU) en un grupo elástico</span><span class="sxs-lookup"><span data-stu-id="41cf0-113">Change Database Transaction Unit (DTU) settings in an elastic pool</span></span>

```java
// Set an pool of 200 eDTUs to share between the databases
// and ensure that a database always has 10 DTUs available but never uses more than 50
elasticPool = elasticPool.update()
                    .withDtu(200)
                    .withDatabaseDtuMin(10)
                    .withDatabaseDtuMax(50)
                    .apply();
```

<span data-ttu-id="41cf0-114">Revise la [documentación sobre DTU y eDTU](https://docs.microsoft.com/azure/sql-database/sql-database-what-is-a-dtu) para más información sobre la asignación de recursos a bases de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="41cf0-114">Review the [DTUs and eDTUs documentation](https://docs.microsoft.com/azure/sql-database/sql-database-what-is-a-dtu) to learn more about allocating resources to SQL databases.</span></span>

## <a name="create-a-new-database-and-add-it-to-an-elastic-pool"></a><span data-ttu-id="41cf0-115">Creación de una nueva base de datos y agregarla a un grupo elástico</span><span class="sxs-lookup"><span data-stu-id="41cf0-115">Create a new database and add it to an elastic pool</span></span>

```java
// Add a newly created database to the elastic pool
SqlDatabase anotherDatabase = sqlServer.databases().define(anotherDatabaseName).create();
elasticPool.update().withExistingDatabase(anotherDatabase).apply();            
```

<span data-ttu-id="41cf0-116">La API crea `anotherDatabase` en el [nivel S0](https://docs.microsoft.com/azure/sql-database/sql-database-service-tiers) en la primera instrucción.</span><span class="sxs-lookup"><span data-stu-id="41cf0-116">The API creates `anotherDatabase` at [S0 tier](https://docs.microsoft.com/azure/sql-database/sql-database-service-tiers) in the first statement.</span></span> <span data-ttu-id="41cf0-117">Al mover `anotherDatabase` al grupo elástico, los recursos de base de datos se asignan en función de la configuración del grupo.</span><span class="sxs-lookup"><span data-stu-id="41cf0-117">Moving `anotherDatabase` to the elastic pool assigns the database resources based on the pool settings.</span></span>

## <a name="remove-a-database-from-an-elastic-pool"></a><span data-ttu-id="41cf0-118">Eliminación de una base de datos de un grupo elástico</span><span class="sxs-lookup"><span data-stu-id="41cf0-118">Remove a database from an elastic pool</span></span>
```java
// Assign an edition since the database resources are no longer managed in the pool 
anotherDatabase = anotherDatabase.update()
                     .withoutElasticPool()
                     .withEdition(DatabaseEditions.STANDARD)
                     .apply();
```

<span data-ttu-id="41cf0-119">Consulte la [referencia de la clase DatabaseEditions](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._database_editions) para los valores que se pasarán a `withEdition()`.</span><span class="sxs-lookup"><span data-stu-id="41cf0-119">See the [DatabaseEditions class reference](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._database_editions) for values to pass to `withEdition()`.</span></span>

## <a name="list-current-database-activities-in-an-elastic-pool"></a><span data-ttu-id="41cf0-120">Enumeración de las actividades de base de datos en un grupo elástico</span><span class="sxs-lookup"><span data-stu-id="41cf0-120">List current database activities in an elastic pool</span></span>
```java
// get a list of in-flight elastic operations on databases in the pool and log them 
for (ElasticPoolDatabaseActivity databaseActivity : elasticPool.listDatabaseActivities()) {
    System.out.println("Database " + databaseActivity.databaseName() 
        + " performing operation " + databaseActivity.operation() + 
        " with objective " + databaseActivity.requestedServiceObjective());
}
```

<span data-ttu-id="41cf0-121">Las actividades de la base de datos incluyen mover una base de datos dentro o fuera de un grupo elástico y actualizar las bases de datos en un grupo elástico.</span><span class="sxs-lookup"><span data-stu-id="41cf0-121">Database activities include moving a database in or out of an elastic pool and updating databases in an elastic pool.</span></span>


## <a name="list-databases-in-an-elastic-pool"></a><span data-ttu-id="41cf0-122">Enumeración de bases de datos de un grupo elástico</span><span class="sxs-lookup"><span data-stu-id="41cf0-122">List databases in an elastic pool</span></span>
```java
// Log a list of databases in the elastic pool 
for (SqlDatabase databaseInServer : elasticPool.listDatabases()) {
    System.out.println(databaseInServer.name());
}
```

<span data-ttu-id="41cf0-123">Revise los métodos de [com.microsoft.azure.management.sql.SqlDatabase](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._sql_database) para consultar las bases de datos con más detalle.</span><span class="sxs-lookup"><span data-stu-id="41cf0-123">Review the methods in [com.microsoft.azure.management.sql.SqlDatabase](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._sql_database) to query the databases in more detail.</span></span>

## <a name="delete-an-elastic-pool"></a><span data-ttu-id="41cf0-124">Eliminación de un grupo elástico</span><span class="sxs-lookup"><span data-stu-id="41cf0-124">Delete an elastic pool</span></span>
```java
sqlServer.elasticPools().delete(elasticPoolName);
```

<span data-ttu-id="41cf0-125">El grupo elástico debe estar vacío antes de eliminarlo.</span><span class="sxs-lookup"><span data-stu-id="41cf0-125">The elastic pool must be empty before deleting it.</span></span>

## <a name="sample-code-summary"></a><span data-ttu-id="41cf0-126">Resumen de código de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="41cf0-126">Sample code summary.</span></span>

<span data-ttu-id="41cf0-127">El ejemplo crea un servidor SQL con dos bases de datos administradas en un único grupo elástico.</span><span class="sxs-lookup"><span data-stu-id="41cf0-127">The sample creates a SQL server with two databases managed in a single elasic pool.</span></span> <span data-ttu-id="41cf0-128">Se actualizan los límites de recursos del grupo elástico y se agregan bases de datos adicionales al grupo.</span><span class="sxs-lookup"><span data-stu-id="41cf0-128">The elastic pool resource limits are updated, then additional databases are added to the pool.</span></span> <span data-ttu-id="41cf0-129">A continuación, el código lee la configuración y el estado del grupo elástico.</span><span class="sxs-lookup"><span data-stu-id="41cf0-129">The code then reads the elastic pool's configuration and state.</span></span> 

<span data-ttu-id="41cf0-130">El ejemplo elimina todos los recursos que ha creado antes de salir.</span><span class="sxs-lookup"><span data-stu-id="41cf0-130">The sample deletes all resources it created before exiting.</span></span>

| <span data-ttu-id="41cf0-131">Clase utilizada en el ejemplo</span><span class="sxs-lookup"><span data-stu-id="41cf0-131">Class used in sample</span></span> | <span data-ttu-id="41cf0-132">Notas</span><span class="sxs-lookup"><span data-stu-id="41cf0-132">Notes</span></span> |
|-------|-------|
| [<span data-ttu-id="41cf0-133">SqlServer</span><span class="sxs-lookup"><span data-stu-id="41cf0-133">SqlServer</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._sql_server) | <span data-ttu-id="41cf0-134">Servidor de base de datos SQL de Azure creado por la cadena fluida `azure.sqlServers().define()...create()`.</span><span class="sxs-lookup"><span data-stu-id="41cf0-134">SQL DB server in Azure created by `azure.sqlServers().define()...create()` fluent chain.</span></span> <span data-ttu-id="41cf0-135">Proporciona métodos para crear y trabajar con bases de datos y grupos elásticos.</span><span class="sxs-lookup"><span data-stu-id="41cf0-135">Provides methods to create and work with elastic pools and databases.</span></span> 
| [<span data-ttu-id="41cf0-136">SqlDatabase</span><span class="sxs-lookup"><span data-stu-id="41cf0-136">SqlDatabase</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._sql_database) | <span data-ttu-id="41cf0-137">Objeto de cliente que representa una base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="41cf0-137">Client side object representing a SQL database.</span></span> <span data-ttu-id="41cf0-138">Se creó mediante `sqlServer().define()...create()`.</span><span class="sxs-lookup"><span data-stu-id="41cf0-138">Created through `sqlServer().define()...create()`.</span></span> 
| [<span data-ttu-id="41cf0-139">DatabaseEditions</span><span class="sxs-lookup"><span data-stu-id="41cf0-139">DatabaseEditions</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._database_editions) | <span data-ttu-id="41cf0-140">Campos estáticos de valor constante usados para establecer los recursos de base de datos al crear una base de datos fuera de un grupo elástico o al mover una base de datos fuera de un grupo elástico</span><span class="sxs-lookup"><span data-stu-id="41cf0-140">Constant static fields used to set database resources when creating a database outside of an elastic pool or when moving a database out of an elastic pool</span></span>  
| [<span data-ttu-id="41cf0-141">SqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="41cf0-141">SqlElasticPool</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._sql_elastic_pool) | <span data-ttu-id="41cf0-142">Creado a partir de la sección `withNewElasticPool()` de la cadena fluida que creó el servidor SQL SqlServer en Azure.</span><span class="sxs-lookup"><span data-stu-id="41cf0-142">Created from the `withNewElasticPool()` section of the fluent chain that created the SqlServer in Azure.</span></span> <span data-ttu-id="41cf0-143">Proporciona métodos para establecer los límites de recursos para las bases de datos que se ejecutan en el grupo elástico y para el propio grupo elástico.</span><span class="sxs-lookup"><span data-stu-id="41cf0-143">Provides methods to set resource limits for databases running in the elastic pool and for the elastic pool itself.</span></span> 
| [<span data-ttu-id="41cf0-144">ElasticPoolEditions</span><span class="sxs-lookup"><span data-stu-id="41cf0-144">ElasticPoolEditions</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._elastic_pool_editions) | <span data-ttu-id="41cf0-145">Clase de campos constantes que definen los recursos disponibles para un grupo elástico.</span><span class="sxs-lookup"><span data-stu-id="41cf0-145">Class of constant fields defining the resources available to an elastic pool.</span></span> <span data-ttu-id="41cf0-146">Consulte la [documentación de grupos elásticos de bases de datos SQL](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-pool) para obtener detalles de la capa.</span><span class="sxs-lookup"><span data-stu-id="41cf0-146">See [SQL database elastic pool documentation](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-pool) for tier details.</span></span> 
| [<span data-ttu-id="41cf0-147">ElasticPoolDatabaseActivity</span><span class="sxs-lookup"><span data-stu-id="41cf0-147">ElasticPoolDatabaseActivity</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._elastic_pool_database_activity) | <span data-ttu-id="41cf0-148">Recuperado desde `SqlElasticPool.listDatabaseActivities()`.</span><span class="sxs-lookup"><span data-stu-id="41cf0-148">Retreived from `SqlElasticPool.listDatabaseActivities()`.</span></span> <span data-ttu-id="41cf0-149">Cada objeto de este tipo representa una actividad realizada en una base de datos en el grupo elástico.</span><span class="sxs-lookup"><span data-stu-id="41cf0-149">Each object of this type represents an activity performed on a database in the elastic pool.</span></span>
| [<span data-ttu-id="41cf0-150">ElasticPoolActivity</span><span class="sxs-lookup"><span data-stu-id="41cf0-150">ElasticPoolActivity</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._elastic_pool_activity) | <span data-ttu-id="41cf0-151">Recuperado en forma de lista de `SqlElasticPool.listActivities()`.</span><span class="sxs-lookup"><span data-stu-id="41cf0-151">Retrieved in a List from `SqlElasticPool.listActivities()`.</span></span> <span data-ttu-id="41cf0-152">Cada uno de los objetos de la lista representa una actividad realizada en el grupo elástico (no en las bases de datos del grupo elástico).</span><span class="sxs-lookup"><span data-stu-id="41cf0-152">Each of object in the list represents an activity performed on the elastic pool (not the databases in the elastic pool).</span></span>

## <a name="next-steps"></a><span data-ttu-id="41cf0-153">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="41cf0-153">Next steps</span></span>

[!INCLUDE [next-steps](includes/java-next-steps.md)]