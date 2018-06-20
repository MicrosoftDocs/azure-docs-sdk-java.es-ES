---
title: 'Guía para desarrolladores: bibliotecas de administración de Azure para Java'
description: Patrones y conceptos para el uso de bibliotecas de administración de Java para administrar los recursos de nube en Azure.
keywords: Azure, Java, SDK, API, Maven, Gradle, autenticación, active directory, entidad de servicio
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 04/16/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: multiple
ms.assetid: f452468b-7aae-4944-abad-0b1aaf19170d
ms.openlocfilehash: 8b52981ddfaadb7227cea4c7df014011196339cb
ms.sourcegitcommit: 1f6a80e067a8bdbbb4b2da2e2145fda73d5fe65a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/05/2017
ms.locfileid: "26184649"
---
# <a name="patterns-and-best-practices-for-development-with-the-azure-libraries-for-java"></a><span data-ttu-id="238ca-104">Patrones y procedimientos recomendados para desarrollar con las bibliotecas de Azure para Java</span><span class="sxs-lookup"><span data-stu-id="238ca-104">Patterns and best practices for development with the Azure libraries for Java</span></span> 

<span data-ttu-id="238ca-105">En este artículo, se enumeran los patrones y los procedimientos recomendados para usar las bibliotecas de Azure para Java en sus proyectos.</span><span class="sxs-lookup"><span data-stu-id="238ca-105">This article lists a series of patterns and best practices when using the Azure libraries for Java in your projects.</span></span> <span data-ttu-id="238ca-106">Cuando desarrolle, siga estos patrones y directrices para reducir la cantidad de código que tendrá que mantener y facilitar la adición o configuración de recursos adicionales en futuras actualizaciones de las bibliotecas de mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="238ca-106">Develop with these patterns and guidelines to reduce the amount of code to maintain and make it easier to add or configure additional resources in future updates to the management libraries.</span></span>

## <a name="build-resources-through-a-fluent-interface"></a><span data-ttu-id="238ca-107">Creación de recursos a través de una interfaz fluida</span><span class="sxs-lookup"><span data-stu-id="238ca-107">Build resources through a fluent interface</span></span>

<span data-ttu-id="238ca-108">Una interfaz fluida es un patrón que crea objetos mediante una cadena de método que configura correctamente los atributos del objeto.</span><span class="sxs-lookup"><span data-stu-id="238ca-108">A fluent interface is a pattern that creates objects using a method chain that correctly configures the object's attributes.</span></span> <span data-ttu-id="238ca-109">Por ejemplo, para crear una nueva cuenta de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="238ca-109">For example, to create a new Azure Storage account</span></span>

```java
StorageAccount storage = azure.storageAccounts().define(storageAccountName)
    .withRegion(region)
    .withNewResourceGroup(resourceGroup)
    .create();
```

<span data-ttu-id="238ca-110">A medida que avanza a través de la cadena de método, el IDE sugiere el siguiente método al que se llamará en la conversación fluida.</span><span class="sxs-lookup"><span data-stu-id="238ca-110">As you go through the method chain, your IDE suggests the next method to call in the fluent conversation.</span></span>   

![Resultado del comando GIF de IntelliJ trabajando con una cadena fluida](media/intelliJFluent.gif)

<span data-ttu-id="238ca-112">Encadene los métodos sugeridos por el IDE mientras tengan sentido para el recurso de Azure que se está definiendo.</span><span class="sxs-lookup"><span data-stu-id="238ca-112">Chain the methods suggested by the IDE as long as they make sense for the Azure resource being defined.</span></span> <span data-ttu-id="238ca-113">Si omite un método necesario en la cadena, el IDE lo resaltará con un error.</span><span class="sxs-lookup"><span data-stu-id="238ca-113">If you are missing a required method in the chain your IDE will highlight it with an error.</span></span>

## <a name="resource-collections"></a><span data-ttu-id="238ca-114">Colecciones de recursos</span><span class="sxs-lookup"><span data-stu-id="238ca-114">Resource collections</span></span>

<span data-ttu-id="238ca-115">La biblioteca de administración tiene un único punto de entrada a través del objeto de nivel superior `com.microsoft.azure.management.Azure` para crear y actualizar recursos.</span><span class="sxs-lookup"><span data-stu-id="238ca-115">The management library has a single point of entry through the top-level `com.microsoft.azure.management.Azure` object to create and update resources.</span></span> <span data-ttu-id="238ca-116">Seleccione el tipo de recursos con los que desea trabajar; para ello, use los métodos de colección de recursos definidos en el objeto `Azure`.</span><span class="sxs-lookup"><span data-stu-id="238ca-116">Select which type of resources to work with using the resource collection methods defined in the `Azure` object.</span></span> <span data-ttu-id="238ca-117">Por ejemplo, SQL Database:</span><span class="sxs-lookup"><span data-stu-id="238ca-117">For example, SQL Database:</span></span>

