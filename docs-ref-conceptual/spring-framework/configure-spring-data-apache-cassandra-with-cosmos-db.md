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
# <a name="how-to-use-spring-data-apache-cassandra-api-with-azure-cosmos-db"></a>Uso de Spring Data Apache Cassandra API con Azure Cosmos DB

## <a name="overview"></a>Información general

En este artículo se explica cómo crear una aplicación de ejemplo que utiliza [Spring Data] para almacenar y recuperar información mediante [Cassandra API de Azure Cosmos DB](/azure/cosmos-db/cassandra-introduction).

## <a name="prerequisites"></a>Requisitos previos

Los siguientes requisitos previos son necesarios para seguir los pasos descritos en este artículo:

* Una suscripción de Azure. Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN] o registrarse para obtener una [cuenta de Azure gratuita].
* Un kit de desarrollo de Java (JDK) admitido Para más información sobre los JDK disponibles para desarrollar en Azure, consulte <https://aka.ms/azure-jdks>.
* [Apache Maven](http://maven.apache.org/), versión 3.0 o posterior.
* [Curl ](https://curl.haxx.se/) o una utilidad HTTP similar para probar la funcionalidad.
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
   - **Nombre de cuenta**: Elija un nombre único para la cuenta de Cosmos DB; se utilizará para crear un nombre de dominio completo como *wingtiptoyscassandra.documents.azure.com*.
   - **API**: Especifique `Cassandra` para este tutorial.
   - **Ubicación**: especifique la región geográfica más cercana a la base de datos.

   ![Especificación de la configuración de la cuenta de Cosmos DB][COSMOSDB02]
   
1. Cuando haya especificado toda la información anterior, haga clic en **Revisar + crear**.

1. Si todo parece correcto en la página de revisión, haga clic en **Crear**.

   ![Revisión de la configuración de la cuenta de Cosmos DB][COSMOSDB03]

### <a name="add-a-keyspace-to-your-azure-cosmos-db-account"></a>Adición de un espacio de claves a la cuenta de Azure Cosmos DB

1. Vaya a Azure Portal en <https://portal.azure.com/> e inicie sesión.

1. Haga clic en **Todos los recursos** y, después, haga clic en la cuenta de Azure Cosmos DB que acaba de crear.

   ![Selección de la cuenta de Azure Cosmos DB][COSMOSDB04]

1. Haga clic en **Explorador de datos** y después en **New Keyspace** (Nuevo espacio de claves). Especifique un identificador único en **Id. de espacio de claves**, a continuación, haga clic en **Aceptar**.

   ![Creación de un espacio de claves de Cosmos DB][COSMOSDB05]

### <a name="retrieve-the-connection-settings-for-your-azure-cosmos-db-account"></a>Recuperación de la configuración de conexión para la cuenta de Azure Cosmos DB

1. Vaya a Azure Portal en <https://portal.azure.com/> e inicie sesión.

1. Haga clic en **Todos los recursos** y, después, haga clic en la cuenta de Azure Cosmos DB que acaba de crear.

   ![Selección de la cuenta de Azure Cosmos DB][COSMOSDB04]

1. Haga clic en **Cadenas de conexión** y copie los valores de los campos **Punto de contacto**, **Puerto**, **Nombre de usuario** y **Contraseña principal**; estos valores se utilizarán para configurar la aplicación posteriormente.

   ![Recuperación de la configuración de conexión de Cosmos DB][COSMOSDB05]

## <a name="configure-the-sample-application"></a>Configurar la aplicación de ejemplo

1. Abra un shell de comandos y clone el proyecto de ejemplo con un comando git como el siguiente ejemplo:

   ```shell
   git clone https://github.com/Azure-Samples/spring-data-cassandra-on-azure.git
   ```

1. Busque el archivo *application.properties* en el directorio *resources* del proyecto de ejemplo, o cree el archivo si todavía no existe.

1. Abra el archivo *application.properties* en un editor de texto y agréguele o configure las siguientes líneas; luego, sustituya los valores de ejemplo por los valores adecuados que se mencionaron anteriormente:

   ```yaml
   spring.data.cassandra.contact-points=wingtiptoyscassandra.cassandra.cosmosdb.azure.com
   spring.data.cassandra.port=10350
   spring.data.cassandra.username=wingtiptoyscassandra
   spring.data.cassandra.password=********
   ```
   Donde:

   | Parámetro | DESCRIPCIÓN |
   |---|---|
   | `spring.data.cassandra.contact-points` | Especifica el **punto de contacto** que se mencionó anteriormente en este artículo. |
   | `spring.data.cassandra.port` | Especifica el **puerto** que se mencionó anteriormente en este artículo. |
   | `spring.data.cassandra.username` | Especifica el **nombre de usuario** que se mencionó anteriormente en este artículo. |
   | `spring.data.cassandra.password` | Especifica la **contraseña principal** que se mencionó anteriormente en este artículo. |

1. Guarde y cierre el archivo *application.properties*.

## <a name="package-and-test-the-sample-application"></a>Empaquetado y prueba de la aplicación de ejemplo 

1. Compile la aplicación de ejemplo con Maven; por ejemplo:

   ```shell
   mvn clean package
   ```

1. Inicie la aplicación de ejemplo; por ejemplo:

   ```shell
   java -jar target/spring-data-cassandra-on-azure-0.1.0-SNAPSHOT.jar
   ```

1. Cree nuevos registros con `curl` desde un símbolo del sistema como en los ejemplos siguientes:

   ```shell
   curl -s -d '{"name":"dog","species":"canine"}' -H "Content-Type: application/json" -X POST http://localhost:8080/pets

   curl -s -d '{"name":"cat","species":"feline"}' -H "Content-Type: application/json" -X POST http://localhost:8080/pets
   ```

   La aplicación debe devolver valores similares a los siguientes:

   ```shell
   Added Pet{id=60fa8cb0-0423-11e9-9a70-39311962166b, name='dog', species='canine'}.

   Added Pet{id=72c1c9e0-0423-11e9-9a70-39311962166b, name='cat', species='feline'}.
   ```

1. Recupere todos los registros existentes con `curl` desde un símbolo del sistema como los siguientes ejemplos:

   ```shell
   curl -s http://localhost:8080/pets
   ```
    
   La aplicación debe devolver valores similares a los siguientes:

   ```json
   [{"id":"60fa8cb0-0423-11e9-9a70-39311962166b","name":"dog","species":"canine"},{"id":"72c1c9e0-0423-11e9-9a70-39311962166b","name":"cat","species":"feline"}]
   ```

## <a name="summary"></a>Resumen

En este tutorial ha creado una aplicación Java de ejemplo que utiliza Spring Data para almacenar y recuperar información mediante Cassandra API de Azure Cosmos DB.

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

[COSMOSDB01]: media/configure-spring-data-apache-cassandra-with-cosmos-db/create-cosmos-db-01.png
[COSMOSDB02]: media/configure-spring-data-apache-cassandra-with-cosmos-db/create-cosmos-db-02.png
[COSMOSDB03]: media/configure-spring-data-apache-cassandra-with-cosmos-db/create-cosmos-db-03.png
[COSMOSDB04]: media/configure-spring-data-apache-cassandra-with-cosmos-db/create-cosmos-db-04.png
[COSMOSDB05]: media/configure-spring-data-apache-cassandra-with-cosmos-db/create-cosmos-db-05.png
