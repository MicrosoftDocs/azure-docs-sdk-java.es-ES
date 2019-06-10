---
title: Instalación del JDK de Azul Zulu para Azure y Azure Stack
description: Procedimiento de instalación de los kits de desarrollo de Java (JDK) de Azul Zulu para el desarrollo en Azure con Windows, Linux y Mac
author: erickson-doug
manager: douge
ms.author: douge
ms.date: 4/19/2019
ms.devlang: java
ms.topic: conceptual
ms.openlocfilehash: 33d2206f9a0a1cc9fadc60b17c1a93f66c592fe3
ms.sourcegitcommit: 04cff6e3c6d3a9c15f7d88d5d3c238f0bdc787fd
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2019
ms.locfileid: "64568598"
---
# <a name="install-the-jdk-for-azure-and-azure-stack"></a>Instalación del JDK para Azure y Azure Stack

Las compilaciones del OpenJDK de Azul Zulu Enterprise son una distribución gratuita, multiplataforma y lista para producción del OpenJDK para Azure y Azure Stack respaldado por Microsoft y Azul Systems. Contienen todos los componentes para la creación y ejecución de aplicaciones de Java SE.

Hay [varios tipos de paquete de descarga admitidos para cada sistema operativo cliente](https://www.azul.com/downloads/azure-only/zulu/). También puede obtener una imagen de máquina virtual desde la galería de Azure Marketplace para las plataformas siguientes:

  * [Azul Zulu: Java 8 en Ubuntu 18.04](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/azul.azul-zulu8-ubuntu-1804)
  * [Azul Zulu: Java 8 en Windows Server 2019](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/azul.azul-zulu8-windows-2019)
  
  * [Azul Zulu: Java 11 en Ubuntu 18.04](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/azul.azul-zulu11-ubuntu-1804)
  * [Azul Zulu: Java 11 en Windows Server 2019](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/azul.azul-zulu11-windows-2019)


> [!NOTE]
> Estas instrucciones tienen como destino la versión de Java 8 de 64 bits del JDK. Azul también proporciona el entorno de ejecución de Java (JRE) como una instalación independiente. JRE se incluye con la instalación del JDK.
>
>  También se proporcionan paquetes de Java 11 en la [página de descargas de Azure de Azul](https://www.azul.com/downloads/azure-only/zulu/).

## <a name="download-and-install-the-azul-zulu-jdks-for-windows"></a>Descarga e instalación de los JDK de Azul Zulu para Windows 

1. [Descargue el JDK 8 de 64 bits de Azul Zulu como un archivo MSI](https://repos.azul.com/azure-only/zulu/packages/zulu-11/11.0.3/zulu-11-azure-jdk_11.31.11-11.0.3-win_x64.msi) en una ubicación del cliente, como `C:\Users\<your_login>\Downloads`. (También se proporcionan paquetes .ZIP en la [página de descargas de Azure de Azul](https://www.azul.com/downloads/azure-only/zulu/)).

2. Vaya al directorio y haga doble clic en el archivo MSI descargado para comenzar la instalación.

## <a name="download-and-install-the-azul-zulu-jdks-for-mac"></a>Descarga e instalación de los JDK de Azul Zulu para Mac 

Estos pasos descargan un archivo ZIP en el equipo Mac. También hay disponible una versión DMG.

1. [Descargue JDK 8 de 64 bits de Azul Zulu como un archivo ZIP](https://repos.azul.com/azure-only/zulu/packages/zulu-11/11.0.3/zulu-11-azure-jdk_11.31.11-11.0.3-macosx_x64.zip) en una ubicación del cliente, como `/Library/Java/JavaVirtualMachines/`. (También se proporcionan paquetes .DMG en la [página de descargas de Azure de Azul](https://www.azul.com/downloads/azure-only/zulu/)).

2. Inicie Finder, vaya al directorio de descarga y haga doble clic en el archivo ZIP. Como alternativa, puede iniciar una ventana de comandos de terminal; para ello, vaya al directorio y ejecute:

```cli
unzip <name_of_zulu_package>.zip
```

## <a name="download-and-install-the-azul-zulu-jdks-for-alpine-linux"></a>Descarga e instalación de los JDK de Azul Zulu para Alpine Linux

1. [Descargue JDK 8 de 64 bits de Azul Zulu como un archivo TAR](https://repos.azul.com/azure-only/zulu/packages/zulu-11/11.0.3/zulu-11-azure-jdk_11.31.11-11.0.3-linux_x64.tar.gz) en una ubicación del cliente, como `/usr/lib/jvm`. (También se proporcionan paquetes .RPM y .DEB en la [página de descargas de Azure de Azul](https://www.azul.com/downloads/azure-only/zulu/)).

2. Vaya al directorio y ejecute el siguiente comando para descomprimir y expandir el archivo:

    ```cli
    tar -xvf <name_of_zulu_package>.tar
    ```

## <a name="confirm-your-installation"></a>Confirmación de la instalación

Para confirmar la instalación, vaya a la línea de comandos y ejecute `java -version`.

La salida del comando debe ser:

```cli
$ java -version

openjdk version "1.8.0_212"
OpenJDK Runtime Environment (Zulu 8.38.0.13-macosx)-Microsoft-Azure-restricted (build 1.8.0_212-b04)
OpenJDK 64-Bit Server VM (Zulu 8.38.0.13-macosx)-Microsoft-Azure-restricted (build 25.212-b04, mixed mode)

```

## <a name="download-and-install-the-azul-zulu-jdks-from-a-yum-repository"></a>Descarga e instalación de los JDK de Azul Zulu desde un repositorio Yum

Azul proporciona los JDK de Azul Zulu en un [repositorio Yum](http://repos.azul.com/azure-only/zulu-azure.repo).

**Para instalar el JDK de Azul Zulu para Java 8, ejecute los siguientes comandos desde la CLI:**

```cli
sudo rpm --import http://repos.azul.com/azul-repo.key
sudo curl http://repos.azul.com/azure-only/zulu-azure.repo -o /etc/yum.repos.d/zulu-azure.repo
sudo yum -q -y update
sudo yum -q -y install zulu-8-azure-jdk
```

Para Java 11, ejecute:

```cli
sudo rpm --import http://repos.azul.com/azul-repo.key
sudo curl http://repos.azul.com/azure-only/zulu-azure.repo -o /etc/yum.repos.d/zulu-azure.repo
sudo yum -q -y update
sudo yum -q -y install zulu-11-azure-jdk
```

Para Java 12 (versión preliminar), ejecute:

```cli
sudo rpm --import http://repos.azul.com/azul-repo.key
sudo curl http://repos.azul.com/azure-only/zulu-azure.repo -o /etc/yum.repos.d/zulu-azure.repo
sudo yum -q -y update
sudo yum -q -y install zulu-12-azure-jdk
```

**Para actualizar un paquete del JDK 8 de Zulu desde un repositorio Yum:**

```cli
sudo yum -q -y install zulu-8-azure-jdk
```

(Cambie el número de versión en el comando anterior si usa las versiones 11 o 12).

**Para eliminar un paquete del JDK 8 de Zulu desde un repositorio Yum:**

```cli
sudo yum -y erase zulu-8-azure-jdk
```
(Cambie el número de versión en el comando anterior si usa las versiones 11 o 12).

## <a name="download-and-install-the-azul-zulu-jdks-from-an-apt-get-repository"></a>Descarga e instalación de los JDK de Azul Zulu desde un repositorio apt-get

Azul proporciona los JDK de Azul Zulu en un [repositorio apt-get](http://repos.azul.com/azure-only/zulu/apt).

**Para instalar el JDK de Azul Zulu para Java 8 con apt-get, ejecute los siguientes comandos desde la CLI:**

```cli
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 0xB1998361219BD9C9
sudo apt-add-repository "deb http://repos.azul.com/azure-only/zulu/apt stable main"
sudo apt-get -q update
sudo apt-get -y install zulu-8-azure-jdk
```

Para Java 11, ejecute:

```cli
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 0xB1998361219BD9C9
sudo apt-add-repository "deb http://repos.azul.com/azure-only/zulu/apt stable main"
sudo apt-get -q update
sudo apt-get -y install zulu-11-azure-jdk
```

Para Java 12 (versión preliminar), ejecute:

```cli
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 0xB1998361219BD9C9
sudo apt-add-repository "deb http://repos.azul.com/azure-only/zulu/apt stable main"
sudo apt-get -q update
sudo apt-get -y install zulu-12-azure-jdk
```

**Para actualizar un paquete del JDK 8 de Zulu desde un repositorio apt-get:**

```cli
sudo apt-get -q update
sudo apt-get -y install zulu-8-azure-jdk
```

Se eliminará automáticamente la versión anterior.
(Cambie el número de versión en el comando anterior si usa las versiones 11 o 12).

**Para eliminar un paquete del JDK 8 de Zulu desde un repositorio apt-get:**

```cli
sudo apt-get -y purge zulu-8-azure-jdk
```

(Cambie el número de versión en el comando anterior si usa las versiones 11 o 12).

Para más instrucciones acerca de cómo preparar, instalar y administrar los JDK de Azul Zulu para el desarrollo en Azure, consulte [la documentación oficial de Zulu](https://docs.azul.com/zulu/zuludocs/index.htm).

