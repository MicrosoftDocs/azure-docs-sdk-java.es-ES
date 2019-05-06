---
title: Managing Redis Caches using the Azure Explorer for Eclipse (Administración de Redis Cache mediante Azure Explorer para Eclipse)
description: Obtenga información acerca de cómo administrar Azure Redis Cache mediante Azure Explorer para Eclipse.
services: ''
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 02/01/2018
ms.devlang: Java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: 00f363e5dacc9c494b01eaa479db7e9e1aff6952
ms.sourcegitcommit: 4f1acf05e3bbb7eb6bca9b65300c1c5b9772185a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/24/2019
ms.locfileid: "63456044"
---
# <a name="managing-redis-caches-using-the-azure-explorer-for-eclipse"></a><span data-ttu-id="14a22-103">Managing Redis Caches using the Azure Explorer for Eclipse (Administración de Redis Cache mediante Azure Explorer para Eclipse)</span><span class="sxs-lookup"><span data-stu-id="14a22-103">Managing Redis Caches using the Azure Explorer for Eclipse</span></span>

<span data-ttu-id="14a22-104">Azure Explorer, que forma parte del kit de herramientas de Azure para Eclipse, proporciona a los desarrolladores de Java una solución fácil de usar para la administración de Redis Cache en su cuenta de Azure desde el IDE de Eclipse.</span><span class="sxs-lookup"><span data-stu-id="14a22-104">The Azure Explorer, which is part of the Azure Toolkit for Eclipse, provides Java developers with an easy-to-use solution for managing redis caches in their Azure account from inside the Eclipse IDE.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="create-a-redis-cache-by-using-eclipse"></a><span data-ttu-id="14a22-105">Creación de Redis Cache mediante una Eclipse</span><span class="sxs-lookup"><span data-stu-id="14a22-105">Create a Redis Cache by using Eclipse</span></span>

<span data-ttu-id="14a22-106">Los siguientes pasos le guían en la creación de instancias de Redis Cache mediante Azure Explorer.</span><span class="sxs-lookup"><span data-stu-id="14a22-106">The following steps walk you through the steps to create a redis cache using the Azure Explorer.</span></span>

1. <span data-ttu-id="14a22-107">Inicie sesión en su cuenta de Azure siguiendo los pasos del artículo [Instrucciones de inicio de sesión del kit de herramientas de Azure para Eclipse].</span><span class="sxs-lookup"><span data-stu-id="14a22-107">Sign in to your Azure account using the steps in the [Sign In Instructions for the Azure Toolkit for Eclipse] article.</span></span>

1. <span data-ttu-id="14a22-108">En la ventana de la herramienta **Azure Explorer**, expanda el nodo **Azure**, haga clic con el botón derecho en **Cachés en Redis** y luego haga clic en **Crear Redis Cache**.</span><span class="sxs-lookup"><span data-stu-id="14a22-108">In the **Azure Explorer** tool window, expand the **Azure** node, right-click **Redis Caches**, and then click **Create Redis Cache**.</span></span>

   ![Creación de un menú de Redis Cache][CR01]

