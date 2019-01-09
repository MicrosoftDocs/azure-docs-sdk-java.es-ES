---
title: Uso de Spring Data JDBC con Azure SQL Database
description: Aprenda a usar Spring Data JDBC con una instancia de Azure SQL Database.
services: sql-database
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 12/19/2018
ms.devlang: java
ms.service: sql-database
ms.tgt_pltfrm: multiple
ms.topic: article
ms.openlocfilehash: 92f489b513eeb05efaacdf07af2b976de8f84868
ms.sourcegitcommit: f0f140b0862ca5338b1b7e5c33cec3e58a70b8fd
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/03/2019
ms.locfileid: "53992503"
---
# <a name="how-to-use-spring-data-jdbc-with-azure-sql-database"></a>Uso de Spring Data JDBC con Azure SQL Database

## <a name="overview"></a>Información general

En este artículo se explica cómo crear una aplicación de ejemplo que utiliza [Spring Data] para almacenar y recuperar información en una instancia de [Azure SQL Database](https://azure.microsoft.com/services/sql-database/) mediante [Java Database Connectivity (JDBC)](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/).

## <a name="prerequisites"></a>Requisitos previos

Los siguientes requisitos previos son necesarios para seguir los pasos descritos en este artículo:

* Una suscripción de Azure. Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN] o registrarse para obtener una [cuenta de Azure gratuita].
* Un kit de desarrollo de Java (JDK) admitido Para más información sobre los JDK disponibles para desarrollar en Azure, consulte <https://aka.ms/azure-jdks>.
* [Apache Maven](http://maven.apache.org/), versión 3.0 o posterior.
* [Curl ](https://curl.haxx.se/) o una utilidad HTTP similar para probar la funcionalidad.
* Un cliente [Git](https://git-scm.com/downloads).

## <a name="create-an-azure-sql-satabase"></a>Creación de una instancia de Azure SQL Database

### <a name="create-a-sql-database-server-using-the-azure-portal"></a>Creación de un servidor de SQL Database mediante Azure Portal

> [!NOTE]
> 
> Puede leer información más detallada sobre la creación de bases de datos SQL de Azure en [Creación de una instancia de Azure SQL Database en Azure Portal](/azure/sql-database/sql-database-get-started-portal).

1. Vaya a Azure Portal en <https://portal.azure.com/> e inicie sesión.

1. Haga clic en **+Crear un recurso**, después en **Bases de datos** y, finalmente, en **SQL Database**.

   ![Creación de una base de datos SQL][SQL01]

1. Especifique la siguiente información:

   - **Nombre de la base de datos**: elija un nombre único para la base de datos SQL; este se creará en el servidor SQL que va a especificar posteriormente.
   - **Suscripción**: especifique la suscripción de Azure que se va a usar.
   - **Grupo de recursos**: especifique si desea crear un nuevo grupo de recursos o elija uno existente.
   - **Seleccionar origen**: para este tutorial, seleccione `Blank database` para crear una nueva base de datos.

   ![Especificación de las propiedades de la base de datos SQL][SQL02]
   
1. Haga clic en **Servidor**, después en **Crear un servidor nuevo** y, después, especifique la siguiente información:

   - **Nombre del servidor**: elija un nombre único para el servidor SQL; se utilizará para crear un nombre de dominio completo como *wingtiptoyssql.database.windows.net*.
   - **Inicio de sesión del administrador del servidor**: especifique el nombre del administrador de base de datos.
   - **Contraseña** y **Confirmar contraseña**: especifique la contraseña para el administrador de base de datos.
   - **Ubicación**: especifique la región geográfica más cercana a la base de datos.

   ![Especificación del servidor SQL Server][SQL03]

1. Cuando haya especificado la información anterior, haga clic en **Seleccionar**.

1. Para este tutorial, especifique el **plan de tarifa** menos costoso y, después, haga clic en **Crear**.

   ![Creación de la base de datos SQL][SQL04]

### <a name="configure-a-firewall-rule-for-your-sql-server-using-the-azure-portal"></a>Configuración de una regla de firewall para el servidor SQL Server mediante Azure Portal

1. Vaya a Azure Portal en <https://portal.azure.com/> e inicie sesión.

1. Haga clic en **Todos los recursos**; después, haga clic en el servidor SQL Server que acaba de crear.

   ![Selección del servidor SQL Server][SQL05]

1. En la sección **Introducción**, haga clic en **Mostrar configuración del firewall**.

   ![Visualización de la configuración del firewall][SQL06]

1. En la sección **Firewalls y redes virtuales**, cree una nueva regla mediante la especificación de un nombre único para la regla, escriba el intervalo de direcciones IP que necesitará para acceder a la base de datos y, después, haga clic en **Guardar**.

   ![Configuración del firewall][SQL07]

### <a name="retrieve-the-connection-string-for-your-sql-server-using-the-azure-portal"></a>Recuperación de la cadena de conexión para el servidor SQL Server con Azure Portal

1. Vaya a Azure Portal en <https://portal.azure.com/> e inicie sesión.

1. Haga clic en **Todos los recursos** y, a continuación, haga clic en la base de datos SQL que acaba de crear.

   ![Selección de la base de datos SQL][SQL08]

1. Haga clic en **Cadenas de conexión**, después haga clic en **JDBC** y copie el valor en el campo de texto JDBC.

   ![Recuperación de la cadena de conexión JDBC][SQL09]

## <a name="configure-the-sample-application"></a>Configurar la aplicación de ejemplo

1. Abra un shell de comandos y clone el proyecto de ejemplo con un comando git como el siguiente ejemplo:

   ```shell
   git clone https://github.com/Azure-Samples/spring-data-jdbc-on-azure.git
   ```

1. Busque el archivo *application.properties* en el directorio *resources* del proyecto de ejemplo, o cree el archivo si todavía no existe.

1. Abra el archivo *application.properties* en un editor de texto y agréguele o configure las siguientes líneas; luego, sustituya los valores de ejemplo por los valores adecuados que se mencionaron anteriormente:

   ```yaml
   spring.datasource.url=jdbc:sqlserver://wingtiptoyssql.database.windows.net:1433;database=wingtiptoys;encrypt=true;trustServerCertificate=false;hostNameInCertificate=*.database.windows.net;loginTimeout=30;
   spring.datasource.username=wingtiptoysuser@wingtiptoyssql
   spring.datasource.password=********
    ```
   Donde:

   | Parámetro | DESCRIPCIÓN |
   |---|---|
   | `spring.datasource.url` | Especifica una versión modificada de la cadena JDBC de SQL que se mencionó anteriormente en este artículo. |
   | `spring.datasource.username` | Especifica el nombre del administrador de SQL que se mencionó anteriormente en este artículo, con el nombre abreviado del servidor anexado. |
   | `spring.datasource.password` | Especifica la contraseña de administrador de SQL que se mencionó anteriormente en este artículo. |

1. Guarde y cierre el archivo *application.properties*.

## <a name="package-and-test-the-sample-application"></a>Empaquetado y prueba de la aplicación de ejemplo 

1. Compile la aplicación de ejemplo con Maven; por ejemplo:

   ```shell
   mvn clean package -P sql
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

En este tutorial ha creado una aplicación Java de ejemplo que Spring Data para almacenar y recuperar información de una instancia de Azure SQL Database mediante JDBC.

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

[SQL01]: media/configure-spring-data-jdbc-with-azure-sql-server/create-azure-sql-01.png
[SQL02]: media/configure-spring-data-jdbc-with-azure-sql-server/create-azure-sql-02.png
[SQL03]: media/configure-spring-data-jdbc-with-azure-sql-server/create-azure-sql-03.png
[SQL04]: media/configure-spring-data-jdbc-with-azure-sql-server/create-azure-sql-04.png
[SQL05]: media/configure-spring-data-jdbc-with-azure-sql-server/create-azure-sql-05.png
[SQL06]: media/configure-spring-data-jdbc-with-azure-sql-server/create-azure-sql-06.png
[SQL07]: media/configure-spring-data-jdbc-with-azure-sql-server/create-azure-sql-07.png
[SQL08]: media/configure-spring-data-jdbc-with-azure-sql-server/create-azure-sql-08.png
[SQL09]: media/configure-spring-data-jdbc-with-azure-sql-server/create-azure-sql-09.png
