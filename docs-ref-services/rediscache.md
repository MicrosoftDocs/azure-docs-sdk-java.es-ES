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
ms.openlocfilehash: 6f19587d3caeaccd2805007f60bd4ba96fee0bf7
ms.sourcegitcommit: 115f4c8ad07a11f17d79e9d945d63917836b11c8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "61593310"
---
# <a name="redis-cache-libraries-for-java"></a>Bibliotecas de Redis Cache para Java

## <a name="overview"></a>Información general

Azure Redis Cache es un almacén de pares de clave y valor seguro y distribuido basado en el popular código abierto [Redis](https://redis.io/) Cache. 

Para empezar a usar Azure Redis Cache, consulte [Uso de Azure Redis Cache con Java](/azure/redis-cache/cache-java-get-started).

## <a name="client-library"></a>Biblioteca de cliente

Conecte con Azure Redis Cache y guarde y recupere los valores de la memoria caché mediante el cliente de código abierto [Jedis](https://github.com/xetorthio/jedis).  

[Agregue una dependencia](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) al archivo `pom.xml` de Maven para utilizar la biblioteca de cliente en el proyecto.   

```XML
<dependency>
    <groupId>redis.clients</groupId>
    <artifactId>jedis</artifactId>
    <version>2.9.0</version>
    <type>jar</type>
</dependency>
```

## <a name="example"></a>Ejemplo

Conecte con Azure Redis e inserte una cadena en la memoria caché.

```java
JedisShardInfo shardInfo = new JedisShardInfo("<name>.redis.cache.windows.net", 6380, useSsl);
    shardInfo.setPassword("<key>"); /* Use your access key. */
    Jedis jedis = new Jedis(shardInfo);
    jedis.set("foo", "bar");
```

## <a name="management-api"></a>API de administración

Cree y escale de Azure Redis y administre claves de acceso con la API de administración.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-redis</artifactId>
    <version>1.3.0</version>
</dependency>
```

## <a name="example"></a>Ejemplo

Cree una nueva instancia de Azure Redis Cache en el [nivel estándar de dos nodos](https://azure.microsoft.com/services/cache/). 

```java
RedisCache cache = azure.redisCaches().define(redisCacheName1)
    .withRegion(Region.US_CENTRAL)
    .withNewResourceGroup(rgName)
    .withStandardSku();
```

> [!div class="nextstepaction"]
> [Explorar las API de administración](/java/api/overview/azure/rediscache/management)

## <a name="samples"></a>Ejemplos

[Administración de Azure Redis Cache](https://github.com/Azure-Samples/redis-java-manage-cache)   

Ver más [código de Java de ejemplo para Azure Redis Cache](https://azure.microsoft.com/resources/samples/?platform=java&term=redis) que puede usar en sus aplicaciones.