1. <span data-ttu-id="14a22-110">Cuando aparece el cuadro de diálogo **Nueva caché en Redis**, especifique las opciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="14a22-110">When the **New Redis Cache** dialog box appears, specify the following options:</span></span>

   ![Creación del cuadro de diálogo Nueva caché en Redis][CR02]

   <span data-ttu-id="14a22-112"> a.</span><span class="sxs-lookup"><span data-stu-id="14a22-112">a.</span></span> <span data-ttu-id="14a22-113">**Nombre DNS**: especifica el subdominio DNS para el nuevo Redis Cache, que se antepone a ".redis.cache.windows.net", por ejemplo *wingtiptoys.redis.cache.windows.net*.</span><span class="sxs-lookup"><span data-stu-id="14a22-113">**DNS Name**: Specifies the DNS subdomain for the new redis cache, which is prepended to ".redis.cache.windows.net"; for example: *wingtiptoys.redis.cache.windows.net*.</span></span>

   <span data-ttu-id="14a22-114">b.</span><span class="sxs-lookup"><span data-stu-id="14a22-114">b.</span></span> <span data-ttu-id="14a22-115">**Suscripción**: especifica la suscripción de Azure que desea usar en la nueva instancia de Redis Cache.</span><span class="sxs-lookup"><span data-stu-id="14a22-115">**Subscription**: Specifies the Azure subscription you want to use for the new redis cache.</span></span>

   <span data-ttu-id="14a22-116">c.</span><span class="sxs-lookup"><span data-stu-id="14a22-116">c.</span></span> <span data-ttu-id="14a22-117">**Grupo de recursos**: especifica el grupo de recursos para la instancia de Redis Cache. Debe elegir una de las siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="14a22-117">**Resource Group**: Specifies the resource group for your redis cache; you need to choose one of the following options:</span></span>
      * <span data-ttu-id="14a22-118">**Crear nuevo**: especifica que quiere crear un nuevo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="14a22-118">**Create New**: Specifies that you want to create a new resource group.</span></span>
      * <span data-ttu-id="14a22-119">**Usar existente**: especifica que se va a elegir entre una lista de grupos de recursos asociados a la cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="14a22-119">**Use Existing**: Specifies that you will choose from a list of resource groups associated with your Azure account.</span></span>

   <span data-ttu-id="14a22-120">d.</span><span class="sxs-lookup"><span data-stu-id="14a22-120">d.</span></span> <span data-ttu-id="14a22-121">**Ubicación**: especifica la ubicación en la que se crea la instancia de Redis Cache, por ejemplo, *Oeste de EE. UU.*</span><span class="sxs-lookup"><span data-stu-id="14a22-121">**Location**: Specifies the location where your redis cache is created; for example, *West US*.</span></span>

   <span data-ttu-id="14a22-122">e.</span><span class="sxs-lookup"><span data-stu-id="14a22-122">e.</span></span> <span data-ttu-id="14a22-123">**Plan de tarifa**: especifica el plan de tarifa que usa Redis Cache. Este valor determina el número de conexiones del cliente.</span><span class="sxs-lookup"><span data-stu-id="14a22-123">**Pricing Tier**: Specifies which pricing tier your redis cache uses; this setting determines the number of client connections.</span></span> <span data-ttu-id="14a22-124">(Para más información, consulte [Precios de Redis Cache]).</span><span class="sxs-lookup"><span data-stu-id="14a22-124">(For more information, see [Redis Cache Pricing].)</span></span>

   <span data-ttu-id="14a22-125">f.</span><span class="sxs-lookup"><span data-stu-id="14a22-125">f.</span></span> <span data-ttu-id="14a22-126">**Puerto no SSL**: especifica si Redis Cache permite conexiones no SSL. De forma predeterminada, se permiten solo las conexiones SSL.</span><span class="sxs-lookup"><span data-stu-id="14a22-126">**Non-SSL port**: Specifies whether your redis cache allows non-SSL connections; by default, only SSL connections are allowed.</span></span>

1. <span data-ttu-id="14a22-127">Cuando haya especificado toda la configuración de Redis Cache, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="14a22-127">When you have specified all your redis cache settings, click **OK**.</span></span>

<span data-ttu-id="14a22-128">Una vez creada la instancia de Redis Cache, se mostrará en Azure Explorer.</span><span class="sxs-lookup"><span data-stu-id="14a22-128">After your redis cache has been created, it will be displayed in the Azure Explorer.</span></span>

   ![Redis Cache en Azure Explorer][CR03]

> [!NOTE]
>
> <span data-ttu-id="14a22-130">Para más información acerca de cómo configurar Azure Redis Cache, consulte [Configuración de Azure Redis Cache].</span><span class="sxs-lookup"><span data-stu-id="14a22-130">For more information about configuring your Azure redis cache settings, see [How to configure Azure Redis Cache].</span></span>
>

