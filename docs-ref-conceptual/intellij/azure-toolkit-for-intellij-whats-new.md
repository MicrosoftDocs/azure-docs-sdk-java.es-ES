---
title: Novedades del kit de herramientas de Azure para IntelliJ
description: "Obtenga información acerca las características más recientes del kit de herramientas de Azure para IntelliJ."
services: 
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 46ed791f-df59-416a-809e-f52345ad973c
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 10/19/2017
ms.author: robmcm;asirveda;martinsawicki
ms.openlocfilehash: 3e3d22cc5720346e31a096adfd935b2712aac4e9
ms.sourcegitcommit: 7f8538e41c833deb69c300ad3431a431136a1f3e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/24/2017
---
# <a name="whats-new-in-the-azure-toolkit-for-intellij"></a>Novedades del kit de herramientas de Azure para IntelliJ

## <a name="azure-toolkit-for-intellij-releases"></a>Kit de herramientas de Azure para versiones de IntelliJ
Este artículo contiene información sobre las diversas versiones y actualizaciones más recientes para el kit de herramientas de Azure para IntelliJ.

> [!NOTE]
> Consulte la siguiente página web para ver la información más reciente:
> 
> <https://github.com/Microsoft/azure-tools-for-java/releases>

> [!NOTE]
> También hay un kit de herramientas de Azure para el IDE de Eclipse. Para obtener más información, consulte [Kit de herramientas de Azure para Eclipse].
> 
> 

### <a name="april-14-2017"></a>14 de abril de 2017
El kit de herramientas de Azure para IntelliJ, versión de abril de 2017, incluye las siguientes mejoras:

* **Experiencia de inicio de sesión mejorada de Azure**: el kit de herramientas de Azure para IntelliJ ahora admite dos métodos para iniciar sesión en la cuenta de Azure: *interactivo* y *automatizado*. Para más información, vea [Instrucciones de inicio de sesión de Azure del kit de herramientas de Azure para IntelliJ].
* **Publicación con contenedores de Docker**: ahora puede publicar las aplicaciones web como contenedores de Docker mediante el kit de herramientas de Azure para IntelliJ. Para más información, vea [Cómo publicar una aplicación web como un contenedor de Docker mediante el kit de herramientas de Azure para IntelliJ].
* **Administración de cuentas de almacenamiento**: el kit de herramientas de Azure para IntelliJ ahora admite la administración de las cuentas de almacenamiento desde la vista del explorador de Azure. Para más información, vea [Administración de cuentas de almacenamiento mediante Azure Explorer para IntelliJ].
* **Administración de máquinas virtuales**: el kit de herramientas de Azure para IntelliJ ahora admite la administración de las máquinas virtuales desde la ventana de herramientas del explorador de Azure. Para más información, vea [Administración de máquinas virtuales mediante Azure Explorer para IntelliJ].
* **Eliminación de la compatibilidad con la depuración remota**. La depuración remota de aplicaciones web de Java en Azure App Service se ha eliminado del kit de herramientas de Azure para IntelliJ; esto ha sido necesario para resolver algunos problemas que los clientes experimentaban al usar el kit de herramientas.

### <a name="august-26-2016"></a>26 de agosto de 2016
En la versión de agosto de 2016, el Kit de herramientas de Azure para IntelliJ incluye las siguientes mejoras:

* **Distribuciones de JDK personalizadas**. El Kit de herramientas de Azure para IntelliJ ahora admite especificar e implementar una versión de JDK arbitraria en el contenedor de Azure WebApp:
  * Además de los JDK que proporciona Azure, puede elegir entre una gran variedad de versiones de Zulu OpenJDK que pone a disposición Azul Systems en Azure.
  * También puede especificar su propia distribución de JDK si la carga como un archivo ZIP en su cuenta de almacenamiento.
