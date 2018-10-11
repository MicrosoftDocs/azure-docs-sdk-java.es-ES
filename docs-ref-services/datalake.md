---
title: Bibliotecas de Azure Data Lake Store para Java
description: Documentación de referencia de las bibliotecas de Data Lake Store para Java
keywords: Azure, Java, SDK, API, macrodatos, data lake
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 06/21/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: data-lake-store
ms.openlocfilehash: bcd1fd17759f7d171006d7b2126019d00d06d1db
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/09/2018
ms.locfileid: "48892586"
---
# <a name="azure-data-lake-store-libraries-for-java"></a><span data-ttu-id="7f356-104">Bibliotecas de Azure Data Lake Store para Java</span><span class="sxs-lookup"><span data-stu-id="7f356-104">Azure Data Lake Store libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="7f356-105">Información general</span><span class="sxs-lookup"><span data-stu-id="7f356-105">Overview</span></span>

<span data-ttu-id="7f356-106">Capture datos de cualquier tamaño, tipo y velocidad de ingesta para análisis con [Azure Data Lake Store](/azure/data-lake-store/data-lake-store-overview).</span><span class="sxs-lookup"><span data-stu-id="7f356-106">Capture data of any size, type, and ingestion speed in a single place for analytics with [Azure Data Lake Store](/azure/data-lake-store/data-lake-store-overview).</span></span>

<span data-ttu-id="7f356-107">Para empezar a trabajar con Data Lake Store, consulte la [Introducción a Azure Data Lake Store con Java](/azure/data-lake-store/data-lake-store-get-started-java-sdk).</span><span class="sxs-lookup"><span data-stu-id="7f356-107">To get started with Data Lake Store, see [Get started with Azure Data Lake Store using Java](/azure/data-lake-store/data-lake-store-get-started-java-sdk).</span></span>


## <a name="client-library"></a><span data-ttu-id="7f356-108">Biblioteca de cliente</span><span class="sxs-lookup"><span data-stu-id="7f356-108">Client library</span></span>

<span data-ttu-id="7f356-109">Lea y escriba archivos, establezca permisos y metadatos, y administre archivos y directorios en Data Lake Store con la biblioteca de cliente.</span><span class="sxs-lookup"><span data-stu-id="7f356-109">Read and write files, set permissions and metadata, and manage files and directories in Data Lake Store with the client library.</span></span>

<span data-ttu-id="7f356-110">[Agregue una dependencia](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) al archivo `pom.xml` de Maven para utilizar la biblioteca de cliente en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="7f356-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>

```XML
<dependency>
   <groupId>com.microsoft.azure</groupId>
   <artifactId>azure-data-lake-store-sdk</artifactId>
   <version>2.1.5</version>
</dependency>
```   

## <a name="example"></a><span data-ttu-id="7f356-111">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="7f356-111">Example</span></span>

<span data-ttu-id="7f356-112">Cree un cliente de Data Lake a partir de un nombre de dominio completo y un token de acceso OAuth2 y, a continuación, cree un archivo en Data Lake y escriba en él.</span><span class="sxs-lookup"><span data-stu-id="7f356-112">Create a Data Lake client from a fully qualified domain name and OAuth2 access token, then create a file in Data Lake and write to it.</span></span>

```java
// AccessTokenProvider provider = new ClientCredsTokenProvider(authTokenEndpoint, clientId, clientKey);
ADLStoreClient client = ADLStoreClient.createClient(accountFQDN, provider);

// create directory
client.createDirectory("/a/b/w");
        
// create file and write some content
String filename = "/a/b/c.txt";
OutputStream stream = client.createFile(filename, IfExists.OVERWRITE  );
PrintStream out = new PrintStream(stream);
for (int i = 1; i <= 10; i++) {
    out.println("This is line #" + i);
    out.format("This is the same line (%d), but using formatted output. %n", i);
}
out.close();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="7f356-113">Explorar las API de cliente</span><span class="sxs-lookup"><span data-stu-id="7f356-113">Explore the Client APIs</span></span>](/java/api/overview/azure/datalakestore/client)


## <a name="management-api"></a><span data-ttu-id="7f356-114">API de administración</span><span class="sxs-lookup"><span data-stu-id="7f356-114">Management API</span></span>

<span data-ttu-id="7f356-115">Use la API de administración para administrar cuentas de Data Lake Store, reglas de firewall y proveedores de identidad de confianza.</span><span class="sxs-lookup"><span data-stu-id="7f356-115">Use the management API to manage Data Lake Store accounts, firewall rules, and trusted identity providers.</span></span>

<span data-ttu-id="7f356-116">[Agregue una dependencia](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) al archivo `pom.xml` de Maven para utilizar la API de administración en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="7f356-116">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>


```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-datalake-store</artifactId>
    <version>1.0.0-beta1.3</version>
</dependency>
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="7f356-117">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="7f356-117">Explore the Management APIs</span></span>](/java/api/overview/azure/datalakestore/management)

## <a name="samples"></a><span data-ttu-id="7f356-118">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="7f356-118">Samples</span></span>

<span data-ttu-id="7f356-119">[Introducción a Azure Data Lake][1]</span><span class="sxs-lookup"><span data-stu-id="7f356-119">[Azure Data Lake Get Started][1]</span></span> 

[1]: https://github.com/Azure-Samples/data-lake-store-java-upload-download-get-started

<span data-ttu-id="7f356-120">Ver más [código de Java de ejemplo para Azure Data Lake Store](https://azure.microsoft.com/resources/samples/?platform=java&term=lake) que puede usar en sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="7f356-120">Explore more [sample Java code for Azure Data Lake Store](https://azure.microsoft.com/resources/samples/?platform=java&term=lake) you can use in your apps.</span></span>
