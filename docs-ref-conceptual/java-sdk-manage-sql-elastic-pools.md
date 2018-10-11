---
title: Administración de grupos elásticos de Azure SQL Database con Java | Microsoft Docs
description: Código de ejemplo para crear y configurar bases de datos SQL de Azure mediante el SDK de Azure para Java
author: rloutlaw
manager: douge
ms.assetid: 9b461de8-46bc-4650-8e9e-59531f4e2a53
ms.topic: article
ms.service: Azure
ms.devlang: java
ms.technology: Azure
ms.date: 3/30/2017
ms.author: routlaw;asirveda
ms.openlocfilehash: 9ec0cf3083b8659fa850b798ca0ecf18b2757234
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/09/2018
ms.locfileid: "48893576"
---
# <a name="manage-azure-sql-databases-in-elastic-pools-from-your-java-applications"></a>Administración de bases de datos SQL de Azure en grupos elásticos desde las aplicaciones Java

[Este ejemplo](https://github.com/Azure-Samples/sql-database-java-manage-sql-dbs-in-elastic-pool) crea un servidor de base de datos SQL con un [grupo elástico](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-pool) para administrar y escalar los recursos para múltiples bases de datos en un único plan.

## <a name="run-the-sample"></a>Ejecución del ejemplo

Cree un [archivo de autenticación](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) y establezca una variable de entorno `AZURE_AUTH_LOCATION` con la ruta de acceso completa al archivo en el equipo. A continuación, ejecute:

```
git clone https://github.com/Azure-Samples/sql-database-java-manage-sql-dbs-in-elastic-pool
cd sql-database-java-manage-sql-dbs-in-elastic-pool
mvn clean compile exec:java
```

[Ver el código completo del ejemplo en GitHub](https://github.com/Azure-Samples/sql-database-java-manage-sql-dbs-in-elastic-pool)

## <a name="authenticate-with-azure"></a>Autenticación con Azure

[!INCLUDE [auth-include](includes/java-auth-include.md)]

## <a name="create-a-sql-database-server-with-an-elastic-pool"></a>Creación de un servidor de bases de datos SQL con un grupo elástico

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

Consulte la [referencia de la clase ElasticPoolEditions](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._elastic_pool_editions) para los valores actuales de edición. Revise la [documentación de grupos elásticos de bases de datos SQL](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-pool) para comparar las características de los recursos de la edición. 

## <a name="change-database-transaction-unit-dtu-settings-in-an-elastic-pool"></a>Cambio de la configuración de la unidad de transmisión de datos (DTU) en un grupo elástico

```java
// Set an pool of 200 eDTUs to share between the databases
// and ensure that a database always has 10 DTUs available but never uses more than 50
elasticPool = elasticPool.update()
                    .withDtu(200)
                    .withDatabaseDtuMin(10)
                    .withDatabaseDtuMax(50)
                    .apply();
```

Revise la [documentación sobre DTU y eDTU](https://docs.microsoft.com/azure/sql-database/sql-database-what-is-a-dtu) para más información sobre la asignación de recursos a bases de datos SQL.

## <a name="create-a-new-database-and-add-it-to-an-elastic-pool"></a>Creación de una nueva base de datos y agregarla a un grupo elástico

```java
// Add a newly created database to the elastic pool
SqlDatabase anotherDatabase = sqlServer.databases().define(anotherDatabaseName).create();
elasticPool.update().withExistingDatabase(anotherDatabase).apply();            
```

La API crea `anotherDatabase` en el [nivel S0](https://docs.microsoft.com/azure/sql-database/sql-database-service-tiers) en la primera instrucción. Al mover `anotherDatabase` al grupo elástico, los recursos de base de datos se asignan en función de la configuración del grupo.

## <a name="remove-a-database-from-an-elastic-pool"></a>Eliminación de una base de datos de un grupo elástico
```java
// Assign an edition since the database resources are no longer managed in the pool 
anotherDatabase = anotherDatabase.update()
                     .withoutElasticPool()
                     .withEdition(DatabaseEditions.STANDARD)
                     .apply();
```

Consulte la [referencia de la clase DatabaseEditions](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._database_editions) para los valores que se pasarán a `withEdition()`.

## <a name="list-current-database-activities-in-an-elastic-pool"></a>Enumeración de las actividades de base de datos en un grupo elástico
```java
// get a list of in-flight elastic operations on databases in the pool and log them 
for (ElasticPoolDatabaseActivity databaseActivity : elasticPool.listDatabaseActivities()) {
    System.out.println("Database " + databaseActivity.databaseName() 
        + " performing operation " + databaseActivity.operation() + 
        " with objective " + databaseActivity.requestedServiceObjective());
}
```

Las actividades de la base de datos incluyen mover una base de datos dentro o fuera de un grupo elástico y actualizar las bases de datos en un grupo elástico.


## <a name="list-databases-in-an-elastic-pool"></a>Enumeración de bases de datos de un grupo elástico
```java
// Log a list of databases in the elastic pool 
for (SqlDatabase databaseInServer : elasticPool.listDatabases()) {
    System.out.println(databaseInServer.name());
}
```

Revise los métodos de [com.microsoft.azure.management.sql.SqlDatabase](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._sql_database) para consultar las bases de datos con más detalle.

## <a name="delete-an-elastic-pool"></a>Eliminación de un grupo elástico
```java
sqlServer.elasticPools().delete(elasticPoolName);
```

El grupo elástico debe estar vacío antes de eliminarlo.

## <a name="sample-code-summary"></a>Resumen de código de ejemplo.

El ejemplo crea un servidor SQL con dos bases de datos administradas en un único grupo elástico. Se actualizan los límites de recursos del grupo elástico y se agregan bases de datos adicionales al grupo. A continuación, el código lee la configuración y el estado del grupo elástico. 

El ejemplo elimina todos los recursos que ha creado antes de salir.

| Clase utilizada en el ejemplo | Notas |
|-------|-------|
| [SqlServer](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._sql_server) | Servidor de base de datos SQL de Azure creado por la cadena fluida `azure.sqlServers().define()...create()`. Proporciona métodos para crear y trabajar con bases de datos y grupos elásticos. 
| [SqlDatabase](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._sql_database) | Objeto de cliente que representa una base de datos SQL. Se creó mediante `sqlServer().define()...create()`. 
| [DatabaseEditions](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._database_editions) | Campos estáticos de valor constante usados para establecer los recursos de base de datos al crear una base de datos fuera de un grupo elástico o al mover una base de datos fuera de un grupo elástico  
| [SqlElasticPool](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._sql_elastic_pool) | Creado a partir de la sección `withNewElasticPool()` de la cadena fluida que creó el servidor SQL SqlServer en Azure. Proporciona métodos para establecer los límites de recursos para las bases de datos que se ejecutan en el grupo elástico y para el propio grupo elástico. 
| [ElasticPoolEditions](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._elastic_pool_editions) | Clase de campos constantes que definen los recursos disponibles para un grupo elástico. Consulte la [documentación de grupos elásticos de bases de datos SQL](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-pool) para obtener detalles de la capa. 
| [ElasticPoolDatabaseActivity](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._elastic_pool_database_activity) | Recuperado desde `SqlElasticPool.listDatabaseActivities()`. Cada objeto de este tipo representa una actividad realizada en una base de datos en el grupo elástico.
| [ElasticPoolActivity](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._elastic_pool_activity) | Recuperado en forma de lista de `SqlElasticPool.listActivities()`. Cada uno de los objetos de la lista representa una actividad realizada en el grupo elástico (no en las bases de datos del grupo elástico).

## <a name="next-steps"></a>Pasos siguientes

[!INCLUDE [next-steps](includes/java-next-steps.md)]