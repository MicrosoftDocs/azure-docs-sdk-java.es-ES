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
# <a name="configure-microprofile-by-using-azure-key-vault"></a><span data-ttu-id="f8e3a-103">Configuración de MicroProfile con Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="f8e3a-103">Configure MicroProfile by using Azure Key Vault</span></span>

<span data-ttu-id="f8e3a-104">En este artículo se muestra cómo configurar una aplicación [MicroProfile](http://microprofile.io) para recuperar secretos desde un [almacén de claves de Azure](https://azure.microsoft.com/services/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="f8e3a-104">This article demonstrates how to configure a [MicroProfile](http://microprofile.io) application to retrieve secrets from an [Azure key vault](https://azure.microsoft.com/services/key-vault/).</span></span> <span data-ttu-id="f8e3a-105">En este proceso, se usa [MicroProfile Config API](https://microprofile.io/project/eclipse/microprofile-config) para crear una conexión directa a un almacén de claves de Azure.</span><span class="sxs-lookup"><span data-stu-id="f8e3a-105">In this process, you use the [MicroProfile Config APIs](https://microprofile.io/project/eclipse/microprofile-config) to create a direct connection to an Azure key vault.</span></span> <span data-ttu-id="f8e3a-106">Con MicroProfile Config API, los desarrolladores pueden usar una API estándar para recuperar e insertar datos de configuración en sus microservicios.</span><span class="sxs-lookup"><span data-stu-id="f8e3a-106">As a developer, by using the MicroProfile Config APIs, you benefit from a standard API for retrieving and injecting configuration data into their microservices.</span></span>

<span data-ttu-id="f8e3a-107">Antes de continuar, eche un vistazo rápido a lo que una combinación de Azure Key Vault y MicroProfile Config API nos permite escribir en nuestro código.</span><span class="sxs-lookup"><span data-stu-id="f8e3a-107">Before you start, take a quick look at what a combination of Azure Key Vault and the MicroProfile Config API enables you to write in your code.</span></span> <span data-ttu-id="f8e3a-108">El siguiente es un fragmento de código de un campo en una clase que ha sido anotada con `@Inject` y `@ConfigProperty`.</span><span class="sxs-lookup"><span data-stu-id="f8e3a-108">The following code snippet is of a field in a class that's annotated with `@Inject` and `@ConfigProperty`.</span></span> <span data-ttu-id="f8e3a-109">El valor *name* especificado en la anotación es el nombre de la propiedad que se va a buscar en Azure Key Vault, y *defaultValue* es el valor en el que se establecerá si no se detecta la clave.</span><span class="sxs-lookup"><span data-stu-id="f8e3a-109">The *name* that's specified in the annotation is the name of the property to look up in your key vault, and the *defaultValue* is what will be set if the key is not discovered.</span></span> <span data-ttu-id="f8e3a-110">El resultado es que el valor que se almacena en el almacén de claves, o el valor predeterminado, se inserta automáticamente en el campo en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="f8e3a-110">The result is that the value that's stored in the key vault, or the default value, is injected automatically into the field at runtime.</span></span> <span data-ttu-id="f8e3a-111">Esta acción simplifica las cosas porque ya no necesita pasar valores en constructores y métodos establecedores.</span><span class="sxs-lookup"><span data-stu-id="f8e3a-111">This action can simplify your life, because you no longer need to pass values around in constructors and setter methods.</span></span> <span data-ttu-id="f8e3a-112">En su lugar, MicroProfile controla esta tarea.</span><span class="sxs-lookup"><span data-stu-id="f8e3a-112">Instead, MicroProfile handles this task.</span></span>

```java
@Inject
@ConfigProperty(name = "key-name", defaultValue = "Unknown")
String keyValue;
```

<span data-ttu-id="f8e3a-113">También se puede acceder a la configuración de MicroProfile directamente para solicitar secretos según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="f8e3a-113">To request secrets, as necessary, you can also access the MicroProfile config directly.</span></span> <span data-ttu-id="f8e3a-114">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="f8e3a-114">For example:</span></span>

```java
public class DemoClass {
    @Inject
    Config config;

    public void method() {
        System.out.println("Hello: " + config.getValue("key-name", String.class));
    }
}
```

<span data-ttu-id="f8e3a-115">Este código de ejemplo usa [Payara Micro](https://www.payara.fish/payara_micro) y [MicroProfile](https://microprofile.io/) para crear un pequeño archivo de requisitos de aplicación web (WAR) de Java que se puede ejecutar localmente en el equipo.</span><span class="sxs-lookup"><span data-stu-id="f8e3a-115">This sample code uses [Payara Micro](https://www.payara.fish/payara_micro) and [MicroProfile](https://microprofile.io/) to create a tiny Java web application requirement (WAR) file that you can run locally on your machine.</span></span> <span data-ttu-id="f8e3a-116">No se muestra cómo incluir el código en un contenedor de Docker ni cómo insertarlo en Azure, pero al final de este artículo se incluyen vínculos a otros tutoriales útiles que explican esto.</span><span class="sxs-lookup"><span data-stu-id="f8e3a-116">It doesn't demonstrate how to Dockerize or push the code to Azure, but the section at the end of this article has links to other useful tutorials that explain this.</span></span>

<span data-ttu-id="f8e3a-117">Este ejemplo utiliza una biblioteca de código abierto gratuita que crea un origen de configuración (con MicroProfile Config API) en el almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="f8e3a-117">The sample uses a free and open source library that creates a config source (using the MicroProfile Config API) in your key vault.</span></span> <span data-ttu-id="f8e3a-118">Para más información sobre esta biblioteca y revisar el código, visite la [página del proyecto en GitHub](https://github.com/Azure/azure-microprofile/tree/master/microprofile-config-keyvault).</span><span class="sxs-lookup"><span data-stu-id="f8e3a-118">To learn more about this library and review the code, see the [project GitHub page](https://github.com/Azure/azure-microprofile/tree/master/microprofile-config-keyvault).</span></span> <span data-ttu-id="f8e3a-119">Si usa la biblioteca, el código de este tutorial puede centrarse simplemente en la configuración de la biblioteca y, a continuación, insertar las claves en el código.</span><span class="sxs-lookup"><span data-stu-id="f8e3a-119">If you use the library, the code in this tutorial can simply focus on the configuration of the library and then inject keys into your code.</span></span> <span data-ttu-id="f8e3a-120">No es necesario escribir ningún código específico de Azure.</span><span class="sxs-lookup"><span data-stu-id="f8e3a-120">You don't need to write any Azure-specific code.</span></span>

<span data-ttu-id="f8e3a-121">Para ejecutar este código en el equipo local, empezando por la creación de un recurso de Azure Key Vault, siga las instrucciones de las secciones siguientes.</span><span class="sxs-lookup"><span data-stu-id="f8e3a-121">To run this code on your local machine, starting with creating a key vault resource, follow the instructions in the next sections.</span></span>

## <a name="create-a-key-vault-resource"></a><span data-ttu-id="f8e3a-122">Creación de un almacén de claves</span><span class="sxs-lookup"><span data-stu-id="f8e3a-122">Create a key vault resource</span></span>

<span data-ttu-id="f8e3a-123">En esta sección, usaremos la CLI de Azure para crear el recurso de Azure Key Vault y rellenarlo con un secreto.</span><span class="sxs-lookup"><span data-stu-id="f8e3a-123">In this section, you use the Azure CLI to create a key vault resource and populate it with one secret.</span></span>

1. <span data-ttu-id="f8e3a-124">Cree una entidad de servicio de Azure.</span><span class="sxs-lookup"><span data-stu-id="f8e3a-124">Create an Azure service principal.</span></span> <span data-ttu-id="f8e3a-125">En este paso se obtiene el identificador de cliente y la clave que necesita para tener acceso a su almacén de claves:</span><span class="sxs-lookup"><span data-stu-id="f8e3a-125">This step gives you the client ID and key that you need to access your key vault:</span></span>

    ```bash
    az login
    az account set --subscription <subscription_id>

    az ad sp create-for-rbac --name <service_principal_name>
    ```

    <span data-ttu-id="f8e3a-126">Vamos a usar *microprofile-keyvault-service-principal* para reemplazar *\<service_principal_name>* en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="f8e3a-126">Let's use *microprofile-keyvault-service-principal* to replace *\<service_principal_name>* in the preceding step.</span></span> <span data-ttu-id="f8e3a-127">La respuesta de Azure será similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="f8e3a-127">The response from Azure would be similar to the following:</span></span>

    ```json
    {
      "appId": "5292398e-XXXX-40ce-XXXX-d49fXXXX9e79",
      "displayName": "microprofile-keyvault-service-principal",
      "name": "http://microprofile-keyvault-service-principal",
      "password": "9b217777-XXXX-4954-XXXX-deafXXXX790a",
      "tenant": "72f988bf-XXXX-41af-XXXX-2d7cd011db47"
    }
    ```

    <span data-ttu-id="f8e3a-128">Hay que resaltar aquí los valores de *appId* y *contraseña*.</span><span class="sxs-lookup"><span data-stu-id="f8e3a-128">Of particular note here are the *appId* and *password* values.</span></span> <span data-ttu-id="f8e3a-129">Se usarán más adelante en este artículo como *identificador de cliente* y *clave*.</span><span class="sxs-lookup"><span data-stu-id="f8e3a-129">You'll use them later in this article as *client ID* and *key*.</span></span>

1. <span data-ttu-id="f8e3a-130">(Opcional) Ahora que ha creado una entidad de servicio, puede crear un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="f8e3a-130">(Optional) Now that you've created a service principal, you can create a resource group.</span></span> <span data-ttu-id="f8e3a-131">Puede omitir este paso si ya tiene un grupo de recursos que le gustaría usar.</span><span class="sxs-lookup"><span data-stu-id="f8e3a-131">If you already have a resource group that you want to use, you can skip this step.</span></span> <span data-ttu-id="f8e3a-132">Para obtener la lista de las ubicaciones de los grupos de recursos, puede llamar a `az account list-locations` y usar el valor *name* de esa lista para especificar dónde se debe crear el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="f8e3a-132">To get a list of resource group locations, you can call `az account list-locations` and use the *name* value from that list to specify where the resource group should be created.</span></span>

    ```bash
    # In this tutorial, "westus" is the resource group location
    # and "jg-test" is the resource group name.
    az group create -l <resource_group_location> -n <resource_group_name>
    ```

1. <span data-ttu-id="f8e3a-133">Cree un almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="f8e3a-133">Create a key vault resource.</span></span> <span data-ttu-id="f8e3a-134">Asegúrese de elegir un nombre de almacén de claves fácil de recordar porque se usará más adelante para hacer referencia a él.</span><span class="sxs-lookup"><span data-stu-id="f8e3a-134">You'll use your key vault name to refer to the key vault later, so be sure to choose a memorable name.</span></span>

    ```bash
    az keyvault create --name <your_keyvault_name>            \
                      --resource-group <your_resource_group> \
                      --location <location>                  \
                      --enabled-for-deployment true          \
                      --enabled-for-disk-encryption true     \
                      --enabled-for-template-deployment true \
                      --sku standard
    ```

1. <span data-ttu-id="f8e3a-135">Conceda los permisos adecuados a la entidad de servicio creada anteriormente, para que pueda tener acceso a los secretos del almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="f8e3a-135">Grant the appropriate permissions to the service principal that you created earlier, so that it can access the key vault secrets.</span></span> <span data-ttu-id="f8e3a-136">El valor de appId en el código siguiente es el valor *appId* del paso 1 donde creó la entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="f8e3a-136">The appId value in the following code is the *appId* value from step 1, where you created the service principal.</span></span> <span data-ttu-id="f8e3a-137">Es decir, el valor *appId* del paso 1 era *5292398e-XXXX-40ce-XXXX-d49fXXXX9e79*, pero debe usar el valor que se muestra en su salida de terminal.</span><span class="sxs-lookup"><span data-stu-id="f8e3a-137">That is, the *appId* in step 1 was *5292398e-XXXX-40ce-XXXX-d49fXXXX9e79*, but you should use the value from your own terminal output.</span></span>

    ```bash
    az keyvault set-policy --name <your_keyvault_name>   \
                          --secret-permission get list  \
                          --spn <your_sp_appId_created_in_step1>
    ```

1. <span data-ttu-id="f8e3a-138">Ahora puede insertar un secreto en el almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="f8e3a-138">Now you can push a secret into your key vault.</span></span> <span data-ttu-id="f8e3a-139">Use el nombre de clave *demo-key* y establezca el valor de la clave en *demo-value*:</span><span class="sxs-lookup"><span data-stu-id="f8e3a-139">Use the key name *demo-key*, and set the value of the key to *demo-value*:</span></span>

    ```bash
    az keyvault secret set --name demo-key      \
                           --value demo-value   \
                           --vault-name <your_keyvault_name>  
    ```

<span data-ttu-id="f8e3a-140">Eso es todo.</span><span class="sxs-lookup"><span data-stu-id="f8e3a-140">That's it!</span></span> <span data-ttu-id="f8e3a-141">Ahora tiene un almacén de claves en ejecución en Azure con un solo secreto.</span><span class="sxs-lookup"><span data-stu-id="f8e3a-141">You now have a key vault running in Azure with a single secret.</span></span> <span data-ttu-id="f8e3a-142">Ahora puede clonar este repositorio y configurarlo para usar este recurso en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f8e3a-142">You can now clone this repo and configure it to use this resource in your app.</span></span>

## <a name="get-up-and-running-locally"></a><span data-ttu-id="f8e3a-143">Preparación y ejecución local</span><span class="sxs-lookup"><span data-stu-id="f8e3a-143">Get up and running locally</span></span>

<span data-ttu-id="f8e3a-144">Este ejemplo se basa en una aplicación de ejemplo disponible en GitHub, por lo que vamos a clonarla y a recorrer el código.</span><span class="sxs-lookup"><span data-stu-id="f8e3a-144">This example is based on a sample application that's available on GitHub, so you'll clone that application and then step through the code.</span></span> 

1. <span data-ttu-id="f8e3a-145">Escriba los siguientes comandos para clonar el código en su equipo:</span><span class="sxs-lookup"><span data-stu-id="f8e3a-145">Clone the code onto your machine by entering the following commands:</span></span>

    `git clone https://github.com/Azure-Samples/microprofile-configsource-keyvault.git`

    `cd microprofile-configsource-keyvault`

1. <span data-ttu-id="f8e3a-146">Vaya a *src/main/resources/META-INF/microprofile-config.properties* y cambie las propiedades del archivo *microprofile-config.properties* por los valores de los pasos anteriores.</span><span class="sxs-lookup"><span data-stu-id="f8e3a-146">Go to *src/main/resources/META-INF/microprofile-config.properties*, and then change the properties in the *microprofile-config.properties* file by using the values from the previous steps.</span></span>

1. <span data-ttu-id="f8e3a-147">Intente ejecutar el servidor mediante `mvn clean package payara-micro:start`.</span><span class="sxs-lookup"><span data-stu-id="f8e3a-147">Try running the server by using `mvn clean package payara-micro:start`.</span></span>

1. <span data-ttu-id="f8e3a-148">Intente acceder a [http://localhost:8080/keyvault-configsource/api/config](http://localhost:8080/keyvault-configsource/api/config) en el explorador web.</span><span class="sxs-lookup"><span data-stu-id="f8e3a-148">Try accessing [http://localhost:8080/keyvault-configsource/api/config](http://localhost:8080/keyvault-configsource/api/config) in your web browser.</span></span> <span data-ttu-id="f8e3a-149">Verá una respuesta sencilla que muestra los valores que se va a leer desde el almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="f8e3a-149">You should see a simple response that demonstrates values that are being read from your key vault.</span></span>

## <a name="summary"></a><span data-ttu-id="f8e3a-150">Resumen</span><span class="sxs-lookup"><span data-stu-id="f8e3a-150">Summary</span></span>

<span data-ttu-id="f8e3a-151">Esta aplicación de ejemplo combina MicroProfile Config API, Azure Key Vault y la biblioteca de código abierto gratuita [microprofile-config-keyvault](https://github.com/Azure/azure-microprofile/tree/master/microprofile-config-keyvault) para facilitar la inserción de datos de configuración y secretos en nuestros servicios web de MicroProfile.</span><span class="sxs-lookup"><span data-stu-id="f8e3a-151">This sample application combines the MicroProfile Config API, Azure Key Vault, and the free and open source [microprofile-config-keyvault](https://github.com/Azure/azure-microprofile/tree/master/microprofile-config-keyvault) library to enable easy injection of configuration data and secrets into your MicroProfile web services.</span></span>
