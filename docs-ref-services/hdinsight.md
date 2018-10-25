---
title: SDK de Azure HDInsight para Java
description: Referencia del SDK de Azure HDInsight para Java. El SDK de HDInsight para Java proporciona clases y métodos que permiten administrar los clústeres de HDInsight.
author: tylerfox
ms.author: tyfox
ms.reviewer: jasonh
ms.service: hdinsight
ms.topic: reference
ms.devlang: java
ms.date: 9/20/2018
ms.openlocfilehash: 9fd35d12e0aa864b5d23cf03547f7b76dc74c677
ms.sourcegitcommit: 4d52e47073fb0b3ac40a2689daea186bad5b1ef5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/23/2018
ms.locfileid: "49799901"
---
# <a name="hdinsight-java-management-sdk-preview"></a><span data-ttu-id="39da0-104">SDK de administración de HDInsight para Java (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="39da0-104">HDInsight Java Management SDK (Preview)</span></span>

## <a name="overview"></a><span data-ttu-id="39da0-105">Información general</span><span class="sxs-lookup"><span data-stu-id="39da0-105">Overview</span></span>

<span data-ttu-id="39da0-106">El SDK de HDInsight para Java proporciona clases y métodos que permiten administrar los clústeres de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="39da0-106">The HDInsight Java SDK provides classes and methods that allow you to manage your HDInsight clusters.</span></span> <span data-ttu-id="39da0-107">Incluye operaciones para crear, eliminar, actualizar, enumerar, cambiar tamaño, ejecutar acciones de script, supervisar y obtener propiedades de clústeres de HDInsight, entre otras.</span><span class="sxs-lookup"><span data-stu-id="39da0-107">It includes operations to create, delete, update, list, resize, execute script actions, monitor, get properties of HDInsight clusters, and more.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="39da0-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="39da0-108">Prerequisites</span></span>

