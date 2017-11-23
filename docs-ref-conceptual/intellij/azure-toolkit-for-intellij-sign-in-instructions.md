---
title: "Instrucciones de inicio de sesión del kit de herramientas de Azure para IntelliJ"
description: "Obtenga información sobre cómo iniciar sesión en Microsoft Azure con el kit de herramientas de Azure para IntelliJ."
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
ms.openlocfilehash: 25c25e58b079c1e08d62feff389b899b26e82b5e
ms.sourcegitcommit: 613c1ffd2e0279fc7a96fca98aa1809563f52ee1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="sign-in-instructions-for-the-azure-toolkit-for-intellij"></a><span data-ttu-id="7ab60-103">Instrucciones de inicio de sesión del kit de herramientas de Azure para IntelliJ</span><span class="sxs-lookup"><span data-stu-id="7ab60-103">Sign-in instructions for the Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="7ab60-104">El kit de herramientas de Azure para IntelliJ proporciona dos métodos para iniciar sesión en su cuenta de Azure:</span><span class="sxs-lookup"><span data-stu-id="7ab60-104">The Azure Toolkit for IntelliJ provides two methods for signing in to your Azure account:</span></span>

  * <span data-ttu-id="7ab60-105">**Automatizado**: cree un archivo de credenciales que puede usar para iniciar sesión automáticamente en su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="7ab60-105">**Automated**: You create a credentials file that you can use to automatically sign in to your Azure account.</span></span>
  * <span data-ttu-id="7ab60-106">**Interactivo**: escriba sus credenciales de Azure cada vez que inicie sesión su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="7ab60-106">**Interactive**: You enter your Azure credentials each time you sign in to your Azure account.</span></span>

<span data-ttu-id="7ab60-107">Los pasos descritos en las secciones siguientes explican cómo utilizar cada método.</span><span class="sxs-lookup"><span data-stu-id="7ab60-107">The following sections describe how to use each method.</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="sign-in-to-your-azure-account-automatically"></a><span data-ttu-id="7ab60-108">Inicio sesión en la cuenta de Azure de forma automática</span><span class="sxs-lookup"><span data-stu-id="7ab60-108">Sign in to your Azure account automatically</span></span>

<span data-ttu-id="7ab60-109">Los siguientes pasos lo guiarán por el proceso de creación de un archivo de credenciales que contiene los datos de entidades de servicio.</span><span class="sxs-lookup"><span data-stu-id="7ab60-109">This section walks you through creating a credentials file that contains your service principal data.</span></span> <span data-ttu-id="7ab60-110">Cuando finalice este proceso, Eclipse usará el archivo de credenciales para iniciar sesión automáticamente en Azure cada vez que abra el proyecto.</span><span class="sxs-lookup"><span data-stu-id="7ab60-110">After you have completed this process, Eclipse uses the credentials file to automatically sign you in to Azure each time you open your project.</span></span>

1. <span data-ttu-id="7ab60-111">Abra el proyecto con IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="7ab60-111">Open your project with IntelliJ IDEA.</span></span>

1. <span data-ttu-id="7ab60-112">En el menú **Herramientas**, seleccione **Azure** y, luego, haga clic en **Inicio de sesión en Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="7ab60-112">On the **Tools** menu, point to **Azure**, and then click **Azure Sign In**.</span></span>

   ![El comando de inicio de sesión en Azure IntelliJ][A01]

1. <span data-ttu-id="7ab60-114">En la ventana **Inicio de sesión en Microsoft Azure**, seleccione **Automatizado** y, luego, haga clic en **Nuevo**.</span><span class="sxs-lookup"><span data-stu-id="7ab60-114">In the **Azure Sign In** window, select **Automated**, and then click **New**.</span></span>

   ![La ventana Inicio de sesión en Microsoft Azure con el modo Automatizado seleccionado][A02]

1. <span data-ttu-id="7ab60-116">En la ventana **Inicio de sesión en Microsoft Azure**, escriba sus credenciales de Azure y, luego, haga clic en **Iniciar sesión**.</span><span class="sxs-lookup"><span data-stu-id="7ab60-116">In the **Azure Login Dialog** window, enter your Azure credentials, and then click **Sign in**.</span></span>

   ![El cuadro de diálogo Inicio de sesión en Microsoft Azure][A03]

