---
title: Publicación de una aplicación web como contenedor de Docker con el kit de herramientas de Azure para IntelliJ
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
ms.openlocfilehash: 64cefc1ace5d0377dea25fdbdc83d8dada31ddf7
ms.sourcegitcommit: ed130145f9e5c2d803791d96bb118023175e644a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/28/2018
---
# <a name="publish-a-web-app-as-a-docker-container-by-using-the-azure-toolkit-for-intellij"></a><span data-ttu-id="3db7b-103">Publicación de una aplicación web como contenedor de Docker con el kit de herramientas de Azure para IntelliJ</span><span class="sxs-lookup"><span data-stu-id="3db7b-103">Publish a web app as a Docker container by using the Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="3db7b-104">Los contenedores de Docker son un método muy utilizado para implementar aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="3db7b-104">Docker containers are a widely used method for deploying web applications.</span></span> <span data-ttu-id="3db7b-105">Usando contenedores de Docker, los desarrolladores pueden consolidar todos sus archivos de proyecto y dependencias en un único paquete para implementarlo en un servidor.</span><span class="sxs-lookup"><span data-stu-id="3db7b-105">By using Docker containers, developers can consolidate all their project files and dependencies into a single package for deployment to a server.</span></span> <span data-ttu-id="3db7b-106">El kit de herramientas de Azure para IntelliJ simplifica este proceso para los desarrolladores de Java, ya que agrega características de *publicación como contenedor de Docker* para su implementación en Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="3db7b-106">The Azure Toolkit for IntelliJ simplifies this process for Java developers by adding *Publish as Docker Container* features for deployment to Microsoft Azure.</span></span> <span data-ttu-id="3db7b-107">En este artículo se le guía por los pasos necesarios para publicar aplicaciones en Azure como contenedores de Docker.</span><span class="sxs-lookup"><span data-stu-id="3db7b-107">This article walks you through the steps required to publish your applications to Azure as Docker containers.</span></span>

> [!NOTE]
>
> <span data-ttu-id="3db7b-108">Hay más información disponible sobre Docker en el [sitio web de Docker].</span><span class="sxs-lookup"><span data-stu-id="3db7b-108">More information about Docker is available on the [Docker website].</span></span>
>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="publish-your-web-app-to-azure-by-using-a-docker-container"></a><span data-ttu-id="3db7b-109">Publicación de su aplicación web en Azure mediante un contenedor de Docker</span><span class="sxs-lookup"><span data-stu-id="3db7b-109">Publish your web app to Azure by using a Docker container</span></span>

