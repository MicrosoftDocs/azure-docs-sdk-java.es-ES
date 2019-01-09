---
title: Uso de Spring Data JPA con PostgreSQL de Azure
description: Aprenda a usar Spring Data de JPA con una base de datos PostgreSQL de Azure.
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
ms.openlocfilehash: 1849e03674534882a579f85b2654a628bd867487
ms.sourcegitcommit: f0f140b0862ca5338b1b7e5c33cec3e58a70b8fd
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/03/2019
ms.locfileid: "53992514"
---
# <a name="how-to-use-spring-data-jpa-with-azure-postgresql"></a><span data-ttu-id="1b2f6-103">Uso de Spring Data JPA con PostgreSQL de Azure</span><span class="sxs-lookup"><span data-stu-id="1b2f6-103">How to use Spring Data JPA with Azure PostgreSQL</span></span>

## <a name="overview"></a><span data-ttu-id="1b2f6-104">Información general</span><span class="sxs-lookup"><span data-stu-id="1b2f6-104">Overview</span></span>

<span data-ttu-id="1b2f6-105">En este artículo se explica cómo crear una aplicación de ejemplo que utiliza [Spring Data] para almacenar y recuperar información en una base de datos [PostgreSQL]https://www.postgresql.org/ de Azure mediante [Java Persistence API (JPA)](https://docs.oracle.com/javaee/7/tutorial/persistence-intro.htm).</span><span class="sxs-lookup"><span data-stu-id="1b2f6-105">This article demonstrates creating a sample application that uses [Spring Data] to store and retrieve information in an Azure [PostgreSQL]https://www.postgresql.org/ database using [Java Persistence API (JPA)](https://docs.oracle.com/javaee/7/tutorial/persistence-intro.htm).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1b2f6-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="1b2f6-106">Prerequisites</span></span>

<span data-ttu-id="1b2f6-107">Los siguientes requisitos previos son necesarios para seguir los pasos descritos en este artículo:</span><span class="sxs-lookup"><span data-stu-id="1b2f6-107">The following prerequisites are required in order to complete the steps in this article:</span></span>

