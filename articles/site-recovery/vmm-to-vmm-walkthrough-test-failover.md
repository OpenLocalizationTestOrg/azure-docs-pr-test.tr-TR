---
title: "bir yük devretme sınaması için Hyper-V VM çoğaltma tooa Azure Site Recovery ile ikincil site aaaRun | Microsoft Docs"
description: "Nasıl toorun bir yük devretme sınaması için Hyper-V VM çoğaltma tooa ikincil System Center VMM site Azure Site Recovery ile açıklar."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: a3fd11ce-65a1-4308-8435-45cf954353ef
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: a60411541c2db001c573735bcb0d651f6618f295
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-run-a-test-failover-for-hyper-v-replication-tooa-secondary-site"></a>10. adım: bir yük devretme sınaması için Hyper-V çoğaltma tooa ikincil site çalıştırma


Hyper-V sanal makineleri (VM'ler) için çoğaltma ile etkinleştirdikten sonra [Azure Site Recovery](site-recovery-overview.md), bu makale toorun yük devretme testi kullanın. Yük devretme testi çoğaltmanın üretim ortamınızı etkilemeden düzgün çalıştığını doğrular. 


Bu makaleyi okuduktan sonra tüm yorumlar hello altındaki ya da hello sonrası [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="before-you-start"></a>Başlamadan önce

- Yük devretme testi tetiklendiğinde hello ağ toowhich hello test çoğaltma sanal makineleri bağlanacak belirtebilirsiniz. [Daha fazla bilgi edinin](site-recovery-test-failover-vmm-to-vmm.md#network-options-in-site-recovery) hello ağ seçenekleri hakkında.
- Ağ eşleme sırasında seçtiğiniz bir ağ seçmeyin öneririz.
- Bu makaledeki yönergeleri Hello açıklamak nasıl toofail tek bir VM üzerinde. Hakkında bilgi edinin [kurtarma planları oluşturma](site-recovery-create-recovery-plans.md) toofail birden çok VM birlikte istiyorsanız.
- Hakkında bilgi edinin [yük devretme sınaması işlemlerini sınırlamalar](site-recovery-test-failover-vmm-to-vmm.md#things-to-note).
- Merhaba tooa VM yük devretme testi sırasında verilen IP adresi olduğundan hello VM hello aynı IP adresi almasını (Merhaba IP adresi hello test yük devretme ağda kullanılabilir olduğunu pek fazla) planlanmış veya planlanmamış bir yük devretme için. Başlangıç IP adresi hello test yük devretme ağında kullanılabilir değilse, hello VM hello test yük devretme ağı testinde kullanılabilirse başka bir IP adresi alır.
- Üretim ağınızda toodo yük devretme sınaması için uçtan uca ağ bağlantısı makinenin tam validatation istiyorsanız, dikkat edin:
    - Merhaba hello test yük devretme yapılırken birincil VM kapatılmalıdır. Aksi durumda, iki VM aynı kimlik hello çalıştıran hello ile aynı hello ağ aynı anda. 
    - Yük devretme hello temizleme test ettiğinizde tootest VM'ler değişiklik yaparsanız, bu değişiklikler kaybolur. Bu değişiklikler çoğaltılmış geri toohello olmayan birincil VM.
    - Testleri bir üretim ağı toodowntime üretim iş yükleri için yol açar. Kullanıcıların değil toouse ister hello olağanüstü durum kurtarma ayrıntıya devam ederken hello uygulama.  


## <a name="run-a-test-failover-for-a-vm"></a>Bir VM için yük devretme testi çalıştırma

1. tek bir VM üzerinde toofail içinde **çoğaltılan öğeler**, hello VM tıklayın > **yük devretme testi**.
2. İçinde **sınama yük devretmesi**, test sanal makineleri bağlı toonetworks hello test yük devretme sonrasında nasıl olacağını belirtin. 
3. Tıklatın **Tamam** toobegin hello yük devretme. Merhaba üzerinde ilerleme durumunu izlemek **işleri** sekmesi.
5. Yük devretme işlemi tamamlandıktan sonra o hello test sanal makineleri Başlat başarıyla doğrulayın.
6. İşiniz bittiğinde tıklatın **temizleme yük devretme testi** hello kurtarma planı üzerinde.
7. İçinde **notları**hello yük devretme testiyle ilişkili gözlemlerinizi kaydetmek ve kaydedin. Bu adım hello sanal makineler ve yük devretme testi sırasında oluşturulan ağlar siler.


## <a name="next-steps"></a>Sonraki adımlar

Merhaba dağıtımı test ettikten sonra diğer türleri hakkında daha fazla bilgi [yük devretme](site-recovery-failover.md).
