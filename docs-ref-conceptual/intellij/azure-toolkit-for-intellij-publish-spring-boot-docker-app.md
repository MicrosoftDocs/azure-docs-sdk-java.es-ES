---
title: Publicar una aplicación Spring Boot como contenedor de Docker mediante el kit de herramientas de Azure para IntelliJ
description: Aprenda a publicar una aplicación web en Microsoft Azure como un contenedor de Docker con el kit de herramientas de Azure para IntelliJ.
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
ms.openlocfilehash: 4228352efa4354bfe4969c1a5ecd3f3b40483f85
ms.sourcegitcommit: 151aaa6ccc64d94ed67f03e846bab953bde15b4a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/03/2018
ms.locfileid: "28954736"
---
# <a name="publish-a-spring-boot-app-as-a-docker-container-by-using-the-azure-toolkit-for-intellij"></a><span data-ttu-id="00c9a-103">Publicar una aplicación Spring Boot como contenedor de Docker mediante el kit de herramientas de Azure para IntelliJ</span><span class="sxs-lookup"><span data-stu-id="00c9a-103">Publish a Spring Boot app as a Docker container by using the Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="00c9a-104">[Spring Framework] es una solución de código abierto que ayuda a los desarrolladores de Java a crear aplicaciones de nivel empresarial.</span><span class="sxs-lookup"><span data-stu-id="00c9a-104">The [Spring Framework] is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="00c9a-105">Uno de los proyectos más populares que se basa en esa plataforma es [Spring Boot], que proporciona un enfoque simplificado para crear aplicaciones de Java independientes.</span><span class="sxs-lookup"><span data-stu-id="00c9a-105">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating standalone Java applications.</span></span>

<span data-ttu-id="00c9a-106">[Docker] es una solución de código abierto que ayuda a los desarrolladores a automatizar la implementación, el escalado y la administración de sus aplicaciones que se ejecutan en contenedores.</span><span class="sxs-lookup"><span data-stu-id="00c9a-106">[Docker] is an open-source solution that helps developers automate the deployment, scaling, and management of their applications that are running in containers.</span></span>

<span data-ttu-id="00c9a-107">Este tutorial le guía por los pasos necesarios para implementar una aplicación Spring Boot como un contenedor de Docker en Microsoft Azure mediante el kit de herramientas de Azure para IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="00c9a-107">This tutorial walks you through the steps to deploy a Spring Boot application as a Docker container to Microsoft Azure by using the Azure Toolkit for IntelliJ.</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="clone-the-default-spring-boot-docker-repo"></a><span data-ttu-id="00c9a-108">Clonar el repositorio de Docker predeterminado de Spring Boot</span><span class="sxs-lookup"><span data-stu-id="00c9a-108">Clone the default Spring Boot Docker repo</span></span>

<span data-ttu-id="00c9a-109">Los siguientes pasos le guían por la clonación del repositorio de Docker de Spring Boot mediante IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="00c9a-109">The following steps walk you through cloning the Spring Boot Docker repo by using IntelliJ.</span></span> <span data-ttu-id="00c9a-110">Si quiere usar una línea de comandos, vea [Implementación de una aplicación de Spring Boot en Linux en Azure Container Service][Deploy Spring Boot on Linux in AKS].</span><span class="sxs-lookup"><span data-stu-id="00c9a-110">If you want to use a command line, see [Deploy a Spring Boot application on Linux in Azure Container Service][Deploy Spring Boot on Linux in AKS].</span></span>

1. <span data-ttu-id="00c9a-111">Abra IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="00c9a-111">Open IntelliJ.</span></span>

1. <span data-ttu-id="00c9a-112">En la página principal, seleccione la opción **GitHub** en la lista **Check out from Version Control** (Extraer del repositorio del control de versiones).</span><span class="sxs-lookup"><span data-stu-id="00c9a-112">On the welcome screen, select the **GitHub** option in the **Check out from Version Control** list.</span></span>

   ![Opción de GitHub para el control de versiones][CL01]

