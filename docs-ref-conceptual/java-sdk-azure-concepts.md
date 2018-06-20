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
# <a name="patterns-and-best-practices-for-development-with-the-azure-libraries-for-java"></a>Patrones y procedimientos recomendados para desarrollar con las bibliotecas de Azure para Java 

En este artículo, se enumeran los patrones y los procedimientos recomendados para usar las bibliotecas de Azure para Java en sus proyectos. Cuando desarrolle, siga estos patrones y directrices para reducir la cantidad de código que tendrá que mantener y facilitar la adición o configuración de recursos adicionales en futuras actualizaciones de las bibliotecas de mantenimiento.

## <a name="build-resources-through-a-fluent-interface"></a>Creación de recursos a través de una interfaz fluida

Una interfaz fluida es un patrón que crea objetos mediante una cadena de método que configura correctamente los atributos del objeto. Por ejemplo, para crear una nueva cuenta de Azure Storage

```java
StorageAccount storage = azure.storageAccounts().define(storageAccountName)
    .withRegion(region)
    .withNewResourceGroup(resourceGroup)
    .create();
```

A medida que avanza a través de la cadena de método, el IDE sugiere el siguiente método al que se llamará en la conversación fluida.   

![Resultado del comando GIF de IntelliJ trabajando con una cadena fluida](media/intelliJFluent.gif)

Encadene los métodos sugeridos por el IDE mientras tengan sentido para el recurso de Azure que se está definiendo. Si omite un método necesario en la cadena, el IDE lo resaltará con un error.

## <a name="resource-collections"></a>Colecciones de recursos

La biblioteca de administración tiene un único punto de entrada a través del objeto de nivel superior `com.microsoft.azure.management.Azure` para crear y actualizar recursos. Seleccione el tipo de recursos con los que desea trabajar; para ello, use los métodos de colección de recursos definidos en el objeto `Azure`. Por ejemplo, SQL Database:

```java
SqlServer sqlServer = azure.sqlServers().define(sqlServerName)
    .withRegion(Region.US_EAST)
    .withNewResourceGroup(rgName)
    .withAdministratorLogin(administratorLogin)
    .withAdministratorPassword(administratorPassword)
    .create();
```

## <a name="lists-and-iterations"></a>Listas e iteraciones

Cada colección de recursos tiene un método `list()` que devuelve todas las instancias de ese recurso en la suscripción actual. Por ejemplo, `azure.sqlServers().list()` devuelve todas las bases de datos SQL de la suscripción.

Use el método `listByResourceGroup(String groupname)` para establecer el ámbito de la lista devuelta en un determinado [grupo de recursos de Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups).  

Puede buscar y recorrer en iteración la colección `PagedList<T>` devuelta simplemente como lo haría con una colección `List<T>` normal:

```java
PagedList<VirtualMachine> vms = azure.virtualMachines().list();
for (VirtualMachine vm : vms) {
    System.out.println("Found virtual machine with ID " + vm.id());
}
```   

## <a name="collections-returned-from-queries"></a>Colecciones devueltas por las consultas

Las bibliotecas de administración devuelven tipos de colección específicos a partir de consultas basadas en la estructura de los resultados.

- `List<T>`: datos sin ordenar que son fáciles de buscar y recorrer en iteración.
- `Map<T>`: las asignaciones son pares de clave y valor con claves únicas, pero no necesariamente valores únicos. Un ejemplo de asignación sería la configuración de una aplicación para una aplicación web de App Service.
- `Set<T>`: los conjuntos tienen claves y valores únicos. Un ejemplo de conjunto serían las redes conectadas a una máquina virtual, que tendría un identificador único (la clave) y una configuración de red única (el valor).

## <a name="actionable-verbs"></a>Verbos procesables

Los métodos con verbos en sus nombres tienen acción inmediata en Azure. Estos métodos funcionan de forma sincrónica y bloquean la ejecución en el subproceso actual hasta que terminan. 

| Verbo   |  Ejemplo de uso |
|--------|---------------|
| create | `azure.virtualMachines().create(listOfVMCreatables)` |
| apply  | `virtualMachineScaleSet.update().withCapacity(6).apply()` |
| delete | `azure.disks().deleteById(id)` | 
| list   | `azure.sqlServers().list()` | 
| get    | `VirtualMachine vm  = azure.virtualMachines().getByResourceGroup(group, vmName)` |

>[!NOTE]
> `define()` y `update()` son verbos, pero no producen bloqueos a menos que vayan seguidos por `create()` o `apply()`.
 
