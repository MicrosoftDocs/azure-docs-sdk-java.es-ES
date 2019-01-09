---
title: Cómo crear una aplicación de Spring Cloud Stream Binder con Azure Event Hubs
description: Obtenga información sobre cómo configurar una aplicación de Spring Cloud Stream Binder basada en Java creada con Spring Boot Initializr con Azure Event Hubs.
services: event-hubs
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 12/19/2018
ms.devlang: java
ms.service: event-hubs
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: na
ms.openlocfilehash: 98b3dc1243bf293ede121eafd51b041649d165db
ms.sourcegitcommit: f0f140b0862ca5338b1b7e5c33cec3e58a70b8fd
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/03/2019
ms.locfileid: "53991429"
---
# <a name="how-to-create-a-spring-cloud-stream-binder-application-with-azure-event-hubs"></a><span data-ttu-id="8786e-103">Cómo crear una aplicación de Spring Cloud Stream Binder con Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="8786e-103">How to create a Spring Cloud Stream Binder application with Azure Event Hubs</span></span>

## <a name="overview"></a><span data-ttu-id="8786e-104">Información general</span><span class="sxs-lookup"><span data-stu-id="8786e-104">Overview</span></span>

<span data-ttu-id="8786e-105">En este artículo se muestra cómo configurar una aplicación de Spring Cloud Stream Binder basada en Java creada con Spring Boot Initializer con Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="8786e-105">This article demonstrates how to configure a Java-based Spring Cloud Stream Binder application created with the Spring Boot Initializer with Azure Event Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8786e-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="8786e-106">Prerequisites</span></span>

<span data-ttu-id="8786e-107">Los siguientes requisitos previos son necesarios para seguir los pasos descritos en este artículo:</span><span class="sxs-lookup"><span data-stu-id="8786e-107">The following prerequisites are required in order to follow the steps in this article:</span></span>

* <span data-ttu-id="8786e-108">Una suscripción de Azure. Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN] o registrarse para obtener una [cuenta de Azure gratuita].</span><span class="sxs-lookup"><span data-stu-id="8786e-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="8786e-109">Un kit de desarrollo de Java (JDK) admitido</span><span class="sxs-lookup"><span data-stu-id="8786e-109">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="8786e-110">Para más información sobre los JDK disponibles para desarrollar en Azure, consulte <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="8786e-110">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="8786e-111">[Apache Maven](http://maven.apache.org/), versión 3.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="8786e-111">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

> [!IMPORTANT]
>
> <span data-ttu-id="8786e-112">Se necesita Spring Boot versión 2.0 o posteriores para completar los pasos descritos en este artículo.</span><span class="sxs-lookup"><span data-stu-id="8786e-112">Spring Boot version 2.0 or greater is required to complete the steps in this article.</span></span>
>

## <a name="create-an-azure-event-hub-using-the-azure-portal"></a><span data-ttu-id="8786e-113">Creación de un centro de eventos de Azure mediante Azure Portal</span><span class="sxs-lookup"><span data-stu-id="8786e-113">Create an Azure Event Hub using the Azure portal</span></span>

### <a name="create-an-azure-event-hub-namespace"></a><span data-ttu-id="8786e-114">Creación de un espacio de nombres del centro de eventos de Azure</span><span class="sxs-lookup"><span data-stu-id="8786e-114">Create an Azure Event Hub Namespace</span></span>

1. <span data-ttu-id="8786e-115">Vaya a Azure Portal en <https://portal.azure.com/> e inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="8786e-115">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="8786e-116">Haga clic en **+Crear un recurso**, en **Internet de las cosas** y en **Event Hubs**.</span><span class="sxs-lookup"><span data-stu-id="8786e-116">Click **+Create a resource**, then **Internet of Things**, and then click **Event Hubs**.</span></span>

   ![Creación de un espacio de nombres del centro de eventos de Azure][IMG01]

