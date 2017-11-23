---
title: "Publicar una aplicación Spring Boot como contenedor de Docker mediante el kit de herramientas de Azure para IntelliJ"
description: "Aprenda a publicar una aplicación web en Microsoft Azure como un contenedor de Docker con el kit de herramientas de Azure para IntelliJ."
services: 
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
ms.date: 11/01/2017
ms.author: robmcm
ms.openlocfilehash: 65fbdc32824c2b6312929f4888844d1673101ac8
ms.sourcegitcommit: 062e07cbd42cda74f02c82b933ce90da646a50a0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="publish-a-spring-boot-app-as-a-docker-container-by-using-the-azure-toolkit-for-intellij"></a>Publicar una aplicación Spring Boot como contenedor de Docker mediante el kit de herramientas de Azure para IntelliJ

[Spring Framework] es una solución de código abierto que ayuda a los desarrolladores de Java a crear aplicaciones de nivel empresarial. Uno de los proyectos más populares que se basa en esa plataforma es [Spring Boot], que proporciona un enfoque simplificado para crear aplicaciones de Java independientes.

[Docker] es una solución de código abierto que ayuda a los desarrolladores a automatizar la implementación, el escalado y la administración de sus aplicaciones que se ejecutan en contenedores.

Este tutorial le guía por los pasos necesarios para implementar una aplicación Spring Boot como un contenedor de Docker en Microsoft Azure mediante el kit de herramientas de Azure para IntelliJ.

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="clone-the-default-spring-boot-docker-repo"></a>Clonar el repositorio de Docker predeterminado de Spring Boot

Los siguientes pasos le guían por la clonación del repositorio de Docker de Spring Boot mediante IntelliJ. Si quiere usar una línea de comandos, vea [Implementación de una aplicación de Spring Boot en Linux en Azure Container Service][Deploy Spring Boot on Linux in AKS].

1. Abra IntelliJ.

1. En la página principal, seleccione la opción **GitHub** en la lista **Check out from Version Control** (Extraer del repositorio del control de versiones).

   ![Opción de GitHub para el control de versiones][CL01]

1. Introduzca sus credenciales si se le pide que inicie sesión.

   * Si está usando un nombre de usuario y una contraseña para iniciar sesión en GitHub: 

      ![Cuadro de diálogo para escribir el nombre de usuario y la contraseña de GitHub][CL02a]

   * Si está usando un token para iniciar sesión en GitHub: 

      ![Cuadro de diálogo para especificar un token de GitHub][CL02b]

1. Escriba **https://github.com/spring-guides/gs-spring-boot-docker.git** para la dirección URL de repositorio, especifique la ruta de acceso local y la información de la carpeta y, después, haga clic en **Clonar**.

   ![Cuadro de diálogo Clonar repositorio][CL03]

1. Cuando se le pida crear un proyecto de IntelliJ, haga clic en **No**.

   ![Declinación para crear un proyecto de IntelliJ][CL04]

1. En la página principal, haga clic en **Importar proyecto**.

   ![Selección de Importar proyecto][CL05]

1. Busque la ruta de acceso donde ha clonado el repositorio de Spring Boot, seleccione la carpeta **complete** bajo la raíz y, después, haga clic en **Aceptar**.

   ![Seleccionar una carpeta para la importación][CL06]

1. Cuando se le pida, seleccione **Create project from existing sources** (Crear proyecto a partir de orígenes existentes).

   ![Opción para crear un proyecto a partir de orígenes existentes][CL07]

1. Especifique el nombre del proyecto o acepte el valor predeterminado, compruebe la ruta de acceso correcta a la carpeta **complete** y, después, haga clic en **Siguiente**.

   ![Especificar el nombre del proyecto][CL08]

1. Personalice los directorios para importar y haga clic en **Next** (Siguiente).

   ![Elegir directorios][CL09]

1. Revise las bibliotecas que se van a importar y haga clic en **Next** (Siguiente).

   ![Revisar bibliotecas de proyecto][CL10]

1. Revise la estructura del módulo y haga clic en **Next** (Siguiente).

   ![Revisar la estructura del módulo][CL11]

1. Especifique el JDK y, después, haga clic en **Next** (Siguiente).

   ![Especificar un JDK][CL12]

1. Haga clic en **Finalizar**

   ![Botón Finalizar][CL13]

IntelliJ importa la aplicación Spring Boot como un proyecto y muestra la estructura una vez finalizada la importación.

![Aplicación Spring Boot en IntelliJ][CL14]

## <a name="build-your-spring-boot-app"></a>Crear una aplicación Spring Boot

### <a name="build-the-app-by-using-the-maven-pom"></a>Crear la aplicación con POM de Maven

1. Abra la ventana de herramientas de Maven si todavía no está abierta. Haga clic en **Vista** > **Ventanas de herramientas** > **Proyectos de Maven**.

   ![Comandos Ventanas de herramientas y Proyectos de Maven][BU01]

1. En la ventana de herramientas de Maven, haga clic con el botón derecho en **package** (Paquete) y seleccione **Run Maven Build** (Ejecutar la compilación de Maven). (Si el proyecto de Maven no se muestra automáticamente, haga clic en el icono **Reimportar** en la barra de herramientas de Maven).

   ![Comando Ejecutar la compilación de Maven][BU02]

1. IntelliJ debería mostrar un mensaje **COMPILACIÓN CORRECTA** cuando se cree correctamente la aplicación Spring Boot.

   ![Mensaje COMPILACIÓN CORRECTA][BU03]

### <a name="create-a-deployment-ready-artifact"></a>Creación de un artefacto preparado para la implementación