* <span data-ttu-id="39da0-109">Una cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="39da0-109">An Azure account.</span></span> <span data-ttu-id="39da0-110">Si no tiene una, [obtenga la versión de evaluación gratuita](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="39da0-110">If you don't have one, [get a free trial](https://azure.microsoft.com/free/).</span></span>
* [<span data-ttu-id="39da0-111">Java JDK</span><span class="sxs-lookup"><span data-stu-id="39da0-111">Java JDK</span></span>](https://www.oracle.com/technetwork/java/javase/downloads/index.html)
* [<span data-ttu-id="39da0-112">Maven</span><span class="sxs-lookup"><span data-stu-id="39da0-112">Maven</span></span>](https://maven.apache.org/install.html)

## <a name="sdk-installation"></a><span data-ttu-id="39da0-113">Instalación del SDK</span><span class="sxs-lookup"><span data-stu-id="39da0-113">SDK Installation</span></span>

<span data-ttu-id="39da0-114">El SDK de HDInsight para Java está disponible con Maven [aquí](https://mvnrepository.com/artifact/com.microsoft.azure.hdinsight.v2018_06_01_preview/azure-mgmt-hdinsight).</span><span class="sxs-lookup"><span data-stu-id="39da0-114">The HDInsight Java SDK is available through Maven [here](https://mvnrepository.com/artifact/com.microsoft.azure.hdinsight.v2018_06_01_preview/azure-mgmt-hdinsight).</span></span> <span data-ttu-id="39da0-115">Agregue la siguiente dependencia en pom.xml:</span><span class="sxs-lookup"><span data-stu-id="39da0-115">Add the following dependency to your pom.xml:</span></span>

```
<dependency>
    <groupId>com.microsoft.azure.hdinsight.v2018_06_01_preview</groupId>
    <artifactId>azure-mgmt-hdinsight</artifactId>
    <version>1.0.0-beta-1</version>
</dependency>
```

<span data-ttu-id="39da0-116">También debe agregar las siguientes dependencias al archivo pom.xml:</span><span class="sxs-lookup"><span data-stu-id="39da0-116">You will also need to add the following dependencies to your pom.xml:</span></span>

* [<span data-ttu-id="39da0-117">Biblioteca de autenticación de cliente de Azure:</span><span class="sxs-lookup"><span data-stu-id="39da0-117">Azure Client Authentication Library:</span></span>](https://mvnrepository.com/artifact/com.microsoft.azure/azure-client-authentication/1.6.2)
  ```
  <dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-client-authentication</artifactId>
    <version>1.6.2</version>
    <scope>test</scope>
  </dependency>
  ```

* [<span data-ttu-id="39da0-118">Runtime de cliente de Java de Azure para ARM:</span><span class="sxs-lookup"><span data-stu-id="39da0-118">Azure Java Client Runtime For ARM:</span></span>](https://mvnrepository.com/artifact/com.microsoft.azure/azure-arm-client-runtime/1.6.2)
  ```
  <dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-arm-client-runtime</artifactId>
    <version>1.6.2</version>
  </dependency>
  ```

## <a name="authentication"></a><span data-ttu-id="39da0-119">Autenticación</span><span class="sxs-lookup"><span data-stu-id="39da0-119">Authentication</span></span>

<span data-ttu-id="39da0-120">En primer lugar, el SDK necesita autenticarse en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="39da0-120">The SDK first needs to be authenticated with your Azure subscription.</span></span>  <span data-ttu-id="39da0-121">Siga el ejemplo siguiente para crear una entidad de servicio y usarla para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="39da0-121">Follow the example below to create a service principal and use it to authenticate.</span></span> <span data-ttu-id="39da0-122">Una vez hecho esto, tendrá una instancia de `HDInsightManagementClientImpl`, que contiene muchos métodos que pueden usarse para realizar operaciones de administración (se describen en las secciones siguientes).</span><span class="sxs-lookup"><span data-stu-id="39da0-122">After this is done, you will have an instance of an `HDInsightManagementClientImpl`, which contains many methods (outlined in below sections) that can be used to perform management operations.</span></span>

> [!NOTE]
> <span data-ttu-id="39da0-123">Además del siguiente ejemplo, hay otras maneras de autenticar que podrían ser más adecuadas para sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="39da0-123">There are other ways to authenticate besides the below example that could potentially be better suited for your needs.</span></span> <span data-ttu-id="39da0-124">Todos los métodos se describen aquí: [Autenticación con las bibliotecas de administración de Azure para Java](https://docs.microsoft.com/en-us/java/azure/java-sdk-azure-authenticate?view=azure-java-stable)</span><span class="sxs-lookup"><span data-stu-id="39da0-124">All methods are outlined here: [Authenticate with the Azure management libraries for Java](https://docs.microsoft.com/en-us/java/azure/java-sdk-azure-authenticate?view=azure-java-stable)</span></span>

### <a name="authentication-example-using-a-service-principal"></a><span data-ttu-id="39da0-125">Ejemplo de autenticación con una entidad de servicio</span><span class="sxs-lookup"><span data-stu-id="39da0-125">Authentication Example Using a Service Principal</span></span>

<span data-ttu-id="39da0-126">En primer lugar, inicie sesión en [Azure Cloud Shell](https://shell.azure.com/bash).</span><span class="sxs-lookup"><span data-stu-id="39da0-126">First, login to [Azure Cloud Shell](https://shell.azure.com/bash).</span></span> <span data-ttu-id="39da0-127">Compruebe que está usando la suscripción en la que desea crear la entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="39da0-127">Verify you are currently using the subscription in which you want the service principal created.</span></span> 

```azurecli-interactive
az account show
```

<span data-ttu-id="39da0-128">La información de la suscripción se muestra en formato JSON.</span><span class="sxs-lookup"><span data-stu-id="39da0-128">Your subscription information is displayed as JSON.</span></span>

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

<span data-ttu-id="39da0-129">Si no ha iniciado sesión en la suscripción correcta, ejecute lo siguiente para seleccionar la correcta:</span><span class="sxs-lookup"><span data-stu-id="39da0-129">If you're not logged into the correct subscription, select the correct one by running:</span></span> 
```azurecli-interactive
az account set -s <name or ID of subscription>
```

> [!IMPORTANT]
> <span data-ttu-id="39da0-130">Si aún no ha registrado el proveedor de recursos de HDInsight con otro método (por ejemplo, creando un clúster de HDInsight mediante Azure Portal), deberá hacerlo una vez antes de poder realizar la autenticación.</span><span class="sxs-lookup"><span data-stu-id="39da0-130">If you have not already registered the HDInsight Resource Provider by another method (such as by creating an HDInsight Cluster through the Azure Portal), you need to do this once before you can authenticate.</span></span> <span data-ttu-id="39da0-131">Se puede hacer desde [Azure Cloud Shell](https://shell.azure.com/bash), con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="39da0-131">This can be done from the [Azure Cloud Shell](https://shell.azure.com/bash) by running the following command:</span></span>
>```azurecli-interactive
>az provider register --namespace Microsoft.HDInsight
>```

<span data-ttu-id="39da0-132">A continuación, elija un nombre para la entidad de servicio y créela con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="39da0-132">Next, choose a name for your service principal and create it with the following command:</span></span>

```azurecli-interactive
az ad sp create-for-rbac --name <Service Principal Name> --sdk-auth
```

<span data-ttu-id="39da0-133">La información de la entidad de servicio se muestra con formato JSON.</span><span class="sxs-lookup"><span data-stu-id="39da0-133">The service principal information is displayed as JSON.</span></span>

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
<span data-ttu-id="39da0-134">Copie el siguiente fragmento de código y rellene `TENANT_ID`, `CLIENT_ID`, `CLIENT_SECRET` y `SUBSCRIPTION_ID` con las cadenas del código JSON que se devolvió después de ejecutar el comando para crear la entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="39da0-134">Copy the below snippet and fill in `TENANT_ID`, `CLIENT_ID`, `CLIENT_SECRET`, and `SUBSCRIPTION_ID` with the strings from the JSON that was returned after running the command to create the service principal.</span></span>

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


## <a name="cluster-management"></a><span data-ttu-id="39da0-135">Administración de clústeres</span><span class="sxs-lookup"><span data-stu-id="39da0-135">Cluster Management</span></span>

> [!NOTE]
> <span data-ttu-id="39da0-136">En esta sección se da por supuesto que ya ha autenticado y construido una instancia de `HDInsightManagementClientImpl`, y que la ha almacenado en una variable llamada `client`.</span><span class="sxs-lookup"><span data-stu-id="39da0-136">This section assumes you have already authenticated and constructed an `HDInsightManagementClientImpl` instance and store it in a variable called `client`.</span></span> <span data-ttu-id="39da0-137">En la sección Autenticación anterior encontrará las instrucciones para autenticarse y obtener un `HDInsightManagementClientImpl`.</span><span class="sxs-lookup"><span data-stu-id="39da0-137">Instructions for authenticating and obtaining an `HDInsightManagementClientImpl` can be found in the Authentication section above.</span></span>

### <a name="create-a-cluster"></a><span data-ttu-id="39da0-138">Creación de un clúster</span><span class="sxs-lookup"><span data-stu-id="39da0-138">Create a Cluster</span></span>

<span data-ttu-id="39da0-139">Para crear un nuevo clúster, se puede llamar a `client.clusters().create()`.</span><span class="sxs-lookup"><span data-stu-id="39da0-139">A new cluster can be created by calling `client.clusters().create()`.</span></span>

#### <a name="example"></a><span data-ttu-id="39da0-140">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="39da0-140">Example</span></span>

<span data-ttu-id="39da0-141">En este ejemplo se muestra cómo crear un clúster de Spark con dos nodos principales y un nodo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="39da0-141">This example demonstrates how to create a Spark cluster with 2 head nodes and 1 worker node.</span></span>

> [!NOTE]
> <span data-ttu-id="39da0-142">En primer lugar debe crear un grupo de recursos y la cuenta de almacenamiento, tal y como se explica más adelante.</span><span class="sxs-lookup"><span data-stu-id="39da0-142">You first need to create a Resource Group and Storage Account, as explained below.</span></span> <span data-ttu-id="39da0-143">Si ya los ha creado, puede omitir estos pasos.</span><span class="sxs-lookup"><span data-stu-id="39da0-143">If you have already created these, you can skip these steps.</span></span>

##### <a name="creating-a-resource-group"></a><span data-ttu-id="39da0-144">Creación de un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="39da0-144">Creating a Resource Group</span></span>

<span data-ttu-id="39da0-145">Puede crear un grupo de recursos con [Azure Cloud Shell](https://shell.azure.com/bash), con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="39da0-145">You can create a resource group using the [Azure Cloud Shell](https://shell.azure.com/bash) by running</span></span>
```azurecli-interactive
az group create -l <Region Name (i.e. eastus)> --n <Resource Group Name>
```
##### <a name="creating-a-storage-account"></a><span data-ttu-id="39da0-146">Creación de una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="39da0-146">Creating a Storage Account</span></span>

<span data-ttu-id="39da0-147">Puede crear una cuenta de almacenamiento con [Azure Cloud Shell](https://shell.azure.com/bash), con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="39da0-147">You can create a storage account using the [Azure Cloud Shell](https://shell.azure.com/bash) by running:</span></span>
```azurecli-interactive
az storage account create -n <Storage Account Name> -g <Existing Resource Group Name> -l <Region Name (i.e. eastus)> --sku <SKU i.e. Standard_LRS>
```
<span data-ttu-id="39da0-148">Ahora, ejecute el siguiente comando para obtener la clave de la cuenta de almacenamiento (que necesitará para crear un clúster):</span><span class="sxs-lookup"><span data-stu-id="39da0-148">Now run the following command to get the key for your storage account (you will need this to create a cluster):</span></span>
```azurecli-interactive
az storage account keys list -n <Storage Account Name>
```
---
<span data-ttu-id="39da0-149">El siguiente fragmento de código de Java crea un clúster de Spark con dos nodos principales y un nodo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="39da0-149">The below Java snippet creates a Spark cluster with 2 head nodes and 1 worker node.</span></span> <span data-ttu-id="39da0-150">Rellene las variables en blanco tal y como se explica en los comentarios y no dude en cambiar otros parámetros para que se adapten a sus necesidades específicas.</span><span class="sxs-lookup"><span data-stu-id="39da0-150">Fill in the blank variables as explained in the comments and feel free to change other parameters to suit your specific needs.</span></span>

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

### <a name="get-cluster-details"></a><span data-ttu-id="39da0-151">Obtención de los detalles del clúster</span><span class="sxs-lookup"><span data-stu-id="39da0-151">Get Cluster Details</span></span>

<span data-ttu-id="39da0-152">Para obtener las propiedades de un clúster determinado:</span><span class="sxs-lookup"><span data-stu-id="39da0-152">To get properties for a given cluster:</span></span>

```java
client.clusters.getByResourceGroup("<Resource Group Name>", "<Cluster Name>");
```

#### <a name="example"></a><span data-ttu-id="39da0-153">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="39da0-153">Example</span></span>

<span data-ttu-id="39da0-154">Puede usar `get` para confirmar que ha creado correctamente el clúster.</span><span class="sxs-lookup"><span data-stu-id="39da0-154">You can use `get` to confirm that you have successfully created your cluster.</span></span>

```java
ClusterInner cluster = client.clusters().getByResourceGroup("<Resource Group Name>", "<Cluster Name>");
System.out.println(cluster.name()); //Prints the name of the cluster
System.out.println(cluster.id()); //Prints the resource Id of the cluster
```

<span data-ttu-id="39da0-155">La salida debe ser similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="39da0-155">The output should look like:</span></span>

```
<Cluster Name>
/subscriptions/XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX/resourceGroups/<Resource Group Name>/providers/Microsoft.HDInsight/clusters/<Cluster Name>
```

### <a name="list-clusters"></a><span data-ttu-id="39da0-156">Lista de clústeres</span><span class="sxs-lookup"><span data-stu-id="39da0-156">List Clusters</span></span>

#### <a name="list-clusters-under-the-subscription"></a><span data-ttu-id="39da0-157">Lista de clústeres de la suscripción</span><span class="sxs-lookup"><span data-stu-id="39da0-157">List Clusters Under The Subscription</span></span>

```java
client.clusters.list();
```
#### <a name="list-clusters-by-resource-group"></a><span data-ttu-id="39da0-158">Lista de clústeres por grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="39da0-158">List Clusters By Resource Group</span></span>

```java
client.clusters.listByResourceGroup("<Resource Group Name>");
```
> [!NOTE]
> <span data-ttu-id="39da0-159">Tanto `List()` como `ListByResourceGroup()` devuelven un objeto `PagedList<ClusterInner>`.</span><span class="sxs-lookup"><span data-stu-id="39da0-159">Both `List()` and `ListByResourceGroup()` return a `PagedList<ClusterInner>` object.</span></span> <span data-ttu-id="39da0-160">Una llamada a `loadNext()` devuelve una lista de clústeres en esa página y hace avanzar el objeto `ClusterPaged` a la página siguiente.</span><span class="sxs-lookup"><span data-stu-id="39da0-160">Calling `loadNext()` returns a list of clusters on that page and advances the `ClusterPaged` object to the next page.</span></span> <span data-ttu-id="39da0-161">Esto se puede repetir hasta que `hasNextPage()` devuelva `false`, que indica que no existen más páginas.</span><span class="sxs-lookup"><span data-stu-id="39da0-161">This can be repeated until `hasNextPage()` return `false`, indicating that there are no more pages.</span></span>

#### <a name="example"></a><span data-ttu-id="39da0-162">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="39da0-162">Example</span></span>

<span data-ttu-id="39da0-163">El ejemplo siguiente imprime las propiedades de todos los clústeres de la suscripción actual:</span><span class="sxs-lookup"><span data-stu-id="39da0-163">The following example prints the properties of all clusters for the current subscription:</span></span>

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

### <a name="delete-a-cluster"></a><span data-ttu-id="39da0-164">Eliminación de un clúster</span><span class="sxs-lookup"><span data-stu-id="39da0-164">Delete a Cluster</span></span>

<span data-ttu-id="39da0-165">Para eliminar un clúster:</span><span class="sxs-lookup"><span data-stu-id="39da0-165">To delete a cluster:</span></span>

```java
client.clusters.delete("<Resource Group Name>", "<Cluster Name>");
```

### <a name="update-cluster-tags"></a><span data-ttu-id="39da0-166">Actualización de las etiquetas del clúster</span><span class="sxs-lookup"><span data-stu-id="39da0-166">Update Cluster Tags</span></span>

<span data-ttu-id="39da0-167">Puede actualizar las etiquetas de un clúster determinado de este modo:</span><span class="sxs-lookup"><span data-stu-id="39da0-167">You can update the tags of a given cluster like so:</span></span>

```java
client.clusters.update("<Resource Group Name>", "<Cluster Name>", <Map<String,String> of Tags>);
```

### <a name="resize-cluster"></a><span data-ttu-id="39da0-168">Cambio del tamaño de clúster</span><span class="sxs-lookup"><span data-stu-id="39da0-168">Resize Cluster</span></span>

<span data-ttu-id="39da0-169">Para cambiar el tamaño de un número de nodos de trabajo de un clúster determinado, puede especificar un nuevo tamaño como sigue:</span><span class="sxs-lookup"><span data-stu-id="39da0-169">You can resize a given cluster's number of worker nodes by specifying a new size like so:</span></span>

```java
client.clusters.resize("<Resource Group Name>", "<Cluster Name>", <Num of Worker Nodes (int)>)
```

## <a name="cluster-monitoring"></a><span data-ttu-id="39da0-170">Supervisión de clústeres</span><span class="sxs-lookup"><span data-stu-id="39da0-170">Cluster Monitoring</span></span>

<span data-ttu-id="39da0-171">El SDK de administración de HDInsight también puede utilizarse para administrar la supervisión en los clústeres mediante Operations Management Suite (OMS).</span><span class="sxs-lookup"><span data-stu-id="39da0-171">The HDInsight Management SDK can also be used to manage monitoring on your clusters via the Operations Management Suite (OMS).</span></span>

### <a name="enable-oms-monitoring"></a><span data-ttu-id="39da0-172">Habilitación de OMS Monitoring</span><span class="sxs-lookup"><span data-stu-id="39da0-172">Enable OMS Monitoring</span></span>

> [!NOTE]
> <span data-ttu-id="39da0-173">Para habilitar OMS Monitoring, debe tener un área de trabajo de Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="39da0-173">To enable OMS Monitoring, you must have an existing Log Analytics workspace.</span></span> <span data-ttu-id="39da0-174">Si aún no ha creado una, consulte cómo hacerlo aquí: [Creación de un área de trabajo de Log Analytics en Azure Portal](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-quick-create-workspace).</span><span class="sxs-lookup"><span data-stu-id="39da0-174">If you have not already created one, you can learn how to do that here: [Create a Log Analytics workspace in the Azure portal](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-quick-create-workspace).</span></span>

<span data-ttu-id="39da0-175">Para habilitar OMS Monitoring en el clúster:</span><span class="sxs-lookup"><span data-stu-id="39da0-175">To enable OMS Monitoring on your cluster:</span></span>

```java
client.extensions().enableMonitoring("<Resource Group Name", "<Cluster Name>", new ClusterMonitoringRequest().withWorkspaceId("<Workspace Id>"));
```

### <a name="view-status-of-oms-monitoring"></a><span data-ttu-id="39da0-176">Ver el estado de OMS Monitoring</span><span class="sxs-lookup"><span data-stu-id="39da0-176">View Status Of OMS Monitoring</span></span>

<span data-ttu-id="39da0-177">Para obtener el estado de OMS en el clúster:</span><span class="sxs-lookup"><span data-stu-id="39da0-177">To get the status of OMS on your cluster:</span></span>

```java
client.extensions().getMonitoringStatus("<Resource Group Name", "Cluster Name");
```

### <a name="disable-oms-monitoring"></a><span data-ttu-id="39da0-178">Deshabilitación de OMS Monitoring</span><span class="sxs-lookup"><span data-stu-id="39da0-178">Disable OMS Monitoring</span></span>

<span data-ttu-id="39da0-179">Para deshabilitar OMS en el clúster:</span><span class="sxs-lookup"><span data-stu-id="39da0-179">To disable OMS on your cluster:</span></span>

```java
client.extensions().disableMonitoring("<Resource Group Name>", "<Cluster Name>");
```

## <a name="script-actions"></a><span data-ttu-id="39da0-180">Acciones de script</span><span class="sxs-lookup"><span data-stu-id="39da0-180">Script Actions</span></span>

<span data-ttu-id="39da0-181">HDInsight proporciona un método de configuración llamado acciones de script, que invoca scripts personalizados para personalizar el clúster.</span><span class="sxs-lookup"><span data-stu-id="39da0-181">HDInsight provides a configuration method called script actions that invokes custom scripts to customize the cluster.</span></span>
> [!NOTE]
> <span data-ttu-id="39da0-182">Para más información sobre cómo usar las acciones de script, consulte [Personalización de clústeres de HDInsight basados en Linux mediante la acción de script](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span><span class="sxs-lookup"><span data-stu-id="39da0-182">More information on how to use script actions can be found here: [Customize Linux-based HDInsight clusters using script actions](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux)</span></span>

### <a name="execute-script-actions"></a><span data-ttu-id="39da0-183">Ejecución de acciones de script</span><span class="sxs-lookup"><span data-stu-id="39da0-183">Execute Script Actions</span></span>

<span data-ttu-id="39da0-184">Puede ejecutar acciones de script en un clúster determinado de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="39da0-184">You can execute script actions on a given cluster like so:</span></span>

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

### <a name="delete-script-action"></a><span data-ttu-id="39da0-185">Eliminación de una acción de script</span><span class="sxs-lookup"><span data-stu-id="39da0-185">Delete Script Action</span></span>

<span data-ttu-id="39da0-186">Para eliminar una acción de script persistente específica en un clúster determinado:</span><span class="sxs-lookup"><span data-stu-id="39da0-186">To delete a specified persisted script action on a given cluster:</span></span>

```java
client.scriptActions().delete("<Resource Group Name>", "<Cluster Name>", "<Script Name>");
```

### <a name="list-persisted-script-actions"></a><span data-ttu-id="39da0-187">Lista de acciones de script persistentes</span><span class="sxs-lookup"><span data-stu-id="39da0-187">List Persisted Script Actions</span></span>

> [!NOTE]
> <span data-ttu-id="39da0-188">El método `listByCluster()` devuelve un objeto `PagedList<RuntimeScriptActionDetailInner>`.</span><span class="sxs-lookup"><span data-stu-id="39da0-188">Both `listByCluster()` returns a `PagedList<RuntimeScriptActionDetailInner>` object.</span></span> <span data-ttu-id="39da0-189">Una llamada a `currentPage().items()` devuelve una lista de `RuntimeScriptActionDetailInner` y `loadNextPage()` avanza a la página siguiente.</span><span class="sxs-lookup"><span data-stu-id="39da0-189">Calling `currentPage().items()` returns a list of `RuntimeScriptActionDetailInner`, and `loadNextPage()` advances to the next page.</span></span> <span data-ttu-id="39da0-190">Esto se puede repetir hasta que `hasNextPage()` devuelva `false`, que indica que no existen más páginas.</span><span class="sxs-lookup"><span data-stu-id="39da0-190">This can be repeated until `hasNextPage()` returns `false`, indicating that there are no more pages.</span></span>

<span data-ttu-id="39da0-191">Para mostrar una lista de todas las acciones de script persistentes para el clúster especificado:</span><span class="sxs-lookup"><span data-stu-id="39da0-191">To list all persisted script actions for the specified cluster:</span></span>
```java
client.scriptActions().listByCluster("<Resource Group Name>", "<Cluster Name>");
```

#### <a name="example"></a><span data-ttu-id="39da0-192">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="39da0-192">Example</span></span>

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

### <a name="list-all-scripts-execution-history"></a><span data-ttu-id="39da0-193">Lista del historial de ejecución de todos los scripts</span><span class="sxs-lookup"><span data-stu-id="39da0-193">List All Scripts' Execution History</span></span>

<span data-ttu-id="39da0-194">Para mostrar una lista del historial de ejecución de todos los scripts para el clúster especificado:</span><span class="sxs-lookup"><span data-stu-id="39da0-194">To list all scripts' execution history for the specified cluster:</span></span>

```java
client.scriptExecutionHistorys().listByCluster("<Resource Group Name>", "<Cluster Name>");
```

#### <a name="example"></a><span data-ttu-id="39da0-195">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="39da0-195">Example</span></span>

<span data-ttu-id="39da0-196">Este ejemplo imprime todos los detalles de todas las ejecuciones de script pasadas.</span><span class="sxs-lookup"><span data-stu-id="39da0-196">This example prints all the details for all past script executions.</span></span>

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
