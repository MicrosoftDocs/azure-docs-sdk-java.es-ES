---
title: Uso de Spring Data Apache Cassandra API con Azure Cosmos DB
description: Aprenda a usar Spring Data Apache Cassandra API con Azure Cosmos DB.
services: cosmos-db
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 12/19/2018
ms.devlang: java
ms.service: cosmos-db
ms.tgt_pltfrm: multiple
ms.topic: article
ms.openlocfilehash: 1f3f7a55b49d64077df9e7d4d6acc3af4495b424
ms.sourcegitcommit: f0f140b0862ca5338b1b7e5c33cec3e58a70b8fd
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/03/2019
ms.locfileid: "53992506"
---
# <a name="how-to-use-spring-data-apache-cassandra-api-with-azure-cosmos-db"></a><span data-ttu-id="12a83-103">Uso de Spring Data Apache Cassandra API con Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="12a83-103">How to use Spring Data Apache Cassandra API with Azure Cosmos DB</span></span>

## <a name="overview"></a><span data-ttu-id="12a83-104">Información general</span><span class="sxs-lookup"><span data-stu-id="12a83-104">Overview</span></span>

<span data-ttu-id="12a83-105">En este artículo se explica cómo crear una aplicación de ejemplo que utiliza [Spring Data] para almacenar y recuperar información mediante [Cassandra API de Azure Cosmos DB](/azure/cosmos-db/cassandra-introduction).</span><span class="sxs-lookup"><span data-stu-id="12a83-105">This article demonstrates creating a sample application that uses [Spring Data] to store and retrieve information using the [Azure Cosmos DB Cassandra API](/azure/cosmos-db/cassandra-introduction).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="12a83-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="12a83-106">Prerequisites</span></span>

<span data-ttu-id="12a83-107">Los siguientes requisitos previos son necesarios para seguir los pasos descritos en este artículo:</span><span class="sxs-lookup"><span data-stu-id="12a83-107">The following prerequisites are required in order to complete the steps in this article:</span></span>

