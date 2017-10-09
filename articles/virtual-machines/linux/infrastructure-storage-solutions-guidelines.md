---
title: "Linux VM'ler için Azure'da aaaStorage çözümleri | Microsoft Docs"
description: "Azure altyapı Hizmetleri'nde depolama çözümlerini dağıtma hello anahtar tasarım ve uygulama yönergeleri hakkında bilgi edinin."
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3c368f07-189b-4520-bbe2-f4080253bbf2
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d270c4786d7b55b18b011aa345063b6816a80876
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-infrastructure-guidelines-for-linux-vms"></a>Azure depolama altyapısı yönergeleri Linux VM'ler

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

Bu makalede, depolama gereksinimlerini ve sanal makine (VM) en iyi performans elde etmek için tasarım konuları anlamaya odaklanır.

## <a name="implementation-guidelines-for-storage"></a>Depolama için uygulama rehberi
Kararları:

* Toouse Azure diskleri yönetilen veya yönetilmeyen diskleri mısınız?
* İş yükü için toouse standart veya Premium depolama gerekiyor mu?
* Disk şeritleme toocreate diskler 4 TB'den büyük gerekiyor mu?
* İş yükü için disk şeritleme tooachieve en iyi g/ç performansı gerekiyor mu?
* Hangi depolama hesaplarını toohost BT iş yükü veya altyapı ihtiyacınız var?

Görevler:

* G/ç gereksinimlerini dağıtıyorsanız ve hello uygun rakam ve depolama hesapları türünü planlamak hello uygulamaları gözden geçirin.
* Depolama hesapları, adlandırma kuralını kullanarak Hello kümesi oluşturun. Hello Azure CLI veya hello portalı kullanabilirsiniz.

