---
title: Uso de Spring Data JDBC con MySQL de Azure
description: Aprenda a usar Spring Data JDBC con una base de datos MySQL de Azure.
services: mysql
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 12/19/2018
ms.devlang: java
ms.service: mysql
ms.tgt_pltfrm: multiple
ms.topic: article
ms.openlocfilehash: 5ec89194c72cef81c79d21382e41b33ebe91d3d0
ms.sourcegitcommit: f0f140b0862ca5338b1b7e5c33cec3e58a70b8fd
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/03/2019
ms.locfileid: "53992507"
---
# <a name="how-to-use-spring-data-jdbc-with-azure-mysql"></a><span data-ttu-id="678e9-103">Uso de Spring Data JDBC con MySQL de Azure</span><span class="sxs-lookup"><span data-stu-id="678e9-103">How to use Spring Data JDBC with Azure MySQL</span></span>

## <a name="overview"></a><span data-ttu-id="678e9-104">Información general</span><span class="sxs-lookup"><span data-stu-id="678e9-104">Overview</span></span>

<span data-ttu-id="678e9-105">En este artículo se explica cómo crear una aplicación de ejemplo que utiliza [Spring Data] para almacenar y recuperar información en una base de datos [MySQL](https://www.mysql.com/) de Azure mediante [Java Database Connectivity (JDBC)](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/).</span><span class="sxs-lookup"><span data-stu-id="678e9-105">This article demonstrates creating a sample application that uses [Spring Data] to store and retrieve information in an Azure [MySQL](https://www.mysql.com/) database using [Java Database Connectivity (JDBC)](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="678e9-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="678e9-106">Prerequisites</span></span>

<span data-ttu-id="678e9-107">Los siguientes requisitos previos son necesarios para seguir los pasos descritos en este artículo:</span><span class="sxs-lookup"><span data-stu-id="678e9-107">The following prerequisites are required in order to complete the steps in this article:</span></span>

* <span data-ttu-id="678e9-108">Una suscripción de Azure. Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN] o registrarse para obtener una [cuenta de Azure gratuita].</span><span class="sxs-lookup"><span data-stu-id="678e9-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="678e9-109">Un kit de desarrollo de Java (JDK) admitido</span><span class="sxs-lookup"><span data-stu-id="678e9-109">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="678e9-110">Para más información sobre los JDK disponibles para desarrollar en Azure, consulte <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="678e9-110">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="678e9-111">[Apache Maven](http://maven.apache.org/), versión 3.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="678e9-111">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>
* <span data-ttu-id="678e9-112">[Curl ](https://curl.haxx.se/) o una utilidad HTTP similar para probar la funcionalidad.</span><span class="sxs-lookup"><span data-stu-id="678e9-112">[Curl](https://curl.haxx.se/) or similar HTTP utility to test functionality.</span></span>
* <span data-ttu-id="678e9-113">Utilidad de línea de comandos [mysql](https://dev.mysql.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="678e9-113">The [mysql](https://dev.mysql.com/downloads/) command-line utility.</span></span>
* <span data-ttu-id="678e9-114">Un cliente [Git](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="678e9-114">A [Git](https://git-scm.com/downloads) client.</span></span>

## <a name="create-a-mysql-database-for-azure"></a><span data-ttu-id="678e9-115">Creación de una base de datos MySQL para Azure</span><span class="sxs-lookup"><span data-stu-id="678e9-115">Create a MySQL database for Azure</span></span>

### <a name="create-a-mysql-database-server-using-the-azure-portal"></a><span data-ttu-id="678e9-116">Creación de un servidor de bases de datos MySQL mediante Azure Portal</span><span class="sxs-lookup"><span data-stu-id="678e9-116">Create a MySQL database server using the Azure Portal</span></span>

> [!NOTE]
> 
> <span data-ttu-id="678e9-117">Puede leer información más detallada sobre la creación de bases de datos MySQL en [Creación de un servidor de Azure Database for MySQL mediante Azure Portal](/azure/mysql/quickstart-create-mysql-server-database-using-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="678e9-117">You can read more detailed information about creating MySQL databases in [Create an Azure Database for MySQL server by using the Azure portal](/azure/mysql/quickstart-create-mysql-server-database-using-azure-portal).</span></span>

1. <span data-ttu-id="678e9-118">Vaya a Azure Portal en <https://portal.azure.com/> e inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="678e9-118">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="678e9-119">Haga clic sucesivamente en **+Crear un recurso**, después en **Bases de datos** y, finalmente en **Azure Database for MySQL**.</span><span class="sxs-lookup"><span data-stu-id="678e9-119">Click **+Create a resource**, then **Databases**, and then click **Azure Database for MySQL**.</span></span>

   ![Creación de una base de datos MySQL][MYSQL01]

1. <span data-ttu-id="678e9-121">Escriba la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="678e9-121">Enter the following information:</span></span>

   - <span data-ttu-id="678e9-122">**Nombre del servidor**: Elija un nombre único para el servidor MySQL; se utilizará para crear un nombre de dominio completo como *wingtiptoysmysql.mysql.database.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="678e9-122">**Server name**: Choose a unique name for your MySQL server; this will be used to create a fully-qualified domain name like *wingtiptoysmysql.mysql.database.azure.com*.</span></span>
   - <span data-ttu-id="678e9-123">**Suscripción**: especifique la suscripción de Azure que se va a usar.</span><span class="sxs-lookup"><span data-stu-id="678e9-123">**Subscription**: Specify your Azure subscription to use.</span></span>
   - <span data-ttu-id="678e9-124">**Grupo de recursos**: especifique si desea crear un nuevo grupo de recursos o elija uno existente.</span><span class="sxs-lookup"><span data-stu-id="678e9-124">**Resource group**: Specify whether to create a new resource group, or choose an existing resource group.</span></span>
   - <span data-ttu-id="678e9-125">**Seleccionar origen**: para este tutorial, seleccione `Blank` para crear una nueva base de datos.</span><span class="sxs-lookup"><span data-stu-id="678e9-125">**Select source**: For this tutorial, select `Blank` to create a new database.</span></span>
   - <span data-ttu-id="678e9-126">**Inicio de sesión del administrador del servidor**: especifique el nombre del administrador de base de datos.</span><span class="sxs-lookup"><span data-stu-id="678e9-126">**Server admin login**: Specify the database administrator name.</span></span>
   - <span data-ttu-id="678e9-127">**Contraseña** y **Confirmar contraseña**: especifique la contraseña para el administrador de base de datos.</span><span class="sxs-lookup"><span data-stu-id="678e9-127">**Password** and **Confirm password**: Specify the password for your database administrator.</span></span>
   - <span data-ttu-id="678e9-128">**Ubicación**: especifique la región geográfica más cercana a la base de datos.</span><span class="sxs-lookup"><span data-stu-id="678e9-128">**Location**: Specify the closest geographic region for your database.</span></span>
   - <span data-ttu-id="678e9-129">**Versión**: especifique la versión de la base de datos más reciente.</span><span class="sxs-lookup"><span data-stu-id="678e9-129">**Version**: Specify the most-up-to-date database version.</span></span>
   - <span data-ttu-id="678e9-130">**Plan de tarifa**: para este tutorial, especifique el plan de tarifa menos costoso.</span><span class="sxs-lookup"><span data-stu-id="678e9-130">**Pricing tier**: For this tutorial, specify the least-expensive pricing tier.</span></span>

   ![Creación de propiedades de la base de datos MySQL][MYSQL02]

1. <span data-ttu-id="678e9-132">Cuando haya especificado la información anterior, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="678e9-132">When you have entered all of the above information, click **Create**.</span></span>

### <a name="configure-a-firewall-rule-for-your-mysql-database-server-using-the-azure-portal"></a><span data-ttu-id="678e9-133">Configuración de una regla de firewall para el servidor de bases de datos MySQL mediante Azure Portal</span><span class="sxs-lookup"><span data-stu-id="678e9-133">Configure a firewall rule for your MySQL database server using the Azure Portal</span></span>

1. <span data-ttu-id="678e9-134">Vaya a Azure Portal en <https://portal.azure.com/> e inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="678e9-134">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="678e9-135">Haga clic en **Todos los recursos** y, a continuación, haga clic en la base de datos de MySQL que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="678e9-135">Click **All Resources**, then click the MySQL database you just created.</span></span>

   ![Selección de la base de datos MySQL][MYSQL03]

1. <span data-ttu-id="678e9-137">Haga clic en **Seguridad de la conexión** y, en las **reglas de firewall**, cree una nueva regla mediante la especificación de un nombre único para la regla, escriba el intervalo de direcciones IP que necesitará para acceder a la base de datos y, después, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="678e9-137">Click **Connection security**, and in the **Firewall rules**, create a new rule by specifying a unique name for the rule, then enter the range of IP addresses that will need access to your database, and then click **Save**.</span></span>

   ![Configuración de la seguridad de la conexión][MYSQL04]

### <a name="retrieve-the-connection-string-for-your-mysql-server-using-the-azure-portal"></a><span data-ttu-id="678e9-139">Recuperación de la cadena de conexión para el servidor de MySQL mediante Azure Portal</span><span class="sxs-lookup"><span data-stu-id="678e9-139">Retrieve the connection string for your MySQL server using the Azure Portal</span></span>

1. <span data-ttu-id="678e9-140">Vaya a Azure Portal en <https://portal.azure.com/> e inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="678e9-140">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="678e9-141">Haga clic en **Todos los recursos** y, a continuación, haga clic en la base de datos de MySQL que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="678e9-141">Click **All Resources**, then click the MySQL database you just created.</span></span>

   ![Selección de la base de datos MySQL][MYSQL03]

1. <span data-ttu-id="678e9-143">Haga clic en **Cadenas de conexión** y copie el valor en el campo de texto **JDBC**.</span><span class="sxs-lookup"><span data-stu-id="678e9-143">Click **Connection strings**, and copy the value in the **JDBC** text field.</span></span>

   ![Recuperación de la cadena de conexión JDBC][MYSQL05]

### <a name="create-mysql-database-using-the-mysql-command-line-utility"></a><span data-ttu-id="678e9-145">Creación de la base de datos MySQL mediante la utilidad de línea de comandos `mysql`</span><span class="sxs-lookup"><span data-stu-id="678e9-145">Create MySQL database using the `mysql` command-line utility</span></span>

1. <span data-ttu-id="678e9-146">Abra un shell de comandos y conéctese al servidor MySQL mediante la escritura de un `mysql` comando similar al ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="678e9-146">Open a command shell and connect to your MySQL server by entering a `mysql` command like the following example:</span></span>

   ```shell
   mysql --host wingtiptoysmysql.mysql.database.azure.com --user wingtiptoysuser@wingtiptoysmysql -p
   ```
   <span data-ttu-id="678e9-147">Donde:</span><span class="sxs-lookup"><span data-stu-id="678e9-147">Where:</span></span>

   | <span data-ttu-id="678e9-148">Parámetro</span><span class="sxs-lookup"><span data-stu-id="678e9-148">Parameter</span></span> | <span data-ttu-id="678e9-149">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="678e9-149">Description</span></span> |
   |---|---|
   | `host` | <span data-ttu-id="678e9-150">Especifica el nombre completo del servidor MySQL que se mencionó anteriormente en este artículo.</span><span class="sxs-lookup"><span data-stu-id="678e9-150">Specifies your fully qualified MySQL server name from earlier in this article.</span></span> |
   | `user` | <span data-ttu-id="678e9-151">Especifica el administrador de MySQL y el nombre de servidor abreviado que se mencionaron anteriormente en este artículo.</span><span class="sxs-lookup"><span data-stu-id="678e9-151">Specifies your MySQL administrator and shortened server name from earlier in this article.</span></span> |
   | `p` | <span data-ttu-id="678e9-152">Especifica que se debe esperar hasta que se pida una contraseña.</span><span class="sxs-lookup"><span data-stu-id="678e9-152">Specifies to wait until prompted for a password.</span></span> |

   <span data-ttu-id="678e9-153">El servidor MySQL debería responder con una pantalla similar al ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="678e9-153">Your MySQL server should respond with a display like the following example:</span></span>

   ```shell
   Welcome to the MySQL monitor.  Commands end with ; or \g.
   Your MySQL connection id is 64552
   Server version: 5.6.39.0 MySQL Community Server (GPL)
   
   Copyright (c) 2000, 2016, Oracle and/or its affiliates. All rights reserved.
   
   Oracle is a registered trademark of Oracle Corporation and/or its
   affiliates. Other names may be trademarks of their respective
   owners.
   
   Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.
   
   mysql>
   ```

1. <span data-ttu-id="678e9-154">Cree una base de datos denominada *mysqldb* mediante la escritura de un comando `mysql` similar al ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="678e9-154">Create a database named *mysqldb* by entering a `mysql` command like the following example:</span></span>

   ```SQL
   CREATE DATABASE mysqldb;
   ```

   <span data-ttu-id="678e9-155">El servidor MySQL debería responder con una pantalla similar al ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="678e9-155">Your MySQL server should respond with a display like the following example:</span></span>

   ```shell
   Query OK, 1 row affected (0.30 sec)
   ```

1. <span data-ttu-id="678e9-156">OPCIONAL: Puede comprobar que se creó la base de datos mediante la escritura de un comando `mysql` similar al ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="678e9-156">OPTIONAL: You can verify that your database was created by entering a `mysql` command like the following example:</span></span>

   ```SQL
   SHOW DATABASES;
   ```

   <span data-ttu-id="678e9-157">El servidor MySQL debería responder con una pantalla similar al ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="678e9-157">Your MySQL server should respond with a display like the following example:</span></span>

   ```shell
   +--------------------+
   | Database           |
   +--------------------+
   | information_schema |
   | mysql              |
   | mysqldb            |
   | performance_schema |
   | sys                |
   +--------------------+
   ```

1. <span data-ttu-id="678e9-158">Escriba `\q` para salir de la utilidad `mysql`.</span><span class="sxs-lookup"><span data-stu-id="678e9-158">Enter `\q` to exit the `mysql` utility.</span></span>

## <a name="configure-the-sample-application"></a><span data-ttu-id="678e9-159">Configurar la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="678e9-159">Configure the sample application</span></span>

1. <span data-ttu-id="678e9-160">Abra un shell de comandos y clone el proyecto de ejemplo con un comando git como el siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="678e9-160">Open a command shell and clone the sample project using a git command like the following example:</span></span>

   ```shell
   git clone https://github.com/Azure-Samples/spring-data-jdbc-on-azure.git
   ```

1. <span data-ttu-id="678e9-161">Busque el archivo *application.properties* en el directorio *resources* del proyecto de ejemplo, o cree el archivo si todavía no existe.</span><span class="sxs-lookup"><span data-stu-id="678e9-161">Locate the *application.properties* file in the *resources* directory of the sample project, or create the file if it does not already exist.</span></span>

1. <span data-ttu-id="678e9-162">Abra el archivo *application.properties* en un editor de texto y agréguele o configure las siguientes líneas; luego, sustituya los valores de ejemplo por los valores adecuados que se mencionaron anteriormente:</span><span class="sxs-lookup"><span data-stu-id="678e9-162">Open the *application.properties* file in a text editor, and add or configure the following lines in the file, and replace the sample values with the appropriate values from earlier:</span></span>

   ```yaml
   spring.datasource.url=jdbc:mysql://wingtiptoysmysql.mysql.database.azure.com:3306/mysqldb?useSSL=true&requireSSL=false&serverTimezone=UTC
   spring.datasource.username=wingtiptoysuser@wingtiptoysmysql
   spring.datasource.password=********
    ```
   <span data-ttu-id="678e9-163">Donde:</span><span class="sxs-lookup"><span data-stu-id="678e9-163">Where:</span></span>

   | <span data-ttu-id="678e9-164">Parámetro</span><span class="sxs-lookup"><span data-stu-id="678e9-164">Parameter</span></span> | <span data-ttu-id="678e9-165">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="678e9-165">Description</span></span> |
   |---|---|
   | `spring.datasource.url` | <span data-ttu-id="678e9-166">Especifica la cadena de JDBC de MySQL que se mencionó anteriormente en este artículo, con la zona horaria agregada.</span><span class="sxs-lookup"><span data-stu-id="678e9-166">Specifies your MySQL JDBC string from earlier in this article, with the time zone added.</span></span> |
   | `spring.datasource.username` | <span data-ttu-id="678e9-167">Especifica el nombre del administrador de MySQL que se mencionó anteriormente en este artículo, con el nombre abreviado del servidor anexado.</span><span class="sxs-lookup"><span data-stu-id="678e9-167">Specifies your MySQL administrator name from earlier in this article, with the shortened server name appended to it.</span></span> |
   | `spring.datasource.password` | <span data-ttu-id="678e9-168">Especifica la contraseña de administrador de MySQL que se mencionó anteriormente en este artículo.</span><span class="sxs-lookup"><span data-stu-id="678e9-168">Specifies your MySQL administrator password from earlier in this article.</span></span> |

1. <span data-ttu-id="678e9-169">Guarde y cierre el archivo *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="678e9-169">Save and close the *application.properties* file.</span></span>

## <a name="package-and-test-the-sample-application"></a><span data-ttu-id="678e9-170">Empaquetado y prueba de la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="678e9-170">Package and test the sample application</span></span> 

1. <span data-ttu-id="678e9-171">Compile la aplicación de ejemplo con Maven; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="678e9-171">Build the sample application with Maven; for example:</span></span>

   ```shell
   mvn clean package -P mysql
   ```

1. <span data-ttu-id="678e9-172">Inicie la aplicación de ejemplo; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="678e9-172">Start the sample application; for example:</span></span>

   ```shell
   java -jar target/spring-data-jdbc-on-azure-0.1.0-SNAPSHOT.jar
   ```

1. <span data-ttu-id="678e9-173">Cree nuevos registros con `curl` desde un símbolo del sistema como en los ejemplos siguientes:</span><span class="sxs-lookup"><span data-stu-id="678e9-173">Create new records using `curl` from a command prompt like the following examples:</span></span>

   ```shell
   curl -s -d '{"name":"dog","species":"canine"}' -H "Content-Type: application/json" -X POST http://localhost:8080/pets

   curl -s -d '{"name":"cat","species":"feline"}' -H "Content-Type: application/json" -X POST http://localhost:8080/pets
   ```

   <span data-ttu-id="678e9-174">La aplicación debe devolver valores similares a los siguientes:</span><span class="sxs-lookup"><span data-stu-id="678e9-174">Your application should return values like the following:</span></span>

   ```shell
   Added Pet(id=1, name=dog, species=canine).

   Added Pet(id=2, name=cat, species=feline).
   ```

1. <span data-ttu-id="678e9-175">Recupere todos los registros existentes con `curl` desde un símbolo del sistema como los siguientes ejemplos:</span><span class="sxs-lookup"><span data-stu-id="678e9-175">Retrieve all of the existing records using `curl` from a command prompt like the following examples:</span></span>

   ```shell
   curl -s http://localhost:8080/pets
   ```
    
   <span data-ttu-id="678e9-176">La aplicación debe devolver valores similares a los siguientes:</span><span class="sxs-lookup"><span data-stu-id="678e9-176">Your application should return values like the following:</span></span>

   ```json
   [{"id":1,"name":"dog","species":"canine"},{"id":2,"name":"cat","species":"feline"}]
   ```

## <a name="summary"></a><span data-ttu-id="678e9-177">Resumen</span><span class="sxs-lookup"><span data-stu-id="678e9-177">Summary</span></span>

<span data-ttu-id="678e9-178">En este tutorial ha creado una aplicación Java de ejemplo que Spring Data para almacenar y recuperar información de una base de datos MySQL de Azure mediante JDBC.</span><span class="sxs-lookup"><span data-stu-id="678e9-178">In this tutorial, you created a sample Java application that uses Spring Data to store and retrieve information in an Azure MySQL database using JDBC.</span></span>

## <a name="next-steps"></a><span data-ttu-id="678e9-179">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="678e9-179">Next steps</span></span>

<span data-ttu-id="678e9-180">Para más información acerca de Spring y Azure, vaya al centro de documentación de Azure.</span><span class="sxs-lookup"><span data-stu-id="678e9-180">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="678e9-181">Spring en Azure</span><span class="sxs-lookup"><span data-stu-id="678e9-181">Spring on Azure</span></span>](/java/azure/spring-framework)

### <a name="additional-resources"></a><span data-ttu-id="678e9-182">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="678e9-182">Additional Resources</span></span>

<span data-ttu-id="678e9-183">Para más información sobre el uso de Azure con Java, consulte [Azure para desarrolladores de Java] y [Working with Azure DevOps and Java] (Trabajo con Azure DevOps y Java).</span><span class="sxs-lookup"><span data-stu-id="678e9-183">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Working with Azure DevOps and Java].</span></span>

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

[MYSQL01]: media/configure-spring-data-jdbc-with-azure-mysql/create-mysql-01.png
[MYSQL02]: media/configure-spring-data-jdbc-with-azure-mysql/create-mysql-02.png
[MYSQL03]: media/configure-spring-data-jdbc-with-azure-mysql/create-mysql-03.png
[MYSQL04]: media/configure-spring-data-jdbc-with-azure-mysql/create-mysql-04.png
[MYSQL05]: media/configure-spring-data-jdbc-with-azure-mysql/create-mysql-05.png
