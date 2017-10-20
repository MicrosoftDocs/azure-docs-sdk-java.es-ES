---
title: Bibliotecas de Azure Active Directory para Java
description: "Documentación de referencia del cliente Java y las bibliotecas de administración de Azure Active Directory para Java"
keywords: "Azure, Java, SDK, API, SQL, autenticación, AAD, Active Directory, Graph, OAuth 2.0"
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/11/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: active-directory
ms.openlocfilehash: 081b8455a6cd8f26ce714328d10ce25ea6a07e3b
ms.sourcegitcommit: 4b63ecd2c92a9115dfae018618e4e4046b061b3e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/14/2017
---
# <a name="azure-active-directory-libraries-for-java"></a>Bibliotecas de Azure Active Directory para Java

## <a name="overview"></a>Información general

Proporcione inicio de sesión a los usuarios y controle el acceso a aplicaciones y API con [Azure Active Directory](/azure/active-directory/active-directory-whatis).

Para empezar a trabajar con Azure AD, consulte [Inicio de sesión y cierre de sesión de una aplicación web de Java con Azure AD](/azure/active-directory/develop/active-directory-devquickstarts-webapp-java).

## <a name="client-library"></a>Biblioteca de cliente

Configure la autenticación de OAuth2, OpenID Connect o Active Directory Graph y el inicio de sesión único de [SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference) con la [biblioteca de autenticación de Azure Active Directory (ADAL) para Java](https://github.com/AzureAD/azure-activedirectory-library-for-java).

[Agregue una dependencia](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) al archivo `pom.xml` de Maven para utilizar la biblioteca de cliente en el proyecto.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>adal4j</artifactId>
    <version>1.2.0</version>
</dependency>
```   

### <a name="example"></a>Ejemplo

Recupere un JSON Web Token (JWT) para un usuario del inquilino de Active Directory con la [API Graph](https://docs.microsoft.com/azure/active-directory/develop/active-directory-graph-api) de Azure Active Directory. Este token, a continuación, puede usarse para autenticar al usuario con una aplicación o API.

```java
ExecutorService service = Executors.newFixedThreadPool(1);
AuthenticationContext context = new AuthenticationContext(AUTHORITY, false, service);
Future<AuthenticationResult> future = context.acquireToken(
    "https://graph.windows.net", YOUR_TENANT_ID, username, password,
    null);
AuthenticationResult result = future.get();
System.out.println("Access Token - " + result.getAccessToken());
System.out.println("Refresh Token - " + result.getRefreshToken());
System.out.println("ID Token - " + result.getIdToken());
```

## <a name="management-api"></a>API de administración

Configure el [control de acceso basado en roles](/azure/active-directory/role-based-access-control-what-is) y asigne identidades (usuarios y [entidades de servicio](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-objects)) a esos roles con la API de administración. 

[Agregue una dependencia](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) al archivo `pom.xml` de Maven para utilizar la API de administración en el proyecto.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-graph-rbac</artifactId>
    <version>1.3.0</version>
</dependency>
```

### <a name="example"></a>Ejemplo 

Cree una nueva entidad de servicio y asígnele el rol de colaborador.

```java
ServicePrincipal sp = Azure.servicePrincipals().define(spName)
    .withNewApplication("http://" + spName)
    .create();
RoleAssignment roleAssignment2 = authenticated.roleAssignments()
    .define("contribRoleAssignment")
    .forServicePrincipal(sp)
    .withBuiltInRole(BuiltInRole.CONTRIBUTOR)
    .withSubscriptionScope("862f67bc-d3ae-4243-bec7-3da6dca77717")
    .create();
```

> [!div class="nextstepaction"]
> [Explorar las API de administración](/java/api/overview/azure/activedirectory/managementapi)


## <a name="samples"></a>Muestras

[Administración de grupos, usuarios y roles](https://github.com/Azure-Samples/aad-java-browse-graph-and-manage-roles)    
[Inicio y cierre de sesión de usuarios en una aplicación web de Java](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect)    
[Acceso a una API con Azure AD mediante una aplicación de línea de comandos](https://github.com/Azure-Samples/active-directory-java-native-headless)   
[Llamada a la API Graph de Azure AD desde la aplicación web de Java](https://github.com/Azure-Samples/active-directory-java-graphapi-web/)  

Vea más [código de Java de ejemplo para Azure AD](https://azure.microsoft.com/en-us/resources/samples/?term=active+directory&platform=java) que puede usar en sus aplicaciones.