1. <span data-ttu-id="7ab60-118">En la ventana **Create authentication files** (Crear archivos de autenticación), seleccione las suscripciones que desea utilizar, elija el directorio de destino y, luego, haga clic en **Iniciar**.</span><span class="sxs-lookup"><span data-stu-id="7ab60-118">In the **Create Authentication Files** window, select the subscriptions that you want to use, choose your destination directory, and then click **Start**.</span></span>

   ![La ventana Create authentication files (Crear archivos de autenticación)][A04]

1. <span data-ttu-id="7ab60-120">En el cuadro de diálogo **Service Principal Creation Status** (Estado de creación de entidades de servicio), una vez que se hayan creado correctamente los archivos, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="7ab60-120">In the **Service Principal Creation Status** dialog box, after your files have been created successfully, click **OK**.</span></span>

   ![El cuadro de diálogo Service Principal Creation Status (Estado de creación de entidades de servicio)][A05]

1. <span data-ttu-id="7ab60-122">En la ventana **Inicio de sesión en Microsoft Azure**, haga clic en **Iniciar sesión en**.</span><span class="sxs-lookup"><span data-stu-id="7ab60-122">In the **Azure Sign In** window, click **Sign in**.</span></span>

   ![Cuadro de diálogo Inicio de sesión en Microsoft Azure][A06]

1. <span data-ttu-id="7ab60-124">En el cuadro de diálogo **Seleccionar suscripciones**, elija las suscripciones que desea usar y, luego, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="7ab60-124">In the **Select Subscriptions** dialog box, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![Cuadro de diálogo Seleccionar suscripciones][A07]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-automatically"></a><span data-ttu-id="7ab60-126">Cierre de sesión de la cuenta de Azure después de haber iniciado sesión de forma automática</span><span class="sxs-lookup"><span data-stu-id="7ab60-126">Sign out of your Azure account after you have signed in automatically</span></span>

<span data-ttu-id="7ab60-127">Después de haber configurado la cuenta con los pasos anteriores, el kit de herramientas de Azure iniciará sesión automáticamente en su cuenta de Azure cada vez que reinicie IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="7ab60-127">After you have configured your account by using the preceding steps, the Azure Toolkit automatically signs you in to your Azure account each time you restart IntelliJ IDEA.</span></span> <span data-ttu-id="7ab60-128">Sin embargo, para cerrar la sesión de su cuenta de Azure e impedir que el kit de herramientas de Azure inicie sesión automáticamente, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="7ab60-128">However, to sign out of your Azure account and prevent the Azure Toolkit from signing you in automatically, do the following:</span></span>

1. <span data-ttu-id="7ab60-129">En IntelliJ IDEA, haga clic en **Herramientas**, seleccione **Azure** y, luego, haga clic en **Cierre de sesión en Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="7ab60-129">In IntelliJ IDEA, on the **Tools** menu, point to **Azure**, and then click **Azure Sign Out**.</span></span>

   ![El comando de cierre de sesión en Azure IntelliJ][L01]

1. <span data-ttu-id="7ab60-131">En la ventana confirmación **Cierre de sesión en Microsoft Azure**, haga clic en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="7ab60-131">In the **Azure Sign Out** confirmation window, click **Yes**.</span></span>

   ![La ventana de confirmación Cierre de sesión en Microsoft Azure][L03]

## <a name="sign-in-to-your-azure-account-automatically-by-using-an-existing-credentials-file"></a><span data-ttu-id="7ab60-133">Inicio de sesión en su cuenta de Azure de forma automática mediante un archivo de credenciales</span><span class="sxs-lookup"><span data-stu-id="7ab60-133">Sign in to your Azure account automatically by using an existing credentials file</span></span>

