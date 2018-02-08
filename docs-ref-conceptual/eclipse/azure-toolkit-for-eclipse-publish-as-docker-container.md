---
title: "Publicación de un contenedor de Docker con el kit de herramientas de Azure para Eclipse"
description: "Aprenda a publicar una aplicación web en Microsoft Azure como un contenedor de Docker con el kit de herramientas de Azure para Eclipse."
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
ms.openlocfilehash: aec3682cc14204ca2b395d4b851db7bb68cb8728
ms.sourcegitcommit: 151aaa6ccc64d94ed67f03e846bab953bde15b4a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/03/2018
---
# <a name="publish-a-web-app-as-a-docker-container-by-using-the-azure-toolkit-for-eclipse"></a>Publicación de una aplicación web como contenedor de Docker con el kit de herramientas de Azure para Eclipse

Los contenedores de Docker son un método muy utilizado para implementar aplicaciones web. Usando contenedores de Docker, los desarrolladores pueden consolidar todos sus archivos de proyecto y dependencias en un único paquete para implementarlo en un servidor. El kit de herramientas de Azure para Eclipse simplifica este proceso para los desarrolladores de Java, ya que agrega características de *publicación como contenedor de Docker* para su implementación en Microsoft Azure. En este artículo se le guía por los pasos necesarios para publicar aplicaciones en Azure como contenedores de Docker.

> [!NOTE]
> Hay más información disponible sobre Docker en el [sitio web de Docker].
>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="publish-your-web-app-to-azure-by-using-a-docker-container"></a>Publicación de su aplicación web en Azure mediante un contenedor de Docker

1. Abra el proyecto de aplicación web en Eclipse.

1. Para iniciar el asistente **Publish as Docker Container** (Publicar como contenedor de Docker), realice una de las siguientes acciones:

   * En la vista **Navegador**, haga clic con el botón derecho en el proyecto y haga clic en **Azure** y en **Publish as Docker Container** (Publicar como contenedor de Docker).

      ![Vista de navegador del comando Publish as Docker Container (Publicar como contenedor de Docker)][PUB01]

   * En la barra de herramientas de Eclipse, haga clic en el botón **Publish** (Publicar) y en **Publish as Docker Container** (Publicar como contenedor de Docker).

      ![Barra de herramientas de Eclipse del comando Publish as Docker Container (Publicar como contenedor de Docker)][PUB02]
      
   Se abre el asistente **Deploy Docker Container on Azure** (Implementar contenedor de Docker en Azure).

   ![Asistente Deploy Docker Container on Azure (Implementar contenedor de Docker en Azure)][PUB03]

1. En la ventana **Type an image name, select the artifact's path and check a Docker host to be used** (Escriba un nombre de imagen, seleccione la ruta de acceso del artefacto y elija el host de Docker que se usará), haga lo siguiente:

   a. En el cuadro **Docker image name** (Nombre de imagen de Docker), escriba un nombre único para el host de Docker. (El asistente crea automáticamente un nombre, pero se puede modificar).

   b. En el área **Hosts**, se muestran todos los hosts de Docker que ya haya creado. Realice cualquiera de las siguientes acciones:

   * Si tiene un host de Docker existente, puede implementar la aplicación web en él.
   * Para crear un nuevo host de Docker, haga clic en **Agregar**.  
      
      Se abre el cuadro de diálogo **Create Docker Host** (Crear host de Docker).

   ![Asistente Deploy Docker Container on Azure (Implementar contenedor de Docker en Azure)][PUB04a]

1. En la ventana **Configure the new virtual machine** (Configurar la nueva máquina virtual), especifique las siguientes opciones de su host de Docker (el asistente genera automáticamente la mayor parte de las opciones, pero puede modificarla).

   a. **Name** (Nombre): escriba un nombre único para el host de Docker (no es lo mismo que el nombre de imagen de Docker que especificó antes).

   b. **Subscription** (Suscripción): escriba la suscripción de Azure que usa para el host.

   c. **Region** (Región): escriba la región geográfica donde se encuentra el host.

   d. En la pestaña **Host OS and Size** (Sistema operativo y tamaño del host): 
   * **Host OS** (Sistema operativo de host): escriba el sistema operativo de la máquina virtual que contiene el host.
   * **Size** (Tamaño): escriba el tamaño de la máquina virtual del host.

   e. En la pestaña **Resource Group** (Grupo de recursos): 
   * **New resource group** (Nuevo grupo de recursos): cree un grupo de recursos para el host.
   * **Existing resource group** (Grupo de recursos existente): especifique un grupo de recursos existente desde su cuenta de Azure.

   f. En la pestaña**Network** (Red): 
   * **New virtual network** (Nueva red virtual): cree una red virtual para el host.
   * **Existing virtual network** (Red virtual existente): especifique una red virtual existente desde su cuenta de Azure.

   g. Haga clic en la pestaña **Storage** (Almacenamiento): 
   * **New storage account** (Nueva cuenta de almacenamiento): cree una cuenta de almacenamiento para el host.
   * **Existing storage account** (Cuenta de almacenamiento existente): especifique una cuenta de almacenamiento existente desde su cuenta de Azure.

1. Haga clic en **Siguiente**.

