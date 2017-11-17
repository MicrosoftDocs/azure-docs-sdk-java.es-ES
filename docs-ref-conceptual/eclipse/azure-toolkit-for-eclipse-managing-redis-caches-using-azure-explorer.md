---
title: "Managing Redis Caches using the Azure Explorer for Eclipse (Administración de Redis Cache mediante Azure Explorer para Eclipse)"
description: "Obtenga información acerca de cómo administrar Azure Redis Cache mediante Azure Explorer para Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 09/11/2017
ms.author: robmcm
ms.openlocfilehash: 64b9fefd202128eb0afc95be720619fd6e534958
ms.sourcegitcommit: 256044d7cbce16dcb8dc4e195d0f63c10cb44d4e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/13/2017
---
# <a name="managing-redis-caches-using-the-azure-explorer-for-eclipse"></a><span data-ttu-id="ad6c2-103">Managing Redis Caches using the Azure Explorer for Eclipse (Administración de Redis Cache mediante Azure Explorer para Eclipse)</span><span class="sxs-lookup"><span data-stu-id="ad6c2-103">Managing Redis Caches using the Azure Explorer for Eclipse</span></span>

<span data-ttu-id="ad6c2-104">Azure Explorer, que forma parte del kit de herramientas de Azure para Eclipse, proporciona a los desarrolladores de Java una solución fácil de usar para la administración de Redis Cache en su cuenta de Azure desde el IDE de Eclipse.</span><span class="sxs-lookup"><span data-stu-id="ad6c2-104">The Azure Explorer, which is part of the Azure Toolkit for Eclipse, provides Java developers with an easy-to-use solution for managing redis caches in their Azure account from inside the Eclipse IDE.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="create-a-redis-cache-by-using-eclipse"></a><span data-ttu-id="ad6c2-105">Creación de Redis Cache mediante una Eclipse</span><span class="sxs-lookup"><span data-stu-id="ad6c2-105">Create a Redis Cache by using Eclipse</span></span>

<span data-ttu-id="ad6c2-106">Los siguientes pasos le guían en la creación de instancias de Redis Cache mediante Azure Explorer.</span><span class="sxs-lookup"><span data-stu-id="ad6c2-106">The following steps walk you through the steps to create a redis cache using the Azure Explorer.</span></span>

1. <span data-ttu-id="ad6c2-107">Inicie sesión en su cuenta de Azure siguiendo los pasos del artículo [Instrucciones de inicio de sesión del kit de herramientas de Azure para Eclipse].</span><span class="sxs-lookup"><span data-stu-id="ad6c2-107">Sign in to your Azure account using the steps in the [Sign In Instructions for the Azure Toolkit for Eclipse] article.</span></span>

1. <span data-ttu-id="ad6c2-108">En la ventana de la herramienta **Azure Explorer**, expanda el nodo **Azure**, haga clic con el botón derecho en **Cachés en Redis** y luego haga clic en **Crear Redis Cache**.</span><span class="sxs-lookup"><span data-stu-id="ad6c2-108">In the **Azure Explorer** tool window, expand the **Azure** node, right-click **Redis Caches**, and then click **Create Redis Cache**.</span></span>

   ![Creación de un menú de Redis Cache][CR01]