<span data-ttu-id="7ab60-134">Si cierra la sesión de su cuenta de Azure mientras utiliza IntelliJ IDEA, debe usar un archivo de credenciales para iniciar sesión automáticamente en la cuenta.</span><span class="sxs-lookup"><span data-stu-id="7ab60-134">If you sign out of your Azure account when you are using IntelliJ IDEA, you must use an existing credentials file to automatically sign back in to the account.</span></span> <span data-ttu-id="7ab60-135">Para configurar el kit de herramientas de Azure para que Eclipse use un archivo de credenciales, realice lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="7ab60-135">To configure the Azure Toolkit for Eclipse to use an existing credentials file, do the following:</span></span>

1. <span data-ttu-id="7ab60-136">Abra el proyecto con IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="7ab60-136">Open your project with IntelliJ IDEA.</span></span>

1. <span data-ttu-id="7ab60-137">En el menú **Herramientas**, seleccione **Azure** y, luego, haga clic en **Inicio de sesión en Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="7ab60-137">On the **Tools** menu, point to **Azure**, and then click **Azure Sign In**.</span></span>

   ![El comando de inicio de sesión en Azure IntelliJ][A01]

1. <span data-ttu-id="7ab60-139">En la ventana **Inicio de sesión en Microsoft Azure**, seleccione **Automatizado** y, luego, haga clic en **Examinar**.</span><span class="sxs-lookup"><span data-stu-id="7ab60-139">In the **Azure Sign In** window, select **Automated**, and then click **Browse**.</span></span>

   ![La ventana Inicio de sesión en Microsoft Azure con el modo Automatizado seleccionado][A02]

1. <span data-ttu-id="7ab60-141">En el cuadro de diálogo **Select Authentication File** (Seleccionar archivo de autenticación), elija un archivo de credenciales creado anteriormente y, luego, haga clic en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="7ab60-141">In the **Select Authentication File** dialog box, select a previously created credentials file, and then click **Select**.</span></span>

   ![El cuadro de diálogo Select Authentication File (Seleccionar archivo de autenticación)][A08]

1. <span data-ttu-id="7ab60-143">En la ventana **Inicio de sesión en Microsoft Azure**, haga clic en **Iniciar sesión en**.</span><span class="sxs-lookup"><span data-stu-id="7ab60-143">In the **Azure Sign In** window, click **Sign in**.</span></span>

   ![La ventana Inicio de sesión en Microsoft Azure con el modo Automatizado seleccionado][A06]

1. <span data-ttu-id="7ab60-145">En el cuadro de diálogo **Seleccionar suscripciones**, elija las suscripciones que desea usar y, luego, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="7ab60-145">In the **Select Subscriptions** dialog box, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![Cuadro de diálogo Seleccionar suscripciones][A07]

## <a name="sign-in-to-your-azure-account-interactively"></a><span data-ttu-id="7ab60-147">Inicio de sesión en la cuenta de Azure de forma interactiva</span><span class="sxs-lookup"><span data-stu-id="7ab60-147">Sign in to your Azure account interactively</span></span>

<span data-ttu-id="7ab60-148">En los pasos siguientes se explica cómo iniciar sesión en Azure especificando manualmente las credenciales de Azure:</span><span class="sxs-lookup"><span data-stu-id="7ab60-148">To sign in to Azure by manually entering your Azure credentials, do the following:</span></span>

1. <span data-ttu-id="7ab60-149">Abra el proyecto con IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="7ab60-149">Open your project with IntelliJ IDEA.</span></span>

1. <span data-ttu-id="7ab60-150">Haga clic en **Herramientas**, seleccione **Azure** y, luego, haga clic en **Inicio de sesión en Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="7ab60-150">Click **Tools**, point to **Azure**, and then click **Azure Sign In**.</span></span>

   ![El comando de inicio de sesión en Azure IntelliJ][I01]

1. <span data-ttu-id="7ab60-152">En la ventana **Inicio de sesión en Microsoft Azure**, seleccione **Interactivo** y, luego, haga clic en **Iniciar sesión**.</span><span class="sxs-lookup"><span data-stu-id="7ab60-152">In the **Azure Sign In** window, select **Interactive**, and then click **Sign in**.</span></span>

   ![La ventana Inicio de sesión en Microsoft Azure con el modo Interactivo seleccionado][I02]

