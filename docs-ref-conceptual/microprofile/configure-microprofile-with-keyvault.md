---
title: Configuración de MicroProfile con Azure Key Vault
description: Aprenda cómo insertar secretos en un servicio web de MicroProfile con Azure Key Vault
services: key-vault
documentationcenter: java
author: jonathangiles
manager: routlaw
editor: jonathangiles
ms.assetid: ''
ms.author: jogiles
ms.date: 09/07/2018
ms.devlang: java
ms.service: key-vault
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: fa93788f9b600d963f35ea599a58d309d3a3ee52
ms.sourcegitcommit: 77dc6c03a2e6264df688d91a04fc6b40950779ef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2018
ms.locfileid: "43240828"
---
# <a name="configure-microprofile-with-azure-key-vault"></a>Configuración de MicroProfile con Azure Key Vault

Este tutorial mostrará cómo configurar una aplicación de [MicroProfile](http://microprofile.io) para recuperar secretos de [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) mediante [MicroProfile Config API](https://microprofile.io/project/eclipse/microprofile-config) para crear un conexión directa a Azure Key Vault. Con MicroProfile Config API, los desarrolladores pueden usar una API estándar para recuperar e insertar datos de configuración en sus microservicios.

Antes de continuar, vamos a ver rápidamente lo que una combinación de Azure Key Vault y MicroProfile Config API nos permite escribir en nuestro código. Este es un fragmento de código de un campo en una clase que ha sido anotada con `@Inject` y `@ConfigProperty`. El valor de `name` especificado en la anotación es el nombre de la propiedad que se va a buscar en Azure Key Vault, y `defaultValue` es el valor en el que se establecerá si no se detecta la clave. El resultado final es que el valor almacenado en Azure Key Vault, o el valor predeterminado, se insertará automáticamente en el campo en tiempo de ejecución, lo que facilita el trabajo de los desarrolladores que ya no necesitan pasar valores en constructores y métodos setter porque MicroProfile se hace cargo de eso.

```java
@Inject
@ConfigProperty(name = "key-name", defaultValue = "Unknown")
String keyValue;
```

También se puede acceder a la configuración de MicroProfile directamente, para solicitar secretos según sea necesario, por ejemplo:

```java
public class DemoClass {
    @Inject
    Config config;

    public void method() {
        System.out.println("Hello: " + config.getValue("key-name", String.class));
    }
}
```

Este ejemplo usa [Payara Micro](https://www.payara.fish/payara_micro) y [MicroProfile](https://microprofile.io/) para crear un pequeño archivo .war de Java que se puede ejecutar localmente en el equipo. No se muestra cómo incluir el código en un contenedor de Docker ni insertar el código en Azure, pero al final de este tutorial se incluyen vínculos a otros tutoriales útiles que explican esto.

Este ejemplo utiliza una biblioteca de código abierto gratuita que crea un origen de configuración (con MicroProfile Config API) para Azure Key Vault. Para obtener más información sobre esta biblioteca y revisar el código, visite la [página de GitHub del proyecto](https://github.com/Azure/azure-microprofile/tree/master/microprofile-config-keyvault). Con esta biblioteca, el código de este tutorial puede centrarse en la configuración de la biblioteca y en la inserción de claves en el código, y no es necesario escribir ningún código específico de Azure.

Estos son los pasos necesarios para ejecutar este código en el equipo local, empezando por la creación de un recurso de Azure Key Vault.

## <a name="creating-an-azure-key-vault-resource"></a>Creación de un recurso de Azure Key Vault

Usaremos la CLI de Azure para crear el recurso de Azure Key Vault y rellenarlo con un secreto.

1. En primer lugar, creamos una entidad de servicio de Azure. Esto nos proporciona el identificador y la clave de cliente necesarios para tener acceso a Key Vault:

```bash
az login
az account set --subscription <subscription_id>

az ad sp create-for-rbac --name <service_principal_name>
```

Supongamos que usamos `microprofile-keyvault-service-principal` como nombre de la entidad de servicio del paso anterior. La respuesta de Azure para hacer esto tendrá la siguiente forma, ligeramente censurada:

```json
{
  "appId": "5292398e-XXXX-40ce-XXXX-d49fXXXX9e79",
  "displayName": "microprofile-keyvault-service-principal",
  "name": "http://microprofile-keyvault-service-principal",
  "password": "9b217777-XXXX-4954-XXXX-deafXXXX790a",
  "tenant": "72f988bf-XXXX-41af-XXXX-2d7cd011db47"
}
```

Hay que resaltar aquí los valores `appID` y `password`; son lo que usaremos más adelante como `client ID` y `key`, respectivamente.

Ahora que hemos creado una entidad de servicio, podemos crear también un grupo de recursos (si ya tiene uno que desea usar, puede omitir este paso). Tenga en cuenta que para obtener la lista de las ubicaciones de los grupos de recursos, puede llamar a `az account list-locations` y usar el valor `name` de esa lista para especificar dónde se debe crear el grupo de recursos.

```bash
# For this tutorial, the author chose to use `westus`
# and `jg-test` for the resource group name.
az group create -l <resource_group_location> -n <resource_group_name>
```

Ahora crearemos un recurso de Azure Key Vault. Tenga en cuenta que el nombre del almacén de claves es el que se va a usar para hacer referencia al almacén de claves más adelante, así que elija algo fácil de recordar.

```bash
az keyvault create --name <your_keyvault_name>            \
                   --resource-group <your_resource_group> \
                   --location <location>                  \
                   --enabled-for-deployment true          \
                   --enabled-for-disk-encryption true     \
                   --enabled-for-template-deployment true \
                   --sku standard
```

También es necesario conceder los permisos adecuados a la entidad de servicio creada anteriormente, para que pueda tener acceso a los secretos de Key Vault. Tenga en cuenta que el valor de appID es el valor `appId` obtenido cuando se creó la entidad de servicio (es decir, `5292398e-XXXX-40ce-XXXX-d49fXXXX9e79`, pero usa el valor de la salida del terminal).

```bash
az keyvault set-policy --name <your_keyvault_name>   \
                       --secret-permission get list  \
                       --spn <your_sp_appId_created_in_step1>
```

Ahora estamos listos para insertar un secreto en Key Vault. Vamos a usar el nombre de clave `demo-key` y a establecer el valor de la clave en `demo-value`:

```bash
az keyvault secret set --name demo-key      \
                       --value demo-value   \
                       --vault-name <your_keyvault_name>  
```

Eso es todo. Ahora tenemos un almacén de claves en ejecución en Azure con un solo secreto. Podemos clonar este repositorio y configurarlo para usar este recurso en nuestra aplicación.

## <a name="getting-up-and-running-locally"></a>Preparación y ejecución local

Este ejemplo se basa en una aplicación de ejemplo disponible en GitHub, por lo que vamos a clonarla y a recorrer el código. Siga estos pasos para obtener el código clonado en su equipo:

1. `git clone https://github.com/Azure-Samples/microprofile-configsource-keyvault.git`

1. `cd microprofile-configsource-keyvault`

1. Vaya a `src/main/resources/META-INF/microprofile-config.properties` y cambie las propiedades en el archivo microprofile-config.properties con detalles de lo anterior.

1. Intente ejecutar el servidor mediante `mvn clean package payara-micro:start`.

1. Intente acceder a [http://localhost:8080/keyvault-configsource/api/config](http://localhost:8080/keyvault-configsource/api/config) en su explorador web. Verá una respuesta sencilla que muestra los valores que se va a leer desde Azure Key Vault.

## <a name="summary"></a>Resumen

Esta aplicación de ejemplo reúne MicroProfile Config API, Azure Key Vault y la biblioteca de código abierto gratuita [microprofile-config-keyvault](https://github.com/Azure/azure-microprofile/tree/master/microprofile-config-keyvault) para facilitar la inserción de datos de configuración y secretos en nuestros servicios web de MicroProfile.
