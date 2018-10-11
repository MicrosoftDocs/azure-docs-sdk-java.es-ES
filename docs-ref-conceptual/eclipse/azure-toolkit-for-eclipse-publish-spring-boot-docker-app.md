---
title: Publicar una aplicación Spring Boot como contenedor de Docker mediante el kit de herramientas de Azure para Eclipse
description: Aprenda a publicar una aplicación web en Microsoft Azure como un contenedor de Docker con el kit de herramientas de Azure para Eclipse.
services: ''
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 02/01/2018
ms.devlang: Java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: c116e0712afd8e48983f946f43eddfd0c79c0ba8
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/09/2018
ms.locfileid: "48899177"
---
# <a name="publish-a-spring-boot-app-as-a-docker-container-by-using-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="ec46c-103">Publicar una aplicación Spring Boot como contenedor de Docker mediante el kit de herramientas de Azure para Eclipse</span><span class="sxs-lookup"><span data-stu-id="ec46c-103">Publish a Spring Boot app as a Docker container by using the Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="ec46c-104">[Spring Framework] es una solución de código abierto que ayuda a los desarrolladores de Java a crear aplicaciones de nivel empresarial.</span><span class="sxs-lookup"><span data-stu-id="ec46c-104">The [Spring Framework] is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="ec46c-105">Uno de los proyectos más populares que se basa en esa plataforma es [Spring Boot], que proporciona un enfoque simplificado para crear aplicaciones de Java independientes.</span><span class="sxs-lookup"><span data-stu-id="ec46c-105">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating standalone Java applications.</span></span>

<span data-ttu-id="ec46c-106">[Docker] es una solución de código abierto que ayuda a los desarrolladores a automatizar la implementación, el escalado y la administración de sus aplicaciones que se ejecutan en contenedores.</span><span class="sxs-lookup"><span data-stu-id="ec46c-106">[Docker] is an open-source solution that helps developers automate the deployment, scaling, and management of their applications that are running in containers.</span></span>

<span data-ttu-id="ec46c-107">Este tutorial le guía por los pasos necesarios para implementar una aplicación Spring Boot como un contenedor de Docker en Microsoft Azure con el kit de herramientas de Azure para Eclipse.</span><span class="sxs-lookup"><span data-stu-id="ec46c-107">This tutorial walks you through the steps to deploy a Spring Boot application as a Docker container to Microsoft Azure by using the Azure Toolkit for Eclipse.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="clone-the-default-spring-boot-docker-repository"></a><span data-ttu-id="ec46c-108">Clonar el repositorio de Docker predeterminado de Spring Boot</span><span class="sxs-lookup"><span data-stu-id="ec46c-108">Clone the default Spring Boot Docker repository</span></span>

### <a name="import-the-public-repository"></a><span data-ttu-id="ec46c-109">Importar el repositorio público</span><span class="sxs-lookup"><span data-stu-id="ec46c-109">Import the public repository</span></span>

<span data-ttu-id="ec46c-110">Los siguientes pasos le guiarán por la clonación del repositorio de Docker de Spring Boot al equipo local mediante IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="ec46c-110">The following steps walk you through cloning the Spring Boot Docker repository to your local computer by using IntelliJ.</span></span> <span data-ttu-id="ec46c-111">Si quiere usar una línea de comandos, vea [Implementación de una aplicación de Spring Boot en Linux en Azure Container Service][Deploy Spring Boot on Linux in AKS].</span><span class="sxs-lookup"><span data-stu-id="ec46c-111">If you want to use a command line, see [Deploy a Spring Boot application on Linux in Azure Container Service][Deploy Spring Boot on Linux in AKS].</span></span>

1. <span data-ttu-id="ec46c-112">Abra Eclipse.</span><span class="sxs-lookup"><span data-stu-id="ec46c-112">Open Eclipse.</span></span>

1. <span data-ttu-id="ec46c-113">Haga clic en **Archivo** > **Importar**.</span><span class="sxs-lookup"><span data-stu-id="ec46c-113">Click **File** > **Import**.</span></span>

   ![Menú de importación de archivo][CL01]

