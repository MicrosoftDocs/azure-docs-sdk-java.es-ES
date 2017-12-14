---
title: "Cómo usar el iniciador de Spring Boot para Azure Storage"
description: "Aprenda a configurar una aplicación de Spring Boot Initializer con el iniciador de Azure Storage."
services: storage
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 12/01/2017
ms.author: yungez;robmcm
ms.openlocfilehash: 0979c810711a01464c0b2c6e12a582a3f5eefef1
ms.sourcegitcommit: fc48e038721e6910cb8b1f8951df765d517e504d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/06/2017
---
# <a name="how-to-use-the-spring-boot-starter-for-azure-storage"></a><span data-ttu-id="8a864-103">Cómo usar el iniciador de Spring Boot para Azure Storage</span><span class="sxs-lookup"><span data-stu-id="8a864-103">How to use the Spring Boot Starter for Azure Storage</span></span>

## <a name="overview"></a><span data-ttu-id="8a864-104">Información general</span><span class="sxs-lookup"><span data-stu-id="8a864-104">Overview</span></span>

<span data-ttu-id="8a864-105">En este artículo se describe cómo crear una aplicación personalizada con **Spring Initializr** y, después, cómo usarla para acceder a Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="8a864-105">This article walks you through creating a custom application using the **Spring Initializr**, and then using that application to access Azure storage.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8a864-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="8a864-106">Prerequisites</span></span>

<span data-ttu-id="8a864-107">Los siguientes requisitos previos son necesarios para seguir los pasos descritos en este artículo:</span><span class="sxs-lookup"><span data-stu-id="8a864-107">The following prerequisites are required in order to follow the steps in this article:</span></span>

