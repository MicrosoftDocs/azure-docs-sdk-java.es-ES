---
title: "Ejecución de una aplicación web Hola mundo como contenedor de Linux con el kit de herramientas de Azure para IntelliJ"
description: "Aprenda a crear una aplicación web de Hola mundo básica en un contenedor de Linux y publicarla en Azure mediante el kit de herramientas de Azure para IntelliJ."
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 10/19/2017
ms.author: robmcm
ms.openlocfilehash: c3c6339bb5a8415854253701d0ac340d42587509
ms.sourcegitcommit: 7f8538e41c833deb69c300ad3431a431136a1f3e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/24/2017
---
# <a name="run-a-hello-world-web-app-in-a-linux-container-by-using-the-azure-toolkit-for-intellij"></a>Ejecución de una aplicación web Hola mundo como contenedor de Linux con el kit de herramientas de Azure para IntelliJ

Los contenedores de [cliente de Docker] son un método muy utilizado para implementar aplicaciones web. Usando contenedores de Docker, los desarrolladores pueden consolidar todos sus archivos de proyecto y dependencias en un único paquete para implementarlo en un servidor. El kit de herramientas de Azure para IntelliJ simplifica este proceso para los desarrolladores de Java, ya que agrega características para implementar contenedores en Microsoft Azure.

En este artículo se muestran los pasos necesarios para crear una aplicación web de Hola mundo básica y publicar la aplicación web en un contenedor de Linux en Azure mediante el kit de herramientas de Azure para IntelliJ.

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]
* Un [cliente de Docker].

> [!NOTE]
>
> Para completar los pasos de este tutorial, debe configurar [cliente de Docker] para que exponga el demonio en el puerto 2375 sin TLS. Puede configurar esta opción al instalar Docker o mediante el menú de configuración de Docker.
>
> ![Menú de configuración de Docker][docker-settings-menu]
>

## <a name="create-a-new-web-app-project"></a>Creación de un proyecto de aplicación web nuevo

1. Inicie IntelliJ e inicie sesión en su cuenta de Azure siguiendo los pasos del artículo [Instrucciones de inicio de sesión del kit de herramientas de Azure para IntelliJ].

1. Haga clic en el menú **File** (Archivo), en **New** (Nuevo) y en **Project** (Proyecto).
   
   ![Creación de un proyecto][file-new-project]

1. En el cuadro de diálogo **New Project** (Nuevo proyecto), seleccione **Maven**, **maven-archetype-webapp** y haga clic en **Next** (Siguiente).
   
   ![Elección de una aplicación web de arquetipo Maven][maven-archetype-webapp]
   
1. Especifique **GroupId** y **ArtifactId** para la aplicación web y haga clic en **Next** (Siguiente).
   
   ![Especificación de GroupId y ArtifactId][groupid-and-artifactid]

1. Personalice la configuración de Maven o acepte los valores predeterminados y haga clic en **Next** (Siguiente).
   
   ![Especificación de la configuración de Maven][maven-options]

1. Especifique el nombre y la ubicación del proyecto, y haga clic en **Finish**(Finalizar).
   
   ![Especificación del nombre del proyecto][project-name]

## <a name="create-an-azure-container-registry-to-use-as-a-private-docker-registry"></a>Creación de una instancia de Azure Container Registry para usarla como un registro de Docker privado

Los siguientes pasos le muestran cómo usar Azure Portal para crear una instancia de Azure Container Registry.

> [!NOTE]
>
> Si quiere usar la CLI de Azure en lugar de Azure Portal, siga los pasos descritos en [Creación de un registro de contenedor privado de Docker con la CLI de Azure 2.0][Create Docker Registry using Azure CLI].
>

1. Vaya a [Azure Portal] e inicie sesión.

   Una vez que haya iniciado sesión en su cuenta en Azure Portal, puede seguir los pasos descritos en el artículo [Creación de un registro de contenedor privado de Docker con la CLI de Azure], que se vuelven a explicar en los pasos siguientes para mayor comodidad.

1. Haga clic en el icono de menú **+ Nuevo**, en **Contenedores** y en **Azure Container Registry**.
   
   ![Crear una instancia de Azure Container Registry][AR01]

1. Cuando aparezca la página de información de la plantilla de Azure Container Registry, haga clic en **Crear**. 

   ![Crear una instancia de Azure Container Registry][AR02]

1. Cuando aparezca la página **Crear Registro de contenedor**, escriba su **Nombre del Registro** y **Grupo de recursos**, elija **Habilitar** para el **Usuario administrador** y haga clic en **Crear**.

   ![Configurar Azure Container Registry][AR03]

