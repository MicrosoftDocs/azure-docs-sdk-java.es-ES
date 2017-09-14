---
title: Novedades del kit de herramientas de Azure para Eclipse
description: "Obtenga información acerca las características más recientes del kit de herramientas de Azure para Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 16b066ea-aae7-4c30-9a12-fa0c3711b93e
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 09/11/2017
ms.author: robmcm;asirveda;martinsawicki
ms.openlocfilehash: 31af7e6494f978f341e1f99a30117c57ef30a05b
ms.sourcegitcommit: 256044d7cbce16dcb8dc4e195d0f63c10cb44d4e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/13/2017
---
# <a name="whats-new-in-the-azure-toolkit-for-eclipse"></a>Novedades del kit de herramientas de Azure para Eclipse

## <a name="azure-toolkit-for-eclipse-releases"></a>Kit de herramientas de Azure para versiones de Eclipse
Este artículo contiene información sobre las diversas versiones y actualizaciones más recientes para el kit de herramientas de Azure para Eclipse.

> [!NOTE]
> También hay un Kit de herramientas de Azure para el IDE de IntelliJ. Para más información, consulte [Kit de herramientas de Azure para IntelliJ].
> 
> 

### <a name="april-14-2017"></a>14 de abril de 2017
El kit de herramientas de Azure para Eclipse, versión de abril de 2017, incluye las siguientes mejoras:

* **Experiencia de inicio de sesión mejorada de Azure**: el kit de herramientas de Azure para Eclipse ahora admite dos métodos para iniciar sesión en la cuenta de Azure: *interactivo* y *automatizado*. Para más información, vea [Instrucciones de inicio de sesión de Azure del kit de herramientas de Azure para Eclipse].
* **Publicación con contenedores de Docker**: ahora puede publicar las aplicaciones web como contenedores de Docker mediante el kit de herramientas de Azure para Eclipse. Para más información, vea [Cómo publicar una aplicación web como un contenedor de Docker mediante el kit de herramientas de Azure para Eclipse].
* **Administración de cuentas de almacenamiento**: el kit de herramientas de Azure para Eclipse ahora admite la administración de las cuentas de almacenamiento desde la vista del explorador de Azure. Para más información, vea [Administración de cuentas de almacenamiento mediante Azure Explorer para Eclipse].
* **Administración de máquinas virtuales**: el kit de herramientas de Azure para Eclipse ahora admite la administración de las máquinas virtuales desde la vista del explorador de Azure. Para más información, vea [Administración de máquinas virtuales mediante Azure Explorer para Eclipse].
* **Eliminación de la compatibilidad con la depuración remota**. La depuración remota de aplicaciones web de Java en Azure App Service se ha eliminado del kit de herramientas de Azure para Eclipse; era necesario para resolver algunos problemas que los clientes experimentaban al usar el kit de herramientas.

### <a name="august-26-2016"></a>26 de agosto de 2016
El kit de herramientas de Azure para Eclipse, versión de agosto de 2016, incluye las siguientes mejoras:

* **Distribuciones de JDK personalizadas**. El Kit de herramientas de Azure para Eclipse ahora admite especificar e implementar una versión de JDK arbitraria en el contenedor de Azure WebApp:
  * Además de los JDK que proporciona Azure, puede elegir entre una gran variedad de versiones de Zulu OpenJDK que pone a disposición Azul Systems en Azure.
  * También puede especificar su propia distribución de JDK si la carga como un archivo ZIP en su cuenta de almacenamiento.
* **Mejoras en la vista del Explorador de Azure**:
  * Compatibilidad con la administración de máquinas virtuales mediante el nuevo modelo de Azure Resource Manager: puede crear y eliminar máquinas virtuales basadas en Resource Manager sin salir del IDE, así como incluirlas en listas.
  * Compatibilidad con la administración de blobs de cuentas de almacenamiento mediante Azure Resource Manager, lo que complementa la funcionalidad existente para administrar las cuentas de almacenamiento clásicas.
* **Microsoft JDBC Driver 6.0 para SQL Server**. Esta actualización incluye la versión más reciente de Microsoft JDBC Driver para Microsoft SQL Server (6.0), que ahora se incluye como una biblioteca que se puede agregar fácilmente a los proyectos de Java, con lo que sustituye a la versión anterior.

### <a name="june-29-2016"></a>29 de junio de 2016
El kit de herramientas de Azure para Eclipse, versión de junio de 2016, incluye las siguientes mejoras:

* **Requisito de Java 8**. El Kit de herramientas de Azure para Eclipse ahora requiere Java 8, aunque este requisito es solo para el kit de herramientas: las aplicaciones pueden seguir usando todas las versiones de Java compatibles con Azure.
* **Compatibilidad para el JDK más reciente de Java**. Las versiones más recientes de los JDK de Java ahora admiten el Kit de herramientas de Azure para Eclipse.
* **Compatibilidad con la versión 2.9.1 del SDK de Azure**. La versión más reciente del SDK de Azure ahora es el requisito previo mínimo para el kit de herramientas de Azure para Eclipse.
* **Ejemplos integrados**. El Kit de herramientas de Azure para Eclipse ahora cuenta con varias aplicaciones de ejemplo para ayudar a los desarrolladores a empezar a trabajar.
* **Integración de herramientas de HDInsight**. Las herramientas de Azure HDInsight ahora están incluidas en el Kit de herramientas de Azure para Eclipse. Para más información, consulte [Complemento Herramientas de HDInsight para Eclipse].
* **Depuración remota de Java Web Apps**. El Kit de herramientas de Azure para Eclipse ahora admite la depuración remota de aplicaciones web de Java en Azure App Service.
* **Compatibilidad con la versión Kepler de Luna.** La nueva versión mínima necesaria del IDE de Eclipse es Luna.

### <a name="april-12-2016"></a>12 de abril de 2016
El kit de herramientas de Azure para Eclipse, versión de abril de 2016, incluye las siguientes mejoras:

* **Compatibilidad con la versión 2.9.0 del SDK de Azure**. La versión más reciente del SDK de Azure ahora es el requisito previo mínimo para el kit de herramientas de Azure para Eclipse.
* **Mejoras variadas en la facilidad de uso, la capacidad de respuesta y el rendimiento relacionadas con la compatibilidad de aplicaciones web de Azure**. Diversas optimizaciones de rendimiento con respecto a la manera en que el kit de herramientas se comunica con Azure generan una IU con mayor capacidad de respuesta.
* **Capacidad de eliminar un contenedor de aplicaciones web en Azure desde Eclipse**. El kit de herramientas de Azure para Eclipse ahora le permite eliminar un contenedor web de Azure existente sin salir de Eclipse.

### <a name="march-7-2016"></a>7 de marzo de 2016
El kit de herramientas de Azure para Eclipse, versión de marzo de 2016, incluye las siguientes mejoras:

