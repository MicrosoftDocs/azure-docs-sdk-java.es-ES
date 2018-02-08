---
title: "Publicar una aplicación Spring Boot como contenedor de Docker mediante el kit de herramientas de Azure para Eclipse"
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
ms.openlocfilehash: b54c10dc33324d902a0e778770df8ec4d71dc9a1
ms.sourcegitcommit: 151aaa6ccc64d94ed67f03e846bab953bde15b4a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/03/2018
---
# <a name="publish-a-spring-boot-app-as-a-docker-container-by-using-the-azure-toolkit-for-eclipse"></a>Publicar una aplicación Spring Boot como contenedor de Docker mediante el kit de herramientas de Azure para Eclipse

[Spring Framework] es una solución de código abierto que ayuda a los desarrolladores de Java a crear aplicaciones de nivel empresarial. Uno de los proyectos más populares que se basa en esa plataforma es [Spring Boot], que proporciona un enfoque simplificado para crear aplicaciones de Java independientes.

[Docker] es una solución de código abierto que ayuda a los desarrolladores a automatizar la implementación, el escalado y la administración de sus aplicaciones que se ejecutan en contenedores.

Este tutorial le guía por los pasos necesarios para implementar una aplicación Spring Boot como un contenedor de Docker en Microsoft Azure con el kit de herramientas de Azure para Eclipse.

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="clone-the-default-spring-boot-docker-repository"></a>Clonar el repositorio de Docker predeterminado de Spring Boot

### <a name="import-the-public-repository"></a>Importar el repositorio público

Los siguientes pasos le guiarán por la clonación del repositorio de Docker de Spring Boot al equipo local mediante IntelliJ. Si quiere usar una línea de comandos, vea [Implementación de una aplicación de Spring Boot en Linux en Azure Container Service][Deploy Spring Boot on Linux in AKS].

1. Abra Eclipse.

1. Haga clic en **Archivo** > **Importar**.

   ![Menú de importación de archivo][CL01]

1. Cuando se abra el cuadro de diálogo **Importar**:

   a. Expanda **GIT**.

   b. Seleccione **Proyectos de GIT**.
   
   c. Haga clic en **Next**.

   ![Cuadro de diálogo de importación][CL02]

1. En la página **Seleccionar origen del repositorio**:

   a. Seleccione **Clonar URI**.
   
   b. Haga clic en **Next**.

   ![Página Seleccionar origen del repositorio][CL03]

1. En la página **Repositorio GIT de origen**:

   a. Para **URI**, escriba `https://github.com/spring-guides/gs-spring-boot-docker.git`. Con este paso se deberían rellenar automáticamente los campos **Host** y **Ruta de acceso de repositorio** con los valores correctos.
   
   b. El repositorio de Spring Boot es público, por lo que no debe escribir el nombre de usuario ni la contraseña de GIT.
   
   c. Haga clic en **Next**.

   ![Página Repositorio de GIT de origen][CL04]

1. En la página **Selección de rama**, haga clic en **Siguiente**.

   ![Página Selección de rama][CL05]

1. En la página **Destino local**:

   a. Especifique la carpeta local donde desea que esté el repositorio local.
   
   b. Haga clic en **Next**.

   ![Página Destino local][CL06]

1. En la página **Seleccionar un asistente para usar en la importación de proyectos**:

   a. Seleccione **Import as a general project** (Importar como proyecto general).
   
   b. Haga clic en **Next**.

   ![Página "Seleccionar un asistente para usar en la importación de proyectos"][CL07]

1. En la página **Importar proyectos**:

   a. Especifique el nombre del proyecto.
   
   b. Haga clic en **Finalizar**

   ![Página Importar proyectos][CL08]

1. Una vez que el repositorio se clone correctamente, verá todos los archivos en Eclipse.

   ![Repositorio local][CL09]

### <a name="create-a-maven-project-from-your-local-repository"></a>Crear un proyecto de Maven desde el repositorio local

El repositorio de Docker de Spring Boot contiene un proyecto de Maven finalizado que usará para este tutorial. 

1. Haga clic en **Archivo** > **Importar**.

   ![Comando Importar en el menú Archivo][CL01]

1. Cuando se abra el cuadro de diálogo **Importar**:

   a. Expanda **Maven**.
   
   b. Seleccione **Existing Maven Projects** (Proyectos existentes de Maven).
   
   c. Haga clic en **Next**.

   ![Cuadro de diálogo de importación][MV01]

