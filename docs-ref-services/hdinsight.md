---
title: SDK de Azure HDInsight para Java
description: Referencia del SDK de Azure HDInsight para Java. El SDK de HDInsight para Java proporciona clases y métodos que permiten administrar los clústeres de HDInsight.
author: tylerfox
ms.author: tyfox
ms.reviewer: jasonh
ms.service: hdinsight
ms.topic: reference
ms.devlang: java
ms.date: 04/15/2019
ms.openlocfilehash: fe87c9214e2a620230cf2f1f52261fd66a2b8857
ms.sourcegitcommit: f33befab25a66a252b4c91c7aeb1b77cb32821bb
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/17/2019
ms.locfileid: "59705123"
---
# <a name="hdinsight-sdk-for-java"></a><span data-ttu-id="aa0b9-104">SDK de Azure HDInsight para Java</span><span class="sxs-lookup"><span data-stu-id="aa0b9-104">HDInsight SDK for Java</span></span>

## <a name="overview"></a><span data-ttu-id="aa0b9-105">Información general</span><span class="sxs-lookup"><span data-stu-id="aa0b9-105">Overview</span></span>

<span data-ttu-id="aa0b9-106">El SDK de HDInsight para Java proporciona clases y métodos que permiten administrar los clústeres de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="aa0b9-106">The HDInsight SDK for Java provides classes and methods that allow you to manage your HDInsight clusters.</span></span> <span data-ttu-id="aa0b9-107">Incluye operaciones para crear, eliminar, actualizar, enumerar, cambiar tamaño, ejecutar acciones de script, supervisar y obtener propiedades de clústeres de HDInsight, entre otras.</span><span class="sxs-lookup"><span data-stu-id="aa0b9-107">It includes operations to create, delete, update, list, resize, execute script actions, monitor, get properties of HDInsight clusters, and more.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aa0b9-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="aa0b9-108">Prerequisites</span></span>

