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
# <a name="azure-event-grid-libraries-for-java"></a><span data-ttu-id="ee6b3-104">Bibliotecas de Azure Event Grid para Java</span><span class="sxs-lookup"><span data-stu-id="ee6b3-104">Azure Event Grid libraries for Java</span></span>

<span data-ttu-id="ee6b3-105">Cree aplicaciones orientadas a eventos que escuchen y reaccionen a los eventos de los servicios de Azure y orígenes personalizados mediante un control de eventos simple basado en HTTP con Azure Event Grid.</span><span class="sxs-lookup"><span data-stu-id="ee6b3-105">Build event-driven applications that listen and react to events from Azure services and custom sources using simple HTTP-based event handling with Azure Event Grid.</span></span>

<span data-ttu-id="ee6b3-106">[Para más información](/azure/event-grid/overview) acerca de Azure Event Grid y empezar a trabajar con el [tutorial de eventos de Azure Blob Storage](/azure/storage/blobs/storage-blob-event-quickstart).</span><span class="sxs-lookup"><span data-stu-id="ee6b3-106">[Learn more](/azure/event-grid/overview) about Azure Event Grid and get started with the [Azure Blob storage event tutorial](/azure/storage/blobs/storage-blob-event-quickstart).</span></span> 

## <a name="client-sdk"></a><span data-ttu-id="ee6b3-107">Client SDK</span><span class="sxs-lookup"><span data-stu-id="ee6b3-107">Client SDK</span></span>

<span data-ttu-id="ee6b3-108">Puede crear eventos, autenticar y enviar a temas con Client SDK de Azure Event Grid.</span><span class="sxs-lookup"><span data-stu-id="ee6b3-108">Create events, authenticate, and post to topics using the Azure Event Grid Client SDK.</span></span>

<span data-ttu-id="ee6b3-109">[Agregue una dependencia](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) al archivo `pom.xml` de Maven para utilizar la biblioteca de cliente en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="ee6b3-109">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-eventgrid</artifactId>
    <version>1.2.0</version>
</dependency>
```   

### <a name="publish-events"></a><span data-ttu-id="ee6b3-110">Publicación de eventos</span><span class="sxs-lookup"><span data-stu-id="ee6b3-110">Publish events</span></span>

<span data-ttu-id="ee6b3-111">El código siguiente se autentica con Azure y publica una `List` de eventos `EventGridEvent` de un tipo personalizado (en este ejemplo, `Contoso.Items.ItemsReceived`) en un tema.</span><span class="sxs-lookup"><span data-stu-id="ee6b3-111">The following code authenticates with Azure and publishes a `List` of  `EventGridEvent` events of a custom type (in this example, `Contoso.Items.ItemsReceived` ) to a topic.</span></span> <span data-ttu-id="ee6b3-112">La clave del tema y la dirección del punto de conexión utilizadas en el ejemplo se pueden recuperar en la CLI de Azure:</span><span class="sxs-lookup"><span data-stu-id="ee6b3-112">The topic key and endpoint address used in the sample can be retrieved from the Azure CLI:</span></span>

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
> [<span data-ttu-id="ee6b3-113">Explorar las API de cliente de Event Grid</span><span class="sxs-lookup"><span data-stu-id="ee6b3-113">Explore the Event Grid Client APIs</span></span>](/java/api/overview/azure/eventgrid/client)

## <a name="management-sdk"></a><span data-ttu-id="ee6b3-114">SDK de administración</span><span class="sxs-lookup"><span data-stu-id="ee6b3-114">Management SDK</span></span>

<span data-ttu-id="ee6b3-115">El SDK de administración de Event Grid permite crear, actualizar y eliminar instancias, temas y suscripciones de Event Grid.</span><span class="sxs-lookup"><span data-stu-id="ee6b3-115">Create, update, or delete Event Grid instances, topics, and subscriptions with the Event Grid management SDK.</span></span>

<span data-ttu-id="ee6b3-116">[Agregue una dependencia](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) al archivo `pom.xml` de Maven para utilizar la biblioteca de cliente en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="ee6b3-116">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure</artifactId>
    <version>1.16.0</version>
</dependency>
```   

<span data-ttu-id="ee6b3-117">En el ejemplo siguiente se crea una suscripción de Event Grid, que se toma del [ejemplo de EventGrid para Java](https://github.com/Azure-Samples/event-grid-java-publish-consume-events)</span><span class="sxs-lookup"><span data-stu-id="ee6b3-117">The following example creates an Event Grid subscription, taken from the [EventGrid Java samples](https://github.com/Azure-Samples/event-grid-java-publish-consume-events)</span></span>

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
> [<span data-ttu-id="ee6b3-118">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="ee6b3-118">Explore the management APIs</span></span>](/java/api/overview/azure/eventgrid/management)