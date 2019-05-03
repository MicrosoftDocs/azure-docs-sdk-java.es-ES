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
ms.openlocfilehash: fdf0334a8796d636a1968943cc34d7ae98d6361c
ms.sourcegitcommit: c2019ba6da6c7c28b17b5a85f89e49bb5e570ba4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2018
ms.locfileid: "44040263"
---
# <a name="get-started-with-cloud-development-using-java-on-azure"></a><span data-ttu-id="b44d0-104">Introducción al desarrollo de soluciones para la nube con Java en Azure</span><span class="sxs-lookup"><span data-stu-id="b44d0-104">Get started with cloud development using Java on Azure</span></span>

<span data-ttu-id="b44d0-105">Esta guía ayuda a configurar un entorno de desarrollo para desarrollar en Java para Azure.</span><span class="sxs-lookup"><span data-stu-id="b44d0-105">This guide walks you through setting up a development environment for Azure development in Java.</span></span> <span data-ttu-id="b44d0-106">Después, creará algunos recursos de Azure y los conectará para realizar algunas tareas básicas, como cargar un archivo o implementar una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="b44d0-106">You'll then create some Azure resources and connect them to to perform some basic tasks, like uploading a file or deploying a web application.</span></span> <span data-ttu-id="b44d0-107">Cuando haya terminado, estará listo para comenzar a usar los servicios de Azure en sus propias aplicaciones de Java.</span><span class="sxs-lookup"><span data-stu-id="b44d0-107">When you're done, you'll be ready to start using Azure services in your own Java applications.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b44d0-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="b44d0-108">Prerequisites</span></span>

