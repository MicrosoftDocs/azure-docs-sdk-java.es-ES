---
title: Bibliotecas de Azure App Service para Java
description: Automatice la implementación de aplicaciones web en Azure App Service mediante las API de administración de Azure.
keywords: Azure, Java, SDK, API, aplicaciones web, móviles, App Service
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/09/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: appservice
ms.openlocfilehash: adbb527666553ecc3039ce35c035d017f502c801
ms.sourcegitcommit: 49b17bbf34732512f836ee634818f1058147ff5c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
ms.locfileid: "31823798"
---
# <a name="azure-app-service-libraries-for-java"></a><span data-ttu-id="63e6e-104">Bibliotecas de Azure App Service para Java</span><span class="sxs-lookup"><span data-stu-id="63e6e-104">Azure App Service libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="63e6e-105">Información general</span><span class="sxs-lookup"><span data-stu-id="63e6e-105">Overview</span></span>

<span data-ttu-id="63e6e-106">Implemente y administre sitios web, aplicaciones web y API de REST con [Azure App Service](/azure/app-service).</span><span class="sxs-lookup"><span data-stu-id="63e6e-106">Deploy and manage websites, web applications, and REST APIs with [Azure App Service](/azure/app-service).</span></span>

<span data-ttu-id="63e6e-107">Para empezar a trabajar con Azure App Service, consulte [Creación de la primera aplicación web de Java en Azure](/azure/app-service-web/app-service-web-get-started-java).</span><span class="sxs-lookup"><span data-stu-id="63e6e-107">To get started with Azure App Service, see [Create your first Java web app in Azure](/azure/app-service-web/app-service-web-get-started-java).</span></span>

## <a name="management-api"></a><span data-ttu-id="63e6e-108">API de administración</span><span class="sxs-lookup"><span data-stu-id="63e6e-108">Management API</span></span>

<span data-ttu-id="63e6e-109">Implemente, escale y configure aplicaciones en Azure App Service con la API de administración.</span><span class="sxs-lookup"><span data-stu-id="63e6e-109">Deploy, scale, and configure applications in Azure App Service with the management API.</span></span>

<span data-ttu-id="63e6e-110">[Agregue una dependencia](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) al archivo `pom.xml` de Maven para utilizar la API de administración en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="63e6e-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-appservice</artifactId>
    <version>1.3.0</version>
</dependency>
```   

> [!div class="nextstepaction"]
> [<span data-ttu-id="63e6e-111">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="63e6e-111">Explore the Management APIs</span></span>](/java/api/overview/azure/appservice/management)

### <a name="example"></a><span data-ttu-id="63e6e-112">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="63e6e-112">Example</span></span>

<span data-ttu-id="63e6e-113">Implemente una aplicación web desde una imagen de Docker en una aplicación web de Azure en Linux.</span><span class="sxs-lookup"><span data-stu-id="63e6e-113">Deploy a webapp from a Docker image into an Azure Web App running on Linux.</span></span>

```java
WebApp app = azure.webApps().define("newLinuxWebApp")
    .withExistingLinuxPlan(myLinuxAppServicePlan)
    .withExistingResourceGroup("myResourceGroup")
    .withPrivateDockerHubImage("username/my-java-app")
    .withCredentials("dockerHubUser","dockerHubPassword")
    .withAppSetting("PORT","8080").
    .create();
```

## <a name="samples"></a><span data-ttu-id="63e6e-114">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="63e6e-114">Samples</span></span>

<span data-ttu-id="63e6e-115">[Implementación de una aplicación web desde FTP o GitHub][1]</span><span class="sxs-lookup"><span data-stu-id="63e6e-115">[Deploy a web app from FTP or GitHub][1]</span></span>  
<span data-ttu-id="63e6e-116">[Intercambio entre versiones de la aplicación con ranuras de implementación][2]</span><span class="sxs-lookup"><span data-stu-id="63e6e-116">[Swap between app versions with deployment slots][2]</span></span>  
<span data-ttu-id="63e6e-117">[Configuración de un dominio personalizado][3] </span><span class="sxs-lookup"><span data-stu-id="63e6e-117">[Configure a custom domain][3] </span></span>  
<span data-ttu-id="63e6e-118">[Escalado de una aplicación web en varias regiones][4]</span><span class="sxs-lookup"><span data-stu-id="63e6e-118">[Scale a web app across multiple regions][4]</span></span>   

<span data-ttu-id="63e6e-119">Ver más [código de Java de ejemplo para Azure App Service](https://azure.microsoft.com/resources/samples/?platform=java&term=appservice) que puede usar en sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="63e6e-119">Explore more [sample Java code for Azure App Service](https://azure.microsoft.com/resources/samples/?platform=java&term=appservice) you can use in your apps.</span></span>

[1]: ../docs-ref-conceptual/java-sdk-configure-webapp-sources.md
[2]: https://azure.microsoft.com/resources/samples/app-service-java-manage-staging-and-production-slots-for-web-apps/
[3]: https://azure.microsoft.com/resources/samples/app-service-java-manage-web-apps-with-custom-domains/
[4]: https://azure.microsoft.com/resources/samples/app-service-java-scale-web-apps-on-linux/
