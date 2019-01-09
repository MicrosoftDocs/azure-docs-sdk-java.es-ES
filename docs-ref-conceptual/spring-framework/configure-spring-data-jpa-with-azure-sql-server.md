---
title: Uso de Spring Data JPA con Azure SQL Database
description: Aprenda a usar Spring Data JPA con una instancia de Azure SQL Database.
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
ms.openlocfilehash: 7119283bec250a4ab0854ba2c29b0906624448e9
ms.sourcegitcommit: f0f140b0862ca5338b1b7e5c33cec3e58a70b8fd
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/03/2019
ms.locfileid: "53992510"
---
# <a name="how-to-use-spring-data-jpa-with-azure-sql-database"></a><span data-ttu-id="1da65-103">Uso de Spring Data JPA con Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="1da65-103">How to use Spring Data JPA with Azure SQL Database</span></span>

## <a name="overview"></a><span data-ttu-id="1da65-104">Información general</span><span class="sxs-lookup"><span data-stu-id="1da65-104">Overview</span></span>

<span data-ttu-id="1da65-105">En este artículo se explica cómo crear una aplicación de ejemplo que utiliza [Spring Data] para almacenar y recuperar información en una instancia de [Azure SQL Database](https://azure.microsoft.com/services/sql-database/) mediante [Java Persistence API (JPA)](https://docs.oracle.com/javaee/7/tutorial/persistence-intro.htm).</span><span class="sxs-lookup"><span data-stu-id="1da65-105">This article demonstrates creating a sample application that uses [Spring Data] to store and retrieve information in an [Azure SQL Database](https://azure.microsoft.com/services/sql-database/) using [Java Persistence API (JPA)](https://docs.oracle.com/javaee/7/tutorial/persistence-intro.htm).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1da65-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="1da65-106">Prerequisites</span></span>

<span data-ttu-id="1da65-107">Los siguientes requisitos previos son necesarios para seguir los pasos descritos en este artículo:</span><span class="sxs-lookup"><span data-stu-id="1da65-107">The following prerequisites are required in order to complete the steps in this article:</span></span>

* <span data-ttu-id="1da65-108">Una suscripción de Azure. Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN] o registrarse para obtener una [cuenta de Azure gratuita].</span><span class="sxs-lookup"><span data-stu-id="1da65-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="1da65-109">Un kit de desarrollo de Java (JDK) admitido</span><span class="sxs-lookup"><span data-stu-id="1da65-109">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="1da65-110">Para más información sobre los JDK disponibles para desarrollar en Azure, consulte <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="1da65-110">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="1da65-111">[Apache Maven](http://maven.apache.org/), versión 3.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="1da65-111">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>
* <span data-ttu-id="1da65-112">[Curl ](https://curl.haxx.se/) o una utilidad HTTP similar para probar la funcionalidad.</span><span class="sxs-lookup"><span data-stu-id="1da65-112">[Curl](https://curl.haxx.se/) or similar HTTP utility to test functionality.</span></span>
* <span data-ttu-id="1da65-113">Un cliente [Git](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="1da65-113">A [Git](https://git-scm.com/downloads) client.</span></span>

## <a name="create-an-azure-sql-satabase"></a><span data-ttu-id="1da65-114">Creación de una instancia de Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="1da65-114">Create an Azure SQL Satabase</span></span>

### <a name="create-a-sql-database-server-using-the-azure-portal"></a><span data-ttu-id="1da65-115">Creación de un servidor de SQL Database mediante Azure Portal</span><span class="sxs-lookup"><span data-stu-id="1da65-115">Create a SQL database server using the Azure Portal</span></span>

> [!NOTE]
> 
> <span data-ttu-id="1da65-116">Puede leer información más detallada sobre la creación de bases de datos SQL de Azure en [Creación de una instancia de Azure SQL Database en Azure Portal](/azure/sql-database/sql-database-get-started-portal).</span><span class="sxs-lookup"><span data-stu-id="1da65-116">You can read more detailed information about creating Azure SQL databases in [Create an Azure SQL database in the Azure portal](/azure/sql-database/sql-database-get-started-portal).</span></span>

1. <span data-ttu-id="1da65-117">Vaya a Azure Portal en <https://portal.azure.com/> e inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="1da65-117">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="1da65-118">Haga clic en **+Crear un recurso**, después en **Bases de datos** y, finalmente, en **SQL Database**.</span><span class="sxs-lookup"><span data-stu-id="1da65-118">Click **+Create a resource**, then **Databases**, and then click **SQL Database**.</span></span>

   ![Creación de una base de datos SQL][SQL01]

1. <span data-ttu-id="1da65-120">Especifique la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="1da65-120">Specify the following information:</span></span>

   - <span data-ttu-id="1da65-121">**Nombre de la base de datos**: elija un nombre único para la base de datos SQL; este se creará en el servidor SQL que va a especificar posteriormente.</span><span class="sxs-lookup"><span data-stu-id="1da65-121">**Database name**: Choose a unique name for your SQL database; this will be created in the SQL server that you will specify later.</span></span>
   - <span data-ttu-id="1da65-122">**Suscripción**: especifique la suscripción de Azure que se va a usar.</span><span class="sxs-lookup"><span data-stu-id="1da65-122">**Subscription**: Specify your Azure subscription to use.</span></span>
   - <span data-ttu-id="1da65-123">**Grupo de recursos**: especifique si desea crear un nuevo grupo de recursos o elija uno existente.</span><span class="sxs-lookup"><span data-stu-id="1da65-123">**Resource group**: Specify whether to create a new resource group, or choose an existing resource group.</span></span>
   - <span data-ttu-id="1da65-124">**Seleccionar origen**: para este tutorial, seleccione `Blank database` para crear una nueva base de datos.</span><span class="sxs-lookup"><span data-stu-id="1da65-124">**Select source**: For this tutorial, select `Blank database` to create a new database.</span></span>

   ![Especificación de las propiedades de la base de datos SQL][SQL02]
   
1. <span data-ttu-id="1da65-126">Haga clic en **Servidor**, después en **Crear un servidor nuevo** y, después, especifique la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="1da65-126">Click **Server**, then **Create a new server**, and then specify the following information:</span></span>

   - <span data-ttu-id="1da65-127">**Nombre del servidor**: elija un nombre único para el servidor SQL; se utilizará para crear un nombre de dominio completo como *wingtiptoyssql.database.windows.net*.</span><span class="sxs-lookup"><span data-stu-id="1da65-127">**Server name**: Choose a unique name for your SQL server; this will be used to create a fully-qualified domain name like *wingtiptoyssql.database.windows.net*.</span></span>
   - <span data-ttu-id="1da65-128">**Inicio de sesión del administrador del servidor**: especifique el nombre del administrador de base de datos.</span><span class="sxs-lookup"><span data-stu-id="1da65-128">**Server admin login**: Specify the database administrator name.</span></span>
   - <span data-ttu-id="1da65-129">**Contraseña** y **Confirmar contraseña**: especifique la contraseña para el administrador de base de datos.</span><span class="sxs-lookup"><span data-stu-id="1da65-129">**Password** and **Confirm password**: Specify the password for your database administrator.</span></span>
   - <span data-ttu-id="1da65-130">**Ubicación**: especifique la región geográfica más cercana a la base de datos.</span><span class="sxs-lookup"><span data-stu-id="1da65-130">**Location**: Specify the closest geographic region for your database.</span></span>

   ![Especificación del servidor SQL Server][SQL03]

1. <span data-ttu-id="1da65-132">Cuando haya especificado la información anterior, haga clic en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="1da65-132">When you have entered all of the above information, click **Select**.</span></span>

1. <span data-ttu-id="1da65-133">Para este tutorial, especifique el **plan de tarifa** menos costoso y, después, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="1da65-133">For this tutorial, specify the least-expensive **Pricing tier**, and then click **Create**.</span></span>

   ![Creación de la base de datos SQL][SQL04]

### <a name="configure-a-firewall-rule-for-your-sql-server-using-the-azure-portal"></a><span data-ttu-id="1da65-135">Configuración de una regla de firewall para el servidor SQL Server mediante Azure Portal</span><span class="sxs-lookup"><span data-stu-id="1da65-135">Configure a firewall rule for your SQL server using the Azure Portal</span></span>

1. <span data-ttu-id="1da65-136">Vaya a Azure Portal en <https://portal.azure.com/> e inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="1da65-136">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="1da65-137">Haga clic en **Todos los recursos**; después, haga clic en el servidor SQL Server que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="1da65-137">Click **All Resources**, then click the SQL server you just created.</span></span>

   ![Selección del servidor SQL Server][SQL05]

1. <span data-ttu-id="1da65-139">En la sección **Introducción**, haga clic en **Mostrar configuración del firewall**.</span><span class="sxs-lookup"><span data-stu-id="1da65-139">In the **Overview** section, click **Show firewall settings**</span></span>

   ![Visualización de la configuración del firewall][SQL06]

1. <span data-ttu-id="1da65-141">En la sección **Firewalls y redes virtuales**, cree una nueva regla mediante la especificación de un nombre único para la regla, escriba el intervalo de direcciones IP que necesitará para acceder a la base de datos y, después, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="1da65-141">In the **Firewalls and virtual networks** section, create a new rule by specifying a unique name for the rule, then enter the range of IP addresses that will need access to your database, and then click **Save**.</span></span>

   ![Configuración del firewall][SQL07]

### <a name="retrieve-the-connection-string-for-your-sql-server-using-the-azure-portal"></a><span data-ttu-id="1da65-143">Recuperación de la cadena de conexión para el servidor SQL Server con Azure Portal</span><span class="sxs-lookup"><span data-stu-id="1da65-143">Retrieve the connection string for your SQL server using the Azure Portal</span></span>

1. <span data-ttu-id="1da65-144">Vaya a Azure Portal en <https://portal.azure.com/> e inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="1da65-144">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="1da65-145">Haga clic en **Todos los recursos** y, a continuación, haga clic en la base de datos SQL que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="1da65-145">Click **All Resources**, then click the SQL database you just created.</span></span>

   ![Selección de la base de datos SQL][SQL08]

1. <span data-ttu-id="1da65-147">Haga clic en **Cadenas de conexión**, después haga clic en **JDBC** y copie el valor en el campo de texto JDBC.</span><span class="sxs-lookup"><span data-stu-id="1da65-147">Click **Connection strings**, then click **JDBC**, and copy the value in the JDBC text field.</span></span>

   ![Recuperación de la cadena de conexión JDBC][SQL09]

## <a name="configure-the-sample-application"></a><span data-ttu-id="1da65-149">Configurar la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="1da65-149">Configure the sample application</span></span>

1. <span data-ttu-id="1da65-150">Abra un shell de comandos y clone el proyecto de ejemplo con un comando git como el siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="1da65-150">Open a command shell and clone the sample project using a git command like the following example:</span></span>

   ```shell
   git clone https://github.com/Azure-Samples/spring-data-jdbc-on-azure.git
   ```

1. <span data-ttu-id="1da65-151">Busque el archivo *application.properties* en el directorio *resources* del proyecto de ejemplo, o cree el archivo si todavía no existe.</span><span class="sxs-lookup"><span data-stu-id="1da65-151">Locate the *application.properties* file in the *resources* directory of the sample project, or create the file if it does not already exist.</span></span>

1. <span data-ttu-id="1da65-152">Abra el archivo *application.properties* en un editor de texto y agréguele o configure las siguientes líneas; luego, sustituya los valores de ejemplo por los valores adecuados que se mencionaron anteriormente:</span><span class="sxs-lookup"><span data-stu-id="1da65-152">Open the *application.properties* file in a text editor, and add or configure the following lines in the file, and replace the sample values with the appropriate values from earlier:</span></span>

   ```yaml
   spring.datasource.url=jdbc:sqlserver://wingtiptoyssql.database.windows.net:1433;database=wingtiptoys;encrypt=true;trustServerCertificate=false;hostNameInCertificate=*.database.windows.net;loginTimeout=30;
   spring.datasource.username=wingtiptoysuser@wingtiptoyssql
   spring.datasource.password=********
    ```
   <span data-ttu-id="1da65-153">Donde:</span><span class="sxs-lookup"><span data-stu-id="1da65-153">Where:</span></span>

   | <span data-ttu-id="1da65-154">Parámetro</span><span class="sxs-lookup"><span data-stu-id="1da65-154">Parameter</span></span> | <span data-ttu-id="1da65-155">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="1da65-155">Description</span></span> |
   |---|---|
   | `spring.datasource.url` | <span data-ttu-id="1da65-156">Especifica una versión modificada de la cadena JDBC de SQL que se mencionó anteriormente en este artículo.</span><span class="sxs-lookup"><span data-stu-id="1da65-156">Specifies an edited version of your SQL JDBC string from earlier in this article.</span></span> |
   | `spring.datasource.username` | <span data-ttu-id="1da65-157">Especifica el nombre del administrador de SQL que se mencionó anteriormente en este artículo, con el nombre abreviado del servidor anexado.</span><span class="sxs-lookup"><span data-stu-id="1da65-157">Specifies your SQL administrator name from earlier in this article, with the shortened server name appended to it.</span></span> |
   | `spring.datasource.password` | <span data-ttu-id="1da65-158">Especifica la contraseña de administrador de SQL que se mencionó anteriormente en este artículo.</span><span class="sxs-lookup"><span data-stu-id="1da65-158">Specifies your SQL administrator password from earlier in this article.</span></span> |

1. <span data-ttu-id="1da65-159">Guarde y cierre el archivo *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="1da65-159">Save and close the *application.properties* file.</span></span>

## <a name="package-and-test-the-sample-application"></a><span data-ttu-id="1da65-160">Empaquetado y prueba de la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="1da65-160">Package and test the sample application</span></span> 

1. <span data-ttu-id="1da65-161">Compile la aplicación de ejemplo con Maven; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="1da65-161">Build the sample application with Maven; for example:</span></span>

   ```shell
   mvn clean package -P sql
   ```

1. <span data-ttu-id="1da65-162">Inicie la aplicación de ejemplo; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="1da65-162">Start the sample application; for example:</span></span>

   ```shell
   java -jar target/spring-data-jpa-on-azure-0.1.0-SNAPSHOT.jar
   ```

1. <span data-ttu-id="1da65-163">Cree nuevos registros con `curl` desde un símbolo del sistema como en los ejemplos siguientes:</span><span class="sxs-lookup"><span data-stu-id="1da65-163">Create new records using `curl` from a command prompt like the following examples:</span></span>

   ```shell
   curl -s -d '{"name":"dog","species":"canine"}' -H "Content-Type: application/json" -X POST http://localhost:8080/pets

   curl -s -d '{"name":"cat","species":"feline"}' -H "Content-Type: application/json" -X POST http://localhost:8080/pets
   ```

   <span data-ttu-id="1da65-164">La aplicación debe devolver valores similares a los siguientes:</span><span class="sxs-lookup"><span data-stu-id="1da65-164">Your application should return values like the following:</span></span>

   ```shell
   Added Pet(id=1, name=dog, species=canine).

   Added Pet(id=2, name=cat, species=feline).
   ```

1. <span data-ttu-id="1da65-165">Recupere todos los registros existentes con `curl` desde un símbolo del sistema como los siguientes ejemplos:</span><span class="sxs-lookup"><span data-stu-id="1da65-165">Retrieve all of the existing records using `curl` from a command prompt like the following examples:</span></span>

   ```shell
   curl -s http://localhost:8080/pets
   ```
    
   <span data-ttu-id="1da65-166">La aplicación debe devolver valores similares a los siguientes:</span><span class="sxs-lookup"><span data-stu-id="1da65-166">Your application should return values like the following:</span></span>

   ```json
   [{"id":1,"name":"dog","species":"canine"},{"id":2,"name":"cat","species":"feline"}]
   ```

## <a name="summary"></a><span data-ttu-id="1da65-167">Resumen</span><span class="sxs-lookup"><span data-stu-id="1da65-167">Summary</span></span>

<span data-ttu-id="1da65-168">En este tutorial ha creado una aplicación Java de ejemplo que Spring Data para almacenar y recuperar información de una instancia de Azure SQL Database mediante JPA.</span><span class="sxs-lookup"><span data-stu-id="1da65-168">In this tutorial, you created a sample Java application that uses Spring Data to store and retrieve information in an Azure SQL database using JPA.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1da65-169">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1da65-169">Next steps</span></span>

<span data-ttu-id="1da65-170">Para más información acerca de Spring y Azure, vaya al centro de documentación de Azure.</span><span class="sxs-lookup"><span data-stu-id="1da65-170">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1da65-171">Spring en Azure</span><span class="sxs-lookup"><span data-stu-id="1da65-171">Spring on Azure</span></span>](/java/azure/spring-framework)

### <a name="additional-resources"></a><span data-ttu-id="1da65-172">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="1da65-172">Additional Resources</span></span>

<span data-ttu-id="1da65-173">Para más información sobre el uso de Azure con Java, consulte [Azure para desarrolladores de Java] y [Working with Azure DevOps and Java] (Trabajo con Azure DevOps y Java).</span><span class="sxs-lookup"><span data-stu-id="1da65-173">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Working with Azure DevOps and Java].</span></span>

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

[SQL01]: media/configure-spring-data-jpa-with-azure-sql-server/create-azure-sql-01.png
[SQL02]: media/configure-spring-data-jpa-with-azure-sql-server/create-azure-sql-02.png
[SQL03]: media/configure-spring-data-jpa-with-azure-sql-server/create-azure-sql-03.png
[SQL04]: media/configure-spring-data-jpa-with-azure-sql-server/create-azure-sql-04.png
[SQL05]: media/configure-spring-data-jpa-with-azure-sql-server/create-azure-sql-05.png
[SQL06]: media/configure-spring-data-jpa-with-azure-sql-server/create-azure-sql-06.png
[SQL07]: media/configure-spring-data-jpa-with-azure-sql-server/create-azure-sql-07.png
[SQL08]: media/configure-spring-data-jpa-with-azure-sql-server/create-azure-sql-08.png
[SQL09]: media/configure-spring-data-jpa-with-azure-sql-server/create-azure-sql-09.png
