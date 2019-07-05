---
title: Java Flight Recorder y Mission Control
description: Guía para el uso de Java Flight Recorder y Mission Control para recopilar y revisar los datos de la aplicación.
author: bmitchell287
manager: douge
ms.author: brendm
ms.date: 4/9/2019
ms.devlang: java
ms.topic: conceptual
ms.openlocfilehash: 64f64f2e5891fccf9d62510f39bd99d73457d590
ms.sourcegitcommit: f8faa4a14c714e148c513fd46f119524f3897abf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2019
ms.locfileid: "67533621"
---
# <a name="use-java-flight-recorder-and-mission-control"></a><span data-ttu-id="953cb-103">Uso de Java Flight Recorder y Mission Control</span><span class="sxs-lookup"><span data-stu-id="953cb-103">Use Java Flight Recorder and Mission Control</span></span>

<span data-ttu-id="953cb-104">Zulu Mission Control es una compilación completamente probada de JDK Mission Control, publicado como código abierto por Oracle en 2018 y que se administra como un proyecto bajo el ámbito de OpenJDK.</span><span class="sxs-lookup"><span data-stu-id="953cb-104">Zulu Mission Control is a fully-tested build of JDK Mission Control, which was open-sourced by Oracle in 2018 and is managed as a project under the OpenJDK umbrella.</span></span> <span data-ttu-id="953cb-105">Junto con Java Flight Recorder, Mission Control ofrece supervisión interactiva de baja sobrecarga y funcionalidades de administración para las cargas de trabajo de Java.</span><span class="sxs-lookup"><span data-stu-id="953cb-105">Coupled with Java Flight Recorder (JFR), Mission Control delivers low-overhead, interactive monitoring and management capabilities for Java workloads.</span></span>

<span data-ttu-id="953cb-106">Zulu Mission Control es compatible con los kits de desarrollo de Java (JDK) y los entornos de ejecución de Java (JRE) siguientes:</span><span class="sxs-lookup"><span data-stu-id="953cb-106">Zulu Mission Control is compatible with the following Java Development Kits (JDKs) and Java Runtime Environments (JREs):</span></span>

* <span data-ttu-id="953cb-107">Zulu 12.1 y versiones posteriores</span><span class="sxs-lookup"><span data-stu-id="953cb-107">Zulu 12.1 and later</span></span>
* <span data-ttu-id="953cb-108">Zulu 11.0 y versiones posteriores</span><span class="sxs-lookup"><span data-stu-id="953cb-108">Zulu 11.0 and later</span></span>
* <span data-ttu-id="953cb-109">Zulu 8u202 (8.36) y versiones posteriores</span><span class="sxs-lookup"><span data-stu-id="953cb-109">Zulu 8u202 (8.36) and later</span></span>
* <span data-ttu-id="953cb-110">Oracle OpenJDK 11 y 15, y versiones posteriores</span><span class="sxs-lookup"><span data-stu-id="953cb-110">Oracle OpenJDK 11 and 15 and later</span></span>
* <span data-ttu-id="953cb-111">Oracle Java 11.0 y versiones posteriores</span><span class="sxs-lookup"><span data-stu-id="953cb-111">Oracle Java 11.0 and later</span></span>
* <span data-ttu-id="953cb-112">Oracle Java 8.0 y versiones posteriores</span><span class="sxs-lookup"><span data-stu-id="953cb-112">Oracle Java 8.0 and later</span></span>

## <a name="install-zulu-mission-control-and-connect-to-a-jvm"></a><span data-ttu-id="953cb-113">Instalación de Zulu Mission Control y conexión a una máquina virtual Java</span><span class="sxs-lookup"><span data-stu-id="953cb-113">Install Zulu Mission Control and connect to a JVM</span></span>

<span data-ttu-id="953cb-114">Para instalar Zulu Mission Control, conectarse a una máquina Virtual Java (JVM) y ganar visibilidad en tiempo real en todos los aspectos de una aplicación en ejecución, haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="953cb-114">To install Zulu Mission Control, connect to a Java Virtual Machine (JVM), and gain real-time visibility into all aspects of a running application, do the following:</span></span>

1.  <span data-ttu-id="953cb-115">[Instale un JDK y JRE compatible con Zulu Mission Control](java-jdk-install.md).</span><span class="sxs-lookup"><span data-stu-id="953cb-115">[Install a Zulu Mission Control-compatible JDK and JRE](java-jdk-install.md).</span></span>