1. <span data-ttu-id="00c9a-114">Introduzca sus credenciales si se le pide que inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="00c9a-114">Enter your credentials if you are prompted to log in.</span></span>

   * <span data-ttu-id="00c9a-115">Si está usando un nombre de usuario y una contraseña para iniciar sesión en GitHub:</span><span class="sxs-lookup"><span data-stu-id="00c9a-115">If you are using a username/password to log in to GitHub:</span></span> 

      ![Cuadro de diálogo para escribir el nombre de usuario y la contraseña de GitHub][CL02a]

   * <span data-ttu-id="00c9a-117">Si está usando un token para iniciar sesión en GitHub:</span><span class="sxs-lookup"><span data-stu-id="00c9a-117">If you are using a token to log in to GitHub:</span></span> 

      ![Cuadro de diálogo para especificar un token de GitHub][CL02b]

1. <span data-ttu-id="00c9a-119">Escriba **https://github.com/spring-guides/gs-spring-boot-docker.git** para la dirección URL de repositorio, especifique la ruta de acceso local y la información de la carpeta y, después, haga clic en **Clonar**.</span><span class="sxs-lookup"><span data-stu-id="00c9a-119">Enter **https://github.com/spring-guides/gs-spring-boot-docker.git** for the repo URL, specify your local path and folder information, and then click **Clone**.</span></span>

   ![Cuadro de diálogo Clonar repositorio][CL03]

1. <span data-ttu-id="00c9a-121">Cuando se le pida crear un proyecto de IntelliJ, haga clic en **No**.</span><span class="sxs-lookup"><span data-stu-id="00c9a-121">When you're prompted to create an IntelliJ project, select **No**.</span></span>

   ![Declinación para crear un proyecto de IntelliJ][CL04]

1. <span data-ttu-id="00c9a-123">En la página principal, haga clic en **Importar proyecto**.</span><span class="sxs-lookup"><span data-stu-id="00c9a-123">On the welcome page, click **Import Project**.</span></span>

   ![Selección de Importar proyecto][CL05]

1. <span data-ttu-id="00c9a-125">Busque la ruta de acceso donde ha clonado el repositorio de Spring Boot, seleccione la carpeta **complete** bajo la raíz y, después, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="00c9a-125">Locate the path where you cloned the Spring Boot repo, select the **complete** folder under the root, and then click **OK**.</span></span>

   ![Seleccionar una carpeta para la importación][CL06]

1. <span data-ttu-id="00c9a-127">Cuando se le pida, seleccione **Create project from existing sources** (Crear proyecto a partir de orígenes existentes).</span><span class="sxs-lookup"><span data-stu-id="00c9a-127">When you're prompted, select **Create project from existing sources**.</span></span>

   ![Opción para crear un proyecto a partir de orígenes existentes][CL07]

1. <span data-ttu-id="00c9a-129">Especifique el nombre del proyecto o acepte el valor predeterminado, compruebe la ruta de acceso correcta a la carpeta **complete** y, después, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="00c9a-129">Specify your project name or accept the default, verify the correct path to the **complete** folder, and then click **Next**.</span></span>

   ![Especificar el nombre del proyecto][CL08]

1. <span data-ttu-id="00c9a-131">Personalice los directorios para importar y haga clic en **Next** (Siguiente).</span><span class="sxs-lookup"><span data-stu-id="00c9a-131">Customize any directories for importing, and then click **Next**.</span></span>

   ![Elegir directorios][CL09]

1. <span data-ttu-id="00c9a-133">Revise las bibliotecas que se van a importar y haga clic en **Next** (Siguiente).</span><span class="sxs-lookup"><span data-stu-id="00c9a-133">Review the libraries to import, and then click **Next**.</span></span>

   ![Revisar bibliotecas de proyecto][CL10]