1. <span data-ttu-id="ec46c-115">Cuando se abra el cuadro de diálogo **Importar**:</span><span class="sxs-lookup"><span data-stu-id="ec46c-115">When the **Import** dialog box opens:</span></span>

   <span data-ttu-id="ec46c-116">a.</span><span class="sxs-lookup"><span data-stu-id="ec46c-116">a.</span></span> <span data-ttu-id="ec46c-117">Expanda **GIT**.</span><span class="sxs-lookup"><span data-stu-id="ec46c-117">Expand **Git**.</span></span>

   <span data-ttu-id="ec46c-118">b.</span><span class="sxs-lookup"><span data-stu-id="ec46c-118">b.</span></span> <span data-ttu-id="ec46c-119">Seleccione **Proyectos de GIT**.</span><span class="sxs-lookup"><span data-stu-id="ec46c-119">Select **Projects from Git**.</span></span>
   
   <span data-ttu-id="ec46c-120">c.</span><span class="sxs-lookup"><span data-stu-id="ec46c-120">c.</span></span> <span data-ttu-id="ec46c-121">Haga clic en **Next**.</span><span class="sxs-lookup"><span data-stu-id="ec46c-121">Click **Next**.</span></span>

   ![Cuadro de diálogo de importación][CL02]

1. <span data-ttu-id="ec46c-123">En la página **Seleccionar origen del repositorio**:</span><span class="sxs-lookup"><span data-stu-id="ec46c-123">On the **Select Repository Source** page:</span></span>

   <span data-ttu-id="ec46c-124">a.</span><span class="sxs-lookup"><span data-stu-id="ec46c-124">a.</span></span> <span data-ttu-id="ec46c-125">Seleccione **Clonar URI**.</span><span class="sxs-lookup"><span data-stu-id="ec46c-125">Select **Clone URI**.</span></span>
   
   <span data-ttu-id="ec46c-126">b.</span><span class="sxs-lookup"><span data-stu-id="ec46c-126">b.</span></span> <span data-ttu-id="ec46c-127">Haga clic en **Next**.</span><span class="sxs-lookup"><span data-stu-id="ec46c-127">Click **Next**.</span></span>

   ![Página Seleccionar origen del repositorio][CL03]

1. <span data-ttu-id="ec46c-129">En la página **Repositorio GIT de origen**:</span><span class="sxs-lookup"><span data-stu-id="ec46c-129">On the **Source Git Repository** page:</span></span>

   <span data-ttu-id="ec46c-130">a.</span><span class="sxs-lookup"><span data-stu-id="ec46c-130">a.</span></span> <span data-ttu-id="ec46c-131">Para **URI**, escriba `https://github.com/spring-guides/gs-spring-boot-docker.git`.</span><span class="sxs-lookup"><span data-stu-id="ec46c-131">For **URI**, enter `https://github.com/spring-guides/gs-spring-boot-docker.git`.</span></span> <span data-ttu-id="ec46c-132">Con este paso se deberían rellenar automáticamente los campos **Host** y **Ruta de acceso de repositorio** con los valores correctos.</span><span class="sxs-lookup"><span data-stu-id="ec46c-132">This step should automatically populate the **Host** and **Repository path** fields with the correct values.</span></span>
   
   <span data-ttu-id="ec46c-133">b.</span><span class="sxs-lookup"><span data-stu-id="ec46c-133">b.</span></span> <span data-ttu-id="ec46c-134">El repositorio de Spring Boot es público, por lo que no debe escribir el nombre de usuario ni la contraseña de GIT.</span><span class="sxs-lookup"><span data-stu-id="ec46c-134">The Spring Boot repository is public, so you should not have to enter your Git username and password.</span></span>
   
   <span data-ttu-id="ec46c-135">c.</span><span class="sxs-lookup"><span data-stu-id="ec46c-135">c.</span></span> <span data-ttu-id="ec46c-136">Haga clic en **Next**.</span><span class="sxs-lookup"><span data-stu-id="ec46c-136">Click **Next**.</span></span>

   ![Página Repositorio de GIT de origen][CL04]

1. <span data-ttu-id="ec46c-138">En la página **Selección de rama**, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="ec46c-138">On the **Branch Selection** page, click **Next**.</span></span>

   ![Página Selección de rama][CL05]

1. <span data-ttu-id="ec46c-140">En la página **Destino local**:</span><span class="sxs-lookup"><span data-stu-id="ec46c-140">On the **Local Destination** page:</span></span>

   <span data-ttu-id="ec46c-141">a.</span><span class="sxs-lookup"><span data-stu-id="ec46c-141">a.</span></span> <span data-ttu-id="ec46c-142">Especifique la carpeta local donde desea que esté el repositorio local.</span><span class="sxs-lookup"><span data-stu-id="ec46c-142">Specify the local folder where you want your local repo.</span></span>
   
   <span data-ttu-id="ec46c-143">b.</span><span class="sxs-lookup"><span data-stu-id="ec46c-143">b.</span></span> <span data-ttu-id="ec46c-144">Haga clic en **Next**.</span><span class="sxs-lookup"><span data-stu-id="ec46c-144">Click **Next**.</span></span>

   ![Página Destino local][CL06]