* <span data-ttu-id="aa0b9-109">Una cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="aa0b9-109">An Azure account.</span></span> <span data-ttu-id="aa0b9-110">Si no tiene una, [obtenga la versión de evaluación gratuita](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="aa0b9-110">If you don't have one, [get a free trial](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="aa0b9-111">Un kit de desarrollo de Java (JDK) admitido</span><span class="sxs-lookup"><span data-stu-id="aa0b9-111">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="aa0b9-112">Para más información sobre los JDK disponibles para desarrollar en Azure, consulte <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="aa0b9-112">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* [<span data-ttu-id="aa0b9-113">Maven</span><span class="sxs-lookup"><span data-stu-id="aa0b9-113">Maven</span></span>](https://maven.apache.org/download.cgi)

## <a name="sdk-installation"></a><span data-ttu-id="aa0b9-114">Instalación del SDK</span><span class="sxs-lookup"><span data-stu-id="aa0b9-114">SDK Installation</span></span>

<span data-ttu-id="aa0b9-115">El SDK de HDInsight para Java está disponible con Maven [aquí](https://search.maven.org/artifact/com.microsoft.azure.hdinsight.v2018_06_01_preview/azure-mgmt-hdinsight).</span><span class="sxs-lookup"><span data-stu-id="aa0b9-115">The HDInsight SDK for Java is available through Maven [here](https://search.maven.org/artifact/com.microsoft.azure.hdinsight.v2018_06_01_preview/azure-mgmt-hdinsight).</span></span> <span data-ttu-id="aa0b9-116">Agregue la siguiente dependencia en pom.xml:</span><span class="sxs-lookup"><span data-stu-id="aa0b9-116">Add the following dependency to your pom.xml:</span></span>

```
<dependency>
    <groupId>com.microsoft.azure.hdinsight.v2018_06_01_preview</groupId>
    <artifactId>azure-mgmt-hdinsight</artifactId>
    <version>1.0.0-beta-1</version>
</dependency>
```

<span data-ttu-id="aa0b9-117">También debe agregar las siguientes dependencias al archivo pom.xml:</span><span class="sxs-lookup"><span data-stu-id="aa0b9-117">You will also need to add the following dependencies to your pom.xml:</span></span>

* [<span data-ttu-id="aa0b9-118">Biblioteca de autenticación de cliente de Azure:</span><span class="sxs-lookup"><span data-stu-id="aa0b9-118">Azure Client Authentication Library:</span></span>](https://search.maven.org/artifact/com.microsoft.azure/azure-client-authentication)
  ```
  <dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-client-authentication</artifactId>
    <version>1.6.5</version>
  </dependency>
  ```

* [<span data-ttu-id="aa0b9-119">Runtime de cliente de Java de Azure para ARM:</span><span class="sxs-lookup"><span data-stu-id="aa0b9-119">Azure Java Client Runtime For ARM:</span></span>](https://search.maven.org/artifact/com.microsoft.azure/azure-arm-client-runtime)
  ```
  <dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-arm-client-runtime</artifactId>
    <version>1.6.5</version>
  </dependency>
  ```

## <a name="authentication"></a><span data-ttu-id="aa0b9-120">Authentication</span><span class="sxs-lookup"><span data-stu-id="aa0b9-120">Authentication</span></span>

<span data-ttu-id="aa0b9-121">En primer lugar, el SDK necesita autenticarse en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="aa0b9-121">The SDK first needs to be authenticated with your Azure subscription.</span></span>  <span data-ttu-id="aa0b9-122">Siga el ejemplo siguiente para crear una entidad de servicio y usarla para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="aa0b9-122">Follow the example below to create a service principal and use it to authenticate.</span></span> <span data-ttu-id="aa0b9-123">Una vez hecho esto, tendrá una instancia de `HDInsightManagementClientImpl`, que contiene muchos métodos que pueden usarse para realizar operaciones de administración (se describen en las secciones siguientes).</span><span class="sxs-lookup"><span data-stu-id="aa0b9-123">After this is done, you will have an instance of an `HDInsightManagementClientImpl`, which contains many methods (outlined in below sections) that can be used to perform management operations.</span></span>

> [!NOTE]
> <span data-ttu-id="aa0b9-124">Además del siguiente ejemplo, hay otras maneras de autenticar que podrían ser más adecuadas para sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="aa0b9-124">There are other ways to authenticate besides the below example that could potentially be better suited for your needs.</span></span> <span data-ttu-id="aa0b9-125">Todos los métdosos se describen aquí: [Autenticación con las bibliotecas de administración de Azure para Java](https://docs.microsoft.com/en-us/java/azure/java-sdk-azure-authenticate?view=azure-java-stable)</span><span class="sxs-lookup"><span data-stu-id="aa0b9-125">All methods are outlined here: [Authenticate with the Azure management libraries for Java](https://docs.microsoft.com/en-us/java/azure/java-sdk-azure-authenticate?view=azure-java-stable)</span></span>

### <a name="authentication-example-using-a-service-principal"></a><span data-ttu-id="aa0b9-126">Ejemplo de autenticación con una entidad de servicio</span><span class="sxs-lookup"><span data-stu-id="aa0b9-126">Authentication Example Using a Service Principal</span></span>

<span data-ttu-id="aa0b9-127">En primer lugar, inicie sesión en [Azure Cloud Shell](https://shell.azure.com/bash).</span><span class="sxs-lookup"><span data-stu-id="aa0b9-127">First, login to [Azure Cloud Shell](https://shell.azure.com/bash).</span></span> <span data-ttu-id="aa0b9-128">Compruebe que está usando la suscripción en la que desea crear la entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="aa0b9-128">Verify you are currently using the subscription in which you want the service principal created.</span></span> 

```azurecli-interactive
az account show
```

<span data-ttu-id="aa0b9-129">La información de la suscripción se muestra en formato JSON.</span><span class="sxs-lookup"><span data-stu-id="aa0b9-129">Your subscription information is displayed as JSON.</span></span>

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

<span data-ttu-id="aa0b9-130">Si no ha iniciado sesión en la suscripción correcta, ejecute lo siguiente para seleccionar la correcta:</span><span class="sxs-lookup"><span data-stu-id="aa0b9-130">If you're not logged into the correct subscription, select the correct one by running:</span></span> 
```azurecli-interactive
az account set -s <name or ID of subscription>
```

> [!IMPORTANT]
> <span data-ttu-id="aa0b9-131">Si aún no ha registrado el proveedor de recursos de HDInsight con otro método (por ejemplo, creando un clúster de HDInsight mediante Azure Portal), deberá hacerlo una vez antes de poder realizar la autenticación.</span><span class="sxs-lookup"><span data-stu-id="aa0b9-131">If you have not already registered the HDInsight Resource Provider by another method (such as by creating an HDInsight Cluster through the Azure Portal), you need to do this once before you can authenticate.</span></span> <span data-ttu-id="aa0b9-132">Se puede hacer desde [Azure Cloud Shell](https://shell.azure.com/bash), con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="aa0b9-132">This can be done from the [Azure Cloud Shell](https://shell.azure.com/bash) by running the following command:</span></span>
>```azurecli-interactive
>az provider register --namespace Microsoft.HDInsight
>```

<span data-ttu-id="aa0b9-133">A continuación, elija un nombre para la entidad de servicio y créela con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="aa0b9-133">Next, choose a name for your service principal and create it with the following command:</span></span>

```azurecli-interactive
az ad sp create-for-rbac --name <Service Principal Name> --sdk-auth
```

<span data-ttu-id="aa0b9-134">La información de la entidad de servicio se muestra con formato JSON.</span><span class="sxs-lookup"><span data-stu-id="aa0b9-134">The service principal information is displayed as JSON.</span></span>

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
<span data-ttu-id="aa0b9-135">Copie el siguiente fragmento de código y rellene `TENANT_ID`, `CLIENT_ID`, `CLIENT_SECRET` y `SUBSCRIPTION_ID` con las cadenas del código JSON que se devolvió después de ejecutar el comando para crear la entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="aa0b9-135">Copy the below snippet and fill in `TENANT_ID`, `CLIENT_ID`, `CLIENT_SECRET`, and `SUBSCRIPTION_ID` with the strings from the JSON that was returned after running the command to create the service principal.</span></span>

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

        HDInsightManagementClientImpl client = new HDInsightManagementClientImpl(credentials)
                .withSubscriptionId(SUBSCRIPTION_ID);
```

## <a name="cluster-management"></a><span data-ttu-id="aa0b9-136">Administración de clústeres</span><span class="sxs-lookup"><span data-stu-id="aa0b9-136">Cluster Management</span></span>

> [!NOTE]
> <span data-ttu-id="aa0b9-137">En esta sección se da por supuesto que ya ha autenticado y construido una instancia de `HDInsightManagementClientImpl`, y que la ha almacenado en una variable llamada `client`.</span><span class="sxs-lookup"><span data-stu-id="aa0b9-137">This section assumes you have already authenticated and constructed an `HDInsightManagementClientImpl` instance and store it in a variable called `client`.</span></span> <span data-ttu-id="aa0b9-138">En la sección Autenticación anterior encontrará las instrucciones para autenticarse y obtener un `HDInsightManagementClientImpl`.</span><span class="sxs-lookup"><span data-stu-id="aa0b9-138">Instructions for authenticating and obtaining an `HDInsightManagementClientImpl` can be found in the Authentication section above.</span></span>

### <a name="create-a-cluster"></a><span data-ttu-id="aa0b9-139">Creación de un clúster</span><span class="sxs-lookup"><span data-stu-id="aa0b9-139">Create a Cluster</span></span>

<span data-ttu-id="aa0b9-140">Para crear un nuevo clúster, se puede llamar a `client.clusters().create()`.</span><span class="sxs-lookup"><span data-stu-id="aa0b9-140">A new cluster can be created by calling `client.clusters().create()`.</span></span>

#### <a name="samples"></a><span data-ttu-id="aa0b9-141">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="aa0b9-141">Samples</span></span>

<span data-ttu-id="aa0b9-142">Hay disponibles ejemplos de código para crear varios tipos comunes de clústeres de HDInsight: [Ejemplos de HDInsight para Java](https://github.com/Azure-Samples/hdinsight-java-sdk-samples).</span><span class="sxs-lookup"><span data-stu-id="aa0b9-142">Code samples for creating several common types of HDInsight clusters are available: [HDInsight Java Samples](https://github.com/Azure-Samples/hdinsight-java-sdk-samples).</span></span>

#### <a name="example"></a><span data-ttu-id="aa0b9-143">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="aa0b9-143">Example</span></span>

<span data-ttu-id="aa0b9-144">En este ejemplo se muestra cómo crear un clúster de Spark con dos nodos principales y un nodo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="aa0b9-144">This example demonstrates how to create a Spark cluster with 2 head nodes and 1 worker node.</span></span>

> [!NOTE]
> <span data-ttu-id="aa0b9-145">En primer lugar debe crear un grupo de recursos y la cuenta de almacenamiento, tal y como se explica más adelante.</span><span class="sxs-lookup"><span data-stu-id="aa0b9-145">You first need to create a Resource Group and Storage Account, as explained below.</span></span> <span data-ttu-id="aa0b9-146">Si ya los ha creado, puede omitir estos pasos.</span><span class="sxs-lookup"><span data-stu-id="aa0b9-146">If you have already created these, you can skip these steps.</span></span>

##### <a name="creating-a-resource-group"></a><span data-ttu-id="aa0b9-147">Creación de un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="aa0b9-147">Creating a Resource Group</span></span>

<span data-ttu-id="aa0b9-148">Puede crear un grupo de recursos con [Azure Cloud Shell](https://shell.azure.com/bash), con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="aa0b9-148">You can create a resource group using the [Azure Cloud Shell](https://shell.azure.com/bash) by running</span></span>
```azurecli-interactive
az group create -l <Region Name (i.e. eastus)> --n <Resource Group Name>
```
##### <a name="creating-a-storage-account"></a><span data-ttu-id="aa0b9-149">Creación de una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="aa0b9-149">Creating a Storage Account</span></span>

<span data-ttu-id="aa0b9-150">Puede crear una cuenta de almacenamiento con [Azure Cloud Shell](https://shell.azure.com/bash), con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="aa0b9-150">You can create a storage account using the [Azure Cloud Shell](https://shell.azure.com/bash) by running:</span></span>
```azurecli-interactive
az storage account create -n <Storage Account Name> -g <Existing Resource Group Name> -l <Region Name (i.e. eastus)> --sku <SKU i.e. Standard_LRS>
```
<span data-ttu-id="aa0b9-151">Ahora, ejecute el siguiente comando para obtener la clave de la cuenta de almacenamiento (que necesitará para crear un clúster):</span><span class="sxs-lookup"><span data-stu-id="aa0b9-151">Now run the following command to get the key for your storage account (you will need this to create a cluster):</span></span>
```azurecli-interactive
az storage account keys list -n <Storage Account Name>
```
---
<span data-ttu-id="aa0b9-152">El siguiente fragmento de código de Java crea un clúster de Spark con dos nodos principales y un nodo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="aa0b9-152">The below Java snippet creates a Spark cluster with 2 head nodes and 1 worker node.</span></span> <span data-ttu-id="aa0b9-153">Rellene las variables en blanco tal y como se explica en los comentarios y no dude en cambiar otros parámetros para que se adapten a sus necesidades específicas.</span><span class="sxs-lookup"><span data-stu-id="aa0b9-153">Fill in the blank variables as explained in the comments and feel free to change other parameters to suit your specific needs.</span></span>

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

### <a name="get-cluster-details"></a><span data-ttu-id="aa0b9-154">Obtención de los detalles del clúster</span><span class="sxs-lookup"><span data-stu-id="aa0b9-154">Get Cluster Details</span></span>

<span data-ttu-id="aa0b9-155">Para obtener las propiedades de un clúster determinado:</span><span class="sxs-lookup"><span data-stu-id="aa0b9-155">To get properties for a given cluster:</span></span>

```java
client.clusters.getByResourceGroup("<Resource Group Name>", "<Cluster Name>");
```

#### <a name="example"></a><span data-ttu-id="aa0b9-156">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="aa0b9-156">Example</span></span>

<span data-ttu-id="aa0b9-157">Puede usar `get` para confirmar que ha creado correctamente el clúster.</span><span class="sxs-lookup"><span data-stu-id="aa0b9-157">You can use `get` to confirm that you have successfully created your cluster.</span></span>

```java
ClusterInner cluster = client.clusters().getByResourceGroup("<Resource Group Name>", "<Cluster Name>");
System.out.println(cluster.name()); //Prints the name of the cluster
System.out.println(cluster.id()); //Prints the resource Id of the cluster
```

<span data-ttu-id="aa0b9-158">La salida debe ser similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="aa0b9-158">The output should look like:</span></span>

```
<Cluster Name>
/subscriptions/XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX/resourceGroups/<Resource Group Name>/providers/Microsoft.HDInsight/clusters/<Cluster Name>
```

### <a name="list-clusters"></a><span data-ttu-id="aa0b9-159">Lista de clústeres</span><span class="sxs-lookup"><span data-stu-id="aa0b9-159">List Clusters</span></span>

#### <a name="list-clusters-under-the-subscription"></a><span data-ttu-id="aa0b9-160">Lista de clústeres de la suscripción</span><span class="sxs-lookup"><span data-stu-id="aa0b9-160">List Clusters Under The Subscription</span></span>

```java
client.clusters.list();
```
#### <a name="list-clusters-by-resource-group"></a><span data-ttu-id="aa0b9-161">Lista de clústeres por grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="aa0b9-161">List Clusters By Resource Group</span></span>

```java
client.clusters.listByResourceGroup("<Resource Group Name>");
```
> [!NOTE]
> <span data-ttu-id="aa0b9-162">Tanto `List()` como `ListByResourceGroup()` devuelven un objeto `PagedList<ClusterInner>`.</span><span class="sxs-lookup"><span data-stu-id="aa0b9-162">Both `List()` and `ListByResourceGroup()` return a `PagedList<ClusterInner>` object.</span></span> <span data-ttu-id="aa0b9-163">Una llamada a `loadNext()` devuelve una lista de clústeres en esa página y hace avanzar el objeto `ClusterPaged` a la página siguiente.</span><span class="sxs-lookup"><span data-stu-id="aa0b9-163">Calling `loadNext()` returns a list of clusters on that page and advances the `ClusterPaged` object to the next page.</span></span> <span data-ttu-id="aa0b9-164">Esto se puede repetir hasta que `hasNextPage()` devuelva `false`, que indica que no existen más páginas.</span><span class="sxs-lookup"><span data-stu-id="aa0b9-164">This can be repeated until `hasNextPage()` return `false`, indicating that there are no more pages.</span></span>

#### <a name="example"></a><span data-ttu-id="aa0b9-165">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="aa0b9-165">Example</span></span>

<span data-ttu-id="aa0b9-166">El ejemplo siguiente imprime las propiedades de todos los clústeres de la suscripción actual:</span><span class="sxs-lookup"><span data-stu-id="aa0b9-166">The following example prints the properties of all clusters for the current subscription:</span></span>

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

### <a name="delete-a-cluster"></a><span data-ttu-id="aa0b9-167">Eliminación de un clúster</span><span class="sxs-lookup"><span data-stu-id="aa0b9-167">Delete a Cluster</span></span>

<span data-ttu-id="aa0b9-168">Para eliminar un clúster:</span><span class="sxs-lookup"><span data-stu-id="aa0b9-168">To delete a cluster:</span></span>

```java
client.clusters.delete("<Resource Group Name>", "<Cluster Name>");
```

### <a name="update-cluster-tags"></a><span data-ttu-id="aa0b9-169">Actualización de las etiquetas del clúster</span><span class="sxs-lookup"><span data-stu-id="aa0b9-169">Update Cluster Tags</span></span>

<span data-ttu-id="aa0b9-170">Puede actualizar las etiquetas de un clúster determinado de este modo:</span><span class="sxs-lookup"><span data-stu-id="aa0b9-170">You can update the tags of a given cluster like so:</span></span>

```java
client.clusters.update("<Resource Group Name>", "<Cluster Name>", <Map<String,String> of Tags>);
```

### <a name="resize-cluster"></a><span data-ttu-id="aa0b9-171">Cambio del tamaño de clúster</span><span class="sxs-lookup"><span data-stu-id="aa0b9-171">Resize Cluster</span></span>

<span data-ttu-id="aa0b9-172">Para cambiar el tamaño de un número de nodos de trabajo de un clúster determinado, puede especificar un nuevo tamaño como sigue:</span><span class="sxs-lookup"><span data-stu-id="aa0b9-172">You can resize a given cluster's number of worker nodes by specifying a new size like so:</span></span>

```java
client.clusters.resize("<Resource Group Name>", "<Cluster Name>", <Num of Worker Nodes (int)>)
```

## <a name="cluster-monitoring"></a><span data-ttu-id="aa0b9-173">Supervisión de clústeres</span><span class="sxs-lookup"><span data-stu-id="aa0b9-173">Cluster Monitoring</span></span>

<span data-ttu-id="aa0b9-174">El SDK de administración de HDInsight también puede utilizarse para administrar la supervisión en los clústeres mediante Operations Management Suite (OMS).</span><span class="sxs-lookup"><span data-stu-id="aa0b9-174">The HDInsight Management SDK can also be used to manage monitoring on your clusters via the Operations Management Suite (OMS).</span></span>

### <a name="enable-oms-monitoring"></a><span data-ttu-id="aa0b9-175">Habilitación de OMS Monitoring</span><span class="sxs-lookup"><span data-stu-id="aa0b9-175">Enable OMS Monitoring</span></span>

> [!NOTE]
> <span data-ttu-id="aa0b9-176">Para habilitar OMS Monitoring, debe tener un área de trabajo de Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="aa0b9-176">To enable OMS Monitoring, you must have an existing Log Analytics workspace.</span></span> <span data-ttu-id="aa0b9-177">Si aún no ha creado una, puede aprender a hacerlo aquí: [Creación de un área de trabajo de Log Analytics en Azure Portal](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-quick-create-workspace).</span><span class="sxs-lookup"><span data-stu-id="aa0b9-177">If you have not already created one, you can learn how to do that here: [Create a Log Analytics workspace in the Azure portal](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-quick-create-workspace).</span></span>

<span data-ttu-id="aa0b9-178">Para habilitar OMS Monitoring en el clúster:</span><span class="sxs-lookup"><span data-stu-id="aa0b9-178">To enable OMS Monitoring on your cluster:</span></span>

```java
client.extensions().enableMonitoring("<Resource Group Name", "<Cluster Name>", new ClusterMonitoringRequest().withWorkspaceId("<Workspace Id>"));
```

### <a name="view-status-of-oms-monitoring"></a><span data-ttu-id="aa0b9-179">Ver el estado de OMS Monitoring</span><span class="sxs-lookup"><span data-stu-id="aa0b9-179">View Status Of OMS Monitoring</span></span>

<span data-ttu-id="aa0b9-180">Para obtener el estado de OMS en el clúster:</span><span class="sxs-lookup"><span data-stu-id="aa0b9-180">To get the status of OMS on your cluster:</span></span>

```java
client.extensions().getMonitoringStatus("<Resource Group Name", "Cluster Name");
```

### <a name="disable-oms-monitoring"></a><span data-ttu-id="aa0b9-181">Deshabilitación de OMS Monitoring</span><span class="sxs-lookup"><span data-stu-id="aa0b9-181">Disable OMS Monitoring</span></span>

<span data-ttu-id="aa0b9-182">Para deshabilitar OMS en el clúster:</span><span class="sxs-lookup"><span data-stu-id="aa0b9-182">To disable OMS on your cluster:</span></span>

```java
client.extensions().disableMonitoring("<Resource Group Name>", "<Cluster Name>");
```

## <a name="script-actions"></a><span data-ttu-id="aa0b9-183">Acciones de script</span><span class="sxs-lookup"><span data-stu-id="aa0b9-183">Script Actions</span></span>

<span data-ttu-id="aa0b9-184">HDInsight proporciona un método de configuración llamado acciones de script, que invoca scripts personalizados para personalizar el clúster.</span><span class="sxs-lookup"><span data-stu-id="aa0b9-184">HDInsight provides a configuration method called script actions that invokes custom scripts to customize the cluster.</span></span>
> [!NOTE]
> <span data-ttu-id="aa0b9-185">Encontrará más información sobre cómo usar acciones de script aquí: [Personalización de clústeres de HDInsight basados en Linux mediante acciones de script](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux)</span><span class="sxs-lookup"><span data-stu-id="aa0b9-185">More information on how to use script actions can be found here: [Customize Linux-based HDInsight clusters using script actions](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux)</span></span>

### <a name="execute-script-actions"></a><span data-ttu-id="aa0b9-186">Ejecución de acciones de script</span><span class="sxs-lookup"><span data-stu-id="aa0b9-186">Execute Script Actions</span></span>

<span data-ttu-id="aa0b9-187">Puede ejecutar acciones de script en un clúster determinado de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="aa0b9-187">You can execute script actions on a given cluster like so:</span></span>

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

### <a name="delete-script-action"></a><span data-ttu-id="aa0b9-188">Eliminación de una acción de script</span><span class="sxs-lookup"><span data-stu-id="aa0b9-188">Delete Script Action</span></span>

<span data-ttu-id="aa0b9-189">Para eliminar una acción de script persistente específica en un clúster determinado:</span><span class="sxs-lookup"><span data-stu-id="aa0b9-189">To delete a specified persisted script action on a given cluster:</span></span>

```java
client.scriptActions().delete("<Resource Group Name>", "<Cluster Name>", "<Script Name>");
```

### <a name="list-persisted-script-actions"></a><span data-ttu-id="aa0b9-190">Lista de acciones de script persistentes</span><span class="sxs-lookup"><span data-stu-id="aa0b9-190">List Persisted Script Actions</span></span>

> [!NOTE]
> <span data-ttu-id="aa0b9-191">El método `listByCluster()` devuelve un objeto `PagedList<RuntimeScriptActionDetailInner>`.</span><span class="sxs-lookup"><span data-stu-id="aa0b9-191">Both `listByCluster()` returns a `PagedList<RuntimeScriptActionDetailInner>` object.</span></span> <span data-ttu-id="aa0b9-192">Una llamada a `currentPage().items()` devuelve una lista de `RuntimeScriptActionDetailInner` y `loadNextPage()` avanza a la página siguiente.</span><span class="sxs-lookup"><span data-stu-id="aa0b9-192">Calling `currentPage().items()` returns a list of `RuntimeScriptActionDetailInner`, and `loadNextPage()` advances to the next page.</span></span> <span data-ttu-id="aa0b9-193">Esto se puede repetir hasta que `hasNextPage()` devuelva `false`, que indica que no existen más páginas.</span><span class="sxs-lookup"><span data-stu-id="aa0b9-193">This can be repeated until `hasNextPage()` returns `false`, indicating that there are no more pages.</span></span>

<span data-ttu-id="aa0b9-194">Para mostrar una lista de todas las acciones de script persistentes para el clúster especificado:</span><span class="sxs-lookup"><span data-stu-id="aa0b9-194">To list all persisted script actions for the specified cluster:</span></span>
```java
client.scriptActions().listByCluster("<Resource Group Name>", "<Cluster Name>");
```

#### <a name="example"></a><span data-ttu-id="aa0b9-195">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="aa0b9-195">Example</span></span>

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

### <a name="list-all-scripts-execution-history"></a><span data-ttu-id="aa0b9-196">Lista del historial de ejecución de todos los scripts</span><span class="sxs-lookup"><span data-stu-id="aa0b9-196">List All Scripts' Execution History</span></span>

<span data-ttu-id="aa0b9-197">Para mostrar una lista del historial de ejecución de todos los scripts para el clúster especificado:</span><span class="sxs-lookup"><span data-stu-id="aa0b9-197">To list all scripts' execution history for the specified cluster:</span></span>

```java
client.scriptExecutionHistorys().listByCluster("<Resource Group Name>", "<Cluster Name>");
```

#### <a name="example"></a><span data-ttu-id="aa0b9-198">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="aa0b9-198">Example</span></span>

<span data-ttu-id="aa0b9-199">Este ejemplo imprime todos los detalles de todas las ejecuciones de script pasadas.</span><span class="sxs-lookup"><span data-stu-id="aa0b9-199">This example prints all the details for all past script executions.</span></span>

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
