---
title: Iniciadores de Spring Boot para Azure
description: "En este artículo se describen los diferentes iniciadores de Spring Boot que hay disponibles para Azure."
services: 
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: java
ms.topic: article
ms.date: 12/01/2017
ms.author: robmcm
ms.openlocfilehash: ba5829407d03d275784a3a458d88ea47ac8494b8
ms.sourcegitcommit: fc48e038721e6910cb8b1f8951df765d517e504d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/06/2017
---
# <a name="spring-boot-starters-for-azure"></a><span data-ttu-id="06fd6-103">Iniciadores de Spring Boot para Azure</span><span class="sxs-lookup"><span data-stu-id="06fd6-103">Spring Boot Starters for Azure</span></span>

<span data-ttu-id="06fd6-104">En este artículo se describen los diferentes iniciadores de Spring Boot para [Spring Initializr], que ofrecen a los desarrolladores de Java características de integración para trabajar con Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="06fd6-104">This article describes the various Spring Boot Starters for the [Spring Initializr] that provide Java developers with integration features for working with Microsoft Azure.</span></span>

![Iniciadores de Spring Boot para Azure][spring-boot-starters]

<span data-ttu-id="06fd6-106">Actualmente hay disponibles los siguientes iniciadores de Spring Boot para Azure:</span><span class="sxs-lookup"><span data-stu-id="06fd6-106">The following Spring Boot Starters are currently available for Azure:</span></span>

