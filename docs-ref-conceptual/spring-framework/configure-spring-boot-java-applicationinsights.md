---
title: Configuración de una aplicación de Spring Boot Initializr para que use Azure Application Insights SpringBoot Starter
description: Configure una aplicación de Spring Boot creada con Spring Initializr para que use Application Insights SpringBoot Starter.
services: Application-Insights
documentationcenter: java
author: dhaval24
manager: alexklim
editor: ''
ms.assetid: ''
ms.author: dhdoshi
ms.date: 12/19/2018
ms.devlang: java
ms.service: Azure Monitor
ms.tgt_pltfrm: application-insights
ms.topic: article
ms.workload: na
ms.openlocfilehash: f69cdcc5b479e83b230f23a8a76f96284a1b785b
ms.sourcegitcommit: f0f140b0862ca5338b1b7e5c33cec3e58a70b8fd
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/03/2019
ms.locfileid: "53991439"
---
# <a name="configure-a-spring-boot-initializer-app-to-use-application-insights"></a><span data-ttu-id="ca8b9-103">Configuración de una aplicación de Spring Boot Initializr para que use Application Insights</span><span class="sxs-lookup"><span data-stu-id="ca8b9-103">Configure a Spring Boot Initializer app to use Application Insights</span></span>

<span data-ttu-id="ca8b9-104">En este artículo se explica cómo crear una aplicación de Spring Boot mediante **[Spring Initializr]**, que usa Spring Boot Starter de Azure Application Insights para la supervisión completa de las aplicaciones Java en la nube.</span><span class="sxs-lookup"><span data-stu-id="ca8b9-104">This article walks you through creating a Spring Boot application using **[Spring Initializr]**, that uses Azure Application Insights Spring Boot Starter for end-to-end monitoring of Java applications on cloud.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ca8b9-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ca8b9-105">Prerequisites</span></span>

<span data-ttu-id="ca8b9-106">Los siguientes requisitos previos son necesarios para seguir los pasos descritos en este artículo:</span><span class="sxs-lookup"><span data-stu-id="ca8b9-106">The following prerequisites are required in order to complete the steps in this article:</span></span>

