---
title: Azure para desarrolladores de Java | Microsoft Docs
description: Referencia de SDK y API de Java para Azure
keywords: Java para Azure, referencia de API de Java para Azure, biblioteca de clases Java para Azure, Azure SDK
author: routlaw
manager: douge
ms.assetid: 7b92e776-959b-4632-8b1d-047ce1417616
ms.service: Azure
ms.devlang: java
ms.topic: reference
ms.technology: Azure
ms.date: 3/06/2016
ms.openlocfilehash: 5c8bb4b81080461285551573eefc0d76b47b2d3d
ms.sourcegitcommit: 61030d025614b084e897809e603b2ec79900ec8d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/03/2018
ms.locfileid: "30302553"
---
# <a name="azure-libraries-for-java"></a><span data-ttu-id="efe89-104">Bibliotecas de Azure para Java</span><span class="sxs-lookup"><span data-stu-id="efe89-104">Azure libraries for Java</span></span>

<span data-ttu-id="efe89-105">Las bibliotecas de Azure le ayudarán a utilizar los servicios de Azure en aplicaciones Java usando interfaces nativas.</span><span class="sxs-lookup"><span data-stu-id="efe89-105">Azure libraries help you consume Azure services in your Java apps using native interfaces.</span></span> <span data-ttu-id="efe89-106">Cada biblioteca es independiente y se puede utilizar por separado.</span><span class="sxs-lookup"><span data-stu-id="efe89-106">Each library is independent and can be used separately from the others another.</span></span>

