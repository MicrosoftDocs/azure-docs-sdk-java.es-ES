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
# <a name="how-to-use-spring-data-jdbc-with-azure-postgresql"></a><span data-ttu-id="a311e-103">Uso de Spring Data JDBC con PostgreSQL de Azure</span><span class="sxs-lookup"><span data-stu-id="a311e-103">How to use Spring Data JDBC with Azure PostgreSQL</span></span>

## <a name="overview"></a><span data-ttu-id="a311e-104">Información general</span><span class="sxs-lookup"><span data-stu-id="a311e-104">Overview</span></span>

<span data-ttu-id="a311e-105">En este artículo se explica cómo crear una aplicación de ejemplo que utiliza [Spring Data] para almacenar y recuperar información en una base de datos [PostgreSQL](https://www.postgresql.org/) de Azure mediante [Java Database Connectivity (JDBC)](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/).</span><span class="sxs-lookup"><span data-stu-id="a311e-105">This article demonstrates creating a sample application that uses [Spring Data] to store and retrieve information in an Azure [PostgreSQL](https://www.postgresql.org/) database using [Java Database Connectivity (JDBC)](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a311e-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="a311e-106">Prerequisites</span></span>

<span data-ttu-id="a311e-107">Los siguientes requisitos previos son necesarios para seguir los pasos descritos en este artículo:</span><span class="sxs-lookup"><span data-stu-id="a311e-107">The following prerequisites are required in order to complete the steps in this article:</span></span>

* <span data-ttu-id="a311e-108">Una suscripción de Azure. Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN] o registrarse para obtener una [cuenta de Azure gratuita].</span><span class="sxs-lookup"><span data-stu-id="a311e-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="a311e-109">Un kit de desarrollo de Java (JDK) admitido</span><span class="sxs-lookup"><span data-stu-id="a311e-109">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="a311e-110">Para más información sobre los JDK disponibles para desarrollar en Azure, consulte <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="a311e-110">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="a311e-111">[Apache Maven](http://maven.apache.org/), versión 3.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="a311e-111">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>
* <span data-ttu-id="a311e-112">[Curl ](https://curl.haxx.se/) o una utilidad HTTP similar para probar la funcionalidad.</span><span class="sxs-lookup"><span data-stu-id="a311e-112">[Curl](https://curl.haxx.se/) or similar HTTP utility to test functionality.</span></span>
* <span data-ttu-id="a311e-113">Utilidad de línea de comandos [psql](https://www.postgresql.org/docs/current/app-psql.html).</span><span class="sxs-lookup"><span data-stu-id="a311e-113">The [psql](https://www.postgresql.org/docs/current/app-psql.html) command-line utility.</span></span>
* <span data-ttu-id="a311e-114">Un cliente [Git](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="a311e-114">A [Git](https://git-scm.com/downloads) client.</span></span>

## <a name="create-a-postgresql-database-for-azure"></a><span data-ttu-id="a311e-115">Creación de una base de datos PostgreSQL para Azure</span><span class="sxs-lookup"><span data-stu-id="a311e-115">Create a PostgreSQL database for Azure</span></span>

### <a name="create-a-postgresql-database-server-using-the-azure-portal"></a><span data-ttu-id="a311e-116">Creación de un servidor de bases de datos PostgreSQL mediante Azure Portal</span><span class="sxs-lookup"><span data-stu-id="a311e-116">Create a PostgreSQL database server using the Azure Portal</span></span>

> [!NOTE]
> 
> <span data-ttu-id="a311e-117">Puede leer información más detallada sobre la creación de bases de datos PostgreSQL en [Creación de un servidor de Azure Database for PostgreSQL mediante Azure Portal](/azure/postgresql/quickstart-create-server-database-portal).</span><span class="sxs-lookup"><span data-stu-id="a311e-117">You can read more detailed information about creating PostgreSQL databases in [Create an Azure Database for PostgreSQL server by using the Azure portal](/azure/postgresql/quickstart-create-server-database-portal).</span></span>

1. <span data-ttu-id="a311e-118">Vaya a Azure Portal en <https://portal.azure.com/> e inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="a311e-118">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="a311e-119">Haga clic sucesivamente en **+Crear un recurso**, después en **Bases de datos** y, finalmente en **Azure Database for PostgreSQL**.</span><span class="sxs-lookup"><span data-stu-id="a311e-119">Click **+Create a resource**, then **Databases**, and then click **Azure Database for PostgreSQL**.</span></span>

   ![Creación de una base de datos PostgreSQL][POSTGRESQL01]

1. <span data-ttu-id="a311e-121">Escriba la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="a311e-121">Enter the following information:</span></span>

   - <span data-ttu-id="a311e-122">**Nombre del servidor**: elija un nombre único para el servidor PostgreSQL; se utilizará para crear un nombre de dominio completo como *wingtiptoyspostgresql.postgres.database.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="a311e-122">**Server name**: Choose a unique name for your PostgreSQL server; this will be used to create a fully-qualified domain name like *wingtiptoyspostgresql.postgres.database.azure.com*.</span></span>
   - <span data-ttu-id="a311e-123">**Suscripción**: especifique la suscripción de Azure que se va a usar.</span><span class="sxs-lookup"><span data-stu-id="a311e-123">**Subscription**: Specify your Azure subscription to use.</span></span>
   - <span data-ttu-id="a311e-124">**Grupo de recursos**: especifique si desea crear un nuevo grupo de recursos o elija uno existente.</span><span class="sxs-lookup"><span data-stu-id="a311e-124">**Resource group**: Specify whether to create a new resource group, or choose an existing resource group.</span></span>
   - <span data-ttu-id="a311e-125">**Seleccionar origen**: para este tutorial, seleccione `Blank` para crear una nueva base de datos.</span><span class="sxs-lookup"><span data-stu-id="a311e-125">**Select source**: For this tutorial, select `Blank` to create a new database.</span></span>
   - <span data-ttu-id="a311e-126">**Inicio de sesión del administrador del servidor**: especifique el nombre del administrador de base de datos.</span><span class="sxs-lookup"><span data-stu-id="a311e-126">**Server admin login**: Specify the database administrator name.</span></span>
   - <span data-ttu-id="a311e-127">**Contraseña** y **Confirmar contraseña**: especifique la contraseña para el administrador de base de datos.</span><span class="sxs-lookup"><span data-stu-id="a311e-127">**Password** and **Confirm password**: Specify the password for your database administrator.</span></span>
   - <span data-ttu-id="a311e-128">**Ubicación**: especifique la región geográfica más cercana a la base de datos.</span><span class="sxs-lookup"><span data-stu-id="a311e-128">**Location**: Specify the closest geographic region for your database.</span></span>
   - <span data-ttu-id="a311e-129">**Versión**: especifique la versión de la base de datos más reciente.</span><span class="sxs-lookup"><span data-stu-id="a311e-129">**Version**: Specify the most-up-to-date database version.</span></span>
   - <span data-ttu-id="a311e-130">**Plan de tarifa**: para este tutorial, especifique el plan de tarifa menos costoso.</span><span class="sxs-lookup"><span data-stu-id="a311e-130">**Pricing tier**: For this tutorial, specify the least-expensive pricing tier.</span></span>

   ![Creación de propiedades de la base de datos de PostgreSQL][POSTGRESQL02]

1. <span data-ttu-id="a311e-132">Cuando haya especificado la información anterior, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="a311e-132">When you have entered all of the above information, click **Create**.</span></span>

### <a name="configure-a-firewall-rule-for-your-postgresql-database-server-using-the-azure-portal"></a><span data-ttu-id="a311e-133">Configuración de una regla de firewall para el servidor de bases de datos PostgreSQL mediante Azure Portal</span><span class="sxs-lookup"><span data-stu-id="a311e-133">Configure a firewall rule for your PostgreSQL database server using the Azure Portal</span></span>

1. <span data-ttu-id="a311e-134">Vaya a Azure Portal en <https://portal.azure.com/> e inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="a311e-134">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="a311e-135">Haga clic en **Todos los recursos** y, a continuación, haga clic en la base de datos de PostgreSQL que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="a311e-135">Click **All Resources**, then click the PostgreSQL database you just created.</span></span>

   ![Selección de la base de datos de PostgreSQL][POSTGRESQL03]

1. <span data-ttu-id="a311e-137">Haga clic en **Seguridad de la conexión** y, en las **reglas de firewall**, cree una nueva regla mediante la especificación de un nombre único para la regla, escriba el intervalo de direcciones IP que necesitará para acceder a la base de datos y, después, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="a311e-137">Click **Connection security**, and in the **Firewall rules**, create a new rule by specifying a unique name for the rule, then enter the range of IP addresses that will need access to your database, and then click **Save**.</span></span>

   ![Configuración de la seguridad de la conexión][POSTGRESQL04]

### <a name="retrieve-the-connection-string-for-your-postgresql-server-using-the-azure-portal"></a><span data-ttu-id="a311e-139">Recuperación de la cadena de conexión para el servidor PostgreSQL mediante Azure Portal</span><span class="sxs-lookup"><span data-stu-id="a311e-139">Retrieve the connection string for your PostgreSQL server using the Azure Portal</span></span>

1. <span data-ttu-id="a311e-140">Vaya a Azure Portal en <https://portal.azure.com/> e inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="a311e-140">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="a311e-141">Haga clic en **Todos los recursos** y, a continuación, haga clic en la base de datos de PostgreSQL que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="a311e-141">Click **All Resources**, then click the PostgreSQL database you just created.</span></span>

   ![Selección de la base de datos de PostgreSQL][POSTGRESQL03]

1. <span data-ttu-id="a311e-143">Haga clic en **Cadenas de conexión** y copie el valor en el campo de texto **JDBC**.</span><span class="sxs-lookup"><span data-stu-id="a311e-143">Click **Connection strings**, and copy the value in the **JDBC** text field.</span></span>

   ![Recuperación de la cadena de conexión JDBC][POSTGRESQL05]

### <a name="create-postgresql-database-using-the-psql-command-line-utility"></a><span data-ttu-id="a311e-145">Creación de la base de datos PostgreSQL mediante la utilidad de línea de comandos `psql`</span><span class="sxs-lookup"><span data-stu-id="a311e-145">Create PostgreSQL database using the `psql` command-line utility</span></span>

1. <span data-ttu-id="a311e-146">Abra un shell de comandos y conéctese al servidor PostgreSQL mediante la escritura de un comando `psql` similar al siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="a311e-146">Open a command shell and connect to your PostgreSQL server by entering a `psql` command like the following example:</span></span>

   ```shell
   psql --host=wingtiptoyspostgresql.postgres.database.azure.com --port=5432 --username=wingtiptoysuser@wingtiptoyspostgresql --dbname=postgres
   ```
   <span data-ttu-id="a311e-147">Donde:</span><span class="sxs-lookup"><span data-stu-id="a311e-147">Where:</span></span>

   | <span data-ttu-id="a311e-148">Parámetro</span><span class="sxs-lookup"><span data-stu-id="a311e-148">Parameter</span></span> | <span data-ttu-id="a311e-149">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="a311e-149">Description</span></span> |
   |---|---|
   | `host` | <span data-ttu-id="a311e-150">Especifica el nombre completo del servidor PostgreSQL que se mencionó anteriormente en este artículo.</span><span class="sxs-lookup"><span data-stu-id="a311e-150">Specifies your fully qualified PostgreSQL server name from earlier in this article.</span></span> |
   | `host` | <span data-ttu-id="a311e-151">Especifica el puerto del servidor PostgreSQL, que es `5432` de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="a311e-151">Specifies the PostgreSQL server port, which is `5432` by default.</span></span> |
   | `username` | <span data-ttu-id="a311e-152">Especifica el administrador de PostgreSQL y el nombre de servidor abreviado que se mencionaron anteriormente en este artículo.</span><span class="sxs-lookup"><span data-stu-id="a311e-152">Specifies your PostgreSQL administrator and shortened server name from earlier in this article.</span></span> |
   | `dbname` | <span data-ttu-id="a311e-153">Especifica que desea usar la base de datos predeterminada `postgres` por ahora.</span><span class="sxs-lookup"><span data-stu-id="a311e-153">Specifies that you want to use the default `postgres` database for now.</span></span> |

   <span data-ttu-id="a311e-154">El servidor PostgreSQL debería responder con una pantalla similar al ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="a311e-154">Your PostgreSQL server should respond with a display like the following example:</span></span>

   ```shell
   psql (9.3.24, server 10.5)
   SSL connection (cipher: ECDHE-RSA-AES256-SHA384, bits: 256)
   Type "help" for help.
   
   postgres=>
   ```

1. <span data-ttu-id="a311e-155">Cree una base de datos denominada *mypgsqldb* mediante la escritura de un comando `psql` similar al ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="a311e-155">Create a database named *mypgsqldb* by entering a `psql` command like the following example:</span></span>

   ```SQL
   CREATE DATABASE mypgsqldb;
   ```

   <span data-ttu-id="a311e-156">El servidor PostgreSQL debería responder con una pantalla similar al ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="a311e-156">Your PostgreSQL server should respond with a display like the following example:</span></span>

   ```shell
   CREATE DATABASE
   ```

1. <span data-ttu-id="a311e-157">OPCIONAL: Puede comprobar que se creó la base de datos mediante la escritura de `\l` en `psql`; el servidor PostgreSQL debería responder con algo similar al ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="a311e-157">OPTIONAL: You can verify that your database was created by entering a `\l` at the `psql`; your PostgreSQL server should respond with something like the following example:</span></span>

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

1. <span data-ttu-id="a311e-158">Escriba `\q` para salir de la utilidad `psql`.</span><span class="sxs-lookup"><span data-stu-id="a311e-158">Enter `\q` to exit the `psql` utility.</span></span>

## <a name="configure-the-sample-application"></a><span data-ttu-id="a311e-159">Configurar la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="a311e-159">Configure the sample application</span></span>

1. <span data-ttu-id="a311e-160">Abra un shell de comandos y clone el proyecto de ejemplo con un comando git como el siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="a311e-160">Open a command shell and clone the sample project using a git command like the following example:</span></span>

   ```shell
   git clone https://github.com/Azure-Samples/spring-data-jdbc-on-azure.git
   ```

1. <span data-ttu-id="a311e-161">Busque el archivo *application.properties* en el directorio *resources* del proyecto de ejemplo, o cree el archivo si todavía no existe.</span><span class="sxs-lookup"><span data-stu-id="a311e-161">Locate the *application.properties* file in the *resources* directory of the sample project, or create the file if it does not already exist.</span></span>

1. <span data-ttu-id="a311e-162">Abra el archivo *application.properties* en un editor de texto y agréguele o configure las siguientes líneas; luego, sustituya los valores de ejemplo por los valores adecuados que se mencionaron anteriormente:</span><span class="sxs-lookup"><span data-stu-id="a311e-162">Open the *application.properties* file in a text editor, and add or configure the following lines in the file, and replace the sample values with the appropriate values from earlier:</span></span>

   ```yaml
   spring.datasource.url=jdbc:postgresql://wingtiptoyspostgresql.postgres.database.azure.com:5432/mypgsqldb?ssl=true&sslmode=prefer
   spring.datasource.username=wingtiptoysuser@wingtiptoyspostgresql
   spring.datasource.password=********
    ```
   <span data-ttu-id="a311e-163">Donde:</span><span class="sxs-lookup"><span data-stu-id="a311e-163">Where:</span></span>

   | <span data-ttu-id="a311e-164">Parámetro</span><span class="sxs-lookup"><span data-stu-id="a311e-164">Parameter</span></span> | <span data-ttu-id="a311e-165">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="a311e-165">Description</span></span> |
   |---|---|
   | `spring.datasource.url` | <span data-ttu-id="a311e-166">Especifica la cadena de JDBC de PostgreSQL que se mencionó anteriormente en este artículo.</span><span class="sxs-lookup"><span data-stu-id="a311e-166">Specifies your PostgreSQL JDBC string from earlier in this article.</span></span> |
   | `spring.datasource.username` | <span data-ttu-id="a311e-167">Especifica el nombre del administrador de PostgreSQL que se mencionó anteriormente en este artículo, con el nombre abreviado del servidor anexado.</span><span class="sxs-lookup"><span data-stu-id="a311e-167">Specifies your PostgreSQL administrator name from earlier in this article, with the shortened server name appended to it.</span></span> |
   | `spring.datasource.password` | <span data-ttu-id="a311e-168">Especifica la contraseña de administrador de PostgreSQL que se mencionó anteriormente en este artículo.</span><span class="sxs-lookup"><span data-stu-id="a311e-168">Specifies your PostgreSQL administrator password from earlier in this article.</span></span> |

1. <span data-ttu-id="a311e-169">Guarde y cierre el archivo *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="a311e-169">Save and close the *application.properties* file.</span></span>

## <a name="package-and-test-the-sample-application"></a><span data-ttu-id="a311e-170">Empaquetado y prueba de la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="a311e-170">Package and test the sample application</span></span> 

1. <span data-ttu-id="a311e-171">Compile la aplicación de ejemplo con Maven; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="a311e-171">Build the sample application with Maven; for example:</span></span>

   ```shell
   mvn clean package -P postgresql
   ```

1. <span data-ttu-id="a311e-172">Inicie la aplicación de ejemplo; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="a311e-172">Start the sample application; for example:</span></span>

   ```shell
   java -jar target/spring-data-jdbc-on-azure-0.1.0-SNAPSHOT.jar
   ```

1. <span data-ttu-id="a311e-173">Cree nuevos registros con `curl` desde un símbolo del sistema como en los ejemplos siguientes:</span><span class="sxs-lookup"><span data-stu-id="a311e-173">Create new records using `curl` from a command prompt like the following examples:</span></span>

   ```shell
   curl -s -d '{"name":"dog","species":"canine"}' -H "Content-Type: application/json" -X POST http://localhost:8080/pets

   curl -s -d '{"name":"cat","species":"feline"}' -H "Content-Type: application/json" -X POST http://localhost:8080/pets
   ```

   <span data-ttu-id="a311e-174">La aplicación debe devolver valores similares a los siguientes:</span><span class="sxs-lookup"><span data-stu-id="a311e-174">Your application should return values like the following:</span></span>

   ```shell
   Added Pet(id=1, name=dog, species=canine).

   Added Pet(id=2, name=cat, species=feline).
   ```

1. <span data-ttu-id="a311e-175">Recupere todos los registros existentes con `curl` desde un símbolo del sistema como los siguientes ejemplos:</span><span class="sxs-lookup"><span data-stu-id="a311e-175">Retrieve all of the existing records using `curl` from a command prompt like the following examples:</span></span>

   ```shell
   curl -s http://localhost:8080/pets
   ```
    
   <span data-ttu-id="a311e-176">La aplicación debe devolver valores similares a los siguientes:</span><span class="sxs-lookup"><span data-stu-id="a311e-176">Your application should return values like the following:</span></span>

   ```json
   [{"id":1,"name":"dog","species":"canine"},{"id":2,"name":"cat","species":"feline"}]
   ```

## <a name="summary"></a><span data-ttu-id="a311e-177">Resumen</span><span class="sxs-lookup"><span data-stu-id="a311e-177">Summary</span></span>

<span data-ttu-id="a311e-178">En este tutorial ha creado una aplicación Java de ejemplo que Spring Data para almacenar y recuperar información de una base de datos PostgreSQL de Azure mediante JDBC.</span><span class="sxs-lookup"><span data-stu-id="a311e-178">In this tutorial, you created a sample Java application that uses Spring Data to store and retrieve information in an Azure PostgreSQL database using JDBC.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a311e-179">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a311e-179">Next steps</span></span>

<span data-ttu-id="a311e-180">Para más información acerca de Spring y Azure, vaya al centro de documentación de Azure.</span><span class="sxs-lookup"><span data-stu-id="a311e-180">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a311e-181">Spring en Azure</span><span class="sxs-lookup"><span data-stu-id="a311e-181">Spring on Azure</span></span>](/java/azure/spring-framework)

### <a name="additional-resources"></a><span data-ttu-id="a311e-182">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="a311e-182">Additional Resources</span></span>

<span data-ttu-id="a311e-183">Para más información sobre el uso de Azure con Java, consulte [Azure para desarrolladores de Java] y [Working with Azure DevOps and Java] (Trabajo con Azure DevOps y Java).</span><span class="sxs-lookup"><span data-stu-id="a311e-183">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Working with Azure DevOps and Java].</span></span>

<!-- URL List -->

[Azure para desarrolladores de Java]: /java/azure/
[Azure for Java Developers]: /java/azure/
[cuenta de Azure gratuita]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Working with Azure DevOps and Java]: /azure/devops/ (Trabajo con Azure DevOps y Java)
[ventajas como suscriptor de MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
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
