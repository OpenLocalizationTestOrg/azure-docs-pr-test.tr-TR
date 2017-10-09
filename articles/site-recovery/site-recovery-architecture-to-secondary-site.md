---
title: "Şirket içi makine çoğaltma tooa ikincil şirket içi site iş Azure Site kurtarma aaaHow mu? | Microsoft Belgeleri"
description: "Bu makalede, bileşenleri ve çoğaltma sanal makineleri ve fiziksel sunucuları tooa ikincil site hello Azure Site Recovery hizmeti ile şirket içi kullanılan mimarisi genel bakış sağlar."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: c413efcd-d750-4b22-b34b-15bcaa03934a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/29/2017
ms.author: raynew
ms.openlocfilehash: 097a3f43446fec69ed7f9e0b7f11e8d11f41cc6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-on-premises-machine-replication-tooa-secondary-site-work-in-site-recovery"></a>Şirket içi çoğaltma tooa ikincil sitenin Site Recovery işlerinde nasıl makine?

Bu makalede hello bileşenleri açıklar ve işlemler çoğaltırken söz konusu şirket içi sanal makineleri ve fiziksel sunucuları tooAzure, hello kullanarak [Azure Site Recovery](site-recovery-overview.md) hizmet.

Tooa ikincil şirket içi siteye hello çoğaltabilirsiniz:
- Şirket içi Hyper-V VM'leri, Hyper-V kümelerindeki Hyper-V VM'leri ve System Center Virtual Machine Manager (VMM) bulutlarında yönetilen tek başına konaklar.
- Şirket içi VMware VM'leri ve Windows/Linux fiziksel sunucuları. Bu senaryoda çoğaltma işlemi Scout tarafından yönetilir.

