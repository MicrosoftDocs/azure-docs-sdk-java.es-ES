---
title: Configurar implementaciones de aplicación web con Java | Microsoft Docs
description: Código de ejemplo de Java para configurar implementaciones Git o FTP de Azure App Service mediante el SDK de Azure para Java
author: rloutlaw
manager: douge
ms.assetid: 833e9c78-1e50-4c23-a611-f73a2f0c2983
ms.service: Azure
ms.devlang: java
ms.topic: article
ms.date: 03/30/2017
ms.author: routlaw;asirveda
ms.openlocfilehash: 910d1e43c9942d6402aeccb8757ba819b7453dab
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/28/2017
ms.locfileid: "21931191"
---
# <a name="configure-azure-app-service-deployment-sources-from-your-java-applications"></a>Configurar orígenes de implementación de Azure App Service desde las aplicaciones Java

[Este ejemplo](https://github.com/Azure-Samples/compute-java-create-virtual-machines-across-regions-in-parallel) implementa código para cuatro aplicaciones en un solo plan de [Azure App Service](https://docs.microsoft.com/azure/app-service/), cada uno con un origen de implementación diferente.

## <a name="run-the-sample"></a>Ejecución del ejemplo

Cree un [archivo de autenticación](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) y establezca una variable de entorno `AZURE_AUTH_LOCATION` con la ruta de acceso completa al archivo en el equipo. A continuación, ejecute:

```
git clone https://github.com/Azure-Samples/app-service-java-configure-deployment-sources-for-web-apps.git
cd app-service-java-configure-deployment-sources-for-web-apps
mvn clean compile exec:java
```

Vea el [código completo del ejemplo en GitHub](https://github.com/Azure-Samples/app-service-java-configure-deployment-sources-for-web-apps/blob/master/src/main/java/com/microsoft/azure/management/appservice/samples/ManageWebAppSourceControl.java).

## <a name="authenticate-with-azure"></a>Autenticación con Azure

[!INCLUDE [auth-include](includes/java-auth-include.md)]

## <a name="create-a-app-service-app-running-apache-tomcat"></a>Creación de una aplicación de App Service que ejecuta Apache Tomcat

```java
// create a new Standard app service plan and create a single Java 8/Tomcat 8 app in it
WebApp app1 = azure.webApps().define(app1Name)
             .withNewResourceGroup(rgName)
             .withNewAppServicePlan(planName)
             .withRegion(Region.US_WEST)
             .withPricingTier(AppServicePricingTier.STANDARD_S1)
             .withJavaVersion(JavaVersion.JAVA_8_NEWEST)
             .withWebContainer(WebContainer.TOMCAT_8_0_NEWEST)
             .create();
```

`withJavaVersion()` y `withWebContainer()` configuran App Service para dar servicio a solicitudes HTTP con Tomcat 8.

## <a name="deploy-a-java-application-using-ftp"></a>Implementación de una aplicación Java con FTP
```java
// pass the PublishingProfile that contains FTP information to a helper method 
uploadFileToFtp(app1.getPublishingProfile(), "helloworld.war", 
      ManageWebAppSourceControl.class.getResourceAsStream("/helloworld.war"));

// Use the FTP classes in the Apache Commons library to connect to Azure using 
// the information from the PublishingProfile
private static void uploadFileToFtp(PublishingProfile profile, String fileName, InputStream file) throws Exception {
        FTPClient ftpClient = new FTPClient();
        String[] ftpUrlSegments = profile.ftpUrl().split("/", 2);
        String server = ftpUrlSegments[0];
        // Tomcat will deploy WAR files uploaded to this directory.
        String path = "./site/wwwroot/webapps"; 

        // FTP the build WAR to Azure
        ftpClient.connect(server);
        ftpClient.login(profile.ftpUsername(), profile.ftpPassword());
        ftpClient.setFileType(FTP.BINARY_FILE_TYPE);
        ftpClient.changeWorkingDirectory(path);
        ftpClient.storeFile(fileName, file);
        ftpClient.disconnect();
}
```

Este código carga un archivo WAR en el directorio `/site/wwwroot/webapps`. Tomcat implementa los archivos WAR colocados en este directorio en App Service de forma predeterminada.

## <a name="deploy-a-java-application-from-a-local-git-repo"></a>Implementación de una aplicación Java desde un repositorio de Git local

```java
// get the publishing profile from the App Service webapp
PublishingProfile profile = app2.getPublishingProfile();

// create a new Git repo in the sample directory under src/main/resources 
Git git = Git
    .init()
    .setDirectory(new File(ManageWebAppSourceControl.class.getResource("/azure-samples-appservice-helloworld/").getPath()))
    .call();
git.add().addFilepattern(".").call();
// add the files in the sample app to an initial commit
git.commit().setMessage("Initial commit").call(); 

// push the commit using the Azure Git remote URL and credentials in the publishing profile
PushCommand command = git.push();
command.setRemote(profile.gitUrl()); 
command.setCredentialsProvider(new UsernamePasswordCredentialsProvider(profile.gitUsername(), profile.gitPassword()));
command.setRefSpecs(new RefSpec("master:master")); 
command.setForce(true);
command.call();
```      

Este código usa las bibliotecas [JGit](https://eclipse.org/jgit/) para crear un nuevo repositorio de Git en la carpeta `src/main/resources/azure-samples-appservice-helloworld`. Después, el ejemplo agrega todos los archivos de la carpeta a una confirmación inicial y envía la confirmación a Azure utilizando la información de implementación de Git desde el objeto `PublishingProfile` de la aplicación web. 

>[!NOTE]
> El diseño de los archivos en el repositorio debe coincidir exactamente con cómo desea que se implementen los archivos en el directorio `/site/wwwroot/` de Azure App Service.

## <a name="deploy-an-application-from-a-public-git-repo"></a>Implementación de una aplicación desde un repositorio de Git público

```java
// deploy a .NET sample app from a public GitHub repo into a new webapp
WebApp app3 = azure.webApps().define(app3Name)
                .withNewResourceGroup(rgName)
                .withExistingAppServicePlan(plan)
                .defineSourceControl()
                .withPublicGitRepository(
                   "https://github.com/Azure-Samples/app-service-web-dotnet-get-started")
                .withBranch("master")
                .attach()
                .create();
 ```

 El entorno de tiempo de ejecución de App Service crea e implementa automáticamente el proyecto de .NET usando el código más reciente en la rama `master` del repositorio.

## <a name="continuous-deployment-from-a-github-repo"></a>Implementación continua desde un repositorio de GitHub

```java
// deploy the application whenever you push a new commit or merge a pull request into your master branch
WebApp app4 = azure.webApps()
                    .define(app4Name)
                    .withExistingResourceGroup(rgName)
                    .withExistingAppServicePlan(plan)
                    // Uncomment the following lines to turn on continuous deployment scenario
                    //.defineSourceControl()
                    //    .withContinuouslyIntegratedGitHubRepository("username", "reponame")
                    //    .withBranch("master")
                    //    .withGitHubAccessToken("YOUR GITHUB PERSONAL TOKEN")
                    //    .attach()
                    .create();
```  

Los valores de `username` y `reponame` son los que se utilizan en GitHub. [Cree un token de acceso personal de GitHub](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/) con permisos de lectura en el repositorio y páselo a `withGitHubAccessToken`. 


## <a name="sample-explanation"></a>Explicación del ejemplo

El ejemplo crea la primera aplicación con Java 8 y Tomcat 8 que se ejecuta en un plan [Estándar](https://docs.microsoft.com/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview) de App Service recién creado. El código, a continuación, envía por FTP un archivo WAR usando la información del objeto `PublishingProfile` y Tomcat lo implementa.

La segunda aplicación usa el mismo plan que la primera y también se configura como una aplicación de Java 8 y Tomcat 8. Las bibliotecas de JGit crean un nuevo repositorio de Git en una carpeta que contiene una aplicación web de Java desempaquetada en una estructura de directorios que se asigna a App Service. Una nueva confirmación agrega los archivos en la carpeta al nuevo repositorio de Git y Git envía la confirmación a Azure con una dirección URL remota y el nombre de usuario y la contraseña proporcionados por el objeto `PublishingProfile` de la aplicación web.

La tercera aplicación no está configurada para Java y Tomcat. En su lugar, se implementa un ejemplo de .NET de un repositorio de GitHub público directamente desde el origen.

La cuarta aplicación implementa el código en la rama principal cada vez que inserte cambios o fusione una solicitud de incorporación de cambios en la rama principal del repositorio de GitHub.

| Clase utilizada en el ejemplo | Notas
|-------|-------|
| [WebApp](https://docs.microsoft.com/java/api/com.microsoft.azure.management.appservice._web_app) | Creada con la cadena fluida `azure.webApps().define()....create()`. Crea una aplicación web de App Service y los recursos necesarios para la aplicación. La mayoría de los métodos consultan el objeto para obtener detalles de configuración, pero los métodos de verbo como `restart()` cambian el estado de la aplicación web.
| [WebContainer](https://docs.microsoft.com/java/api/com.microsoft.azure.management.appservice._web_container) | Clase con campos públicos estáticos usados como parámetros de `withWebContainer()` al definir una aplicación web que ejecuta un webcontainer de Java. Tiene opciones para versiones de Tomcat y Jetty.
| [PublishingProfile](https://docs.microsoft.com/java/api/com.microsoft.azure.management.appservice._publishing_profile) | Se obtiene a través de un objeto WebApp mediante el método `getPublishingProfile()`. Contiene información de implementación de FTP y Git, incluido el nombre de usuario de implementación y la contraseña (que es distinto al de la cuenta de Azure o las credenciales de la entidad de servicio).
| [AppServicePlan](https://docs.microsoft.com/java/api/com.microsoft.azure.management.appservice._app_service_plan) | Devuelto por `azure.appServices().appServicePlans().getByResourceGroup()`. Hay métodos disponibles para comprobar la capacidad, el nivel y el número de aplicaciones web que se ejecutan en el plan.
| [AppServicePricingTier](https://docs.microsoft.com/java/api/com.microsoft.azure.management.appservice._app_service_pricing_tier) | Clase con campos públicos estáticos que representa los niveles de App Service. Permite definir un nivel de plan en línea durante la creación de aplicaciones con `withPricingTier()` o directamente al definir un plan a través de `azure.appServices().appServicePlans().define()`
| [JavaVersion](https://docs.microsoft.com/java/api/com.microsoft.azure.management.appservice._java_version) | Clase con campos públicos estáticos que representa las versiones de Java admitidas por App Service. Se usa con `withJavaVersion()` durante la cadena `define()...create()` al crear una aplicación web nueva.

## <a name="next-steps"></a>Pasos siguientes

[!INCLUDE [next-steps](includes/java-next-steps.md)]