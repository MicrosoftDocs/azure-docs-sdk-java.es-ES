---
title: "Administración de instancias de Redis Cache mediante Azure Explorer para IntelliJ"
description: "Obtenga información acerca de cómo administrar instancias de Azure Redis Cache mediante Azure Explorer para IntelliJ."
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
ms.date: 11/01/2017
ms.author: robmcm
ms.openlocfilehash: b715ffb97a4ca2b13e8020d354341139be4be45b
ms.sourcegitcommit: 613c1ffd2e0279fc7a96fca98aa1809563f52ee1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="managing-redis-caches-using-the-azure-explorer-for-intellij"></a>Administración de instancias de Redis Cache mediante Azure Explorer para IntelliJ

Azure Explorer, que forma parte del kit de herramientas de Azure para IntelliJ, proporciona a los desarrolladores de Java una solución fácil de usar para la administración de instancias de Redis Cache en su cuenta de Azure desde el IDE de IntelliJ.

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-intellij-show-azure-explorer](../includes/azure-toolkit-for-intellij-show-azure-explorer.md)]

## <a name="create-a-redis-cache-by-using-intellij"></a>Creación de una instancia de Redis Cache mediante IntelliJ

Los siguientes pasos le guían en la creación de instancias de Redis Cache mediante Azure Explorer.

1. Inicie sesión en su cuenta de Azure siguiendo los pasos del artículo [Instrucciones de inicio de sesión del kit de herramientas de Azure para IntelliJ].

1. En la ventana de la herramienta **Azure Explorer**, expanda el nodo **Azure**, haga clic con el botón derecho en **Cachés en Redis** y luego haga clic en **Crear Redis Cache**.

   ![Creación de un menú de Redis Cache][CR01]

1. Cuando aparece el cuadro de diálogo **Nueva caché en Redis**, especifique las opciones siguientes:

   ![Creación del cuadro de diálogo Nueva caché en Redis][CR02]

   a. **Nombre DNS**: especifica el subdominio DNS para el nuevo Redis Cache, que se antepone a ".redis.cache.windows.net", por ejemplo *wingtiptoys.redis.cache.windows.net*.

   b. **Suscripción**: especifica la suscripción de Azure que quiere usar para la nueva cuenta Redis Cache.

   c. **Grupo de recursos**: Especifica el grupo de recursos para la instancia de Redis Cache. Debe elegir una de las siguientes opciones: 
      * **Crear nuevo**: especifica que quiere crear un nuevo grupo de recursos. 
      * **Usar existente**: especifica que se va a elegir de una lista de grupos de recursos asociados a la cuenta de Azure. 

   d. **Ubicación**: especifica la ubicación donde se creará la instancia de Redis Cache, por ejemplo, *oeste de EE. UU*.

   e. **Plan de tarifa**: especifica qué plan de tarifa usa Redis Cache. Esta configuración determina el número de conexiones del cliente. (Para más información, consulte [Precios de Redis Cache]).

   f. **Puerto sin SSL**: especifica si Redis Cache permite las conexiones sin SSL. De forma predeterminada, se permiten solo las conexiones SSL.

1. Cuando haya especificado toda la configuración de Redis Cache, haga clic en **Aceptar**.

Una vez creada la instancia de Redis Cache, se mostrará en Azure Explorer.

   ![Redis Cache en Azure Explorer][CR03]

> [!NOTE]
>
> Para más información acerca de cómo configurar Azure Redis Cache, consulte [Configuración de Azure Redis Cache].
>

## <a name="display-the-properties-for-your-redis-cache-in-intellij"></a>Mostrar las propiedades de Redis Cache en IntelliJ

1. En Azure Explorer, haga clic con el botón derecho en Redis Cache y, después, en **Mostrar propiedades**.

   ![Menú contextual de Azure Explorer para mostrar las propiedades de Redis Cache][SP01]

1. Azure Explorer muestra las propiedades de Redis Cache.

   ![Propiedades de caché en Redis][SP02]

## <a name="delete-your-redis-cache-by-using-intellij"></a>Eliminar Redis Cache con IntelliJ

1. En Azure Explorer, haga clic con el botón derecho en Redis Cache y, después, en **Eliminar**.

   ![Menú contextual de Azure Explorer para eliminar una instancia de Redis Cache][DE01]

1. Cuando se le pida que confirme la eliminación de Redis Cache, haga clic en **Sí**.

   ![Eliminar una instancia de Redis Cache][DE02]

## <a name="next-steps"></a>Pasos siguientes

Para más información acerca de Azure Redis Cache, opciones de configuración y precios, consulte los vínculos siguientes:

* [Azure Redis Cache]
* [Documentación de Redis Cache]
* [Precios de Redis Cache]
* [Configuración de Azure Redis Cache]

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

<!-- URL List -->

[Precios de Redis Cache]: https://azure.microsoft.com/pricing/details/cache/
[Azure Redis Cache]: https://azure.microsoft.com/services/cache/
[Documentación de Redis Cache]: /azure/redis-cache
[Configuración de Azure Redis Cache]: /azure/redis-cache/cache-configure
[Instrucciones de inicio de sesión del kit de herramientas de Azure para IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md

<!-- IMG List -->

[CR01]: media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/CR01.png
[CR02]: media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/CR02.png
[CR03]: media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/CR03.png

[SP01]: media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/SP01.png
[SP02]: media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/SP02.png

[DE01]: media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/DE01.png
[DE02]: media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/DE02.png
