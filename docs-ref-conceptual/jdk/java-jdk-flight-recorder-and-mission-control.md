---
title: Java Flight Recorder y Mission Control
description: Guía para el uso de Java Flight Recorder y Mission Control para recopilar y revisar los datos de la aplicación.
author: bmitchell287
manager: douge
ms.author: brendm
ms.date: 4/9/2019
ms.devlang: java
ms.topic: conceptual
ms.openlocfilehash: b27e0f741f1322b7e8e1df363dbb2f40a3d34d53
ms.sourcegitcommit: 04cff6e3c6d3a9c15f7d88d5d3c238f0bdc787fd
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2019
ms.locfileid: "64568568"
---
# <a name="using-java-flight-recorder-jfr-and-mission-control"></a><span data-ttu-id="762e8-103">Uso de Java Flight Recorder (JFR) y Mission Control</span><span class="sxs-lookup"><span data-stu-id="762e8-103">Using Java Flight Recorder (JFR) and Mission Control</span></span>

<span data-ttu-id="762e8-104">Zulu Mission Control es una compilación completamente probada de JDK Mission Control, liberado como código abierto por Oracle en 2018 y que se administra como un proyecto bajo el paraguas de OpenJDK.</span><span class="sxs-lookup"><span data-stu-id="762e8-104">Zulu Mission Control is a fully-tested build of JDK Mission Control, which was open sourced by Oracle in 2018 and is managed as a project under the OpenJDK umbrella.</span></span> <span data-ttu-id="762e8-105">Junto con Flight Recorder, Mission Control ofrece supervisión interactiva de baja sobrecarga y funcionalidades de administración para las cargas de trabajo de Java.</span><span class="sxs-lookup"><span data-stu-id="762e8-105">Coupled with Flight Recorder, Mission Control delivers low-overhead, interactive monitoring and management capabilities for Java workloads.</span></span>

<span data-ttu-id="762e8-106">Zulu Mission Control es compatible con los siguientes JDK y JRE:</span><span class="sxs-lookup"><span data-stu-id="762e8-106">Zulu Mission Control is compatible with the following JDKs/JREs:</span></span>

* <span data-ttu-id="762e8-107">Zulu 12.1 y versiones posteriores</span><span class="sxs-lookup"><span data-stu-id="762e8-107">Zulu 12.1 and later</span></span>
* <span data-ttu-id="762e8-108">Zulu 11.0 y versiones posteriores</span><span class="sxs-lookup"><span data-stu-id="762e8-108">Zulu 11.0 and later</span></span>
* <span data-ttu-id="762e8-109">Zulu 8u202 (8.36) y versiones posteriores</span><span class="sxs-lookup"><span data-stu-id="762e8-109">Zulu 8u202 (8.36) and later</span></span>
* <span data-ttu-id="762e8-110">Oracle OpenJDK 11+15 y versiones posteriores</span><span class="sxs-lookup"><span data-stu-id="762e8-110">Oracle OpenJDK 11+15 and later</span></span>
* <span data-ttu-id="762e8-111">Oracle Java 11.0 y versiones posteriores</span><span class="sxs-lookup"><span data-stu-id="762e8-111">Oracle Java 11.0 and later</span></span>
* <span data-ttu-id="762e8-112">Oracle Java 8.0 y versiones posteriores</span><span class="sxs-lookup"><span data-stu-id="762e8-112">Oracle Java 8.0 and later</span></span>

<span data-ttu-id="762e8-113">Siga los pasos que aparecen a continuación para instalar Zulu Mission Control, conectarse a una máquina Virtual Java (JVM) y ganar visibilidad en tiempo real en todos los aspectos de una aplicación en ejecución.</span><span class="sxs-lookup"><span data-stu-id="762e8-113">Follow the steps below to install Zulu Mission Control, connect to a Java Virtual Machine (JVM), and gain real-time visibility into all aspects of a running application.</span></span>

1.  <span data-ttu-id="762e8-114">[Instale un JDK/JRE compatible con Zulu Mission Control](java-jdk-install.md).</span><span class="sxs-lookup"><span data-stu-id="762e8-114">[Install a Zulu Mission Control compatible JDK/JRE](java-jdk-install.md).</span></span>