Existen versiones asincrónicas de algunos de estos métodos con el sufijo `Async` mediante las [Extensiones reactivas](https://github.com/ReactiveX/RxJava). 

Algunos objetos tienen otros métodos con los que cambian el estado del recurso de Azure. Por ejemplo, `restart()` en una `VirtualMachine`.

```java
VirtualMachine vmToRestart = azure.getVirtualMachines().getById(id);
vmToRestart.restart();
```
Estos métodos no siempre tienen versiones asincrónicas y bloquearán la ejecución en su subproceso hasta que terminen.

<a name="Creatables"></a>

## <a name="lazy-resource-creation"></a>Creación de recursos diferida

Se produce un problema al crear recursos de Azure cuando un nuevo recurso depende de otro recurso que aún no existe. Un ejemplo de este escenario sería reservar una dirección IP pública y configurar un disco al crear una nueva máquina virtual. No desea comprobar la reserva de la dirección ni la creación del disco, solo desea asegurarse de que la máquina virtual tiene los recursos cuando se crea.

Los objetos `Creatable<T>` le permiten definir recursos de Azure para usar en el código sin tener que esperar a que se creen en su suscripción. Las bibliotecas de administración aplazan la creación de objetos `Creatable<T>` hasta que se necesiten.

Puede generar objetos `Creatable<T>` para recursos de Azure con el verbo `define()`:

```java
Creatable<PublicIPAddress> publicIPAddressCreatable = azure.publicIPAddresses().define(publicIPAddressName)
    .withRegion(Region.US_EAST)
    .withNewResourceGroup(rgName);
```

El recurso de Azure definido por `Creatable<PublicIPAddress>` en este ejemplo aún no existe en la suscripción cuando se ejecuta este código.  Use el objeto `publicIPAddressCreatable` para crear otros recursos de Azure con esta dirección IP. 

```java
Creatable<VirtualMachine> vmCreatable = azure.virtualMachines().define("creatableVM")
    .withNewPrimaryPublicIPAddress(publicIPAddressCreatable)
```

Los recursos `Creatable<T>` se generan en la suscripción cuando cualquier recurso que se define utilizando el objeto se crea en Azure mediante `create()`. Siguiendo con el ejemplo de la máquina virtual y la dirección IP:

```java
CreatedResources<VirtualMachine> virtualMachine = azure.virtualMachines().create(vmCreatable);
```

Al pasar `Creatable<T>` a las llamadas a `create()`, se devuelve un objeto `CreatedResources` en lugar de un objeto de recurso único.  El objeto `CreatedResources<T>` le permite tener acceso a todos los recursos creados por la llamada a `create()` y no solo al recurso especificado en la llamada. Para tener acceso a la dirección IP pública creada en Azure para la máquina virtual creada en el ejemplo anterior:

```java
PublicIPAddress pip = (PublicIPAddress) virtualMachine.createdRelatedResource(publicIPAddressCreatable.key());
```    

## <a name="exception-handling"></a>Control de excepciones

Las clases de excepción de las bibliotecas de administración extienden `com.microsoft.rest.RestException`. Puede detectar las excepciones generadas por las bibliotecas de administración con un bloque `catch (RestException exception)` después de la correspondiente instrucción `try`.

## <a name="logs-and-trace"></a>Registros y seguimiento

Es posible configurar la cantidad de registro de la biblioteca de administración cuando se crea el objeto de punto de entrada `Azure` mediante `withLogLevel()`. Existen los siguientes niveles de seguimiento:

| Nivel de seguimiento | Registro habilitado 
| ------------ | ---------------
| com.microsoft.rest.LogLevel.NONE | Sin salida
| com.microsoft.rest.LogLevel.BASIC | Registra las direcciones URL de las llamadas REST subyacentes, con códigos de respuesta y hora
| com.microsoft.rest.LogLevel.BODY | Se registra lo incluido en el nivel BASIC más los cuerpos de solicitud y respuesta de las llamadas REST
| com.microsoft.rest.LogLevel.HEADERS | Se registra lo incluido en el nivel BASIC más los encabezados de solicitud y respuesta de las llamadas REST
| com.microsoft.rest.LogLevel.BODY_AND_HEADERS | Se registra todo lo incluido en los niveles de registro BODY y HEADERS

Puede enlazar una [implementación de registro de SLF4J](https://www.slf4j.org/manual.html) si tiene que registrar la salida en un marco de trabajo de registro como [Log4J 2](https://logging.apache.org/log4j/2.x/).