1. <span data-ttu-id="ad6c2-110">Cuando aparece el cuadro de diálogo **Nueva caché en Redis**, especifique las opciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="ad6c2-110">When the **New Redis Cache** dialog box appears, specify the following options:</span></span>

   ![Creación del cuadro de diálogo Nueva caché en Redis][CR02]

   <span data-ttu-id="ad6c2-112">a.</span><span class="sxs-lookup"><span data-stu-id="ad6c2-112">a.</span></span> <span data-ttu-id="ad6c2-113">**Nombre DNS**: Especifica el subdominio DNS para el nuevo Redis Cache, que se antepone a ".redis.cache.windows.net", por ejemplo *wingtiptoys.redis.cache.windows.net*.</span><span class="sxs-lookup"><span data-stu-id="ad6c2-113">**DNS Name**: Specifies the DNS subdomain for the new redis cache, which is prepended to ".redis.cache.windows.net"; for example: *wingtiptoys.redis.cache.windows.net*.</span></span>

   <span data-ttu-id="ad6c2-114">b.</span><span class="sxs-lookup"><span data-stu-id="ad6c2-114">b.</span></span> <span data-ttu-id="ad6c2-115">**Suscripción**: especifica la suscripción de Azure que quiere usar para la nueva cuenta Redis Cache.</span><span class="sxs-lookup"><span data-stu-id="ad6c2-115">**Subscription**: Specifies the Azure subscription you want to use for the new redis cache.</span></span>

   <span data-ttu-id="ad6c2-116">c.</span><span class="sxs-lookup"><span data-stu-id="ad6c2-116">c.</span></span> <span data-ttu-id="ad6c2-117">**Grupo de recursos**: Especifica el grupo de recursos para la instancia de Redis Cache. Debe elegir una de las siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="ad6c2-117">**Resource Group**: Specifies the resource group for your redis cache; you need to choose one of the following options:</span></span>
      * <span data-ttu-id="ad6c2-118">**Crear nuevo**: especifica que quiere crear un nuevo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="ad6c2-118">**Create New**: Specifies that you want to create a new resource group.</span></span>
      * <span data-ttu-id="ad6c2-119">**Usar existente**: especifica que se va a elegir de una lista de grupos de recursos asociados a la cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="ad6c2-119">**Use Existing**: Specifies that you will choose from a list of resource groups associated with your Azure account.</span></span>

   <span data-ttu-id="ad6c2-120">d.</span><span class="sxs-lookup"><span data-stu-id="ad6c2-120">d.</span></span> <span data-ttu-id="ad6c2-121">**Ubicación**: especifica la ubicación donde se creará la instancia de Redis Cache, por ejemplo, *oeste de EE. UU*.</span><span class="sxs-lookup"><span data-stu-id="ad6c2-121">**Location**: Specifies the location where your redis cache is created; for example, *West US*.</span></span>

   <span data-ttu-id="ad6c2-122">e.</span><span class="sxs-lookup"><span data-stu-id="ad6c2-122">e.</span></span> <span data-ttu-id="ad6c2-123">**Plan de tarifa**: especifica qué plan de tarifa usa Redis Cache. Esta configuración determina el número de conexiones del cliente.</span><span class="sxs-lookup"><span data-stu-id="ad6c2-123">**Pricing Tier**: Specifies which pricing tier your redis cache uses; this setting determines the number of client connections.</span></span> <span data-ttu-id="ad6c2-124">(Para más información, consulte [Precios de Redis Cache]).</span><span class="sxs-lookup"><span data-stu-id="ad6c2-124">(For more information, see [Redis Cache Pricing].)</span></span>

   <span data-ttu-id="ad6c2-125">f.</span><span class="sxs-lookup"><span data-stu-id="ad6c2-125">f.</span></span> <span data-ttu-id="ad6c2-126">**Puerto sin SSL**: especifica si Redis Cache permite las conexiones sin SSL. De forma predeterminada, se permiten solo las conexiones SSL.</span><span class="sxs-lookup"><span data-stu-id="ad6c2-126">**Non-SSL port**: Specifies whether your redis cache allows non-SSL connections; by default, only SSL connections are allowed.</span></span>

1. <span data-ttu-id="ad6c2-127">Cuando haya especificado toda la configuración de Redis Cache, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="ad6c2-127">When you have specified all your redis cache settings, click **OK**.</span></span>

<span data-ttu-id="ad6c2-128">Una vez creada la instancia de Redis Cache, se mostrará en Azure Explorer.</span><span class="sxs-lookup"><span data-stu-id="ad6c2-128">After your redis cache has been created, it will be displayed in the Azure Explorer.</span></span>

   ![Redis Cache en Azure Explorer][CR03]

