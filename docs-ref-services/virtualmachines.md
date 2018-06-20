---
title: Bibliotecas de Azure Virtual Machines para Java
description: ''
keywords: Azure, Java, SDK, API, Compute, Virtual Machines
author: douge
ms.author: douge
manager: douge
ms.date: 05/17/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: compute
ms.openlocfilehash: a54bc40e1d28ba6ee1d8b0638cb259adbb69d78d
ms.sourcegitcommit: 49b17bbf34732512f836ee634818f1058147ff5c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
ms.locfileid: "31823758"
---
# <a name="azure-virtual-machine-libraries"></a>Bibliotecas de Azure Virtual Machines

## <a name="overview"></a>Información general

Recursos informáticos bajo demanda y escalables que se ejecutan en Linux o Windows.

Para empezar a trabajar con Azure Virtual Machines, consulte [Creación de una máquina virtual Linux con Azure Portal](/azure/virtual-machines/linux/quick-create-portal).

## <a name="management-api"></a>API de administración

Cree, configure y escale horizontalmente máquinas virtuales Windows y Linux de Azure desde código con la API de administración.

[Agregue una dependencia](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) al archivo `pom.xml` de Maven para utilizar la API de administración en el proyecto.  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-compute</artifactId>
    <version>1.3.0</version>
</dependency>
```   


## <a name="example"></a>Ejemplo

Cree una nueva máquina virtual Linux en un nuevo grupo de recursos de Azure.

```java
VirtualMachine newLinuxVm = azure.virtualMachines().define(linuxVmName)
            .withRegion(Region.US_EAST)
            .withNewResourceGroup("myResourceGroup")
            .withNewPrimaryNetwork("10.0.0.0/28")
            .withPrimaryPrivateIpAddressDynamic()
            .withoutPrimaryPublicIpAddress()
            .withPopularLinuxImage(KnownLinuxVirtualMachineImage.UBUNTU_SERVER_16_04_LTS)
            .withRootUsername(userName)
            .withSshKey(key)
            .withSize(VirtualMachineSizeTypes.STANDARD_D3_V2)
            .create();
```

> [!div class="nextstepaction"]
> [Explorar las API de administración](/java/api/overview/azure/virtualmachines/management)


## <a name="samples"></a>Ejemplos

[Administración de máquinas virtuales][1]   
[Administración de redes virtuales][6]   
[Creación de una máquina virtual desde una imagen personalizada][2]   
[Creación de máquinas virtuales en varias regiones en paralelo][5]    
[Creación de un conjunto de escalado de máquinas virtuales con un equilibrador de carga][7]    

[1]: ../docs-ref-conceptual/java-sdk-manage-virtual-machines.md
[2]: https://azure.microsoft.com/resources/samples/managed-disk-java-create-virtual-machine-using-custom-image/
[5]: ../docs-ref-conceptual/java-sdk-virtual-machines-in-parallel.md
[6]: ../docs-ref-conceptual/java-sdk-manage-virtual-networks.md
[7]: ../docs-ref-conceptual/java-sdk-manage-vm-scalesets.md

Ver más [código de Java de ejemplo para Azure Virtual Machines](https://azure.microsoft.com/resources/samples/?platform=java&term=VM) que puede usar en las aplicaciones.