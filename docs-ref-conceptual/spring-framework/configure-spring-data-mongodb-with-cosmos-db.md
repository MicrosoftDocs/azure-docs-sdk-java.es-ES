---
title: Uso de Spring Data MongoDB API con Azure Cosmos DB
description: Aprenda a usar Spring Data MongoDB API con Azure Cosmos DB.
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
ms.openlocfilehash: 55fb356820e2cc5eb8d1fe4030053d9e580583af
ms.sourcegitcommit: f0f140b0862ca5338b1b7e5c33cec3e58a70b8fd
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/03/2019
ms.locfileid: "53992543"
---
# <a name="how-to-use-spring-data-mongodb-api-with-azure-cosmos-db"></a><span data-ttu-id="cc734-103">Uso de Spring Data MongoDB API con Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="cc734-103">How to use Spring Data MongoDB API with Azure Cosmos DB</span></span>

## <a name="overview"></a><span data-ttu-id="cc734-104">Información general</span><span class="sxs-lookup"><span data-stu-id="cc734-104">Overview</span></span>

<span data-ttu-id="cc734-105">En este artículo se explica cómo crear una aplicación de ejemplo que utiliza [Spring Data] para almacenar y recuperar información mediante [MongoDB API de Azure Cosmos DB](/azure/cosmos-db/mongodb-introduction).</span><span class="sxs-lookup"><span data-stu-id="cc734-105">This article demonstrates creating a sample application that uses [Spring Data] to store and retrieve information using the [Azure Cosmos DB MongoDB API](/azure/cosmos-db/mongodb-introduction).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cc734-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="cc734-106">Prerequisites</span></span>

<span data-ttu-id="cc734-107">Los siguientes requisitos previos son necesarios para seguir los pasos descritos en este artículo:</span><span class="sxs-lookup"><span data-stu-id="cc734-107">The following prerequisites are required in order to complete the steps in this article:</span></span>

