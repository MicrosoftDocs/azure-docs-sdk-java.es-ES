---
title: Instrucciones de inicio de sesión del kit de herramientas de Azure para Eclipse
description: Obtenga información sobre cómo iniciar sesión en Microsoft Azure utilizando el Kit de herramientas de Azure para Eclipse.
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
ms.openlocfilehash: eb6099ab0c19bf3588cb7fd668f070771e58fe74
ms.sourcegitcommit: 8230cf6b15ac51a9f8a209e9b76411a0385029aa
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/16/2018
---
# <a name="azure-sign-in-instructions-for-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="4bed0-103">Instrucciones de inicio de sesión del kit de herramientas de Azure para Eclipse</span><span class="sxs-lookup"><span data-stu-id="4bed0-103">Azure Sign In Instructions for the Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="4bed0-104">El kit de herramientas de Azure para Eclipse proporciona dos métodos para iniciar sesión en su cuenta de Azure:</span><span class="sxs-lookup"><span data-stu-id="4bed0-104">The Azure Toolkit for Eclipse provides two methods for signing into your Azure account:</span></span>

  * <span data-ttu-id="4bed0-105">**Automatizado**: al utilizar este método, se creará un archivo de credenciales que contiene los datos de entidades de seguridad de servicio. Después, podrá utilizar el archivo de credenciales para iniciar sesión automáticamente en su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="4bed0-105">**Automated** - when you are using this method, you will create a credentials file which contains your service principal data, after which you can use the credentials file to automatically sign into your Azure account.</span></span>
  * <span data-ttu-id="4bed0-106">**Interactivo**: al usar este método, deberá especificar sus credenciales de Azure cada vez que inicie sesión en su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="4bed0-106">**Interactive** - when you are using this method, you will enter your Azure credentials each time you sign into your Azure account.</span></span>

<span data-ttu-id="4bed0-107">Los pasos descritos en las secciones siguientes explican cómo utilizar cada método.</span><span class="sxs-lookup"><span data-stu-id="4bed0-107">The steps in the following sections will describe how to use each method.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="signing-into-your-azure-account-automatically-and-creating-a-credentials-file-to-use-in-the-future"></a><span data-ttu-id="4bed0-108">Inicio de sesión en su cuenta de Azure de forma automática y creación de un archivo de credenciales para utilizarlo en el futuro</span><span class="sxs-lookup"><span data-stu-id="4bed0-108">Signing into your Azure account automatically and creating a credentials file to use in the future</span></span>

<span data-ttu-id="4bed0-109">Los siguientes pasos lo guiarán por el proceso de creación de un archivo de credenciales que contiene los datos de entidades de seguridad de servicio.</span><span class="sxs-lookup"><span data-stu-id="4bed0-109">The following steps will walk you through creating a credentials file which contains your service principal data.</span></span> <span data-ttu-id="4bed0-110">Cuando finalice estos pasos, Eclipse usará automáticamente el archivo de credenciales para iniciar sesión automáticamente en Azure cada vez que abra el proyecto.</span><span class="sxs-lookup"><span data-stu-id="4bed0-110">Once you have completed these steps, Eclipse will automatically use the credentials file to automatically sign you into Azure each time you open your project.</span></span>

1. <span data-ttu-id="4bed0-111">Abra el proyecto con Eclipse.</span><span class="sxs-lookup"><span data-stu-id="4bed0-111">Open your project with Eclipse.</span></span>

1. <span data-ttu-id="4bed0-112">Haga clic en **Herramientas** y, luego, en **Azure**y en **Iniciar sesión**.</span><span class="sxs-lookup"><span data-stu-id="4bed0-112">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>

   ![Menú de Eclipse para iniciar sesión en Azure][A01]

1. <span data-ttu-id="4bed0-114">Cuando se muestra el cuadro de diálogo **Inicio de sesión en Microsoft Azure**, seleccione **Automatizado** y, luego, haga clic en **Nuevo**.</span><span class="sxs-lookup"><span data-stu-id="4bed0-114">When the **Azure Sign In** dialog box appears, select **Automated**, and then click **New**.</span></span>

   ![Cuadro de diálogo Iniciar sesión][A02]

