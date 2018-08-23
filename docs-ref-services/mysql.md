---
title: Bibliotecas de Azure Database for MySQL para Java
description: Documentación de referencia para las bibliotecas de cliente de Java para Azure Database for MySQL
keywords: Azure, Java, SDK, API, SQL, base de datos, PostGres, MySQL
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 05/17/2017
ms.topic: article
ms.devlang: java
ms.service: mysql
ms.openlocfilehash: f3c0b84a8c6577e5a844c4084b3d9cfaf3a52323
ms.sourcegitcommit: 1b22376e4ceb3d2f2734c8fc80823a44cc5fe8fb
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/14/2018
ms.locfileid: "42703322"
---
# <a name="azure-database-for-mysql-libraries-for-java"></a><span data-ttu-id="132db-104">Bibliotecas de Azure Database for MySQL para Java</span><span class="sxs-lookup"><span data-stu-id="132db-104">Azure Database for MySQL libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="132db-105">Información general</span><span class="sxs-lookup"><span data-stu-id="132db-105">Overview</span></span>

<span data-ttu-id="132db-106">[Azure Database for MySQL](/azure/sql-database/sql-database-technical-overview) es un servicio de base de datos relacional basado en el motor de servidor de código abierto de [MySQL](https://www.mysql.com/).</span><span class="sxs-lookup"><span data-stu-id="132db-106">[Azure Database for MySQL](/azure/sql-database/sql-database-technical-overview) is a relational database service based on the open source [MySQL](https://www.mysql.com/) Server engine.</span></span> 

<span data-ttu-id="132db-107">Para empezar a trabajar con Azure Database for MySQL, consulte [Uso de Java para conectarse y consultar datos](/azure/mysql/connect-java).</span><span class="sxs-lookup"><span data-stu-id="132db-107">To get started with Azure Database for MySQL, see [Use Java to connect and query data](/azure/mysql/connect-java).</span></span>

## <a name="client-jbdc-driver"></a><span data-ttu-id="132db-108">Controlador JBDC de cliente</span><span class="sxs-lookup"><span data-stu-id="132db-108">Client JBDC driver</span></span>

<span data-ttu-id="132db-109">Conecte con Azure Database for MySQL desde las aplicaciones mediante el [controlador JDBC de MySQL](https://dev.mysql.com/downloads/connector/j/) de código abierto.</span><span class="sxs-lookup"><span data-stu-id="132db-109">Connect to Azure Database for MySQL from your applications using the open-source [MySQL JDBC driver](https://dev.mysql.com/downloads/connector/j/).</span></span> <span data-ttu-id="132db-110">Puede usar la [API de JDBC para Java](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/) para conectarse directamente a la base de datos o utilizar entornos de acceso a datos que interactúan con la base de datos a través de JDBC como [Hibernate](http://hibernate.org/).</span><span class="sxs-lookup"><span data-stu-id="132db-110">You can use the [Java JDBC API](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/) to directly connect to the database or use data access frameworks that interact with the database through JDBC such as [Hibernate](http://hibernate.org/).</span></span>

<span data-ttu-id="132db-111">[Agregue una dependencia](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) al archivo de Maven `pom.xml` para utilizar el controlador JDBC de cliente en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="132db-111">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client JDBC driver in your project.</span></span>  

```XML
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>5.1.42</version>
</dependency>
```   

## <a name="example"></a><span data-ttu-id="132db-112">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="132db-112">Example</span></span>

<span data-ttu-id="132db-113">Conecte con Azure Database for MySQL mediante JDBC y seleccione todos los registros de la tabla de ventas.</span><span class="sxs-lookup"><span data-stu-id="132db-113">Connect to Azure Database for MySQL using JDBC and select all records in the sales table.</span></span> <span data-ttu-id="132db-114">Puede obtener la cadena de conexión JDBC para la base de datos en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="132db-114">You can get the JDBC connection string for the database from the Azure Portal.</span></span>

```java
String url = String.format("jdbc:mysql://fabrikamysql.mysql.database.azure.com:3306/fabrikamdb?verifyServerCertificate=true&useSSL=true&requireSSL=false");
try {
    Connection conn = DriverManager.getConnection(url, "frank@fabrikamysql", "aBcDeFgHiJkL");
    String selectSql = "SELECT * FROM SALES";
    Statement statement = conn.createStatement();
    ResultSet resultSet = statement.executeQuery(selectSql);
}
```

## <a name="samples"></a><span data-ttu-id="132db-115">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="132db-115">Samples</span></span>

<span data-ttu-id="132db-116">[Compilación de una aplicación web de Java y MySQL](/azure/app-service-web/app-service-web-tutorial-java-mysql) </span><span class="sxs-lookup"><span data-stu-id="132db-116">[Build a Java and MySQL web app](/azure/app-service-web/app-service-web-tutorial-java-mysql) </span></span>  
[<span data-ttu-id="132db-117">Diseño de una base de datos MySQL mediante la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="132db-117">Design a MySQL database using the Azure CLI</span></span>](/azure/mysql/tutorial-design-database-using-cli)   

<span data-ttu-id="132db-118">Vea más [código de Java de ejemplo para Azure Database for MySQL](https://azure.microsoft.com/resources/samples/?platform=java&term=mysql) que puede usar en sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="132db-118">Explore more [sample Java code for Azure Database for MySQL](https://azure.microsoft.com/resources/samples/?platform=java&term=mysql) you can use in your apps.</span></span>
