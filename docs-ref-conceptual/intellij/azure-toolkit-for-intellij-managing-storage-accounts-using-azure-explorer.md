---
title: "Administración de cuentas de almacenamiento mediante Azure Explorer para IntelliJ"
description: "Obtenga información sobre cómo administrar las cuentas de Azure Storage mediante Azure Explorer para IntelliJ."
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
ms.openlocfilehash: f37ae653286af1e36d730bda713527caa7504ac0
ms.sourcegitcommit: 613c1ffd2e0279fc7a96fca98aa1809563f52ee1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="manage-storage-accounts-by-using-the-azure-explorer-for-intellij"></a><span data-ttu-id="ccdf1-103">Administración de cuentas de almacenamiento mediante Azure Explorer para IntelliJ</span><span class="sxs-lookup"><span data-stu-id="ccdf1-103">Manage storage accounts by using the Azure Explorer for IntelliJ</span></span>

<span data-ttu-id="ccdf1-104">Azure Explorer, que forma parte del kit de herramientas de Azure para IntelliJ, proporciona a los desarrolladores de Java una solución fácil de usar para la administración de cuentas de almacenamiento en su cuenta de Azure desde el entorno de desarrollo integrado de IntelliJ (IDE).</span><span class="sxs-lookup"><span data-stu-id="ccdf1-104">The Azure Explorer, which is part of the Azure Toolkit for IntelliJ, provides Java developers with an easy-to-use solution for managing storage accounts in their Azure account from inside the IntelliJ integrated development environment (IDE).</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-intellij-show-azure-explorer](../includes/azure-toolkit-for-intellij-show-azure-explorer.md)]

## <a name="create-a-storage-account-in-intellij"></a><span data-ttu-id="ccdf1-105">Creación de una cuenta de almacenamiento en IntelliJ</span><span class="sxs-lookup"><span data-stu-id="ccdf1-105">Create a storage account in IntelliJ</span></span>

