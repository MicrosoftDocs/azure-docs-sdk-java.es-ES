---
title: Bibliotecas de Azure Database for MySQL para Java
description: "Documentación de referencia para las bibliotecas de cliente de Java para Azure Database for MySQL"
keywords: Azure, Java, SDK, API, SQL, base de datos, PostGres, MySQL
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 05/17/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: mysql
ms.openlocfilehash: 72c94ef4bdad7adeae63da2efda93b52a9afef53
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/28/2017
---
# <a name="azure-database-for-mysql-libraries-for-java"></a>Bibliotecas de Azure Database for MySQL para Java

## <a name="overview"></a>Información general

[Azure Database for MySQL](/azure/sql-database/sql-database-technical-overview) es un servicio de base de datos relacional basado en el motor de servidor de código abierto de [MySQL](https://www.mysql.com/). 

Para empezar a trabajar con Azure Database for MySQL, consulte [Uso de Java para conectarse y consultar datos](/azure/mysql/connect-java).

## <a name="client-jbdc-driver"></a>Controlador JBDC de cliente

Conecte con Azure Database for MySQL desde las aplicaciones mediante el [controlador JDBC de MySQL](https://dev.mysql.com/downloads/connector/j/) de código abierto. Puede usar la [API de JDBC para Java](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/) para conectarse directamente a la base de datos o utilizar entornos de acceso a datos que interactúan con la base de datos a través de JDBC como [Hibernate](http://hibernate.org/).

[Agregue una dependencia](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) al archivo de Maven `pom.xml` para utilizar el controlador JDBC de cliente en el proyecto.  

```XML
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>5.1.42</version>
</dependency>
```   

## <a name="example"></a>Ejemplo

Conecte con Azure Database for MySQL mediante JDBC y seleccione todos los registros de la tabla de ventas. Puede obtener la cadena de conexión JDBC para la base de datos en Azure Portal.

```java
String url = String.format("jdbc:mysql://fabrikamysql.mysql.database.azure.com:3306/fabrikamdb?verifyServerCertificate=true&useSSL=true&requireSSL=false");
try {
    Connection conn = DriverManager.getConnection(url, "frank@fabrikamysql", "aBcDeFgHiJkL");
    String selectSql = "SELECT * FROM SALES";
    Statement statement = conn.createStatement();
    ResultSet resultSet = statement.executeQuery(selectSql);
}
```

## <a name="samples"></a>Muestras

[Compilación de una aplicación web de Java y MySQL](/azure/app-service-web/app-service-web-tutorial-java-mysql)   
[Diseño de una base de datos MySQL mediante la CLI de Azure](/azure/mysql/tutorial-design-database-using-cli)   

Vea más [código de Java de ejemplo para Azure Database for MySQL](https://azure.microsoft.com/resources/samples/?platform=java&term=mysql) que puede usar en sus aplicaciones.
