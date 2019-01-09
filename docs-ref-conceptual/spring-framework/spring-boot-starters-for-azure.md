---
title: Iniciadores de Spring Boot para Azure
description: En este artículo se describen los diferentes iniciadores de Spring Boot que hay disponibles para Azure.
services: ''
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 12/19/2018
ms.devlang: java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: 69c0381313994796af31d5301ceadb9f6f40dcb5
ms.sourcegitcommit: f0f140b0862ca5338b1b7e5c33cec3e58a70b8fd
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/03/2019
ms.locfileid: "53991559"
---
# <a name="spring-boot-starters-for-azure"></a><span data-ttu-id="51152-103">Iniciadores de Spring Boot para Azure</span><span class="sxs-lookup"><span data-stu-id="51152-103">Spring Boot Starters for Azure</span></span>

<span data-ttu-id="51152-104">En este artículo se describen los diferentes iniciadores de Spring Boot para [Spring Initializr], que ofrecen a los desarrolladores de Java características de integración para trabajar con Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="51152-104">This article describes the various Spring Boot Starters for the [Spring Initializr] that provide Java developers with integration features for working with Microsoft Azure.</span></span>

![Iniciadores de Spring Boot para Azure][spring-boot-starters]

<span data-ttu-id="51152-106">Actualmente hay disponibles los siguientes iniciadores de Spring Boot para Azure:</span><span class="sxs-lookup"><span data-stu-id="51152-106">The following Spring Boot Starters are currently available for Azure:</span></span>