1. <span data-ttu-id="4bed0-116">Cuando se muestre el cuadro de diálogo **Inicio de sesión en Microsoft Azure**, escriba sus credenciales de Azure y, luego, haga clic en **Iniciar sesión**.</span><span class="sxs-lookup"><span data-stu-id="4bed0-116">When the **Azure Log In** dialog box appears, enter your Azure credentials, and then click **Sign In**.</span></span>

   ![Cuadro de diálogo Inicio de sesión en Microsoft Azure][A03]

1. <span data-ttu-id="4bed0-118">Cuando se muestre el cuadro de diálogo **Create authentication files** (Crear archivos de autenticación), seleccione las suscripciones que desea utilizar, elija el directorio de destino y, luego, haga clic en **Iniciar**.</span><span class="sxs-lookup"><span data-stu-id="4bed0-118">When the **Create authentication files** dialog box appears, select the subscriptions that you want to use, choose your destination directory, and then click **Start**.</span></span>

   ![Cuadro de diálogo Inicio de sesión en Microsoft Azure][A04]

1. <span data-ttu-id="4bed0-120">Se mostrará el cuadro de diálogo **Service Principal Creation Status** (Estado de creación de entidades de servicio) y, una vez que se hayan creado correctamente los archivos, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="4bed0-120">The **Service Principal Creatation Status** dialog box will be displayed, and after your files have been created successfully, click **OK**.</span></span>

   ![Cuadro de diálogo Service Principal Creation Status (Estado de creación de entidades de servicio)][A05]

1. <span data-ttu-id="4bed0-122">Cuando se muestre el cuadro de diálogo **Inicio de sesión en Microsoft Azure** , haga clic en **Iniciar sesión**.</span><span class="sxs-lookup"><span data-stu-id="4bed0-122">When the **Azure Sign In** dialog box appears, click **Sign In**.</span></span>

   ![Cuadro de diálogo Inicio de sesión en Microsoft Azure][A06]

1. <span data-ttu-id="4bed0-124">Cuando se muestre el cuadro de diálogo **Seleccionar suscripciones**, seleccione las suscripciones que desea usar y, luego, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="4bed0-124">When the **Select Subscriptions** dialog box appears, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![Cuadro de diálogo Seleccionar suscripciones][A07]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-automatically"></a><span data-ttu-id="4bed0-126">Cierre de sesión de la cuenta de Azure al iniciar sesión de forma automática</span><span class="sxs-lookup"><span data-stu-id="4bed0-126">Signing out of your Azure account when you signed in automatically</span></span>

<span data-ttu-id="4bed0-127">Después de haber configurado los pasos en la sección anterior, el kit de herramientas de Azure cerrará automáticamente la sesión de su cuenta de Azure cada vez que reinicie Eclipse.</span><span class="sxs-lookup"><span data-stu-id="4bed0-127">After you have configured the steps in the previous section, the Azure Toolkit will automatically sign you into your Azure account each time you restart Eclipse.</span></span> <span data-ttu-id="4bed0-128">Sin embargo, para cerrar la sesión de su cuenta de Azure e impedir que el kit de herramientas de Azure inicie sesión automáticamente, siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="4bed0-128">However, to sign out of your Azure account and prevent the Azure Toolkit from signing you in automatically, use the following steps.</span></span>

1. <span data-ttu-id="4bed0-129">En Eclipse, haga clic en **Herramientas** y, luego, en **Azure** y en **Cerrar sesión**.</span><span class="sxs-lookup"><span data-stu-id="4bed0-129">In Eclipse, click **Tools**, then click **Azure**, and then click **Sign Out**.</span></span>

   ![Menú de Eclipse para cerrar sesión en Azure][L01]

1. <span data-ttu-id="4bed0-131">Cuando se muestre el cuadro de diálogo **Cierre de sesión en Microsoft Azure** , haga clic en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="4bed0-131">When the **Azure Sign Out** dialog box appears, click **Yes**.</span></span>

   ![Cuadro de diálogo Cerrar sesión][L03]

## <a name="signing-into-your-azure-account-automatically-using-a-credentials-file-which-you-have-already-created"></a><span data-ttu-id="4bed0-133">Inicio de sesión en su cuenta de Azure de forma automática y uso de un archivo de credenciales existente</span><span class="sxs-lookup"><span data-stu-id="4bed0-133">Signing into your Azure account automatically using a credentials file which you have already created</span></span>