* <span data-ttu-id="12a83-108">Una suscripción de Azure. Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN] o registrarse para obtener una [cuenta de Azure gratuita].</span><span class="sxs-lookup"><span data-stu-id="12a83-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="12a83-109">Un kit de desarrollo de Java (JDK) admitido</span><span class="sxs-lookup"><span data-stu-id="12a83-109">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="12a83-110">Para más información sobre los JDK disponibles para desarrollar en Azure, consulte <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="12a83-110">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="12a83-111">[Apache Maven](http://maven.apache.org/), versión 3.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="12a83-111">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>
* <span data-ttu-id="12a83-112">[Curl ](https://curl.haxx.se/) o una utilidad HTTP similar para probar la funcionalidad.</span><span class="sxs-lookup"><span data-stu-id="12a83-112">[Curl](https://curl.haxx.se/) or similar HTTP utility to test functionality.</span></span>
* <span data-ttu-id="12a83-113">Un cliente [Git](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="12a83-113">A [Git](https://git-scm.com/downloads) client.</span></span>

## <a name="create-an-azure-cosmos-db-account"></a><span data-ttu-id="12a83-114">Creación de una cuenta de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="12a83-114">Create an Azure Cosmos DB account</span></span>

### <a name="create-a-cosmos-db-account-using-the-azure-portal"></a><span data-ttu-id="12a83-115">Creación de una cuenta de Cosmos DB mediante Azure Portal</span><span class="sxs-lookup"><span data-stu-id="12a83-115">Create a Cosmos DB account using the Azure Portal</span></span>

> [!NOTE]
> 
> <span data-ttu-id="12a83-116">Puede leer información más detallada sobre cómo crear cuentas de Azure Cosmos DB en la [documentación de Azure Cosmos DB](/azure/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="12a83-116">You can read more detailed information about creating Azure Cosmos DB accounts in [Azure Cosmos DB Documentation](/azure/cosmos-db/).</span></span>

1. <span data-ttu-id="12a83-117">Vaya a Azure Portal en <https://portal.azure.com/> e inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="12a83-117">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="12a83-118">Haga clic sucesivamente en **+ Crear un recurso**, en **Bases de datos** y, finalmente, en **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="12a83-118">Click **+Create a resource**, then **Databases**, and then click **Azure Cosmos DB**.</span></span>

   ![Creación de una cuenta de Azure Cosmos DB][COSMOSDB01]

1. <span data-ttu-id="12a83-120">Especifique la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="12a83-120">Specify the following information:</span></span>

   - <span data-ttu-id="12a83-121">**Suscripción**: especifique la suscripción de Azure que se va a usar.</span><span class="sxs-lookup"><span data-stu-id="12a83-121">**Subscription**: Specify your Azure subscription to use.</span></span>
   - <span data-ttu-id="12a83-122">**Grupo de recursos**: especifique si desea crear un nuevo grupo de recursos o elija uno existente.</span><span class="sxs-lookup"><span data-stu-id="12a83-122">**Resource group**: Specify whether to create a new resource group, or choose an existing resource group.</span></span>
   - <span data-ttu-id="12a83-123">**Nombre de cuenta**: Elija un nombre único para la cuenta de Cosmos DB; se utilizará para crear un nombre de dominio completo como *wingtiptoyscassandra.documents.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="12a83-123">**Account name**: Choose a unique name for your Cosmos DB account; this will be used to create a fully-qualified domain name like *wingtiptoyscassandra.documents.azure.com*.</span></span>
   - <span data-ttu-id="12a83-124">**API**: Especifique `Cassandra` para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="12a83-124">**API**: Specify `Cassandra` for this tutorial.</span></span>
   - <span data-ttu-id="12a83-125">**Ubicación**: especifique la región geográfica más cercana a la base de datos.</span><span class="sxs-lookup"><span data-stu-id="12a83-125">**Location**: Specify the closest geographic region for your database.</span></span>

   ![Especificación de la configuración de la cuenta de Cosmos DB][COSMOSDB02]
   
1. <span data-ttu-id="12a83-127">Cuando haya especificado toda la información anterior, haga clic en **Revisar + crear**.</span><span class="sxs-lookup"><span data-stu-id="12a83-127">When you have entered all of the above information, click **Review + create**.</span></span>

1. <span data-ttu-id="12a83-128">Si todo parece correcto en la página de revisión, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="12a83-128">If everything looks correct on the review page, click **Create**.</span></span>

   ![Revisión de la configuración de la cuenta de Cosmos DB][COSMOSDB03]

### <a name="add-a-keyspace-to-your-azure-cosmos-db-account"></a><span data-ttu-id="12a83-130">Adición de un espacio de claves a la cuenta de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="12a83-130">Add a keyspace to your Azure Cosmos DB account</span></span>

1. <span data-ttu-id="12a83-131">Vaya a Azure Portal en <https://portal.azure.com/> e inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="12a83-131">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="12a83-132">Haga clic en **Todos los recursos** y, después, haga clic en la cuenta de Azure Cosmos DB que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="12a83-132">Click **All Resources**, then click the Azure Cosmos DB account you just created.</span></span>

   ![Selección de la cuenta de Azure Cosmos DB][COSMOSDB04]

1. <span data-ttu-id="12a83-134">Haga clic en **Explorador de datos** y después en **New Keyspace** (Nuevo espacio de claves).</span><span class="sxs-lookup"><span data-stu-id="12a83-134">Click **Data Explorer**, then click **New Keyspace**.</span></span> <span data-ttu-id="12a83-135">Especifique un identificador único en **Id. de espacio de claves**, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="12a83-135">Enter a unique identifier for your **Keyspace id**, then click **OK**.</span></span>

   ![Creación de un espacio de claves de Cosmos DB][COSMOSDB05]

### <a name="retrieve-the-connection-settings-for-your-azure-cosmos-db-account"></a><span data-ttu-id="12a83-137">Recuperación de la configuración de conexión para la cuenta de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="12a83-137">Retrieve the connection settings for your Azure Cosmos DB account</span></span>

1. <span data-ttu-id="12a83-138">Vaya a Azure Portal en <https://portal.azure.com/> e inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="12a83-138">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="12a83-139">Haga clic en **Todos los recursos** y, después, haga clic en la cuenta de Azure Cosmos DB que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="12a83-139">Click **All Resources**, then click the Azure Cosmos DB account you just created.</span></span>

   ![Selección de la cuenta de Azure Cosmos DB][COSMOSDB04]

1. <span data-ttu-id="12a83-141">Haga clic en **Cadenas de conexión** y copie los valores de los campos **Punto de contacto**, **Puerto**, **Nombre de usuario** y **Contraseña principal**; estos valores se utilizarán para configurar la aplicación posteriormente.</span><span class="sxs-lookup"><span data-stu-id="12a83-141">Click **Connection strings**, and copy the values for the **Contact Point**, **Port**, **Username**, and **Primary Password** fields; you will use those values to configure your application later.</span></span>

   ![Recuperación de la configuración de conexión de Cosmos DB][COSMOSDB05]

## <a name="configure-the-sample-application"></a><span data-ttu-id="12a83-143">Configurar la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="12a83-143">Configure the sample application</span></span>

1. <span data-ttu-id="12a83-144">Abra un shell de comandos y clone el proyecto de ejemplo con un comando git como el siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="12a83-144">Open a command shell and clone the sample project using a git command like the following example:</span></span>

   ```shell
   git clone https://github.com/Azure-Samples/spring-data-cassandra-on-azure.git
   ```

1. <span data-ttu-id="12a83-145">Busque el archivo *application.properties* en el directorio *resources* del proyecto de ejemplo, o cree el archivo si todavía no existe.</span><span class="sxs-lookup"><span data-stu-id="12a83-145">Locate the *application.properties* file in the *resources* directory of the sample project, or create the file if it does not already exist.</span></span>

1. <span data-ttu-id="12a83-146">Abra el archivo *application.properties* en un editor de texto y agréguele o configure las siguientes líneas; luego, sustituya los valores de ejemplo por los valores adecuados que se mencionaron anteriormente:</span><span class="sxs-lookup"><span data-stu-id="12a83-146">Open the *application.properties* file in a text editor, and add or configure the following lines in the file, and replace the sample values with the appropriate values from earlier:</span></span>

   ```yaml
   spring.data.cassandra.contact-points=wingtiptoyscassandra.cassandra.cosmosdb.azure.com
   spring.data.cassandra.port=10350
   spring.data.cassandra.username=wingtiptoyscassandra
   spring.data.cassandra.password=********
   ```
   <span data-ttu-id="12a83-147">Donde:</span><span class="sxs-lookup"><span data-stu-id="12a83-147">Where:</span></span>

   | <span data-ttu-id="12a83-148">Parámetro</span><span class="sxs-lookup"><span data-stu-id="12a83-148">Parameter</span></span> | <span data-ttu-id="12a83-149">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="12a83-149">Description</span></span> |
   |---|---|
   | `spring.data.cassandra.contact-points` | <span data-ttu-id="12a83-150">Especifica el **punto de contacto** que se mencionó anteriormente en este artículo.</span><span class="sxs-lookup"><span data-stu-id="12a83-150">Specifies the **Contact Point** from earlier in this article.</span></span> |
   | `spring.data.cassandra.port` | <span data-ttu-id="12a83-151">Especifica el **puerto** que se mencionó anteriormente en este artículo.</span><span class="sxs-lookup"><span data-stu-id="12a83-151">Specifies the **Port** from earlier in this article.</span></span> |
   | `spring.data.cassandra.username` | <span data-ttu-id="12a83-152">Especifica el **nombre de usuario** que se mencionó anteriormente en este artículo.</span><span class="sxs-lookup"><span data-stu-id="12a83-152">Specifies your **Username** from earlier in this article.</span></span> |
   | `spring.data.cassandra.password` | <span data-ttu-id="12a83-153">Especifica la **contraseña principal** que se mencionó anteriormente en este artículo.</span><span class="sxs-lookup"><span data-stu-id="12a83-153">Specifies your **Primary Password** from earlier in this article.</span></span> |

1. <span data-ttu-id="12a83-154">Guarde y cierre el archivo *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="12a83-154">Save and close the *application.properties* file.</span></span>

## <a name="package-and-test-the-sample-application"></a><span data-ttu-id="12a83-155">Empaquetado y prueba de la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="12a83-155">Package and test the sample application</span></span> 

1. <span data-ttu-id="12a83-156">Compile la aplicación de ejemplo con Maven; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="12a83-156">Build the sample application with Maven; for example:</span></span>

   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="12a83-157">Inicie la aplicación de ejemplo; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="12a83-157">Start the sample application; for example:</span></span>

   ```shell
   java -jar target/spring-data-cassandra-on-azure-0.1.0-SNAPSHOT.jar
   ```

1. <span data-ttu-id="12a83-158">Cree nuevos registros con `curl` desde un símbolo del sistema como en los ejemplos siguientes:</span><span class="sxs-lookup"><span data-stu-id="12a83-158">Create new records using `curl` from a command prompt like the following examples:</span></span>

   ```shell
   curl -s -d '{"name":"dog","species":"canine"}' -H "Content-Type: application/json" -X POST http://localhost:8080/pets

   curl -s -d '{"name":"cat","species":"feline"}' -H "Content-Type: application/json" -X POST http://localhost:8080/pets
   ```

   <span data-ttu-id="12a83-159">La aplicación debe devolver valores similares a los siguientes:</span><span class="sxs-lookup"><span data-stu-id="12a83-159">Your application should return values like the following:</span></span>

   ```shell
   Added Pet{id=60fa8cb0-0423-11e9-9a70-39311962166b, name='dog', species='canine'}.

   Added Pet{id=72c1c9e0-0423-11e9-9a70-39311962166b, name='cat', species='feline'}.
   ```

1. <span data-ttu-id="12a83-160">Recupere todos los registros existentes con `curl` desde un símbolo del sistema como los siguientes ejemplos:</span><span class="sxs-lookup"><span data-stu-id="12a83-160">Retrieve all of the existing records using `curl` from a command prompt like the following examples:</span></span>

   ```shell
   curl -s http://localhost:8080/pets
   ```
    
   <span data-ttu-id="12a83-161">La aplicación debe devolver valores similares a los siguientes:</span><span class="sxs-lookup"><span data-stu-id="12a83-161">Your application should return values like the following:</span></span>

   ```json
   [{"id":"60fa8cb0-0423-11e9-9a70-39311962166b","name":"dog","species":"canine"},{"id":"72c1c9e0-0423-11e9-9a70-39311962166b","name":"cat","species":"feline"}]
   ```

## <a name="summary"></a><span data-ttu-id="12a83-162">Resumen</span><span class="sxs-lookup"><span data-stu-id="12a83-162">Summary</span></span>

<span data-ttu-id="12a83-163">En este tutorial ha creado una aplicación Java de ejemplo que utiliza Spring Data para almacenar y recuperar información mediante Cassandra API de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="12a83-163">In this tutorial, you created a sample Java application that uses Spring Data to store and retrieve information using the Azure Cosmos DB Cassandra API.</span></span>

## <a name="next-steps"></a><span data-ttu-id="12a83-164">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="12a83-164">Next steps</span></span>

<span data-ttu-id="12a83-165">Para más información acerca de Spring y Azure, vaya al centro de documentación de Azure.</span><span class="sxs-lookup"><span data-stu-id="12a83-165">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="12a83-166">Spring en Azure</span><span class="sxs-lookup"><span data-stu-id="12a83-166">Spring on Azure</span></span>](/java/azure/spring-framework)

### <a name="additional-resources"></a><span data-ttu-id="12a83-167">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="12a83-167">Additional Resources</span></span>

<span data-ttu-id="12a83-168">Para más información sobre el uso de Azure con Java, consulte [Azure para desarrolladores de Java] y [Working with Azure DevOps and Java] (Trabajo con Azure DevOps y Java).</span><span class="sxs-lookup"><span data-stu-id="12a83-168">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Working with Azure DevOps and Java].</span></span>

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

[COSMOSDB01]: media/configure-spring-data-apache-cassandra-with-cosmos-db/create-cosmos-db-01.png
[COSMOSDB02]: media/configure-spring-data-apache-cassandra-with-cosmos-db/create-cosmos-db-02.png
[COSMOSDB03]: media/configure-spring-data-apache-cassandra-with-cosmos-db/create-cosmos-db-03.png
[COSMOSDB04]: media/configure-spring-data-apache-cassandra-with-cosmos-db/create-cosmos-db-04.png
[COSMOSDB05]: media/configure-spring-data-apache-cassandra-with-cosmos-db/create-cosmos-db-05.png