* <span data-ttu-id="cc734-108">Una suscripción de Azure. Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN] o registrarse para obtener una [cuenta de Azure gratuita].</span><span class="sxs-lookup"><span data-stu-id="cc734-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="cc734-109">Un kit de desarrollo de Java (JDK) admitido</span><span class="sxs-lookup"><span data-stu-id="cc734-109">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="cc734-110">Para más información sobre los JDK disponibles para desarrollar en Azure, consulte <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="cc734-110">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="cc734-111">[Apache Maven](http://maven.apache.org/), versión 3.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="cc734-111">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>
* <span data-ttu-id="cc734-112">Un cliente [Git](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="cc734-112">A [Git](https://git-scm.com/downloads) client.</span></span>

## <a name="create-an-azure-cosmos-db-account"></a><span data-ttu-id="cc734-113">Creación de una cuenta de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="cc734-113">Create an Azure Cosmos DB account</span></span>

### <a name="create-a-cosmos-db-account-using-the-azure-portal"></a><span data-ttu-id="cc734-114">Creación de una cuenta de Cosmos DB mediante Azure Portal</span><span class="sxs-lookup"><span data-stu-id="cc734-114">Create a Cosmos DB account using the Azure Portal</span></span>

> [!NOTE]
> 
> <span data-ttu-id="cc734-115">Puede leer información más detallada sobre cómo crear cuentas de Azure Cosmos DB en la [documentación de Azure Cosmos DB](/azure/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="cc734-115">You can read more detailed information about creating Azure Cosmos DB accounts in [Azure Cosmos DB Documentation](/azure/cosmos-db/).</span></span>

1. <span data-ttu-id="cc734-116">Vaya a Azure Portal en <https://portal.azure.com/> e inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="cc734-116">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="cc734-117">Haga clic sucesivamente en **+ Crear un recurso**, en **Bases de datos** y, finalmente, en **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="cc734-117">Click **+Create a resource**, then **Databases**, and then click **Azure Cosmos DB**.</span></span>

   ![Creación de una cuenta de Azure Cosmos DB][COSMOSDB01]

1. <span data-ttu-id="cc734-119">Especifique la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="cc734-119">Specify the following information:</span></span>

   - <span data-ttu-id="cc734-120">**Suscripción**: especifique la suscripción de Azure que se va a usar.</span><span class="sxs-lookup"><span data-stu-id="cc734-120">**Subscription**: Specify your Azure subscription to use.</span></span>
   - <span data-ttu-id="cc734-121">**Grupo de recursos**: especifique si desea crear un nuevo grupo de recursos o elija uno existente.</span><span class="sxs-lookup"><span data-stu-id="cc734-121">**Resource group**: Specify whether to create a new resource group, or choose an existing resource group.</span></span>
   - <span data-ttu-id="cc734-122">**Nombre de cuenta**: Elija un nombre único para la cuenta de Cosmos DB; se utilizará para crear un nombre de dominio completo como *wingtiptoysmongodb.documents.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="cc734-122">**Account name**: Choose a unique name for your Cosmos DB account; this will be used to create a fully-qualified domain name like *wingtiptoysmongodb.documents.azure.com*.</span></span>
   - <span data-ttu-id="cc734-123">**API**: Especifique `Azure Cosmos DB for MongoDB API` para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="cc734-123">**API**: Specify `Azure Cosmos DB for MongoDB API` for this tutorial.</span></span>
   - <span data-ttu-id="cc734-124">**Ubicación**: especifique la región geográfica más cercana a la base de datos.</span><span class="sxs-lookup"><span data-stu-id="cc734-124">**Location**: Specify the closest geographic region for your database.</span></span>

   ![Especificación de la configuración de la cuenta de Cosmos DB][COSMOSDB02]
   
1. <span data-ttu-id="cc734-126">Cuando haya especificado toda la información anterior, haga clic en **Revisar + crear**.</span><span class="sxs-lookup"><span data-stu-id="cc734-126">When you have entered all of the above information, click **Review + create**.</span></span>

1. <span data-ttu-id="cc734-127">Si todo parece correcto en la página de revisión, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="cc734-127">If everything looks correct on the review page, click **Create**.</span></span>

   ![Revisión de la configuración de la cuenta de Cosmos DB][COSMOSDB03]

### <a name="retrieve-the-connection-string-for-your-azure-cosmos-db-account"></a><span data-ttu-id="cc734-129">Recuperación de la cadena de conexión para la cuenta de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="cc734-129">Retrieve the connection string for your Azure Cosmos DB account</span></span>

1. <span data-ttu-id="cc734-130">Vaya a Azure Portal en <https://portal.azure.com/> e inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="cc734-130">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="cc734-131">Haga clic en **Todos los recursos** y, después, haga clic en la cuenta de Azure Cosmos DB que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="cc734-131">Click **All Resources**, then click the Azure Cosmos DB account you just created.</span></span>

   ![Selección de la cuenta de Azure Cosmos DB][COSMOSDB04]

1. <span data-ttu-id="cc734-133">Haga clic en **Cadenas de conexión** y copie el valor del campo **Cadena de conexión principal**; utilizará ese valor para configurar la aplicación más adelante.</span><span class="sxs-lookup"><span data-stu-id="cc734-133">Click **Connection strings**, and copy the value for the **Primary Connection String** field; you will use that value to configure your application later.</span></span>

   ![Recuperación de la cadena de conexión de Cosmos DB][COSMOSDB06]

## <a name="configure-the-sample-application"></a><span data-ttu-id="cc734-135">Configurar la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="cc734-135">Configure the sample application</span></span>

1. <span data-ttu-id="cc734-136">Abra un shell de comandos y clone el proyecto de ejemplo con un comando git como el siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="cc734-136">Open a command shell and clone the sample project using a git command like the following example:</span></span>

   ```shell
   git clone https://github.com/spring-guides/gs-accessing-data-mongodb.git
   ```

1. <span data-ttu-id="cc734-137">Cree un directorio *resources* en el directorio *&lt;raíz del proyecto&gt;/complete/src/main* del proyecto de ejemplo y cree un archivo *application.properties* en el directorio *resources*.</span><span class="sxs-lookup"><span data-stu-id="cc734-137">Create a *resources* directory in the *&lt;project root&gt;/complete/src/main* directory of the sample project, and create an *application.properties* file in the *resources* directory.</span></span>

1. <span data-ttu-id="cc734-138">Abra el archivo *application.properties* en un editor de texto y agréguele las siguientes líneas; después, sustituya los valores de ejemplo por los valores adecuados que se mencionaron anteriormente:</span><span class="sxs-lookup"><span data-stu-id="cc734-138">Open the *application.properties* file in a text editor, and add the following lines in the file, and replace the sample values with the appropriate values from earlier:</span></span>

   ```yaml
   spring.data.mongodb.database=wingtiptoysmongodb
   spring.data.mongodb.uri=mongodb://wingtiptoysmongodb:AbCdEfGhIjKlMnOpQrStUvWxYz==@wingtiptoysmongodb.documents.azure.com:10255/?ssl=true&replicaSet=globaldb
   ```
   <span data-ttu-id="cc734-139">Donde:</span><span class="sxs-lookup"><span data-stu-id="cc734-139">Where:</span></span>

   | <span data-ttu-id="cc734-140">Parámetro</span><span class="sxs-lookup"><span data-stu-id="cc734-140">Parameter</span></span> | <span data-ttu-id="cc734-141">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="cc734-141">Description</span></span> |
   |---|---|
   | `spring.data.mongodb.database` | <span data-ttu-id="cc734-142">Especifica el nombre de la cuenta de Cosmos DB que se mencionó anteriormente en este artículo.</span><span class="sxs-lookup"><span data-stu-id="cc734-142">Specifies the name of your Cosmos DB account from earlier in this article.</span></span> |
   | `spring.data.mongodb.uri` | <span data-ttu-id="cc734-143">Especifica la **cadena de conexión principal** que se mencionó anteriormente en este artículo.</span><span class="sxs-lookup"><span data-stu-id="cc734-143">Specifies the **Primary Connection String** from earlier in this article.</span></span> |

1. <span data-ttu-id="cc734-144">Guarde y cierre el archivo *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="cc734-144">Save and close the *application.properties* file.</span></span>

## <a name="package-and-test-the-sample-application"></a><span data-ttu-id="cc734-145">Empaquetado y prueba de la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="cc734-145">Package and test the sample application</span></span> 

1. <span data-ttu-id="cc734-146">Cree la aplicación de ejemplo con Maven y configure Maven para omitir pruebas, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="cc734-146">Build the sample application with Maven, and configure Maven to skip tests; for example:</span></span>

   ```shell
   mvn clean package -DskipTests
   ```

1. <span data-ttu-id="cc734-147">Inicie la aplicación de ejemplo; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="cc734-147">Start the sample application; for example:</span></span>

   ```shell
   java -jar target/gs-accessing-data-mongodb-0.1.0.jar
   ```
    
   <span data-ttu-id="cc734-148">La aplicación debe devolver valores similares a los siguientes:</span><span class="sxs-lookup"><span data-stu-id="cc734-148">Your application should return values like the following:</span></span>

   ```json
   Customers found with findAll():
   -------------------------------
   Customer[id=5c1b4ae4d0b5080ac105cc13, firstName='Alice', lastName='Smith']
   Customer[id=5c1b4ae4d0b5080ac105cc14, firstName='Bob', lastName='Smith']
   
   Customer found with findByFirstName('Alice'):
   --------------------------------
   Customer[id=5c1b4ae4d0b5080ac105cc13, firstName='Alice', lastName='Smith']
   Customers found with findByLastName('Smith'):
   --------------------------------
   Customer[id=5c1b4ae4d0b5080ac105cc13, firstName='Alice', lastName='Smith']
   Customer[id=5c1b4ae4d0b5080ac105cc14, firstName='Bob', lastName='Smith']
   ```

## <a name="summary"></a><span data-ttu-id="cc734-149">Resumen</span><span class="sxs-lookup"><span data-stu-id="cc734-149">Summary</span></span>

<span data-ttu-id="cc734-150">En este tutorial ha creado una aplicación Java de ejemplo que utiliza Spring Data para almacenar y recuperar información mediante MongoDB API de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="cc734-150">In this tutorial, you created a sample Java application that uses Spring Data to store and retrieve information using the Azure Cosmos DB MongoDB API.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cc734-151">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cc734-151">Next steps</span></span>

<span data-ttu-id="cc734-152">Para más información acerca de Spring y Azure, vaya al centro de documentación de Azure.</span><span class="sxs-lookup"><span data-stu-id="cc734-152">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="cc734-153">Spring en Azure</span><span class="sxs-lookup"><span data-stu-id="cc734-153">Spring on Azure</span></span>](/java/azure/spring-framework)

### <a name="additional-resources"></a><span data-ttu-id="cc734-154">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="cc734-154">Additional Resources</span></span>

<span data-ttu-id="cc734-155">Para más información sobre el uso de Azure con Java, consulte [Azure para desarrolladores de Java] y [Working with Azure DevOps and Java] (Trabajo con Azure DevOps y Java).</span><span class="sxs-lookup"><span data-stu-id="cc734-155">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Working with Azure DevOps and Java].</span></span>

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

[COSMOSDB01]: media/configure-spring-data-mongodb-with-cosmos-db/create-cosmos-db-01.png
[COSMOSDB02]: media/configure-spring-data-mongodb-with-cosmos-db/create-cosmos-db-02.png
[COSMOSDB03]: media/configure-spring-data-mongodb-with-cosmos-db/create-cosmos-db-03.png
[COSMOSDB04]: media/configure-spring-data-mongodb-with-cosmos-db/create-cosmos-db-04.png
[COSMOSDB06]: media/configure-spring-data-mongodb-with-cosmos-db/create-cosmos-db-06.png
