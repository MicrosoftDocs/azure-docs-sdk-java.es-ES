---
ms.openlocfilehash: ab31ee32ea940db2d7bcfa2fe36475d8a648bfc9
ms.sourcegitcommit: 115f4c8ad07a11f17d79e9d945d63917836b11c8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "61592620"
---
| **Creación de máquinas virtuales** || 
|---|---|
| [Administración de máquinas virtuales][1] | Cree, modifique, inicie, detenga y elimine máquinas virtuales. |
| [Creación de una máquina virtual desde una imagen personalizada][2] | Cree una imagen de máquina virtual personalizada y úsela para crear nuevas máquinas virtuales. | 
| [Creación de una máquina virtual mediante un VHD especializado desde una instantánea][3] | Cree una instantánea del sistema operativo de la máquina virtual y los discos de datos, cree discos administrados a partir de las instantáneas y, a continuación, asocie los discos administrados para crear una máquina virtual. |  
| [Creación de máquinas virtuales en paralelo en la misma red][4] | Cree máquinas virtuales en la misma región de la misma red virtual con dos subredes en paralelo. |
| [Creación de máquinas virtuales en varias regiones en paralelo][5] | Cree y equilibre la carga de un conjunto de máquinas virtuales a través de varias regiones de Azure. |
| **Máquinas virtuales de red** || 
| [Administración de redes virtuales][6] | Configure una red virtual con dos subredes y restrinja el acceso a Internet a ellas. |
| **Creación de conjuntos de escalado** ||
| [Creación de un conjunto de escalado de máquinas virtuales con un equilibrador de carga][7] | Cree un conjunto de escalado de máquinas virtuales, configure un equilibrador de carga y obtenga las cadenas de conexión SSH a las máquinas virtuales del conjunto de escalado. |

[1]: ../java-sdk-manage-virtual-machines.md
[2]: https://azure.microsoft.com/resources/samples/managed-disk-java-create-virtual-machine-using-custom-image/
[3]: https://azure.microsoft.com/resources/samples/managed-disk-java-create-virtual-machine-using-specialized-disk-from-vhd/
[4]: https://azure.microsoft.com/resources/samples/compute-java-manage-virtual-machines-in-parallel/
[5]: ../java-sdk-virtual-machines-in-parallel.md
[6]: ../java-sdk-manage-virtual-networks.md
[7]: ../java-sdk-manage-vm-scalesets.md