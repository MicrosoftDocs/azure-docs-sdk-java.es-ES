---
title: Bibliotecas de Azure Traffic Manager para Java
description: Documentación de referencia de las bibliotecas de administración de Traffic Manager para Java
keywords: Azure, Java, SDK, API, equilibrio de carga, distribución de la carga,red, Traffic Manager
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/11/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: traffic-manager
ms.openlocfilehash: fd78402f50df16ad7d57c0ca67815bfad5b18d51
ms.sourcegitcommit: 49b17bbf34732512f836ee634818f1058147ff5c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
ms.locfileid: "31823748"
---
# <a name="azure-traffic-manager-libraries-for-java"></a>Bibliotecas de Azure Traffic Manager para Java

## <a name="overview"></a>Información general

Con [Azure Traffic Manager](/azure/traffic-manager/traffic-manager-overview) puede controlar la distribución del tráfico de usuario en los puntos de conexión de servicio en los diferentes centros de datos.

Para empezar a trabajar con Azure Traffic Manager, consulte [Creación de un perfil de Traffic Manager](/azure/traffic-manager/traffic-manager-create-profile).

## <a name="management-api"></a>API de administración

Cree perfiles de Traffic Manager, defina puntos de conexión y cambie el método de enrutamiento con la API de administración. 

[Agregue una dependencia](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) al archivo `pom.xml` de Maven para utilizar la API de administración en el proyecto.  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-trafficmanager</artifactId>
    <version>1.3.0</version>
</dependency>
```   

## <a name="example"></a>Ejemplo

Cree un perfil de Traffic Manager y asigne un punto de conexión único.

```java
TrafficManagerProfile tmProfile = azure.trafficManagerProfiles().define("testTMProfile")
        .withNewResourceGroup(Region.US_EAST)
        .withLeafDomainLabel("testTMProfile")
        .withPriorityBasedRouting()
        .defineAzureTargetEndpoint("endpoint")
        .toResourceId(webAppId)
        .withRoutingPriority(1)
        .attach()
        .create();
```

> [!div class="nextstepaction"]
> [Explorar las API de administración](/java/api/overview/azure/trafficmanager/management)

## <a name="samples"></a>Ejemplos

[Equilibrado del tráfico de aplicación web en varias regiones](https://github.com/Azure-Samples/traffic-manager-java-manage-profiles)

Ver más [código de Java de ejemplo para Azure Traffic Manager](https://azure.microsoft.com/resources/samples/?platform=java&term=traffic) que puede usar en sus aplicaciones.
