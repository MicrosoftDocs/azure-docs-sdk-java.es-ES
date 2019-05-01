---
title: Ejemplos de aplicaciones web de las bibliotecas de administración de Azure para Java
description: Obtenga código de ejemplo para la creación y actualización de aplicaciones web hospedadas en Azure App Service mediante las bibliotecas de administración de Azure para Java.
keywords: Azure, Java, SDK, API, Maven, Gradle, aplicaciones web, servicio de aplicaciones
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 04/16/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: multiple
ms.assetid: 43633e5c-9fb1-4807-ba63-e24c126754e2
ms.openlocfilehash: be4031059587ceb88f6824356f677c37a198de80
ms.sourcegitcommit: 115f4c8ad07a11f17d79e9d945d63917836b11c8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "61592590"
---
# <a name="azure-management-libraries-for-java-samples-for-web-apps"></a><span data-ttu-id="94d2d-104">Ejemplos de aplicaciones web para las bibliotecas de administración de Azure para Java</span><span class="sxs-lookup"><span data-stu-id="94d2d-104">Azure management libraries for Java samples for web apps</span></span>

| <span data-ttu-id="94d2d-105">**Creación de una aplicación**</span><span class="sxs-lookup"><span data-stu-id="94d2d-105">**Create an app**</span></span> ||
|---|---|
| <span data-ttu-id="94d2d-106">[Creación de una aplicación web e implementación desde FTP o GitHub][1]</span><span class="sxs-lookup"><span data-stu-id="94d2d-106">[Create a web app and deploy from FTP or GitHub][1]</span></span> | <span data-ttu-id="94d2d-107">Implemente aplicaciones web desde Git local o FTP e integración continua desde GitHub.</span><span class="sxs-lookup"><span data-stu-id="94d2d-107">Deploy web apps from local Git, FTP, and continuous integration from GitHub.</span></span> |
| <span data-ttu-id="94d2d-108">[Creación de una aplicación web y administración de los espacios de implementación][2]</span><span class="sxs-lookup"><span data-stu-id="94d2d-108">[Create a web app and manage deployment slots][2]</span></span> | <span data-ttu-id="94d2d-109">Cree una aplicación web, implemente en espacios de ensayo y, después, intercambie las implementaciones entre los espacios.</span><span class="sxs-lookup"><span data-stu-id="94d2d-109">Create a web app and deploy to staging slots, and then swap deployments between slots.</span></span> |
| <span data-ttu-id="94d2d-110">**Configuración de la aplicación**</span><span class="sxs-lookup"><span data-stu-id="94d2d-110">**Configure app**</span></span> ||
| <span data-ttu-id="94d2d-111">[Creación de una aplicación web y configuración de un dominio personalizado][3]</span><span class="sxs-lookup"><span data-stu-id="94d2d-111">[Create a web app and configure a custom domain][3]</span></span> | <span data-ttu-id="94d2d-112">Cree una aplicación web con un dominio personalizado y un certificado SSL autofirmado.</span><span class="sxs-lookup"><span data-stu-id="94d2d-112">Create a web app with a custom domain and self-signed SSL certificate.</span></span> |
| <span data-ttu-id="94d2d-113">**Escalado de aplicaciones**</span><span class="sxs-lookup"><span data-stu-id="94d2d-113">**Scale apps**</span></span> ||
| <span data-ttu-id="94d2d-114">[Escalado de una aplicación web con alta disponibilidad en varias regiones][4]</span><span class="sxs-lookup"><span data-stu-id="94d2d-114">[Scale a web app with high availability across multiple regions][4]</span></span> | <span data-ttu-id="94d2d-115">Escale una aplicación web en tres regiones geográficas diferentes y haga que estén disponibles a través de un punto de conexión único mediante Azure Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="94d2d-115">Scale a web app in three different geographical regions and make them available through a single endpoint using Azure Traffic Manager.</span></span> | 
| <span data-ttu-id="94d2d-116">**Conexión de la aplicación a recursos**</span><span class="sxs-lookup"><span data-stu-id="94d2d-116">**Connect app to resources**</span></span> ||
| <span data-ttu-id="94d2d-117">[Conexión de una aplicación web a una cuenta de almacenamiento][5]</span><span class="sxs-lookup"><span data-stu-id="94d2d-117">[Connect a web app to a storage account][5]</span></span> | <span data-ttu-id="94d2d-118">Cree una cuenta de Azure Storage y agregue la cadena de conexión de la cuenta a la configuración de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="94d2d-118">Create an Azure storage account and add the storage account connection string to the app settings.</span></span> |
| <span data-ttu-id="94d2d-119">[Conexión de una aplicación web a una base de datos SQL][6]</span><span class="sxs-lookup"><span data-stu-id="94d2d-119">[Connect a web app to a SQL database][6]</span></span> | <span data-ttu-id="94d2d-120">Cree una aplicación web y una base de datos SQL y agregue la cadena de conexión de la base de datos SQL a la configuración de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="94d2d-120">Create a web app and SQL database, and then add the SQL database connection string to the app settings.</span></span> |

[1]: java-sdk-configure-webapp-sources.md
[2]: https://azure.microsoft.com/resources/samples/app-service-java-manage-staging-and-production-slots-for-web-apps/
[3]: https://azure.microsoft.com/resources/samples/app-service-java-manage-web-apps-with-custom-domains/
[4]: https://azure.microsoft.com/resources/samples/app-service-java-scale-web-apps-on-linux/
[5]: https://azure.microsoft.com/resources/samples/app-service-java-manage-storage-connections-for-web-apps/
[6]: https://azure.microsoft.com/resources/samples/app-service-java-manage-data-connections-for-web-apps/