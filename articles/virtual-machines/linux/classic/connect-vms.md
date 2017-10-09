---
title: bir bulut hizmetinde Linux VM'ler aaaConnect | Microsoft Docs
description: "Merhaba Klasik dağıtım modeli tooan Azure bulut hizmeti veya sanal ağ ile oluşturulan Linux sanal makineleri bağlayın."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 2fd23055-6b34-4ef0-88a8-fc19e32fb3c9
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/06/2017
ms.author: cynthn
ms.openlocfilehash: 323baf04390d53ffb2810e24a24d175c08e60cd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-linux-virtual-machines-created-with-hello-classic-deployment-model-with-a-virtual-network-or-cloud-service"></a>Bir sanal ağ veya Bulut hizmeti ile Merhaba Klasik dağıtım modeliyle oluşturulan Linux sanal makineleri Bağlan
> [!IMPORTANT]
> Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md). Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır. Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.

Merhaba Klasik dağıtım modeliyle oluşturulan Linux sanal makinelerin her zaman bir bulut hizmetinde yerleştirilir. Merhaba bulut hizmeti, bir kapsayıcı gibi davranır ve benzersiz bir genel DNS adı, bir ortak IP adresi ve bitiş noktaları tooaccess hello sanal makine kümesi hello Internet sağlar. Merhaba bulut hizmeti sanal bir ağa olabilir, ancak bu zorunlu değildir. Ayrıca [bir sanal ağ veya Bulut hizmeti ile Windows sanal makinelere bağlanmak](../../windows/classic/connect-vms.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

Bir bulut hizmeti bir sanal ağ içinde değilse, adlı bir *tek başına* bulut hizmeti. bir tek başına bulut hizmeti Hello sanal makinelerin diğer sanal makinelerle kullanarak diğer sanal makinelerin Genel DNS adlarını hello ve hello trafiği hello Internet geçen iletişim kurar. Bulut hizmeti ile Merhaba sanal ağdaki diğer tüm sanal makineler hello Internet herhangi bir trafik göndermeden iletişim kurabilir, bir sanal ağ içinde hello sanal makineler bir bulut hizmeti ise.

Yerleştirdiğiniz varsa aynı tek başına bulut hizmeti sanal makinelerinizi Merhaba, Yük Dengeleme kullanmaya devam edebilirsiniz ve kullanılabilirlik ayarlar. Ayrıntılar için bkz [Yük Dengeleme sanal makineleri](../../virtual-machines-linux-load-balance.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ve [hello sanal makinelerin kullanılabilirliğini yönetme](../manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Ancak, alt ağlar hello sanal makinelerde düzenlemek veya tek başına bulut hizmeti tooyour şirket içi ağ bağlanabilirsiniz. Örnek aşağıda verilmiştir:

[!INCLUDE [virtual-machines-common-classic-connect-vms](../../../../includes/virtual-machines-common-classic-connect-vms.md)]

## <a name="next-steps"></a>Sonraki adımlar
Bir sanal makineyi oluşturduktan sonra bir çok fikirdir[bir veri diski Ekle](attach-disk.md) Hizmetleri ve iş yükleri bir konum toostore verileri alacak şekilde.
