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
# <a name="azure-resource-manager-libraries-for-java"></a><span data-ttu-id="a597d-104">Bibliotecas de Azure Resource Manager para Java</span><span class="sxs-lookup"><span data-stu-id="a597d-104">Azure Resource Manager libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="a597d-105">Información general</span><span class="sxs-lookup"><span data-stu-id="a597d-105">Overview</span></span>

<span data-ttu-id="a597d-106">Implemente, supervise y administre grupos de recursos con [Azure Resource Manager](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview).</span><span class="sxs-lookup"><span data-stu-id="a597d-106">Deploy, monitor, and manage resources in groups with [Azure Resource Manager](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview).</span></span>

## <a name="management-api"></a><span data-ttu-id="a597d-107">API de administración</span><span class="sxs-lookup"><span data-stu-id="a597d-107">Management API</span></span>

<span data-ttu-id="a597d-108">Use la API de administración para crear grupos de recursos e implementar recursos desde plantillas.</span><span class="sxs-lookup"><span data-stu-id="a597d-108">Use the management API to create resource groups and deploy resources from templates.</span></span>

<span data-ttu-id="a597d-109">[Agregue una dependencia](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) al archivo `pom.xml` de Maven para utilizar la API de administración en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="a597d-109">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>


```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-resources</artifactId>
    <version>1.3.0</version>
</dependency>
```

## <a name="example"></a><span data-ttu-id="a597d-110">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="a597d-110">Example</span></span>

<span data-ttu-id="a597d-111">Cree un nuevo grupo de recursos en la región de Azure este de EE. UU.</span><span class="sxs-lookup"><span data-stu-id="a597d-111">Create a new resource group in the Azure Eastern US region.</span></span>

```java
ResourceGroup resourceGroup = azure.resourceGroups().define("myResourceGroup")
            .withRegion(Region.US_EAST)
            .create();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="a597d-112">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="a597d-112">Explore the Management APIs</span></span>](/java/api/overview/azure/resources/managementapi)

## <a name="samples"></a><span data-ttu-id="a597d-113">Muestras</span><span class="sxs-lookup"><span data-stu-id="a597d-113">Samples</span></span>

<span data-ttu-id="a597d-114">[Administración de grupos de recursos de Azure con Java][1] 
[Implementación de los recursos mediante una plantilla de ARM][2]</span><span class="sxs-lookup"><span data-stu-id="a597d-114">[Manage Azure Resource Groups with Java][1] 
[Deploy resources using an ARM template][2]</span></span>

[1]: https://github.com/Azure-Samples/resources-java-manage-resource-group
[2]: https://github.com/Azure-Samples/resources-java-deploy-using-arm-template

<span data-ttu-id="a597d-115">Consulte la [lista completa](https://azure.microsoft.com/resources/samples/?platform=java&term=resource) de ejemplos de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a597d-115">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=java&term=resource) of Azure Resource Manager samples.</span></span>
