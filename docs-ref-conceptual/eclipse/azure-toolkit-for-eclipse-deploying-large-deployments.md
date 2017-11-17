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
# <a name="deploying-large-deployments"></a><span data-ttu-id="43ee6-103">Implementación de implementaciones de gran tamaño</span><span class="sxs-lookup"><span data-stu-id="43ee6-103">Deploying Large Deployments</span></span>

<span data-ttu-id="43ee6-104">Si su implementación es demasiado grande para incluirse en la carpeta approot predeterminada, puede usar un recurso de almacenamiento local como la carpeta raíz de implementación para su JDK y el servidor de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="43ee6-104">If your deployment is too large to be contained in the default approot folder, you can use a local storage resource as the deployment root folder for your JDK and application server.</span></span>

## <a name="to-use-a-local-storage-resource-as-the-deployment-root-folder-for-large-deployments"></a><span data-ttu-id="43ee6-105">Para usar un recurso de almacenamiento local como la carpeta raíz de implementación para implementaciones grandes</span><span class="sxs-lookup"><span data-stu-id="43ee6-105">To use a local storage resource as the deployment root folder for large deployments</span></span>

1. <span data-ttu-id="43ee6-106">Cree un recurso de almacenamiento local nuevo.</span><span class="sxs-lookup"><span data-stu-id="43ee6-106">Create a new local storage resource.</span></span> <span data-ttu-id="43ee6-107">El nombre del recurso no importa.</span><span class="sxs-lookup"><span data-stu-id="43ee6-107">The name of the resource does not matter.</span></span> <span data-ttu-id="43ee6-108">Los recursos de almacenamiento se definen en el nivel de rol.</span><span class="sxs-lookup"><span data-stu-id="43ee6-108">Storage resources are defined at the role level.</span></span> <span data-ttu-id="43ee6-109">La forma más rápida de obtener acceso al cuadro de diálogo de configuración de almacenamiento local para el que podría crear un nuevo recurso de almacenamiento local es mediante los siguientes pasos: haga clic con el botón secundario en el rol en la vista del **Explorador de proyectos** (expandir el nodo del proyecto de Azure si no ve el rol), haga clic en **Azure** y luego haga clic en **Almacenamiento local**.</span><span class="sxs-lookup"><span data-stu-id="43ee6-109">The quickest way to access the local storage configuration dialog, from which you could create a new local storage resource, is by using the following steps: Right-click the role in the **Project Explorer** view (expand your Azure project node if you don't see the role), click **Azure**, and then click **Local Storage**.</span></span> <span data-ttu-id="43ee6-110">En el cuadro de diálogo **Almacenamiento local**, haga clic en **Agregar** para crear un recurso de almacenamiento local nuevo.</span><span class="sxs-lookup"><span data-stu-id="43ee6-110">Within the **Local Storage** dialog, click **Add** to create a new local storage resource.</span></span>

1. <span data-ttu-id="43ee6-111">Establezca el tamaño que quiera en un mínimo 2048 MB (cualquier tamaño menor podría producir los mismos problemas de tamaño de archivo que se encontraría en approot).</span><span class="sxs-lookup"><span data-stu-id="43ee6-111">Set the desired size to at least 2048 MB (anything less may cause the same file size problems as you would encounter in the approot).</span></span>

1. <span data-ttu-id="43ee6-112">Asegúrese de que la opción **Limpiar el contenido cuando se recicle la instancia de rol** está activada; esto le ayudará a evitar que la lógica de inicio de la implementación tenga conflictos con archivos ya existentes en el recurso cuando se recicle la instancia de rol.</span><span class="sxs-lookup"><span data-stu-id="43ee6-112">Ensure that **Clean the contents when the role instance is recycled** is checked; this will help prevent the deployment's startup logic from running into conflicts with pre-existing files in the resource when the role instance is recycled.</span></span>

1. <span data-ttu-id="43ee6-113">Asegúrese de que el valor de **Variable de entorno que almacena la ruta de acceso de directorio del recurso tras la implementación** se establece en la cadena **DEPLOYROOT**.</span><span class="sxs-lookup"><span data-stu-id="43ee6-113">Ensure that the **Environment variable storing the resource's directory path after deployment** value is set to the string **DEPLOYROOT**.</span></span> <span data-ttu-id="43ee6-114">Su cuadro de diálogo de recursos del almacenamiento local tendrá un aspecto similar al siguiente.</span><span class="sxs-lookup"><span data-stu-id="43ee6-114">Your local storage resource dialog will look similar to the following.</span></span>

   ![][ic667943]

<span data-ttu-id="43ee6-115">Como alternativa, si usa **DEPLOYROOT** como el *nombre* de su recurso local y no cambia el nombre de la variable de entorno generada automáticamente (que se establecerá en **DEPLOYROOT_PATH** en ese caso), eso funcionará también para su aplicación.</span><span class="sxs-lookup"><span data-stu-id="43ee6-115">Alternatively, if you use **DEPLOYROOT** as the *name* of your local resource and you do not change the automatically-generated environment variable name (which will be set to **DEPLOYROOT_PATH** in that case), that would work for your application as well.</span></span>

<span data-ttu-id="43ee6-116">Encontrará información adicional sobre la creación de un recurso de almacenamiento local en [Propiedades de almacenamiento local][Local storage properties].</span><span class="sxs-lookup"><span data-stu-id="43ee6-116">Additional information about creating a local storage resource can be found at [Local storage properties][Local storage properties].</span></span>

## <a name="next-steps"></a><span data-ttu-id="43ee6-117">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="43ee6-117">Next steps</span></span>

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
