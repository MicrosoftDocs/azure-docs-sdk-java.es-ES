---
title: Administración de máquinas virtuales mediante Azure Explorer para IntelliJ
description: Aprenda a administrar las máquinas virtuales de Azure mediante Azure Explorer para IntelliJ.
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
ms.openlocfilehash: 213efa7fc31705b0ffcba6f2fe40e7186a365fae
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/09/2018
ms.locfileid: "48893526"
---
# <a name="manage-virtual-machines-by-using-the-azure-explorer-for-intellij"></a><span data-ttu-id="1cd28-103">Administración de máquinas virtuales mediante Azure Explorer para IntelliJ</span><span class="sxs-lookup"><span data-stu-id="1cd28-103">Manage virtual machines by using the Azure Explorer for IntelliJ</span></span>

<span data-ttu-id="1cd28-104">Azure Explorer, que forma parte del kit de herramientas de Azure para IntelliJ, proporciona a los desarrolladores de Java una solución fácil de usar para la administración de máquinas virtuales en su cuenta de Azure desde el entorno de desarrollo integrado de IntelliJ (IDE).</span><span class="sxs-lookup"><span data-stu-id="1cd28-104">The Azure Explorer, which is part of the Azure Toolkit for IntelliJ, provides Java developers with an easy-to-use solution for managing virtual machines in their Azure account from inside the IntelliJ integrated development environment (IDE).</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-intellij-show-azure-explorer](../includes/azure-toolkit-for-intellij-show-azure-explorer.md)]

## <a name="create-a-virtual-machine-in-intellij"></a><span data-ttu-id="1cd28-105">Creación de una máquina virtual en IntelliJ</span><span class="sxs-lookup"><span data-stu-id="1cd28-105">Create a virtual machine in IntelliJ</span></span>

<span data-ttu-id="1cd28-106">Para crear una máquina virtual con Azure Explorer, haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="1cd28-106">To create a virtual machine by using the Azure Explorer, do the following:</span></span> 

