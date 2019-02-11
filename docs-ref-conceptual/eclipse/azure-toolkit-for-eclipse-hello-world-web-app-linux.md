---
title: Implementación de una aplicación web Hola mundo en un contenedor Linux en la nube con Azure Toolkit for Eclipse
description: Ejecución de una aplicación web Hola mundo en un contenedor Linux y su implementación en la nube con Azure Toolkit for Eclipse.
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 12/20/2018
ms.devlang: Java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.openlocfilehash: 799f21a282956f9a88aa35743157fc1292197569
ms.sourcegitcommit: 54e7f077d694a5b1dd7fa6c8870b7d476af9829c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/02/2019
ms.locfileid: "55649251"
---
# <a name="deploy-a-hello-world-web-app-to-a-linux-container-in-the-cloud-using-the-azure-toolkit-for-eclipse"></a>Implementación de una aplicación web Hola mundo en un contenedor Linux en la nube mediante Azure Toolkit for Eclipse

Los contenedores de [Docker] son un método muy utilizado para implementar aplicaciones web. Usando contenedores de Docker, los desarrolladores pueden consolidar todos sus archivos de proyecto y dependencias en un único paquete para implementarlo en un servidor. Azure Toolkit for Eclipse simplifica este proceso para los desarrolladores de Java, ya que agrega características para implementar contenedores en Microsoft Azure.

En este artículo se muestran los pasos necesarios para crear una aplicación web de Hola mundo básica y publicar la aplicación web en un contenedor de Linux en Azure mediante Azure Toolkit for Eclipse.

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]
* Un cliente de [Docker].

> [!NOTE]
>
> Para completar los pasos de este tutorial, debe configurar [Docker] para que exponga el demonio en el puerto 2375 sin TLS. Puede configurar esta opción al instalar Docker o mediante el menú de configuración de Docker.
>
> ![Menú de configuración de Docker][docker-settings-menu]
>

## <a name="create-a-new-web-app-project"></a>Creación de un proyecto de aplicación web nuevo