```java
SqlServer sqlServer = azure.sqlServers().define(sqlServerName)
    .withRegion(Region.US_EAST)
    .withNewResourceGroup(rgName)
    .withAdministratorLogin(administratorLogin)
    .withAdministratorPassword(administratorPassword)
    .create();
```

## <a name="lists-and-iterations"></a><span data-ttu-id="238ca-118">Listas e iteraciones</span><span class="sxs-lookup"><span data-stu-id="238ca-118">Lists and iterations</span></span>

<span data-ttu-id="238ca-119">Cada colección de recursos tiene un método `list()` que devuelve todas las instancias de ese recurso en la suscripción actual.</span><span class="sxs-lookup"><span data-stu-id="238ca-119">Each resource collection has a `list()` method to return every instance of that resource in your current subscription.</span></span> <span data-ttu-id="238ca-120">Por ejemplo, `azure.sqlServers().list()` devuelve todas las bases de datos SQL de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="238ca-120">For example, `azure.sqlServers().list()` returns all SQL databases in the subscription.</span></span>

<span data-ttu-id="238ca-121">Use el método `listByResourceGroup(String groupname)` para establecer el ámbito de la lista devuelta en un determinado [grupo de recursos de Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups).</span><span class="sxs-lookup"><span data-stu-id="238ca-121">Use the `listByResourceGroup(String groupname)` method to scope the returned List to a specific [Azure resource group](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups).</span></span>  

<span data-ttu-id="238ca-122">Puede buscar y recorrer en iteración la colección `PagedList<T>` devuelta simplemente como lo haría con una colección `List<T>` normal:</span><span class="sxs-lookup"><span data-stu-id="238ca-122">Search and iterate over the returned `PagedList<T>` collection just as you would a normal `List<T>`:</span></span>

```java
PagedList<VirtualMachine> vms = azure.virtualMachines().list();
for (VirtualMachine vm : vms) {
    System.out.println("Found virtual machine with ID " + vm.id());
}
```   

## <a name="collections-returned-from-queries"></a><span data-ttu-id="238ca-123">Colecciones devueltas por las consultas</span><span class="sxs-lookup"><span data-stu-id="238ca-123">Collections returned from queries</span></span>

<span data-ttu-id="238ca-124">Las bibliotecas de administración devuelven tipos de colección específicos a partir de consultas basadas en la estructura de los resultados.</span><span class="sxs-lookup"><span data-stu-id="238ca-124">The management libraries return specific collection types from queries based on the structure of the results.</span></span>

- <span data-ttu-id="238ca-125">`List<T>`: datos sin ordenar que son fáciles de buscar y recorrer en iteración.</span><span class="sxs-lookup"><span data-stu-id="238ca-125">`List<T>`: Unordered data that is easy to search and iterate over.</span></span>
- <span data-ttu-id="238ca-126">`Map<T>`: las asignaciones son pares de clave y valor con claves únicas, pero no necesariamente valores únicos.</span><span class="sxs-lookup"><span data-stu-id="238ca-126">`Map<T>`: Maps are key/value pairs with unique keys, but not necessarily unique values.</span></span> <span data-ttu-id="238ca-127">Un ejemplo de asignación sería la configuración de una aplicación para una aplicación web de App Service.</span><span class="sxs-lookup"><span data-stu-id="238ca-127">An example of a Map would be app settings for an App Service Web App.</span></span>
- <span data-ttu-id="238ca-128">`Set<T>`: los conjuntos tienen claves y valores únicos.</span><span class="sxs-lookup"><span data-stu-id="238ca-128">`Set<T>`: Sets have unique keys and values.</span></span> <span data-ttu-id="238ca-129">Un ejemplo de conjunto serían las redes conectadas a una máquina virtual, que tendría un identificador único (la clave) y una configuración de red única (el valor).</span><span class="sxs-lookup"><span data-stu-id="238ca-129">An example of a Set would be networks attached to a virtual machine, which would have both an unique identifier (the key) and a unique network configuration (the value).</span></span>

## <a name="actionable-verbs"></a><span data-ttu-id="238ca-130">Verbos procesables</span><span class="sxs-lookup"><span data-stu-id="238ca-130">Actionable verbs</span></span>