> [!NOTE]
>
> <span data-ttu-id="ad6c2-130">Para más información acerca de cómo configurar Azure Redis Cache, consulte [Configuración de Azure Redis Cache].</span><span class="sxs-lookup"><span data-stu-id="ad6c2-130">For more information about configuring your Azure redis cache settings, see [How to configure Azure Redis Cache].</span></span>
>

## <a name="display-the-properties-for-your-redis-cache-in-eclipse"></a><span data-ttu-id="ad6c2-131">Mostrar las propiedades de Redis Cache en Eclipse</span><span class="sxs-lookup"><span data-stu-id="ad6c2-131">Display the properties for your Redis Cache in Eclipse</span></span>

1. <span data-ttu-id="ad6c2-132">En Azure Explorer, haga clic con el botón derecho en Redis Cache y, después, en **Mostrar propiedades**.</span><span class="sxs-lookup"><span data-stu-id="ad6c2-132">In the Azure Explorer, right-click your redis cache and click **Show properties**.</span></span>

   ![Menú contextual de Azure Explorer para mostrar las propiedades de Redis Cache][SP01]

1. <span data-ttu-id="ad6c2-134">Azure Explorer muestra las propiedades de Redis Cache.</span><span class="sxs-lookup"><span data-stu-id="ad6c2-134">The Azure Explorer displays the properties for your redis cache.</span></span>

   ![Propiedades de caché en Redis][SP02]

## <a name="delete-your-redis-cache-by-using-eclipse"></a><span data-ttu-id="ad6c2-136">Eliminación de Redis Cache con Eclipse</span><span class="sxs-lookup"><span data-stu-id="ad6c2-136">Delete your Redis Cache by using Eclipse</span></span>

1. <span data-ttu-id="ad6c2-137">En Azure Explorer, haga clic con el botón derecho en Redis Cache y, después, en **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="ad6c2-137">In the Azure Explorer, right-click your redis cache and click **Delete**.</span></span>

   ![Menú contextual de Azure Explorer para eliminar una instancia de Redis Cache][DE01]

1. <span data-ttu-id="ad6c2-139">Cuando se le pida que confirme la eliminación de Redis Cache, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="ad6c2-139">Click **OK** when prompted to delete your redis cache.</span></span>

   ![Eliminar una instancia de Redis Cache][DE02]

## <a name="next-steps"></a><span data-ttu-id="ad6c2-141">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ad6c2-141">Next steps</span></span>

<span data-ttu-id="ad6c2-142">Para más información acerca de Azure Redis Cache, opciones de configuración y precios, consulte los vínculos siguientes:</span><span class="sxs-lookup"><span data-stu-id="ad6c2-142">For more information about Azure redis caches, configuration settings and pricing, see the following links:</span></span>

* <span data-ttu-id="ad6c2-143">[Azure Redis Cache]</span><span class="sxs-lookup"><span data-stu-id="ad6c2-143">[Azure Redis Cache]</span></span>
* <span data-ttu-id="ad6c2-144">[Documentación de Redis Cache]</span><span class="sxs-lookup"><span data-stu-id="ad6c2-144">[Redis Cache Documentation]</span></span>
* <span data-ttu-id="ad6c2-145">[Precios de Redis Cache]</span><span class="sxs-lookup"><span data-stu-id="ad6c2-145">[Redis Cache Pricing]</span></span>
* <span data-ttu-id="ad6c2-146">[Configuración de Azure Redis Cache]</span><span class="sxs-lookup"><span data-stu-id="ad6c2-146">[How to configure Azure Redis Cache]</span></span>

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<!-- URL List -->

[Precios de Redis Cache]: https://azure.microsoft.com/pricing/details/cache/
[Azure Redis Cache]: https://azure.microsoft.com/services/cache/
[Documentación de Redis Cache]: /azure/redis-cache/
[Configuración de Azure Redis Cache]: /azure/redis-cache/cache-configure

<!-- IMG List -->

[CR01]: media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/CR01.png
[CR02]: media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/CR02.png
[CR03]: media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/CR03.png

[SP01]: media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/SP01.png
[SP02]: media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/SP02.png

[DE01]: media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/DE01.png
[DE02]: media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/DE02.png
