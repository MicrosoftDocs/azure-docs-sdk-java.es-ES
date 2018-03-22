---
title: Bibliotecas de Azure Event Hub para Java
description: Documentación de referencia de las bibliotecas de Azure Event Hub para Java
keywords: Azure, Java, SDK, API, event hub, IoT, procesamiento de flujo
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 06/21/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: event-hub
ms.openlocfilehash: 076906ff3cafcb4eba97b0a022e5214d7834517c
ms.sourcegitcommit: 02b70b9f5d34415c337601f0b818f7e0985fd884
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/22/2018
---
# <a name="azure-event-hub-libraries-for-java"></a><span data-ttu-id="2257d-104">Bibliotecas de Azure Event Hub para Java</span><span class="sxs-lookup"><span data-stu-id="2257d-104">Azure Event Hub libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="2257d-105">Información general</span><span class="sxs-lookup"><span data-stu-id="2257d-105">Overview</span></span>

<span data-ttu-id="2257d-106">Recopile y administre millones de eventos por segundo de dispositivos y aplicaciones de IoT conectados con [Azure Event Hubs](/azure/event-hubs/event-hubs-what-is-event-hubs).</span><span class="sxs-lookup"><span data-stu-id="2257d-106">Collect and manage millions of events per second from connected IoT devices and applications with [Azure Event Hubs](/azure/event-hubs/event-hubs-what-is-event-hubs).</span></span>

<span data-ttu-id="2257d-107">Para empezar a trabajar con Azure Event Hubs, consulte [Recibir eventos desde Azure Event Hubs con Java](/azure/event-hubs/event-hubs-java-get-started-receive-eph).</span><span class="sxs-lookup"><span data-stu-id="2257d-107">To get started with Azure Event Hubs, see [Receive events from Azure Event Hubs using Java](/azure/event-hubs/event-hubs-java-get-started-receive-eph).</span></span>


## <a name="client-library"></a><span data-ttu-id="2257d-108">Biblioteca de cliente</span><span class="sxs-lookup"><span data-stu-id="2257d-108">Client library</span></span>

<span data-ttu-id="2257d-109">Envíe eventos a una instancia de Azure Event Hub y utilice y procese los eventos de un centro de eventos mediante la biblioteca de cliente de Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="2257d-109">Send events to an Azure Event Hub and consume and process events from an Event Hub using the Event Hubs client library.</span></span>

<span data-ttu-id="2257d-110">[Agregue una dependencia](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) al archivo `pom.xml` de Maven para utilizar la biblioteca de cliente en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="2257d-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-eventhubs</artifactId>
    <version>0.14.3</version>
</dependency>
```   

## <a name="example"></a><span data-ttu-id="2257d-111">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="2257d-111">Example</span></span>

<span data-ttu-id="2257d-112">Envíe un evento a un centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="2257d-112">Send an event to an event hub.</span></span>

```java
ConnectionStringBuilder connStr = new ConnectionStringBuilder(namespaceName, eventHubName,sasKeyName, sasKey);

byte[] payloadBytes = "Test AMQP message from JMS".getBytes("UTF-8");
EventData sendEvent = new EventData(payloadBytes);
EventHubClient ehClient = EventHubClient.createFromConnectionStringSync(connStr.toString());
ehClient.sendSync(sendEvent);
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="2257d-113">Explorar las API de cliente</span><span class="sxs-lookup"><span data-stu-id="2257d-113">Explore the Client APIs</span></span>](/java/api/overview/azure/eventhub/client)


## <a name="samples"></a><span data-ttu-id="2257d-114">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="2257d-114">Samples</span></span>

<span data-ttu-id="2257d-115">[Escritura en Event Hubs mediante JMS y lectura desde Apache Storm][1]
[Lectura y escritura de Event Hubs mediante una topología de .NET y Java híbrida][2]</span><span class="sxs-lookup"><span data-stu-id="2257d-115">[Write to Event Hub via JMS and read from Apache Storm][1]
[Read and write from EventHubs using a hybrid .NET/Java topology][2]</span></span> 

[1]: https://github.com/Azure-Samples/event-hubs-java-storm-sender-jms-receiver
[2]: https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub

<span data-ttu-id="2257d-116">Vea más [código de Java de ejemplo para Azure Event Hubs](https://azure.microsoft.com/resources/samples/?platform=java&term=event) que puede usar en sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="2257d-116">Explore more [sample Java code for Azure Event Hubs](https://azure.microsoft.com/resources/samples/?platform=java&term=event) you can use in your apps.</span></span>

