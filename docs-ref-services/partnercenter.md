---
title: SDK de Java del Centro de partners
description: Documentación de referencia del SDK de Partner Center para Java
keywords: API, CSP, proveedor de soluciones en la nube, Java, Centro de partners, SDK
author: iswillia
ms.author: iswillia
manager: lesliep
ms.date: 10/09/2018
ms.topic: reference
ms.prod: partnercenter
ms.technology: partnercenter
ms.devlang: java
ms.openlocfilehash: 2adfbdbd37d6eb91e48ee37091f951b3f7d59eb9
ms.sourcegitcommit: 4da7d2f470331feb7d76a1658f5825f365cdba9a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/12/2018
ms.locfileid: "49121652"
---
# <a name="partner-center-libraries-for-java"></a><span data-ttu-id="caee4-104">Bibliotecas del Centro de partners para Java</span><span class="sxs-lookup"><span data-stu-id="caee4-104">Partner Center libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="caee4-105">Información general</span><span class="sxs-lookup"><span data-stu-id="caee4-105">Overview</span></span>

<span data-ttu-id="caee4-106">Las bibliotecas del Centro de partners para Java forman un SDK que permite interactuar con el servicio Centro de partners de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="caee4-106">The Partner Center libraries for Java is a SDK that provides the ability to interact with Microsoft's Partner Center service.</span></span> <span data-ttu-id="caee4-107">Esto permite a los asociados realizar las operaciones del Centro de partners mediante programación.</span><span class="sxs-lookup"><span data-stu-id="caee4-107">This enables partners to perform the Partner Center operations programmatically.</span></span> <span data-ttu-id="caee4-108">Es la última incorporación a la cartera existente de API REST y el SDK de .NET.</span><span class="sxs-lookup"><span data-stu-id="caee4-108">This is the latest addition to existing portfolio of REST APIs and the .NET SDK.</span></span>

## <a name="client-library"></a><span data-ttu-id="caee4-109">Biblioteca de cliente</span><span class="sxs-lookup"><span data-stu-id="caee4-109">Client library</span></span>

<span data-ttu-id="caee4-110">Administre los recursos del Centro de partners con la biblioteca cliente.</span><span class="sxs-lookup"><span data-stu-id="caee4-110">Manage resources in Partner Center using the client library.</span></span>

<span data-ttu-id="caee4-111">[Agregue una dependencia](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) al archivo `pom.xml` de Maven para utilizar la biblioteca de cliente en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="caee4-111">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>

```xml
<dependency>
    <groupId>com.microsoft.store</groupId>
    <artifactId>partnercenter</artifactId>
    <version>1.8.0</version>
</dependency>
```   

### <a name="example"></a><span data-ttu-id="caee4-112">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="caee4-112">Example</span></span>

<span data-ttu-id="caee4-113">Recupera una lista completa de clientes asociados con el distribuidor autenticado.</span><span class="sxs-lookup"><span data-stu-id="caee4-113">Retrieves a complete list of customer associated with the authenticated reseller.</span></span>

```java
IPartnerCredentials appCredentials = PartnerCredentials.getInstance().generateByApplicationCredentials('YOUR_APP_ID', 'YOUR_APP_SECRET', 'YOUR_TENANT_ID');
IAggregatePartner partnerOperations = PartnerService.getInstance().createPartnerOperations(appCredentials);

// Query the customers
SeekBasedResourceCollection<Customer> customersPage = partnerOperations.getCustomers().query(QueryFactory.getInstance().buildIndexedQuery(100));
this.getContext().getConsoleHelper().stopProgress();

// Create a customer enumerator which will aid us in traversing the customer pages
IResourceCollectionEnumerator<SeekBasedResourceCollection<Customer>> customersEnumerator =
    partnerOperations.getEnumerators().getCustomers().create( customersPage );

int pageNumber = 1;

while ( customersEnumerator.hasValue() )
{
    /*
     * Perform some operation with the current page of customers using 
     * customersEnumerator.getCurrent()  
     */

    // Get the next page of customers
    customersEnumerator.next();
}
```

## <a name="samples"></a><span data-ttu-id="caee4-114">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="caee4-114">Samples</span></span>

<span data-ttu-id="caee4-115">[Escenarios admitidos](https://docs.microsoft.com/partner-center/develop/scenarios)
[Aplicación de consola de ejemplo](https://github.com/Microsoft/Partner-Center-Java-Samples)</span><span class="sxs-lookup"><span data-stu-id="caee4-115">[Supported scenarios](https://docs.microsoft.com/partner-center/develop/scenarios)
[Sample console application](https://github.com/Microsoft/Partner-Center-Java-Samples)</span></span>  