* <span data-ttu-id="8a864-108">Una suscripción de Azure. Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) o registrarse para obtener una [cuenta de Azure gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8a864-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free Azure account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="8a864-109">La [Interfaz de la línea de comandos (CLI) de Azure](http://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8a864-109">The [Azure Command-Line Interface (CLI)](http://docs.microsoft.com/cli/azure/overview).</span></span>
* <span data-ttu-id="8a864-110">Un [kit de desarrollo de Java (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/) actualizado, versión 1.7 o posteriores.</span><span class="sxs-lookup"><span data-stu-id="8a864-110">An up-to-date [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 or later.</span></span>
* <span data-ttu-id="8a864-111">[Apache Maven](http://maven.apache.org/), versión 3.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="8a864-111">Apache's [Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-a-custom-application-using-the-spring-initializr"></a><span data-ttu-id="8a864-112">Creación de una aplicación personalizada mediante Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="8a864-112">Create a custom application using the Spring Initializr</span></span>

1. <span data-ttu-id="8a864-113">Vaya a <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="8a864-113">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="8a864-114">Especifique que quiere generar un proyecto de **Maven** con **Java**, escriba los nombres de **Group** (Grupo) y **Artifact** (Artefacto) de su aplicación y luego haga clic en el vínculo **Switch to the full version** (Cambiar a la versión completa) de Spring Initializr.</span><span class="sxs-lookup"><span data-stu-id="8a864-114">Specify that you want to generate a **Maven** project with **Java**, enter the **Group** and **Aritifact** names for your application, and then click the link to **Switch to the full version** of the Spring Initializr.</span></span>

   ![Opciones básicas de Spring Initializr](media/configure-spring-boot-starter-java-app-with-azure-storage/spring-initializr-basic.png)

   > [!NOTE]
   >
   > <span data-ttu-id="8a864-116">Spring Initializr usará los nombres de **Group** (Grupo) y **Artifact** (Artefacto) para crear el nombre del paquete, por ejemplo: *com.contoso.wingtiptoysdemo*.</span><span class="sxs-lookup"><span data-stu-id="8a864-116">The Spring Initializr will use the **Group** and **Aritifact** names to create the package name; for example: *com.contoso.wingtiptoysdemo*.</span></span>
   >

1. <span data-ttu-id="8a864-117">Desplácese a la sección **Azure** y active la casilla **Azure Storage**.</span><span class="sxs-lookup"><span data-stu-id="8a864-117">Scroll down to the **Azure** section and check the box for **Azure Storage**.</span></span>

   ![Opciones completas de Spring Initializr](media/configure-spring-boot-starter-java-app-with-azure-storage/spring-initializr-advanced.png)

1. <span data-ttu-id="8a864-119">Desplácese a la parte inferior de la página y haga clic en el botón **Generate Project** (Generar proyecto).</span><span class="sxs-lookup"><span data-stu-id="8a864-119">Scroll to the bottom of the page and click the button to **Generate Project**.</span></span>

   ![Opciones completas de Spring Initializr](media/configure-spring-boot-starter-java-app-with-azure-storage/spring-initializr-generate.png)

1. <span data-ttu-id="8a864-121">Cuando se le solicite, descargue el proyecto en una ruta de acceso del equipo local.</span><span class="sxs-lookup"><span data-stu-id="8a864-121">When prompted, download the project to a path on your local computer.</span></span>

   ![Descarga del proyecto personalizado de Spring Boot](media/configure-spring-boot-starter-java-app-with-azure-storage/download-app.png)

## <a name="sign-into-azure-and-select-the-subscription-to-use"></a><span data-ttu-id="8a864-123">Inicie sesión en Azure y seleccione la suscripción que desea usar.</span><span class="sxs-lookup"><span data-stu-id="8a864-123">Sign into Azure and select the subscription to use</span></span>

1. <span data-ttu-id="8a864-124">Abra el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="8a864-124">Open a command prompt.</span></span>

1. <span data-ttu-id="8a864-125">Inicie sesión en la cuenta de Azure mediante la CLI de Azure:</span><span class="sxs-lookup"><span data-stu-id="8a864-125">Sign into your Azure account by using the Azure CLI:</span></span>

   ```azurecli
   az login
   ```
   <span data-ttu-id="8a864-126">Siga las instrucciones para completar el proceso de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="8a864-126">Follow the instructions to complete the sign-in process.</span></span>

1. <span data-ttu-id="8a864-127">Muestre las suscripciones:</span><span class="sxs-lookup"><span data-stu-id="8a864-127">List your subscriptions:</span></span>

   ```azurecli
   az account list
   ```
   <span data-ttu-id="8a864-128">Azure devolverá la lista de sus suscripciones, y tendrá que copiar el GUID de la suscripción que desea usar; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="8a864-128">Azure will return a list of your subscriptions, and you will need to copy the GUID for the subscription that you want to use; for example:</span></span>

   ```json
   [
     {
       "cloudName": "AzureCloud",
       "id": "ssssssss-ssss-ssss-ssss-ssssssssssss",
       "isDefault": true,
       "name": "Converted Windows Azure MSDN - Visual Studio Ultimate",
       "state": "Enabled",
       "tenantId": "tttttttt-tttt-tttt-tttt-tttttttttttt",
       "user": {
         "name": "contoso@microsoft.com",
         "type": "user"
       }
     }
   ]

1. Specify the GUID for the account you want to use with Azure; for example:

   ```azurecli
   az account set -s ssssssss-ssss-ssss-ssss-ssssssssssss
   ```

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="8a864-129">Creación de una cuenta de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="8a864-129">Create an Azure Storage account</span></span>

1. <span data-ttu-id="8a864-130">Cree un grupo de recursos para los recursos de Azure que se usarán en este artículo; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="8a864-130">Create a resource group for the Azure resources you will use in this article; for example:</span></span>
   ```azurecli
   az group create --name wingtiptoysresources --location westus
   ```
   <span data-ttu-id="8a864-131">Donde:</span><span class="sxs-lookup"><span data-stu-id="8a864-131">Where:</span></span>
   | <span data-ttu-id="8a864-132">Parámetro</span><span class="sxs-lookup"><span data-stu-id="8a864-132">Parameter</span></span> | <span data-ttu-id="8a864-133">Descripción</span><span class="sxs-lookup"><span data-stu-id="8a864-133">Description</span></span> |
   |---|---|
   | `name` | <span data-ttu-id="8a864-134">Especifica un nombre único para el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="8a864-134">Specifies a unique name for your resource group.</span></span> |
   | `location` | <span data-ttu-id="8a864-135">Especifica la [región de Azure](https://azure.microsoft.com/regions/) donde se hospedará el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="8a864-135">Specifies the [Azure region](https://azure.microsoft.com/regions/) where your resource group will be hosted.</span></span> |

   <span data-ttu-id="8a864-136">La CLI de Azure mostrará los resultados de la creación del grupo de recursos, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="8a864-136">The Azure CLI will display the results of your resource group creation; for example:</span></span>  

   ```json
   {
     "id": "/subscriptions/ssssssss-ssss-ssss-ssss-ssssssssssss/resourceGroups/wingtiptoysresources",
     "location": "westus",
     "managedBy": null,
     "name": "wingtiptoysresources",
     "properties": {
       "provisioningState": "Succeeded"
     },
     "tags": null
   }
   ```

1. <span data-ttu-id="8a864-137">Cree una cuenta de almacenamiento de Azure en el grupo de recursos para su aplicación de Spring Boot; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="8a864-137">Create an Azure storage account in the in the resource group for your Spring Boot app; for example:</span></span>
   ```azurecli
   az storage account create --name wingtiptoysstorage --resource-group wingtiptoysresources --location westus --sku Standard_LRS
   ```
   <span data-ttu-id="8a864-138">Donde:</span><span class="sxs-lookup"><span data-stu-id="8a864-138">Where:</span></span>
   | <span data-ttu-id="8a864-139">Parámetro</span><span class="sxs-lookup"><span data-stu-id="8a864-139">Parameter</span></span> | <span data-ttu-id="8a864-140">Descripción</span><span class="sxs-lookup"><span data-stu-id="8a864-140">Description</span></span> |
   |---|---|
   | `name` | <span data-ttu-id="8a864-141">Especifica un nombre único para la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="8a864-141">Specifies a unique name for your storage account.</span></span> |
   | `resource-group` | <span data-ttu-id="8a864-142">Especifica el nombre del grupo de recursos que creó en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="8a864-142">Specifies the name of the resource group group you created in the previous step.</span></span> |
   | `location` | <span data-ttu-id="8a864-143">Especifica la [región de Azure](https://azure.microsoft.com/regions/) donde se hospedará la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="8a864-143">Specifies the [Azure region](https://azure.microsoft.com/regions/) where your storage account will be hosted.</span></span> |
   | `sku` | <span data-ttu-id="8a864-144">Especifica uno de los siguientes valores: `Premium_LRS`, `Standard_GRS`, `Standard_LRS`, `Standard_RAGRS`, `Standard_ZRS`.</span><span class="sxs-lookup"><span data-stu-id="8a864-144">Specifies one of the following: `Premium_LRS`, `Standard_GRS`, `Standard_LRS`, `Standard_RAGRS`, `Standard_ZRS`.</span></span> |

   <span data-ttu-id="8a864-145">Azure devolverá una cadena JSON larga que contiene el estado de aprovisionamiento; por ejemplo: |</span><span class="sxs-lookup"><span data-stu-id="8a864-145">Azure will return a long JSON string which contains the provisioning state; for example: |</span></span>
   
   ```json
   {
     "id": "/subscriptions/ssssssss-ssss-ssss-ssss-ssssssssssss/...",
     "identity": null,
     "kind": "Storage"
       ...
       ... (A long list of values will be displayed here.)
       ...
     "statusOfPrimary": "available",
     "statusOfSecondary": null,
     "tags": {},
     "type": "Microsoft.Storage/storageAccounts"
   }
   ```

1. <span data-ttu-id="8a864-146">Recupere la cadena de conexión de la cuenta de almacenamiento; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="8a864-146">Retrieve the connection string for your storage account; for example:</span></span>
   ```azurecli
   az storage account show-connection-string --name wingtiptoysstorage --resource-group wingtiptoysresources
   ```
   <span data-ttu-id="8a864-147">Donde:</span><span class="sxs-lookup"><span data-stu-id="8a864-147">Where:</span></span>
   | <span data-ttu-id="8a864-148">Parámetro</span><span class="sxs-lookup"><span data-stu-id="8a864-148">Parameter</span></span> | <span data-ttu-id="8a864-149">Descripción</span><span class="sxs-lookup"><span data-stu-id="8a864-149">Description</span></span> |
   | ---|---|
   | `name` | <span data-ttu-id="8a864-150">Especifica el nombre único de la cuenta de almacenamiento que creó en pasos anteriores.</span><span class="sxs-lookup"><span data-stu-id="8a864-150">Specifies a unique name of the storage account you created in previous steps.</span></span> |
   | `resource-group` | <span data-ttu-id="8a864-151">Especifica el nombre del grupo de recursos que creó en pasos anteriores.</span><span class="sxs-lookup"><span data-stu-id="8a864-151">Specifies the name of the resource group you created in previous steps.</span></span> |

   <span data-ttu-id="8a864-152">Azure devolverá una cadena JSON que contiene la cadena de conexión de la cuenta de almacenamiento; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="8a864-152">Azure will return a JSON string which contains the connection string for your storage account; for example:</span></span>

   ```json
   {
     "connectionString": "DefaultEndpointsProtocol=https;EndpointSuffix=core.windows.net;AccountName=wingtiptoysstorage;AccountKey=AbCdEfGhIjKlMnOpQrStUvWxYz=="
   }
   ```

## <a name="configure-and-compile-your-spring-boot-application"></a><span data-ttu-id="8a864-153">Configuración y compilación de la aplicación de Spring Boot</span><span class="sxs-lookup"><span data-stu-id="8a864-153">Configure and compile your Spring Boot application</span></span>

1. <span data-ttu-id="8a864-154">Extraiga en un directorio los archivos del archivo de proyecto descargado.</span><span class="sxs-lookup"><span data-stu-id="8a864-154">Extract the files from the downloaded project archive into a directory.</span></span>

1. <span data-ttu-id="8a864-155">Vaya a la carpeta *src/main/resources* del proyecto y abra el archivo *application.properties* en un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="8a864-155">Navigate to the *src/main/resources* folder in your project and open the *application.properties* file in a text editor.</span></span>

1. <span data-ttu-id="8a864-156">Escriba la clave de la cuenta de almacenamiento; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="8a864-156">Add the key for your storage account; for example:</span></span>
   ```yaml
   azure.storage.connection-string=DefaultEndpointsProtocol=https;EndpointSuffix=core.windows.net;AccountName=wingtiptoysstorage;AccountKey=AbCdEfGhIjKlMnOpQrStUvWxYz==
   ```

1. <span data-ttu-id="8a864-157">Vaya a la carpeta */src/main/java/com/example/wingtiptoysdemo* de su proyecto y abra el archivo *WingtiptoysdemoApplication.java* en un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="8a864-157">Navigate to the */src/main/java/com/example/wingtiptoysdemo* folder in your project and open the *WingtiptoysdemoApplication.java* file in a text editor.</span></span>

1. <span data-ttu-id="8a864-158">Reemplace el código Java existente por el ejemplo siguiente, que enumera los blobs de un contenedor:</span><span class="sxs-lookup"><span data-stu-id="8a864-158">Replace the existing Java code with the following example that lists the blobs in a container:</span></span>

   ```java
   package com.example.wingtiptoysdemo;

   import com.microsoft.azure.storage.*;
   import com.microsoft.azure.storage.blob.*;
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.boot.CommandLineRunner;
   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;

   import java.net.URISyntaxException;

   @SpringBootApplication
   public class WingtiptoysdemoApplication implements CommandLineRunner {

      @Autowired
      private CloudStorageAccount cloudStorageAccount;

      final String containerName = "mycontainer";

      public static void main(String[] args) {
         SpringApplication.run(WingtiptoysdemoApplication.class, args);
      }

      public void run(String... var1)
             throws URISyntaxException, StorageException {
          // Create a container (if it does not exist).
          createContainerIfNotExists(containerName);
          // Upload a blob to the container.
          uploadTextBlob(containerName);
      }

      private void createContainerIfNotExists(String containerName)
            throws URISyntaxException, StorageException {
         try
         {
            // Create a blob client.
            final CloudBlobClient blobClient = cloudStorageAccount.createCloudBlobClient();
            // Get a reference to a container. (Name must be lower case.)
            final CloudBlobContainer container = blobClient.getContainerReference(containerName);
            // Create the container if it does not exist.
            container.createIfNotExists();
         }
         catch (Exception e)
         {
            // Output the stack trace.
            e.printStackTrace();
         }
      }

      private void uploadTextBlob(String containerName)
            throws URISyntaxException, StorageException {
         try
         {
            // Create a blob client.
            final CloudBlobClient blobClient = cloudStorageAccount.createCloudBlobClient();
            // Get a reference to a container. (Name must be lower case.)
            final CloudBlobContainer container = blobClient.getContainerReference(containerName);
            // Get a blob reference for a text file.
            CloudBlockBlob blob = container.getBlockBlobReference("test.txt");
            // Upload some text into the blob.
            blob.uploadText("Hello World!");
         }
         catch (Exception e)
         {
            // Output the stack trace.
            e.printStackTrace();
         }
      }
   }
   ```
   > [!NOTE]
   >
   > <span data-ttu-id="8a864-159">El ejemplo anterior aplica automáticamente la configuración de la cuenta de almacenamiento que definió en el archivo *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="8a864-159">The above example autowires the storage account settings that you defined in the *application.properties* file.</span></span>
   >

1. <span data-ttu-id="8a864-160">Compile y ejecute la aplicación:</span><span class="sxs-lookup"><span data-stu-id="8a864-160">Compile and run the application:</span></span>
   ```shell
   mvn clean package spring-boot:run
   ```
   
   <span data-ttu-id="8a864-161">La aplicación creará un contenedor y cargará en él un archivo de texto como un blob, que se mostrará en la lista de la cuenta de almacenamiento, en [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8a864-161">The application will create a container and upload a text file as a blob to the container, which will be listed under your storage account in the [Azure portal](https://portal.azure.com).</span></span>

   ![Lista de blobs en Azure Portal](media/configure-spring-boot-starter-java-app-with-azure-storage/list-blobs-in-portal.png)

   > [!NOTE]
   > 
   > <span data-ttu-id="8a864-163">Al compilar la aplicación, puede que vea el siguiente mensaje de error:</span><span class="sxs-lookup"><span data-stu-id="8a864-163">When you compile your application, you might see the following error message:</span></span>
   > 
   > `[INFO] ------------------------------------------------------------------------`<br/>
   > `[INFO] BUILD FAILURE`<br/>
   > `[INFO] ------------------------------------------------------------------------`<br/>
   > `[INFO] Total time: 2.616 s`<br/>
   > `[INFO] Finished at: 2017-11-11T13:14:15Z`<br/>
   > `[INFO] Final Memory: 26M/213M`<br/>
   > `[INFO] ------------------------------------------------------------------------`<br/>
   > `[ERROR] Failed to execute goal org.apache.maven.plugins:maven-surefire-plugin:2`<br/>
   > `.18.1:test (default-test) on project wingtiptoysdemo: Execution default-test of`<br/>
   > `goal org.apache.maven.plugins:maven-surefire-plugin:2.18.1:test failed: The for`<br/>
   > `ked VM terminated without properly saying goodbye. VM crash or System.exit called?`<br/>
   > `[ERROR] Command was /bin/sh -c cd /home/robert/SpringBoot/wingtiptoysdemo && /u`<br/>
   > `sr/lib/jvm/java-8-openjdk-amd64/jre/bin/java -jar /home/robert/SpringBoot/wingt`<br/>
   > `iptoysdemo/target/surefire/surefirebooter6371623993063346766.jar /home/robert/S`<br/>
   > `pringBoot/wingtiptoysdemo/target/surefire/surefire5107893623933537917tmp /home/`<br/>
   > `robert/SpringBoot/wingtiptoysdemo/target/surefire/surefire_01414159391084128068tmp`<br/>
   > `[ERROR] -> [Help 1]`<br/>
   > 
   > <span data-ttu-id="8a864-164">En este caso, quizás quiera deshabilitar las pruebas Surefire de Maven; para ello, agregue la siguiente entrada de complemento al archivo *pom.xml*:</span><span class="sxs-lookup"><span data-stu-id="8a864-164">If this happens, you might want to disable the Maven Surefire testing; to do so, add the following plugin entry in your *pom.xml* file:</span></span>
   > 
   > ```xml
   > <plugin>
   >   <groupId>org.apache.maven.plugins</groupId>
   >   <artifactId>maven-surefire-plugin</artifactId>
   >   <version>2.20.1</version>
   >   <configuration>
   >     <skipTests>true</skipTests>
   >   </configuration>
   > </plugin>
   > ```
   > 

## <a name="next-steps"></a><span data-ttu-id="8a864-165">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8a864-165">Next steps</span></span>

<span data-ttu-id="8a864-166">Para más información acerca de otros iniciadores de Spring Boot disponibles para Microsoft Azure, consulte [Iniciadores de Spring Boot para Azure](spring-boot-starters-for-azure.md).</span><span class="sxs-lookup"><span data-stu-id="8a864-166">For more information about the additional Spring Boot Starters that are available for Microsoft Azure, see [Spring Boot Starters for Azure](spring-boot-starters-for-azure.md).</span></span>

<span data-ttu-id="8a864-167">Para más información acerca de cómo integrar la funcionalidad de Azure en aplicaciones basadas en Spring, consulte [Spring Framework en Azure](/java/azure/spring-framework/).</span><span class="sxs-lookup"><span data-stu-id="8a864-167">For additional information about integrating Azure functionality into your Spring-based applications, see [Spring Framework on Azure](/java/azure/spring-framework/).</span></span>

<span data-ttu-id="8a864-168">Para información detallada acerca de otras API de almacenamiento de Azure que puede llamar desde aplicaciones de Spring Boot, consulte los artículos siguientes:</span><span class="sxs-lookup"><span data-stu-id="8a864-168">For detailed information about additional Azure storage APIs that you can call from your Spring Boot applications, see the following articles:</span></span>
* [<span data-ttu-id="8a864-169">Uso de Azure Blob Storage en Java</span><span class="sxs-lookup"><span data-stu-id="8a864-169">How to use Azure Blob storage from Java</span></span>](/azure/storage/blobs/storage-java-how-to-use-blob-storage)
* [<span data-ttu-id="8a864-170">Uso de Azure Queue Storage en Java</span><span class="sxs-lookup"><span data-stu-id="8a864-170">How to use Azure Queue storage from Java</span></span>](/azure/storage/queues/storage-java-how-to-use-queue-storage)
* [<span data-ttu-id="8a864-171">Uso de Azure Table Storage en Java</span><span class="sxs-lookup"><span data-stu-id="8a864-171">How to use Azure Table storage from Java</span></span>](/azure/cosmos-db/table-storage-how-to-use-java)
* [<span data-ttu-id="8a864-172">Uso de Azure File Storage en Java</span><span class="sxs-lookup"><span data-stu-id="8a864-172">How to use Azure File storage from Java</span></span>](/azure/storage/files/storage-java-how-to-use-file-storage)