- <span data-ttu-id="b44d0-109">Una cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="b44d0-109">An Azure account.</span></span> <span data-ttu-id="b44d0-110">Si no tiene una, [consiga una evaluación gratuita](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="b44d0-110">If you don't have one, [get a free trial](https://azure.microsoft.com/free/)</span></span>
- <span data-ttu-id="b44d0-111">[Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/quickstart) o [CLI de Azure 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="b44d0-111">[Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/quickstart) or [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2).</span></span>
- <span data-ttu-id="b44d0-112">[Java 8](https://www.azul.com/downloads/zulu/) (incluido en Azure Cloud Shell)</span><span class="sxs-lookup"><span data-stu-id="b44d0-112">[Java 8](https://www.azul.com/downloads/zulu/) (included in Azure Cloud Shell)</span></span>
- <span data-ttu-id="b44d0-113">[Maven 3](http://maven.apache.org/download.cgi) (incluido en Azure Cloud Shell)</span><span class="sxs-lookup"><span data-stu-id="b44d0-113">[Maven 3](http://maven.apache.org/download.cgi) (included in Azure Cloud Shell)</span></span>

## <a name="set-up-authentication"></a><span data-ttu-id="b44d0-114">Configuración de la autenticación</span><span class="sxs-lookup"><span data-stu-id="b44d0-114">Set up authentication</span></span>

<span data-ttu-id="b44d0-115">La aplicación Java necesita leer y crear permisos en su suscripción de Azure para ejecutar el código de ejemplo de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="b44d0-115">Your Java application needs read and create permissions in your Azure subscription to run the sample code in this tutorial.</span></span> <span data-ttu-id="b44d0-116">Cree una entidad de servicio y configure la aplicación para que se ejecute con sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="b44d0-116">Create a service principal and configure your application to run with its credentials.</span></span> <span data-ttu-id="b44d0-117">Las entidades de servicio proporcionan una manera de crear una cuenta no interactiva asociada con su identidad a la que conceder únicamente los privilegios que la aplicación necesita para la ejecución.</span><span class="sxs-lookup"><span data-stu-id="b44d0-117">Service principals provide a way to create a non-interactive account associated with your identity to which you grant only the privileges your app needs to run.</span></span>

<span data-ttu-id="b44d0-118">[Cree una entidad de servicio mediante la CLI de Azure 2.0](/cli/azure/create-an-azure-service-principal-azure-cli) y capture la salida.</span><span class="sxs-lookup"><span data-stu-id="b44d0-118">[Create a service principal using the Azure CLI 2.0](/cli/azure/create-an-azure-service-principal-azure-cli) and capture the output.</span></span> <span data-ttu-id="b44d0-119">Proporcione una [contraseña segura](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-policy) en el argumento de contraseña en lugar de `MY_SECURE_PASSWORD`.</span><span class="sxs-lookup"><span data-stu-id="b44d0-119">Provide a [secure password](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-policy) in the password argument instead of `MY_SECURE_PASSWORD`.</span></span> <span data-ttu-id="b44d0-120">La contraseña debe tener de 8 a 16 caracteres y cumplir al menos tres de los siguientes cuatro criterios:</span><span class="sxs-lookup"><span data-stu-id="b44d0-120">Your password must be 8 to 16 characters and match at least 3 out of the 4 following criteria:</span></span>

* <span data-ttu-id="b44d0-121">Incluir caracteres en minúsculas.</span><span class="sxs-lookup"><span data-stu-id="b44d0-121">Include lowercase characters</span></span>
* <span data-ttu-id="b44d0-122">Incluir caracteres en mayúsculas.</span><span class="sxs-lookup"><span data-stu-id="b44d0-122">Include uppercase characters</span></span>
* <span data-ttu-id="b44d0-123">Incluir números.</span><span class="sxs-lookup"><span data-stu-id="b44d0-123">Include numbers</span></span>
* <span data-ttu-id="b44d0-124">Incluir uno de los siguientes símbolos: @ # $ % ^ & \* - _ !</span><span class="sxs-lookup"><span data-stu-id="b44d0-124">Include one of the following symbols: @ # $ % ^ & \* - _ !</span></span> <span data-ttu-id="b44d0-125">+ = [ ] { } | \ : ‘ , .</span><span class="sxs-lookup"><span data-stu-id="b44d0-125">+ = [ ] { } | \ : ‘ , .</span></span> <span data-ttu-id="b44d0-126">?</span><span class="sxs-lookup"><span data-stu-id="b44d0-126">?</span></span> <span data-ttu-id="b44d0-127">/ \` ~ “ ( ) ;</span><span class="sxs-lookup"><span data-stu-id="b44d0-127">/ \` ~ “ ( ) ;</span></span>


```azurecli-interactive
az ad sp create-for-rbac --name AzureJavaTest --password "MY_SECURE_PASSWORD"
```

<span data-ttu-id="b44d0-128">Lo que da una respuesta con el siguiente formato:</span><span class="sxs-lookup"><span data-stu-id="b44d0-128">Which gives you a reply in the following format:</span></span>

```json
{
  "appId": "a487e0c1-82af-47d9-9a0b-af184eb87646d",
  "displayName": "AzureJavaTest",
  "name": "http://AzureJavaTest",
  "password": password,
  "tenant": "tttttttt-tttt-tttt-tttt-tttttttttttt"
}
```

<span data-ttu-id="b44d0-129">A continuación, copie lo siguiente en un archivo de texto en el sistema:</span><span class="sxs-lookup"><span data-stu-id="b44d0-129">Next, copy the following into a text file on your system:</span></span>

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

<span data-ttu-id="b44d0-130">Reemplace los primeros cuatro valores por lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="b44d0-130">Replace the top four values with the following:</span></span>

- <span data-ttu-id="b44d0-131">subscription: use el valor de *id* que se muestra con el comando `az account show` en la CLI de Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="b44d0-131">subscription: use the *id* value from `az account show` in the Azure CLI 2.0.</span></span>
- <span data-ttu-id="b44d0-132">client: use el valor de *appId* procedente de la salida de una entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="b44d0-132">client: use the *appId* value from the output taken from a service principal output.</span></span>
- <span data-ttu-id="b44d0-133">key: use el valor de *password* procedente de la salida de la entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="b44d0-133">key: use the *password* value from the service principal output.</span></span>
- <span data-ttu-id="b44d0-134">tenant: use el valor de *tenant* procedente de la salida de la entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="b44d0-134">tenant: use the *tenant* value from the service principal output.</span></span>

<span data-ttu-id="b44d0-135">Guarde este archivo en una ubicación segura en el sistema donde el código pueda leerlo.</span><span class="sxs-lookup"><span data-stu-id="b44d0-135">Save this file in a secure location on your system where your code can read it.</span></span> <span data-ttu-id="b44d0-136">Dado que este archivo se puede usar para código futuro, se recomienda guardarlo en un lugar externo a la aplicación de este artículo.</span><span class="sxs-lookup"><span data-stu-id="b44d0-136">You may use this file for future code so it's recommended to store it somewhere external to the application in this article.</span></span>

<span data-ttu-id="b44d0-137">Establezca una variable de entorno `AZURE_AUTH_LOCATION` con la ruta de acceso completa al archivo de autenticación en el shell.</span><span class="sxs-lookup"><span data-stu-id="b44d0-137">Set an environment variable `AZURE_AUTH_LOCATION` with the full path to the authentication file in your shell.</span></span>   

```bash
export AZURE_AUTH_LOCATION=/Users/raisa/azureauth.properties
```

<span data-ttu-id="b44d0-138">Si trabaja en un entorno Windows, agregue la variable a las propiedades del sistema.</span><span class="sxs-lookup"><span data-stu-id="b44d0-138">If you're working in a windows environment, add the variable to your system properties.</span></span> <span data-ttu-id="b44d0-139">Abra una ventana de PowerShell con privilegios de administrador y, después de reemplazar la segunda variable por la ruta de acceso al archivo, escriba el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="b44d0-139">Open a PowerShell window with administrator privledges and, after replacing the second variable with the path to your file, enter the following command:</span></span>

```powershell
setx AZURE_AUTH_LOCATION "C:\<fullpath>\azureauth.properties" /m
```

## <a name="tooling"></a><span data-ttu-id="b44d0-140">Herramientas</span><span class="sxs-lookup"><span data-stu-id="b44d0-140">Tooling</span></span>

### <a name="create-a-new-maven-project"></a><span data-ttu-id="b44d0-141">Creación de un nuevo proyecto de Maven</span><span class="sxs-lookup"><span data-stu-id="b44d0-141">Create a new Maven project</span></span>

> [!NOTE]
> <span data-ttu-id="b44d0-142">Esta guía usa la herramienta de compilación de Maven para compilar y ejecutar el código de ejemplo, pero otras herramientas de compilación como Gradle también funcionan con las bibliotecas de Azure para Java.</span><span class="sxs-lookup"><span data-stu-id="b44d0-142">This guide uses Maven build tool to build and run the sample code, but other build tools such as Gradle also work with the Azure libraries for Java.</span></span> 

<span data-ttu-id="b44d0-143">Cree un proyecto de Maven desde la línea de comandos en un nuevo directorio en el sistema:</span><span class="sxs-lookup"><span data-stu-id="b44d0-143">Create a Maven project from the command line in a new directory on your system:</span></span>

```
mkdir java-azure-test
cd java-azure-test
mvn archetype:generate -DgroupId=com.fabrikam -DartifactId=AzureApp  \ 
-DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
```

<span data-ttu-id="b44d0-144">Esto crea un proyecto básico de Maven bajo la carpeta `testAzureApp`.</span><span class="sxs-lookup"><span data-stu-id="b44d0-144">This creates a basic Maven project under the `testAzureApp` folder.</span></span> <span data-ttu-id="b44d0-145">Agregue las siguientes entradas en el archivo `pom.xml` del proyecto para importar las bibliotecas que se utilizan en el código de ejemplo en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="b44d0-145">Add the following entries into the project `pom.xml` to import the libraries used in the sample code in this tutorial.</span></span>

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

<span data-ttu-id="b44d0-146">Agregue una entrada `build` bajo el elemento de nivel superior `project` para usar [maven-exec-plugin](http://www.mojohaus.org/exec-maven-plugin/) para ejecutar los ejemplos:</span><span class="sxs-lookup"><span data-stu-id="b44d0-146">Add a `build` entry under the top-level `project` element to use the [maven-exec-plugin](http://www.mojohaus.org/exec-maven-plugin/) to run the samples:</span></span>

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

### <a name="install-the-azure-toolkit-for-intellij"></a><span data-ttu-id="b44d0-147">Instalación del kit de herramientas de Azure para IntelliJ</span><span class="sxs-lookup"><span data-stu-id="b44d0-147">Install the Azure Toolkit for Intellij</span></span>

<span data-ttu-id="b44d0-148">El [kit de herramientas de Azure](intellij/azure-toolkit-for-intellij-installation.md) se necesita si se van a implementar aplicaciones web o API mediante programación, pero no se usa en ningún otro tipo de implementación.</span><span class="sxs-lookup"><span data-stu-id="b44d0-148">The [Azure toolkit](intellij/azure-toolkit-for-intellij-installation.md) is necessary if you're going to be deploying web apps or APIs programmatically but is not currently used for any other kinds of development.</span></span> <span data-ttu-id="b44d0-149">El siguiente es el resumen del proceso de instalación.</span><span class="sxs-lookup"><span data-stu-id="b44d0-149">The following is a summary of the installation process.</span></span> <span data-ttu-id="b44d0-150">Para obtener los pasos detallados, consulte [Instalación del Kit de herramientas de Azure para IntelliJ](intellij/azure-toolkit-for-intellij-installation.md).</span><span class="sxs-lookup"><span data-stu-id="b44d0-150">For detailed stpes, visit [Installing the Azure Toolkit for IntelliJ](intellij/azure-toolkit-for-intellij-installation.md).</span></span>

<span data-ttu-id="b44d0-151">Seleccione el menú **File** (Archivo) y, luego, seleccione **Settings...** (Configuración...).</span><span class="sxs-lookup"><span data-stu-id="b44d0-151">Select the **File** menu and then select **Settings...**.</span></span> 

<span data-ttu-id="b44d0-152">Seleccione **Browse repositories...** (Examinar repositorios...) y busque "Azure"; instale **Azure toolkit for Intellij** (Kit de herramientas de Azure para Intellij).</span><span class="sxs-lookup"><span data-stu-id="b44d0-152">Select **Browse repositories...** and then search "Azure" and install the **Azure toolkit for Intellij**.</span></span>

<span data-ttu-id="b44d0-153">Reinicie Intellij.</span><span class="sxs-lookup"><span data-stu-id="b44d0-153">Restart Intellij.</span></span>

### <a name="install-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="b44d0-154">Instalación del kit de herramientas de Azure para Eclipse</span><span class="sxs-lookup"><span data-stu-id="b44d0-154">Install the Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="b44d0-155">El [kit de herramientas de Azure](eclipse/azure-toolkit-for-eclipse.md) se necesita si se van a implementar aplicaciones web o API mediante programación, pero no se usa en ningún otro tipo de implementación.</span><span class="sxs-lookup"><span data-stu-id="b44d0-155">The [Azure toolkit](eclipse/azure-toolkit-for-eclipse.md) is necessary if you're going to be deploying web apps or APIs programmatically but is not currently used for any other kinds of development.</span></span> <span data-ttu-id="b44d0-156">El siguiente es el resumen del proceso de instalación.</span><span class="sxs-lookup"><span data-stu-id="b44d0-156">The following is a summary of the installation process.</span></span> <span data-ttu-id="b44d0-157">Para obtener los pasos detallados, consulte [Instalación del kit de herramientas de Azure para Eclipse](eclipse/azure-toolkit-for-eclipse.md).</span><span class="sxs-lookup"><span data-stu-id="b44d0-157">For detailed stpes, visit [Installing the Azure Toolkit for Eclipse](eclipse/azure-toolkit-for-eclipse.md).</span></span>

<span data-ttu-id="b44d0-158">En el menú **Help** (Ayuda), seleccione **Install New Software** (Instalar nuevo software).</span><span class="sxs-lookup"><span data-stu-id="b44d0-158">Select the **Help** menu and then select **Install New software**.</span></span>

<span data-ttu-id="b44d0-159">En el campo **Work with:** (Trabajar con:), escriba `http://dl.microsoft.com/eclipse` y presione ENTRAR.</span><span class="sxs-lookup"><span data-stu-id="b44d0-159">In the **Work with:** field enter `http://dl.microsoft.com/eclipse` and press enter.</span></span>

<span data-ttu-id="b44d0-160">Después, active la casilla situada junto a **Azure toolkit for Java** (Kit de herramientas de Azure para Java) y desactive la casilla **Contact all update sites during install to find required software** (Conectar con todos los sitios de actualización durante la instalación para buscar el software necesario).</span><span class="sxs-lookup"><span data-stu-id="b44d0-160">Then, select the checkbox next to **Azure toolkit for Java** and uncheck the checkbox for **Contact all update sites during install to find required software**.</span></span> <span data-ttu-id="b44d0-161">Después, seleccione Next (Siguiente).</span><span class="sxs-lookup"><span data-stu-id="b44d0-161">Then select next.</span></span>

## <a name="create-a-linux-virtual-machine"></a><span data-ttu-id="b44d0-162">Creación de una máquina virtual con Linux</span><span class="sxs-lookup"><span data-stu-id="b44d0-162">Create a Linux virtual machine</span></span>

<span data-ttu-id="b44d0-163">Cree un nuevo archivo denominado `AzureApp.java` en el directorio `src/main/java/com/fabirkam` del proyecto y pegue el siguiente bloque de código.</span><span class="sxs-lookup"><span data-stu-id="b44d0-163">Create a new file named `AzureApp.java` in the project's `src/main/java/com/fabirkam` directory and paste in the following block of code.</span></span> <span data-ttu-id="b44d0-164">Actualice las variables `userName` y `sshKey` con los valores reales de la máquina.</span><span class="sxs-lookup"><span data-stu-id="b44d0-164">Update the `userName` and `sshKey` variables with real values for your machine.</span></span> <span data-ttu-id="b44d0-165">El código crea una nueva máquina virtual Linux con el nombre `testLinuxVM` en el grupo de recursos `sampleResourceGroup` en la región de Azure Este de EE. UU.</span><span class="sxs-lookup"><span data-stu-id="b44d0-165">The code creates a new Linux VM with name `testLinuxVM` in a resource group `sampleResourceGroup` running in the US East Azure region.</span></span>

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

<span data-ttu-id="b44d0-166">Ejecute el ejemplo desde la línea de comandos:</span><span class="sxs-lookup"><span data-stu-id="b44d0-166">Run the sample from the command line:</span></span>

```
mvn compile exec:java
```

<span data-ttu-id="b44d0-167">Podrá ver algunas solicitudes REST y respuestas en la consola a medida que el SDK realiza las llamadas subyacentes a la API de REST de Azure para configurar la máquina virtual y sus recursos.</span><span class="sxs-lookup"><span data-stu-id="b44d0-167">You'll see some REST requests and responses in the console as the SDK makes the underlying calls to the Azure REST API to configure the virtual machine and its resources.</span></span> <span data-ttu-id="b44d0-168">Cuando finalice el programa, compruebe la máquina virtual en la suscripción con la CLI de Azure 2.0:</span><span class="sxs-lookup"><span data-stu-id="b44d0-168">When the program finishes, verify the virtual machine in your subscription with the Azure CLI 2.0:</span></span>

```azurecli-interactive
az vm list --resource-group sampleVmResourceGroup
```

<span data-ttu-id="b44d0-169">Una vez que haya comprobado que el código ha funcionado, utilice la CLI para eliminar la máquina virtual y sus recursos.</span><span class="sxs-lookup"><span data-stu-id="b44d0-169">Once you've verified that the code worked, use the CLI to delete the VM and its resources.</span></span>

```azurecli-interactive
az group delete --name sampleVmResourceGroup
```

## <a name="deploy-a-web-app-from-a-github-repo"></a><span data-ttu-id="b44d0-170">Implementación de una aplicación web desde un repositorio de GitHub</span><span class="sxs-lookup"><span data-stu-id="b44d0-170">Deploy a web app from a GitHub repo</span></span>

<span data-ttu-id="b44d0-171">Reemplace el método main en `AzureApp.java` por el siguiente, actualizando la variable `appName` a un valor único antes de ejecutar el código.</span><span class="sxs-lookup"><span data-stu-id="b44d0-171">Replace the main method in `AzureApp.java` with the one below, updating the `appName` variable to a unique value before running the code.</span></span> <span data-ttu-id="b44d0-172">Este código implementa una aplicación web desde la rama `master` en un repositorio de GitHub público en una nueva [aplicación web de Azure App Service](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) que se ejecuta en el plan de tarifa gratuito.</span><span class="sxs-lookup"><span data-stu-id="b44d0-172">This code deploys a web application from the `master` branch in a public GitHub repo into a new [Azure App Service Web App](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) running in the free pricing tier.</span></span>

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

<span data-ttu-id="b44d0-173">Ejecute el código igual que antes mediante Maven:</span><span class="sxs-lookup"><span data-stu-id="b44d0-173">Run the code as before using Maven:</span></span>

```
mvn clean compile exec:java
```

<span data-ttu-id="b44d0-174">Abra un explorador que apunta a la aplicación mediante la CLI:</span><span class="sxs-lookup"><span data-stu-id="b44d0-174">Open a browser pointed to the application using the CLI:</span></span>

```azurecli-interactive
az appservice web browse --resource-group sampleWebResourceGroup --name YOUR_APP_NAME
```

<span data-ttu-id="b44d0-175">Elimine la aplicación web y el plan de su suscripción una vez que haya comprobado la implementación.</span><span class="sxs-lookup"><span data-stu-id="b44d0-175">Remove the web app and plan from your subscription once you've verified the deployment.</span></span>

```azurecli-interactive
az group delete --name sampleWebResourceGroup
```

## <a name="connect-to-an-azure-sql-database"></a><span data-ttu-id="b44d0-176">Conexión a una base de datos de Azure SQL</span><span class="sxs-lookup"><span data-stu-id="b44d0-176">Connect to an Azure SQL database</span></span>

<span data-ttu-id="b44d0-177">Reemplace el método main actual en `AzureApp.java` por el código siguiente y establezca un valor real para la variable `dbPassword`.</span><span class="sxs-lookup"><span data-stu-id="b44d0-177">Replace the current main method in `AzureApp.java` with the code below, setting a real value for the `dbPassword` variable.</span></span>
<span data-ttu-id="b44d0-178">Este código crea una nueva base de datos SQL con una regla de firewall que permite el acceso remoto y, a continuación, se conecta a ella con el controlador de JBDC de SQL Database.</span><span class="sxs-lookup"><span data-stu-id="b44d0-178">This code creates a new SQL database with a firewall rule allowing remote access,  and then connects to it using the SQL Database JBDC driver.</span></span> 

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
<span data-ttu-id="b44d0-179">Ejecute el ejemplo desde la línea de comandos:</span><span class="sxs-lookup"><span data-stu-id="b44d0-179">Run the sample from the command line:</span></span>

```
mvn clean compile exec:java
```

<span data-ttu-id="b44d0-180">A continuación, limpie los recursos mediante la CLI:</span><span class="sxs-lookup"><span data-stu-id="b44d0-180">Then clean up the resources using the CLI:</span></span>

```azurecli-interactive
az group delete --name sampleSqlResourceGroup
```

## <a name="write-a-blob-into-a-new-storage-account"></a><span data-ttu-id="b44d0-181">Escritura de un blob en una nueva cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="b44d0-181">Write a blob into a new storage account</span></span>

<span data-ttu-id="b44d0-182">Reemplace el método main actual en `AzureApp.java` por el código siguiente.</span><span class="sxs-lookup"><span data-stu-id="b44d0-182">Replace the current main method in `AzureApp.java` with the code below.</span></span> <span data-ttu-id="b44d0-183">Este código crea una [cuenta de Azure Storage](https://docs.microsoft.com/azure/storage/storage-introduction) y, a continuación, usa las bibliotecas de Azure Storage para Java para crear un nuevo archivo de texto en la nube.</span><span class="sxs-lookup"><span data-stu-id="b44d0-183">This code creates an [Azure storage account](https://docs.microsoft.com/azure/storage/storage-introduction) and then uses the Azure Storage libraries for Java to create a new text file in the cloud.</span></span>

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

<span data-ttu-id="b44d0-184">Ejecute el ejemplo desde la línea de comandos:</span><span class="sxs-lookup"><span data-stu-id="b44d0-184">Run the sample from the command line:</span></span>

```
mvn clean compile exec:java
```

<span data-ttu-id="b44d0-185">Puede buscar el archivo `helloazure.txt` en la cuenta de almacenamiento a través de Azure Portal o con [Azure Storage Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-explorer-blobs).</span><span class="sxs-lookup"><span data-stu-id="b44d0-185">You can browse for the `helloazure.txt` file in your storage account through the Azure portal or with [Azure Storage Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-explorer-blobs).</span></span>

<span data-ttu-id="b44d0-186">Limpie la cuenta de almacenamiento mediante la CLI:</span><span class="sxs-lookup"><span data-stu-id="b44d0-186">Clean up the storage account using the CLI:</span></span>

```azurecli-interactive
az group delete --name sampleStorageResourceGroup
```

## <a name="explore-more-samples"></a><span data-ttu-id="b44d0-187">Ver más ejemplos</span><span class="sxs-lookup"><span data-stu-id="b44d0-187">Explore more samples</span></span>

<span data-ttu-id="b44d0-188">Para más información sobre cómo usar las bibliotecas de administración de Azure para Java para administrar recursos y automatizar tareas, consulte nuestro código de ejemplo para [máquinas virtuales](java-sdk-azure-virtual-machine-samples.md), [aplicaciones web](java-sdk-azure-web-apps-samples.md) y [bases de datos SQL](java-sdk-azure-sql-database-samples.md).</span><span class="sxs-lookup"><span data-stu-id="b44d0-188">To learn more about how to use the Azure management libraries for Java to manage resources and automate tasks, see our sample code for [virtual machines](java-sdk-azure-virtual-machine-samples.md), [web apps](java-sdk-azure-web-apps-samples.md) and [SQL database](java-sdk-azure-sql-database-samples.md).</span></span>

## <a name="reference-and-release-notes"></a><span data-ttu-id="b44d0-189">Referencia y notas de la versión</span><span class="sxs-lookup"><span data-stu-id="b44d0-189">Reference and release notes</span></span>

<span data-ttu-id="b44d0-190">Hay una [referencia](http://docs.microsoft.com/java/api) disponible para todos los paquetes.</span><span class="sxs-lookup"><span data-stu-id="b44d0-190">A [reference](http://docs.microsoft.com/java/api) is available for all packages.</span></span>

## <a name="get-help-and-give-feedback"></a><span data-ttu-id="b44d0-191">Obtener ayuda y proporcionar comentarios</span><span class="sxs-lookup"><span data-stu-id="b44d0-191">Get help and give feedback</span></span>

<span data-ttu-id="b44d0-192">Puede publicar preguntas a la comunidad en [Stack Overflow](http://stackoverflow.com/questions/tagged/azure+java).</span><span class="sxs-lookup"><span data-stu-id="b44d0-192">Post questions to the community on [Stack Overflow](http://stackoverflow.com/questions/tagged/azure+java).</span></span> <span data-ttu-id="b44d0-193">Puede informar sobre errores y abrir incidencias con las bibliotecas de Azure para Java en el [proyecto en GitHub](https://github.com/Azure/azure-sdk-for-java).</span><span class="sxs-lookup"><span data-stu-id="b44d0-193">Report bugs and open issues against the Azure libraries for Java on the [project GitHub](https://github.com/Azure/azure-sdk-for-java).</span></span>
