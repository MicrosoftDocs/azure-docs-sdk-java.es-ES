---
title: "Publicación de una aplicación web como contenedor de Docker con el kit de herramientas de Azure para IntelliJ"
description: "Aprenda a publicar una aplicación web en Microsoft Azure como un contenedor de Docker con el kit de herramientas de Azure para IntelliJ."
services: 
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 
ms.author: robmcm
ms.date: 02/01/2018
ms.devlang: Java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: f92040b34b9897d9feea8d2ec5e8748e75fff7f7
ms.sourcegitcommit: 151aaa6ccc64d94ed67f03e846bab953bde15b4a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/03/2018
---
# <a name="publish-a-web-app-as-a-docker-container-by-using-the-azure-toolkit-for-intellij"></a>Publicación de una aplicación web como contenedor de Docker con el kit de herramientas de Azure para IntelliJ

Los contenedores de Docker son un método muy utilizado para implementar aplicaciones web. Usando contenedores de Docker, los desarrolladores pueden consolidar todos sus archivos de proyecto y dependencias en un único paquete para implementarlo en un servidor. El kit de herramientas de Azure para IntelliJ simplifica este proceso para los desarrolladores de Java, ya que agrega características de *publicación como contenedor de Docker* para su implementación en Microsoft Azure. En este artículo se le guía por los pasos necesarios para publicar aplicaciones en Azure como contenedores de Docker.

> [!NOTE]
>
> Hay más información disponible sobre Docker en el [sitio web de Docker].
>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="publish-your-web-app-to-azure-by-using-a-docker-container"></a>Publicación de su aplicación web en Azure mediante un contenedor de Docker

