---
title: Autenticación con las bibliotecas de administración de Azure para Java
description: Autenticación con una entidad de servicio en las bibliotecas de administración de Azure para Java
keywords: Azure, Java, SDK, API, Maven, Gradle, autenticación, active directory, entidad de servicio
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 04/16/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: multiple
ms.assetid: 10f457e3-578b-4655-8cd1-51339226ee7d
ms.openlocfilehash: 1d556955fcc5b73f1ba099a0b846b571ba64ccff
ms.sourcegitcommit: 107c3c5ed8c6991c751f95bcaf3757220940df9e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="authenticate-with-the-azure-libraries-for-java"></a>Autenticación con las bibliotecas de Azure para Java 

## <a name="connect-to-services-with-connection-strings"></a>Conexión a los servicios con cadenas de conexión

La mayoría de las bibliotecas de servicio de Azure utilizan una cadena de conexión o una clave segura para la autenticación. Por ejemplo, SQL Database incluye información de nombre de usuario y contraseña en la cadena de conexión JDBC:

```java
String url = "jdbc:sqlserver://myazuredb.database.windows.net:1433;" + 
        "database=testjavadb;" + 
        "user=myazdbuser;" +
        "password=myazdbpass;" +
        "encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;";
        Connection conn = DriverManager.getConnection(url);
```

Azure Storage usa una clave de almacenamiento para autorizar a la aplicación:

```java
final String storageConnection = "DefaultEndpointsProtocol=https;"
        + "AccountName=" + storageName 
        + ";AccountKey=" + storageKey
        + ";EndpointSuffix=core.windows.net";
```

Las cadenas de conexión de servicio se usan para autenticarse en otros servicios de Azure como [Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/sql-api-java-application#UseService), [Redis Cache](https://docs.microsoft.com/azure/redis-cache/cache-java-get-started) y [Service Bus](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-java-how-to-use-queues). Puede obtener las cadenas de conexión mediante Azure Portal o la CLI.  También puede usar las bibliotecas de administración de Azure para Java para consultar recursos para generar cadenas de conexión en el código. 

Por ejemplo, este código usa las bibliotecas de administración para crear una cadena de conexión de la cuenta de almacenamiento:

```java
// create a new storage account
StorageAccount storage = azure.storageAccounts().getByResourceGroup("myResourceGroup","myStorageAccount");

// create a storage container to hold the file
List<StorageAccountKey> keys = storage.getKeys();
final String storageConnection = "DefaultEndpointsProtocol=https;"
        + "AccountName=" + storage.name()
        + ";AccountKey=" + keys.get(0).value()
        + ";EndpointSuffix=core.windows.net";
```

Otras bibliotecas requieren que la aplicación se ejecute con una [entidad de servicio](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-objects) que autoriza la ejecución de la aplicación con las credenciales otorgadas. Esta configuración es similar a los pasos de la autenticación basada en objetos para la biblioteca de administración que se enumeran a continuación.

<a name="mgmt-auth"></a>

##  <a name="authenticate-with-the-azure-management-libraries-for-java"></a>Autenticación con las bibliotecas de administración de Azure para Java

Hay dos opciones para autenticar la aplicación con Azure cuando se usan las bibliotecas de administración para Java para crear y administrar recursos.

### <a name="authenticate-with-an-applicationtokencredentials-object"></a>Autenticación con un objeto ApplicationTokenCredentials

Cree una instancia de `ApplicationTokenCredentials` para proporcionar las credenciales de la entidad de servicio al objeto de nivel superior de `Azure` desde el código.

```java
import com.microsoft.azure.credentials.ApplicationTokenCredentials;
import com.microsoft.azure.AzureEnvironment;

// ...

ApplicationTokenCredentials credentials = new ApplicationTokenCredentials(client, 
        tenant,
        key, 
        AzureEnvironment.AZURE);
        
Azure azure = Azure
        .configure()
        .withLogLevel(LogLevel.NONE)
        .authenticate(credentials)
        .withDefaultSubscription();
```

Los valores de `client`, `tenant` y `key` son los mismos valores de la entidad de servicio que se utilizan en la [autenticación basada en archivo](#mgmt-file). El valor de `AzureEnvironment.AZURE` crea credenciales en la nube pública de Azure. Cámbielo por un valor diferente si necesita obtener acceso a otra nube (por ejemplo, `AzureEnvironment.AZURE_GERMANY`).  

 Lee los valores de la entidad de servicio desde las variables de entorno o desde un almacén de administración de secretos como [Key Vault](/azure/key-vault/key-vault-whatis). Evite establecer estos valores como cadenas de texto no cifrado en el código para prevenir la exposición accidental de las credenciales en el historial de control de versiones.   

<a name="mgmt-file"></a>

### <a name="file-based-authentication-preview"></a>Autenticación basada en archivo (versión preliminar)

La manera más sencilla de autenticar consiste en crear un archivo de propiedades que contenga las credenciales de una [entidad de servicio de Azure](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-objects) con el formato siguiente:

```text
# sample management library properties file
subscription=########-####-####-####-############
client=########-####-####-####-############
key=XXXXXXXXXXXXXXXX
tenant=########-####-####-####-############
managementURI=https\://management.core.windows.net/
baseURL=https\://management.azure.com/
authURL=https\://login.windows.net/
graphURL=https\://graph.windows.net/
```

- subscription: use el valor de *id* que se muestra con el comando `az account show` en la CLI de Azure 2.0.
- client: use el valor de *appId* procedente de la salida de una entidad de servicio creada para ejecutar la aplicación. Si no tiene una entidad de servicio para la aplicación, puede [crear una con la CLI de Azure 2.0](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli).
- key: use el valor de *password* (contraseña) procedente de la salida en la CLI de la creación de la entidad de servicio 
- tenant: use el valor de *tenant* procedente de la salida en la CLI de la creación de la entidad de servicio

Guarde este archivo en una ubicación segura en el sistema en la que el código pueda leerlo. Establezca una variable de entorno con la ruta de acceso completa al archivo en el shell:

```bash
export AZURE_AUTH_LOCATION=/Users/raisa/azureauth.properties
```

Cree el objeto `Azure` de punto de entrada para empezar a trabajar con las bibliotecas. Lea la ubicación del archivo de propiedades desde la variable de entorno.

```java
// pull in the location of the authenticaiton properties file from the environment 
final File credFile = new File(System.getenv("AZURE_AUTH_LOCATION"));

Azure azure = Azure
        .configure()
        .withLogLevel(LogLevel.NONE)
        .authenticate(credFile)
        .withDefaultSubscription();
```



