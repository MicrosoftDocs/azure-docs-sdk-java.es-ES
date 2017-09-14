---
title: "Implementación de implementaciones de gran tamaño"
description: "Obtenga información sobre cómo realizar implementaciones grandes mediante el kit de herramientas de Azure para Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 5e18bace-5df0-4af8-ad86-6151ea8bd823
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 09/11/2017
ms.author: robmcm
ms.openlocfilehash: 0e367e74d038043f1626dbf19aab87db6451bc02
ms.sourcegitcommit: 256044d7cbce16dcb8dc4e195d0f63c10cb44d4e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/13/2017
---
# <a name="deploying-large-deployments"></a>Implementación de implementaciones de gran tamaño

Si su implementación es demasiado grande para incluirse en la carpeta approot predeterminada, puede usar un recurso de almacenamiento local como la carpeta raíz de implementación para su JDK y el servidor de aplicaciones.

## <a name="to-use-a-local-storage-resource-as-the-deployment-root-folder-for-large-deployments"></a>Para usar un recurso de almacenamiento local como la carpeta raíz de implementación para implementaciones grandes

1. Cree un recurso de almacenamiento local nuevo. El nombre del recurso no importa. Los recursos de almacenamiento se definen en el nivel de rol. La forma más rápida de obtener acceso al cuadro de diálogo de configuración de almacenamiento local para el que podría crear un nuevo recurso de almacenamiento local es mediante los siguientes pasos: haga clic con el botón secundario en el rol en la vista del **Explorador de proyectos** (expandir el nodo del proyecto de Azure si no ve el rol), haga clic en **Azure** y luego haga clic en **Almacenamiento local**. En el cuadro de diálogo **Almacenamiento local**, haga clic en **Agregar** para crear un recurso de almacenamiento local nuevo.

1. Establezca el tamaño que quiera en un mínimo 2048 MB (cualquier tamaño menor podría producir los mismos problemas de tamaño de archivo que se encontraría en approot).

1. Asegúrese de que la opción **Limpiar el contenido cuando se recicle la instancia de rol** está activada; esto le ayudará a evitar que la lógica de inicio de la implementación tenga conflictos con archivos ya existentes en el recurso cuando se recicle la instancia de rol.

1. Asegúrese de que el valor de **Variable de entorno que almacena la ruta de acceso de directorio del recurso tras la implementación** se establece en la cadena **DEPLOYROOT**. Su cuadro de diálogo de recursos del almacenamiento local tendrá un aspecto similar al siguiente.

   ![][ic667943]

Como alternativa, si usa **DEPLOYROOT** como el *nombre* de su recurso local y no cambia el nombre de la variable de entorno generada automáticamente (que se establecerá en **DEPLOYROOT_PATH** en ese caso), eso funcionará también para su aplicación.

Encontrará información adicional sobre la creación de un recurso de almacenamiento local en [Propiedades de almacenamiento local][Local storage properties].

## <a name="next-steps"></a>Pasos siguientes

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[Local storage properties]: http://go.microsoft.com/fwlink/?LinkID=699525#local_storage_properties

<!-- IMG List -->

[ic667943]: media/azure-toolkit-for-eclipse-deploying-large-deployments/ic667943.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn268601.aspx -->
