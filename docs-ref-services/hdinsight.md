---
title: SDK de Azure HDInsight para Java
description: Referencia del SDK de Azure HDInsight para Java. El SDK de HDInsight para Java proporciona clases y métodos que permiten administrar los clústeres de HDInsight.
author: tylerfox
ms.author: tyfox
ms.reviewer: jasonh
ms.service: hdinsight
ms.topic: reference
ms.devlang: java
ms.date: 11/21/2018
ms.openlocfilehash: 96ecbedc90706775a80b97c42f0d55a46a45b8ac
ms.sourcegitcommit: 8d0c59ae7c91adbb9be3c3e6d4a3429ffe51519d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/27/2018
ms.locfileid: "52338689"
---
# <a name="hdinsight-java-management-sdk-preview"></a>SDK de administración de HDInsight para Java (versión preliminar)

## <a name="overview"></a>Información general

El SDK de HDInsight para Java proporciona clases y métodos que permiten administrar los clústeres de HDInsight. Incluye operaciones para crear, eliminar, actualizar, enumerar, cambiar tamaño, ejecutar acciones de script, supervisar y obtener propiedades de clústeres de HDInsight, entre otras.

## <a name="prerequisites"></a>Requisitos previos

* Una cuenta de Azure. Si no tiene una, [obtenga la versión de evaluación gratuita](https://azure.microsoft.com/free/).
* Un kit de desarrollo de Java (JDK) admitido Para más información sobre los JDK disponibles para desarrollar en Azure, consulte <https://aka.ms/azure-jdks>.
* [Maven](https://maven.apache.org/install.html)

## <a name="sdk-installation"></a>Instalación del SDK

El SDK de HDInsight para Java está disponible con Maven [aquí](https://mvnrepository.com/artifact/com.microsoft.azure.hdinsight.v2018_06_01_preview/azure-mgmt-hdinsight). Agregue la siguiente dependencia en pom.xml:

```
<dependency>
    <groupId>com.microsoft.azure.hdinsight.v2018_06_01_preview</groupId>
    <artifactId>azure-mgmt-hdinsight</artifactId>
    <version>1.0.0-beta-1</version>
</dependency>
```

También debe agregar las siguientes dependencias al archivo pom.xml:

* [Biblioteca de autenticación de cliente de Azure:](https://mvnrepository.com/artifact/com.microsoft.azure/azure-client-authentication/1.6.2)
  ```
  <dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-client-authentication</artifactId>
    <version>1.6.2</version>
    <scope>test</scope>
  </dependency>
  ```

* [Runtime de cliente de Java de Azure para ARM:](https://mvnrepository.com/artifact/com.microsoft.azure/azure-arm-client-runtime/1.6.2)
  ```
  <dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-arm-client-runtime</artifactId>
    <version>1.6.2</version>
  </dependency>
  ```

## <a name="authentication"></a>Autenticación

En primer lugar, el SDK necesita autenticarse en su suscripción de Azure.  Siga el ejemplo siguiente para crear una entidad de servicio y usarla para la autenticación. Una vez hecho esto, tendrá una instancia de `HDInsightManagementClientImpl`, que contiene muchos métodos que pueden usarse para realizar operaciones de administración (se describen en las secciones siguientes).

> [!NOTE]
> Además del siguiente ejemplo, hay otras maneras de autenticar que podrían ser más adecuadas para sus necesidades. Todos los métodos se describen aquí: [Autenticación con las bibliotecas de administración de Azure para Java](https://docs.microsoft.com/en-us/java/azure/java-sdk-azure-authenticate?view=azure-java-stable)

### <a name="authentication-example-using-a-service-principal"></a>Ejemplo de autenticación con una entidad de servicio

En primer lugar, inicie sesión en [Azure Cloud Shell](https://shell.azure.com/bash). Compruebe que está usando la suscripción en la que desea crear la entidad de servicio. 

```azurecli-interactive
az account show
```

La información de la suscripción se muestra en formato JSON.

```json
{
  "environmentName": "AzureCloud",
  "id": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "isDefault": true,
  "name": "XXXXXXX",
  "state": "Enabled",
  "tenantId": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "user": {
    "cloudShellID": true,
    "name": "XXX@XXX.XXX",
    "type": "user"
  }
}
```

Si no ha iniciado sesión en la suscripción correcta, ejecute lo siguiente para seleccionar la correcta: 
```azurecli-interactive
az account set -s <name or ID of subscription>
```

> [!IMPORTANT]
> Si aún no ha registrado el proveedor de recursos de HDInsight con otro método (por ejemplo, creando un clúster de HDInsight mediante Azure Portal), deberá hacerlo una vez antes de poder realizar la autenticación. Se puede hacer desde [Azure Cloud Shell](https://shell.azure.com/bash), con el siguiente comando:
>```azurecli-interactive
>az provider register --namespace Microsoft.HDInsight
>```

A continuación, elija un nombre para la entidad de servicio y créela con el siguiente comando:

```azurecli-interactive
az ad sp create-for-rbac --name <Service Principal Name> --sdk-auth
```

La información de la entidad de servicio se muestra con formato JSON.

```json
{
  "clientId": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "clientSecret": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "subscriptionId": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "tenantId": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "activeDirectoryEndpointUrl": "https://login.microsoftonline.com",
  "resourceManagerEndpointUrl": "https://management.azure.com/",
  "activeDirectoryGraphResourceId": "https://graph.windows.net/",
  "sqlManagementEndpointUrl": "https://management.core.windows.net:8443/",
  "galleryEndpointUrl": "https://gallery.azure.com/",
  "managementEndpointUrl": "https://management.core.windows.net/"
}
```
Copie el siguiente fragmento de código y rellene `TENANT_ID`, `CLIENT_ID`, `CLIENT_SECRET` y `SUBSCRIPTION_ID` con las cadenas del código JSON que se devolvió después de ejecutar el comando para crear la entidad de servicio.

```java
import com.microsoft.azure.management.hdinsight.v2018_06_01_preview.*;
import com.microsoft.azure.management.hdinsight.v2018_06_01_preview.implementation.HDInsightManagementClientImpl;

public class Main {
    public static void main (String[] args) {

        // Tenant ID for your Azure Subscription
        String TENANT_ID = "";
        // Your Service Principal App Client ID
        String CLIENT_ID = "";
        // Your Service Principal Client Secret
        String CLIENT_SECRET = "";
        // Azure Subscription ID
        String SUBSCRIPTION_ID = "";

        ApplicationTokenCredentials credentials = new ApplicationTokenCredentials(
                CLIENT_ID,
                TENANT_ID,
                CLIENT_SECRET,
                AzureEnvironment.AZURE);

        HDInsightManagementClientImpl client = new HDInsightManagementClientImpl(credentials);
```


## <a name="cluster-management"></a>Administración de clústeres

> [!NOTE]
> En esta sección se da por supuesto que ya ha autenticado y construido una instancia de `HDInsightManagementClientImpl`, y que la ha almacenado en una variable llamada `client`. En la sección Autenticación anterior encontrará las instrucciones para autenticarse y obtener un `HDInsightManagementClientImpl`.

### <a name="create-a-cluster"></a>Creación de un clúster

Para crear un nuevo clúster, se puede llamar a `client.clusters().create()`.

#### <a name="example"></a>Ejemplo

En este ejemplo se muestra cómo crear un clúster de Spark con dos nodos principales y un nodo de trabajo.

> [!NOTE]
> En primer lugar debe crear un grupo de recursos y la cuenta de almacenamiento, tal y como se explica más adelante. Si ya los ha creado, puede omitir estos pasos.

##### <a name="creating-a-resource-group"></a>Creación de un grupo de recursos

Puede crear un grupo de recursos con [Azure Cloud Shell](https://shell.azure.com/bash), con el siguiente comando:
```azurecli-interactive
az group create -l <Region Name (i.e. eastus)> --n <Resource Group Name>
```
##### <a name="creating-a-storage-account"></a>Creación de una cuenta de almacenamiento

Puede crear una cuenta de almacenamiento con [Azure Cloud Shell](https://shell.azure.com/bash), con el siguiente comando:
```azurecli-interactive
az storage account create -n <Storage Account Name> -g <Existing Resource Group Name> -l <Region Name (i.e. eastus)> --sku <SKU i.e. Standard_LRS>
```
Ahora, ejecute el siguiente comando para obtener la clave de la cuenta de almacenamiento (que necesitará para crear un clúster):
```azurecli-interactive
az storage account keys list -n <Storage Account Name>
```
---
El siguiente fragmento de código de Java crea un clúster de Spark con dos nodos principales y un nodo de trabajo. Rellene las variables en blanco tal y como se explica en los comentarios y no dude en cambiar otros parámetros para que se adapten a sus necesidades específicas.

```java
// The name for the cluster you are creating
String clusterName = "";
// The name of your existing Resource Group
String resourceGroupName = "";
// Choose a username
String username = "";
// Choose a password
String password = "";
// Replace <> with the name of your storage account
String storageAccount = "<>.blob.core.windows.net";
// Storage account key you obtained above
String storageAccountKey = "";
// Choose a region
String location = "";
String container = "default";

HashMap<String, HashMap<String, String>> configurations = new HashMap<String, HashMap<String, String>>();
        HashMap<String, String> gateway = new HashMap<String, String>();
        gateway.put("restAuthCredential.enabled_credential", "True");
        gateway.put("restAuthCredential.username", username);
        gateway.put("restAuthCredential.password", password);
        configurations.put("gateway", gateway);

        ClusterCreateParametersExtended parameters = new ClusterCreateParametersExtended()
            .withLocation(location)
            .withTags(Collections.EMPTY_MAP)
            .withProperties(
                new ClusterCreateProperties()
                    .withClusterVersion("3.6")
                    .withOsType(OSType.LINUX)
                    .withClusterDefinition(new ClusterDefinition()
                            .withKind("spark")
                            .withConfigurations(configurations)
                    )
                    .withTier(Tier.STANDARD)
                    .withComputeProfile(new ComputeProfile()
                        .withRoles(List.of(
                            new Role()
                                .withName("headnode")
                                .withTargetInstanceCount(2)
                                .withHardwareProfile(new HardwareProfile()
                                    .withVmSize("Large")
                                )
                                .withOsProfile(new OsProfile()
                                    .withLinuxOperatingSystemProfile(new LinuxOperatingSystemProfile()
                                            .withUsername(username)
                                            .withPassword(password)
                                    )
                                ),
                            new Role()
                                    .withName("workernode")
                                    .withTargetInstanceCount(1)
                                    .withHardwareProfile(new HardwareProfile()
                                        .withVmSize("Large")
                                    )
                                    .withOsProfile(new OsProfile()
                                        .withLinuxOperatingSystemProfile(new LinuxOperatingSystemProfile()
                                            .withUsername(username)
                                            .withPassword(password)
                                        )
                                    )
                        ))
                    )
                    .withStorageProfile(new StorageProfile()
                        .withStorageaccounts(List.of(
                                new StorageAccount()
                                    .withName(storageAccount)
                                    .withKey(storageAccountKey)
                                    .withContainer(container)
                                    .withIsDefault(true)
                        ))
                    )
            );
        client.clusters().create(resourceGroupName, clusterName, parameters);
```

### <a name="get-cluster-details"></a>Obtención de los detalles del clúster

Para obtener las propiedades de un clúster determinado:

```java
client.clusters.getByResourceGroup("<Resource Group Name>", "<Cluster Name>");
```

#### <a name="example"></a>Ejemplo

Puede usar `get` para confirmar que ha creado correctamente el clúster.

```java
ClusterInner cluster = client.clusters().getByResourceGroup("<Resource Group Name>", "<Cluster Name>");
System.out.println(cluster.name()); //Prints the name of the cluster
System.out.println(cluster.id()); //Prints the resource Id of the cluster
```

La salida debe ser similar a la siguiente:

```
<Cluster Name>
/subscriptions/XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX/resourceGroups/<Resource Group Name>/providers/Microsoft.HDInsight/clusters/<Cluster Name>
```

### <a name="list-clusters"></a>Lista de clústeres

#### <a name="list-clusters-under-the-subscription"></a>Lista de clústeres de la suscripción

```java
client.clusters.list();
```
#### <a name="list-clusters-by-resource-group"></a>Lista de clústeres por grupo de recursos

```java
client.clusters.listByResourceGroup("<Resource Group Name>");
```
> [!NOTE]
> Tanto `List()` como `ListByResourceGroup()` devuelven un objeto `PagedList<ClusterInner>`. Una llamada a `loadNext()` devuelve una lista de clústeres en esa página y hace avanzar el objeto `ClusterPaged` a la página siguiente. Esto se puede repetir hasta que `hasNextPage()` devuelva `false`, que indica que no existen más páginas.

#### <a name="example"></a>Ejemplo

El ejemplo siguiente imprime las propiedades de todos los clústeres de la suscripción actual:

```java
PagedList<ClusterInner> clusterPages = client.clusters().list();
while (true) {
    for (ClusterInner cluster : clusterPages.currentPage().items()) {
        System.out.println(cluster.name());
    }
    if (clusterPages.hasNextPage()) {
        clusterPages.loadNextPage();
    } else {
        break;
    }
}
```

### <a name="delete-a-cluster"></a>Eliminación de un clúster

Para eliminar un clúster:

```java
client.clusters.delete("<Resource Group Name>", "<Cluster Name>");
```

### <a name="update-cluster-tags"></a>Actualización de las etiquetas del clúster

Puede actualizar las etiquetas de un clúster determinado de este modo:

```java
client.clusters.update("<Resource Group Name>", "<Cluster Name>", <Map<String,String> of Tags>);
```

### <a name="resize-cluster"></a>Cambio del tamaño de clúster

Para cambiar el tamaño de un número de nodos de trabajo de un clúster determinado, puede especificar un nuevo tamaño como sigue:

```java
client.clusters.resize("<Resource Group Name>", "<Cluster Name>", <Num of Worker Nodes (int)>)
```

## <a name="cluster-monitoring"></a>Supervisión de clústeres

El SDK de administración de HDInsight también puede utilizarse para administrar la supervisión en los clústeres mediante Operations Management Suite (OMS).

### <a name="enable-oms-monitoring"></a>Habilitación de OMS Monitoring

> [!NOTE]
> Para habilitar OMS Monitoring, debe tener un área de trabajo de Log Analytics. Si aún no ha creado una, consulte cómo hacerlo aquí: [Creación de un área de trabajo de Log Analytics en Azure Portal](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-quick-create-workspace).

Para habilitar OMS Monitoring en el clúster:

```java
client.extensions().enableMonitoring("<Resource Group Name", "<Cluster Name>", new ClusterMonitoringRequest().withWorkspaceId("<Workspace Id>"));
```

### <a name="view-status-of-oms-monitoring"></a>Ver el estado de OMS Monitoring

Para obtener el estado de OMS en el clúster:

```java
client.extensions().getMonitoringStatus("<Resource Group Name", "Cluster Name");
```

### <a name="disable-oms-monitoring"></a>Deshabilitación de OMS Monitoring

Para deshabilitar OMS en el clúster:

```java
client.extensions().disableMonitoring("<Resource Group Name>", "<Cluster Name>");
```

## <a name="script-actions"></a>Acciones de script

HDInsight proporciona un método de configuración llamado acciones de script, que invoca scripts personalizados para personalizar el clúster.
> [!NOTE]
> Para más información sobre cómo usar las acciones de script, consulte [Personalización de clústeres de HDInsight basados en Linux mediante la acción de script](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).

### <a name="execute-script-actions"></a>Ejecución de acciones de script

Puede ejecutar acciones de script en un clúster determinado de la siguiente manera:

```java
RuntimeScriptAction scriptAction1 = new RuntimeScriptAction()
    .withName("<Script Name>")
    .withUri("<URL To Script>")
    .withRoles(<List<String> of roles>);
client.clusters().executeScriptActions(
    resourceGroupName, 
    clusterName, 
    new ExecuteScriptActionParameters().withPersistOnSuccess(false).withScriptActions(new LinkedList<>(Arrays.asList(scriptAction1)))); //add more RuntimeScriptActions to the list to execute multiple scripts
```

### <a name="delete-script-action"></a>Eliminación de una acción de script

Para eliminar una acción de script persistente específica en un clúster determinado:

```java
client.scriptActions().delete("<Resource Group Name>", "<Cluster Name>", "<Script Name>");
```

### <a name="list-persisted-script-actions"></a>Lista de acciones de script persistentes

> [!NOTE]
> El método `listByCluster()` devuelve un objeto `PagedList<RuntimeScriptActionDetailInner>`. Una llamada a `currentPage().items()` devuelve una lista de `RuntimeScriptActionDetailInner` y `loadNextPage()` avanza a la página siguiente. Esto se puede repetir hasta que `hasNextPage()` devuelva `false`, que indica que no existen más páginas.

Para mostrar una lista de todas las acciones de script persistentes para el clúster especificado:
```java
client.scriptActions().listByCluster("<Resource Group Name>", "<Cluster Name>");
```

#### <a name="example"></a>Ejemplo

```java
PagedList<RuntimeScriptActionDetailInner> scriptsPaged = client.scriptActions().listByCluster(resourceGroupName, clusterName);
while (true) {
    for (RuntimeScriptActionDetailInner script : scriptsPaged.currentPage().items()) {
        System.out.println(script.name()); //There are methods to get other properties of RuntimeScriptActionDetail besides name(), such as status(), operation(), startTime(), endTime(), etc. See reference documentation.
    }
    if (scriptsPaged.hasNextPage()) {
        scriptsPaged.loadNextPage();
    } else {
        break;
    }
}
```

### <a name="list-all-scripts-execution-history"></a>Lista del historial de ejecución de todos los scripts

Para mostrar una lista del historial de ejecución de todos los scripts para el clúster especificado:

```java
client.scriptExecutionHistorys().listByCluster("<Resource Group Name>", "<Cluster Name>");
```

#### <a name="example"></a>Ejemplo

Este ejemplo imprime todos los detalles de todas las ejecuciones de script pasadas.

```java
PagedList<RuntimeScriptActionDetailInner> scriptExecutionsPaged = client.scriptExecutionHistorys().listByCluster(resourceGroupName, clusterName);
while (true) {
    for (RuntimeScriptActionDetailInner script : scriptExecutionsPaged.currentPage().items()) {
        System.out.println(script.name()); //There are methods to get other properties of RuntimeScriptActionDetail besides name(), such as status(), operation(), startTime(), endTime(), etc. See reference documentation.
    }
    if (scriptExecutionsPaged.hasNextPage()) {
        scriptExecutionsPaged.loadNextPage();
    } else {
        break;
    }
}
```