Para publicar la aplicación Spring Boot, debe crear un artefacto preparado para la implementación. Para ello, siga los pasos que se describen a continuación:

1. Abra el proyecto de aplicación web en IntelliJ.

1. Haga clic en **Archivo** y después en **Estructura del proyecto**.

   ![Comando Estructura del proyecto][ART01]

1. Haga clic en el signo más verde (**+**) para agregar un artefacto, haga clic en **JAR** y después en **Vacío**.

   ![Agregar un artefacto][ART02]

1. Nombre el artefacto asegurándose de no agregar la extensión ".jar" y, después, especifique la carpeta de destino para la salida de Maven.

   ![Especificar las propiedades del artefacto][ART03]

1. Cree un manifiesto para el artefacto (opcional):

   a. Haga clic en **Create Manifest** (Crear manifiesto).

      ![Haga clic en el botón Crear manifiesto][ART04a]

   b. Elija la ruta de acceso predeterminada del artefacto y haga clic en **OK** (Aceptar).

      ![Especificar la ruta de acceso del artefacto][ART04b]

   c. Haga clic en los puntos suspensivos (**...**) para buscar la clase principal.

      ![Buscar la clase principal][ART04c]

   d. Elija la clase principal y haga clic en **OK** (Aceptar).

      ![Especificar la clase principal][ART04d]

1. Haga clic en **Aceptar**.

   ![Cerrar el cuadro de diálogo Estructura del proyecto][ART05]

> [!NOTE]
> Para más información sobre cómo crear artefactos en IntelliJ, consulte [Configuring Artifacts] (Configuración de artefactos) en el sitio web de JetBrains.
>

### <a name="build-the-artifact-for-deployment"></a>Compilar el artefacto para la implementación

1. Haga clic en **Build** (Compilar) y haga clic en **Artifacts** (Artefactos).

   ![Comando Compilar artefactos][BU04]

1. Cuando aparece el menú contextual **Build Artifact** (Compilar artefacto), haga clic en **Build** (Compilar).

   ![Menú contextual Compilar artefacto][BU05]

IntelliJ debe mostrar el artefacto completado para la aplicación Spring Boot en la ventana de herramientas del proyecto.

   ![Artefacto creado][BU06]

## <a name="publish-your-web-app-to-azure-by-using-a-docker-container"></a>Publicación de su aplicación web en Azure mediante un contenedor de Docker

1. Si no ha iniciado sesión en su cuenta de Azure, siga los pasos de [Instrucciones de inicio de sesión del kit de herramientas de Azure para IntelliJ][Azure Sign In for IntelliJ].

1. En la ventana de la herramienta del explorador de proyectos, haga clic con el botón derecho en el proyecto y seleccione **Azure** > **Publish as Docker Container** (Publicar como contenedor de Docker).

   ![Comando Publish as Docker Container (Publicar como contenedor de Docker)][PU01]

1. Cuando aparece el cuadro de diálogo **Deploy Docker Container on Azure** (Implementar un contenedor de Docker en Azure), se muestran todos los hosts de Docker existentes. Si decide implementar en un host existente, puede ir al paso 4. En caso contrario, use los pasos siguientes para crear un host:

   a. Haga clic en el signo más verde (**+**).

      ![Agregar un nuevo host de Docker][PU02]

   b. Cuando aparezca el cuadro de diálogo **Create Docker Host** (Crear host de Docker), puede aceptar los valores predeterminados o especificar cualquier configuración personalizada para el nuevo host de Docker. (Para obtener descripciones detalladas de las distintas configuraciones, vea [Publicación de una aplicación web como contenedor de Docker con el kit de herramientas de Azure para IntelliJ][Publish Container with Azure Toolkit]). Haga clic en **Siguiente** cuando haya especificado qué configuración usar.

      ![Especificar las opciones de host de Docker][PU03a]

   c. Puede elegir usar las credenciales de inicio de sesión existentes desde Azure Key Vault, o puede escribir las nuevas credenciales de inicio de sesión de Docker. Haga clic en **Finalizar** cuando haya especificado las opciones.

      ![Especificar credenciales del host de Docker][PU03b]

1. Seleccione el host de Docker y, después, haga clic en **Siguiente**.

   ![Seleccionar el host de Docker que se va a usar][PU04]

1. En la última página del cuadro de diálogo **Deploy Docker Container on Azure** (Implementar un contenedor de Docker en Azure), especifique las siguientes opciones:

   a. Puede elegir especificar un nombre personalizado para el contenedor que va a hospedar el contenedor de Docker, o puede aceptar el valor predeterminado.

   b. Escriba los puertos TCP para el host de Docker mediante la sintaxis siguiente: *[puerto externo]*:*[puerto interno]*. Por ejemplo, **80:8080** especifica un puerto externo de 80 y el puerto de Spring Boot interno predeterminado de 8080.
   
      Si ha personalizado el puerto interno, (por ejemplo, mediante la edición del archivo application.yml), debe especificar el número de puerto para que el enrutamiento correcto se produzca en Azure.

   c. Después de configurar estas opciones, haga clic en **Finalizar**.

   ![Implementar un contenedor de Docker en Azure][PU05]

1. Cuando el kit de herramientas de Azure ha terminado la publicación, el registro de actividad de Azure muestra **Publicado** en el estado.

   ![Host de Docker correctamente implementado][PU06]

## <a name="next-steps"></a>Pasos siguientes

Para obtener información sobre métodos adicionales para crear aplicaciones Spring Boot con IntelliJ, vea [Creating Spring Boot Projects](https://www.jetbrains.com/help/idea/creating-spring-boot-projects.html) (Creación de proyectos Spring Boot) en el sitio web de JetBrains.

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
