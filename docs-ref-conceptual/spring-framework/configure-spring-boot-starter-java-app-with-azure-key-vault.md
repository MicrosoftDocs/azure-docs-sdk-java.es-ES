---
title: Cómo usar el iniciador de Spring Boot para Azure Key Vault
description: Aprenda a configurar una aplicación de Spring Boot Initializer con el iniciador de Azure Key Vault.
services: key-vault
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 02/01/2018
ms.devlang: java
ms.service: key-vault
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: identity
ms.openlocfilehash: 78b7a9a2e26168b19dc8a1d12e47456752b57ffc
ms.sourcegitcommit: e017de4677c5bedd6ef88c8c1b6da279dc973efe
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/15/2018
ms.locfileid: "45639778"
---
# <a name="how-to-use-the-spring-boot-starter-for-azure-key-vault"></a><span data-ttu-id="dfcb8-103">Cómo usar el iniciador de Spring Boot para Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="dfcb8-103">How to use the Spring Boot Starter for Azure Key Vault</span></span>

## <a name="overview"></a><span data-ttu-id="dfcb8-104">Información general</span><span class="sxs-lookup"><span data-stu-id="dfcb8-104">Overview</span></span>

<span data-ttu-id="dfcb8-105">En este artículo se muestra cómo crear una aplicación con **[Spring Initializr]** que usa la funcionalidad Spring Boot Starter para Azure Key Vault para recuperar una cadena de conexión almacenada como un secreto en un almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="dfcb8-105">This article demonstrates creating an app with the **[Spring Initializr]** that uses the Spring Boot Starter for Azure Key Vault to retrieve a connection string that is stored as a secret in a key vault.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dfcb8-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="dfcb8-106">Prerequisites</span></span>

<span data-ttu-id="dfcb8-107">Los siguientes requisitos previos son necesarios para seguir los pasos descritos en este artículo:</span><span class="sxs-lookup"><span data-stu-id="dfcb8-107">The following prerequisites are required in order to complete the steps in this article:</span></span>