1. <span data-ttu-id="00c9a-135">Revise la estructura del módulo y haga clic en **Next** (Siguiente).</span><span class="sxs-lookup"><span data-stu-id="00c9a-135">Review the module structure, and then click **Next**.</span></span>

   ![Revisar la estructura del módulo][CL11]

1. <span data-ttu-id="00c9a-137">Especifique el JDK y, después, haga clic en **Next** (Siguiente).</span><span class="sxs-lookup"><span data-stu-id="00c9a-137">Specify your JDK, and then click **Next**.</span></span>

   ![Especificar un JDK][CL12]

1. <span data-ttu-id="00c9a-139">Haga clic en **Finalizar**</span><span class="sxs-lookup"><span data-stu-id="00c9a-139">Click **Finish**.</span></span>

   ![Botón Finalizar][CL13]

<span data-ttu-id="00c9a-141">IntelliJ importa la aplicación Spring Boot como un proyecto y muestra la estructura una vez finalizada la importación.</span><span class="sxs-lookup"><span data-stu-id="00c9a-141">IntelliJ imports the Spring Boot app as a project and displays the structure when the import has finished.</span></span>

![Aplicación Spring Boot en IntelliJ][CL14]

## <a name="build-your-spring-boot-app"></a><span data-ttu-id="00c9a-143">Crear una aplicación Spring Boot</span><span class="sxs-lookup"><span data-stu-id="00c9a-143">Build your Spring Boot app</span></span>

### <a name="build-the-app-by-using-the-maven-pom"></a><span data-ttu-id="00c9a-144">Crear la aplicación con POM de Maven</span><span class="sxs-lookup"><span data-stu-id="00c9a-144">Build the app by using the Maven POM</span></span>

1. <span data-ttu-id="00c9a-145">Abra la ventana de herramientas de Maven si todavía no está abierta.</span><span class="sxs-lookup"><span data-stu-id="00c9a-145">Open the Maven tool window if it is not already opened.</span></span> <span data-ttu-id="00c9a-146">Haga clic en **Vista** > **Ventanas de herramientas** > **Proyectos de Maven**.</span><span class="sxs-lookup"><span data-stu-id="00c9a-146">Click **View** > **Tool Windows** > **Maven Projects**.</span></span>

   ![Comandos Ventanas de herramientas y Proyectos de Maven][BU01]

1. <span data-ttu-id="00c9a-148">En la ventana de herramientas de Maven, haga clic con el botón derecho en **package** (Paquete) y seleccione **Run Maven Build** (Ejecutar la compilación de Maven).</span><span class="sxs-lookup"><span data-stu-id="00c9a-148">In the Maven tool window, right-click **package** and select **Run Maven Build**.</span></span> <span data-ttu-id="00c9a-149">(Si el proyecto de Maven no se muestra automáticamente, haga clic en el icono **Reimportar** en la barra de herramientas de Maven).</span><span class="sxs-lookup"><span data-stu-id="00c9a-149">(If your Maven project does not show up automatically, click the **Reimport** icon on the Maven toolbar.)</span></span>

   ![Comando Ejecutar la compilación de Maven][BU02]

1. <span data-ttu-id="00c9a-151">IntelliJ debería mostrar un mensaje **COMPILACIÓN CORRECTA** cuando se cree correctamente la aplicación Spring Boot.</span><span class="sxs-lookup"><span data-stu-id="00c9a-151">IntelliJ should display a **BUILD SUCCESS** message when your Spring Boot app is successfully created.</span></span>

   ![Mensaje COMPILACIÓN CORRECTA][BU03]

### <a name="create-a-deployment-ready-artifact"></a><span data-ttu-id="00c9a-153">Creación de un artefacto preparado para la implementación</span><span class="sxs-lookup"><span data-stu-id="00c9a-153">Create a deployment-ready artifact</span></span>

