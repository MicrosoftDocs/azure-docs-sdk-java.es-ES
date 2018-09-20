---
title: Cómo usar el iniciador de Spring Boot para Azure Key Vault
description: Aprenda a configurar una aplicación de Spring Boot Initializer con el iniciador de Azure Key Vault.
services: key-vault
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 02/01/2018
ms.devlang: java
ms.service: key-vault
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: identity
ms.openlocfilehash: 78b7a9a2e26168b19dc8a1d12e47456752b57ffc
ms.sourcegitcommit: e017de4677c5bedd6ef88c8c1b6da279dc973efe
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/15/2018
ms.locfileid: "45639778"
---
# <a name="how-to-use-the-spring-boot-starter-for-azure-key-vault"></a>Cómo usar el iniciador de Spring Boot para Azure Key Vault

## <a name="overview"></a>Información general

En este artículo se muestra cómo crear una aplicación con **[Spring Initializr]** que usa la funcionalidad Spring Boot Starter para Azure Key Vault para recuperar una cadena de conexión almacenada como un secreto en un almacén de claves.

## <a name="prerequisites"></a>Requisitos previos

Los siguientes requisitos previos son necesarios para seguir los pasos descritos en este artículo:

* Una suscripción de Azure. Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN] o registrarse para obtener una [cuenta de Azure gratuita].
* Un [kit de desarrollo de Java (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), versión 1.7 o posterior.
* [Apache Maven](http://maven.apache.org/), versión 3.0 o posterior.

## <a name="create-an-app-using-the-spring-initialzr"></a>Creación de una aplicación con Spring Initialzr

1. Vaya a <https://start.spring.io/>.

1. Especifique que quiere generar un proyecto de **Maven** con **Java**, escriba los nombres de **Group** (Grupo) y **Artifact** (Artefacto) de su aplicación y luego haga clic en el vínculo **Switch to the full version** (Cambiar a la versión completa) de Spring Initializr.

   ![Especificar los nombres de grupo y artefacto][secrets-01]

1. Desplácese a la sección **Azure** y active la casilla **Azure Key Vault**.

   ![Seleccione el iniciador Azure Key Vault][secrets-02]

1. Desplácese a la parte inferior de la página y haga clic en el botón **Generate Project** (Generar proyecto).

   ![Generación del proyecto de Spring Boot][secrets-03]

1. Cuando se le solicite, descargue el proyecto en una ruta de acceso del equipo local.

## <a name="sign-into-azure-and-select-the-subscription-to-use"></a>Inicie sesión en Azure y seleccione la suscripción que desea usar.

1. Abra el símbolo del sistema.

1. Inicie sesión en la cuenta de Azure mediante la CLI de Azure:

   ```azurecli
   az login
   ```
   Siga las instrucciones para completar el proceso de inicio de sesión.

1. Muestre las suscripciones:

   ```azurecli
   az account list
   ```
   Azure devolverá la lista de sus suscripciones, y tendrá que copiar el GUID de la suscripción que desea usar; por ejemplo:

   ```json
   [
     {
       "cloudName": "AzureCloud",
       "id": "ssssssss-ssss-ssss-ssss-ssssssssssss",
       "isDefault": true,
       "name": "Converted Windows Azure MSDN - Visual Studio Ultimate",
       "state": "Enabled",
       "tenantId": "tttttttt-tttt-tttt-tttt-tttttttttttt",
       "user": {
         "name": "contoso@microsoft.com",
         "type": "user"
       }
     }
   ]
   ```

1. Especifique el identificador GUID de la cuenta que desea usar con Azure; por ejemplo:

   ```azurecli
   az account set -s ssssssss-ssss-ssss-ssss-ssssssssssss
   ```

## <a name="create-and-configure-a-new-azure-key-vault-using-the-azure-cli"></a>Creación y configuración de un nuevo almacén de claves de Azure Key Vault mediante la CLI de Azure

1. Cree un grupo de recursos para los recursos de Azure que se usarán para el almacén de claves; por ejemplo:
   ```azurecli
   az group create --name wingtiptoysresources --location westus
   ```
   Donde:

   | Parámetro | DESCRIPCIÓN |
   |---|---|
   | `name` | Especifica un nombre único para el grupo de recursos. |
   | `location` | Especifica la [región de Azure](https://azure.microsoft.com/regions/) donde se hospedará el grupo de recursos. |

   La CLI de Azure mostrará los resultados de la creación del grupo de recursos, por ejemplo:  

   ```json
   {
     "id": "/subscriptions/ssssssss-ssss-ssss-ssss-ssssssssssss/resourceGroups/wingtiptoysresources",
     "location": "westus",
     "managedBy": null,
     "name": "wingtiptoysresources",
     "properties": {
       "provisioningState": "Succeeded"
     },
     "tags": null
   }
   ```

2. Cree una entidad de servicio de Azure desde el registro de su aplicación; por ejemplo:
   ```shell
   az ad sp create-for-rbac --name "wingtiptoysuser"
   ```
   Donde:

   | Parámetro | DESCRIPCIÓN |
   |---|---|
   | `name` | Especifica el nombre de la entidad de servicio de Azure. |

   La CLI de Azure devolverá un mensaje de estado de JSON que contiene los valores de *appId* y *password*, que usará más adelante como identificador de cliente y contraseña de cliente; por ejemplo:

   ```json
   {
     "appId": "iiiiiiii-iiii-iiii-iiii-iiiiiiiiiiii",
     "displayName": "wingtiptoysuser",
     "name": "http://wingtiptoysuser",
     "password": "pppppppp-pppp-pppp-pppp-pppppppppppp",
     "tenant": "tttttttt-tttt-tttt-tttt-tttttttttttt"
   }
   ```

3. Cree un nuevo almacén de claves en el grupo de recursos; por ejemplo:
   ```azurecli
   az keyvault create --name wingtiptoyskeyvault --resource-group wingtiptoysresources --location westus --enabled-for-deployment true --enabled-for-disk-encryption true --enabled-for-template-deployment true --sku standard --query properties.vaultUri
   ```
   Donde:

   | Parámetro | DESCRIPCIÓN |
   |---|---|
   | `name` | Especifica un nombre único para el almacén de claves. |
   | `location` | Especifica la [región de Azure](https://azure.microsoft.com/regions/) donde se hospedará el grupo de recursos. |
   | `enabled-for-deployment` | Especifica la [opción de implementación del almacén de claves](https://docs.microsoft.com/cli/azure/keyvault). |
   | `enabled-for-disk-encryption` | Especifica la [opción de cifrado del almacén de claves](https://docs.microsoft.com/cli/azure/keyvault). |
   | `enabled-for-template-deployment` | Especifica la [opción de cifrado del almacén de claves](https://docs.microsoft.com/cli/azure/keyvault). |
   | `sku` | Especifica la [opción de SKU del almacén de claves](https://docs.microsoft.com/cli/azure/keyvault). |
   | `query` | Especifica el valor que se recuperará de la respuesta, que es el URI del almacén de claves que tendrá que completar en este tutorial. |

   La CLI de Azure mostrará el URI del almacén de claves, que usará más adelante; por ejemplo:  

   ```
   "https://wingtiptoyskeyvault.vault.azure.net"
   ```

4. Establezca la directiva de acceso de la entidad de servicio de Azure que creó anteriormente; por ejemplo:
   ```azurecli
   az keyvault set-policy --name wingtiptoyskeyvault --secret-permission set get list delete --spn "iiiiiiii-iiii-iiii-iiii-iiiiiiiiiiii"
   ```
   Donde:

   | Parámetro | DESCRIPCIÓN |
   |---|---|
   | `name` | Especifica el nombre del almacén de claves anterior. |
   | `secret-permission` | Especifica las [directivas de seguridad](https://docs.microsoft.com/cli/azure/keyvault) para su almacén de claves. |
   | `spn` | Especifica el GUID del registro de la aplicación anterior. |

   La CLI de Azure mostrará los resultados de la creación de la directiva de seguridad, por ejemplo:  

   ```json
   {
     "id": "/subscriptions/ssssssss-ssss-ssss-ssss-ssssssssssss/...",
     "location": "westus",
     "name": "wingtiptoyskeyvault",
     "properties": {
       ...
       ... (A long list of values will be displayed here.)
       ...
     },
     "resourceGroup": "wingtiptoysresources",
     "tags": {},
     "type": "Microsoft.KeyVault/vaults"
   }
   ```

5. Guarde un secreto en su nuevo almacén de claves; por ejemplo:
   ```azurecli
   az keyvault secret set --vault-name "wingtiptoyskeyvault" --name "connectionString" --value "jdbc:sqlserver://SERVER.database.windows.net:1433;database=DATABASE;"
   ```
   Donde:

   | Parámetro | DESCRIPCIÓN |
   |---|---|
   | `vault-name` | Especifica el nombre del almacén de claves anterior. |
   | `name` | Especifica el nombre del secreto. |
   | `value` | Especifica el valor del secreto. |

   La CLI de Azure mostrará los resultados de la creación del secreto; por ejemplo:  

   ```json
   {
     "attributes": {
       "created": "2017-12-01T09:00:16+00:00",
       "enabled": true,
       "expires": null,
       "notBefore": null,
       "recoveryLevel": "Purgeable",
       "updated": "2017-12-01T09:00:16+00:00"
     },
     "contentType": null,
     "id": "https://wingtiptoyskeyvault.vault.azure.net/secrets/connectionString/123456789abcdef123456789abcdef",
     "kid": null,
     "managed": null,
     "tags": {
       "file-encoding": "utf-8"
     },
     "value": "jdbc:sqlserver://wingtiptoys.database.windows.net:1433;database=DATABASE;"
   }
   ```

## <a name="configure-and-compile-your-spring-boot-application"></a>Configuración y compilación de la aplicación de Spring Boot

1. Extraiga los archivos del archivo del proyecto de Spring Boot que descargó anteriormente en un directorio.

2. Vaya a la carpeta *src/main/resources* del proyecto y abra el archivo *application.properties* en un editor de texto.

3. Agregue los valores del almacén de claves que obtuvo en los pasos realizados anteriormente en este tutorial; por ejemplo:
   ```yaml
   azure.keyvault.uri=https://wingtiptoyskeyvault.vault.azure.net/
   azure.keyvault.client-id=iiiiiiii-iiii-iiii-iiii-iiiiiiiiiiii
   azure.keyvault.client-key=pppppppp-pppp-pppp-pppp-pppppppppppp
   ```
   Donde:

   |          Parámetro          |                                 DESCRIPCIÓN                                 |
   |-----------------------------|-----------------------------------------------------------------------------|
   |    `azure.keyvault.uri`     |           Especifica el URI obtenido cuando creó el almacén de claves.           |
   | `azure.keyvault.client-id`  |  Especifica el GUID de *appId* obtenido cuando creó la entidad de servicio.   |
   | `azure.keyvault.client-key` | Especifica el GUID de *password* obtenido cuando creó la entidad de servicio. |


4. Vaya al archivo de código fuente principal del proyecto; por ejemplo: */src/main/java/com/wingtiptoys/secrets*.

5. Abra el archivo Java principal de la aplicación en un editor de texto (por ejemplo: *SecretsApplication.java*) y agregue las siguientes líneas al archivo:

   ```java
   package com.wingtiptoys.secrets;

   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;
   import org.springframework.beans.factory.annotation.Value;
   import org.springframework.boot.CommandLineRunner;

   @SpringBootApplication
   public class SecretsApplication implements CommandLineRunner {

      @Value("${connectionString}")
      private String connectionString;

      public static void main(String[] args) {
         SpringApplication.run(SecretsApplication.class, args);
      }

      public void run(String... varl) throws Exception {
         System.out.println(String.format("\nConnection String stored in Azure Key Vault:\n%s\n",connectionString));
      }
   }
   ```
   Este código de ejemplo recupera la cadena de conexión del almacén de claves y la muestra en la línea de comandos.

6. Guarde y cierre el archivo Java.

## <a name="build-and-test-your-app"></a>Compilación y prueba de la aplicación

1. Vaya al directorio donde está el archivo *pom.xml* de su aplicación de Spring Boot:

1. Compile la aplicación de Spring Boot con Maven; por ejemplo:

   ```bash
   mvn clean package
   ```

   Maven mostrará los resultados de la compilación.

   ![Estado de compilación de la aplicación de Spring Boot][build-application-01]

1. Ejecute la aplicación de Spring Boot con Maven; la aplicación mostrará la cadena de conexión del almacén de claves. Por ejemplo: 

   ```bash
   mvn spring-boot:run
   ```

   ![Mensaje en tiempo de ejecución de Spring Boot][build-application-02]

## <a name="next-steps"></a>Pasos siguientes

Para más información sobre el uso de Azure Key Vault, consulte los siguientes artículos:

* [Documentación de Key Vault].

* [Introducción a Azure Key Vault]

Para obtener más información sobre el uso de aplicaciones de Spring Boot en Azure, consulte los siguientes artículos:

* [Implementación de una aplicación de Spring Boot en Azure App Service](deploy-spring-boot-java-web-app-on-azure.md)

* [Ejecución de una aplicación de Spring Boot en un clúster de Kubernetes en Azure Container Service](deploy-spring-boot-java-app-on-kubernetes.md)

Para más información sobre el uso de Azure con Java, consulte [Azure para desarrolladores de Java] y [Herramientas de Java para Visual Studio Team Services].

<!-- URL List -->

[Documentación de Key Vault]: /azure/key-vault/
[Introducción a Azure Key Vault]: /azure/key-vault/key-vault-get-started
[Azure para desarrolladores de Java]: https://docs.microsoft.com/java/azure/
[cuenta de Azure gratuita]: https://azure.microsoft.com/pricing/free-trial/
[Herramientas de Java para Visual Studio Team Services]: https://java.visualstudio.com/
[ventajas como suscriptor de MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[secrets-01]: media/configure-spring-boot-starter-java-app-with-azure-key-vault/secrets-01.png
[secrets-02]: media/configure-spring-boot-starter-java-app-with-azure-key-vault/secrets-02.png
[secrets-03]: media/configure-spring-boot-starter-java-app-with-azure-key-vault/secrets-03.png

[build-application-01]: media/configure-spring-boot-starter-java-app-with-azure-key-vault/build-application-01.png
[build-application-02]: media/configure-spring-boot-starter-java-app-with-azure-key-vault/build-application-02.png
