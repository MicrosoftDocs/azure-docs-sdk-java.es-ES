---
title: Cómo usar el iniciador de Spring Boot para Azure Storage
description: Aprenda a configurar una aplicación de Spring Boot Initializer con el iniciador de Azure Storage.
services: storage
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 09/10/2018
ms.devlang: java
ms.service: storage
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage
ms.openlocfilehash: 4838b6dbd354ad941df12933dddfa7f3e7eef905
ms.sourcegitcommit: 4d52e47073fb0b3ac40a2689daea186bad5b1ef5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/23/2018
ms.locfileid: "49799971"
---
# <a name="how-to-use-the-spring-boot-starter-for-azure-storage"></a><span data-ttu-id="18b38-103">Cómo usar el iniciador de Spring Boot para Azure Storage</span><span class="sxs-lookup"><span data-stu-id="18b38-103">How to use the Spring Boot Starter for Azure Storage</span></span>

## <a name="overview"></a><span data-ttu-id="18b38-104">Información general</span><span class="sxs-lookup"><span data-stu-id="18b38-104">Overview</span></span>

<span data-ttu-id="18b38-105">Este artículo explica cómo crear una aplicación personalizada con **Spring Initializr** y, a continuación, agregar el iniciador de almacenamiento de Azure a la aplicación y usar la aplicación para cargar un blob en la cuenta de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="18b38-105">This article walks you through creating a custom application using the **Spring Initializr**, then adding the Azure storage starter to your application, and then using your application to upload a blob to your Azure storage account.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="18b38-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="18b38-106">Prerequisites</span></span>

<span data-ttu-id="18b38-107">Los siguientes requisitos previos son necesarios para seguir los pasos descritos en este artículo:</span><span class="sxs-lookup"><span data-stu-id="18b38-107">The following prerequisites are required in order to follow the steps in this article:</span></span>

