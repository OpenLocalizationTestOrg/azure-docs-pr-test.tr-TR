---
title: Site Recovery ile aaaMigrate tooAzure | Microsoft Docs
description: "Bu makalede geçirme VM'ler ve Azure Site Recovery ile fiziksel sunucuları tooAzure genel bakış sağlar"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: c413efcd-d750-4b22-b34b-15bcaa03934a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/05/2017
ms.author: raynew
ms.openlocfilehash: 6e65deee337c5371d441812ddb820dc8bc233684
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-tooazure-with-site-recovery"></a>Site Recovery ile tooAzure geçirme

Sanal makineleri ve fiziksel sunucuların geçişi için hello Azure Site Recovery hizmeti kullanarak genel bir bakış için bu makaleyi okuyun.

Site Recovery, yönetme tarafından şirket içi fiziksel sunucuların ve sanal makineleri toohello buluta (Azure'a) veya tooa ikincil veri merkezine çoğaltma tooyour BCDR stratejinize katkı sağlayan bir Azure hizmetidir. Kesinti birincil konumunuzda meydana toohello ikincil konum tookeep uygulamalar ve iş yüklerini kullanılabilir başarısız. Toonormal işlemleri geri döndüğünde geri tooyour birincil konumu başarısız. [Site Recovery nedir?](site-recovery-overview.md) bölümünden daha fazla bilgi edinebilirsiniz. Var olan iş yükleri tooAzure tooexpedite bulut gezisine ve kullanılabilir Azure'un sunduğu özellikler dizisi hello şirket içi Site Recovery toomigrate de kullanabilirsiniz.

Nasıl hızlı bir genel bakış için tooperform geçiş toothis video başvurun.
>[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/ASRHowTo-Video2-Migrate-Virtual-Machines-to-Azure/player]

Bu makalede hello dağıtımda [Azure portal](https://portal.azure.com). Merhaba [Klasik Azure portalı](https://manage.windowsazure.com/) olması kullanılan toomaintain varolan Site Recovery kasası, ancak yeni kasa oluşturamazsınız.

Bu makalenin hello altındaki tüm yorumlar gönderin. Merhaba hakkında teknik sorular sormak [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="what-do-we-mean-by-migration"></a>Geçiş ile kast edilen nedir?

Çoğaltma, şirket içi sanal makineleri ve fiziksel sunucuları, tooAzure veya tooa ikincil site için Site Recovery dağıtabilirsiniz. Makine, çoğaltma kesintileri gerçekleştiğinde ve onu kurtarır olduğunda bunları geri toohello birincil site başarısız olduğunda bunları hello birincil siteden yük devredin. Kullanıcıların bunları Azure Vm'leri olarak erişebilmesi için ek toothis içinde Site Recovery toomigrate VM'ler ve fiziksel sunucuları tooAzure kullanabilirsiniz. Geçiş, çoğaltma ve hello birincil site tooAzure yük devretmeyi ve Geçişi tamamlamak hareketi kapsar.

## <a name="what-can-site-recovery-migrate"></a>Site Recovery nelerin geçişini yapabilir?

Şunları yapabilirsiniz:

- Şirket içi Hyper-V sanal makineleri, VMware Vm'lerini ve fiziksel sunucuları, toorun Azure vm'lerinde çalışan iş yükünü geçirin. Ayrıca bu senaryoda tam çoğaltma ve bu yeniden çalışma gerçekleştirebilirsiniz.
- Bir Azure bölgesinden diğerine [Azure IaaS VM’lerini](site-recovery-migrate-azure-to-azure.md) geçirebilirsiniz. Şu anda bu senaryoda yalnızca geçiş desteklenmektedir ve yeniden çalışma desteği yoktur.
- Geçiş [AWS Windows örneklerini](site-recovery-migrate-aws-to-azure.md) tooAzure Iaas Vm'leri. Şu anda bu senaryoda yalnızca geçiş desteklenmektedir ve yeniden çalışma desteği yoktur.

## <a name="migrate-on-premises-vms-and-physical-servers"></a>Şirket içi VM’leri ve fiziksel sunucuları geçirme

toomigrate Hyper-V sanal makineleri, VMware Vm'lerini ve fiziksel sunucuları şirket içi, neredeyse hello olarak normal çoğaltma için kullanılanlarla aynı adımları izleyin.

1. Kurtarma Hizmetleri kasası ayarlama
2. Gerekli hello yönetim sunucularını yapılandırın (VMware, VMM, Hyper-istediğinize bağlı olarak V - toomigrate) toohello kasası ekleyin ve çoğaltma ayarlarını belirtin.
3. Merhaba makineleri için çoğaltmayı etkinleştirme toomigrate istiyor
4. Merhaba ilk geçişten sonra onu gerektiği gibi çalıştığını her şeyi hızlı sınama yük devretme tooensure çalıştırın.
5. Çoğaltma ortamınızın çalıştığını doğruladıktan sonra senaryonuz için [desteklenen özelliklere](site-recovery-failover.md) göre planlanmış veya planlanmamış yük devretme seçeneğini kullanırsınız. Mümkün oldukça planlı yük devretme kullanmanız önerilir.
6. Geçiş için bir yük devretme toocommit gerek yok veya silebilirsiniz. Bunun yerine, hello seçin **tam geçiş** seçeneği toomigrate istediğiniz her makine için.
     - İçinde **çoğaltılan öğeler**, hello VM sağ tıklayın ve **tam geçiş**. Tıklatın **Tamam** toocomplete. Merhaba tam geçiş işine izleyerek içinde hello VM özelliklerinde, ilerleme durumunu izleyebilirsiniz **Site Recovery işleri**.
     - Merhaba **tam geçiş** eylem hello geçiş işlemini tamamlar, hello makinesi için çoğaltma kaldırır ve hello makine için Site Recovery Faturalaması durdurulur.

![tamgeçiş](./media/site-recovery-hyper-v-site-to-azure/migrate.png)

## <a name="migrate-between-azure-regions"></a>Azure bölgeleri arasında geçiş yapma

Site Recovery kullanarak farklı bölgelerdeki Azure VM’leri arasında geçiş yapabilirsiniz. Bu senaryoda yalnızca geçiş desteklenir. Diğer bir deyişle, hello Azure Vm'lerini çoğaltma ve tooanother bölge başarısız ancak geri kapatamazsınız. Bu senaryoda, bir kurtarma Hizmetleri kasasını oluşturup bir şirket içi yapılandırma sunucusu toomanage çoğaltma dağıtmak, toohello kasası ekleyin ve çoğaltma ayarlarını belirtin. Toomigrate istediğiniz ve hızlı çalıştırmak hello makineleri yük devretme testi için çoğaltmayı etkinleştirin. Merhaba ile planlanmamış yük devretme çalıştırırsanız **tam geçiş** seçeneği.

## <a name="migrate-aws-tooazure"></a>AWS tooAzure geçirme

AWS örnekleri tooAzure VM'ler geçirebilirsiniz. Bu senaryoda yalnızca geçiş desteklenir. Diğer bir deyişle, hello AWS örnekleri çoğaltabilir ve tooAzure başarısız ancak geri kapatamazsınız. AWS örnekleri işlenmesini hello aynı fiziksel sunucuları geçiş amacıyla şekilde. Bir kurtarma Hizmetleri kasasını oluşturup, bir şirket içi yapılandırma sunucusu toomanage çoğaltma dağıtmak, toohello kasası ekleyin ve çoğaltma ayarlarını belirtin. Toomigrate istediğiniz ve hızlı çalıştırmak hello makineleri yük devretme testi için çoğaltmayı etkinleştirin. Merhaba ile planlanmamış yük devretme çalıştırırsanız **tam geçiş** seçeneği.




## <a name="next-steps"></a>Sonraki adımlar

- [VMware Vm'leri tooAzure geçirme](site-recovery-vmware-to-azure.md)
- [VMM Bulutları tooAzure Hyper-V sanal makineleri geçirme](site-recovery-vmm-to-azure.md)
- [VMM tooAzure Hyper-V sanal makineleri geçirme](site-recovery-hyper-v-site-to-azure.md)
- [Azure VM’lerini bir Azure bölgesinden diğerine geçirme](site-recovery-migrate-azure-to-azure.md)
- [AWS örnekleri tooAzure geçirme](site-recovery-migrate-aws-to-azure.md)
- [Geçirilen makinelerin tooenable çoğaltma hazırlama](site-recovery-azure-to-azure-after-migration.md) tooanother bölge olağanüstü durum kurtarma gerekir.
- [Azure sanal makinelerini çoğaltarak](site-recovery-azure-to-azure.md) iş yüklerinizi korumaya başlayın.
