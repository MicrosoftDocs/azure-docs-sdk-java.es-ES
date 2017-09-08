---
title: Bibliotecas de Azure SQL Database para Java
description: "Conecte con Azure SQL Database mediante el controlador JDBC o administre las instancias de Azure SQL Database con la API de administración."
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
ms.openlocfilehash: 332bfa45b41f7b183e5c35ec9a1f3537f7d849ba
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/28/2017
---
# <a name="azure-sql-database-libraries-for-java"></a>Bibliotecas de Azure SQL Database para Java

## <a name="overview"></a>Información general

[Azure SQL Database](/azure/sql-database/sql-database-technical-overview) es un servicio de base de datos relacional basado en el motor Microsoft SQL Server que admite datos de tabla, JSON, espaciales y XML. 

Para empezar a trabajar con Azure SQL Database, consulte [Azure SQL Database: uso de Java para conectarse y consultar datos](/azure/sql-database/sql-database-connect-query-java).

## <a name="client-jdbc-driver"></a>Controlador JDBC de cliente

Conecte con Azure SQL Database desde las aplicaciones mediante el [controlador JDBC de SQL Database](/sql/connect/jdbc/microsoft-jdbc-driver-for-sql-server). Puede usar la [API de JDBC para Java](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/) para conectarse directamente a la base de datos o utilizar entornos de acceso a datos que interactúan con la base de datos a través de JDBC como [Hibernate](http://hibernate.org/).

[Agregue una dependencia](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) al archivo de Maven `pom.xml` para utilizar el controlador JDBC de cliente en el proyecto.


```XML
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>6.2.1.jre8</version>
</dependency>
```   

### <a name="example"></a>Ejemplo

Conecte con SQL Database y seleccione todos los registros de una tabla con JDBC.

```java
String connectionString = "jdbc:sqlserver://fabrikam.database.windows.net:1433;database=fiber;user=raisa;password=testpass;encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;";
try {
    Connection conn = DriverManager.getConnection(connectionString);
    Statement statement = conn.createStatement();
    ResultSet resultSet = statement.executeQuery("SELECT * FROM SALES");
}  
```

## <a name="management-api"></a>API de administración

Cree y administre los recursos de Azure SQL Database de la suscripción con la API de administración.   

[Agregue una dependencia](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) al archivo `pom.xml` de Maven para utilizar la API de administración en el proyecto.


```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-sql</artifactId>
    <version>1.1.2</version>
</dependency>
```

> [!div class="nextstepaction"]
> [Explorar las API de administración](/java/api/overview/azure/sql/managementapi)

### <a name="example"></a>Ejemplo

Cree un recurso de SQL Database y restrinja el acceso a un intervalo de direcciones IP mediante una regla de firewall.

```java
SqlServer sqlServer = azure.sqlServers().define(sqlDbName)
                    .withRegion(Region.US_EAST)
                    .withNewResourceGroup(resourceGroupName)
                    .withAdministratorLogin(administratorLogin)
                    .withAdministratorPassword(administratorPassword)
                    .withNewFirewallRule("172.16.0.0", "172.31.255.255")
                    .create();
```

## <a name="samples"></a>Muestras

[!INCLUDE [java-sql-samples](../docs-ref-conceptual/includes/sql.md)]

Ver más [código de Java de ejemplo para Azure SQL Database](https://azure.microsoft.com/resources/samples/?platform=java&term=SQL) que puede usar en sus aplicaciones.