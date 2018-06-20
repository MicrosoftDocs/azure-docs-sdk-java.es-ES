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
# <a name="azure-iot-libraries-for-java"></a>Bibliotecas de Azure IoT para Java

Conecte, supervise y controle los recursos de Internet de las cosas con [Azure IoT Hub](https://docs.microsoft.com/azure/iot-hub/iot-hub-what-is-iot-hub).

Para empezar a trabajar con Azure IoT Hub, consulte [Conexión del dispositivo con IoT Hub con Java](/azure/iot-hub/iot-hub-java-java-getstarted).

## <a name="iot-service-library"></a>Biblioteca de servicios IoT

Registre dispositivos y envíe mensajes desde la nube a los dispositivos registrados mediante la biblioteca de servicios IoT.

[Agregue una dependencia](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) al archivo `pom.xml` de Maven para utilizar la biblioteca de cliente en el proyecto.  

```XML
<dependency>
    <groupId>com.microsoft.azure.sdk.iot</groupId>
    <artifactId>iot-service-client</artifactId>
    <version>1.6.23</version>
</dependency>
```   

## <a name="iot-device-library"></a>Biblioteca de dispositivo de IoT

Envíe mensajes a la nube y reciba mensajes en los dispositivos mediante la biblioteca de dispositivos de IoT.

[Agregue una dependencia](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) al archivo `pom.xml` de Maven para utilizar la biblioteca de cliente en el proyecto.  

```XML
<dependency>
    <groupId>com.microsoft.azure.sdk.iot</groupId>
    <artifactId>iot-device-client</artifactId>
    <version>1.3.31</version>
</dependency>
```

> [!div class="nextstepaction"]
> [Explorar las API de cliente](/java/api/overview/azure/iot/client)   

## <a name="example"></a>Ejemplo

Envíe un mensaje desde Azure IoT Hub a un dispositivo.

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


## <a name="samples"></a>Ejemplos

[Ejemplos de dispositivos IoT](https://github.com/Azure/azure-iot-sdk-java/tree/master/device/iot-device-samples)     
[Ejemplos de servicios IoT](https://github.com/Azure/azure-iot-sdk-java/tree/master/service/iot-service-samples)

Ver más [código de Java de ejemplo para Azure IoT](https://azure.microsoft.com/resources/samples/?platform=java&term=iot) que puede usar en sus aplicaciones.
