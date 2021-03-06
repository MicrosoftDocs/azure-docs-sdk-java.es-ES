---
ms.openlocfilehash: 0a9b06932baa51c3cf003a4485a3a25261ffe91d
ms.sourcegitcommit: 115f4c8ad07a11f17d79e9d945d63917836b11c8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "61592515"
---
Cree un [archivo de autenticación](../java-sdk-azure-authenticate.md#mgmt-file) y exporte una variable de entorno `AZURE_AUTH_LOCATION` en la línea de comandos con la ruta de acceso completa al archivo.

```bash
export AZURE_AUTH_LOCATION=/Users/raisa/azure.auth
```

El archivo de autenticación se usa para configurar el objeto `Azure` del punto de entrada utilizado por las bibliotecas de administración para definir, crear y configurar los recursos de Azure.

```java
// pull in the location of the security file from the environment 
final File credFile = new File(System.getenv("AZURE_AUTH_LOCATION"));

Azure azure = Azure
        .configure()
        .withLogLevel(LogLevel.NONE)
        .authenticate(credFile)
        .withDefaultSubscription();
```

[Más información](../java-sdk-azure-authenticate.md#mgmt-auth) acerca de las opciones de autenticación al utilizar las bibliotecas de administración de Azure para Java.