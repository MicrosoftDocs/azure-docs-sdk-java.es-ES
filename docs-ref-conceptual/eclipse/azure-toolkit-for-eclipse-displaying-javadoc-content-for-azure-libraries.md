---
title: Visualización del contenido de Javadoc en Eclipse para el paquete de bibliotecas de Azure para Java
description: Cómo mostrar el contenido de Javadoc para las bibliotecas de Azure en Eclipse
services: ''
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: 30f8b6a1-1d76-4d1c-861b-1db478c46e6b
ms.author: robmcm
ms.date: 02/01/2018
ms.devlang: Java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: 6f1edcc1411e8ec716dbfe41271d21d2397515c5
ms.sourcegitcommit: 151aaa6ccc64d94ed67f03e846bab953bde15b4a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/03/2018
ms.locfileid: "28954506"
---
# <a name="displaying-javadoc-content-in-eclipse-for-the-azure-libraries-package-for-java"></a><span data-ttu-id="01711-103">Visualización del contenido de Javadoc en Eclipse para el paquete de bibliotecas de Azure para Java</span><span class="sxs-lookup"><span data-stu-id="01711-103">Displaying Javadoc Content in Eclipse for the Azure Libraries Package for Java</span></span>

<span data-ttu-id="01711-104">El contenido de Javadoc de las bibliotecas de Azure para Java se puede ver en el entorno de Eclipse asociando el contenido de Javadoc a las bibliotecas de Azure para Java.</span><span class="sxs-lookup"><span data-stu-id="01711-104">The Javadoc content for the Azure Libraries for Java can be viewed within your Eclipse environment by associating the Javadoc content to the Azure Libraries for Java.</span></span> <span data-ttu-id="01711-105">En los pasos siguientes se muestra cómo usar esta funcionalidad en Eclipse.</span><span class="sxs-lookup"><span data-stu-id="01711-105">The following steps show you how to use this functionality within Eclipse.</span></span>

<span data-ttu-id="01711-106">Este procedimiento supone que ya ha agregado la biblioteca de Azure para Java a su ruta de acceso de compilación.</span><span class="sxs-lookup"><span data-stu-id="01711-106">This procedure assumes you have already added the Azure Library for Java to your build path.</span></span>

## <a name="to-display-javadoc-content-in-eclipse-for-the-azure-libraries-for-java"></a><span data-ttu-id="01711-107">Para mostrar el contenido de Javadoc en Eclipse para las bibliotecas de Azure para Java</span><span class="sxs-lookup"><span data-stu-id="01711-107">To display Javadoc content in Eclipse for the Azure Libraries for Java</span></span>

1. <span data-ttu-id="01711-108">En el Explorador de proyectos de Eclipse, en la sección del proyecto **Bibliotecas de referencia** , abra el menú contextual de la biblioteca de Azure para JAR de Java.</span><span class="sxs-lookup"><span data-stu-id="01711-108">Within Eclipse's Project Explorer, in the **Referenced Libraries** section of your project, open the context menu for the Azure Library for Java JAR.</span></span> <span data-ttu-id="01711-109">Por ejemplo, **microsoft-windowsazure-api-0.1.0.jar** (el número de versión puede ser diferente, en función de la versión que haya instalado).</span><span class="sxs-lookup"><span data-stu-id="01711-109">For example, **microsoft-windowsazure-api-0.1.0.jar** (the version number may be different, dependent upon which version you have installed).</span></span>

1. <span data-ttu-id="01711-110">Haga clic en **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="01711-110">Click **Properties**.</span></span>

1. <span data-ttu-id="01711-111">En el cuadro de diálogo **Properties** (Propiedades), en el panel izquierdo, haga clic en **Javadoc Location** (Ubicación de Javadoc).</span><span class="sxs-lookup"><span data-stu-id="01711-111">Within the **Properties** dialog, in the left-hand pane, click **Javadoc Location**.</span></span> <span data-ttu-id="01711-112">Aparecerá el cuadro de diálogo **Ubicación de Javadoc** .</span><span class="sxs-lookup"><span data-stu-id="01711-112">The **Javadoc Location** dialog is displayed.</span></span>

