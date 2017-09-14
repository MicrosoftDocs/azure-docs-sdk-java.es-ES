---
title: "Notas de la versión de las bibliotecas de administración de Azure para Java | Microsoft Docs"
description: "Vea las novedades y los cambios importantes en las bibliotecas de administración de Azure para Java"
keywords: Azure, Java, API, referencia, notas, actualizaciones, en desuso
author: routlaw
manager: douge
ms.assetid: 1f128cf9-f747-4344-84e1-f9964709deb8
ms.service: Azure
ms.devlang: java
ms.topic: reference
ms.technology: Azure
ms.date: 3/06/2016
ms.openlocfilehash: c0d5c4b3702d3bee4e93de51cec36e72aeaf598f
ms.sourcegitcommit: ae39830d5a54fedceac78d8df1718e77741e03fa
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/09/2017
---
# <a name="release-notes"></a>Notas de la versión 

## <a name="june-30-2017---110"></a>30 de junio de 2017-1.1.0 

V1.1 es compatible con la versión 1.0 de las API pensadas para uso público que alcanzaron la fase de disponibilidad general (estable) en la versión 1.0.

Se incorporaron algunos cambios importantes en las API marcadas con la anotación @Beta en la versión V.0

Si va a migrar código a la versión 1.1.0, puede usar [estas notas](https://github.com/Azure/azure-sdk-for-java/blob/master/notes/prepare-for-1.1.0.md) para preparar el código de 1.0.0 para 1.1.0.

### <a name="generally-availabile-in-v11"></a>Disponibilidad general en la versión V1.1

Algunas de las API que estaban todavía en la versión V1.0 beta ahora están disponibles de forma general en la versión V1.1, en concreto:

- métodos asincrónicos
- todos los métodos de la red CDN que anteriormente se encontraban en la versión beta
- todos los métodos y las interfaces de Application Gateway que anteriormente se encontraban en la versión beta

 Algunas partes de la biblioteca aún están en versión preliminar. Consulte la tabla siguiente sobre el estado actual de las bibliotecas:

Servicio o característica | Disponible de forma general | Disponible como versión preliminar  | Próximamente |
---------|---------|---------|---------|
Proceso  | Máquinas virtuales y extensiones de máquinas virtuales, conjuntos de escalado de máquinas virtuales, discos administrados   | Azure container service, Azure container registry |    |
Storage   |  Cuentas de almacenamiento       |         |   Cifrado      |
SQL Database  | Bases de datos, firewalls, grupos elásticos        |         |   Más características      |
Redes    |  Redes virtuales, interfaces de red, direcciones IP, tablas de enrutamiento, grupos de seguridad de red, DNS, administradores de tráfico, puertas de enlace de aplicaciones  |    Equilibradores de carga     |   VPN, monitores de red   |
Más servicios    |  Resource Manager, Key Vault, Redis, CDN, Batch       |  Aplicaciones web, aplicaciones de función, Service Bus, Graph RBAC, DocumentDB   | Supervisión, programación, funciones de administración, búsqueda, más características de Graph RBAC        |
Aspectos básicos     |   Autenticación: núcleo, métodos asincrónicos       |      |         |

### <a name="import-with-maven"></a>Importación con Maven

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure</artifactId>
    <version>1.2.1</version>
</dependency>
```

### <a name="get-help-and-give-feedback"></a>Obtener ayuda y proporcionar comentarios

Revisar la comunidad de [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-java-sdk) para obtener ayuda con las bibliotecas en su propio código. Si encuentra errores o tiene sugerencias para mejorar estas bibliotecas, puede enviarlas a través de [GitHub](https://github.com/Azure/azure-sdk-for-java/issues).

### <a name="migrate-from-previous-releases"></a>Migración desde versiones anteriores

[Migración desde 1.0.0-beta5](https://github.com/Azure/azure-sdk-for-java/blob/master/notes/prepare-for-1.0.0.md)  [Migración desde 1.1.0](https://github.com/Azure/azure-sdk-for-java/blob/master/notes/prepare-for-1.1.0.md)


