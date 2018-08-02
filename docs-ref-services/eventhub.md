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
ms.openlocfilehash: b6646ef27edace4247090e749c9a52cd6a33a82c
ms.sourcegitcommit: 3d3460289ab6b9165c2cf6a3dd56eafd0692501e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/17/2018
ms.locfileid: "34283029"
---
# <a name="azure-event-hub-libraries-for-java"></a>Bibliotecas de Azure Event Hub para Java

## <a name="overview"></a>Información general

Recopile y administre millones de eventos por segundo de dispositivos y aplicaciones de IoT conectados con [Azure Event Hubs](/azure/event-hubs/event-hubs-what-is-event-hubs).

Para empezar a trabajar con Azure Event Hubs, consulte [Recibir eventos desde Azure Event Hubs con Java](/azure/event-hubs/event-hubs-java-get-started-receive-eph).


## <a name="client-library"></a>Biblioteca de cliente

Envíe eventos a una instancia de Azure Event Hub y utilice y procese los eventos de un centro de eventos mediante la biblioteca de cliente de Event Hubs.

[Agregue una dependencia](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) al archivo `pom.xml` de Maven para utilizar la [biblioteca de cliente](https://mvnrepository.com/artifact/com.microsoft.azure/azure-eventhubs) en el proyecto.
 

## <a name="example"></a>Ejemplo

Envíe un evento a un centro de eventos.

```java
final ConnectionStringBuilder connStr = new ConnectionStringBuilder()
                                            .setNamespaceName(namespaceName)
                                            .setEventHubName(eventHubName)
                                            .setSasKeyName(sasKeyName)
                                            .setSasKey(sasKey);
final EventHubClient ehClient = EventHubClient.createSync(connStr.toString());

final byte[] payloadBytes = "Test AMQP message".getBytes("UTF-8");
final EventData sendEvent = new EventData(payloadBytes);

ehClient.sendSync(sendEvent);
```


> [!div class="nextstepaction"]
> [Explorar las API de cliente](/java/api/overview/azure/eventhubs/client)



## <a name="samples"></a>Ejemplos

[Uso de ejemplos para explorar las API del plano de datos de Event Hubs][1]

[Escritura en Event Hubs mediante JMS y lectura desde Apache Storm][2]

[Lectura y escritura desde Event Hubs mediante una topología híbrida de .NET y Java][3] 

[1]: https://github.com/Azure/azure-event-hubs/tree/master/samples/Java
[2]: https://github.com/Azure-Samples/event-hubs-java-storm-sender-jms-receiver
[3]: https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub

Vea más [código de Java de ejemplo para Azure Event Hubs](https://azure.microsoft.com/resources/samples/?platform=java&term=event) que puede usar en sus aplicaciones.