1. <span data-ttu-id="1cd28-107">Inicie sesión en su cuenta de Azure siguiendo los pasos del artículo [Instrucciones de inicio de sesión del kit de herramientas de Azure para IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="1cd28-107">Sign in to your Azure account by using the steps in the [Sign-in instructions for the Azure Toolkit for IntelliJ] article.</span></span>

2. <span data-ttu-id="1cd28-108">En la vista **Azure Explorer**, expanda el nodo **Azure**, haga clic con el botón derecho en **Virtual Machines** y, luego, en **Crear máquina virtual**.</span><span class="sxs-lookup"><span data-stu-id="1cd28-108">In the **Azure Explorer** view, expand the **Azure** node, right-click **Virtual Machines**, and then click **Create VM**.</span></span> 

   <span data-ttu-id="1cd28-109">![El comando Crear máquina virtual][CR01]</span><span class="sxs-lookup"><span data-stu-id="1cd28-109">![The Create VM command][CR01]</span></span>  
    <span data-ttu-id="1cd28-110">El Asistente **para crear nueva máquina virtual** se abrirá.</span><span class="sxs-lookup"><span data-stu-id="1cd28-110">The **Create new Virtual Machine** wizard opens.</span></span>

3. <span data-ttu-id="1cd28-111">En la ventana **Elegir una suscripción**, seleccione su suscripción y, luego, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="1cd28-111">In the **Choose a Subscription** window, select your subscription, and then click **Next**.</span></span> 

   ![Ventana Elegir una suscripción][CR02]

4. <span data-ttu-id="1cd28-113">En la ventana **Seleccionar una imagen de máquina virtual**, escriba la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="1cd28-113">In the **Select a Virtual Machine Image** window, enter the following information:</span></span>

   * <span data-ttu-id="1cd28-114">**Ubicación**: especifica la ubicación donde se creará la máquina virtual (por ejemplo, *oeste de EE. UU.*).</span><span class="sxs-lookup"><span data-stu-id="1cd28-114">**Location**: Specifies where your virtual machine will be created (for example, *West US*).</span></span> 

   * <span data-ttu-id="1cd28-115">**Imagen recomendada**: especifica que elegirá una imagen de una lista abreviada de imágenes usadas con frecuencia.</span><span class="sxs-lookup"><span data-stu-id="1cd28-115">**Recommended image**: Specifies that you will choose an image from an abbreviated list of commonly used images.</span></span>

   * <span data-ttu-id="1cd28-116">**Imagen personalizada**: especifica que elegirá una imagen personalizada proporcionando la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="1cd28-116">**Custom image**: Specifies that you will choose a custom image by providing the following information:</span></span>

      * <span data-ttu-id="1cd28-117">**Publicador**: especifica el publicador que creó la imagen que se usará para crear la máquina virtual (por ejemplo, *Microsoft*).</span><span class="sxs-lookup"><span data-stu-id="1cd28-117">**Publisher**: Specifies the publisher that created the image that you will use for your virtual machine (for example, *Microsoft*).</span></span>

      * <span data-ttu-id="1cd28-118">**Oferta**: especifica la oferta de máquina virtual que quiere usar del publicador seleccionado (por ejemplo, *JDK*).</span><span class="sxs-lookup"><span data-stu-id="1cd28-118">**Offer**: Specifies the virtual machine offering to use from the selected publisher (for example, *JDK*).</span></span>

      * <span data-ttu-id="1cd28-119">**SKU**: especifica la referencia de almacén (SKU) que quiere usar de la oferta seleccionada (por ejemplo, *JDK_8*).</span><span class="sxs-lookup"><span data-stu-id="1cd28-119">**Sku**: Specifies the stockkeeping unit (SKU) to use from the selected offering (for example, *JDK_8*).</span></span>

      * <span data-ttu-id="1cd28-120">**N.º de versión**: especifica la versión que quiere usar de la SKU seleccionada.</span><span class="sxs-lookup"><span data-stu-id="1cd28-120">**Version #**: Specifies which version of the selected SKU to use.</span></span>

   ![La ventana Seleccionar una imagen de máquina virtual][CR03]

5. <span data-ttu-id="1cd28-122">Haga clic en **Next**.</span><span class="sxs-lookup"><span data-stu-id="1cd28-122">Click **Next**.</span></span> 

6. <span data-ttu-id="1cd28-123">En la pantalla **Configuración básica de máquina virtual**, escriba la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="1cd28-123">In the **Virtual Machine Basic Settings** window, enter the following information:</span></span>

   * <span data-ttu-id="1cd28-124">**Nombre de máquina virtual**: especifica el nombre de la nueva máquina virtual, que debe comenzar con una letra y contener solo letras, números y guiones.</span><span class="sxs-lookup"><span data-stu-id="1cd28-124">**Virtual machine name**: Specifies the name for your new virtual machine, which must start with a letter and contain only letters, numbers, and hyphens.</span></span>

   * <span data-ttu-id="1cd28-125">**Tamaño**: especifica el número de núcleos y la memoria que se asignará para la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="1cd28-125">**Size**: Specifies the number of cores and memory to allocate for your virtual machine.</span></span>

   * <span data-ttu-id="1cd28-126">**Nombre de usuario**: especifica la cuenta de administrador que se creará para administrar la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="1cd28-126">**User name**: Specifies the administrator account to create for managing your virtual machine.</span></span>

   * <span data-ttu-id="1cd28-127">**Contraseña** y **Confirmar**: especifica la contraseña de la cuenta de administrador.</span><span class="sxs-lookup"><span data-stu-id="1cd28-127">**Password** and **Confirm**: Specifies the password for your administrator account.</span></span>

   ![La ventana Configuración básica de máquina virtual][CR04]

7. <span data-ttu-id="1cd28-129">Haga clic en **Next**.</span><span class="sxs-lookup"><span data-stu-id="1cd28-129">Click **Next**.</span></span> 

8. <span data-ttu-id="1cd28-130">En la ventana **Recursos asociados**, escriba la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="1cd28-130">In the **Associated Resources** window, enter the following information:</span></span>

   * <span data-ttu-id="1cd28-131">**Grupo de recursos**: especifica el grupo de recursos para su máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="1cd28-131">**Resource group**: Specifies the resource group for your virtual machine.</span></span> <span data-ttu-id="1cd28-132">Seleccione una de las siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="1cd28-132">Select one of the following options:</span></span>
      * <span data-ttu-id="1cd28-133">**Crear nuevo**: especifica que quiere crear un nuevo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="1cd28-133">**Create new**: Specifies that you want to create a new resource group.</span></span>
      * <span data-ttu-id="1cd28-134">**Usar existente**: especifica que se quiere elegir de una lista de grupos de recursos asociados a la cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="1cd28-134">**Use existing**: Specifies that you want to select from a list of resource groups that are associated with your Azure account.</span></span>

       ![La ventana Recursos asociados][CR07]

   * <span data-ttu-id="1cd28-136">**Cuenta de almacenamiento**: especifica la cuenta de almacenamiento que se usará para almacenar la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="1cd28-136">**Storage account**: Specifies the storage account to use for storing your virtual machine.</span></span> <span data-ttu-id="1cd28-137">Puede usar una cuenta de almacenamiento o crear una.</span><span class="sxs-lookup"><span data-stu-id="1cd28-137">You can choose an existing storage account or create a new account.</span></span> <span data-ttu-id="1cd28-138">Si elige **Crear nuevo**, se mostrará el cuadro de diálogo siguiente:</span><span class="sxs-lookup"><span data-stu-id="1cd28-138">If you choose **Create New**, the following dialog box appears:</span></span>

      ![El cuadro de diálogo Crear cuenta de almacenamiento][CR05]

   * <span data-ttu-id="1cd28-140">**Red virtual** y **Subred**: especifica la red virtual y subred que se conectará la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="1cd28-140">**Virtual Network** and **Subnet**: Specifies the virtual network and subnet that your virtual machine will connect to.</span></span> <span data-ttu-id="1cd28-141">Puede usar una red y subred existentes, o puede crear una nueva red y subred.</span><span class="sxs-lookup"><span data-stu-id="1cd28-141">You can use an existing network and subnet, or you can create a new network and subnet.</span></span> <span data-ttu-id="1cd28-142">Si selecciona **Crear nuevo**, se mostrará el cuadro de diálogo siguiente:</span><span class="sxs-lookup"><span data-stu-id="1cd28-142">If you select **Create new**, the following dialog box appears:</span></span>

      ![Cuadro de diálogo Crear red virtual][CR06]

   * <span data-ttu-id="1cd28-144">**Dirección IP pública**: especifica una dirección IP externa para la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="1cd28-144">**Public IP address**: Specifies an external-facing IP address for your virtual machine.</span></span> <span data-ttu-id="1cd28-145">Puede crear una dirección IP o, si la máquina virtual no tiene una dirección IP pública, puede seleccionar **(Ninguno)**.</span><span class="sxs-lookup"><span data-stu-id="1cd28-145">You can choose to create a new IP address or, if your virtual machine will not have a public IP address, you can select **(None)**.</span></span> 

   * <span data-ttu-id="1cd28-146">**Grupo de seguridad de red**: especifica un firewall de red opcional para la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="1cd28-146">**Network security group**: Specifies an optional networking firewall for your virtual machine.</span></span> <span data-ttu-id="1cd28-147">Puede seleccionar un firewall o, si la máquina virtual no utiliza un firewall, puede seleccionar **(Ninguno)**.</span><span class="sxs-lookup"><span data-stu-id="1cd28-147">You can select an existing firewall or, if your virtual machine will not use a network firewall, you can select **(None)**.</span></span> 

   * <span data-ttu-id="1cd28-148">**Conjunto de disponibilidad**: especifica un conjunto de disponibilidad opcional al que puede pertenecer su máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="1cd28-148">**Availability set**: Specifies an optional availability set that your virtual machine can belong to.</span></span> <span data-ttu-id="1cd28-149">Puede seleccionar un conjunto de disponibilidad, crear uno o, si la máquina virtual no pertenece a un conjunto de disponibilidad, seleccionar **(Ninguno)**.</span><span class="sxs-lookup"><span data-stu-id="1cd28-149">You can select an existing availability set, create a new availability set or, if your virtual machine will not belong to an availability set, select **(None)**.</span></span>

9. <span data-ttu-id="1cd28-150">Haga clic en **Finalizar**</span><span class="sxs-lookup"><span data-stu-id="1cd28-150">Click **Finish**.</span></span>  
    <span data-ttu-id="1cd28-151">La nueva máquina virtual aparece en la ventana de la herramienta Azure Explorer.</span><span class="sxs-lookup"><span data-stu-id="1cd28-151">Your new virtual machine appears in the Azure Explorer tool window.</span></span> 

   ![Nueva máquina virtual en la vista de Azure Explorer][CR08]

## <a name="restart-a-virtual-machine-in-intellij"></a><span data-ttu-id="1cd28-153">Reinicio de una máquina virtual en IntelliJ</span><span class="sxs-lookup"><span data-stu-id="1cd28-153">Restart a virtual machine in IntelliJ</span></span>

<span data-ttu-id="1cd28-154">Para reiniciar una máquina virtual mediante Azure Explorer en IntelliJ, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="1cd28-154">To restart a virtual machine by using the Azure Explorer in IntelliJ, do the following:</span></span>

1. <span data-ttu-id="1cd28-155">En la vista **Azure Explorer**, haga clic con el botón derecho en la máquina virtual y elija **Reiniciar**.</span><span class="sxs-lookup"><span data-stu-id="1cd28-155">In the **Azure Explorer** view, right-click the virtual machine, and then select **Restart**.</span></span>

   ![El comando de reinicio de máquina virtual][RE01]

2. <span data-ttu-id="1cd28-157">En la ventana confirmación, haga clic en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="1cd28-157">In the confirmation window, click **Yes**.</span></span> 

   ![La ventana de confirmación de reinicio de máquina virtual][RE02]

## <a name="shut-down-a-virtual-machine-in-intellij"></a><span data-ttu-id="1cd28-159">Apagado de una máquina virtual en IntelliJ</span><span class="sxs-lookup"><span data-stu-id="1cd28-159">Shut down a virtual machine in IntelliJ</span></span>

<span data-ttu-id="1cd28-160">Para apagar una máquina virtual en funcionamiento con Azure Explorer en IntelliJ, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="1cd28-160">To shut down a running virtual machine by using the Azure Explorer in IntelliJ, do the following:</span></span>

1. <span data-ttu-id="1cd28-161">En la vista **Azure Explorer**, haga clic con el botón derecho en la máquina virtual y elija **Apagar**.</span><span class="sxs-lookup"><span data-stu-id="1cd28-161">In the **Azure Explorer** view, right-click the virtual machine, and then select **Shutdown**.</span></span>

   ![El comando de apagado de máquina virtual][SH01]

2. <span data-ttu-id="1cd28-163">En la ventana confirmación, haga clic en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="1cd28-163">In the confirmation window, click **Yes**.</span></span> 

   ![La ventana de confirmación de apagado de máquina virtual][SH02]

## <a name="delete-a-virtual-machine-in-intellij"></a><span data-ttu-id="1cd28-165">Eliminación de una máquina virtual en IntelliJ</span><span class="sxs-lookup"><span data-stu-id="1cd28-165">Delete a virtual machine in IntelliJ</span></span>

<span data-ttu-id="1cd28-166">Para eliminar una máquina virtual con Azure Explorer en IntelliJ, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="1cd28-166">To delete a virtual machine by using the Azure Explorer in IntelliJ, do the following:</span></span>

1. <span data-ttu-id="1cd28-167">En la vista **Azure Explorer**, haga clic con el botón derecho en la máquina virtual y elija **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="1cd28-167">In the **Azure Explorer** view, right-click the virtual machine, and then select **Delete**.</span></span>

   ![El comando de eliminación de máquina virtual][DE01]

2. <span data-ttu-id="1cd28-169">En la ventana confirmación, haga clic en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="1cd28-169">In the confirmation window, click **Yes**.</span></span> 

   ![La ventana de confirmación de eliminación de máquina virtual][DE02]

## <a name="next-steps"></a><span data-ttu-id="1cd28-171">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1cd28-171">Next steps</span></span>

<span data-ttu-id="1cd28-172">Para obtener más información sobre los tamaños y los precios de máquinas virtuales de Azure, consulte los siguientes vínculos:</span><span class="sxs-lookup"><span data-stu-id="1cd28-172">For more information about Azure virtual-machine sizes and pricing, see the following resources:</span></span>

* <span data-ttu-id="1cd28-173">Tamaños de máquinas virtuales de Azure</span><span class="sxs-lookup"><span data-stu-id="1cd28-173">Azure virtual-machine sizes</span></span>
  * <span data-ttu-id="1cd28-174">[Tamaños de las máquinas virtuales Windows en Azure]</span><span class="sxs-lookup"><span data-stu-id="1cd28-174">[Sizes for Windows virtual machines in Azure]</span></span>
  * <span data-ttu-id="1cd28-175">[Tamaños de las máquinas virtuales Linux en Azure]</span><span class="sxs-lookup"><span data-stu-id="1cd28-175">[Sizes for Linux virtual machines in Azure]</span></span>
* <span data-ttu-id="1cd28-176">Precios de máquinas virtuales de Azure</span><span class="sxs-lookup"><span data-stu-id="1cd28-176">Azure virtual-machine pricing</span></span>
  * <span data-ttu-id="1cd28-177">[Precios de máquinas virtuales Windows]</span><span class="sxs-lookup"><span data-stu-id="1cd28-177">[Windows virtual-machine pricing]</span></span>
  * <span data-ttu-id="1cd28-178">[Precios de máquinas virtuales Linux]</span><span class="sxs-lookup"><span data-stu-id="1cd28-178">[Linux virtual-machine pricing]</span></span>

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

<!-- URL List -->

[Instrucciones de inicio de sesión del kit de herramientas de Azure para IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Sign-in instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Tamaños de las máquinas virtuales Windows en Azure]: /azure/virtual-machines/virtual-machines-windows-sizes
[Sizes for Windows virtual machines in Azure]: /azure/virtual-machines/virtual-machines-windows-sizes
[Tamaños de las máquinas virtuales Linux en Azure]: /azure/virtual-machines/virtual-machines-linux-sizes
[Sizes for Linux virtual machines in Azure]: /azure/virtual-machines/virtual-machines-linux-sizes
[Precios de máquinas virtuales Windows]: /pricing/details/virtual-machines/windows/
[Windows virtual-machine pricing]: /pricing/details/virtual-machines/windows/
[Precios de máquinas virtuales Linux]: /pricing/details/virtual-machines/linux/
[Linux virtual-machine pricing]: /pricing/details/virtual-machines/linux/

<!-- IMG List -->

[RE01]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/RE01.png
[RE02]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/RE02.png

[SH01]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/SH01.png
[SH02]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/SH02.png

[DE01]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/DE01.png
[DE02]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/DE02.png

[CR01]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR01.png
[CR02]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR02.png
[CR03]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR03.png
[CR04]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR04.png
[CR05]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR05.png
[CR06]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR06.png
[CR07]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR07.png
[CR08]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR08.png