<span data-ttu-id="00c9a-154">Para publicar la aplicación Spring Boot, debe crear un artefacto preparado para la implementación.</span><span class="sxs-lookup"><span data-stu-id="00c9a-154">To publish your Spring Boot app, you need to create a deployment-ready artifact.</span></span> <span data-ttu-id="00c9a-155">Para ello, siga los pasos que se describen a continuación:</span><span class="sxs-lookup"><span data-stu-id="00c9a-155">Use the following steps:</span></span>

1. <span data-ttu-id="00c9a-156">Abra el proyecto de aplicación web en IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="00c9a-156">Open your web app project in IntelliJ.</span></span>

1. <span data-ttu-id="00c9a-157">Haga clic en **Archivo** y después en **Estructura del proyecto**.</span><span class="sxs-lookup"><span data-stu-id="00c9a-157">Click **File**, and then click **Project Structure**.</span></span>

   ![Comando Estructura del proyecto][ART01]

1. <span data-ttu-id="00c9a-159">Haga clic en el signo más verde (**+**) para agregar un artefacto, haga clic en **JAR** y después en **Vacío**.</span><span class="sxs-lookup"><span data-stu-id="00c9a-159">Click the green plus (**+**) symbol to add an artifact, click **JAR**, and then click **Empty**.</span></span>

   ![Agregar un artefacto][ART02]

1. <span data-ttu-id="00c9a-161">Nombre el artefacto asegurándose de no agregar la extensión ".jar" y, después, especifique la carpeta de destino para la salida de Maven.</span><span class="sxs-lookup"><span data-stu-id="00c9a-161">Name your artifact while making sure not to add the ".jar" extension, and then specify the target folder for the Maven output.</span></span>

   ![Especificar las propiedades del artefacto][ART03]

1. <span data-ttu-id="00c9a-163">Cree un manifiesto para el artefacto (opcional):</span><span class="sxs-lookup"><span data-stu-id="00c9a-163">Create a manifest for your artifact (optional):</span></span>

   <span data-ttu-id="00c9a-164">a.</span><span class="sxs-lookup"><span data-stu-id="00c9a-164">a.</span></span> <span data-ttu-id="00c9a-165">Haga clic en **Create Manifest** (Crear manifiesto).</span><span class="sxs-lookup"><span data-stu-id="00c9a-165">Click **Create Manifest**.</span></span>

      ![Haga clic en el botón Crear manifiesto][ART04a]

   <span data-ttu-id="00c9a-167">b.</span><span class="sxs-lookup"><span data-stu-id="00c9a-167">b.</span></span> <span data-ttu-id="00c9a-168">Elija la ruta de acceso predeterminada del artefacto y haga clic en **OK** (Aceptar).</span><span class="sxs-lookup"><span data-stu-id="00c9a-168">Choose the default path for the artifact, and then click **OK**.</span></span>

      ![Especificar la ruta de acceso del artefacto][ART04b]

   <span data-ttu-id="00c9a-170">c.</span><span class="sxs-lookup"><span data-stu-id="00c9a-170">c.</span></span> <span data-ttu-id="00c9a-171">Haga clic en los puntos suspensivos (**...**) para buscar la clase principal.</span><span class="sxs-lookup"><span data-stu-id="00c9a-171">Click the ellipsis (**...**) to locate the main class.</span></span>

      ![Buscar la clase principal][ART04c]

   <span data-ttu-id="00c9a-173">d.</span><span class="sxs-lookup"><span data-stu-id="00c9a-173">d.</span></span> <span data-ttu-id="00c9a-174">Elija la clase principal y haga clic en **OK** (Aceptar).</span><span class="sxs-lookup"><span data-stu-id="00c9a-174">Choose your main class, and then click **OK**.</span></span>

      ![Especificar la clase principal][ART04d]

1. <span data-ttu-id="00c9a-176">Haga clic en **OK**.</span><span class="sxs-lookup"><span data-stu-id="00c9a-176">Click **OK**.</span></span>

   ![Cerrar el cuadro de diálogo Estructura del proyecto][ART05]