<span data-ttu-id="4bed0-134">Si cierra la sesión de Azure al utilizar Eclipse, debe volver a configurar el kit de herramientas de Azure para Eclipse con el fin de usar un archivo de credenciales ya creado antes de poder iniciar sesión automáticamente en su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="4bed0-134">If you sign out of Azure when you are using Eclipse, you will need to reconfigure the Azure Toolkit for Eclipse to use a credentials file which have created before you can automatically sign into your Azure acccount.</span></span> <span data-ttu-id="4bed0-135">Los siguientes pasos lo guiarán a través del proceso de configuración del kit de herramientas de Azure para usar un archivo de credenciales existente.</span><span class="sxs-lookup"><span data-stu-id="4bed0-135">The following steps will walk you through configuring the Azure Toolkit to use an existing credentials file.</span></span>

1. <span data-ttu-id="4bed0-136">Abra el proyecto con Eclipse.</span><span class="sxs-lookup"><span data-stu-id="4bed0-136">Open your project with Eclipse.</span></span>

1. <span data-ttu-id="4bed0-137">Haga clic en **Herramientas** y, luego, en **Azure**y en **Iniciar sesión**.</span><span class="sxs-lookup"><span data-stu-id="4bed0-137">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>

   ![Menú de Eclipse para iniciar sesión en Azure][A01]

1. <span data-ttu-id="4bed0-139">Cuando se muestra el cuadro de diálogo **Inicio de sesión en Microsoft Azure**, seleccione **Automatizado** y, luego, haga clic en **Examinar**.</span><span class="sxs-lookup"><span data-stu-id="4bed0-139">When the **Azure Sign In** dialog box appears, select **Automated**, and then click **Browse**.</span></span>

   ![Cuadro de diálogo Iniciar sesión][A02]

1. <span data-ttu-id="4bed0-141">Cuando se muestra el cuadro de diálogo **Select Authentication File** (Seleccionar archivo de autenticación), elija un archivo de credenciales que creó anteriormente y, luego, haga clic en **Open** (Abrir).</span><span class="sxs-lookup"><span data-stu-id="4bed0-141">When the **Select Authenticated File** dialog box appears, select a credentials file which you created earlier, and then click **Open**.</span></span>

   ![Cuadro de diálogo Iniciar sesión][A08]

1. <span data-ttu-id="4bed0-143">Cuando se muestre el cuadro de diálogo **Inicio de sesión en Microsoft Azure**, haga clic en **Iniciar sesión**.</span><span class="sxs-lookup"><span data-stu-id="4bed0-143">When the **Azure Sign In** dialog box appears, click **Sign In**.</span></span>

   ![Cuadro de diálogo Inicio de sesión en Microsoft Azure][A06]

1. <span data-ttu-id="4bed0-145">Cuando se muestre el cuadro de diálogo **Seleccionar suscripciones**, seleccione las suscripciones que desea usar y, luego, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="4bed0-145">When the **Select Subscriptions** dialog box appears, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![Cuadro de diálogo Seleccionar suscripciones][A07]

## <a name="signing-into-your-azure-account-interactively"></a><span data-ttu-id="4bed0-147">Inicio de sesión en la cuenta de Azure de forma interactiva</span><span class="sxs-lookup"><span data-stu-id="4bed0-147">Signing into your Azure account interactively</span></span>

<span data-ttu-id="4bed0-148">En los pasos siguientes se explica cómo iniciar sesión en Azure especificando manualmente las credenciales de Azure.</span><span class="sxs-lookup"><span data-stu-id="4bed0-148">The following steps will illustrate how to sign into Azure by manually entering your Azure credentials.</span></span>

1. <span data-ttu-id="4bed0-149">Abra el proyecto con Eclipse.</span><span class="sxs-lookup"><span data-stu-id="4bed0-149">Open your project with Eclipse.</span></span>

1. <span data-ttu-id="4bed0-150">Haga clic en **Herramientas** y, luego, en **Azure**y en **Iniciar sesión**.</span><span class="sxs-lookup"><span data-stu-id="4bed0-150">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>

   ![Menú de Eclipse para iniciar sesión en Azure][I01]

