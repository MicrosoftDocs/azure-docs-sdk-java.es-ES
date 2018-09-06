---
title: Bibliotecas de Azure Key Vault para Java
description: Introducción a las bibliotecas de Azure Key Vault para Java
keywords: Azure, Java, SDK, API, keyvault, proteger, claves, secretos, almacén
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/20/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: keyvault
ms.openlocfilehash: b3433d2da2054741015b9fa669753a8edb48cdf3
ms.sourcegitcommit: 280d13b43cef94177d95e03879a5919da234a23c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/31/2018
ms.locfileid: "43324302"
---
# <a name="azure-key-vault-libraries-for-java"></a><span data-ttu-id="833dd-104">Bibliotecas de Azure Key Vault para Java</span><span class="sxs-lookup"><span data-stu-id="833dd-104">Azure Key Vault libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="833dd-105">Información general</span><span class="sxs-lookup"><span data-stu-id="833dd-105">Overview</span></span>

<span data-ttu-id="833dd-106">[Azure Key Vault](/azure/key-vault/) protege y administra claves y secretos criptográficos usados por aplicaciones y servicios en la nube.</span><span class="sxs-lookup"><span data-stu-id="833dd-106">Safeguard and manage cryptographic keys and secrets used by cloud applications and services with [Azure Key Vault](/azure/key-vault/).</span></span>

<span data-ttu-id="833dd-107">Para empezar a trabajar con Azure Key Vault, consulte [Introducción a Azure Key Vault](/azure/key-vault/key-vault-get-started).</span><span class="sxs-lookup"><span data-stu-id="833dd-107">To get started with Azure Key Vault, see [Get started with Azure Key Vault](/azure/key-vault/key-vault-get-started).</span></span>

## <a name="client-library"></a><span data-ttu-id="833dd-108">Biblioteca de cliente</span><span class="sxs-lookup"><span data-stu-id="833dd-108">Client library</span></span>

<span data-ttu-id="833dd-109">Cree, actualice y elimine claves y secretos en Azure Key Vault con las bibliotecas de cliente.</span><span class="sxs-lookup"><span data-stu-id="833dd-109">Create, update, and delete keys and secrets in Azure Key Vault with the client libraries.</span></span>

<span data-ttu-id="833dd-110">[Agregue una dependencia](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) al archivo `pom.xml` de Maven para utilizar la biblioteca de cliente en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="833dd-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-keyvault</artifactId>
    <version>1.1.0</version>
</dependency>
```   

## <a name="example"></a><span data-ttu-id="833dd-111">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="833dd-111">Example</span></span>

<span data-ttu-id="833dd-112">Recupere una [clave de web JSON](https://tools.ietf.org/html/draft-ietf-jose-json-web-key-18) desde un almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="833dd-112">Retrieve a [JSON web key](https://tools.ietf.org/html/draft-ietf-jose-json-web-key-18) from a Key Vault.</span></span>

```java
KeyVaultClient kvc = new KeyVaultClient(credentials);
KeyBundle returnedKeyBundle = kvc.getKey(vaultUrl, keyName);
JsonWebKey jsonKey = returnedKeyBundle.key();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="833dd-113">Explorar las API de cliente</span><span class="sxs-lookup"><span data-stu-id="833dd-113">Explore the Client APIs</span></span>](/java/api/overview/azure/keyvault/client)


## <a name="management-api"></a><span data-ttu-id="833dd-114">API de administración</span><span class="sxs-lookup"><span data-stu-id="833dd-114">Management API</span></span>

<span data-ttu-id="833dd-115">Uso de las bibliotecas de administración de Azure Key Vault para crear almacenes de claves, autorizar aplicaciones y administrar permisos.</span><span class="sxs-lookup"><span data-stu-id="833dd-115">Use the Azure Key Vault management libraries to create key vaults, authorize applications, and manage permissions.</span></span> 

<span data-ttu-id="833dd-116">[Agregue una dependencia](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) al archivo `pom.xml` de Maven para utilizar la API de administración en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="833dd-116">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-keyvault</artifactId>
    <version>1.15.0</version>
</dependency>
```

## <a name="example"></a><span data-ttu-id="833dd-117">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="833dd-117">Example</span></span>

<span data-ttu-id="833dd-118">Autorice a una aplicación que se ejecuta con una [entidad de servicio](/azure/azure-resource-manager/resource-group-create-service-principal-portal) `clientId` a enumerar y recuperar los secretos de un almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="833dd-118">Authorize and application running with [service principal](/azure/azure-resource-manager/resource-group-create-service-principal-portal) `clientId` to list and retrieve secrets from a key vault.</span></span> 

```java
vault1 = vault1.update()
            .defineAccessPolicy()
                .forServicePrincipal(clientId)
                .allowKeyAllPermissions()
                .allowSecretPermissions(SecretPermissions.GET)
                .allowSecretPermissions(SecretPermissions.LIST)
                .attach()
            .apply();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="833dd-119">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="833dd-119">Explore the Management APIs</span></span>](/java/api/overview/azure/keyvault/management)


## <a name="samples"></a><span data-ttu-id="833dd-120">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="833dd-120">Samples</span></span>

<span data-ttu-id="833dd-121">Ver más [código de Java de ejemplo para Azure Key Vault](https://azure.microsoft.com/resources/samples/?platform=java&term=key+vault) que puede usar en sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="833dd-121">Explore more [sample Java code for Azure Key Vault](https://azure.microsoft.com/resources/samples/?platform=java&term=key+vault) you can use in your apps.</span></span>
