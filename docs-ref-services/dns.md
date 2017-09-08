---
title: Bibliotecas de DNS de Azure para Java
description: "Documentación de referencia de las bibliotecas de administración de DNS de Azure para Java"
keywords: Azure, Java, SDK, API, dominios, DNS, nombre, servicio, servicio de nombres de dominio
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/11/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: dns
ms.openlocfilehash: 7b4f26fe6d99620207e3a53c8262180cccc66fd6
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/28/2017
---
# <a name="azure-traffic-manager-libraries-for-java"></a><span data-ttu-id="dd759-104">Bibliotecas de Azure Traffic Manager para Java</span><span class="sxs-lookup"><span data-stu-id="dd759-104">Azure Traffic Manager libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="dd759-105">Información general</span><span class="sxs-lookup"><span data-stu-id="dd759-105">Overview</span></span>

<span data-ttu-id="dd759-106">Proporcione resolución de nombres de dominio y administre los registros DNS con las mismas credenciales, API, herramientas y facturación que los otros servicios de Azure con [Azure DNS](/azure/dns/dns-overview).</span><span class="sxs-lookup"><span data-stu-id="dd759-106">Provide domain name resolution and manage your DNS records using the same credentials, APIs, tools, and billing as your other Azure services with [Azure DNS](/azure/dns/dns-overview).</span></span>

<span data-ttu-id="dd759-107">Para empezar a usar Azure DNS, consulte [Introducción a Azure DNS mediante la CLI de Azure 2.0](/azure/dns/dns-getstarted-cli).</span><span class="sxs-lookup"><span data-stu-id="dd759-107">To get started with Azure DNS, see [Get started with Azure DNS using the Azure CLI 2.0](/azure/dns/dns-getstarted-cli).</span></span>

## <a name="management-api"></a><span data-ttu-id="dd759-108">API de administración</span><span class="sxs-lookup"><span data-stu-id="dd759-108">Management API</span></span>

<span data-ttu-id="dd759-109">Cree zonas DNS y agregue registros a las zonas con la API de administración.</span><span class="sxs-lookup"><span data-stu-id="dd759-109">Create DNS zones and add records to zones with the management API.</span></span>

<span data-ttu-id="dd759-110">[Agregue una dependencia](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) al archivo `pom.xml` de Maven para utilizar la biblioteca de cliente en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="dd759-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-dns</artifactId>
    <version>1.1.2</version>
</dependency>
```   

### <a name="example"></a><span data-ttu-id="dd759-111">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="dd759-111">Example</span></span>

<span data-ttu-id="dd759-112">Cree una zona DNS raíz y agregue un registro CNAME `www` en un grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="dd759-112">Create a root DNS zone and add a `www` CNAME record in an existing resource group.</span></span>

```java
DnsZone rootDnsZone = azure.dnsZones().define("contoso.com")
        .withExistingResourceGroup("myResourceGroup")
        .create();
rootDnsZone = rootDnsZone.update()
        .withCNameRecordSet("www", "172.30.241.20")
        .apply();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="dd759-113">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="dd759-113">Explore the Management APIs</span></span>](/java/api/overview/azure/dns/managementapi)

## <a name="samples"></a><span data-ttu-id="dd759-114">Muestras</span><span class="sxs-lookup"><span data-stu-id="dd759-114">Samples</span></span>

[<span data-ttu-id="dd759-115">Hospedaje y administración de dominios con Azure DNS</span><span class="sxs-lookup"><span data-stu-id="dd759-115">Host and manage your domains with Azure DNS</span></span>](https://github.com/Azure-Samples/dns-java-host-and-manage-your-domains)

<span data-ttu-id="dd759-116">Ver más [código de Java de ejemplo para DNS de Azure](https://azure.microsoft.com/resources/samples/?platform=java&term=dns) que puede usar en sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="dd759-116">Explore more [sample Java code for Azure DNS](https://azure.microsoft.com/resources/samples/?platform=java&term=dns) you can use in your apps.</span></span>