1. <span data-ttu-id="4bed0-152">Cuando se muestra el cuadro de diálogo **Inicio de sesión en Microsoft Azure**, seleccione **Interactivo** y, luego, haga clic en **Iniciar sesión**.</span><span class="sxs-lookup"><span data-stu-id="4bed0-152">When the **Azure Sign In** dialog box appears, select **Interactive**, and then click **Sign In**.</span></span>

   ![Cuadro de diálogo Iniciar sesión][I02]

1. <span data-ttu-id="4bed0-154">Cuando se muestre el cuadro de diálogo **Inicio de sesión en Microsoft Azure**, escriba sus credenciales de Azure y, luego, haga clic en **Iniciar sesión**.</span><span class="sxs-lookup"><span data-stu-id="4bed0-154">When the **Azure Log In** dialog box appears, enter your Azure credentials, and then click **Sign In**.</span></span>

   ![Cuadro de diálogo Inicio de sesión en Microsoft Azure][I03]

1. <span data-ttu-id="4bed0-156">Cuando se muestre el cuadro de diálogo **Seleccionar suscripciones**, seleccione las suscripciones que desea usar y, luego, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="4bed0-156">When the **Select Subscriptions** dialog box appears, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![Cuadro de diálogo Seleccionar suscripciones][I04]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-interactively"></a><span data-ttu-id="4bed0-158">Cierre de sesión de la cuenta de Azure al iniciar sesión de forma interactiva</span><span class="sxs-lookup"><span data-stu-id="4bed0-158">Signing out of your Azure account when you signed in interactively</span></span>

<span data-ttu-id="4bed0-159">Después de haber configurado los pasos en la sección anterior, se cerrará automáticamente la sesión de su cuenta de Azure cada vez que reinicie Eclipse.</span><span class="sxs-lookup"><span data-stu-id="4bed0-159">After you have configured the steps in the previous section, you will automatically signed out of your Azure account each time you restart Eclipse.</span></span> <span data-ttu-id="4bed0-160">Sin embargo, si desea cerrar sesión de su cuenta de Azure sin tener que reiniciar Eclipse, siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="4bed0-160">However, if you want to sign out of your Azure account without restarting Eclipse, use the following steps.</span></span>

1. <span data-ttu-id="4bed0-161">En Eclipse, haga clic en **Herramientas** y, luego, en **Azure** y en **Cerrar sesión**.</span><span class="sxs-lookup"><span data-stu-id="4bed0-161">In Eclipse, click **Tools**, then click **Azure**, and then click **Sign Out**.</span></span>

   ![Menú de Eclipse para cerrar sesión en Azure][L01]

1. <span data-ttu-id="4bed0-163">Cuando se muestre el cuadro de diálogo **Cierre de sesión en Microsoft Azure** , haga clic en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="4bed0-163">When the **Azure Sign Out** dialog box appears, click **Yes**.</span></span>

   ![Cuadro de diálogo Cerrar sesión][L02]

## <a name="next-steps"></a><span data-ttu-id="4bed0-165">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4bed0-165">Next steps</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<!-- URL List -->


<!-- IMG List -->

[I01]: media/azure-toolkit-for-eclipse-sign-in-instructions/I01.png
[I02]: media/azure-toolkit-for-eclipse-sign-in-instructions/I02.png
[I03]: media/azure-toolkit-for-eclipse-sign-in-instructions/I03.png
[I04]: media/azure-toolkit-for-eclipse-sign-in-instructions/I04.png

[A01]: media/azure-toolkit-for-eclipse-sign-in-instructions/A01.png
[A02]: media/azure-toolkit-for-eclipse-sign-in-instructions/A02.png
[A03]: media/azure-toolkit-for-eclipse-sign-in-instructions/A03.png
[A04]: media/azure-toolkit-for-eclipse-sign-in-instructions/A04.png
[A05]: media/azure-toolkit-for-eclipse-sign-in-instructions/A05.png
[A06]: media/azure-toolkit-for-eclipse-sign-in-instructions/A06.png
[A07]: media/azure-toolkit-for-eclipse-sign-in-instructions/A07.png
[A08]: media/azure-toolkit-for-eclipse-sign-in-instructions/A08.png

[L01]: media/azure-toolkit-for-eclipse-sign-in-instructions/L01.png
[L02]: media/azure-toolkit-for-eclipse-sign-in-instructions/L02.png
[L03]: media/azure-toolkit-for-eclipse-sign-in-instructions/L03.png