## <a name="display-the-properties-for-your-redis-cache-in-eclipse"></a><span data-ttu-id="14a22-131">Mostrar las propiedades de Redis Cache en Eclipse</span><span class="sxs-lookup"><span data-stu-id="14a22-131">Display the properties for your Redis Cache in Eclipse</span></span>

1. <span data-ttu-id="14a22-132">En Azure Explorer, haga clic con el botón derecho en Redis Cache y, después, en **Mostrar propiedades**.</span><span class="sxs-lookup"><span data-stu-id="14a22-132">In the Azure Explorer, right-click your redis cache and click **Show properties**.</span></span>

   ![Menú contextual de Azure Explorer para mostrar las propiedades de Redis Cache][SP01]

1. <span data-ttu-id="14a22-134">Azure Explorer muestra las propiedades de Redis Cache.</span><span class="sxs-lookup"><span data-stu-id="14a22-134">The Azure Explorer displays the properties for your redis cache.</span></span>

   ![Propiedades de caché en Redis][SP02]

## <a name="delete-your-redis-cache-by-using-eclipse"></a><span data-ttu-id="14a22-136">Eliminación de Redis Cache con Eclipse</span><span class="sxs-lookup"><span data-stu-id="14a22-136">Delete your Redis Cache by using Eclipse</span></span>

1. <span data-ttu-id="14a22-137">En Azure Explorer, haga clic con el botón derecho en Redis Cache y, después, en **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="14a22-137">In the Azure Explorer, right-click your redis cache and click **Delete**.</span></span>

   ![Menú contextual de Azure Explorer para eliminar una instancia de Redis Cache][DE01]

1. <span data-ttu-id="14a22-139">Cuando se le pida que confirme la eliminación de Redis Cache, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="14a22-139">Click **OK** when prompted to delete your redis cache.</span></span>

   ![Eliminar una instancia de Redis Cache][DE02]

## <a name="next-steps"></a><span data-ttu-id="14a22-141">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="14a22-141">Next steps</span></span>

<span data-ttu-id="14a22-142">Para más información acerca de Azure Redis Cache, opciones de configuración y precios, consulte los vínculos siguientes:</span><span class="sxs-lookup"><span data-stu-id="14a22-142">For more information about Azure redis caches, configuration settings and pricing, see the following links:</span></span>

* <span data-ttu-id="14a22-143">[Azure Redis Cache]</span><span class="sxs-lookup"><span data-stu-id="14a22-143">[Azure Redis Cache]</span></span>
* <span data-ttu-id="14a22-144">[Documentación de Redis Cache]</span><span class="sxs-lookup"><span data-stu-id="14a22-144">[Redis Cache Documentation]</span></span>
* <span data-ttu-id="14a22-145">[Precios de Redis Cache]</span><span class="sxs-lookup"><span data-stu-id="14a22-145">[Redis Cache Pricing]</span></span>
* <span data-ttu-id="14a22-146">[Configuración de Azure Redis Cache]</span><span class="sxs-lookup"><span data-stu-id="14a22-146">[How to configure Azure Redis Cache]</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<!-- URL List -->

[Precios de Redis Cache]: https://azure.microsoft.com/pricing/details/cache/
[Redis Cache Pricing]: https://azure.microsoft.com/pricing/details/cache/
[Azure Redis Cache]: https://azure.microsoft.com/services/cache/
[Documentación de Redis Cache]: /azure/redis-cache/
[Redis Cache Documentation]: /azure/redis-cache/
[Configuración de Azure Redis Cache]: /azure/redis-cache/cache-configure
[How to configure Azure Redis Cache]: /azure/redis-cache/cache-configure

<!-- IMG List -->

[CR01]: media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/CR01.png
[CR02]: media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/CR02.png
[CR03]: media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/CR03.png

[SP01]: media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/SP01.png
[SP02]: media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/SP02.png

[DE01]: media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/DE01.png
[DE02]: media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/DE02.png
