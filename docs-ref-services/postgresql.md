---
title: Bibliotecas de Azure Database for PostgreSQL para Java
description: Documentación de referencia para las bibliotecas de cliente de Java para Azure Database for PostgreSQL
keywords: Azure, Java, SDK, API, SQL, base de datos, PostGres, PostgreSQL
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 05/17/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: postgresql
ms.openlocfilehash: d6fa2acb9a2f44b157ae52ba6e41f6777a43b574
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/28/2017
ms.locfileid: "21930981"
---
# <a name="azure-database-for-postgresql-libraries-for-java"></a>Bibliotecas de Azure Database for PostgreSQL para Java

## <a name="overview"></a>Información general

[Azure Database for PostgreSQL](/azure/sql-database/sql-database-technical-overview) es un servicio de base de datos relacional en Azure creado para desarrolladores y basado en la versión de la comunidad de código abierto del motor de base de datos [PostgreSQL](https://www.postgresql.org/).

Para empezar a trabajar con Azure Database for PostgreSQL, consulte [Uso de Java para conectarse y consultar datos](/azure/postgresql/connect-java).

## <a name="client-jdbc-driver"></a>Controlador JDBC de cliente

Conecte con Azure Database for PostgreSQL desde las aplicaciones mediante el [controlador JDBC de PostgreSQL](https://jdbc.postgresql.org/) de código abierto. Puede usar la [API de JDBC para Java](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/) para conectarse directamente a la base de datos o utilizar entornos de acceso a datos que interactúan con la base de datos a través de JDBC como [Hibernate](http://hibernate.org/).

[Agregue una dependencia](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) al archivo de Maven `pom.xml` para utilizar el controlador JDBC de cliente en el proyecto.  

```XML
<dependency>
    <groupId>org.postgresql</groupId>
    <artifactId>postgresql</artifactId>
    <version>42.1.1</version>
</dependency>
```   

## <a name="example"></a>Ejemplo

Conecte con Azure Database for PostgreSQL mediante JDBC y seleccione todos los registros de la tabla de ventas. Puede obtener la cadena de conexión JDBC para la base de datos en Azure Portal.

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

## <a name="samples"></a>Muestras

[Diseño de una base de datos PostgreSQL mediante la CLI de Azure](https://docs.microsoft.com/azure/postgresql/tutorial-design-database-using-azure-cli) 

Vea más [código de Java de ejemplo para Azure Database for PostgreSQL](https://azure.microsoft.com/resources/samples/?platform=java&term=postgres) que puede usar en sus aplicaciones.
