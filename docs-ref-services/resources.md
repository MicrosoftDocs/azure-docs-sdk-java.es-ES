---
title: Bibliotecas de Azure Resource Manager para Java
description: "Documentación de referencia de las bibliotecas de Resource Manager para Java"
keywords: Azure, Java, SDK, API, grupos de recursos, arm, resource manager
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 06/21/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: data-lake-store
ms.openlocfilehash: 4b73f6b03258e7d99bcca235cc2728d5e085b32a
ms.sourcegitcommit: 634ab7578c73a219f8f3a2a6d43999d9d372cb43
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/09/2017
---
# <a name="azure-resource-manager-libraries-for-java"></a>Bibliotecas de Azure Resource Manager para Java

## <a name="overview"></a>Información general

Implemente, supervise y administre grupos de recursos con [Azure Resource Manager](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview).

## <a name="management-api"></a>API de administración

Use la API de administración para crear grupos de recursos e implementar recursos desde plantillas.

[Agregue una dependencia](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) al archivo `pom.xml` de Maven para utilizar la API de administración en el proyecto.


```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-resources</artifactId>
    <version>1.3.0</version>
</dependency>
```

## <a name="example"></a>Ejemplo

Cree un nuevo grupo de recursos en la región de Azure este de EE. UU.

```java
ResourceGroup resourceGroup = azure.resourceGroups().define("myResourceGroup")
            .withRegion(Region.US_EAST)
            .create();
```

> [!div class="nextstepaction"]
> [Explorar las API de administración](/java/api/overview/azure/resources/managementapi)

## <a name="samples"></a>Muestras

[Administración de grupos de recursos de Azure con Java][1] 
[Implementación de los recursos mediante una plantilla de ARM][2]

[1]: https://github.com/Azure-Samples/resources-java-manage-resource-group
[2]: https://github.com/Azure-Samples/resources-java-deploy-using-arm-template

Consulte la [lista completa](https://azure.microsoft.com/resources/samples/?platform=java&term=resource) de ejemplos de Azure Resource Manager.