* <span data-ttu-id="ca8b9-107">Una suscripción de Azure. Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN] o registrarse para obtener una [cuenta de Azure gratuita].</span><span class="sxs-lookup"><span data-stu-id="ca8b9-107">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="ca8b9-108">Un kit de desarrollo de Java (JDK) admitido</span><span class="sxs-lookup"><span data-stu-id="ca8b9-108">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="ca8b9-109">Para más información sobre los JDK disponibles para desarrollar en Azure, consulte <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="ca8b9-109">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="ca8b9-110">[Apache Maven](http://maven.apache.org/), versión 3.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="ca8b9-110">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-a-custom-application-using-the-spring-initializr"></a><span data-ttu-id="ca8b9-111">Creación de una aplicación personalizada mediante Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="ca8b9-111">Create a custom application using the Spring Initializr</span></span>

1. <span data-ttu-id="ca8b9-112">Vaya a [https://start.spring.io/](https://start.spring.io/).</span><span class="sxs-lookup"><span data-stu-id="ca8b9-112">Browse to [https://start.spring.io/](https://start.spring.io/).</span></span>

1. <span data-ttu-id="ca8b9-113">Especifique que quiere generar un proyecto de **Maven** con **Java**, escriba los nombres de **Group** (Grupo) y **Artifact** (Artefacto) de su aplicación y seleccione la dependencia web en la sección de dependencias.</span><span class="sxs-lookup"><span data-stu-id="ca8b9-113">Specify that you want to generate a **Maven** project with **Java**, enter the **Group** and **Artifact** names for your application, and then select web dependency in the dependenies section.</span></span>

   ![Opciones básicas de Spring Initializr][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="ca8b9-115">Spring Initializr usa los nombres de **Group** (Grupo) y **Artifact** (Artefacto) para crear el nombre del paquete, por ejemplo: *com.example.demo*.</span><span class="sxs-lookup"><span data-stu-id="ca8b9-115">The Spring Initializr will use the **Group** and **Artifact** names to create the package name; for example: *com.example.demo*.</span></span>
   >

1. <span data-ttu-id="ca8b9-116">Haga clic en el botón para **generar el proyecto**.</span><span class="sxs-lookup"><span data-stu-id="ca8b9-116">Click the button to **Generate Project**.</span></span>

1. <span data-ttu-id="ca8b9-117">Cuando se le solicite, descargue el proyecto en una ruta de acceso del equipo local.</span><span class="sxs-lookup"><span data-stu-id="ca8b9-117">When prompted, download the project to a path on your local computer.</span></span>

1. <span data-ttu-id="ca8b9-118">Después de extraer los archivos en el sistema local, la aplicación personalizada de Spring Boot estará lista para editarla.</span><span class="sxs-lookup"><span data-stu-id="ca8b9-118">After you have extracted the files on your local system, your custom Spring Boot application will be ready for editing.</span></span>

   ![Archivos de proyecto personalizados de Spring Boot][SI02]

## <a name="create-an-application-insights-resource-on-azure"></a><span data-ttu-id="ca8b9-120">Creación de un recurso de Application Insights en Azure</span><span class="sxs-lookup"><span data-stu-id="ca8b9-120">Create an Application Insights Resource on Azure</span></span>

1. <span data-ttu-id="ca8b9-121">Vaya a Azure Portal en <https://portal.azure.com/> y haga clic en **+Nuevo**.</span><span class="sxs-lookup"><span data-stu-id="ca8b9-121">Browse to the Azure portal at <https://portal.azure.com/> and click **+New**.</span></span>

   ![Azure Portal][AZ01]

1. <span data-ttu-id="ca8b9-123">Haga clic en **Herramientas de administración** y en **Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="ca8b9-123">Click **Management Tools**, and then click **Application Insights**.</span></span>

   ![Azure Portal][AZ02]

1. <span data-ttu-id="ca8b9-125">En la página **Nuevo recurso de Application Insights**, especifique la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="ca8b9-125">On the **New Application Insights Resource** page, specify the following information:</span></span>

   * <span data-ttu-id="ca8b9-126">Escriba el **nombre** del recurso de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="ca8b9-126">Enter the **Name** for your Application Insights resource.</span></span>
   * <span data-ttu-id="ca8b9-127">Establezca **Tipo de aplicación** en Aplicación web de Java.</span><span class="sxs-lookup"><span data-stu-id="ca8b9-127">Choose the **Application Type** to Java Web Application.</span></span>
   * <span data-ttu-id="ca8b9-128">Seleccione la **Suscripción**, el **Grupo de recursos** y la **Ubicación**.</span><span class="sxs-lookup"><span data-stu-id="ca8b9-128">Specify your **Subscription**, **Resource group** and **Location**.</span></span>
   * <span data-ttu-id="ca8b9-129">Seleccione la opción Anclar al panel si desea anclar el recurso en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="ca8b9-129">Select Pin to dashboard option, if you would like to pin the resource on your Azure portal.</span></span>

   <span data-ttu-id="ca8b9-130">Cuando haya especificado estas opciones, haga clic en **Crear** para crear el recurso de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="ca8b9-130">When you have specified these options, click **Create** to create your Application Insights resource.</span></span>

   ![Azure Portal][AZ03]

1. <span data-ttu-id="ca8b9-132">Después de crear el recurso, verá que aparece en la lista **Panel** de Azure, así como en las páginas **Todos los recursos**.</span><span class="sxs-lookup"><span data-stu-id="ca8b9-132">Once your resource has been created, you will see it listed on your Azure **Dashboard**, as well as under the **All Resources** pages.</span></span> <span data-ttu-id="ca8b9-133">Puede hacer clic en el recurso en cualquiera de esas ubicaciones para abrir la página de información general del recurso de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="ca8b9-133">You can click on your resource on any of those locations to open the overview page of the Application Insights resource.</span></span> <span data-ttu-id="ca8b9-134">En esta página de información general, copie la **clave de instrumentación**.</span><span class="sxs-lookup"><span data-stu-id="ca8b9-134">From this overview page please copy the **instrumentation key**.</span></span>

   ![Azure Portal][AZ04]

## <a name="configure-your-downloaded-spring-boot-application-to-use-application-insights"></a><span data-ttu-id="ca8b9-136">Configuración de la aplicación de Spring Boot descargada para que use Application Insights</span><span class="sxs-lookup"><span data-stu-id="ca8b9-136">Configure your downloaded Spring Boot Application to use Application Insights</span></span>

1. <span data-ttu-id="ca8b9-137">Busque el archivo *POM.xml* en el directorio raíz de la aplicación y agregue la siguiente dependencia en la sección de dependencias.</span><span class="sxs-lookup"><span data-stu-id="ca8b9-137">Locate the *POM.xml* file in the root directory of your app, and add the following dependency in its dependencies section.</span></span> 

```XML
 <dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>applicationinsights-spring-boot-starter</artifactId>
    <version>1.1.1</version>
</dependency>
```

1. <span data-ttu-id="ca8b9-138">Busque el archivo *application.properties* en el directorio *resources* de la aplicación, o cree el archivo si todavía no existe.</span><span class="sxs-lookup"><span data-stu-id="ca8b9-138">Locate the *application.properties* file in the *resources* directory of your app, or create the file if it does not already exist.</span></span>

   ![Localización del archivo application.properties][RE01]

1. <span data-ttu-id="ca8b9-140">Abra el archivo *application.properties* en un editor de texto y agréguele las siguientes líneas; luego, sustituya los valores de ejemplo por las propiedades adecuadas con las credenciales correctas:</span><span class="sxs-lookup"><span data-stu-id="ca8b9-140">Open the *application.properties* file in a text editor, and add the following lines to the file, and replace the sample values with the appropriate properties with appropriate credentials:</span></span>

   ```yaml
   # Specify the instrumentation key of your Application Insights resource.
   azure.application-insights.instrumentation-key=[your ikey from the resource]
   # Specify the name of your springboot application. This can be any logical name you would like to give to your app.
   spring.application.name=[your app name]
   ```

   <span data-ttu-id="ca8b9-141">Para conocer más formas de ajustar Application Insights, consulte el [archivo léame de Spring Boot Starter de Application Insights](https://github.com/Microsoft/ApplicationInsights-Java/blob/master/azure-application-insights-spring-boot-starter/README.md).</span><span class="sxs-lookup"><span data-stu-id="ca8b9-141">For more ways to fine tune Application Insights please refer to [Application Insights Springboot starter readme](https://github.com/Microsoft/ApplicationInsights-Java/blob/master/azure-application-insights-spring-boot-starter/README.md).</span></span>

   > [!NOTE]
   > 
   > <span data-ttu-id="ca8b9-142">Puede usar diferentes claves de instrumentación de Application Insights (por ejemplo,</span><span class="sxs-lookup"><span data-stu-id="ca8b9-142">You can use different Application Insights instrumentation keys (i.e</span></span> <span data-ttu-id="ca8b9-143">recursos diferentes) para los distintos perfiles como PROD, DEV, etc. Consulte las [propiedades específicas de los perfiles de Spring Boot] para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="ca8b9-143">different resources) for different profiles like PROD, DEV etc. Please refer to [Spring Boot Profile Specific Properties] for additional information.</span></span> 

1. <span data-ttu-id="ca8b9-144">Guarde y cierre el archivo *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="ca8b9-144">Save and close the *application.properties* file.</span></span>

1. <span data-ttu-id="ca8b9-145">Cree una carpeta denominada *controller* en la carpeta de origen para el paquete; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="ca8b9-145">Create a folder named *controller* under the source folder for your package; for example:</span></span>

   `D:\Microsoft\demo\src\main\java\com\example\demo\controller`

   <span data-ttu-id="ca8b9-146">O bien</span><span class="sxs-lookup"><span data-stu-id="ca8b9-146">-or-</span></span>

   `/users/example/home/demo/src/main/java/com/example/demo/controller`

1. <span data-ttu-id="ca8b9-147">Cree un archivo llamado *TestController.java* en la carpeta *controller*.</span><span class="sxs-lookup"><span data-stu-id="ca8b9-147">Create a new file named *TestController.java* in the *controller* folder.</span></span> <span data-ttu-id="ca8b9-148">Abra el archivo en un editor de texto y agréguele el siguiente código:</span><span class="sxs-lookup"><span data-stu-id="ca8b9-148">Open the file in a text editor and add the following code to it:</span></span>

   ```java
    package com.example.demo;

    import com.microsoft.applicationinsights.TelemetryClient;
    import java.io.IOException;
    import org.springframework.beans.factory.annotation.Autowired;
    import org.springframework.web.bind.annotation.GetMapping;
    import org.springframework.web.bind.annotation.RequestMapping;
    import org.springframework.web.bind.annotation.RestController;
    import com.microsoft.applicationinsights.telemetry.Duration;

    @RestController
    @RequestMapping("/sample")
    public class TestController {

        @Autowired
        TelemetryClient telemetryClient;

        @GetMapping("/hello")
        public String hello() {

            //track a custom event  
            telemetryClient.trackEvent("Sending a custom event...");

            //trace a custom trace
            telemetryClient.trackTrace("Sending a custom trace....");

            //track a custom metric
            telemetryClient.trackMetric("custom metric", 1.0);

            //track a custom dependency
            telemetryClient.trackDependency("SQL", "Insert", new Duration(0, 0, 1, 1, 1), true);

            return "hello";
        }
    }
   ```

   <span data-ttu-id="ca8b9-149">Necesitará reemplazar `com.example.demo` con el nombre del paquete para el proyecto.</span><span class="sxs-lookup"><span data-stu-id="ca8b9-149">Where you will need to replace `com.example.demo` with the package name for your project.</span></span>

1. <span data-ttu-id="ca8b9-150">Guarde y cierre el archivo *TestController.java*.</span><span class="sxs-lookup"><span data-stu-id="ca8b9-150">Save and close the *TestController.java* file.</span></span>

1. <span data-ttu-id="ca8b9-151">Compile la aplicación de Spring Boot con Maven y ejecútela; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="ca8b9-151">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. <span data-ttu-id="ca8b9-152">Pruebe la aplicación web. Para ello, vaya a http://localhost:8080/sample/hello con un explorador web, o bien utilice una sintaxis como la del siguiente ejemplo si tiene cURL disponible:</span><span class="sxs-lookup"><span data-stu-id="ca8b9-152">Test the web app by browsing to http://localhost:8080/sample/hello using a web browser, or use the syntax like the following example if you have curl available:</span></span>

   ```shell
   curl http://localhost:8080/sample/hello
   ```

   <span data-ttu-id="ca8b9-153">Verá el mensaje "Hola"</span><span class="sxs-lookup"><span data-stu-id="ca8b9-153">You should see the "hello!"</span></span> <span data-ttu-id="ca8b9-154">del controlador de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="ca8b9-154">message from your sample controller displayed.</span></span> <span data-ttu-id="ca8b9-155">Application Insights recopilará esta solicitud automáticamente y la enviará como un elemento de telemetría con la información asociada de evento personalizado, métrica personalizada, dependencia personalizada y seguimiento personalizado, tal y como se especifica en la lógica del controlador.</span><span class="sxs-lookup"><span data-stu-id="ca8b9-155">Application Insights will automatically collect this request and send it as a telemetry item with it's associated custom event, custom metric, custom dependency and custom trace as specified in the controller logic.</span></span> 

   <span data-ttu-id="ca8b9-156">Después de unos segundos, verá los datos en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="ca8b9-156">After a few seconds you should see the data on Azure portal.</span></span> 

   ![Azure Portal][AZ05]

   <span data-ttu-id="ca8b9-158">Haga clic en el icono del mapa de aplicación para ver los componentes generales y su interacción entre sí.</span><span class="sxs-lookup"><span data-stu-id="ca8b9-158">You can click on Application Map tile to view high level components and their interaction with each other.</span></span> <span data-ttu-id="ca8b9-159">Este es el lugar recomendado para ver la información general de toda la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ca8b9-159">This is a recommended place to get a high level overview of entire application.</span></span> <span data-ttu-id="ca8b9-160">Cada microservicio de Spring Boot se reconoce por el nombre de la aplicación de Spring.</span><span class="sxs-lookup"><span data-stu-id="ca8b9-160">Each Spring Boot Microservice is recognized by the spring application name.</span></span> <span data-ttu-id="ca8b9-161">Recuerde que debe establecerlo.</span><span class="sxs-lookup"><span data-stu-id="ca8b9-161">Please remember to set it.</span></span>

   ![Azure Portal][AZ08] 

## <a name="configure-springboot-application-to-send-log4j-logs-to-application-insights"></a><span data-ttu-id="ca8b9-163">Configuración de la aplicación de Spring Boot para enviar registros log4j a Application Insights</span><span class="sxs-lookup"><span data-stu-id="ca8b9-163">Configure Springboot Application to send log4j logs to Application Insights</span></span>

1. <span data-ttu-id="ca8b9-164">Modifique el archivo POM.xml del proyecto y agregue o modifique la sección de dependencias con la siguiente información.</span><span class="sxs-lookup"><span data-stu-id="ca8b9-164">Modify the POM.xml file of the project and add/modify the dependencies section with following.</span></span> 

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
        <exclusions>
            <exclusion>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-starter-logging</artifactId>
            </exclusion>
        </exclusions>
    </dependency>

    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-test</artifactId>
        <scope>test</scope>
    </dependency>

    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-log4j2</artifactId>
    </dependency>

    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>applicationinsights-spring-boot-starter</artifactId>
        <version>1.1.1</version>
    </dependency>

    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>applicationinsights-logging-log4j2</artifactId>
        <version>2.1.1</version>
    </dependency>
</dependencies>
```

2. <span data-ttu-id="ca8b9-165">Guarde y cierre el archivo *POM.xml*.</span><span class="sxs-lookup"><span data-stu-id="ca8b9-165">Save and close the *POM.xml* file.</span></span>

3. <span data-ttu-id="ca8b9-166">En la carpeta \src\main\resources, cree un nuevo archivo *log4j2.xml* y configúrelo.</span><span class="sxs-lookup"><span data-stu-id="ca8b9-166">In \src\main\resources folder, create a new file *log4j2.xml* and configure it.</span></span> <span data-ttu-id="ca8b9-167">Por ejemplo: </span><span class="sxs-lookup"><span data-stu-id="ca8b9-167">For example:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<Configuration packages="com.microsoft.applicationinsights.log4j.v2">
  <Properties>
    <Property name="LOG_PATTERN">
      %d{yyyy-MM-dd HH:mm:ss.SSS} %5p ${hostName} --- [%15.15t] %-40.40c{1.} : %m%n%ex
    </Property>
  </Properties>
  <Appenders>
    <Console name="Console" target="SYSTEM_OUT">
      <PatternLayout pattern="%d{HH:mm:ss.SSS} [%t] %-5level %logger{36} - %msg%n"/>
    </Console>
    <ApplicationInsightsAppender name="aiAppender">
    </ApplicationInsightsAppender>
  </Appenders>
  <Loggers>
    <Root level="trace">
      <AppenderRef ref="Console"  />
      <AppenderRef ref="aiAppender"  />
    </Root>
  </Loggers>
</Configuration>
```
4. <span data-ttu-id="ca8b9-168">Vuelva a compilar y ejecutar la aplicación de Spring Boot como se indicó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="ca8b9-168">Build and run the Spring Boot application again as shown above.</span></span> 

<span data-ttu-id="ca8b9-169">En pocos segundos, verá que todos los registros de Spring están disponibles en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="ca8b9-169">Within few seconds, you should see all the spring logs being available on Azure Portal.</span></span> 

![Azure Portal][AZ06]

<span data-ttu-id="ca8b9-171">Puede consultar incluso los mensajes de registro detallados y realizar el análisis en el portal de análisis.</span><span class="sxs-lookup"><span data-stu-id="ca8b9-171">You can even look at the detailed log messages and do analysis on Analytics Portal.</span></span> 

![Azure Portal][AZ07]

## <a name="next-steps"></a><span data-ttu-id="ca8b9-173">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ca8b9-173">Next steps</span></span>

<span data-ttu-id="ca8b9-174">Para más información acerca de Spring y Azure, vaya al centro de documentación de Azure.</span><span class="sxs-lookup"><span data-stu-id="ca8b9-174">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ca8b9-175">Spring en Azure</span><span class="sxs-lookup"><span data-stu-id="ca8b9-175">Spring on Azure</span></span>](/java/azure/spring-framework)

### <a name="additional-resources"></a><span data-ttu-id="ca8b9-176">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="ca8b9-176">Additional Resources</span></span>

<span data-ttu-id="ca8b9-177">Para obtener más información sobre el uso de aplicaciones de Spring Boot en Azure, consulte los siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="ca8b9-177">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="ca8b9-178">Implementación de una aplicación de Spring Boot en Azure App Service</span><span class="sxs-lookup"><span data-stu-id="ca8b9-178">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)

* [<span data-ttu-id="ca8b9-179">Ejecución de una aplicación de Spring Boot en un clúster de Kubernetes en Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="ca8b9-179">Running a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="ca8b9-180">Application Insights permite recopilar automáticamente las dependencias externas y correlacionarlas con las solicitudes entrantes.</span><span class="sxs-lookup"><span data-stu-id="ca8b9-180">Application Insights supports automatic collection of external dependencies and its correlation with incoming requests.</span></span> <span data-ttu-id="ca8b9-181">Actualmente se admite la recopilación automática de Oracle, MsSQL, MySQL y Redis.</span><span class="sxs-lookup"><span data-stu-id="ca8b9-181">Currently we support autocollection of Oracle, MsSQL, MySQL and Redis.</span></span> <span data-ttu-id="ca8b9-182">Para más información sobre cómo habilitar la recopilación automática, consulte el artículo sobre [cómo usar el agente de Application Insights para Java](/azure/application-insights/app-insights-java-agent).</span><span class="sxs-lookup"><span data-stu-id="ca8b9-182">For more details on enabling autocollection please follow the article [how to use Application Insights Java agent](/azure/application-insights/app-insights-java-agent).</span></span>

<span data-ttu-id="ca8b9-183">Para más información sobre Azure Application Insights y sus funcionalidades de supervisión, consulte la página principal de **[Application Insights]**.</span><span class="sxs-lookup"><span data-stu-id="ca8b9-183">For more information about Azure Application Insights, and it's monitoring capabilities, see the **[Application Insights]** home page.</span></span>

<span data-ttu-id="ca8b9-184">Para más información acerca de las opciones de configuración adicionales de Spring Boot Starter de Application Insights, consulte este [vínculo](https://github.com/Microsoft/ApplicationInsights-Java/blob/master/azure-application-insights-spring-boot-starter/README.md).</span><span class="sxs-lookup"><span data-stu-id="ca8b9-184">For more information about additional configuration details of Application Insights Spring Boot Starter, please refer to this [link](https://github.com/Microsoft/ApplicationInsights-Java/blob/master/azure-application-insights-spring-boot-starter/README.md).</span></span>

<span data-ttu-id="ca8b9-185">Para solicitar características y notificar posibles errores, abra incidencias en nuestro repositorio de [GitHub](https://github.com/Microsoft/ApplicationInsights-Java/issues).</span><span class="sxs-lookup"><span data-stu-id="ca8b9-185">For feature requests and potential bugs, please open issues on our [GitHub](https://github.com/Microsoft/ApplicationInsights-Java/issues) repository.</span></span>

<span data-ttu-id="ca8b9-186">Para más información sobre el uso de Azure con Java, consulte [Azure para desarrolladores de Java] y [Working with Azure DevOps and Java] (Trabajo con Azure DevOps y Java).</span><span class="sxs-lookup"><span data-stu-id="ca8b9-186">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Working with Azure DevOps and Java].</span></span>

<span data-ttu-id="ca8b9-187">**[Spring Framework]** es una solución de código abierto que ayuda a los desarrolladores de Java a crear aplicaciones de nivel empresarial.</span><span class="sxs-lookup"><span data-stu-id="ca8b9-187">The **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="ca8b9-188">Uno de los proyectos más populares que se basa en esa plataforma es [Spring Boot], que proporciona un enfoque simplificado para crear aplicaciones de Java independientes.</span><span class="sxs-lookup"><span data-stu-id="ca8b9-188">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="ca8b9-189">Para ayudar a los desarrolladores a empezar con Spring Boot, hay varios paquetes de ejemplo de Spring Boot disponibles en [https://github.com/spring-guides/](https://github.com/spring-guides/).</span><span class="sxs-lookup"><span data-stu-id="ca8b9-189">To help developers get started with Spring Boot, several sample Spring Boot packages are available at [https://github.com/spring-guides/](https://github.com/spring-guides/).</span></span> <span data-ttu-id="ca8b9-190">Además de elegir de la lista de proyectos básicos de Spring Boot, el **[Spring Initializr]** ayuda a los desarrolladores en los primeros pasos para crear aplicaciones de Spring Boot personalizadas.</span><span class="sxs-lookup"><span data-stu-id="ca8b9-190">In addition to choosing from the list of basic Spring Boot projects, the **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>

<!-- URL List -->

[Azure para desarrolladores de Java]: /java/azure/
[Azure for Java Developers]: /java/azure/
[cuenta de Azure gratuita]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Working with Azure DevOps and Java]: /azure/devops/ (Trabajo con Azure DevOps y Java)
[ventajas como suscriptor de MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Propiedades específicas de los perfiles de Spring Boot]: https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-external-config.html#boot-features-external-config-profile-specific-properties
[Spring Boot Profile Specific Properties]: https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-external-config.html#boot-features-external-config-profile-specific-properties
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/
[Application Insights]: /azure/application-insights/

<!-- IMG List -->

[AZ01]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/Create_resource.png
[AZ02]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/Create_resource_2.png
[AZ03]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/Create_resource_3.png
[AZ04]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/Get_IKey.png
[AZ05]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/OverviewBladeResults.png
[AZ06]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/Search_and_traces.png
[AZ07]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/traces_details.png
[AZ08]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/AppMap.png

[SI01]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/spring_start.png
[SI02]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/After_extract.png

[RE01]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/applicationproperties_loc.png
[RE02]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/applicationinsightsproperties.png
