---
title: Bibliotecas de la red CDN de Azure para Java
description: "Documentación de referencia de las bibliotecas de administración de la red CDN para Java"
keywords: "Azure, Java, SDK, API, contenido, distribución, red, CDN"
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/11/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: cdn
ms.openlocfilehash: 91df958d2d78fb4fd959c228b28c6ae003716be6
ms.sourcegitcommit: 634ab7578c73a219f8f3a2a6d43999d9d372cb43
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/09/2017
---
# <a name="azure-cdn-libraries-for-java"></a><span data-ttu-id="f4d53-104">Bibliotecas de la red CDN de Azure para Java</span><span class="sxs-lookup"><span data-stu-id="f4d53-104">Azure CDN libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="f4d53-105">Información general</span><span class="sxs-lookup"><span data-stu-id="f4d53-105">Overview</span></span>

<span data-ttu-id="f4d53-106">[Azure Content Delivery Network](/azure/cdn/cdn-overview) (CDN) almacena en caché contenido web estático en ubicaciones colocadas estratégicamente para proporcionar el máximo rendimiento a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="f4d53-106">Cache static web content at strategically placed locations to provide maximum throughput for users with [Azure Content Delivery Network](/azure/cdn/cdn-overview) (CDN).</span></span>

<span data-ttu-id="f4d53-107">Para empezar a trabajar con la red CDN de Azure, consulte [Introducción a la red CDN de Azure](/azure/cdn/cdn-create-new-endpoint).</span><span class="sxs-lookup"><span data-stu-id="f4d53-107">To get started with Azure CDN, see [Getting started with Azure CDN](/azure/cdn/cdn-create-new-endpoint).</span></span>

## <a name="management-api"></a><span data-ttu-id="f4d53-108">API de administración</span><span class="sxs-lookup"><span data-stu-id="f4d53-108">Management API</span></span>

<span data-ttu-id="f4d53-109">Cree perfiles de red CDN, defina puntos de conexión y agregue contenido a la red CDN mediante la API de administración.</span><span class="sxs-lookup"><span data-stu-id="f4d53-109">Create CDN profiles, define endpoints, and add content to the CDN using the management API.</span></span>

<span data-ttu-id="f4d53-110">[Agregue una dependencia](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) al archivo `pom.xml` de Maven para utilizar la API de administración en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="f4d53-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-cdn</artifactId>
    <version>1.3.0</version>
</dependency>
```   

### <a name="example"></a><span data-ttu-id="f4d53-111">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="f4d53-111">Example</span></span>

<span data-ttu-id="f4d53-112">Cree un perfil de CDN, asigne los puntos de conexión y cargue contenido en la red CDN.</span><span class="sxs-lookup"><span data-stu-id="f4d53-112">Create a CDN profile, assign endpoints, and load content into the CDN.</span></span>

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
> [<span data-ttu-id="f4d53-113">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="f4d53-113">Explore the Management APIs</span></span>](/java/api/overview/azure/cdn/managementapi)

## <a name="samples"></a><span data-ttu-id="f4d53-114">Muestras</span><span class="sxs-lookup"><span data-stu-id="f4d53-114">Samples</span></span>

[<span data-ttu-id="f4d53-115">Administración de redes CDN con Java</span><span class="sxs-lookup"><span data-stu-id="f4d53-115">Manage CDNs with Java</span></span>](https://github.com/Azure-Samples/cdn-java-manage-cdn)

<span data-ttu-id="f4d53-116">Ver más [código de Java de ejemplo para la red CDN de Azure](https://azure.microsoft.com/resources/samples/?platform=java&term=cdn) que puede usar en sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="f4d53-116">Explore more [sample Java code for Azure CDN](https://azure.microsoft.com/resources/samples/?platform=java&term=cdn) you can use in your apps.</span></span>