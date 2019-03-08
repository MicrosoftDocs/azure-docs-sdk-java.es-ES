---
title: Uso de Spring Data JDBC con PostgreSQL de Azure
description: Aprenda a usar Spring Data JDBC con una base de datos PostgreSQL de Azure.
services: postgresql
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 12/19/2018
ms.devlang: java
ms.service: postgresql
ms.tgt_pltfrm: multiple
ms.topic: article
ms.openlocfilehash: 29f3c957dd0ccd754eedef12e3fc01c3484dddf3
ms.sourcegitcommit: 1c1412ad5d8960975c3fc7fd3d1948152ef651ef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/05/2019
ms.locfileid: "57335398"
---
# <a name="how-to-use-spring-data-jdbc-with-azure-postgresql"></a>Uso de Spring Data JDBC con PostgreSQL de Azure

## <a name="overview"></a>Información general

En este artículo se explica cómo crear una aplicación de ejemplo que utiliza [Spring Data] para almacenar y recuperar información en una base de datos [PostgreSQL](https://www.postgresql.org/) de Azure mediante [Java Database Connectivity (JDBC)](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/).

## <a name="prerequisites"></a>Requisitos previos

Los siguientes requisitos previos son necesarios para seguir los pasos descritos en este artículo:

* Una suscripción de Azure. Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN] o registrarse para obtener una [cuenta de Azure gratuita].
* Un kit de desarrollo de Java (JDK) admitido Para más información sobre los JDK disponibles para desarrollar en Azure, consulte <https://aka.ms/azure-jdks>.
* [Apache Maven](http://maven.apache.org/), versión 3.0 o posterior.
* [Curl ](https://curl.haxx.se/) o una utilidad HTTP similar para probar la funcionalidad.
* Utilidad de línea de comandos [psql](https://www.postgresql.org/docs/current/app-psql.html).
* Un cliente [Git](https://git-scm.com/downloads).

## <a name="create-a-postgresql-database-for-azure"></a>Creación de una base de datos PostgreSQL para Azure

### <a name="create-a-postgresql-database-server-using-the-azure-portal"></a>Creación de un servidor de bases de datos PostgreSQL mediante Azure Portal

> [!NOTE]
> 
> Puede leer información más detallada sobre la creación de bases de datos PostgreSQL en [Creación de un servidor de Azure Database for PostgreSQL mediante Azure Portal](/azure/postgresql/quickstart-create-server-database-portal).

1. Vaya a Azure Portal en <https://portal.azure.com/> e inicie sesión.

1. Haga clic sucesivamente en **+Crear un recurso**, después en **Bases de datos** y, finalmente en **Azure Database for PostgreSQL**.

   ![Creación de una base de datos PostgreSQL][POSTGRESQL01]

1. Escriba la siguiente información:

   - **Nombre del servidor**: elija un nombre único para el servidor PostgreSQL; se utilizará para crear un nombre de dominio completo como *wingtiptoyspostgresql.postgres.database.azure.com*.
   - **Suscripción**: especifique la suscripción de Azure que se va a usar.
   - **Grupo de recursos**: especifique si desea crear un nuevo grupo de recursos o elija uno existente.
   - **Seleccionar origen**: para este tutorial, seleccione `Blank` para crear una nueva base de datos.
   - **Inicio de sesión del administrador del servidor**: especifique el nombre del administrador de base de datos.
   - **Contraseña** y **Confirmar contraseña**: especifique la contraseña para el administrador de base de datos.
   - **Ubicación**: especifique la región geográfica más cercana a la base de datos.
   - **Versión**: especifique la versión de la base de datos más reciente.
   - **Plan de tarifa**: para este tutorial, especifique el plan de tarifa menos costoso.

   ![Creación de propiedades de la base de datos de PostgreSQL][POSTGRESQL02]

1. Cuando haya especificado la información anterior, haga clic en **Crear**.

### <a name="configure-a-firewall-rule-for-your-postgresql-database-server-using-the-azure-portal"></a>Configuración de una regla de firewall para el servidor de bases de datos PostgreSQL mediante Azure Portal

1. Vaya a Azure Portal en <https://portal.azure.com/> e inicie sesión.

1. Haga clic en **Todos los recursos** y, a continuación, haga clic en la base de datos de PostgreSQL que acaba de crear.

   ![Selección de la base de datos de PostgreSQL][POSTGRESQL03]

1. Haga clic en **Seguridad de la conexión** y, en las **reglas de firewall**, cree una nueva regla mediante la especificación de un nombre único para la regla, escriba el intervalo de direcciones IP que necesitará para acceder a la base de datos y, después, haga clic en **Guardar**.

   ![Configuración de la seguridad de la conexión][POSTGRESQL04]

### <a name="retrieve-the-connection-string-for-your-postgresql-server-using-the-azure-portal"></a>Recuperación de la cadena de conexión para el servidor PostgreSQL mediante Azure Portal

1. Vaya a Azure Portal en <https://portal.azure.com/> e inicie sesión.

1. Haga clic en **Todos los recursos** y, a continuación, haga clic en la base de datos de PostgreSQL que acaba de crear.

   ![Selección de la base de datos de PostgreSQL][POSTGRESQL03]

1. Haga clic en **Cadenas de conexión** y copie el valor en el campo de texto **JDBC**.

   ![Recuperación de la cadena de conexión JDBC][POSTGRESQL05]

### <a name="create-postgresql-database-using-the-psql-command-line-utility"></a>Creación de la base de datos PostgreSQL mediante la utilidad de línea de comandos `psql`

1. Abra un shell de comandos y conéctese al servidor PostgreSQL mediante la escritura de un comando `psql` similar al siguiente ejemplo:

   ```shell
   psql --host=wingtiptoyspostgresql.postgres.database.azure.com --port=5432 --username=wingtiptoysuser@wingtiptoyspostgresql --dbname=postgres
   ```
   Donde:

   | Parámetro | DESCRIPCIÓN |
   |---|---|
   | `host` | Especifica el nombre completo del servidor PostgreSQL que se mencionó anteriormente en este artículo. |
   | `host` | Especifica el puerto del servidor PostgreSQL, que es `5432` de forma predeterminada. |
   | `username` | Especifica el administrador de PostgreSQL y el nombre de servidor abreviado que se mencionaron anteriormente en este artículo. |
   | `dbname` | Especifica que desea usar la base de datos predeterminada `postgres` por ahora. |

   El servidor PostgreSQL debería responder con una pantalla similar al ejemplo siguiente:

   ```shell
   psql (9.3.24, server 10.5)
   SSL connection (cipher: ECDHE-RSA-AES256-SHA384, bits: 256)
   Type "help" for help.
   
   postgres=>
   ```

1. Cree una base de datos denominada *mypgsqldb* mediante la escritura de un comando `psql` similar al ejemplo siguiente:

   ```SQL
   CREATE DATABASE mypgsqldb;
   ```

   El servidor PostgreSQL debería responder con una pantalla similar al ejemplo siguiente:

   ```shell
   CREATE DATABASE
   ```

1. OPCIONAL: Puede comprobar que se creó la base de datos mediante la escritura de `\l` en `psql`; el servidor PostgreSQL debería responder con algo similar al ejemplo siguiente:

   ```shell
                   List of databases
          Name        |      Owner      | Encoding
   -------------------+-----------------+----------
    azure_maintenance | azure_superuser | UTF8
    azure_sys         | azure_superuser | UTF8
    mypgsqldb         | wingtiptoysuser | UTF8
    postgres          | azure_superuser | UTF8
    template0         | azure_superuser | UTF8
    template1         | azure_superuser | UTF8
   (6 rows)
   ```

1. Escriba `\q` para salir de la utilidad `psql`.

## <a name="configure-the-sample-application"></a>Configurar la aplicación de ejemplo

1. Abra un shell de comandos y clone el proyecto de ejemplo con un comando git como el siguiente ejemplo:

   ```shell
   git clone https://github.com/Azure-Samples/spring-data-jdbc-on-azure.git
   ```

1. Busque el archivo *application.properties* en el directorio *resources* del proyecto de ejemplo, o cree el archivo si todavía no existe.

1. Abra el archivo *application.properties* en un editor de texto y agréguele o configure las siguientes líneas; luego, sustituya los valores de ejemplo por los valores adecuados que se mencionaron anteriormente:

   ```yaml
   spring.datasource.url=jdbc:postgresql://wingtiptoyspostgresql.postgres.database.azure.com:5432/mypgsqldb?ssl=true&sslmode=prefer
   spring.datasource.username=wingtiptoysuser@wingtiptoyspostgresql
   spring.datasource.password=********
    ```
   Donde:

   | Parámetro | DESCRIPCIÓN |
   |---|---|
   | `spring.datasource.url` | Especifica la cadena de JDBC de PostgreSQL que se mencionó anteriormente en este artículo. |
   | `spring.datasource.username` | Especifica el nombre del administrador de PostgreSQL que se mencionó anteriormente en este artículo, con el nombre abreviado del servidor anexado. |
   | `spring.datasource.password` | Especifica la contraseña de administrador de PostgreSQL que se mencionó anteriormente en este artículo. |

1. Guarde y cierre el archivo *application.properties*.

## <a name="package-and-test-the-sample-application"></a>Empaquetado y prueba de la aplicación de ejemplo 

1. Compile la aplicación de ejemplo con Maven; por ejemplo:

   ```shell
   mvn clean package -P postgresql
   ```

1. Inicie la aplicación de ejemplo; por ejemplo:

   ```shell
   java -jar target/spring-data-jdbc-on-azure-0.1.0-SNAPSHOT.jar
   ```

1. Cree nuevos registros con `curl` desde un símbolo del sistema como en los ejemplos siguientes:

   ```shell
   curl -s -d '{"name":"dog","species":"canine"}' -H "Content-Type: application/json" -X POST http://localhost:8080/pets

   curl -s -d '{"name":"cat","species":"feline"}' -H "Content-Type: application/json" -X POST http://localhost:8080/pets
   ```

   La aplicación debe devolver valores similares a los siguientes:

   ```shell
   Added Pet(id=1, name=dog, species=canine).

   Added Pet(id=2, name=cat, species=feline).
   ```

1. Recupere todos los registros existentes con `curl` desde un símbolo del sistema como los siguientes ejemplos:

   ```shell
   curl -s http://localhost:8080/pets
   ```
    
   La aplicación debe devolver valores similares a los siguientes:

   ```json
   [{"id":1,"name":"dog","species":"canine"},{"id":2,"name":"cat","species":"feline"}]
   ```

## <a name="summary"></a>Resumen

En este tutorial ha creado una aplicación Java de ejemplo que Spring Data para almacenar y recuperar información de una base de datos PostgreSQL de Azure mediante JDBC.

## <a name="next-steps"></a>Pasos siguientes

Para más información acerca de Spring y Azure, vaya al centro de documentación de Azure.

> [!div class="nextstepaction"]
> [Spring en Azure](/java/azure/spring-framework)

### <a name="additional-resources"></a>Recursos adicionales

Para más información sobre el uso de Azure con Java, consulte [Azure para desarrolladores de Java] y [Working with Azure DevOps and Java] (Trabajo con Azure DevOps y Java).

<!-- URL List -->

[Azure para desarrolladores de Java]: /java/azure/
[cuenta de Azure gratuita]: https://azure.microsoft.com/pricing/free-trial/
[Working with Azure DevOps and Java]: /azure/devops/ (Trabajo con Azure DevOps y Java)
[ventajas como suscriptor de MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Data]: https://spring.io/projects/spring-data
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[POSTGRESQL01]: media/configure-spring-data-jdbc-with-azure-postgresql/create-postgresql-01.png
[POSTGRESQL02]: media/configure-spring-data-jdbc-with-azure-postgresql/create-postgresql-02.png
[POSTGRESQL03]: media/configure-spring-data-jdbc-with-azure-postgresql/create-postgresql-03.png
[POSTGRESQL04]: media/configure-spring-data-jdbc-with-azure-postgresql/create-postgresql-04.png
[POSTGRESQL05]: media/configure-spring-data-jdbc-with-azure-postgresql/create-postgresql-05.png
