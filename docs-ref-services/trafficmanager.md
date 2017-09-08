---
title: Bibliotecas de Azure Traffic Manager para Java
description: "Documentación de referencia de las bibliotecas de administración de Traffic Manager para Java"
keywords: "Azure, Java, SDK, API, equilibrio de carga, distribución de la carga,red, Traffic Manager"
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/11/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: traffic-manager
ms.openlocfilehash: 3b9c8f0e3bd5e8feb5a819a7c2583ffbbcf53e38
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/28/2017
---
# <a name="azure-traffic-manager-libraries-for-java"></a><span data-ttu-id="f4c62-104">Bibliotecas de Azure Traffic Manager para Java</span><span class="sxs-lookup"><span data-stu-id="f4c62-104">Azure Traffic Manager libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="f4c62-105">Información general</span><span class="sxs-lookup"><span data-stu-id="f4c62-105">Overview</span></span>

<span data-ttu-id="f4c62-106">Con [Azure Traffic Manager](/azure/traffic-manager/traffic-manager-overview) puede controlar la distribución del tráfico de usuario en los puntos de conexión de servicio en los diferentes centros de datos.</span><span class="sxs-lookup"><span data-stu-id="f4c62-106">Control the distribution of user traffic for service endpoints in different datacenters with [Azure Traffic Manager](/azure/traffic-manager/traffic-manager-overview).</span></span>

<span data-ttu-id="f4c62-107">Para empezar a trabajar con Azure Traffic Manager, consulte [Creación de un perfil de Traffic Manager](/azure/traffic-manager/traffic-manager-create-profile).</span><span class="sxs-lookup"><span data-stu-id="f4c62-107">To get started with Azure Traffic Manager, see [Create a Traffic Manager profile](/azure/traffic-manager/traffic-manager-create-profile).</span></span>

## <a name="management-api"></a><span data-ttu-id="f4c62-108">API de administración</span><span class="sxs-lookup"><span data-stu-id="f4c62-108">Management API</span></span>

<span data-ttu-id="f4c62-109">Cree perfiles de Traffic Manager, defina puntos de conexión y cambie el método de enrutamiento con la API de administración.</span><span class="sxs-lookup"><span data-stu-id="f4c62-109">Create Traffic Manager profiles, define endpoints, and change the routing method with the management API.</span></span> 

<span data-ttu-id="f4c62-110">[Agregue una dependencia](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) al archivo `pom.xml` de Maven para utilizar la API de administración en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="f4c62-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-trafficmanager</artifactId>
    <version>1.1.2</version>
</dependency>
```   

## <a name="example"></a><span data-ttu-id="f4c62-111">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="f4c62-111">Example</span></span>

<span data-ttu-id="f4c62-112">Cree un perfil de Traffic Manager y asigne un punto de conexión único.</span><span class="sxs-lookup"><span data-stu-id="f4c62-112">Create a Traffic Manager profile and assign a single endpoint.</span></span>

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
> [<span data-ttu-id="f4c62-113">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="f4c62-113">Explore the Management APIs</span></span>](/java/api/overview/azure/trafficmanager/managementapi)

## <a name="samples"></a><span data-ttu-id="f4c62-114">Muestras</span><span class="sxs-lookup"><span data-stu-id="f4c62-114">Samples</span></span>

[<span data-ttu-id="f4c62-115">Equilibrado del tráfico de aplicación web en varias regiones</span><span class="sxs-lookup"><span data-stu-id="f4c62-115">Balance web app traffic across multiple regions</span></span>](https://github.com/Azure-Samples/traffic-manager-java-manage-profiles)

<span data-ttu-id="f4c62-116">Ver más [código de Java de ejemplo para Azure Traffic Manager](https://azure.microsoft.com/resources/samples/?platform=java&term=traffic) que puede usar en sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="f4c62-116">Explore more [sample Java code for Azure Traffic Manager](https://azure.microsoft.com/resources/samples/?platform=java&term=traffic) you can use in your apps.</span></span>
