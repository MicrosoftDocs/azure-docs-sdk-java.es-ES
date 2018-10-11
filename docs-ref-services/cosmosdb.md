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
ms.openlocfilehash: 6fc9f90cb3c8130aa82b20554a94a8b5ab78c083
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/09/2018
ms.locfileid: "48899264"
---
# <a name="azure-cosmos-db-libraries-for-java"></a><span data-ttu-id="48693-104">Bibliotecas de Azure Cosmos DB para Java</span><span class="sxs-lookup"><span data-stu-id="48693-104">Azure Cosmos DB libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="48693-105">Información general</span><span class="sxs-lookup"><span data-stu-id="48693-105">Overview</span></span>

<span data-ttu-id="48693-106">Almacene y consulte pares de clave-valor, documentos JSON, gráficos y datos en columnas en una base de datos distribuida globalmente con [Azure Cosmos DB](/azure/cosmos-db/introduction).</span><span class="sxs-lookup"><span data-stu-id="48693-106">Store and query key-value, JSON document, graph, and columnar data in a globally distributed database with [Azure Cosmos DB](/azure/cosmos-db/introduction).</span></span>

<span data-ttu-id="48693-107">Para empezar a trabajar con Azure Cosmos DB, consulte [Azure Cosmos DB: crear una aplicación de API con Java y Azure Portal](/azure/cosmos-db/create-sql-api-java).</span><span class="sxs-lookup"><span data-stu-id="48693-107">To get started with Azure Cosmos DB, see [Azure Cosmos DB: Build an API app with Java and the Azure portal](/azure/cosmos-db/create-sql-api-java).</span></span>

## <a name="client-library"></a><span data-ttu-id="48693-108">Biblioteca de cliente</span><span class="sxs-lookup"><span data-stu-id="48693-108">Client library</span></span>

<span data-ttu-id="48693-109">Conecte con Azure Cosmos DB utilizando la biblioteca de cliente de [SQL API](/azure/cosmos-db/sql-api-introduction) para trabajar con datos JSON con la [sintaxis de consulta SQL](/azure/cosmos-db/sql-api-sql-query).</span><span class="sxs-lookup"><span data-stu-id="48693-109">Connect to Azure Cosmos DB using the [SQL API](/azure/cosmos-db/sql-api-introduction) client library to work with JSON data with [SQL query syntax](/azure/cosmos-db/sql-api-sql-query).</span></span>

<span data-ttu-id="48693-110">[Agregue una dependencia](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) al archivo `pom.xml` de Maven para utilizar la biblioteca de cliente de Cosmos DB en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="48693-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the Cosmos DB client library in your project.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-documentdb</artifactId>
    <version>1.12.0</version>
</dependency>
```

### <a name="example"></a><span data-ttu-id="48693-111">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="48693-111">Example</span></span>

<span data-ttu-id="48693-112">Seleccione documentos JSON coincidentes en Cosmos DB con la sintaxis de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="48693-112">Select matching JSON documents in Cosmos DB using SQL query syntax.</span></span>

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
> [<span data-ttu-id="48693-113">Explorar las API de cliente</span><span class="sxs-lookup"><span data-stu-id="48693-113">Explore the Client APIs</span></span>](/java/api/overview/azure/cosmosdb/client)


## <a name="samples"></a><span data-ttu-id="48693-114">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="48693-114">Samples</span></span>

<span data-ttu-id="48693-115">[Desarrollo de una aplicación Java con la API de MongoDB de Azure Cosmos DB][2] </span><span class="sxs-lookup"><span data-stu-id="48693-115">[Develop a Java app using Azure Cosmos DB MongoDB API][2] </span></span>  
<span data-ttu-id="48693-116">[Desarrollo de una aplicación Java con Graph API de Azure Cosmos DB][3] </span><span class="sxs-lookup"><span data-stu-id="48693-116">[Develop a Java app using Azure Cosmos DB Graph API][3] </span></span>  
<span data-ttu-id="48693-117">[Desarrollo de una aplicación Java con SQL API de Azure Cosmos DB][4]</span><span class="sxs-lookup"><span data-stu-id="48693-117">[Develop a Java app using Azure Cosmos DB SQL API][4]</span></span>        

<span data-ttu-id="48693-118">Vea más [código de Java de ejemplo para Azure Cosmos DB](https://azure.microsoft.com/resources/samples/?platform=java&term=cosmos) que puede usar en sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="48693-118">Explore more [sample Java code for Azure Cosmos DB](https://azure.microsoft.com/resources/samples/?platform=java&term=cosmos) you can use in your apps.</span></span>

[2]: https://github.com/Azure-Samples/azure-cosmos-db-mongodb-java-getting-started
[3]: https://github.com/Azure-Samples/azure-cosmos-db-graph-java-getting-started
[4]: https://github.com/Azure-Samples/azure-cosmos-db-documentdb-java-getting-started