<span data-ttu-id="ccdf1-106">Para crear una cuenta de almacenamiento con Azure Explorer, haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="ccdf1-106">To create a storage account by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="ccdf1-107">Inicie sesión en su cuenta de Azure siguiendo los pasos del artículo [Instrucciones de inicio de sesión del kit de herramientas de Azure para IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="ccdf1-107">Sign in to your Azure account by using the [Sign-in instructions for the Azure Toolkit for IntelliJ].</span></span> 

2. <span data-ttu-id="ccdf1-108">En la vista de **Azure Explorer**, expanda el nodo **Azure**, haga clic con el botón derecho en **Cuentas de almacenamiento** y, después, haga clic en **Crear cuenta de almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="ccdf1-108">In the **Azure Explorer** view, expand the **Azure** node, right-click **Storage Accounts**, and then click **Create Storage Account**.</span></span>

   ![Comando Crear cuenta de almacenamiento][CS01]

3. <span data-ttu-id="ccdf1-110">En el cuadro de diálogo**Crear cuenta de almacenamiento**, especifique las siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="ccdf1-110">In the **Create Storage Account** dialog box, specify the following options:</span></span>

   ![Cuadro de diálogo Crear nueva cuenta de almacenamiento][CS02]

   * <span data-ttu-id="ccdf1-112">**Nombre**: especifica el nombre para la nueva cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="ccdf1-112">**Name**: Specifies the name for the new storage account.</span></span>

   * <span data-ttu-id="ccdf1-113">**Tipo de cuenta**: especifica el tipo de cuenta de almacenamiento que se va a crear, por ejemplo, "Blob Storage".</span><span class="sxs-lookup"><span data-stu-id="ccdf1-113">**Account kind**: Specifies the type of storage account to create (for example, "Blob storage").</span></span> <span data-ttu-id="ccdf1-114">Para más información, consulte [Acerca de las cuentas de almacenamiento de Azure].</span><span class="sxs-lookup"><span data-stu-id="ccdf1-114">For more information, see [About Azure storage accounts].</span></span> 

   * <span data-ttu-id="ccdf1-115">**Rendimiento**: especifica la oferta de cuenta de almacenamiento que quiere usar del publicador seleccionado; por ejemplo, "Premium".</span><span class="sxs-lookup"><span data-stu-id="ccdf1-115">**Performance**: Specifies which storage account offering to use from the selected publisher (for example, "Premium").</span></span> <span data-ttu-id="ccdf1-116">Para obtener más información, consulte [Objetivos de escalabilidad y rendimiento de Azure Storage].</span><span class="sxs-lookup"><span data-stu-id="ccdf1-116">For more information, see [Azure storage scalability and performance targets].</span></span> 

   * <span data-ttu-id="ccdf1-117">**Replicación**: especifica la replicación para la cuenta de almacenamiento; por ejemplo, en "Redundancia de zona".</span><span class="sxs-lookup"><span data-stu-id="ccdf1-117">**Replication**: Specifies the replication for the storage account (for example, "Zone-Redundant").</span></span> <span data-ttu-id="ccdf1-118">Para obtener más información, vea el artículo de [replicación de Azure Storage].</span><span class="sxs-lookup"><span data-stu-id="ccdf1-118">For more information, see [Azure storage replication].</span></span> 

   * <span data-ttu-id="ccdf1-119">**Suscripción**: especifica la suscripción de Azure que quiere usar para la nueva cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="ccdf1-119">**Subscription**: Specifies the Azure subscription that you want to use for the new storage account.</span></span>

   * <span data-ttu-id="ccdf1-120">**Ubicación**: especifica la ubicación donde se creará la cuenta de almacenamiento; por ejemplo, "oeste de EE. UU.".</span><span class="sxs-lookup"><span data-stu-id="ccdf1-120">**Location**: Specifies the location where your storage account will be created (for example, "West US").</span></span>

   * <span data-ttu-id="ccdf1-121">**Grupo de recursos**: especifica el grupo de recursos para su máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ccdf1-121">**Resource Group**: Specifies the resource group for your virtual machine.</span></span> <span data-ttu-id="ccdf1-122">Seleccione una de las siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="ccdf1-122">Select one of the following options:</span></span>
      * <span data-ttu-id="ccdf1-123">**Crear nuevo**: especifica que quiere crear un nuevo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="ccdf1-123">**Create new**: Specifies that you want to create a new resource group.</span></span>
      * <span data-ttu-id="ccdf1-124">**Usar existente**: especifica que se va a elegir de una lista de grupos de recursos asociados a la cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="ccdf1-124">**Use existing**: Specifies that you will select from a list of resource groups that are associated with your Azure account.</span></span>

4. <span data-ttu-id="ccdf1-125">Cuando haya especificado todas las opciones anteriores, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="ccdf1-125">When you have specified all of the preceding options, click **OK**.</span></span>

## <a name="create-a-storage-container-in-intellij"></a><span data-ttu-id="ccdf1-126">Creación de un contenedor de almacenamiento en IntelliJ</span><span class="sxs-lookup"><span data-stu-id="ccdf1-126">Create a storage container in IntelliJ</span></span>

<span data-ttu-id="ccdf1-127">Para crear un contenedor de almacenamiento con Azure Explorer, haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="ccdf1-127">To create a storage container by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="ccdf1-128">En la vista de Azure Explorer, haga clic con el botón derecho en la cuenta de almacenamiento donde quiera crear un contenedor y, después, haga clic en **Crear contenedor de blobs**.</span><span class="sxs-lookup"><span data-stu-id="ccdf1-128">In the Azure Explorer view, right-click the storage account where you want to create a container, and then click **Create blob container**.</span></span>

   ![Comando Crear contenedor de blobs][CC01]

2. <span data-ttu-id="ccdf1-130">En el cuadro de diálogo **Crear contenedor de blobs**, especifique el nombre para el contenedor y, después, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="ccdf1-130">In the **Create blob container** dialog box, specify the name for your container, and then click **OK**.</span></span> <span data-ttu-id="ccdf1-131">Para obtener más información sobre la nomenclatura de contenedores de almacenamiento, vea [Asignar nombres y hacer referencia a contenedores, blobs y metadatos].</span><span class="sxs-lookup"><span data-stu-id="ccdf1-131">For more information about naming storage containers, see [Naming and referencing containers, blobs, and metadata].</span></span>

   ![Cuadro de diálogo Crear contenedor de almacenamiento][CC02]

## <a name="delete-a-storage-container-in-intellij"></a><span data-ttu-id="ccdf1-133">Eliminación de un contenedor de almacenamiento en IntelliJ</span><span class="sxs-lookup"><span data-stu-id="ccdf1-133">Delete a storage container in IntelliJ</span></span>

<span data-ttu-id="ccdf1-134">Para eliminar un contenedor de almacenamiento mediante Azure Explorer, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="ccdf1-134">To delete a storage container by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="ccdf1-135">En la vista de Azure Explorer, haga clic con el botón derecho en el contenedor de almacenamiento y, después, haga clic en **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="ccdf1-135">In the Azure Explorer view, right-click the storage container, and then click **Delete**.</span></span>

   ![Comando Eliminar contenedor de almacenamiento][DC01]

2. <span data-ttu-id="ccdf1-137">En la ventana confirmación, haga clic en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="ccdf1-137">In the confirmation window, click **Yes**.</span></span>

   ![Ventana de confirmación Eliminar contenedor de almacenamiento][DC02]

## <a name="delete-a-storage-account-in-intellij"></a><span data-ttu-id="ccdf1-139">Eliminación de una cuenta de almacenamiento en IntelliJ</span><span class="sxs-lookup"><span data-stu-id="ccdf1-139">Delete a storage account in IntelliJ</span></span>

<span data-ttu-id="ccdf1-140">Para crear una cuenta de almacenamiento con Azure Explorer, haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="ccdf1-140">To delete a storage account by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="ccdf1-141">En la vista de **Azure Explorer**, haga clic con el botón derecho en la cuenta de almacenamiento y seleccione **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="ccdf1-141">In the **Azure Explorer** view, right-click the storage account, and then select **Delete**.</span></span>

   ![Menú Eliminar cuenta de almacenamiento][DS01]

2. <span data-ttu-id="ccdf1-143">En la ventana confirmación, haga clic en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="ccdf1-143">In the confirmation window, click **Yes**.</span></span>

   ![Ventana de confirmación Eliminar cuenta de almacenamiento][DS02]

## <a name="next-steps"></a><span data-ttu-id="ccdf1-145">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ccdf1-145">Next steps</span></span>

<span data-ttu-id="ccdf1-146">Para obtener más información sobre las cuentas de Azure Storage, tamaños y precios, vea los siguientes recursos:</span><span class="sxs-lookup"><span data-stu-id="ccdf1-146">For more information about Azure storage accounts, sizes, and pricing, see the following resources:</span></span>

* <span data-ttu-id="ccdf1-147">[Introducción a Microsoft Azure Storage]</span><span class="sxs-lookup"><span data-stu-id="ccdf1-147">[Introduction to Microsoft Azure Storage]</span></span>
* <span data-ttu-id="ccdf1-148">[Acerca de las cuentas de almacenamiento de Azure]</span><span class="sxs-lookup"><span data-stu-id="ccdf1-148">[About Azure storage accounts]</span></span>
* <span data-ttu-id="ccdf1-149">Tamaños de cuentas de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="ccdf1-149">Azure storage-account sizes</span></span>
  * <span data-ttu-id="ccdf1-150">[Tamaños de las cuentas de almacenamiento de Windows en Azure]</span><span class="sxs-lookup"><span data-stu-id="ccdf1-150">[Sizes for Windows storage accounts in Azure]</span></span>
  * <span data-ttu-id="ccdf1-151">[Tamaños de las cuentas de almacenamiento de Linux en Azure]</span><span class="sxs-lookup"><span data-stu-id="ccdf1-151">[Sizes for Linux storage accounts in Azure]</span></span>
* <span data-ttu-id="ccdf1-152">Precios de las cuentas de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="ccdf1-152">Azure storage-account pricing</span></span>
  * <span data-ttu-id="ccdf1-153">[Precios de cuentas de almacenamiento de Windows]</span><span class="sxs-lookup"><span data-stu-id="ccdf1-153">[Windows storage-account pricing]</span></span>
  * <span data-ttu-id="ccdf1-154">[Precios de cuentas de almacenamiento de Linux]</span><span class="sxs-lookup"><span data-stu-id="ccdf1-154">[Linux storage-account pricing]</span></span>

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

<!-- URL List -->

[Instrucciones de inicio de sesión del kit de herramientas de Azure para IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Introducción a Microsoft Azure Storage]: /azure/storage/storage-introduction
[Acerca de las cuentas de almacenamiento de Azure]: /azure/storage/storage-create-storage-account
[replicación de Azure Storage]: /azure/storage/storage-redundancy
[Objetivos de escalabilidad y rendimiento de Azure Storage]: /azure/storage/storage-scalability-targets
[Asignar nombres y hacer referencia a contenedores, blobs y metadatos]: http://go.microsoft.com/fwlink/?LinkId=255555

[Tamaños de las cuentas de almacenamiento de Windows en Azure]: /azure/virtual-machines/virtual-machines-windows-sizes
[Tamaños de las cuentas de almacenamiento de Linux en Azure]: /azure/virtual-machines/virtual-machines-linux-sizes
[Precios de cuentas de almacenamiento de Windows]: /pricing/details/virtual-machines/windows/
[Precios de cuentas de almacenamiento de Linux]: /pricing/details/virtual-machines/linux/

<!-- IMG List -->

[CS01]: media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CS01.png
[CS02]: media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CS02.png
[CC01]: media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CC01.png
[CC02]: media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CC02.png

[DS01]: media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DS01.png
[DS02]: media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DS02.png
[DC01]: media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DC01.png
[DC02]: media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DC02.png
