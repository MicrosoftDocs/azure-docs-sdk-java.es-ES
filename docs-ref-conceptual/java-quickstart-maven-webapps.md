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
ms.openlocfilehash: 9c3d39e12b00dd1dd3d5f76162ce0f387c7a947c
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/28/2017
---
# <a name="create-and-deploy-a-java-app-to-azure-with-maven"></a>Crear e implementar una aplicación de Java en Azure con Maven

Esta guía de inicio rápido le ayuda a crear e implementar una sencilla aplicación web de Java en [Azure App Service](/azure/app-service/app-service-value-prop-what-is) en unos pocos minutos usando [Maven de Apache](http://maven.apache.org) y la CLI de Azure.

## <a name="before-you-begin"></a>Antes de empezar

Antes de empezar, configure lo siguiente:

- [Git](https://git-scm.com/)
- [Java 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html)
- [Maven 3](http://maven.apache.org/download.cgi)
- [CLI de Azure 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2)

Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de empezar.

## <a name="get-the-sample-code"></a>Obtención del código de ejemplo

Clone el repositorio de la aplicación de ejemplo en la máquina local. El ejemplo es una sencilla aplicación de JSP con configuración adicional de Maven en el archivo `pom.xml` del proyecto para probar la aplicación localmente y ayudar a implementar el ejemplo en Azure App Service.

```
git clone https://github.com/Azure-Samples/app-service-maven
```

## <a name="run-the-app-locally"></a>Ejecución de la aplicación de forma local

Abra un símbolo del sistema y use Maven para compilar la aplicación y ejecutarla en un contenedor web local de [Tomcat](https://tomcat.apache.org). 

```
cd app-service-maven
mvn package
mvn tomcat7:run-war
```

Abra el explorador y navegue hasta http://localhost:8080 para previsualizar la aplicación:

  ![Mensaje Hola mundo de la aplicación de ejemplo de Java](media/maven-quickstart/java-app-hello-world-output.png)

## <a name="log-in-to-azure"></a>Inicie sesión en Azure.

Inicie sesión en la CLI de Azure con `az login`. Este tutorial rápido usa la CLI para consultar y crear los recursos de Azure necesarios para hospedar la aplicación.
   
```azurecli
az login
```

## <a name="create-a-resource-group"></a>Crear un grupo de recursos   

Cree un grupo de recursos con [az group create](/cli/azure/group#create). Un grupo de recursos de Azure es un contenedor lógico en el que se implementan y se administran los recursos de Azure.

```azurecli
az group create --location "East US" --name myResourceGroup
```

Para ver los valores posibles que puede usar para `---location`, use el comando [az appservice list-locations](/cli/azure/appservice#list-locations)

## <a name="create-an-app-service-plan"></a>Creación de un plan de App Service

Cree un [plan de App Service](/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview) **GRATUITO** con [az appservice plan create](/cli/azure/appservice/plan#create). Los planes de App Service asignan recursos compartidos entre todas las aplicaciones web que se ejecutan en el plan.


```azurecli
az appservice plan create --name my-free-appservice-plan --resource-group myResourceGroup --sku FREE
```

Cuando se ha creado el plan de App Service, la CLI de Azure muestra información similar a la del ejemplo siguiente:

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


## <a name="create-a-web-app"></a>Creación de una aplicación web

Cree una aplicación web que use los recursos del plan mediante el comando [az webapp create](/cli/azure/appservice/web#create) de la CLI de Azure. La definición de la aplicación web proporciona un espacio para implementar el código y una dirección URL para tener acceso a la aplicación una vez que se esté ejecutando.

En el comando siguiente, sustituya su nombre de aplicación único donde vea el marcador de posición <appname>. <appname> se utiliza en el nombre de host predeterminado para la aplicación web. Si <appname> no es único, obtendrá el mensaje de error descriptivo "Ya existe un sitio web con el nombre especificado."

```azurecli
az webapp create --name appname --resource-group myResourceGroup --plan my-free-appservice-plan
```

Cuando se ha creado la aplicación web, la CLI de Azure muestra información similar a la del ejemplo siguiente:

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

## <a name="configure-java-and-tomcat"></a>Configuración de Java y Tomcat

Configurar la aplicación web para usar Java y Tomcat mediante el comando [az webapp config](/cli/azure/appservice/web#config) de la CLI de Azure. En el ejemplo siguiente se configura App Service para ejecutar Java 8 y [Apache Tomcat 8.5](http://tomcat.apache.org/) para ejecutar la aplicación.

```azurecli
az webapp config set \ 
--name appname \
--resource-group myResourceGroup \
--java-container TOMCAT \
--java-version 1.8.0_73  \
--java-container-version 8.5
```

## <a name="configure-maven"></a>Configuración de Maven 

El archivo `pom.xml` de Maven del ejemplo incluye la configuración para enviar el ejemplo por FTP a Azure, pero deberá personalizarlo para implementar su propia aplicación web. Puede recuperar las credenciales de App Service con [az appservice web deployment list-publishing-profiles](/cli/azure/appservice/web/deployment#list-publishing-profiles):

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

Reemplace los marcadores de posición en el archivo `az-settings.xml` por la contraseña, el nombre de usuario y el nombre de host FTP de la salida. Asegúrese de usar solo un carácter `\` en el nombre de usuario en lugar del valor de escape de la salida de la CLI.
   
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

## <a name="deploy-the-sample-application"></a>Implementación de la aplicación de ejemplo

Implementar el ejemplo en Azure mediante el parámetro `-s` de Maven para utilizar la configuración del archivo `az-settings.xml`.

```
mvn install -s az-settings.xml
```

## <a name="browse-to-web-app"></a>Navegación a la aplicación web

Vea el ejemplo en ejecución en Azure:

```azurecli
az webapp browse --name appname --resource-group myResourceGroup
```

## <a name="update-the-app"></a>Actualización de la aplicación

Con un editor de texto, abra `src/main/webapp/index.jsp` y reemplace el código JSP existente por el siguiente.

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

Implemente la actualización con Maven:

```
mvn clean package
mvn install -s az-settings.xml
```

Actualice el explorador después de volver a implementar la aplicación para ver los cambios.

## <a name="manage-your-new-azure-app"></a>Administración de la nueva aplicación de Azure

Vaya a Azure Portal para echar un vistazo a la aplicación web que acaba de crear.

Para ello, inicie sesión en [https://portal.azure.com/](https://portal.azure.com).

En el menú izquierdo, haga clic en **App Service**, a continuación, haga clic en el nombre de la aplicación web de Azure.

 ![Selección de la aplicación en la lista de aplicaciones web del portal](media/azure-app-service-portal.png)

Para probar la supervisión, ejecute `curl` en la aplicación para enviar algo de tráfico.

```bash
curl http://<appname>.azurewebsites.net/?[1-30]
```

Podrá ver la actividad de solicitud en la supervisión después de unos minutos.

 ![Supervisión en Azure Portal](media/java-app-monitoring.png)

## <a name="clean-up-resources"></a>Limpieza de recursos

Para eliminar todos los recursos creados en este tutorial de inicio rápido, ejecute el siguiente comando:

```azurecli
az group delete --name myResrouceGroup
```

## <a name="next-steps"></a>Pasos siguientes

Examine la lista completa de [ejemplos de Java de Azure](https://azure.microsoft.com/resources/samples/?term=java).