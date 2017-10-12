---
title: Bibliotecas de Azure Key Vault para Java
description: "Introducción a las bibliotecas de Azure Key Vault para Java"
keywords: "Azure, Java, SDK, API, keyvault, proteger, claves, secretos, almacén"
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/20/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: keyvault
ms.openlocfilehash: 51ac51f5436397a0c9f1a4572dcf79a40f10b538
ms.sourcegitcommit: 634ab7578c73a219f8f3a2a6d43999d9d372cb43
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/09/2017
---
# <a name="azure-key-vault-libraries-for-java"></a>Bibliotecas de Azure Key Vault para Java

## <a name="overview"></a>Información general

[Azure Key Vault](/azure/key-vault/) protege y administra claves y secretos criptográficos usados por aplicaciones y servicios en la nube.

Para empezar a trabajar con Azure Key Vault, consulte [Introducción a Azure Key Vault](/azure/key-vault/key-vault-get-started).

## <a name="client-library"></a>Biblioteca de cliente

Cree, actualice y elimine claves y secretos en Azure Key Vault con las bibliotecas de cliente.

[Agregue una dependencia](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) al archivo `pom.xml` de Maven para utilizar la biblioteca de cliente en el proyecto.  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-keyvault</artifactId>
    <version>1.0.0</version>
</dependency>
```   

## <a name="example"></a>Ejemplo

Recupere una [clave de web JSON](https://tools.ietf.org/html/draft-ietf-jose-json-web-key-18) desde un almacén de claves.

```java
KeyVaultClient kvc = new KeyVaultClient(credentials);
KeyBundle returnedKeyBundle = getKey(vaultUrl, keyName);
JsonWebKey jsonKey = returnedKeyBundle.key();
```

> [!div class="nextstepaction"]
> [Explorar las API de cliente](/java/api/overview/azure/keyvault/clientlibrary)


## <a name="management-api"></a>API de administración

Uso de las bibliotecas de administración de Azure Key Vault para crear almacenes de claves, autorizar aplicaciones y administrar permisos. 

[Agregue una dependencia](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) al archivo `pom.xml` de Maven para utilizar la API de administración en el proyecto.  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-keyvault</artifactId>
    <version>1.3.0</version>
</dependency>
```

## <a name="example"></a>Ejemplo

Autorice a una aplicación que se ejecuta con una [entidad de servicio](/azure/azure-resource-manager/resource-group-create-service-principal-portal) `clientId` a enumerar y recuperar los secretos de un almacén de claves. 

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
> [Explorar las API de administración](/java/api/overview/azure/keyvault/managementapi)


## <a name="samples"></a>Muestras

[Administración de almacenes de claves][1]   

[1]: https://github.com/Azure-Samples/key-vault-java-manage-key-vaults

Ver más [código de Java de ejemplo para Azure Key Vault](https://azure.microsoft.com/resources/samples/?platform=java&term=key+vault) que puede usar en sus aplicaciones.
