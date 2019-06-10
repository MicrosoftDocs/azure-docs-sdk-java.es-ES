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
ms.openlocfilehash: b4b13de38913ae6e7ae2bb09210ac742efc9d0ad
ms.sourcegitcommit: d18d9dce22b7f7af178f756bd341433d24e3c3b5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2019
ms.locfileid: "66575312"
---
# <a name="sign-in-instructions-for-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="20d35-103">Instrucciones de inicio de sesión del kit de herramientas de Azure para Eclipse</span><span class="sxs-lookup"><span data-stu-id="20d35-103">Sign-in instructions for the Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="20d35-104">El kit de herramientas de Azure para Eclipse proporciona dos métodos para iniciar sesión en su cuenta de Azure:</span><span class="sxs-lookup"><span data-stu-id="20d35-104">The Azure Toolkit for Eclipse provides two methods for signing into your Azure account:</span></span>

  - [<span data-ttu-id="20d35-105">Iniciar sesión en su cuenta de Azure mediante el inicio de sesión de dispositivo</span><span class="sxs-lookup"><span data-stu-id="20d35-105">Sign in to your Azure account by Device Login</span></span>](#sign-in-to-your-azure-account-by-device-login)
  - [<span data-ttu-id="20d35-106">Iniciar sesión en su cuenta de Azure mediante entidad de servicio</span><span class="sxs-lookup"><span data-stu-id="20d35-106">Sign in to your Azure account by Service Principal</span></span>](#sign-in-to-your-azure-account-by-service-principal)

<span data-ttu-id="20d35-107">También se proporcionan métodos de [**Cierre de sesión**](#sign-out-of-your-azure-account).</span><span class="sxs-lookup"><span data-stu-id="20d35-107">[**Sign out**](#sign-out-of-your-azure-account) methods are also provided.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="sign-in-to-your-azure-account-by-device-login"></a><span data-ttu-id="20d35-108">Inicio de sesión en su cuenta de Azure mediante el inicio de sesión de dispositivo</span><span class="sxs-lookup"><span data-stu-id="20d35-108">Sign in to your Azure account by Device Login</span></span>

<span data-ttu-id="20d35-109">Para iniciar sesión en Azure mediante el inicio de sesión de dispositivo, haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="20d35-109">To sign in Azure by device login, do the following:</span></span>

1. <span data-ttu-id="20d35-110">Abra el proyecto con Eclipse.</span><span class="sxs-lookup"><span data-stu-id="20d35-110">Open your project with Eclipse.</span></span>

2. <span data-ttu-id="20d35-111">Haga clic en **Herramientas** y, luego, en **Azure**y en **Iniciar sesión**.</span><span class="sxs-lookup"><span data-stu-id="20d35-111">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>
   <span data-ttu-id="20d35-112">![Menú de Eclipse para iniciar sesión en Azure][I01]</span><span class="sxs-lookup"><span data-stu-id="20d35-112">![Eclipse Menu for Azure Sign In][I01]</span></span>

3. <span data-ttu-id="20d35-113">En la ventana **Inicio de sesión de Azure**, seleccione **Inicio de sesión de dispositivo** y, luego, haga clic en **Iniciar sesión**.</span><span class="sxs-lookup"><span data-stu-id="20d35-113">In the **Azure Sign In** window, select **Device Login**, and then click **Sign in**.</span></span>

   ![Ventana Inicio de sesión de Azure con el inicio de sesión de dispositivo seleccionado][I02]

4. <span data-ttu-id="20d35-115">Haga clic en **Copiar y abrir** en el cuadro de diálogo **Inicio de sesión de dispositivo de Azure**.</span><span class="sxs-lookup"><span data-stu-id="20d35-115">Click **Copy&Open** in **Azure Device Login** dialog .</span></span>

   ![El cuadro de diálogo Inicio de sesión en Microsoft Azure][I03]

> [!NOTE]
>
> <span data-ttu-id="20d35-117">Si no se abre el explorador, configure Eclipse para utilizar un explorador externo, como Internet Explorer, Firefox o Chrome:</span><span class="sxs-lookup"><span data-stu-id="20d35-117">If the browser doesn't open, configure Eclipse to use an external browser like Internet Explorer, Firefox, or Chrome:</span></span>
>
> 1. <span data-ttu-id="20d35-118">En Eclipse, abra Preferencias -> General -> Explorador web -> Usar un explorador web externo</span><span class="sxs-lookup"><span data-stu-id="20d35-118">Open Preferences -> General -> Web Browser -> Use external web browser in Eclipse</span></span>
>
> 2. <span data-ttu-id="20d35-119">Seleccione el explorador que prefiera utilizar</span><span class="sxs-lookup"><span data-stu-id="20d35-119">Select the browser you prefer to use</span></span>
>

5. <span data-ttu-id="20d35-120">En el explorador, pegue el código del dispositivo (que se ha copiado al hacer clic en **Copiar y abrir** en el último paso) y, a continuación, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="20d35-120">In the browser, paste your device code (which has been copied when you clicked **Copy&Open** in last step) and then click **Next**.</span></span>

   ![Explorador de inicio de sesión de dispositivo][I04]

6. <span data-ttu-id="20d35-122">Finalmente, en el cuadro de diálogo **Seleccionar suscripciones**, elija las suscripciones que desea usar y, luego, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="20d35-122">Finally, in the **Select Subscriptions** dialog box, select the subscriptions that you want to use, then click **OK**.</span></span>

   ![Cuadro de diálogo Seleccionar suscripciones][I05]

## <a name="sign-in-to-your-azure-account-by-service-principal"></a><span data-ttu-id="20d35-124">Inicio de sesión en su cuenta de Azure mediante entidad de servicio</span><span class="sxs-lookup"><span data-stu-id="20d35-124">Sign in to your Azure account by Service Principal</span></span>

<span data-ttu-id="20d35-125">Los siguientes pasos lo guiarán por el proceso de creación de un archivo de credenciales que contiene los datos de entidades de servicio.</span><span class="sxs-lookup"><span data-stu-id="20d35-125">This section walks you through creating a credentials file that contains your service principal data.</span></span> <span data-ttu-id="20d35-126">Cuando finalice este proceso, Eclipse usará el archivo de credenciales para iniciar sesión automáticamente en Azure cuando abra el proyecto.</span><span class="sxs-lookup"><span data-stu-id="20d35-126">After you have completed this process, Eclipse uses the credentials file to automatically sign you in to Azure when open your project.</span></span>

1. <span data-ttu-id="20d35-127">Abra el proyecto con Eclipse.</span><span class="sxs-lookup"><span data-stu-id="20d35-127">Open your project with Eclipse.</span></span>

2. <span data-ttu-id="20d35-128">Haga clic en **Herramientas** y, luego, en **Azure**y en **Iniciar sesión**.</span><span class="sxs-lookup"><span data-stu-id="20d35-128">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>
   <span data-ttu-id="20d35-129">![Comando de inicio de sesión en Azure de Eclipse][A01]</span><span class="sxs-lookup"><span data-stu-id="20d35-129">![The Eclipse Azure Sign In command][A01]</span></span>

3. <span data-ttu-id="20d35-130">En la ventana **Iniciar sesión de Azure**, seleccione **Entidad de servicio**.</span><span class="sxs-lookup"><span data-stu-id="20d35-130">In the **Azure Sign In** window, select **Service Principal**.</span></span> <span data-ttu-id="20d35-131">Si aún no tiene el archivo de autenticación de la entidad de servicio, haga clic en **Nuevo** para crear uno.</span><span class="sxs-lookup"><span data-stu-id="20d35-131">If you do not have the service principal authentication file yet, click **New** to create one.</span></span> <span data-ttu-id="20d35-132">En caso contrario, haga clic en **Examinar** para abrirlo y vaya al paso 8.</span><span class="sxs-lookup"><span data-stu-id="20d35-132">Otherwise you can click **Browse** to open it and jump to step 8.</span></span>

   ![Ventana de inicio de sesión de Azure con la entidad de servicio seleccionada][A02]

4. <span data-ttu-id="20d35-134">Haga clic en **Copiar y abrir** en el cuadro de diálogo **Inicio de sesión de dispositivo de Azure**.</span><span class="sxs-lookup"><span data-stu-id="20d35-134">Click **Copy&Open** in **Azure Device Login** dialog.</span></span>

   ![El cuadro de diálogo Inicio de sesión en Microsoft Azure][A08]

> [!NOTE]
>
> <span data-ttu-id="20d35-136">Si no se abre el explorador, configure Eclipse para utilizar un explorador externo, como Internet Explorer o Chrome:</span><span class="sxs-lookup"><span data-stu-id="20d35-136">If the browser doesn't open, configure eclipse to use an external browser like IE or Chrome:</span></span>
>
> 1. <span data-ttu-id="20d35-137">En Eclipse, abra Preferencias -> General -> Explorador web -> Usar un explorador web externo.</span><span class="sxs-lookup"><span data-stu-id="20d35-137">Open Preferences -> General -> Web Browser -> Use external web browser in Eclipse</span></span>
>
> 2. <span data-ttu-id="20d35-138">Seleccione el explorador que prefiera utilizar.</span><span class="sxs-lookup"><span data-stu-id="20d35-138">Select the browser you prefer to use</span></span>
>

5. <span data-ttu-id="20d35-139">En el explorador, pegue el código del dispositivo (que se ha copiado al hacer clic en **Copiar y abrir** en el último paso) y, a continuación, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="20d35-139">In the browser, paste your device code (which has been copied when you click **Copy&Open** in last step) and then click **Next**.</span></span>

   ![Explorador de inicio de sesión de dispositivo][A03]

6. <span data-ttu-id="20d35-141">En la ventana **Create authentication files** (Crear archivos de autenticación), seleccione las suscripciones que desea utilizar, elija el directorio de destino y, luego, haga clic en **Iniciar**.</span><span class="sxs-lookup"><span data-stu-id="20d35-141">In the **Create Authentication Files** window, select the subscriptions that you want to use, choose your destination directory, and then click **Start**.</span></span>

   ![La ventana Create authentication files (Crear archivos de autenticación)][A04]

7. <span data-ttu-id="20d35-143">En el cuadro de diálogo **Estado de creación de entidades de servicio**, una vez que se hayan creado correctamente los archivos, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="20d35-143">In the **Service Principal Creation Status** dialog box, click **OK** after your files have been created successfully.</span></span>

   ![El cuadro de diálogo Service Principal Creation Status (Estado de creación de entidades de servicio)][A05]

8. <span data-ttu-id="20d35-145">La dirección del archivo creado se rellenará automáticamente en la ventana **Inicio de sesión de Azure**. Ahora, haga clic en **Iniciar sesión**.</span><span class="sxs-lookup"><span data-stu-id="20d35-145">Address of the created file will be automatically filled in the **Azure Sign In** window, now click **Sign in**.</span></span>

   ![Cuadro de diálogo Inicio de sesión en Microsoft Azure][A06]

9. <span data-ttu-id="20d35-147">Finalmente, en el cuadro de diálogo **Seleccionar suscripciones**, elija las suscripciones que desea usar y, luego, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="20d35-147">Finally, in the **Select Subscriptions** dialog box, select the subscriptions that you want to use, then click **OK**.</span></span>

   ![Cuadro de diálogo Seleccionar suscripciones][A07]

## <a name="sign-out-of-your-azure-account"></a><span data-ttu-id="20d35-149">Cierre de sesión en la cuenta de Azure</span><span class="sxs-lookup"><span data-stu-id="20d35-149">Sign out of your Azure account</span></span>

<span data-ttu-id="20d35-150">Después de haber configurado la cuenta con los pasos anteriores, iniciará sesión automáticamente cada vez que inicie Eclipse.</span><span class="sxs-lookup"><span data-stu-id="20d35-150">After you have configured your account by preceding steps, you will be automatically signed in each time you start Eclipse.</span></span> <span data-ttu-id="20d35-151">Sin embargo, si desea cerrar sesión de su cuenta de Azure, siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="20d35-151">However, if you want to sign out of your Azure account, use the following steps.</span></span>

1. <span data-ttu-id="20d35-152">En Eclipse, haga clic en **Herramientas** y, luego, en **Azure** y en **Cerrar sesión**.</span><span class="sxs-lookup"><span data-stu-id="20d35-152">In Eclipse, click **Tools**, then click **Azure**, and then click **Sign Out**.</span></span>

   ![Menú de Eclipse para cerrar sesión en Azure][L01]

2. <span data-ttu-id="20d35-154">Cuando se muestre el cuadro de diálogo **Cierre de sesión en Microsoft Azure** , haga clic en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="20d35-154">When the **Azure Sign Out** dialog box appears, click **Yes**.</span></span>

   ![Cuadro de diálogo Cerrar sesión][L02]

## <a name="next-steps"></a><span data-ttu-id="20d35-156">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="20d35-156">Next steps</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<!-- URL List -->


<!-- IMG List -->

[I01]: media/azure-toolkit-for-eclipse-sign-in-instructions/I01.png
[I02]: media/azure-toolkit-for-eclipse-sign-in-instructions/I02.png
[I03]: media/azure-toolkit-for-eclipse-sign-in-instructions/I03.png
[I04]: media/azure-toolkit-for-eclipse-sign-in-instructions/I04.png
[I05]: media/azure-toolkit-for-eclipse-sign-in-instructions/I05.png

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