## <a name="storage"></a>Depolama
Azure depolama, sanal makineleri (VM'ler) ve uygulamaları dağıtma ve yönetme, önemli bir parçasıdır. Sanal makineleri destekleyen hello altyapı parçası olduğunu da ve Azure depolama dosya verileri, yapılandırılmamış verilerinizi ve iletileri depolamak için hizmetler sağlar.

[Azure yönetilen diskleri](../../storage/storage-managed-disks-overview.md) depolama hello arka planda işler. Yönetilmeyen diskler ile depolama hesapları Azure Vm'leriniz için toohold hello diskleri (VHD dosyaları) oluşturun. Yukarı ölçeklendirilirken tüm disklerinizi depolama için hello IOPS sınırı aşmayan için ek depolama hesapları oluşturulan emin olmanız gerekir. Yönetilen depolama işleme diskler ile Merhaba depolama hesabı sınırları tarafından artık sınırlıdır (20.000 IOPS gibi / hesabını). Ayrıca artık özel görüntülerini (VHD dosyaları) toomultiple depolama hesaplarınızı toocopy yok. Bunları merkezi bir konumda – Azure bölgesi başına bir depolama hesabı – yönetmek ve bunları toocreate yüzlerce VM'lerin bir abonelikte kullanın. Yeni dağıtımlar için yönetilen diskleri kullanmanızı öneririz.

Sanal makineleri desteklemek için kullanılabilen iki tür depolama hesabı vardır:

* Standart depolama hesapları verin (Azure VM diskleri depolamak için kullanılan) tooblob depolama erişim depolama, kuyruk depolama, tablo ve dosya depolama alanı.
* [Premium depolama](../../storage/storage-premium-storage.md) hesapları teslim g/ç yoğun iş yükleri, MongoDB parçalı küme gibi yüksek performanslı, düşük gecikmeli disk desteği. Premium depolama şu anda yalnızca Azure VM diskleri destekler.

Azure, bir işletim sistemi diski, geçici bir disk ve sıfır veya daha fazla isteğe bağlı veri diskleri VM'ler oluşturur. Hello geçici disk nerede hello makine yaşıyor hello düğümde yerel olarak depolanır ancak hello işletim sistemi diski ve veri diskleri Azure sayfa bloblarını markalarıdır. Tooonly VM bir bakım olayı sırasında konaklar arasında geçişi yapılacak hello olarak kalıcı olmayan verileri geçici bu diski kullanan uygulamalarını tasarlarken dikkatli olun. Merhaba geçici diskte depolanan tüm verileri kaybolacak.

Dayanıklılık ve yüksek kullanılabilirlik sağlanır hello temel Azure depolama ortamı tooensure tarafından verilerinizi planlanmamış Bakım veya donanım arızalarına karşı korumalı kalır. Azure depolama ortamınızı tasarlarken, tooreplicate VM depolama birini seçebilirsiniz:

* yerel olarak bir belirtilen Azure veri merkezi içinde
* belirli bir bölgedeki içerisinde Azure veri merkezi arasında
* farklı bölgelere Azure veri merkezleri arasında.

Okuyabilirsiniz [yüksek kullanılabilirlik için hello çoğaltma seçenekleri hakkında daha fazla](../../storage/storage-introduction.md#replication-for-durability-and-high-availability).

İşletim sistemi ve veri disklerle 4 TB maksimum boyuta sahip. Veri diskleri toopresent mantıksal 1023 GB tooyour VM büyük birimleri birlikte havuzu tarafından bu sınırı mantıksal Birimi Yöneticisi (LVM) toosurpass kullanabilirsiniz.

Bazı ölçeklenebilirlik sınırları - daha fazla bilgi için Azure Storage dağıtımlarınızın tasarlarken bkz [Microsoft Azure aboneliği ve hizmet sınırları, kotaları ve kısıtlamaları](../../azure-subscription-service-limits.md#storage-limits). Ayrıca bkz. [Azure storage ölçeklenebilirlik ve performans hedefleri](../../storage/storage-scalability-targets.md).

Uygulama depolaması için belgeler, görüntüler, yedeklemeler, yapılandırma verileri, günlükleri, vb. gibi yapılandırılmamış nesne verilerini depolayabilir. BLOB storage kullanarak. Uygulamanızı yerine tooa bağlı sanal disk toohello VM yazma hello uygulama tooAzure blob depolama alanına doğrudan yazabilirsiniz. BLOB storage ayrıca hello seçeneği sağlar [sık erişimli ve seyrek erişimli depolama katmanları](../../storage/storage-blob-storage-tiers.md) kullanılabilirlik gereksinimlerini ve maliyet kısıtlamaları bağlı olarak.

## <a name="striped-disks"></a>Şeritli diskleri
Toocreate diskleri 1023 GB'den büyük çoğu durumda sağlayarak yanı sıra, veri diskleri için şeritleme kullanarak performans tooback hello depolama tek bir birim için birden çok BLOB'ları vererek geliştirir. Şeritleme, hello g/ç toowrite gerekli ve tek bir mantıksal disk okuma verileri paralel olarak devam eder.

Azure hello veri diski sayısı ve hello VM boyutuna bağlı olarak kullanılabilir bant genişliği miktarını sınırlar uygular. Ayrıntılar için bkz [sanal makineler için Boyutlar](sizes.md)

Azure veri diski için disk şeritleme kullanıyorsanız, yönergeleri izleyerek hello göz önünde bulundurun:

* Merhaba VM boyutu için izin verilen hello maksimum veri diskleri bağlayın.
* LVM kullanın.
* Azure veri diski önbelleğe alma seçeneklerini kullanmaktan kaçının (ilke önbelleğe alma = yok).

Daha fazla bilgi için bkz: [yapılandırma LVM bir Linux VM üzerinde](configure-lvm.md).

## <a name="multiple-storage-accounts"></a>Birden çok depolama hesabı
Bu bölümde çok uygulanmaz[Azure yönetilen diskleri](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)gibi ayrı bir depolama hesapları oluşturmayın. 

Yönetilmeyen diskler için Azure Storage ortamınızı tasarlarken, birden çok depolama hesabı kullanabilirsiniz VM'ler hello sayıda dağıttığınız artar. Bu yaklaşım hello g/ç hello temel Azure depolama altyapısı toomaintain en iyi performans için sanal makineleri ve uygulamalarınızı üzerinden kullanıma dağıtmaya yardımcı olur. Dağıttığınız hello uygulamaları tasarlarken, her VM sahip hello g/ç gereksinimleri ve bu VM'lerin dengeyi Azure depolama hesapları arasında göz önünde bulundurun. Bir veya iki toojust depolama hesaplarında VM'ler yoğun tüm hello yüksek g/ç gruplandırma tooavoid deneyin.

Merhaba farklı Azure depolama seçenekleri hello g/ç özellikleri hakkında daha fazla bilgi ve bazı üst sınırlar önermek için bkz: [Azure storage ölçeklenebilirlik ve performans hedefleri](../../storage/storage-scalability-targets.md).

## <a name="next-steps"></a>Sonraki adımlar
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