1. En la página **Maven Projects** (Proyectos de Maven):

   a. Para **Directorio raíz**, especifique la carpeta **complete** del repositorio local.
   
   b. Expanda la sección **Avanzado** y escriba un nombre personalizado para **Plantilla de nombre**.
   
   c. Active la casilla para el archivo **pom.xml** en el proyecto.
   
   d. Haga clic en **Finalizar**

   ![Página de proyectos de Maven][MV02]

1. Cuando el proyecto de Maven se abra correctamente, verá un segundo proyecto en Eclipse.

   ![Proyecto local de Maven][MV03]

## <a name="build-your-spring-boot-app-by-using-maven"></a>Crear una aplicación Spring Boot mediante Maven

1. En el Explorador de proyectos de Eclipse, seleccione el proyecto de Maven.

1. Haga clic en **Ejecutar** > **Ejecutar como** > **Compilación de Maven**.

   ![Comandos para ejecutar como compilación de Maven][BU01]

1. Una vez que la aplicación se compile correctamente, la ventana de la consola muestra el estado.

   ![Compilación correcta de Maven][BU02]

## <a name="publish-your-web-app-to-azure-by-using-a-docker-container"></a>Publicación de su aplicación web en Azure mediante un contenedor de Docker

1. En el Explorador de proyectos de Eclipse, seleccione el proyecto de Maven.

1. Haga clic en el menú **Publicar** de Azure y, luego, en **Publicar como contenedor de Docker**.

   ![Comando Publish as Docker Container (Publicar como contenedor de Docker)][PU01]

1. Cuando aparezca el cuadro de diálogo **Implementación del contenedor de Docker en Azure**:

   a. Escriba un nombre de imagen de Docker personalizado.
   
   b. Para **Artifact to deploy** (Artefacto para implementar), especifique la ruta de acceso al archivo **gs-spring-boot-docker-0.1.0.jar** que acaba de crear.

   ![Especificar opciones de Docker][PU02]

   Se muestran todos los hosts de Docker existentes. 

1. Si decide implementar en un host existente, puede ir al paso 5. En caso contrario, use los pasos siguientes para crear un host:

   a. Haga clic en **Agregar**.

      ![Agregar un nuevo host de Docker][PU03]

   b. Cuando aparezca el cuadro de diálogo **Create Docker Host** (Crear host de Docker), puede aceptar los valores predeterminados o especificar cualquier configuración personalizada para el nuevo host de Docker. (Para obtener descripciones detalladas de las distintas configuraciones, vea [Publicación de una aplicación web como contenedor de Docker con el kit de herramientas de Azure para IntelliJ][Publish Container with Azure Toolkit]). Haga clic en **Siguiente** cuando haya especificado qué configuración usar.

      ![Especificar las opciones de host de Docker][PU04]

   c. Puede elegir usar las credenciales de inicio de sesión existentes desde Azure Key Vault, o puede escribir las nuevas credenciales de inicio de sesión de Docker. Haga clic en **Finalizar** cuando haya especificado las opciones.

      ![Especificar credenciales del host de Docker][PU05]

1. Seleccione el host de Docker y, después, haga clic en **Siguiente**.

   ![Seleccionar el host de Docker que se va a usar][PU06]

1. En la última página del cuadro de diálogo **Deploying Docker Container on Azure** (Implementación de un contenedor de Docker en Azure), especifique las siguientes opciones:

   a. Puede elegir especificar un nombre personalizado para el contenedor que va a hospedar el contenedor de Docker, o puede aceptar el valor predeterminado.

   b. Escriba los puertos TCP para el host de Docker mediante la sintaxis siguiente: *[puerto externo]*:*[puerto interno]*. Por ejemplo, **80:8080** especifica un puerto externo de 80 y el puerto de Spring Boot interno predeterminado de 8080.
   
      Si ha personalizado el puerto interno, (por ejemplo, mediante la edición del archivo application.yml), debe especificar el número de puerto para que el enrutamiento correcto se produzca en Azure.

   c. Después de configurar estas opciones, haga clic en **Finalizar**.

   ![Implementar un contenedor de Docker en Azure][PU07]

1. Cuando el kit de herramientas de Azure ha terminado la publicación, el registro de actividad de Azure muestra **Publicado** en el estado.

   ![Host de Docker correctamente implementado][PU08]

## <a name="next-steps"></a>pasos siguientes

Para ver más recursos de Docker, consulte el [sitio web oficial de Docker].

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