1. <span data-ttu-id="ec46c-146">En la página **Seleccionar un asistente para usar en la importación de proyectos**:</span><span class="sxs-lookup"><span data-stu-id="ec46c-146">On the **Select a wizard to use for importing projects** page:</span></span>

   <span data-ttu-id="ec46c-147">a.</span><span class="sxs-lookup"><span data-stu-id="ec46c-147">a.</span></span> <span data-ttu-id="ec46c-148">Seleccione **Import as a general project** (Importar como proyecto general).</span><span class="sxs-lookup"><span data-stu-id="ec46c-148">Select **Import as a general project**.</span></span>
   
   <span data-ttu-id="ec46c-149">b.</span><span class="sxs-lookup"><span data-stu-id="ec46c-149">b.</span></span> <span data-ttu-id="ec46c-150">Haga clic en **Next**.</span><span class="sxs-lookup"><span data-stu-id="ec46c-150">Click **Next**.</span></span>

   ![Página "Seleccionar un asistente para usar en la importación de proyectos"][CL07]

1. <span data-ttu-id="ec46c-152">En la página **Importar proyectos**:</span><span class="sxs-lookup"><span data-stu-id="ec46c-152">On the **Import Projects** page:</span></span>

   <span data-ttu-id="ec46c-153">a.</span><span class="sxs-lookup"><span data-stu-id="ec46c-153">a.</span></span> <span data-ttu-id="ec46c-154">Especifique el nombre del proyecto.</span><span class="sxs-lookup"><span data-stu-id="ec46c-154">Specify your project name.</span></span>
   
   <span data-ttu-id="ec46c-155">b.</span><span class="sxs-lookup"><span data-stu-id="ec46c-155">b.</span></span> <span data-ttu-id="ec46c-156">Haga clic en **Finalizar**</span><span class="sxs-lookup"><span data-stu-id="ec46c-156">Click **Finish**.</span></span>

   ![Página Importar proyectos][CL08]

1. <span data-ttu-id="ec46c-158">Una vez que el repositorio se clone correctamente, verá todos los archivos en Eclipse.</span><span class="sxs-lookup"><span data-stu-id="ec46c-158">When the repository is cloned successfully, you see all the files listed in Eclipse.</span></span>

   ![Repositorio local][CL09]

### <a name="create-a-maven-project-from-your-local-repository"></a><span data-ttu-id="ec46c-160">Crear un proyecto de Maven desde el repositorio local</span><span class="sxs-lookup"><span data-stu-id="ec46c-160">Create a Maven project from your local repository</span></span>

<span data-ttu-id="ec46c-161">El repositorio de Docker de Spring Boot contiene un proyecto de Maven finalizado que usará para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="ec46c-161">The Spring Boot Docker repository contains a completed Maven project, which you will use for this tutorial.</span></span> 

1. <span data-ttu-id="ec46c-162">Haga clic en **Archivo** > **Importar**.</span><span class="sxs-lookup"><span data-stu-id="ec46c-162">Click **File** > **Import**.</span></span>

   ![Comando Importar en el menú Archivo][CL01]

1. <span data-ttu-id="ec46c-164">Cuando se abra el cuadro de diálogo **Importar**:</span><span class="sxs-lookup"><span data-stu-id="ec46c-164">When the **Import** dialog box opens:</span></span>

   <span data-ttu-id="ec46c-165">a.</span><span class="sxs-lookup"><span data-stu-id="ec46c-165">a.</span></span> <span data-ttu-id="ec46c-166">Expanda **Maven**.</span><span class="sxs-lookup"><span data-stu-id="ec46c-166">Expand **Maven**.</span></span>
   
   <span data-ttu-id="ec46c-167">b.</span><span class="sxs-lookup"><span data-stu-id="ec46c-167">b.</span></span> <span data-ttu-id="ec46c-168">Seleccione **Existing Maven Projects** (Proyectos existentes de Maven).</span><span class="sxs-lookup"><span data-stu-id="ec46c-168">Select **Existing Maven Projects**.</span></span>
   
   <span data-ttu-id="ec46c-169">c.</span><span class="sxs-lookup"><span data-stu-id="ec46c-169">c.</span></span> <span data-ttu-id="ec46c-170">Haga clic en **Next**.</span><span class="sxs-lookup"><span data-stu-id="ec46c-170">Click **Next**.</span></span>

   ![Cuadro de diálogo de importación][MV01]