> [!NOTE]
> * Para publicar la aplicación web, debe crear un artefacto preparado para la implementación. Para aprender más, consulte la sección [Información adicional sobre la creación de artefactos](#artifacts).
>
> * Después de haber completado al asistente para implementar al menos una vez, la mayor parte de la configuración se utiliza como predeterminada cuando vuelva a ejecutar el asistente.
>

1. Abra el proyecto de aplicación web en IntelliJ.

2. Para iniciar el asistente **Publish as Docker Container** (Publicar como contenedor de Docker), realice una de las siguientes acciones:

   * En la ventana de la herramienta **Project** (Proyecto), haga clic con el botón derecho en el proyecto y haga clic en **Azure** y en **Publish as Docker Container** (Publicar como contenedor de Docker):

      ![Comando Publish as Docker Container (Publicar como contenedor de Docker)][PUB01]

   * En la barra de herramientas de IntelliJ, haga clic en el botón **Publish Group** (Publicar grupo) y en **Publish as Docker Container** (Publicar como contenedor de Docker):

      ![Comando Publish as Docker Container (Publicar como contenedor de Docker)][PUB02]  
    Se abre el asistente **Deploy Docker Container on Azure** (Implementar contenedor de Docker en Azure).

   ![Asistente Deploy Docker Container on Azure (Implementar contenedor de Docker en Azure)][PUB03]

3. En la ventana **Type an image name, select the artifact's path and check a Docker host to be used** (Escriba un nombre de imagen, seleccione la ruta de acceso del artefacto y elija el host de Docker que se usará), haga lo siguiente: 

   a. En el cuadro **Docker image name** (Nombre de imagen de Docker), escriba un nombre único para el host de Docker. (El asistente crea automáticamente un nombre, pero se puede modificar). 

   b. En el área **Hosts**, se muestran todos los hosts de Docker que ya haya creado. Realice cualquiera de las siguientes acciones: 
      * Si tiene un host de Docker existente, puede implementar la aplicación web en él.
      * Para crear un host de Docker, haga clic en el signo más de color verde (**+**).  
       Se abre el cuadro de diálogo **Create Docker Host** (Crear host de Docker). 

      ![Asistente Deploy Docker Container on Azure (Implementar contenedor de Docker en Azure)][PUB04a]

4. En la ventana **Configure the new virtual machine** (Configurar la nueva máquina virtual), proporcione la siguiente información acerca de su host de Docker. (El asistente genera automáticamente la mayor parte de la información, pero puede modificarla). 

   a. En el cuadro **Name** (Nombre), escriba un nombre único para el host de Docker. (No es lo mismo que el nombre de imagen de Docker que especificó antes). 
    
   b. En el cuadro **Subscription** (Suscripción), escriba la suscripción de Azure que usa para el host. 
      
   c. En el cuadro **Region** (Región), escriba la región geográfica donde se encuentra el host.
      
   d. En la pestaña **OS and Size** (Sistema operativo y tamaño), realice lo siguiente:      
      * **Host OS** (Sistema operativo de host): escriba el sistema operativo de la máquina virtual que contiene el host. 
      * **Size** (Tamaño): escriba el tamaño de la máquina virtual del host.   
       
   e. En la pestaña **Resource Group** (Grupo de recursos), seleccione una de las siguientes acciones:      
      * **New resource group** (Nuevo grupo de recursos): cree un grupo de recursos para el host.
      * **Existing resource group** (Grupo de recursos existente): especifique un grupo de recursos existente desde su cuenta de Azure. 
       
   f. En la pestaña **Network** (Red), seleccione una de las siguientes acciones:      
      * **New virtual network** (Nueva red virtual): cree una red virtual para el host.
      * **Existing virtual network** (Red virtual existente): especifique una red virtual existente desde su cuenta de Azure. 
       
   g. En la pestaña **Storage** (Almacenamiento), seleccione una de las siguientes acciones:      
      * **New storage account** (Nueva cuenta de almacenamiento): cree una cuenta de almacenamiento para el host.
      * **Existing storage account** (Cuenta de almacenamiento existente): especifique una cuenta de almacenamiento existente desde su cuenta de Azure.
       
5. Haga clic en **Next**.  
     Se abre la ventana **Configure log in credentials and port settings** (Configurar credenciales de inicio de sesión y configuración de puerto).

      ![Ventana Configure log in credentials and port settings (Configurar credenciales de inicio de sesión y configuración de puerto)][PUB05]

6. Seleccione una de las siguientes opciones:

      * **Import credentials from Azure Key Vault**  (Importar credenciales de Azure Key Vault): especifique un conjunto de credenciales previamente guardadas que están almacenadas en la suscripción de Azure.

          > [!NOTE]
          > Una instancia de Azure Key Vault que se crea con una cuenta o entidad de servicio específica no es accesible automáticamente para otra cuenta o entidad de servicio que comparta la suscripción. Para permitir que otra cuenta o entidad de servicio use la instancia de Key Vault, debe usar Azure Portal para agregar la cuenta o entidad de servicio.

      * **New log in credentials** (Nuevas credenciales de inicio de sesión): cree un conjunto de credenciales de inicio de sesión. Si selecciona esta opción, haga lo siguiente:

        a. En la pestaña **VM Credentials** (Credenciales de la máquina virtual), proporcione la siguiente información para las credenciales de inicio de sesión de máquina virtual del host de Docker: ***Username** (Nombre de usuario): escriba el nombre de usuario para las credenciales de inicio de sesión de máquina virtual.
             * **Password** (Contraseña) y **Confirm** (Confirmar): escriba la contraseña para las credenciales del inicio de sesión de la máquina virtual.
             * **SSH**: especifique la configuración de Secure Shell (SSH) para el host de Docker. Puede seleccionar una de las siguientes opciones: ***None** (Ninguna): especifica que la máquina virtual no permite conexiones SSH.
                * **Auto-generate** (Generar automáticamente): crea automáticamente la configuración necesaria para la conexión mediante SSH.
                * **Import from directory** (Importar desde directorio): permite especificar un directorio que contiene un conjunto de configuraciones de SSH previamente guardadas. El directorio debe contener los dos archivos siguientes:
                
                  * *id_rsa*: Contains the RSA identification for a user.
                  * *id_rsa.pub*: Contains the RSA public key that is used for authentication.
            
        b. En la pestaña **Docker Daemon Access** (Acceso de demonio de Docker), proporcione la siguiente información:

          ![Create Docker Host (Crear host de Docker)][PUB06]
    
             * **Docker Daemon port**: Enter the unique TCP port for your Docker host.
             * **TLS Security**: Enter the Transport Layer Security settings for your Docker host. You can choose from the following options:
                * **None**: Specifies that your virtual machine does not allow TLS connections.
                * **Auto-generate**: Automatically creates the requisite settings for connecting via TLS.
                * **Import from directory**: Specifies a directory that contains a set of previously saved TLS settings. The directory must contain the following six files: 
                   * *ca.pem* and *ca-key.pem*: Contain the certificate and public key for the TLS Certificate Authority.
                   * *cert.pem* and *key.pem*: Contain client certificate and public key which will be used for TLS authentication.
                   * *server.pem* and *server-key.pem*: Contain the client certificate and public key that is used for TLS authentication.

7. Después de haber escrito la información necesaria, haga clic en **Finish** (Finalizar).  
    Vuelve a aparecer el asistente **Deploy Docker Container on Azure** (Implementar contenedor de Docker en Azure).

   ![Asistente Deploy Docker Container on Azure (Implementar contenedor de Docker en Azure)][PUB07]

8. Haga clic en **Next**.  
    Se abre la ventana **Configure the Docker container to be created** (Configurar el contenedor de Docker que se va a crear).

   ![Ventana Configure the Docker container to be created (Configurar el contenedor de Docker que se va a crear)][PUB08]

9. En la ventana **Configure the Docker container to be created** (Configurar el contenedor de Docker que se va a crear), proporcione la siguiente información: 

   a. En el cuadro **Docker container name** (Nombre del contenedor de Docker), escriba un nombre único para el contenedor de Docker.

   b. Elija una de las siguientes imágenes de Docker: 

      * **Predefined Docker image** (Imagen de Docker predefinida): especifique una imagen de Docker preexistente de Azure. 

        > [!NOTE]
        > La lista de imágenes de Docker de este cuadro consta de varias imágenes para las que se ha configurado el kit de herramientas de Azure para aplicar revisiones, de modo que su artefacto se implementa automáticamente. 

      * **Custom Dockerfile** (Dockerfile personalizado): especifique un Dockerfile guardado antes desde el equipo local.

        > [!NOTE]
        > Esta es una característica más avanzada para desarrolladores que deseen implementar su propio Dockerfile. Sin embargo, es responsabilidad de los desarrolladores que usen esta opción asegurarse de que su Dockerfile se ha creado correctamente. Como el kit de herramientas de Azure no valida el contenido de un Dockerfile personalizado, la implementación puede dar error si el Dockerfile tiene problemas. Además, dado que el kit de herramientas de Azure espera que el Dockerfile personalizado contenga un artefacto de aplicación web, intenta abrir una conexión HTTP. Si los desarrolladores publican un tipo diferente de artefacto, podrían recibir errores inofensivos después de la implementación.

   c. En el cuadro **Port settings** (Configuración de puerto), escriba el enlace de puerto TCP único para su contenedor de Docker. 

10. Después de completar los pasos anteriores, haga clic en **Finish** (Finalizar). 

El kit de herramientas de Azure comienza a implementar la aplicación web en Azure en un contenedor de Docker. A menos que haya configurado IntelliJ para implementarse en segundo plano, aparece la barra de progreso **Deploying to Azure** (Implementando en Azure). 

![Barra de progreso de la implementación][PUB09]

<a name="artifacts"></a>
## <a name="additional-information-about-creating-artifacts"></a>Información adicional sobre la creación de artefactos

Para crear un artefacto preparado para la implementación, haga lo siguiente:

1. Abra el proyecto de aplicación web en IntelliJ.

2. Haga clic en **Archivo** y después en **Estructura del proyecto**.

   ![Comando Project Structure (Estructura del proyecto)][ART01]

3. Para agregar un artefacto, haga clic en el signo más de color verde (**+**) y en **Web Application: Archive** (Aplicación web: archivo).

   ![Comando Web Application: Archive (Aplicación web: archivo)][ART02]

4. En el cuadro **Name** (Nombre), escriba un nombre para el artefacto (no incluya la extensión *.war*) y haga clic en **Aceptar**.

   ![Cuadro Name (Nombre) del artefacto][ART03]

Para más información sobre cómo crear artefactos en IntelliJ, consulte [Configuring Artifacts] (Configuración de artefactos) en el sitio web de JetBrains.

## <a name="next-steps"></a>pasos siguientes

Para más recursos de Docker, consulte el [sitio web de Docker] oficial.

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
