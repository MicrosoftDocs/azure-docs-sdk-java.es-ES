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
---
# <a name="azure-application-insights-libraries-for-java"></a><span data-ttu-id="8ab8b-104">Bibliotecas de Azure Application Insights para Java</span><span class="sxs-lookup"><span data-stu-id="8ab8b-104">Azure Application Insights libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="8ab8b-105">Información general</span><span class="sxs-lookup"><span data-stu-id="8ab8b-105">Overview</span></span>

<span data-ttu-id="8ab8b-106">Detecte, evalúe y diagnostique problemas en los servicio y las aplicaciones con [Application Insights](/azure/application-insights/app-insights-overview).</span><span class="sxs-lookup"><span data-stu-id="8ab8b-106">Detect, triage, and diagnose issues in your web apps and services with [Application Insights](/azure/application-insights/app-insights-overview).</span></span>

<span data-ttu-id="8ab8b-107">Para empezar a trabajar con Application Insights, consulte [Introducción a Application Insights en un proyecto web de Java](/azure/application-insights/app-insights-java-get-started).</span><span class="sxs-lookup"><span data-stu-id="8ab8b-107">To get started with Application Insights, see [Get started with Application Insights in a Java web project](/azure/application-insights/app-insights-java-get-started).</span></span>

## <a name="client-library"></a><span data-ttu-id="8ab8b-108">Biblioteca de cliente</span><span class="sxs-lookup"><span data-stu-id="8ab8b-108">Client library</span></span>

<span data-ttu-id="8ab8b-109">Agregue telemetría para el seguimiento de eventos, excepciones y métricas de usuario en sus aplicaciones con la biblioteca de cliente de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="8ab8b-109">Add telemetry to track events, exceptions, and user metrics in your apps with the Application Insights client library.</span></span>

<span data-ttu-id="8ab8b-110">[Agregue una dependencia](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) al archivo `pom.xml` de Maven para utilizar la biblioteca de cliente en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="8ab8b-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>applicationinsights-web</artifactId>   
    <version>1.0.8</version>
</dependency>
```   

### <a name="example"></a><span data-ttu-id="8ab8b-111">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="8ab8b-111">Example</span></span>

<span data-ttu-id="8ab8b-112">Cree una nueva entrada de métrica y registre un valor para la misma.</span><span class="sxs-lookup"><span data-stu-id="8ab8b-112">Create a new metric entry and record a value for it.</span></span>

```java
    MetricTelemetry sample = new MetricTelemetry();
    sample.setName("metric name");
    sample.setValue(42.3);
    telemetryClient.TrackMetric(sample);
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="8ab8b-113">Explorar las API de cliente</span><span class="sxs-lookup"><span data-stu-id="8ab8b-113">Explore the Client APIs</span></span>](/java/api/overview/azure/appinsights/client)

## <a name="samples"></a><span data-ttu-id="8ab8b-114">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="8ab8b-114">Samples</span></span>

<span data-ttu-id="8ab8b-115">Vea más [código de Java de ejemplo para Application Insights](https://azure.microsoft.com/en-us/resources/samples/?term=insights&platform=java) que puede usar en sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="8ab8b-115">Explore more [sample Java code for Application Insights](https://azure.microsoft.com/en-us/resources/samples/?term=insights&platform=java) you can use in your apps.</span></span>