1. <span data-ttu-id="ec46c-172">En la página **Maven Projects** (Proyectos de Maven):</span><span class="sxs-lookup"><span data-stu-id="ec46c-172">On the **Maven Projects** page:</span></span>

   <span data-ttu-id="ec46c-173">a.</span><span class="sxs-lookup"><span data-stu-id="ec46c-173">a.</span></span> <span data-ttu-id="ec46c-174">Para **Directorio raíz**, especifique la carpeta **complete** del repositorio local.</span><span class="sxs-lookup"><span data-stu-id="ec46c-174">For **Root Directory**, specify the **complete** folder in your local repository.</span></span>
   
   <span data-ttu-id="ec46c-175">b.</span><span class="sxs-lookup"><span data-stu-id="ec46c-175">b.</span></span> <span data-ttu-id="ec46c-176">Expanda la sección **Avanzado** y escriba un nombre personalizado para **Plantilla de nombre**.</span><span class="sxs-lookup"><span data-stu-id="ec46c-176">Expand the **Advanced** section, and enter a custom name for **Name template**.</span></span>
   
   <span data-ttu-id="ec46c-177">c.</span><span class="sxs-lookup"><span data-stu-id="ec46c-177">c.</span></span> <span data-ttu-id="ec46c-178">Active la casilla para el archivo **pom.xml** en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="ec46c-178">Select the box for the **pom.xml** file in the project.</span></span>
   
   <span data-ttu-id="ec46c-179">d.</span><span class="sxs-lookup"><span data-stu-id="ec46c-179">d.</span></span> <span data-ttu-id="ec46c-180">Haga clic en **Finalizar**</span><span class="sxs-lookup"><span data-stu-id="ec46c-180">Click **Finish**.</span></span>

   ![Página de proyectos de Maven][MV02]

1. <span data-ttu-id="ec46c-182">Cuando el proyecto de Maven se abra correctamente, verá un segundo proyecto en Eclipse.</span><span class="sxs-lookup"><span data-stu-id="ec46c-182">When the Maven project is opened successfully, you see a second project listed in Eclipse.</span></span>

   ![Proyecto local de Maven][MV03]

## <a name="build-your-spring-boot-app-by-using-maven"></a><span data-ttu-id="ec46c-184">Crear una aplicación Spring Boot mediante Maven</span><span class="sxs-lookup"><span data-stu-id="ec46c-184">Build your Spring Boot app by using Maven</span></span>

1. <span data-ttu-id="ec46c-185">En el Explorador de proyectos de Eclipse, seleccione el proyecto de Maven.</span><span class="sxs-lookup"><span data-stu-id="ec46c-185">In the Eclipse Project Explorer, select the Maven project.</span></span>

1. <span data-ttu-id="ec46c-186">Haga clic en **Ejecutar** > **Ejecutar como** > **Compilación de Maven**.</span><span class="sxs-lookup"><span data-stu-id="ec46c-186">Click **Run** > **Run As** > **Maven build**.</span></span>

   ![Comandos para ejecutar como compilación de Maven][BU01]

1. <span data-ttu-id="ec46c-188">Una vez que la aplicación se compile correctamente, la ventana de la consola muestra el estado.</span><span class="sxs-lookup"><span data-stu-id="ec46c-188">When your application is successfully built, the console window shows the status.</span></span>

   ![Compilación correcta de Maven][BU02]

## <a name="publish-your-web-app-to-azure-by-using-a-docker-container"></a><span data-ttu-id="ec46c-190">Publicación de su aplicación web en Azure mediante un contenedor de Docker</span><span class="sxs-lookup"><span data-stu-id="ec46c-190">Publish your web app to Azure by using a Docker container</span></span>

1. <span data-ttu-id="ec46c-191">En el Explorador de proyectos de Eclipse, seleccione el proyecto de Maven.</span><span class="sxs-lookup"><span data-stu-id="ec46c-191">In the Eclipse Project Explorer, select the Maven project.</span></span>

