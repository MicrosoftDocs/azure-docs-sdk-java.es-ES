---
title: Bibliotecas de Azure Cosmos DB para Java
description: Documentación de referencia para las bibliotecas de cliente de Java para Azure Cosmos DB
keywords: Azure, Java, SDK, API, SQL, base de datos, MongoDB, Cosmos DB, NoSQL
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/10/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: cosmosdb
ms.openlocfilehash: d8748dc6fcc0c839a8b2d2f817c0477bcac5baa2
ms.sourcegitcommit: 4d52e47073fb0b3ac40a2689daea186bad5b1ef5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/23/2018
ms.locfileid: "49799891"
---
# <a name="azure-cosmos-db-libraries-for-java"></a>Bibliotecas de Azure Cosmos DB para Java

## <a name="overview"></a>Información general

Almacene y consulte pares de clave-valor, documentos JSON, gráficos y datos en columnas en una base de datos distribuida globalmente con [Azure Cosmos DB](/azure/cosmos-db/introduction).

Para empezar a trabajar con Azure Cosmos DB, consulte [Azure Cosmos DB: crear una aplicación de API con Java y Azure Portal](/azure/cosmos-db/create-sql-api-java).

## <a name="client-library"></a>Biblioteca de cliente

Conecte con Azure Cosmos DB utilizando la biblioteca de cliente de [SQL API](/azure/cosmos-db/sql-api-introduction) para trabajar con datos JSON con la [sintaxis de consulta SQL](/azure/cosmos-db/sql-api-sql-query).

[Agregue una dependencia](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) al archivo `pom.xml` de Maven para utilizar la biblioteca de cliente de Cosmos DB en el proyecto.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-documentdb</artifactId>
    <version>1.12.0</version>
</dependency>
```

### <a name="example"></a>Ejemplo

Seleccione documentos JSON coincidentes en Cosmos DB con la sintaxis de consulta SQL.

```java
DocumentClient client = new DocumentClient("https://contoso.documents.azure.com:443",
                "contosoCosmosDBKey", 
                new ConnectionPolicy(),
                ConsistencyLevel.Session);

List<Document> results = client.queryDocuments("dbs/" + DATABASE_ID + "/colls/" + COLLECTION_ID,
        "SELECT * FROM myCollection WHERE myCollection.email = 'allen [at] contoso.com'",
        null)
    .getQueryIterable()
    .toList();
```

> [!div class="nextstepaction"]
> [Explorar las API de cliente](/java/api/overview/azure/cosmosdb/client)


## <a name="samples"></a>Ejemplos

[Desarrollo de una aplicación Java con la API de MongoDB de Azure Cosmos DB][2]   
[Desarrollo de una aplicación Java con Graph API de Azure Cosmos DB][3]   
[Desarrollo de una aplicación Java con SQL API de Azure Cosmos DB][4]        

Vea más [código de Java de ejemplo para Azure Cosmos DB](https://azure.microsoft.com/resources/samples/?platform=java&term=cosmos) que puede usar en sus aplicaciones.

[2]: https://github.com/Azure-Samples/azure-cosmos-db-mongodb-java-getting-started
[3]: https://github.com/Azure-Samples/azure-cosmos-db-graph-java-getting-started
[4]: https://github.com/Azure-Samples/azure-cosmos-db-documentdb-java-getting-started