1. Una vez que se haya creado el Registro de contenedor, desplácese hasta él en Azure Portal y haga clic en **Claves de acceso**. Tome nota del nombre de usuario y la contraseña para usarlos en los pasos siguientes.

   ![Claves de acceso de Azure Container Registry][AR04]

## <a name="deploy-your-web-app-in-a-docker-container"></a>Implementación de una aplicación web en un contenedor de Docker

1. Haga clic con el botón derecho en el proyecto en Project Explorer, elija **Azure** y haga clic en **Add Docker Support** (Agregar compatibilidad con Docker).

   Se creará automáticamente un archivo de Docker con una configuración predeterminada.

   ![Agregue compatibilidad con Docker][add-docker-support]

1. Después de agregar compatibilidad con Docker, haga clic con el botón derecho en el proyecto en Project Explorer, elija **Azure** y haga clic en **Run on Web App (Linux)** [Ejecutar en aplicación web (Linux)].

   ![Ejecutar en aplicación web (Linux)][run-on-web-app-linux]

1. En el cuadro de diálogo **Run on Web App (Linux)** [Ejecutar en aplicación web (Linux)] que aparece, rellene la información necesaria:

   * **Name** (Nombre): especifica el nombre descriptivo que se muestra en el kit de herramientas de Azure. 

   * **Server URL** (Dirección URL del servidor): especifica la dirección URL para el registro de contenedor de la sección anterior de este artículo; se suele utilizar la sintaxis siguiente: "*registro*.azurecr.io". 

   * **Username** (Nombre de usuario) y **Password** (Contraseña): especifica las claves de acceso para el registro de contenedor de la sección anterior de este artículo. 

   * **Image and tag** (Imagen y etiqueta): especifica el nombre de imagen de contenedor; se suele utilizar la sintaxis siguiente: "*registro*.azurecr.io/*nombreDeAplicación*:latest", donde: 
      * *registro* es el registro de contenedor de la sección anterior de este artículo 
      * *nombreDeAplicación* es el nombre de la aplicación web 

   * **Use Existing Web App** (Usar la aplicación web existente) o **Create New Web App** (Crear aplicación web nueva): especifica si se implementa el contenedor en una aplicación web existente o se crea una aplicación web nueva. 

   * **Resource Group** (Grupo de recursos): especifica si va a utilizar un grupo de recursos existente o va a crear uno nuevo. 

   * **App Service Plan** (Plan de App Service): especifica si va a utilizar un grupo de recursos existente o va a crear uno nuevo. 

1. Cuando haya terminado de configurar los valores enumerados anteriormente, haga clic en **Run** (Ejecutar).

   ![Crear aplicación web][create-web-app]

1. Después de publicar la aplicación web, la configuración se guardará como valor predeterminado y podrá ejecutar la aplicación en Azure al hacer clic en el icono de flecha verde de la barra de herramientas. Para modificar esta configuración, haga clic en el menú desplegable de la aplicación web y, luego, en **Edit Configurations** (Editar configuraciones).

   ![Menú Editar configuración][edit-configuration-menu]

1. Cuando aparezca el cuadro de diálogo **Run/Debug Configurations** (Ejecutar/Depurar configuraciones), podrá modificar cualquiera de los valores predeterminados y hacer clic en **OK** (Aceptar).

   ![Cuadro de diálogo Editar configuración][edit-configuration-dialog]

## <a name="next-steps"></a>Pasos siguientes

Para ver más recursos de Docker, vaya al [sitio web oficial de Docker][cliente de Docker].

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<!-- URL List -->

[Azure Portal]: https://portal.azure.com/
[Creación de un registro de contenedor privado de Docker con la CLI de Azure]: /azure/container-registry/container-registry-get-started-portal
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Create Docker Registry using Azure CLI]: /azure/container-registry/container-registry-get-started-azure-cli

[cliente de Docker]: https://www.docker.com/
[Configuring artifacts]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html

<!-- IMG List -->

[AR01]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/AR01.png
[AR02]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/AR02.png
[AR03]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/AR03.png
[AR04]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/AR04.png

[docker-settings-menu]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/docker-settings-menu.png
[file-new-project]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/file-new-project.png
[maven-archetype-webapp]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/maven-archetype-webapp.png
[groupid-and-artifactid]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/groupid-and-artifactid.png
[maven-options]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/maven-options.png
[project-name]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/project-name.png
[add-docker-support]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/add-docker-support.png
[run-on-web-app-linux]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/run-on-web-app-linux.png
[create-web-app]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/create-web-app.png
[edit-configuration-menu]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/edit-configuration-menu.png
[edit-configuration-dialog]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/edit-configuration-dialog.png
[successfully-deployed]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/successfully-deployed.png
