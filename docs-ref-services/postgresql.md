---
title: Bibliotecas de Azure Database for PostgreSQL para Java
description: Documentación de referencia para las bibliotecas de cliente de Java para Azure Database for PostgreSQL
keywords: Azure, Java, SDK, API, SQL, base de datos, PostGres, PostgreSQL
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 05/17/2017
ms.topic: article
ms.devlang: java
ms.service: postgresql
ms.openlocfilehash: 0f93d26a07de9acf72a46792793b573dba878fba
ms.sourcegitcommit: 1b22376e4ceb3d2f2734c8fc80823a44cc5fe8fb
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/14/2018
ms.locfileid: "42703342"
---
# <a name="azure-database-for-postgresql-libraries-for-java"></a><span data-ttu-id="d7a16-104">Bibliotecas de Azure Database for PostgreSQL para Java</span><span class="sxs-lookup"><span data-stu-id="d7a16-104">Azure Database for PostgreSQL libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="d7a16-105">Información general</span><span class="sxs-lookup"><span data-stu-id="d7a16-105">Overview</span></span>

<span data-ttu-id="d7a16-106">[Azure Database for PostgreSQL](/azure/sql-database/sql-database-technical-overview) es un servicio de base de datos relacional en Azure creado para desarrolladores y basado en la versión de la comunidad de código abierto del motor de base de datos [PostgreSQL](https://www.postgresql.org/).</span><span class="sxs-lookup"><span data-stu-id="d7a16-106">[Azure Database for PostgreSQL](/azure/sql-database/sql-database-technical-overview) is a relational database service in Azure built for developers based on the community version of open source [PostgreSQL](https://www.postgresql.org/) database engine.</span></span>

<span data-ttu-id="d7a16-107">Para empezar a trabajar con Azure Database for PostgreSQL, consulte [Uso de Java para conectarse y consultar datos](/azure/postgresql/connect-java).</span><span class="sxs-lookup"><span data-stu-id="d7a16-107">To get started with Azure Database for PostgreSQL, see [Use Java to connect and query data](/azure/postgresql/connect-java).</span></span>

## <a name="client-jdbc-driver"></a><span data-ttu-id="d7a16-108">Controlador JDBC de cliente</span><span class="sxs-lookup"><span data-stu-id="d7a16-108">Client JDBC driver</span></span>

<span data-ttu-id="d7a16-109">Conecte con Azure Database for PostgreSQL desde las aplicaciones mediante el [controlador JDBC de PostgreSQL](https://jdbc.postgresql.org/) de código abierto.</span><span class="sxs-lookup"><span data-stu-id="d7a16-109">Connect to Azure Database for PostgreSQL from your applications using the open-source [PostgreSQL JDBC driver](https://jdbc.postgresql.org/).</span></span> <span data-ttu-id="d7a16-110">Puede usar la [API de JDBC para Java](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/) para conectarse directamente a la base de datos o utilizar entornos de acceso a datos que interactúan con la base de datos a través de JDBC como [Hibernate](http://hibernate.org/).</span><span class="sxs-lookup"><span data-stu-id="d7a16-110">You can use the [Java JDBC API](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/) to directly connect to the database or use data access frameworks that interact with the database through JDBC such as [Hibernate](http://hibernate.org/).</span></span>

<span data-ttu-id="d7a16-111">[Agregue una dependencia](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) al archivo de Maven `pom.xml` para utilizar el controlador JDBC de cliente en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="d7a16-111">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client JDBC driver in your project.</span></span>  

```XML
<dependency>
    <groupId>org.postgresql</groupId>
    <artifactId>postgresql</artifactId>
    <version>42.1.1</version>
</dependency>
```   

## <a name="example"></a><span data-ttu-id="d7a16-112">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="d7a16-112">Example</span></span>

<span data-ttu-id="d7a16-113">Conecte con Azure Database for PostgreSQL mediante JDBC y seleccione todos los registros de la tabla de ventas.</span><span class="sxs-lookup"><span data-stu-id="d7a16-113">Connect to Azure Database for PostgreSQL using JDBC and select all records in the sales table.</span></span> <span data-ttu-id="d7a16-114">Puede obtener la cadena de conexión JDBC para la base de datos en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="d7a16-114">You can get the JDBC connection string for the database from the Azure Portal.</span></span>

```java
String url = String.format("jdbc:postgresql://mypostgresdb.postgres.database.azure.com:5432/mydb?user=frank@mypostgresdb&password=AbCdEfGhIjK&ssl=true");
Connection connection = null;
try {
    connection = DriverManager.getConnection(url);
    String selectSql = "SELECT * FROM SALES";
    Statement statement = connection.createStatement();
    ResultSet resultSet = statement.executeQuery(selectSql);
}
```

## <a name="samples"></a><span data-ttu-id="d7a16-115">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="d7a16-115">Samples</span></span>

[<span data-ttu-id="d7a16-116">Diseño de una base de datos PostgreSQL mediante la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="d7a16-116">Design a PostgreSQL database using the Azure CLI</span></span>](https://docs.microsoft.com/azure/postgresql/tutorial-design-database-using-azure-cli) 

<span data-ttu-id="d7a16-117">Vea más [código de Java de ejemplo para Azure Database for PostgreSQL](https://azure.microsoft.com/resources/samples/?platform=java&term=postgres) que puede usar en sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="d7a16-117">Explore more [sample Java code for Azure Database for PostgreSQL](https://azure.microsoft.com/resources/samples/?platform=java&term=postgres) you can use in your apps.</span></span>
