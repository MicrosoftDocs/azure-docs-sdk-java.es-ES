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
# <a name="how-to-use-spring-data-mongodb-api-with-azure-cosmos-db"></a>Uso de Spring Data MongoDB API con Azure Cosmos DB

## <a name="overview"></a>Información general

En este artículo se explica cómo crear una aplicación de ejemplo que utiliza [Spring Data] para almacenar y recuperar información mediante [MongoDB API de Azure Cosmos DB](/azure/cosmos-db/mongodb-introduction).

## <a name="prerequisites"></a>Requisitos previos

Los siguientes requisitos previos son necesarios para seguir los pasos descritos en este artículo:

* Una suscripción de Azure. Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN] o registrarse para obtener una [cuenta de Azure gratuita].
* Un kit de desarrollo de Java (JDK) admitido Para más información sobre los JDK disponibles para desarrollar en Azure, consulte <https://aka.ms/azure-jdks>.
* [Apache Maven](http://maven.apache.org/), versión 3.0 o posterior.
* Un cliente [Git](https://git-scm.com/downloads).

## <a name="create-an-azure-cosmos-db-account"></a>Creación de una cuenta de Azure Cosmos DB

### <a name="create-a-cosmos-db-account-using-the-azure-portal"></a>Creación de una cuenta de Cosmos DB mediante Azure Portal

> [!NOTE]
> 
> Puede leer información más detallada sobre cómo crear cuentas de Azure Cosmos DB en la [documentación de Azure Cosmos DB](/azure/cosmos-db/).

1. Vaya a Azure Portal en <https://portal.azure.com/> e inicie sesión.

1. Haga clic sucesivamente en **+ Crear un recurso**, en **Bases de datos** y, finalmente, en **Azure Cosmos DB**.

   ![Creación de una cuenta de Azure Cosmos DB][COSMOSDB01]

1. Especifique la siguiente información:

   - **Suscripción**: especifique la suscripción de Azure que se va a usar.
   - **Grupo de recursos**: especifique si desea crear un nuevo grupo de recursos o elija uno existente.
   - **Nombre de cuenta**: Elija un nombre único para la cuenta de Cosmos DB; se utilizará para crear un nombre de dominio completo como *wingtiptoysmongodb.documents.azure.com*.
   - **API**: Especifique `Azure Cosmos DB for MongoDB API` para este tutorial.
   - **Ubicación**: especifique la región geográfica más cercana a la base de datos.

   ![Especificación de la configuración de la cuenta de Cosmos DB][COSMOSDB02]
   
1. Cuando haya especificado toda la información anterior, haga clic en **Revisar + crear**.

1. Si todo parece correcto en la página de revisión, haga clic en **Crear**.

   ![Revisión de la configuración de la cuenta de Cosmos DB][COSMOSDB03]

### <a name="retrieve-the-connection-string-for-your-azure-cosmos-db-account"></a>Recuperación de la cadena de conexión para la cuenta de Azure Cosmos DB

1. Vaya a Azure Portal en <https://portal.azure.com/> e inicie sesión.

1. Haga clic en **Todos los recursos** y, después, haga clic en la cuenta de Azure Cosmos DB que acaba de crear.

   ![Selección de la cuenta de Azure Cosmos DB][COSMOSDB04]

1. Haga clic en **Cadenas de conexión** y copie el valor del campo **Cadena de conexión principal**; utilizará ese valor para configurar la aplicación más adelante.

   ![Recuperación de la cadena de conexión de Cosmos DB][COSMOSDB06]

## <a name="configure-the-sample-application"></a>Configurar la aplicación de ejemplo

1. Abra un shell de comandos y clone el proyecto de ejemplo con un comando git como el siguiente ejemplo:

   ```shell
   git clone https://github.com/spring-guides/gs-accessing-data-mongodb.git
   ```

1. Cree un directorio *resources* en el directorio *&lt;raíz del proyecto&gt;/complete/src/main* del proyecto de ejemplo y cree un archivo *application.properties* en el directorio *resources*.

1. Abra el archivo *application.properties* en un editor de texto y agréguele las siguientes líneas; después, sustituya los valores de ejemplo por los valores adecuados que se mencionaron anteriormente:

   ```yaml
   spring.data.mongodb.database=wingtiptoysmongodb
   spring.data.mongodb.uri=mongodb://wingtiptoysmongodb:AbCdEfGhIjKlMnOpQrStUvWxYz==@wingtiptoysmongodb.documents.azure.com:10255/?ssl=true&replicaSet=globaldb
   ```
   Donde:

   | Parámetro | DESCRIPCIÓN |
   |---|---|
   | `spring.data.mongodb.database` | Especifica el nombre de la cuenta de Cosmos DB que se mencionó anteriormente en este artículo. |
   | `spring.data.mongodb.uri` | Especifica la **cadena de conexión principal** que se mencionó anteriormente en este artículo. |

1. Guarde y cierre el archivo *application.properties*.

## <a name="package-and-test-the-sample-application"></a>Empaquetado y prueba de la aplicación de ejemplo 

1. Cree la aplicación de ejemplo con Maven y configure Maven para omitir pruebas, por ejemplo:

   ```shell
   mvn clean package -DskipTests
   ```

1. Inicie la aplicación de ejemplo; por ejemplo:

   ```shell
   java -jar target/gs-accessing-data-mongodb-0.1.0.jar
   ```
    
   La aplicación debe devolver valores similares a los siguientes:

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

## <a name="summary"></a>Resumen

En este tutorial ha creado una aplicación Java de ejemplo que utiliza Spring Data para almacenar y recuperar información mediante MongoDB API de Azure Cosmos DB.

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

[COSMOSDB01]: media/configure-spring-data-mongodb-with-cosmos-db/create-cosmos-db-01.png
[COSMOSDB02]: media/configure-spring-data-mongodb-with-cosmos-db/create-cosmos-db-02.png
[COSMOSDB03]: media/configure-spring-data-mongodb-with-cosmos-db/create-cosmos-db-03.png
[COSMOSDB04]: media/configure-spring-data-mongodb-with-cosmos-db/create-cosmos-db-04.png
[COSMOSDB06]: media/configure-spring-data-mongodb-with-cosmos-db/create-cosmos-db-06.png