* **Compatibilidad para la implementación rápida de las aplicaciones Java ligeras**. El kit de herramientas de Azure para Eclipse ahora admite la implementación rápida de las aplicaciones Java ligeras en contenedores de aplicaciones web de Azure, por lo que la implementación de aplicaciones Java ahora tarda segundos en lugar de minutos.
* **Compatibilidad con la administración de aplicaciones web mediante la vista Azure Explorer**. La vista del explorador de Azure del kit de herramientas ahora admite la enumeración, inicio y detención de Azure Web Apps.
* **Distribuciones actualizadas de OpenJDK de Zulu, Jetty y Tomcat**. El kit de herramientas de Azure para Eclipse proporciona compatibilidad con versiones actualizadas de OpenJDK de Zulu, Jetty y Tomcat para las implementaciones de Java en servicios en la nube de Azure.

### <a name="january-4-2016"></a>4 de enero de 2016
El kit de herramientas de Azure para Eclipse, versión de enero de 2016, incluye las siguientes mejoras:

* **Compatibilidad con las actualizaciones de Zulu de OpenJDK**. Para más información, consulte la [página web de Azul Systems para Zulu de OpenJDK].
* **Distribuciones actualizadas de Tomcat y Jetty**. Se han actualizado las distribuciones de Jetty y Tomcat que están disponibles en Microsoft Azure para su uso con el kit de herramientas de Azure para Eclipse.
* **Paridad de características entre Eclipse y kits de herramientas de IntelliJ para Azure**. El kit de herramientas de Azure para Eclipse y el [Kit de herramientas de Azure para IntelliJ] ahora admiten el mismo conjunto de características.

### <a name="september-1-2015"></a>1 de septiembre de 2015
El kit de herramientas de Azure para Eclipse, versión de septiembre de 2015, incluye las siguientes mejoras:

