---
title: Bibliotecas de Azure Event Grid para Java
description: Documentación de referencia de las bibliotecas de Azure Event Grid para Java
keywords: Azure, Java, SDK, API, cuadrícula de eventos, mensajería, basado en eventos
author: rloutlaw
ms.author: routlaw
manager: angerobe
ms.date: 07/11/2017
ms.topic: managed-reference
ms.devlang: java
ms.service: event-grid
ms.openlocfilehash: 35acbdeede2fbc541128029ad43f149209a057c4
ms.sourcegitcommit: db36eeb667a0bfe6d113953bb0583240db61b0f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/26/2018
ms.locfileid: "50134637"
---
# <a name="azure-event-grid-libraries-for-java"></a>Bibliotecas de Azure Event Grid para Java

Cree aplicaciones orientadas a eventos que escuchen y reaccionen a los eventos de los servicios de Azure y orígenes personalizados mediante un control de eventos simple basado en HTTP con Azure Event Grid.

[Para más información](/azure/event-grid/overview) acerca de Azure Event Grid y empezar a trabajar con el [tutorial de eventos de Azure Blob Storage](/azure/storage/blobs/storage-blob-event-quickstart). 

## <a name="client-sdk"></a>Client SDK

Puede crear eventos, autenticar y enviar a temas con Client SDK de Azure Event Grid.

[Agregue una dependencia](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) al archivo `pom.xml` de Maven para utilizar la biblioteca de cliente en el proyecto.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-eventgrid</artifactId>
    <version>1.2.0</version>
</dependency>
```   

### <a name="publish-events"></a>Publicación de eventos

El código siguiente se autentica con Azure y publica una `List` de eventos `EventGridEvent` de un tipo personalizado (en este ejemplo, `Contoso.Items.ItemsReceived`) en un tema. La clave del tema y la dirección del punto de conexión utilizadas en el ejemplo se pueden recuperar en la CLI de Azure:

```azurecli-interactive
az eventgrid topic show -g gridResourceGroup -n topicName
az eventgrid topic key list -g gridResourceGroup -n topicName
```

```java
// Create an event grid client.
TopicCredentials topicCredentials = new TopicCredentials(System.getenv("EVENTGRID_TOPIC_KEY"));
EventGridClient client = new EventGridClientImpl(topicCredentials);

// Publish custom events to the EventGrid.
System.out.println("Publish custom events to the EventGrid");
List<EventGridEvent> eventsList = new ArrayList<>();
for (int i = 0; i < 5; i++) {
    eventsList.add(new EventGridEvent(
        UUID.randomUUID().toString(),
        String.format("Door%d", i),
        new ContosoItemReceivedEventData("Contoso Item SKU #1"),
        "Contoso.Items.ItemReceived",
        DateTime.now(),
        "2.0"
    ));
}

String eventGridEndpoint = String.format("https://%s/", new URI(System.getenv("EVENTGRID_TOPIC_ENDPOINT")).getHost());

client.publishEvents(eventGridEndpoint, eventsList);
```

> [!div class="nextstepaction"]
> [Explorar las API de cliente de Event Grid](/java/api/overview/azure/eventgrid/client)

## <a name="management-sdk"></a>SDK de administración

El SDK de administración de Event Grid permite crear, actualizar y eliminar instancias, temas y suscripciones de Event Grid.

[Agregue una dependencia](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) al archivo `pom.xml` de Maven para utilizar la biblioteca de cliente en el proyecto.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure</artifactId>
    <version>1.16.0</version>
</dependency>
```   

En el ejemplo siguiente se crea una suscripción de Event Grid, que se toma del [ejemplo de EventGrid para Java](https://github.com/Azure-Samples/event-grid-java-publish-consume-events)

```java
// Create an event grid subscription.
//
System.out.println("Creating an Azure EventGrid Subscription");

EventSubscription eventSubscription = eventGridManager.eventSubscriptions().define(eventSubscriptionName)
    .withScope(eventGridTopic.id())
    .withDestination(new EventHubEventSubscriptionDestination()
        .withResourceId(eventHub.id()))
    .withFilter(new EventSubscriptionFilter()
        .withIsSubjectCaseSensitive(false)
        .withSubjectBeginsWith("")
        .withSubjectEndsWith(""))
    .create();
```

> [!div class="nextstepaction"]
> [Explorar las API de administración](/java/api/overview/azure/eventgrid/management)