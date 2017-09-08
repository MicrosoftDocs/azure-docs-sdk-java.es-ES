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
ms.openlocfilehash: 10073a1b2250a37347128dd9c8faf1375b2ab6ae
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/28/2017
---
# <a name="azure-libraries-for-java"></a>Bibliotecas de Azure para Java

Las bibliotecas de Azure le ayudarán a utilizar los servicios de Azure en aplicaciones Java usando interfaces nativas. Cada biblioteca es independiente y se puede utilizar por separado.

| | | | |
|:-------------:|:----------:|:----:|:---:|
| [Azure Storage](#azure-storage) | [SQL Database](#sql-database)  | [Redis Cache](#redis-cache)   | [DocumentDB](#documentdb) |
| [Bus de servicio](#servicebus)  | [Azure Active Directory](#azuread) | [Key Vault](#keyvault)  | [Event Hubs](#eventhub)
| [Servicio IoT](#iotservice) | [Dispositivo de IoT](#iotdevice) | [Data Lake](#datalake)  | [AppInsights](#appinsights) | 
| [Batch](#batch) | [Administración de recursos de Azure](#management) |

## <a name="install-with-maven"></a>Instalación con Maven

Agregue una entrada de dependencia en el archivo `pom.xml` para importar una biblioteca en el proyecto [Maven](https://maven.apache.org).

Por ejemplo, para incluir la versión más reciente de las [bibliotecas de administración de Azure para Java](#management):

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure</artifactId>
    <version>1.1.2</version>
</dependency>
```

Se admiten otras herramientas de compilación de Java como Gradle, pero no se proporcionan los pasos de instalación en este artículo. Revise la documentación de la herramienta de compilación sobre cómo utilizar las importaciones de Maven.

## <a name="azure-service-libraries"></a>Bibliotecas de servicio de Azure

Integre los servicios de Azure para agregar funcionalidad a las aplicaciones con estas bibliotecas. Obtenga más información acerca de cómo crear aplicaciones con servicios de Azure en el [centro para desarrolladores de Java](https://azure.microsoft.com/develop/java).

<a name="azure-storage"></a>

### <a name="azure-storageazurestoragestorage-introduction"></a>[Azure Storage](/azure/storage/storage-introduction)  

Almacenamiento de datos y mensajería para las aplicaciones.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-storage</artifactId>
    <version>5.4.0</version>
</dependency>
```   

[Ejemplos](https://github.com/Azure/azure-storage-java/tree/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage) | [Referencia](/java/api/overview/azure/storage) | [GitHub](https://github.com/Azure/azure-storage-java)  | [Notas de la versión](https://github.com/Azure/azure-storage-java/blob/master/ChangeLog.txt)

<a name="sql-database"></a>

### <a name="sql-databaseazuresql-databasesql-database-technical-overview"></a>[SQL Database](/azure/sql-database/sql-database-technical-overview)

Controlador JDBC para Azure SQL Database.

```XML
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>6.2.1.jre8</version>
</dependency>
```

[Ejemplos](/sql/connect/jdbc/step-3-proof-of-concept-connecting-to-sql-using-java) | [Referencia](/java/api/overview/azure/sql) | [GitHub](https://github.com/Microsoft/mssql-jdbc)  | [Notas de la versión](https://github.com/Microsoft/mssql-jdbc/blob/master/CHANGELOG.md)

<a name="redis-cache"></a>

### <a name="redis-cachehttpsazuremicrosoftcomservicescache"></a>[Redis Cache](https://azure.microsoft.com/services/cache/)

Almacén de pares clave-valor de baja latencia y alto rendimiento.

```XML
<dependency>
    <groupId>redis.clients</groupId>
    <artifactId>jedis</artifactId>
    <version>2.9.0</version>
    <type>jar</type>
    <scope>compile</scope>
</dependency>
```   

[Ejemplos](/azure/redis-cache/cache-java-get-started) | [Referencia](http://xetorthio.github.io/jedis)  | [GitHub](https://github.com/xetorthio/jedis)  | [Notas de la versión](https://github.com/xetorthio/jedis/releases)  

<a name="documentdb"></a>

### <a name="cosmos-dbazuredocumentdbdocumentdb-introduction"></a>[Cosmos DB](/azure/documentdb/documentdb-introduction)

Base de datos NoSQL escalable con documentos JSON y la sintaxis de consulta SQL o JavaScript.   

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-documentdb</artifactId>
    <version>1.12.0</version>
</dependency>
```

[Ejemplos](/azure/documentdb/documentdb-java-application) | [Referencia](http://azure.github.io/azure-documentdb-java/) | [GitHub](https://github.com/Azure/azure-documentdb-java)   | [Notas de la versión](https://github.com/Azure/azure-documentdb-java/blob/master/changelog.md)

<a name="servicebus"></a>
 
 ### <a name="servicebusazureservice-bus-messagingservice-bus-messaging-overview"></a>[Service Bus](/azure/service-bus-messaging/service-bus-messaging-overview) 
    
 Service Bus es un servicio de plataforma de mensajería transaccional de clase empresarial.
 
 ```XML
 <dependency> 
     <groupId>com.microsoft.azure</groupId> 
     <artifactId>azure-servicebus</artifactId> 
     <version>1.0.0</version> 
 </dependency>   
 ```
 
 [Ejemplos](https://github.com/Azure/azure-service-bus/tree/master/samples/Java) | [Referencia](https://docs.microsoft.com/java/api/overview/azure/servicebus) | [GitHub](https://github.com/azure/azure-service-bus-java)  | [Notas de la versión](https://github.com/Azure/azure-service-bus-java)   
  
<a name="azuread"></a>

### <a name="azure-active-directoryazureactive-directoryactive-directory-whatis"></a>[Azure Active Directory](/azure/active-directory/active-directory-whatis)   

Administración de identidades e inicio de sesión seguro para sus aplicaciones.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>adal4j</artifactId>
    <version>1.2.0</version>
</dependency>
```
   
[Ejemplos](https://github.com/Azure-Samples?utf8=%E2%9C%93&q=active%20directory%20&type=&language=java) | [Referencia](/java/api/overview/azure/activedirectory) | [GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-java) | [Notas de la versión](https://github.com/AzureAD/azure-activedirectory-library-for-javaT-)
 
<a name="keyvault"></a>

### <a name="key-vaultazurekey-vault"></a>[Key Vault](/azure/key-vault) 

Acceso seguro a claves y secretos desde las aplicaciones. 

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-keyvault</artifactId>
    <version>1.0.0</version>
</dependency>
```

[Ejemplos](https://github.com/Azure-Samples/key-vault-java-manage-key-vaults) | [Referencia](/java/api/overview/azure/keyvault) | [GitHub](https://github.com/Azure/azure-keyvault-java) | [Notas de la versión](https://github.com/Azure/azure-keyvault-java) 

<a name="eventhub"></a>

### <a name="event-hubazureevent-hubsevent-hubs-what-is-event-hubs"></a>[Event Hubs](/azure/event-hubs/event-hubs-what-is-event-hubs) 
   
Control de eventos y datos de telemetría de alto rendimiento para instrumentación o escenarios de IoT.

```XML
<dependency> 
    <groupId>com.microsoft.azure</groupId> 
    <artifactId>azure-eventhubs</artifactId> 
    <version>0.14.4</version> 
</dependency>   
```

[Ejemplos](https://github.com/Azure/azure-event-hubs/tree/master/samples#java) | [Referencia](/java/api/overview/azure/eventhub) | [GitHub](https://github.com/azure/azure-event-hubs-java)  | [Notas de la versión](https://github.com/Azure/azure-event-hubs-java)

<a name="iotservice"></a> 

### <a name="iot-serviceazureiot-hub"></a>[Servicio IoT](/azure/iot-hub/)

Administración de identidades, envío de mensajes y obtención de información de los dispositivos registrados en su IoT Hub.

```XML
<dependency>
    <groupId>com.microsoft.azure.sdk.iot</groupId>
    <artifactId>iot-service-client</artifactId>
    <version>1.7.23</version>
</dependency>
```   
   
[Ejemplos](https://github.com/Azure/azure-iot-sdk-java/tree/master/service/iot-service-samples) | [Referencia](/java/api/overview/azure/iot) | [GitHub](https://github.com/Azure/azure-iot-sdk-java) | [Notas de la versión](https://github.com/Azure/azure-iot-sdk-java/blob/master/readme.md)

<a name="iotdevice"></a> 

### <a name="iot-deviceazureiot-hubiot-hub-devguide"></a>[Dispositivo de IoT](/azure/iot-hub/iot-hub-devguide)

Envío de mensajes a un IoT Hub desde el dispositivo.  

```XML
<dependency>
    <groupId>com.microsoft.azure.sdk.iot</groupId>
    <artifactId>iot-device-client</artifactId>
    <version>1.3.32</version>
</dependency>
```  

[Ejemplos](https://github.com/Azure/azure-iot-sdk-java/tree/master/device/iot-device-samples) | [Referencia](/java/api/overview/azure/iot) | [GitHub](https://github.com/Azure/azure-iot-sdk-java) | [Notas de la versión](https://github.com/Azure/azure-iot-sdk-java/blob/master/readme.md)

<a name="datalake"></a> 

### <a name="data-lake-storeazuredata-lake-storedata-lake-store-overview"></a>[Data Lake Store](/azure/data-lake-store/data-lake-store-overview)   
   
Captura de datos de cualquier tamaño y forma en una única ubicación para realizar análisis.    

```XML
<dependency>
   <groupId>com.microsoft.azure</groupId>
   <artifactId>azure-data-lake-store-sdk</artifactId>
   <version>2.1.5</version>
</dependency>
```   

[Ejemplos](https://github.com/Azure-Samples/data-lake-store-java-upload-download-get-started) | [Referencia](/java/api/overview/azure/datalakestore) | [GitHub](https://github.com/Azure/azure-data-lake-store-java) | [Notas de la versión](https://github.com/Azure/azure-data-lake-store-java/blob/master/CHANGES.md)

<a name="appinsights"></a> 

### <a name="appinsightsazureapplication-insightsapp-insights-overview"></a>[AppInsights](/azure/application-insights/app-insights-overview)

Seguimiento de uso, incorporación de telemetría y supervisión de aplicaciones web.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>applicationinsights-web</artifactId>
    <version>1.0.8</version>
</dependency>
```

[Ejemplos](/azure/application-insights/app-insights-java-get-started) | [Referencia](/java/api/overview/azure/appinsights) | [GitHub](https://github.com/Microsoft/ApplicationInsights-Java) | [Notas de la versión](https://github.com/Microsoft/ApplicationInsights-Java#to-upgrade-to-the-latest-sdk)

<a name="batch"></a>

### <a name="batchazurebatch"></a>[Batch](/azure/batch)

Ejecución de aplicaciones en paralelo a gran escala y de informática de alto rendimiento de manera eficaz en la nube.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-batch</artifactId>
    <version>2.0.0</version>
</dependency>
```

[Ejemplos](https://github.com/azure/azure-batch-samples) | [Referencia](/java/api/overview/azure/batch) | [GitHub](https://github.com/azure/azure-batch-sdk-for-java) | [Notas de la versión](https://github.com/Azure/azure-batch-sdk-for-java/blob/master/README.md)

<a name="management"></a> 

## <a name="manage-azure-resources"></a>Administración de recursos de Azure

Cree, actualice y elimine recursos de Azure desde el código de aplicación.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure</artifactId>
    <version>1.1.2</version>
</dependency>
```

[Ejemplos](https://github.com/Azure/azure-sdk-for-java#sample-code) | [Referencia](https://docs.microsoft.com/java/api/overview/azure/) | [GitHub](https://github.com/Azure/azure-sdk-for-java) | [Notas de la versión](java-sdk-azure-release-notes.md)

<a name="servicebus"></a>

### <a name="servicebushttpsdocsmicrosoftcomen-usazureservice-bus-messagingservice-bus-messaging-overview"></a>[Service Bus](https://docs.microsoft.com/en-us/azure/service-bus-messaging/service-bus-messaging-overview) 
   
Service Bus es un servicio de plataforma de mensajería transaccional de clase empresarial.

```XML
<dependency> 
    <groupId>com.microsoft.azure</groupId> 
    <artifactId>azure-servicebus</artifactId> 
    <version>1.0.0</version> 
</dependency>   
```

[Ejemplos](https://github.com/Azure/azure-service-bus/tree/master/samples/Java) | [Referencia](https://docs.microsoft.com/java/api/overview/azure/servicebus) | [GitHub](https://github.com/azure/azure-service-bus-java)  | [Notas de la versión](https://github.com/Azure/azure-service-bus-java)

