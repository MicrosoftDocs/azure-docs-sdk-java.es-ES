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
# <a name="adding-a-root-certificate-to-the-java-ca-certificates-store"></a><span data-ttu-id="acb7c-103">Incorporación de un certificado raíz al almacén de certificados CA de Java</span><span class="sxs-lookup"><span data-stu-id="acb7c-103">Adding a root certificate to the Java CA certificates store</span></span>

<span data-ttu-id="acb7c-104">Las aplicaciones que utilizan servicios de Azure (como Azure Service Bus), deben confiar en el certificado raíz Baltimore CyberTrust.</span><span class="sxs-lookup"><span data-stu-id="acb7c-104">Applications that use Azure services (such as Azure Service Bus) need to trust the Baltimore CyberTrust root certificate.</span></span> <span data-ttu-id="acb7c-105">Este certificado podría estar instalado en el sistema pero, si no es así, los pasos descritos en este tutorial le mostrarán cómo usar la utilidad **keytool** de Oracle para agregar el certificado raíz de entidad de certificación (CA) necesario al almacén de certificados de CA de Java (cacerts) que utilizará para los servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="acb7c-105">This certificate may already be installed on your system, but if it is not, the steps in this tutorial will show you how to use Oracle's **keytool** to add the required certificate authority (CA) root certificate to the Java CA certificate (cacerts) store that you will use for Azure services.</span></span>

<span data-ttu-id="acb7c-106">La utilidad keytool de Oracle es una _herramienta de administración de certificados y claves_ que permite a los desarrolladores administrar la lista de certificados de confianza que se usarán con Java.</span><span class="sxs-lookup"><span data-stu-id="acb7c-106">Oracle's keytool utility is a _Key and Certificate Management Tool_, which allows developers to manage the list of trusted certificates for use with Java.</span></span> <span data-ttu-id="acb7c-107">Puede usar keytool para agregar el certificado de entidad de certificación antes de comprimir su JDK y agregarlo a la carpeta **approot** de su proyecto de Azure, o puede ejecutar una tarea de inicio de Azure que use keytool para agregar el certificado.</span><span class="sxs-lookup"><span data-stu-id="acb7c-107">You can use keytool to add the CA certificate before zipping your JDK and adding it to your Azure project's **approot** folder, or you could run an Azure start-up task that uses keytool to add the certificate.</span></span>

