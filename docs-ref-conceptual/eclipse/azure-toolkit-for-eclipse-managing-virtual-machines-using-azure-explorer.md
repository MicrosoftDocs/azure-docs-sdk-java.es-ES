---
title: Administración de máquinas virtuales con Azure Explorer para Eclipse
description: Obtenga información sobre cómo administrar máquinas virtuales de Azure mediante Azure Explorer para Eclipse.
services: ''
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 11/13/2018
ms.devlang: Java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: 53dfbfb0de2bcb56ebfc4d5ca2c4c19528edcfbf
ms.sourcegitcommit: 8d0c59ae7c91adbb9be3c3e6d4a3429ffe51519d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/27/2018
ms.locfileid: "52338699"
---
# <a name="manage-virtual-machines-by-using-the-azure-explorer-for-eclipse"></a><span data-ttu-id="c6464-103">Administración de máquinas virtuales con Azure Explorer para Eclipse</span><span class="sxs-lookup"><span data-stu-id="c6464-103">Manage virtual machines by using the Azure Explorer for Eclipse</span></span>

<span data-ttu-id="c6464-104">Azure Explorer, que forma parte del kit de herramientas de Azure para Eclipse, proporciona a los desarrolladores de Java una solución fácil de usar para la administración de máquinas virtuales en su cuenta de Azure desde el entorno de desarrollo integrado de Eclipse (IDE).</span><span class="sxs-lookup"><span data-stu-id="c6464-104">The Azure Explorer, which is part of the Azure Toolkit for Eclipse, provides Java developers with an easy-to-use solution for managing virtual machines in their Azure account from inside the Eclipse integrated development environment (IDE).</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="create-a-virtual-machine-in-eclipse"></a><span data-ttu-id="c6464-105">Creación de una máquina virtual en Eclipse</span><span class="sxs-lookup"><span data-stu-id="c6464-105">Create a virtual machine in Eclipse</span></span>