1. <span data-ttu-id="ec46c-192">Haga clic en el menú **Publicar** de Azure y, luego, en **Publicar como contenedor de Docker**.</span><span class="sxs-lookup"><span data-stu-id="ec46c-192">Click the Azure **Publish** menu, and then click **Publish as Docker Container**.</span></span>

   ![Comando Publish as Docker Container (Publicar como contenedor de Docker)][PU01]

1. <span data-ttu-id="ec46c-194">Cuando aparezca el cuadro de diálogo **Implementación del contenedor de Docker en Azure**:</span><span class="sxs-lookup"><span data-stu-id="ec46c-194">When the **Deploying Docker Container on Azure** dialog box appears:</span></span>

   <span data-ttu-id="ec46c-195">a.</span><span class="sxs-lookup"><span data-stu-id="ec46c-195">a.</span></span> <span data-ttu-id="ec46c-196">Escriba un nombre de imagen de Docker personalizado.</span><span class="sxs-lookup"><span data-stu-id="ec46c-196">Enter a custom Docker image name.</span></span>
   
   <span data-ttu-id="ec46c-197">b.</span><span class="sxs-lookup"><span data-stu-id="ec46c-197">b.</span></span> <span data-ttu-id="ec46c-198">Para **Artifact to deploy** (Artefacto para implementar), especifique la ruta de acceso al archivo **gs-spring-boot-docker-0.1.0.jar** que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="ec46c-198">For **Artifact to deploy**, specify the path to the **gs-spring-boot-docker-0.1.0.jar** file you just built.</span></span>

   ![Especificar opciones de Docker][PU02]

   <span data-ttu-id="ec46c-200">Se muestran todos los hosts de Docker existentes.</span><span class="sxs-lookup"><span data-stu-id="ec46c-200">Any existing Docker hosts are displayed.</span></span> 

1. <span data-ttu-id="ec46c-201">Si decide implementar en un host existente, puede ir al paso 5.</span><span class="sxs-lookup"><span data-stu-id="ec46c-201">If you choose to deploy to an existing host, you can skip to step 5.</span></span> <span data-ttu-id="ec46c-202">En caso contrario, use los pasos siguientes para crear un host:</span><span class="sxs-lookup"><span data-stu-id="ec46c-202">Otherwise, use the following steps to create a host:</span></span>

   <span data-ttu-id="ec46c-203">a.</span><span class="sxs-lookup"><span data-stu-id="ec46c-203">a.</span></span> <span data-ttu-id="ec46c-204">Haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="ec46c-204">Click **Add**.</span></span>

      ![Agregar un nuevo host de Docker][PU03]

   <span data-ttu-id="ec46c-206">b.</span><span class="sxs-lookup"><span data-stu-id="ec46c-206">b.</span></span> <span data-ttu-id="ec46c-207">Cuando aparezca el cuadro de diálogo **Create Docker Host** (Crear host de Docker), puede aceptar los valores predeterminados o especificar cualquier configuración personalizada para el nuevo host de Docker.</span><span class="sxs-lookup"><span data-stu-id="ec46c-207">When the **Create Docker Host** dialog box appears, you can choose to accept the defaults, or you can specify any custom settings for your new Docker host.</span></span> <span data-ttu-id="ec46c-208">(Para obtener descripciones detalladas de las distintas configuraciones, vea [Publicación de una aplicación web como contenedor de Docker con el kit de herramientas de Azure para IntelliJ][Publish Container with Azure Toolkit]). Haga clic en **Siguiente** cuando haya especificado qué configuración usar.</span><span class="sxs-lookup"><span data-stu-id="ec46c-208">(For detailed descriptions of the various settings, see [Publish a web app as a Docker container by using the Azure Toolkit for IntelliJ][Publish Container with Azure Toolkit].) Click **Next** when you have specified which settings to use.</span></span>

      ![Especificar las opciones de host de Docker][PU04]

   <span data-ttu-id="ec46c-210">c.</span><span class="sxs-lookup"><span data-stu-id="ec46c-210">c.</span></span> <span data-ttu-id="ec46c-211">Puede elegir usar las credenciales de inicio de sesión existentes desde Azure Key Vault, o puede escribir las nuevas credenciales de inicio de sesión de Docker.</span><span class="sxs-lookup"><span data-stu-id="ec46c-211">You can choose to use existing login credentials from an Azure key vault, or you can choose to enter new Docker login credentials.</span></span> <span data-ttu-id="ec46c-212">Haga clic en **Finalizar** cuando haya especificado las opciones.</span><span class="sxs-lookup"><span data-stu-id="ec46c-212">Click **Finish** when you have specified your options.</span></span>

      ![Especificar credenciales del host de Docker][PU05]