Bu makalenin veya hello hello altındaki tüm yorumlar sonrası [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="replicate-hyper-v-vms-tooa-secondary-on-premises-site"></a>Hyper-V sanal makineleri tooa ikincil şirket içi siteye Çoğalt


### <a name="architectural-components"></a>Mimari bileşenler

İşte Hyper-V sanal makineleri tooa ikincil site çoğaltmak için gerekir.

**Bileşen** | **Konum** | **Ayrıntılar**
--- | --- | ---
**Azure** | Bir Microsoft hesabınızın olması gerekir. |
**VMM sunucusu** | Bir VMM sunucusunun hello birincil sitede ve hello ikincil sitedeki öneririz | Her bir VMM sunucusunun bağlı toohello olmalıdır Internet.<br/><br/> Her sunucu en az bir VMM özel bulut, Hyper-V hello yetenek profili kümesine sahip olması gerekir.<br/><br/> Hello Azure Site Recovery sağlayıcısı hello VMM sunucusuna yükleyin. Merhaba sağlayıcı düzenler ve çoğaltma hello Site Recovery hizmeti ile Merhaba yönetir Internet. Merhaba sağlayıcı ile Azure arasındaki iletişimler güvenli ve şifrelidir.
**Hyper-V sunucusu** |  Bir veya daha fazla Hyper-V ana bilgisayar sunucuları hello birincil ve ikincil VMM bulutlarında.<br/><br/> Sunucuları bağlı toohello olmalıdır Internet.<br/><br/> Veri hello LAN veya Kerberos veya sertifika kimlik doğrulaması kullanarak VPN üzerinden hello birincil ve ikincil Hyper-V ana bilgisayar sunucuları arasında çoğaltılır.  
**Hyper-V VM’leri** | Merhaba kaynak Hyper-V konak sunucusunda bulunan. | Merhaba kaynak ana bilgisayar sunucusunun tooreplicate istediğiniz en az bir VM'ye sahip olması gerekir.

### <a name="replication-process"></a>Çoğaltma işlemi

1. Azure hesabı hello ayarlayın.
2. Site Recovery kurtarma için bir Kurtarma Hizmetleri kasası ayarlarsınız ve aşağıdakileri de içeren kasa ayarlarını yapılandırırsınız:

    - Merhaba çoğaltma kaynağı ve hedefi (birincil ve ikincil siteler).
    - Hello Azure Site Recovery sağlayıcısı ve hello Microsoft Azure kurtarma Hizmetleri Aracısı yüklemesi. Merhaba sağlayıcı VMM sunucuları ve hello Aracısı her Hyper-V ana bilgisayarda yüklü.
    - Kaynak VMM bulutu için bir çoğaltma ilkesi oluşturursunuz. Merhaba, uygulanan tooall hello bulut ana bilgisayarda yer alan VM'ler ilkesidir.
    - Hyper-V VM’leri için çoğaltmayı etkinleştirirsiniz. İlk çoğaltma hello Çoğaltma İlkesi ayarlarına uygun şekilde gerçekleştirilir.
4. Veri değişiklikleri izlenir ve hello ilk çoğaltma sonlandırıldıktan sonra değişim çoğaltması toobegins değiştirir. Bir öğe için izlenen değişiklikler bir .hrl dosyasında saklanır.
5. Bir test yük devretme toomake emin çalıştırmadan her şeyi çalışmaktadır.

**Şekil 1: VMM tooVMM çoğaltma**

![Şirket içi tooon içi](./media/site-recovery-components/arch-onprem-onprem.png)

### <a name="failover-and-failback-process"></a>Yük devretme ve yeniden çalışma işlemi

1. Şirket içi siteler arasında planlanmış veya planlanmamış bir [yük devretme](site-recovery-failover.md) gerçekleştirebilirsiniz. Planlanmış bir yük devretme çalıştırın, sonra kaynak VM'ler tooensure kapatın, veri kaybı.
2. Üzerinde tek bir makine başarısız veya oluşturma [kurtarma planlarına](site-recovery-create-recovery-plans.md) birden fazla makine tooorchestrate yük devretme.
4. Merhaba yük devretme makineler hello ikincil konumdaki sonra bir planlanmamış yük devretme tooa ikincil site gerçekleştirirseniz koruma veya çoğaltma için etkin değil. Planlanmış bir yük devretme hello yük devretme sonrasında çalıştırdıysanız hello ikincil konumdaki makineler korunur.
5. Ardından, VM hello çoğaltmasından hello yük devretme toostart erişilirken hello iş yükü uygulayın.
6. Birincil sitenizi yeniden kullanılabilir duruma geldiğinde, çoğaltmayı tersine çevirme tooreplicate hello ikincil site toohello birincil gelen başlatır. Çoğaltmayı tersine çevirme hello sanal makineleri korumalı bir duruma getirir, ancak hello ikincil veri merkezine hala hello etkin konumdur.
7. toomake hello birincil site hello etkin konuma yeniden planlı bir yük devretme ikincil tooprimary, başka bir tersine çoğaltma tarafından izlenen işlemini başlatır.




## <a name="replicate-vmware-vmsphysical-servers-tooa-secondary-site"></a>VMware VM'ler/fiziksel sunucular tooa ikincil siteye çoğaltma

VMware Vm'lerini veya fiziksel sunucuları tooa ikincil site mimari bu bileşenleri kullanarak Inmage Scout kullanarak Çoğalt:


### <a name="architectural-components"></a>Mimari bileşenler

**Bileşen** | **Konum** | **Ayrıntılar**
--- | --- | ---
**Azure** | InMage Scout. | tooobtain Inmage Scout bir Azure aboneliği gerekir.<br/><br/> Bir kurtarma Hizmetleri kasası oluşturduktan sonra Inmage Scout indirin ve hello en son güncelleştirmeleri tooset hello dağıtım yükleyin.
**İşlem sunucusu** | Birincil sitede bulunur | Merhaba işlem sunucusu toohandle önbelleğe alma, sıkıştırma ve veri iyileştirme dağıtın.<br/><br/> Ayrıca, göndermeli yüklemesi hello tooprotect istediğiniz birleşik aracı toomachines yürütür.
**Yapılandırma sunucusu** | İkincil sitede bulunur | Hello yapılandırma sunucusu yönetir, yapılandırma ve dağıtımınız, ya da izleme hello Yönetim Web sitesini veya hello vContinuum konsolunu kullanarak.
**vContinuum sunucusu** | İsteğe bağlı. Hello aynı yüklü konumu hello yapılandırma sunucusu olarak. | Korunan ortamınızı yönetmeye ve izlemeye yönelik bir konsol sağlar.
**Ana hedef sunucu** | Merhaba ikincil sitede bulunan | Merhaba ana hedef sunucusu çoğaltılan verileri tutar. Merhaba işlem sunucusundan verileri alır, hello ikincil sitede çoğaltılan bir makine oluşturur ve hello veri bekletme noktalarını tutar.<br/><br/> Merhaba ihtiyacınız olan ana hedef sunucusu sayısı koruduğunuz makine hello sayısına bağlıdır.<br/><br/> Toofail geri toohello birincil site istiyorsanız, bir ana hedef sunucusu var. çok gerekir. Merhaba birleşik aracı bu sunucuda yüklü.
**VMware ESX/ESXi ve vCenter sunucusu** |  VM’ler ESX/ESXi ana bilgisayarlarında barındırılır. Ana bilgisayarlar bir vCenter sunucusu ile yönetilir | Bir VMware altyapı tooreplicate VMware Vm'lerini gerekir.
**VM’ler/fiziksel sunucular** |  VMware Vm'lerini ve fiziksel sunucularda tooreplicate istediğiniz yüklenen birleşik aracı. | Merhaba aracı hello bileşenlerinin tümünü arasındaki bir iletişim sağlayıcısı gibi davranır.


### <a name="replication-process"></a>Çoğaltma işlemi

1. Merhaba bileşen sunucularını (yapılandırma, işlem, ana hedef) her sitede ayarlayın ve tooreplicate istediğiniz makinelere hello birleşik aracı yükleyin.
2. İlk çoğaltma sonrasında hello aracı her makinede delta çoğaltma değişiklikleri toohello işlem sunucusuna gönderir.
3. Merhaba işlem sunucusu hello verileri iyileştirir ve hello ikincil sitede toohello ana hedef sunucusuna aktarır. Merhaba yapılandırma sunucusu hello çoğaltma sürecini yönetir.

**Şekil 2: VMware tooVMware çoğaltma**

![VMware tooVMware](./media/site-recovery-components/vmware-to-vmware.png)


## <a name="next-steps"></a>Sonraki adımlar

Gözden geçirme hello [destek matrisi](site-recovery-support-matrix-to-sec-site.md)
