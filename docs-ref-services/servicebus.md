---
title: Bibliotecas de Service Bus para Java
description: "Documentación de referencia del cliente Java y las bibliotecas de administración de Service Bus para Java"
keywords: "Azure, Java, SDK, API, mensajería, amqp, qpid, JMS, pubsub, pub-sub, agente de mensajes"
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/11/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: service-bus
ms.openlocfilehash: 12b5f218008c208bfa85ef02820c56bbcf0b224a
ms.sourcegitcommit: ae39830d5a54fedceac78d8df1718e77741e03fa
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/09/2017
---
# <a name="service-bus-libraries-for-java"></a><span data-ttu-id="6da95-104">Bibliotecas de Service Bus para Java</span><span class="sxs-lookup"><span data-stu-id="6da95-104">Service Bus libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="6da95-105">Información general</span><span class="sxs-lookup"><span data-stu-id="6da95-105">Overview</span></span>

<span data-ttu-id="6da95-106">Service Bus es un servicio de plataforma de mensajería transaccional de clase empresarial que proporciona colas y temas de publicación y suscripción altamente confiables, con funcionalidades y características como entrega ordenada, sesiones, creación de particiones, programación, suscripciones complejas, flujos de trabajo y administración de transacciones.</span><span class="sxs-lookup"><span data-stu-id="6da95-106">Service Bus is an enterprise-class, transactional messaging platform service that provides highly reliable queues and publish/subscribe topics with deep feature capabilities such as ordered delivery, sessions, partitioning, scheduling, complex subscriptions, as well as workflow and transaction handling.</span></span>

<span data-ttu-id="6da95-107">Las funcionalidades de Service Bus son comparables y, a menudo, superan las de los agentes de mensajes heredados locales de tecnología avanzada.</span><span class="sxs-lookup"><span data-stu-id="6da95-107">The Service Bus feature capabilities are comparable and often exceed those of high-end, on-premises legacy message brokers.</span></span> <span data-ttu-id="6da95-108">Las características de Service Bus están disponibles a través de protocolos basados en estándares como AMQP 1.0 y HTTPS, y todos los movimientos de los protocolos están totalmente documentados, lo que permite una amplia interoperabilidad.</span><span class="sxs-lookup"><span data-stu-id="6da95-108">The Service Bus features are available via standards-based protocols like AMQP 1.0 and HTTPS and all protocol gestures are fully documented, allowing for broad interoperability.</span></span> 

<span data-ttu-id="6da95-109">Centrado en una mensajería duradera altamente disponible y confiable, Service Bus Premium proporciona rendimiento competitivo incluso en implementaciones con importantes centros de datos locales, pero sin procesos de selección y adquisición de hardware, planeamiento y ejecución de la implementación ni sesiones interminables de optimización del rendimiento.</span><span class="sxs-lookup"><span data-stu-id="6da95-109">Focusing on highly available and reliable durable messaging, the Service Bus Premium provides competitive throughput performance even with substantial local datacenter deployments, but without hardware selection and acquisition processes, deployment planning and execution, and endless performance optimization sessions.</span></span> 

<span data-ttu-id="6da95-110">Service Bus Premium es una oferta completamente administrada con capacidad dedicada reservada para cada inquilino, que da como resultado un rendimiento predecible con un modelo de precios simple y orientado a la capacidad con costo general muy inferior al de los agentes comerciales en implementaciones locales.</span><span class="sxs-lookup"><span data-stu-id="6da95-110">Service Bus Premium is a fully managed offering with dedicated capacity reserved for each tenant that yields predictable performance with a simple, capacity-oriented pricing model and at extremely lower overall cost than commercial on-premises brokers.</span></span> <span data-ttu-id="6da95-111">Para muchos clientes, Service Bus Premium puede reemplazar clústeres de mensajería locales dedicados hoy en día, incluso si las cargas de trabajo conectadas no se ejecutan en la nube.</span><span class="sxs-lookup"><span data-stu-id="6da95-111">For many customers, Service Bus Premium can replace dedicated on-premises messaging clusters today, even if the attached workloads do not run in the cloud.</span></span> 

