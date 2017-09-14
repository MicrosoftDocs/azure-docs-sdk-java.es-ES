---
title: "Notas de la versión de las bibliotecas de administración de Azure para Java | Microsoft Docs"
description: "Vea las novedades y los cambios importantes en las bibliotecas de administración de Azure para Java"
keywords: Azure, Java, API, referencia, notas, actualizaciones, en desuso
author: routlaw
manager: douge
ms.assetid: 1f128cf9-f747-4344-84e1-f9964709deb8
ms.service: Azure
ms.devlang: java
ms.topic: reference
ms.technology: Azure
ms.date: 3/06/2016
ms.openlocfilehash: c0d5c4b3702d3bee4e93de51cec36e72aeaf598f
ms.sourcegitcommit: ae39830d5a54fedceac78d8df1718e77741e03fa
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/09/2017
---
# <a name="release-notes"></a><span data-ttu-id="414e4-104">Notas de la versión</span><span class="sxs-lookup"><span data-stu-id="414e4-104">Release Notes</span></span> 

## <a name="june-30-2017---110"></a><span data-ttu-id="414e4-105">30 de junio de 2017-1.1.0</span><span class="sxs-lookup"><span data-stu-id="414e4-105">June 30, 2017 - 1.1.0</span></span> 

<span data-ttu-id="414e4-106">V1.1 es compatible con la versión 1.0 de las API pensadas para uso público que alcanzaron la fase de disponibilidad general (estable) en la versión 1.0.</span><span class="sxs-lookup"><span data-stu-id="414e4-106">V1.1 is backwards compatible with V1.0 in the APIs intended for public use that reached the general availability (stable) stage in V1.0.</span></span>

<span data-ttu-id="414e4-107">Se incorporaron algunos cambios importantes en las API marcadas con la anotación @Beta en la versión V.0</span><span class="sxs-lookup"><span data-stu-id="414e4-107">Some breaking changes were introduced in APIs marked with the @Beta annotation in V.0</span></span>