<span data-ttu-id="c6464-106">Para crear una máquina virtual con Azure Explorer, haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="c6464-106">To create a virtual machine by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="c6464-107">Inicie sesión en su cuenta de Azure siguiendo los pasos del artículo [Instrucciones de inicio de sesión del kit de herramientas de Azure para Eclipse](https://docs.microsoft.com/java/azure/eclipse/azure-toolkit-for-eclipse-sign-in-instructions).</span><span class="sxs-lookup"><span data-stu-id="c6464-107">Sign in to your Azure account by using the [Sign-in instructions for the Azure Toolkit for Eclipse](https://docs.microsoft.com/java/azure/eclipse/azure-toolkit-for-eclipse-sign-in-instructions).</span></span>

2. <span data-ttu-id="c6464-108">En la vista **Azure Explorer**, expanda el nodo **Azure**, haga clic con el botón derecho en **Virtual Machines** y, luego, en **Crear máquina virtual**.</span><span class="sxs-lookup"><span data-stu-id="c6464-108">In the **Azure Explorer** view, expand the **Azure** node, right-click **Virtual Machines**, and then click **Create VM**.</span></span>

   ![Comando Crear máquina virtual][CR01]  

   <span data-ttu-id="c6464-110">El Asistente **para crear nueva máquina virtual** se abrirá.</span><span class="sxs-lookup"><span data-stu-id="c6464-110">The **Create new Virtual Machine** wizard opens.</span></span>

3. <span data-ttu-id="c6464-111">En la ventana **Elegir una suscripción**, seleccione su suscripción y, luego, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="c6464-111">In the **Choose a Subscription** window, select your subscription, and then click **Next**.</span></span>

   ![Ventana Elegir una suscripción][CR02]

4. <span data-ttu-id="c6464-113">En la ventana **Seleccionar una imagen de máquina virtual**, escriba la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="c6464-113">In the **Select a Virtual Machine Image** window, enter the following information:</span></span>

   * <span data-ttu-id="c6464-114">**Ubicación**: especifica la ubicación donde se creará la máquina virtual (por ejemplo, *oeste de EE. UU.*).</span><span class="sxs-lookup"><span data-stu-id="c6464-114">**Location**: Specifies where your virtual machine will be created (for example, *West US*).</span></span>

   * <span data-ttu-id="c6464-115">**Publicador**: especifica el publicador que creó la imagen que se usará para crear la máquina virtual (por ejemplo, *Microsoft*).</span><span class="sxs-lookup"><span data-stu-id="c6464-115">**Publisher**: Specifies the publisher that created the image you'll use to create your virtual machine (for example, *Microsoft*).</span></span>

   * <span data-ttu-id="c6464-116">**Oferta**: especifica la oferta de máquina virtual que quiere usar del publicador seleccionado (por ejemplo, *JDK*).</span><span class="sxs-lookup"><span data-stu-id="c6464-116">**Offer**: Specifies the virtual machine offering to use from the selected publisher (for example, *JDK*).</span></span>

   * <span data-ttu-id="c6464-117">**SKU**: especifica la referencia de almacén (SKU) que quiere usar de la oferta seleccionada (por ejemplo, *JDK_8*).</span><span class="sxs-lookup"><span data-stu-id="c6464-117">**Sku**: Specifies the stockkeeping unit (SKU) to use from the selected offering (for example, *JDK_8*).</span></span>

   * <span data-ttu-id="c6464-118">**N.º de versión**: especifica la versión que quiere usar de la SKU seleccionada.</span><span class="sxs-lookup"><span data-stu-id="c6464-118">**Version #**: Specifies which version of the selected SKU to use.</span></span>

   ![La ventana Seleccionar una imagen de máquina virtual][CR03]

5. <span data-ttu-id="c6464-120">Haga clic en **Next**.</span><span class="sxs-lookup"><span data-stu-id="c6464-120">Click **Next**.</span></span>

6. <span data-ttu-id="c6464-121">En la pantalla **Configuración básica de máquina virtual**, escriba la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="c6464-121">In the **Virtual Machine Basic Settings** window, enter the following information:</span></span>

   * <span data-ttu-id="c6464-122">**Nombre de máquina virtual**: especifica el nombre de la nueva máquina virtual, que debe comenzar con una letra y contener solo letras, números y guiones.</span><span class="sxs-lookup"><span data-stu-id="c6464-122">**Virtual Machine Name**: Specifies the name for your new virtual machine, which must start with a letter and contain only letters, numbers, and hyphens.</span></span>

   * <span data-ttu-id="c6464-123">**Tamaño**: especifica el número de núcleos y la memoria que se asignará para la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c6464-123">**Size**: Specifies the number of cores and memory to allocate for your virtual machine.</span></span>

   * <span data-ttu-id="c6464-124">**Nombre de usuario**: especifica la cuenta de administrador que se creará para administrar la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c6464-124">**User name**: Specifies the administrator account to create for managing your virtual machine.</span></span>

   * <span data-ttu-id="c6464-125">**Contraseña** y **Confirmar**: especifica la contraseña de la cuenta de administrador.</span><span class="sxs-lookup"><span data-stu-id="c6464-125">**Password** and **Confirm**: Specifies the password for your administrator account.</span></span>

   ![La ventana Configuración básica de máquina virtual][CR04]

7. <span data-ttu-id="c6464-127">Haga clic en **Next**.</span><span class="sxs-lookup"><span data-stu-id="c6464-127">Click **Next**.</span></span>

8. <span data-ttu-id="c6464-128">En la ventana **Crear una nueva cuenta de almacenamiento**, escriba la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="c6464-128">In the **Create New Storage Account** window, enter the following information:</span></span>

   * <span data-ttu-id="c6464-129">**Grupo de recursos**: especifica el grupo de recursos para su máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c6464-129">**Resource Group**: Specifies the resource group for your virtual machine.</span></span> <span data-ttu-id="c6464-130">Seleccione una de las siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="c6464-130">Select one of the following options:</span></span>
     * <span data-ttu-id="c6464-131">**Crear nuevo**: especifica que quiere crear un nuevo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="c6464-131">**Create new**: Specifies that you want to create a new resource group.</span></span>
     * <span data-ttu-id="c6464-132">**Usar existente**: especifica que desea seleccionar un grupo de recursos que ya está asociado a la cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="c6464-132">**Use existing**: Specifies that you want to select a resource group that is already associated with your Azure account.</span></span>

       ![Cuadro de diálogo Crear una nueva cuenta de almacenamiento][CR05]

   * <span data-ttu-id="c6464-134">**Cuenta de almacenamiento**: especifica la cuenta de almacenamiento que se usará para almacenar la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c6464-134">**Storage account**: Specifies the storage account to use for storing your virtual machine.</span></span> <span data-ttu-id="c6464-135">Puede usar una cuenta de almacenamiento existente o crear una nueva.</span><span class="sxs-lookup"><span data-stu-id="c6464-135">You can use an existing storage account or create a new account.</span></span>

   * <span data-ttu-id="c6464-136">**Red virtual** y **Subred**: especifica la red virtual y subred que se conectará la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c6464-136">**Virtual Network** and **Subnet**: Specifies the virtual network and subnet that your virtual machine will connect to.</span></span> <span data-ttu-id="c6464-137">Puede usar una red y subred existentes, o puede crear una nueva red y subred.</span><span class="sxs-lookup"><span data-stu-id="c6464-137">You can use an existing network and subnet, or you can create a new network and subnet.</span></span> <span data-ttu-id="c6464-138">Si selecciona **Crear nuevo**, se mostrará el cuadro de diálogo siguiente:</span><span class="sxs-lookup"><span data-stu-id="c6464-138">If you select **Create new**, the following dialog box is displayed:</span></span>

      ![Cuadro de diálogo Crear una red virtual nueva][CR06]

9. <span data-ttu-id="c6464-140">En la ventana **Recursos asociados**, escriba la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="c6464-140">In the **Associated Resources** window, enter the following information:</span></span>

   * <span data-ttu-id="c6464-141">**Dirección IP pública**: especifica una dirección IP externa para la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c6464-141">**Public IP address**: Specifies an external-facing IP address for your virtual machine.</span></span> <span data-ttu-id="c6464-142">Puede crear una dirección IP o, si la máquina virtual no tiene una dirección IP pública, puede seleccionar **(Ninguno)**.</span><span class="sxs-lookup"><span data-stu-id="c6464-142">You can choose to create a new IP address or, if your virtual machine will not have a public IP address, you can select **(None)**.</span></span>

   * <span data-ttu-id="c6464-143">**Grupo de seguridad de red**: especifica un firewall de red opcional para la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c6464-143">**Network security group**: Specifies an optional networking firewall for your virtual machine.</span></span> <span data-ttu-id="c6464-144">Puede seleccionar un firewall o, si la máquina virtual no utiliza un firewall, puede seleccionar **(Ninguno)**.</span><span class="sxs-lookup"><span data-stu-id="c6464-144">You can select an existing firewall or, if your virtual machine will not use a network firewall, you can select **(None)**.</span></span>

   * <span data-ttu-id="c6464-145">**Conjunto de disponibilidad**: especifica un conjunto de disponibilidad opcional al que puede pertenecer su máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c6464-145">**Availability set**: Specifies an optional availability set that your virtual machine can belong to.</span></span> <span data-ttu-id="c6464-146">Puede seleccionar un conjunto de disponibilidad, crear uno o, si la máquina virtual no pertenece a un conjunto de disponibilidad, seleccionar **(Ninguno)**.</span><span class="sxs-lookup"><span data-stu-id="c6464-146">You can select an existing availability set or create a new availability set or, if your virtual machine will not belong to an availability set, you can select **(None)**.</span></span>

   ![La ventana Recursos asociados][CR07]

10. <span data-ttu-id="c6464-148">Haga clic en **Finalizar**</span><span class="sxs-lookup"><span data-stu-id="c6464-148">Click **Finish**.</span></span>  

    <span data-ttu-id="c6464-149">La nueva máquina virtual aparece en la ventana de la herramienta Azure Explorer.</span><span class="sxs-lookup"><span data-stu-id="c6464-149">Your new virtual machine is displayed in the Azure Explorer tool window.</span></span>

    ![Nueva máquina virtual][CR08]

## <a name="restart-a-virtual-machine-in-eclipse"></a><span data-ttu-id="c6464-151">Reinicio de una máquina virtual en Eclipse</span><span class="sxs-lookup"><span data-stu-id="c6464-151">Restart a virtual machine in Eclipse</span></span>

<span data-ttu-id="c6464-152">Para reiniciar una máquina virtual mediante Azure Explorer en Eclipse, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="c6464-152">To restart a virtual machine by using the Azure Explorer in Eclipse, do the following:</span></span>

1. <span data-ttu-id="c6464-153">En la vista **Azure Explorer**, haga clic con el botón derecho en la máquina virtual y elija **Reiniciar**.</span><span class="sxs-lookup"><span data-stu-id="c6464-153">In the **Azure Explorer** view, right-click the virtual machine, and then select **Restart**.</span></span>

   ![El comando de reinicio de máquina virtual][RE01]

1. <span data-ttu-id="c6464-155">En la ventana confirmación, haga clic en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="c6464-155">In the confirmation window, click **Yes**.</span></span>

   ![Ventana de confirmación de Reiniciar][RE02]

## <a name="shut-down-a-virtual-machine-in-eclipse"></a><span data-ttu-id="c6464-157">Apagado de una máquina virtual en Eclipse</span><span class="sxs-lookup"><span data-stu-id="c6464-157">Shut down a virtual machine in Eclipse</span></span>

<span data-ttu-id="c6464-158">Para apagar una máquina virtual en funcionamiento con Azure Explorer en Eclipse, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="c6464-158">To shut down a running virtual machine by using the Azure Explorer in Eclipse, do the following:</span></span>

1. <span data-ttu-id="c6464-159">En la vista **Azure Explorer**, haga clic con el botón derecho en la máquina virtual y elija **Apagar**.</span><span class="sxs-lookup"><span data-stu-id="c6464-159">In the **Azure Explorer** view, right-click the virtual machine, and then select **Shutdown**.</span></span>

   ![El comando de apagado de máquina virtual][SH01]

1. <span data-ttu-id="c6464-161">En la ventana confirmación, haga clic en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="c6464-161">In the confirmation window, click **Yes**.</span></span>

   ![Ventana de confirmación de apagado de máquina virtual][SH02]

## <a name="delete-a-virtual-machine-in-eclipse"></a><span data-ttu-id="c6464-163">Eliminación de una máquina virtual en Eclipse</span><span class="sxs-lookup"><span data-stu-id="c6464-163">Delete a virtual machine in Eclipse</span></span>

<span data-ttu-id="c6464-164">Para eliminar una máquina virtual mediante Azure Explorer en Eclipse, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="c6464-164">To delete a virtual machine by using the Azure Explorer in Eclipse, do the following:</span></span>

1. <span data-ttu-id="c6464-165">En la vista **Azure Explorer**, haga clic con el botón derecho en la máquina virtual y elija **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="c6464-165">In the **Azure Explorer** view, right-click the virtual machine, and then select **Delete**.</span></span>

   ![El comando de eliminación de máquina virtual][DE01]

1. <span data-ttu-id="c6464-167">En la ventana confirmación, haga clic en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="c6464-167">In the confirmation window, click **Yes**.</span></span>

   ![Ventana de confirmación de eliminación de máquina virtual][DE02]

## <a name="next-steps"></a><span data-ttu-id="c6464-169">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c6464-169">Next steps</span></span>

<span data-ttu-id="c6464-170">Para obtener más información sobre los tamaños y los precios de máquinas virtuales de Azure, consulte los siguientes vínculos:</span><span class="sxs-lookup"><span data-stu-id="c6464-170">For more information about Azure virtual-machine sizes and pricing, see the following resources:</span></span>

* <span data-ttu-id="c6464-171">Tamaños de máquinas virtuales de Azure</span><span class="sxs-lookup"><span data-stu-id="c6464-171">Azure virtual-machine sizes</span></span>
  * <span data-ttu-id="c6464-172">[Tamaños de las máquinas virtuales Windows en Azure]</span><span class="sxs-lookup"><span data-stu-id="c6464-172">[Sizes for Windows virtual machines in Azure]</span></span>
  * <span data-ttu-id="c6464-173">[Tamaños de las máquinas virtuales Linux en Azure]</span><span class="sxs-lookup"><span data-stu-id="c6464-173">[Sizes for Linux virtual machines in Azure]</span></span>
* <span data-ttu-id="c6464-174">Precios de máquinas virtuales de Azure</span><span class="sxs-lookup"><span data-stu-id="c6464-174">Azure virtual-machine pricing</span></span>
  * <span data-ttu-id="c6464-175">[Precios de máquinas virtuales Windows]</span><span class="sxs-lookup"><span data-stu-id="c6464-175">[Windows virtual-machine pricing]</span></span>
  * <span data-ttu-id="c6464-176">[Precios de máquinas virtuales Linux]</span><span class="sxs-lookup"><span data-stu-id="c6464-176">[Linux virtual-machine pricing]</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<!-- URL List -->

[Tamaños de las máquinas virtuales Windows en Azure]: /azure/virtual-machines/virtual-machines-windows-sizes
[Sizes for Windows virtual machines in Azure]: /azure/virtual-machines/virtual-machines-windows-sizes
[Tamaños de las máquinas virtuales Linux en Azure]: /azure/virtual-machines/virtual-machines-linux-sizes
[Sizes for Linux virtual machines in Azure]: /azure/virtual-machines/virtual-machines-linux-sizes
[Precios de máquinas virtuales Windows]: /pricing/details/virtual-machines/windows/
[Windows virtual-machine pricing]: /pricing/details/virtual-machines/windows/
[Precios de máquinas virtuales Linux]: /pricing/details/virtual-machines/linux/
[Linux virtual-machine pricing]: /pricing/details/virtual-machines/linux/

<!-- IMG List -->

[RE01]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/RE01.png
[RE02]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/RE02.png

[SH01]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/SH01.png
[SH02]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/SH02.png

[DE01]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/DE01.png
[DE02]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/DE02.png

[CR01]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR01.png
[CR02]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR02.png
[CR03]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR03.png
[CR04]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR04.png
[CR05]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR05.png
[CR06]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR06.png
[CR07]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR07.png
[CR08]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR08.png
