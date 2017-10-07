---
title: "aaaLinux VM boyutları Azure'da | Microsoft Docs"
description: "Farklı boyutlarda Hello Azure Linux sanal makineler için kullanılabilir listeler."
services: virtual-machines-linux
documentationcenter: 
author: jonbeck7
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: da681171-f045-4c80-a5a9-d8bd47964673
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 07/28/2017
ms.author: jonbeck
ms.openlocfilehash: 56cbe0a0d7d34def07636edba74c4c699e336012
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="sizes-for-linux-virtual-machines-in-azure"></a>Azure'daki Linux sanal makineler için Boyutlar
Bu makalede hello kullanılabilir boyutları ve Linux uygulamaları ve iş yüklerini toorun kullanabileceğiniz Azure sanal makineler için başlangıç seçenekleri. Bu kaynaklar toouse planlaması yaparken de dağıtım konuları toobe farkında sağlar. Bu makalede ayrıca kullanılabilir [Windows sanal makineleri](../windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).


| Tür                     | Boyutlar           |    Açıklama       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| [Genel amaçlı](sizes-general.md)          | Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7  | Dengeli CPU/bellek oranı. Test ve geliştirme, küçük toomedium veritabanları ve düşük toomedium trafiği web sunucuları için idealdir. |
| [İşlem için iyileştirilmiş](sizes-compute.md)        | FS, F             | Yüksek CPU/bellek oranı. Orta düzey trafik web sunucuları, ağ cihazları, banyo işlemleri ve uygulama sunucuları için iyidir.        |
| [Bellek için iyileştirilmiş](sizes-memory.md)         | Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D   | Yüksek bellek CPU oranı. İlişkisel veritabanı sunucuları, Orta toolarge önbellekleri ve bellek içi analizi için mükemmel.                 |
| [Depolama için iyileştirilmiş](sizes-storage.md)        | Ls                | Yüksek disk aktarım hızı ve GÇ. Büyük Veri, SQL ve NoSQL veritabanları için ideal.                                                         |
| [GPU](sizes-gpu.md)            | NV, NC            | Yoğun Grafik işleme ve video düzenleme için hedeflenen özelleştirilmiş sanal makineler. Tek veya birden çok GPU ile kullanılabilir.       |
| [Yüksek performanslı işlem](sizes-hpc.md) | H, A8-11          | İşleme düzeyi yüksek olan isteğe bağlı ağ arabirimleri (RDMA) içeren sanal makineler, şimdiye kadarki en hızlı ve en güçlü CPU ile sunuluyor. 

<br>

- Merhaba çeşitli boyutlarda fiyatlandırma hakkında daha fazla bilgi için bkz: [sanal makineler fiyatlandırma](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux). 
- VM boyutları Azure bölgelerindeki kullanılabilirlik için bkz: [bölgeye göre ürünleri](https://azure.microsoft.com/regions/services/).
- Azure vm'lerinde toosee genel sınırları bkz [Azure aboneliği ve hizmet sınırları, kotaları ve kısıtlamaları](../../azure-subscription-service-limits.md).
- Hakkında daha fazla bilgi [Azure işlem birimleri (ACU)](../windows/acu.md) Azure SKU'ları üzerinde işlem performans karşılaştırmanıza yardımcı olur.


## <a name="rest-api"></a>REST API'si

VM boyutları için hello REST API tooquery kullanma hakkında daha fazla bilgi için hello aşağıdakilere bakın:

- [Yeniden boyutlandırma için kullanılabilir sanal makine boyutlarını Listele](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-for-resizing)
- [Bir abonelik için kullanılabilir sanal makine boyutlarını Listele](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region)
- [Bir kullanılabilirlik kümesinde kullanılabilir sanal makine boyutlarını Listele](
https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-availability-set)

## <a name="acu"></a>ACU

Hakkında daha fazla bilgi [Azure işlem birimleri (ACU)](acu.md) Azure SKU'ları üzerinde işlem performans karşılaştırmanıza yardımcı olur.

## <a name="next-steps"></a>Sonraki adımlar

Kullanılabilen hello farklı VM boyutları hakkında daha fazla bilgi edinin:
- [Genel amaçlı](sizes-general.md)
- [İşlem için iyileştirilmiş](sizes-compute.md)
- [Bellek için iyileştirilmiş](sizes-memory.md)
- [Depolama için iyileştirilmiş](sizes-storage.md)
- [GPU](sizes-gpu.md)
- [Yüksek performanslı işlem](sizes-hpc.md)



