---
title: Notas de la versión de las bibliotecas de administración de Azure para Java | Microsoft Docs
description: Vea las novedades y los cambios importantes en las bibliotecas de administración de Azure para Java
keywords: Azure, Java, API, referencia, notas, actualizaciones, en desuso
author: routlaw
manager: douge
ms.assetid: 1f128cf9-f747-4344-84e1-f9964709deb8
ms.service: Azure
ms.devlang: java
ms.topic: reference
ms.technology: Azure
ms.date: 3/06/2016
ms.openlocfilehash: 0aaa83ceb42192441decb5972baae56fed337fb2
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/09/2018
ms.locfileid: "48899460"
---
# <a name="release-notes"></a><span data-ttu-id="913c2-104">Notas de la versión</span><span class="sxs-lookup"><span data-stu-id="913c2-104">Release Notes</span></span> 

## <a name="october-5-2017---130"></a><span data-ttu-id="913c2-105">5 de octubre de 2017: 1.3.0</span><span class="sxs-lookup"><span data-stu-id="913c2-105">October 5, 2017 - 1.3.0</span></span> 

<span data-ttu-id="913c2-106">La versión 1.3.0 es compatible con versiones anteriores de servicios y características que alcanzaron la etapa de disponibilidad general (estable) en versiones anteriores.</span><span class="sxs-lookup"><span data-stu-id="913c2-106">Version 1.3.0 is backwards compatible with previous versions for services and features use that reached the general availability (stable) stage in previous releases.</span></span>

<span data-ttu-id="913c2-107">Los principales cambios con respecto a las versiones preliminares de esos servicios están marcados con la anotación @Beta.</span><span class="sxs-lookup"><span data-stu-id="913c2-107">Any breaking changes from Preview versions for those services are marked with the @Beta annotation.</span></span>

