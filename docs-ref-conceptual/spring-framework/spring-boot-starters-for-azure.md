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
# <a name="spring-boot-starters-for-azure"></a>Iniciadores de Spring Boot para Azure

En este artículo se describen los diferentes iniciadores de Spring Boot para [Spring Initializr], que ofrecen a los desarrolladores de Java características de integración para trabajar con Microsoft Azure.

![Iniciadores de Spring Boot para Azure][spring-boot-starters]

Actualmente hay disponibles los siguientes iniciadores de Spring Boot para Azure:

* **[Compatibilidad para Azure](#azure-support)**

   Ofrece funcionalidad de configuración automática para los servicios de Azure, entre otros, Service Bus, Storage o Active Directory.

* **[Azure Active Directory](#azure-active-directory)**

   Ofrece funcionalidad de integración de Spring Security con Azure Active Directory con fines de autenticación.

* **[Azure Key Vault](#azure-key-vault)**

   Ofrece compatibilidad con la anotación de valores de Spring para la integración con los secretos de Azure Key Vault.

* **[Azure Storage](#azure-storage)**

   Ofrece compatibilidad con Spring Boot para los servicios de Azure Storage.

<a name="azure-support"></a>
## <a name="azure-support"></a>Compatibilidad para Azure

Esta utilidad Spring Boot Starter ofrece compatibilidad de configuración automática para los servicios de Azure; por ejemplo: Service Bus, Storage, Active Directory, Cosmos DB, Key Vault, etcétera.

Para ver ejemplos de cómo usar las diferentes características de Azure que proporciona este iniciador, consulte los recursos siguientes:

* <https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples>

Cuando se agrega este iniciador a un proyecto de Spring Boot, se realizan los siguientes cambios en el archivo *pom.xml*:

* La siguiente propiedad se agrega al elemento `<properties>`:

   ```xml
   <properties>
      <!-- Other properties will be listed here -->
      <azure.version>0.2.0</azure.version>
   </properties>
   ```

* La dependencia de `spring-boot-starter` predeterminada se reemplaza por lo siguiente:

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-spring-boot</artifactId>
   </dependency>
   ```

* Se agrega la siguiente sección al archivo:

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
## <a name="azure-active-directory"></a>Azure Active Directory

Este iniciador de Spring Boot ofrece funcionalidad de configuración automática para Spring Security con el fin de ofrecer integración con Azure Active Directory para la autenticación.

Para ver ejemplos de cómo usar las características de Azure Active Directory que proporciona este iniciador, consulte los recursos siguientes:

* <https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-active-directory-spring-boot-sample>

Cuando se agrega este iniciador a un proyecto de Spring Boot, se realizan los siguientes cambios en el archivo *pom.xml*:

* La siguiente propiedad se agrega al elemento `<properties>`:

   ```xml
   <properties>
      <!-- Other properties will be listed here -->
      <azure.version>0.2.0</azure.version>
   </properties>
   ```

* La dependencia de `spring-boot-starter` predeterminada se reemplaza por lo siguiente:

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-active-directory-spring-boot-starter</artifactId>
   </dependency>
   ```

* Se agrega la siguiente sección al archivo:

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
## <a name="azure-key-vault"></a>Azure Key Vault

Este iniciador de Spring Boot ofrece compatibilidad con la anotación de valores de Spring para la integración con los secretos de Azure Key Vault.

Para ver ejemplos de cómo usar las características de Azure Key Vault que proporciona este iniciador, consulte los recursos siguientes:

* <https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-keyvault-secrets-spring-boot-sample>

Cuando se agrega este iniciador a un proyecto de Spring Boot, se realizan los siguientes cambios en el archivo *pom.xml*:

* La siguiente propiedad se agrega al elemento `<properties>`:

   ```xml
   <properties>
      <!-- Other properties will be listed here -->
      <azure.version>0.2.0</azure.version>
   </properties>
   ```

* La dependencia de `spring-boot-starter` predeterminada se reemplaza por lo siguiente:

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-keyvault-secrets-spring-boot-starter</artifactId>
   </dependency>
   ```

* Se agrega la siguiente sección al archivo:

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
## <a name="azure-storage"></a>Azure Storage

Este iniciador de Spring Boot ofrece compatibilidad para la integración con Spring Boot a los servicios de Azure Storage.

Para ver ejemplos de cómo usar las características de Azure Storage que proporciona este iniciador, consulte los recursos siguientes:

* [Cómo usar el iniciador de Spring Boot para Azure Storage](configure-spring-boot-starter-java-app-with-azure-storage.md)

* <https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-storage-spring-boot-sample>

Cuando se agrega este iniciador a un proyecto de Spring Boot, se realizan los siguientes cambios en el archivo *pom.xml*:

* La siguiente propiedad se agrega al elemento `<properties>`:

   ```xml
   <properties>
      <!-- Other properties will be listed here -->
      <azure.version>0.2.0</azure.version>
   </properties>
   ```

* La dependencia de `spring-boot-starter` predeterminada se reemplaza por lo siguiente:

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-storage-spring-boot-starter</artifactId>
   </dependency>
   ```

* Se agrega la siguiente sección al archivo:

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

## <a name="next-steps"></a>Pasos siguientes

Para más información acerca de Spring y Azure, vaya al centro de documentación de Azure.

> [!div class="nextstepaction"]
> [Spring en Azure](/java/azure/spring-framework)

### <a name="additional-resources"></a>Recursos adicionales

Para más información sobre el uso de aplicaciones de [Spring Boot] en Azure, consulte [Spring en Azure].

Para más información sobre el uso de Azure con Java, consulte [Azure para desarrolladores de Java] y [Working with Azure DevOps and Java] (Trabajo con Azure DevOps y Java).

Para obtener ayuda para dar sus primeros pasos con sus propias aplicaciones de Spring Boot, consulte **Spring Initializr** en https://start.spring.io/.

<!-- URL List -->

[Azure para desarrolladores de Java]: /java/azure/
[Working with Azure DevOps and Java]: /azure/devops/ (Trabajo con Azure DevOps y Java)
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring en Azure]: /java/azure/spring-framework/
[Spring Framework]: https://spring.io/
[Spring Initializr]: https://start.spring.io/

<!-- IMG List -->

[spring-boot-starters]: media/spring-boot-starters-for-azure/spring-boot-starters-cropped.png
