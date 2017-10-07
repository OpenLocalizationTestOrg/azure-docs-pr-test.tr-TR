---
title: "Azure Site Recovery kullanarak çoğaltma tooAzure aaaPrerequisites | Microsoft Docs"
description: "Bu makalede hello Azure Site Recovery hizmetini kullanarak sanal makineleri ve fiziksel makineler tooAzure çoğaltma için önkoşullar özetlenmektedir."
services: site-recovery
documentationcenter: 
author: rajani-janaki-ram
manager: jwhit
editor: tysonn
ms.assetid: e24eea6c-50a7-4cd5-aab4-2c5c4d72ee2d
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/01/2017
ms.author: rajanaki
ms.openlocfilehash: c66cea8b097a872bae57e7b42e659e58c4b0b1f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
#  <a name="prerequisites-for-replicating-azure-virtual-machines-tooanother-region-by-using-azure-site-recovery"></a>Azure Site Recovery kullanarak Azure sanal makineleri tooanother bölge çoğaltma için Önkoşullar

> [!div class="op_single_selector"]
> * [Azure tooAzure çoğaltma](site-recovery-azure-to-azure-prereq.md)
> * [Şirket içi tooAzure çoğaltma](site-recovery-prereq.md)

Hello Azure Site Recovery hizmeti düzenleyerek tooyour iş devamlılığı ve olağanüstü durum kurtarma (BCDR) stratejinize katkıda bulunur:
* Azure sanal makineleri tooanother Azure bölgesi çoğaltma.
* Şirket içi fiziksel sunucuların ve sanal makinelerin tooAzure veya tooa ikincil veri merkezine çoğaltma. 

Kesinti birincil konumunuzda meydana tooa ikincil konum tookeep uygulamalar ve iş yüklerini kullanılabilir başarısız olabilir. Toonormal işlemleri geri döndüğünde geri tooyour birincil konumu başarısız olabilir. Site kurtarma hakkında daha fazla bilgi için bkz: [Site Recovery nedir?](site-recovery-overview.md).

Bu makalede hello önkoşullar gerekli toobegin şirket içi tooAzure Site Recovery Çoğaltmada özetlenmektedir.

Merhaba makalenin hello altındaki tüm yorumlar gönderin ya da hello hakkında teknik sorular sormak [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="azure-requirements"></a>Azure gereksinimleri

**Gereksinim** | **Ayrıntılar**
--- | ---
**Azure hesabı** | A [Microsoft Azure](http://azure.microsoft.com/) hesabı.<br/><br/> [Ücretsiz deneme sürümüyle](https://azure.microsoft.com/pricing/free-trial/) başlayabilirsiniz.
**Site Recovery hizmeti** | Site Recovery fiyatlandırması hakkında daha fazla bilgi için bkz: [Site Recovery fiyatlandırma](https://azure.microsoft.com/pricing/details/site-recovery/). Merhaba hedefinde toouse olağanüstü durum kurtarma konumu olarak istediğiniz Azure bölgesini kurtarma Hizmetleri kasası oluşturmanızı öneririz. Örneğin, kaynağınız VM'ler Doğu ABD çalıştıran ve BİZE tooreplicate tooCentral istiyorsanız Orta ABD hello kasası oluşturma öneririz.|
**Azure kapasite** | Merhaba hedef olağanüstü durum kurtarma konumu olarak toouse istediğiniz Azure bölgesini toohave sanal makineler, depolama hesapları ve ağ bileşenleri için yeterli kapasiteye sahip bir abonelik gerekiyor. Daha fazla kapasite destek tooadd başvurabilirsiniz.
**Depolama Kılavuzu** | Merhaba uyduğundan emin [depolama Kılavuzu](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks) performans sorunları tooavoid kaynağınız Azure sanal makineleri için. Merhaba varsayılan ayarları izlerseniz, Site Recovery gerekli hello depolama hesapları hello kaynak yapılandırmasını temel alarak oluşturur. Özelleştirme ve kendi ayarlarınızı seçerseniz, hello uyduğundan emin [sanal makine disklerini için ölçeklenebilirlik hedefleri](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks).
**Ağ Kılavuzu** | Belirli URL veya IP aralıkları için Azure sanal makineden toowhitelist hello giden bağlantı gerekir. Daha fazla ayrıntı için toohello başvurun [Azure sanal makineleri çoğaltmak için kılavuz ağ](site-recovery-azure-to-azure-networking-guidance.md) makalesi.
**Azure VM** | Tüm hello son kök sertifikaları hello Windows veya Linux VM üzerinde mevcut olduğundan emin olun. Merhaba son kök sertifikaları mevcut değilse hello VM toosecurity kısıtlamaları nedeniyle kayıtlı tooSite kurtarma olamaz.

>[!NOTE]
>Merhaba belirli yapılandırmalar için desteği hakkında daha fazla ayrıntı için okuma [destek matrisi](site-recovery-support-matrix-azure-to-azure.md).

## <a name="next-steps"></a>Sonraki adımlar
- Daha fazla bilgi edinmek [Azure sanal makineleri çoğaltmak için kılavuz ağ](site-recovery-azure-to-azure-networking-guidance.md).
- İş yükleri tarafından korumaya başlamak [Azure sanal makineleri çoğaltmak](site-recovery-azure-to-azure.md).