1.  <span data-ttu-id="953cb-116">[Descargue Zulu Mission Control](https://www.azul.com/products/zulu-mission-control/), elija la versión adecuada para su sistema, guárdelo localmente y cambie a ese directorio.</span><span class="sxs-lookup"><span data-stu-id="953cb-116">[Download Zulu Mission Control](https://www.azul.com/products/zulu-mission-control/), choose the appropriate version for your system, save it locally, and change to that directory.</span></span>

1.  <span data-ttu-id="953cb-117">Expanda el archivo descargado.</span><span class="sxs-lookup"><span data-stu-id="953cb-117">Expand the downloaded file.</span></span>

    <span data-ttu-id="953cb-118">**Linux:**</span><span class="sxs-lookup"><span data-stu-id="953cb-118">**Linux:**</span></span>

    ```cli
    tar -xzvf zmc7.0.0-EA-linux_x64.tar.gz
    ```

    <span data-ttu-id="953cb-119">**Windows:**</span><span class="sxs-lookup"><span data-stu-id="953cb-119">**Windows:**</span></span>

    ```cli
    unzip -zxvf zmc7.0.0-EA-win_x64.zip 
    ```

    <span data-ttu-id="953cb-120">**macOS:**</span><span class="sxs-lookup"><span data-stu-id="953cb-120">**macOS:**</span></span>

    ```cli
    tar -xzvf zmc7.0.0-EA-macosx_x64.tar.gz
    ```

1.  <span data-ttu-id="953cb-121">Inicie la aplicación de Java mediante uno de los JDK compatibles.</span><span class="sxs-lookup"><span data-stu-id="953cb-121">Start your Java application by using one of the compatible JDKs.</span></span> <span data-ttu-id="953cb-122">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="953cb-122">For example:</span></span>

    ```cli
    $JAVA_HOME/bin/java -jar MyApplication.jar
    ```

1.  <span data-ttu-id="953cb-123">Inicie Zulu Mission Control.</span><span class="sxs-lookup"><span data-stu-id="953cb-123">Start Zulu Mission Control.</span></span>

    <span data-ttu-id="953cb-124">**Linux:**</span><span class="sxs-lookup"><span data-stu-id="953cb-124">**Linux:**</span></span>

    ```cli
    zmc7.0.0-EA-linux_x64/zmc
    ```

    <span data-ttu-id="953cb-125">**Windows:**</span><span class="sxs-lookup"><span data-stu-id="953cb-125">**Windows:**</span></span>

    ```cli
    zmc7.0.0-EA-win_x64\zmc.exe 
    ```

    <span data-ttu-id="953cb-126">**macOS:**</span><span class="sxs-lookup"><span data-stu-id="953cb-126">**macOS:**</span></span>

    ```cli
    zmc7.0.0-EA-macosx_x64/Zulu\ Mission\ Control.app/Contents/MacOS/zmc
    ```

1.  <span data-ttu-id="953cb-127">(Opcional) Cambie la instalación de la máquina virtual Java para Mission Control.</span><span class="sxs-lookup"><span data-stu-id="953cb-127">(Optional) Switch the JVM installation for Mission Control.</span></span>

    <span data-ttu-id="953cb-128">En dispositivos Windows, *zmc.exe* usará la instalación de la máquina virtual Java predeterminada configurada en el Registro.</span><span class="sxs-lookup"><span data-stu-id="953cb-128">On Windows devices, *zmc.exe* uses the default JVM installation that's configured in the registry.</span></span> <span data-ttu-id="953cb-129">Zulu Mission Control se debe iniciar desde un JDK completo para poder detectar automáticamente las instancias locales de JVM.</span><span class="sxs-lookup"><span data-stu-id="953cb-129">Zulu Mission Control must be launched from a full JDK to be able to detect local JVM instances automatically.</span></span> <span data-ttu-id="953cb-130">Si la instalación es un JRE, no se detectará ninguna máquina virtual Java y recibirá la advertencia siguiente:</span><span class="sxs-lookup"><span data-stu-id="953cb-130">If the installation is a JRE, no JVM will be detected, and you will receive the following warning:</span></span>

    > [!div class="mx-imgBorder"]
    <span data-ttu-id="953cb-131">![Advertencia si la instalación JDK es solo JRE](../media/jdk/azul-jfr-1.png)</span><span class="sxs-lookup"><span data-stu-id="953cb-131">![Warning if JDK installation is JRE-only](../media/jdk/azul-jfr-1.png)</span></span>

    <span data-ttu-id="953cb-132">Para cambiar la máquina virtual Java que utiliza Mission Control, haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="953cb-132">To change the JVM that's used by Mission Control, do the following:</span></span> 

    <span data-ttu-id="953cb-133">a.</span><span class="sxs-lookup"><span data-stu-id="953cb-133">a.</span></span> <span data-ttu-id="953cb-134">Abra el archivo de configuración *zmc.ini*, ubicado en el mismo directorio que el archivo *zmc.exe*.</span><span class="sxs-lookup"><span data-stu-id="953cb-134">Open the *zmc.ini* configuration file, which is in the same directory as the *zmc.exe* file.</span></span>

    <span data-ttu-id="953cb-135">b.</span><span class="sxs-lookup"><span data-stu-id="953cb-135">b.</span></span> <span data-ttu-id="953cb-136">Antes de la línea `-vmargs`, agregue dos líneas:</span><span class="sxs-lookup"><span data-stu-id="953cb-136">Before the line `-vmargs`, add two lines:</span></span>  

       * <span data-ttu-id="953cb-137">En la primera línea, escriba `–vm`.</span><span class="sxs-lookup"><span data-stu-id="953cb-137">On the first line, enter `–vm`.</span></span>  
       * <span data-ttu-id="953cb-138">En la segunda línea, escriba la ruta de acceso a la instalación de JDK (por ejemplo, `C:\Program Files\Java\jdk1.8.0_212\bin\javaw.exe`).</span><span class="sxs-lookup"><span data-stu-id="953cb-138">On the second line, enter the path to your JDK installation (for example, `C:\Program Files\Java\jdk1.8.0_212\bin\javaw.exe`).</span></span>

1.  <span data-ttu-id="953cb-139">Busque la máquina virtual Java que se está ejecutando la aplicación:</span><span class="sxs-lookup"><span data-stu-id="953cb-139">Locate the JVM that's running your application by doing the following:</span></span>

    <span data-ttu-id="953cb-140">a.</span><span class="sxs-lookup"><span data-stu-id="953cb-140">a.</span></span> <span data-ttu-id="953cb-141">En el panel izquierdo de la ventana de Zulu Mission Control, seleccione la pestaña **JVM Browser** (Explorador de máquinas virtuales Java).</span><span class="sxs-lookup"><span data-stu-id="953cb-141">In the left pane of the Zulu Mission Control window, select the **JVM Browser** tab.</span></span>

    <span data-ttu-id="953cb-142">b.</span><span class="sxs-lookup"><span data-stu-id="953cb-142">b.</span></span> <span data-ttu-id="953cb-143">En la lista, seleccione y expanda la instancia de la máquina virtual Java que ejecuta la aplicación.</span><span class="sxs-lookup"><span data-stu-id="953cb-143">In the list, select and expand the JVM instance that's running your application.</span></span>

    ![Instancia de máquina virtual Java expandida en la lista](../media/jdk/azul-jfr-2.png)


1.  <span data-ttu-id="953cb-145">Inicie el registro del vuelo, si es necesario.</span><span class="sxs-lookup"><span data-stu-id="953cb-145">Start a flight recording, if necessary.</span></span>

    <span data-ttu-id="953cb-146">a.</span><span class="sxs-lookup"><span data-stu-id="953cb-146">a.</span></span> <span data-ttu-id="953cb-147">En el panel izquierdo, en **Flight Recorder** (Registrador de vuelo), si se muestra un mensaje *No Recordings* (No hay registros), inicie el registro del vuelo; para ello, haga clic con el botón secundario en **Flight Recorder** (Registrador de vuelo) y, a continuación, seleccione **Start Fllight Recording** (Iniciar registro del vuelo).</span><span class="sxs-lookup"><span data-stu-id="953cb-147">In the left pane, under **Flight Recorder**, if a *No Recordings* message is displayed, start a recording by right-clicking **Flight Recorder** and then selecting **Start Flight Recording**.</span></span>

    <span data-ttu-id="953cb-148">b.</span><span class="sxs-lookup"><span data-stu-id="953cb-148">b.</span></span> <span data-ttu-id="953cb-149">Seleccione **Time fixed recording** (Registro de duración determinada) o **Continuous recording** (Registro continuo) y una configuración detallada **Profiling** (Generación de perfiles) o una configuración con baja sobrecarga **Continuous** (Continua); por último, seleccione **Finish** (Finalizar).</span><span class="sxs-lookup"><span data-stu-id="953cb-149">Select either **Time fixed recording** or **Continuous recording**, and either a **Profiling** configuration (fine-grained) or a **Continuous** configuration (lower overhead), and then select **Finish**.</span></span>

    ![Inicio de un registro del vuelo](../media/jdk/azul-jfr-3.png)

    <span data-ttu-id="953cb-151">El registro del vuelo debería aparecer debajo de la línea **Flight Recorder**, en el explorador de máquinas virtuales Java.</span><span class="sxs-lookup"><span data-stu-id="953cb-151">A flight recording should appear below the **Flight Recorder** line in the JVM browser.</span></span>

1. <span data-ttu-id="953cb-152">Volcado del registro del vuelo</span><span class="sxs-lookup"><span data-stu-id="953cb-152">Dump the flight recording.</span></span> <span data-ttu-id="953cb-153">Para hacerlo, haga clic con el botón derecho en la línea que representa el registro del vuelo y seleccione **Dump whole recording** (Volcar el registro completo).</span><span class="sxs-lookup"><span data-stu-id="953cb-153">To do so, right-click the line that represents the flight recording, and then select **Dump whole recording**.</span></span>

    <span data-ttu-id="953cb-154">Aparece una nueva pestaña en el panel grande del lado derecho de la ventana de Zulu Mission Control.</span><span class="sxs-lookup"><span data-stu-id="953cb-154">A new tab appears in the large pane on the right side of the Zulu Mission Control window.</span></span> <span data-ttu-id="953cb-155">Este panel representa el registro del vuelo recién volcado desde la máquina virtual Java donde se ejecuta la aplicación.</span><span class="sxs-lookup"><span data-stu-id="953cb-155">This pane represents the flight recording that was just dumped from the JVM that's running your application.</span></span>

1. <span data-ttu-id="953cb-156">Examine el registro del vuelo con Zulu Mission Control.</span><span class="sxs-lookup"><span data-stu-id="953cb-156">Examine the flight recording by using Zulu Mission Control.</span></span> <span data-ttu-id="953cb-157">Para ello, seleccione la pestaña **Outline** (Esquema) en el panel izquierdo de la ventana de Zulu Mission Control.</span><span class="sxs-lookup"><span data-stu-id="953cb-157">To do so, select the **Outline** tab in the left pane of the Zulu Mission Control window.</span></span> <span data-ttu-id="953cb-158">Esta pestaña contiene vistas diferentes de los datos recopilados en el registro del vuelo.</span><span class="sxs-lookup"><span data-stu-id="953cb-158">This tab displays various views of the data that's collected in the flight recording.</span></span>
 
    ![Revisión del registro del vuelo](../media/jdk/azul-jfr-4.png)

## <a name="resources"></a><span data-ttu-id="953cb-160">Recursos</span><span class="sxs-lookup"><span data-stu-id="953cb-160">Resources</span></span>

<span data-ttu-id="953cb-161">Para más información, vaya al sitio de Azul Systems y consulte [Azul Webinar: Open Source Flight Recorder and Mission Control - Managing and Measuring OpenJDK 8 Performance](https://www.azul.com/presentation/azul-webinar-open-source-flight-recorder-and-mission-control-managing-and-measuring-openjdk-8-performance/) (Flight Recorder y Mission Control de código abierto: administración y medida del rendimiento de OpenJDK 8).</span><span class="sxs-lookup"><span data-stu-id="953cb-161">To learn more, go to the Azul Systems site and view [Azul Webinar: Open Source Flight Recorder and Mission Control - Managing and Measuring OpenJDK 8 Performance](https://www.azul.com/presentation/azul-webinar-open-source-flight-recorder-and-mission-control-managing-and-measuring-openjdk-8-performance/).</span></span> <span data-ttu-id="953cb-162">El narrador del vídeo es Simon Ritter, responsable de tecnología de Azul Systems.</span><span class="sxs-lookup"><span data-stu-id="953cb-162">The video is narrated by Azul Systems Deputy CTO Simon Ritter.</span></span> <span data-ttu-id="953cb-163">El análisis de Flight Recorder comienza en el minuto 31:30.</span><span class="sxs-lookup"><span data-stu-id="953cb-163">The Flight Recorder discussion starts at 31:30.</span></span>

