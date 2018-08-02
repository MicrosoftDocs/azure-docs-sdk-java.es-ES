---
title: Introducción a las bibliotecas de Azure para Java
description: Aprenda a crear recursos de nube de Azure y a conectarlos y usarlos en las aplicaciones de Java.
keywords: Azure, Java, SDK, API, autenticación, introducción
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 04/16/2017
ms.topic: get-started-article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: multiple
ms.assetid: b1e10b79-f75e-4605-aecd-eed64873e2d3
ms.openlocfilehash: f069183c96cdc42d590d2e58a5a6a500be5ab69a
ms.sourcegitcommit: 720c2eaf66532d277015610ec375c71e934d9ee6
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
ms.locfileid: "29065532"
---
# <a name="get-started-with-cloud-development-using-the-azure-libraries-for-java"></a>Introducción al desarrollo de soluciones para la nube con las bibliotecas de Azure para Java

Esta guía ayuda a configurar un entorno de desarrollo para desarrollar en Java para Azure. Después, creará algunos recursos de Azure y los conectará para realizar algunas tareas básicas, como cargar un archivo o implementar una aplicación web. Cuando haya terminado, estará listo para comenzar a usar los servicios de Azure en sus propias aplicaciones de Java.

## <a name="prerequisites"></a>requisitos previos

