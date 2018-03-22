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
# <a name="azure-event-hub-libraries-for-java"></a>Bibliotecas de Azure Event Hub para Java

## <a name="overview"></a>Información general

Recopile y administre millones de eventos por segundo de dispositivos y aplicaciones de IoT conectados con [Azure Event Hubs](/azure/event-hubs/event-hubs-what-is-event-hubs).

Para empezar a trabajar con Azure Event Hubs, consulte [Recibir eventos desde Azure Event Hubs con Java](/azure/event-hubs/event-hubs-java-get-started-receive-eph).


## <a name="client-library"></a>Biblioteca de cliente

Envíe eventos a una instancia de Azure Event Hub y utilice y procese los eventos de un centro de eventos mediante la biblioteca de cliente de Event Hubs.

[Agregue una dependencia](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) al archivo `pom.xml` de Maven para utilizar la biblioteca de cliente en el proyecto.  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-eventhubs</artifactId>
    <version>0.14.3</version>
</dependency>
```   

## <a name="example"></a>Ejemplo

Envíe un evento a un centro de eventos.

```java
ConnectionStringBuilder connStr = new ConnectionStringBuilder(namespaceName, eventHubName,sasKeyName, sasKey);

byte[] payloadBytes = "Test AMQP message from JMS".getBytes("UTF-8");
EventData sendEvent = new EventData(payloadBytes);
EventHubClient ehClient = EventHubClient.createFromConnectionStringSync(connStr.toString());
ehClient.sendSync(sendEvent);
```

> [!div class="nextstepaction"]
> [Explorar las API de cliente](/java/api/overview/azure/eventhub/client)


## <a name="samples"></a>Ejemplos

[Escritura en Event Hubs mediante JMS y lectura desde Apache Storm][1]
[Lectura y escritura de Event Hubs mediante una topología de .NET y Java híbrida][2] 

[1]: https://github.com/Azure-Samples/event-hubs-java-storm-sender-jms-receiver
[2]: https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub

Vea más [código de Java de ejemplo para Azure Event Hubs](https://azure.microsoft.com/resources/samples/?platform=java&term=event) que puede usar en sus aplicaciones.