* <span data-ttu-id="1b2f6-108">Una suscripción de Azure. Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN] o registrarse para obtener una [cuenta de Azure gratuita].</span><span class="sxs-lookup"><span data-stu-id="1b2f6-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="1b2f6-109">Un kit de desarrollo de Java (JDK) admitido</span><span class="sxs-lookup"><span data-stu-id="1b2f6-109">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="1b2f6-110">Para más información sobre los JDK disponibles para desarrollar en Azure, consulte <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="1b2f6-110">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="1b2f6-111">[Apache Maven](http://maven.apache.org/), versión 3.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="1b2f6-111">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>
* <span data-ttu-id="1b2f6-112">[Curl ](https://curl.haxx.se/) o una utilidad HTTP similar para probar la funcionalidad.</span><span class="sxs-lookup"><span data-stu-id="1b2f6-112">[Curl](https://curl.haxx.se/) or similar HTTP utility to test functionality.</span></span> <span data-ttu-id="1b2f6-113">o una utilidad HTTP similar para probar la funcionalidad.</span><span class="sxs-lookup"><span data-stu-id="1b2f6-113">or similar HTTP utility to test functionality.</span></span>
* <span data-ttu-id="1b2f6-114">Utilidad de línea de comandos [psql](https://www.postgresql.org/docs/current/app-psql.html).</span><span class="sxs-lookup"><span data-stu-id="1b2f6-114">The [psql](https://www.postgresql.org/docs/current/app-psql.html) command-line utility.</span></span>
* <span data-ttu-id="1b2f6-115">Un cliente [Git](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="1b2f6-115">A [Git](https://git-scm.com/downloads) client.</span></span>

## <a name="create-a-postgresql-database-for-azure"></a><span data-ttu-id="1b2f6-116">Creación de una base de datos PostgreSQL para Azure</span><span class="sxs-lookup"><span data-stu-id="1b2f6-116">Create a PostgreSQL database for Azure</span></span>

### <a name="create-a-postgresql-database-server-using-the-azure-portal"></a><span data-ttu-id="1b2f6-117">Creación de un servidor de bases de datos PostgreSQL mediante Azure Portal</span><span class="sxs-lookup"><span data-stu-id="1b2f6-117">Create a PostgreSQL database server using the Azure Portal</span></span>

> [!NOTE]
> 
> <span data-ttu-id="1b2f6-118">Puede leer información más detallada sobre la creación de bases de datos PostgreSQL en [Creación de un servidor de Azure Database for PostgreSQL mediante Azure Portal](/azure/postgresql/quickstart-create-server-database-portal).</span><span class="sxs-lookup"><span data-stu-id="1b2f6-118">You can read more detailed information about creating PostgreSQL databases in [Create an Azure Database for PostgreSQL server by using the Azure portal](/azure/postgresql/quickstart-create-server-database-portal).</span></span>

1. <span data-ttu-id="1b2f6-119">Vaya a Azure Portal en <https://portal.azure.com/> e inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="1b2f6-119">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="1b2f6-120">Haga clic sucesivamente en **+Crear un recurso**, después en **Bases de datos** y, finalmente en **Azure Database for PostgreSQL**.</span><span class="sxs-lookup"><span data-stu-id="1b2f6-120">Click **+Create a resource**, then **Databases**, and then click **Azure Database for PostgreSQL**.</span></span>

   ![Creación de una base de datos PostgreSQL][POSTGRESQL01]

1. <span data-ttu-id="1b2f6-122">Escriba la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="1b2f6-122">Enter the following information:</span></span>

   - <span data-ttu-id="1b2f6-123">**Nombre del servidor**: elija un nombre único para el servidor PostgreSQL; se utilizará para crear un nombre de dominio completo como *wingtiptoyspostgresql.postgres.database.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="1b2f6-123">**Server name**: Choose a unique name for your PostgreSQL server; this will be used to create a fully-qualified domain name like *wingtiptoyspostgresql.postgres.database.azure.com*.</span></span>
   - <span data-ttu-id="1b2f6-124">**Suscripción**: especifique la suscripción de Azure que se va a usar.</span><span class="sxs-lookup"><span data-stu-id="1b2f6-124">**Subscription**: Specify your Azure subscription to use.</span></span>
   - <span data-ttu-id="1b2f6-125">**Grupo de recursos**: especifique si desea crear un nuevo grupo de recursos o elija uno existente.</span><span class="sxs-lookup"><span data-stu-id="1b2f6-125">**Resource group**: Specify whether to create a new resource group, or choose an existing resource group.</span></span>
   - <span data-ttu-id="1b2f6-126">**Seleccionar origen**: para este tutorial, seleccione `Blank` para crear una nueva base de datos.</span><span class="sxs-lookup"><span data-stu-id="1b2f6-126">**Select source**: For this tutorial, select `Blank` to create a new database.</span></span>
   - <span data-ttu-id="1b2f6-127">**Inicio de sesión del administrador del servidor**: especifique el nombre del administrador de base de datos.</span><span class="sxs-lookup"><span data-stu-id="1b2f6-127">**Server admin login**: Specify the database administrator name.</span></span>
   - <span data-ttu-id="1b2f6-128">**Contraseña** y **Confirmar contraseña**: especifique la contraseña para el administrador de base de datos.</span><span class="sxs-lookup"><span data-stu-id="1b2f6-128">**Password** and **Confirm password**: Specify the password for your database administrator.</span></span>
   - <span data-ttu-id="1b2f6-129">**Ubicación**: especifique la región geográfica más cercana a la base de datos.</span><span class="sxs-lookup"><span data-stu-id="1b2f6-129">**Location**: Specify the closest geographic region for your database.</span></span>
   - <span data-ttu-id="1b2f6-130">**Versión**: especifique la versión de la base de datos más reciente.</span><span class="sxs-lookup"><span data-stu-id="1b2f6-130">**Version**: Specify the most-up-to-date database version.</span></span>
   - <span data-ttu-id="1b2f6-131">**Plan de tarifa**: para este tutorial, especifique el plan de tarifa menos costoso.</span><span class="sxs-lookup"><span data-stu-id="1b2f6-131">**Pricing tier**: For this tutorial, specify the least-expensive pricing tier.</span></span>

   ![Creación de propiedades de la base de datos de PostgreSQL][POSTGRESQL02]

1. <span data-ttu-id="1b2f6-133">Cuando haya especificado la información anterior, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="1b2f6-133">When you have entered all of the above information, click **Create**.</span></span>

### <a name="configure-a-firewall-rule-for-your-postgresql-database-server-using-the-azure-portal"></a><span data-ttu-id="1b2f6-134">Configuración de una regla de firewall para el servidor de bases de datos PostgreSQL mediante Azure Portal</span><span class="sxs-lookup"><span data-stu-id="1b2f6-134">Configure a firewall rule for your PostgreSQL database server using the Azure Portal</span></span>

1. <span data-ttu-id="1b2f6-135">Vaya a Azure Portal en <https://portal.azure.com/> e inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="1b2f6-135">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="1b2f6-136">Haga clic en **Todos los recursos** y, a continuación, haga clic en la base de datos de PostgreSQL que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="1b2f6-136">Click **All Resources**, then click the PostgreSQL database you just created.</span></span>

   ![Selección de la base de datos de PostgreSQL][POSTGRESQL03]

1. <span data-ttu-id="1b2f6-138">Haga clic en **Seguridad de la conexión** y, en las **reglas de firewall**, cree una nueva regla mediante la especificación de un nombre único para la regla, escriba el intervalo de direcciones IP que necesitará para acceder a la base de datos y, después, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="1b2f6-138">Click **Connection security**, and in the **Firewall rules**, create a new rule by specifying a unique name for the rule, then enter the range of IP addresses that will need access to your database, and then click **Save**.</span></span>

   ![Configuración de la seguridad de la conexión][POSTGRESQL04]

### <a name="retrieve-the-connection-string-for-your-postgresql-server-using-the-azure-portal"></a><span data-ttu-id="1b2f6-140">Recuperación de la cadena de conexión para el servidor PostgreSQL mediante Azure Portal</span><span class="sxs-lookup"><span data-stu-id="1b2f6-140">Retrieve the connection string for your PostgreSQL server using the Azure Portal</span></span>

1. <span data-ttu-id="1b2f6-141">Vaya a Azure Portal en <https://portal.azure.com/> e inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="1b2f6-141">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="1b2f6-142">Haga clic en **Todos los recursos** y, a continuación, haga clic en la base de datos de PostgreSQL que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="1b2f6-142">Click **All Resources**, then click the PostgreSQL database you just created.</span></span>

   ![Selección de la base de datos de PostgreSQL][POSTGRESQL03]

1. <span data-ttu-id="1b2f6-144">Haga clic en **Cadenas de conexión** y copie el valor en el campo de texto **JDBC**.</span><span class="sxs-lookup"><span data-stu-id="1b2f6-144">Click **Connection strings**, and copy the value in the **JDBC** text field.</span></span>

   ![Recuperación de la cadena de conexión JDBC][POSTGRESQL05]

### <a name="create-postgresql-database-using-the-psql-command-line-utility"></a><span data-ttu-id="1b2f6-146">Creación de la base de datos PostgreSQL mediante la utilidad de línea de comandos `psql`</span><span class="sxs-lookup"><span data-stu-id="1b2f6-146">Create PostgreSQL database using the `psql` command-line utility</span></span>

1. <span data-ttu-id="1b2f6-147">Abra un shell de comandos y conéctese al servidor PostgreSQL mediante la escritura de un comando `psql` similar al siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="1b2f6-147">Open a command shell and connect to your PostgreSQL server by entering a `psql` command like the following example:</span></span>

   ```shell
   psql --host=wingtiptoyspostgresql.postgres.database.azure.com --port=5432 --username=wingtiptoysuser@wingtiptoyspostgresql --dbname=postgres
   ```
   <span data-ttu-id="1b2f6-148">Donde:</span><span class="sxs-lookup"><span data-stu-id="1b2f6-148">Where:</span></span>

   | <span data-ttu-id="1b2f6-149">Parámetro</span><span class="sxs-lookup"><span data-stu-id="1b2f6-149">Parameter</span></span> | <span data-ttu-id="1b2f6-150">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="1b2f6-150">Description</span></span> |
   |---|---|
   | `host` | <span data-ttu-id="1b2f6-151">Especifica el nombre completo del servidor PostgreSQL que se mencionó anteriormente en este artículo.</span><span class="sxs-lookup"><span data-stu-id="1b2f6-151">Specifies your fully qualified PostgreSQL server name from earlier in this article.</span></span> |
   | `host` | <span data-ttu-id="1b2f6-152">Especifica el puerto del servidor PostgreSQL, que es `5432` de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="1b2f6-152">Specifies the PostgreSQL server port, which is `5432` by default.</span></span> |
   | `username` | <span data-ttu-id="1b2f6-153">Especifica el administrador de PostgreSQL y el nombre de servidor abreviado que se mencionaron anteriormente en este artículo.</span><span class="sxs-lookup"><span data-stu-id="1b2f6-153">Specifies your PostgreSQL administrator and shortened server name from earlier in this article.</span></span> |
   | `dbname` | <span data-ttu-id="1b2f6-154">Especifica que desea usar la base de datos predeterminada `postgres` por ahora.</span><span class="sxs-lookup"><span data-stu-id="1b2f6-154">Specifies that you want to use the default `postgres` database for now.</span></span> |

   <span data-ttu-id="1b2f6-155">El servidor PostgreSQL debería responder con una pantalla similar al ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="1b2f6-155">Your PostgreSQL server should respond with a display like the following example:</span></span>

   ```shell
   psql (9.3.24, server 10.5)
   SSL connection (cipher: ECDHE-RSA-AES256-SHA384, bits: 256)
   Type "help" for help.
   
   postgres=>
   ```

1. <span data-ttu-id="1b2f6-156">Cree una base de datos denominada *mypgsqldb* mediante la escritura de un comando `psql` similar al ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="1b2f6-156">Create a database named *mypgsqldb* by entering a `psql` command like the following example:</span></span>

   ```SQL
   CREATE DATABASE mypgsqldb;
   ```

   <span data-ttu-id="1b2f6-157">El servidor PostgreSQL debería responder con una pantalla similar al ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="1b2f6-157">Your PostgreSQL server should respond with a display like the following example:</span></span>

   ```shell
   CREATE DATABASE
   ```

1. <span data-ttu-id="1b2f6-158">OPCIONAL: Puede comprobar que se creó la base de datos mediante la escritura de `\l` en `psql`; el servidor PostgreSQL debería responder con algo similar al ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="1b2f6-158">OPTIONAL: You can verify that your database was created by entering a `\l` at the `psql`; your PostgreSQL server should respond with something like the following example:</span></span>

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

1. <span data-ttu-id="1b2f6-159">Escriba `\q` para salir de la utilidad `psql`.</span><span class="sxs-lookup"><span data-stu-id="1b2f6-159">Enter `\q` to exit the `psql` utility.</span></span>

## <a name="configure-the-sample-application"></a><span data-ttu-id="1b2f6-160">Configurar la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="1b2f6-160">Configure the sample application</span></span>

1. <span data-ttu-id="1b2f6-161">Abra un shell de comandos y clone el proyecto de ejemplo con un comando git como el siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="1b2f6-161">Open a command shell and clone the sample project using a git command like the following example:</span></span>

   ```shell
   git clone https://github.com/Azure-Samples/spring-data-jpa-on-azure.git
   ```

1. <span data-ttu-id="1b2f6-162">Busque el archivo *application.properties* en el directorio *resources* del proyecto de ejemplo, o cree el archivo si todavía no existe.</span><span class="sxs-lookup"><span data-stu-id="1b2f6-162">Locate the *application.properties* file in the *resources* directory of the sample project, or create the file if it does not already exist.</span></span>

1. <span data-ttu-id="1b2f6-163">Abra el archivo *application.properties* en un editor de texto y agréguele o configure las siguientes líneas; luego, sustituya los valores de ejemplo por los valores adecuados que se mencionaron anteriormente:</span><span class="sxs-lookup"><span data-stu-id="1b2f6-163">Open the *application.properties* file in a text editor, and add or configure the following lines in the file, and replace the sample values with the appropriate values from earlier:</span></span>

   ```yaml
   spring.datasource.url=jdbc:postgresql://wingtiptoyspostgresql.postgres.database.azure.com:5432/mypgsqldb?ssl=true&sslmode=prefer
   spring.datasource.username=wingtiptoysuser@wingtiptoyspostgresql
   spring.datasource.password=********
    ```
   <span data-ttu-id="1b2f6-164">Donde:</span><span class="sxs-lookup"><span data-stu-id="1b2f6-164">Where:</span></span>

   | <span data-ttu-id="1b2f6-165">Parámetro</span><span class="sxs-lookup"><span data-stu-id="1b2f6-165">Parameter</span></span> | <span data-ttu-id="1b2f6-166">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="1b2f6-166">Description</span></span> |
   |---|---|
   | `spring.datasource.url` | <span data-ttu-id="1b2f6-167">Especifica la cadena de JDBC de PostgreSQL que se mencionó anteriormente en este artículo.</span><span class="sxs-lookup"><span data-stu-id="1b2f6-167">Specifies your PostgreSQL JDBC string from earlier in this article.</span></span> |
   | `spring.datasource.username` | <span data-ttu-id="1b2f6-168">Especifica el nombre del administrador de PostgreSQL que se mencionó anteriormente en este artículo, con el nombre abreviado del servidor anexado.</span><span class="sxs-lookup"><span data-stu-id="1b2f6-168">Specifies your PostgreSQL administrator name from earlier in this article, with the shortened server name appended to it.</span></span> |
   | `spring.datasource.password` | <span data-ttu-id="1b2f6-169">Especifica la contraseña de administrador de PostgreSQL que se mencionó anteriormente en este artículo.</span><span class="sxs-lookup"><span data-stu-id="1b2f6-169">Specifies your PostgreSQL administrator password from earlier in this article.</span></span> |

1. <span data-ttu-id="1b2f6-170">Guarde y cierre el archivo *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="1b2f6-170">Save and close the *application.properties* file.</span></span>

## <a name="package-and-test-the-sample-application"></a><span data-ttu-id="1b2f6-171">Empaquetado y prueba de la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="1b2f6-171">Package and test the sample application</span></span> 

1. <span data-ttu-id="1b2f6-172">Compile la aplicación de ejemplo con Maven; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="1b2f6-172">Build the sample application with Maven; for example:</span></span>

   ```shell
   mvn clean package -P postgresql
   ```

1. <span data-ttu-id="1b2f6-173">Inicie la aplicación de ejemplo; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="1b2f6-173">Start the sample application; for example:</span></span>

   ```shell
   java -jar target/spring-data-jdbc-on-azure-0.1.0-SNAPSHOT.jar
   ```

1. <span data-ttu-id="1b2f6-174">Cree nuevos registros con `curl` desde un símbolo del sistema como en los ejemplos siguientes:</span><span class="sxs-lookup"><span data-stu-id="1b2f6-174">Create new records using `curl` from a command prompt like the following examples:</span></span>

   ```shell
   curl -s -d '{"name":"dog","species":"canine"}' -H "Content-Type: application/json" -X POST http://localhost:8080/pets

   curl -s -d '{"name":"cat","species":"feline"}' -H "Content-Type: application/json" -X POST http://localhost:8080/pets
   ```

   <span data-ttu-id="1b2f6-175">La aplicación debe devolver valores similares a los siguientes:</span><span class="sxs-lookup"><span data-stu-id="1b2f6-175">Your application should return values like the following:</span></span>

   ```shell
   Added Pet(id=1, name=dog, species=canine).

   Added Pet(id=2, name=cat, species=feline).
   ```

1. <span data-ttu-id="1b2f6-176">Recupere todos los registros existentes con `curl` desde un símbolo del sistema como los siguientes ejemplos:</span><span class="sxs-lookup"><span data-stu-id="1b2f6-176">Retrieve all of the existing records using `curl` from a command prompt like the following examples:</span></span>

   ```shell
   curl -s http://localhost:8080/pets
   ```
    
   <span data-ttu-id="1b2f6-177">La aplicación debe devolver valores similares a los siguientes:</span><span class="sxs-lookup"><span data-stu-id="1b2f6-177">Your application should return values like the following:</span></span>

   ```json
   [{"id":1,"name":"dog","species":"canine"},{"id":2,"name":"cat","species":"feline"}]
   ```

## <a name="summary"></a><span data-ttu-id="1b2f6-178">Resumen</span><span class="sxs-lookup"><span data-stu-id="1b2f6-178">Summary</span></span>

<span data-ttu-id="1b2f6-179">En este tutorial ha creado una aplicación Java de ejemplo que Spring Data para almacenar y recuperar información de una base de datos PostgreSQL de Azure mediante JPA.</span><span class="sxs-lookup"><span data-stu-id="1b2f6-179">In this tutorial, you created a sample Java application that uses Spring Data to store and retrieve information in an Azure PostgreSQL database using JPA.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1b2f6-180">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1b2f6-180">Next steps</span></span>

<span data-ttu-id="1b2f6-181">Para más información acerca de Spring y Azure, vaya al centro de documentación de Azure.</span><span class="sxs-lookup"><span data-stu-id="1b2f6-181">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1b2f6-182">Spring en Azure</span><span class="sxs-lookup"><span data-stu-id="1b2f6-182">Spring on Azure</span></span>](/java/azure/spring-framework)

### <a name="additional-resources"></a><span data-ttu-id="1b2f6-183">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="1b2f6-183">Additional Resources</span></span>

<span data-ttu-id="1b2f6-184">Para más información sobre el uso de Azure con Java, consulte [Azure para desarrolladores de Java] y [Working with Azure DevOps and Java] (Trabajo con Azure DevOps y Java).</span><span class="sxs-lookup"><span data-stu-id="1b2f6-184">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Working with Azure DevOps and Java].</span></span>

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

[POSTGRESQL01]: media/configure-spring-data-jpa-with-azure-postgresql/create-postgresql-01.png
[POSTGRESQL02]: media/configure-spring-data-jpa-with-azure-postgresql/create-postgresql-02.png
[POSTGRESQL03]: media/configure-spring-data-jpa-with-azure-postgresql/create-postgresql-03.png
[POSTGRESQL04]: media/configure-spring-data-jpa-with-azure-postgresql/create-postgresql-04.png
[POSTGRESQL05]: media/configure-spring-data-jpa-with-azure-postgresql/create-postgresql-05.png
