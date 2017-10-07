---
title: "bir yük devretme sınaması için Hyper-V (System Center VMM olmadan) çoğaltma tooAzure aaaRun | Microsoft Docs"
description: "Hyper-V sanal makineleri hello Azure Site Recovery hizmetini kullanarak tooAzure çoğaltmak için yük devretme testi çalıştırmak için gereken hello adımları özetler."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: c9a4c3ca-84a0-4668-b700-9b0046202299
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: dbcca080a8fa139e2ea0d132323101dd0f7cd265
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="step-11-run-a-test-failover-for-hyper-v-replication-tooazure"></a>11. adım: bir yük devretme sınaması için Hyper-V çoğaltma tooAzure çalıştırma

Bu makalede nasıl toorun bir test yük devretmeyi (System Center VMM tarafından yönetilmediğinden) Hyper-V sanal makineleri şirket içi hello kullanarak tooAzure [Azure Site Recovery](site-recovery-overview.md) hello Azure portal hizmeti.

POST açıklamaları ve soruları hello altındaki bu makalenin veya hello [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="before-you-start"></a>Başlamadan önce

Merhaba VM özelliklerini doğrulayın ve herhangi bir değişiklik öneririz yük devretme testi çalıştırmadan önce gerekir. Merhaba VM Özellikleri'nde erişebilirsiniz **öğeleri çoğaltılan**. Merhaba **Essentials** dikey makineler ayarlarını ve durumu hakkında bilgileri gösterir.

## <a name="managed-disk-considerations"></a>Yönetilen disk değerlendirmeleri

[Yönetilen diskleri](../virtual-machines/windows/managed-disks-overview.md) hello VM disklerle ilişkilendirilmiş hello depolama hesaplarını yöneterek Azure VM'ler için disk yönetimi kolaylaştırabilir. 

- Yönetilen diskleri oluşturulur ve yalnızca bir yük devretme tooAzure meydana geldiğinde toohello VM bağlı. Korumayı etkinleştirdiğinizde toostorage hesapları şirket içi Vm'lerden gelen verilerini çoğaltır.
- Yönetilen diskleri hello Resource manager dağıtım modeli kullanılarak dağıtılan VM'ler için oluşturulabilir.
- Yeniden çalışma alanından Azure tooan Hyper-V ortamına yönetilen disklerle makineler için şu anda desteklenmiyor şirket içi. Yalnızca ayarlamalısınız **yönetilen diskleri kullanımını** çok**Evet** bir geçiş yalnızca (yük devretme tooAzure geri dönme olmadan) yaptığınız varsa
- Bu ayar etkinse, yalnızca kullanılabilirlik sahip kaynak gruplarını ayarlar **yönetilen diskleri kullanımını** etkin seçilebilir. Yönetilen bir diske sahip sanal makineleri kullanılabilirlik kümeleri ile birlikte olmalıdır **yönetilen diskleri kullanımını** çok ayarlamak**Evet**. Merhaba ayarı VM'ler için etkin değil, yalnızca kaynak gruplarındaki kullanılabilirlik kümelerini yönetilen diski etkin olmayan seçilebilir. [Daha fazla bilgi edinin](https://docs.microsoft.com/azure/virtual-machines/windows/manage-availability#use-managed-disks-for-vms-in-an-availability-set).
- - Çoğaltma için kullandığınız hello depolama hesabı depolama hizmeti şifrelemesi ile şifrelenmiş yönetilen diskleri yük devretme sırasında oluşturulamıyor. Bu durumda olmayan yönetilen diskleri kullanımını etkinleştirmek veya hello VM korumasını devre dışı bırakmak hem toouse şifreleme etkin olmayan bir depolama hesabı yeniden etkinleştirmek. [Daha fazla bilgi edinin](https://docs.microsoft.com/azure/storage/storage-managed-disks-overview#managed-disks-and-encryption).

 
## <a name="network-considerations"></a>Ağ konuları
    
- Yük devretme sonrasında Azure VM'de hello için kullanılan hello hedef IP adresi toobe ayarlayabilirsiniz. Bir adresi sağlamazsanız, yükü devredilen makine üzerinde hello DHCP kullanır. Yük devretmede kullanılamayan bir adres ayarlarsanız hello yük devretme başarısız olur. Merhaba hello test yük devretme ağı testinde Hello adresi varsa, yük devretme sınaması için aynı hedef IP adresi kullanılabilir.
- ağ bağdaştırıcısı Hello sayısını hello hedef sanal makine için aşağıdaki gibi belirtin hello boyuta göre dikte edilir:
    - Merhaba hello kaynak makinedeki ağ bağdaştırıcısı sayısı küçük veya buna eşit ise toohello bağdaştırıcı sayısı hello hedef makine boyutu için izin verilen sonra hello hedef olacaktır hello aynı sayıda bağdaştırıcıya hello kaynağı olarak.
    - Merhaba hello kaynak sanal makinenin bağdaştırıcı sayısı hello hedef boyutu sonra hello maksimum hedef boyutu kullanılır için izin verilen hello sayıyı aşarsa.
    - Örneğin, kaynak makinenin iki bağdaştırıcısı varsa ve hello hedef makine boyutu dört adet bağdaştırıcıyı destekliyorsa, hello hedef makinenin iki bağdaştırıcısı gerekir. Merhaba kaynak makinenin iki bağdaştırıcısı varsa, ancak hello hedef boyut yalnızca bir destekler hello hedef makine yalnızca bir bağdaştırıcısı olur.     
- Merhaba VM birden çok ağ bağdaştırıcısı varsa bunların tümü toohello bağlanır aynı ağ.
- Merhaba sanal makine birden çok ağ bağdaştırıcısı hello varsa, önce bir hello listede gösterilen hello haline gelir *varsayılan* hello Azure sanal makine ağ bağdaştırıcısı.


## <a name="view-and-manage-vm-settings"></a>VM ayarlarını görüntülemek ve yönetmek

Bir yük devretme çalıştırmadan önce hello hello kaynak makinenin özelliklerini doğrulamanızı öneririz.

1. İçinde **korunan öğeler**, tıklatın **çoğaltılan öğeler**ve hello VM'ı tıklatın.

    ![Çoğaltmayı etkinleştirme](./media/hyper-v-site-walkthrough-test-failover/test-failover1.png)
2. Merhaba, **yinelenmiş öğesi** bölmesinde, VM bilgileri, sistem durumu ve hello en son kullanılabilir kurtarma noktalarını özetini görebilirsiniz. Tıklatın **özellikleri** tooview daha ayrıntıları.

    ![Çoğaltmayı etkinleştirme](./media/hyper-v-site-walkthrough-test-failover/test-failover2.png)
3. İçinde **işlem ve ağ**, şunları yapabilirsiniz:
    - Hello Azure VM adını değiştirin. Merhaba adı karşılamalıdır [Azure gereksinimleri](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
    - Bir yük devretme sonrasında [kaynak grubu] belirtin.
    - Hello Azure VM için bir hedef boyutu belirtin
    - Seçin bir [kullanılabilirlik kümesi](../virtual-machines/windows/tutorial-availability-sets.md).
    - Belirtin olup olmadığını toouse [yönetilen diskleri](#managed-disk-considerations). Seçin **Evet**tooattach yönetilen diskleri tooyour geçiş tooAzure makinede istiyorsanız.
    - Görüntülemek veya hello ağ/alt hangi hello Azure VM yük devretme sonrasında bulunur ve tooit atanacak hello IP adresi dahil olmak üzere ağ ayarlarını değiştirin.

    ![Çoğaltmayı etkinleştirme](./media/hyper-v-site-walkthrough-test-failover/test-failover4.png)
4. İçinde **diskleri**hello işletim sistemiyle ilgili bilgileri görebilirsiniz ve veri disklerde hello VM.


## <a name="run-a-test-failover"></a>Yük devretme testi çalıştırma

Şimdi, test yük devretme toomake her şeyin beklendiği gibi çalıştığından emin çalıştırın.

- Tooconnect tooAzure VM'ler istiyorsanız, yük devretme işleminden sonra RDP kullanarak [tooconnect hazırlama](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover).
 - Active Directory ve DNS toocopy test ortamınızda gereksinim duyduğunuz toofully sınayın. [Daha fazla bilgi edinin](site-recovery-active-directory.md#test-failover-considerations).
 - Yük devretme testi hakkında tam bilgi için okuma [bu makalede](site-recovery-test-failover-to-azure.md) makalesi.
 
 Artık bir yük devretme çalıştırın:

1. tek bir makineye üzerinden toofail içinde **çoğaltılan öğeler**, hello VM tıklayın > **+ yük devretme testi** simgesi.
2. bir kurtarma üzerinden toofail planlama **kurtarma planları**, sağ hello planı > **yük devretme testi**. bir kurtarma planı toocreate [bu yönergeleri izleyin](site-recovery-create-recovery-plans.md).
3. İçinde **yük devretme testi**seçin hello Azure ağ toowhich Azure Vm'lerinin yük devretme gerçekleştikten sonra bağlanır.
4. Tıklatın **Tamam** toobegin hello yük devretme. Merhaba VM tooopen üzerinde özelliklerini tıklayarak ya da hello ilerleme durumunu izleyebilirsiniz **yük devretme testi** kasa adı işinde > **işleri** > **Site Recovery işleri**.
5. Hello yük devretme işlemi tamamlandıktan sonra ayrıca olması toosee hello çoğaltma Azure makine görünür hello Azure portalı > **sanal makineleri**. Bu hello VM toohello uygun ağ ve çalıştığını bağlı hello uygun boyutta olduğundan emin olmanız gerekir.
6. Yük devretme sonrasında bağlantıları için hazır durumunda mümkün tooconnect toohello Azure VM olması gerekir.
7. Bitirdikten sonra tıklayın **temizleme yük devretme testi** hello kurtarma planı üzerinde. İçinde **notları** kaydedin ve hello yük devretme testiyle ilişkili gözlemlerinizi kaydetmek. Bu yük devretme testi sırasında oluşturulan hello sanal makineleri siler.



## <a name="next-steps"></a>Sonraki adımlar

- [Daha fazla bilgi edinin](site-recovery-failover.md) yerine, farklı türlerde hakkında ve nasıl toorun bunları.
- [Yeniden çalışma hakkında okuyun](site-recovery-failback-from-azure-to-hyper-v.md), toofail arka ve çoğaltma Azure Vm'leri yedekleme toohello birincil şirket içi Hyper-V sitesi.