> [!NOTE]
> <span data-ttu-id="00c9a-178">Para más información sobre cómo crear artefactos en IntelliJ, consulte [Configuring Artifacts] (Configuración de artefactos) en el sitio web de JetBrains.</span><span class="sxs-lookup"><span data-stu-id="00c9a-178">For more information about creating artifacts in IntelliJ, see [Configuring Artifacts] on the JetBrains website.</span></span>
>

### <a name="build-the-artifact-for-deployment"></a><span data-ttu-id="00c9a-179">Compilar el artefacto para la implementación</span><span class="sxs-lookup"><span data-stu-id="00c9a-179">Build the artifact for deployment</span></span>

1. <span data-ttu-id="00c9a-180">Haga clic en **Build** (Compilar) y haga clic en **Artifacts** (Artefactos).</span><span class="sxs-lookup"><span data-stu-id="00c9a-180">Click **Build**, and then click **Artifacts**.</span></span>

   ![Comando Compilar artefactos][BU04]

1. <span data-ttu-id="00c9a-182">Cuando aparece el menú contextual **Build Artifact** (Compilar artefacto), haga clic en **Build** (Compilar).</span><span class="sxs-lookup"><span data-stu-id="00c9a-182">When the **Build Artifact** context menu appears, click **Build**.</span></span>

   ![Menú contextual Compilar artefacto][BU05]

<span data-ttu-id="00c9a-184">IntelliJ debe mostrar el artefacto completado para la aplicación Spring Boot en la ventana de herramientas del proyecto.</span><span class="sxs-lookup"><span data-stu-id="00c9a-184">IntelliJ should display the completed artifact for your Spring Boot app in the project tool window.</span></span>

   ![Artefacto creado][BU06]

## <a name="publish-your-web-app-to-azure-by-using-a-docker-container"></a><span data-ttu-id="00c9a-186">Publicación de su aplicación web en Azure mediante un contenedor de Docker</span><span class="sxs-lookup"><span data-stu-id="00c9a-186">Publish your web app to Azure by using a Docker container</span></span>