<span data-ttu-id="238ca-131">Los métodos con verbos en sus nombres tienen acción inmediata en Azure.</span><span class="sxs-lookup"><span data-stu-id="238ca-131">Methods with verbs in their names take immediate action in Azure.</span></span> <span data-ttu-id="238ca-132">Estos métodos funcionan de forma sincrónica y bloquean la ejecución en el subproceso actual hasta que terminan.</span><span class="sxs-lookup"><span data-stu-id="238ca-132">These methods work synchronously and block execution in the current thread until they complete.</span></span> 

| <span data-ttu-id="238ca-133">Verbo</span><span class="sxs-lookup"><span data-stu-id="238ca-133">Verb</span></span>   |  <span data-ttu-id="238ca-134">Ejemplo de uso</span><span class="sxs-lookup"><span data-stu-id="238ca-134">Sample Usage</span></span> |
|--------|---------------|
| <span data-ttu-id="238ca-135">create</span><span class="sxs-lookup"><span data-stu-id="238ca-135">create</span></span> | `azure.virtualMachines().create(listOfVMCreatables)` |
| <span data-ttu-id="238ca-136">apply</span><span class="sxs-lookup"><span data-stu-id="238ca-136">apply</span></span>  | `virtualMachineScaleSet.update().withCapacity(6).apply()` |
| <span data-ttu-id="238ca-137">delete</span><span class="sxs-lookup"><span data-stu-id="238ca-137">delete</span></span> | `azure.disks().deleteById(id)` | 
| <span data-ttu-id="238ca-138">list</span><span class="sxs-lookup"><span data-stu-id="238ca-138">list</span></span>   | `azure.sqlServers().list()` | 
| <span data-ttu-id="238ca-139">get</span><span class="sxs-lookup"><span data-stu-id="238ca-139">get</span></span>    | `VirtualMachine vm  = azure.virtualMachines().getByResourceGroup(group, vmName)` |

>[!NOTE]
> <span data-ttu-id="238ca-140">`define()` y `update()` son verbos, pero no producen bloqueos a menos que vayan seguidos por `create()` o `apply()`.</span><span class="sxs-lookup"><span data-stu-id="238ca-140">`define()` and `update()` are verbs but do not block unless followed by a `create()` or `apply()`.</span></span>
 
