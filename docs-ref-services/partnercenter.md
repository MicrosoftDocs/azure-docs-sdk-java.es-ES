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
# <a name="partner-center-libraries-for-java"></a>Bibliotecas del Centro de partners para Java

## <a name="overview"></a>Información general

Las bibliotecas del Centro de partners para Java forman un SDK que permite interactuar con el servicio Centro de partners de Microsoft. Esto permite a los asociados realizar las operaciones del Centro de partners mediante programación. Es la última incorporación a la cartera existente de API REST y el SDK de .NET.

## <a name="client-library"></a>Biblioteca de cliente

Administre los recursos del Centro de partners con la biblioteca cliente.

[Agregue una dependencia](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) al archivo `pom.xml` de Maven para utilizar la biblioteca de cliente en el proyecto.

```xml
<dependency>
    <groupId>com.microsoft.store</groupId>
    <artifactId>partnercenter</artifactId>
    <version>1.8.0</version>
</dependency>
```   

### <a name="example"></a>Ejemplo

Recupera una lista completa de clientes asociados con el distribuidor autenticado.

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

## <a name="samples"></a>Ejemplos

[Escenarios admitidos](https://docs.microsoft.com/partner-center/develop/scenarios)
[Aplicación de consola de ejemplo](https://github.com/Microsoft/Partner-Center-Java-Samples)  