<span data-ttu-id="acb7c-108">A partir del 15 de abril de 2013, Azure empezó la migración del certificado raíz de GTE CyberTrust Global a Baltimore CyberTrust.</span><span class="sxs-lookup"><span data-stu-id="acb7c-108">Beginning April 15, 2013, Azure began migrating from the GTE CyberTrust Global root certificate to the Baltimore CyberTrust root certificate.</span></span> <span data-ttu-id="acb7c-109">Los pasos siguientes muestran cómo usar keytool para agregar el certificado raíz de Baltimore CyberTrust a su almacén de certificados CA de Java (cacerts).</span><span class="sxs-lookup"><span data-stu-id="acb7c-109">The following steps show you how to use keytool to add the Baltimore CyberTrust root certificate to your Java CA certificate (cacerts) store.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="acb7c-110">Puede usar los pasos de este artículo para configurar el SDK de Java para confiar en los certificados raíz de otras entidades emisoras de certificados de confianza.</span><span class="sxs-lookup"><span data-stu-id="acb7c-110">You can use the steps in this article to configure your Java SDK to trust the root certificates from other trusted certificate authorities.</span></span> <span data-ttu-id="acb7c-111">Por ejemplo, podría elegir un certificado raíz de la lista de certificados en [GeoTrust Root Certificates](http://www.geotrust.com/resources/root-certificates/).</span><span class="sxs-lookup"><span data-stu-id="acb7c-111">For example, you might choose a root certificate from the list of certificates at [GeoTrust Root Certificates](http://www.geotrust.com/resources/root-certificates/).</span></span>
> 

## <a name="determining-which-root-certificates-are-installed"></a><span data-ttu-id="acb7c-112">Determinación de los certificados raíz que se instalan</span><span class="sxs-lookup"><span data-stu-id="acb7c-112">Determining which root certificates are installed</span></span>

<span data-ttu-id="acb7c-113">El certificado Baltimore podría estar ya instalado en el almacén cacerts, por lo que deberá usar los pasos siguientes para determinar si ya se ha instalado.</span><span class="sxs-lookup"><span data-stu-id="acb7c-113">The Baltimore certificate might already be installed in your cacerts store, so you need to use the following steps to determine if it has already been installed.</span></span>

1. <span data-ttu-id="acb7c-114">En un símbolo del sistema de administrador, vaya a la carpeta **jdk\jre\lib\security** de su JDK y ejecute el siguiente comando para enumerar los certificados que están instalados en el sistema:</span><span class="sxs-lookup"><span data-stu-id="acb7c-114">At an administrator command prompt, navigate to your JDK's **jdk\jre\lib\security** folder, and then run the following command to list the certificates that are installed on your system:</span></span>

   ```shell
   keytool -list -keystore cacerts
   ```

1. <span data-ttu-id="acb7c-115">Si se le pide la contraseña del almacén, la contraseña predeterminada es **changeit**.</span><span class="sxs-lookup"><span data-stu-id="acb7c-115">If you are prompted for the store password, the default password is **changeit**.</span></span>

   > [!NOTE]
   > 
   > <span data-ttu-id="acb7c-116">Si desea cambiar la contraseña, consulte la documentación de keytool en <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>.</span><span class="sxs-lookup"><span data-stu-id="acb7c-116">If you want to change the store password, see the keytool documentation at <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>.</span></span>
   > 

1. <span data-ttu-id="acb7c-117">Si no ve el certificado con la huella digital `d4:de:20:d0:5e:66:fc:53:fe:1a:50:88:2c:78:db:28:52:ca:e4:74`, utilice los pasos de la sección siguiente para descargar e instalar el certificado.</span><span class="sxs-lookup"><span data-stu-id="acb7c-117">If you do not see the certificate with the thumbprint of `d4:de:20:d0:5e:66:fc:53:fe:1a:50:88:2c:78:db:28:52:ca:e4:74`, use the steps in the following section to download and install the certificate.</span></span>

## <a name="to-add-a-root-certificate-to-the-cacerts-store"></a><span data-ttu-id="acb7c-118">Para agregar un certificado al almacén cacerts</span><span class="sxs-lookup"><span data-stu-id="acb7c-118">To add a root certificate to the cacerts store</span></span>

1. <span data-ttu-id="acb7c-119">Descargue el certificado raíz de Baltimore CyberTrust desde <https://cacert.omniroot.com/bc2025.crt> y guárdelo en un archivo local con la extensión **.cer** en su carpeta **jdk\jre\lib\security**.</span><span class="sxs-lookup"><span data-stu-id="acb7c-119">Download the Baltimore CyberTrust root certificate from <https://cacert.omniroot.com/bc2025.crt>, and save to a local file with extension **.cer** in your **jdk\jre\lib\security** folder.</span></span> <span data-ttu-id="acb7c-120">Este ejemplo, damos por hecho que ya ha descargado el archivo del certificado raíz de Baltimore CyberTrust con el nombre **bc2025.cer**.</span><span class="sxs-lookup"><span data-stu-id="acb7c-120">For this example, assume that you downloaded the Baltimore CyberTrust root certificate file as **bc2025.cer**.</span></span>

   > [!NOTE]
   > 
   > <span data-ttu-id="acb7c-121">El certificado raíz de Baltimore CyberTrust tiene el número de serie `02:00:00:b9` y una huella digital de SHA1 `d4:de:20:d0:5e:66:fc:53:fe:1a:50:88:2c:78:db:28:52:ca:e4:74`.</span><span class="sxs-lookup"><span data-stu-id="acb7c-121">The Baltimore CyberTrust root certificate has a serial number of `02:00:00:b9`, and a SHA1 thumbprint of `d4:de:20:d0:5e:66:fc:53:fe:1a:50:88:2c:78:db:28:52:ca:e4:74`.</span></span>
   > 

2. <span data-ttu-id="acb7c-122">Importe el certificado al almacén cacerts con el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="acb7c-122">Import the certificate to the cacerts store by using the following command:</span></span>

   ```shell
   keytool -keystore cacerts -importcert -alias bc2025ca -file bc2025.cer
   ```
   <span data-ttu-id="acb7c-123">Donde:</span><span class="sxs-lookup"><span data-stu-id="acb7c-123">Where:</span></span>

   |  <span data-ttu-id="acb7c-124">.</span><span class="sxs-lookup"><span data-stu-id="acb7c-124">Parameter</span></span>   |                              <span data-ttu-id="acb7c-125">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="acb7c-125">Description</span></span>                               |
   |--------------|------------------------------------------------------------------------|
   |  `keystore`  |                    <span data-ttu-id="acb7c-126">Especifica el almacén de certificados.</span><span class="sxs-lookup"><span data-stu-id="acb7c-126">Specifies the certificate store.</span></span>                    |
   | `importcert` |            <span data-ttu-id="acb7c-127">Especifica que va a importar un certificado.</span><span class="sxs-lookup"><span data-stu-id="acb7c-127">Specifies that you are importing a certificate.</span></span>             |
   |   `alias`    |                <span data-ttu-id="acb7c-128">Especifica un alias para el certificado.</span><span class="sxs-lookup"><span data-stu-id="acb7c-128">Specifies an alias for the certificate.</span></span>                 |
   |    `file`    | <span data-ttu-id="acb7c-129">Especifica el nombre de archivo del certificado raíz que va a importar.</span><span class="sxs-lookup"><span data-stu-id="acb7c-129">Specifies the filename of the root certificate that you are importing.</span></span> |


3. <span data-ttu-id="acb7c-130">Si se le pide que confíe en el certificado, compruebe que la huella digital es `d4:de:20:d0:5e:66:fc:53:fe:1a:50:88:2c:78:db:28:52:ca:e4:74` y escriba **y** si la huella digital es correcta.</span><span class="sxs-lookup"><span data-stu-id="acb7c-130">If you are prompted to trust the certificate, verify the thumbprint as `d4:de:20:d0:5e:66:fc:53:fe:1a:50:88:2c:78:db:28:52:ca:e4:74`, and type **y** if the thumbprint is correct.</span></span>

4. <span data-ttu-id="acb7c-131">Ejecute el siguiente comando para asegurarse de que el certificado CA se ha importado correctamente:</span><span class="sxs-lookup"><span data-stu-id="acb7c-131">Run the following command to ensure the CA certificate has been successfully imported:</span></span>

   ```shell
   keytool -list -keystore cacerts
   ```

<span data-ttu-id="acb7c-132">Después de agregar correctamente el certificado raíz al JDK, puede comprimir el contenido de JDK en un archivo zip y agregarlo a la carpeta **approot** de su proyecto de Azure.</span><span class="sxs-lookup"><span data-stu-id="acb7c-132">After you have successfully added the root certificate to your JDK, you can zip the contents of JDK and add it to your Azure project's **approot** folder.</span></span>

## <a name="next-steps"></a><span data-ttu-id="acb7c-133">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="acb7c-133">Next steps</span></span>

<span data-ttu-id="acb7c-134">Para más información acerca de la utilidad keytool, consulte <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>.</span><span class="sxs-lookup"><span data-stu-id="acb7c-134">For more information about the keytool utility, see <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>.</span></span>

<span data-ttu-id="acb7c-135">Para obtener más información sobre los certificados raíz que usa Azure, consulte [Azure Root Certificate Migration (Migración de certificados raíz de Azure)](http://blogs.msdn.com/b/windowsazure/archive/2013/03/15/windows-azure-root-certificate-migration.aspx).</span><span class="sxs-lookup"><span data-stu-id="acb7c-135">For more information about the root certificates used by Azure, see [Azure Root Certificate Migration](http://blogs.msdn.com/b/windowsazure/archive/2013/03/15/windows-azure-root-certificate-migration.aspx).</span></span>

<span data-ttu-id="acb7c-136">Para más información sobre Java, consulte [Azure para desarrolladores de Java](/java/azure).</span><span class="sxs-lookup"><span data-stu-id="acb7c-136">For more information about Java, see [Azure for Java developers](/java/azure).</span></span>