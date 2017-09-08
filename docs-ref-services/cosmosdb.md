---
title: Bibliotecas de Azure Cosmos DB para Java
description: "Documentación de referencia para las bibliotecas de cliente de Java para Azure Cosmos DB"
keywords: Azure, Java, SDK, API, SQL, base de datos, MongoDB, Cosmos DB, NoSQL, DocumentDB
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/10/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: cosmosdb
ms.openlocfilehash: 249907528c24395b0da5d64e4dc06e3422894cfe
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/28/2017
---
# <a name="azure-cosmos-db-libraries-for-java"></a><span data-ttu-id="52004-104">Bibliotecas de Azure Cosmos DB para Java</span><span class="sxs-lookup"><span data-stu-id="52004-104">Azure Cosmos DB libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="52004-105">Información general</span><span class="sxs-lookup"><span data-stu-id="52004-105">Overview</span></span>

<span data-ttu-id="52004-106">Almacene y consulte pares de clave-valor, documentos JSON, gráficos y datos en columnas en una base de datos distribuida globalmente con [Cosmos DB](/azure/cosmos-db/introduction).</span><span class="sxs-lookup"><span data-stu-id="52004-106">Store and query key-value, JSON document, graph, and columnar data in a globally distributed database with [Cosmos DB](/azure/cosmos-db/introduction).</span></span>

<span data-ttu-id="52004-107">Para empezar a trabajar con Cosmos DB, consulte [Azure Cosmos DB: crear una aplicación de API con Java y Azure Portal](/azure/cosmos-db/create-documentdb-java).</span><span class="sxs-lookup"><span data-stu-id="52004-107">To get started with Cosmos DB, see [Azure Cosmos DB: Build an API app with Java and the Azure portal](/azure/cosmos-db/create-documentdb-java).</span></span>

## <a name="client-library"></a><span data-ttu-id="52004-108">Biblioteca de cliente</span><span class="sxs-lookup"><span data-stu-id="52004-108">Client library</span></span>

<span data-ttu-id="52004-109">Conecte con Cosmos DB utilizando la biblioteca de cliente de [DocumentDB](/azure/cosmos-db/documentdb-introduction) para trabajar con datos JSON con la [sintaxis de consulta SQL](/azure/cosmos-db/documentdb-sql-query).</span><span class="sxs-lookup"><span data-stu-id="52004-109">Connect to Cosmos DB using the [DocumentDB](/azure/cosmos-db/documentdb-introduction) client library to work with JSON data with [SQL query syntax](/azure/cosmos-db/documentdb-sql-query).</span></span>

<span data-ttu-id="52004-110">[Agregue una dependencia](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) al archivo `pom.xml` de Maven para utilizar la biblioteca de cliente de Cosmos DB en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="52004-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the Cosmos DB client library in your project.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-documentdb</artifactId>
    <version>1.12.0</version>
</dependency>
```

### <a name="example"></a><span data-ttu-id="52004-111">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="52004-111">Example</span></span>

<span data-ttu-id="52004-112">Seleccione documentos JSON coincidentes en Cosmos DB con la sintaxis de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="52004-112">Select matching JSON documents in Cosmos DB using SQL query syntax.</span></span>

```java
DocumentClient client = new DocumentClient(new DocumentClient("https://contoso.documents.azure.com:443",
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
> [<span data-ttu-id="52004-113">Explorar las API de cliente</span><span class="sxs-lookup"><span data-stu-id="52004-113">Explore the Client APIs</span></span>](/java/api/overview/azure/cosmosdb/clientlibrary)


## <a name="samples"></a><span data-ttu-id="52004-114">Muestras</span><span class="sxs-lookup"><span data-stu-id="52004-114">Samples</span></span>

<span data-ttu-id="52004-115">[Desarrollo de una aplicación Java con la API de MongoDB de Azure Cosmos DB][2] </span><span class="sxs-lookup"><span data-stu-id="52004-115">[Develop a Java app using Azure Cosmos DB MongoDB API][2] </span></span>  
<span data-ttu-id="52004-116">[Desarrollo de una aplicación Java con la API Graph de Azure Cosmos DB][3] </span><span class="sxs-lookup"><span data-stu-id="52004-116">[Develop a Java app using Azure Cosmos DB Graph API][3] </span></span>  
<span data-ttu-id="52004-117">[Desarrollo de una aplicación Java con la API de DocumentDB de Azure Cosmos DB][4]</span><span class="sxs-lookup"><span data-stu-id="52004-117">[Develop a Java app using Azure Cosmos DB DocumentDB API][4]</span></span>        

<span data-ttu-id="52004-118">Vea más [código de Java de ejemplo para Azure Cosmos DB](https://azure.microsoft.com/resources/samples/?platform=java&term=cosmos) que puede usar en sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="52004-118">Explore more [sample Java code for Azure Cosmos DB](https://azure.microsoft.com/resources/samples/?platform=java&term=cosmos) you can use in your apps.</span></span>

[2]: https://github.com/Azure-Samples/azure-cosmos-db-mongodb-java-getting-started
[3]: https://github.com/Azure-Samples/azure-cosmos-db-graph-java-getting-started
[4]: https://github.com/Azure-Samples/azure-cosmos-db-documentdb-java-getting-started