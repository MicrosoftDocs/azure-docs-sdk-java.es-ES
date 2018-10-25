---
title: Bibliotecas de Azure Active Directory para Java
description: Documentación de referencia del cliente Java y las bibliotecas de administración de Azure Active Directory para Java
keywords: Azure, Java, SDK, API, SQL, autenticación, AAD, Active Directory, Graph, OAuth 2.0
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/11/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.openlocfilehash: 6147fc959727b53cd796534cefc927145b52d81d
ms.sourcegitcommit: 4d52e47073fb0b3ac40a2689daea186bad5b1ef5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/23/2018
ms.locfileid: "49799841"
---
# <a name="azure-active-directory-libraries-for-java"></a><span data-ttu-id="90665-104">Bibliotecas de Azure Active Directory para Java</span><span class="sxs-lookup"><span data-stu-id="90665-104">Azure Active Directory libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="90665-105">Información general</span><span class="sxs-lookup"><span data-stu-id="90665-105">Overview</span></span>

<span data-ttu-id="90665-106">Proporcione inicio de sesión a los usuarios y controle el acceso a aplicaciones y API con [Azure Active Directory](/azure/active-directory/active-directory-whatis).</span><span class="sxs-lookup"><span data-stu-id="90665-106">Sign-on users and control access to applications and APIs with [Azure Active Directory](/azure/active-directory/active-directory-whatis).</span></span>

<span data-ttu-id="90665-107">Para empezar a trabajar con Azure AD, consulte [Inicio de sesión y cierre de sesión de una aplicación web de Java con Azure AD](/azure/active-directory/develop/active-directory-devquickstarts-webapp-java).</span><span class="sxs-lookup"><span data-stu-id="90665-107">To get started with Azure AD, see [Java web app sign-in and sign-out with Azure AD](/azure/active-directory/develop/active-directory-devquickstarts-webapp-java).</span></span>

## <a name="client-library"></a><span data-ttu-id="90665-108">Biblioteca de cliente</span><span class="sxs-lookup"><span data-stu-id="90665-108">Client library</span></span>

<span data-ttu-id="90665-109">Configure la autenticación de OAuth2, OpenID Connect o Active Directory Graph y el inicio de sesión único de [SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference) con la [biblioteca de autenticación de Azure Active Directory (ADAL) para Java](https://github.com/AzureAD/azure-activedirectory-library-for-java).</span><span class="sxs-lookup"><span data-stu-id="90665-109">Configure OAuth2, OpenID Connect, or Active Directory Graph authentication and [SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference) single-sign on with the [Azure Active Directory authentication library (ADAL) for Java](https://github.com/AzureAD/azure-activedirectory-library-for-java).</span></span>

<span data-ttu-id="90665-110">[Agregue una dependencia](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) al archivo `pom.xml` de Maven para utilizar la biblioteca de cliente en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="90665-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>adal4j</artifactId>
    <version>1.2.0</version>
</dependency>
```   

### <a name="example"></a><span data-ttu-id="90665-111">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="90665-111">Example</span></span>

<span data-ttu-id="90665-112">Recupere un JSON Web Token (JWT) para un usuario del inquilino de Active Directory con [Graph API](https://docs.microsoft.com/azure/active-directory/develop/active-directory-graph-api) de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="90665-112">Retrieve a JSON Web Token (JWT) for a user in your an Active Directory tenant using Azure Active Directory's [Graph API](https://docs.microsoft.com/azure/active-directory/develop/active-directory-graph-api).</span></span> <span data-ttu-id="90665-113">Este token, a continuación, puede usarse para autenticar al usuario con una aplicación o API.</span><span class="sxs-lookup"><span data-stu-id="90665-113">This token can then be used to authenticate the user with an application or API.</span></span>

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

## <a name="management-api"></a><span data-ttu-id="90665-114">API de administración</span><span class="sxs-lookup"><span data-stu-id="90665-114">Management API</span></span>

<span data-ttu-id="90665-115">Configure el [control de acceso basado en roles](/azure/active-directory/role-based-access-control-what-is) y asigne identidades (usuarios y [entidades de servicio](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-objects)) a esos roles con la API de administración.</span><span class="sxs-lookup"><span data-stu-id="90665-115">Configure [role based access control](/azure/active-directory/role-based-access-control-what-is) and assign identities (such as users and [service principals](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-objects)) to those roles with the management API.</span></span> 

<span data-ttu-id="90665-116">[Agregue una dependencia](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) al archivo `pom.xml` de Maven para utilizar la API de administración en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="90665-116">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-graph-rbac</artifactId>
    <version>1.3.0</version>
</dependency>
```

### <a name="example"></a><span data-ttu-id="90665-117">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="90665-117">Example</span></span> 

<span data-ttu-id="90665-118">Cree una nueva entidad de servicio y asígnele el rol de colaborador.</span><span class="sxs-lookup"><span data-stu-id="90665-118">Create a new service principal and assign it the Contributor role.</span></span>

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
> [<span data-ttu-id="90665-119">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="90665-119">Explore the Management APIs</span></span>](/java/api/overview/azure/activedirectory/management)


## <a name="samples"></a><span data-ttu-id="90665-120">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="90665-120">Samples</span></span>

<span data-ttu-id="90665-121">[Administración de grupos, usuarios y roles](https://github.com/Azure-Samples/aad-java-manage-users-groups-and-roles)  </span><span class="sxs-lookup"><span data-stu-id="90665-121">[Manage groups, users, and roles](https://github.com/Azure-Samples/aad-java-manage-users-groups-and-roles)  </span></span>  
<span data-ttu-id="90665-122">[Inicio y cierre de sesión de usuarios en una aplicación web de Java](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect)  </span><span class="sxs-lookup"><span data-stu-id="90665-122">[Sign-in and sign-out users in a Java web app](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect)  </span></span>  
<span data-ttu-id="90665-123">[Acceso a una API con Azure AD mediante una aplicación de línea de comandos](https://github.com/Azure-Samples/active-directory-java-native-headless) </span><span class="sxs-lookup"><span data-stu-id="90665-123">[Access an API with Azure AD using a command line app](https://github.com/Azure-Samples/active-directory-java-native-headless) </span></span>  
[<span data-ttu-id="90665-124">Llamada a Graph API de Azure AD desde la aplicación web de Java</span><span class="sxs-lookup"><span data-stu-id="90665-124">Call the Active AD Graph API from your Java web app</span></span>](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect)  

<span data-ttu-id="90665-125">Vea más [código de Java de ejemplo para Azure AD](https://azure.microsoft.com/en-us/resources/samples/?term=active+directory&platform=java) que puede usar en sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="90665-125">Explore more [sample Java code for Azure AD](https://azure.microsoft.com/en-us/resources/samples/?term=active+directory&platform=java) you can use in your apps.</span></span>
