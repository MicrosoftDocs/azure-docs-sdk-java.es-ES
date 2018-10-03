---
title: Cómo usar el iniciador de Spring Boot para Apache Kafka con Azure Event Hubs
description: Aprenda a configurar una aplicación creada con Spring Boot Initializer para usar Apache Kafka con Azure Event Hubs.
services: event-hubs
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 09/10/2018
ms.devlang: java
ms.service: event-hubs
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: na
ms.openlocfilehash: 00062f5442e072af30036388f2f1f066221d7316
ms.sourcegitcommit: fd67d4088be2cad01c642b9ecf3f9475d9cb4f3c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/21/2018
ms.locfileid: "46506587"
---
# <a name="how-to-use-the-spring-boot-starter-for-apache-kafka-with-azure-event-hubs"></a><span data-ttu-id="f5216-103">Cómo usar el iniciador de Spring Boot para Apache Kafka con Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="f5216-103">How to use the Spring Boot Starter for Apache Kafka with Azure Event Hubs</span></span>

## <a name="overview"></a><span data-ttu-id="f5216-104">Información general</span><span class="sxs-lookup"><span data-stu-id="f5216-104">Overview</span></span>

<span data-ttu-id="f5216-105">En este artículo se muestra cómo configurar una aplicación de Spring Cloud Stream Binder basada en Java creada con Spring Boot Initializer para usar [Apache Kafka] con Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="f5216-105">This article demonstrates how to configure a Java-based Spring Cloud Stream Binder created with the Spring Boot Initializer to use [Apache Kafka] with Azure Event Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f5216-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="f5216-106">Prerequisites</span></span>

<span data-ttu-id="f5216-107">Los siguientes requisitos previos son necesarios para seguir los pasos descritos en este artículo:</span><span class="sxs-lookup"><span data-stu-id="f5216-107">The following prerequisites are required in order to follow the steps in this article:</span></span>

