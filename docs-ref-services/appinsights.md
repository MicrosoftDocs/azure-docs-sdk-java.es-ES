---
title: Bibliotecas de Azure Application Insights para Java
description: Documentación de referencia de la API de administración de Java para Azure Appplication Insights
keywords: Azure, Java, SDK, API, AppInsights, telemetría, diagnóstico, seguimiento, registros, rendimiento
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/21/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: appinsights
ms.openlocfilehash: d881ff66ad806e13f7d2cbafff6ce85c23240304
ms.sourcegitcommit: 49b17bbf34732512f836ee634818f1058147ff5c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
ms.locfileid: "31823768"
---
# <a name="azure-application-insights-libraries-for-java"></a>Bibliotecas de Azure Application Insights para Java

## <a name="overview"></a>Información general

Detecte, evalúe y diagnostique problemas en los servicio y las aplicaciones con [Application Insights](/azure/application-insights/app-insights-overview).

Para empezar a trabajar con Application Insights, consulte [Introducción a Application Insights en un proyecto web de Java](/azure/application-insights/app-insights-java-get-started).

## <a name="client-library"></a>Biblioteca de cliente

Agregue telemetría para el seguimiento de eventos, excepciones y métricas de usuario en sus aplicaciones con la biblioteca de cliente de Application Insights.

[Agregue una dependencia](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) al archivo `pom.xml` de Maven para utilizar la biblioteca de cliente en el proyecto.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>applicationinsights-web</artifactId>   
    <version>1.0.8</version>
</dependency>
```   

### <a name="example"></a>Ejemplo

Cree una nueva entrada de métrica y registre un valor para la misma.

```java
    MetricTelemetry sample = new MetricTelemetry();
    sample.setName("metric name");
    sample.setValue(42.3);
    telemetryClient.TrackMetric(sample);
```

> [!div class="nextstepaction"]
> [Explorar las API de cliente](/java/api/overview/azure/appinsights/client)

## <a name="samples"></a>Ejemplos

Vea más [código de Java de ejemplo para Application Insights](https://azure.microsoft.com/en-us/resources/samples/?term=insights&platform=java) que puede usar en sus aplicaciones.