* **Mejoras en la vista del Explorador de Azure**:
  * Compatibilidad con la administración de máquinas virtuales mediante el nuevo modelo de Azure Resource Manager: puede crear y eliminar máquinas virtuales basadas en Resource Manager sin salir del IDE, así como incluirlas en listas.
  * Compatibilidad con la administración de blobs de cuentas de almacenamiento mediante Azure Resource Manager, lo que complementa la funcionalidad existente para administrar las cuentas de almacenamiento clásicas.
* **Microsoft JDBC Driver 6.0 para SQL Server**. Esta actualización incluye la versión más reciente de Microsoft JDBC Driver para Microsoft SQL Server (6.0), que ahora se incluye como una biblioteca que se puede agregar fácilmente a los proyectos de Java, con lo que sustituye a la versión anterior.

### <a name="june-29-2016"></a>29 de junio de 2016
El kit de herramientas de Azure para IntelliJ, versión de junio de 2016, incluye las siguientes mejoras:

* **Requisito de Java 8**. El Kit de herramientas de Azure para IntelliJ ahora requiere Java 8, aunque este requisito es solo para el kit de herramientas: las aplicaciones pueden seguir usando todas las versiones de Java compatibles con Azure.
* **Compatibilidad para el JDK más reciente de Java**. Las versiones más recientes de los JDK de Java ahora admiten el Kit de herramientas de Azure para IntelliJ.
* **Compatibilidad con la versión 2.9.1 del SDK de Azure**. La versión más reciente del SDK de Azure ahora es el requisito previo mínimo para el kit de herramientas de Azure para IntelliJ.
* **Ejemplos integrados**. El Kit de herramientas de Azure para IntelliJ ahora cuenta con varias aplicaciones de ejemplo para ayudar a los desarrolladores a empezar a trabajar.
* **Integración de herramientas de HDInsight**. Las herramientas de Azure HDInsight ahora están incluidas en el Kit de herramientas de Azure para IntelliJ. Para más información, consulte [Complemento Herramientas de HDInsight para IntelliJ].
* **Depuración remota de Java Web Apps**. El Kit de herramientas de Azure para IntelliJ ahora admite la depuración remota de aplicaciones web de Java en Azure App Service.

### <a name="april-12-2016"></a>12 de abril de 2016
El kit de herramientas de Azure para IntelliJ, versión de abril de 2016, incluye las siguientes mejoras:

* **Compatibilidad con la versión 2.9.0 del SDK de Azure**. La versión más reciente del SDK de Azure ahora es el requisito previo mínimo para el kit de herramientas de Azure para IntelliJ.
* **Mejoras variadas en la facilidad de uso, la capacidad de respuesta y el rendimiento relacionadas con la compatibilidad de aplicaciones web de Azure**. Diversas optimizaciones de rendimiento con respecto a la manera en que el kit de herramientas se comunica con Azure generan una IU con mayor capacidad de respuesta.
* **Capacidad de eliminar un contenedor de aplicaciones web en Azure desde IntelliJ**. El kit de herramientas de Azure para IntelliJ ahora le permite eliminar un contenedor web de Azure existente sin salir de IntelliJ.

## <a name="next-steps"></a>Pasos siguientes

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<!-- URL List -->

[Kit de herramientas de Azure para Eclipse]: ../eclipse/azure-toolkit-for-eclipse.md

[Instrucciones de inicio de sesión de Azure del kit de herramientas de Azure para IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Cómo publicar una aplicación web como un contenedor de Docker mediante el kit de herramientas de Azure para IntelliJ]: ./azure-toolkit-for-intellij-publish-as-docker-container.md
[Administración de cuentas de almacenamiento mediante Azure Explorer para IntelliJ]: ./azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer.md
[Administración de máquinas virtuales mediante Azure Explorer para IntelliJ]: ./azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer.md

[Azure Java Developer Center]: https://docs.microsoft.com/java/azure

[Complemento Herramientas de HDInsight para IntelliJ]: /azure/hdinsight/hdinsight-apache-spark-intellij-tool-plugin
