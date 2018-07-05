---
title: Incorporación de un certificado raíz para Azure al almacén de certificados CA de Java
description: Vea cómo agregar un certificado raíz de entidad de certificación (CA) al almacén de certificados CA de Java (cacerts) para usarlo con Microsoft Azure.
services: ''
documentationcenter: java
author: rmcmurray
manager: mbaldwin
ms.assetid: d3699b0a-835c-43fb-844d-9c25344e5cda
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 05/23/2018
ms.author: robmcm
ms.openlocfilehash: 29b2b598968c9a3a896fffee3ce56f9b0cb4b1ee
ms.sourcegitcommit: 5282a51bf31771671df01af5814df1d2b8e4620c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/28/2018
ms.locfileid: "37090738"
---
# <a name="adding-a-root-certificate-to-the-java-ca-certificates-store"></a>Incorporación de un certificado raíz al almacén de certificados CA de Java

Las aplicaciones que utilizan servicios de Azure (como Azure Service Bus), deben confiar en el certificado raíz Baltimore CyberTrust. Este certificado podría estar instalado en el sistema pero, si no es así, los pasos descritos en este tutorial le mostrarán cómo usar la utilidad **keytool** de Oracle para agregar el certificado raíz de entidad de certificación (CA) necesario al almacén de certificados de CA de Java (cacerts) que utilizará para los servicios de Azure.

La utilidad keytool de Oracle es una _herramienta de administración de certificados y claves_ que permite a los desarrolladores administrar la lista de certificados de confianza que se usarán con Java. Puede usar keytool para agregar el certificado de entidad de certificación antes de comprimir su JDK y agregarlo a la carpeta **approot** de su proyecto de Azure, o puede ejecutar una tarea de inicio de Azure que use keytool para agregar el certificado.

A partir del 15 de abril de 2013, Azure empezó la migración del certificado raíz de GTE CyberTrust Global a Baltimore CyberTrust. Los pasos siguientes muestran cómo usar keytool para agregar el certificado raíz de Baltimore CyberTrust a su almacén de certificados CA de Java (cacerts).

> [!NOTE]
> 
> Puede usar los pasos de este artículo para configurar el SDK de Java para confiar en los certificados raíz de otras entidades emisoras de certificados de confianza. Por ejemplo, podría elegir un certificado raíz de la lista de certificados en [GeoTrust Root Certificates](http://www.geotrust.com/resources/root-certificates/).
> 

## <a name="determining-which-root-certificates-are-installed"></a>Determinación de los certificados raíz que se instalan

El certificado Baltimore podría estar ya instalado en el almacén cacerts, por lo que deberá usar los pasos siguientes para determinar si ya se ha instalado.

1. En un símbolo del sistema de administrador, vaya a la carpeta **jdk\jre\lib\security** de su JDK y ejecute el siguiente comando para enumerar los certificados que están instalados en el sistema:

   ```shell
   keytool -list -keystore cacerts
   ```

1. Si se le pide la contraseña del almacén, la contraseña predeterminada es **changeit**.

   > [!NOTE]
   > 
   > Si desea cambiar la contraseña, consulte la documentación de keytool en <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>.
   > 

1. Si no ve el certificado con la huella digital `d4:de:20:d0:5e:66:fc:53:fe:1a:50:88:2c:78:db:28:52:ca:e4:74`, utilice los pasos de la sección siguiente para descargar e instalar el certificado.

## <a name="to-add-a-root-certificate-to-the-cacerts-store"></a>Para agregar un certificado al almacén cacerts

1. Descargue el certificado raíz de Baltimore CyberTrust desde <https://cacert.omniroot.com/bc2025.crt> y guárdelo en un archivo local con la extensión **.cer** en su carpeta **jdk\jre\lib\security**. Este ejemplo, damos por hecho que ya ha descargado el archivo del certificado raíz de Baltimore CyberTrust con el nombre **bc2025.cer**.

   > [!NOTE]
   > 
   > El certificado raíz de Baltimore CyberTrust tiene el número de serie `02:00:00:b9` y una huella digital de SHA1 `d4:de:20:d0:5e:66:fc:53:fe:1a:50:88:2c:78:db:28:52:ca:e4:74`.
   > 

2. Importe el certificado al almacén cacerts con el comando siguiente:

   ```shell
   keytool -keystore cacerts -importcert -alias bc2025ca -file bc2025.cer
   ```
   Donde:

   |  .   |                              DESCRIPCIÓN                               |
   |--------------|------------------------------------------------------------------------|
   |  `keystore`  |                    Especifica el almacén de certificados.                    |
   | `importcert` |            Especifica que va a importar un certificado.             |
   |   `alias`    |                Especifica un alias para el certificado.                 |
   |    `file`    | Especifica el nombre de archivo del certificado raíz que va a importar. |


3. Si se le pide que confíe en el certificado, compruebe que la huella digital es `d4:de:20:d0:5e:66:fc:53:fe:1a:50:88:2c:78:db:28:52:ca:e4:74` y escriba **y** si la huella digital es correcta.

4. Ejecute el siguiente comando para asegurarse de que el certificado CA se ha importado correctamente:

   ```shell
   keytool -list -keystore cacerts
   ```

Después de agregar correctamente el certificado raíz al JDK, puede comprimir el contenido de JDK en un archivo zip y agregarlo a la carpeta **approot** de su proyecto de Azure.

## <a name="next-steps"></a>Pasos siguientes

Para más información acerca de la utilidad keytool, consulte <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>.

Para obtener más información sobre los certificados raíz que usa Azure, consulte [Azure Root Certificate Migration (Migración de certificados raíz de Azure)](http://blogs.msdn.com/b/windowsazure/archive/2013/03/15/windows-azure-root-certificate-migration.aspx).

Para más información sobre Java, consulte [Azure para desarrolladores de Java](/java/azure).
