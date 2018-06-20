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
# <a name="azure-network-libraries-for-java"></a><span data-ttu-id="d4780-104">Bibliotecas del servicio de red de Azure para Java</span><span class="sxs-lookup"><span data-stu-id="d4780-104">Azure Network libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="d4780-105">Información general</span><span class="sxs-lookup"><span data-stu-id="d4780-105">Overview</span></span>

<span data-ttu-id="d4780-106">Conecte con recursos de Azure, filtre y equilibre el tráfico y administre el enrutamiento con el [servicio de red de Azure](/azure/networking/networking-overview).</span><span class="sxs-lookup"><span data-stu-id="d4780-106">Connect Azure resources, filter and balance traffic, and manage routing with [Azure Networking](/azure/networking/networking-overview).</span></span>

<span data-ttu-id="d4780-107">Para empezar a trabajar con el servicio de red de Azure, consulte [Creación de su primera red virtual](/azure/virtual-network/virtual-network-get-started-vnet-subnet).</span><span class="sxs-lookup"><span data-stu-id="d4780-107">To get started with Azure Networking, see [Create your first virtual network](/azure/virtual-network/virtual-network-get-started-vnet-subnet).</span></span>

## <a name="management-api"></a><span data-ttu-id="d4780-108">API de administración</span><span class="sxs-lookup"><span data-stu-id="d4780-108">Management API</span></span>

<span data-ttu-id="d4780-109">Cree y administre [redes virtuales](/azure/virtual-network/virtual-networks-overview), [ExpressRoutes](/azure/expressroute/) y [puertas de enlace de aplicaciones](/azure/application-gateway/) de Azure con la API de administración.</span><span class="sxs-lookup"><span data-stu-id="d4780-109">Create and manage Azure [virtual networks](/azure/virtual-network/virtual-networks-overview) , [ExpressRoutes](/azure/expressroute/) , and [Application Gateways](/azure/application-gateway/) with the management API.</span></span>

<span data-ttu-id="d4780-110">[Agregue una dependencia](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) al archivo `pom.xml` de Maven para utilizar la API de administración en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="d4780-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-network</artifactId>
    <version>1.3.0</version>
</dependency>
```   

### <a name="example"></a><span data-ttu-id="d4780-111">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="d4780-111">Example</span></span>

<span data-ttu-id="d4780-112">Cree una nueva red virtual con una sola subred.</span><span class="sxs-lookup"><span data-stu-id="d4780-112">Create a new virtual network with a single subnet.</span></span>

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
> [<span data-ttu-id="d4780-113">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="d4780-113">Explore the Management APIs</span></span>](/java/api/overview/azure/networking/management)

## <a name="samples"></a><span data-ttu-id="d4780-114">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="d4780-114">Samples</span></span>

<span data-ttu-id="d4780-115">[Administración de redes virtuales](https://github.com/Azure-Samples/network-java-manage-virtual-network) </span><span class="sxs-lookup"><span data-stu-id="d4780-115">[Manage virtual networks](https://github.com/Azure-Samples/network-java-manage-virtual-network) </span></span>  
<span data-ttu-id="d4780-116">[Administración de interfaces de red](https://github.com/Azure-Samples/network-java-manage-network-interface) </span><span class="sxs-lookup"><span data-stu-id="d4780-116">[Manage network interfaces](https://github.com/Azure-Samples/network-java-manage-network-interface) </span></span>  
<span data-ttu-id="d4780-117">[Administración de puertas de enlace de aplicaciones](https://github.com/Azure-Samples/application-gateway-java-manage-simple-application-gateways) </span><span class="sxs-lookup"><span data-stu-id="d4780-117">[Manage Application Gateways](https://github.com/Azure-Samples/application-gateway-java-manage-simple-application-gateways) </span></span>  
[<span data-ttu-id="d4780-118">Administración de equilibradores de carga accesibles desde Internet</span><span class="sxs-lookup"><span data-stu-id="d4780-118">Manage internet facing load balancers</span></span>](https://github.com/Azure-Samples/network-java-manage-internet-facing-load-balancers)   

<span data-ttu-id="d4780-119">Vea más [código de Java de ejemplo para el servicio de red de Azure](https://azure.microsoft.com/resources/samples/?platform=java&term=network) que puede usar en sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="d4780-119">Explore more [sample Java code for Azure Networking](https://azure.microsoft.com/resources/samples/?platform=java&term=network) you can use in your apps.</span></span>
