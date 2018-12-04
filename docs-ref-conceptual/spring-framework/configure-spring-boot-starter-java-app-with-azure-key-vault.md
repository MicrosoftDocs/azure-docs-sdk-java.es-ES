---
title: Cómo usar el iniciador de Spring Boot para Azure Key Vault
description: Aprenda a configurar una aplicación de Spring Boot Initializer con el iniciador de Azure Key Vault.
services: key-vault
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 11/21/2018
ms.devlang: java
ms.service: key-vault
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: identity
ms.openlocfilehash: fcb18de809f4465239f1f360a755624a5095e03a
ms.sourcegitcommit: 8d0c59ae7c91adbb9be3c3e6d4a3429ffe51519d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/27/2018
ms.locfileid: "52339159"
---
# <a name="how-to-use-the-spring-boot-starter-for-azure-key-vault"></a><span data-ttu-id="e95c3-103">Cómo usar el iniciador de Spring Boot para Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="e95c3-103">How to use the Spring Boot Starter for Azure Key Vault</span></span>

## <a name="overview"></a><span data-ttu-id="e95c3-104">Información general</span><span class="sxs-lookup"><span data-stu-id="e95c3-104">Overview</span></span>

<span data-ttu-id="e95c3-105">En este artículo se muestra cómo crear una aplicación con **[Spring Initializr]** que usa la funcionalidad Spring Boot Starter para Azure Key Vault para recuperar una cadena de conexión almacenada como un secreto en un almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="e95c3-105">This article demonstrates creating an app with the **[Spring Initializr]** that uses the Spring Boot Starter for Azure Key Vault to retrieve a connection string that is stored as a secret in a key vault.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e95c3-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e95c3-106">Prerequisites</span></span>

<span data-ttu-id="e95c3-107">Los siguientes requisitos previos son necesarios para seguir los pasos descritos en este artículo:</span><span class="sxs-lookup"><span data-stu-id="e95c3-107">The following prerequisites are required in order to complete the steps in this article:</span></span>

* <span data-ttu-id="e95c3-108">Una suscripción de Azure. Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN] o registrarse para obtener una [cuenta de Azure gratuita].</span><span class="sxs-lookup"><span data-stu-id="e95c3-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="e95c3-109">Un kit de desarrollo de Java (JDK) admitido</span><span class="sxs-lookup"><span data-stu-id="e95c3-109">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="e95c3-110">Para más información sobre los JDK disponibles para desarrollar en Azure, consulte <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="e95c3-110">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="e95c3-111">[Apache Maven](http://maven.apache.org/), versión 3.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="e95c3-111">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-an-app-using-spring-initializr"></a><span data-ttu-id="e95c3-112">Creación de una aplicación con Spring Initialzr</span><span class="sxs-lookup"><span data-stu-id="e95c3-112">Create an app using Spring Initializr</span></span>

1. <span data-ttu-id="e95c3-113">Vaya a <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="e95c3-113">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="e95c3-114">Especifique que quiere generar un proyecto de **Maven** con **Java**, escriba los nombres de **Group** (Grupo) y **Artifact** (Artefacto) de su aplicación y luego haga clic en el vínculo **Switch to the full version** (Cambiar a la versión completa) de Spring Initializr.</span><span class="sxs-lookup"><span data-stu-id="e95c3-114">Specify that you want to generate a **Maven** project with **Java**, enter the **Group** and **Aritifact** names for your application, and then click the link to **Switch to the full version** of the Spring Initializr.</span></span>

   ![Especificar los nombres de grupo y artefacto][secrets-01]

1. <span data-ttu-id="e95c3-116">Desplácese a la sección **Azure** y active la casilla **Azure Key Vault**.</span><span class="sxs-lookup"><span data-stu-id="e95c3-116">Scroll down to the **Azure** section and check the box for **Azure Key Vault**.</span></span>

   ![Seleccione el iniciador Azure Key Vault][secrets-02]

1. <span data-ttu-id="e95c3-118">Desplácese a la parte inferior de la página y haga clic en el botón **Generate Project** (Generar proyecto).</span><span class="sxs-lookup"><span data-stu-id="e95c3-118">Scroll to the bottom of the page and click the button to **Generate Project**.</span></span>

   ![Generación del proyecto de Spring Boot][secrets-03]

1. <span data-ttu-id="e95c3-120">Cuando se le solicite, descargue el proyecto en una ruta de acceso del equipo local.</span><span class="sxs-lookup"><span data-stu-id="e95c3-120">When prompted, download the project to a path on your local computer.</span></span>