> [!NOTE]
> * <span data-ttu-id="3db7b-110">Para publicar la aplicación web, debe crear un artefacto preparado para la implementación.</span><span class="sxs-lookup"><span data-stu-id="3db7b-110">To publish your web app, you must create a deployment-ready artifact.</span></span> <span data-ttu-id="3db7b-111">Para aprender más, consulte la sección [Información adicional sobre la creación de artefactos](#artifacts).</span><span class="sxs-lookup"><span data-stu-id="3db7b-111">To learn more, see the [Additional information about creating artifacts](#artifacts) section.</span></span>
>
> * <span data-ttu-id="3db7b-112">Después de haber completado al asistente para implementar al menos una vez, la mayor parte de la configuración se utiliza como predeterminada cuando vuelva a ejecutar el asistente.</span><span class="sxs-lookup"><span data-stu-id="3db7b-112">After you have completed the deployment wizard at least once, most of your settings are used as defaults when you run the wizard again.</span></span>
>

1. <span data-ttu-id="3db7b-113">Abra el proyecto de aplicación web en IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="3db7b-113">Open your web app project in IntelliJ.</span></span>

2. <span data-ttu-id="3db7b-114">Para iniciar el asistente **Publish as Docker Container** (Publicar como contenedor de Docker), realice una de las siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="3db7b-114">To start the **Publish as Docker Container** wizard, do either of the following:</span></span>

   * <span data-ttu-id="3db7b-115">En la ventana de la herramienta **Project** (Proyecto), haga clic con el botón derecho en el proyecto y haga clic en **Azure** y en **Publish as Docker Container** (Publicar como contenedor de Docker):</span><span class="sxs-lookup"><span data-stu-id="3db7b-115">In the **Project** tool window, right-click your project, click **Azure**, and then click **Publish as Docker Container**:</span></span>

      ![Comando Publish as Docker Container (Publicar como contenedor de Docker)][PUB01]

   * <span data-ttu-id="3db7b-117">En la barra de herramientas de IntelliJ, haga clic en el botón **Publish Group** (Publicar grupo) y en **Publish as Docker Container** (Publicar como contenedor de Docker):</span><span class="sxs-lookup"><span data-stu-id="3db7b-117">On the IntelliJ toolbar, click the **Publish Group** button, and then click **Publish as Docker Container**:</span></span>

      <span data-ttu-id="3db7b-118">![Comando Publish as Docker Container (Publicar como contenedor de Docker)][PUB02]</span><span class="sxs-lookup"><span data-stu-id="3db7b-118">![The Publish as Docker Container command][PUB02]</span></span>  
    <span data-ttu-id="3db7b-119">Se abre el asistente **Deploy Docker Container on Azure** (Implementar contenedor de Docker en Azure).</span><span class="sxs-lookup"><span data-stu-id="3db7b-119">The **Deploy Docker Container on Azure** wizard opens.</span></span>

   ![Asistente Deploy Docker Container on Azure (Implementar contenedor de Docker en Azure)][PUB03]

3. <span data-ttu-id="3db7b-121">En la ventana **Type an image name, select the artifact's path and check a Docker host to be used** (Escriba un nombre de imagen, seleccione la ruta de acceso del artefacto y elija el host de Docker que se usará), haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="3db7b-121">In the **Type an image name, select the artifact's path and check a Docker host to be used** window, do the following:</span></span> 

   <span data-ttu-id="3db7b-122">a.</span><span class="sxs-lookup"><span data-stu-id="3db7b-122">a.</span></span> <span data-ttu-id="3db7b-123">En el cuadro **Docker image name** (Nombre de imagen de Docker), escriba un nombre único para el host de Docker.</span><span class="sxs-lookup"><span data-stu-id="3db7b-123">In the **Docker image name** box, enter a unique name for your Docker host.</span></span> <span data-ttu-id="3db7b-124">(El asistente crea automáticamente un nombre, pero se puede modificar).</span><span class="sxs-lookup"><span data-stu-id="3db7b-124">(The wizard automatically creates a name, but you can modify it.)</span></span> 

   <span data-ttu-id="3db7b-125">b.</span><span class="sxs-lookup"><span data-stu-id="3db7b-125">b.</span></span> <span data-ttu-id="3db7b-126">En el área **Hosts**, se muestran todos los hosts de Docker que ya haya creado.</span><span class="sxs-lookup"><span data-stu-id="3db7b-126">The **Hosts** area displays any Docker hosts that you have already created.</span></span> <span data-ttu-id="3db7b-127">Realice cualquiera de las siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="3db7b-127">Do either of the following:</span></span> 
      * <span data-ttu-id="3db7b-128">Si tiene un host de Docker existente, puede implementar la aplicación web en él.</span><span class="sxs-lookup"><span data-stu-id="3db7b-128">If you have an existing Docker host, you can deploy your web app to it.</span></span>
      * <span data-ttu-id="3db7b-129">Para crear un host de Docker, haga clic en el signo más de color verde (**+**).</span><span class="sxs-lookup"><span data-stu-id="3db7b-129">To create a Docker host, click the green plus sign (**+**).</span></span>  
       <span data-ttu-id="3db7b-130">Se abre el cuadro de diálogo **Create Docker Host** (Crear host de Docker).</span><span class="sxs-lookup"><span data-stu-id="3db7b-130">The **Create Docker Host** dialog box opens.</span></span> 

      ![Asistente Deploy Docker Container on Azure (Implementar contenedor de Docker en Azure)][PUB04a]

4. <span data-ttu-id="3db7b-132">En la ventana **Configure the new virtual machine** (Configurar la nueva máquina virtual), proporcione la siguiente información acerca de su host de Docker.</span><span class="sxs-lookup"><span data-stu-id="3db7b-132">In the **Configure the new virtual machine** window, provide the following information about your Docker host.</span></span> <span data-ttu-id="3db7b-133">(El asistente genera automáticamente la mayor parte de la información, pero puede modificarla).</span><span class="sxs-lookup"><span data-stu-id="3db7b-133">(The wizard automatically generates most of the information for you, but you can modify any of them.)</span></span> 

   <span data-ttu-id="3db7b-134">a.</span><span class="sxs-lookup"><span data-stu-id="3db7b-134">a.</span></span> <span data-ttu-id="3db7b-135">En el cuadro **Name** (Nombre), escriba un nombre único para el host de Docker.</span><span class="sxs-lookup"><span data-stu-id="3db7b-135">In the **Name** box, enter a unique name for the Docker host.</span></span> <span data-ttu-id="3db7b-136">(No es lo mismo que el nombre de imagen de Docker que especificó antes).</span><span class="sxs-lookup"><span data-stu-id="3db7b-136">(It is not the same as the Docker image name that you specified earlier.)</span></span> 
    
   <span data-ttu-id="3db7b-137">b.</span><span class="sxs-lookup"><span data-stu-id="3db7b-137">b.</span></span> <span data-ttu-id="3db7b-138">En el cuadro **Subscription** (Suscripción), escriba la suscripción de Azure que usa para el host.</span><span class="sxs-lookup"><span data-stu-id="3db7b-138">In the **Subscription** box, enter the Azure subscription that you use for your host.</span></span> 
      
   <span data-ttu-id="3db7b-139">c.</span><span class="sxs-lookup"><span data-stu-id="3db7b-139">c.</span></span> <span data-ttu-id="3db7b-140">En el cuadro **Region** (Región), escriba la región geográfica donde se encuentra el host.</span><span class="sxs-lookup"><span data-stu-id="3db7b-140">In the **Region** box, enter the geographical region where your host is located.</span></span>
      
   <span data-ttu-id="3db7b-141">d.</span><span class="sxs-lookup"><span data-stu-id="3db7b-141">d.</span></span> <span data-ttu-id="3db7b-142">En la pestaña **OS and Size** (Sistema operativo y tamaño), realice lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="3db7b-142">On the **OS and Size** tab, do the following:</span></span>      
      * <span data-ttu-id="3db7b-143">**Host OS** (Sistema operativo de host): escriba el sistema operativo de la máquina virtual que contiene el host.</span><span class="sxs-lookup"><span data-stu-id="3db7b-143">**Host OS**: Enter the operating system for the virtual machine that contains your host.</span></span> 
      * <span data-ttu-id="3db7b-144">**Size** (Tamaño): escriba el tamaño de la máquina virtual del host.</span><span class="sxs-lookup"><span data-stu-id="3db7b-144">**Size**: Enter the virtual-machine size for your host.</span></span>   
       
   <span data-ttu-id="3db7b-145">e.</span><span class="sxs-lookup"><span data-stu-id="3db7b-145">e.</span></span> <span data-ttu-id="3db7b-146">En la pestaña **Resource Group** (Grupo de recursos), seleccione una de las siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="3db7b-146">On the **Resource Group** tab, select either of the following:</span></span>      
      * <span data-ttu-id="3db7b-147">**New resource group** (Nuevo grupo de recursos): cree un grupo de recursos para el host.</span><span class="sxs-lookup"><span data-stu-id="3db7b-147">**New resource group**: Create a resource group for your host.</span></span>
      * <span data-ttu-id="3db7b-148">**Existing resource group** (Grupo de recursos existente): especifique un grupo de recursos existente desde su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="3db7b-148">**Existing resource group**: Specify an existing resource group from your Azure account.</span></span> 
       
   <span data-ttu-id="3db7b-149">f.</span><span class="sxs-lookup"><span data-stu-id="3db7b-149">f.</span></span> <span data-ttu-id="3db7b-150">En la pestaña **Network** (Red), seleccione una de las siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="3db7b-150">On the **Network** tab, select either of the following:</span></span>      
      * <span data-ttu-id="3db7b-151">**New virtual network** (Nueva red virtual): cree una red virtual para el host.</span><span class="sxs-lookup"><span data-stu-id="3db7b-151">**New virtual network**: Create a virtual network for your host.</span></span>
      * <span data-ttu-id="3db7b-152">**Existing virtual network** (Red virtual existente): especifique una red virtual existente desde su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="3db7b-152">**Existing virtual network**: Specify an existing virtual network from your Azure account.</span></span> 
       
   <span data-ttu-id="3db7b-153">g.</span><span class="sxs-lookup"><span data-stu-id="3db7b-153">g.</span></span> <span data-ttu-id="3db7b-154">En la pestaña **Storage** (Almacenamiento), seleccione una de las siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="3db7b-154">On the **Storage** tab, select either of the following:</span></span>      
      * <span data-ttu-id="3db7b-155">**New storage account** (Nueva cuenta de almacenamiento): cree una cuenta de almacenamiento para el host.</span><span class="sxs-lookup"><span data-stu-id="3db7b-155">**New storage account**: Create a storage account for your host.</span></span>
      * <span data-ttu-id="3db7b-156">**Existing storage account** (Cuenta de almacenamiento existente): especifique una cuenta de almacenamiento existente desde su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="3db7b-156">**Existing storage account**: Specify an existing storage account from your Azure account.</span></span>
       
5. <span data-ttu-id="3db7b-157">Haga clic en **Next**.</span><span class="sxs-lookup"><span data-stu-id="3db7b-157">Click **Next**.</span></span>  
     <span data-ttu-id="3db7b-158">Se abre la ventana **Configure log in credentials and port settings** (Configurar credenciales de inicio de sesión y configuración de puerto).</span><span class="sxs-lookup"><span data-stu-id="3db7b-158">The **Configure log in credentials and port settings** window opens.</span></span>

      ![Ventana Configure log in credentials and port settings (Configurar credenciales de inicio de sesión y configuración de puerto)][PUB05]

6. <span data-ttu-id="3db7b-160">Seleccione una de las siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="3db7b-160">Select one of the following options:</span></span>

      * <span data-ttu-id="3db7b-161">**Import credentials from Azure Key Vault**  (Importar credenciales de Azure Key Vault): especifique un conjunto de credenciales previamente guardadas que están almacenadas en la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="3db7b-161">**Import credentials from Azure Key Vault**: Specify a previously saved set of credentials that are stored in your Azure subscription.</span></span>

          > [!NOTE]
          > <span data-ttu-id="3db7b-162">Una instancia de Azure Key Vault que se crea con una cuenta o entidad de servicio específica no es accesible automáticamente para otra cuenta o entidad de servicio que comparta la suscripción.</span><span class="sxs-lookup"><span data-stu-id="3db7b-162">An Azure key vault that's created with a specific account or service principal is not automatically accessible by another account or service principal that shares the subscription.</span></span> <span data-ttu-id="3db7b-163">Para permitir que otra cuenta o entidad de servicio use la instancia de Key Vault, debe usar Azure Portal para agregar la cuenta o entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="3db7b-163">To allow another account or service principal to use the key vault, you must use the Azure portal to add the account or service principal.</span></span>

      * <span data-ttu-id="3db7b-164">**New log in credentials** (Nuevas credenciales de inicio de sesión): cree un conjunto de credenciales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="3db7b-164">**New log in credentials**: Create a new set of login credentials.</span></span> <span data-ttu-id="3db7b-165">Si selecciona esta opción, haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="3db7b-165">If you select this option, do the following:</span></span>

    <span data-ttu-id="3db7b-166">a.</span><span class="sxs-lookup"><span data-stu-id="3db7b-166">a.</span></span> <span data-ttu-id="3db7b-167">En la pestaña **VM Credentials** (Credenciales de máquina virtual), indique la siguiente información para las credenciales de inicio de sesión de la máquina virtual del host de Docker:</span><span class="sxs-lookup"><span data-stu-id="3db7b-167">On the **VM Credentials** tab, provide the following information for the virtual-machine login credentials of your Docker host:</span></span>

    * <span data-ttu-id="3db7b-168">**Username** (Nombre de usuario): especifique el nombre de usuario para las credenciales de inicio de sesión de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="3db7b-168">**Username**: Enter the username for your virtual-machine login credentials.</span></span>

    * <span data-ttu-id="3db7b-169">**Password** (Contraseña) y **Confirm** (Confirmar): escriba la contraseña para las credenciales de inicio de sesión de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="3db7b-169">**Password** and **Confirm**: Enter the password for your virtual-machine login credentials.</span></span>

    * <span data-ttu-id="3db7b-170">**SSH**: especifique la configuración de Secure Shell (SSH) para el host de Docker.</span><span class="sxs-lookup"><span data-stu-id="3db7b-170">**SSH**: Enter the Secure Shell (SSH) settings for your Docker host.</span></span> <span data-ttu-id="3db7b-171">Puede seleccionar una de las siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="3db7b-171">You can select one of the following options:</span></span>

        * <span data-ttu-id="3db7b-172">**None** (Ninguna): especifica que la máquina virtual no permite conexiones SSH.</span><span class="sxs-lookup"><span data-stu-id="3db7b-172">**None**: Specifies that your virtual machine does not allow SSH connections.</span></span>

        * <span data-ttu-id="3db7b-173">**Auto-generate** (Generar automáticamente): crea automáticamente la configuración necesaria para la conexión mediante SSH.</span><span class="sxs-lookup"><span data-stu-id="3db7b-173">**Auto-generate**: Automatically creates the requisite settings for connecting via SSH.</span></span>

        * <span data-ttu-id="3db7b-174">**Import from directory** (Importar desde directorio): permite especificar un directorio que contiene un conjunto de configuraciones de SSH previamente guardadas.</span><span class="sxs-lookup"><span data-stu-id="3db7b-174">**Import from directory**: Allows you to specify a directory that contains a set of previously saved SSH settings.</span></span> <span data-ttu-id="3db7b-175">El directorio debe contener los dos archivos siguientes:</span><span class="sxs-lookup"><span data-stu-id="3db7b-175">The directory must contain the following two files:</span></span>

            * <span data-ttu-id="3db7b-176">*id_rsa*: contiene la identificación de RSA de un usuario.</span><span class="sxs-lookup"><span data-stu-id="3db7b-176">*id_rsa*: Contains the RSA identification for a user.</span></span>

            * <span data-ttu-id="3db7b-177">*id_rsa.pub*: contiene la clave pública de RSA que se usa para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="3db7b-177">*id_rsa.pub*: Contains the RSA public key that is used for authentication.</span></span>

    <span data-ttu-id="3db7b-178">b.</span><span class="sxs-lookup"><span data-stu-id="3db7b-178">b.</span></span> <span data-ttu-id="3db7b-179">En la pestaña **Docker Daemon Access** (Acceso de demonio de Docker), proporcione la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="3db7b-179">On the **Docker Daemon Access** tab, provide the following information:</span></span>

    ![Create Docker Host (Crear host de Docker)][PUB06]
    
    * <span data-ttu-id="3db7b-181">**Docker Daemon port** (Puerto de demonio de Docker): especifica el puerto TCP único de su host de Docker.</span><span class="sxs-lookup"><span data-stu-id="3db7b-181">**Docker Daemon port**: Enter the unique TCP port for your Docker host.</span></span>
    
    * <span data-ttu-id="3db7b-182">**Seguridad de TLS**: especifique la configuración de seguridad de la capa de transporte para el host de Docker.</span><span class="sxs-lookup"><span data-stu-id="3db7b-182">**TLS Security**: Enter the Transport Layer Security settings for your Docker host.</span></span> <span data-ttu-id="3db7b-183">Puede elegir entre las siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="3db7b-183">You can choose from the following options:</span></span>
    
        * <span data-ttu-id="3db7b-184">**None** (Ninguna): especifica que su máquina virtual no permite conexiones TLS.</span><span class="sxs-lookup"><span data-stu-id="3db7b-184">**None**: Specifies that your virtual machine does not allow TLS connections.</span></span>
        
        * <span data-ttu-id="3db7b-185">**Auto-generate** (Generar automáticamente): crea automáticamente la configuración necesaria para la conexión mediante TLS.</span><span class="sxs-lookup"><span data-stu-id="3db7b-185">**Auto-generate**: Automatically creates the requisite settings for connecting via TLS.</span></span>
        
        * <span data-ttu-id="3db7b-186">**Import from directory** (Importar desde directorio): especifica un directorio que contiene un conjunto de configuraciones de TLS previamente guardadas.</span><span class="sxs-lookup"><span data-stu-id="3db7b-186">**Import from directory**: Specifies a directory that contains a set of previously saved TLS settings.</span></span> <span data-ttu-id="3db7b-187">El directorio debe contener los seis archivos siguientes:</span><span class="sxs-lookup"><span data-stu-id="3db7b-187">The directory must contain the following six files:</span></span>
        
            * <span data-ttu-id="3db7b-188">*ca.pem* y *ca-key.pem*: contienen el certificado y la clave pública de la entidad de certificación de TLS.</span><span class="sxs-lookup"><span data-stu-id="3db7b-188">*ca.pem* and *ca-key.pem*: Contain the certificate and public key for the TLS Certificate Authority.</span></span>
            
            * <span data-ttu-id="3db7b-189">*cert.pem* y *key.pem*: contienen el certificado de cliente y la clave pública que se usarán para la autenticación TLS.</span><span class="sxs-lookup"><span data-stu-id="3db7b-189">*cert.pem* and *key.pem*: Contain client certificate and public key which will be used for TLS authentication.</span></span>
            
            * <span data-ttu-id="3db7b-190">*server.pem* y *server-key.pem*: contienen el certificado de cliente y la clave pública que se usarán para la autenticación TLS.</span><span class="sxs-lookup"><span data-stu-id="3db7b-190">*server.pem* and *server-key.pem*: Contain the client certificate and public key that is used for TLS authentication.</span></span>

7. <span data-ttu-id="3db7b-191">Después de haber escrito la información necesaria, haga clic en **Finish** (Finalizar).</span><span class="sxs-lookup"><span data-stu-id="3db7b-191">After you have entered the required information, click **Finish**.</span></span>  
    <span data-ttu-id="3db7b-192">Vuelve a aparecer el asistente **Deploy Docker Container on Azure** (Implementar contenedor de Docker en Azure).</span><span class="sxs-lookup"><span data-stu-id="3db7b-192">The **Deploy Docker Container on Azure** wizard reappears.</span></span>

   ![Asistente Deploy Docker Container on Azure (Implementar contenedor de Docker en Azure)][PUB07]

8. <span data-ttu-id="3db7b-194">Haga clic en **Next**.</span><span class="sxs-lookup"><span data-stu-id="3db7b-194">Click **Next**.</span></span>  
    <span data-ttu-id="3db7b-195">Se abre la ventana **Configure the Docker container to be created** (Configurar el contenedor de Docker que se va a crear).</span><span class="sxs-lookup"><span data-stu-id="3db7b-195">The **Configure the Docker container to be created** window opens.</span></span>

   ![Ventana Configure the Docker container to be created (Configurar el contenedor de Docker que se va a crear)][PUB08]

9. <span data-ttu-id="3db7b-197">En la ventana **Configure the Docker container to be created** (Configurar el contenedor de Docker que se va a crear), proporcione la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="3db7b-197">In the **Configure the Docker container to be created** window, provide the following information:</span></span> 

   <span data-ttu-id="3db7b-198">a.</span><span class="sxs-lookup"><span data-stu-id="3db7b-198">a.</span></span> <span data-ttu-id="3db7b-199">En el cuadro **Docker container name** (Nombre del contenedor de Docker), escriba un nombre único para el contenedor de Docker.</span><span class="sxs-lookup"><span data-stu-id="3db7b-199">In the **Docker container name** box, enter a unique name for your Docker container.</span></span>

   <span data-ttu-id="3db7b-200">b.</span><span class="sxs-lookup"><span data-stu-id="3db7b-200">b.</span></span> <span data-ttu-id="3db7b-201">Elija una de las siguientes imágenes de Docker:</span><span class="sxs-lookup"><span data-stu-id="3db7b-201">Choose one of the following Docker images:</span></span> 

      * <span data-ttu-id="3db7b-202">**Predefined Docker image** (Imagen de Docker predefinida): especifique una imagen de Docker preexistente de Azure.</span><span class="sxs-lookup"><span data-stu-id="3db7b-202">**Predefined Docker image**: Specify a pre-existing Docker image from Azure.</span></span> 

        > [!NOTE]
        > <span data-ttu-id="3db7b-203">La lista de imágenes de Docker de este cuadro consta de varias imágenes para las que se ha configurado el kit de herramientas de Azure para aplicar revisiones, de modo que su artefacto se implementa automáticamente.</span><span class="sxs-lookup"><span data-stu-id="3db7b-203">The list of Docker images in this box consists of several images that the Azure Toolkit has been configured to patch so that your artifact is deployed automatically.</span></span> 

      * <span data-ttu-id="3db7b-204">**Custom Dockerfile** (Dockerfile personalizado): especifique un Dockerfile guardado antes desde el equipo local.</span><span class="sxs-lookup"><span data-stu-id="3db7b-204">**Custom Dockerfile**: Specify a previously saved Dockerfile from your local computer.</span></span>

        > [!NOTE]
        > <span data-ttu-id="3db7b-205">Esta es una característica más avanzada para desarrolladores que deseen implementar su propio Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="3db7b-205">This is a more advanced feature for developers who want to deploy their own Dockerfile.</span></span> <span data-ttu-id="3db7b-206">Sin embargo, es responsabilidad de los desarrolladores que usen esta opción asegurarse de que su Dockerfile se ha creado correctamente.</span><span class="sxs-lookup"><span data-stu-id="3db7b-206">However, it is up to developers who use this option to ensure that their Dockerfile is built correctly.</span></span> <span data-ttu-id="3db7b-207">Como el kit de herramientas de Azure no valida el contenido de un Dockerfile personalizado, la implementación puede dar error si el Dockerfile tiene problemas.</span><span class="sxs-lookup"><span data-stu-id="3db7b-207">Because the Azure Toolkit does not validate the content in a custom Dockerfile, the deployment might fail if the Dockerfile has issues.</span></span> <span data-ttu-id="3db7b-208">Además, dado que el kit de herramientas de Azure espera que el Dockerfile personalizado contenga un artefacto de aplicación web, intenta abrir una conexión HTTP.</span><span class="sxs-lookup"><span data-stu-id="3db7b-208">In addition, because the Azure Toolkit expects the custom Dockerfile to contain a web app artifact, it attempts to open an HTTP connection.</span></span> <span data-ttu-id="3db7b-209">Si los desarrolladores publican un tipo diferente de artefacto, podrían recibir errores inofensivos después de la implementación.</span><span class="sxs-lookup"><span data-stu-id="3db7b-209">If developers publish a different type of artifact, they might receive innocuous errors after deployment.</span></span>

   <span data-ttu-id="3db7b-210">c.</span><span class="sxs-lookup"><span data-stu-id="3db7b-210">c.</span></span> <span data-ttu-id="3db7b-211">En el cuadro **Port settings** (Configuración de puerto), escriba el enlace de puerto TCP único para su contenedor de Docker.</span><span class="sxs-lookup"><span data-stu-id="3db7b-211">In the **Port settings** box, enter the unique TCP port binding for your Docker container.</span></span> 

10. <span data-ttu-id="3db7b-212">Después de completar los pasos anteriores, haga clic en **Finish** (Finalizar).</span><span class="sxs-lookup"><span data-stu-id="3db7b-212">After you have completed the preceding steps, click **Finish**.</span></span> 

<span data-ttu-id="3db7b-213">El kit de herramientas de Azure comienza a implementar la aplicación web en Azure en un contenedor de Docker.</span><span class="sxs-lookup"><span data-stu-id="3db7b-213">The Azure Toolkit begins deploying your web app to Azure in a Docker container.</span></span> <span data-ttu-id="3db7b-214">A menos que haya configurado IntelliJ para implementarse en segundo plano, aparece la barra de progreso **Deploying to Azure** (Implementando en Azure).</span><span class="sxs-lookup"><span data-stu-id="3db7b-214">Unless you have configured IntelliJ to be deployed in the background, a **Deploying to Azure** progress bar appears.</span></span> 

![Barra de progreso de la implementación][PUB09]

<a name="artifacts"></a>
## <a name="additional-information-about-creating-artifacts"></a><span data-ttu-id="3db7b-216">Información adicional sobre la creación de artefactos</span><span class="sxs-lookup"><span data-stu-id="3db7b-216">Additional information about creating artifacts</span></span>

<span data-ttu-id="3db7b-217">Para crear un artefacto preparado para la implementación, haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="3db7b-217">To create a deployment-ready artifact, do the following:</span></span>

1. <span data-ttu-id="3db7b-218">Abra el proyecto de aplicación web en IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="3db7b-218">Open your web app project in IntelliJ.</span></span>

2. <span data-ttu-id="3db7b-219">Haga clic en **Archivo** y después en **Estructura del proyecto**.</span><span class="sxs-lookup"><span data-stu-id="3db7b-219">Click **File**, and then click **Project Structure**.</span></span>

   ![Comando Project Structure (Estructura del proyecto)][ART01]

3. <span data-ttu-id="3db7b-221">Para agregar un artefacto, haga clic en el signo más de color verde (**+**) y en **Web Application: Archive** (Aplicación web: archivo).</span><span class="sxs-lookup"><span data-stu-id="3db7b-221">To add an artifact, click the green plus sign (**+**), and then click **Web Application: Archive**.</span></span>

   ![Comando Web Application: Archive (Aplicación web: archivo)][ART02]

4. <span data-ttu-id="3db7b-223">En el cuadro **Name** (Nombre), escriba un nombre para el artefacto (no incluya la extensión *.war*) y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="3db7b-223">In the **Name** box, enter a name for your artifact (do not include the *.war* extension), and then click **OK**.</span></span>

   ![Cuadro Name (Nombre) del artefacto][ART03]

<span data-ttu-id="3db7b-225">Para más información sobre cómo crear artefactos en IntelliJ, consulte [Configuring Artifacts] (Configuración de artefactos) en el sitio web de JetBrains.</span><span class="sxs-lookup"><span data-stu-id="3db7b-225">For more information about creating artifacts in IntelliJ, see [Configuring artifacts] on the JetBrains website.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3db7b-226">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3db7b-226">Next steps</span></span>

<span data-ttu-id="3db7b-227">Para más recursos de Docker, consulte el [sitio web de Docker] oficial.</span><span class="sxs-lookup"><span data-stu-id="3db7b-227">For additional resources for Docker, see the official [Docker website].</span></span>

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

<!-- URL List -->

[sitio web de Docker]: https://www.docker.com/
[Configuring Artifacts]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html (Configuración de artefactos)

<!-- IMG List -->

[PUB01]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB01.png
[PUB02]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB02.png
[PUB03]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB03.png
[PUB04a]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04a.png
[PUB04b]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04b.png
[PUB04c]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04c.png
[PUB04d]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04d.png
[PUB05]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB05.png
[PUB06]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB06.png
[PUB07]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB07.png
[PUB08]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB08.png
[PUB09]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB09.png

[ART01]: media/azure-toolkit-for-intellij-publish-as-docker-container/ART01.png
[ART02]: media/azure-toolkit-for-intellij-publish-as-docker-container/ART02.png
[ART03]: media/azure-toolkit-for-intellij-publish-as-docker-container/ART03.png
