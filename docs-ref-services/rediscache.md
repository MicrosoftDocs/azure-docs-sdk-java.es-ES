---
title: Bibliotecas de Redis Cache para Java
description: Documentación de referencia del cliente Java y las bibliotecas de administración de Redis Cache para Java
keywords: Azure, Java, SDK, API, caché, redis, caché web, clave y valor, en memoria
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/11/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: redis-cache
ms.openlocfilehash: dd03825d9ae7cba32087f92262d5ef213cf3af0b
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/09/2018
ms.locfileid: "48892776"
---
# <a name="redis-cache-libraries-for-java"></a><span data-ttu-id="e613f-104">Bibliotecas de Redis Cache para Java</span><span class="sxs-lookup"><span data-stu-id="e613f-104">Redis Cache libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="e613f-105">Información general</span><span class="sxs-lookup"><span data-stu-id="e613f-105">Overview</span></span>

<span data-ttu-id="e613f-106">Azure Redis Cache es un almacén de pares de clave y valor seguro y distribuido basado en el popular código abierto [Redis](https://redis.io/) Cache.</span><span class="sxs-lookup"><span data-stu-id="e613f-106">Azure Redis Cache is a secure, distributed key-value store based on the popular open source [Redis](https://redis.io/) cache.</span></span> 

<span data-ttu-id="e613f-107">Para empezar a usar Azure Redis Cache, consulte [Uso de Azure Redis Cache con Java](/azure/redis-cache/cache-java-get-started).</span><span class="sxs-lookup"><span data-stu-id="e613f-107">To get started with Azure Redis Cache, see [How to use Azure Redis Cache with Java](/azure/redis-cache/cache-java-get-started).</span></span>

## <a name="client-library"></a><span data-ttu-id="e613f-108">Biblioteca de cliente</span><span class="sxs-lookup"><span data-stu-id="e613f-108">Client library</span></span>

<span data-ttu-id="e613f-109">Conecte con Azure Redis Cache y guarde y recupere los valores de la memoria caché mediante el cliente de código abierto [Jedis](https://github.com/xetorthio/jedis).</span><span class="sxs-lookup"><span data-stu-id="e613f-109">Connect to Azure Redis Cache and store and retrieve values from the cache using the open-source [Jedis](https://github.com/xetorthio/jedis) client.</span></span>  

<span data-ttu-id="e613f-110">[Agregue una dependencia](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) al archivo `pom.xml` de Maven para utilizar la biblioteca de cliente en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="e613f-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>   

```XML
<dependency>
    <groupId>redis.clients</groupId>
    <artifactId>jedis</artifactId>
    <version>2.9.0</version>
    <type>jar</type>
</dependency>
```

## <a name="example"></a><span data-ttu-id="e613f-111">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="e613f-111">Example</span></span>

<span data-ttu-id="e613f-112">Conecte con Azure Redis e inserte una cadena en la memoria caché.</span><span class="sxs-lookup"><span data-stu-id="e613f-112">Connect to Azure Redis and insert a string into the cache.</span></span>

```java
JedisShardInfo shardInfo = new JedisShardInfo("<name>.redis.cache.windows.net", 6380, useSsl);
    shardInfo.setPassword("<key>"); /* Use your access key. */
    Jedis jedis = new Jedis(shardInfo);
    jedis.set("foo", "bar");
```

## <a name="management-api"></a><span data-ttu-id="e613f-113">API de administración</span><span class="sxs-lookup"><span data-stu-id="e613f-113">Management API</span></span>

<span data-ttu-id="e613f-114">Cree y escale de Azure Redis y administre claves de acceso con la API de administración.</span><span class="sxs-lookup"><span data-stu-id="e613f-114">Create and scale Azure Redis resources and manage access keys to with the management API.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-redis</artifactId>
    <version>1.3.0</version>
</dependency>
```

## <a name="example"></a><span data-ttu-id="e613f-115">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="e613f-115">Example</span></span>

<span data-ttu-id="e613f-116">Cree una nueva instancia de Azure Redis Cache en el [nivel estándar de dos nodos](https://azure.microsoft.com/services/cache/).</span><span class="sxs-lookup"><span data-stu-id="e613f-116">Create a new Azure Redis Cache in the [two-node standard tier](https://azure.microsoft.com/services/cache/).</span></span> 

```java
RedisCache cache = azure.redisCaches().define(redisCacheName1)
    .withRegion(Region.US_CENTRAL)
    .withNewResourceGroup(rgName)
    .withStandardSku();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="e613f-117">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="e613f-117">Explore the Management APIs</span></span>](/java/api/overview/azure/rediscache/management)

## <a name="samples"></a><span data-ttu-id="e613f-118">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="e613f-118">Samples</span></span>

[<span data-ttu-id="e613f-119">Administración de Azure Redis Cache</span><span class="sxs-lookup"><span data-stu-id="e613f-119">Manage Azure Redis Cache</span></span>](https://github.com/Azure-Samples/redis-java-manage-cache)   

<span data-ttu-id="e613f-120">Ver más [código de Java de ejemplo para Azure Redis Cache](https://azure.microsoft.com/resources/samples/?platform=java&term=redis) que puede usar en sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="e613f-120">Explore more [sample Java code for Azure Redis Cache](https://azure.microsoft.com/resources/samples/?platform=java&term=redis) you can use in your apps.</span></span>