1. <span data-ttu-id="ec46c-214">Seleccione el host de Docker y, después, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="ec46c-214">Select your Docker host, and then click **Next**.</span></span>

   ![Seleccionar el host de Docker que se va a usar][PU06]

1. <span data-ttu-id="ec46c-216">En la última página del cuadro de diálogo **Deploying Docker Container on Azure** (Implementación de un contenedor de Docker en Azure), especifique las siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="ec46c-216">On the last page of the **Deploying Docker Container on Azure** dialog box, specify the following options:</span></span>

   <span data-ttu-id="ec46c-217">a.</span><span class="sxs-lookup"><span data-stu-id="ec46c-217">a.</span></span> <span data-ttu-id="ec46c-218">Puede elegir especificar un nombre personalizado para el contenedor que va a hospedar el contenedor de Docker, o puede aceptar el valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="ec46c-218">You can choose to specify a custom name for the container that will host your Docker container, or you can accept the default.</span></span>

   <span data-ttu-id="ec46c-219">b.</span><span class="sxs-lookup"><span data-stu-id="ec46c-219">b.</span></span> <span data-ttu-id="ec46c-220">Escriba los puertos TCP para el host de Docker mediante la sintaxis siguiente: *[puerto externo]*:*[puerto interno]*.</span><span class="sxs-lookup"><span data-stu-id="ec46c-220">Enter the TCP ports for your docker host by using the following syntax: *[external port]*:*[internal port]*.</span></span> <span data-ttu-id="ec46c-221">Por ejemplo, **80:8080** especifica un puerto externo de 80 y el puerto de Spring Boot interno predeterminado de 8080.</span><span class="sxs-lookup"><span data-stu-id="ec46c-221">For example, **80:8080** specifies an external port of 80 and the default internal Spring Boot port of 8080.</span></span>
   
      <span data-ttu-id="ec46c-222">Si ha personalizado el puerto interno, (por ejemplo, mediante la edición del archivo application.yml), debe especificar el número de puerto para que el enrutamiento correcto se produzca en Azure.</span><span class="sxs-lookup"><span data-stu-id="ec46c-222">If you have customized your internal port (for example, by editing the application.yml file), you need to specify the port number for the correct routing to occur in Azure.</span></span>

   <span data-ttu-id="ec46c-223">c.</span><span class="sxs-lookup"><span data-stu-id="ec46c-223">c.</span></span> <span data-ttu-id="ec46c-224">Después de configurar estas opciones, haga clic en **Finalizar**.</span><span class="sxs-lookup"><span data-stu-id="ec46c-224">After you configure these options, click **Finish**.</span></span>

   ![Implementar un contenedor de Docker en Azure][PU07]

1. <span data-ttu-id="ec46c-226">Cuando el kit de herramientas de Azure ha terminado la publicación, el registro de actividad de Azure muestra **Publicado** en el estado.</span><span class="sxs-lookup"><span data-stu-id="ec46c-226">When the Azure Toolkit has finished publishing, the Azure Activity Log displays **Published** for the status.</span></span>

   ![Host de Docker correctamente implementado][PU08]

## <a name="next-steps"></a><span data-ttu-id="ec46c-228">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ec46c-228">Next steps</span></span>

<span data-ttu-id="ec46c-229">Para más recursos de Docker, consulte el [sitio web de Docker](https://www.docker.com/) oficial.</span><span class="sxs-lookup"><span data-stu-id="ec46c-229">For additional resources for Docker, see the official [Docker website](https://www.docker.com/).</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<!-- URL List -->

[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Deploy Spring Boot on Linux in AKS]: /azure/container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux
[Docker]: https://www.docker.com/
[Publish Container with Azure Toolkit]: azure-toolkit-for-eclipse-publish-as-docker-container.md
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[CL01]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL01.png
[CL02]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL02.png
[CL03]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL03.png
[CL04]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL04.png
[CL05]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL05.png
[CL06]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL06.png
[CL07]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL07.png
[CL08]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL08.png
[CL09]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL09.png

[MV01]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV01.png
[MV02]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV02.png
[MV03]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV03.png

[BU01]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/BU01.png
[BU02]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/BU02.png

[PU01]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU01.png
[PU02]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU02.png
[PU03]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU03.png
[PU04]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU04.png
[PU05]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU05.png
[PU06]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU06.png
[PU07]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU07.png
[PU08]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU08.png
