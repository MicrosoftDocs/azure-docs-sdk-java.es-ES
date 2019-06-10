---
title: JDK de Java y soporte técnico a largo plazo para el desarrollo en Azure
description: Descargas e instrucciones del equipo de soporte técnico de Azure para el desarrollo y ejecución de aplicaciones Java.
author: bmitchell287
manager: douge
ms.devlang: java
ms.topic: conceptual
ms.date: 04/09/2019
ms.author: brendm
ms.openlocfilehash: 340f6149ffe39ccbb2d7de534ed63b8784d1f63a
ms.sourcegitcommit: 394521c47ac9895d00d9f97535cc9d1e27d08fe9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/28/2019
ms.locfileid: "66270884"
---
# <a name="java-long-term-support-for-azure-and-azure-stack"></a><span data-ttu-id="1a858-103">Soporte técnico a largo plazo de Java para Azure y Azure Stack</span><span class="sxs-lookup"><span data-stu-id="1a858-103">Java Long-Term Support for Azure and Azure Stack</span></span>

<span data-ttu-id="1a858-104">Los desarrolladores Java que trabajan con Azure y Azure Stack pueden crear y ejecutar aplicaciones Java de producción con [compilaciones de Azul Zulu Enterprise para Azure](https://www.azul.com/downloads/azure-only/zulu/) sin incurrir en costos de soporte técnico adicionales.</span><span class="sxs-lookup"><span data-stu-id="1a858-104">Java developers on Azure and Azure Stack can build and run production Java applications using [Azul Zulu Enterprise for Azure](https://www.azul.com/downloads/azure-only/zulu/) without incurring additional support costs.</span></span> <span data-ttu-id="1a858-105">Puede usar cualquier entorno de ejecución de Java que desee en Azure, pero cuando se usa Zulu se obtienen actualizaciones de mantenimiento gratuitas y se pueden abrir incidencias de soporte técnico con Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1a858-105">You can use any Java runtime you want on Azure, but when you use Zulu you get free maintenance updates and can create support issues with Microsoft.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1a858-106">Descarga e instalación de Java</span><span class="sxs-lookup"><span data-stu-id="1a858-106">Download and install Java</span></span>](java-jdk-install.md)

## <a name="long-term-support-lts"></a><span data-ttu-id="1a858-107">Soporte técnico a largo plazo (LTS)</span><span class="sxs-lookup"><span data-stu-id="1a858-107">Long-term support (LTS)</span></span>

* [<span data-ttu-id="1a858-108">Java 11</span><span class="sxs-lookup"><span data-stu-id="1a858-108">Java 11</span></span>](https://www.azul.com/downloads/azure-only/zulu/#java11)
* [<span data-ttu-id="1a858-109">Java 8</span><span class="sxs-lookup"><span data-stu-id="1a858-109">Java 8</span></span>](https://www.azul.com/downloads/azure-only/zulu/#java8)
* [<span data-ttu-id="1a858-110">Java 7</span><span class="sxs-lookup"><span data-stu-id="1a858-110">Java 7</span></span>](https://www.azul.com/downloads/azure-only/zulu/#java7)

## <a name="technical-preview"></a><span data-ttu-id="1a858-111">Versión preliminar técnica</span><span class="sxs-lookup"><span data-stu-id="1a858-111">Technical preview</span></span>

* [<span data-ttu-id="1a858-112">Java 12</span><span class="sxs-lookup"><span data-stu-id="1a858-112">Java 12</span></span>](https://www.azul.com/downloads/azure-only/zulu/#java12)

## <a name="what-is-the-zulu-openjdk-for-azure"></a><span data-ttu-id="1a858-113">¿Qué es el OpenJDK de Zulu para Azure?</span><span class="sxs-lookup"><span data-stu-id="1a858-113">What is the Zulu OpenJDK for Azure?</span></span>

<span data-ttu-id="1a858-114">Las compilaciones del OpenJDK de Azul Zulu Enterprise son una distribución gratuita, multiplataforma y lista para producción del OpenJDK para Azure y Azure Stack respaldado por Microsoft y Azul Systems.</span><span class="sxs-lookup"><span data-stu-id="1a858-114">Azul Zulu Enterprise builds of OpenJDK are a no-cost, multi-platform, production-ready distribution of the OpenJDK for Azure and Azure Stack backed by Microsoft and Azul Systems.</span></span> <span data-ttu-id="1a858-115">Estas distribuciones son:</span><span class="sxs-lookup"><span data-stu-id="1a858-115">These distributions are:</span></span>

* <span data-ttu-id="1a858-116">Compilaciones 100% código abierto del OpenJDK empaquetado como Kits de desarrollo de Java (JDK), entornos de ejecución de Java (JRE) y versiones desatendidas de JRE.</span><span class="sxs-lookup"><span data-stu-id="1a858-116">100% open source builds of OpenJDK packaged as Java Development Kits (JDKs), Java Runtime Environments (JREs), and Headless JREs.</span></span> <span data-ttu-id="1a858-117">Estos archivos binarios son totalmente compatibles con las compilaciones comerciales de Java Standard Edition (SE) que se pueden usar con aplicaciones de Java o componentes de Azure y Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="1a858-117">These binaries are fully compatible and compliant commercial builds of Java Standard Edition (SE) that can be used with Java applications or components on Azure and Azure Stack.</span></span>
* <span data-ttu-id="1a858-118">Se proporcionan con soporte técnico a largo plazo, incluidas las correcciones de errores, las mejoras de rendimiento y las revisiones de seguridad.</span><span class="sxs-lookup"><span data-stu-id="1a858-118">Provided with long-term support including bug fixes, performance enhancements, and security patches.</span></span>
* <span data-ttu-id="1a858-119">Están disponibles para desarrollar y ejecutar aplicaciones de Java en Windows, Linux y MacOS.</span><span class="sxs-lookup"><span data-stu-id="1a858-119">Available for developing and running Java applications on Windows, Linux, and MacOS.</span></span>
* <span data-ttu-id="1a858-120">Están disponibles como imágenes de contenedor en Docker Hub y como máquinas virtuales (Windows y Linux) en Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="1a858-120">Available as container images on Docker Hub and as virtual machines (Windows and Linux) on Azure Marketplace.</span></span>
* <span data-ttu-id="1a858-121">Son utilizadas por Microsoft Azure para posibilitar muchos servicios de Azure, como:</span><span class="sxs-lookup"><span data-stu-id="1a858-121">Used by Microsoft Azure to power many Azure services, such as:</span></span>
  * <span data-ttu-id="1a858-122">App Service en Windows</span><span class="sxs-lookup"><span data-stu-id="1a858-122">App Service Windows</span></span>
  * <span data-ttu-id="1a858-123">App Service en Linux</span><span class="sxs-lookup"><span data-stu-id="1a858-123">App Service Linux</span></span>
  * <span data-ttu-id="1a858-124">Functions</span><span class="sxs-lookup"><span data-stu-id="1a858-124">Functions</span></span>
  * <span data-ttu-id="1a858-125">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="1a858-125">Service Fabric</span></span>
  * <span data-ttu-id="1a858-126">HDInsight</span><span class="sxs-lookup"><span data-stu-id="1a858-126">HDInsight</span></span>
  * <span data-ttu-id="1a858-127">Search</span><span class="sxs-lookup"><span data-stu-id="1a858-127">Search</span></span>
  * <span data-ttu-id="1a858-128">Azure DevOps</span><span class="sxs-lookup"><span data-stu-id="1a858-128">Azure DevOps</span></span>
  * <span data-ttu-id="1a858-129">Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="1a858-129">Cloud Shell</span></span>  

## <a name="supported-java-versions-and-update-schedule"></a><span data-ttu-id="1a858-130">Versiones de Java admitidas y programación de actualizaciones</span><span class="sxs-lookup"><span data-stu-id="1a858-130">Supported Java versions and update schedule</span></span>

<span data-ttu-id="1a858-131">Azul Systems proporciona [compilaciones de Zulu Enterprise del OpenJDK para Microsoft Azure](https://www.azul.com/downloads/azure-only/zulu/) con soporte técnico completo para todas las versiones de Java con soporte técnico a largo plazo (LTS), a partir de Java SE 7, 8 y 11.</span><span class="sxs-lookup"><span data-stu-id="1a858-131">Azul Systems provides fully-supported [Zulu Enterprise builds of OpenJDK for Microsoft Azure](https://www.azul.com/downloads/azure-only/zulu/) for all long-term support (LTS) versions of Java, starting with Java SE 7, 8, and 11.</span></span> <span data-ttu-id="1a858-132">Encontrará más información en la [nota de prensa de Azul](https://www.azul.com/press_release/free-java-production-support-for-microsoft-azure-azure-stack).</span><span class="sxs-lookup"><span data-stu-id="1a858-132">More information can be found in the [Azul press release](https://www.azul.com/press_release/free-java-production-support-for-microsoft-azure-azure-stack).</span></span>

|<span data-ttu-id="1a858-133">Java SE LTS</span><span class="sxs-lookup"><span data-stu-id="1a858-133">Java SE LTS</span></span>  |<span data-ttu-id="1a858-134">Soporte técnico hasta</span><span class="sxs-lookup"><span data-stu-id="1a858-134">Support until</span></span>  |
|---------|----------|
|<span data-ttu-id="1a858-135">[![Java 7](../media/jdk/java-7.png)](https://www.azul.com/downloads/azure-only/zulu/#java7)</span><span class="sxs-lookup"><span data-stu-id="1a858-135">[![Java 7](../media/jdk/java-7.png)](https://www.azul.com/downloads/azure-only/zulu/#java7)</span></span> |<span data-ttu-id="1a858-136">Julio de 2023</span><span class="sxs-lookup"><span data-stu-id="1a858-136">July 2023</span></span> |
|<span data-ttu-id="1a858-137">[![Java 8](../media/jdk/java-8.png)](https://www.azul.com/downloads/azure-only/zulu/#java8)</span><span class="sxs-lookup"><span data-stu-id="1a858-137">[![Java 8](../media/jdk/java-8.png)](https://www.azul.com/downloads/azure-only/zulu/#java8)</span></span> |<span data-ttu-id="1a858-138">Marzo de 2025</span><span class="sxs-lookup"><span data-stu-id="1a858-138">March 2025</span></span>|
|<span data-ttu-id="1a858-139">[![Java 11](../media/jdk/java-11.png)](https://www.azul.com/downloads/azure-only/zulu/#java11)</span><span class="sxs-lookup"><span data-stu-id="1a858-139">[![Java 11](../media/jdk/java-11.png)](https://www.azul.com/downloads/azure-only/zulu/#java11)</span></span> |<span data-ttu-id="1a858-140">Septiembre de 2026</span><span class="sxs-lookup"><span data-stu-id="1a858-140">Sept. 2026</span></span>|
|<span data-ttu-id="1a858-141">[![Java 12](../media/jdk/java-12.png)]()</span><span class="sxs-lookup"><span data-stu-id="1a858-141">[![Java 12](../media/jdk/java-12.png)]()</span></span> |<span data-ttu-id="1a858-142">**Versión preliminar**</span><span class="sxs-lookup"><span data-stu-id="1a858-142">**PREVIEW**</span></span>|

<span data-ttu-id="1a858-143">Estas versiones del JDK tienen actualizaciones de seguridad trimestrales, correcciones de errores, así como actualizaciones críticas y revisiones fuera de banda según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="1a858-143">These JDK releases have quarterly security updates, bug fixes, and critical out-of-band updates and patches as needed.</span></span>  <span data-ttu-id="1a858-144">Este soporte técnico incluye el traslado a versiones anteriores de las actualizaciones de seguridad y las correcciones de errores para Java 7 y 8 notificadas en las versiones más recientes de Java, como Java 11 y garantiza la continuidad de la estabilidad y seguridad de las versiones anteriores de Java.</span><span class="sxs-lookup"><span data-stu-id="1a858-144">This support includes back ports of security updates and bug fixes to Java 7 and 8 reported in newer versions of Java such as Java 11, which ensures the continued stability and security of older versions of Java.</span></span>  <span data-ttu-id="1a858-145">Los clientes de Azure tienen derecho a estas actualizaciones de seguridad y a las correcciones de errores de la plataforma sin incurrir en cuotas de suscripción a Java SE no planeadas.</span><span class="sxs-lookup"><span data-stu-id="1a858-145">Azure customers can get these security updates and platform bug fixes without incurring any unplanned Java SE subscription fees.</span></span>

<span data-ttu-id="1a858-146">Azul Systems mantiene una [hoja de ruta de Java SE](https://www.azul.com/products/azul_support_roadmap/) para estas versiones.</span><span class="sxs-lookup"><span data-stu-id="1a858-146">Azul Systems maintains a [Java SE roadmap](https://www.azul.com/products/azul_support_roadmap/) for these releases.</span></span>

## <a name="benefits-for-developers"></a><span data-ttu-id="1a858-147">Ventajas para desarrolladores</span><span class="sxs-lookup"><span data-stu-id="1a858-147">Benefits for developers</span></span>

<span data-ttu-id="1a858-148">Las versiones del JDK de Azul Zulu:</span><span class="sxs-lookup"><span data-stu-id="1a858-148">The Azul Zulu JDK releases are:</span></span>

1. <span data-ttu-id="1a858-149">Tienen el respaldo y soporte técnico de Microsoft y Azul Systems</span><span class="sxs-lookup"><span data-stu-id="1a858-149">Backed and supported by both Microsoft and Azul Systems</span></span>

   * <span data-ttu-id="1a858-150">Los archivos binarios de Zulu están listos para producción y están respaldados por Microsoft y Azul Systems</span><span class="sxs-lookup"><span data-stu-id="1a858-150">Zulu binaries are production-ready and backed by Microsoft and Azul Systems</span></span>
   * <span data-ttu-id="1a858-151">Zulu incluye soporte técnico a largo plazo (LTS) sin costo para Java 7, 8 y 11.</span><span class="sxs-lookup"><span data-stu-id="1a858-151">Zulu comes with zero-cost long-term support (LTS) for Java 7, 8, and 11.</span></span> <span data-ttu-id="1a858-152">(Se proporcionará también LTS para Java 17).</span><span class="sxs-lookup"><span data-stu-id="1a858-152">(LTS will be provided for Java 17, as well).</span></span> <span data-ttu-id="1a858-153">Puede actualizar las versiones de Java solo cuando lo necesite.</span><span class="sxs-lookup"><span data-stu-id="1a858-153">You can upgrade Java versions only when you need to.</span></span>
   * <span data-ttu-id="1a858-154">Java 7 admitido hasta julio de 2023.</span><span class="sxs-lookup"><span data-stu-id="1a858-154">Java 7 supported until July 2023.</span></span> <span data-ttu-id="1a858-155">Java 8 y 11 admitidos más allá de 2024.</span><span class="sxs-lookup"><span data-stu-id="1a858-155">Java 8 and 11 are supported beyond 2024.</span></span>
   * <span data-ttu-id="1a858-156">Microsoft se compromete a ejecutan Zulu internamente en máquinas que posibilitan muchos servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="1a858-156">Microsoft is committed to running Zulu internally on machines that power many Azure services.</span></span>

2. <span data-ttu-id="1a858-157">Para entornos de producción</span><span class="sxs-lookup"><span data-stu-id="1a858-157">Production-ready</span></span>

   * <span data-ttu-id="1a858-158">100 % código abierto para sus compilaciones del OpenJDK.</span><span class="sxs-lookup"><span data-stu-id="1a858-158">100% open-source for its builds of OpenJDK.</span></span>
   * <span data-ttu-id="1a858-159">Sustituciones inmediatas para muchas distribuciones de Java SE.</span><span class="sxs-lookup"><span data-stu-id="1a858-159">Drop-in replacements for many Java SE distributions.</span></span>
   * <span data-ttu-id="1a858-160">JDK, JRE y JRE desatendido</span><span class="sxs-lookup"><span data-stu-id="1a858-160">JDK, JRE, and JRE-headless</span></span>
   * <span data-ttu-id="1a858-161">Java 7, 8 y 11</span><span class="sxs-lookup"><span data-stu-id="1a858-161">Java 7, 8, and 11</span></span>
   * <span data-ttu-id="1a858-162">Comprobada la compatibilidad con las especificaciones de Java SE mediante el Kit de compatibilidad de tecnología (TCK) de la Comunidad OpenJDK.</span><span class="sxs-lookup"><span data-stu-id="1a858-162">Verified compliant with the Java SE  specifications using the OpenJDK Community Technology Compatibility Kit (TCK).</span></span>
   * <span data-ttu-id="1a858-163">Los desarrolladores seguirán recibiendo actualizaciones de producción para Java SE, incluidas correcciones de errores, mejoras de rendimiento y revisiones de seguridad para Java SE 7, 8 y 11.</span><span class="sxs-lookup"><span data-stu-id="1a858-163">Developers will continue to receive production updates for Java SE, including bug fixes, performance enhancements, and security patches for Java SE 7, 8, and 11.</span></span>

3. <span data-ttu-id="1a858-164">Compatible con varias plataformas.</span><span class="sxs-lookup"><span data-stu-id="1a858-164">Supported for multi-platform.</span></span> <span data-ttu-id="1a858-165">Zulu es compatible con los archivos binarios de varias plataformas y versiones, incluidas:</span><span class="sxs-lookup"><span data-stu-id="1a858-165">Zulu supports binaries for multiple platforms and versions, including:</span></span>

   * <span data-ttu-id="1a858-166">Cliente Windows</span><span class="sxs-lookup"><span data-stu-id="1a858-166">Windows Client</span></span>
     * <span data-ttu-id="1a858-167">10</span><span class="sxs-lookup"><span data-stu-id="1a858-167">10</span></span>
     * <span data-ttu-id="1a858-168">8.1</span><span class="sxs-lookup"><span data-stu-id="1a858-168">8.1</span></span>
     * <span data-ttu-id="1a858-169">8, 7</span><span class="sxs-lookup"><span data-stu-id="1a858-169">8, 7</span></span>
   * <span data-ttu-id="1a858-170">Windows Server</span><span class="sxs-lookup"><span data-stu-id="1a858-170">Windows Server</span></span>
     * <span data-ttu-id="1a858-171">2016 R2</span><span class="sxs-lookup"><span data-stu-id="1a858-171">2016R2</span></span>
     * <span data-ttu-id="1a858-172">2016</span><span class="sxs-lookup"><span data-stu-id="1a858-172">2016</span></span>
     * <span data-ttu-id="1a858-173">2012 R2</span><span class="sxs-lookup"><span data-stu-id="1a858-173">2012 R2</span></span>
     * <span data-ttu-id="1a858-174">2012</span><span class="sxs-lookup"><span data-stu-id="1a858-174">2012</span></span>
     * <span data-ttu-id="1a858-175">2008 R2</span><span class="sxs-lookup"><span data-stu-id="1a858-175">2008 R2</span></span>
   * <span data-ttu-id="1a858-176">Linux, incluidas</span><span class="sxs-lookup"><span data-stu-id="1a858-176">Linux, including</span></span>
     * <span data-ttu-id="1a858-177">RHEL</span><span class="sxs-lookup"><span data-stu-id="1a858-177">RHEL</span></span>
     * <span data-ttu-id="1a858-178">CentOS</span><span class="sxs-lookup"><span data-stu-id="1a858-178">CentOS</span></span>
     * <span data-ttu-id="1a858-179">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="1a858-179">Ubuntu</span></span>
     * <span data-ttu-id="1a858-180">SLES</span><span class="sxs-lookup"><span data-stu-id="1a858-180">SLES</span></span>
     * <span data-ttu-id="1a858-181">Debian</span><span class="sxs-lookup"><span data-stu-id="1a858-181">Debian</span></span>
     * <span data-ttu-id="1a858-182">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="1a858-182">Oracle Linux</span></span>
   * <span data-ttu-id="1a858-183">Mac OS X</span><span class="sxs-lookup"><span data-stu-id="1a858-183">Mac OS X</span></span>
   * <span data-ttu-id="1a858-184">se entrega en varios tipos de paquetes:</span><span class="sxs-lookup"><span data-stu-id="1a858-184">delivered in multiple package types:</span></span>
     * <span data-ttu-id="1a858-185">MSI, ZIP, TAR, DEB, RPM y DMG</span><span class="sxs-lookup"><span data-stu-id="1a858-185">MSI, ZIP, TAR, DEB, RPM, and DMG</span></span>

    <span data-ttu-id="1a858-186">Están disponibles en Docker imágenes de contenedor de Docker certificadas para el JDK, JRE y JRE desatendido en varias imágenes de sistema operativo base.</span><span class="sxs-lookup"><span data-stu-id="1a858-186">Certified Docker container images for Zulu JDK, JRE, and JRE-headless on multiple base OS images are available at Docker.</span></span>

    <span data-ttu-id="1a858-187">Centro:</span><span class="sxs-lookup"><span data-stu-id="1a858-187">Hub:</span></span>

    * [<span data-ttu-id="1a858-188">JDK</span><span class="sxs-lookup"><span data-stu-id="1a858-188">JDK</span></span>](https://hub.docker.com/_/microsoft-java-jdk)
    * [<span data-ttu-id="1a858-189">JRE</span><span class="sxs-lookup"><span data-stu-id="1a858-189">JRE</span></span>](https://hub.docker.com/_/microsoft-java-jre)
    * [<span data-ttu-id="1a858-190">JRE desatendido</span><span class="sxs-lookup"><span data-stu-id="1a858-190">JRE-headless</span></span>](https://hub.docker.com/_/microsoft-java-jre-headless)

4. <span data-ttu-id="1a858-191">Sin costo</span><span class="sxs-lookup"><span data-stu-id="1a858-191">No cost</span></span>

   * <span data-ttu-id="1a858-192">Microsoft proporciona todo lo que necesita para crear y escalar aplicaciones de Java en Azure sin costo para usted.</span><span class="sxs-lookup"><span data-stu-id="1a858-192">Microsoft provides everything you need to build and scale Java apps on Azure at no cost to you.</span></span> <span data-ttu-id="1a858-193">A través de Zulu recibirá actualizaciones de seguridad gratuitas y correcciones de errores de la plataforma para las aplicaciones de Java sin cargos.</span><span class="sxs-lookup"><span data-stu-id="1a858-193">Through Zulu you'll receive free security updates and platform bug fixes for Java apps without any fees.</span></span>
   * <span data-ttu-id="1a858-194">[Java Flight Recorder y Mission Control](java-jdk-flight-recorder-and-mission-control.md) están disponibles en las versiones de Zulu Java 8, 11 y 12 (versión preliminar).</span><span class="sxs-lookup"><span data-stu-id="1a858-194">[Java Flight Recorder and Mission Control](java-jdk-flight-recorder-and-mission-control.md) are available in Zulu Java 8, 11, and 12 (Preview).</span></span>

5. <span data-ttu-id="1a858-195">Versión preliminar técnica de versiones que no son LTS</span><span class="sxs-lookup"><span data-stu-id="1a858-195">Tech Preview of Non-LTS versions</span></span>

   * <span data-ttu-id="1a858-196">Las versiones preliminares técnicas proporcionan oportunidades para probar progresivamente nuevas características que se entregan en versiones a corto plazo que finalmente se convertirán en Java 17 LTS.</span><span class="sxs-lookup"><span data-stu-id="1a858-196">Tech previews provide you with opportunities to progressively test new features as they are delivered in short-term versions that will eventually graduate to Java 17 LTS.</span></span>

6. <span data-ttu-id="1a858-197">Los cambios en OpenJDK se transmiten hacia arriba</span><span class="sxs-lookup"><span data-stu-id="1a858-197">Changes to OpenJDK are up-streamed</span></span>

   * <span data-ttu-id="1a858-198">Los autores de Azul Systems insertan los cambios de Zulu en OpenJDK, lo que hace que el repositorio de nivel superior sea completo e inclusivo.</span><span class="sxs-lookup"><span data-stu-id="1a858-198">Azul Systems committers push Zulu changes to OpenJDK which makes the upstream repo comprehensive and inclusive.</span></span>

<span data-ttu-id="1a858-199">Como siempre, los desarrolladores de Java pueden traer sus propios entornos de ejecución de Java, incluidos Oracle JDK y Red Hat JDK, a Azure y aprovechar esta infraestructura segura y con servicios muy completos.</span><span class="sxs-lookup"><span data-stu-id="1a858-199">As always, Java developers can bring their own Java run-times, including Oracle JDK and Red Hat JDK, to Azure and use  the secure infrastructure and feature-rich services.</span></span> <span data-ttu-id="1a858-200">La edición para producción de Oracle Java SE también está disponible para que los desarrolladores de Java ejecuten cargas de trabajo de Java en máquinas virtuales Windows o Linux en Azure.</span><span class="sxs-lookup"><span data-stu-id="1a858-200">The production edition of Oracle Java SE is also available to Java developers for running Java workloads in Windows or Linux virtual machines on Azure.</span></span>

## <a name="use-for-local-development"></a><span data-ttu-id="1a858-201">Uso para desarrollo local</span><span class="sxs-lookup"><span data-stu-id="1a858-201">Use for local development</span></span> 

<span data-ttu-id="1a858-202">Los desarrolladores pueden [descargar](https://www.azul.com/downloads/azure-only/zulu/) los JDK de Java para Azure y Azure Stack para usarlos en los entornos de desarrollo locales.</span><span class="sxs-lookup"><span data-stu-id="1a858-202">Developers can [download](https://www.azul.com/downloads/azure-only/zulu/) Java JDKs for Azure and Azure Stack for use in local development environments.</span></span> <span data-ttu-id="1a858-203">Las descargas están disponibles para Windows, Linux y macOS.</span><span class="sxs-lookup"><span data-stu-id="1a858-203">Downloads are available for Windows, Linux, and macOS.</span></span> <span data-ttu-id="1a858-204">Los desarrolladores que trabajan en Linux también pueden obtener los paquetes mediante los administradores de paquetes [yum](https://www.azul.com/downloads/azure-only/zulu/#yum-repo) y [apt](https://www.azul.com/downloads/azure-only/zulu/#apt-repo).</span><span class="sxs-lookup"><span data-stu-id="1a858-204">Developers working on Linux can also get packages through the [yum](https://www.azul.com/downloads/azure-only/zulu/#yum-repo) and [apt](https://www.azul.com/downloads/azure-only/zulu/#apt-repo) package managers.</span></span>

<span data-ttu-id="1a858-205">Para más información, consulte [Imágenes de Docker para Azure](java-jdk-docker-images.md).</span><span class="sxs-lookup"><span data-stu-id="1a858-205">For additional guidance see [Docker images for Azure](java-jdk-docker-images.md).</span></span>