- Una cuenta de Azure. Si no tiene una, [consiga una evaluación gratuita](https://azure.microsoft.com/free/).
- [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/quickstart) o [CLI de Azure 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2).
- [Java 8](https://www.azul.com/downloads/zulu/) (incluido en Azure Cloud Shell)
- [Maven 3](http://maven.apache.org/download.cgi) (incluido en Azure Cloud Shell)

## <a name="set-up-authentication"></a>Configuración de la autenticación

La aplicación Java necesita leer y crear permisos en su suscripción de Azure para ejecutar el código de ejemplo de este tutorial. Cree una entidad de servicio y configure la aplicación para que se ejecute con sus credenciales. Las entidades de servicio proporcionan una manera de crear una cuenta no interactiva asociada con su identidad a la que conceder únicamente los privilegios que la aplicación necesita para la ejecución.

[Cree una entidad de servicio mediante la CLI de Azure 2.0](/cli/azure/create-an-azure-service-principal-azure-cli) y capture la salida. Proporcione una [contraseña segura](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-policy) en el argumento de contraseña en lugar de `MY_SECURE_PASSWORD`. La contraseña debe tener de 8 a 16 caracteres y cumplir al menos tres de los siguientes cuatro criterios:

* Incluir caracteres en minúsculas.
* Incluir caracteres en mayúsculas.
* Incluir números.
* Incluir uno de los siguientes símbolos: @ # $ % ^ & * - _ ! + = [ ] { } | \ : ‘ , . ? / ` ~ “ ( ) ;


```azurecli-interactive
az ad sp create-for-rbac --name AzureJavaTest --password "MY_SECURE_PASSWORD"
```

Lo que da una respuesta con el siguiente formato:

```json
{
  "appId": "a487e0c1-82af-47d9-9a0b-af184eb87646d",
  "displayName": "AzureJavaTest",
  "name": "http://AzureJavaTest",
  "password": password,
  "tenant": "tttttttt-tttt-tttt-tttt-tttttttttttt"
}
```

A continuación, copie lo siguiente en un archivo de texto en el sistema:

```text
# sample management library properties file
subscription=ssssssss-ssss-ssss-ssss-ssssssssssss
client=cccccccc-cccc-cccc-cccc-cccccccccccc
key=kkkkkkkkkkkkkkkk
tenant=tttttttt-tttt-tttt-tttt-tttttttttttt
managementURI=https\://management.core.windows.net/
baseURL=https\://management.azure.com/
authURL=https\://login.windows.net/
graphURL=https\://graph.windows.net/
```

Reemplace los primeros cuatro valores por lo siguiente:

- subscription: use el valor de *id* que se muestra con el comando `az account show` en la CLI de Azure 2.0.
- client: use el valor de *appId* procedente de la salida de una entidad de servicio.
- key: use el valor de *password* procedente de la salida de la entidad de servicio.
- tenant: use el valor de *tenant* procedente de la salida de la entidad de servicio.

Guarde este archivo en una ubicación segura en el sistema donde el código pueda leerlo. Dado que este archivo se puede usar para código futuro, se recomienda guardarlo en un lugar externo a la aplicación de este artículo.

Establezca una variable de entorno `AZURE_AUTH_LOCATION` con la ruta de acceso completa al archivo de autenticación en el shell.   

```bash
export AZURE_AUTH_LOCATION=/Users/raisa/azureauth.properties
```

Si trabaja en un entorno Windows, agregue la variable a las propiedades del sistema. Abra una ventana de PowerShell con privilegios de administrador y, después de reemplazar la segunda variable por la ruta de acceso al archivo, escriba el siguiente comando:

```powershell
setx AZURE_AUTH_LOCATION "C:\<fullpath>\azureauth.properties" /m
```

## <a name="create-a-new-maven-project"></a>Creación de un nuevo proyecto de Maven

> [!NOTE]
> Esta guía usa la herramienta de compilación de Maven para compilar y ejecutar el código de ejemplo, pero otras herramientas de compilación como Gradle también funcionan con las bibliotecas de Azure para Java. 

Cree un proyecto de Maven desde la línea de comandos en un nuevo directorio en el sistema:

```
mkdir java-azure-test
cd java-azure-test
mvn archetype:generate -DgroupId=com.fabrikam -DartifactId=AzureApp  \ 
-DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
```

Esto crea un proyecto básico de Maven bajo la carpeta `testAzureApp`. Agregue las siguientes entradas en el archivo `pom.xml` del proyecto para importar las bibliotecas que se utilizan en el código de ejemplo en este tutorial.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure</artifactId>
    <version>1.3.0</version>
</dependency>
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-storage</artifactId>
    <version>5.0.0</version>
</dependency>
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>6.2.1.jre8</version>
</dependency>
```

Agregue una entrada `build` bajo el elemento de nivel superior `project` para usar [maven-exec-plugin](http://www.mojohaus.org/exec-maven-plugin/) para ejecutar los ejemplos:

```XML
<build>
    <plugins>
        <plugin>
            <groupId>org.codehaus.mojo</groupId>
            <artifactId>exec-maven-plugin</artifactId>
            <configuration>
                <mainClass>com.fabrikam.AzureApp</mainClass>
            </configuration>
        </plugin>
    </plugins>
</build>
 ```
   
## <a name="create-a-linux-virtual-machine"></a>Creación de una máquina virtual con Linux

Cree un nuevo archivo denominado `AzureApp.java` en el directorio `src/main/java/com/fabirkam` del proyecto y pegue el siguiente bloque de código. Actualice las variables `userName` y `sshKey` con los valores reales de la máquina. El código crea una nueva máquina virtual Linux con el nombre `testLinuxVM` en el grupo de recursos `sampleResourceGroup` en la región de Azure Este de EE. UU.

```java
package com.fabrikam;

import com.microsoft.azure.management.Azure;
import com.microsoft.azure.management.compute.VirtualMachine;
import com.microsoft.azure.management.compute.KnownLinuxVirtualMachineImage;
import com.microsoft.azure.management.compute.VirtualMachineSizeTypes;
import com.microsoft.azure.management.appservice.WebApp;
import com.microsoft.azure.management.storage.StorageAccount;
import com.microsoft.azure.management.storage.SkuName;
import com.microsoft.azure.management.storage.StorageAccountKey;
import com.microsoft.azure.management.sql.SqlDatabase;
import com.microsoft.azure.management.sql.SqlServer;
import com.microsoft.azure.management.resources.fluentcore.arm.Region;
import com.microsoft.azure.management.resources.fluentcore.utils.SdkContext;

import com.microsoft.rest.LogLevel;

import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;

import java.io.File;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.Statement;

public class AzureApp {

    public static void main(String[] args) {

        final String userName = "YOUR_VM_USERNAME";
        final String sshKey = "YOUR_PUBLIC_SSH_KEY";

        try {

            // use the properties file with the service principal information to authenticate
            // change the name of the environment variable if you used a different name in the previous step
            final File credFile = new File(System.getenv("AZURE_AUTH_LOCATION"));    
            Azure azure = Azure.configure()
                    .withLogLevel(LogLevel.BASIC)
                    .authenticate(credFile)
                    .withDefaultSubscription();
           
            // create a Ubuntu virtual machine in a new resource group 
            VirtualMachine linuxVM = azure.virtualMachines().define("testLinuxVM")
                    .withRegion(Region.US_EAST)
                    .withNewResourceGroup("sampleVmResourceGroup")
                    .withNewPrimaryNetwork("10.0.0.0/24")
                    .withPrimaryPrivateIPAddressDynamic()
                    .withoutPrimaryPublicIPAddress()
                    .withPopularLinuxImage(KnownLinuxVirtualMachineImage.UBUNTU_SERVER_16_04_LTS)
                    .withRootUsername(userName)
                    .withSsh(sshKey)
                    .withUnmanagedDisks()
                    .withSize(VirtualMachineSizeTypes.STANDARD_D3_V2)
                    .create();   

        } catch (Exception e) {
            System.out.println(e.getMessage());
            e.printStackTrace();
        }
    }
}
```

Ejecute el ejemplo desde la línea de comandos:

```
mvn compile exec:java
```

Podrá ver algunas solicitudes REST y respuestas en la consola a medida que el SDK realiza las llamadas subyacentes a la API de REST de Azure para configurar la máquina virtual y sus recursos. Cuando finalice el programa, compruebe la máquina virtual en la suscripción con la CLI de Azure 2.0:

```azurecli-interactive
az vm list --resource-group sampleVmResourceGroup
```

Una vez que haya comprobado que el código ha funcionado, utilice la CLI para eliminar la máquina virtual y sus recursos.

```azurecli-interactive
az group delete --name sampleVmResourceGroup
```

## <a name="deploy-a-web-app-from-a-github-repo"></a>Implementación de una aplicación web desde un repositorio de GitHub

Reemplace el método main en `AzureApp.java` por el siguiente, actualizando la variable `appName` a un valor único antes de ejecutar el código. Este código implementa una aplicación web desde la rama `master` en un repositorio de GitHub público en una nueva [aplicación web de Azure App Service](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) que se ejecuta en el plan de tarifa gratuito.

```java
    public static void main(String[] args) {
        try {

            final File credFile = new File(System.getenv("AZURE_AUTH_LOCATION"));
            final String appName = "YOUR_APP_NAME";

            Azure azure = Azure.configure()
                    .withLogLevel(LogLevel.BASIC)
                    .authenticate(credFile)
                    .withDefaultSubscription();

            WebApp app = azure.webApps().define(appName)
                    .withRegion(Region.US_WEST2)
                    .withNewResourceGroup("sampleWebResourceGroup")
                    .withNewWindowsPlan(PricingTier.FREE_F1)
                    .defineSourceControl()
                    .withPublicGitRepository(
                            "https://github.com/Azure-Samples/app-service-web-java-get-started")
                    .withBranch("master")
                    .attach()
                    .create();

        } catch (Exception e) {
            System.out.println(e.getMessage());
            e.printStackTrace();
        }
    }
```

Ejecute el código igual que antes mediante Maven:

```
mvn clean compile exec:java
```

Abra un explorador que apunta a la aplicación mediante la CLI:

```azurecli-interactive
az appservice web browse --resource-group sampleWebResourceGroup --name YOUR_APP_NAME
```

Elimine la aplicación web y el plan de su suscripción una vez que haya comprobado la implementación.

```azurecli-interactive
az group delete --name sampleWebResourceGroup
```

## <a name="connect-to-an-azure-sql-database"></a>Conexión a una base de datos SQL de Azure

Reemplace el método main actual en `AzureApp.java` por el código siguiente y establezca un valor real para la variable `dbPassword`.
Este código crea una nueva base de datos SQL con una regla de firewall que permite el acceso remoto y, a continuación, se conecta a ella con el controlador de JBDC de SQL Database. 

```java

    public static void main(String args[])
    {
        // create the db using the management libraries
        try {
            final File credFile = new File(System.getenv("AZURE_AUTH_LOCATION"));
            Azure azure = Azure.configure()
                    .withLogLevel(LogLevel.BASIC)
                    .authenticate(credFile)
                    .withDefaultSubscription();

            final String adminUser = SdkContext.randomResourceName("db",8);
            final String sqlServerName = SdkContext.randomResourceName("sql",10);
            final String sqlDbName = SdkContext.randomResourceName("dbname",8);
            final String dbPassword = "YOUR_PASSWORD_HERE";


            SqlServer sampleSQLServer = azure.sqlServers().define(sqlServerName)
                            .withRegion(Region.US_EAST)
                            .withNewResourceGroup("sampleSqlResourceGroup")
                            .withAdministratorLogin(adminUser)
                            .withAdministratorPassword(dbPassword)
                            .withNewFirewallRule("0.0.0.0","255.255.255.255")
                            .create();

            SqlDatabase sampleSQLDb = sampleSQLServer.databases().define(sqlDbName).create();

            // assemble the connection string to the database
            final String domain = sampleSQLServer.fullyQualifiedDomainName();
            String url = "jdbc:sqlserver://"+ domain + ":1433;" +
                    "database=" + sqlDbName +";" +
                    "user=" + adminUser+ "@" + sqlServerName + ";" +
                    "password=" + dbPassword + ";" +
                    "encrypt=true;trustServerCertificate=false;hostNameInCertificate=*.database.windows.net;loginTimeout=30;";

            // connect to the database, create a table and insert a entry into it
            Connection conn = DriverManager.getConnection(url);

            String createTable = "CREATE TABLE CLOUD ( name varchar(255), code int);";
            String insertValues = "INSERT INTO CLOUD (name, code ) VALUES ('Azure', 1);";
            String selectValues = "SELECT * FROM CLOUD";
            Statement createStatement = conn.createStatement();
            createStatement.execute(createTable);
            Statement insertStatement = conn.createStatement();
            insertStatement.execute(insertValues);
            Statement selectStatement = conn.createStatement();
            ResultSet rst = selectStatement.executeQuery(selectValues);

            while (rst.next()) {
                System.out.println(rst.getString(1) + " "
                        + rst.getString(2));
            }


        } catch (Exception e) {
            System.out.println(e.getMessage());
            System.out.println(e.getStackTrace().toString());
        }
    }
```
Ejecute el ejemplo desde la línea de comandos:

```
mvn clean compile exec:java
```

A continuación, limpie los recursos mediante la CLI:

```azurecli-interactive
az group delete --name sampleSqlResourceGroup
```

## <a name="write-a-blob-into-a-new-storage-account"></a>Escritura de un blob en una nueva cuenta de almacenamiento

Reemplace el método main actual en `AzureApp.java` por el código siguiente. Este código crea una [cuenta de Azure Storage](https://docs.microsoft.com/azure/storage/storage-introduction) y, a continuación, usa las bibliotecas de Azure Storage para Java para crear un nuevo archivo de texto en la nube.

```java
public static void main(String[] args) {

    try {

        // use the properties file with the service principal information to authenticate
        // change the name of the environment variable if you used a different name in the previous step
        final File credFile = new File(System.getenv("AZURE_AUTH_LOCATION"));
        Azure azure = Azure.configure()
                .withLogLevel(LogLevel.BASIC)
                .authenticate(credFile)
                .withDefaultSubscription();

        // create a new storage account
        String storageAccountName = SdkContext.randomResourceName("st",8);
        StorageAccount storage = azure.storageAccounts().define(storageAccountName)
                    .withRegion(Region.US_WEST2)
                    .withNewResourceGroup("sampleStorageResourceGroup")
                    .create();

        // create a storage container to hold the file
        List<StorageAccountKey> keys = storage.getKeys();
        final String storageConnection = "DefaultEndpointsProtocol=https;"
                + "AccountName=" + storage.name()
                + ";AccountKey=" + keys.get(0).value()
                + ";EndpointSuffix=core.windows.net";

        CloudStorageAccount account = CloudStorageAccount.parse(storageConnection);
        CloudBlobClient serviceClient = account.createCloudBlobClient();

        // Container name must be lower case.
        CloudBlobContainer container = serviceClient.getContainerReference("helloazure");
        container.createIfNotExists();

        // Make the container public
        BlobContainerPermissions containerPermissions = new BlobContainerPermissions();
        containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);
        container.uploadPermissions(containerPermissions);

        // write a blob to the container
        CloudBlockBlob blob = container.getBlockBlobReference("helloazure.txt");
        blob.uploadText("hello Azure");

    } catch (Exception e) {
        System.out.println(e.getMessage());
        e.printStackTrace();
    }
    }
}
```

Ejecute el ejemplo desde la línea de comandos:

```
mvn clean compile exec:java
```

Puede buscar el archivo `helloazure.txt` en la cuenta de almacenamiento a través de Azure Portal o con [Azure Storage Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-explorer-blobs).

Limpie la cuenta de almacenamiento mediante la CLI:

```azurecli-interactive
az group delete --name sampleStorageResourceGroup
```

## <a name="explore-more-samples"></a>Ver más ejemplos

Para más información sobre cómo usar las bibliotecas de administración de Azure para Java para administrar recursos y automatizar tareas, consulte nuestro código de ejemplo para [máquinas virtuales](java-sdk-azure-virtual-machine-samples.md), [aplicaciones web](java-sdk-azure-web-apps-samples.md) y [bases de datos SQL](java-sdk-azure-sql-database-samples.md).

## <a name="reference-and-release-notes"></a>Referencia y notas de la versión

Hay una [referencia](http://docs.microsoft.com/java/api) disponible para todos los paquetes.

## <a name="get-help-and-give-feedback"></a>Obtener ayuda y proporcionar comentarios

Puede publicar preguntas a la comunidad en [Stack Overflow](http://stackoverflow.com/questions/tagged/azure+java). Puede informar sobre errores y abrir incidencias con las bibliotecas de Azure para Java en el [proyecto en GitHub](https://github.com/Azure/azure-sdk-for-java).