1. <span data-ttu-id="00c9a-187">Si no ha iniciado sesión en su cuenta de Azure, siga los pasos de [Instrucciones de inicio de sesión del kit de herramientas de Azure para IntelliJ][Azure Sign In for IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="00c9a-187">If you have not signed in to your Azure account, follow the steps in [Sign-in instructions for the Azure Toolkit for IntelliJ][Azure Sign In for IntelliJ].</span></span>

1. <span data-ttu-id="00c9a-188">En la ventana de la herramienta del explorador de proyectos, haga clic con el botón derecho en el proyecto y seleccione **Azure** > **Publish as Docker Container** (Publicar como contenedor de Docker).</span><span class="sxs-lookup"><span data-stu-id="00c9a-188">In the Project Explorer tool window, right-click the project, and then select **Azure** > **Publish as Docker Container**.</span></span>

   ![Comando Publish as Docker Container (Publicar como contenedor de Docker)][PU01]

1. <span data-ttu-id="00c9a-190">Cuando aparece el cuadro de diálogo **Deploy Docker Container on Azure** (Implementar un contenedor de Docker en Azure), se muestran todos los hosts de Docker existentes.</span><span class="sxs-lookup"><span data-stu-id="00c9a-190">When the **Deploy Docker Container on Azure** dialog box appears, any existing Docker hosts are displayed.</span></span> <span data-ttu-id="00c9a-191">Si decide implementar en un host existente, puede ir al paso 4.</span><span class="sxs-lookup"><span data-stu-id="00c9a-191">If you choose to deploy to an existing host, you can skip to step 4.</span></span> <span data-ttu-id="00c9a-192">En caso contrario, use los pasos siguientes para crear un host:</span><span class="sxs-lookup"><span data-stu-id="00c9a-192">Otherwise, use the following steps to create a host:</span></span>

   <span data-ttu-id="00c9a-193">a.</span><span class="sxs-lookup"><span data-stu-id="00c9a-193">a.</span></span> <span data-ttu-id="00c9a-194">Haga clic en el signo más verde (**+**).</span><span class="sxs-lookup"><span data-stu-id="00c9a-194">Click the green plus (**+**) symbol.</span></span>

      ![Agregar un nuevo host de Docker][PU02]

   <span data-ttu-id="00c9a-196">b.</span><span class="sxs-lookup"><span data-stu-id="00c9a-196">b.</span></span> <span data-ttu-id="00c9a-197">Cuando aparezca el cuadro de diálogo **Create Docker Host** (Crear host de Docker), puede aceptar los valores predeterminados o especificar cualquier configuración personalizada para el nuevo host de Docker.</span><span class="sxs-lookup"><span data-stu-id="00c9a-197">When the **Create Docker Host** dialog box appears, you can choose to accept the defaults, or you can specify any custom settings for your new Docker host.</span></span> <span data-ttu-id="00c9a-198">(Para obtener descripciones detalladas de las distintas configuraciones, vea [Publicación de una aplicación web como contenedor de Docker con el kit de herramientas de Azure para IntelliJ][Publish Container with Azure Toolkit]). Haga clic en **Siguiente** cuando haya especificado qué configuración usar.</span><span class="sxs-lookup"><span data-stu-id="00c9a-198">(For detailed descriptions of the various settings, see [Publish a web app as a Docker container by using the Azure Toolkit for IntelliJ][Publish Container with Azure Toolkit].) Click **Next** when you have specified which settings to use.</span></span>

      ![Especificar las opciones de host de Docker][PU03a]

   <span data-ttu-id="00c9a-200">c.</span><span class="sxs-lookup"><span data-stu-id="00c9a-200">c.</span></span> <span data-ttu-id="00c9a-201">Puede elegir usar las credenciales de inicio de sesión existentes desde Azure Key Vault, o puede escribir las nuevas credenciales de inicio de sesión de Docker.</span><span class="sxs-lookup"><span data-stu-id="00c9a-201">You can choose to use existing login credentials from an Azure key vault, or you can choose to enter new Docker login credentials.</span></span> <span data-ttu-id="00c9a-202">Haga clic en **Finalizar** cuando haya especificado las opciones.</span><span class="sxs-lookup"><span data-stu-id="00c9a-202">Click **Finish** when you have specified your options.</span></span>

      ![Especificar credenciales del host de Docker][PU03b]

1. <span data-ttu-id="00c9a-204">Seleccione el host de Docker y, después, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="00c9a-204">Select your Docker host, and then click **Next**.</span></span>

   ![Seleccionar el host de Docker que se va a usar][PU04]

1. <span data-ttu-id="00c9a-206">En la última página del cuadro de diálogo **Deploy Docker Container on Azure** (Implementar un contenedor de Docker en Azure), especifique las siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="00c9a-206">On the last page of the **Deploy Docker Container on Azure** dialog box, specify the following options:</span></span>

   <span data-ttu-id="00c9a-207">a.</span><span class="sxs-lookup"><span data-stu-id="00c9a-207">a.</span></span> <span data-ttu-id="00c9a-208">Puede elegir especificar un nombre personalizado para el contenedor que va a hospedar el contenedor de Docker, o puede aceptar el valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="00c9a-208">You can choose to specify a custom name for the container that will host your Docker container, or you can accept the default.</span></span>

   <span data-ttu-id="00c9a-209">b.</span><span class="sxs-lookup"><span data-stu-id="00c9a-209">b.</span></span> <span data-ttu-id="00c9a-210">Escriba los puertos TCP para el host de Docker mediante la sintaxis siguiente: *[puerto externo]*:*[puerto interno]*.</span><span class="sxs-lookup"><span data-stu-id="00c9a-210">Enter the TCP ports for your docker host by using the following syntax: *[external port]*:*[internal port]*.</span></span> <span data-ttu-id="00c9a-211">Por ejemplo, **80:8080** especifica un puerto externo de 80 y el puerto de Spring Boot interno predeterminado de 8080.</span><span class="sxs-lookup"><span data-stu-id="00c9a-211">For example, **80:8080** specifies an external port of 80 and the default internal Spring Boot port of 8080.</span></span>
   
      <span data-ttu-id="00c9a-212">Si ha personalizado el puerto interno, (por ejemplo, mediante la edición del archivo application.yml), debe especificar el número de puerto para que el enrutamiento correcto se produzca en Azure.</span><span class="sxs-lookup"><span data-stu-id="00c9a-212">If you have customized your internal port (for example, by editing the application.yml file), you need to specify the port number for the correct routing to occur in Azure.</span></span>

   <span data-ttu-id="00c9a-213">c.</span><span class="sxs-lookup"><span data-stu-id="00c9a-213">c.</span></span> <span data-ttu-id="00c9a-214">Después de configurar estas opciones, haga clic en **Finalizar**.</span><span class="sxs-lookup"><span data-stu-id="00c9a-214">After you have configured these options, click **Finish**.</span></span>

   ![Implementar un contenedor de Docker en Azure][PU05]

1. <span data-ttu-id="00c9a-216">Cuando el kit de herramientas de Azure ha terminado la publicación, el registro de actividad de Azure muestra **Publicado** en el estado.</span><span class="sxs-lookup"><span data-stu-id="00c9a-216">When the Azure Toolkit has finished publishing, the Azure Activity Log displays **Published** for the status.</span></span>

   ![Host de Docker correctamente implementado][PU06]

## <a name="next-steps"></a><span data-ttu-id="00c9a-218">pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="00c9a-218">Next steps</span></span>

<span data-ttu-id="00c9a-219">Para obtener información sobre métodos adicionales para crear aplicaciones Spring Boot con IntelliJ, vea [Creating Spring Boot Projects](https://www.jetbrains.com/help/idea/creating-spring-boot-projects.html) (Creación de proyectos Spring Boot) en el sitio web de JetBrains.</span><span class="sxs-lookup"><span data-stu-id="00c9a-219">To learn about additional methods for creating Spring Boot apps by using IntelliJ, see [Creating Spring Boot Projects](https://www.jetbrains.com/help/idea/creating-spring-boot-projects.html) on the JetBrains website.</span></span>

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

<!-- URL List -->

[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Sign In for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Configuring Artifacts]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html (Configuración de artefactos)
[Deploy Spring Boot on Linux in AKS]: /azure/container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux
[Docker]: https://www.docker.com/
[Publish Container with Azure Toolkit]: ./azure-toolkit-for-intellij-publish-as-docker-container.md
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[CL01]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL01.png
[CL02a]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL02a.png
[CL02b]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL02b.png
[CL03]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL03.png
[CL04]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL04.png
[CL05]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL05.png
[CL06]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL06.png
[CL07]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL07.png
[CL08]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL08.png
[CL09]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL09.png
[CL10]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL10.png
[CL11]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL11.png
[CL12]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL12.png
[CL13]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL13.png
[CL14]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL14.png

[ART01]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART01.png
[ART02]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART02.png
[ART03]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART03.png
[ART04a]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04a.png
[ART04b]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04b.png
[ART04c]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04c.png
[ART04d]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04d.png
[ART05]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART05.png

[BU01]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU01.png
[BU02]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU02.png
[BU03]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU03.png
[BU04]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU04.png
[BU05]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU05.png
[BU06]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU06.png

[PU01]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU01.png
[PU02]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU02.png
[PU03a]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU03a.png
[PU03b]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU03b.png
[PU04]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU04.png
[PU05]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU05.png
[PU06]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU06.png
