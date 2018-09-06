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
# <a name="configure-microprofile-with-azure-key-vault"></a><span data-ttu-id="c508c-103">Configuración de MicroProfile con Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="c508c-103">Configure MicroProfile with Azure Key Vault</span></span>

<span data-ttu-id="c508c-104">Este tutorial mostrará cómo configurar una aplicación de [MicroProfile](http://microprofile.io) para recuperar secretos de [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) mediante [MicroProfile Config API](https://microprofile.io/project/eclipse/microprofile-config) para crear un conexión directa a Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="c508c-104">This tutorial will demonstrate how to configure a [MicroProfile](http://microprofile.io) application to retrieve secrets from [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) using the [MicroProfile Config APIs](https://microprofile.io/project/eclipse/microprofile-config) to create a direct connection to Azure Key Vault.</span></span> <span data-ttu-id="c508c-105">Con MicroProfile Config API, los desarrolladores pueden usar una API estándar para recuperar e insertar datos de configuración en sus microservicios.</span><span class="sxs-lookup"><span data-stu-id="c508c-105">By using the MicroProfile Config APIs, developers benefit from a standard API for retrieving and injecting configuration data into their microservices.</span></span>

<span data-ttu-id="c508c-106">Antes de continuar, vamos a ver rápidamente lo que una combinación de Azure Key Vault y MicroProfile Config API nos permite escribir en nuestro código.</span><span class="sxs-lookup"><span data-stu-id="c508c-106">Before we dive in, lets quickly take a look at what a combination of Azure Key Vault and the MicroProfile Config API enables us to write in our code.</span></span> <span data-ttu-id="c508c-107">Este es un fragmento de código de un campo en una clase que ha sido anotada con `@Inject` y `@ConfigProperty`.</span><span class="sxs-lookup"><span data-stu-id="c508c-107">Here's a code snippet of a field in a class that has been annotated with `@Inject` and `@ConfigProperty`.</span></span> <span data-ttu-id="c508c-108">El valor de `name` especificado en la anotación es el nombre de la propiedad que se va a buscar en Azure Key Vault, y `defaultValue` es el valor en el que se establecerá si no se detecta la clave.</span><span class="sxs-lookup"><span data-stu-id="c508c-108">The `name` specified in the annotation is the name of the property to look up in Azure Key Vault, and the `defaultValue` is what will be set if the key is not discovered.</span></span> <span data-ttu-id="c508c-109">El resultado final es que el valor almacenado en Azure Key Vault, o el valor predeterminado, se insertará automáticamente en el campo en tiempo de ejecución, lo que facilita el trabajo de los desarrolladores que ya no necesitan pasar valores en constructores y métodos setter porque MicroProfile se hace cargo de eso.</span><span class="sxs-lookup"><span data-stu-id="c508c-109">The end result is that the value stored in Azure Key Vault, or the default value, will be injected automatically into the field at runtime, simplifying the life of developers as they no longer need to pass values around in constuctors and setter methods, instead leaving it to MicroProfile to handle.</span></span>

```java
@Inject
@ConfigProperty(name = "key-name", defaultValue = "Unknown")
String keyValue;
```

<span data-ttu-id="c508c-110">También se puede acceder a la configuración de MicroProfile directamente, para solicitar secretos según sea necesario, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c508c-110">It is also possible to access the MicroProfile config directly, to request secrets as necessary, e.g.:</span></span>

```java
public class DemoClass {
    @Inject
    Config config;

    public void method() {
        System.out.println("Hello: " + config.getValue("key-name", String.class));
    }
}
```

<span data-ttu-id="c508c-111">Este ejemplo usa [Payara Micro](https://www.payara.fish/payara_micro) y [MicroProfile](https://microprofile.io/) para crear un pequeño archivo .war de Java que se puede ejecutar localmente en el equipo.</span><span class="sxs-lookup"><span data-stu-id="c508c-111">This sample makes use of [Payara Micro](https://www.payara.fish/payara_micro) and [MicroProfile](https://microprofile.io/) to create a tiny Java war file that can be run locally on your machine.</span></span> <span data-ttu-id="c508c-112">No se muestra cómo incluir el código en un contenedor de Docker ni insertar el código en Azure, pero al final de este tutorial se incluyen vínculos a otros tutoriales útiles que explican esto.</span><span class="sxs-lookup"><span data-stu-id="c508c-112">It does not demonstrate how to dockerise or push the code to Azure, but the links section at the end of this tutorial has links to other useful tutorials that explain this.</span></span>

<span data-ttu-id="c508c-113">Este ejemplo utiliza una biblioteca de código abierto gratuita que crea un origen de configuración (con MicroProfile Config API) para Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="c508c-113">This sample makes use of a free and open source library that creats a config source (using the MicroProfile Config API) for Azure Key Vault.</span></span> <span data-ttu-id="c508c-114">Para obtener más información sobre esta biblioteca y revisar el código, visite la [página de GitHub del proyecto](https://github.com/Azure/azure-microprofile/tree/master/microprofile-config-keyvault).</span><span class="sxs-lookup"><span data-stu-id="c508c-114">You can learn more about this library, and review the code, on the [project GitHub page](https://github.com/Azure/azure-microprofile/tree/master/microprofile-config-keyvault).</span></span> <span data-ttu-id="c508c-115">Con esta biblioteca, el código de este tutorial puede centrarse en la configuración de la biblioteca y en la inserción de claves en el código, y no es necesario escribir ningún código específico de Azure.</span><span class="sxs-lookup"><span data-stu-id="c508c-115">By using this library, the code in this tutorial can simply focus on configuration of the library, followed by injecting keys into your code, and we don't need to write any Azure-specific code.</span></span>

<span data-ttu-id="c508c-116">Estos son los pasos necesarios para ejecutar este código en el equipo local, empezando por la creación de un recurso de Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="c508c-116">Here are the steps required to run this code on your local machine, starting with creating an Azure Key Vault resource.</span></span>

## <a name="creating-an-azure-key-vault-resource"></a><span data-ttu-id="c508c-117">Creación de un recurso de Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="c508c-117">Creating an Azure Key Vault resource</span></span>

<span data-ttu-id="c508c-118">Usaremos la CLI de Azure para crear el recurso de Azure Key Vault y rellenarlo con un secreto.</span><span class="sxs-lookup"><span data-stu-id="c508c-118">We will use the Azure CLI to create the Azure Key Vault resource and populate it with one secret.</span></span>

1. <span data-ttu-id="c508c-119">En primer lugar, creamos una entidad de servicio de Azure.</span><span class="sxs-lookup"><span data-stu-id="c508c-119">Firstly, lets create an Azure service principal.</span></span> <span data-ttu-id="c508c-120">Esto nos proporciona el identificador y la clave de cliente necesarios para tener acceso a Key Vault:</span><span class="sxs-lookup"><span data-stu-id="c508c-120">This will provide us with the client ID and key we need to access Key Vault:</span></span>

```bash
az login
az account set --subscription <subscription_id>

az ad sp create-for-rbac --name <service_principal_name>
```

<span data-ttu-id="c508c-121">Supongamos que usamos `microprofile-keyvault-service-principal` como nombre de la entidad de servicio del paso anterior.</span><span class="sxs-lookup"><span data-stu-id="c508c-121">Lets say we use `microprofile-keyvault-service-principal` for the service principal name in the previous step.</span></span> <span data-ttu-id="c508c-122">La respuesta de Azure para hacer esto tendrá la siguiente forma, ligeramente censurada:</span><span class="sxs-lookup"><span data-stu-id="c508c-122">The response from Azure for doing this will be in the following, slightly censored, form:</span></span>

```json
{
  "appId": "5292398e-XXXX-40ce-XXXX-d49fXXXX9e79",
  "displayName": "microprofile-keyvault-service-principal",
  "name": "http://microprofile-keyvault-service-principal",
  "password": "9b217777-XXXX-4954-XXXX-deafXXXX790a",
  "tenant": "72f988bf-XXXX-41af-XXXX-2d7cd011db47"
}
```

<span data-ttu-id="c508c-123">Hay que resaltar aquí los valores `appID` y `password`; son lo que usaremos más adelante como `client ID` y `key`, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="c508c-123">Of particular note here is the `appID` and `password` values - these are what we will use later on as `client ID` and `key`, respectively.</span></span>

<span data-ttu-id="c508c-124">Ahora que hemos creado una entidad de servicio, podemos crear también un grupo de recursos (si ya tiene uno que desea usar, puede omitir este paso).</span><span class="sxs-lookup"><span data-stu-id="c508c-124">Now that we have created a service principal, we can optionally create a resource group (if you already have one you want to use, you can skip this step).</span></span> <span data-ttu-id="c508c-125">Tenga en cuenta que para obtener la lista de las ubicaciones de los grupos de recursos, puede llamar a `az account list-locations` y usar el valor `name` de esa lista para especificar dónde se debe crear el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="c508c-125">Note that to get a list of resource group locations, you can call `az account list-locations` and use the `name` value from that list to specify where the resource group should be created.</span></span>

```bash
# For this tutorial, the author chose to use `westus`
# and `jg-test` for the resource group name.
az group create -l <resource_group_location> -n <resource_group_name>
```

<span data-ttu-id="c508c-126">Ahora crearemos un recurso de Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="c508c-126">We now create an Azure Key Vault resource.</span></span> <span data-ttu-id="c508c-127">Tenga en cuenta que el nombre del almacén de claves es el que se va a usar para hacer referencia al almacén de claves más adelante, así que elija algo fácil de recordar.</span><span class="sxs-lookup"><span data-stu-id="c508c-127">Note that the Key Vault name is what you will use to reference the key vault later, so choose something memorable.</span></span>

```bash
az keyvault create --name <your_keyvault_name>            \
                   --resource-group <your_resource_group> \
                   --location <location>                  \
                   --enabled-for-deployment true          \
                   --enabled-for-disk-encryption true     \
                   --enabled-for-template-deployment true \
                   --sku standard
```

<span data-ttu-id="c508c-128">También es necesario conceder los permisos adecuados a la entidad de servicio creada anteriormente, para que pueda tener acceso a los secretos de Key Vault.</span><span class="sxs-lookup"><span data-stu-id="c508c-128">We also need to grant the appropriate permissions to the service principal we created earlier, so that it may access the Key Vault secrets.</span></span> <span data-ttu-id="c508c-129">Tenga en cuenta que el valor de appID es el valor `appId` obtenido cuando se creó la entidad de servicio (es decir, `5292398e-XXXX-40ce-XXXX-d49fXXXX9e79`, pero usa el valor de la salida del terminal).</span><span class="sxs-lookup"><span data-stu-id="c508c-129">Note that the appID value is the `appId` value from above where we created the service principal (that is, `5292398e-XXXX-40ce-XXXX-d49fXXXX9e79` - but use the value from your terminal output).</span></span>

```bash
az keyvault set-policy --name <your_keyvault_name>   \
                       --secret-permission get list  \
                       --spn <your_sp_appId_created_in_step1>
```

<span data-ttu-id="c508c-130">Ahora estamos listos para insertar un secreto en Key Vault.</span><span class="sxs-lookup"><span data-stu-id="c508c-130">We are now at the point where we can push a secret into Key Vault.</span></span> <span data-ttu-id="c508c-131">Vamos a usar el nombre de clave `demo-key` y a establecer el valor de la clave en `demo-value`:</span><span class="sxs-lookup"><span data-stu-id="c508c-131">Lets use the key name `demo-key`, and set the value of the key to be `demo-value`:</span></span>

```bash
az keyvault secret set --name demo-key      \
                       --value demo-value   \
                       --vault-name <your_keyvault_name>  
```

<span data-ttu-id="c508c-132">Eso es todo.</span><span class="sxs-lookup"><span data-stu-id="c508c-132">That's it!</span></span> <span data-ttu-id="c508c-133">Ahora tenemos un almacén de claves en ejecución en Azure con un solo secreto.</span><span class="sxs-lookup"><span data-stu-id="c508c-133">We now have Key Vault running in Azure with a single secret.</span></span> <span data-ttu-id="c508c-134">Podemos clonar este repositorio y configurarlo para usar este recurso en nuestra aplicación.</span><span class="sxs-lookup"><span data-stu-id="c508c-134">We can now clone this repo and configure it to use this resource in our app.</span></span>

## <a name="getting-up-and-running-locally"></a><span data-ttu-id="c508c-135">Preparación y ejecución local</span><span class="sxs-lookup"><span data-stu-id="c508c-135">Getting up and running locally</span></span>

<span data-ttu-id="c508c-136">Este ejemplo se basa en una aplicación de ejemplo disponible en GitHub, por lo que vamos a clonarla y a recorrer el código.</span><span class="sxs-lookup"><span data-stu-id="c508c-136">This example is based on a sample application available on GitHub, so we will clone that and then step through the code.</span></span> <span data-ttu-id="c508c-137">Siga estos pasos para obtener el código clonado en su equipo:</span><span class="sxs-lookup"><span data-stu-id="c508c-137">Follow the steps below to get the code cloned onto your machine:</span></span>

1. `git clone https://github.com/Azure-Samples/microprofile-configsource-keyvault.git`

1. `cd microprofile-configsource-keyvault`

1. <span data-ttu-id="c508c-138">Vaya a `src/main/resources/META-INF/microprofile-config.properties` y cambie las propiedades en el archivo microprofile-config.properties con detalles de lo anterior.</span><span class="sxs-lookup"><span data-stu-id="c508c-138">Navigate to `src/main/resources/META-INF/microprofile-config.properties` and change the properties in microprofile-config.properties file with details from above.</span></span>

1. <span data-ttu-id="c508c-139">Intente ejecutar el servidor mediante `mvn clean package payara-micro:start`.</span><span class="sxs-lookup"><span data-stu-id="c508c-139">Try running the server using `mvn clean package payara-micro:start`</span></span>

1. <span data-ttu-id="c508c-140">Intente acceder a [http://localhost:8080/keyvault-configsource/api/config](http://localhost:8080/keyvault-configsource/api/config) en su explorador web. Verá una respuesta sencilla que muestra los valores que se va a leer desde Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="c508c-140">Try accessing [http://localhost:8080/keyvault-configsource/api/config](http://localhost:8080/keyvault-configsource/api/config) in your web browser - you should see a simple response that demonstrates values being read from Azure Key Vault.</span></span>

## <a name="summary"></a><span data-ttu-id="c508c-141">Resumen</span><span class="sxs-lookup"><span data-stu-id="c508c-141">Summary</span></span>

<span data-ttu-id="c508c-142">Esta aplicación de ejemplo reúne MicroProfile Config API, Azure Key Vault y la biblioteca de código abierto gratuita [microprofile-config-keyvault](https://github.com/Azure/azure-microprofile/tree/master/microprofile-config-keyvault) para facilitar la inserción de datos de configuración y secretos en nuestros servicios web de MicroProfile.</span><span class="sxs-lookup"><span data-stu-id="c508c-142">This sample application bakes together the MicroProfile Config API, Azure Key Vault, and the free and open source [microprofile-config-keyvault](https://github.com/Azure/azure-microprofile/tree/master/microprofile-config-keyvault) library to enable easy injection of configuration data and secrets into our MicroProfile web services.</span></span>
