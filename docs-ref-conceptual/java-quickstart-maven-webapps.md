---
title: "Implementación de una aplicación web de Java en Azure en cinco minutos con Maven | Microsoft Docs"
description: "Crear e implementar una aplicación de Java compilada con Maven en Azure"
services: app-service\web
documentationcenter: 
author: rloutlaw
manager: douge
editor: 
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 03/17/2017
ms.author: routlaw
ms.openlocfilehash: 1adc0a104ba22bcd353664e68323165890e46c64
ms.sourcegitcommit: 30d502b3150fa14bcc1251f5f88c7c0dd83e531e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/12/2017
---
# <a name="create-and-deploy-a-java-app-to-azure-with-maven"></a><span data-ttu-id="6c7be-103">Crear e implementar una aplicación de Java en Azure con Maven</span><span class="sxs-lookup"><span data-stu-id="6c7be-103">Create and deploy a Java app to Azure with Maven</span></span>

<span data-ttu-id="6c7be-104">Esta guía de inicio rápido le ayuda a crear e implementar una sencilla aplicación web de Java en [Azure App Service](/azure/app-service/app-service-value-prop-what-is) en unos pocos minutos usando [Maven de Apache](http://maven.apache.org) y la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="6c7be-104">This quickstart helps you create and deploy a simple Java web app to [Azure App Service](/azure/app-service/app-service-value-prop-what-is) in just a few minutes using [Apache Maven](http://maven.apache.org) and the Azure CLI.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="6c7be-105">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="6c7be-105">Before you begin</span></span>

<span data-ttu-id="6c7be-106">Antes de empezar, configure lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="6c7be-106">Before you start, set up the following:</span></span>

- [<span data-ttu-id="6c7be-107">Git</span><span class="sxs-lookup"><span data-stu-id="6c7be-107">Git</span></span>](https://git-scm.com/)
- [<span data-ttu-id="6c7be-108">Java 8</span><span class="sxs-lookup"><span data-stu-id="6c7be-108">Java 8</span></span>](https://www.azul.com/downloads/zulu/)
- [<span data-ttu-id="6c7be-109">Maven 3</span><span class="sxs-lookup"><span data-stu-id="6c7be-109">Maven 3</span></span>](http://maven.apache.org/download.cgi)
- [<span data-ttu-id="6c7be-110">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="6c7be-110">Azure CLI 2.0</span></span>](https://docs.microsoft.com/cli/azure/install-az-cli2)

<span data-ttu-id="6c7be-111">Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de empezar.</span><span class="sxs-lookup"><span data-stu-id="6c7be-111">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="get-the-sample-code"></a><span data-ttu-id="6c7be-112">Obtención del código de ejemplo</span><span class="sxs-lookup"><span data-stu-id="6c7be-112">Get the sample code</span></span>

<span data-ttu-id="6c7be-113">Clone el repositorio de la aplicación de ejemplo en la máquina local.</span><span class="sxs-lookup"><span data-stu-id="6c7be-113">Clone the sample app repository to your local machine.</span></span> <span data-ttu-id="6c7be-114">El ejemplo es una sencilla aplicación de JSP con configuración adicional de Maven en el archivo `pom.xml` del proyecto para probar la aplicación localmente y ayudar a implementar el ejemplo en Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="6c7be-114">The sample is a simple JSP application with additional Maven configuration in the project `pom.xml` to test the app locally and help deploy the sample to Azure App Service.</span></span>

```
git clone https://github.com/Azure-Samples/app-service-maven
```

## <a name="run-the-app-locally"></a><span data-ttu-id="6c7be-115">Ejecución de la aplicación de forma local</span><span class="sxs-lookup"><span data-stu-id="6c7be-115">Run the app locally</span></span>

<span data-ttu-id="6c7be-116">Abra un símbolo del sistema y use Maven para compilar la aplicación y ejecutarla en un contenedor web local de [Tomcat](https://tomcat.apache.org).</span><span class="sxs-lookup"><span data-stu-id="6c7be-116">Open a command prompt and use Maven to build the app and run it in a local [Tomcat](https://tomcat.apache.org) web container.</span></span> 

```
cd app-service-maven
mvn package
mvn tomcat7:run-war
```

<span data-ttu-id="6c7be-117">Abra el explorador y navegue hasta http://localhost:8080 para previsualizar la aplicación:</span><span class="sxs-lookup"><span data-stu-id="6c7be-117">Open a web browser and navigate to http://localhost:8080 to preview the app:</span></span>

  ![Mensaje Hola mundo de la aplicación de ejemplo de Java](media/maven-quickstart/java-app-hello-world-output.png)

## <a name="log-in-to-azure"></a><span data-ttu-id="6c7be-119">Inicie sesión en Azure.</span><span class="sxs-lookup"><span data-stu-id="6c7be-119">Log in to Azure</span></span>

<span data-ttu-id="6c7be-120">Inicie sesión en la CLI de Azure con `az login`.</span><span class="sxs-lookup"><span data-stu-id="6c7be-120">Log in to the Azure CLI with `az login`.</span></span> <span data-ttu-id="6c7be-121">Este tutorial rápido usa la CLI para consultar y crear los recursos de Azure necesarios para hospedar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6c7be-121">This quickstart uses the CLI to query and create the Azure resources needed to host the app.</span></span>
   
```azurecli
az login
```

## <a name="create-a-resource-group"></a><span data-ttu-id="6c7be-122">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="6c7be-122">Create a resource group</span></span>   

<span data-ttu-id="6c7be-123">Cree un grupo de recursos con [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="6c7be-123">Create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="6c7be-124">Un grupo de recursos de Azure es un contenedor lógico en el que se implementan y se administran los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="6c7be-124">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span>

```azurecli
az group create --location "East US" --name myResourceGroup
```

<span data-ttu-id="6c7be-125">Para ver los valores posibles que puede usar para `---location`, use el comando [az appservice list-locations](/cli/azure/appservice#list-locations)</span><span class="sxs-lookup"><span data-stu-id="6c7be-125">To see other possible values you can use for `---location`, use [az appservice list-locations](/cli/azure/appservice#list-locations)</span></span>

## <a name="create-an-app-service-plan"></a><span data-ttu-id="6c7be-126">Creación de un plan de App Service</span><span class="sxs-lookup"><span data-stu-id="6c7be-126">Create an App Service plan</span></span>

<span data-ttu-id="6c7be-127">Cree un [plan de App Service](/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview) **GRATUITO** con [az appservice plan create](/cli/azure/appservice/plan#create).</span><span class="sxs-lookup"><span data-stu-id="6c7be-127">Create a **FREE** [App Service plan](/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview) using [az appservice plan create](/cli/azure/appservice/plan#create).</span></span> <span data-ttu-id="6c7be-128">Los planes de App Service asignan recursos compartidos entre todas las aplicaciones web que se ejecutan en el plan.</span><span class="sxs-lookup"><span data-stu-id="6c7be-128">App Service plans allocate resources shared across all web apps running in the plan.</span></span>


```azurecli
az appservice plan create --name my-free-appservice-plan --resource-group myResourceGroup --sku FREE
```

<span data-ttu-id="6c7be-129">Cuando se ha creado el plan de App Service, la CLI de Azure muestra información similar a la del ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="6c7be-129">When the App Service Plan is ready, the Azure CLI shows information similar to the following example:</span></span>

```json
{
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/my-free-appservice-plan",
    "location": "East US",
    "sku": {
    "capacity": 1,
    "family": "S",
    "name": "S1",
    "tier": "Standard"
    },
    "status": "Ready",
    "type": "Microsoft.Web/serverfarms"
}
```


## <a name="create-a-web-app"></a><span data-ttu-id="6c7be-130">Creación de una aplicación web</span><span class="sxs-lookup"><span data-stu-id="6c7be-130">Create a web app</span></span>

<span data-ttu-id="6c7be-131">Cree una aplicación web que use los recursos del plan mediante el comando [az webapp create](/cli/azure/appservice/web#create) de la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="6c7be-131">Create a web app that uses the plan's resources using the Azure CLI [az webapp create](/cli/azure/appservice/web#create) command.</span></span> <span data-ttu-id="6c7be-132">La definición de la aplicación web proporciona un espacio para implementar el código y una dirección URL para tener acceso a la aplicación una vez que se esté ejecutando.</span><span class="sxs-lookup"><span data-stu-id="6c7be-132">The web app definition provides a space to deploy the code to and a URL to access the app once it's running.</span></span>

<span data-ttu-id="6c7be-133">En el comando siguiente, sustituya su nombre de aplicación único donde vea el marcador de posición <appname>.</span><span class="sxs-lookup"><span data-stu-id="6c7be-133">In the command below substitute your own unique app name where you see the <appname> placeholder.</span></span> <span data-ttu-id="6c7be-134"><appname> se utiliza en el nombre de host predeterminado para la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="6c7be-134">The <appname> is used in the default hostname for the web app.</span></span> <span data-ttu-id="6c7be-135">Si <appname> no es único, obtendrá el mensaje de error descriptivo "Ya existe un sitio web con el nombre especificado."</span><span class="sxs-lookup"><span data-stu-id="6c7be-135">If <appname> is not unique, you get the friendly error message "Website with given name already exists."</span></span>

```azurecli
az webapp create --name appname --resource-group myResourceGroup --plan my-free-appservice-plan
```

<span data-ttu-id="6c7be-136">Cuando se ha creado la aplicación web, la CLI de Azure muestra información similar a la del ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="6c7be-136">When the Web App has been created, the Azure CLI shows information similar to the following example.1</span></span>

```json
{
    "clientAffinityEnabled": true,
    "defaultHostName": "<appname>.azurewebsites.net",
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/sites/<appname>",
    "isDefaultContainer": null,
    "kind": "app",
    "location": "East US",
    "name": "<app_name>",
    "repositorySiteName": "<app_name>",
    "reserved": true,
    "resourceGroup": "myResourceGroup",
    "serverFarmId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/my-free-appservice-plan",
    "state": "Running",
    "type": "Microsoft.Web/sites",
}
```

## <a name="configure-java-and-tomcat"></a><span data-ttu-id="6c7be-137">Configuración de Java y Tomcat</span><span class="sxs-lookup"><span data-stu-id="6c7be-137">Configure Java and Tomcat</span></span>

<span data-ttu-id="6c7be-138">Configurar la aplicación web para usar Java y Tomcat mediante el comando [az webapp config](/cli/azure/appservice/web#config) de la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="6c7be-138">Configure the web app to use Java and Tomcat using the Azure CLI's [az webapp config](/cli/azure/appservice/web#config) command.</span></span> <span data-ttu-id="6c7be-139">En el ejemplo siguiente se configura App Service para ejecutar Java 8 y [Apache Tomcat 8.5](http://tomcat.apache.org/) para ejecutar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6c7be-139">The example below configures App Service to run Java 8 and [Apache Tomcat 8.5](http://tomcat.apache.org/) to run the app.</span></span>

```azurecli
az webapp config set \ 
--name appname \
--resource-group myResourceGroup \
--java-container TOMCAT \
--java-version 1.8.0_73  \
--java-container-version 8.5
```

## <a name="configure-maven"></a><span data-ttu-id="6c7be-140">Configuración de Maven</span><span class="sxs-lookup"><span data-stu-id="6c7be-140">Configure Maven</span></span> 

<span data-ttu-id="6c7be-141">El archivo `pom.xml` de Maven del ejemplo incluye la configuración para enviar el ejemplo por FTP a Azure, pero deberá personalizarlo para implementar su propia aplicación web.</span><span class="sxs-lookup"><span data-stu-id="6c7be-141">The sample's Maven `pom.xml` includes configuration to FTP the sample into Azure, but you'll need to customize it to deploy to your own web app.</span></span> <span data-ttu-id="6c7be-142">Puede recuperar las credenciales de App Service con [az appservice web deployment list-publishing-profiles](/cli/azure/appservice/web/deployment#list-publishing-profiles):</span><span class="sxs-lookup"><span data-stu-id="6c7be-142">Retreive your App Seevice credentials with [az appservice web deployment list-publishing-profiles](/cli/azure/appservice/web/deployment#list-publishing-profiles):</span></span>

```azurecli
az webapp deployment list-publishing-profiles  \
--name appname \ 
--resource-group myResourceGroup  \
--query "[?publishMethod=='FTP'].{URL:publishUrl, Username:userName,Password:userPWD}" 
```

```json
[
  {
    "Password": "aBcDeFgHiJkLmNoPqRsTuVwXyZ",
    "URL": "ftp://waws-prod-blu-045.ftp.azurewebsites.windows.net/site/wwwroot",
    "Username": "appname\\$appname"
  }
]
```

<span data-ttu-id="6c7be-143">Reemplace los marcadores de posición en el archivo `az-settings.xml` por la contraseña, el nombre de usuario y el nombre de host FTP de la salida.</span><span class="sxs-lookup"><span data-stu-id="6c7be-143">Replace the placeholders in the `az-settings.xml` file with password, username, and FTP hostname from the output.</span></span> <span data-ttu-id="6c7be-144">Asegúrese de usar solo un carácter `\` en el nombre de usuario en lugar del valor de escape de la salida de la CLI.</span><span class="sxs-lookup"><span data-stu-id="6c7be-144">Make sure to only use one `\` character in the username instead of the escaped value from the CLI output.</span></span>
   
```XML
...
    <server>
      <id>azure-hello-world</id>
      <username>appname\$appname</username>
      <password>aBcDeFgHiJkLmNoPqRsTuVwXyZ</password>
    </server>
...
   <configuration>
     <fromFile>${basedir}/target/AzureAppDemo-0.0.1-SNAPSHOT.war</fromFile>
     <url>ftp://waws-prod-blu-045.ftp.azurewebsites.windows.net/site/wwwroot</url>
     <toFile>webapps/ROOT.war</toFile>
     <serverId>azure-hello-world</serverId>
   </configuration>
...
```

## <a name="deploy-the-sample-application"></a><span data-ttu-id="6c7be-145">Implementación de la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="6c7be-145">Deploy the sample application</span></span>

<span data-ttu-id="6c7be-146">Implementar el ejemplo en Azure mediante el parámetro `-s` de Maven para utilizar la configuración del archivo `az-settings.xml`.</span><span class="sxs-lookup"><span data-stu-id="6c7be-146">Deploy with sample to Azure, using Maven's `-s` parameter to use the configuration in the `az-settings.xml` file.</span></span>

```
mvn install -s az-settings.xml
```

## <a name="browse-to-web-app"></a><span data-ttu-id="6c7be-147">Navegación a la aplicación web</span><span class="sxs-lookup"><span data-stu-id="6c7be-147">Browse to web app</span></span>

<span data-ttu-id="6c7be-148">Vea el ejemplo en ejecución en Azure:</span><span class="sxs-lookup"><span data-stu-id="6c7be-148">View the sample running in Azure:</span></span>

```azurecli
az webapp browse --name appname --resource-group myResourceGroup
```

## <a name="update-the-app"></a><span data-ttu-id="6c7be-149">Actualización de la aplicación</span><span class="sxs-lookup"><span data-stu-id="6c7be-149">Update the app</span></span>

<span data-ttu-id="6c7be-150">Con un editor de texto, abra `src/main/webapp/index.jsp` y reemplace el código JSP existente por el siguiente.</span><span class="sxs-lookup"><span data-stu-id="6c7be-150">Using a text editor, open `src/main/webapp/index.jsp`, and replace the existing JSP with the one below.</span></span>

```html
<%--
  Copyright (c) Microsoft Corporation. All rights reserved.
  Licensed under the MIT License. See License.txt in the project root for
  license information.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java"  import="java.util.Date" %>
<html>
<head>
  <title>Azure Samples Hello World</title>
</head>
<body>
  <H1>Hello Azure!</H1>
   Current time is: <%= new Date() %>
</body>
</html>
```

<span data-ttu-id="6c7be-151">Implemente la actualización con Maven:</span><span class="sxs-lookup"><span data-stu-id="6c7be-151">Deploy the update with Maven:</span></span>

```
mvn clean package
mvn install -s az-settings.xml
```

<span data-ttu-id="6c7be-152">Actualice el explorador después de volver a implementar la aplicación para ver los cambios.</span><span class="sxs-lookup"><span data-stu-id="6c7be-152">Refresh your browser after the app redeploys to view your changes.</span></span>

## <a name="manage-your-new-azure-app"></a><span data-ttu-id="6c7be-153">Administración de la nueva aplicación de Azure</span><span class="sxs-lookup"><span data-stu-id="6c7be-153">Manage your new Azure app</span></span>

<span data-ttu-id="6c7be-154">Vaya a Azure Portal para echar un vistazo a la aplicación web que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="6c7be-154">Go to the Azure portal to take a look at the web app you just created.</span></span>

<span data-ttu-id="6c7be-155">Para ello, inicie sesión en [https://portal.azure.com/](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6c7be-155">To do this, sign in to [https://portal.azure.com](https://portal.azure.com).</span></span>

<span data-ttu-id="6c7be-156">En el menú izquierdo, haga clic en **App Service**, a continuación, haga clic en el nombre de la aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="6c7be-156">From the left menu, click **App Service**, then click the name of your Azure web app.</span></span>

 ![Selección de la aplicación en la lista de aplicaciones web del portal](media/azure-app-service-portal.png)

<span data-ttu-id="6c7be-158">Para probar la supervisión, ejecute `curl` en la aplicación para enviar algo de tráfico.</span><span class="sxs-lookup"><span data-stu-id="6c7be-158">Test the monitoring by running `curl` against the app to send some traffic.</span></span>

```bash
curl http://<appname>.azurewebsites.net/?[1-30]
```

<span data-ttu-id="6c7be-159">Podrá ver la actividad de solicitud en la supervisión después de unos minutos.</span><span class="sxs-lookup"><span data-stu-id="6c7be-159">You'll see the request activity in the monitoring after a couple of minutes.</span></span>

 ![Supervisión en Azure Portal](media/java-app-monitoring.png)

## <a name="clean-up-resources"></a><span data-ttu-id="6c7be-161">Limpieza de recursos</span><span class="sxs-lookup"><span data-stu-id="6c7be-161">Clean up resources</span></span>

<span data-ttu-id="6c7be-162">Para eliminar todos los recursos creados en este tutorial de inicio rápido, ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="6c7be-162">To remove all the resources created in this guide, run the following command:</span></span>

```azurecli
az group delete --name myResrouceGroup
```

## <a name="next-steps"></a><span data-ttu-id="6c7be-163">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6c7be-163">Next steps</span></span>

<span data-ttu-id="6c7be-164">Examine la lista completa de [ejemplos de Java de Azure](https://azure.microsoft.com/resources/samples/?term=java).</span><span class="sxs-lookup"><span data-stu-id="6c7be-164">Browse the full list of [Azure Java samples](https://azure.microsoft.com/resources/samples/?term=java).</span></span>