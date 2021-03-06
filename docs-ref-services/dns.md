---
title: Bibliotecas de DNS de Azure para Java
description: Documentación de referencia de las bibliotecas de administración de DNS de Azure para Java
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
ms.openlocfilehash: 90751d2134b218e16415effeb336a62c6c737cb3
ms.sourcegitcommit: 733115fe0a7b5109b511b4a32490f8264cf91217
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/15/2019
ms.locfileid: "65626066"
---
# <a name="azure-dns-libraries-for-java"></a>Bibliotecas de DNS de Azure para Java

## <a name="overview"></a>Información general

Proporcione resolución de nombres de dominio y administre los registros DNS con las mismas credenciales, API, herramientas y facturación que los otros servicios de Azure con [Azure DNS](/azure/dns/dns-overview).

Para empezar a usar Azure DNS, consulte [Introducción a Azure DNS mediante la CLI de Azure 2.0](/azure/dns/dns-getstarted-cli).

## <a name="management-api"></a>API de administración

Cree zonas DNS y agregue registros a las zonas con la API de administración.

[Agregue una dependencia](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) al archivo `pom.xml` de Maven para utilizar la biblioteca de cliente en el proyecto.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-dns</artifactId>
    <version>1.22.0</version>
</dependency>
```   

### <a name="example"></a>Ejemplo

Cree una zona DNS raíz y agregue un registro CNAME `www` en un grupo de recursos existente.

```java
DnsZone rootDnsZone = azure.dnsZones().define("contoso.com")
        .withExistingResourceGroup("myResourceGroup")
        .create();
rootDnsZone = rootDnsZone.update()
        .withCNameRecordSet("www", "172.30.241.20")
        .apply();
```

> [!div class="nextstepaction"]
> [Explorar las API de administración](/java/api/overview/azure/dns/management)

## <a name="samples"></a>Ejemplos

[Hospedaje y administración de dominios con Azure DNS](https://github.com/Azure-Samples/dns-java-host-and-manage-your-domains)

Ver más [código de Java de ejemplo para DNS de Azure](https://azure.microsoft.com/resources/samples/?platform=java&term=dns) que puede usar en sus aplicaciones.

<!---Loc Comment: Please, refer to conversation section to check the issue. Thanks.--->