1. <span data-ttu-id="8786e-118">En la página **Crear espacio de nombres**, escriba la información siguiente:</span><span class="sxs-lookup"><span data-stu-id="8786e-118">On the **Create Namespace** page, enter the following information:</span></span>

   * <span data-ttu-id="8786e-119">Escriba un **Nombre** único, que pasará a formar parte del identificador URI del espacio de nombres del centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="8786e-119">Enter a unique **Name**, which will become part of the URI for your event hub namespace.</span></span> <span data-ttu-id="8786e-120">Por ejemplo: si escribió **wingtiptoys** para el **Nombre**, el identificador URI sería *wingtiptoys.servicebus.windows.net*.</span><span class="sxs-lookup"><span data-stu-id="8786e-120">For example: if you entered **wingtiptoys** for the **Name**, the URI would be *wingtiptoys.servicebus.windows.net*.</span></span>
   * <span data-ttu-id="8786e-121">Elija un **Plan de tarifa** para el espacio de nombres del centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="8786e-121">Choose a **Pricing tier** for your event hub namespace.</span></span>
   * <span data-ttu-id="8786e-122">Elija la **Suscripción** que quiere usar para el espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="8786e-122">Choose the **Subscription** you want to use for your namespace.</span></span>
   * <span data-ttu-id="8786e-123">Especifique si quiere crear un nuevo **Grupo de recursos** para el espacio de nombres o elija un grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="8786e-123">Specify whether to create a new **Resource group** for your namespace, or choose an existing resource group.</span></span>
   * <span data-ttu-id="8786e-124">Especifique la **Ubicación** del espacio de nombres del centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="8786e-124">Specify the **Location** for your event hub namespace.</span></span>

   ![Especificación de las opciones del espacio de nombres del centro de eventos de Azure][IMG02]

1. <span data-ttu-id="8786e-126">Cuando haya especificado las opciones enumeradas anteriormente, haga clic en **Crear** para crear el espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="8786e-126">When you have specified the options listed above, click **Create** to create your namespace.</span></span>

### <a name="create-an-azure-event-hub-in-your-namespace"></a><span data-ttu-id="8786e-127">Creación de un centro de eventos de Azure en el espacio de nombres</span><span class="sxs-lookup"><span data-stu-id="8786e-127">Create an Azure Event Hub in your namespace</span></span>

1. <span data-ttu-id="8786e-128">Vaya a Azure Portal en <https://portal.azure.com/>.</span><span class="sxs-lookup"><span data-stu-id="8786e-128">Browse to the Azure portal at <https://portal.azure.com/>.</span></span>

1. <span data-ttu-id="8786e-129">Haga clic en **Todos los recursos** y, a continuación, en el espacio de nombres que ha creado.</span><span class="sxs-lookup"><span data-stu-id="8786e-129">Click **All resources**, and then click the namespace that you created.</span></span>

   ![Selección del espacio de nombres del centro de eventos de Azure][IMG03]

1. <span data-ttu-id="8786e-131">Haga clic en **Event Hubs** y, a continuación, haga clic en **+Centro de eventos**.</span><span class="sxs-lookup"><span data-stu-id="8786e-131">Click **Event Hubs**, and then click **+Event Hub**.</span></span>

   ![Adición de un nuevo centro de eventos de Azure][IMG04]

1. <span data-ttu-id="8786e-133">En la página **Crear centro de eventos**, escriba un **Nombre** único para el centro de eventos y haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="8786e-133">On the **Create Event Hub** page, enter a unique **Name** for your Event Hub, and then click **Create**.</span></span>

   ![Creación de un Centro de eventos de Azure][IMG05]

1. <span data-ttu-id="8786e-135">Cuando se haya creado el centro de eventos, se mostrará en la página **Event Hubs**.</span><span class="sxs-lookup"><span data-stu-id="8786e-135">When your Event Hub has been created, it will be listed on the **Event Hubs** page.</span></span>

   ![Creación de un Centro de eventos de Azure][IMG06]

### <a name="create-an-azure-storage-account-for-your-event-hub-checkpoints"></a><span data-ttu-id="8786e-137">Creación de una cuenta de Azure Storage para los puntos de comprobación del centro de eventos</span><span class="sxs-lookup"><span data-stu-id="8786e-137">Create an Azure Storage Account for your Event Hub checkpoints</span></span>

1. <span data-ttu-id="8786e-138">Vaya a Azure Portal en <https://portal.azure.com/>.</span><span class="sxs-lookup"><span data-stu-id="8786e-138">Browse to the Azure portal at <https://portal.azure.com/>.</span></span>

1. <span data-ttu-id="8786e-139">Haga clic en **+Crear un recurso**, en **Almacenamiento** y en **Cuenta de almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="8786e-139">Click **+Create a resource**, then **Storage**, and then click **Storage Account**.</span></span>

   ![Creación de una cuenta de Azure Storage][IMG07]

