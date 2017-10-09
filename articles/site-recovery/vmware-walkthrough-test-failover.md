---
title: "bir yük devretme sınaması için VMware çoğaltma tooAzure aaaRun | Microsoft Docs"
description: "VMware sanal makinelerini hello Azure Site Recovery hizmetini kullanarak tooAzure çoğaltmak için yük devretme testi çalıştırmak için gereken hello adımları özetler."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: a640e139-3a09-4ad8-8283-8fa92544f4c6
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: bed934446f0c6940089bfae24a13de4fb1556a62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="step-12-run-a-test-failover-tooazure-for-vmware-vms"></a>12. adım: bir test yük devretme tooAzure VMware Vm'leri için çalıştırın.

Nasıl hello kullanarak tooAzure toorun bir test yük devretme işlemini şirket içi VMware sanal makineleri bu makalede [Azure Site Recovery](site-recovery-overview.md) hello Azure portal hizmeti.

POST açıklamaları ve soruları hello altındaki bu makalenin veya hello [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="before-you-start"></a>Başlamadan önce

Merhaba VM özelliklerini doğrulayın ve herhangi bir değişiklik öneririz yük devretme testi çalıştırmadan önce gerekir. Merhaba VM Özellikleri'nde erişebilirsiniz **öğeleri çoğaltılan**. Merhaba **Essentials** dikey makineler ayarlarını ve durumu hakkında bilgileri gösterir.

## <a name="managed-disk-considerations"></a>Yönetilen disk değerlendirmeleri

[Yönetilen diskleri](../virtual-machines/windows/managed-disks-overview.md) hello VM disklerle ilişkilendirilmiş hello depolama hesaplarını yöneterek Azure VM'ler için disk yönetimi kolaylaştırabilir. 

- Bir sanal makine için korumayı etkinleştirdiğinizde, VM verisi tooa depolama hesabı çoğaltır. Yönetilen diskleri oluşturulur ve yalnızca yük devretme durumunda toohello VM bağlı.
- Yönetilen diskleri hello Resource Manager modelini kullanarak dağıtılan VM'ler için oluşturulabilir.  
- Bu ayar etkinse, yalnızca kullanılabilirlik sahip kaynak gruplarını ayarlar **yönetilen diskleri kullanımını** etkin seçilebilir. Yönetilen bir diske sahip sanal makineleri kullanılabilirlik kümeleri ile birlikte olmalıdır **yönetilen diskleri kullanımını** çok ayarlamak**Evet**. Merhaba ayarı VM'ler için etkin değil, yalnızca kaynak gruplarındaki kullanılabilirlik kümelerini yönetilen diski etkin olmayan seçilebilir.
- [Daha fazla bilgi edinin](https://docs.microsoft.com/azure/virtual-machines/windows/manage-availability#use-managed-disks-for-vms-in-an-availability-set) yönetilen diskleri ve kullanılabilirlik hakkında ayarlar.
- Çoğaltma için kullandığınız hello depolama hesabı depolama hizmeti şifrelemesi ile şifrelenmiş yönetilen diskleri yük devretme sırasında oluşturulamıyor. Bu durumda olmayan yönetilen diskleri kullanımını etkinleştirmek veya hello VM korumasını devre dışı bırakmak hem toouse şifreleme etkin olmayan bir depolama hesabı yeniden etkinleştirmek. [Daha fazla bilgi edinin](https://docs.microsoft.com/azure/storage/storage-managed-disks-overview#managed-disks-and-encryption).


## <a name="network-considerations"></a>Ağ konuları

Yük devretme sonrasında oluşturulan bir Azure VM için hello hedef IP adresini ayarlayabilirsiniz.

- Bir adresi sağlamazsanız, yükü devredilen makine üzerinde hello DHCP kullanır.
- Yük devretmede kullanılamayan bir adres ayarlarsanız yük devretme çalışmaz.
- Merhaba hello test yük devretme ağı testinde Hello adresi varsa, yük devretme sınaması için aynı hedef IP adresi kullanılabilir.
- ağ bağdaştırıcısı Hello sayısını hello hedef sanal makine için belirttiğiniz hello boyuta göre dikte edilir:

     - Merhaba hello kaynak makinedeki ağ bağdaştırıcısı sayısıdır hello ile aynı veya sayısından küçük, hello hello hedef makine boyutu için izin verilen bağdaştırıcıları sonra hello hedef olacaktır hello aynı sayıda bağdaştırıcıya hello kaynağı olarak.
     - Merhaba maksimum hedef boyutu kullanılır hello hello kaynak sanal makinenin bağdaştırıcı sayısı hello hedef boyutu için izin verilen hello sayıyı aşarsa.
     - Örneğin, kaynak makinenin iki bağdaştırıcısı varsa ve hello hedef makine boyutu dört adet bağdaştırıcıyı destekliyorsa hello hedef makinenin iki bağdaştırıcısı gerekir. Merhaba kaynak makinenin iki bağdaştırıcısı varsa, ancak hello hedef boyut yalnızca bir destekler hello hedef makine yalnızca bir bağdaştırıcısı olur.     
   - Merhaba sanal makinede birden fazla ağ bağdaştırıcısı varsa bunların tümü toohello bağlanır aynı ağ.
   - Merhaba sanal makine birden çok ağ bağdaştırıcısı hello varsa, önce bir hello listede gösterilen hello haline gelir *varsayılan* hello Azure sanal makine ağ bağdaştırıcısı.
 - [Daha fazla bilgi edinin](vmware-walkthrough-network.md) IP adresleme hakkında.



## <a name="view-and-modify-vm-settings"></a>Görüntüleme ve VM ayarlarını değiştirme

Bir yük devretme çalıştırmadan önce hello hello kaynak makinenin özelliklerini doğrulamanızı öneririz.

1. İçinde **korunan öğeler**, tıklatın **çoğaltılan öğeler**ve hello VM'ı tıklatın.
2. Merhaba, **yinelenmiş öğesi** bölmesinde, VM bilgileri, sistem durumu ve hello en son kullanılabilir kurtarma noktalarını özetini görebilirsiniz. Tıklatın **özellikleri** tooview daha ayrıntıları.
3. İçinde **işlem ve ağ**, şunları yapabilirsiniz:
    - Hello Azure VM adını değiştirin. Merhaba adı karşılamalıdır [Azure gereksinimleri](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
    - Bir yük devretme sonrasında [kaynak grubu] belirtin.
    - Hello Azure VM için bir hedef boyutu belirtin
    - Seçin bir [kullanılabilirlik kümesi](../virtual-machines/windows/tutorial-availability-sets.md).
    - Belirtin olup olmadığını toouse [yönetilen diskleri](#managed-disk-considerations). Seçin **Evet**tooattach yönetilen diskleri tooyour geçiş tooAzure makinede istiyorsanız.
    - Görüntülemek veya hello ağ/alt hangi hello Azure VM yük devretme sonrasında bulunur ve tooit atanacak hello IP adresi dahil olmak üzere ağ ayarlarını değiştirin.
4. İçinde **diskleri**hello işletim sistemiyle ilgili bilgileri görebilirsiniz ve veri disklerde hello VM.

## <a name="run-a-test-failover"></a>Yük devretme testi çalıştırma

Her şeyi kurduktan sonra bir test yük devretme toomake her şeyin beklendiği gibi çalıştığından emin çalıştırın.

- Tooconnect tooAzure VM'ler istiyorsanız, yük devretme işleminden sonra RDP kullanarak [tooconnect hazırlama](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover).
 - Active Directory ve DNS toocopy test ortamınızda gereksinim duyduğunuz toofully sınayın. [Daha fazla bilgi edinin](site-recovery-active-directory.md#test-failover-considerations).
 - Yük devretme testi hakkında tam bilgi için okuma [bu makalede](site-recovery-test-failover-to-azure.md) makalesi.
- Başlamadan önce hızlı bir video genel bakış alın:


     >[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video4-Recovery-Plan-DR-Drill-and-Failover/player]


Şimdi, bir yük devretme çalıştırın:

1. tek bir makineye üzerinden toofail içinde **ayarları** > **çoğaltılan öğeler**, hello VM tıklayın > **+ yük devretme testi** simgesi.

    ![Yük devretme sınaması](./media/vmware-walkthrough-test-failover/test-failover.png)

2. bir kurtarma üzerinden toofail planlama **ayarları** > **kurtarma planları**, sağ hello planı > **yük devretme testi**. bir kurtarma planı toocreate [bu yönergeleri izleyin](site-recovery-create-recovery-plans.md).  

3. İçinde **yük devretme testi**seçin hello Azure ağ toowhich Azure Vm'lerinin yük devretme gerçekleştikten sonra bağlanır.

4. Tıklatın **Tamam** toobegin hello yük devretme. Merhaba VM tooopen üzerinde özelliklerini tıklayarak ya da hello ilerleme durumunu izleyebilirsiniz **yük devretme testi** kasa adı işinde > **ayarları** > **işleri**  >  **Site Recovery işleri**.

5. Hello yük devretme işlemi tamamlandıktan sonra ayrıca olması toosee hello çoğaltma Azure makine görünür hello Azure portalı > **sanal makineleri**. Bu hello VM toohello uygun ağ ve çalıştığını bağlı hello uygun boyutta olduğundan emin olmanız gerekir.

6. Yük devretme sonrasında bağlantıları için hazır durumunda mümkün tooconnect toohello Azure VM olması gerekir.

7. Bitirdikten sonra tıklayın **temizleme yük devretme testi** hello kurtarma planı üzerinde. İçinde **notları**hello yük devretme testiyle ilişkili gözlemlerinizi kaydetmek ve kaydedin. Bu yük devretme testi sırasında oluşturulan hello VM'ler siler.



## <a name="next-steps"></a>Sonraki adımlar

- [Daha fazla bilgi edinin](site-recovery-failover.md) yerine, farklı türlerde hakkında ve nasıl toorun bunları.
- Makineleri çoğaltmak yerine ve geri, başarısız olan geçiş [daha fazla bilgi](site-recovery-migrate-to-azure.md#migrate-on-premises-vms-and-physical-servers).
- [Yeniden çalışma hakkında okuyun](site-recovery-failback-azure-to-vmware.md), toofail arka ve çoğaltma Azure Vm'leri yedekleme toohello içi birincil site.