1. En la ventana **Configure log in credentials and port settings** (Configurar credenciales de inicio de sesión y configuración de puerto), seleccione una de las siguientes opciones:

   * **Import credentials from Azure Key Vault** (Importar credenciales de Azure Key Vault): especifique un conjunto de credenciales previamente guardadas que están almacenadas en la suscripción de Azure. 

   >[!NOTE]
   >Una instancia de Azure Key Vault que se crea con una cuenta o entidad de servicio específica no es accesible automáticamente para otra cuenta o entidad de servicio que comparta la suscripción. Para permitir que otra cuenta o entidad de servicio use la instancia de Key Vault, debe usar Azure Portal para agregar la cuenta o entidad de servicio.
   >

   * **New log in credentials** (Nuevas credenciales de inicio de sesión): crea un conjunto de credenciales de inicio de sesión. Si selecciona esta opción, haga lo siguiente: 
    
      * En la pestaña **VM Credentials** (Credenciales de máquina virtual), elija una de las siguientes opciones para el inicio de sesión de máquina virtual del host de Docker: 

         * **Username** (Nombre de usuario): especifica el nombre de usuario de las credenciales inicio de sesión de la máquina virtual. 
         * **Password** (Contraseña) y **Confirm** (Confirmar): escriba la contraseña para las credenciales del inicio de sesión de la máquina virtual. 
         * **SSH**: especifique la configuración de Secure Shell (SSH) para el host de Docker. Puede elegir entre las siguientes opciones: 
            * **None** (Ninguna): especifica que la máquina virtual no permitirá conexiones SSH. 
            * **Auto-generate** (Generar automáticamente): crea automáticamente la configuración necesaria para la conexión mediante SSH. 
            * **Import from directory** (Importar desde directorio): especifica un directorio que contiene un conjunto de configuraciones de SSH previamente guardadas. El directorio debe contener los dos archivos siguientes: 
               * *id_rsa*: contiene la identificación de RSA de un usuario. 
               * *id_rsa.pub*: contiene la clave pública de RSA que se usa para la autenticación. 
        
         ![Create Docker Host (Crear host de Docker)][PUB05]

      * En la pestaña **Docker Daemon Credentials** (Credenciales demonio de Docker), especifique las siguientes opciones: 

         * **Docker Daemon port** (Puerto de demonio de Docker): especifica el puerto TCP único de su host de Docker. 
         * **Seguridad de TLS**: especifique la configuración de seguridad de la capa de transporte para el host de Docker. Puede elegir entre las siguientes opciones: 
            * **None** (Ninguna): especifica que su máquina virtual no permitirá conexiones TLS. 
            * **Auto-generate** (Generar automáticamente): crea automáticamente la configuración necesaria para la conexión mediante TLS. 
            * **Import from directory** (Importar desde directorio): especifica un directorio que contiene un conjunto de configuraciones de TLS previamente guardadas. Más concretamente, el directorio debe contener los seis archivos siguientes: 
               * *ca.pem* y *ca-key.pem*: contienen el certificado y la clave pública de la entidad de certificación de TLS. 
               * *cert.pem* y *key.pem*: contienen el certificado de cliente y la clave pública que se usarán para la autenticación TLS. 
               * *server.pem* y *server-key.pem*: contienen el certificado de servidor y la clave pública del host. 

         ![Create Docker Host (Crear host de Docker)][PUB06]

1. Después de haber escrito toda la información anterior, haga clic en **Finish** (Finalizar).

1. En el asistente **Deploy Docker Container on Azure** (Implementar contenedor de Docker en Azure), haga clic en **Next** (Siguiente).

   ![Asistente Deploy Docker Container on Azure (Implementar contenedor de Docker en Azure)][PUB07]

1. En la ventana **Configure the Docker container to be created** (Configurar el contenedor de Docker que se va a crear), realice lo siguiente:

   a. En el cuadro **Docker container name** (Nombre del contenedor de Docker), escriba un nombre único para el contenedor de Docker.

   b. Elija una de las siguientes imágenes de Docker: 

      * **Predefined Docker image** (Imagen de Docker predefinida): especifica una imagen de Docker preexistente de Azure. 

      >[!NOTE]
      >La lista de imágenes de Docker de este cuadro consta de varias imágenes para las que se ha configurado el kit de herramientas de Azure para aplicar revisiones, de modo que su artefacto se implementa automáticamente.
      >

      * **Custom Dockerfile** (Dockerfile personalizado): especifica un Dockerfile guardado antes desde el equipo local.

      >[!NOTE]
      >Esta es una característica más avanzada para desarrolladores que deseen implementar su propio Dockerfile. Sin embargo, es responsabilidad de los desarrolladores que usen esta opción asegurarse de que su Dockerfile se ha creado correctamente. El kit de herramientas de Azure no valida el contenido de un Dockerfile personalizado, por lo que la implementación puede dar error si el Dockerfile tiene problemas. Además, dado que el kit de herramientas de Azure espera que el Dockerfile personalizado contenga un artefacto de aplicación web, intenta abrir una conexión HTTP. Si los desarrolladores publican un tipo diferente de artefacto, podrían recibir errores inofensivos después de la implementación.
      >

   c. **Port settings** (Configuración de puerto): escriba el enlace de puerto TCP único para su contenedor de Docker.

      ![Ventana Configure the Docker container to be created (Configurar el contenedor de Docker que se va a crear)][PUB08]

1. Después de completar todos los pasos anteriores, haga clic en **Finish** (Finalizar).

El kit de herramientas de Azure comienza a implementar la aplicación web en Azure en un contenedor de Docker. 

## <a name="next-steps"></a>pasos siguientes

Para más recursos de Docker, consulte el [sitio web de Docker] oficial.

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<!-- URL List -->

[sitio web de Docker]: https://www.docker.com/

<!-- IMG List -->

[PUB01]: media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB01.png
[PUB02]: media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB02.png
[PUB03]: media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB03.png
[PUB04a]: media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04a.png
[PUB04b]: media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04b.png
[PUB04c]: media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04c.png
[PUB04d]: media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04d.png
[PUB05]: media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB05.png
[PUB06]: media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB06.png
[PUB07]: media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB07.png
[PUB08]: media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB08.png