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
# <a name="use-java-flight-recorder-and-mission-control"></a>Uso de Java Flight Recorder y Mission Control

Zulu Mission Control es una compilación completamente probada de JDK Mission Control, publicado como código abierto por Oracle en 2018 y que se administra como un proyecto bajo el ámbito de OpenJDK. Junto con Java Flight Recorder, Mission Control ofrece supervisión interactiva de baja sobrecarga y funcionalidades de administración para las cargas de trabajo de Java.

Zulu Mission Control es compatible con los kits de desarrollo de Java (JDK) y los entornos de ejecución de Java (JRE) siguientes:

* Zulu 12.1 y versiones posteriores
* Zulu 11.0 y versiones posteriores
* Zulu 8u202 (8.36) y versiones posteriores
* Oracle OpenJDK 11 y 15, y versiones posteriores
* Oracle Java 11.0 y versiones posteriores
* Oracle Java 8.0 y versiones posteriores

## <a name="install-zulu-mission-control-and-connect-to-a-jvm"></a>Instalación de Zulu Mission Control y conexión a una máquina virtual Java

Para instalar Zulu Mission Control, conectarse a una máquina Virtual Java (JVM) y ganar visibilidad en tiempo real en todos los aspectos de una aplicación en ejecución, haga lo siguiente:

1.  [Instale un JDK y JRE compatible con Zulu Mission Control](java-jdk-install.md).

1.  [Descargue Zulu Mission Control](https://www.azul.com/products/zulu-mission-control/), elija la versión adecuada para su sistema, guárdelo localmente y cambie a ese directorio.

1.  Expanda el archivo descargado.

    **Linux:**

    ```cli
    tar -xzvf zmc7.0.0-EA-linux_x64.tar.gz
    ```

    **Windows:**

    ```cli
    unzip -zxvf zmc7.0.0-EA-win_x64.zip 
    ```

    **macOS:**

    ```cli
    tar -xzvf zmc7.0.0-EA-macosx_x64.tar.gz
    ```

1.  Inicie la aplicación de Java mediante uno de los JDK compatibles. Por ejemplo:

    ```cli
    $JAVA_HOME/bin/java -jar MyApplication.jar
    ```

1.  Inicie Zulu Mission Control.

    **Linux:**

    ```cli
    zmc7.0.0-EA-linux_x64/zmc
    ```

    **Windows:**

    ```cli
    zmc7.0.0-EA-win_x64\zmc.exe 
    ```

    **macOS:**

    ```cli
    zmc7.0.0-EA-macosx_x64/Zulu\ Mission\ Control.app/Contents/MacOS/zmc
    ```

1.  (Opcional) Cambie la instalación de la máquina virtual Java para Mission Control.

    En dispositivos Windows, *zmc.exe* usará la instalación de la máquina virtual Java predeterminada configurada en el Registro. Zulu Mission Control se debe iniciar desde un JDK completo para poder detectar automáticamente las instancias locales de JVM. Si la instalación es un JRE, no se detectará ninguna máquina virtual Java y recibirá la advertencia siguiente:

    > [!div class="mx-imgBorder"]
    ![Advertencia si la instalación JDK es solo JRE](../media/jdk/azul-jfr-1.png)

    Para cambiar la máquina virtual Java que utiliza Mission Control, haga lo siguiente: 

    a. Abra el archivo de configuración *zmc.ini*, ubicado en el mismo directorio que el archivo *zmc.exe*.

    b. Antes de la línea `-vmargs`, agregue dos líneas:  

       * En la primera línea, escriba `–vm`.  
       * En la segunda línea, escriba la ruta de acceso a la instalación de JDK (por ejemplo, `C:\Program Files\Java\jdk1.8.0_212\bin\javaw.exe`).

1.  Busque la máquina virtual Java que se está ejecutando la aplicación:

    a. En el panel izquierdo de la ventana de Zulu Mission Control, seleccione la pestaña **JVM Browser** (Explorador de máquinas virtuales Java).

    b. En la lista, seleccione y expanda la instancia de la máquina virtual Java que ejecuta la aplicación.

    ![Instancia de máquina virtual Java expandida en la lista](../media/jdk/azul-jfr-2.png)


1.  Inicie el registro del vuelo, si es necesario.

    a. En el panel izquierdo, en **Flight Recorder** (Registrador de vuelo), si se muestra un mensaje *No Recordings* (No hay registros), inicie el registro del vuelo; para ello, haga clic con el botón secundario en **Flight Recorder** (Registrador de vuelo) y, a continuación, seleccione **Start Fllight Recording** (Iniciar registro del vuelo).

    b. Seleccione **Time fixed recording** (Registro de duración determinada) o **Continuous recording** (Registro continuo) y una configuración detallada **Profiling** (Generación de perfiles) o una configuración con baja sobrecarga **Continuous** (Continua); por último, seleccione **Finish** (Finalizar).

    ![Inicio de un registro del vuelo](../media/jdk/azul-jfr-3.png)

    El registro del vuelo debería aparecer debajo de la línea **Flight Recorder**, en el explorador de máquinas virtuales Java.

1. Volcado del registro del vuelo Para hacerlo, haga clic con el botón derecho en la línea que representa el registro del vuelo y seleccione **Dump whole recording** (Volcar el registro completo).

    Aparece una nueva pestaña en el panel grande del lado derecho de la ventana de Zulu Mission Control. Este panel representa el registro del vuelo recién volcado desde la máquina virtual Java donde se ejecuta la aplicación.

1. Examine el registro del vuelo con Zulu Mission Control. Para ello, seleccione la pestaña **Outline** (Esquema) en el panel izquierdo de la ventana de Zulu Mission Control. Esta pestaña contiene vistas diferentes de los datos recopilados en el registro del vuelo.
 
    ![Revisión del registro del vuelo](../media/jdk/azul-jfr-4.png)

## <a name="resources"></a>Recursos

Para más información, vaya al sitio de Azul Systems y consulte [Azul Webinar: Open Source Flight Recorder and Mission Control - Managing and Measuring OpenJDK 8 Performance](https://www.azul.com/presentation/azul-webinar-open-source-flight-recorder-and-mission-control-managing-and-measuring-openjdk-8-performance/) (Flight Recorder y Mission Control de código abierto: administración y medida del rendimiento de OpenJDK 8). El narrador del vídeo es Simon Ritter, responsable de tecnología de Azul Systems. El análisis de Flight Recorder comienza en el minuto 31:30.