<span data-ttu-id="6da95-112">Puede obtener información sobre los conceptos de Service Bus [en la sección de documentación de mensajería](https://docs.microsoft.com/en-us/azure/service-bus-messaging/)</span><span class="sxs-lookup"><span data-stu-id="6da95-112">Learn more about Service Bus concepts [in the messaging documentation section](https://docs.microsoft.com/en-us/azure/service-bus-messaging/)</span></span> 

<span data-ttu-id="6da95-113">Para desarrolladores de Java, Service Bus proporciona una API nativa compatible con Microsoft y también puede usarse con bibliotecas compatibles con AMQP 1.0, como el proveedor JMS de Apache Qpid Proton.</span><span class="sxs-lookup"><span data-stu-id="6da95-113">For Java developers, Service Bus provides a Microsoft supported native API and Service Bus can also be used with AMQP 1.0 compliant libraries such as Apache Qpid Proton's JMS provider.</span></span>

<span data-ttu-id="6da95-114">El cliente oficial de Service Bus está disponible en [forma de código fuente en GitHub](https://github.com/azure/azure-service-bus-java) y los archivos binarios y fuentes empaquetados [están disponibles en Maven Central](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-servicebus%22).</span><span class="sxs-lookup"><span data-stu-id="6da95-114">The official Service Bus client is available in [source code form on GitHub](https://github.com/azure/azure-service-bus-java) and binaries and packaged sources [are available on Maven Central](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-servicebus%22).</span></span> 


## <a name="client-library"></a><span data-ttu-id="6da95-115">Biblioteca de cliente</span><span class="sxs-lookup"><span data-stu-id="6da95-115">Client library</span></span>


<span data-ttu-id="6da95-116">Agregue una dependencia al archivo `pom.xml` del proyecto de Maven para utilizar la biblioteca en su propio proyecto.</span><span class="sxs-lookup"><span data-stu-id="6da95-116">Add a dependency to your Maven project's `pom.xml` file to use the library in your own project.</span></span> <span data-ttu-id="6da95-117">Especifique la versión según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="6da95-117">Specify the version as desired.</span></span>

<span data-ttu-id="6da95-118">[Agregue una dependencia](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) al archivo `pom.xml` de Maven para utilizar la biblioteca de cliente en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="6da95-118">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>   

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-servicebus</artifactId>
    <version>1.0.0</version>
</dependency>
```

## <a name="examples"></a><span data-ttu-id="6da95-119">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="6da95-119">Examples</span></span>

<span data-ttu-id="6da95-120">El [repositorio de código de ejemplo](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/) contiene ejemplos de mensajes de Service Bus [QueueClient](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/src/com/microsoft/azure/servicebus/samples/BasicSendReceiveWithQueueClient.java) y [TopicClient y SubscriptionClient](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/src/com/microsoft/azure/servicebus/samples/BasicSendReceiveWithTopicSubscriptionClient.java) y [MessageSender y MessageReceiver](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/src/com/microsoft/azure/servicebus/samples/SendReceiveWithMessageSenderReceiver.java).</span><span class="sxs-lookup"><span data-stu-id="6da95-120">The [sample code repository](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/) contains samples for how to [QueueClient](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/src/com/microsoft/azure/servicebus/samples/BasicSendReceiveWithQueueClient.java) and [TopicClient and SubscriptionClient](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/src/com/microsoft/azure/servicebus/samples/BasicSendReceiveWithTopicSubscriptionClient.java) and [MessageSender and MessageReceiver](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/src/com/microsoft/azure/servicebus/samples/SendReceiveWithMessageSenderReceiver.java) messages from Service Bus.</span></span>


```java
public class BasicSendReceiveWithQueueClient {
    // Connection String for the namespace can be obtained from the Azure portal under the
    // 'Shared Access policies' section.
    private static final String connectionString = "{connection string}";
    private static final String queueName = "{queue name}";
    private static IQueueClient queueClient;
    private static int totalSend = 100;
    private static int totalReceived = 0;

    public static void main(String[] args) throws Exception {

        Log.log("Starting BasicSendReceiveWithQueueClient sample");

        // create client
        Log.log("Create queue client.");
        queueClient = new QueueClient(new ConnectionStringBuilder(connectionString, queueName), ReceiveMode.PeekLock);

        // send and receive
        queueClient.registerMessageHandler(new MessageHandler(queueClient), new MessageHandlerOptions(1, false, Duration.ofMinutes(1)));
        for (int i = 0; i < totalSend; i++) {
            int j = i;
            Log.log("Sending message #%d.", j);
            queueClient.sendAsync(new Message("" + i)).thenRunAsync(() -> { Log.log("Sent message #%d.", j);});
        }

        while(totalReceived != totalSend) {
            Thread.sleep(1000);
        }

        Log.log("Received all messages, exiting the sample.");
        Log.log("Closing queue client.");
        queueClient.close();
    }

    static class MessageHandler implements IMessageHandler {
        private IQueueClient client;

        public MessageHandler(IQueueClient client) {
            this.client = client;
        }

        @Override
        public CompletableFuture<Void> onMessageAsync(IMessage iMessage) {
            Log.log("Received message with sq#: %d and lock token: %s.", iMessage.getSequenceNumber(), iMessage.getLockToken());
            return this.client.completeAsync(iMessage.getLockToken()).thenRunAsync(() -> {
                Log.log("Completed message sq#: %d and locktoken: %s", iMessage.getSequenceNumber(), iMessage.getLockToken());
                totalReceived++;
            });
        }

        @Override
        public void notifyException(Throwable throwable, ExceptionPhase exceptionPhase) {
            Log.log(exceptionPhase + "-" + throwable.getMessage());
        }
    }
}
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="6da95-121">Explorar las API de cliente</span><span class="sxs-lookup"><span data-stu-id="6da95-121">Explore the Client APIs</span></span>](/java/api/overview/azure/servicebus/clientlibrary)

## <a name="management-api"></a><span data-ttu-id="6da95-122">API de administración</span><span class="sxs-lookup"><span data-stu-id="6da95-122">Management API</span></span>

<span data-ttu-id="6da95-123">Cree y administre espacios de nombres, temas, colas y suscripciones con la API de administración.</span><span class="sxs-lookup"><span data-stu-id="6da95-123">Create and manage namespaces, topics, queues, and subscriptions with the management API.</span></span>

<span data-ttu-id="6da95-124">[Agregue una dependencia](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) al archivo `pom.xml` de Maven para utilizar la API de administración en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="6da95-124">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-servicebus</artifactId>
    <version>1.2.1</version>
</dependency>
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="6da95-125">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="6da95-125">Explore the Management APIs</span></span>](/java/api/overview/azure/servicebus/managementapi)


## <a name="examples"></a><span data-ttu-id="6da95-126">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="6da95-126">Examples</span></span>

<span data-ttu-id="6da95-127">[Administración de colas de Service Bus](https://github.com/Azure-Samples/service-bus-java-manage-queue-with-basic-features)
[Creación y suscripción a temas de Service Bus](https://github.com/Azure-Samples/service-bus-java-manage-publish-subscribe-with-basic-features)</span><span class="sxs-lookup"><span data-stu-id="6da95-127">[Manage Service Bus queues](https://github.com/Azure-Samples/service-bus-java-manage-queue-with-basic-features)
[Create and subscribe to Service Bus topics](https://github.com/Azure-Samples/service-bus-java-manage-publish-subscribe-with-basic-features)</span></span>

<span data-ttu-id="6da95-128">Vea más [código de Java de ejemplo para Azure Service Bus](https://azure.microsoft.com/resources/samples/?platform=java&term=bus) que puede usar en sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="6da95-128">Explore more [sample Java code for Azure Service Bus](https://azure.microsoft.com/resources/samples/?platform=java&term=bus) you can use in your apps.</span></span>