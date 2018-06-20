---
title: Bibliotecas de Azure SQL Database para Java
description: Conecte con Azure SQL Database mediante el controlador JDBC o administre las instancias de Azure SQL Database con la API de administración.
keywords: Azure, Java, SDK, API, SQL, base de datos, JDBC
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/05/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: sql-database
ms.openlocfilehash: 37f7d3caf10e6b709cee2452c63a543d49e0ead8
ms.sourcegitcommit: 49b17bbf34732512f836ee634818f1058147ff5c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
ms.locfileid: "31823718"
---
# <a name="azure-sql-database-libraries-for-java"></a><span data-ttu-id="52f25-104">Bibliotecas de Azure SQL Database para Java</span><span class="sxs-lookup"><span data-stu-id="52f25-104">Azure SQL Database libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="52f25-105">Información general</span><span class="sxs-lookup"><span data-stu-id="52f25-105">Overview</span></span>

<span data-ttu-id="52f25-106">[Azure SQL Database](/azure/sql-database/sql-database-technical-overview) es un servicio de base de datos relacional basado en el motor Microsoft SQL Server que admite datos de tabla, JSON, espaciales y XML.</span><span class="sxs-lookup"><span data-stu-id="52f25-106">[Azure SQL Database](/azure/sql-database/sql-database-technical-overview) is a relational database service using the Microsoft SQL Server engine that supports table, JSON, spatial, and XML data.</span></span> 

<span data-ttu-id="52f25-107">Para empezar a trabajar con Azure SQL Database, consulte [Azure SQL Database: uso de Java para conectarse y consultar datos](/azure/sql-database/sql-database-connect-query-java).</span><span class="sxs-lookup"><span data-stu-id="52f25-107">To get started with Azure SQL Database, see [Azure SQL Database: Use Java to connect and query data](/azure/sql-database/sql-database-connect-query-java).</span></span>

## <a name="client-jdbc-driver"></a><span data-ttu-id="52f25-108">Controlador JDBC de cliente</span><span class="sxs-lookup"><span data-stu-id="52f25-108">Client JDBC driver</span></span>

<span data-ttu-id="52f25-109">Conecte con Azure SQL Database desde las aplicaciones mediante el [controlador JDBC de SQL Database](/sql/connect/jdbc/microsoft-jdbc-driver-for-sql-server).</span><span class="sxs-lookup"><span data-stu-id="52f25-109">Connect to Azure SQL Database from your applications using the [SQL Database JDBC driver](/sql/connect/jdbc/microsoft-jdbc-driver-for-sql-server).</span></span> <span data-ttu-id="52f25-110">Puede usar la [API de JDBC para Java](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/) para conectarse directamente a la base de datos o utilizar entornos de acceso a datos que interactúan con la base de datos a través de JDBC como [Hibernate](http://hibernate.org/).</span><span class="sxs-lookup"><span data-stu-id="52f25-110">You can use the [Java JDBC API](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/) to directly connect with the database or use data access frameworks that interact with the database through JDBC such as [Hibernate](http://hibernate.org/).</span></span>

<span data-ttu-id="52f25-111">[Agregue una dependencia](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) al archivo de Maven `pom.xml` para utilizar el controlador JDBC de cliente en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="52f25-111">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client JDBC driver in your project.</span></span>


```XML
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>6.2.1.jre8</version>
</dependency>
```   

### <a name="example"></a><span data-ttu-id="52f25-112">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="52f25-112">Example</span></span>

<span data-ttu-id="52f25-113">Conecte con SQL Database y seleccione todos los registros de una tabla con JDBC.</span><span class="sxs-lookup"><span data-stu-id="52f25-113">Connect to SQL database and select all records in a table using JDBC.</span></span>

```java
String connectionString = "jdbc:sqlserver://fabrikam.database.windows.net:1433;database=fiber;user=raisa;password=testpass;encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;";
try {
    Connection conn = DriverManager.getConnection(connectionString);
    Statement statement = conn.createStatement();
    ResultSet resultSet = statement.executeQuery("SELECT * FROM SALES");
}  
```

## <a name="management-api"></a><span data-ttu-id="52f25-114">API de administración</span><span class="sxs-lookup"><span data-stu-id="52f25-114">Management API</span></span>

<span data-ttu-id="52f25-115">Cree y administre los recursos de Azure SQL Database de la suscripción con la API de administración.</span><span class="sxs-lookup"><span data-stu-id="52f25-115">Create and manage Azure SQL Database resources in your subscription with the management API.</span></span>   

<span data-ttu-id="52f25-116">[Agregue una dependencia](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) al archivo `pom.xml` de Maven para utilizar la API de administración en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="52f25-116">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>


```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-sql</artifactId>
    <version>1.3.0</version>
</dependency>
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="52f25-117">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="52f25-117">Explore the Management APIs</span></span>](/java/api/overview/azure/sql/management)

### <a name="example"></a><span data-ttu-id="52f25-118">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="52f25-118">Example</span></span>

<span data-ttu-id="52f25-119">Cree un recurso de SQL Database y restrinja el acceso a un intervalo de direcciones IP mediante una regla de firewall.</span><span class="sxs-lookup"><span data-stu-id="52f25-119">Create a SQL Database resource and restrict access to a range of IP addresses using a firewall rule.</span></span>

```java
SqlServer sqlServer = azure.sqlServers().define(sqlDbName)
                    .withRegion(Region.US_EAST)
                    .withNewResourceGroup(resourceGroupName)
                    .withAdministratorLogin(administratorLogin)
                    .withAdministratorPassword(administratorPassword)
                    .withNewFirewallRule("172.16.0.0", "172.31.255.255")
                    .create();
```

## <a name="samples"></a><span data-ttu-id="52f25-120">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="52f25-120">Samples</span></span>

[!INCLUDE [java-sql-samples](../docs-ref-conceptual/includes/sql.md)]

<span data-ttu-id="52f25-121">Ver más [código de Java de ejemplo para Azure SQL Database](https://azure.microsoft.com/resources/samples/?platform=java&term=SQL) que puede usar en sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="52f25-121">Explore more [sample Java code for Azure SQL Database](https://azure.microsoft.com/resources/samples/?platform=java&term=SQL) you can use in your apps.</span></span>