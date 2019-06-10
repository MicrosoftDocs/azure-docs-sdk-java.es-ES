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
# <a name="install-the-jdk-for-azure-and-azure-stack"></a><span data-ttu-id="f92b5-103">Instalación del JDK para Azure y Azure Stack</span><span class="sxs-lookup"><span data-stu-id="f92b5-103">Install the JDK for Azure and Azure Stack</span></span>

<span data-ttu-id="f92b5-104">Las compilaciones del OpenJDK de Azul Zulu Enterprise son una distribución gratuita, multiplataforma y lista para producción del OpenJDK para Azure y Azure Stack respaldado por Microsoft y Azul Systems.</span><span class="sxs-lookup"><span data-stu-id="f92b5-104">Azul Zulu Enterprise builds of OpenJDK are a no-cost, multi-platform, production-ready distribution of the OpenJDK for Azure and Azure Stack backed by Microsoft and Azul Systems.</span></span> <span data-ttu-id="f92b5-105">Contienen todos los componentes para la creación y ejecución de aplicaciones de Java SE.</span><span class="sxs-lookup"><span data-stu-id="f92b5-105">They contain all the components for building and running Java SE applications.</span></span>

<span data-ttu-id="f92b5-106">Hay [varios tipos de paquete de descarga admitidos para cada sistema operativo cliente](https://www.azul.com/downloads/azure-only/zulu/).</span><span class="sxs-lookup"><span data-stu-id="f92b5-106">There are [multiple download package types supported for each client OS](https://www.azul.com/downloads/azure-only/zulu/).</span></span> <span data-ttu-id="f92b5-107">También puede obtener una imagen de máquina virtual desde la galería de Azure Marketplace para las plataformas siguientes:</span><span class="sxs-lookup"><span data-stu-id="f92b5-107">You can also get a virtual machine image from the Azure Marketplace Gallery for the following platforms:</span></span>

  * [<span data-ttu-id="f92b5-108">Azul Zulu: Java 8 en Ubuntu 18.04</span><span class="sxs-lookup"><span data-stu-id="f92b5-108">Azul Zulu: Java 8 on Ubuntu 18.04</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/azul.azul-zulu8-ubuntu-1804)
  * [<span data-ttu-id="f92b5-109">Azul Zulu: Java 8 en Windows Server 2019</span><span class="sxs-lookup"><span data-stu-id="f92b5-109">Azul Zulu: Java 8 on Windows Server 2019</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/azul.azul-zulu8-windows-2019)
  
  * [<span data-ttu-id="f92b5-110">Azul Zulu: Java 11 en Ubuntu 18.04</span><span class="sxs-lookup"><span data-stu-id="f92b5-110">Azul Zulu: Java 11 on Ubuntu 18.04</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/azul.azul-zulu11-ubuntu-1804)
  * [<span data-ttu-id="f92b5-111">Azul Zulu: Java 11 en Windows Server 2019</span><span class="sxs-lookup"><span data-stu-id="f92b5-111">Azul Zulu: Java 11 on Windows Server 2019</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/azul.azul-zulu11-windows-2019)


> [!NOTE]
> <span data-ttu-id="f92b5-112">Estas instrucciones tienen como destino la versión de Java 8 de 64 bits del JDK.</span><span class="sxs-lookup"><span data-stu-id="f92b5-112">These instructions target the 64-bit Java 8 version of the JDK.</span></span> <span data-ttu-id="f92b5-113">Azul también proporciona el entorno de ejecución de Java (JRE) como una instalación independiente.</span><span class="sxs-lookup"><span data-stu-id="f92b5-113">Azul also provides the Java Run-time Environment (JRE) as a stand-alone installation.</span></span> <span data-ttu-id="f92b5-114">JRE se incluye con la instalación del JDK.</span><span class="sxs-lookup"><span data-stu-id="f92b5-114">The JRE is included with the JDK install.</span></span>
>
>  <span data-ttu-id="f92b5-115">También se proporcionan paquetes de Java 11 en la [página de descargas de Azure de Azul](https://www.azul.com/downloads/azure-only/zulu/).</span><span class="sxs-lookup"><span data-stu-id="f92b5-115">Java 11 packages are also provided on [Azul's Azure downloads page](https://www.azul.com/downloads/azure-only/zulu/).</span></span>

## <a name="download-and-install-the-azul-zulu-jdks-for-windows"></a><span data-ttu-id="f92b5-116">Descarga e instalación de los JDK de Azul Zulu para Windows</span><span class="sxs-lookup"><span data-stu-id="f92b5-116">Download and install the Azul Zulu JDKs for Windows</span></span> 

1. <span data-ttu-id="f92b5-117">[Descargue el JDK 8 de 64 bits de Azul Zulu como un archivo MSI](https://repos.azul.com/azure-only/zulu/packages/zulu-11/11.0.3/zulu-11-azure-jdk_11.31.11-11.0.3-win_x64.msi) en una ubicación del cliente, como `C:\Users\<your_login>\Downloads`.</span><span class="sxs-lookup"><span data-stu-id="f92b5-117">[Download the 64-bit Azul Zulu JDK 8 as an MSI](https://repos.azul.com/azure-only/zulu/packages/zulu-11/11.0.3/zulu-11-azure-jdk_11.31.11-11.0.3-win_x64.msi) to a location on your client, such as `C:\Users\<your_login>\Downloads`.</span></span> <span data-ttu-id="f92b5-118">(También se proporcionan paquetes .ZIP en la [página de descargas de Azure de Azul](https://www.azul.com/downloads/azure-only/zulu/)).</span><span class="sxs-lookup"><span data-stu-id="f92b5-118">(.ZIP packages are also provided on [Azul's Azure downloads page](https://www.azul.com/downloads/azure-only/zulu/).)</span></span>

2. <span data-ttu-id="f92b5-119">Vaya al directorio y haga doble clic en el archivo MSI descargado para comenzar la instalación.</span><span class="sxs-lookup"><span data-stu-id="f92b5-119">Navigate to the directory and double-click the downloaded MSI file to begin installation.</span></span>

## <a name="download-and-install-the-azul-zulu-jdks-for-mac"></a><span data-ttu-id="f92b5-120">Descarga e instalación de los JDK de Azul Zulu para Mac</span><span class="sxs-lookup"><span data-stu-id="f92b5-120">Download and install the Azul Zulu JDKs for Mac</span></span> 

<span data-ttu-id="f92b5-121">Estos pasos descargan un archivo ZIP en el equipo Mac.</span><span class="sxs-lookup"><span data-stu-id="f92b5-121">These steps download a ZIP file to your Mac.</span></span> <span data-ttu-id="f92b5-122">También hay disponible una versión DMG.</span><span class="sxs-lookup"><span data-stu-id="f92b5-122">There is also a DMG version available.</span></span>

1. <span data-ttu-id="f92b5-123">[Descargue JDK 8 de 64 bits de Azul Zulu como un archivo ZIP](https://repos.azul.com/azure-only/zulu/packages/zulu-11/11.0.3/zulu-11-azure-jdk_11.31.11-11.0.3-macosx_x64.zip) en una ubicación del cliente, como `/Library/Java/JavaVirtualMachines/`.</span><span class="sxs-lookup"><span data-stu-id="f92b5-123">[Download the 64-bit Azul Zulu JDK 8 as a ZIP file](https://repos.azul.com/azure-only/zulu/packages/zulu-11/11.0.3/zulu-11-azure-jdk_11.31.11-11.0.3-macosx_x64.zip) to a location on your client, such as `/Library/Java/JavaVirtualMachines/`.</span></span> <span data-ttu-id="f92b5-124">(También se proporcionan paquetes .DMG en la [página de descargas de Azure de Azul](https://www.azul.com/downloads/azure-only/zulu/)).</span><span class="sxs-lookup"><span data-stu-id="f92b5-124">(.DMG packages are also provided on [Azul's Azure downloads page](https://www.azul.com/downloads/azure-only/zulu/).)</span></span>

2. <span data-ttu-id="f92b5-125">Inicie Finder, vaya al directorio de descarga y haga doble clic en el archivo ZIP.</span><span class="sxs-lookup"><span data-stu-id="f92b5-125">Launch Finder, navigate to the download directory, and double-click the ZIP file.</span></span> <span data-ttu-id="f92b5-126">Como alternativa, puede iniciar una ventana de comandos de terminal; para ello, vaya al directorio y ejecute:</span><span class="sxs-lookup"><span data-stu-id="f92b5-126">Alternatively, you can launch a terminal command window, navigate to the directory, and run:</span></span>

```cli
unzip <name_of_zulu_package>.zip
```

## <a name="download-and-install-the-azul-zulu-jdks-for-alpine-linux"></a><span data-ttu-id="f92b5-127">Descarga e instalación de los JDK de Azul Zulu para Alpine Linux</span><span class="sxs-lookup"><span data-stu-id="f92b5-127">Download and install the Azul Zulu JDKs for Alpine Linux</span></span>

1. <span data-ttu-id="f92b5-128">[Descargue JDK 8 de 64 bits de Azul Zulu como un archivo TAR](https://repos.azul.com/azure-only/zulu/packages/zulu-11/11.0.3/zulu-11-azure-jdk_11.31.11-11.0.3-linux_x64.tar.gz) en una ubicación del cliente, como `/usr/lib/jvm`.</span><span class="sxs-lookup"><span data-stu-id="f92b5-128">[Download the 64-bit Azul Zulu JDK 8 as a TAR file](https://repos.azul.com/azure-only/zulu/packages/zulu-11/11.0.3/zulu-11-azure-jdk_11.31.11-11.0.3-linux_x64.tar.gz) to a location on your client, such as `/usr/lib/jvm`.</span></span> <span data-ttu-id="f92b5-129">(También se proporcionan paquetes .RPM y .DEB en la [página de descargas de Azure de Azul](https://www.azul.com/downloads/azure-only/zulu/)).</span><span class="sxs-lookup"><span data-stu-id="f92b5-129">(.RPM and .DEB packages are also provided on [Azul's Azure downloads page](https://www.azul.com/downloads/azure-only/zulu/).)</span></span>

2. <span data-ttu-id="f92b5-130">Vaya al directorio y ejecute el siguiente comando para descomprimir y expandir el archivo:</span><span class="sxs-lookup"><span data-stu-id="f92b5-130">Go to your directory and run the following command to unzip and expand the file:</span></span>

    ```cli
    tar -xvf <name_of_zulu_package>.tar
    ```

## <a name="confirm-your-installation"></a><span data-ttu-id="f92b5-131">Confirmación de la instalación</span><span class="sxs-lookup"><span data-stu-id="f92b5-131">Confirm your installation</span></span>

<span data-ttu-id="f92b5-132">Para confirmar la instalación, vaya a la línea de comandos y ejecute `java -version`.</span><span class="sxs-lookup"><span data-stu-id="f92b5-132">To confirm your installation, go to the command-line and run `java -version`.</span></span>

<span data-ttu-id="f92b5-133">La salida del comando debe ser:</span><span class="sxs-lookup"><span data-stu-id="f92b5-133">The output of the command should be:</span></span>

```cli
$ java -version

openjdk version "1.8.0_212"
OpenJDK Runtime Environment (Zulu 8.38.0.13-macosx)-Microsoft-Azure-restricted (build 1.8.0_212-b04)
OpenJDK 64-Bit Server VM (Zulu 8.38.0.13-macosx)-Microsoft-Azure-restricted (build 25.212-b04, mixed mode)

```

## <a name="download-and-install-the-azul-zulu-jdks-from-a-yum-repository"></a><span data-ttu-id="f92b5-134">Descarga e instalación de los JDK de Azul Zulu desde un repositorio Yum</span><span class="sxs-lookup"><span data-stu-id="f92b5-134">Download and install the Azul Zulu JDKs from a Yum repository</span></span>

<span data-ttu-id="f92b5-135">Azul proporciona los JDK de Azul Zulu en un [repositorio Yum](http://repos.azul.com/azure-only/zulu-azure.repo).</span><span class="sxs-lookup"><span data-stu-id="f92b5-135">The Azul Zulu JDKs are provided in a [Yum repository](http://repos.azul.com/azure-only/zulu-azure.repo) by Azul.</span></span>

<span data-ttu-id="f92b5-136">**Para instalar el JDK de Azul Zulu para Java 8, ejecute los siguientes comandos desde la CLI:**</span><span class="sxs-lookup"><span data-stu-id="f92b5-136">**To install the Azul Zulu JDK for Java 8, run the following commands from your CLI:**</span></span>

```cli
sudo rpm --import http://repos.azul.com/azul-repo.key
sudo curl http://repos.azul.com/azure-only/zulu-azure.repo -o /etc/yum.repos.d/zulu-azure.repo
sudo yum -q -y update
sudo yum -q -y install zulu-8-azure-jdk
```

<span data-ttu-id="f92b5-137">Para Java 11, ejecute:</span><span class="sxs-lookup"><span data-stu-id="f92b5-137">For Java 11, run:</span></span>

```cli
sudo rpm --import http://repos.azul.com/azul-repo.key
sudo curl http://repos.azul.com/azure-only/zulu-azure.repo -o /etc/yum.repos.d/zulu-azure.repo
sudo yum -q -y update
sudo yum -q -y install zulu-11-azure-jdk
```

<span data-ttu-id="f92b5-138">Para Java 12 (versión preliminar), ejecute:</span><span class="sxs-lookup"><span data-stu-id="f92b5-138">For Java 12 (Preview), run:</span></span>

```cli
sudo rpm --import http://repos.azul.com/azul-repo.key
sudo curl http://repos.azul.com/azure-only/zulu-azure.repo -o /etc/yum.repos.d/zulu-azure.repo
sudo yum -q -y update
sudo yum -q -y install zulu-12-azure-jdk
```

<span data-ttu-id="f92b5-139">**Para actualizar un paquete del JDK 8 de Zulu desde un repositorio Yum:**</span><span class="sxs-lookup"><span data-stu-id="f92b5-139">**To update a Zulu JDK 8 package from a Yum repository:**</span></span>

```cli
sudo yum -q -y install zulu-8-azure-jdk
```

<span data-ttu-id="f92b5-140">(Cambie el número de versión en el comando anterior si usa las versiones 11 o 12).</span><span class="sxs-lookup"><span data-stu-id="f92b5-140">(Change the version number in the command above if you are using versions 11 or 12.)</span></span>

<span data-ttu-id="f92b5-141">**Para eliminar un paquete del JDK 8 de Zulu desde un repositorio Yum:**</span><span class="sxs-lookup"><span data-stu-id="f92b5-141">**To remove a Zulu JDK 8 package from a Yum repository:**</span></span>

```cli
sudo yum -y erase zulu-8-azure-jdk
```
<span data-ttu-id="f92b5-142">(Cambie el número de versión en el comando anterior si usa las versiones 11 o 12).</span><span class="sxs-lookup"><span data-stu-id="f92b5-142">(Change the version number in the command above if you are using versions 11 or 12.)</span></span>

## <a name="download-and-install-the-azul-zulu-jdks-from-an-apt-get-repository"></a><span data-ttu-id="f92b5-143">Descarga e instalación de los JDK de Azul Zulu desde un repositorio apt-get</span><span class="sxs-lookup"><span data-stu-id="f92b5-143">Download and install the Azul Zulu JDKs from an apt-get repository</span></span>

<span data-ttu-id="f92b5-144">Azul proporciona los JDK de Azul Zulu en un [repositorio apt-get](http://repos.azul.com/azure-only/zulu/apt).</span><span class="sxs-lookup"><span data-stu-id="f92b5-144">The Azul Zulu JDKs are also provided in an [apt-get repository](http://repos.azul.com/azure-only/zulu/apt) by Azul.</span></span>

<span data-ttu-id="f92b5-145">**Para instalar el JDK de Azul Zulu para Java 8 con apt-get, ejecute los siguientes comandos desde la CLI:**</span><span class="sxs-lookup"><span data-stu-id="f92b5-145">**To install the Azul Zulu JDK for Java 8 with apt-get, run the following commands from your CLI:**</span></span>

```cli
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 0xB1998361219BD9C9
sudo apt-add-repository "deb http://repos.azul.com/azure-only/zulu/apt stable main"
sudo apt-get -q update
sudo apt-get -y install zulu-8-azure-jdk
```

<span data-ttu-id="f92b5-146">Para Java 11, ejecute:</span><span class="sxs-lookup"><span data-stu-id="f92b5-146">For Java 11, run:</span></span>

```cli
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 0xB1998361219BD9C9
sudo apt-add-repository "deb http://repos.azul.com/azure-only/zulu/apt stable main"
sudo apt-get -q update
sudo apt-get -y install zulu-11-azure-jdk
```

<span data-ttu-id="f92b5-147">Para Java 12 (versión preliminar), ejecute:</span><span class="sxs-lookup"><span data-stu-id="f92b5-147">For Java 12 (Preview), run:</span></span>

```cli
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 0xB1998361219BD9C9
sudo apt-add-repository "deb http://repos.azul.com/azure-only/zulu/apt stable main"
sudo apt-get -q update
sudo apt-get -y install zulu-12-azure-jdk
```

<span data-ttu-id="f92b5-148">**Para actualizar un paquete del JDK 8 de Zulu desde un repositorio apt-get:**</span><span class="sxs-lookup"><span data-stu-id="f92b5-148">**To update a Zulu JDK 8 package from an apt-get repository:**</span></span>

```cli
sudo apt-get -q update
sudo apt-get -y install zulu-8-azure-jdk
```

<span data-ttu-id="f92b5-149">Se eliminará automáticamente la versión anterior.</span><span class="sxs-lookup"><span data-stu-id="f92b5-149">The previous release will be automatically removed.</span></span>
<span data-ttu-id="f92b5-150">(Cambie el número de versión en el comando anterior si usa las versiones 11 o 12).</span><span class="sxs-lookup"><span data-stu-id="f92b5-150">(Change the version number in the command above if you are using versions 11 or 12.)</span></span>

<span data-ttu-id="f92b5-151">**Para eliminar un paquete del JDK 8 de Zulu desde un repositorio apt-get:**</span><span class="sxs-lookup"><span data-stu-id="f92b5-151">**To remove a Zulu JDK 8 package from an apt-get repository:**</span></span>

```cli
sudo apt-get -y purge zulu-8-azure-jdk
```

<span data-ttu-id="f92b5-152">(Cambie el número de versión en el comando anterior si usa las versiones 11 o 12).</span><span class="sxs-lookup"><span data-stu-id="f92b5-152">(Change the version number in the command above if you are using versions 11 or 12.)</span></span>

<span data-ttu-id="f92b5-153">Para más instrucciones acerca de cómo preparar, instalar y administrar los JDK de Azul Zulu para el desarrollo en Azure, consulte [la documentación oficial de Zulu](https://docs.azul.com/zulu/zuludocs/index.htm).</span><span class="sxs-lookup"><span data-stu-id="f92b5-153">For more detailed guidance on preparing, installing, and managing your Azul Zulu JDKs for Azure development, read [the official Zulu docs](https://docs.azul.com/zulu/zuludocs/index.htm).</span></span>

