---
title: "bir yük devretme sınaması için Azure Site Recovery ile Azure VM çoğaltma aaaRun | Microsoft Docs"
description: "Azure sanal makinelerini çoğaltma tooanother Azure bölgesini kullanma hello için Azure Site Recovery yük devretme testi çalıştırmak için hizmet hello adımları özetlemektedir."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: e15c1b0c-5d75-4fdf-acb0-e61def9e9339
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: raynew
ms.openlocfilehash: c1f765aa94c59dd70b33317ebbcd04beb7977969
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-run-a-test-failover-for-azure-vm-replication"></a>6. adım: bir yük devretme sınaması için Azure VM çoğaltma çalıştırma

Azure sanal makinesi (VM) için çoğaltma etkinleştirdikten sonra hello toorun test hello kullanarak bir Azure bölgesi tooanother yük devretmeyi bu makaledeki adımları [Azure Site Recovery](site-recovery-overview.md) hello Azure portal hizmeti.

- Hello makale bitirdikten sonra doğrulandı bir test yük devretmesi ile en az bir Azure VM tooyour ikincil Azure bölgesi başarısız olabilir. 
- Bu makalenin hello altındaki tüm yorumlar gönderin ya da hello sorular sormak [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)

>[!NOTE]
>
> Azure VM çoğaltma şu anda önizlemede değil.


## <a name="before-you-start"></a>Başlamadan önce

- Yük devretme testi çalıştırmadan önce hello VM özelliklerini doğrulayın ve istediğiniz değişiklikleri yapın öneririz. Merhaba VM Özellikleri'nde erişebilirsiniz **öğeleri çoğaltılan**. Merhaba **Essentials** dikey makineler ayarlarını ve durumu hakkında bilgileri gösterir.
- Merhaba test yük devretme ve değil hello ağ için ayrı bir Azure VM ağ kullanmanız önerilir (varsayılan veya özelleştirilmiş), ayarlanan üretim yük devretme için.
- Merhaba test yük devretme başarısız Azure Vm'leri (ve bunların depolama) üzerinden toohello ikincil Azure bölgesi. Herhangi bir bağımlı uygulamaları veya kaynakları kopyalamaz. VM'ler başarısız çalışan uygulamaları Active Directory veya DNS gibi başka kaynaklar bağımlı olması durumunda zaten ikincil Bölgenizde kullanılabilir değillerse, tooreplicate bunlar de gerekir. [Daha fazla bilgi](site-recovery-test-failover-to-azure.md#prepare-active-directory-and-dns)
- Bir şirket içi siteden yük devretme sonrasında tooaccess çoğaltılan VM'ler istiyorsanız, çok ihtiyacınız[tooconnect hazırlama](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover) toothese VM'ler.

## <a name="run-a-test-failover"></a>Yük devretme testi çalıştırma

1. İçinde **ayarları** > **çoğaltılan öğeler**, hello VM tıklatın **+ yük devretme testi** simgesi. 

2. İçinde **yük devretme testi**, bir kurtarma noktası toouse hello yük devretme için seçin:

    - **En son işlenen**: başarısız hello Site Recovery hizmeti tarafından işlenmiş toohello en son kurtarma noktası üzerinden VM hello. Merhaba zaman damgası gösterilir. Bu seçenek ile düşük RTO (Kurtarma süresi hedefi) sağlayan verileri işleme hiçbir zaman harcanmaktadır.
    - **Son uygulama tutarlı**: Bu seçenek tüm VM'ler toohello en son uygulama tutarlı bir kurtarma noktası başarısız olur. Merhaba zaman damgası gösterilir. 
    - **Özel**: herhangi bir kurtarma noktası seçin.
 
3. Merhaba yük devretme gerçekleştikten sonra select hello hedef Azure sanal ağı toowhich ikincil bölge'hello Azure Vm'lerde bağlanır.
4. toostart yük devretme Merhaba, tıklatın **Tamam**. tootrack ilerleme, hello VM tooopen, Özellikler'i tıklatın. Veya hello tıklatabilirsiniz **yük devretme testi** hello kasa adı işinde > **ayarları** > **işleri** > **Site Recovery işleri**.
5. Merhaba sonra Yük devretme, hello çoğaltma Azure VM hello Azure portalında görünür bittikten > **sanal makineleri**. Bu hello VM toohello uygun ağ ve çalıştığını bağlı hello uygun boyutta olduğundan emin olun.
6. toodelete hello hello test yük devretmesi sırasında oluşturulan VM'ler tıklatın **temizleme yük devretme sınaması** öğesi veya hello kurtarma planı üzerinde hello yinelenmiş. İçinde **notları**hello yük devretme testiyle ilişkili gözlemlerinizi kaydetmek ve kaydedin. 

[Daha fazla bilgi edinin](site-recovery-test-failover-to-azure.md) yük devretme sınaması işlemlerini hakkında.

## <a name="next-steps"></a>Sonraki adımlar

Yük devretme test ettikten sonra bu kılavuzda tamamlanır. Şimdi, yük devretme işlemlerini üretimde çalıştırma hakkında bilgi alın:

- [Daha fazla bilgi edinin](site-recovery-failover.md) yerine, farklı türlerde hakkında ve nasıl toorun bunları.
- Birden çok VM başarısız hakkında daha fazla bilgi [bir kurtarma planı kullanarak](site-recovery-create-recovery-plans.md).
- Daha fazla bilgi edinmek [kurtarma planlarına kullanarak](site-recovery-create-recovery-plans.md).
- Daha fazla bilgi edinmek [Azure sanal makineleri yeniden korumayı](site-recovery-how-to-reprotect.md) yük devretme sonrasında.

