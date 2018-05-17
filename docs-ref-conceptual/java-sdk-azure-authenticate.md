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
# <a name="authenticate-with-the-azure-libraries-for-java"></a><span data-ttu-id="95288-104">Autenticación con las bibliotecas de Azure para Java</span><span class="sxs-lookup"><span data-stu-id="95288-104">Authenticate with the Azure libraries for Java</span></span> 

## <a name="connect-to-services-with-connection-strings"></a><span data-ttu-id="95288-105">Conexión a los servicios con cadenas de conexión</span><span class="sxs-lookup"><span data-stu-id="95288-105">Connect to services with connection strings</span></span>

<span data-ttu-id="95288-106">La mayoría de las bibliotecas de servicio de Azure utilizan una cadena de conexión o una clave segura para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="95288-106">Most Azure service libraries use a connection string or secure key for authentication.</span></span> <span data-ttu-id="95288-107">Por ejemplo, SQL Database incluye información de nombre de usuario y contraseña en la cadena de conexión JDBC:</span><span class="sxs-lookup"><span data-stu-id="95288-107">For example, SQL Database includes username and password information in the JDBC connection string:</span></span>

```java
String url = "jdbc:sqlserver://myazuredb.database.windows.net:1433;" + 
        "database=testjavadb;" + 
        "user=myazdbuser;" +
        "password=myazdbpass;" +
        "encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;";
        Connection conn = DriverManager.getConnection(url);
```

<span data-ttu-id="95288-108">Azure Storage usa una clave de almacenamiento para autorizar a la aplicación:</span><span class="sxs-lookup"><span data-stu-id="95288-108">Azure Storage uses a storage key to authorize the application:</span></span>

```java
final String storageConnection = "DefaultEndpointsProtocol=https;"
        + "AccountName=" + storageName 
        + ";AccountKey=" + storageKey
        + ";EndpointSuffix=core.windows.net";
```

