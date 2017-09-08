---
title: "Configurar implementaciones de aplicación web con Java | Microsoft Docs"
description: "Código de ejemplo de Java para configurar implementaciones Git o FTP de Azure App Service mediante el SDK de Azure para Java"
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
---
# <a name="configure-azure-app-service-deployment-sources-from-your-java-applications"></a><span data-ttu-id="99c43-103">Configurar orígenes de implementación de Azure App Service desde las aplicaciones Java</span><span class="sxs-lookup"><span data-stu-id="99c43-103">Configure Azure App Service deployment sources from your Java applications</span></span>

<span data-ttu-id="99c43-104">[Este ejemplo](https://github.com/Azure-Samples/compute-java-create-virtual-machines-across-regions-in-parallel) implementa código para cuatro aplicaciones en un solo plan de [Azure App Service](https://docs.microsoft.com/azure/app-service/), cada uno con un origen de implementación diferente.</span><span class="sxs-lookup"><span data-stu-id="99c43-104">[This sample](https://github.com/Azure-Samples/compute-java-create-virtual-machines-across-regions-in-parallel) deploys code to four applications in a single [Azure App Service](https://docs.microsoft.com/azure/app-service/) plan, each using a different deployment source.</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="99c43-105">Ejecución del ejemplo</span><span class="sxs-lookup"><span data-stu-id="99c43-105">Run the sample</span></span>

<span data-ttu-id="99c43-106">Cree un [archivo de autenticación](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) y establezca una variable de entorno `AZURE_AUTH_LOCATION` con la ruta de acceso completa al archivo en el equipo.</span><span class="sxs-lookup"><span data-stu-id="99c43-106">Create an [authentication file](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) and set an environment variable `AZURE_AUTH_LOCATION` with the full path to the file on your computer.</span></span> <span data-ttu-id="99c43-107">A continuación, ejecute:</span><span class="sxs-lookup"><span data-stu-id="99c43-107">Then run:</span></span>

```
git clone https://github.com/Azure-Samples/app-service-java-configure-deployment-sources-for-web-apps.git
cd app-service-java-configure-deployment-sources-for-web-apps
mvn clean compile exec:java
```

<span data-ttu-id="99c43-108">Vea el [código completo del ejemplo en GitHub](https://github.com/Azure-Samples/app-service-java-configure-deployment-sources-for-web-apps/blob/master/src/main/java/com/microsoft/azure/management/appservice/samples/ManageWebAppSourceControl.java).</span><span class="sxs-lookup"><span data-stu-id="99c43-108">View the [complete sample code on GitHub](https://github.com/Azure-Samples/app-service-java-configure-deployment-sources-for-web-apps/blob/master/src/main/java/com/microsoft/azure/management/appservice/samples/ManageWebAppSourceControl.java).</span></span>

## <a name="authenticate-with-azure"></a><span data-ttu-id="99c43-109">Autenticación con Azure</span><span class="sxs-lookup"><span data-stu-id="99c43-109">Authenticate with Azure</span></span>

[!INCLUDE [auth-include](includes/java-auth-include.md)]

## <a name="create-a-app-service-app-running-apache-tomcat"></a><span data-ttu-id="99c43-110">Creación de una aplicación de App Service que ejecuta Apache Tomcat</span><span class="sxs-lookup"><span data-stu-id="99c43-110">Create a App Service app running Apache Tomcat</span></span>

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

<span data-ttu-id="99c43-111">`withJavaVersion()` y `withWebContainer()` configuran App Service para dar servicio a solicitudes HTTP con Tomcat 8.</span><span class="sxs-lookup"><span data-stu-id="99c43-111">`withJavaVersion()` and `withWebContainer()` configure App Service to serve HTTP requests using Tomcat 8.</span></span>

## <a name="deploy-a-java-application-using-ftp"></a><span data-ttu-id="99c43-112">Implementación de una aplicación Java con FTP</span><span class="sxs-lookup"><span data-stu-id="99c43-112">Deploy a Java application using FTP</span></span>
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

<span data-ttu-id="99c43-113">Este código carga un archivo WAR en el directorio `/site/wwwroot/webapps`.</span><span class="sxs-lookup"><span data-stu-id="99c43-113">This code uploads a WAR file to the `/site/wwwroot/webapps` directory.</span></span> <span data-ttu-id="99c43-114">Tomcat implementa los archivos WAR colocados en este directorio en App Service de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="99c43-114">Tomcat deploys WAR files placed in this directory by default in App Service.</span></span>

## <a name="deploy-a-java-application-from-a-local-git-repo"></a><span data-ttu-id="99c43-115">Implementación de una aplicación Java desde un repositorio de Git local</span><span class="sxs-lookup"><span data-stu-id="99c43-115">Deploy a Java application from a local Git repo</span></span>

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

<span data-ttu-id="99c43-116">Este código usa las bibliotecas [JGit](https://eclipse.org/jgit/) para crear un nuevo repositorio de Git en la carpeta `src/main/resources/azure-samples-appservice-helloworld`.</span><span class="sxs-lookup"><span data-stu-id="99c43-116">This code uses the [JGit](https://eclipse.org/jgit/) libraries to create a new Git repo in the `src/main/resources/azure-samples-appservice-helloworld` folder.</span></span> <span data-ttu-id="99c43-117">Después, el ejemplo agrega todos los archivos de la carpeta a una confirmación inicial y envía la confirmación a Azure utilizando la información de implementación de Git desde el objeto `PublishingProfile` de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="99c43-117">The sample then adds all files in the folder to an initial commit and pushes the commit to Azure using Git deployment information from the webapp's `PublishingProfile`.</span></span> 

>[!NOTE]
> <span data-ttu-id="99c43-118">El diseño de los archivos en el repositorio debe coincidir exactamente con cómo desea que se implementen los archivos en el directorio `/site/wwwroot/` de Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="99c43-118">The layout of the files in the repo must match exactly how you want the files deployed under the `/site/wwwroot/` directory in Azure App Service.</span></span>

## <a name="deploy-an-application-from-a-public-git-repo"></a><span data-ttu-id="99c43-119">Implementación de una aplicación desde un repositorio de Git público</span><span class="sxs-lookup"><span data-stu-id="99c43-119">Deploy an application from a public Git repo</span></span>

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

 <span data-ttu-id="99c43-120">El entorno de tiempo de ejecución de App Service crea e implementa automáticamente el proyecto de .NET usando el código más reciente en la rama `master` del repositorio.</span><span class="sxs-lookup"><span data-stu-id="99c43-120">The App Service runtime automatically builds and deploys the .NET project using the latest code on the `master` branch of the repo.</span></span>

## <a name="continuous-deployment-from-a-github-repo"></a><span data-ttu-id="99c43-121">Implementación continua desde un repositorio de GitHub</span><span class="sxs-lookup"><span data-stu-id="99c43-121">Continuous deployment from a GitHub repo</span></span>

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

<span data-ttu-id="99c43-122">Los valores de `username` y `reponame` son los que se utilizan en GitHub.</span><span class="sxs-lookup"><span data-stu-id="99c43-122">The `username` and `reponame` values are the ones used in GitHub.</span></span> <span data-ttu-id="99c43-123">[Cree un token de acceso personal de GitHub](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/) con permisos de lectura en el repositorio y páselo a `withGitHubAccessToken`.</span><span class="sxs-lookup"><span data-stu-id="99c43-123">[Create a GitHub personal access token](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/) with repo read permissions and pass it to `withGitHubAccessToken`.</span></span> 


## <a name="sample-explanation"></a><span data-ttu-id="99c43-124">Explicación del ejemplo</span><span class="sxs-lookup"><span data-stu-id="99c43-124">Sample explanation</span></span>

<span data-ttu-id="99c43-125">El ejemplo crea la primera aplicación con Java 8 y Tomcat 8 que se ejecuta en un plan [Estándar](https://docs.microsoft.com/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview) de App Service recién creado.</span><span class="sxs-lookup"><span data-stu-id="99c43-125">The sample creates the first application using Java 8 and Tomcat 8 running in a newly created [Standard](https://docs.microsoft.com/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview) App Service plan.</span></span> <span data-ttu-id="99c43-126">El código, a continuación, envía por FTP un archivo WAR usando la información del objeto `PublishingProfile` y Tomcat lo implementa.</span><span class="sxs-lookup"><span data-stu-id="99c43-126">The code then FTPs a WAR file using the information in the `PublishingProfile` object and Tomcat deploys it.</span></span>

<span data-ttu-id="99c43-127">La segunda aplicación usa el mismo plan que la primera y también se configura como una aplicación de Java 8 y Tomcat 8.</span><span class="sxs-lookup"><span data-stu-id="99c43-127">The second application uses in the same plan as the first and is also configured as a Java 8/Tomcat 8 application.</span></span> <span data-ttu-id="99c43-128">Las bibliotecas de JGit crean un nuevo repositorio de Git en una carpeta que contiene una aplicación web de Java desempaquetada en una estructura de directorios que se asigna a App Service.</span><span class="sxs-lookup"><span data-stu-id="99c43-128">The JGit libraries create a new Git repository in a folder that contains an unpacked Java web application in a directory structure that maps to App Service.</span></span> <span data-ttu-id="99c43-129">Una nueva confirmación agrega los archivos en la carpeta al nuevo repositorio de Git y Git envía la confirmación a Azure con una dirección URL remota y el nombre de usuario y la contraseña proporcionados por el objeto `PublishingProfile` de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="99c43-129">A new commit adds the files in the folder to the new Git repo, and Git pushes the commit to Azure with a remote URL and username/password provided by the webapp's `PublishingProfile`.</span></span>

<span data-ttu-id="99c43-130">La tercera aplicación no está configurada para Java y Tomcat.</span><span class="sxs-lookup"><span data-stu-id="99c43-130">The third application is not configured for Java and Tomcat.</span></span> <span data-ttu-id="99c43-131">En su lugar, se implementa un ejemplo de .NET de un repositorio de GitHub público directamente desde el origen.</span><span class="sxs-lookup"><span data-stu-id="99c43-131">Instead, a .NET sample in a public GitHub repo is deployed directly from source.</span></span>

<span data-ttu-id="99c43-132">La cuarta aplicación implementa el código en la rama principal cada vez que inserte cambios o fusione una solicitud de incorporación de cambios en la rama principal del repositorio de GitHub.</span><span class="sxs-lookup"><span data-stu-id="99c43-132">The fourth application deploys the code in your master branch every time you push changes or merge a pull request into the GitHub repo's master branch.</span></span>

| <span data-ttu-id="99c43-133">Clase utilizada en el ejemplo</span><span class="sxs-lookup"><span data-stu-id="99c43-133">Class used in sample</span></span> | <span data-ttu-id="99c43-134">Notas</span><span class="sxs-lookup"><span data-stu-id="99c43-134">Notes</span></span>
|-------|-------|
| [<span data-ttu-id="99c43-135">WebApp</span><span class="sxs-lookup"><span data-stu-id="99c43-135">WebApp</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.appservice._web_app) | <span data-ttu-id="99c43-136">Creada con la cadena fluida `azure.webApps().define()....create()`.</span><span class="sxs-lookup"><span data-stu-id="99c43-136">Created from the `azure.webApps().define()....create()` fluent chain.</span></span> <span data-ttu-id="99c43-137">Crea una aplicación web de App Service y los recursos necesarios para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="99c43-137">Creates a App Service web app and any resources needed for the app.</span></span> <span data-ttu-id="99c43-138">La mayoría de los métodos consultan el objeto para obtener detalles de configuración, pero los métodos de verbo como `restart()` cambian el estado de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="99c43-138">Most methods query the object for configuration details, but verb methods like `restart()` change the state of the webapp.</span></span>
| [<span data-ttu-id="99c43-139">WebContainer</span><span class="sxs-lookup"><span data-stu-id="99c43-139">WebContainer</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.appservice._web_container) | <span data-ttu-id="99c43-140">Clase con campos públicos estáticos usados como parámetros de `withWebContainer()` al definir una aplicación web que ejecuta un webcontainer de Java.</span><span class="sxs-lookup"><span data-stu-id="99c43-140">Class with static public fields used as paramters to `withWebContainer()` when defining a WebApp running a Java webcontainer.</span></span> <span data-ttu-id="99c43-141">Tiene opciones para versiones de Tomcat y Jetty.</span><span class="sxs-lookup"><span data-stu-id="99c43-141">Has choices for both Jetty and Tomcat versions.</span></span>
| [<span data-ttu-id="99c43-142">PublishingProfile</span><span class="sxs-lookup"><span data-stu-id="99c43-142">PublishingProfile</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.appservice._publishing_profile) | <span data-ttu-id="99c43-143">Se obtiene a través de un objeto WebApp mediante el método `getPublishingProfile()`.</span><span class="sxs-lookup"><span data-stu-id="99c43-143">Obtained through a WebApp object using the `getPublishingProfile()` method.</span></span> <span data-ttu-id="99c43-144">Contiene información de implementación de FTP y Git, incluido el nombre de usuario de implementación y la contraseña (que es distinto al de la cuenta de Azure o las credenciales de la entidad de servicio).</span><span class="sxs-lookup"><span data-stu-id="99c43-144">Contains FTP and Git deployment information, including deployment username and password (which is separate from Azure account or service principal credentials).</span></span>
| [<span data-ttu-id="99c43-145">AppServicePlan</span><span class="sxs-lookup"><span data-stu-id="99c43-145">AppServicePlan</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.appservice._app_service_plan) | <span data-ttu-id="99c43-146">Devuelto por `azure.appServices().appServicePlans().getByResourceGroup()`.</span><span class="sxs-lookup"><span data-stu-id="99c43-146">Returned by `azure.appServices().appServicePlans().getByResourceGroup()`.</span></span> <span data-ttu-id="99c43-147">Hay métodos disponibles para comprobar la capacidad, el nivel y el número de aplicaciones web que se ejecutan en el plan.</span><span class="sxs-lookup"><span data-stu-id="99c43-147">Methods are availble to check the capacity, tier, and number of web apps running in the plan.</span></span>
| [<span data-ttu-id="99c43-148">AppServicePricingTier</span><span class="sxs-lookup"><span data-stu-id="99c43-148">AppServicePricingTier</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.appservice._app_service_pricing_tier) | <span data-ttu-id="99c43-149">Clase con campos públicos estáticos que representa los niveles de App Service.</span><span class="sxs-lookup"><span data-stu-id="99c43-149">Class with static public fields representing App Service tiers.</span></span> <span data-ttu-id="99c43-150">Permite definir un nivel de plan en línea durante la creación de aplicaciones con `withPricingTier()` o directamente al definir un plan a través de `azure.appServices().appServicePlans().define()`</span><span class="sxs-lookup"><span data-stu-id="99c43-150">Used to define a plan tier in-line during app creation with `withPricingTier()` or directly when defining a plan via `azure.appServices().appServicePlans().define()`</span></span>
| [<span data-ttu-id="99c43-151">JavaVersion</span><span class="sxs-lookup"><span data-stu-id="99c43-151">JavaVersion</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.appservice._java_version) | <span data-ttu-id="99c43-152">Clase con campos públicos estáticos que representa las versiones de Java admitidas por App Service.</span><span class="sxs-lookup"><span data-stu-id="99c43-152">Class with static public fields representing Java versions supported by App Service.</span></span> <span data-ttu-id="99c43-153">Se usa con `withJavaVersion()` durante la cadena `define()...create()` al crear una aplicación web nueva.</span><span class="sxs-lookup"><span data-stu-id="99c43-153">Used with `withJavaVersion()` during the `define()...create()` chain when creating a new webapp.</span></span>

## <a name="next-steps"></a><span data-ttu-id="99c43-154">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="99c43-154">Next steps</span></span>

[!INCLUDE [next-steps](includes/java-next-steps.md)]