| | | | |
|:-------------:|:----------:|:----:|:---:|
| [<span data-ttu-id="efe89-107">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="efe89-107">Azure Storage</span></span>](#azure-storage) | [<span data-ttu-id="efe89-108">SQL Database</span><span class="sxs-lookup"><span data-stu-id="efe89-108">SQL Database</span></span>](#sql-database)  | [<span data-ttu-id="efe89-109">Redis Cache</span><span class="sxs-lookup"><span data-stu-id="efe89-109">Redis Cache</span></span>](#redis-cache)   | [<span data-ttu-id="efe89-110">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="efe89-110">Azure Cosmos DB</span></span>](#cosmos-db) |
| [<span data-ttu-id="efe89-111">Service Bus</span><span class="sxs-lookup"><span data-stu-id="efe89-111">Service Bus</span></span>](#servicebus)  | [<span data-ttu-id="efe89-112">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="efe89-112">Azure Active Directory</span></span>](#azuread) | [<span data-ttu-id="efe89-113">Key Vault</span><span class="sxs-lookup"><span data-stu-id="efe89-113">Key Vault</span></span>](#keyvault)  | [<span data-ttu-id="efe89-114">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="efe89-114">Event Hub</span></span>](#eventhub)
| [<span data-ttu-id="efe89-115">Servicio IoT</span><span class="sxs-lookup"><span data-stu-id="efe89-115">IoT Service</span></span>](#iotservice) | [<span data-ttu-id="efe89-116">Dispositivo IoT</span><span class="sxs-lookup"><span data-stu-id="efe89-116">IoT Device</span></span>](#iotdevice) | [<span data-ttu-id="efe89-117">Data Lake</span><span class="sxs-lookup"><span data-stu-id="efe89-117">Data Lake</span></span>](#datalake)  | [<span data-ttu-id="efe89-118">AppInsights</span><span class="sxs-lookup"><span data-stu-id="efe89-118">AppInsights</span></span>](#appinsights) | 
| [<span data-ttu-id="efe89-119">Batch</span><span class="sxs-lookup"><span data-stu-id="efe89-119">Batch</span></span>](#batch) | [<span data-ttu-id="efe89-120">Administración de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="efe89-120">Manage Azure resources</span></span>](#management) |

## <a name="install-with-maven"></a><span data-ttu-id="efe89-121">Instalación con Maven</span><span class="sxs-lookup"><span data-stu-id="efe89-121">Install with Maven</span></span>

<span data-ttu-id="efe89-122">Agregue una entrada de dependencia en el archivo `pom.xml` para importar una biblioteca en el proyecto [Maven](https://maven.apache.org).</span><span class="sxs-lookup"><span data-stu-id="efe89-122">Add a dependency entry in your `pom.xml` to import a library into your [Maven](https://maven.apache.org) project.</span></span>

<span data-ttu-id="efe89-123">Por ejemplo, para incluir la versión más reciente de las [bibliotecas de administración de Azure para Java](#management):</span><span class="sxs-lookup"><span data-stu-id="efe89-123">For example, to include the latest version of the [Azure management libraries for Java](#management):</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure</artifactId>
    <version>1.3.0</version>
</dependency>
```

<span data-ttu-id="efe89-124">Se admiten otras herramientas de compilación de Java como Gradle, pero no se proporcionan los pasos de instalación en este artículo.</span><span class="sxs-lookup"><span data-stu-id="efe89-124">Other Java build tools like Gradle are supported but the install steps are not provided in this article.</span></span> <span data-ttu-id="efe89-125">Revise la documentación de la herramienta de compilación sobre cómo utilizar las importaciones de Maven.</span><span class="sxs-lookup"><span data-stu-id="efe89-125">Review the documentation for your build tool on how to consume Maven imports.</span></span>

## <a name="azure-service-libraries"></a><span data-ttu-id="efe89-126">Bibliotecas de servicio de Azure</span><span class="sxs-lookup"><span data-stu-id="efe89-126">Azure service libraries</span></span>

<span data-ttu-id="efe89-127">Integre los servicios de Azure para agregar funcionalidad a las aplicaciones con estas bibliotecas.</span><span class="sxs-lookup"><span data-stu-id="efe89-127">Integrate Azure services to add functionality to your apps using these libraries.</span></span> <span data-ttu-id="efe89-128">Obtenga más información acerca de cómo crear aplicaciones con servicios de Azure en el [centro para desarrolladores de Java](https://azure.microsoft.com/develop/java).</span><span class="sxs-lookup"><span data-stu-id="efe89-128">Learn more about building apps with Azure services at the [Java developer center](https://azure.microsoft.com/develop/java).</span></span>

<a name="azure-storage"></a>

### <a name="azure-storageazurestoragestorage-introduction"></a>[<span data-ttu-id="efe89-129">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="efe89-129">Azure Storage</span></span>](/azure/storage/storage-introduction)  

<span data-ttu-id="efe89-130">Almacenamiento de datos y mensajería para las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="efe89-130">Data storage and messaging for your applications.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-storage</artifactId>
    <version>5.4.0</version>
</dependency>
```   

<span data-ttu-id="efe89-131">[Ejemplos](https://github.com/Azure/azure-storage-java/tree/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage) | [Referencia](/java/api/overview/azure/storage) | [GitHub](https://github.com/Azure/azure-storage-java)  | [Notas de la versión](https://github.com/Azure/azure-storage-java/blob/master/ChangeLog.txt)</span><span class="sxs-lookup"><span data-stu-id="efe89-131">[Samples](https://github.com/Azure/azure-storage-java/tree/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage) | [Reference](/java/api/overview/azure/storage) | [GitHub](https://github.com/Azure/azure-storage-java)  | [Release Notes](https://github.com/Azure/azure-storage-java/blob/master/ChangeLog.txt)</span></span>

<a name="sql-database"></a>

### <a name="sql-databaseazuresql-databasesql-database-technical-overview"></a>[<span data-ttu-id="efe89-132">SQL Database</span><span class="sxs-lookup"><span data-stu-id="efe89-132">SQL Database</span></span>](/azure/sql-database/sql-database-technical-overview)

<span data-ttu-id="efe89-133">Controlador JDBC para Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="efe89-133">JDBC driver for Azure SQL Database.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>6.2.1.jre8</version>
</dependency>
```

<span data-ttu-id="efe89-134">[Ejemplos](/sql/connect/jdbc/step-3-proof-of-concept-connecting-to-sql-using-java) | [Referencia](/java/api/overview/azure/sql) | [GitHub](https://github.com/Microsoft/mssql-jdbc)  | [Notas de la versión](https://github.com/Microsoft/mssql-jdbc/blob/master/CHANGELOG.md)</span><span class="sxs-lookup"><span data-stu-id="efe89-134">[Samples](/sql/connect/jdbc/step-3-proof-of-concept-connecting-to-sql-using-java) | [Reference](/java/api/overview/azure/sql) | [GitHub](https://github.com/Microsoft/mssql-jdbc)  | [Release Notes](https://github.com/Microsoft/mssql-jdbc/blob/master/CHANGELOG.md)</span></span>

<a name="redis-cache"></a>

### <a name="redis-cachehttpsazuremicrosoftcomservicescache"></a>[<span data-ttu-id="efe89-135">Redis Cache</span><span class="sxs-lookup"><span data-stu-id="efe89-135">Redis Cache</span></span>](https://azure.microsoft.com/services/cache/)

<span data-ttu-id="efe89-136">Almacén de pares clave-valor de baja latencia y alto rendimiento.</span><span class="sxs-lookup"><span data-stu-id="efe89-136">Low-latency, high-performance key-value store.</span></span>

```XML
<dependency>
    <groupId>redis.clients</groupId>
    <artifactId>jedis</artifactId>
    <version>2.9.0</version>
    <type>jar</type>
    <scope>compile</scope>
</dependency>
```   

<span data-ttu-id="efe89-137">[Ejemplos](/azure/redis-cache/cache-java-get-started) | [Referencia](http://xetorthio.github.io/jedis)  | [GitHub](https://github.com/xetorthio/jedis)  | [Notas de la versión](https://github.com/xetorthio/jedis/releases)</span><span class="sxs-lookup"><span data-stu-id="efe89-137">[Samples](/azure/redis-cache/cache-java-get-started) | [Reference](http://xetorthio.github.io/jedis)  | [GitHub](https://github.com/xetorthio/jedis)  | [Release Notes](https://github.com/xetorthio/jedis/releases)</span></span>  

<a name="cosmos-db"></a>

### <a name="azure-cosmos-dbazurecosmos-dbintroduction"></a>[<span data-ttu-id="efe89-138">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="efe89-138">Azure Cosmos DB</span></span>](/azure/cosmos-db/introduction)

<span data-ttu-id="efe89-139">Base de datos NoSQL escalable con documentos JSON y la sintaxis de consulta SQL o JavaScript.</span><span class="sxs-lookup"><span data-stu-id="efe89-139">Scalable NoSQL database with JSON documents and a SQL or JavaScript query syntax.</span></span>   

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-documentdb</artifactId>
    <version>1.12.0</version>
</dependency>
```

<span data-ttu-id="efe89-140">[Ejemplos](/azure/cosmos-db/sql-api-java-application) | [Referencia](http://azure.github.io/azure-documentdb-java/) | [GitHub](https://github.com/Azure/azure-documentdb-java)   | [Notas de la versión](https://github.com/Azure/azure-documentdb-java/blob/master/changelog.md)</span><span class="sxs-lookup"><span data-stu-id="efe89-140">[Samples](/azure/cosmos-db/sql-api-java-application) | [Reference](http://azure.github.io/azure-documentdb-java/) | [GitHub](https://github.com/Azure/azure-documentdb-java)   | [Release Notes](https://github.com/Azure/azure-documentdb-java/blob/master/changelog.md)</span></span>

<a name="servicebus"></a>
 
 ### <a name="servicebusazureservice-bus-messagingservice-bus-messaging-overview"></a>[<span data-ttu-id="efe89-141">Service Bus</span><span class="sxs-lookup"><span data-stu-id="efe89-141">ServiceBus</span></span>](/azure/service-bus-messaging/service-bus-messaging-overview) 
    
 <span data-ttu-id="efe89-142">Service Bus es un servicio de plataforma de mensajería transaccional de clase empresarial.</span><span class="sxs-lookup"><span data-stu-id="efe89-142">Service Bus is an enterprise-class, transactional messaging platform service.</span></span>
 
 ```XML
 <dependency> 
     <groupId>com.microsoft.azure</groupId> 
     <artifactId>azure-servicebus</artifactId> 
     <version>1.0.0</version> 
 </dependency>   
 ```
 
 <span data-ttu-id="efe89-143">[Ejemplos](https://github.com/Azure/azure-service-bus/tree/master/samples/Java) | [Referencia](https://docs.microsoft.com/java/api/overview/azure/servicebus) | [GitHub](https://github.com/azure/azure-service-bus-java)  | [Notas de la versión](https://github.com/Azure/azure-service-bus-java)</span><span class="sxs-lookup"><span data-stu-id="efe89-143">[Samples](https://github.com/Azure/azure-service-bus/tree/master/samples/Java) | [Reference](https://docs.microsoft.com/java/api/overview/azure/servicebus) | [GitHub](https://github.com/azure/azure-service-bus-java)  | [Release Notes](https://github.com/Azure/azure-service-bus-java)</span></span>   
  
<a name="azuread"></a>

### <a name="azure-active-directoryazureactive-directoryactive-directory-whatis"></a>[<span data-ttu-id="efe89-144">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="efe89-144">Azure Active Directory</span></span>](/azure/active-directory/active-directory-whatis)   

<span data-ttu-id="efe89-145">Administración de identidades e inicio de sesión seguro para sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="efe89-145">Identity management and secure sign-in for your applications.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>adal4j</artifactId>
    <version>1.2.0</version>
</dependency>
```
   
<span data-ttu-id="efe89-146">[Ejemplos](https://github.com/Azure-Samples?utf8=%E2%9C%93&q=active%20directory%20&type=&language=java) | [Referencia](/java/api/overview/azure/activedirectory) | [GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-java) | [Notas de la versión](https://github.com/AzureAD/azure-activedirectory-library-for-javaT-)</span><span class="sxs-lookup"><span data-stu-id="efe89-146">[Samples](https://github.com/Azure-Samples?utf8=%E2%9C%93&q=active%20directory%20&type=&language=java) | [Reference](/java/api/overview/azure/activedirectory) | [GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-java) | [Release Notes](https://github.com/AzureAD/azure-activedirectory-library-for-javaT-)</span></span>
 
<a name="keyvault"></a>

### <a name="key-vaultazurekey-vault"></a>[<span data-ttu-id="efe89-147">Key Vault</span><span class="sxs-lookup"><span data-stu-id="efe89-147">Key Vault</span></span>](/azure/key-vault) 

<span data-ttu-id="efe89-148">Acceso seguro a claves y secretos desde las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="efe89-148">Safely access keys and secrets from your applications.</span></span> 

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-keyvault</artifactId>
    <version>1.0.0</version>
</dependency>
```

<span data-ttu-id="efe89-149">[Ejemplos](https://github.com/Azure-Samples/key-vault-java-manage-key-vaults) | [Referencia](/java/api/overview/azure/keyvault) | [GitHub](https://github.com/Azure/azure-keyvault-java) | [Notas de la versión](https://github.com/Azure/azure-keyvault-java)</span><span class="sxs-lookup"><span data-stu-id="efe89-149">[Samples](https://github.com/Azure-Samples/key-vault-java-manage-key-vaults) | [Reference](/java/api/overview/azure/keyvault) | [GitHub](https://github.com/Azure/azure-keyvault-java) | [Release Notes](https://github.com/Azure/azure-keyvault-java)</span></span> 

<a name="eventhub"></a>

### <a name="event-hubazureevent-hubsevent-hubs-what-is-event-hubs"></a>[<span data-ttu-id="efe89-150">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="efe89-150">Event Hub</span></span>](/azure/event-hubs/event-hubs-what-is-event-hubs) 
   
<span data-ttu-id="efe89-151">Control de eventos y datos de telemetría de alto rendimiento para instrumentación o escenarios de IoT.</span><span class="sxs-lookup"><span data-stu-id="efe89-151">High-throughput event and telemetry handling for your instrumentation or IoT scenarios.</span></span>

```XML
<dependency> 
    <groupId>com.microsoft.azure</groupId> 
    <artifactId>azure-eventhubs</artifactId> 
    <version>0.14.4</version> 
</dependency>   
```

<span data-ttu-id="efe89-152">[Ejemplos](https://github.com/Azure/azure-event-hubs/tree/master/samples#java) | [Referencia](/java/api/overview/azure/eventhub) | [GitHub](https://github.com/azure/azure-event-hubs-java)  | [Notas de la versión](https://github.com/Azure/azure-event-hubs-java)</span><span class="sxs-lookup"><span data-stu-id="efe89-152">[Samples](https://github.com/Azure/azure-event-hubs/tree/master/samples#java) | [Reference](/java/api/overview/azure/eventhub) | [GitHub](https://github.com/azure/azure-event-hubs-java)  | [Release Notes](https://github.com/Azure/azure-event-hubs-java)</span></span>

<a name="iotservice"></a> 

### <a name="iot-serviceazureiot-hub"></a>[<span data-ttu-id="efe89-153">Servicio IoT</span><span class="sxs-lookup"><span data-stu-id="efe89-153">IoT Service</span></span>](/azure/iot-hub/)

<span data-ttu-id="efe89-154">Administración de identidades, envío de mensajes y obtención de información de los dispositivos registrados en su IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="efe89-154">Manage identities, send messages, and get feedback from devices registered with your IoT hub.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure.sdk.iot</groupId>
    <artifactId>iot-service-client</artifactId>
    <version>1.7.23</version>
</dependency>
```   
   
<span data-ttu-id="efe89-155">[Ejemplos](https://github.com/Azure/azure-iot-sdk-java/tree/master/service/iot-service-samples) | [Referencia](/java/api/overview/azure/iot) | [GitHub](https://github.com/Azure/azure-iot-sdk-java) | [Notas de la versión](https://github.com/Azure/azure-iot-sdk-java/blob/master/readme.md)</span><span class="sxs-lookup"><span data-stu-id="efe89-155">[Samples](https://github.com/Azure/azure-iot-sdk-java/tree/master/service/iot-service-samples) | [Reference](/java/api/overview/azure/iot) | [GitHub](https://github.com/Azure/azure-iot-sdk-java) | [Release Notes](https://github.com/Azure/azure-iot-sdk-java/blob/master/readme.md)</span></span>

<a name="iotdevice"></a> 

### <a name="iot-deviceazureiot-hubiot-hub-devguide"></a>[<span data-ttu-id="efe89-156">Dispositivo IoT</span><span class="sxs-lookup"><span data-stu-id="efe89-156">IoT Device</span></span>](/azure/iot-hub/iot-hub-devguide)

<span data-ttu-id="efe89-157">Envío de mensajes a un IoT Hub desde el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="efe89-157">Send a message to an IoT hub from your device.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure.sdk.iot</groupId>
    <artifactId>iot-device-client</artifactId>
    <version>1.3.32</version>
</dependency>
```  

<span data-ttu-id="efe89-158">[Ejemplos](https://github.com/Azure/azure-iot-sdk-java/tree/master/device/iot-device-samples) | [Referencia](/java/api/overview/azure/iot) | [GitHub](https://github.com/Azure/azure-iot-sdk-java) | [Notas de la versión](https://github.com/Azure/azure-iot-sdk-java/blob/master/readme.md)</span><span class="sxs-lookup"><span data-stu-id="efe89-158">[Samples](https://github.com/Azure/azure-iot-sdk-java/tree/master/device/iot-device-samples) | [Reference](/java/api/overview/azure/iot) | [GitHub](https://github.com/Azure/azure-iot-sdk-java) | [Release Notes](https://github.com/Azure/azure-iot-sdk-java/blob/master/readme.md)</span></span>

<a name="datalake"></a> 

### <a name="data-lake-storeazuredata-lake-storedata-lake-store-overview"></a>[<span data-ttu-id="efe89-159">Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="efe89-159">Data Lake Store</span></span>](/azure/data-lake-store/data-lake-store-overview)   
   
<span data-ttu-id="efe89-160">Captura de datos de cualquier tamaño y forma en una única ubicación para realizar análisis.</span><span class="sxs-lookup"><span data-stu-id="efe89-160">Capture data of any size and shape into a single location for performing analytics.</span></span>    

```XML
<dependency>
   <groupId>com.microsoft.azure</groupId>
   <artifactId>azure-data-lake-store-sdk</artifactId>
   <version>2.1.5</version>
</dependency>
```   

<span data-ttu-id="efe89-161">[Ejemplos](https://github.com/Azure-Samples/data-lake-store-java-upload-download-get-started) | [Referencia](/java/api/overview/azure/datalakestore) | [GitHub](https://github.com/Azure/azure-data-lake-store-java) | [Notas de la versión](https://github.com/Azure/azure-data-lake-store-java/blob/master/CHANGES.md)</span><span class="sxs-lookup"><span data-stu-id="efe89-161">[Samples](https://github.com/Azure-Samples/data-lake-store-java-upload-download-get-started) | [Reference](/java/api/overview/azure/datalakestore) | [GitHub](https://github.com/Azure/azure-data-lake-store-java) | [Release Notes](https://github.com/Azure/azure-data-lake-store-java/blob/master/CHANGES.md)</span></span>

<a name="appinsights"></a> 

### <a name="appinsightsazureapplication-insightsapp-insights-overview"></a>[<span data-ttu-id="efe89-162">AppInsights</span><span class="sxs-lookup"><span data-stu-id="efe89-162">AppInsights</span></span>](/azure/application-insights/app-insights-overview)

<span data-ttu-id="efe89-163">Seguimiento de uso, incorporación de telemetría y supervisión de aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="efe89-163">Track usage, add telemetry, and monitor your web apps.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>applicationinsights-web</artifactId>
    <version>1.0.8</version>
</dependency>
```

<span data-ttu-id="efe89-164">[Ejemplos](/azure/application-insights/app-insights-java-get-started) | [Referencia](/java/api/overview/azure/appinsights) | [GitHub](https://github.com/Microsoft/ApplicationInsights-Java) | [Notas de la versión](https://github.com/Microsoft/ApplicationInsights-Java#to-upgrade-to-the-latest-sdk)</span><span class="sxs-lookup"><span data-stu-id="efe89-164">[Samples](/azure/application-insights/app-insights-java-get-started) | [Reference](/java/api/overview/azure/appinsights) | [GitHub](https://github.com/Microsoft/ApplicationInsights-Java) | [Release Notes](https://github.com/Microsoft/ApplicationInsights-Java#to-upgrade-to-the-latest-sdk)</span></span>

<a name="batch"></a>

### <a name="batchazurebatch"></a>[<span data-ttu-id="efe89-165">Batch</span><span class="sxs-lookup"><span data-stu-id="efe89-165">Batch</span></span>](/azure/batch)

<span data-ttu-id="efe89-166">Ejecución de aplicaciones en paralelo a gran escala y de informática de alto rendimiento de manera eficaz en la nube.</span><span class="sxs-lookup"><span data-stu-id="efe89-166">Run large-scale parallel and high-performance computing applications efficiently in the cloud.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-batch</artifactId>
    <version>2.0.0</version>
</dependency>
```

<span data-ttu-id="efe89-167">[Ejemplos](https://github.com/azure/azure-batch-samples) | [Referencia](/java/api/overview/azure/batch) | [GitHub](https://github.com/azure/azure-batch-sdk-for-java) | [Notas de la versión](https://github.com/Azure/azure-batch-sdk-for-java/blob/master/README.md)</span><span class="sxs-lookup"><span data-stu-id="efe89-167">[Samples](https://github.com/azure/azure-batch-samples) | [Reference](/java/api/overview/azure/batch) | [GitHub](https://github.com/azure/azure-batch-sdk-for-java) | [Release Notes](https://github.com/Azure/azure-batch-sdk-for-java/blob/master/README.md)</span></span>

<a name="management"></a> 

## <a name="manage-azure-resources"></a><span data-ttu-id="efe89-168">Administración de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="efe89-168">Manage Azure resources</span></span>

<span data-ttu-id="efe89-169">Cree, actualice y elimine recursos de Azure desde el código de aplicación.</span><span class="sxs-lookup"><span data-stu-id="efe89-169">Create, update, and delete Azure resources from your application code.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure</artifactId>
    <version>1.3.0</version>
</dependency>
```

<span data-ttu-id="efe89-170">[Ejemplos](https://github.com/Azure/azure-sdk-for-java#sample-code) | [Referencia](https://docs.microsoft.com/java/api/overview/azure/) | [GitHub](https://github.com/Azure/azure-sdk-for-java) | [Notas de la versión](java-sdk-azure-release-notes.md)</span><span class="sxs-lookup"><span data-stu-id="efe89-170">[Samples](https://github.com/Azure/azure-sdk-for-java#sample-code) | [Reference](https://docs.microsoft.com/java/api/overview/azure/) | [GitHub](https://github.com/Azure/azure-sdk-for-java) | [Release Notes](java-sdk-azure-release-notes.md)</span></span>

<a name="servicebus"></a>

### <a name="servicebushttpsdocsmicrosoftcomazureservice-bus-messagingservice-bus-messaging-overview"></a>[<span data-ttu-id="efe89-171">Service Bus</span><span class="sxs-lookup"><span data-stu-id="efe89-171">ServiceBus</span></span>](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-messaging-overview) 
   
<span data-ttu-id="efe89-172">Service Bus es un servicio de plataforma de mensajería transaccional de clase empresarial.</span><span class="sxs-lookup"><span data-stu-id="efe89-172">Service Bus is an enterprise-class, transactional messaging platform service.</span></span>

```XML
<dependency> 
    <groupId>com.microsoft.azure</groupId> 
    <artifactId>azure-servicebus</artifactId> 
    <version>1.0.0</version> 
</dependency>   
```

<span data-ttu-id="efe89-173">[Ejemplos](https://github.com/Azure/azure-service-bus/tree/master/samples/Java) | [Referencia](https://docs.microsoft.com/java/api/overview/azure/servicebus) | [GitHub](https://github.com/azure/azure-service-bus-java)  | [Notas de la versión](https://github.com/Azure/azure-service-bus-java)</span><span class="sxs-lookup"><span data-stu-id="efe89-173">[Samples](https://github.com/Azure/azure-service-bus/tree/master/samples/Java) | [Reference](https://docs.microsoft.com/java/api/overview/azure/servicebus) | [GitHub](https://github.com/azure/azure-service-bus-java)  | [Release Notes](https://github.com/Azure/azure-service-bus-java)</span></span>

