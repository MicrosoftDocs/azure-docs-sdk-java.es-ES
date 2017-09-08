---
title: Bibliotecas de Azure Data Lake Store para Java
description: "Documentación de referencia de las bibliotecas de Data Lake Store para Java"
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
ms.openlocfilehash: 66ff566e74203d3b5a8e9bcc170f4c21cf310645
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/28/2017
---
# <a name="azure-data-lake-store-libraries-for-java"></a>Bibliotecas de Azure Data Lake Store para Java

## <a name="overview"></a>Información general

Capture datos de cualquier tamaño, tipo y velocidad de ingesta para análisis con [Azure Data Lake Store](/azure/data-lake-store/data-lake-store-overview).

Para empezar a trabajar con Data Lake Store, consulte la [Introducción a Azure Data Lake Store con Java](/azure/data-lake-store/data-lake-store-get-started-java-sdk).


## <a name="client-library"></a>Biblioteca de cliente

Lea y escriba archivos, establezca permisos y metadatos, y administre archivos y directorios en Data Lake Store con la biblioteca de cliente.

[Agregue una dependencia](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) al archivo `pom.xml` de Maven para utilizar la biblioteca de cliente en el proyecto.

```XML
<dependency>
   <groupId>com.microsoft.azure</groupId>
   <artifactId>azure-data-lake-store-sdk</artifactId>
   <version>2.1.5</version>
</dependency>
```   

## <a name="example"></a>Ejemplo

Cree un cliente de Data Lake a partir de un nombre de dominio completo y un token de acceso OAuth2 y, a continuación, cree un archivo en Data Lake y escriba en él.

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
> [Explorar las API de cliente](/java/api/overview/azure/datalakestore/clientlibrary)


## <a name="management-api"></a>API de administración

Use la API de administración para administrar cuentas de Data Lake Store, reglas de firewall y proveedores de identidad de confianza.

[Agregue una dependencia](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) al archivo `pom.xml` de Maven para utilizar la API de administración en el proyecto.


```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-datalake-store</artifactId>
    <version>1.0.0-beta1.3</version>
</dependency>
```

> [!div class="nextstepaction"]
> [Explorar las API de administración](/java/api/overview/azure/datalakestore/managementapi)

## <a name="samples"></a>Muestras

[Introducción a Azure Data Lake][1] 

[1]: https://github.com/Azure-Samples/data-lake-store-java-upload-download-get-started

Ver más [código de Java de ejemplo para Azure Data Lake Store](https://azure.microsoft.com/resources/samples/?platform=java&term=lake) que puede usar en sus aplicaciones.