1. <span data-ttu-id="8786e-141">En la página **Crear espacio de nombres**, escriba la información siguiente:</span><span class="sxs-lookup"><span data-stu-id="8786e-141">On the **Create Namespace** page, enter the following information:</span></span>

   * <span data-ttu-id="8786e-142">Escriba un **Nombre** único, que pasará a formar parte del identificador URI de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="8786e-142">Enter a unique **Name**, which will become part of the URI for your storage account.</span></span> <span data-ttu-id="8786e-143">Por ejemplo: si escribió **wingtiptoys** para el **Nombre**, el identificador URI sería *wingtiptoys.core.windows.net*.</span><span class="sxs-lookup"><span data-stu-id="8786e-143">For example: if you entered **wingtiptoys** for the **Name**, the URI would be *wingtiptoys.core.windows.net*.</span></span>
   * <span data-ttu-id="8786e-144">Elija **Blob Storage** para **Tipo de cuenta**.</span><span class="sxs-lookup"><span data-stu-id="8786e-144">Choose **Blob storage** for the **Account kind**.</span></span>
   * <span data-ttu-id="8786e-145">Especifique la **Ubicación** de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="8786e-145">Specify the **Location** for your storage account.</span></span>
   * <span data-ttu-id="8786e-146">Elija la **Suscripción** que quiere usar para la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="8786e-146">Choose the **Subscription** you want to use for your storage account.</span></span>
   * <span data-ttu-id="8786e-147">Especifique si quiere crear un nuevo **Grupo de recursos** para la cuenta de almacenamiento o elija un grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="8786e-147">Specify whether to create a new **Resource group** for your storage account, or choose an existing resource group.</span></span>

   ![Especificación de las opciones de la cuenta de Azure Storage][IMG08]

1. <span data-ttu-id="8786e-149">Cuando haya especificado las opciones enumeradas anteriormente, haga clic en **Crear** para crear la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="8786e-149">When you have specified the options listed above, click **Create** to create your storage account.</span></span>

## <a name="create-a-simple-spring-boot-application-with-the-spring-initializr"></a><span data-ttu-id="8786e-150">Creación de una aplicación sencilla de Spring Boot con Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="8786e-150">Create a simple Spring Boot application with the Spring Initializr</span></span>