1. <span data-ttu-id="7ab60-154">Cuando se muestre el cuadro de diálogo **Inicio de sesión en Microsoft Azure**, escriba sus credenciales de Azure y, luego, haga clic en **Iniciar sesión**.</span><span class="sxs-lookup"><span data-stu-id="7ab60-154">In the **Azure Log In** dialog box appears, enter your Azure credentials, and then click **Sign in**.</span></span>

   ![El cuadro de diálogo Inicio de sesión en Microsoft Azure][I03]

1. <span data-ttu-id="7ab60-156">En el cuadro de diálogo **Seleccionar suscripciones**, elija las suscripciones que desea usar y, luego, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="7ab60-156">In the **Select Subscriptions** dialog box, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![Cuadro de diálogo Seleccionar suscripciones][I04]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-interactively"></a><span data-ttu-id="7ab60-158">Cierre de sesión de la cuenta de Azure al iniciar sesión de forma interactiva</span><span class="sxs-lookup"><span data-stu-id="7ab60-158">Sign out of your Azure account after you have signed in interactively</span></span>

<span data-ttu-id="7ab60-159">Después de haber configurado la cuenta con los pasos anteriores, se cerrará automáticamente la sesión de su cuenta de Azure cada vez que reinicie IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="7ab60-159">After you have configured your account by using the preceding steps, you will be automatically signed out of your Azure account each time you restart IntelliJ IDEA.</span></span> <span data-ttu-id="7ab60-160">Sin embargo, si desea cerrar sesión de su cuenta de Azure *sin* tener que reiniciar IntelliJ IDEA, siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="7ab60-160">However, if you want to sign out of your Azure account *without* restarting IntelliJ IDEA, do the following.</span></span>

1. <span data-ttu-id="7ab60-161">En IntelliJ IDEA, haga clic en **Herramientas**, seleccione **Azure** y, luego, haga clic en **Cierre de sesión en Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="7ab60-161">In IntelliJ IDEA, on the **Tools** menu, point to **Azure**, and then click **Azure Sign Out**.</span></span>

   ![El comando de cierre de sesión en Azure IntelliJ][L01]

1. <span data-ttu-id="7ab60-163">En la ventana confirmación **Cierre de sesión en Microsoft Azure**, haga clic en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="7ab60-163">In the **Azure Sign Out** confirmation window, click **Yes**.</span></span>

   ![La ventana de confirmación Cierre de sesión en Microsoft Azure][L02]

## <a name="next-steps"></a><span data-ttu-id="7ab60-165">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7ab60-165">Next steps</span></span>

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

<!-- URL List -->

<!-- IMG List -->

[I01]: media/azure-toolkit-for-intellij-sign-in-instructions/I01.png
[I02]: media/azure-toolkit-for-intellij-sign-in-instructions/I02.png
[I03]: media/azure-toolkit-for-intellij-sign-in-instructions/I03.png
[I04]: media/azure-toolkit-for-intellij-sign-in-instructions/I04.png

[A01]: media/azure-toolkit-for-intellij-sign-in-instructions/A01.png
[A02]: media/azure-toolkit-for-intellij-sign-in-instructions/A02.png
[A03]: media/azure-toolkit-for-intellij-sign-in-instructions/A03.png
[A04]: media/azure-toolkit-for-intellij-sign-in-instructions/A04.png
[A05]: media/azure-toolkit-for-intellij-sign-in-instructions/A05.png
[A06]: media/azure-toolkit-for-intellij-sign-in-instructions/A06.png
[A07]: media/azure-toolkit-for-intellij-sign-in-instructions/A07.png
[A08]: media/azure-toolkit-for-intellij-sign-in-instructions/A08.png

[L01]: media/azure-toolkit-for-intellij-sign-in-instructions/L01.png
[L02]: media/azure-toolkit-for-intellij-sign-in-instructions/L02.png
[L03]: media/azure-toolkit-for-intellij-sign-in-instructions/L03.png
