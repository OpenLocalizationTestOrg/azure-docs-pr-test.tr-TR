---
title: "Hyper-V çoğaltma tooAzure için System Center VMM aaaPrepare | Microsoft Docs"
description: "Açıklar nasıl tooprepare System Center VMM sunucusuna Azure Site Recovery kullanarak Hyper-V çoğaltma tooAzure için"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: afcd81ae-d192-4013-a0af-3dac45b3c7e9
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 773b06afaf7d3eea1fe64f050bf3970943cf466a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-prepare-vmm-servers-and-hyper-v-hosts-for-hyper-v-replication-tooazure"></a>6. adım: VMM sunucuları ve Hyper-V konakları için Hyper-V çoğaltma tooAzure hazırlama

Ayarladıktan sonra [Azure bileşenleri](vmm-to-azure-walkthrough-prepare-azure.md) hello dağıtımı için Azure Site Recovery ile bu makale tooprepare şirket içi VMM sunucuları ve Hyper-V konakları toointeract hello yönergeleri kullanın.

Bu makaleyi okuduktan sonra hello altındaki tüm yorumlar post veya üzerinde hello teknik sorular sormak [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="prepare-vmm-servers"></a>VMM sunucuları hazırlama

- Site Recovery çoğaltma (site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers) hello destek gereksinimlerini karşılayan en az bir VMM sunucusu gerekir.
- Emin olun hello VMM sunucusu için hazır [ağ eşlemesi](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure).
- Merhaba VMM sunucusunun bu URL'leri erişebildiğinden emin olun

    [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]
    
- IP adresi tabanlı güvenlik duvarı kuralları varsa, iletişim tooAzure izin emin olun.
- Merhaba izin [Azure veri merkezi IP aralıkları](https://www.microsoft.com/download/confirmation.aspx?id=41653)ve hello HTTPS (443 numaralı) bağlantı noktası.
- IP adres aralıklarını hello aboneliğinizin Azure bölgesi ve Batı ABD (erişim denetimi ve kimlik yönetimi için kullanılan) izin verir.

Site Recovery dağıtımı sırasında hello Site kurtarma sağlayıcısı indirin ve her VMM sunucusuna yükleyin. Kurtarma Hizmetleri kasası hello Hello VMM sunucusu kayıtlı.




## <a name="next-steps"></a>Sonraki adımlar

Çok Git[adım 7: bir kasa oluşturun](vmm-to-azure-walkthrough-create-vault.md)

