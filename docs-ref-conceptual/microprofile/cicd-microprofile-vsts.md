---
title: CI/CD para aplicaciones de MicroProfile con Azure DevOps
description: Obtenga información sobre cómo configurar un ciclo de versión de CI/CD para implementar una aplicación de MicroProfile en una instancia de Azure Web App for Containers con Azure DevOps
services: Azure DevOps
documentationcenter: MicroProfile
author: ruyakubu
manager: brunoborges
editor: ruyakubu
ms.assetid: ''
ms.author: ruyakubu
ms.date: 09/14/2018
ms.devlang: Java
ms.service: Azure DevOps
ms.tgt_pltfrm: multiple
ms.topic: tutorial
ms.workload: web
ms.openlocfilehash: 818e37291fa47f99cb161c63a86062bddbf6248c
ms.sourcegitcommit: 4d52e47073fb0b3ac40a2689daea186bad5b1ef5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/23/2018
ms.locfileid: "49799941"
---
# <a name="cicd-for-microprofile-applications-using-azure-devops"></a>CI/CD para aplicaciones de MicroProfile con Azure DevOps

Este tutorial muestra cómo pueden los desarrolladores de Java EE configurar fácilmente un ciclo de versión de CI/CD para implementar sus aplicaciones de [MicroProfile](http://microprofile.io) en Azure Web App for Containers con Azure DevOps (anteriormente conocido como VSTS).  En este ejemplo, vamos a usar una aplicación de MicroProfile que usa [Payara Micro](https://www.payara.fish/payara_micro) como imagen base.   

```Dockerfile
FROM payara/micro:5.182
COPY target/*.war $DEPLOY_DIR/ROOT.war
EXPOSE 8080
```
El proceso de inclusión en contenedores de Azure DevOps se inicia con la creación de una imagen de Docker y la inserción de la imagen de contenedor en Azure Container Registry.  A continuación, se completará con una canalización de versión de Azure DevOps para implementar la imagen de contenedor en una aplicación web.

## <a name="prerequisites"></a>Requisitos previos
- Copie y guarde la dirección URL de Git desde [Github](https://github.com/Azure-Samples/microprofile-hello-azure).
- Regístrese o inicie sesión en su cuenta de [Azure DevOps](https://dev.azure.com).
- Cree un nuevo [proyecto de Azure DevOps](https://docs.microsoft.com/en-us/vsts/organizations/projects/create-project?view=vsts&tabs=new-nav) y use la dirección URL de Git anterior para **importar un repositorio**.
- Cree una instancia de [Azure Container Registry](https://azure.microsoft.com/en-us/services/container-registry) (ACR).
- Cree una instancia de Azure Web App for Containers.
  > [!NOTE]
  >
  > Seleccione "Inicio rápido" en la configuración del contenedor al aprovisionar la instancia de la aplicación web.


## <a name="create-a-build-definition"></a>Creación de una definición de compilación

La definición de compilación de Azure DevOps ejecuta automáticamente todas las tareas de la compilación cada vez que hay una confirmación en el código fuente de la aplicación de Java EE.  En este ejemplo, Azure DevOps usa Maven para compilar el proyecto de MicroProfile de Java.

1. Haga clic en la pestaña "Compilación y versión" en la parte superior de la página del proyecto de Azure DevOps.  A continuación, seleccione el vínculo **Compilaciones**. 

<img src="media/VSTS/Buid-and-Release1.png">

2. Haga clic en el botón **Nueva canalización** y, a continuación, en **Continuar** para comenzar a definir las tareas de compilación.
3. Seleccione "Maven" en la lista de plantillas y haga clic en el botón **Aplicar** para compilar el proyecto de Java.
4. Use el menú desplegable del campo Grupo de agentes para seleccionar la opción **Hosted Linux Preview**.
   > [!NOTE]
   >
   > Esto informa a Azure DevOps sobre qué servidor de compilación se va a utilizar.  Puede usar un servidor de compilación personalizado privado.

5. Para configurar la compilación para la integración continua, seleccione la pestaña **Desencadenadores** y active la casilla de verificación **Habilitar la integración continua**.  

<img src="media/VSTS/Build-Triggers2.png"> 

6. Seleccione la pestaña <strong>Tareas</strong> para volver a la página principal de la canalización de compilación.
7. Use el menú desplegable <strong>Guardar y poner en cola&amp;</strong> y seleccione la opción <strong>Guardar</strong>.


## <a name="create-a-docker-build-image"></a>Creación de una imagen de compilación de Docker

En esta tarea, Azure DevOps usa un Dockerfile con una imagen base de Payara Micro para crear una imagen de Docker.  

1. Seleccione la pestaña **Tareas** para volver a la página principal de la canalización de compilación.
2. Haga clic en el icono **+** para agregar la nueva tarea a la definición de compilación.

<img src="media/VSTS/Tasks-add4.png">

3. Seleccione &quot;Docker&quot; en la lista de plantillas y haga clic en el botón <strong>Agregar</strong>.
4. Escriba un nombre descriptivo para el campo <strong>Nombre para mostrar</strong>.
5. Compruebe que está seleccionado <strong>Azure Container Registry</strong> en el menú desplegable <strong>Tipo de registro de contenedor</strong>.
&gt; [!NOTE]
&gt; &gt; Si usa Docker Hub u otro registro, seleccione &quot;Registro de contenedor&quot; en su lugar.  A continuación, haga clic en el botón &quot;+ Nuevo&quot; para proporcionar las credenciales y la información de conexión. A continuación, vaya a la sección Comandos para continuar.

6. Utilice el menú desplegable **Suscripción de Azure** para seleccionar el identificador de suscripción de Azure.  A continuación, haga clic en el botón **Autorizar**
7. En el menú desplegable **Registro de contenedor de Azure**, seleccione el nombre del registro que creó en Azure.
8. Compruebe que está seleccionada la opción **Compilar** en el menú desplegable **Comando**.
9. Para el campo **Dockerfile**, haga clic en el icono de la ruta de acceso junto al cuadro de texto para seleccionar el archivo Dockerfile del proyecto de Github.  A continuación, haga clic en el botón **Aceptar**.

<img src="media/VSTS/Dockerfile5.png">

10. En **Nombre de la imagen**, active la casilla de verificación **Incluir última etiqueta**. 
11. Use el menú desplegable **Guardar y poner en cola** para seleccionar la opción **Guardar**.

## <a name="push-docker-image-to-acr"></a>Inserción de una imagen de Docker en ACR

En esta tarea, Azure DevOps insertará la imagen de Docker en la instancia de Azure Container Registry.  Se usará para ejecutar la aplicación de MicroProfile API como una aplicación web de Java en contenedores.

1. Puesto que estamos usando Docker en Azure DevOps, repita los pasos 1 a 7 anteriores de la sección **Creación de una imagen de compilación de Docker** para crear una nueva plantilla de Docker.
2. Seleccione **Insertar** en el menú desplegable **Comando**.
3. Haga clic en la pestaña **Guardar y poner en cola** y, a continuación, seleccione la opción **Guardar y poner en cola**.
4. Compruebe que está seleccionado **Hosted Linux Preview** en Grupo de agentes en la ventana emergente.  A continuación, haga clic en el botón **Guardar y poner en cola**.
5. Haga clic en el número de compilación para comprobar que la canalización de compilación para el proyecto de Java ha finalizado correctamente.

<img src="media/VSTS/Build-Number6.png">


## <a name="create-a-release-definition-for-a-java-app"></a>Creación de una definición de versión para una aplicación de Java

La canalización de versión de Azure DevOps desencadena automáticamente la implementación de los artefactos de compilación en un entorno de destino, como por ejemplo Azure, tan pronto como el proceso de compilación finaliza correctamente.   La canalización de versión se puede crear para los entornos de desarrollo, prueba, ensayo o producción.

1. Haga clic en la pestaña "Compilación y versión" en la parte superior de la página del proyecto de Azure DevOps.  A continuación, seleccione el vínculo **Versiones**.

<img src="media/VSTS/Release-new-pipeline7.png">

2. Haga clic en el botón &quot;Nueva canalización**
3. Seleccione <strong>Implementar una aplicación de Java en Azure App Service</strong> en la lista de plantillas y, a continuación, haga clic en el botón <strong>Aplicar</strong>.

<img src="media/VSTS/deploy-java-template8.png">

4. Establezca un <strong>Nombre de fase</strong> (por ejemplo, desarrollo, prueba, ensayo o producción).  A continuación, haga clic en el botón <strong>X</strong> para cerrar la ventana emergente.
5. Haga clic en el botón <strong>+ Agregar</strong> en la sección Artefactos.  Esto vinculará los artefactos de la definición de compilación con esta definición de versión.<br/>6. Use el menú desplegable <strong>Origen (canalización de compilación)</strong> para seleccionar la definición de compilación. A continuación, haga clic en el botón <strong>Agregar</strong> para continuar.

<img src="media/VSTS/add-artifact9.png">

7. Haga clic en la pestaña <strong>Tareas</strong> de la canalización.  A continuación, seleccione el nombre de fase.

<img src="media/VSTS/release-stage10.png">

8. Utilice el menú desplegable **Suscripción de Azure** para seleccionar el identificador de suscripción de Azure.
9. Seleccione **Aplicación Linux** en el menú desplegable **Tipo de aplicación**
10. Seleccione el nombre de la instancia de Web App for Containers que creó anteriormente en el menú desplegable **Nombre de App Service**.
11. Escriba el nombre de la instancia de Azure Container Registry en el campo **Registro o espacio de nombres**.  Por ejemplo, **myregistry.azure.io**
12. Escriba el nombre del registro en el campo **Repositorio**.
13. Haga clic en **Implementar Azure App Service**.  Escriba la etiqueta de la imagen de contenedor en el cuadro de texto **Etiqueta**. 
14. Haga clic en **Ejecutar en el agente**.  Seleccione **Hosted Linux Preview** en el menú desplegable Grupo de agentes. 

## <a name="setup-environment-variables"></a>Configuración de las variables de entorno

1. Haga clic en la pestaña **Variables**.  A continuación, haga clic en el botón **+ Agregar** para definir las variables de entorno.
2. Agregue el nombre de variable y sus valores para la dirección URL del registro de contenedor, el nombre de usuario y la contraseña.   Por seguridad, haga clic en el icono de candado para mantener oculto el valor de la contraseña.

Por ejemplo: 
- registry.password
- registry.url
- registry.username

<img src="media/VSTS/environment-variables12.png">

3. Haga clic en la pestaña **Tareas** para volver a la página principal de la definición de canalización de versión
4. Haga clic en **Implementar Azure App Service**. 
5. Expanda la sección **Configuración y opciones de la aplicación** y, a continuación, haga clic en la ruta de navegación del campo **Configuración de la aplicación** para agregar las variables de entorno para la conexión al registro de contenedor durante la implementación.
6. Haga clic en el botón ** + Agregar** para definir la siguiente configuración de la aplicación y asignar las variables de entorno.
7. DOCKER_REGISTRY_SERVER_PASSWORD = $(registry.password)
8. DOCKER_REGISTRY_SERVER_URL = $(registry.url)
9. DOCKER_REGISTRY_SERVER_USERNAME = $(registry.username)

<img src="media/VSTS/environment-variables14.png">

7. Haga clic en el botón <strong>Aceptar</strong> para continuar.

## <a name="setup-continious-deployment--deploy-java-application"></a>Configuración de la implementación continua e implementación de la aplicación de Java

1. Para habilitar la implementación continua, haga clic en la pestaña **Canalizaciones**.
2. En la sección Artefactos, haga clic en el icono de rayo que aparece.  A continuación, establezca el **Desencadenador de implementación continua** en habilitado.

<img src="media/VSTS/release-enable-CD.png">

3. Haga clic en el botón <strong>Guardar</strong> y, a continuación, en el botón <strong>Aceptar</strong>. 
4. Haga clic en el menú desplegable <strong>+ Versión</strong> y, a continuación, seleccione el vínculo <strong>Crear una versión</strong>.
5. Use el menú desplegable <strong>Fases para un cambio de desencadenador de automático a manual</strong> para seleccionar la casilla de verificación del nombre de fase.
6. Haga clic en el botón <strong>Crear</strong> para continuar.
7. Haga clic en el número de versión.  A continuación, mantenga el cursor del mouse sobre el nombre de fase y haga clic en el botón <strong>Implementar</strong>.
8. A continuación, haga clic en el botón <strong>Implementar</strong> en la ventana emergente para iniciar el proceso de implementación en Azure.


## <a name="test-the-java-web-application"></a>Prueba de la aplicación web de Java
1. Ejecute la dirección URL de la aplicación web en el explorador web:  
   https://{nombre-de-app-service}.azurewebsites.net/api/hello


<img src="media/VSTS/web-app16.png">

2. En la página web debe aparecer **Hello Azure!**

<img src="media/VSTS/web-api17.png">
