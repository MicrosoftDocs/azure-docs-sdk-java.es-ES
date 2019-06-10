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
# <a name="java-long-term-support-for-azure-and-azure-stack"></a>Soporte técnico a largo plazo de Java para Azure y Azure Stack

Los desarrolladores Java que trabajan con Azure y Azure Stack pueden crear y ejecutar aplicaciones Java de producción con [compilaciones de Azul Zulu Enterprise para Azure](https://www.azul.com/downloads/azure-only/zulu/) sin incurrir en costos de soporte técnico adicionales. Puede usar cualquier entorno de ejecución de Java que desee en Azure, pero cuando se usa Zulu se obtienen actualizaciones de mantenimiento gratuitas y se pueden abrir incidencias de soporte técnico con Microsoft.

> [!div class="nextstepaction"]
> [Descarga e instalación de Java](java-jdk-install.md)

## <a name="long-term-support-lts"></a>Soporte técnico a largo plazo (LTS)

* [Java 11](https://www.azul.com/downloads/azure-only/zulu/#java11)
* [Java 8](https://www.azul.com/downloads/azure-only/zulu/#java8)
* [Java 7](https://www.azul.com/downloads/azure-only/zulu/#java7)

## <a name="technical-preview"></a>Versión preliminar técnica

* [Java 12](https://www.azul.com/downloads/azure-only/zulu/#java12)

## <a name="what-is-the-zulu-openjdk-for-azure"></a>¿Qué es el OpenJDK de Zulu para Azure?

Las compilaciones del OpenJDK de Azul Zulu Enterprise son una distribución gratuita, multiplataforma y lista para producción del OpenJDK para Azure y Azure Stack respaldado por Microsoft y Azul Systems. Estas distribuciones son:

* Compilaciones 100% código abierto del OpenJDK empaquetado como Kits de desarrollo de Java (JDK), entornos de ejecución de Java (JRE) y versiones desatendidas de JRE. Estos archivos binarios son totalmente compatibles con las compilaciones comerciales de Java Standard Edition (SE) que se pueden usar con aplicaciones de Java o componentes de Azure y Azure Stack.
* Se proporcionan con soporte técnico a largo plazo, incluidas las correcciones de errores, las mejoras de rendimiento y las revisiones de seguridad.
* Están disponibles para desarrollar y ejecutar aplicaciones de Java en Windows, Linux y MacOS.
* Están disponibles como imágenes de contenedor en Docker Hub y como máquinas virtuales (Windows y Linux) en Azure Marketplace.
* Son utilizadas por Microsoft Azure para posibilitar muchos servicios de Azure, como:
  * App Service en Windows
  * App Service en Linux
  * Functions
  * Service Fabric
  * HDInsight
  * Search
  * Azure DevOps
  * Cloud Shell  

## <a name="supported-java-versions-and-update-schedule"></a>Versiones de Java admitidas y programación de actualizaciones

Azul Systems proporciona [compilaciones de Zulu Enterprise del OpenJDK para Microsoft Azure](https://www.azul.com/downloads/azure-only/zulu/) con soporte técnico completo para todas las versiones de Java con soporte técnico a largo plazo (LTS), a partir de Java SE 7, 8 y 11. Encontrará más información en la [nota de prensa de Azul](https://www.azul.com/press_release/free-java-production-support-for-microsoft-azure-azure-stack).

|Java SE LTS  |Soporte técnico hasta  |
|---------|----------|
|[![Java 7](../media/jdk/java-7.png)](https://www.azul.com/downloads/azure-only/zulu/#java7) |Julio de 2023 |
|[![Java 8](../media/jdk/java-8.png)](https://www.azul.com/downloads/azure-only/zulu/#java8) |Marzo de 2025|
|[![Java 11](../media/jdk/java-11.png)](https://www.azul.com/downloads/azure-only/zulu/#java11) |Septiembre de 2026|
|[![Java 12](../media/jdk/java-12.png)]() |**Versión preliminar**|

Estas versiones del JDK tienen actualizaciones de seguridad trimestrales, correcciones de errores, así como actualizaciones críticas y revisiones fuera de banda según sea necesario.  Este soporte técnico incluye el traslado a versiones anteriores de las actualizaciones de seguridad y las correcciones de errores para Java 7 y 8 notificadas en las versiones más recientes de Java, como Java 11 y garantiza la continuidad de la estabilidad y seguridad de las versiones anteriores de Java.  Los clientes de Azure tienen derecho a estas actualizaciones de seguridad y a las correcciones de errores de la plataforma sin incurrir en cuotas de suscripción a Java SE no planeadas.

Azul Systems mantiene una [hoja de ruta de Java SE](https://www.azul.com/products/azul_support_roadmap/) para estas versiones.

## <a name="benefits-for-developers"></a>Ventajas para desarrolladores

Las versiones del JDK de Azul Zulu:

1. Tienen el respaldo y soporte técnico de Microsoft y Azul Systems

   * Los archivos binarios de Zulu están listos para producción y están respaldados por Microsoft y Azul Systems
   * Zulu incluye soporte técnico a largo plazo (LTS) sin costo para Java 7, 8 y 11. (Se proporcionará también LTS para Java 17). Puede actualizar las versiones de Java solo cuando lo necesite.
   * Java 7 admitido hasta julio de 2023. Java 8 y 11 admitidos más allá de 2024.
   * Microsoft se compromete a ejecutan Zulu internamente en máquinas que posibilitan muchos servicios de Azure.

2. Para entornos de producción

   * 100 % código abierto para sus compilaciones del OpenJDK.
   * Sustituciones inmediatas para muchas distribuciones de Java SE.
   * JDK, JRE y JRE desatendido
   * Java 7, 8 y 11
   * Comprobada la compatibilidad con las especificaciones de Java SE mediante el Kit de compatibilidad de tecnología (TCK) de la Comunidad OpenJDK.
   * Los desarrolladores seguirán recibiendo actualizaciones de producción para Java SE, incluidas correcciones de errores, mejoras de rendimiento y revisiones de seguridad para Java SE 7, 8 y 11.

3. Compatible con varias plataformas. Zulu es compatible con los archivos binarios de varias plataformas y versiones, incluidas:

   * Cliente Windows
     * 10
     * 8.1
     * 8, 7
   * Windows Server
     * 2016 R2
     * 2016
     * 2012 R2
     * 2012
     * 2008 R2
   * Linux, incluidas
     * RHEL
     * CentOS
     * Ubuntu
     * SLES
     * Debian
     * Oracle Linux
   * Mac OS X
   * se entrega en varios tipos de paquetes:
     * MSI, ZIP, TAR, DEB, RPM y DMG

    Están disponibles en Docker imágenes de contenedor de Docker certificadas para el JDK, JRE y JRE desatendido en varias imágenes de sistema operativo base.

    Centro:

    * [JDK](https://hub.docker.com/_/microsoft-java-jdk)
    * [JRE](https://hub.docker.com/_/microsoft-java-jre)
    * [JRE desatendido](https://hub.docker.com/_/microsoft-java-jre-headless)

4. Sin costo

   * Microsoft proporciona todo lo que necesita para crear y escalar aplicaciones de Java en Azure sin costo para usted. A través de Zulu recibirá actualizaciones de seguridad gratuitas y correcciones de errores de la plataforma para las aplicaciones de Java sin cargos.
   * [Java Flight Recorder y Mission Control](java-jdk-flight-recorder-and-mission-control.md) están disponibles en las versiones de Zulu Java 8, 11 y 12 (versión preliminar).

5. Versión preliminar técnica de versiones que no son LTS

   * Las versiones preliminares técnicas proporcionan oportunidades para probar progresivamente nuevas características que se entregan en versiones a corto plazo que finalmente se convertirán en Java 17 LTS.

6. Los cambios en OpenJDK se transmiten hacia arriba

   * Los autores de Azul Systems insertan los cambios de Zulu en OpenJDK, lo que hace que el repositorio de nivel superior sea completo e inclusivo.

Como siempre, los desarrolladores de Java pueden traer sus propios entornos de ejecución de Java, incluidos Oracle JDK y Red Hat JDK, a Azure y aprovechar esta infraestructura segura y con servicios muy completos. La edición para producción de Oracle Java SE también está disponible para que los desarrolladores de Java ejecuten cargas de trabajo de Java en máquinas virtuales Windows o Linux en Azure.

## <a name="use-for-local-development"></a>Uso para desarrollo local 

Los desarrolladores pueden [descargar](https://www.azul.com/downloads/azure-only/zulu/) los JDK de Java para Azure y Azure Stack para usarlos en los entornos de desarrollo locales. Las descargas están disponibles para Windows, Linux y macOS. Los desarrolladores que trabajan en Linux también pueden obtener los paquetes mediante los administradores de paquetes [yum](https://www.azul.com/downloads/azure-only/zulu/#yum-repo) y [apt](https://www.azul.com/downloads/azure-only/zulu/#apt-repo).

Para más información, consulte [Imágenes de Docker para Azure](java-jdk-docker-images.md).