<span data-ttu-id="414e4-108">Si va a migrar código a la versión 1.1.0, puede usar [estas notas](https://github.com/Azure/azure-sdk-for-java/blob/master/notes/prepare-for-1.1.0.md) para preparar el código de 1.0.0 para 1.1.0.</span><span class="sxs-lookup"><span data-stu-id="414e4-108">If you are migrating your code to 1.1.0, you can use [these notes](https://github.com/Azure/azure-sdk-for-java/blob/master/notes/prepare-for-1.1.0.md) for preparing your code for 1.1.0 from 1.0.0.</span></span>

### <a name="generally-availabile-in-v11"></a><span data-ttu-id="414e4-109">Disponibilidad general en la versión V1.1</span><span class="sxs-lookup"><span data-stu-id="414e4-109">Generally availabile in V1.1</span></span>

<span data-ttu-id="414e4-110">Algunas de las API que estaban todavía en la versión V1.0 beta ahora están disponibles de forma general en la versión V1.1, en concreto:</span><span class="sxs-lookup"><span data-stu-id="414e4-110">Some of the APIs that were still in Beta in V1.0 are now GA in V1.1, in particular:</span></span>

- <span data-ttu-id="414e4-111">métodos asincrónicos</span><span class="sxs-lookup"><span data-stu-id="414e4-111">async methods</span></span>
- <span data-ttu-id="414e4-112">todos los métodos de la red CDN que anteriormente se encontraban en la versión beta</span><span class="sxs-lookup"><span data-stu-id="414e4-112">all methods in CDN that were previously in Beta</span></span>
- <span data-ttu-id="414e4-113">todos los métodos y las interfaces de Application Gateway que anteriormente se encontraban en la versión beta</span><span class="sxs-lookup"><span data-stu-id="414e4-113">all methods and interfaces in Application Gateways that were previously in Beta</span></span>

 <span data-ttu-id="414e4-114">Algunas partes de la biblioteca aún están en versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="414e4-114">Some parts of the library are still in Preview.</span></span> <span data-ttu-id="414e4-115">Consulte la tabla siguiente sobre el estado actual de las bibliotecas:</span><span class="sxs-lookup"><span data-stu-id="414e4-115">Refer to the table below for the current state of the libraries:</span></span>

<span data-ttu-id="414e4-116">Servicio o característica</span><span class="sxs-lookup"><span data-stu-id="414e4-116">Service or feature</span></span> | <span data-ttu-id="414e4-117">Disponible de forma general</span><span class="sxs-lookup"><span data-stu-id="414e4-117">Available as GA</span></span> | <span data-ttu-id="414e4-118">Disponible como versión preliminar</span><span class="sxs-lookup"><span data-stu-id="414e4-118">Available as Preview</span></span>  | <span data-ttu-id="414e4-119">Próximamente</span><span class="sxs-lookup"><span data-stu-id="414e4-119">Coming soon</span></span> |
---------|---------|---------|---------|
<span data-ttu-id="414e4-120">Proceso</span><span class="sxs-lookup"><span data-stu-id="414e4-120">Compute</span></span>  | <span data-ttu-id="414e4-121">Máquinas virtuales y extensiones de máquinas virtuales, conjuntos de escalado de máquinas virtuales, discos administrados</span><span class="sxs-lookup"><span data-stu-id="414e4-121">Virtual machines and VM extensions, Virtual machine scale sets, managed disks</span></span>   | <span data-ttu-id="414e4-122">Azure container service, Azure container registry</span><span class="sxs-lookup"><span data-stu-id="414e4-122">Azure container service, Azure container registry</span></span> |    |
<span data-ttu-id="414e4-123">Storage</span><span class="sxs-lookup"><span data-stu-id="414e4-123">Storage</span></span>   |  <span data-ttu-id="414e4-124">Cuentas de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="414e4-124">Storage accounts</span></span>       |         |   <span data-ttu-id="414e4-125">Cifrado</span><span class="sxs-lookup"><span data-stu-id="414e4-125">Encryption</span></span>      |
<span data-ttu-id="414e4-126">SQL Database</span><span class="sxs-lookup"><span data-stu-id="414e4-126">SQL Database</span></span>  | <span data-ttu-id="414e4-127">Bases de datos, firewalls, grupos elásticos</span><span class="sxs-lookup"><span data-stu-id="414e4-127">Databases, firewalls, elastic pools</span></span>        |         |   <span data-ttu-id="414e4-128">Más características</span><span class="sxs-lookup"><span data-stu-id="414e4-128">More features</span></span>      |
<span data-ttu-id="414e4-129">Redes</span><span class="sxs-lookup"><span data-stu-id="414e4-129">Networking</span></span>    |  <span data-ttu-id="414e4-130">Redes virtuales, interfaces de red, direcciones IP, tablas de enrutamiento, grupos de seguridad de red, DNS, administradores de tráfico, puertas de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="414e4-130">Virtual networks , network interfaces , IP addresses ,routing tables, network security groups , DNS, Traffic managers, Application gateways</span></span>  |    <span data-ttu-id="414e4-131">Equilibradores de carga</span><span class="sxs-lookup"><span data-stu-id="414e4-131">Load balancers</span></span>     |   <span data-ttu-id="414e4-132">VPN, monitores de red</span><span class="sxs-lookup"><span data-stu-id="414e4-132">VPN, Network watchers</span></span>   |
<span data-ttu-id="414e4-133">Más servicios</span><span class="sxs-lookup"><span data-stu-id="414e4-133">More services</span></span>    |  <span data-ttu-id="414e4-134">Resource Manager, Key Vault, Redis, CDN, Batch</span><span class="sxs-lookup"><span data-stu-id="414e4-134">Resource Manager, Key Vault, Redis,  CDN, Batch</span></span>       |  <span data-ttu-id="414e4-135">Aplicaciones web, aplicaciones de función, Service Bus, Graph RBAC, DocumentDB</span><span class="sxs-lookup"><span data-stu-id="414e4-135">Web apps, Function apps, Service Bus, Graph RBAC, DocumentDB</span></span>   | <span data-ttu-id="414e4-136">Supervisión, programación, funciones de administración, búsqueda, más características de Graph RBAC</span><span class="sxs-lookup"><span data-stu-id="414e4-136">Monitor ,Scheduler, Functions management, Search, more Graph RBAC features</span></span>        |
<span data-ttu-id="414e4-137">Aspectos básicos</span><span class="sxs-lookup"><span data-stu-id="414e4-137">Fundamentals</span></span>     |   <span data-ttu-id="414e4-138">Autenticación: núcleo, métodos asincrónicos</span><span class="sxs-lookup"><span data-stu-id="414e4-138">Authentication - core , Async methods</span></span>       |      |         |

### <a name="import-with-maven"></a><span data-ttu-id="414e4-139">Importación con Maven</span><span class="sxs-lookup"><span data-stu-id="414e4-139">Import with Maven</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure</artifactId>
    <version>1.2.1</version>
</dependency>
```

### <a name="get-help-and-give-feedback"></a><span data-ttu-id="414e4-140">Obtener ayuda y proporcionar comentarios</span><span class="sxs-lookup"><span data-stu-id="414e4-140">Get help and give feedback</span></span>

<span data-ttu-id="414e4-141">Revisar la comunidad de [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-java-sdk) para obtener ayuda con las bibliotecas en su propio código.</span><span class="sxs-lookup"><span data-stu-id="414e4-141">Check out the [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-java-sdk) community for help using the libraries in your own code.</span></span> <span data-ttu-id="414e4-142">Si encuentra errores o tiene sugerencias para mejorar estas bibliotecas, puede enviarlas a través de [GitHub](https://github.com/Azure/azure-sdk-for-java/issues).</span><span class="sxs-lookup"><span data-stu-id="414e4-142">If you encounter any bugs or have suggestions to improve these libraries, please file issues via [GitHub](https://github.com/Azure/azure-sdk-for-java/issues).</span></span>

### <a name="migrate-from-previous-releases"></a><span data-ttu-id="414e4-143">Migración desde versiones anteriores</span><span class="sxs-lookup"><span data-stu-id="414e4-143">Migrate from previous releases</span></span>

<span data-ttu-id="414e4-144">[Migración desde 1.0.0-beta5](https://github.com/Azure/azure-sdk-for-java/blob/master/notes/prepare-for-1.0.0.md)  [Migración desde 1.1.0](https://github.com/Azure/azure-sdk-for-java/blob/master/notes/prepare-for-1.1.0.md)</span><span class="sxs-lookup"><span data-stu-id="414e4-144">[Migrate from 1.0.0-beta5](https://github.com/Azure/azure-sdk-for-java/blob/master/notes/prepare-for-1.0.0.md)  [Migrate from 1.1.0](https://github.com/Azure/azure-sdk-for-java/blob/master/notes/prepare-for-1.1.0.md)</span></span>


