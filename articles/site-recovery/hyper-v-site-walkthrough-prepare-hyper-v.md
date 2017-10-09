---
title: "aaaPrepare Hyper-V çoğaltma tooAzure (System Center VMM) barındıran | Microsoft Docs"
description: "Tooprepare Hyper-V çoğaltma tooAzure için Azure Site RECOVERY'yi kullanarak nasıl barındıran açıklar"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 0f204e24-8d78-4076-95c5-8137d1be9c01
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: 714b229d5efbd66a9844bd09e36ac3f69919a6bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-prepare-hyper-v-hosts-for-replication-tooazure"></a>6. adım: Hyper-V konakları için çoğaltma tooAzure hazırlayın.

Bu makale tooprepare şirket içi Hyper-V konakları toointeract Azure Site Recovery ile Merhaba yönergeleri kullanın.

Bu makaleyi okuduktan sonra hello altındaki tüm yorumlar post veya üzerinde hello teknik sorular sormak [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="prepare-hosts"></a>Ana bilgisayarını hazırlayın

- Merhaba Hyper-V konakları hello karşıladığından emin olun [Önkoşullar](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm).
- Merhaba konakları gerekli hello URL'leri erişebildiğinden emin olun:

    [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]
    
- IP adresi tabanlı güvenlik duvarı kuralları varsa, iletişim tooAzure izin emin olun.
- Merhaba izin [Azure veri merkezi IP aralıkları](https://www.microsoft.com/download/confirmation.aspx?id=41653)ve hello HTTPS (443 numaralı) bağlantı noktası.
- IP adres aralıklarını hello aboneliğinizin Azure bölgesi ve Batı ABD (erişim denetimi ve kimlik yönetimi için kullanılan) izin verir.

Site Recovery dağıtımı sırasında tooreplicate tooa Hyper-V sitesinin istediğiniz Vm'leri içeren Hyper-V konakları ekleyin. Her ana bilgisayarda Hello Site Recovery sağlayıcısı ve kurtarma Hizmetleri Aracısı yüklenir. Merhaba Hyper-V site kurtarma Hizmetleri kasası hello kaydedilir.

## <a name="next-steps"></a>Sonraki adımlar

Çok Git[adım 7: bir kasa oluşturun](hyper-v-site-walkthrough-create-vault.md)

