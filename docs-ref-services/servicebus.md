---
title: Bibliotecas de Service Bus para Java
description: Documentación de referencia del cliente Java y las bibliotecas de administración de Service Bus para Java
keywords: Azure, Java, SDK, API, mensajería, amqp, qpid, JMS, pubsub, pub-sub, agente de mensajes
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/11/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: service-bus
ms.openlocfilehash: 2099695784a59bf539aeae745df1fe38ec84f511
ms.sourcegitcommit: 115f4c8ad07a11f17d79e9d945d63917836b11c8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "61593280"
---
# <a name="service-bus-libraries-for-java"></a>Bibliotecas de Service Bus para Java

## <a name="overview"></a>Información general

Service Bus es un servicio de plataforma de mensajería transaccional de clase empresarial que proporciona colas y temas de publicación y suscripción altamente confiables, con funcionalidades y características como entrega ordenada, sesiones, creación de particiones, programación, suscripciones complejas, flujos de trabajo y administración de transacciones.

Las funcionalidades de Service Bus son comparables y, a menudo, superan las de los agentes de mensajes heredados locales de tecnología avanzada. Las características de Service Bus están disponibles a través de protocolos basados en estándares como AMQP 1.0 y HTTPS, y todos los movimientos de los protocolos están totalmente documentados, lo que permite una amplia interoperabilidad. 

Centrado en una mensajería duradera altamente disponible y confiable, Service Bus Premium proporciona rendimiento competitivo incluso en implementaciones con importantes centros de datos locales, pero sin procesos de selección y adquisición de hardware, planeamiento y ejecución de la implementación ni sesiones interminables de optimización del rendimiento. 

Service Bus Premium es una oferta completamente administrada con capacidad dedicada reservada para cada inquilino, que da como resultado un rendimiento predecible con un modelo de precios simple y orientado a la capacidad con costo general muy inferior al de los agentes comerciales en implementaciones locales. Para muchos clientes, Service Bus Premium puede reemplazar clústeres de mensajería locales dedicados hoy en día, incluso si las cargas de trabajo conectadas no se ejecutan en la nube. 

Puede obtener información sobre los conceptos de Service Bus [en la sección de documentación de mensajería](https://docs.microsoft.com/azure/service-bus-messaging/) 

Para desarrolladores de Java, Service Bus proporciona una API nativa compatible con Microsoft y también puede usarse con bibliotecas compatibles con AMQP 1.0, como el proveedor JMS de Apache Qpid Proton.

## <a name="client-library"></a>Biblioteca de cliente

El cliente oficial de Service Bus está disponible en [forma de código fuente en GitHub](https://github.com/azure/azure-service-bus-java) y los archivos binarios y fuentes empaquetados [están disponibles en Maven Central](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-servicebus%22).

**El [repositorio de código de ejemplo](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/) contiene ejemplos para:**
* Procedimientos para utilizar [QueueClient](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/src/com/microsoft/azure/servicebus/samples/BasicSendReceiveWithQueueClient.java)
* Procedimientos para utilizar [TopicClient y SubscriptionClient](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/src/com/microsoft/azure/servicebus/samples/BasicSendReceiveWithTopicSubscriptionClient.java)
* Procedimientos para usar mensajes [MessageSender y MessageReceiver](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/src/com/microsoft/azure/servicebus/samples/SendReceiveWithMessageSenderReceiver.java) de Service Bus.

Agregue una dependencia al archivo `pom.xml` del proyecto de Maven para utilizar la biblioteca en su propio proyecto. Especifique la versión según sea necesario.

[Agregue una dependencia](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) al archivo `pom.xml` de Maven para utilizar la biblioteca de cliente en el proyecto.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-servicebus</artifactId>
    <version>1.0.0</version>
</dependency>
```

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
> [Explorar las API de cliente](/java/api/overview/azure/servicebus/client)
> [Puede buscar más ejemplos aquí (consulte más detalles más arriba)](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/)

## <a name="management-api"></a>API de administración

Cree y administre espacios de nombres, temas, colas y suscripciones con la API de administración.

**Aquí puede encontrar algunos ejemplos:**
* [Administración de colas de Service Bus](https://github.com/Azure-Samples/service-bus-java-manage-queue-with-basic-features)
* [Creación y suscripción a temas de Service Bus](https://github.com/Azure-Samples/service-bus-java-manage-publish-subscribe-with-basic-features)

**Uso de la API de administración en el proyecto:**
\
[Agregue una dependencia](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) al archivo `pom.xml` de Maven para utilizar la API de administración en el proyecto.  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-servicebus</artifactId>
    <version>1.3.0</version>
</dependency>
```

> [!div class="nextstepaction"]
> [Explorar las API de administración](/java/api/overview/azure/servicebus/management)

Vea más [código de Java de ejemplo para Azure Service Bus](https://azure.microsoft.com/resources/samples/?platform=java&term=bus) que puede usar en sus aplicaciones.
