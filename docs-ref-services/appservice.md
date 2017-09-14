---
title: Bibliotecas de Azure App Service para Java
description: "Automatice la implementación de aplicaciones web en Azure App Service mediante las API de administración de Azure."
keywords: "Azure, Java, SDK, API, aplicaciones web, móviles, App Service"
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/09/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: appservice
ms.openlocfilehash: e5d2a66dc984d34fb9a6668d2ea3bf1ee6164e70
ms.sourcegitcommit: ae39830d5a54fedceac78d8df1718e77741e03fa
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/09/2017
---
# <a name="azure-app-service-libraries-for-java"></a>Bibliotecas de Azure App Service para Java

## <a name="overview"></a>Información general

Implemente y administre sitios web, aplicaciones web y API de REST con [Azure App Service](/azure/app-service).

Para empezar a trabajar con Azure App Service, consulte [Creación de la primera aplicación web de Java en Azure](/azure/app-service-web/app-service-web-get-started-java).

## <a name="management-api"></a>API de administración

Implemente, escale y configure aplicaciones en Azure App Service con la API de administración.

[Agregue una dependencia](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) al archivo `pom.xml` de Maven para utilizar la API de administración en el proyecto.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-appservice</artifactId>
    <version>1.2.1</version>
</dependency>
```   

> [!div class="nextstepaction"]
> [Explorar las API de administración](/java/api/overview/azure)

### <a name="example"></a>Ejemplo

Implemente una aplicación web desde una imagen de Docker en una aplicación web de Azure en Linux.

```java
WebApp app = azure.webApps().define("newLinuxWebApp")
    .withExistingLinuxPlan(myLinuxAppServicePlan)
    .withExistingResourceGroup("myResourceGroup")
    .withPrivateDockerHubImage("username/my-java-app")
    .withCredentials("dockerHubUser","dockerHubPassword")
    .withAppSetting("PORT","8080").
    .create();
```

## <a name="samples"></a>Muestras

[Implementación de una aplicación web desde FTP o GitHub][1]  
[Intercambio entre versiones de la aplicación con ranuras de implementación][2]  
[Configuración de un dominio personalizado][3]   
[Escalado de una aplicación web en varias regiones][4]   

Ver más [código de Java de ejemplo para Azure App Service](https://azure.microsoft.com/resources/samples/?platform=java&term=appservice) que puede usar en sus aplicaciones.

[1]: ../docs-ref-conceptual/java-sdk-configure-webapp-sources.md
[2]: https://azure.microsoft.com/resources/samples/app-service-java-manage-staging-and-production-slots-for-web-apps/
[3]: https://azure.microsoft.com/resources/samples/app-service-java-manage-web-apps-with-custom-domains/
[4]: https://azure.microsoft.com/resources/samples/app-service-java-scale-web-apps-on-linux/