<span data-ttu-id="238ca-141">Existen versiones asincrónicas de algunos de estos métodos con el sufijo `Async` mediante las [Extensiones reactivas](https://github.com/ReactiveX/RxJava).</span><span class="sxs-lookup"><span data-stu-id="238ca-141">Asynchronous versions of some of these  methods exist with the `Async` suffix using [Reactive extensions](https://github.com/ReactiveX/RxJava).</span></span> 

<span data-ttu-id="238ca-142">Algunos objetos tienen otros métodos con los que cambian el estado del recurso de Azure.</span><span class="sxs-lookup"><span data-stu-id="238ca-142">Some objects have other methods with that change the state of the resource in Azure.</span></span> <span data-ttu-id="238ca-143">Por ejemplo, `restart()` en una `VirtualMachine`.</span><span class="sxs-lookup"><span data-stu-id="238ca-143">For example, `restart()` on a `VirtualMachine`.</span></span>

```java
VirtualMachine vmToRestart = azure.getVirtualMachines().getById(id);
vmToRestart.restart();
```
<span data-ttu-id="238ca-144">Estos métodos no siempre tienen versiones asincrónicas y bloquearán la ejecución en su subproceso hasta que terminen.</span><span class="sxs-lookup"><span data-stu-id="238ca-144">These methods do not always have asynchronous versions and will block execution on their thread until they complete.</span></span>

<a name="Creatables"></a>

## <a name="lazy-resource-creation"></a><span data-ttu-id="238ca-145">Creación de recursos diferida</span><span class="sxs-lookup"><span data-stu-id="238ca-145">Lazy resource creation</span></span>

<span data-ttu-id="238ca-146">Se produce un problema al crear recursos de Azure cuando un nuevo recurso depende de otro recurso que aún no existe.</span><span class="sxs-lookup"><span data-stu-id="238ca-146">A challenge when creating Azure resources arises when a new resource depends on another resource that doesn't yet exist.</span></span> <span data-ttu-id="238ca-147">Un ejemplo de este escenario sería reservar una dirección IP pública y configurar un disco al crear una nueva máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="238ca-147">An example of this scenario is reserving a public IP address and setting up a disk when creating a new virtual machine.</span></span> <span data-ttu-id="238ca-148">No desea comprobar la reserva de la dirección ni la creación del disco, solo desea asegurarse de que la máquina virtual tiene los recursos cuando se crea.</span><span class="sxs-lookup"><span data-stu-id="238ca-148">You don't want to verify reserving the address or the creating the disk, you just want to ensure the virtual machine has those resources when it is created.</span></span>

<span data-ttu-id="238ca-149">Los objetos `Creatable<T>` le permiten definir recursos de Azure para usar en el código sin tener que esperar a que se creen en su suscripción.</span><span class="sxs-lookup"><span data-stu-id="238ca-149">`Creatable<T>` objects let you define Azure resources for use in your code without waiting around for them to be created in your subscription.</span></span> <span data-ttu-id="238ca-150">Las bibliotecas de administración aplazan la creación de objetos `Creatable<T>` hasta que se necesiten.</span><span class="sxs-lookup"><span data-stu-id="238ca-150">The management libraries defer creating  `Creatable<T>` objects until they are needed.</span></span>

<span data-ttu-id="238ca-151">Puede generar objetos `Creatable<T>` para recursos de Azure con el verbo `define()`:</span><span class="sxs-lookup"><span data-stu-id="238ca-151">Generate `Creatable<T>` objects for Azure resources through the `define()` verb:</span></span>

```java
Creatable<PublicIPAddress> publicIPAddressCreatable = azure.publicIPAddresses().define(publicIPAddressName)
    .withRegion(Region.US_EAST)
    .withNewResourceGroup(rgName);
```

<span data-ttu-id="238ca-152">El recurso de Azure definido por `Creatable<PublicIPAddress>` en este ejemplo aún no existe en la suscripción cuando se ejecuta este código.</span><span class="sxs-lookup"><span data-stu-id="238ca-152">The Azure resource defined by the `Creatable<PublicIPAddress>` in this example does not yet exist in your subscription when this code executes.</span></span>  <span data-ttu-id="238ca-153">Use el objeto `publicIPAddressCreatable` para crear otros recursos de Azure con esta dirección IP.</span><span class="sxs-lookup"><span data-stu-id="238ca-153">Use the `publicIPAddressCreatable` object to create other Azure resources with this IP address.</span></span> 

```java
Creatable<VirtualMachine> vmCreatable = azure.virtualMachines().define("creatableVM")
    .withNewPrimaryPublicIPAddress(publicIPAddressCreatable)
```

<span data-ttu-id="238ca-154">Los recursos `Creatable<T>` se generan en la suscripción cuando cualquier recurso que se define utilizando el objeto se crea en Azure mediante `create()`.</span><span class="sxs-lookup"><span data-stu-id="238ca-154">The `Creatable<T>` resources are generated in your subscription when any resource that is defined using the object is built in Azure using `create()`.</span></span> <span data-ttu-id="238ca-155">Siguiendo con el ejemplo de la máquina virtual y la dirección IP:</span><span class="sxs-lookup"><span data-stu-id="238ca-155">Continuing the IP address and virtual machine example:</span></span>

```java
CreatedResources<VirtualMachine> virtualMachine = azure.virtualMachines().create(vmCreatable);
```

<span data-ttu-id="238ca-156">Al pasar `Creatable<T>` a las llamadas a `create()`, se devuelve un objeto `CreatedResources` en lugar de un objeto de recurso único.</span><span class="sxs-lookup"><span data-stu-id="238ca-156">Passing the `Creatable<T>` to `create()` calls returns a `CreatedResources` object instead of a single resource object.</span></span>  <span data-ttu-id="238ca-157">El objeto `CreatedResources<T>` le permite tener acceso a todos los recursos creados por la llamada a `create()` y no solo al recurso especificado en la llamada.</span><span class="sxs-lookup"><span data-stu-id="238ca-157">The `CreatedResources<T>` object lets you access all resources created by the `create()` call, not just the typed resource in the call.</span></span> <span data-ttu-id="238ca-158">Para tener acceso a la dirección IP pública creada en Azure para la máquina virtual creada en el ejemplo anterior:</span><span class="sxs-lookup"><span data-stu-id="238ca-158">To access the public IP address created in Azure for the virtual machine created in the above example:</span></span>

```java
PublicIPAddress pip = (PublicIPAddress) virtualMachine.createdRelatedResource(publicIPAddressCreatable.key());
```    

## <a name="exception-handling"></a><span data-ttu-id="238ca-159">Control de excepciones</span><span class="sxs-lookup"><span data-stu-id="238ca-159">Exception handling</span></span>

<span data-ttu-id="238ca-160">Las clases de excepción de las bibliotecas de administración extienden `com.microsoft.rest.RestException`.</span><span class="sxs-lookup"><span data-stu-id="238ca-160">The management libraries' Exception classes extend `com.microsoft.rest.RestException`.</span></span> <span data-ttu-id="238ca-161">Puede detectar las excepciones generadas por las bibliotecas de administración con un bloque `catch (RestException exception)` después de la correspondiente instrucción `try`.</span><span class="sxs-lookup"><span data-stu-id="238ca-161">Catch exceptions generated by the management libraries with a `catch (RestException exception)` block after the relevant `try` statement.</span></span>

## <a name="logs-and-trace"></a><span data-ttu-id="238ca-162">Registros y seguimiento</span><span class="sxs-lookup"><span data-stu-id="238ca-162">Logs and trace</span></span>

<span data-ttu-id="238ca-163">Es posible configurar la cantidad de registro de la biblioteca de administración cuando se crea el objeto de punto de entrada `Azure` mediante `withLogLevel()`.</span><span class="sxs-lookup"><span data-stu-id="238ca-163">Configure the amount of logging from the management library when you build the entry point `Azure` object using `withLogLevel()`.</span></span> <span data-ttu-id="238ca-164">Existen los siguientes niveles de seguimiento:</span><span class="sxs-lookup"><span data-stu-id="238ca-164">The following trace levels exist:</span></span>

| <span data-ttu-id="238ca-165">Nivel de seguimiento</span><span class="sxs-lookup"><span data-stu-id="238ca-165">Trace level</span></span> | <span data-ttu-id="238ca-166">Registro habilitado</span><span class="sxs-lookup"><span data-stu-id="238ca-166">Logging enabled</span></span> 
| ------------ | ---------------
| <span data-ttu-id="238ca-167">com.microsoft.rest.LogLevel.NONE</span><span class="sxs-lookup"><span data-stu-id="238ca-167">com.microsoft.rest.LogLevel.NONE</span></span> | <span data-ttu-id="238ca-168">Sin salida</span><span class="sxs-lookup"><span data-stu-id="238ca-168">No output</span></span>
| <span data-ttu-id="238ca-169">com.microsoft.rest.LogLevel.BASIC</span><span class="sxs-lookup"><span data-stu-id="238ca-169">com.microsoft.rest.LogLevel.BASIC</span></span> | <span data-ttu-id="238ca-170">Registra las direcciones URL de las llamadas REST subyacentes, con códigos de respuesta y hora</span><span class="sxs-lookup"><span data-stu-id="238ca-170">Logs the URLs to underlying REST calls, response codes and times</span></span>
| <span data-ttu-id="238ca-171">com.microsoft.rest.LogLevel.BODY</span><span class="sxs-lookup"><span data-stu-id="238ca-171">com.microsoft.rest.LogLevel.BODY</span></span> | <span data-ttu-id="238ca-172">Se registra lo incluido en el nivel BASIC más los cuerpos de solicitud y respuesta de las llamadas REST</span><span class="sxs-lookup"><span data-stu-id="238ca-172">Everything in BASIC plus request and response bodies for the REST calls</span></span>
| <span data-ttu-id="238ca-173">com.microsoft.rest.LogLevel.HEADERS</span><span class="sxs-lookup"><span data-stu-id="238ca-173">com.microsoft.rest.LogLevel.HEADERS</span></span> | <span data-ttu-id="238ca-174">Se registra lo incluido en el nivel BASIC más los encabezados de solicitud y respuesta de las llamadas REST</span><span class="sxs-lookup"><span data-stu-id="238ca-174">Everything in BASIC plus the request and response headers REST calls</span></span>
| <span data-ttu-id="238ca-175">com.microsoft.rest.LogLevel.BODY_AND_HEADERS</span><span class="sxs-lookup"><span data-stu-id="238ca-175">com.microsoft.rest.LogLevel.BODY_AND_HEADERS</span></span> | <span data-ttu-id="238ca-176">Se registra todo lo incluido en los niveles de registro BODY y HEADERS</span><span class="sxs-lookup"><span data-stu-id="238ca-176">Everything in both BODY and HEADERS log level</span></span>

<span data-ttu-id="238ca-177">Puede enlazar una [implementación de registro de SLF4J](https://www.slf4j.org/manual.html) si tiene que registrar la salida en un marco de trabajo de registro como [Log4J 2](https://logging.apache.org/log4j/2.x/).</span><span class="sxs-lookup"><span data-stu-id="238ca-177">Bind a [SLF4J logging implementation](https://www.slf4j.org/manual.html) if you need to log output to a logging framework like [Log4J 2](https://logging.apache.org/log4j/2.x/).</span></span>