* <span data-ttu-id="18b38-108">Una suscripción de Azure. Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) o registrarse para obtener una [cuenta de Azure gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="18b38-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free Azure account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="18b38-109">La [Interfaz de la línea de comandos (CLI) de Azure](http://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="18b38-109">The [Azure Command-Line Interface (CLI)](http://docs.microsoft.com/cli/azure/overview).</span></span>
* <span data-ttu-id="18b38-110">Un [kit de desarrollo de Java (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/) actualizado, versión 1.7 o posteriores.</span><span class="sxs-lookup"><span data-stu-id="18b38-110">An up-to-date [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 or later.</span></span>
* <span data-ttu-id="18b38-111">[Apache Maven](http://maven.apache.org/), versión 3.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="18b38-111">Apache's [Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

> [!IMPORTANT]
>
> <span data-ttu-id="18b38-112">Se necesita Spring Boot versión 2.0 o posteriores para completar los pasos descritos en este artículo.</span><span class="sxs-lookup"><span data-stu-id="18b38-112">Spring Boot version 2.0 or greater is required to complete the steps in this article.</span></span>
>

## <a name="create-an-azure-storage-account-and-blob-container-for-your-application"></a><span data-ttu-id="18b38-113">Creación de una cuenta de Azure Storage y un contenedor de blobs para la aplicación</span><span class="sxs-lookup"><span data-stu-id="18b38-113">Create an Azure Storage Account and blob container for your application</span></span>

1. <span data-ttu-id="18b38-114">Vaya a Azure Portal en <https://portal.azure.com/> e inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="18b38-114">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="18b38-115">Haga clic en **+Crear un recurso**, en **Almacenamiento** y en **Cuenta de almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="18b38-115">Click **+Create a resource**, then **Storage**, and then click **Storage Account**.</span></span>

   ![Creación de una cuenta de Azure Storage][IMG01]

1. <span data-ttu-id="18b38-117">En la página **Crear espacio de nombres**, escriba la información siguiente:</span><span class="sxs-lookup"><span data-stu-id="18b38-117">On the **Create Namespace** page, enter the following information:</span></span>

   * <span data-ttu-id="18b38-118">Escriba un **Nombre** único, que pasará a formar parte del identificador URI de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="18b38-118">Enter a unique **Name**, which will become part of the URI for your storage account.</span></span> <span data-ttu-id="18b38-119">Por ejemplo: si escribió **wingtiptoysstorage** para el **Nombre**, el identificador URI sería *wingtiptoysstorage.core.windows.net*.</span><span class="sxs-lookup"><span data-stu-id="18b38-119">For example: if you entered **wingtiptoysstorage** for the **Name**, the URI would be *wingtiptoysstorage.core.windows.net*.</span></span>
   * <span data-ttu-id="18b38-120">Elija **Blob Storage** para **Tipo de cuenta**.</span><span class="sxs-lookup"><span data-stu-id="18b38-120">Choose **Blob storage** for the **Account kind**.</span></span>
   * <span data-ttu-id="18b38-121">Especifique la **Ubicación** de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="18b38-121">Specify the **Location** for your storage account.</span></span>
   * <span data-ttu-id="18b38-122">Elija la **Suscripción** que quiere usar para la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="18b38-122">Choose the **Subscription** you want to use for your storage account.</span></span>
   * <span data-ttu-id="18b38-123">Especifique si quiere crear un nuevo **Grupo de recursos** para la cuenta de almacenamiento o elija un grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="18b38-123">Specify whether to create a new **Resource group** for your storage account, or choose an existing resource group.</span></span>

   ![Especificación de las opciones de la cuenta de Azure Storage][IMG02]

1. <span data-ttu-id="18b38-125">Cuando haya especificado las opciones enumeradas anteriormente, haga clic en **Crear** para crear la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="18b38-125">When you have specified the options listed above, click **Create** to create your storage account.</span></span>

1. <span data-ttu-id="18b38-126">Cuando Azure Portal ha creado la cuenta de almacenamiento, haga clic en **Blobs** y, a continuación, haga clic en **+Contenedor**.</span><span class="sxs-lookup"><span data-stu-id="18b38-126">When the Azure portal has created your storage account, click **Blobs**, then click **+Container**.</span></span>

   ![Creación de un contenedor de blobs][IMG03]

1. <span data-ttu-id="18b38-128">Escriba un **Nombre** para el contenedor de blobs y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="18b38-128">Enter a **Name** for your blob container, and then click **OK**.</span></span>

   ![Especificación de las opciones del contenedor de blobs][IMG04]

1. <span data-ttu-id="18b38-130">Azure Portal enumerará el contenedor de blobs una vez se haya creado.</span><span class="sxs-lookup"><span data-stu-id="18b38-130">The Azure portal will list your blob container after is has been created.</span></span>

   ![Revisión de la lista de contenedores de blobs][IMG05]

## <a name="create-a-simple-spring-boot-application-with-the-spring-initializr"></a><span data-ttu-id="18b38-132">Creación de una aplicación sencilla de Spring Boot con Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="18b38-132">Create a simple Spring Boot application with the Spring Initializr</span></span>

1. <span data-ttu-id="18b38-133">Vaya a <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="18b38-133">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="18b38-134">Especifique las opciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="18b38-134">Specify the following options:</span></span>

   * <span data-ttu-id="18b38-135">Genere un proyecto de **Maven** con **Java**.</span><span class="sxs-lookup"><span data-stu-id="18b38-135">Generate a **Maven** project with **Java**.</span></span>
   * <span data-ttu-id="18b38-136">Especifique una versión de **Spring Boot** igual o superior a la 2.0.</span><span class="sxs-lookup"><span data-stu-id="18b38-136">Specify a **Spring Boot** version that is equal to or greater than 2.0.</span></span>
   * <span data-ttu-id="18b38-137">Especifique los nombres de **Group** (Grupo) y **Artifact** (Artefacto) de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="18b38-137">Specify the **Group** and **Artifact** names for your application.</span></span>
   * <span data-ttu-id="18b38-138">Agregue la dependencia **Web**.</span><span class="sxs-lookup"><span data-stu-id="18b38-138">Add the **Web** dependency.</span></span>

      ![Opciones básicas de Spring Initializr][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="18b38-140">Spring Initializr usa los nombres de **Group** (Grupo) y **Artifact** (Artefacto) para crear el nombre del paquete, por ejemplo: *com.wingtiptoys.storage*.</span><span class="sxs-lookup"><span data-stu-id="18b38-140">The Spring Initializr uses the **Group** and **Artifact** names to create the package name; for example: *com.wingtiptoys.storage*.</span></span>
   >

1. <span data-ttu-id="18b38-141">Cuando haya especificado las opciones enumeradas anteriormente, haga clic en **Generate Project** (Generar proyecto).</span><span class="sxs-lookup"><span data-stu-id="18b38-141">When you have specified the options listed above, click **Generate Project**.</span></span>

1. <span data-ttu-id="18b38-142">Cuando se le solicite, descargue el proyecto en una ruta de acceso del equipo local.</span><span class="sxs-lookup"><span data-stu-id="18b38-142">When prompted, download the project to a path on your local computer.</span></span>

   ![Descarga del proyecto de Spring][SI02]

1. <span data-ttu-id="18b38-144">Después de extraer los archivos en el sistema local, la aplicación sencilla de Spring Boot estará lista para editarla.</span><span class="sxs-lookup"><span data-stu-id="18b38-144">After you have extracted the files on your local system, your simple Spring Boot application will be ready for editing.</span></span>

## <a name="configure-your-spring-boot-app-to-use-the-azure-storage-starter"></a><span data-ttu-id="18b38-145">Configuración de la aplicación de Spring Boot para usar el iniciador de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="18b38-145">Configure your Spring Boot app to use the Azure Storage starter</span></span>

1. <span data-ttu-id="18b38-146">Busque el archivo *pom.xml* en el directorio raíz de la aplicación, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="18b38-146">Locate the *pom.xml* file in the root directory of your app; for example:</span></span>

   `C:\SpringBoot\storage\pom.xml`

   <span data-ttu-id="18b38-147">O bien</span><span class="sxs-lookup"><span data-stu-id="18b38-147">-or-</span></span>

   `/users/example/home/storage/pom.xml`

1. <span data-ttu-id="18b38-148">Abra el archivo *pom.xml* en un editor de texto y agregue el iniciador Spring Cloud Azure Storage a la lista `<dependencies>`:</span><span class="sxs-lookup"><span data-stu-id="18b38-148">Open the *pom.xml* file in a text editor, and add the Spring Cloud Azure Storage starter to the list of `<dependencies>`:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>spring-azure-starter-storage</artifactId>
      <version>1.0.0.M2</version>
   </dependency>
   ```

   ![Edición del archivo pom.xml][SI03]

1. <span data-ttu-id="18b38-150">Guarde y cierre el archivo *pom.xml*.</span><span class="sxs-lookup"><span data-stu-id="18b38-150">Save and close the *pom.xml* file.</span></span>

## <a name="create-an-azure-credential-file"></a><span data-ttu-id="18b38-151">Creación de un archivo de credenciales de Azure</span><span class="sxs-lookup"><span data-stu-id="18b38-151">Create an Azure Credential File</span></span>

1. <span data-ttu-id="18b38-152">Abra el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="18b38-152">Open a command prompt.</span></span>

1. <span data-ttu-id="18b38-153">Vaya al directorio *resources* de la aplicación de Spring Boot, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="18b38-153">Navigate to the *resources* directory of your Spring Boot app; for example:</span></span>

   ```shell
   cd C:\SpringBoot\storage\src\main\resources
   ```

   <span data-ttu-id="18b38-154">O bien</span><span class="sxs-lookup"><span data-stu-id="18b38-154">-or-</span></span>

   ```shell
   cd /users/example/home/storage/src/main/resources
   ```

1. <span data-ttu-id="18b38-155">Inicio de sesión en la cuenta de Azure</span><span class="sxs-lookup"><span data-stu-id="18b38-155">Sign in to your Azure account:</span></span>

   ```azurecli
   az login
   ```

1. <span data-ttu-id="18b38-156">Muestre las suscripciones:</span><span class="sxs-lookup"><span data-stu-id="18b38-156">List your subscriptions:</span></span>

   ```azurecli
   az account list
   ```
   <span data-ttu-id="18b38-157">Azure devolverá la lista de sus suscripciones, y tendrá que copiar el GUID de la suscripción que desea usar; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="18b38-157">Azure will return a list of your subscriptions, and you will need to copy the GUID for the subscription that you want to use; for example:</span></span>

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

1. <span data-ttu-id="18b38-158">Cree el archivo de credenciales de Azure:</span><span class="sxs-lookup"><span data-stu-id="18b38-158">Create your Azure Credential file:</span></span>

   ```azurecli
   az ad sp create-for-rbac --sdk-auth > my.azureauth
   ```

   <span data-ttu-id="18b38-159">Este comando crea un archivo *my.azureauth* en el directorio *resources* con un contenido similar al del siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="18b38-159">This command will create a *my.azureauth* file in your *resources* directory with contents that resemble the following example:</span></span>

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

## <a name="configure-your-spring-boot-app-to-use-your-azure-storage-account"></a><span data-ttu-id="18b38-160">Configuración de la aplicación de Spring Boot para usar la cuenta de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="18b38-160">Configure your Spring Boot app to use your Azure Storage account</span></span>

1. <span data-ttu-id="18b38-161">Busque el archivo *application.properties* en el directorio *resources* de la aplicación, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="18b38-161">Locate the *application.properties* in the *resources* directory of your app; for example:</span></span>

   `C:\SpringBoot\storage\src\main\resources\application.properties`

   <span data-ttu-id="18b38-162">O bien</span><span class="sxs-lookup"><span data-stu-id="18b38-162">-or-</span></span>

   `/users/example/home/storage/src/main/resources/application.properties`

2. <span data-ttu-id="18b38-163">Abra el archivo *application.properties* en un editor de texto, agregue las siguientes líneas y, a continuación, sustituya los valores de ejemplo por las propiedades adecuadas de la cuenta de almacenamiento:</span><span class="sxs-lookup"><span data-stu-id="18b38-163">Open the *application.properties* file in a text editor, add the following lines, and then replace the sample values with the appropriate properties for your storage account:</span></span>

   ```yaml
   spring.cloud.azure.credential-file-path=my.azureauth
   spring.cloud.azure.resource-group=wingtiptoysresources
   spring.cloud.azure.region=West US
   spring.cloud.azure.storage.account=wingtiptoysstorage
   ```
   <span data-ttu-id="18b38-164">Donde:</span><span class="sxs-lookup"><span data-stu-id="18b38-164">Where:</span></span>

   |                   <span data-ttu-id="18b38-165">Campo</span><span class="sxs-lookup"><span data-stu-id="18b38-165">Field</span></span>                   |                                            <span data-ttu-id="18b38-166">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="18b38-166">Description</span></span>                                            |
   |-------------------------------------------|---------------------------------------------------------------------------------------------------|
   | `spring.cloud.azure.credential-file-path` |            <span data-ttu-id="18b38-167">Especifica el archivo de credenciales de Azure que creó anteriormente en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="18b38-167">Specifies Azure credential file that you created earlier in this tutorial.</span></span>             |
   |    `spring.cloud.azure.resource-group`    |           <span data-ttu-id="18b38-168">Especifica el grupo de recursos de Azure que contiene la cuenta de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="18b38-168">Specifies the Azure Resource Group that contains your Azure Storage account.</span></span>            |
   |        `spring.cloud.azure.region`        | <span data-ttu-id="18b38-169">Especifica la región geográfica que seleccionó cuando creó la cuenta de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="18b38-169">Specifies the geographical region that you specified when you created your Azure Storage account.</span></span> |
   |   `spring.cloud.azure.storage.account`    |            <span data-ttu-id="18b38-170">Especifica la cuenta de Azure Storage que creó anteriormente en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="18b38-170">Specifies Azure Storage account that you created earlier in this tutorial.</span></span>             |


3. <span data-ttu-id="18b38-171">Guarde y cierre el archivo *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="18b38-171">Save and close the *application.properties* file.</span></span>

## <a name="add-sample-code-to-implement-basic-azure-storage-functionality"></a><span data-ttu-id="18b38-172">Adición de código de ejemplo para implementar la funcionalidad básica de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="18b38-172">Add sample code to implement basic Azure storage functionality</span></span>

<span data-ttu-id="18b38-173">En esta sección, creará las clases de Java necesarias para almacenar un blob en la cuenta de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="18b38-173">In this section, you create the necessary Java classes for storing a blob in your Azure storage account.</span></span>

### <a name="modify-the-main-application-class"></a><span data-ttu-id="18b38-174">Modificación de la clase de aplicación principal</span><span class="sxs-lookup"><span data-stu-id="18b38-174">Modify the main application class</span></span>

1. <span data-ttu-id="18b38-175">Busque el archivo de Java de la aplicación principal en el directorio del paquete de la aplicación; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="18b38-175">Locate the main application Java file in the package directory of your app; for example:</span></span>

   `C:\SpringBoot\storage\src\main\java\com\wingtiptoys\storage\StorageApplication.java`

   <span data-ttu-id="18b38-176">O bien</span><span class="sxs-lookup"><span data-stu-id="18b38-176">-or-</span></span>

   `/users/example/home/storage/src/main/java/com/wingtiptoys/storage/StorageApplication.java`

1. <span data-ttu-id="18b38-177">Abra el archivo de Java de la aplicación principal en un editor de texto y agregue las siguientes líneas al archivo:</span><span class="sxs-lookup"><span data-stu-id="18b38-177">Open the main application Java file in a text editor, and add the following lines to the file:</span></span>

   ```java
   package com.wingtiptoys.storage;

   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;

   @SpringBootApplication
   public class StorageApplication {
      public static void main(String[] args) {
         SpringApplication.run(StorageApplication.class, args);
      }
   }
   ```

1. <span data-ttu-id="18b38-178">Guarde y cierre el archivo de Java de la aplicación principal.</span><span class="sxs-lookup"><span data-stu-id="18b38-178">Save and close the main application Java file.</span></span>

### <a name="add-a-web-controller-class"></a><span data-ttu-id="18b38-179">Adición de una clase de controlador web</span><span class="sxs-lookup"><span data-stu-id="18b38-179">Add a web controller class</span></span>

1. <span data-ttu-id="18b38-180">Cree un archivo Java nuevo llamado *WebController.java* en el directorio del paquete de la aplicación, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="18b38-180">Create a new Java file named *WebController.java* in the package directory of your app; for example:</span></span>

   `C:\SpringBoot\storage\src\main\java\com\wingtiptoys\storage\WebController.java`

   <span data-ttu-id="18b38-181">O bien</span><span class="sxs-lookup"><span data-stu-id="18b38-181">-or-</span></span>

   `/users/example/home/storage/src/main/java/com/wingtiptoys/storage/WebController.java`

1. <span data-ttu-id="18b38-182">Abra el archivo de Java del controlador web en un editor de texto y agregue las siguientes líneas al archivo:</span><span class="sxs-lookup"><span data-stu-id="18b38-182">Open the web controller Java file in a text editor, and add the following lines to the file:</span></span>

   ```java
   package com.wingtiptoys.storage;

   import org.springframework.beans.factory.annotation.Value;
   import org.springframework.core.io.Resource;
   import org.springframework.core.io.WritableResource;
   import org.springframework.util.StreamUtils;
   import org.springframework.web.bind.annotation.GetMapping;
   import org.springframework.web.bind.annotation.PostMapping;
   import org.springframework.web.bind.annotation.RequestBody;
   import org.springframework.web.bind.annotation.RestController;

   import java.io.IOException;
   import java.io.OutputStream;
   import java.nio.charset.Charset;

   @RestController
   public class WebController {

      @Value("blob://test/myfile.txt")
      private Resource blobFile;

      @GetMapping(value = "/")
      public String readBlobFile() throws IOException {
         return StreamUtils.copyToString(
            this.blobFile.getInputStream(),
            Charset.defaultCharset()) + "\n";
      }

      @PostMapping(value = "/")
      public String writeBlobFile(@RequestBody String data) throws IOException {
         try (OutputStream os = ((WritableResource) this.blobFile).getOutputStream()) {
            os.write(data.getBytes());
         }
         return "File was updated.\n";
      }
   }
   ```

   <span data-ttu-id="18b38-183">Donde la sintaxis `@Value("blob://[container]/[blob]")` define respectivamente los nombres del contenedor y el blob en los que desea almacenar los datos.</span><span class="sxs-lookup"><span data-stu-id="18b38-183">Where the `@Value("blob://[container]/[blob]")` syntax respectively defines the names of the container and blob where you want to store the data.</span></span>

1. <span data-ttu-id="18b38-184">Guarde y cierre el archivo de Java del controlador web.</span><span class="sxs-lookup"><span data-stu-id="18b38-184">Save and close the web controller Java file.</span></span>

1. <span data-ttu-id="18b38-185">Abra un símbolo del sistema y cambie el directorio a la carpeta donde se encuentra el archivo *pom.xml*; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="18b38-185">Open a command prompt and change directory to the folder where your *pom.xml* file is located; for example:</span></span>

   `cd C:\SpringBoot\storage`

   <span data-ttu-id="18b38-186">O bien</span><span class="sxs-lookup"><span data-stu-id="18b38-186">-or-</span></span>

   `cd /users/example/home/storage`

1. <span data-ttu-id="18b38-187">Compile la aplicación de Spring Boot con Maven y ejecútela; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="18b38-187">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. <span data-ttu-id="18b38-188">Una vez que se está ejecutando la aplicación, puede usar *curl* para probar la aplicación, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="18b38-188">Once your application is running, you can use *curl* to test your application; for example:</span></span>

   <span data-ttu-id="18b38-189">a.</span><span class="sxs-lookup"><span data-stu-id="18b38-189">a.</span></span> <span data-ttu-id="18b38-190">Envíe una solicitud POST para actualizar el contenido de un archivo:</span><span class="sxs-lookup"><span data-stu-id="18b38-190">Send a POST request to update a file's contents:</span></span>

      ```shell
      curl -X POST -H "Content-Type: text/plain" -d "Hello World" http://localhost:8080/
      ```

      <span data-ttu-id="18b38-191">Debería ver una respuesta que indica que se actualizó el archivo.</span><span class="sxs-lookup"><span data-stu-id="18b38-191">You should see a response that the file was updated.</span></span>

   <span data-ttu-id="18b38-192">b.</span><span class="sxs-lookup"><span data-stu-id="18b38-192">b.</span></span> <span data-ttu-id="18b38-193">Envíe una solicitud GET para comprobar el contenido del archivo:</span><span class="sxs-lookup"><span data-stu-id="18b38-193">Send a GET request to verify the file's contents:</span></span>

      ```shell
      curl -X GET http://localhost:8080/
      ```

     <span data-ttu-id="18b38-194">Debería ver el texto "Hello World" que se envió.</span><span class="sxs-lookup"><span data-stu-id="18b38-194">You should see the "Hello World" text that you posted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="18b38-195">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="18b38-195">Next steps</span></span>

<span data-ttu-id="18b38-196">Para más información acerca de otros iniciadores de Spring Boot disponibles para Microsoft Azure, consulte [Iniciadores de Spring Boot para Azure](spring-boot-starters-for-azure.md).</span><span class="sxs-lookup"><span data-stu-id="18b38-196">For more information about the additional Spring Boot Starters that are available for Microsoft Azure, see [Spring Boot Starters for Azure](spring-boot-starters-for-azure.md).</span></span>

<span data-ttu-id="18b38-197">Para más información acerca de cómo integrar la funcionalidad de Azure en aplicaciones basadas en Spring, consulte [Spring Framework en Azure](/java/azure/spring-framework/).</span><span class="sxs-lookup"><span data-stu-id="18b38-197">For additional information about integrating Azure functionality into your Spring-based applications, see [Spring Framework on Azure](/java/azure/spring-framework/).</span></span>

<span data-ttu-id="18b38-198">Para información detallada acerca de otras API de almacenamiento de Azure que puede llamar desde aplicaciones de Spring Boot, consulte los artículos siguientes:</span><span class="sxs-lookup"><span data-stu-id="18b38-198">For detailed information about additional Azure storage APIs that you can call from your Spring Boot applications, see the following articles:</span></span>
* [<span data-ttu-id="18b38-199">Uso de Azure Blob Storage en Java</span><span class="sxs-lookup"><span data-stu-id="18b38-199">How to use Azure Blob storage from Java</span></span>](/azure/storage/blobs/storage-java-how-to-use-blob-storage)
* [<span data-ttu-id="18b38-200">Uso de Azure Queue Storage en Java</span><span class="sxs-lookup"><span data-stu-id="18b38-200">How to use Azure Queue storage from Java</span></span>](/azure/storage/queues/storage-java-how-to-use-queue-storage)
* [<span data-ttu-id="18b38-201">Uso de Azure Table Storage en Java</span><span class="sxs-lookup"><span data-stu-id="18b38-201">How to use Azure Table storage from Java</span></span>](/azure/cosmos-db/table-storage-how-to-use-java)
* [<span data-ttu-id="18b38-202">Uso de Azure File Storage en Java</span><span class="sxs-lookup"><span data-stu-id="18b38-202">How to use Azure File storage from Java</span></span>](/azure/storage/files/storage-java-how-to-use-file-storage)

<!-- IMG List -->

[IMG01]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-storage-account-01.png
[IMG02]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-storage-account-02.png
[IMG03]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-storage-account-03.png
[IMG04]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-storage-account-04.png
[IMG05]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-storage-account-05.png

[SI01]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-project-01.png
[SI02]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-project-02.png
[SI03]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-project-03.png