* <span data-ttu-id="06fd6-107">**[Compatibilidad para Azure](#azure-support)**</span><span class="sxs-lookup"><span data-stu-id="06fd6-107">**[Azure Support](#azure-support)**</span></span>

   <span data-ttu-id="06fd6-108">Ofrece funcionalidad de configuración automática para los servicios de Azure, entre otros, Service Bus, Storage o Active Directory.</span><span class="sxs-lookup"><span data-stu-id="06fd6-108">Provides auto-configuration support for Azure Services; e.g. Service Bus, Storage, Active Directory, etc.</span></span>

* <span data-ttu-id="06fd6-109">**[Azure Active Directory](#azure-active-directory)**</span><span class="sxs-lookup"><span data-stu-id="06fd6-109">**[Azure Active Directory](#azure-active-directory)**</span></span>

   <span data-ttu-id="06fd6-110">Ofrece funcionalidad de integración de Spring Security con Azure Active Directory con fines de autenticación.</span><span class="sxs-lookup"><span data-stu-id="06fd6-110">Provides integration support for Spring Security with Azure Active Directory for authentication.</span></span>

* <span data-ttu-id="06fd6-111">**[Azure Key Vault](#azure-key-vault)**</span><span class="sxs-lookup"><span data-stu-id="06fd6-111">**[Azure Key Vault](#azure-key-vault)**</span></span>

   <span data-ttu-id="06fd6-112">Ofrece compatibilidad con la anotación de valores de Spring para la integración con los secretos de Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="06fd6-112">Provides Spring value annotation support for integration with Azure Key Vault Secrets.</span></span>

* <span data-ttu-id="06fd6-113">**[Azure Storage](#azure-storage)**</span><span class="sxs-lookup"><span data-stu-id="06fd6-113">**[Azure Storage](#azure-storage)**</span></span>

   <span data-ttu-id="06fd6-114">Ofrece compatibilidad con Spring Boot para los servicios de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="06fd6-114">Provides Spring Boot support for Azure Storage services.</span></span>

<a name="azure-support"></a>
## <a name="azure-support"></a><span data-ttu-id="06fd6-115">Compatibilidad para Azure</span><span class="sxs-lookup"><span data-stu-id="06fd6-115">Azure Support</span></span>

<span data-ttu-id="06fd6-116">Este iniciador de Spring Boot ofrece funcionalidad de configuración automática para los servicios de Azure, entre ellos, Service Bus, Storage, Active Directory, Cosmos DB o Key Vault.</span><span class="sxs-lookup"><span data-stu-id="06fd6-116">This Spring Boot Starter provides auto-configuration support for Azure Services; for example: Service Bus, Storage, Active Directory, Cosmos DB, Key Vault, etc.</span></span>

<span data-ttu-id="06fd6-117">Para ver ejemplos de cómo usar las diferentes características de Azure que proporciona este iniciador, consulte los recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="06fd6-117">For examples of how to use the various Azure features that are provided by this starter, see the following:</span></span>

* <span data-ttu-id="06fd6-118"><https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples></span><span class="sxs-lookup"><span data-stu-id="06fd6-118"><https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples></span></span>

<span data-ttu-id="06fd6-119">Cuando se agrega este iniciador a un proyecto de Spring Boot, se realizan los siguientes cambios en el archivo *pom.xml*:</span><span class="sxs-lookup"><span data-stu-id="06fd6-119">When you add this starter to a Spring Boot project, the following changes are made to the *pom.xml* file:</span></span>

* <span data-ttu-id="06fd6-120">La siguiente propiedad se agrega al elemento `<properties>`:</span><span class="sxs-lookup"><span data-stu-id="06fd6-120">The following property is added to `<properties>` element:</span></span>

   ```xml
   <properties>
      <!-- Other properties will be listed here -->
      <azure.version>0.2.0</azure.version>
   </properties>
   ```

* <span data-ttu-id="06fd6-121">La dependencia de `spring-boot-starter` predeterminada se reemplaza por lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="06fd6-121">The default `spring-boot-starter` dependency is replaced with the following:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-spring-boot</artifactId>
   </dependency>
   ```

* <span data-ttu-id="06fd6-122">Se agrega la siguiente sección al archivo:</span><span class="sxs-lookup"><span data-stu-id="06fd6-122">The following section is added to the file:</span></span>

   ```xml
   <dependencyManagement>
      <dependencies>
         <dependency>
            <groupId>com.microsoft.azure</groupId>
            <artifactId>azure-spring-boot-bom</artifactId>
            <version>${azure.version}</version>
            <type>pom</type>
            <scope>import</scope>
         </dependency>
      </dependencies>
   </dependencyManagement>
   ```

<a name="azure-active-directory"></a>
## <a name="azure-active-directory"></a><span data-ttu-id="06fd6-123">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="06fd6-123">Azure Active Directory</span></span>

<span data-ttu-id="06fd6-124">Este iniciador de Spring Boot ofrece funcionalidad de configuración automática para Spring Security con el fin de ofrecer integración con Azure Active Directory para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="06fd6-124">This Spring Boot Starter provides auto-configuration support for Spring Security in order to provide integration with Azure Active Directory for authentication.</span></span>

<span data-ttu-id="06fd6-125">Para ver ejemplos de cómo usar las características de Azure Active Directory que proporciona este iniciador, consulte los recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="06fd6-125">For examples of how to use the Azure Active Directory features that are provided by this starter, see the following:</span></span>

* <span data-ttu-id="06fd6-126"><https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-active-directory-spring-boot-sample></span><span class="sxs-lookup"><span data-stu-id="06fd6-126"><https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-active-directory-spring-boot-sample></span></span>

<span data-ttu-id="06fd6-127">Cuando se agrega este iniciador a un proyecto de Spring Boot, se realizan los siguientes cambios en el archivo *pom.xml*:</span><span class="sxs-lookup"><span data-stu-id="06fd6-127">When you add this starter to a Spring Boot project, the following changes are made to the *pom.xml* file:</span></span>

* <span data-ttu-id="06fd6-128">La siguiente propiedad se agrega al elemento `<properties>`:</span><span class="sxs-lookup"><span data-stu-id="06fd6-128">The following property is added to `<properties>` element:</span></span>

   ```xml
   <properties>
      <!-- Other properties will be listed here -->
      <azure.version>0.2.0</azure.version>
   </properties>
   ```

* <span data-ttu-id="06fd6-129">La dependencia de `spring-boot-starter` predeterminada se reemplaza por lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="06fd6-129">The default `spring-boot-starter` dependency is replaced with the following:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-active-directory-spring-boot-starter</artifactId>
   </dependency>
   ```

* <span data-ttu-id="06fd6-130">Se agrega la siguiente sección al archivo:</span><span class="sxs-lookup"><span data-stu-id="06fd6-130">The following section is added to the file:</span></span>

   ```xml
   <dependencyManagement>
      <dependencies>
         <dependency>
            <groupId>com.microsoft.azure</groupId>
            <artifactId>azure-spring-boot-bom</artifactId>
            <version>${azure.version}</version>
            <type>pom</type>
            <scope>import</scope>
         </dependency>
      </dependencies>
   </dependencyManagement>
   ```

<a name="azure-key-vault"></a>
## <a name="azure-key-vault"></a><span data-ttu-id="06fd6-131">Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="06fd6-131">Azure Key Vault</span></span>

<span data-ttu-id="06fd6-132">Este iniciador de Spring Boot ofrece compatibilidad con la anotación de valores de Spring para la integración con los secretos de Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="06fd6-132">This Spring Boot Starter provides Spring value annotation support for integration with Azure Key Vault Secrets.</span></span>

<span data-ttu-id="06fd6-133">Para ver ejemplos de cómo usar las características de Azure Key Vault que proporciona este iniciador, consulte los recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="06fd6-133">For examples of how to use the Azure Key Vault features that are provided by this starter, see the following:</span></span>

* <span data-ttu-id="06fd6-134"><https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-keyvault-secrets-spring-boot-sample></span><span class="sxs-lookup"><span data-stu-id="06fd6-134"><https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-keyvault-secrets-spring-boot-sample></span></span>

<span data-ttu-id="06fd6-135">Cuando se agrega este iniciador a un proyecto de Spring Boot, se realizan los siguientes cambios en el archivo *pom.xml*:</span><span class="sxs-lookup"><span data-stu-id="06fd6-135">When you add this starter to a Spring Boot project, the following changes are made to the *pom.xml* file:</span></span>

* <span data-ttu-id="06fd6-136">La siguiente propiedad se agrega al elemento `<properties>`:</span><span class="sxs-lookup"><span data-stu-id="06fd6-136">The following property is added to `<properties>` element:</span></span>

   ```xml
   <properties>
      <!-- Other properties will be listed here -->
      <azure.version>0.2.0</azure.version>
   </properties>
   ```

* <span data-ttu-id="06fd6-137">La dependencia de `spring-boot-starter` predeterminada se reemplaza por lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="06fd6-137">The default `spring-boot-starter` dependency is replaced with the following:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-keyvault-secrets-spring-boot-starter</artifactId>
   </dependency>
   ```

* <span data-ttu-id="06fd6-138">Se agrega la siguiente sección al archivo:</span><span class="sxs-lookup"><span data-stu-id="06fd6-138">The following section is added to the file:</span></span>

   ```xml
   <dependencyManagement>
      <dependencies>
         <dependency>
            <groupId>com.microsoft.azure</groupId>
            <artifactId>azure-spring-boot-bom</artifactId>
            <version>${azure.version}</version>
            <type>pom</type>
            <scope>import</scope>
         </dependency>
      </dependencies>
   </dependencyManagement>
   ```

<a name="azure-storage"></a>
## <a name="azure-storage"></a><span data-ttu-id="06fd6-139">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="06fd6-139">Azure Storage</span></span>

<span data-ttu-id="06fd6-140">Este iniciador de Spring Boot ofrece compatibilidad para la integración con Spring Boot a los servicios de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="06fd6-140">This Spring Boot Starter provides Spring Boot integration support for Azure Storage services.</span></span>

<span data-ttu-id="06fd6-141">Para ver ejemplos de cómo usar las características de Azure Storage que proporciona este iniciador, consulte los recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="06fd6-141">For examples of how to use the Azure Storage features that are provided by this starter, see the following:</span></span>

* [<span data-ttu-id="06fd6-142">Cómo usar el iniciador de Spring Boot para Azure Storage</span><span class="sxs-lookup"><span data-stu-id="06fd6-142">How to use the Spring Boot Starter for Azure Storage</span></span>](configure-spring-boot-starter-java-app-with-azure-storage.md)

* <span data-ttu-id="06fd6-143"><https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-storage-spring-boot-sample></span><span class="sxs-lookup"><span data-stu-id="06fd6-143"><https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-storage-spring-boot-sample></span></span>

<span data-ttu-id="06fd6-144">Cuando se agrega este iniciador a un proyecto de Spring Boot, se realizan los siguientes cambios en el archivo *pom.xml*:</span><span class="sxs-lookup"><span data-stu-id="06fd6-144">When you add this starter to a Spring Boot project, the following changes are made to the *pom.xml* file:</span></span>

* <span data-ttu-id="06fd6-145">La siguiente propiedad se agrega al elemento `<properties>`:</span><span class="sxs-lookup"><span data-stu-id="06fd6-145">The following property is added to `<properties>` element:</span></span>

   ```xml
   <properties>
      <!-- Other properties will be listed here -->
      <azure.version>0.2.0</azure.version>
   </properties>
   ```

* <span data-ttu-id="06fd6-146">La dependencia de `spring-boot-starter` predeterminada se reemplaza por lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="06fd6-146">The default `spring-boot-starter` dependency is replaced with the following:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-storage-spring-boot-starter</artifactId>
   </dependency>
   ```

* <span data-ttu-id="06fd6-147">Se agrega la siguiente sección al archivo:</span><span class="sxs-lookup"><span data-stu-id="06fd6-147">The following section is added to the file:</span></span>

   ```xml
   <dependencyManagement>
      <dependencies>
         <dependency>
            <groupId>com.microsoft.azure</groupId>
            <artifactId>azure-spring-boot-bom</artifactId>
            <version>${azure.version}</version>
            <type>pom</type>
            <scope>import</scope>
         </dependency>
      </dependencies>
   </dependencyManagement>
   ```

## <a name="next-steps"></a><span data-ttu-id="06fd6-148">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="06fd6-148">Next steps</span></span>

<span data-ttu-id="06fd6-149">Para más información sobre el uso de aplicaciones de [Spring Boot] en Azure, consulte [Spring en Azure].</span><span class="sxs-lookup"><span data-stu-id="06fd6-149">For more information about using [Spring Boot] applications on Azure, see [Spring on Azure].</span></span>

<span data-ttu-id="06fd6-150">Para más información sobre el uso de Azure con Java, consulte [Azure para desarrolladores de Java] y [Java Tools for Visual Studio Team Services] (Herramientas de Java para Visual Studio Team Services).</span><span class="sxs-lookup"><span data-stu-id="06fd6-150">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="06fd6-151">Para obtener ayuda para dar sus primeros pasos con sus propias aplicaciones de Spring Boot, consulte **Spring Initializr** en https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="06fd6-151">For help with getting started with your own Spring Boot applications, see the **Spring Initializr** at https://start.spring.io/.</span></span>

<!-- URL List -->

[Azure para desarrolladores de Java]: https://docs.microsoft.com/java/azure/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring en Azure]: https://docs.microsoft.com/java/azure/spring-framework/
[Spring Framework]: https://spring.io/
[Spring Initializr]: https://start.spring.io/

<!-- IMG List -->

[spring-boot-starters]: media/spring-boot-starters-for-azure/spring-boot-starters-cropped.png