* **Compatibilidad con las actualizaciones de Zulu de OpenJDK**. Para más información, consulte la [página web de Azul Systems para Zulu de OpenJDK].
* **Distribuciones actualizadas de Tomcat y Jetty**. Se han actualizado las distribuciones de Jetty y Tomcat que están disponibles en Microsoft Azure para su uso con el kit de herramientas de Azure para Eclipse. Estas distribuciones permiten a los desarrolladores crear proyectos de desarrollo rápido y de prueba con el kit de herramientas de Azure para Eclipse.
* **Compatibilidad con las referencias automáticamente actualizadas de Tomcat y Jetty**. Además de las versiones específicas de Tomcat y Jetty que están disponibles en Azure, los desarrolladores ahora pueden hacer referencia a una distribución conocida como la "más reciente (autoactualizada)", que actualizará automáticamente a la distribución más reciente de cada versión principal de Jetty o Tomcat la próxima vez que las instancias de rol se reciclen. El reciclaje se produce automáticamente, pero los desarrolladores pueden desencadenar manualmente un reciclaje a través de Azure Portal. Esta nueva característica significa que los desarrolladores no tienen que volver a implementar su aplicación para poder tener el software de servidor actualizado. (
* Actualmente, esta funcionalidad está pensada solo para aplicaciones con fines de desarrollo y prueba o con aplicaciones no críticas y no es recomendable para la producción.
* **Vista del explorador de Azure para blobs, colas y tablas de Azure Storage**. Esto permite a los desarrolladores realizar un conjunto de tareas comunes con los artefactos de almacenamiento directamente desde el IDE de Eclipse. Por ejemplo: eliminar, cargar o descargar blobs.

### <a name="august-1-2015"></a>1 de agosto de 2015
El kit de herramientas de Azure para Eclipse, versión de agosto de 2015, incluye las siguientes mejoras:

* **Administración de claves de instrumentación de Application Insights**. Esta actualización le permite adquirir, crear y administrar las claves de instrumentación de Application Insights directamente desde el IDE de Eclipse.
* **Microsoft JDBC Driver 4.1 para SQL Server**. Esta actualización incluye compatibilidad para la versión más reciente de JDBC Driver para Microsoft SQL Server.
* **Versión 2.7 del SDK de Azure**. Esta última actualización para el SDK de Azure es el nuevo requisito previo para el kit de herramientas cuando se instala en Windows. Tenga en cuenta que esto no es necesario en sistemas operativos que no sean Windows.
* **Compatibilidad con la actualización de Zulu de OpenJDK v7**. Para más información, consulte la [página web de Azul Systems para Zulu de OpenJDK].

### <a name="may-1-2015"></a>1 de mayo de 2015
El kit de herramientas de Azure para Eclipse, versión de mayo de 2015, incluye las siguientes mejoras:

* **Interfaz de usuario de selección de servidor mejorada**. Esta versión simplifica el uso del kit de herramientas en los sistemas operativos que no son Windows.
* **Compatibilidad con proyectos de Maven**. Esta versión admite proyectos de Maven como aplicaciones que el kit de herramientas puede implementar en Azure y configurar en Application Insights.
* **Versión 2.6 del SDK de Azure**. Esta última actualización para el SDK de Azure es el nuevo requisito previo para el kit de herramientas cuando se instala en Windows. Tenga en cuenta que esto no es necesario en sistemas operativos que no sean Windows.
* **Actualización de implementación en lugar de volver a publicarla**. Si vuelve a publicar un proyecto de implementación cuando la versión anterior ya está en funcionamiento, el kit de herramientas usa ahora la funcionalidad de actualización de implementación de Azure en lugar de apagar la implementación anterior y volver a publicarla desde cero como ocurría en el pasado. Esto permite que el servicio en la nube se ejecute sin interrupción siempre que sea posible, lo cual ayuda a lograr una alta disponibilidad incluso durante una actualización y acelera el proceso para volver a publicar.
* **Compatibilidad con la actualización 40 de Zulu de OpenJDK v8 más reciente**. Para más información, consulte la [página web de Azul Systems para Zulu de OpenJDK].

### <a name="march-9-2015"></a>9 de marzo de 2015
El kit de herramientas de Azure para Eclipse, versión de marzo de 2015, incluye las siguientes mejoras:

* **Compatibilidad para Mac, Ubuntu y tipos de Linux adicionales**. Esta versión del kit de herramientas de Azure para Eclipse agrega compatibilidad para Mac OS y varias plataformas de Unix, por lo que los desarrolladores pueden instalarla para crear, configurar y publicar proyectos de Java en Azure Cloud Services (PaaS) desde Eclipse que se están ejecutando en sistemas operativos distintos de Windows.

> [!NOTE]
> Esta capacidad existe solo en versión preliminar y no se recomienda su uso en entornos de producción. No hay ningún contrato de nivel de servicio (SLA) de soporte al cliente, pero se agradecen los comentarios.
> 
> 

* **Nuevo complemento de Application Insights**. Los desarrolladores pueden ahora configurar telemetría automática de servidores con Application Insights en Azure.
* **Automatización de la implementación de la línea de comandos basada en Ant**. Esta característica permite a los desarrolladores automatizar la publicación de las versiones más recientes de sus implementaciones usando Ant fuera de Eclipse. Un script generado previamente se configura automáticamente para un proyecto después de la primera vez que se implementa desde Eclipse y las implementaciones posteriores pueden volver a usarlo para automatizarlas por completo a través de la línea de comandos únicamente.
* **Disponibilidad de Tomcat y Jetty en Azure para una implementación más fácil y rápida**. Los desarrolladores pueden ahora hacer referencia a distintas versiones de Tomcat y Jetty que están disponibles en Azure directamente en lugar de tener que cargar un servidor de Java a sus cuentas (o mediante el kit de herramientas), por lo que no es necesario cargar este servidor en escenarios de iniciación rápidos.
* **Método abreviado para la publicación de aplicaciones web de Java en los servicios en la nube de Azure**. Para reducir la curva de aprendizaje para escenarios sencillos de desarrollo y pruebas, los desarrolladores ahora pueden publicar aplicaciones de Java más directamente en Azure. En lugar de tener que pasar por el proceso de crear y configurar un proyecto de implementación de Azure, las aplicaciones se implementarán con una instancia predeterminada de Tomcat v8 y Zulu JVM (OpenJDK).

### <a name="january-30-2015"></a>30 de enero de 2015
El kit de herramientas de Azure para Eclipse, versión de enero de 2015, incluye las siguientes mejoras:

* **Compatibilidad con IBM ® WebSphere ® Application Server Liberty Core**. Esta versión agrega IBM WebSphere Application Server Liberty Core a la lista de servidores de aplicaciones compatibles desde los que el kit de herramientas es capaz de implementarse en Azure. Esta última adición amplía la lista actual de servidores de aplicaciones que el kit de herramientas admite &quot;directamente&quot;, lista que ya incluía varias versiones de Tomcat, Jetty, JBoss y GlassFish.
* **Inclusión del SDK de Application Insights**. Esta biblioteca de API de cliente recién publicada (v0.9.0) ahora forma parte del paquete de bibliotecas de Azure para Java.
* **Paquete actualizado para bibliotecas de Azure para Java**. Esta actualización incluye bibliotecas de Azure para Java v0.7.0 y para la API de Storage Client v2.0.0, así como el SDK de Application Insights v0.9.0 recién publicado.

### <a name="november-12-2014"></a>12 de noviembre de 2014
El kit de herramientas de Azure para Eclipse, versión de noviembre de 2014, incluye las siguientes mejoras:

* **Compatibilidad con la versión 2.5 del SDK de Azure**. Esta última actualización para el SDK de Azure es el nuevo requisito previo para el kit de herramientas.
* **Compatibilidad con la versión actualizada de los paquetes de las versiones v1.8, v1.7 y v1.6 de Zulu de OpenJDK**. Para más información, consulte la [página web de Azul Systems para Zulu de OpenJDK].
* **Compatibilidad con los nuevos tamaños Standard_D para los servicios en la nube**, que ofrecen un mayor rendimiento y recursos adicionales de memoria. Para obtener más información, consulte [Tamaños de máquinas virtuales y servicios en la nube de Azure].

### <a name="october-17-2014"></a>17 de octubre de 2014
El kit de herramientas de Azure para Eclipse, versión de octubre de 2014, incluye las siguientes mejoras:

* **Mejoras de rendimiento en los escenarios de publicación en la nube**. La carga de información de suscripción es mucho más rápida cuando los usuarios tienen varias suscripciones y cuentas de almacenamiento.
* **Compatibilidad con la versión actualizada del paquete v1.8 de Zulu de OpenJDK**. Para más información, consulte la [página web de Azul Systems para Zulu de OpenJDK].
* **Compatibilidad con versiones en desuso de paquetes de JDK de terceros**. Los paquetes de JDK en desuso ya no aparecerán en el menú desplegable para los nuevos proyectos de implementación. Los proyectos ya existentes que hagan referencia a los paquetes de JDK en desuso podrán seguir haciéndolo durante un tiempo, pero se recomienda actualizar estos proyectos para que se basen en la versión más reciente.
* **Versión actualizada del paquete para bibliotecas de Azure para la biblioteca de API de cliente de Java**. Para más información, consulte la [API de cliente de Microsoft Azure].
* **Correcciones de errores.** Esta versión contiene una serie de correcciones de errores que se basaban en informes de usuario y pruebas.

### <a name="august-5-2014"></a>5 de agosto de 2014
El kit de herramientas de Azure para Eclipse, versión de agosto de 2014, incluye las siguientes mejoras:

* **Compatibilidad con la versión 2.4 del SDK de Azure.** Las versiones anteriores del kit de herramientas para Eclipse no funcionan con este SDK publicado recientemente.
* **Compatibilidad con la versión actualizada de los paquetes v1.6, 1.7 y v1.8 de Zulu de OpenJDK.** Para más información, consulte la [página web de Azul Systems para Zulu de OpenJDK].
* **Versión actualizada del paquete para bibliotecas de Azure para la biblioteca de API de cliente de Java.** Para más información, consulte la [API de cliente de Microsoft Azure].
* **Compatibilidad con la versión más reciente del formato de archivo de la configuración de publicación.** Se agregó compatibilidad para la versión 2.0 del formato de archivo de la configuración de publicación.
* **Cambios de arquitectura detrás de la característica de publicación en la nube.** El kit de herramientas usa ahora la API de cliente más reciente de Microsoft Azure para Java para su compatibilidad con la publicación en la nube.
* **Correcciones de errores.** Esta versión contiene una serie de correcciones solicitadas por el usuario.

### <a name="june-12-2014"></a>12 de junio de 2014
El kit de herramientas de Azure para Eclipse, versión de junio de 2014, es una actualización secundaria de servicio que proporciona las siguientes mejoras:

* **Compatibilidad con el paquete de la versión v1.8 de Zulu de OpenJDK.** Para más información, consulte la [página web de Azul Systems para Zulu de OpenJDK].
* **Compatibilidad con las versiones actualizadas de los paquetes v1.6 y v1.7 de Zulu de OpenJDK.** Para más información, consulte la [página web de Azul Systems para Zulu de OpenJDK].
* **Versión actualizada del paquete para bibliotecas de Azure para la biblioteca de API de cliente de Java.** Para más información, consulte la [API de cliente de Microsoft Azure].
* **Correcciones de errores.** Esta versión contiene una serie de correcciones solicitadas por el usuario.

### <a name="april-4-2014"></a>4 de abril de 2014
El complemento de Azure para Eclipse, versión de abril de 2014. Se trata de una actualización que acompaña a la versión 2.3 del SDK de Azure, que es un requisito previo y se descargará automáticamente al instalar el complemento. Esta actualización incluye nuevas características, correcciones de errores y algunas mejoras de facilidad de uso basadas en comentarios que se han producido desde la versión preliminar de febrero de 2014:

* **Compatibilidad con la versión 2.3 del SDK de Azure.** El complemento de Azure para Eclipse, versión de abril de 2014, requiere la versión 2.3 del SDK de Azure. Al usar el nuevo complemento, si no tiene todavía la versión 2.3 del SDK de Azure, se le solicitará que permita su instalación. No utilice la versión 2.3 del SDK de Azure con versiones anteriores del complemento.
* **Actualización de las aplicaciones sin la implementación del paquete completo.** Al implementar las aplicaciones de Java que forman parte de su proyecto, el complemento las carga ahora automáticamente en la cuenta de almacenamiento seleccionada de tal forma que pueda actualizarlo y reciclar las instancias de rol para implementar los bits más recientes de la aplicación sin tener que recompilar e implementar de nuevo todo el paquete.
* **Tomcat 8 es ahora un servidor de aplicaciones reconocido.** Si selecciona un directorio de instalación de Tomcat 8 en el equipo en la pestaña **Servidor** del cuadro de diálogo **Proyecto de implementación de Azure**, el complemento lo detectará automáticamente y podrá implementar Tomcat 8 de forma automática, de manera similar a las versiones anteriores de Tomcat que ya están en la lista.
* **Actualizaciones del paquete de Zulu de OpenJDK de Azul: actualización 51 de v1.7 y actualización 47 de v1.6.** A partir de esta versión, la actualización 51 del paquete de Zulu de Open JDK v7 de Azul System ya está disponible. Además, los paquetes de Zulu de Open JDK v6 empiezan a estar disponibles, empezando por la actualización 47. Estas actualizaciones son actualizaciones adicionales al paquete disponible anteriormente de Zulu de Open JDK v7, actualizaciones 45, 40 y 25.
* **Compatibilidad con los tamaños A8 y A9 de las máquinas virtuales de Microsoft Azure.** Ahora ya puede implementar un servicio en la nube con los tamaños de máquinas virtuales de memoria alta A8 y A9. Para más información sobre estos tamaños de máquinas virtuales, consulte [Tamaños de máquinas virtuales y servicios en la nube de Azure].
* **Redirección automática de HTTP a HTTPS para roles con SSL habilitado.** Cuando el servicio en la nube contiene solo roles HTTPS, si la solicitud de usuario especifica HTTP, este le redireccionará automáticamente a HTTPS. No hay ninguna necesidad de crear un rol independiente para controlar las solicitudes HTTP.
* **Emulador rápido usado para la emulación local.** El emulador rápido de Azure ahora se usa como emulador a la hora de depurar las aplicaciones localmente.
* **Azure ha pasado a llamarse Microsoft Azure.** Las pantallas de la interfaz de usuario reflejan ahora que Azure se ha cambiado el nombre y ya no se llama Azure.

### <a name="february-6-2014"></a>6 de febrero de 2014
Se ha publicado el complemento de Azure para Eclipse, versión preliminar de febrero de 2014. Esta actualización incluye nuevas características, correcciones de errores y algunas mejoras de facilidad de uso basadas en comentarios que se han producido desde la versión preliminar de octubre de 2013:

* **Compatibilidad con la descarga de SSL.** La descarga de capa de sockets seguros (SSL) se ha agregado como característica, lo que le permitirá habilitar fácilmente la compatibilidad con el protocolo HTTPS en su implementación de Java en Azure, sin necesidad de configurar SSL en el servidor de aplicaciones Java. Esto es especialmente importante para la afinidad de la sesión o en escenarios de comunicación autenticados. Por ejemplo, cuando se usa el filtro Access Control Service (ACS), que ya es compatible con el kit de herramientas. Para más información, consulte [SSL Offloading] y[ Uso de la descarga de SSL].
* **GlassFish 4 es ahora un servidor de aplicaciones reconocido**. Si selecciona un directorio de instalación de GlassFish 4 en el equipo en la pestaña **Servidor** del cuadro de diálogo **Proyecto de implementación de Azure**, el complemento lo detectará automáticamente y podrá implementar GlassFish OSE 4 de forma automática, de manera similar a la versión GlassFish OSE 3 que ya está en la lista.
* **Actualización 45 del paquete de Zulu de OpenJDK de Azul.** A partir de esta versión, la actualización 45 de Zulu (paquete Open JDK v7) de Azul System ya está disponible; esta actualización viene a sumarse a las actualizaciones 40 y 25 disponibles anteriormente.
* **Compatibilidad con modo 'auto' para puertos de punto de conexión privado.** Puede establecer un puerto privado en automático para los puntos de conexión de entrada y los puntos de conexión internos para permitir que Azure asigne automáticamente un puerto a ese punto de conexión. Anteriormente solo podía asignar un número de puerto específico.
* **Compatibilidad para personalizar el nombre de certificado (CN) en la interfaz de usuario de creación de un certificado autofirmado.** Anteriormente, se usó el mismo nombre codificado de forma rígida para todos los certificados nuevos; ahora puede especificar su propio nombre de certificado para ayudar a distinguir entre varios certificados en Azure Portal usados para distintos fines.
* **Barra de herramientas de Azure:** la barra de herramientas se ha actualizado con los siguientes cambios: 
  * ![][ic710876] Este icono se agregó para el **nuevo proyecto de implementación de Azure**.
  * ![][ic710877] Este icono se agregó como un acceso directo al cuadro de diálogo de creación de un certificado autofirmado.
* **Compatibilidad con el tamaño A5 de máquina virtual de Azure.** Ahora ya puede implementar un servicio en la nube con el tamaño de máquinas virtuales de memoria alta A5. Para más información sobre este tamaño de máquinas virtuales, consulte [Tamaños de máquinas virtuales y servicios en la nube de Azure].
* **Compatibilidad con Microsoft Windows Server 2012 R2.** Ahora puede seleccionar Windows Server 2012 R2 como sistema operativo en la nube.

### <a name="october-22-2013"></a>22 de octubre de 2013
Se ha publicado el complemento de Azure para Eclipse, versión preliminar de octubre de 2013. Esta actualización incluye nuevas características, correcciones de errores y algunas mejoras de facilidad de uso basadas en comentarios que se han producido desde la versión preliminar de septiembre de 2013:

* **Compatibilidad con la versión 2.2 del SDK de Azure.** El complemento de Azure para Eclipse, versión preliminar de octubre de 2013, es compatible con la versión 2.2 del SDK de Azure. El complemento seguirá funcionando con la versión 2.1 del SDK de Azure e instalará automáticamente la versión 2.2 si no tiene al menos la versión 2.1 instalada.
* **Actualización 40 del paquete de Zulu de OpenJDK de Azul.** Como se anunció para la versión preliminar de septiembre de 2013, el complemento ahora se habilita mediante un JDK proporcionado por terceros directamente en Azure, sin necesidad de cargar su propio JDK. En la versión de octubre de 2013, la actualización 40 de Zulu (paquete Open JDK v7) de Azul System ya está disponible; esta actualización viene a sumarse a la actualización 25 publicada originalmente.
* **Vínculo de implementación en la nube en el registro de actividades.** En el registro de actividades de Azure, cuando la implementación tenga un estado **Publicado**, puede hacer clic en **Publicado** puesto que ahora es un vínculo a la implementación y esta se abrirá a continuación en el explorador. (El estado **Publicado** se etiquetaba previamente como **En ejecución**).
* **Selección de sistema operativo de destino disponible en el momento de la publicación.** El cuadro de diálogo **Publicar en Azure** contiene un nuevo campo, **SO de destino**, que proporciona una manera más reconocible para establecer su sistema operativo de destino.
* **Sobrescritura automática de la implementación anterior**. El cuadro de diálogo **Publicar en Azure** contiene una nueva casilla, **Sobrescribir implementación anterior**. Si se activa esta opción, cuando se publique la nueva implementación se sobrescribirá automáticamente la implementación anterior; así no experimentará problemas con el &quot;conflicto 409&quot; al publicar en la misma ubicación sin anular primero la publicación de la implementación anterior.
* **Jetty 9 es ahora un servidor de aplicaciones reconocido.** Si selecciona un directorio de instalación de Jetty 9 en el equipo en la pestaña **Servidor** del cuadro de diálogo **Proyecto de implementación de Azure**, el complemento lo detectará automáticamente y podrá implementar Jetty 9 de forma automática, de manera similar a las versiones anteriores de Jetty que ya están en la lista.
* **Adición de un rol desde el menú contextual del proyecto.** El menú contextual del proyecto de **Azure** contiene ahora un nuevo elemento de menú, **Agregar rol**, que proporciona una forma más rápida y reconocible de agregar un nuevo rol al proyecto de Azure.
* **Una actualización para el paquete de las bibliotecas de Azure para la biblioteca de Java.** Esta se basa en la versión 0.4.6 de la [API de cliente de Microsoft Azure].

### <a name="september-25-2013"></a>25 de septiembre de 2013
Se ha publicado el complemento de Azure para Eclipse, versión preliminar de septiembre de 2013. Esta actualización incluye nuevas características, correcciones de errores y algunas mejoras de facilidad de uso basadas en comentarios que se han producido desde la versión preliminar de agosto de 2013:

* **Capacidad para implementar el paquete de Zulu de OpenJDK de Azul disponible en Azure.** Se ha agregado una nueva opción al especificar el JDK que desea usar con la implementación de Azure. Con esta opción, puede implementar un paquete JDK de terceros directamente en la nube de Azure, sin tener que cargar los suyos propios. Azul Systems ofrece el primer paquete de este tipo llamado Zulu, basado en OpenJDK, que ahora se puede implementar mediante esta opción.
* **Una actualización para el paquete de las bibliotecas de Azure para la biblioteca de Java.** Esta se basa en la versión 0.4.5 de la [API de cliente de Microsoft Azure].

### <a name="august-1-2013"></a>1 de agosto de 2013
Se ha publicado el complemento de Azure para Eclipse, versión preliminar de agosto de 2013. Se trata de una actualización que acompaña a la versión 2.1 del SDK de Azure, que es un requisito previo y se descargará automáticamente al instalar el complemento. Esta actualización incluye nuevas características, correcciones de errores y algunas mejoras de facilidad de uso basadas en comentarios que se han producido desde la versión preliminar de julio de 2013:

* **Eliminación de opciones para incluir el JDK local y el servidor de aplicaciones local como parte del paquete de implementación.** Descargar el JDK y el servidor de aplicaciones del almacenamiento en la nube durante la implementación es preferible a insertar estos componentes en el paquete, puesto que la descarga de elementos da como resultado paquetes de implementación de menor tamaño, tiempos de implementación más rápidos y un mantenimiento más sencillo. Como resultado, se han quitado las opciones para incluir el JDK y el servidor de aplicaciones en el paquete de implementación. Los proyectos existentes que se configuraron para incluir el JDK local y el servidor de aplicaciones local como parte del paquete de implementación se convertirán automáticamente para la carga automática del JDK y del servidor de aplicaciones en el almacenamiento en la nube.
* **Compatibilidad con la versión 2.1 del SDK de Azure.** El complemento de Azure para Eclipse, versión preliminar de agosto de 2013, requiere la versión 2.1 del SDK de Azure. No utilice la versión preliminar de agosto de 2013 con versiones anteriores del SDK de Azure y no utilice la versión 2.1 con versiones anteriores del complemento de Azure para Eclipse.
* **Compatibilidad con la versión Kepler de Eclipse.** En relación con esto, la nueva versión mínima necesaria del IDE de Eclipse es Indigo. El complemento de Azure para Eclipse ha dejado de probarse oficialmente en Helios.

### <a name="july-3-2013"></a>3 de julio de 2013
Se ha publicado el complemento de Azure para Eclipse, versión preliminar de julio de 2013. Esta actualización incluye nuevas características, correcciones de errores y algunas mejoras de facilidad de uso basadas en comentarios que se han producido desde la versión preliminar de mayo de 2013:

* **Capacidad de crear una cuenta de almacenamiento.** Se ha agregado el botón **Nueva** al cuadro de diálogo **Agregar cuenta de almacenamiento**. Esto le permite crear una cuenta de almacenamiento dentro del complemento de Eclipse, sin necesidad de iniciar sesión en el portal de administración de Azure. (Debe tener una suscripción de Azure para usar esta característica). Para más información acerca de la creación de una cuenta de almacenamiento, consulte [Creación de una nueva cuenta de almacenamiento].
* **Nueva opción &quot;(automática)&quot; de cuenta de almacenamiento usada para la implementación automática de JDK y del servidor y para almacenamiento en caché.** Al usar la opción **Cargar automáticamente** para el JDK y el servidor de aplicaciones, podrá ya especificar la opción **(automática)** para la cuenta de almacenamiento y la dirección URL que se usarán al cargar el JDK y el servidor de aplicaciones, o al usar el almacenamiento en caché de Azure. En ese momento, estas características usarán automáticamente la misma cuenta de almacenamiento que la que seleccionó en el cuadro de diálogo **Publicar en Azure** . Se ha actualizado el tutorial [Creación de una aplicación Hola a todos para Azure en Eclipse] para incluir el uso de la nueva opción **(automática)** .
* **Capacidad de configurar los puntos de conexión de servicio de Azure.** Especifique los puntos de conexión de servicio que determinan si la aplicación se implementa y se administra en la plataforma global de Azure, es operada en Azure por medio de 21Vianet en China o en una plataforma privada de Azure. Para más información, consulte [Puntos de conexión de servicio de Azure].
* **Las implementaciones de gran tamaño pueden especificar un recurso de almacenamiento local.** En caso de que su implementación sea demasiado grande para incluirse en la carpeta approot predeterminada, ahora puede especificar un recurso de almacenamiento local como destino de implementación para el JDK y el servidor de aplicaciones. Para más información, consulte [Deploying Large Deployments].
* **Compatibilidad con los tamaños A6 y A7 de máquinas virtuales de Azure.** Ahora ya puede implementar un servicio en la nube con los tamaños de máquinas virtuales de memoria alta A6 y A7. Para más información sobre estos tamaños, consulte [Tamaños de máquinas virtuales y servicios en la nube de Azure].
* **Una actualización para el paquete de las bibliotecas de Azure para la biblioteca de Java.** Esta se basa en la versión 0.4.4 de la [API de cliente de Microsoft Azure].

### <a name="may-1-2013"></a>1 de mayo de 2013
Se ha publicado el complemento de Azure para Eclipse, versión preliminar de mayo de 2013. Se trata de una actualización principal que acompaña a la versión 2.0 del SDK de Azure, que es un requisito previo y se descargará automáticamente al instalar el complemento. Esta versión incluye nuevas características, correcciones de errores y algunas mejoras de facilidad de uso basadas en comentarios que se han producido desde la versión preliminar de febrero de 2013:

* **Carga automática del JDK y del servidor de aplicaciones en Azure Storage, e implementación desde allí.** Una nueva opción que automáticamente cargará el JDK y el servidor de aplicaciones seleccionados, cuando sea necesario, en una cuenta de Azure Storage especificada e implementará estos componentes desde allí, en lugar de insertar en el paquete de implementación o hacer que el usuario los cargue manualmente. Esta característica habitualmente solicitada puede mejorar considerablemente la facilidad de implementación de los componentes de servidor y del JDK, especialmente para los usuarios inexpertos. Para ver un tutorial que use estas opciones, consulte [Creación de una aplicación Hola a todos para Azure en Eclipse].
* **Seguimiento centralizado de la cuenta de almacenamiento y capacidad para hacer referencia a cuentas de almacenamiento más fácilmente (a través de un control desplegable).** Esto se aplica a varias características que dependen del almacenamiento, como el JDK y la implementación de componentes de servidor y el almacenamiento en caché. Para más información, consulte [Lista de cuentas de Azure Storage].
* **Configuración simplificada de acceso remoto en el asistente Publicar en la nube.** Todo lo que necesita hacer es escribir un nombre de usuario y una contraseña para habilitar el acceso remoto, o dejarlos en blanco para mantener el acceso remoto deshabilitado.
* **Una actualización para el paquete de las bibliotecas de Azure para la biblioteca de Java.** Esta se basa en la versión 0.4.2 de la [API de cliente de Microsoft Azure].
* **Compatibilidad con sesiones temporales en Windows Server 2012.** Anteriormente, las sesiones temporales funcionaban solo en Windows Server 2008 R2, ahora ambos destinos de sistemas operativos en la nube admiten afinidad de sesiones.
* **Mejoras en el rendimiento de la carga de paquete.** Incluso cuando se inserta el JDK y el servidor de aplicaciones en el paquete de implementación, la parte de carga del proceso de implementación es aproximadamente dos veces más rápida en comparación con versiones anteriores.

### <a name="february-8-2013"></a>8 de febrero de 2013
Se ha publicado el complemento de Azure para Eclipse, versión preliminar de febrero de 2013. Esta actualización secundaria incluye correcciones de errores, mejoras de facilidad de uso basadas en comentarios y algunas características nuevas que se han producido desde la versión preliminar de noviembre de 2012:

* Compatibilidad para implementar JDK, servidores de aplicaciones y otros componentes arbitrarios desde descargas públicas o privadas desde Azure Blob Storage en lugar de incluirlos en el paquete de implementación a la hora de implementarlos en la nube.
* Capacidad para cambiar el orden en que se procesan los componentes definidos por el usuario de un rol, mediante la adición de los botones **Subir** y **Bajar** en la sección **Componentes** de las **propiedades del rol de Azure**.
* Actualización del **paquete para bibliotecas de Azure para la biblioteca de Java** , basada en la versión 0.4.0 de la [API de cliente de Microsoft Azure].

### <a name="november-5-2012"></a>5 de noviembre de 2012
Se ha publicado el complemento de Azure para Eclipse, versión preliminar de noviembre de 2012. Esta es una actualización principal que incluye varias características nuevas, así como correcciones de errores adicionales y mejoras de facilidad de uso basadas en comentarios que se han producido desde la versión preliminar de septiembre de 2012:

* Compatibilidad con Microsoft Windows Server 2012 como sistema operativo en la nube.
* Compatibilidad con el soporte colocado de almacenamiento en caché de Azure para clientes con Memcaché.
* Inclusión de las bibliotecas de cliente Apache Qpid JMS para aprovechar la mensajería basada en AMQP de Azure.
* Mejora del asistente **Nuevo proyecto** , con una nueva página al final que proporciona a los usuarios la capacidad de habilitar rápidamente varias características clave comunes en el proyecto: sesiones temporales, almacenamiento en caché y depuración remota.
* Reducción automática de instancias de rol a 1 cuando se ejecuta en el emulador de proceso, para evitar conflictos de enlace de puerto entre instancias de servidor.

### <a name="september-28-2012"></a>28 de septiembre de 2012
Se ha publicado el complemento de Azure para Eclipse, versión preliminar de septiembre de 2012. Esta actualización de servicio incluye una serie de correcciones de errores adicionales realizadas desde la versión preliminar de agosto de 2012, así como algunas mejoras de facilidad de uso en las características ya existentes basadas en comentarios:

* Compatibilidad con Microsoft Windows 8 y Microsoft Windows Server 2012 como sistemas operativos de desarrollo, solucionando así los problemas que anteriormente impidieron que el complemento funcionara correctamente en esos sistemas operativos.
* Compatibilidad mejorada para especificar intervalos de puerto del punto de conexión.
* Correcciones de errores relacionados con las rutas de acceso a archivos que contienen espacios.
* Mejoras en el menú contextual de rol para un acceso más rápido a los valores de configuración específicos del rol.
* Pequeños refinamientos en el asistente **Publicar en la nube** y una serie de correcciones de errores adicionales.

### <a name="august-28-2012"></a>28 de agosto de 2012
Se ha publicado el complemento de Azure para Eclipse, versión preliminar de agosto de 2012. Esta actualización de servicio incluye correcciones de errores adicionales realizadas desde la versión preliminar de julio de 2012, así como algunas mejoras de facilidad de uso en las características ya existentes basadas en comentarios:

* En el cuadro de diálogo Filtro de Azure Access Control Service:
  * **Opción para insertar el certificado de firma** en el archivo WAR de la aplicación, para simplificar la implementación en la nube.
  * **Opción para crear un certificado autofirmado** dentro de la interfaz de usuario del filtro ACS. Para obtener información adicional sobre el filtro de Azure Access Control Service, consulte [Autenticación de usuarios web con Azure Access Control Service mediante Eclipse].
* En el asistente para proyectos de implementación de Azure (también se aplica a la página de propiedades de configuración del servidor del rol):
  * **Detección automática de la ubicación del JDK** en el equipo (que puede reemplazar si lo desea).
  * **Detección automática del tipo de servidor** al seleccionar el directorio de instalación del servidor de aplicaciones.

### <a name="july-15-2012"></a>15 de julio de 2012
Se ha publicado el complemento de Azure para Eclipse, versión preliminar de julio de 2012, que soluciona varios de los errores más prioritarios encontrados y/o notificados por los usuarios después de la versión de junio de 2012. Esta es solo una actualización de servicio, no se incluyen nuevas características.

### <a name="june-7-2012"></a>7 de junio de 2012
Se ha publicado el complemento de Azure para Eclipse, CTP de junio de 2012. Las nuevas características incluyen:

* **Nuevo asistente para proyecto de implementación de Azure:** le permite seleccionar el JDK, el servidor de aplicaciones Java y las aplicaciones de Java directamente en la interfaz de usuario mejorada del asistente. Incluidas en la lista de configuraciones del servidor listas para usar, puede elegir Tomcat 6, Tomcat 7, GlassFish OSE 3, Jetty 7, Jetty 8, JBoss 6 y JBoss 7 (independiente). Además, puede personalizar la lista de configuraciones del servidor. Esta mejora de la interfaz de usuario es una alternativa a arrastrar y colocar archivos comprimidos y copiarlos a través de scripts de inicio, que antes era el método principal. Ese método todavía funciona bien, pero es probable que se use solo para escenarios más avanzados.
* **Página de propiedades de rol de la configuración del servidor:** le permite cambiar fácilmente los JDK, los servidores de aplicaciones de Java y las aplicaciones asociadas con la implementación después de haber creado el proyecto. Para más información, consulte [Propiedades de configuración del servidor].
* **&quot;Asistente &quot;Publicar en la nube **: proporciona una manera fácil de implementar el proyecto en Azure directamente desde Eclipse, automatizando el pesado proceso manual anterior de obtención de credenciales, inicio de sesión en el portal de administración de Azure, carga de un paquete, etc. Para obtener un ejemplo de cómo implementar el proyecto directamente en Azure, consulte [Creación de una aplicación Hola a todos para Azure en Eclipse]
* **Barra de herramientas de Azure:** una barra de herramientas de Azure que está ahora disponible en Eclipse contiene botones que invocan las siguientes características:
  * ![][ic710879] **Ejecutar en emulador de Azure**: ejecuta el proyecto en el emulador.
  * ![][ic710880] **Restablecer emulador de Azure**: restablece el emulador.
  * ![][ic710881] **Crear paquete en la nube para Azure**: compila el paquete para la implementación.
  * ![][ic710876] **Nuevo proyecto de implementación de Azure**: crea un nuevo proyecto de implementación de Azure.
  * ![][ic710882] **Publicar en la nube de Azure**: publica el proyecto en Azure.
  * ![][ic710883] **Cancelar la publicación**: elimina la implementación.
  * Muchos de estos botones de la barra de herramientas de Azure se usan en [Creación de una aplicación Hola a todos para Azure en Eclipse].
* **Bibliotecas de Azure para Java:** ahora disponibles como parte del paquete único de bibliotecas de Azure para la biblioteca de Java en Eclipse, que acompaña a la instalación del complemento y que contiene también todas las dependencias necesarias. Simplemente agregue una referencia a la biblioteca en el proyecto de Java y no necesitará descargar nada por separado. Para más información, consulte [Instalación del kit de herramientas de Azure para Eclipse].
* **Microsoft JDBC Driver 4.0 para SQL Server está disponible durante la instalación del complemento:** durante la instalación del complemento nuevo, se puede instalar la versión más reciente de Microsoft JDBC Driver para SQL Server.
* **Filtro de Azure Access Control Service disponible durante la instalación del complemento:** este componente nuevo, incluido como una biblioteca de Eclipse en el kit de herramientas, habilita a la aplicación web de Java para aprovecharse sin problemas de la autenticación de Azure Access Control Service (ACS) mediante varios proveedores de identidades, como Google, Live.com y Yahoo!. No necesitará escribir la lógica de autenticación personalmente, solo tiene que configurar algunas opciones y dejar que el filtro haga el trabajo pesado de habilitar a los usuarios para iniciar sesión mediante ACS. Así puede centrarse solo en escribir el código que proporciona a los usuarios acceso a los recursos basándose en su identidad, tal como lo devuelve el filtro del objeto de solicitud a la aplicación. Para obtener un tutorial sobre cómo usar el filtro de ACS, consulte [Autenticación de usuarios web con Azure Access Control Service mediante Eclipse].
* **Detección automática de los requisitos previos de la versión 1.7 del SDK de Azure:** al crear un nuevo proyecto de implementación de Azure, esta versión se descargará automáticamente si no está ya instalada.
* **Puntos de conexión de instancia:** permite el acceso directo del punto de conexión del puerto para la comunicación con instancias de rol de carga equilibrada. Se pueden agregar los puntos de conexión de instancia a través de la interfaz de usuario de los puntos de conexión, disponible en la página [Propiedades de puntos de conexión] . Esto ayuda a habilitar la depuración remota y el diagnóstico de JMX para instancias de proceso específicas que se ejecutan en la nube en escenarios con implementaciones de varias instancias. 
* **Interfaz de usuario para componentes:** facilita a los usuarios avanzados la configuración de las dependencias del proyecto entre los roles individuales de Azure en el proyecto y otros recursos externos como los proyectos de aplicación de Java; también facilita la descripción de su lógica de implementación. Para más información, consulte [Propiedades de componentes].
* **Actualización automática de versiones anteriores de proyectos:** si abre un área de trabajo que tiene un proyecto creado con una versión anterior del complemento de Azure, los proyectos antiguos aparecerán en Eclipse como cerrados, porque las versiones anteriores de proyectos no son compatibles con la nueva versión. Si intenta abrir uno de estos proyectos antiguos, se iniciará un asistente de actualización. Si acepta la actualización, se creará un proyecto, con **_Upgraded** anexado al nombre, y se actualizará automáticamente para funcionar con la nueva versión. Puede cambiar el nombre del nuevo proyecto según sea necesario. Como parte de la actualización, el proyecto original no se modificará (y permanecerá cerrado).

### <a name="december-10-2011"></a>10 de diciembre de 2011
Se ha publicado el complemento de Azure para Eclipse, CTP de diciembre de 2011. Las nuevas características incluyen:

* **Compatibilidad con afinidad de la sesión (&quot;sesiones temporales&quot;):** ayuda a habilitar las aplicaciones agrupadas en clúster de Java con estado con solo una casilla. Para más información, consulte [Enable Session Affinity].
* **Ejemplos de scripts de inicio realizados previamente:** para los servidores Java más populares (Tomcat, Jetty, JBoss, GlassFish), que puede simplemente copiar y pegar desde el directorio de ejemplos del proyecto en el script de inicio.
* **Resultados de inicio del emulador en tiempo real:** ahora puede ver la ejecución de todos los pasos desde el script de inicio en una ventana de consola dedicada, que muestra el progreso y los errores en el script que se ejecuta en Azure.
* **Supervisión automática y ligera de java.exe:** que forzará un reciclado de rol cuando java.exe deje de funcionar, mediante un script ligero, realizado previamente e incluido automáticamente en la implementación.
* **Interfaz de usuario de configuración de depuración de la aplicación de Java remota:** permite habilitar fácilmente el depurador remoto de Eclipse para obtener acceso a la aplicación de Java que se ejecuta en el emulador o en la nube de Azure, para que pueda recorrer paso a paso y depurar el código de Java en tiempo real. Para más información, consulte [Depuración de aplicaciones de Azure en Eclipse].
* **Interfaz de usuario de configuración de recurso de almacenamiento local:** gracias a ello ya no tendrá que configurar recursos locales editando el XML directamente. Esta característica también le habilita para acceder a la ruta de acceso al archivo efectiva de su recurso local después de implementarlo a través de una variable de entorno a la que puede hacer referencia directamente desde el script de inicio. Para más información, consulte [Propiedades de almacenamiento local].
* **Interfaz de usuario de configuración de variable de entorno:** gracias a ello ya no es necesario establecer variables de entorno mediante la edición manual de la configuración del XML. Para más información, consulte [Propiedades de variables de entorno].
* **JDBC Driver para SQL Azure:** se instala a través del complemento como una biblioteca de Eclipse perfectamente integrada, lo cual permite una programación más fácil en SQL Azure. 
* **Acceso rápido de menú contextual a la interfaz de usuario de configuración del rol**: simplemente haga clic con el botón derecho en la carpeta de rol y haga clic en **Propiedades**.
* **Iconos de carpeta de rol y de proyecto de Azure personalizados:** para una mejor visibilidad y navegación más sencilla dentro de su área de trabajo y del proyecto.

## <a name="next-steps"></a>Pasos siguientes

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<!-- URL List -->

[Kit de herramientas de Azure para IntelliJ]: ../intellij/azure-toolkit-for-intellij.md
[Instalación del Kit de herramientas de Azure para Eclipse]: azure-toolkit-for-eclipse-installation.md

[Instrucciones de inicio de sesión de Azure del kit de herramientas de Azure para Eclipse]: azure-toolkit-for-eclipse-sign-in-instructions.md
[Cómo publicar una aplicación web como un contenedor de Docker mediante el kit de herramientas de Azure para Eclipse]: ./azure-toolkit-for-eclipse-publish-as-docker-container.md
[Administración de cuentas de almacenamiento mediante Azure Explorer para Eclipse]: ./azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer.md
[Administración de máquinas virtuales mediante Azure Explorer para Eclipse]: ./azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer.md

[Azure Java Developer Center]: https://docs.microsoft.com/java/azure

[página web de Azul Systems para Zulu de OpenJDK]: http://go.microsoft.com/fwlink/?LinkId=402457
[Puntos de conexión de servicio de Azure]: http://go.microsoft.com/fwlink/?LinkID=699526
[Lista de cuentas de Azure Storage]: http://go.microsoft.com/fwlink/?LinkID=699528
[Propiedades de componentes]: http://go.microsoft.com/fwlink/?LinkID=699525#components_properties
[Creación de una aplicación Hola a todos para Azure en Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Depuración de aplicaciones de Azure en Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699535
[Deploying Large Deployments]: http://go.microsoft.com/fwlink/?LinkID=699536
[Propiedades de puntos de conexión]: http://go.microsoft.com/fwlink/?LinkID=699525#endpoints_properties
[Propiedades de variables de entorno]: http://go.microsoft.com/fwlink/?LinkID=699525#environment_variables_properties
[Complemento Herramientas de HDInsight para Eclipse]: /azure/hdinsight/hdinsight-apache-spark-eclipse-tool-plugin
[Autenticación de usuarios web con Azure Access Control Service mediante Eclipse]: http://go.microsoft.com/fwlink/?LinkID=264703
[ Uso de la descarga de SSL]: http://go.microsoft.com/fwlink/?LinkID=699545
[Propiedades de almacenamiento local]: http://go.microsoft.com/fwlink/?LinkID=699525#local_storage_properties
[API de cliente de Microsoft Azure]: http://go.microsoft.com/fwlink/?LinkId=280397
[Propiedades de configuración del servidor]: http://go.microsoft.com/fwlink/?LinkID=699525#server_configuration_properties
[Enable Session Affinity]: http://go.microsoft.com/fwlink/?LinkID=699548
[SSL Offloading]: http://go.microsoft.com/fwlink/?LinkID=699549
[Creación de una nueva cuenta de almacenamiento]: http://go.microsoft.com/fwlink/?LinkID=699528#create_new
[Tamaños de máquinas virtuales y servicios en la nube de Azure]: http://go.microsoft.com/fwlink/?LinkId=466520

<!-- IMG List -->

[ic710876]: media/azure-toolkit-for-eclipse-whats-new/ic710876.png
[ic710877]: media/azure-toolkit-for-eclipse-whats-new/ic710877.png
[ic710879]: media/azure-toolkit-for-eclipse-whats-new/ic710879.png
[ic710880]: media/azure-toolkit-for-eclipse-whats-new/ic710880.png
[ic710881]: media/azure-toolkit-for-eclipse-whats-new/ic710881.png
[ic710876]: media/azure-toolkit-for-eclipse-whats-new/ic710876.png
[ic710882]: media/azure-toolkit-for-eclipse-whats-new/ic710882.png
[ic710883]: media/azure-toolkit-for-eclipse-whats-new/ic710883.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh694270.aspx -->
