---
title: Bibliotecas del servicio de red de Azure para Java
description: Documentación de referencia de las bibliotecas de administración del servicio de red de Azure para Java
keywords: Azure, Java, SDK, API, redes, equilibrio de carga, red virtual, subred
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/20/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: networking
ms.openlocfilehash: bb74ccd8826df7b627e0b5f4e4ffd2da44b2642d
ms.sourcegitcommit: 49b17bbf34732512f836ee634818f1058147ff5c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
ms.locfileid: "31823608"
---
# <a name="azure-network-libraries-for-java"></a>Bibliotecas del servicio de red de Azure para Java

## <a name="overview"></a>Información general

Conecte con recursos de Azure, filtre y equilibre el tráfico y administre el enrutamiento con el [servicio de red de Azure](/azure/networking/networking-overview).

Para empezar a trabajar con el servicio de red de Azure, consulte [Creación de su primera red virtual](/azure/virtual-network/virtual-network-get-started-vnet-subnet).

## <a name="management-api"></a>API de administración

Cree y administre [redes virtuales](/azure/virtual-network/virtual-networks-overview), [ExpressRoutes](/azure/expressroute/) y [puertas de enlace de aplicaciones](/azure/application-gateway/) de Azure con la API de administración.

[Agregue una dependencia](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) al archivo `pom.xml` de Maven para utilizar la API de administración en el proyecto.  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-network</artifactId>
    <version>1.3.0</version>
</dependency>
```   

### <a name="example"></a>Ejemplo

Cree una nueva red virtual con una sola subred.

```java
Network virtualNetwork1 = azure.networks().define(vnetName1)
        .withRegion(Region.US_EAST)
        .withExistingResourceGroup("myResourceGroup")
        .withAddressSpace("192.168.0.0/16")
        .defineSubnet("myVirtualNetwork")
            .withAddressPrefix("192.168.2.0/24")
            .attach()
        .create();
```

> [!div class="nextstepaction"]
> [Explorar las API de administración](/java/api/overview/azure/networking/management)

## <a name="samples"></a>Ejemplos

[Administración de redes virtuales](https://github.com/Azure-Samples/network-java-manage-virtual-network)   
[Administración de interfaces de red](https://github.com/Azure-Samples/network-java-manage-network-interface)   
[Administración de puertas de enlace de aplicaciones](https://github.com/Azure-Samples/application-gateway-java-manage-simple-application-gateways)   
[Administración de equilibradores de carga accesibles desde Internet](https://github.com/Azure-Samples/network-java-manage-internet-facing-load-balancers)   

Vea más [código de Java de ejemplo para el servicio de red de Azure](https://azure.microsoft.com/resources/samples/?platform=java&term=network) que puede usar en sus aplicaciones.