* <span data-ttu-id="dfcb8-108">Una suscripción de Azure. Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN] o registrarse para obtener una [cuenta de Azure gratuita].</span><span class="sxs-lookup"><span data-stu-id="dfcb8-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="dfcb8-109">Un [kit de desarrollo de Java (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), versión 1.7 o posterior.</span><span class="sxs-lookup"><span data-stu-id="dfcb8-109">A [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 or later.</span></span>
* <span data-ttu-id="dfcb8-110">[Apache Maven](http://maven.apache.org/), versión 3.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="dfcb8-110">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-an-app-using-the-spring-initialzr"></a><span data-ttu-id="dfcb8-111">Creación de una aplicación con Spring Initialzr</span><span class="sxs-lookup"><span data-stu-id="dfcb8-111">Create an app using the Spring Initialzr</span></span>

1. <span data-ttu-id="dfcb8-112">Vaya a <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="dfcb8-112">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="dfcb8-113">Especifique que quiere generar un proyecto de **Maven** con **Java**, escriba los nombres de **Group** (Grupo) y **Artifact** (Artefacto) de su aplicación y luego haga clic en el vínculo **Switch to the full version** (Cambiar a la versión completa) de Spring Initializr.</span><span class="sxs-lookup"><span data-stu-id="dfcb8-113">Specify that you want to generate a **Maven** project with **Java**, enter the **Group** and **Aritifact** names for your application, and then click the link to **Switch to the full version** of the Spring Initializr.</span></span>

   ![Especificar los nombres de grupo y artefacto][secrets-01]

1. <span data-ttu-id="dfcb8-115">Desplácese a la sección **Azure** y active la casilla **Azure Key Vault**.</span><span class="sxs-lookup"><span data-stu-id="dfcb8-115">Scroll down to the **Azure** section and check the box for **Azure Key Vault**.</span></span>

   ![Seleccione el iniciador Azure Key Vault][secrets-02]

1. <span data-ttu-id="dfcb8-117">Desplácese a la parte inferior de la página y haga clic en el botón **Generate Project** (Generar proyecto).</span><span class="sxs-lookup"><span data-stu-id="dfcb8-117">Scroll to the bottom of the page and click the button to **Generate Project**.</span></span>

   ![Generación del proyecto de Spring Boot][secrets-03]

1. <span data-ttu-id="dfcb8-119">Cuando se le solicite, descargue el proyecto en una ruta de acceso del equipo local.</span><span class="sxs-lookup"><span data-stu-id="dfcb8-119">When prompted, download the project to a path on your local computer.</span></span>

## <a name="sign-into-azure-and-select-the-subscription-to-use"></a><span data-ttu-id="dfcb8-120">Inicie sesión en Azure y seleccione la suscripción que desea usar.</span><span class="sxs-lookup"><span data-stu-id="dfcb8-120">Sign into Azure and select the subscription to use</span></span>

1. <span data-ttu-id="dfcb8-121">Abra el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="dfcb8-121">Open a command prompt.</span></span>

1. <span data-ttu-id="dfcb8-122">Inicie sesión en la cuenta de Azure mediante la CLI de Azure:</span><span class="sxs-lookup"><span data-stu-id="dfcb8-122">Sign into your Azure account by using the Azure CLI:</span></span>

   ```azurecli
   az login
   ```
   <span data-ttu-id="dfcb8-123">Siga las instrucciones para completar el proceso de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="dfcb8-123">Follow the instructions to complete the sign-in process.</span></span>

1. <span data-ttu-id="dfcb8-124">Muestre las suscripciones:</span><span class="sxs-lookup"><span data-stu-id="dfcb8-124">List your subscriptions:</span></span>

   ```azurecli
   az account list
   ```
   <span data-ttu-id="dfcb8-125">Azure devolverá la lista de sus suscripciones, y tendrá que copiar el GUID de la suscripción que desea usar; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="dfcb8-125">Azure will return a list of your subscriptions, and you will need to copy the GUID for the subscription that you want to use; for example:</span></span>

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

1. <span data-ttu-id="dfcb8-126">Especifique el identificador GUID de la cuenta que desea usar con Azure; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="dfcb8-126">Specify the GUID for the account you want to use with Azure; for example:</span></span>

   ```azurecli
   az account set -s ssssssss-ssss-ssss-ssss-ssssssssssss
   ```

## <a name="create-and-configure-a-new-azure-key-vault-using-the-azure-cli"></a><span data-ttu-id="dfcb8-127">Creación y configuración de un nuevo almacén de claves de Azure Key Vault mediante la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="dfcb8-127">Create and configure a new Azure Key Vault using the Azure CLI</span></span>

1. <span data-ttu-id="dfcb8-128">Cree un grupo de recursos para los recursos de Azure que se usarán para el almacén de claves; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="dfcb8-128">Create a resource group for the Azure resources you will use for your key vault; for example:</span></span>
   ```azurecli
   az group create --name wingtiptoysresources --location westus
   ```
   <span data-ttu-id="dfcb8-129">Donde:</span><span class="sxs-lookup"><span data-stu-id="dfcb8-129">Where:</span></span>

   | <span data-ttu-id="dfcb8-130">Parámetro</span><span class="sxs-lookup"><span data-stu-id="dfcb8-130">Parameter</span></span> | <span data-ttu-id="dfcb8-131">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="dfcb8-131">Description</span></span> |
   |---|---|
   | `name` | <span data-ttu-id="dfcb8-132">Especifica un nombre único para el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="dfcb8-132">Specifies a unique name for your resource group.</span></span> |
   | `location` | <span data-ttu-id="dfcb8-133">Especifica la [región de Azure](https://azure.microsoft.com/regions/) donde se hospedará el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="dfcb8-133">Specifies the [Azure region](https://azure.microsoft.com/regions/) where your resource group will be hosted.</span></span> |

   <span data-ttu-id="dfcb8-134">La CLI de Azure mostrará los resultados de la creación del grupo de recursos, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="dfcb8-134">The Azure CLI will display the results of your resource group creation; for example:</span></span>  

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

2. <span data-ttu-id="dfcb8-135">Cree una entidad de servicio de Azure desde el registro de su aplicación; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="dfcb8-135">Create an Azure service principal from your application registration; for example:</span></span>
   ```shell
   az ad sp create-for-rbac --name "wingtiptoysuser"
   ```
   <span data-ttu-id="dfcb8-136">Donde:</span><span class="sxs-lookup"><span data-stu-id="dfcb8-136">Where:</span></span>

   | <span data-ttu-id="dfcb8-137">Parámetro</span><span class="sxs-lookup"><span data-stu-id="dfcb8-137">Parameter</span></span> | <span data-ttu-id="dfcb8-138">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="dfcb8-138">Description</span></span> |
   |---|---|
   | `name` | <span data-ttu-id="dfcb8-139">Especifica el nombre de la entidad de servicio de Azure.</span><span class="sxs-lookup"><span data-stu-id="dfcb8-139">Specifies the name for your Azure service principal.</span></span> |

   <span data-ttu-id="dfcb8-140">La CLI de Azure devolverá un mensaje de estado de JSON que contiene los valores de *appId* y *password*, que usará más adelante como identificador de cliente y contraseña de cliente; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="dfcb8-140">The Azure CLI will return a JSON status message that contains the *appId* and *password*, which you will use later as the client id and client password; for example:</span></span>

   ```json
   {
     "appId": "iiiiiiii-iiii-iiii-iiii-iiiiiiiiiiii",
     "displayName": "wingtiptoysuser",
     "name": "http://wingtiptoysuser",
     "password": "pppppppp-pppp-pppp-pppp-pppppppppppp",
     "tenant": "tttttttt-tttt-tttt-tttt-tttttttttttt"
   }
   ```

3. <span data-ttu-id="dfcb8-141">Cree un nuevo almacén de claves en el grupo de recursos; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="dfcb8-141">Create a new key vault in the resource group; for example:</span></span>
   ```azurecli
   az keyvault create --name wingtiptoyskeyvault --resource-group wingtiptoysresources --location westus --enabled-for-deployment true --enabled-for-disk-encryption true --enabled-for-template-deployment true --sku standard --query properties.vaultUri
   ```
   <span data-ttu-id="dfcb8-142">Donde:</span><span class="sxs-lookup"><span data-stu-id="dfcb8-142">Where:</span></span>

   | <span data-ttu-id="dfcb8-143">Parámetro</span><span class="sxs-lookup"><span data-stu-id="dfcb8-143">Parameter</span></span> | <span data-ttu-id="dfcb8-144">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="dfcb8-144">Description</span></span> |
   |---|---|
   | `name` | <span data-ttu-id="dfcb8-145">Especifica un nombre único para el almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="dfcb8-145">Specifies a unique name for your key vault.</span></span> |
   | `location` | <span data-ttu-id="dfcb8-146">Especifica la [región de Azure](https://azure.microsoft.com/regions/) donde se hospedará el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="dfcb8-146">Specifies the [Azure region](https://azure.microsoft.com/regions/) where your resource group will be hosted.</span></span> |
   | `enabled-for-deployment` | <span data-ttu-id="dfcb8-147">Especifica la [opción de implementación del almacén de claves](https://docs.microsoft.com/cli/azure/keyvault).</span><span class="sxs-lookup"><span data-stu-id="dfcb8-147">Specifies the [key vault deployment option](https://docs.microsoft.com/cli/azure/keyvault).</span></span> |
   | `enabled-for-disk-encryption` | <span data-ttu-id="dfcb8-148">Especifica la [opción de cifrado del almacén de claves](https://docs.microsoft.com/cli/azure/keyvault).</span><span class="sxs-lookup"><span data-stu-id="dfcb8-148">Specifies the [key vault encryption option](https://docs.microsoft.com/cli/azure/keyvault).</span></span> |
   | `enabled-for-template-deployment` | <span data-ttu-id="dfcb8-149">Especifica la [opción de cifrado del almacén de claves](https://docs.microsoft.com/cli/azure/keyvault).</span><span class="sxs-lookup"><span data-stu-id="dfcb8-149">Specifies the [key vault encryption option](https://docs.microsoft.com/cli/azure/keyvault).</span></span> |
   | `sku` | <span data-ttu-id="dfcb8-150">Especifica la [opción de SKU del almacén de claves](https://docs.microsoft.com/cli/azure/keyvault).</span><span class="sxs-lookup"><span data-stu-id="dfcb8-150">Specifies the [key vault SKU option](https://docs.microsoft.com/cli/azure/keyvault).</span></span> |
   | `query` | <span data-ttu-id="dfcb8-151">Especifica el valor que se recuperará de la respuesta, que es el URI del almacén de claves que tendrá que completar en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="dfcb8-151">Specifies a value to retrieve from the response, which is the key vault URI that you will need to complete this tutorial.</span></span> |

   <span data-ttu-id="dfcb8-152">La CLI de Azure mostrará el URI del almacén de claves, que usará más adelante; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="dfcb8-152">The Azure CLI will display the URI for key vault, which you will use later; for example:</span></span>  

   ```
   "https://wingtiptoyskeyvault.vault.azure.net"
   ```

4. <span data-ttu-id="dfcb8-153">Establezca la directiva de acceso de la entidad de servicio de Azure que creó anteriormente; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="dfcb8-153">Set the access policy for the Azure service principal you created earlier; for example:</span></span>
   ```azurecli
   az keyvault set-policy --name wingtiptoyskeyvault --secret-permission set get list delete --spn "iiiiiiii-iiii-iiii-iiii-iiiiiiiiiiii"
   ```
   <span data-ttu-id="dfcb8-154">Donde:</span><span class="sxs-lookup"><span data-stu-id="dfcb8-154">Where:</span></span>

   | <span data-ttu-id="dfcb8-155">Parámetro</span><span class="sxs-lookup"><span data-stu-id="dfcb8-155">Parameter</span></span> | <span data-ttu-id="dfcb8-156">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="dfcb8-156">Description</span></span> |
   |---|---|
   | `name` | <span data-ttu-id="dfcb8-157">Especifica el nombre del almacén de claves anterior.</span><span class="sxs-lookup"><span data-stu-id="dfcb8-157">Specifies your key vault name from earlier.</span></span> |
   | `secret-permission` | <span data-ttu-id="dfcb8-158">Especifica las [directivas de seguridad](https://docs.microsoft.com/cli/azure/keyvault) para su almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="dfcb8-158">Specifies the [security policies](https://docs.microsoft.com/cli/azure/keyvault) for your key vault.</span></span> |
   | `spn` | <span data-ttu-id="dfcb8-159">Especifica el GUID del registro de la aplicación anterior.</span><span class="sxs-lookup"><span data-stu-id="dfcb8-159">Specifies the GUID for your application registration from earlier.</span></span> |

   <span data-ttu-id="dfcb8-160">La CLI de Azure mostrará los resultados de la creación de la directiva de seguridad, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="dfcb8-160">The Azure CLI will display the results of your security policy creation; for example:</span></span>  

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

5. <span data-ttu-id="dfcb8-161">Guarde un secreto en su nuevo almacén de claves; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="dfcb8-161">Store a secret in your new key vault; for example:</span></span>
   ```azurecli
   az keyvault secret set --vault-name "wingtiptoyskeyvault" --name "connectionString" --value "jdbc:sqlserver://SERVER.database.windows.net:1433;database=DATABASE;"
   ```
   <span data-ttu-id="dfcb8-162">Donde:</span><span class="sxs-lookup"><span data-stu-id="dfcb8-162">Where:</span></span>

   | <span data-ttu-id="dfcb8-163">Parámetro</span><span class="sxs-lookup"><span data-stu-id="dfcb8-163">Parameter</span></span> | <span data-ttu-id="dfcb8-164">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="dfcb8-164">Description</span></span> |
   |---|---|
   | `vault-name` | <span data-ttu-id="dfcb8-165">Especifica el nombre del almacén de claves anterior.</span><span class="sxs-lookup"><span data-stu-id="dfcb8-165">Specifies your key vault name from earlier.</span></span> |
   | `name` | <span data-ttu-id="dfcb8-166">Especifica el nombre del secreto.</span><span class="sxs-lookup"><span data-stu-id="dfcb8-166">Specifies the name of your secret.</span></span> |
   | `value` | <span data-ttu-id="dfcb8-167">Especifica el valor del secreto.</span><span class="sxs-lookup"><span data-stu-id="dfcb8-167">Specifies the value of your secret.</span></span> |

   <span data-ttu-id="dfcb8-168">La CLI de Azure mostrará los resultados de la creación del secreto; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="dfcb8-168">The Azure CLI will display the results of your secret creation; for example:</span></span>  

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

## <a name="configure-and-compile-your-spring-boot-application"></a><span data-ttu-id="dfcb8-169">Configuración y compilación de la aplicación de Spring Boot</span><span class="sxs-lookup"><span data-stu-id="dfcb8-169">Configure and compile your Spring Boot application</span></span>

1. <span data-ttu-id="dfcb8-170">Extraiga los archivos del archivo del proyecto de Spring Boot que descargó anteriormente en un directorio.</span><span class="sxs-lookup"><span data-stu-id="dfcb8-170">Extract the files from the Spring Boot project archive files that you downloaded earlier into a directory.</span></span>

2. <span data-ttu-id="dfcb8-171">Vaya a la carpeta *src/main/resources* del proyecto y abra el archivo *application.properties* en un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="dfcb8-171">Navigate to the *src/main/resources* folder in your project and open the *application.properties* file in a text editor.</span></span>

3. <span data-ttu-id="dfcb8-172">Agregue los valores del almacén de claves que obtuvo en los pasos realizados anteriormente en este tutorial; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="dfcb8-172">Add the values for your key vault using values from the steps that you completed earlier in this tutorial; for example:</span></span>
   ```yaml
   azure.keyvault.uri=https://wingtiptoyskeyvault.vault.azure.net/
   azure.keyvault.client-id=iiiiiiii-iiii-iiii-iiii-iiiiiiiiiiii
   azure.keyvault.client-key=pppppppp-pppp-pppp-pppp-pppppppppppp
   ```
   <span data-ttu-id="dfcb8-173">Donde:</span><span class="sxs-lookup"><span data-stu-id="dfcb8-173">Where:</span></span>

   |          <span data-ttu-id="dfcb8-174">Parámetro</span><span class="sxs-lookup"><span data-stu-id="dfcb8-174">Parameter</span></span>          |                                 <span data-ttu-id="dfcb8-175">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="dfcb8-175">Description</span></span>                                 |
   |-----------------------------|-----------------------------------------------------------------------------|
   |    `azure.keyvault.uri`     |           <span data-ttu-id="dfcb8-176">Especifica el URI obtenido cuando creó el almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="dfcb8-176">Specifies the URI from when you created your key vault.</span></span>           |
   | `azure.keyvault.client-id`  |  <span data-ttu-id="dfcb8-177">Especifica el GUID de *appId* obtenido cuando creó la entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="dfcb8-177">Specifies the *appId* GUID from when you created your service principal.</span></span>   |
   | `azure.keyvault.client-key` | <span data-ttu-id="dfcb8-178">Especifica el GUID de *password* obtenido cuando creó la entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="dfcb8-178">Specifies the *password* GUID from when you created your service principal.</span></span> |


4. <span data-ttu-id="dfcb8-179">Vaya al archivo de código fuente principal del proyecto; por ejemplo: */src/main/java/com/wingtiptoys/secrets*.</span><span class="sxs-lookup"><span data-stu-id="dfcb8-179">Navigate to the main source code file of your project; for example: */src/main/java/com/wingtiptoys/secrets*.</span></span>

5. <span data-ttu-id="dfcb8-180">Abra el archivo Java principal de la aplicación en un editor de texto (por ejemplo: *SecretsApplication.java*) y agregue las siguientes líneas al archivo:</span><span class="sxs-lookup"><span data-stu-id="dfcb8-180">Open the application's main Java file in a file in a text editor; for example: *SecretsApplication.java*, and add the following lines to the file:</span></span>

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
   <span data-ttu-id="dfcb8-181">Este código de ejemplo recupera la cadena de conexión del almacén de claves y la muestra en la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="dfcb8-181">This code example retrieves the connection string from the key vault and displays it to the command line.</span></span>

6. <span data-ttu-id="dfcb8-182">Guarde y cierre el archivo Java.</span><span class="sxs-lookup"><span data-stu-id="dfcb8-182">Save and close the Java file.</span></span>

## <a name="build-and-test-your-app"></a><span data-ttu-id="dfcb8-183">Compilación y prueba de la aplicación</span><span class="sxs-lookup"><span data-stu-id="dfcb8-183">Build and test your app</span></span>

1. <span data-ttu-id="dfcb8-184">Vaya al directorio donde está el archivo *pom.xml* de su aplicación de Spring Boot:</span><span class="sxs-lookup"><span data-stu-id="dfcb8-184">Navigate to the directory where the *pom.xml* file for your Spring Boot app is located:</span></span>

1. <span data-ttu-id="dfcb8-185">Compile la aplicación de Spring Boot con Maven; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="dfcb8-185">Build your Spring Boot application with Maven; for example:</span></span>

   ```bash
   mvn clean package
   ```

   <span data-ttu-id="dfcb8-186">Maven mostrará los resultados de la compilación.</span><span class="sxs-lookup"><span data-stu-id="dfcb8-186">Maven will display the results of your build.</span></span>

   ![Estado de compilación de la aplicación de Spring Boot][build-application-01]

1. <span data-ttu-id="dfcb8-188">Ejecute la aplicación de Spring Boot con Maven; la aplicación mostrará la cadena de conexión del almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="dfcb8-188">Run your Spring Boot application with Maven; the application will display the connection string from your key vault.</span></span> <span data-ttu-id="dfcb8-189">Por ejemplo: </span><span class="sxs-lookup"><span data-stu-id="dfcb8-189">For example:</span></span>

   ```bash
   mvn spring-boot:run
   ```

   ![Mensaje en tiempo de ejecución de Spring Boot][build-application-02]

## <a name="next-steps"></a><span data-ttu-id="dfcb8-191">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="dfcb8-191">Next steps</span></span>

<span data-ttu-id="dfcb8-192">Para más información sobre el uso de Azure Key Vault, consulte los siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="dfcb8-192">For more information about using Azure Key Vaults, see the following articles:</span></span>

* <span data-ttu-id="dfcb8-193">[Documentación de Key Vault].</span><span class="sxs-lookup"><span data-stu-id="dfcb8-193">[Key Vault Documentation].</span></span>

* <span data-ttu-id="dfcb8-194">[Introducción a Azure Key Vault]</span><span class="sxs-lookup"><span data-stu-id="dfcb8-194">[Get started with Azure Key Vault]</span></span>

<span data-ttu-id="dfcb8-195">Para obtener más información sobre el uso de aplicaciones de Spring Boot en Azure, consulte los siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="dfcb8-195">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="dfcb8-196">Implementación de una aplicación de Spring Boot en Azure App Service</span><span class="sxs-lookup"><span data-stu-id="dfcb8-196">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)

* [<span data-ttu-id="dfcb8-197">Ejecución de una aplicación de Spring Boot en un clúster de Kubernetes en Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="dfcb8-197">Running a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="dfcb8-198">Para más información sobre el uso de Azure con Java, consulte [Azure para desarrolladores de Java] y [Herramientas de Java para Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="dfcb8-198">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

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