2.  <span data-ttu-id="762e8-115">Descargue Zulu Mission Control desde [el sitio de descarga de Azul](https://www.azul.com/products/zulu-mission-control/), elija la versión adecuada para su sistema, guárdelo localmente y cambie a ese directorio.</span><span class="sxs-lookup"><span data-stu-id="762e8-115">Download Zulu Mission Control from [the Azul download site](https://www.azul.com/products/zulu-mission-control/), choose the appropriate version for your system, save it locally, and change to that directory.</span></span>

3.  <span data-ttu-id="762e8-116">Expanda el archivo descargado.</span><span class="sxs-lookup"><span data-stu-id="762e8-116">Expand the downloaded file.</span></span>

    <span data-ttu-id="762e8-117">**Linux:**</span><span class="sxs-lookup"><span data-stu-id="762e8-117">**Linux:**</span></span>

    ```cli
    tar -xzvf zmc7.0.0-EA-linux_x64.tar.gz
    ```

    <span data-ttu-id="762e8-118">**Windows:**</span><span class="sxs-lookup"><span data-stu-id="762e8-118">**Windows:**</span></span>

    ```cli
    unzip -zxvf zmc7.0.0-EA-win_x64.zip 
    ```

    <span data-ttu-id="762e8-119">**MacOS:**</span><span class="sxs-lookup"><span data-stu-id="762e8-119">**MacOS:**</span></span>

    ```cli
    tar -xzvf zmc7.0.0-EA-macosx_x64.tar.gz
    ```

4.  <span data-ttu-id="762e8-120">Inicie la aplicación de Java mediante uno de los JDK compatibles.</span><span class="sxs-lookup"><span data-stu-id="762e8-120">Start your Java application using one of the compatible JDKs.</span></span> <span data-ttu-id="762e8-121">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="762e8-121">E.g.:</span></span>

    ```cli
    $JAVA_HOME/bin/java -jar MyApplication.jar
    ```

5.  <span data-ttu-id="762e8-122">Inicio de Zulu Mission Control</span><span class="sxs-lookup"><span data-stu-id="762e8-122">Start Zulu Mission Control</span></span>

    <span data-ttu-id="762e8-123">**Linux:**</span><span class="sxs-lookup"><span data-stu-id="762e8-123">**Linux:**</span></span>

    ```cli
    zmc7.0.0-EA-linux_x64/zmc
    ```

    <span data-ttu-id="762e8-124">**Windows:**</span><span class="sxs-lookup"><span data-stu-id="762e8-124">**Windows:**</span></span>

    ```cli
    zmc7.0.0-EA-win_x64\zmc.exe 
    ```

    <span data-ttu-id="762e8-125">**MacOS:**</span><span class="sxs-lookup"><span data-stu-id="762e8-125">**MacOS:**</span></span>

    ```cli
    zmc7.0.0-EA-macosx_x64/Zulu\ Mission\ Control.app/Contents/MacOS/zmc
    ```

6.  <span data-ttu-id="762e8-126">Cambio de la instalación de JVM para Mission Control (opcional)</span><span class="sxs-lookup"><span data-stu-id="762e8-126">Switch the JVM installation for Mission Control (Optional)</span></span>

    <span data-ttu-id="762e8-127">En Windows, *zmc.exe* usará la instalación de JVM predeterminada configurada en el registro.</span><span class="sxs-lookup"><span data-stu-id="762e8-127">On Windows, *zmc.exe* will use the default JVM installation configured in the registry.</span></span> <span data-ttu-id="762e8-128">Zulu Mission Control se debe iniciar desde un JDK completo para poder detectar automáticamente las instancias locales de JVM.</span><span class="sxs-lookup"><span data-stu-id="762e8-128">Zulu Mission Control must be launched from a full JDK to be able to detect local JVM instances automatically.</span></span> <span data-ttu-id="762e8-129">Si se trata de una versión de JRE, verá la siguiente advertencia:</span><span class="sxs-lookup"><span data-stu-id="762e8-129">If this is a JRE, you will see the warning below:</span></span>

    > [!div class="mx-imgBorder"]
    <span data-ttu-id="762e8-130">![Advertencia si la instalación JDK es solo JRE](../media/jdk/azul-jfr-1.png)</span><span class="sxs-lookup"><span data-stu-id="762e8-130">![Warning if JDK install is JRE-only](../media/jdk/azul-jfr-1.png)</span></span>

    <span data-ttu-id="762e8-131">Para cambiar la versión de JVM utilizada por Mission Control, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="762e8-131">To change the JVM used by Mission Control, follow these steps:</span></span> 
    1.  <span data-ttu-id="762e8-132">Abra el archivo de configuración *zmc.ini*, ubicado en el mismo directorio que el archivo *zmc.exe*</span><span class="sxs-lookup"><span data-stu-id="762e8-132">Open *zmc.ini* configuration file, located in the same directory as the *zmc.exe*</span></span>
    2.  <span data-ttu-id="762e8-133">Antes de la línea `-vmargs`, agregue dos líneas:</span><span class="sxs-lookup"><span data-stu-id="762e8-133">Before the line `-vmargs`, add two lines:</span></span>
        * <span data-ttu-id="762e8-134">En la primera línea, escriba `–vm`</span><span class="sxs-lookup"><span data-stu-id="762e8-134">On the first line, write `–vm`</span></span>
        * <span data-ttu-id="762e8-135">En la segunda línea, escriba la ruta de acceso a la instalación de JDK.</span><span class="sxs-lookup"><span data-stu-id="762e8-135">On the second line, write the path to your JDK installation.</span></span> <span data-ttu-id="762e8-136">(Por ejemplo, `C:\Program Files\Java\jdk1.8.0_212\bin\javaw.exe`).</span><span class="sxs-lookup"><span data-stu-id="762e8-136">(For example, `C:\Program Files\Java\jdk1.8.0_212\bin\javaw.exe`).</span></span>

7.  <span data-ttu-id="762e8-137">Búsqueda de la versión de JVM que ejecuta la aplicación</span><span class="sxs-lookup"><span data-stu-id="762e8-137">Locate the JVM running your application</span></span>
    1.  <span data-ttu-id="762e8-138">En el panel superior izquierdo de la ventana de Zulu Mission Control, haga clic en la pestaña etiquetada **JVM Browser** (Explorador de JVM).</span><span class="sxs-lookup"><span data-stu-id="762e8-138">In the upper left pane of the Zulu Mission Control window click on the tab labelled **JVM Browser**.</span></span>
    2.  <span data-ttu-id="762e8-139">Seleccione y expanda el elemento de la lista de la parte superior izquierda de la instancia de JVM que ejecuta la aplicación.</span><span class="sxs-lookup"><span data-stu-id="762e8-139">Select and expand the list item in the upper left for your the JVM instance running your application.</span></span>

    > [!div class="mx-imgBorder"]
    <span data-ttu-id="762e8-140">![Expansión del elemento de la lista de la parte superior izquierda de la instancia de JVM](../media/jdk/azul-jfr-2.png)</span><span class="sxs-lookup"><span data-stu-id="762e8-140">![Expand the list item in the upper-left for your JVM instance](../media/jdk/azul-jfr-2.png)</span></span>


8.  <span data-ttu-id="762e8-141">Inicie una operación Flight Recording, si es necesario</span><span class="sxs-lookup"><span data-stu-id="762e8-141">Start a Flight Recording, if necessary</span></span>
    1.  <span data-ttu-id="762e8-142">Si Flight Recorder muestra "No hay grabaciones", inicie una con un click con el botón derecho en la línea de Flight Recorder en la pestaña del explorador de JVM y seleccione **Start Flight Recording...**</span><span class="sxs-lookup"><span data-stu-id="762e8-142">If the Flight Recorder displays "No Recordings", start one by right-clicking on the Flight Recorder line in the JVM Browser tab and selecting **Start Flight Recording...**</span></span>
    2.  <span data-ttu-id="762e8-143">Seleccione una grabación de duración fija o una grabación continua y una configuración de generación de perfiles (específica) o una configuración continua (con menor sobrecarga) y, a continuación, haga clic en **Finish** (Finalizar).</span><span class="sxs-lookup"><span data-stu-id="762e8-143">Select either a fixed duration recording or a continuous recording, and either a Profiling configuration (fine-grained) or a Continuous configuration (lower overhead), then click **Finish**.</span></span>

    > [!div class="mx-imgBorder"]
    <span data-ttu-id="762e8-144">![Inicio de una operación Flight Recording](../media/jdk/azul-jfr-3.png)</span><span class="sxs-lookup"><span data-stu-id="762e8-144">![Start a Flight Recording](../media/jdk/azul-jfr-3.png)</span></span>

9.  <span data-ttu-id="762e8-145">Volcado de la operación Flight Recording</span><span class="sxs-lookup"><span data-stu-id="762e8-145">Dump the Flight Recording</span></span>
    1.  <span data-ttu-id="762e8-146">Debería aparecer un elemento Flight Recording debajo de la línea de Flight Recorder en el explorador de JVM.</span><span class="sxs-lookup"><span data-stu-id="762e8-146">A Flight Recording should appear below the Flight Recorder line in the JVM Browser.</span></span> <span data-ttu-id="762e8-147">Haga clic con el botón derecho en la línea que representa la operación Flight Recording y seleccione **Dump whole recording** (Volcar la grabación completa).</span><span class="sxs-lookup"><span data-stu-id="762e8-147">Right-click on the line representing the Flight Recording and select **Dump whole recording**.</span></span>
    2.  <span data-ttu-id="762e8-148">Aparecerá una nueva pestaña en el panel grande del lado derecho de la ventana de Zulu Mission Control.</span><span class="sxs-lookup"><span data-stu-id="762e8-148">A new tab will appear in the large pane on the right side of the Zulu Mission Control window.</span></span> <span data-ttu-id="762e8-149">Este panel representa la grabación de Flight Recording recién volcada desde la instancia de JVM que ejecuta la aplicación.</span><span class="sxs-lookup"><span data-stu-id="762e8-149">This pane represents the Flight Recording just dumped from the JVM running your application.</span></span>

10. <span data-ttu-id="762e8-150">Examen de la grabación de Flight Recording con Zulu Mission Control</span><span class="sxs-lookup"><span data-stu-id="762e8-150">Examine the Flight Recording using Zulu Mission Control</span></span>
    1.  <span data-ttu-id="762e8-151">Si aún no está activada, seleccione la pestaña etiquetada **Outline** (Esquema) en el panel izquierdo de la ventana de Zulu Mission Control.</span><span class="sxs-lookup"><span data-stu-id="762e8-151">If not already activated, select the tab labelled **Outline** in the left pane of the Zulu Mission Control Window.</span></span> <span data-ttu-id="762e8-152">Esta pestaña contiene vistas diferentes de los datos recopilados en la operación Flight Recording.</span><span class="sxs-lookup"><span data-stu-id="762e8-152">This tab contains different views of the data collected in the Flight Recording.</span></span>
 
    > [!div class="mx-imgBorder"]
    <span data-ttu-id="762e8-153">![Revisión de la grabación de Flight Recording](../media/jdk/azul-jfr-4.png)</span><span class="sxs-lookup"><span data-stu-id="762e8-153">![Review the Fliight Recording](../media/jdk/azul-jfr-4.png)</span></span>

## <a name="resources"></a><span data-ttu-id="762e8-154">Recursos</span><span class="sxs-lookup"><span data-stu-id="762e8-154">Resources</span></span>

<span data-ttu-id="762e8-155">También hemos preparado un [vídeo de demostración](https://www.azul.com/presentation/azul-webinar-open-source-flight-recorder-and-mission-control-managing-and-measuring-openjdk-8-performance/) con comentarios de Simon Ritter, CTO de Azul Systems.</span><span class="sxs-lookup"><span data-stu-id="762e8-155">We have also prepared a [demonstration video](https://www.azul.com/presentation/azul-webinar-open-source-flight-recorder-and-mission-control-managing-and-measuring-openjdk-8-performance/) narrated by Azul Systems Deputy CTO Simon Ritter.</span></span> <span data-ttu-id="762e8-156">El vídeo le guiará en la instalación y configuración de Flight Recorder y Zulu Mission Control.</span><span class="sxs-lookup"><span data-stu-id="762e8-156">The video walks you through the configuration and setup of both Flight Recorder and Zulu Mission Control.</span></span> <span data-ttu-id="762e8-157">El análisis de Flight Recorder comienza en el minuto 31:30.</span><span class="sxs-lookup"><span data-stu-id="762e8-157">The Flight Recorder discussion starts at 31:30.</span></span>