* <span data-ttu-id="51152-107">**[Compatibilidad para Azure](#azure-support)**</span><span class="sxs-lookup"><span data-stu-id="51152-107">**[Azure Support](#azure-support)**</span></span>

   <span data-ttu-id="51152-108">Ofrece funcionalidad de configuración automática para los servicios de Azure, entre otros, Service Bus, Storage o Active Directory.</span><span class="sxs-lookup"><span data-stu-id="51152-108">Provides auto-configuration support for Azure Services; e.g. Service Bus, Storage, Active Directory, etc.</span></span>

* <span data-ttu-id="51152-109">**[Azure Active Directory](#azure-active-directory)**</span><span class="sxs-lookup"><span data-stu-id="51152-109">**[Azure Active Directory](#azure-active-directory)**</span></span>

   <span data-ttu-id="51152-110">Ofrece funcionalidad de integración de Spring Security con Azure Active Directory con fines de autenticación.</span><span class="sxs-lookup"><span data-stu-id="51152-110">Provides integration support for Spring Security with Azure Active Directory for authentication.</span></span>

* <span data-ttu-id="51152-111">**[Azure Key Vault](#azure-key-vault)**</span><span class="sxs-lookup"><span data-stu-id="51152-111">**[Azure Key Vault](#azure-key-vault)**</span></span>

   <span data-ttu-id="51152-112">Ofrece compatibilidad con la anotación de valores de Spring para la integración con los secretos de Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="51152-112">Provides Spring value annotation support for integration with Azure Key Vault Secrets.</span></span>

* <span data-ttu-id="51152-113">**[Azure Storage](#azure-storage)**</span><span class="sxs-lookup"><span data-stu-id="51152-113">**[Azure Storage](#azure-storage)**</span></span>

   <span data-ttu-id="51152-114">Ofrece compatibilidad con Spring Boot para los servicios de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="51152-114">Provides Spring Boot support for Azure Storage services.</span></span>

<a name="azure-support"></a>
## <a name="azure-support"></a><span data-ttu-id="51152-115">Compatibilidad para Azure</span><span class="sxs-lookup"><span data-stu-id="51152-115">Azure Support</span></span>

<span data-ttu-id="51152-116">Esta utilidad Spring Boot Starter ofrece compatibilidad de configuración automática para los servicios de Azure; por ejemplo: Service Bus, Storage, Active Directory, Cosmos DB, Key Vault, etcétera.</span><span class="sxs-lookup"><span data-stu-id="51152-116">This Spring Boot Starter provides auto-configuration support for Azure Services; for example: Service Bus, Storage, Active Directory, Cosmos DB, Key Vault, etc.</span></span>

<span data-ttu-id="51152-117">Para ver ejemplos de cómo usar las diferentes características de Azure que proporciona este iniciador, consulte los recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="51152-117">For examples of how to use the various Azure features that are provided by this starter, see the following:</span></span>

* <https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples>

<span data-ttu-id="51152-118">Cuando se agrega este iniciador a un proyecto de Spring Boot, se realizan los siguientes cambios en el archivo *pom.xml*:</span><span class="sxs-lookup"><span data-stu-id="51152-118">When you add this starter to a Spring Boot project, the following changes are made to the *pom.xml* file:</span></span>

* <span data-ttu-id="51152-119">La siguiente propiedad se agrega al elemento `<properties>`:</span><span class="sxs-lookup"><span data-stu-id="51152-119">The following property is added to `<properties>` element:</span></span>

   ```xml
   <properties>
      <!-- Other properties will be listed here -->
      <azure.version>0.2.0</azure.version>
   </properties>
   ```

* <span data-ttu-id="51152-120">La dependencia de `spring-boot-starter` predeterminada se reemplaza por lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="51152-120">The default `spring-boot-starter` dependency is replaced with the following:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-spring-boot</artifactId>
   </dependency>
   ```

* <span data-ttu-id="51152-121">Se agrega la siguiente sección al archivo:</span><span class="sxs-lookup"><span data-stu-id="51152-121">The following section is added to the file:</span></span>

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
## <a name="azure-active-directory"></a><span data-ttu-id="51152-122">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="51152-122">Azure Active Directory</span></span>

<span data-ttu-id="51152-123">Este iniciador de Spring Boot ofrece funcionalidad de configuración automática para Spring Security con el fin de ofrecer integración con Azure Active Directory para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="51152-123">This Spring Boot Starter provides auto-configuration support for Spring Security in order to provide integration with Azure Active Directory for authentication.</span></span>

<span data-ttu-id="51152-124">Para ver ejemplos de cómo usar las características de Azure Active Directory que proporciona este iniciador, consulte los recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="51152-124">For examples of how to use the Azure Active Directory features that are provided by this starter, see the following:</span></span>

* <https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-active-directory-spring-boot-sample>

<span data-ttu-id="51152-125">Cuando se agrega este iniciador a un proyecto de Spring Boot, se realizan los siguientes cambios en el archivo *pom.xml*:</span><span class="sxs-lookup"><span data-stu-id="51152-125">When you add this starter to a Spring Boot project, the following changes are made to the *pom.xml* file:</span></span>

* <span data-ttu-id="51152-126">La siguiente propiedad se agrega al elemento `<properties>`:</span><span class="sxs-lookup"><span data-stu-id="51152-126">The following property is added to `<properties>` element:</span></span>

   ```xml
   <properties>
      <!-- Other properties will be listed here -->
      <azure.version>0.2.0</azure.version>
   </properties>
   ```

* <span data-ttu-id="51152-127">La dependencia de `spring-boot-starter` predeterminada se reemplaza por lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="51152-127">The default `spring-boot-starter` dependency is replaced with the following:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-active-directory-spring-boot-starter</artifactId>
   </dependency>
   ```

* <span data-ttu-id="51152-128">Se agrega la siguiente sección al archivo:</span><span class="sxs-lookup"><span data-stu-id="51152-128">The following section is added to the file:</span></span>

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
## <a name="azure-key-vault"></a><span data-ttu-id="51152-129">Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="51152-129">Azure Key Vault</span></span>

<span data-ttu-id="51152-130">Este iniciador de Spring Boot ofrece compatibilidad con la anotación de valores de Spring para la integración con los secretos de Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="51152-130">This Spring Boot Starter provides Spring value annotation support for integration with Azure Key Vault Secrets.</span></span>

<span data-ttu-id="51152-131">Para ver ejemplos de cómo usar las características de Azure Key Vault que proporciona este iniciador, consulte los recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="51152-131">For examples of how to use the Azure Key Vault features that are provided by this starter, see the following:</span></span>

* <https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-keyvault-secrets-spring-boot-sample>

<span data-ttu-id="51152-132">Cuando se agrega este iniciador a un proyecto de Spring Boot, se realizan los siguientes cambios en el archivo *pom.xml*:</span><span class="sxs-lookup"><span data-stu-id="51152-132">When you add this starter to a Spring Boot project, the following changes are made to the *pom.xml* file:</span></span>

* <span data-ttu-id="51152-133">La siguiente propiedad se agrega al elemento `<properties>`:</span><span class="sxs-lookup"><span data-stu-id="51152-133">The following property is added to `<properties>` element:</span></span>

   ```xml
   <properties>
      <!-- Other properties will be listed here -->
      <azure.version>0.2.0</azure.version>
   </properties>
   ```

* <span data-ttu-id="51152-134">La dependencia de `spring-boot-starter` predeterminada se reemplaza por lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="51152-134">The default `spring-boot-starter` dependency is replaced with the following:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-keyvault-secrets-spring-boot-starter</artifactId>
   </dependency>
   ```

* <span data-ttu-id="51152-135">Se agrega la siguiente sección al archivo:</span><span class="sxs-lookup"><span data-stu-id="51152-135">The following section is added to the file:</span></span>

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
## <a name="azure-storage"></a><span data-ttu-id="51152-136">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="51152-136">Azure Storage</span></span>

<span data-ttu-id="51152-137">Este iniciador de Spring Boot ofrece compatibilidad para la integración con Spring Boot a los servicios de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="51152-137">This Spring Boot Starter provides Spring Boot integration support for Azure Storage services.</span></span>

<span data-ttu-id="51152-138">Para ver ejemplos de cómo usar las características de Azure Storage que proporciona este iniciador, consulte los recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="51152-138">For examples of how to use the Azure Storage features that are provided by this starter, see the following:</span></span>

* [<span data-ttu-id="51152-139">Cómo usar el iniciador de Spring Boot para Azure Storage</span><span class="sxs-lookup"><span data-stu-id="51152-139">How to use the Spring Boot Starter for Azure Storage</span></span>](configure-spring-boot-starter-java-app-with-azure-storage.md)

* <https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-storage-spring-boot-sample>

<span data-ttu-id="51152-140">Cuando se agrega este iniciador a un proyecto de Spring Boot, se realizan los siguientes cambios en el archivo *pom.xml*:</span><span class="sxs-lookup"><span data-stu-id="51152-140">When you add this starter to a Spring Boot project, the following changes are made to the *pom.xml* file:</span></span>

* <span data-ttu-id="51152-141">La siguiente propiedad se agrega al elemento `<properties>`:</span><span class="sxs-lookup"><span data-stu-id="51152-141">The following property is added to `<properties>` element:</span></span>

   ```xml
   <properties>
      <!-- Other properties will be listed here -->
      <azure.version>0.2.0</azure.version>
   </properties>
   ```

* <span data-ttu-id="51152-142">La dependencia de `spring-boot-starter` predeterminada se reemplaza por lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="51152-142">The default `spring-boot-starter` dependency is replaced with the following:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-storage-spring-boot-starter</artifactId>
   </dependency>
   ```

* <span data-ttu-id="51152-143">Se agrega la siguiente sección al archivo:</span><span class="sxs-lookup"><span data-stu-id="51152-143">The following section is added to the file:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="51152-144">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="51152-144">Next steps</span></span>

<span data-ttu-id="51152-145">Para más información acerca de Spring y Azure, vaya al centro de documentación de Azure.</span><span class="sxs-lookup"><span data-stu-id="51152-145">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="51152-146">Spring en Azure</span><span class="sxs-lookup"><span data-stu-id="51152-146">Spring on Azure</span></span>](/java/azure/spring-framework)

### <a name="additional-resources"></a><span data-ttu-id="51152-147">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="51152-147">Additional Resources</span></span>

<span data-ttu-id="51152-148">Para más información sobre el uso de aplicaciones de [Spring Boot] en Azure, consulte [Spring en Azure].</span><span class="sxs-lookup"><span data-stu-id="51152-148">For more information about using [Spring Boot] applications on Azure, see [Spring on Azure].</span></span>

<span data-ttu-id="51152-149">Para más información sobre el uso de Azure con Java, consulte [Azure para desarrolladores de Java] y [Working with Azure DevOps and Java] (Trabajo con Azure DevOps y Java).</span><span class="sxs-lookup"><span data-stu-id="51152-149">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Working with Azure DevOps and Java].</span></span>

<span data-ttu-id="51152-150">Para obtener ayuda para dar sus primeros pasos con sus propias aplicaciones de Spring Boot, consulte **Spring Initializr** en https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="51152-150">For help with getting started with your own Spring Boot applications, see the **Spring Initializr** at https://start.spring.io/.</span></span>

<!-- URL List -->

[Azure para desarrolladores de Java]: /java/azure/
[Azure for Java Developers]: /java/azure/
[Working with Azure DevOps and Java]: /azure/devops/ (Trabajo con Azure DevOps y Java)
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring en Azure]: /java/azure/spring-framework/
[Spring on Azure]: /java/azure/spring-framework/
[Spring Framework]: https://spring.io/
[Spring Initializr]: https://start.spring.io/

<!-- IMG List -->

[spring-boot-starters]: media/spring-boot-starters-for-azure/spring-boot-starters-cropped.png