## <a name="sign-into-azure"></a><span data-ttu-id="e95c3-121">Inicio de sesión en Azure</span><span class="sxs-lookup"><span data-stu-id="e95c3-121">Sign into Azure</span></span>

1. <span data-ttu-id="e95c3-122">Abra el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="e95c3-122">Open a command prompt.</span></span>

1. <span data-ttu-id="e95c3-123">Inicie sesión en la cuenta de Azure mediante la CLI de Azure:</span><span class="sxs-lookup"><span data-stu-id="e95c3-123">Sign into your Azure account by using the Azure CLI:</span></span>

   ```azurecli
   az login
   ```
   <span data-ttu-id="e95c3-124">Siga las instrucciones para completar el proceso de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="e95c3-124">Follow the instructions to complete the sign-in process.</span></span>

1. <span data-ttu-id="e95c3-125">Muestre las suscripciones:</span><span class="sxs-lookup"><span data-stu-id="e95c3-125">List your subscriptions:</span></span>

   ```azurecli
   az account list
   ```
   <span data-ttu-id="e95c3-126">Azure devolverá la lista de sus suscripciones, y tendrá que copiar el GUID de la suscripción que desea usar; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="e95c3-126">Azure will return a list of your subscriptions, and you will need to copy the GUID for the subscription that you want to use; for example:</span></span>

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
   ```

1. <span data-ttu-id="e95c3-127">Especifique el identificador GUID de la cuenta que desea usar con Azure; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="e95c3-127">Specify the GUID for the account you want to use with Azure; for example:</span></span>

   ```azurecli
   az account set -s ssssssss-ssss-ssss-ssss-ssssssssssss
   ```

## <a name="create-a-new-azure-key-vault"></a><span data-ttu-id="e95c3-128">Creación de un nuevo almacén de claves de Azure</span><span class="sxs-lookup"><span data-stu-id="e95c3-128">Create a new Azure Key Vault</span></span>

1. <span data-ttu-id="e95c3-129">Cree un grupo de recursos para los recursos de Azure que se usarán para el almacén de claves; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="e95c3-129">Create a resource group for the Azure resources you will use for your key vault; for example:</span></span>
   ```azurecli
   az group create --name wingtiptoysresources --location westus
   ```
   <span data-ttu-id="e95c3-130">Donde:</span><span class="sxs-lookup"><span data-stu-id="e95c3-130">Where:</span></span>

   | <span data-ttu-id="e95c3-131">Parámetro</span><span class="sxs-lookup"><span data-stu-id="e95c3-131">Parameter</span></span> | <span data-ttu-id="e95c3-132">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="e95c3-132">Description</span></span> |
   |---|---|
   | `name` | <span data-ttu-id="e95c3-133">Especifica un nombre único para el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="e95c3-133">Specifies a unique name for your resource group.</span></span> |
   | `location` | <span data-ttu-id="e95c3-134">Especifica la [región de Azure](https://azure.microsoft.com/regions/) donde se hospedará el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="e95c3-134">Specifies the [Azure region](https://azure.microsoft.com/regions/) where your resource group will be hosted.</span></span> |

   <span data-ttu-id="e95c3-135">La CLI de Azure mostrará los resultados de la creación del grupo de recursos, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="e95c3-135">The Azure CLI will display the results of your resource group creation; for example:</span></span>  

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

2. <span data-ttu-id="e95c3-136">Cree una entidad de servicio de Azure desde el registro de su aplicación; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="e95c3-136">Create an Azure service principal from your application registration; for example:</span></span>
   ```shell
   az ad sp create-for-rbac --name "wingtiptoysuser"
   ```
   <span data-ttu-id="e95c3-137">Donde:</span><span class="sxs-lookup"><span data-stu-id="e95c3-137">Where:</span></span>

   | <span data-ttu-id="e95c3-138">Parámetro</span><span class="sxs-lookup"><span data-stu-id="e95c3-138">Parameter</span></span> | <span data-ttu-id="e95c3-139">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="e95c3-139">Description</span></span> |
   |---|---|
   | `name` | <span data-ttu-id="e95c3-140">Especifica el nombre de la entidad de servicio de Azure.</span><span class="sxs-lookup"><span data-stu-id="e95c3-140">Specifies the name for your Azure service principal.</span></span> |

   <span data-ttu-id="e95c3-141">La CLI de Azure devolverá un mensaje de estado de JSON que contiene los valores de *appId* y *password*, que usará más adelante como identificador de cliente y contraseña de cliente; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="e95c3-141">The Azure CLI will return a JSON status message that contains the *appId* and *password*, which you will use later as the client id and client password; for example:</span></span>

   ```json
   {
     "appId": "iiiiiiii-iiii-iiii-iiii-iiiiiiiiiiii",
     "displayName": "wingtiptoysuser",
     "name": "http://wingtiptoysuser",
     "password": "pppppppp-pppp-pppp-pppp-pppppppppppp",
     "tenant": "tttttttt-tttt-tttt-tttt-tttttttttttt"
   }
   ```

3. <span data-ttu-id="e95c3-142">Cree un nuevo almacén de claves en el grupo de recursos; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="e95c3-142">Create a new key vault in the resource group; for example:</span></span>
   ```azurecli
   az keyvault create --name wingtiptoyskeyvault --resource-group wingtiptoysresources --location westus --enabled-for-deployment true --enabled-for-disk-encryption true --enabled-for-template-deployment true --sku standard --query properties.vaultUri
   ```
   <span data-ttu-id="e95c3-143">Donde:</span><span class="sxs-lookup"><span data-stu-id="e95c3-143">Where:</span></span>

   | <span data-ttu-id="e95c3-144">Parámetro</span><span class="sxs-lookup"><span data-stu-id="e95c3-144">Parameter</span></span> | <span data-ttu-id="e95c3-145">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="e95c3-145">Description</span></span> |
   |---|---|
   | `name` | <span data-ttu-id="e95c3-146">Especifica un nombre único para el almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="e95c3-146">Specifies a unique name for your key vault.</span></span> |
   | `location` | <span data-ttu-id="e95c3-147">Especifica la [región de Azure](https://azure.microsoft.com/regions/) donde se hospedará el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="e95c3-147">Specifies the [Azure region](https://azure.microsoft.com/regions/) where your resource group will be hosted.</span></span> |
   | `enabled-for-deployment` | <span data-ttu-id="e95c3-148">Especifica la [opción de implementación del almacén de claves](https://docs.microsoft.com/cli/azure/keyvault).</span><span class="sxs-lookup"><span data-stu-id="e95c3-148">Specifies the [key vault deployment option](https://docs.microsoft.com/cli/azure/keyvault).</span></span> |
   | `enabled-for-disk-encryption` | <span data-ttu-id="e95c3-149">Especifica la [opción de cifrado del almacén de claves](https://docs.microsoft.com/cli/azure/keyvault).</span><span class="sxs-lookup"><span data-stu-id="e95c3-149">Specifies the [key vault encryption option](https://docs.microsoft.com/cli/azure/keyvault).</span></span> |
   | `enabled-for-template-deployment` | <span data-ttu-id="e95c3-150">Especifica la [opción de cifrado del almacén de claves](https://docs.microsoft.com/cli/azure/keyvault).</span><span class="sxs-lookup"><span data-stu-id="e95c3-150">Specifies the [key vault encryption option](https://docs.microsoft.com/cli/azure/keyvault).</span></span> |
   | `sku` | <span data-ttu-id="e95c3-151">Especifica la [opción de SKU del almacén de claves](https://docs.microsoft.com/cli/azure/keyvault).</span><span class="sxs-lookup"><span data-stu-id="e95c3-151">Specifies the [key vault SKU option](https://docs.microsoft.com/cli/azure/keyvault).</span></span> |
   | `query` | <span data-ttu-id="e95c3-152">Especifica el valor que se recuperará de la respuesta, que es el URI del almacén de claves que tendrá que completar en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="e95c3-152">Specifies a value to retrieve from the response, which is the key vault URI that you will need to complete this tutorial.</span></span> |

   <span data-ttu-id="e95c3-153">La CLI de Azure mostrará el URI del almacén de claves, que usará más adelante; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="e95c3-153">The Azure CLI will display the URI for key vault, which you will use later; for example:</span></span>  

   ```
   "https://wingtiptoyskeyvault.vault.azure.net"
   ```

4. <span data-ttu-id="e95c3-154">Establezca la directiva de acceso de la entidad de servicio de Azure que creó anteriormente; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="e95c3-154">Set the access policy for the Azure service principal you created earlier; for example:</span></span>
   ```azurecli
   az keyvault set-policy --name wingtiptoyskeyvault --secret-permission set get list delete --spn "iiiiiiii-iiii-iiii-iiii-iiiiiiiiiiii"
   ```
   <span data-ttu-id="e95c3-155">Donde:</span><span class="sxs-lookup"><span data-stu-id="e95c3-155">Where:</span></span>

   | <span data-ttu-id="e95c3-156">Parámetro</span><span class="sxs-lookup"><span data-stu-id="e95c3-156">Parameter</span></span> | <span data-ttu-id="e95c3-157">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="e95c3-157">Description</span></span> |
   |---|---|
   | `name` | <span data-ttu-id="e95c3-158">Especifica el nombre del almacén de claves anterior.</span><span class="sxs-lookup"><span data-stu-id="e95c3-158">Specifies your key vault name from earlier.</span></span> |
   | `secret-permission` | <span data-ttu-id="e95c3-159">Especifica las [directivas de seguridad](https://docs.microsoft.com/cli/azure/keyvault) para su almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="e95c3-159">Specifies the [security policies](https://docs.microsoft.com/cli/azure/keyvault) for your key vault.</span></span> |
   | `spn` | <span data-ttu-id="e95c3-160">Especifica el GUID del registro de la aplicación anterior.</span><span class="sxs-lookup"><span data-stu-id="e95c3-160">Specifies the GUID for your application registration from earlier.</span></span> |

   <span data-ttu-id="e95c3-161">La CLI de Azure mostrará los resultados de la creación de la directiva de seguridad, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="e95c3-161">The Azure CLI will display the results of your security policy creation; for example:</span></span>  

   ```json
   {
     "id": "/subscriptions/ssssssss-ssss-ssss-ssss-ssssssssssss/...",
     "location": "westus",
     "name": "wingtiptoyskeyvault",
     "properties": {
       ...
       ... (A long list of values will be displayed here.)
       ...
     },
     "resourceGroup": "wingtiptoysresources",
     "tags": {},
     "type": "Microsoft.KeyVault/vaults"
   }
   ```

5. <span data-ttu-id="e95c3-162">Guarde un secreto en su nuevo almacén de claves; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="e95c3-162">Store a secret in your new key vault; for example:</span></span>
   ```azurecli
   az keyvault secret set --vault-name "wingtiptoyskeyvault" --name "connectionString" --value "jdbc:sqlserver://SERVER.database.windows.net:1433;database=DATABASE;"
   ```
   <span data-ttu-id="e95c3-163">Donde:</span><span class="sxs-lookup"><span data-stu-id="e95c3-163">Where:</span></span>

   | <span data-ttu-id="e95c3-164">Parámetro</span><span class="sxs-lookup"><span data-stu-id="e95c3-164">Parameter</span></span> | <span data-ttu-id="e95c3-165">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="e95c3-165">Description</span></span> |
   |---|---|
   | `vault-name` | <span data-ttu-id="e95c3-166">Especifica el nombre del almacén de claves anterior.</span><span class="sxs-lookup"><span data-stu-id="e95c3-166">Specifies your key vault name from earlier.</span></span> |
   | `name` | <span data-ttu-id="e95c3-167">Especifica el nombre del secreto.</span><span class="sxs-lookup"><span data-stu-id="e95c3-167">Specifies the name of your secret.</span></span> |
   | `value` | <span data-ttu-id="e95c3-168">Especifica el valor del secreto.</span><span class="sxs-lookup"><span data-stu-id="e95c3-168">Specifies the value of your secret.</span></span> |

   <span data-ttu-id="e95c3-169">La CLI de Azure mostrará los resultados de la creación del secreto; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="e95c3-169">The Azure CLI will display the results of your secret creation; for example:</span></span>  

   ```json
   {
     "attributes": {
       "created": "2017-12-01T09:00:16+00:00",
       "enabled": true,
       "expires": null,
       "notBefore": null,
       "recoveryLevel": "Purgeable",
       "updated": "2017-12-01T09:00:16+00:00"
     },
     "contentType": null,
     "id": "https://wingtiptoyskeyvault.vault.azure.net/secrets/connectionString/123456789abcdef123456789abcdef",
     "kid": null,
     "managed": null,
     "tags": {
       "file-encoding": "utf-8"
     },
     "value": "jdbc:sqlserver://wingtiptoys.database.windows.net:1433;database=DATABASE;"
   }
   ```

## <a name="configure-and-compile-your-app"></a><span data-ttu-id="e95c3-170">Configuración y compilación de la aplicación</span><span class="sxs-lookup"><span data-stu-id="e95c3-170">Configure and compile your app</span></span>

1. <span data-ttu-id="e95c3-171">Extraiga los archivos del archivo del proyecto de Spring Boot que descargó anteriormente en un directorio.</span><span class="sxs-lookup"><span data-stu-id="e95c3-171">Extract the files from the Spring Boot project archive files that you downloaded earlier into a directory.</span></span>

2. <span data-ttu-id="e95c3-172">Vaya a la carpeta *src/main/resources* del proyecto y abra el archivo *application.properties* en un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="e95c3-172">Navigate to the *src/main/resources* folder in your project and open the *application.properties* file in a text editor.</span></span>

3. <span data-ttu-id="e95c3-173">Agregue los valores del almacén de claves que obtuvo en los pasos realizados anteriormente en este tutorial; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="e95c3-173">Add the values for your key vault using values from the steps that you completed earlier in this tutorial; for example:</span></span>
   ```yaml
   azure.keyvault.uri=https://wingtiptoyskeyvault.vault.azure.net/
   azure.keyvault.client-id=iiiiiiii-iiii-iiii-iiii-iiiiiiiiiiii
   azure.keyvault.client-key=pppppppp-pppp-pppp-pppp-pppppppppppp
   ```
   <span data-ttu-id="e95c3-174">Donde:</span><span class="sxs-lookup"><span data-stu-id="e95c3-174">Where:</span></span>

   |          <span data-ttu-id="e95c3-175">Parámetro</span><span class="sxs-lookup"><span data-stu-id="e95c3-175">Parameter</span></span>          |                                 <span data-ttu-id="e95c3-176">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="e95c3-176">Description</span></span>                                 |
   |-----------------------------|-----------------------------------------------------------------------------|
   |    `azure.keyvault.uri`     |           <span data-ttu-id="e95c3-177">Especifica el URI obtenido cuando creó el almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="e95c3-177">Specifies the URI from when you created your key vault.</span></span>           |
   | `azure.keyvault.client-id`  |  <span data-ttu-id="e95c3-178">Especifica el GUID de *appId* obtenido cuando creó la entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="e95c3-178">Specifies the *appId* GUID from when you created your service principal.</span></span>   |
   | `azure.keyvault.client-key` | <span data-ttu-id="e95c3-179">Especifica el GUID de *password* obtenido cuando creó la entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="e95c3-179">Specifies the *password* GUID from when you created your service principal.</span></span> |


4. <span data-ttu-id="e95c3-180">Vaya al archivo de código fuente principal del proyecto; por ejemplo: */src/main/java/com/wingtiptoys/secrets*.</span><span class="sxs-lookup"><span data-stu-id="e95c3-180">Navigate to the main source code file of your project; for example: */src/main/java/com/wingtiptoys/secrets*.</span></span>

5. <span data-ttu-id="e95c3-181">Abra el archivo Java principal de la aplicación en un editor de texto (por ejemplo: *SecretsApplication.java*) y agregue las siguientes líneas al archivo:</span><span class="sxs-lookup"><span data-stu-id="e95c3-181">Open the application's main Java file in a file in a text editor; for example: *SecretsApplication.java*, and add the following lines to the file:</span></span>

   ```java
   package com.wingtiptoys.secrets;

   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;
   import org.springframework.beans.factory.annotation.Value;
   import org.springframework.boot.CommandLineRunner;

   @SpringBootApplication
   public class SecretsApplication implements CommandLineRunner {

      @Value("${connectionString}")
      private String connectionString;

      public static void main(String[] args) {
         SpringApplication.run(SecretsApplication.class, args);
      }

      public void run(String... varl) throws Exception {
         System.out.println(String.format("\nConnection String stored in Azure Key Vault:\n%s\n",connectionString));
      }
   }
   ```
   <span data-ttu-id="e95c3-182">Este código de ejemplo recupera la cadena de conexión del almacén de claves y la muestra en la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="e95c3-182">This code example retrieves the connection string from the key vault and displays it to the command line.</span></span>

6. <span data-ttu-id="e95c3-183">Guarde y cierre el archivo Java.</span><span class="sxs-lookup"><span data-stu-id="e95c3-183">Save and close the Java file.</span></span>

## <a name="build-and-test-your-app"></a><span data-ttu-id="e95c3-184">Compilación y prueba de la aplicación</span><span class="sxs-lookup"><span data-stu-id="e95c3-184">Build and test your app</span></span>

1. <span data-ttu-id="e95c3-185">Vaya al directorio donde está el archivo *pom.xml* de su aplicación de Spring Boot:</span><span class="sxs-lookup"><span data-stu-id="e95c3-185">Navigate to the directory where the *pom.xml* file for your Spring Boot app is located:</span></span>

1. <span data-ttu-id="e95c3-186">Compile la aplicación de Spring Boot con Maven; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="e95c3-186">Build your Spring Boot application with Maven; for example:</span></span>

   ```bash
   mvn clean package
   ```

   <span data-ttu-id="e95c3-187">Maven mostrará los resultados de la compilación.</span><span class="sxs-lookup"><span data-stu-id="e95c3-187">Maven will display the results of your build.</span></span>

   ![Estado de compilación de la aplicación de Spring Boot][build-application-01]

1. <span data-ttu-id="e95c3-189">Ejecute la aplicación de Spring Boot con Maven; la aplicación mostrará la cadena de conexión del almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="e95c3-189">Run your Spring Boot application with Maven; the application will display the connection string from your key vault.</span></span> <span data-ttu-id="e95c3-190">Por ejemplo: </span><span class="sxs-lookup"><span data-stu-id="e95c3-190">For example:</span></span>

   ```bash
   mvn spring-boot:run
   ```

   ![Mensaje en tiempo de ejecución de Spring Boot][build-application-02]

## <a name="summary"></a><span data-ttu-id="e95c3-192">Resumen</span><span class="sxs-lookup"><span data-stu-id="e95c3-192">Summary</span></span>

<span data-ttu-id="e95c3-193">En este tutorial, ha creado una nueva aplicación web de Java con **[Spring Initializr]**, ha creado un almacén de claves de Azure para almacenar información confidencial y, a continuación, ha configurado la aplicación para recuperar información del almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="e95c3-193">In this tutorial, you created a new Java web application using the **[Spring Initializr]**, created ab Azure Key Vault to store sensitive information, and then configured your application to retrieve information from your key vault.</span></span>

<span data-ttu-id="e95c3-194">Para más información sobre el uso de Azure Key Vault, consulte los siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="e95c3-194">For more information about using Azure Key Vaults, see the following articles:</span></span>

* <span data-ttu-id="e95c3-195">[Documentación de Key Vault].</span><span class="sxs-lookup"><span data-stu-id="e95c3-195">[Key Vault Documentation].</span></span>

* <span data-ttu-id="e95c3-196">[Introducción a Azure Key Vault]</span><span class="sxs-lookup"><span data-stu-id="e95c3-196">[Get started with Azure Key Vault]</span></span>

<span data-ttu-id="e95c3-197">Para obtener más información sobre el uso de aplicaciones de Spring Boot en Azure, consulte los siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="e95c3-197">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="e95c3-198">Implementación de una aplicación de Spring Boot en Azure App Service</span><span class="sxs-lookup"><span data-stu-id="e95c3-198">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)

* [<span data-ttu-id="e95c3-199">Ejecución de una aplicación de Spring Boot en un clúster de Kubernetes en Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="e95c3-199">Running a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="e95c3-200">Para más información sobre el uso de Azure con Java, consulte [Azure para desarrolladores de Java] y [Herramientas de Java para Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="e95c3-200">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

## <a name="next-steps"></a><span data-ttu-id="e95c3-201">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e95c3-201">Next steps</span></span>

<span data-ttu-id="e95c3-202">Para más información acerca de Spring y Azure, vaya al centro de documentación de Azure.</span><span class="sxs-lookup"><span data-stu-id="e95c3-202">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e95c3-203">Spring en Azure</span><span class="sxs-lookup"><span data-stu-id="e95c3-203">Spring on Azure</span></span>](/java/azure/spring-framework)

<!-- URL List -->

[Documentación de Key Vault]: /azure/key-vault/
[Key Vault Documentation]: /azure/key-vault/
[Introducción a Azure Key Vault]: /azure/key-vault/key-vault-get-started
[Get started with Azure Key Vault]: /azure/key-vault/key-vault-get-started
[Azure para desarrolladores de Java]: https://docs.microsoft.com/java/azure/
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
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

[secrets-01]: media/configure-spring-boot-starter-java-app-with-azure-key-vault/secrets-01.png
[secrets-02]: media/configure-spring-boot-starter-java-app-with-azure-key-vault/secrets-02.png
[secrets-03]: media/configure-spring-boot-starter-java-app-with-azure-key-vault/secrets-03.png

[build-application-01]: media/configure-spring-boot-starter-java-app-with-azure-key-vault/build-application-01.png
[build-application-02]: media/configure-spring-boot-starter-java-app-with-azure-key-vault/build-application-02.png
