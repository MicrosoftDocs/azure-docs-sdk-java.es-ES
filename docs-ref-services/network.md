---
title: Bibliotecas del servicio de red de Azure para Java
description: "Documentación de referencia de las bibliotecas de administración del servicio de red de Azure para Java"
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
ms.openlocfilehash: 7be23ba896887cc88ccdf0fb049cb5f579d496c3
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/28/2017
---
# <a name="azure-network-libraries-for-java"></a><span data-ttu-id="48137-104">Bibliotecas del servicio de red de Azure para Java</span><span class="sxs-lookup"><span data-stu-id="48137-104">Azure Network libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="48137-105">Información general</span><span class="sxs-lookup"><span data-stu-id="48137-105">Overview</span></span>

<span data-ttu-id="48137-106">Conecte con recursos de Azure, filtre y equilibre el tráfico y administre el enrutamiento con el [servicio de red de Azure](/azure/networking/networking-overview).</span><span class="sxs-lookup"><span data-stu-id="48137-106">Connect Azure resources, filter and balance traffic, and manage routing with [Azure Networking](/azure/networking/networking-overview).</span></span>

<span data-ttu-id="48137-107">Para empezar a trabajar con el servicio de red de Azure, consulte [Creación de su primera red virtual](/azure/virtual-network/virtual-network-get-started-vnet-subnet).</span><span class="sxs-lookup"><span data-stu-id="48137-107">To get started with Azure Networking, see [Create your first virtual network](/azure/virtual-network/virtual-network-get-started-vnet-subnet).</span></span>

## <a name="management-api"></a><span data-ttu-id="48137-108">API de administración</span><span class="sxs-lookup"><span data-stu-id="48137-108">Management API</span></span>

<span data-ttu-id="48137-109">Cree y administre [redes virtuales](/azure/virtual-network/virtual-networks-overview), [ExpressRoutes](/azure/expressroute/) y [puertas de enlace de aplicaciones](/azure/application-gateway/) de Azure con la API de administración.</span><span class="sxs-lookup"><span data-stu-id="48137-109">Create and manage Azure [virtual networks](/azure/virtual-network/virtual-networks-overview) , [ExpressRoutes](/azure/expressroute/) , and [Application Gateways](/azure/application-gateway/) with the management API.</span></span>

<span data-ttu-id="48137-110">[Agregue una dependencia](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) al archivo `pom.xml` de Maven para utilizar la API de administración en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="48137-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-network</artifactId>
    <version>1.1.2</version>
</dependency>
```   

### <a name="example"></a><span data-ttu-id="48137-111">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="48137-111">Example</span></span>

<span data-ttu-id="48137-112">Cree una nueva red virtual con una sola subred.</span><span class="sxs-lookup"><span data-stu-id="48137-112">Create a new virtual network with a single subnet.</span></span>

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
> [<span data-ttu-id="48137-113">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="48137-113">Explore the Management APIs</span></span>](/java/api/overview/azure/networking/managementapi)

## <a name="samples"></a><span data-ttu-id="48137-114">Muestras</span><span class="sxs-lookup"><span data-stu-id="48137-114">Samples</span></span>

<span data-ttu-id="48137-115">[Administración de redes virtuales](https://github.com/Azure-Samples/network-java-manage-virtual-network) </span><span class="sxs-lookup"><span data-stu-id="48137-115">[Manage virtual networks](https://github.com/Azure-Samples/network-java-manage-virtual-network) </span></span>  
<span data-ttu-id="48137-116">[Administración de interfaces de red](https://github.com/Azure-Samples/network-java-manage-network-interface) </span><span class="sxs-lookup"><span data-stu-id="48137-116">[Manage network interfaces](https://github.com/Azure-Samples/network-java-manage-network-interface) </span></span>  
<span data-ttu-id="48137-117">[Administración de puertas de enlace de aplicaciones](https://github.com/Azure-Samples/application-gateway-java-manage-simple-application-gateways) </span><span class="sxs-lookup"><span data-stu-id="48137-117">[Manage Application Gateways](https://github.com/Azure-Samples/application-gateway-java-manage-simple-application-gateways) </span></span>  
[<span data-ttu-id="48137-118">Administración de equilibradores de carga accesibles desde Internet</span><span class="sxs-lookup"><span data-stu-id="48137-118">Manage internet facing load balancers</span></span>](https://github.com/Azure-Samples/network-java-manage-internet-facing-load-balancers)   

<span data-ttu-id="48137-119">Vea más [código de Java de ejemplo para el servicio de red de Azure](https://azure.microsoft.com/resources/samples/?platform=java&term=network) que puede usar en sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="48137-119">Explore more [sample Java code for Azure Networking](https://azure.microsoft.com/resources/samples/?platform=java&term=network) you can use in your apps.</span></span>
