---
title: "Hyper-V çoğaltma tooa Azure Site Recovery ile ikincil site için aaaReview hello mimarisi | Microsoft Docs"
description: "Bu makalede, şirket içi Hyper-V sanal makineleri tooa ikincil System Center VMM site Azure Site Recovery ile çoğaltmak için hello mimarisine genel bakış sağlar."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 07099161-4cc7-4f32-8eb9-2a71bbf0750b
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 0de4b4e8601116c73e6fd710597ce4e561884368
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="step-1-review-hello-architecture-for-hyper-v-replication-tooa-secondary-site"></a>1. adım: Hyper-V çoğaltma tooa ikincil site gözden geçirme hello mimarisi

Bu makalede hello bileşenleri ve işlemler çoğaltırken söz konusu şirket içi System Center Virtual Machine Manager (VMM) bulutlarında, tooa hello kullanarak ikincil VMM sitesi Hyper-V sanal makineleri (VM'ler) [Azure Site Recovery](site-recovery-overview.md)hello Azure portal hizmeti.

Bu makalenin veya hello hello altındaki tüm yorumlar sonrası [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).



## <a name="architectural-components"></a>Mimari bileşenler

İşte Hyper-V sanal makineleri tooa ikincil VMM sitesi çoğaltmak için gerekir.

**Bileşen** | **Konum** | **Ayrıntılar**
--- | --- | ---
**Azure** | Azure aboneliği. | Kurtarma Hizmetleri kasası hello Azure aboneliği tooorchestrate oluşturup VMM konumları arasında çoğaltma yönetin.
**VMM sunucusu** | Birincil ve ikincil VMM konumu gerekir. | Bir VMM sunucusunun hello birincil sitede ve hello ikincil sitedeki öneririz 
**Hyper-V sunucusu** |  Bir veya daha fazla Hyper-V ana bilgisayar sunucuları hello birincil ve ikincil VMM bulutlarında. | Veri hello LAN veya Kerberos veya sertifika kimlik doğrulaması kullanarak VPN üzerinden hello birincil ve ikincil Hyper-V ana bilgisayar sunucuları arasında çoğaltılır.  
**Hyper-V VM’leri** | Hyper-V ana bilgisayar sunucusunda. | Merhaba kaynak ana bilgisayar sunucusunun tooreplicate istediğiniz en az bir VM'ye sahip olması gerekir.

## <a name="replication-process"></a>Çoğaltma işlemi

1. Azure hesabı hello ayarlayın, bir kurtarma Hizmetleri kasası oluşturun ve istediğinizi belirtin tooreplicate.
2. Hello Azure Site kurtarma sağlayıcısı VMM sunucuları ve her Hyper-V ana bilgisayarda hello Microsoft Azure kurtarma Hizmetleri aracısını yükleme içeren hello kaynak ve hedef çoğaltma ayarlarını yapılandırın.
3. Merhaba kaynak VMM bulutu için bir çoğaltma ilkesi oluşturun. Merhaba, uygulanan tooall hello bulut ana bilgisayarda yer alan VM'ler ilkesidir.
4. Her VMM için çoğaltmayı etkinleştirmek ve seçtiğiniz hello ayarlarına uygun olarak bir VM başlangıç çoğaltması gerçekleşir.
5. İlk çoğaltma sonrasında, delta değişikliklerin çoğaltılması başlar. Bir öğe için izlenen değişiklikler bir .hrl dosyasında saklanır.


![Şirket içi tooon içi](./media/vmm-to-vmm-walkthrough-architecture/arch-onprem-onprem.png)

## <a name="failover-and-failback-process"></a>Yük devretme ve yeniden çalışma işlemi

1. Şirket içi siteler arasında planlanmış veya planlanmamış bir [yük devretme](site-recovery-failover.md) gerçekleştirebilirsiniz. Planlanmış bir yük devretme çalıştırın, sonra kaynak VM'ler tooensure kapatın, veri kaybı.
2. Üzerinde tek bir makine başarısız veya oluşturma [kurtarma planlarına](site-recovery-create-recovery-plans.md) birden fazla makine tooorchestrate yük devretme.
4. Merhaba yük devretme makineler hello ikincil konumdaki sonra bir planlanmamış yük devretme tooa ikincil site gerçekleştirirseniz koruma veya çoğaltma için etkin değil. Planlanmış bir yük devretme hello yük devretme sonrasında çalıştırdıysanız hello ikincil konumdaki makineler korunur.
5. Ardından, VM hello çoğaltmasından hello yük devretme toostart erişilirken hello iş yükü uygulayın.
6. Birincil sitenizi yeniden kullanılabilir duruma geldiğinde, çoğaltmayı tersine çevirme tooreplicate hello ikincil site toohello birincil gelen başlatır. Çoğaltmayı tersine çevirme hello sanal makineleri korumalı bir duruma getirir, ancak hello ikincil veri merkezine hala hello etkin konumdur.
7. toomake hello birincil site hello etkin konuma yeniden planlı bir yük devretme ikincil tooprimary, başka bir tersine çoğaltma tarafından izlenen işlemini başlatır.



## <a name="next-steps"></a>Sonraki adımlar

Çok Git[2. adım: gözden hello Önkoşullar ve sınırlamalar](vmm-to-vmm-walkthrough-prerequisites.md).