1. Inicie Eclipse e inicie sesión en su cuenta de Azure siguiendo los pasos del artículo [Instrucciones de inicio de sesión de Azure Toolkit for Eclipse](https://docs.microsoft.com/java/azure/eclipse/azure-toolkit-for-eclipse-sign-in-instructions).

1. Haga clic en **File** (Archivo), haga clic en **New** (Nuevo) y luego haga clic en **Dynamic Web Project** (Proyecto web dinámico).
   
   ![Creación de un proyecto][file-new-project]

1. En el cuadro de diálogo **New Dynamic Web Project** (Nuevo proyecto web dinámico), especifique un nombre de proyecto y una ubicación, y haga clic en **Finish** (Finalizar).
   
   ![Especificación del nombre del proyecto][project-name]

## <a name="create-an-azure-container-registry-to-use-as-a-private-docker-registry"></a>Creación de una instancia de Azure Container Registry para usarla como un registro de Docker privado

Los siguientes pasos le muestran cómo usar Azure Portal para crear una instancia de Azure Container Registry.

> [!NOTE]
>
> Si quiere usar la CLI de Azure en lugar de Azure Portal, siga los pasos descritos en [Creación de un registro de contenedor privado de Docker con la CLI de Azure 2.0][Create Docker Registry using Azure CLI].
>

1. Vaya a [Azure Portal] e inicie sesión.

   Una vez que haya iniciado sesión en su cuenta en Azure Portal, puede seguir los pasos descritos en el artículo [Creación de un registro de contenedor privado de Docker con Azure Portal], que se vuelven a explicar en los pasos siguientes para mayor comodidad.

1. Haga clic en el icono de menú **+ Crear un recurso**, en **Contenedores** y en **Container Registry**.
   
   ![Crear una instancia de Azure Container Registry][create-container-registry-01]

1. Cuando aparezca la página **Crear Registro de contenedor**, escriba su **Nombre del Registro** y **Grupo de recursos**, elija **Habilitar** para el **Usuario administrador** y haga clic en **Crear**.

   ![Configurar Azure Container Registry][create-container-registry-02]

## <a name="deploy-your-web-app-in-a-docker-container"></a>Implementación de una aplicación web en un contenedor de Docker

1. Haga clic con el botón derecho en el proyecto en Project Explorer, elija **Azure** y haga clic en **Add Docker Support** (Agregar compatibilidad con Docker).

   Se creará automáticamente un archivo de Docker con una configuración predeterminada.

   ![Agregue compatibilidad con Docker][add-docker-support]

1. Después de agregar compatibilidad con Docker, haga clic con el botón derecho en el proyecto en el explorador de proyectos, elija **Azure** y haga clic en **Publish on Web App for Containers** (Publicar en Web App for Containers).

   ![Publicar en Web App for Containers][run-on-web-app-for-containers]

1. En el cuadro de diálogo **Run on Web App for Containers** (Ejecutar en Web App for Containers) que aparece, rellene la información necesaria:

   * **Docker File** (Archivo de Docker): especifica la ruta de acceso al archivo de Docker que se creó cuando se agregó compatibilidad con Docker al proyecto. 

   * **Container Registry** (Registro de contenedor): En el menú desplegable, elija el registro de contenedor que creó en la sección anterior de este artículo. Los campos **Server URL** (URL del servidor), **Username** (Nombre de usuario) y **Password** (Contraseña) se rellenarán automáticamente.

   * **Image and tag** (Imagen y etiqueta): especifica el nombre de la imagen de contenedor; se suele utilizar la sintaxis siguiente: "*registro*.azurecr.io/*nombreDeAplicación*:latest", donde: 
      * *registro* es el registro de contenedor de la sección anterior de este artículo 
      * *nombreDeAplicación* es el nombre de la aplicación web 

   * **Web App for Containers**: elija **Use Existing** (Usar existente) o **Create New** (Crear nueva) para especificar si se implementa el contenedor en una aplicación web existente o se crea una aplicación web nueva.  Con el **nombre de aplicación** que especifique se creará la dirección URL de la aplicación web; por ejemplo: *wingtiptoys.azurewebsites.net*.

   * **Resource Group** (Grupo de recursos): especifica si va a utilizar un grupo de recursos existente o va a crear uno nuevo. 

   * **App Service Plan** (Plan de App Service): especifica si va a utilizar un plan de App Service existente o va a crear uno nuevo. 

   ![Ejecutar en Web App for Containers][run-on-web-app-linux]

1. Cuando haya terminado de configurar los valores enumerados anteriormente, haga clic en **OK** (Aceptar) para publicar la aplicación web en Azure.

1. Una vez publicada la aplicación web, puede ir a la dirección URL que especificó anteriormente para ella. Por ejemplo: *wingtiptoys.azurewebsites.net*.

   ![Ir a la aplicación web][browsing-to-web-app]

## <a name="next-steps"></a>Pasos siguientes

Para ver más recursos de Docker, vaya al [sitio web oficial de Docker][Docker].

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<!-- URL List -->

[Azure Portal]: https://portal.azure.com/
[Creación de un registro de contenedor privado de Docker con Azure Portal]: /azure/container-registry/container-registry-get-started-portal
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Create Docker Registry using Azure CLI]: /azure/container-registry/container-registry-get-started-azure-cli

[Docker]: https://www.docker.com/
[Configuring artifacts]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html

<!-- IMG List -->

[add-docker-support]: media/azure-toolkit-for-eclipse-hello-world-web-app-linux/add-docker-support.png
[browsing-to-web-app]:  media/azure-toolkit-for-eclipse-hello-world-web-app-linux/browsing-to-web-app.png
[create-container-registry-01]: media/azure-toolkit-for-eclipse-hello-world-web-app-linux/create-container-registry-01.png
[create-container-registry-02]: media/azure-toolkit-for-eclipse-hello-world-web-app-linux/create-container-registry-02.png
[docker-settings-menu]: media/azure-toolkit-for-eclipse-hello-world-web-app-linux/docker-settings-menu.png
[file-new-project]: media/azure-toolkit-for-eclipse-hello-world-web-app-linux/file-new-project.png
[project-name]: media/azure-toolkit-for-eclipse-hello-world-web-app-linux/project-name.png
[run-on-web-app-for-containers]: media/azure-toolkit-for-eclipse-hello-world-web-app-linux/run-on-web-app-for-containers.png
[run-on-web-app-linux]: media/azure-toolkit-for-eclipse-hello-world-web-app-linux/run-on-web-app-linux.png