<span data-ttu-id="913c2-108">Si va a migrar código a la versión 1.3.0, puede usar [estas notas](https://github.com/Azure/azure-sdk-for-java/blob/master/notes/prepare-for-1.3.0.md) para preparar el código existente para la versión 1.3.</span><span class="sxs-lookup"><span data-stu-id="913c2-108">If you are migrating your code to 1.3.0, you can use [these notes](https://github.com/Azure/azure-sdk-for-java/blob/master/notes/prepare-for-1.3.0.md) to prepare your existing code for the 1.3 version.</span></span>

### <a name="generally-availabile-in-v13"></a><span data-ttu-id="913c2-109">Disponibilidad general en la versión V1.3</span><span class="sxs-lookup"><span data-stu-id="913c2-109">Generally availabile in V1.3</span></span>

<span data-ttu-id="913c2-110">Algunas de las API que estaban todavía en la versión beta en versiones anteriores ahora están disponibles de forma general, en concreto:</span><span class="sxs-lookup"><span data-stu-id="913c2-110">Some of the APIs that were still in Beta in previous releases are now GA, in particular:</span></span>

- <span data-ttu-id="913c2-111">métodos asincrónicos</span><span class="sxs-lookup"><span data-stu-id="913c2-111">async methods</span></span>
- <span data-ttu-id="913c2-112">todos los métodos de la red CDN que anteriormente se encontraban en la versión beta</span><span class="sxs-lookup"><span data-stu-id="913c2-112">all methods in CDN that were previously in Beta</span></span>
- <span data-ttu-id="913c2-113">todos los métodos y las interfaces de Application Gateway que anteriormente se encontraban en la versión beta</span><span class="sxs-lookup"><span data-stu-id="913c2-113">all methods and interfaces in Application Gateways that were previously in Beta</span></span>

  <span data-ttu-id="913c2-114">Algunas partes de la biblioteca aún están en versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="913c2-114">Some parts of the library are still in Preview.</span></span> <span data-ttu-id="913c2-115">Consulte la tabla siguiente sobre el estado actual de las bibliotecas:</span><span class="sxs-lookup"><span data-stu-id="913c2-115">Refer to the table below for the current state of the libraries:</span></span>

<span data-ttu-id="913c2-116">Servicio o característica</span><span class="sxs-lookup"><span data-stu-id="913c2-116">Service or feature</span></span> | <span data-ttu-id="913c2-117">Disponible de forma general</span><span class="sxs-lookup"><span data-stu-id="913c2-117">Available as GA</span></span> | <span data-ttu-id="913c2-118">Disponible como versión preliminar</span><span class="sxs-lookup"><span data-stu-id="913c2-118">Available as Preview</span></span> 
---------|---------|---------|-
<span data-ttu-id="913c2-119">Compute</span><span class="sxs-lookup"><span data-stu-id="913c2-119">Compute</span></span>  | <span data-ttu-id="913c2-120">Máquinas virtuales y extensiones de máquinas virtuales, conjuntos de escalado de máquinas virtuales, discos administrados</span><span class="sxs-lookup"><span data-stu-id="913c2-120">Virtual machines and VM extensions, Virtual machine scale sets, managed disks</span></span>   | <span data-ttu-id="913c2-121">Azure container service, Azure container registry</span><span class="sxs-lookup"><span data-stu-id="913c2-121">Azure container service, Azure container registry</span></span> 
<span data-ttu-id="913c2-122">Storage</span><span class="sxs-lookup"><span data-stu-id="913c2-122">Storage</span></span>   |  <span data-ttu-id="913c2-123">Cuentas de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="913c2-123">Storage accounts</span></span>       |    <span data-ttu-id="913c2-124">Cifrado</span><span class="sxs-lookup"><span data-stu-id="913c2-124">Encryption</span></span>     
<span data-ttu-id="913c2-125">SQL Database</span><span class="sxs-lookup"><span data-stu-id="913c2-125">SQL Database</span></span>  | <span data-ttu-id="913c2-126">Bases de datos, firewalls, grupos elásticos</span><span class="sxs-lookup"><span data-stu-id="913c2-126">Databases, firewalls, elastic pools</span></span>              
<span data-ttu-id="913c2-127">Redes</span><span class="sxs-lookup"><span data-stu-id="913c2-127">Networking</span></span>    |  <span data-ttu-id="913c2-128">Redes virtuales, interfaces de red, direcciones IP, tablas de enrutamiento, grupos de seguridad de red, DNS, administradores de tráfico, puertas de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="913c2-128">Virtual networks , network interfaces , IP addresses ,routing tables, network security groups , DNS, Traffic managers, Application gateways</span></span>  |    <span data-ttu-id="913c2-129">Equilibradores de carga, emparejamiento de redes, puerta de enlace de red virtual, Network Watcher</span><span class="sxs-lookup"><span data-stu-id="913c2-129">Load balancers, Network peering, Virtual Network Gateway, Network watchers</span></span> 
<span data-ttu-id="913c2-130">Más servicios</span><span class="sxs-lookup"><span data-stu-id="913c2-130">More services</span></span>    |  <span data-ttu-id="913c2-131">Resource Manager, Key Vault, Redis, CDN, Batch</span><span class="sxs-lookup"><span data-stu-id="913c2-131">Resource Manager, Key Vault, Redis,  CDN, Batch</span></span>       |  <span data-ttu-id="913c2-132">Web Apps, Function App, Service Bus, Graph RBAC, Cosmos DB, Search</span><span class="sxs-lookup"><span data-stu-id="913c2-132">Web apps, Function apps, Service Bus, Graph RBAC, Cosmos DB, Search</span></span>  
<span data-ttu-id="913c2-133">Aspectos básicos</span><span class="sxs-lookup"><span data-stu-id="913c2-133">Fundamentals</span></span>     |   <span data-ttu-id="913c2-134">Autenticación: principal, métodos asincrónicos, identidad de servicio administrada</span><span class="sxs-lookup"><span data-stu-id="913c2-134">Authentication - core , Async methods , Managed Service Identity</span></span>      |      |

> <span data-ttu-id="913c2-135">Las características de la versión preliminar están marcadas con una anotación `@Beta` en el nivel de clase o interfaz o método de las bibliotecas.</span><span class="sxs-lookup"><span data-stu-id="913c2-135">Preview features are marked with a `@Beta` annotation at the class or interface or method level in libraries.</span></span> <span data-ttu-id="913c2-136">Estas características están sujetas a cambios.</span><span class="sxs-lookup"><span data-stu-id="913c2-136">These features are subject to change.</span></span> <span data-ttu-id="913c2-137">Puede que se modifiquen de cualquier manera (o incluso se eliminen) en el futuro.</span><span class="sxs-lookup"><span data-stu-id="913c2-137">They can be modified in any way, or even removed, in the future.</span></span>

### <a name="import-with-maven"></a><span data-ttu-id="913c2-138">Importación con Maven</span><span class="sxs-lookup"><span data-stu-id="913c2-138">Import with Maven</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure</artifactId>
    <version>1.3.0</version>
</dependency>
```

### <a name="get-help-and-give-feedback"></a><span data-ttu-id="913c2-139">Obtención de ayuda y ofrecimiento de comentarios</span><span class="sxs-lookup"><span data-stu-id="913c2-139">Get help and give feedback</span></span>

<span data-ttu-id="913c2-140">Revisar la comunidad de [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-java-sdk) para obtener ayuda con las bibliotecas en su propio código.</span><span class="sxs-lookup"><span data-stu-id="913c2-140">Check out the [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-java-sdk) community for help using the libraries in your own code.</span></span> <span data-ttu-id="913c2-141">Si encuentra errores o tiene sugerencias para mejorar estas bibliotecas, puede enviarlas a través de [GitHub](https://github.com/Azure/azure-sdk-for-java/issues).</span><span class="sxs-lookup"><span data-stu-id="913c2-141">If you encounter any bugs or have suggestions to improve these libraries, please file issues via [GitHub](https://github.com/Azure/azure-sdk-for-java/issues).</span></span>