1. <span data-ttu-id="8786e-151">Vaya a <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="8786e-151">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="8786e-152">Especifique las opciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="8786e-152">Specify the following options:</span></span>

   * <span data-ttu-id="8786e-153">Genere un proyecto de **Maven** con **Java**.</span><span class="sxs-lookup"><span data-stu-id="8786e-153">Generate a **Maven** project with **Java**.</span></span>
   * <span data-ttu-id="8786e-154">Especifique una versión de **Spring Boot** igual o superior a la 2.0.</span><span class="sxs-lookup"><span data-stu-id="8786e-154">Specify a **Spring Boot** version that is equal to or greater than 2.0.</span></span>
   * <span data-ttu-id="8786e-155">Especifique los nombres de **Group** (Grupo) y **Artifact** (Artefacto) de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8786e-155">Specify the **Group** and **Artifact** names for your application.</span></span>
   * <span data-ttu-id="8786e-156">Agregue la dependencia **Web**.</span><span class="sxs-lookup"><span data-stu-id="8786e-156">Add the **Web** dependency.</span></span>

      ![Opciones básicas de Spring Initializr][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="8786e-158">Spring Initializr usa los nombres de **Group** (Grupo) y **Artifact** (Artefacto) para crear el nombre del paquete, por ejemplo: *com.wingtiptoys.eventhub*.</span><span class="sxs-lookup"><span data-stu-id="8786e-158">The Spring Initializr uses the **Group** and **Artifact** names to create the package name; for example: *com.wingtiptoys.eventhub*.</span></span>
   >

1. <span data-ttu-id="8786e-159">Cuando haya especificado las opciones enumeradas anteriormente, haga clic en **Generate Project** (Generar proyecto).</span><span class="sxs-lookup"><span data-stu-id="8786e-159">When you have specified the options listed above, click **Generate Project**.</span></span>

1. <span data-ttu-id="8786e-160">Cuando se le solicite, descargue el proyecto en una ruta de acceso del equipo local.</span><span class="sxs-lookup"><span data-stu-id="8786e-160">When prompted, download the project to a path on your local computer.</span></span>

   ![Descarga del proyecto de Spring][SI02]

1. <span data-ttu-id="8786e-162">Después de extraer los archivos en el sistema local, la aplicación sencilla de Spring Boot estará lista para editarla.</span><span class="sxs-lookup"><span data-stu-id="8786e-162">After you have extracted the files on your local system, your simple Spring Boot application will be ready for editing.</span></span>

## <a name="configure-your-spring-boot-app-to-use-the-azure-event-hub-starter"></a><span data-ttu-id="8786e-163">Configuración de la aplicación de Spring Boot para usar el iniciador del centro de eventos de Azure</span><span class="sxs-lookup"><span data-stu-id="8786e-163">Configure your Spring Boot app to use the Azure Event Hub starter</span></span>

1. <span data-ttu-id="8786e-164">Busque el archivo *pom.xml* en el directorio raíz de la aplicación, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="8786e-164">Locate the *pom.xml* file in the root directory of your app; for example:</span></span>

   `C:\SpringBoot\eventhub\pom.xml`

   <span data-ttu-id="8786e-165">O bien</span><span class="sxs-lookup"><span data-stu-id="8786e-165">-or-</span></span>

   `/users/example/home/eventhub/pom.xml`

1. <span data-ttu-id="8786e-166">Abra el archivo *pom.xml* en un editor de texto y agregue el iniciador Spring Cloud Azure Event Hub Stream Binder a la lista `<dependencies>`:</span><span class="sxs-lookup"><span data-stu-id="8786e-166">Open the *pom.xml* file in a text editor, and add the Spring Cloud Azure Event Hub Stream Binder starter to the list of `<dependencies>`:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>spring-cloud-azure-eventhub-stream-binder</artifactId>
      <version>1.0.0.M2</version>
   </dependency>
   ```

   ![Edición del archivo pom.xml][SI03]

1. <span data-ttu-id="8786e-168">Guarde y cierre el archivo *pom.xml*.</span><span class="sxs-lookup"><span data-stu-id="8786e-168">Save and close the *pom.xml* file.</span></span>

## <a name="create-an-azure-credential-file"></a><span data-ttu-id="8786e-169">Creación de un archivo de credenciales de Azure</span><span class="sxs-lookup"><span data-stu-id="8786e-169">Create an Azure Credential File</span></span>

1. <span data-ttu-id="8786e-170">Abra el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="8786e-170">Open a command prompt.</span></span>

1. <span data-ttu-id="8786e-171">Vaya al directorio *resources* de la aplicación de Spring Boot, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="8786e-171">Navigate to the *resources* directory of your Spring Boot app; for example:</span></span>

   ```shell
   cd C:\SpringBoot\eventhub\src\main\resources
   ```

   <span data-ttu-id="8786e-172">O bien</span><span class="sxs-lookup"><span data-stu-id="8786e-172">-or-</span></span>

   ```shell
   cd /users/example/home/eventhub/src/main/resources
   ```

1. <span data-ttu-id="8786e-173">Inicio de sesión en la cuenta de Azure</span><span class="sxs-lookup"><span data-stu-id="8786e-173">Sign in to your Azure account:</span></span>

   ```azurecli
   az login
   ```

1. <span data-ttu-id="8786e-174">Muestre las suscripciones:</span><span class="sxs-lookup"><span data-stu-id="8786e-174">List your subscriptions:</span></span>

   ```azurecli
   az account list
   ```
   <span data-ttu-id="8786e-175">Azure devolverá la lista de sus suscripciones, y tendrá que copiar el GUID de la suscripción que desea usar; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="8786e-175">Azure will return a list of your subscriptions, and you will need to copy the GUID for the subscription that you want to use; for example:</span></span>

   ```json
   [
     {
       "cloudName": "AzureCloud",
       "id": "11111111-1111-1111-1111-111111111111",
       "isDefault": true,
       "name": "Converted Windows Azure MSDN - Visual Studio Ultimate",
       "state": "Enabled",
       "tenantId": "22222222-2222-2222-2222-222222222222",
       "user": {
         "name": "gena.soto@wingtiptoys.com",
         "type": "user"
       }
     }
   ]
   ```
1. <span data-ttu-id="8786e-176">Especifique el identificador GUID de la suscripción que desea usar con Azure; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="8786e-176">Specify the GUID for the subscription you want to use with Azure; for example:</span></span>

   ```azurecli
   az account set -s 11111111-1111-1111-1111-111111111111
   ```

1. <span data-ttu-id="8786e-177">Cree el archivo de credenciales de Azure:</span><span class="sxs-lookup"><span data-stu-id="8786e-177">Create your Azure Credential file:</span></span>

   ```azurecli
   az ad sp create-for-rbac --sdk-auth > my.azureauth
   ```

   <span data-ttu-id="8786e-178">Este comando crea un archivo *my.azureauth* en el directorio *resources* con un contenido similar al del siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="8786e-178">This command will create a *my.azureauth* file in your *resources* directory with contents that resemble the following example:</span></span>

   ```json
   {
     "clientId": "33333333-3333-3333-3333-333333333333",
     "clientSecret": "44444444-4444-4444-4444-444444444444",
     "subscriptionId": "11111111-1111-1111-1111-111111111111",
     "tenantId": "22222222-2222-2222-2222-222222222222",
     "activeDirectoryEndpointUrl": "https://login.microsoftonline.com",
     "resourceManagerEndpointUrl": "https://management.azure.com/",
     "activeDirectoryGraphResourceId": "https://graph.windows.net/",
     "sqlManagementEndpointUrl": "https://management.core.windows.net:8443/",
     "galleryEndpointUrl": "https://gallery.azure.com/",
     "managementEndpointUrl": "https://management.core.windows.net/"
   }
   ```

## <a name="configure-your-spring-boot-app-to-use-your-azure-event-hub"></a><span data-ttu-id="8786e-179">Configuración de la aplicación de Spring Boot para usar el centro de eventos de Azure</span><span class="sxs-lookup"><span data-stu-id="8786e-179">Configure your Spring Boot app to use your Azure Event Hub</span></span>

1. <span data-ttu-id="8786e-180">Busque el archivo *application.properties* en el directorio *resources* de la aplicación, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="8786e-180">Locate the *application.properties* in the *resources* directory of your app; for example:</span></span>

   `C:\SpringBoot\eventhub\src\main\resources\application.properties`

   <span data-ttu-id="8786e-181">O bien</span><span class="sxs-lookup"><span data-stu-id="8786e-181">-or-</span></span>

   `/users/example/home/eventhub/src/main/resources/application.properties`

2. <span data-ttu-id="8786e-182">Abra el archivo *application.properties* en un editor de texto, agregue las siguientes líneas y, a continuación, sustituya los valores de ejemplo por las propiedades adecuadas del centro de eventos:</span><span class="sxs-lookup"><span data-stu-id="8786e-182">Open the *application.properties* file in a text editor, add the following lines, and then replace the sample values with the appropriate properties for your event hub:</span></span>

   ```yaml
   spring.cloud.azure.credential-file-path=my.azureauth
   spring.cloud.azure.resource-group=wingtiptoysresources
   spring.cloud.azure.region=West US
   spring.cloud.azure.eventhub.namespace=wingtiptoysnamespace
   spring.cloud.azure.eventhub.checkpoint-storage-account=wingtiptoysstorage
   spring.cloud.stream.bindings.input.destination=wingtiptoyshub
   spring.cloud.stream.bindings.input.group=$Default
   spring.cloud.stream.bindings.output.destination=wingtiptoyshub
   spring.cloud.stream.eventhub.bindings.input.consumer.checkpoint-mode=MANUAL
   ```
   <span data-ttu-id="8786e-183">Donde:</span><span class="sxs-lookup"><span data-stu-id="8786e-183">Where:</span></span>

   |                          <span data-ttu-id="8786e-184">Campo</span><span class="sxs-lookup"><span data-stu-id="8786e-184">Field</span></span>                           |                                                                                   <span data-ttu-id="8786e-185">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="8786e-185">Description</span></span>                                                                                    |
   |----------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   |        `spring.cloud.azure.credential-file-path`         |                                                    <span data-ttu-id="8786e-186">Especifica el archivo de credenciales de Azure que creó anteriormente en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="8786e-186">Specifies Azure credential file that you created earlier in this tutorial.</span></span>                                                    |
   |           `spring.cloud.azure.resource-group`            |                                                      <span data-ttu-id="8786e-187">Especifica el grupo de recursos de Azure que contiene el centro de eventos de Azure.</span><span class="sxs-lookup"><span data-stu-id="8786e-187">Specifies the Azure Resource Group that contains your Azure Event Hub.</span></span>                                                      |
   |               `spring.cloud.azure.region`                |                                           <span data-ttu-id="8786e-188">Especifica la región geográfica que seleccionó cuando creó el centro de eventos de Azure.</span><span class="sxs-lookup"><span data-stu-id="8786e-188">Specifies the geographical region that you specified when you created your Azure Event Hub.</span></span>                                            |
   |         `spring.cloud.azure.eventhub.namespace`          |                                          <span data-ttu-id="8786e-189">Especifica el nombre único que proporcionó cuando creó el espacio de nombres del centro de eventos de Azure.</span><span class="sxs-lookup"><span data-stu-id="8786e-189">Specifies the unique name that you specified when you created your Azure Event Hub Namespace.</span></span>                                           |
   | `spring.cloud.azure.eventhub.checkpoint-storage-account` |                                                    <span data-ttu-id="8786e-190">Especifica la cuenta de Azure Storage que creó anteriormente en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="8786e-190">Specifies Azure Storage Account that you created earlier in this tutorial.</span></span>                                                    |
   |     `spring.cloud.stream.bindings.input.destination`     |                            <span data-ttu-id="8786e-191">Especifica el centro de eventos de Azure del destino de entrada, que para este tutorial es el centro que creó anteriormente en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="8786e-191">Specifies the input destination Azure Event Hub, which for this tutorial is the  hub you created earlier in this tutorial.</span></span>                            |
   |       `spring.cloud.stream.bindings.input.group `        | <span data-ttu-id="8786e-192">Especifica un grupo de consumidores del centro de eventos de Azure, que se puede establecer en "$Default" para poder usar el grupo de consumidores básico que se creó cuando creó el centro de eventos de Azure.</span><span class="sxs-lookup"><span data-stu-id="8786e-192">Specifies a Consumer Group from Azure Event Hub, which can be set to '$Default' in order to use the basic consumer group that was created when you created your Azure Event Hub.</span></span> |
   |    `spring.cloud.stream.bindings.output.destination`     |                               <span data-ttu-id="8786e-193">Especifica el centro de eventos de Azure del destino de salida, que en este tutorial será el mismo que el destino de entrada.</span><span class="sxs-lookup"><span data-stu-id="8786e-193">Specifies the output destination Azure Event Hub, which for this tutorial will be the same as the input destination.</span></span>                               |


3. <span data-ttu-id="8786e-194">Guarde y cierre el archivo *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="8786e-194">Save and close the *application.properties* file.</span></span>

## <a name="add-sample-code-to-implement-basic-event-hub-functionality"></a><span data-ttu-id="8786e-195">Adición de código de ejemplo para implementar la funcionalidad básica del centro de eventos</span><span class="sxs-lookup"><span data-stu-id="8786e-195">Add sample code to implement basic event hub functionality</span></span>

<span data-ttu-id="8786e-196">En esta sección se crean las clases de Java necesarias para enviar eventos al centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="8786e-196">In this section, you create the necessary Java classes for sending events to your event hub.</span></span>

### <a name="modify-the-main-application-class"></a><span data-ttu-id="8786e-197">Modificación de la clase de aplicación principal</span><span class="sxs-lookup"><span data-stu-id="8786e-197">Modify the main application class</span></span>

1. <span data-ttu-id="8786e-198">Busque el archivo de Java de la aplicación principal en el directorio del paquete de la aplicación; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="8786e-198">Locate the main application Java file in the package directory of your app; for example:</span></span>

   `C:\SpringBoot\eventhub\src\main\java\com\wingtiptoys\eventhub\EventhubApplication.java`

   <span data-ttu-id="8786e-199">O bien</span><span class="sxs-lookup"><span data-stu-id="8786e-199">-or-</span></span>

   `/users/example/home/eventhub/src/main/java/com/wingtiptoys/eventhub/EventhubApplication.java`

1. <span data-ttu-id="8786e-200">Abra el archivo de Java de la aplicación principal en un editor de texto y agregue las siguientes líneas al archivo:</span><span class="sxs-lookup"><span data-stu-id="8786e-200">Open the main application Java file in a text editor, and add the following lines to the file:</span></span>

   ```java
   package com.wingtiptoys.eventhub;

   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;

   @SpringBootApplication
   public class EventhubApplication {
      public static void main(String[] args) {
         SpringApplication.run(EventhubApplication.class, args);
      }
   }
   ```

1. <span data-ttu-id="8786e-201">Guarde y cierre el archivo de Java de la aplicación principal.</span><span class="sxs-lookup"><span data-stu-id="8786e-201">Save and close the main application Java file.</span></span>

### <a name="create-a-new-class-for-the-source-connector"></a><span data-ttu-id="8786e-202">Creación de una nueva clase para el conector de origen</span><span class="sxs-lookup"><span data-stu-id="8786e-202">Create a new class for the source connector</span></span>

1. <span data-ttu-id="8786e-203">Cree un archivo de Java nuevo llamado *EventhubSource.java* en el directorio del paquete de la aplicación y, a continuación, abra el archivo en un editor de texto y agregue las siguientes líneas:</span><span class="sxs-lookup"><span data-stu-id="8786e-203">Create a new Java file named *EventhubSource.java* in the package directory of your app, then open the file in a text editor and add the following lines:</span></span>

   ```java
   package com.wingtiptoys.eventhub;

   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.cloud.stream.annotation.EnableBinding;
   import org.springframework.cloud.stream.messaging.Source;
   import org.springframework.messaging.support.GenericMessage;
   import org.springframework.web.bind.annotation.PostMapping;
   import org.springframework.web.bind.annotation.RequestBody;
   import org.springframework.web.bind.annotation.RestController;

   @EnableBinding(Source.class)
   @RestController
   public class EventhubSource {

      @Autowired
      private Source source;

      @PostMapping("/messages")
      public String postMessage(@RequestBody String message) {
         this.source.output().send(new GenericMessage<>(message));
         return message;
      }
   }
   ```
1. <span data-ttu-id="8786e-204">Guarde y cierre el archivo *EventhubSource.java*.</span><span class="sxs-lookup"><span data-stu-id="8786e-204">Save and close the *EventhubSource.java* file.</span></span>

### <a name="create-a-new-class-for-the-sink-connector"></a><span data-ttu-id="8786e-205">Creación de una nueva clase para el conector receptor</span><span class="sxs-lookup"><span data-stu-id="8786e-205">Create a new class for the sink connector</span></span>

1. <span data-ttu-id="8786e-206">Cree un archivo de Java nuevo llamado *EventhubSink.java* en el directorio del paquete de la aplicación y, a continuación, abra el archivo en un editor de texto y agregue las siguientes líneas:</span><span class="sxs-lookup"><span data-stu-id="8786e-206">Create a new Java file named *EventhubSink.java* in the package directory of your app, then open the file in a text editor and add the following lines:</span></span>

   ```java
   package com.wingtiptoys.eventhub;

   import com.microsoft.azure.spring.integration.core.AzureHeaders;
   import com.microsoft.azure.spring.integration.core.api.Checkpointer;
   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   import org.springframework.cloud.stream.annotation.EnableBinding;
   import org.springframework.cloud.stream.annotation.StreamListener;
   import org.springframework.cloud.stream.messaging.Sink;
   import org.springframework.messaging.handler.annotation.Header;

   @EnableBinding(Sink.class)
   public class EventhubSink {

      private static final Logger LOGGER = LoggerFactory.getLogger(EventhubSink.class);

      @StreamListener(Sink.INPUT)
      public void handleMessage(String message, @Header(AzureHeaders.CHECKPOINTER) Checkpointer checkpointer) {
         LOGGER.info("New message received: '{}'", message);
         checkpointer.success().handle((r, ex) -> {
            if (ex == null) {
               LOGGER.info("Message '{}' successfully checkpointed", message);
            }
            return null;
         });
      }
   }
   ```

1. <span data-ttu-id="8786e-207">Guarde y cierre el archivo *EventhubSink.java*.</span><span class="sxs-lookup"><span data-stu-id="8786e-207">Save and close the *EventhubSink.java* file.</span></span>

## <a name="build-and-test-your-application"></a><span data-ttu-id="8786e-208">Compilación y prueba de la aplicación</span><span class="sxs-lookup"><span data-stu-id="8786e-208">Build and test your application</span></span>

1. <span data-ttu-id="8786e-209">Abra un símbolo del sistema y cambie el directorio a la carpeta donde se encuentra el archivo *pom.xml*; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="8786e-209">Open a command prompt and change directory to the folder where your *pom.xml* file is located; for example:</span></span>

   `cd C:\SpringBoot\eventhub`

   <span data-ttu-id="8786e-210">O bien</span><span class="sxs-lookup"><span data-stu-id="8786e-210">-or-</span></span>

   `cd /users/example/home/eventhub`

1. <span data-ttu-id="8786e-211">Compile la aplicación de Spring Boot con Maven y ejecútela; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="8786e-211">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. <span data-ttu-id="8786e-212">Una vez que se está ejecutando la aplicación, puede usar *curl* para probar la aplicación, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="8786e-212">Once your application is running, you can use *curl* to test your application; for example:</span></span>

   ```shell
   curl -X POST -H "Content-Type: text/plain" -d "hello" http://localhost:8080/messages
   ```
   <span data-ttu-id="8786e-213">Debería ver el mensaje "hello" en los registros de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8786e-213">You should see "hello" posted to your application's logs.</span></span> <span data-ttu-id="8786e-214">Por ejemplo: </span><span class="sxs-lookup"><span data-stu-id="8786e-214">For example:</span></span>

   ```shell
   [Thread-13] INFO com.wingtiptoys.eventhub.EventhubSink - New message received: 'hello'
   [pool-10-thread-7] INFO com.wingtiptoys.eventhub.EventhubSink - Message 'hello' successfully checkpointed
   ```

## <a name="next-steps"></a><span data-ttu-id="8786e-215">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8786e-215">Next steps</span></span>

<span data-ttu-id="8786e-216">Para más información acerca de Spring y Azure, vaya al centro de documentación de Azure.</span><span class="sxs-lookup"><span data-stu-id="8786e-216">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8786e-217">Spring en Azure</span><span class="sxs-lookup"><span data-stu-id="8786e-217">Spring on Azure</span></span>](/java/azure/spring-framework)

### <a name="additional-resources"></a><span data-ttu-id="8786e-218">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="8786e-218">Additional Resources</span></span>

<span data-ttu-id="8786e-219">Consulte los siguientes artículos para más información sobre la compatibilidad de Azure para Event Hub Stream Binder:</span><span class="sxs-lookup"><span data-stu-id="8786e-219">For more information about Azure support for Event Hub Stream Binder, see the following articles:</span></span>

* [<span data-ttu-id="8786e-220">¿Qué es Azure Event Hubs?</span><span class="sxs-lookup"><span data-stu-id="8786e-220">What is Azure Event Hubs?</span></span>](/azure/event-hubs/event-hubs-about)

* [<span data-ttu-id="8786e-221">Creación de un espacio de nombres de Event Hubs y un centro de eventos con Azure Portal</span><span class="sxs-lookup"><span data-stu-id="8786e-221">Create an Event Hubs namespace and an event hub using the Azure portal</span></span>](/azure/event-hubs/event-hubs-create)

* [<span data-ttu-id="8786e-222">Cómo usar el iniciador de Spring Boot para Apache Kafka con Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="8786e-222">How to use the Spring Boot Starter for Apache Kafka with Azure Event Hubs</span></span>](configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub.md)

<span data-ttu-id="8786e-223">Para más información sobre el uso de Azure con Java, consulte [Azure para desarrolladores de Java] y [Working with Azure DevOps and Java] (Trabajo con Azure DevOps y Java).</span><span class="sxs-lookup"><span data-stu-id="8786e-223">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Working with Azure DevOps and Java].</span></span>

<span data-ttu-id="8786e-224">**[Spring Framework]** es una solución de código abierto que ayuda a los desarrolladores de Java a crear aplicaciones de nivel empresarial.</span><span class="sxs-lookup"><span data-stu-id="8786e-224">The **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="8786e-225">Uno de los proyectos más populares que se basa en esa plataforma es [Spring Boot], que proporciona un enfoque simplificado para crear aplicaciones de Java independientes.</span><span class="sxs-lookup"><span data-stu-id="8786e-225">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="8786e-226">Para ayudar a los desarrolladores a empezar con Spring Boot, puede encontrar varios paquetes de ejemplo de Spring Boot en <https://github.com/spring-guides/>.</span><span class="sxs-lookup"><span data-stu-id="8786e-226">To help developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>.</span></span> <span data-ttu-id="8786e-227">Además de elegir de la lista de proyectos básicos de Spring Boot, el **[Spring Initializr]** ayuda a los desarrolladores en los primeros pasos para crear aplicaciones de Spring Boot personalizadas.</span><span class="sxs-lookup"><span data-stu-id="8786e-227">In addition to choosing from the list of basic Spring Boot projects, the **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>

<!-- URL List -->

[cuenta de Azure gratuita]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Working with Azure DevOps and Java]: /azure/devops/ (Trabajo con Azure DevOps y Java)
[ventajas como suscriptor de MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[IMG01]: ./media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-event-hub-01.png
[IMG02]: ./media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-event-hub-02.png
[IMG03]: ./media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-event-hub-03.png
[IMG04]: ./media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-event-hub-04.png
[IMG05]: ./media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-event-hub-05.png
[IMG06]: ./media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-event-hub-06.png
[IMG07]: ./media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-event-hub-07.png
[IMG08]: ./media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-event-hub-08.png

[SI01]: ./media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-project-01.png
[SI02]: ./media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-project-02.png
[SI03]: ./media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-project-03.png
