---
title: Bibliotecas de la red CDN de Azure para Java
description: Documentación de referencia de las bibliotecas de administración de la red CDN para Java
keywords: Azure, Java, SDK, API, contenido, distribución, red, CDN
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/11/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: cdn
ms.openlocfilehash: 199e9b4b2b2431e23954d24e4adeb4326eb4741c
ms.sourcegitcommit: 49b17bbf34732512f836ee634818f1058147ff5c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
ms.locfileid: "31823738"
---
# <a name="azure-cdn-libraries-for-java"></a>Bibliotecas de la red CDN de Azure para Java

## <a name="overview"></a>Información general

[Azure Content Delivery Network](/azure/cdn/cdn-overview) (CDN) almacena en caché contenido web estático en ubicaciones colocadas estratégicamente para proporcionar el máximo rendimiento a los usuarios.

Para empezar a trabajar con la red CDN de Azure, consulte [Introducción a la red CDN de Azure](/azure/cdn/cdn-create-new-endpoint).

## <a name="management-api"></a>API de administración

Cree perfiles de red CDN, defina puntos de conexión y agregue contenido a la red CDN mediante la API de administración.

[Agregue una dependencia](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) al archivo `pom.xml` de Maven para utilizar la API de administración en el proyecto.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-cdn</artifactId>
    <version>1.3.0</version>
</dependency>
```   

### <a name="example"></a>Ejemplo

Cree un perfil de CDN, asigne los puntos de conexión y cargue contenido en la red CDN.

```java
CdnProfile profile = azure.cdnProfiles().define("testCDN")
        .withRegion(Region.US_EAST)
        .withNewResourceGroup()
        .withStandardVerizonSku()
        .withNewEndpoint("webAppHostname1")
        .withNewEndpoint("webAppHostname2")
        .create();

List<String> contentList = new ArrayList<String>();
contentList.add("/client.js");
contentList.add("/media/fabrikam_logo.png");

for (CdnEndpoint endpoint : profile.endpoints().values()) {
    endpoint.loadContent(contentList);
}
```

> [!div class="nextstepaction"]
> [Explorar las API de administración](/java/api/overview/azure/cdn/management)

## <a name="samples"></a>Ejemplos

[Administración de redes CDN con Java](https://github.com/Azure-Samples/cdn-java-manage-cdn)

Ver más [código de Java de ejemplo para la red CDN de Azure](https://azure.microsoft.com/resources/samples/?platform=java&term=cdn) que puede usar en sus aplicaciones.