1. <span data-ttu-id="01711-113">Puede especificar una **Javadoc URL** (URL de Javadoc) o un **Javadoc in archive** (Javadoc en archivo).</span><span class="sxs-lookup"><span data-stu-id="01711-113">You can specify a **Javadoc URL**, or a **Javadoc in archive**.</span></span>

   * <span data-ttu-id="01711-114">Si decide especificar una **URL de Javadoc**, use las direcciones URL como **http://dl.windowsazure.com/javadoc** o **http://dl.windowsazure.com/storage/javadoc**.</span><span class="sxs-lookup"><span data-stu-id="01711-114">If you choose to specify a **Javadoc URL**, use the URLs such as **http://dl.windowsazure.com/javadoc** or **http://dl.windowsazure.com/storage/javadoc**.</span></span>

   * <span data-ttu-id="01711-115">Si decide usar **Javadoc en archivo**, puede especificar un archivo externo o un archivo de área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="01711-115">If you choose to use **Javadoc in archive**, you can specify an external file, or a workspace file.</span></span>

   <span data-ttu-id="01711-116">Realice su elección y examine o valide según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="01711-116">Make your choice and browse/validate as needed.</span></span> <span data-ttu-id="01711-117">En el ejemplo siguiente se asocian las bibliotecas de Azure para Java con el JAR de Javadoc correspondiente que se ha descargado localmente en una carpeta denominada **c:\MyAzureJARs**.</span><span class="sxs-lookup"><span data-stu-id="01711-117">The following example associates the Azure Libraries for Java with the corresponding Javadoc JAR that has been downloaded locally to a folder named **c:\MyAzureJARs**.</span></span>

   ![Muestre el contenido de Javadoc.][ic553487]

1. <span data-ttu-id="01711-119">*Paso opcional*: haga clic en **Validar**.</span><span class="sxs-lookup"><span data-stu-id="01711-119">*Optional Step*: Click **Validate**.</span></span> <span data-ttu-id="01711-120">Aquí podrían mostrarse posibles problemas con el JAR de Javadoc.</span><span class="sxs-lookup"><span data-stu-id="01711-120">Potential issues with the Javadoc JAR could be displayed here.</span></span>

1. <span data-ttu-id="01711-121">Haga clic en **OK**.</span><span class="sxs-lookup"><span data-stu-id="01711-121">Click **OK**.</span></span>

<span data-ttu-id="01711-122">Una vez asociado a la biblioteca, el contenido de Javadoc debe mostrarse dentro del IDE de Eclipse.</span><span class="sxs-lookup"><span data-stu-id="01711-122">Once associated with the library, the Javadoc content should display within your Eclipse IDE.</span></span> <span data-ttu-id="01711-123">Por ejemplo, si `blob` se define del tipo `CloudBlockBlob` dentro de su código, el siguiente es un ejemplo del contenido de Javadoc que aparece cuando escribe `blob.acquireLease` en el código:</span><span class="sxs-lookup"><span data-stu-id="01711-123">For example, if `blob` is defined of type `CloudBlockBlob` within your code, the following is an example of Javadoc content that appears when you type `blob.acquireLease` in code:</span></span>

![Muestre el contenido de Javadoc.][ic553488]

## <a name="next-steps"></a><span data-ttu-id="01711-125">pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="01711-125">Next steps</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<!-- URL List -->

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh698319.aspx -->

<!-- IMG List -->

[ic553487]: media/azure-toolkit-for-eclipse-displaying-javadoc-content-for-azure-libraries/ic553487.png
[ic553488]: media/azure-toolkit-for-eclipse-displaying-javadoc-content-for-azure-libraries/ic553488.png
