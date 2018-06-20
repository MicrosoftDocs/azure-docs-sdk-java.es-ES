---
title: Bibliotecas de Azure Data Lake Analytics para Java
description: Documentación de referencia de las bibliotecas de Data Lake Analytics para Java
keywords: Azure, Java, SDK, API, macrodatos, data lake
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 06/21/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: data-lake-store
ms.openlocfilehash: c14c89f961951d114362adee4fec6239e78cffb3
ms.sourcegitcommit: 49b17bbf34732512f836ee634818f1058147ff5c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
ms.locfileid: "31823778"
---
# <a name="azure-data-lake-analytics-libraries-for-java"></a>Bibliotecas de Azure Data Lake Analytics para Java

## <a name="overview"></a>Información general

Ejecute trabajos de análisis de macrodatos con capacidad de escalado a conjuntos de datos masivos con [Azure Data Lake Analytics](/azure/data-lake-analytics/data-lake-analytics-overview).

Para empezar a usar Azure Data Lake Analytics, consulte [Introducción a Azure Data Lake Analytics con el SDK de Java](/azure/data-lake-analytics/data-lake-analytics-get-started-java-sdk).

## <a name="management-api"></a>API de administración

Use la API de administración para administrar cuentas, trabajos, directivas y catálogos de Data Lake Analytics.

[Agregue una dependencia](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) al archivo `pom.xml` de Maven para utilizar la API de administración en el proyecto.


```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-datalake-analytics</artifactId>
    <version>1.0.0-beta1.3</version>
</dependency>
```

## <a name="example"></a>Ejemplo

Envíe un nuevo trabajo de U-SQL a Data Lake Analytics.

```java
// authenticate with service principal credentials
ApplicationTokenCredentials creds = new ApplicationTokenCredentials(_clientId, _tenantId, _clientSecret, null);
DataLakeAnalyticsJobManagementClient adlaJobClient = new DataLakeAnalyticsJobManagementClientImpl(creds);

// set up job parameters
UUID jobId = java.util.UUID.randomUUID();
USqlJobProperties properties = new USqlJobProperties();
properties.setScript("@input =  EXTRACT Data string FROM \"/input1.csv\" USING Extractors.Csv(); OUTPUT @input TO @\"/output1.csv\" USING Outputters.Csv();");
JobInformation parameters = new JobInformation();
parameters.setName("testJob");
parameters.setJobId(jobId);
parameters.setType(JobType.USQL);
parameters.setProperties(properties);

// create the job
JobInformation jobInfo = adlaJobClient.getJobOperations().create(accountName, jobId, parameters).getBody();

```

> [!div class="nextstepaction"]
> [Explorar las API de administración](/java/api/overview/azure/datalakeanalytics/management)

## <a name="samples"></a>Ejemplos

[Azure Data Lake Analytics con el SDK de Java][1] 

[1]: https://docs.microsoft.com/azure/data-lake-analytics/data-lake-analytics-get-started-java-sdk

Consulte la [lista completa](https://azure.microsoft.com/resources/samples/?platform=java&term=analytics) de ejemplos de Azure Data Lake Analytics.
