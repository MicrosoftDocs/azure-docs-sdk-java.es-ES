---
title: Bibliotecas de Azure IoT Hub para Java
description: Documentación de referencia de las bibliotecas de Azure IoT Hub para Java
keywords: Azure, Java, SDK, API, evento, IoT, secuencias, dispositivos, iot hub
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/20/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: iot-hub
ms.openlocfilehash: 5e6a102b062b2fff6b297c7e3dda423d1448bcb0
ms.sourcegitcommit: 49b17bbf34732512f836ee634818f1058147ff5c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
ms.locfileid: "31823618"
---
# <a name="azure-iot-libraries-for-java"></a><span data-ttu-id="16008-104">Bibliotecas de Azure IoT para Java</span><span class="sxs-lookup"><span data-stu-id="16008-104">Azure IoT libraries for Java</span></span>

<span data-ttu-id="16008-105">Conecte, supervise y controle los recursos de Internet de las cosas con [Azure IoT Hub](https://docs.microsoft.com/azure/iot-hub/iot-hub-what-is-iot-hub).</span><span class="sxs-lookup"><span data-stu-id="16008-105">Connect, monitor, and control Internet of Things assets with [Azure IoT Hub](https://docs.microsoft.com/azure/iot-hub/iot-hub-what-is-iot-hub).</span></span>

<span data-ttu-id="16008-106">Para empezar a trabajar con Azure IoT Hub, consulte [Conexión del dispositivo con IoT Hub con Java](/azure/iot-hub/iot-hub-java-java-getstarted).</span><span class="sxs-lookup"><span data-stu-id="16008-106">To get started with Azure IoT Hub, see [Connect your device to your IoT hub using Java](/azure/iot-hub/iot-hub-java-java-getstarted).</span></span>

## <a name="iot-service-library"></a><span data-ttu-id="16008-107">Biblioteca de servicios IoT</span><span class="sxs-lookup"><span data-stu-id="16008-107">IoT Service library</span></span>

<span data-ttu-id="16008-108">Registre dispositivos y envíe mensajes desde la nube a los dispositivos registrados mediante la biblioteca de servicios IoT.</span><span class="sxs-lookup"><span data-stu-id="16008-108">Register devices and send messages from the cloud to registered devices using the IoT Service library.</span></span>

<span data-ttu-id="16008-109">[Agregue una dependencia](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) al archivo `pom.xml` de Maven para utilizar la biblioteca de cliente en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="16008-109">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure.sdk.iot</groupId>
    <artifactId>iot-service-client</artifactId>
    <version>1.6.23</version>
</dependency>
```   

## <a name="iot-device-library"></a><span data-ttu-id="16008-110">Biblioteca de dispositivo de IoT</span><span class="sxs-lookup"><span data-stu-id="16008-110">Iot Device library</span></span>

<span data-ttu-id="16008-111">Envíe mensajes a la nube y reciba mensajes en los dispositivos mediante la biblioteca de dispositivos de IoT.</span><span class="sxs-lookup"><span data-stu-id="16008-111">Send messages to the cloud and receive messages on devices using the IoT Device library.</span></span>

<span data-ttu-id="16008-112">[Agregue una dependencia](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) al archivo `pom.xml` de Maven para utilizar la biblioteca de cliente en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="16008-112">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure.sdk.iot</groupId>
    <artifactId>iot-device-client</artifactId>
    <version>1.3.31</version>
</dependency>
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="16008-113">Explorar las API de cliente</span><span class="sxs-lookup"><span data-stu-id="16008-113">Explore the Client APIs</span></span>](/java/api/overview/azure/iot/client)   

## <a name="example"></a><span data-ttu-id="16008-114">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="16008-114">Example</span></span>

<span data-ttu-id="16008-115">Envíe un mensaje desde Azure IoT Hub a un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="16008-115">Send a message from Azure IoT Hub to a device.</span></span>

```java
Message messageToSend = new Message(messageText);
messageToSend.setDeliveryAcknowledgement(DeliveryAcknowledgement.Full);
messageToSend.setMessageId(java.util.UUID.randomUUID().toString());

// set message properties
Map<String, String> propertiesToSend = new HashMap<String, String>();
propertiesToSend.put(messagePropertyKey,messagePropertyKey);
messageToSend.setProperties(propertiesToSend);

CompletableFuture<Void> future = serviceClient.sendAsync(deviceId, messageToSend);
try {
    future.get();
}
catch (ExecutionException e) {
    System.out.println("Exception : " + e.getMessage());
}
```


## <a name="samples"></a><span data-ttu-id="16008-116">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="16008-116">Samples</span></span>

<span data-ttu-id="16008-117">[Ejemplos de dispositivos IoT](https://github.com/Azure/azure-iot-sdk-java/tree/master/device/iot-device-samples)   </span><span class="sxs-lookup"><span data-stu-id="16008-117">[IoT Device samples](https://github.com/Azure/azure-iot-sdk-java/tree/master/device/iot-device-samples)   </span></span>  
[<span data-ttu-id="16008-118">Ejemplos de servicios IoT</span><span class="sxs-lookup"><span data-stu-id="16008-118">IoT Service samples</span></span>](https://github.com/Azure/azure-iot-sdk-java/tree/master/service/iot-service-samples)

<span data-ttu-id="16008-119">Ver más [código de Java de ejemplo para Azure IoT](https://azure.microsoft.com/resources/samples/?platform=java&term=iot) que puede usar en sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="16008-119">Explore more [sample Java code for Azure IoT](https://azure.microsoft.com/resources/samples/?platform=java&term=iot) you can use in your apps.</span></span>
