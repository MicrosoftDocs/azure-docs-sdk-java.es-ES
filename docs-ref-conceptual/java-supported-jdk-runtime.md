---
title: JDK de Java y soporte técnico a largo plazo para el desarrollo en Azure
description: Descargas e instrucciones del equipo de soporte técnico de Azure para el desarrollo y ejecución de aplicaciones Java.
author: rloutlaw
manager: angerobe
ms.devlang: java
ms.topic: article
ms.date: 10/26/2017
ms.author: routlaw
ms.openlocfilehash: 7f75b26bffc02a161e8d58827970bd80a3a6c48a
ms.sourcegitcommit: 66f3dd4bdb09712b73c9194e23028567c0c4ee3f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/30/2018
ms.locfileid: "50235211"
---
# <a name="get-java-jdk-downloads-and-support-when-developing-for-azure"></a>Obtenga descargas del JDK de Java y soporte técnico para el desarrollo en Azure

Los desarrolladores Java que trabajan con Azure y Azure Stack pueden crear y ejecutar aplicaciones Java de producción con [compilaciones de Azul Zulu Enterprise para Azure](https://www.azul.com/downloads/azure-only/zulu/) sin incurrir en costos de soporte técnico adicionales. Puede usar cualquier entorno de ejecución de Java que desee en Azure, pero cuando se usa Zulu se obtienen actualizaciones de mantenimiento gratuitas y se pueden abrir incidencias de soporte técnico con Microsoft con un [plan de soporte técnico de Azure cualificado](https://azure.microsoft.com/support/plans/).

Los desarrolladores pueden usar sus propios entornos de ejecución de Java, incluidos el JDK de Oracle y el JDK de Red Hat, para ejecutar sus aplicaciones en Azure y conectarse a las características y servicios de Azure. La edición para producción de Oracle Java SE continúa estando disponible para los desarrolladores de Java que ejecutan cargas de trabajo en máquinas virtuales Windows o Linux de Azure.

## <a name="supported-java-versions-and-update-schedule"></a>Versiones de Java admitidas y programación de actualizaciones

Azul Systems proporcionará [compilaciones de Zulu Enterprise de OpenJDK para Microsoft Azure](https://www.azul.com/downloads/azure-only/zulu/) con soporte técnico completo para todas las versiones de Java con soporte técnico a largo plazo (LTS), a partir de Java SE 7, 8 y 11. Encontrará más información en la [nota de prensa de Azul](https://www.azul.com/press_release/free-java-production-support-for-microsoft-azure-azure-stack).


Estas versiones de JDK tendrán actualizaciones de seguridad y correcciones de errores trimestrales, así como las actualizaciones críticas y revisiones fuera de banda según sea necesario.  Esta compatibilidad incluye el traslado a versiones anteriores de las actualizaciones de seguridad y correcciones de errores para Java 7 y 8 notificadas en versiones más recientes de Java, como Java 11 y garantiza la continuidad de la estabilidad y seguridad de las versiones anteriores de Java.  Los clientes de Azure tienen derecho a estas actualizaciones de seguridad y a las correcciones de errores de la plataforma sin incurrir en cuotas de suscripción a Java SE no planeadas. Las fechas de soporte técnico para cada versión de Java SE se resaltan en la imagen siguiente.

![Escala de tiempo del soporte técnico de JDK para Azure](media/azure-jdk-support.png)

Azul Systems mantiene una [hoja de ruta de Java SE](https://www.azul.com/products/azul_support_roadmap/) para estas versiones.

## <a name="use-for-local-development"></a>Uso para desarrollo local 

Los desarrolladores pueden [descargar](https://www.azul.com/downloads/azure-only/zulu/) los JDK de Java para Azure y Azure Stack para usarlos en los entornos de desarrollo locales. Las descargas están disponibles para Windows, Linux y macOS. Los desarrolladores que trabajan en Linux también pueden obtener los paquetes mediante los administradores de paquetes [yum](https://www.azul.com/downloads/azure-only/zulu/#yum-repo) y [apt](https://www.azul.com/downloads/azure-only/zulu/#apt-repo).

Cuando se desarrolla para Azure o Azure Stack con el JDS en el entorno local, hay un soporte técnico está disponible con un [plan de soporte técnico de Azure cualificado](https://azure.microsoft.com/support/plans/).

## <a name="use-in-docker-containers"></a>Uso en contenedores de Docker

Con las compilaciones de Zulu Enterprise de OpenJDK, puede crear imágenes de Docker ilimitadas en las distribuciones que desee. Las imágenes de Docker de Zulu basadas en Azul Zulu Enterprise para los JDK de Azure están disponibles en el [repositorio de Docker público de Microsoft](https://hub.docker.com/r/microsoft/java-jdk/). Los archivos Dockerfile utilizados para generar estas imágenes están disponibles en el [repositorio de GitHub de Java de Microsoft](https://github.com/Microsoft/java/tree/master/docker).

Para incluir en contenedores las aplicaciones con estas imágenes, deberá establecer una instrucción `FROM` en el archivo Dockerfile y, a continuación, configurar el contenedor con las dependencias de la aplicación. Por ejemplo, para ejecutar una aplicación Java SE empaquetada en un archivo JAR que enlaza al puerto 8080:

```Dockerfile
FROM  microsoft/java-jdk:<tag>
EXPOSE 8080
ADD target/hello.jar hello.jar
ENTRYPOINT ["java", "-jar","/hello.jar"]
```

## <a name="azure-service-runtime-support"></a>Soporte técnico en tiempo de ejecución del servicio de Azure

Los servicios de la plataforma de Azure como [App Service](/azure/app-service/containers/), [Functions](/azure/azure-functions/functions-create-first-java-maven), [Service Fabric](/azure/service-fabric/) y [HDInsight](/azure/hdinsight/) utilizan compilaciones de Zulu Enterprise de OpenJDK con aplicación automática de revisiones secundarias de Java que incluyen revisiones de seguridad y correcciones de errores.