* <span data-ttu-id="f5216-108">Una suscripción de Azure. Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN] o registrarse para obtener una [cuenta de Azure gratuita].</span><span class="sxs-lookup"><span data-stu-id="f5216-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="f5216-109">Un [kit de desarrollo de Java (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), versión 1.7 o posterior.</span><span class="sxs-lookup"><span data-stu-id="f5216-109">A [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 or later.</span></span>
* <span data-ttu-id="f5216-110">[Apache Maven](http://maven.apache.org/), versión 3.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="f5216-110">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

> [!IMPORTANT]
>
> <span data-ttu-id="f5216-111">Se necesita Spring Boot versión 2.0 o posteriores para completar los pasos descritos en este artículo.</span><span class="sxs-lookup"><span data-stu-id="f5216-111">Spring Boot version 2.0 or greater is required to complete the steps in this article.</span></span>
>

## <a name="create-an-azure-event-hub-using-the-azure-portal"></a><span data-ttu-id="f5216-112">Creación de un centro de eventos de Azure mediante Azure Portal</span><span class="sxs-lookup"><span data-stu-id="f5216-112">Create an Azure Event Hub using the Azure portal</span></span>

### <a name="create-an-azure-event-hub-namespace"></a><span data-ttu-id="f5216-113">Creación de un espacio de nombres del centro de eventos de Azure</span><span class="sxs-lookup"><span data-stu-id="f5216-113">Create an Azure Event Hub Namespace</span></span>

1. <span data-ttu-id="f5216-114">Vaya a Azure Portal en <https://portal.azure.com/> e inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="f5216-114">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="f5216-115">Haga clic en **+Crear un recurso**, en **Internet de las cosas** y en **Event Hubs**.</span><span class="sxs-lookup"><span data-stu-id="f5216-115">Click **+Create a resource**, then **Internet of Things**, and then click **Event Hubs**.</span></span>

   ![Creación de un espacio de nombres del centro de eventos de Azure][IMG01]

1. <span data-ttu-id="f5216-117">En la página **Crear espacio de nombres**, escriba la información siguiente:</span><span class="sxs-lookup"><span data-stu-id="f5216-117">On the **Create Namespace** page, enter the following information:</span></span>

   * <span data-ttu-id="f5216-118">Escriba un **Nombre** único, que pasará a formar parte del identificador URI del espacio de nombres del centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="f5216-118">Enter a unique **Name**, which will become part of the URI for your event hub namespace.</span></span> <span data-ttu-id="f5216-119">Por ejemplo: si escribió **wingtiptoys** para el **Nombre**, el identificador URI sería *wingtiptoys.servicebus.windows.net*.</span><span class="sxs-lookup"><span data-stu-id="f5216-119">For example: if you entered **wingtiptoys** for the **Name**, the URI would be *wingtiptoys.servicebus.windows.net*.</span></span>
   * <span data-ttu-id="f5216-120">Elija un **Plan de tarifa** para el espacio de nombres del centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="f5216-120">Choose a **Pricing tier** for your event hub namespace.</span></span>
   * <span data-ttu-id="f5216-121">Especifique **Habilitar Kafka** para el espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="f5216-121">Specify **Enable Kafka** for your namespace.</span></span>
   * <span data-ttu-id="f5216-122">Elija la **Suscripción** que quiere usar para el espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="f5216-122">Choose the **Subscription** you want to use for your namespace.</span></span>
   * <span data-ttu-id="f5216-123">Especifique si quiere crear un nuevo **Grupo de recursos** para el espacio de nombres o elija un grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="f5216-123">Specify whether to create a new **Resource group** for your namespace, or choose an existing resource group.</span></span>
   * <span data-ttu-id="f5216-124">Especifique la **Ubicación** del espacio de nombres del centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="f5216-124">Specify the **Location** for your event hub namespace.</span></span>
   
   ![Especificación de las opciones del espacio de nombres del centro de eventos de Azure][IMG02]

1. <span data-ttu-id="f5216-126">Cuando haya especificado las opciones enumeradas anteriormente, haga clic en **Crear** para crear el espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="f5216-126">When you have specified the options listed above, click **Create** to create your namespace.</span></span>

### <a name="create-an-azure-event-hub-in-your-namespace"></a><span data-ttu-id="f5216-127">Creación de un centro de eventos de Azure en el espacio de nombres</span><span class="sxs-lookup"><span data-stu-id="f5216-127">Create an Azure Event Hub in your namespace</span></span>

1. <span data-ttu-id="f5216-128">Vaya a Azure Portal en <https://portal.azure.com/>.</span><span class="sxs-lookup"><span data-stu-id="f5216-128">Browse to the Azure portal at <https://portal.azure.com/>.</span></span>

1. <span data-ttu-id="f5216-129">Haga clic en **Todos los recursos** y, a continuación, en el espacio de nombres que ha creado.</span><span class="sxs-lookup"><span data-stu-id="f5216-129">Click **All resources**, and then click the namespace that you created.</span></span>

   ![Selección del espacio de nombres del centro de eventos de Azure][IMG03]

1. <span data-ttu-id="f5216-131">Haga clic en **Event Hubs** y, a continuación, haga clic en **+Centro de eventos**.</span><span class="sxs-lookup"><span data-stu-id="f5216-131">Click **Event Hubs**, and then click **+Event Hub**.</span></span>

   ![Adición de un nuevo centro de eventos de Azure][IMG04]

1. <span data-ttu-id="f5216-133">En la página **Crear centro de eventos**, escriba un **Nombre** único para el centro de eventos y haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="f5216-133">On the **Create Event Hub** page, enter a unique **Name** for your Event Hub, and then click **Create**.</span></span>

   ![Creación de un Centro de eventos de Azure][IMG05]

1. <span data-ttu-id="f5216-135">Cuando se haya creado el centro de eventos, se mostrará en la página **Event Hubs**.</span><span class="sxs-lookup"><span data-stu-id="f5216-135">When your Event Hub has been created, it will be listed on the **Event Hubs** page.</span></span>

   ![Creación de un Centro de eventos de Azure][IMG06]

## <a name="create-a-simple-spring-boot-application-with-the-spring-initializr"></a><span data-ttu-id="f5216-137">Creación de una aplicación sencilla de Spring Boot con Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="f5216-137">Create a simple Spring Boot application with the Spring Initializr</span></span>

1. <span data-ttu-id="f5216-138">Vaya a <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="f5216-138">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="f5216-139">Especifique las opciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="f5216-139">Specify the following options:</span></span>

   * <span data-ttu-id="f5216-140">Genere un proyecto de **Maven** con **Java**.</span><span class="sxs-lookup"><span data-stu-id="f5216-140">Generate a **Maven** project with **Java**.</span></span>
   * <span data-ttu-id="f5216-141">Especifique una versión de **Spring Boot** igual o superior a la 2.0.</span><span class="sxs-lookup"><span data-stu-id="f5216-141">Specify a **Spring Boot** version that is equal to or greater than 2.0.</span></span>
   * <span data-ttu-id="f5216-142">Especifique los nombres de **Group** (Grupo) y **Artifact** (Artefacto) de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f5216-142">Specify the **Group** and **Artifact** names for your application.</span></span>
   * <span data-ttu-id="f5216-143">Agregue la dependencia **Web**.</span><span class="sxs-lookup"><span data-stu-id="f5216-143">Add the **Web** dependency.</span></span>

      ![Opciones básicas de Spring Initializr][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="f5216-145">Spring Initializr usa los nombres de **Group** (Grupo) y **Artifact** (Artefacto) para crear el nombre del paquete, por ejemplo: *com.wingtiptoys.kafka*.</span><span class="sxs-lookup"><span data-stu-id="f5216-145">The Spring Initializr uses the **Group** and **Artifact** names to create the package name; for example: *com.wingtiptoys.kafka*.</span></span>
   >

1. <span data-ttu-id="f5216-146">Cuando haya especificado las opciones enumeradas anteriormente, haga clic en **Generate Project** (Generar proyecto).</span><span class="sxs-lookup"><span data-stu-id="f5216-146">When you have specified the options listed above, click **Generate Project**.</span></span>

1. <span data-ttu-id="f5216-147">Cuando se le solicite, descargue el proyecto en una ruta de acceso del equipo local.</span><span class="sxs-lookup"><span data-stu-id="f5216-147">When prompted, download the project to a path on your local computer.</span></span>

   ![Descarga del proyecto de Spring][SI02]

1. <span data-ttu-id="f5216-149">Después de extraer los archivos en el sistema local, la aplicación sencilla de Spring Boot estará lista para editarla.</span><span class="sxs-lookup"><span data-stu-id="f5216-149">After you have extracted the files on your local system, your simple Spring Boot application will be ready for editing.</span></span>

## <a name="configure-your-spring-boot-app-to-use-the-spring-cloud-kafka-stream-and-azure-event-hub-starters"></a><span data-ttu-id="f5216-150">Configuración de la aplicación de Spring Boot para usar los iniciadores Spring Cloud Kafka Stream y Azure Event Hub</span><span class="sxs-lookup"><span data-stu-id="f5216-150">Configure your Spring Boot app to use the Spring Cloud Kafka Stream and Azure Event Hub starters</span></span>

1. <span data-ttu-id="f5216-151">Busque el archivo *pom.xml* en el directorio raíz de la aplicación, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="f5216-151">Locate the *pom.xml* file in the root directory of your app; for example:</span></span>

   `C:\SpringBoot\kafka\pom.xml`

   <span data-ttu-id="f5216-152">O bien</span><span class="sxs-lookup"><span data-stu-id="f5216-152">-or-</span></span>

   `/users/example/home/kafka/pom.xml`

1. <span data-ttu-id="f5216-153">Abra el archivo *pom.xml* en un editor de texto y agregue los iniciadores Spring Cloud Kafka Stream y Azure Event Hub a la lista `<dependencies>`:</span><span class="sxs-lookup"><span data-stu-id="f5216-153">Open the *pom.xml* file in a text editor, and add the Spring Cloud Kafka Stream and Azure Event Hub starters to the list of `<dependencies>`:</span></span>

   ```xml
   <dependency>
      <groupId>org.springframework.cloud</groupId>
      <artifactId>spring-cloud-starter-stream-kafka</artifactId>
      <version>2.0.1.RELEASE</version>
   </dependency>
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>spring-cloud-azure-starter-eventhub</artifactId>
      <version>1.0.0.M2</version>
   </dependency>
   ```

   ![Edición del archivo pom.xml][SI03]

1. <span data-ttu-id="f5216-155">Guarde y cierre el archivo *pom.xml*.</span><span class="sxs-lookup"><span data-stu-id="f5216-155">Save and close the *pom.xml* file.</span></span>

## <a name="create-an-azure-credential-file"></a><span data-ttu-id="f5216-156">Creación de un archivo de credenciales de Azure</span><span class="sxs-lookup"><span data-stu-id="f5216-156">Create an Azure Credential File</span></span>

1. <span data-ttu-id="f5216-157">Abra el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="f5216-157">Open a command prompt.</span></span>

1. <span data-ttu-id="f5216-158">Vaya al directorio *resources* de la aplicación de Spring Boot, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="f5216-158">Navigate to the *resources* directory of your Spring Boot app; for example:</span></span>

   ```shell
   cd C:\SpringBoot\eventhub\src\main\resources
   ```

   <span data-ttu-id="f5216-159">O bien</span><span class="sxs-lookup"><span data-stu-id="f5216-159">-or-</span></span>

   ```shell
   cd /users/example/home/eventhub/src/main/resources
   ```

1. <span data-ttu-id="f5216-160">Inicio de sesión en la cuenta de Azure</span><span class="sxs-lookup"><span data-stu-id="f5216-160">Sign in to your Azure account:</span></span>

   ```azurecli
   az login
   ```

1. <span data-ttu-id="f5216-161">Muestre las suscripciones:</span><span class="sxs-lookup"><span data-stu-id="f5216-161">List your subscriptions:</span></span>

   ```azurecli
   az account list
   ```
   <span data-ttu-id="f5216-162">Azure devolverá la lista de sus suscripciones, y tendrá que copiar el GUID de la suscripción que desea usar; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="f5216-162">Azure will return a list of your subscriptions, and you will need to copy the GUID for the subscription that you want to use; for example:</span></span>

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

1. Specify the GUID for the subscription you want to use with Azure; for example:

   ```azurecli
   az account set -s 11111111-1111-1111-1111-111111111111
   ```

1. <span data-ttu-id="f5216-163">Cree el archivo de credenciales de Azure:</span><span class="sxs-lookup"><span data-stu-id="f5216-163">Create your Azure Credential file:</span></span>

   ```azurecli
   az ad sp create-for-rbac --sdk-auth > my.azureauth
   ```

   <span data-ttu-id="f5216-164">Este comando crea un archivo *my.azureauth* en el directorio *resources* con un contenido similar al del siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="f5216-164">This command will create a *my.azureauth* file in your *resources* directory with contents that resemble the following example:</span></span>

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

## <a name="configure-your-spring-boot-app-to-use-your-azure-event-hub"></a><span data-ttu-id="f5216-165">Configuración de la aplicación de Spring Boot para usar el centro de eventos de Azure</span><span class="sxs-lookup"><span data-stu-id="f5216-165">Configure your Spring Boot app to use your Azure Event Hub</span></span>

1. <span data-ttu-id="f5216-166">Busque el archivo *application.properties* en el directorio *resources* de la aplicación, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="f5216-166">Locate the *application.properties* in the *resources* directory of your app; for example:</span></span>

   `C:\SpringBoot\eventhub\src\main\resources\application.properties`

   <span data-ttu-id="f5216-167">O bien</span><span class="sxs-lookup"><span data-stu-id="f5216-167">-or-</span></span>

   `/users/example/home/eventhub/src/main/resources/application.properties`

1.  <span data-ttu-id="f5216-168">Abra el archivo *application.properties* en un editor de texto, agregue las siguientes líneas y, a continuación, sustituya los valores de ejemplo por las propiedades adecuadas del centro de eventos:</span><span class="sxs-lookup"><span data-stu-id="f5216-168">Open the *application.properties* file in a text editor, add the following lines, and then replace the sample values with the appropriate properties for your event hub:</span></span>

   ```yaml
   spring.cloud.azure.credential-file-path=my.azureauth
   spring.cloud.azure.resource-group=wingtiptoysresources
   spring.cloud.azure.region=West US
   spring.cloud.azure.eventhub.namespace=wingtiptoysnamespace

   spring.cloud.stream.bindings.input.destination=wingtiptoyshub
   spring.cloud.stream.bindings.input.group=$Default
   spring.cloud.stream.bindings.output.destination=wingtiptoyshub
   ```
   <span data-ttu-id="f5216-169">Donde:</span><span class="sxs-lookup"><span data-stu-id="f5216-169">Where:</span></span>
   | <span data-ttu-id="f5216-170">Campo</span><span class="sxs-lookup"><span data-stu-id="f5216-170">Field</span></span> | <span data-ttu-id="f5216-171">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="f5216-171">Description</span></span> |
   | ---|---|
   | `spring.cloud.azure.credential-file-path` | <span data-ttu-id="f5216-172">Especifica el archivo de credenciales de Azure que creó anteriormente en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="f5216-172">Specifies Azure credential file that you created earlier in this tutorial.</span></span> |
   | `spring.cloud.azure.resource-group` | <span data-ttu-id="f5216-173">Especifica el grupo de recursos de Azure que contiene el centro de eventos de Azure.</span><span class="sxs-lookup"><span data-stu-id="f5216-173">Specifies the Azure Resource Group that contains your Azure Event Hub.</span></span> |
   | `spring.cloud.azure.region` | <span data-ttu-id="f5216-174">Especifica la región geográfica que seleccionó cuando creó el centro de eventos de Azure.</span><span class="sxs-lookup"><span data-stu-id="f5216-174">Specifies the geographical region that you specified when you created your Azure Event Hub.</span></span> |
   | `spring.cloud.azure.eventhub.namespace` | <span data-ttu-id="f5216-175">Especifica el nombre único que proporcionó cuando creó el espacio de nombres del centro de eventos de Azure.</span><span class="sxs-lookup"><span data-stu-id="f5216-175">Specifies the unique name that you specified when you created your Azure Event Hub Namespace.</span></span> |
   | `spring.cloud.stream.bindings.input.destination` | <span data-ttu-id="f5216-176">Especifica el centro de eventos de Azure del destino de entrada, que para este tutorial es el centro que creó anteriormente en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="f5216-176">Specifies the input destination Azure Event Hub, which for this tutorial is the  hub you created earlier in this tutorial.</span></span> |
   | `spring.cloud.stream.bindings.input.group `| <span data-ttu-id="f5216-177">Especifica un grupo de consumidores del centro de eventos de Azure, que se puede establecer en "$Default" para poder usar el grupo de consumidores básico que se creó cuando creó el centro de eventos de Azure.</span><span class="sxs-lookup"><span data-stu-id="f5216-177">Specifies a Consumer Group from Azure Event Hub, which can be set to '$Default' in order to use the basic consumer group that was created when you created your Azure Event Hub.</span></span> |
   | `spring.cloud.stream.bindings.output.destination` | <span data-ttu-id="f5216-178">Especifica el centro de eventos de Azure del destino de salida, que en este tutorial será el mismo que el destino de entrada.</span><span class="sxs-lookup"><span data-stu-id="f5216-178">Specifies the output destination Azure Event Hub, which for this tutorial will be the same as the input destination.</span></span> |

1. <span data-ttu-id="f5216-179">Guarde y cierre el archivo *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="f5216-179">Save and close the *application.properties* file.</span></span>

## <a name="add-sample-code-to-implement-basic-event-hub-functionality"></a><span data-ttu-id="f5216-180">Adición de código de ejemplo para implementar la funcionalidad básica del centro de eventos</span><span class="sxs-lookup"><span data-stu-id="f5216-180">Add sample code to implement basic event hub functionality</span></span>

<span data-ttu-id="f5216-181">En esta sección se crean las clases de Java necesarias para enviar eventos al centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="f5216-181">In this section, you create the necessary Java classes for sending events to your event hub.</span></span>

### <a name="modify-the-main-application-class"></a><span data-ttu-id="f5216-182">Modificación de la clase de aplicación principal</span><span class="sxs-lookup"><span data-stu-id="f5216-182">Modify the main application class</span></span>

1. <span data-ttu-id="f5216-183">Busque el archivo de Java de la aplicación principal en el directorio del paquete de la aplicación; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="f5216-183">Locate the main application Java file in the package directory of your app; for example:</span></span>

   `C:\SpringBoot\kafka\src\main\java\com\wingtiptoys\kafka\KafkaApplication.java`

   <span data-ttu-id="f5216-184">O bien</span><span class="sxs-lookup"><span data-stu-id="f5216-184">-or-</span></span>

   `/users/example/home/kafka/src/main/java/com/wingtiptoys/kafka/KafkaApplication.java`

1. <span data-ttu-id="f5216-185">Abra el archivo de Java de la aplicación principal en un editor de texto y agregue las siguientes líneas al archivo:</span><span class="sxs-lookup"><span data-stu-id="f5216-185">Open the main application Java file in a text editor, and add the following lines to the file:</span></span>

   ```java
   package com.wingtiptoys.kafka;
   
   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;
   
   @SpringBootApplication
   public class KafkaApplication {
      public static void main(String[] args) {
         SpringApplication.run(KafkaApplication.class, args);
      }
   }
   ```

1. <span data-ttu-id="f5216-186">Guarde y cierre el archivo de Java de la aplicación principal.</span><span class="sxs-lookup"><span data-stu-id="f5216-186">Save and close the main application Java file.</span></span>


### <a name="create-a-new-class-for-the-source-connector"></a><span data-ttu-id="f5216-187">Creación de una nueva clase para el conector de origen</span><span class="sxs-lookup"><span data-stu-id="f5216-187">Create a new class for the source connector</span></span>

1. <span data-ttu-id="f5216-188">Cree un archivo de Java nuevo llamado *KafkaSource.java* en el directorio del paquete de la aplicación y, a continuación, abra el archivo en un editor de texto y agregue las siguientes líneas:</span><span class="sxs-lookup"><span data-stu-id="f5216-188">Create a new Java file named *KafkaSource.java* in the package directory of your app, then open the file in a text editor and add the following lines:</span></span>

   ```java
   package com.wingtiptoys.kafka;
   
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.cloud.stream.annotation.EnableBinding;
   import org.springframework.cloud.stream.messaging.Source;
   import org.springframework.messaging.support.GenericMessage;
   import org.springframework.web.bind.annotation.PostMapping;
   import org.springframework.web.bind.annotation.RequestBody;
   import org.springframework.web.bind.annotation.RequestParam;
   import org.springframework.web.bind.annotation.RestController;
   
   @EnableBinding(Source.class)
   @RestController
   public class KafkaSource {
      @Autowired
      private Source source;

      @PostMapping("/messages")
      public String sendMessage(@RequestBody String message) {
         this.source.output().send(new GenericMessage<>(message));
         return message;
      }
   }
   ```

1. <span data-ttu-id="f5216-189">Guarde y cierre el archivo *KafkaSource.java*.</span><span class="sxs-lookup"><span data-stu-id="f5216-189">Save and close the *KafkaSource.java* file.</span></span>

### <a name="create-a-new-class-for-the-sink-connector"></a><span data-ttu-id="f5216-190">Creación de una nueva clase para el conector receptor</span><span class="sxs-lookup"><span data-stu-id="f5216-190">Create a new class for the sink connector</span></span>

1. <span data-ttu-id="f5216-191">Cree un archivo de Java nuevo llamado *KafkaSink.java* en el directorio del paquete de la aplicación y, a continuación, abra el archivo en un editor de texto y agregue las siguientes líneas:</span><span class="sxs-lookup"><span data-stu-id="f5216-191">Create a new Java file named *KafkaSink.java* in the package directory of your app, then open the file in a text editor and add the following lines:</span></span>

   ```java
   package com.wingtiptoys.kafka;
   
   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   import org.springframework.cloud.stream.annotation.EnableBinding;
   import org.springframework.cloud.stream.annotation.StreamListener;
   import org.springframework.cloud.stream.messaging.Sink;
   
   @EnableBinding(Sink.class)
   public class KafkaSink {
      private static final Logger LOGGER = LoggerFactory.getLogger(KafkaSink.class);

      @StreamListener(Sink.INPUT)
      public void handleMessage(String message) {
         LOGGER.info("New message received: " + message);
      }
   }
   ```

1. <span data-ttu-id="f5216-192">Guarde y cierre el archivo *KafkaSink.java*.</span><span class="sxs-lookup"><span data-stu-id="f5216-192">Save and close the *KafkaSink.java* file.</span></span>

## <a name="build-and-test-your-application"></a><span data-ttu-id="f5216-193">Compilación y prueba de la aplicación</span><span class="sxs-lookup"><span data-stu-id="f5216-193">Build and test your application</span></span>

1. <span data-ttu-id="f5216-194">Abra un símbolo del sistema y cambie el directorio a la carpeta donde se encuentra el archivo *pom.xml*; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="f5216-194">Open a command prompt and change directory to the folder where your *pom.xml* file is located; for example:</span></span>

   `cd C:\SpringBoot\kafka`

   <span data-ttu-id="f5216-195">O bien</span><span class="sxs-lookup"><span data-stu-id="f5216-195">-or-</span></span>

   `cd /users/example/home/kafka`

1. <span data-ttu-id="f5216-196">Compile la aplicación de Spring Boot con Maven y ejecútela; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="f5216-196">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. <span data-ttu-id="f5216-197">Una vez que se está ejecutando la aplicación, puede usar *curl* para probar la aplicación, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="f5216-197">Once your application is running, you can use *curl* to test your application; for example:</span></span>

   ```shell
   curl -X POST -H "Content-Type: text/plain" -d "hello" http://localhost:8080/messages
   ```
   <span data-ttu-id="f5216-198">Debería ver el mensaje "hello" en los registros de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f5216-198">You should see "hello" posted to your application's logs.</span></span> <span data-ttu-id="f5216-199">Por ejemplo: </span><span class="sxs-lookup"><span data-stu-id="f5216-199">For example:</span></span>

   ```shell
   [http-nio-8080-exec-2] INFO org.apache.kafka.common.utils.AppInfoParser - Kafka version : 1.0.2
   [http-nio-8080-exec-2] INFO org.apache.kafka.common.utils.AppInfoParser - Kafka commitId : 2a121f7b1d402825
   [wingtiptoyshub.container-0-C-1] INFO com.wingtiptoys.kafka.KafkaSink - New message received: hello
   ```


> [!NOTE]
> 
> <span data-ttu-id="f5216-200">Con fines de prueba, puede modificar el archivo *KafkaSource.java* para que contenga un formulario HTML simple similar al ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="f5216-200">For testing purposes, you could modify your *KafkaSource.java* so that it contains a simple HTML form like the following example:</span></span>
> 
> ```java
> package com.wingtiptoys.kafka;
>    
> import org.springframework.beans.factory.annotation.Autowired;
> import org.springframework.cloud.stream.annotation.EnableBinding;
> import org.springframework.cloud.stream.messaging.Source;
> import org.springframework.messaging.support.GenericMessage;
> import org.springframework.web.bind.annotation.GetMapping;
> import org.springframework.web.bind.annotation.PostMapping;
> import org.springframework.web.bind.annotation.RequestBody;
> import org.springframework.web.bind.annotation.RequestParam;
> import org.springframework.web.bind.annotation.RestController;
> 
> @EnableBinding(Source.class)
> @RestController
> public class KafkaSource {
>   @Autowired
>   private Source source;
> 
>   @GetMapping("/")
>   public String sendForm() {
>     return "<html><body>" +
>       "<form action=\"/messages\" method=\"post\">" +
>       "<input type=\"text\" name=\"text\">" +
>       "<input type=\"submit\">" +
>       "</form></body><html>";
>     }
> 
>   @PostMapping("/messages")
>   public String sendMessage(@RequestBody String message) {
>     this.source.output().send(new GenericMessage<>(message));
>     return message;
>   }
> }
> ```
> 
> <span data-ttu-id="f5216-201">Esto le permitirá utilizar un explorador web para probar la aplicación:</span><span class="sxs-lookup"><span data-stu-id="f5216-201">This will allow you to use a web browser to test your application:</span></span>
> 
> ![Prueba de la aplicación mediante un explorador web][TB01]
> 
> <span data-ttu-id="f5216-203">Cuando se envía el formulario, la aplicación mostrará los resultados:</span><span class="sxs-lookup"><span data-stu-id="f5216-203">When you submit the form, your application will display the results:</span></span>
> 
> ![Respuesta de la aplicación en un explorador web][TB02]
> 

## <a name="next-steps"></a><span data-ttu-id="f5216-205">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f5216-205">Next steps</span></span>

<span data-ttu-id="f5216-206">Consulte los siguientes artículos para más información sobre la compatibilidad de Azure para Event Hub Stream Binder y Apache Kafka:</span><span class="sxs-lookup"><span data-stu-id="f5216-206">For more information about Azure support for Event Hub Stream Binder and Apache Kafka, see the following articles:</span></span>

* [<span data-ttu-id="f5216-207">¿Qué es Azure Event Hubs?</span><span class="sxs-lookup"><span data-stu-id="f5216-207">What is Azure Event Hubs?</span></span>](/azure/event-hubs/event-hubs-about)

* [<span data-ttu-id="f5216-208">Azure Event Hubs para Apache Kafka</span><span class="sxs-lookup"><span data-stu-id="f5216-208">Azure Event Hubs for Apache Kafka</span></span>](/azure/event-hubs/event-hubs-for-kafka-ecosystem-overview)

* [<span data-ttu-id="f5216-209">Creación de un espacio de nombres de Event Hubs y un centro de eventos con Azure Portal</span><span class="sxs-lookup"><span data-stu-id="f5216-209">Create an Event Hubs namespace and an event hub using the Azure portal</span></span>](/azure/event-hubs/event-hubs-create)

* [<span data-ttu-id="f5216-210">Creación de centros de eventos habilitados para Apache Kafka</span><span class="sxs-lookup"><span data-stu-id="f5216-210">Create Apache Kafka enabled event hubs</span></span>](/azure/event-hubs/event-hubs-create-kafka-enabled)

<span data-ttu-id="f5216-211">Para más información sobre el uso de Azure con Java, consulte [Azure para desarrolladores de Java] y [Herramientas de Java para Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="f5216-211">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="f5216-212">**[Spring Framework]** es una solución de código abierto que ayuda a los desarrolladores de Java a crear aplicaciones de nivel empresarial.</span><span class="sxs-lookup"><span data-stu-id="f5216-212">The **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="f5216-213">Uno de los proyectos más populares que se basa en esa plataforma es [Spring Boot], que proporciona un enfoque simplificado para crear aplicaciones de Java independientes.</span><span class="sxs-lookup"><span data-stu-id="f5216-213">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="f5216-214">Para ayudar a los desarrolladores a empezar con Spring Boot, puede encontrar varios paquetes de ejemplo de Spring Boot en <https://github.com/spring-guides/>.</span><span class="sxs-lookup"><span data-stu-id="f5216-214">To help developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>.</span></span> <span data-ttu-id="f5216-215">Además de elegir de la lista de proyectos básicos de Spring Boot, el **[Spring Initializr]** ayuda a los desarrolladores en los primeros pasos para crear aplicaciones de Spring Boot personalizadas.</span><span class="sxs-lookup"><span data-stu-id="f5216-215">In addition to choosing from the list of basic Spring Boot projects, the **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>

<!-- URL List -->

[Apache Kafka]: http://kafka.apache.org
[cuenta de Azure gratuita]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Herramientas de Java para Visual Studio Team Services]: https://java.visualstudio.com/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[ventajas como suscriptor de MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[IMG01]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-kafka-event-hub-01.png
[IMG02]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-kafka-event-hub-02.png
[IMG03]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-kafka-event-hub-03.png
[IMG04]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-kafka-event-hub-04.png
[IMG05]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-kafka-event-hub-05.png
[IMG06]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-kafka-event-hub-06.png
[IMG07]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-kafka-event-hub-07.png
[IMG08]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-kafka-event-hub-08.png

[SI01]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-project-01.png
[SI02]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-project-02.png
[SI03]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-project-03.png

[TB01]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/test-browser-01.png
[TB02]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/test-browser-02.png
