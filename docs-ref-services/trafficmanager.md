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
---
# <a name="azure-traffic-manager-libraries-for-java"></a><span data-ttu-id="a4a37-104">Bibliotecas de Azure Traffic Manager para Java</span><span class="sxs-lookup"><span data-stu-id="a4a37-104">Azure Traffic Manager libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="a4a37-105">Información general</span><span class="sxs-lookup"><span data-stu-id="a4a37-105">Overview</span></span>

<span data-ttu-id="a4a37-106">Con [Azure Traffic Manager](/azure/traffic-manager/traffic-manager-overview) puede controlar la distribución del tráfico de usuario en los puntos de conexión de servicio en los diferentes centros de datos.</span><span class="sxs-lookup"><span data-stu-id="a4a37-106">Control the distribution of user traffic for service endpoints in different datacenters with [Azure Traffic Manager](/azure/traffic-manager/traffic-manager-overview).</span></span>

<span data-ttu-id="a4a37-107">Para empezar a trabajar con Azure Traffic Manager, consulte [Creación de un perfil de Traffic Manager](/azure/traffic-manager/traffic-manager-create-profile).</span><span class="sxs-lookup"><span data-stu-id="a4a37-107">To get started with Azure Traffic Manager, see [Create a Traffic Manager profile](/azure/traffic-manager/traffic-manager-create-profile).</span></span>

## <a name="management-api"></a><span data-ttu-id="a4a37-108">API de administración</span><span class="sxs-lookup"><span data-stu-id="a4a37-108">Management API</span></span>

<span data-ttu-id="a4a37-109">Cree perfiles de Traffic Manager, defina puntos de conexión y cambie el método de enrutamiento con la API de administración.</span><span class="sxs-lookup"><span data-stu-id="a4a37-109">Create Traffic Manager profiles, define endpoints, and change the routing method with the management API.</span></span> 

<span data-ttu-id="a4a37-110">[Agregue una dependencia](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) al archivo `pom.xml` de Maven para utilizar la API de administración en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="a4a37-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-trafficmanager</artifactId>
    <version>1.3.0</version>
</dependency>
```   

## <a name="example"></a><span data-ttu-id="a4a37-111">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="a4a37-111">Example</span></span>

<span data-ttu-id="a4a37-112">Cree un perfil de Traffic Manager y asigne un punto de conexión único.</span><span class="sxs-lookup"><span data-stu-id="a4a37-112">Create a Traffic Manager profile and assign a single endpoint.</span></span>

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
> [<span data-ttu-id="a4a37-113">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="a4a37-113">Explore the Management APIs</span></span>](/java/api/overview/azure/trafficmanager/management)

## <a name="samples"></a><span data-ttu-id="a4a37-114">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="a4a37-114">Samples</span></span>

[<span data-ttu-id="a4a37-115">Equilibrado del tráfico de aplicación web en varias regiones</span><span class="sxs-lookup"><span data-stu-id="a4a37-115">Balance web app traffic across multiple regions</span></span>](https://github.com/Azure-Samples/traffic-manager-java-manage-profiles)

<span data-ttu-id="a4a37-116">Ver más [código de Java de ejemplo para Azure Traffic Manager](https://azure.microsoft.com/resources/samples/?platform=java&term=traffic) que puede usar en sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="a4a37-116">Explore more [sample Java code for Azure Traffic Manager](https://azure.microsoft.com/resources/samples/?platform=java&term=traffic) you can use in your apps.</span></span>
