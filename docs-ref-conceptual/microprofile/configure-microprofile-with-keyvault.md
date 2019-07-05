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
ms.openlocfilehash: c405711813176823f2ddee6b4002f75c2b25fdb5
ms.sourcegitcommit: f8faa4a14c714e148c513fd46f119524f3897abf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2019
ms.locfileid: "67533613"
---
# <a name="configure-microprofile-by-using-azure-key-vault"></a>Configuración de MicroProfile con Azure Key Vault

En este artículo se muestra cómo configurar una aplicación [MicroProfile](http://microprofile.io) para recuperar secretos desde un [almacén de claves de Azure](https://azure.microsoft.com/services/key-vault/). En este proceso, se usa [MicroProfile Config API](https://microprofile.io/project/eclipse/microprofile-config) para crear una conexión directa a un almacén de claves de Azure. Con MicroProfile Config API, los desarrolladores pueden usar una API estándar para recuperar e insertar datos de configuración en sus microservicios.

Antes de continuar, eche un vistazo rápido a lo que una combinación de Azure Key Vault y MicroProfile Config API nos permite escribir en nuestro código. El siguiente es un fragmento de código de un campo en una clase que ha sido anotada con `@Inject` y `@ConfigProperty`. El valor *name* especificado en la anotación es el nombre de la propiedad que se va a buscar en Azure Key Vault, y *defaultValue* es el valor en el que se establecerá si no se detecta la clave. El resultado es que el valor que se almacena en el almacén de claves, o el valor predeterminado, se inserta automáticamente en el campo en tiempo de ejecución. Esta acción simplifica las cosas porque ya no necesita pasar valores en constructores y métodos establecedores. En su lugar, MicroProfile controla esta tarea.

```java
@Inject
@ConfigProperty(name = "key-name", defaultValue = "Unknown")
String keyValue;
```

También se puede acceder a la configuración de MicroProfile directamente para solicitar secretos según sea necesario. Por ejemplo:

```java
public class DemoClass {
    @Inject
    Config config;

    public void method() {
        System.out.println("Hello: " + config.getValue("key-name", String.class));
    }
}
```

Este código de ejemplo usa [Payara Micro](https://www.payara.fish/payara_micro) y [MicroProfile](https://microprofile.io/) para crear un pequeño archivo de requisitos de aplicación web (WAR) de Java que se puede ejecutar localmente en el equipo. No se muestra cómo incluir el código en un contenedor de Docker ni cómo insertarlo en Azure, pero al final de este artículo se incluyen vínculos a otros tutoriales útiles que explican esto.

Este ejemplo utiliza una biblioteca de código abierto gratuita que crea un origen de configuración (con MicroProfile Config API) en el almacén de claves. Para más información sobre esta biblioteca y revisar el código, visite la [página del proyecto en GitHub](https://github.com/Azure/azure-microprofile/tree/master/microprofile-config-keyvault). Si usa la biblioteca, el código de este tutorial puede centrarse simplemente en la configuración de la biblioteca y, a continuación, insertar las claves en el código. No es necesario escribir ningún código específico de Azure.

Para ejecutar este código en el equipo local, empezando por la creación de un recurso de Azure Key Vault, siga las instrucciones de las secciones siguientes.

## <a name="create-a-key-vault-resource"></a>Creación de un almacén de claves

En esta sección, usaremos la CLI de Azure para crear el recurso de Azure Key Vault y rellenarlo con un secreto.

1. Cree una entidad de servicio de Azure. En este paso se obtiene el identificador de cliente y la clave que necesita para tener acceso a su almacén de claves:

    ```bash
    az login
    az account set --subscription <subscription_id>

    az ad sp create-for-rbac --name <service_principal_name>
    ```

    Vamos a usar *microprofile-keyvault-service-principal* para reemplazar *\<service_principal_name>* en el paso anterior. La respuesta de Azure será similar a la siguiente:

    ```json
    {
      "appId": "5292398e-XXXX-40ce-XXXX-d49fXXXX9e79",
      "displayName": "microprofile-keyvault-service-principal",
      "name": "http://microprofile-keyvault-service-principal",
      "password": "9b217777-XXXX-4954-XXXX-deafXXXX790a",
      "tenant": "72f988bf-XXXX-41af-XXXX-2d7cd011db47"
    }
    ```

    Hay que resaltar aquí los valores de *appId* y *contraseña*. Se usarán más adelante en este artículo como *identificador de cliente* y *clave*.

1. (Opcional) Ahora que ha creado una entidad de servicio, puede crear un grupo de recursos. Puede omitir este paso si ya tiene un grupo de recursos que le gustaría usar. Para obtener la lista de las ubicaciones de los grupos de recursos, puede llamar a `az account list-locations` y usar el valor *name* de esa lista para especificar dónde se debe crear el grupo de recursos.

    ```bash
    # In this tutorial, "westus" is the resource group location
    # and "jg-test" is the resource group name.
    az group create -l <resource_group_location> -n <resource_group_name>
    ```

1. Cree un almacén de claves. Asegúrese de elegir un nombre de almacén de claves fácil de recordar porque se usará más adelante para hacer referencia a él.

    ```bash
    az keyvault create --name <your_keyvault_name>            \
                      --resource-group <your_resource_group> \
                      --location <location>                  \
                      --enabled-for-deployment true          \
                      --enabled-for-disk-encryption true     \
                      --enabled-for-template-deployment true \
                      --sku standard
    ```

1. Conceda los permisos adecuados a la entidad de servicio creada anteriormente, para que pueda tener acceso a los secretos del almacén de claves. El valor de appId en el código siguiente es el valor *appId* del paso 1 donde creó la entidad de servicio. Es decir, el valor *appId* del paso 1 era *5292398e-XXXX-40ce-XXXX-d49fXXXX9e79*, pero debe usar el valor que se muestra en su salida de terminal.

    ```bash
    az keyvault set-policy --name <your_keyvault_name>   \
                          --secret-permission get list  \
                          --spn <your_sp_appId_created_in_step1>
    ```

1. Ahora puede insertar un secreto en el almacén de claves. Use el nombre de clave *demo-key* y establezca el valor de la clave en *demo-value*:

    ```bash
    az keyvault secret set --name demo-key      \
                           --value demo-value   \
                           --vault-name <your_keyvault_name>  
    ```

Eso es todo. Ahora tiene un almacén de claves en ejecución en Azure con un solo secreto. Ahora puede clonar este repositorio y configurarlo para usar este recurso en la aplicación.

## <a name="get-up-and-running-locally"></a>Preparación y ejecución local

Este ejemplo se basa en una aplicación de ejemplo disponible en GitHub, por lo que vamos a clonarla y a recorrer el código. 

1. Escriba los siguientes comandos para clonar el código en su equipo:

    `git clone https://github.com/Azure-Samples/microprofile-configsource-keyvault.git`

    `cd microprofile-configsource-keyvault`

1. Vaya a *src/main/resources/META-INF/microprofile-config.properties* y cambie las propiedades del archivo *microprofile-config.properties* por los valores de los pasos anteriores.

1. Intente ejecutar el servidor mediante `mvn clean package payara-micro:start`.

1. Intente acceder a [http://localhost:8080/keyvault-configsource/api/config](http://localhost:8080/keyvault-configsource/api/config) en el explorador web. Verá una respuesta sencilla que muestra los valores que se va a leer desde el almacén de claves.

## <a name="summary"></a>Resumen

Esta aplicación de ejemplo combina MicroProfile Config API, Azure Key Vault y la biblioteca de código abierto gratuita [microprofile-config-keyvault](https://github.com/Azure/azure-microprofile/tree/master/microprofile-config-keyvault) para facilitar la inserción de datos de configuración y secretos en nuestros servicios web de MicroProfile.