<span data-ttu-id="95288-109">Las cadenas de conexión de servicio se usan para autenticarse en otros servicios de Azure como [Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/sql-api-java-application#UseService), [Redis Cache](https://docs.microsoft.com/azure/redis-cache/cache-java-get-started) y [Service Bus](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-java-how-to-use-queues).</span><span class="sxs-lookup"><span data-stu-id="95288-109">Service connection strings are used to authenticate to other Azure services like [Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/sql-api-java-application#UseService), [Redis Cache](https://docs.microsoft.com/azure/redis-cache/cache-java-get-started), and [Service Bus](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-java-how-to-use-queues).</span></span> <span data-ttu-id="95288-110">Puede obtener las cadenas de conexión mediante Azure Portal o la CLI.</span><span class="sxs-lookup"><span data-stu-id="95288-110">You can get the connection strings using the Azure portal or the CLI.</span></span>  <span data-ttu-id="95288-111">También puede usar las bibliotecas de administración de Azure para Java para consultar recursos para generar cadenas de conexión en el código.</span><span class="sxs-lookup"><span data-stu-id="95288-111">You can also use the Azure management libraries for Java to query resources to build connection strings in your code.</span></span> 

<span data-ttu-id="95288-112">Por ejemplo, este código usa las bibliotecas de administración para crear una cadena de conexión de la cuenta de almacenamiento:</span><span class="sxs-lookup"><span data-stu-id="95288-112">For example, this code uses the management libraries to create a storage account connection string:</span></span>

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

<span data-ttu-id="95288-113">Otras bibliotecas requieren que la aplicación se ejecute con una [entidad de servicio](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-objects) que autoriza la ejecución de la aplicación con las credenciales otorgadas.</span><span class="sxs-lookup"><span data-stu-id="95288-113">Other libraries require your application to run with a [service prinicpal](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-objects) authorizing the application to run with granted credentials.</span></span> <span data-ttu-id="95288-114">Esta configuración es similar a los pasos de la autenticación basada en objetos para la biblioteca de administración que se enumeran a continuación.</span><span class="sxs-lookup"><span data-stu-id="95288-114">This configuration is similar to the object-based authentication steps for the management library listed below.</span></span>

<a name="mgmt-auth"></a>

##  <a name="authenticate-with-the-azure-management-libraries-for-java"></a><span data-ttu-id="95288-115">Autenticación con las bibliotecas de administración de Azure para Java</span><span class="sxs-lookup"><span data-stu-id="95288-115">Authenticate with the Azure management libraries for Java</span></span>

<span data-ttu-id="95288-116">Hay dos opciones para autenticar la aplicación con Azure cuando se usan las bibliotecas de administración para Java para crear y administrar recursos.</span><span class="sxs-lookup"><span data-stu-id="95288-116">Two options are available to authenticate your application with Azure when using the Java management libraries to create and manage resources.</span></span>

### <a name="authenticate-with-an-applicationtokencredentials-object"></a><span data-ttu-id="95288-117">Autenticación con un objeto ApplicationTokenCredentials</span><span class="sxs-lookup"><span data-stu-id="95288-117">Authenticate with an ApplicationTokenCredentials object</span></span>

<span data-ttu-id="95288-118">Cree una instancia de `ApplicationTokenCredentials` para proporcionar las credenciales de la entidad de servicio al objeto de nivel superior de `Azure` desde el código.</span><span class="sxs-lookup"><span data-stu-id="95288-118">Create an instance of `ApplicationTokenCredentials` to supply the service principal credentials to the top-level `Azure` object from inside your code.</span></span>

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

<span data-ttu-id="95288-119">Los valores de `client`, `tenant` y `key` son los mismos valores de la entidad de servicio que se utilizan en la [autenticación basada en archivo](#mgmt-file).</span><span class="sxs-lookup"><span data-stu-id="95288-119">The `client`, `tenant` and `key` are the same service principal values used with [file-based authentication](#mgmt-file).</span></span> <span data-ttu-id="95288-120">El valor de `AzureEnvironment.AZURE` crea credenciales en la nube pública de Azure.</span><span class="sxs-lookup"><span data-stu-id="95288-120">The `AzureEnvironment.AZURE` value creates credentials against the Azure public cloud.</span></span> <span data-ttu-id="95288-121">Cámbielo por un valor diferente si necesita obtener acceso a otra nube (por ejemplo, `AzureEnvironment.AZURE_GERMANY`).</span><span class="sxs-lookup"><span data-stu-id="95288-121">Change this to a different value if you need to access another cloud (for example, `AzureEnvironment.AZURE_GERMANY`).</span></span>  

 <span data-ttu-id="95288-122">Lee los valores de la entidad de servicio desde las variables de entorno o desde un almacén de administración de secretos como [Key Vault](/azure/key-vault/key-vault-whatis).</span><span class="sxs-lookup"><span data-stu-id="95288-122">Read the service principal values from environment variables or a secret management store like [Key Vault](/azure/key-vault/key-vault-whatis).</span></span> <span data-ttu-id="95288-123">Evite establecer estos valores como cadenas de texto no cifrado en el código para prevenir la exposición accidental de las credenciales en el historial de control de versiones.</span><span class="sxs-lookup"><span data-stu-id="95288-123">Avoid setting these values as cleartext strings in your code to prevent accidentally exposing credentials in your version control history.</span></span>   

<a name="mgmt-file"></a>

### <a name="file-based-authentication-preview"></a><span data-ttu-id="95288-124">Autenticación basada en archivo (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="95288-124">File based authentication (Preview)</span></span>

<span data-ttu-id="95288-125">La manera más sencilla de autenticar consiste en crear un archivo de propiedades que contenga las credenciales de una [entidad de servicio de Azure](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-objects) con el formato siguiente:</span><span class="sxs-lookup"><span data-stu-id="95288-125">The simplest way to authenticate is to create a properties file that contains credentials for an [Azure service principal](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-objects) using the following format:</span></span>

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

- <span data-ttu-id="95288-126">subscription: use el valor de *id* que se muestra con el comando `az account show` en la CLI de Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="95288-126">subscription: use the *id* value from `az account show` in the Azure CLI 2.0.</span></span>
- <span data-ttu-id="95288-127">client: use el valor de *appId* procedente de la salida de una entidad de servicio creada para ejecutar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="95288-127">client: use the *appId* value from the output taken from a service principal created to run the application.</span></span> <span data-ttu-id="95288-128">Si no tiene una entidad de servicio para la aplicación, puede [crear una con la CLI de Azure 2.0](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="95288-128">If you don't have a service principal for your app, [create one with the Azure CLI 2.0](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli).</span></span>
- <span data-ttu-id="95288-129">key: use el valor de *password* (contraseña) procedente de la salida en la CLI de la creación de la entidad de servicio</span><span class="sxs-lookup"><span data-stu-id="95288-129">key: use the *password* value from the service principal create CLI output</span></span> 
- <span data-ttu-id="95288-130">tenant: use el valor de *tenant* procedente de la salida en la CLI de la creación de la entidad de servicio</span><span class="sxs-lookup"><span data-stu-id="95288-130">tenant: use the *tenant* value from the service principal create CLI output</span></span>

<span data-ttu-id="95288-131">Guarde este archivo en una ubicación segura en el sistema en la que el código pueda leerlo.</span><span class="sxs-lookup"><span data-stu-id="95288-131">Save this file in a secure location on your system where your code can read it.</span></span> <span data-ttu-id="95288-132">Establezca una variable de entorno con la ruta de acceso completa al archivo en el shell:</span><span class="sxs-lookup"><span data-stu-id="95288-132">Set an environment variable with the full path to the file in your shell:</span></span>

```bash
export AZURE_AUTH_LOCATION=/Users/raisa/azureauth.properties
```

<span data-ttu-id="95288-133">Cree el objeto `Azure` de punto de entrada para empezar a trabajar con las bibliotecas.</span><span class="sxs-lookup"><span data-stu-id="95288-133">Create the entry point `Azure` object to start working with the libraries.</span></span> <span data-ttu-id="95288-134">Lea la ubicación del archivo de propiedades desde la variable de entorno.</span><span class="sxs-lookup"><span data-stu-id="95288-134">Read the location of the properties file through the environment variable.</span></span>

```java
// pull in the location of the authenticaiton properties file from the environment 
final File credFile = new File(System.getenv("AZURE_AUTH_LOCATION"));

Azure azure = Azure
        .configure()
        .withLogLevel(LogLevel.NONE)
        .authenticate(credFile)
        .withDefaultSubscription();
```



