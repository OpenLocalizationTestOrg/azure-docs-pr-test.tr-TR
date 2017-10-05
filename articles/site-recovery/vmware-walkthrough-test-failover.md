---
title: "Azure'a yük devretme sınaması VMware çoğaltma için çalıştırma | Microsoft Docs"
description: "VMware Vm'leri Azure Site Recovery hizmetini kullanarak Azure'a çoğaltmak için yük devretme testi çalıştırmak için gereken adımları özetler."
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
ms.openlocfilehash: f1a6df56a2bb0094d972d2e659057cc124156b88
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="step-12-run-a-test-failover-to-azure-for-vmware-vms"></a>12. adım: yük devretme sınaması için Azure VMware Vm'leri için çalıştırma

Bu makalede yük devretme testi şirket içi VMware sanal makinelerini Azure'a nasıl çalıştırılacağını açıklar kullanarak [Azure Site Recovery](site-recovery-overview.md) Azure portalında hizmet.

POST açıklamaları ve soruları alt bu makalenin veya üzerinde [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="before-you-start"></a>Başlamadan önce

VM özelliklerini doğrulayın ve herhangi bir değişiklik öneririz yük devretme testi çalıştırmadan önce gerekir. VM Özellikleri'nde erişebilirsiniz **öğeleri çoğaltılan**. **Essentials** dikey makineler ayarlarını ve durumu hakkında bilgileri gösterir.

## <a name="managed-disk-considerations"></a>Yönetilen disk değerlendirmeleri

[Yönetilen diskleri](../virtual-machines/windows/managed-disks-overview.md) VM diskleri ile ilişkilendirilmiş depolama hesaplarını yöneterek Azure VM'ler için disk yönetimi kolaylaştırabilir. 

- Bir sanal makine için korumayı etkinleştirdiğinizde, bir depolama hesabı VM verilerini çoğaltır. Yönetilen diskleri oluşturulur ve yalnızca yük devretme durumunda VM'ye bağlı.
- Yönetilen diskler yalnızca Resource Manager modelini kullanarak dağıtılan VM'ler için oluşturulabilir.  
- Bu ayar etkinse, yalnızca kullanılabilirlik sahip kaynak gruplarını ayarlar **yönetilen diskleri kullanımını** etkin seçilebilir. Yönetilen bir diske sahip sanal makineleri kullanılabilirlik kümeleri ile birlikte olmalıdır **yönetilen diskleri kullanımını** kümesine **Evet**. Ayar VM'ler için etkin değil, yalnızca kaynak gruplarındaki kullanılabilirlik kümelerini yönetilen diski etkin olmayan seçilebilir.
- [Daha fazla bilgi edinin](https://docs.microsoft.com/azure/virtual-machines/windows/manage-availability#use-managed-disks-for-vms-in-an-availability-set) yönetilen diskleri ve kullanılabilirlik hakkında ayarlar.
- Çoğaltma için kullandığınız depolama hesabı depolama hizmeti şifrelemesi ile şifrelenmiş yönetilen diskleri yük devretme sırasında oluşturulamıyor. Bu durumda yok yönetilen diskleri kullanımını etkinleştirmek veya sanal makine için korumayı devre dışı bırakın hem şifreleme etkin olmayan bir depolama hesabı kullanacak şekilde yeniden etkinleştirin. [Daha fazla bilgi edinin](https://docs.microsoft.com/azure/storage/storage-managed-disks-overview#managed-disks-and-encryption).


## <a name="network-considerations"></a>Ağ konuları

Yük devretme sonrasında oluşturulan bir Azure VM için hedef IP adresini ayarlayabilirsiniz.

- Bir IP adresi sağlamazsanız yük devredilen makine DHCP kullanır.
- Yük devretmede kullanılamayan bir adres ayarlarsanız yük devretme çalışmaz.
- Test Yük Devretme ağ adresi varsa, aynı hedef IP adresi yük devretme sınaması için kullanılabilir.
- Ağ bağdaştırıcısı sayısı, hedef sanal makine için belirlediğiniz boyuta göre dikte edilir:

     - Hedef makine boyutu, daha sonra hedef izin bağdaştırıcı sayısı kaynak olarak aynı sayıda bağdaştırıcıya sahip olur daha kaynak makinedeki ağ bağdaştırıcısı sayısı aynı olarak ya da daha az ise.
     - Kaynak sanal makinenin bağdaştırıcı sayısı maksimum hedef boyutu kullanılır hedef boyutu için izin verilen sayıyı aşarsa.
     - Örneğin, kaynak makinenin iki bağdaştırıcısı varsa ve hedef makine boyutu dört adet bağdaştırıcıyı destekliyorsa hedef makinenin iki bağdaştırıcısı olur. Kaynak makinenin iki bağdaştırıcısı varken hedef boyut yalnızca bir bağdaştırıcıyı destekliyorsa hedef makinenin bir bağdaştırıcısı olur.     
   - Sanal makinede birden fazla ağ bağdaştırıcısı varsa bunların tümü aynı ağa bağlanır.
   - Sanal makine birden çok ağ bağdaştırıcısına sahip sonra listede gösterilen birinci hale *varsayılan* Azure sanal makine ağ bağdaştırıcısı.
 - [Daha fazla bilgi edinin](vmware-walkthrough-network.md) IP adresleme hakkında.



## <a name="view-and-modify-vm-settings"></a>Görüntüleme ve VM ayarlarını değiştirme

Bir yük devretme çalıştırmadan önce kaynak makinenin özelliklerini doğrulamanızı öneririz.

1. İçinde **korunan öğeler**, tıklatın **çoğaltılan öğeler**, VM'a tıklayın.
2. İçinde **yinelenmiş öğesi** bölmesinde, VM bilgileri, sistem durumu ve en son kullanılabilir kurtarma noktalarını özetini görebilirsiniz. Tıklatın **özellikleri** daha fazla ayrıntı görüntülemek için.
3. İçinde **işlem ve ağ**, şunları yapabilirsiniz:
    - Azure VM adını değiştirin. Adı karşılamalıdır [Azure gereksinimleri](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
    - Bir yük devretme sonrasında [kaynak grubu] belirtin.
    - Azure VM için bir hedef boyutu belirtin
    - Seçin bir [kullanılabilirlik kümesi](../virtual-machines/windows/tutorial-availability-sets.md).
    - Kullanıp kullanmayacağınızı belirtin [yönetilen diskleri](#managed-disk-considerations). Seçin **Evet**, Azure geçiş makinenizde yönetilen diskleri eklemek istiyorsanız.
    - Görüntülemek veya, Azure VM yük devretme ve kendisine atanmış IP adresi sonra yer alacağı ağını/alt ağını dahil olmak üzere ağ ayarlarını değiştirin.
4. İçinde **diskleri**, VM işletim sistemi ve veri diskleri hakkındaki bilgileri görebilirsiniz.

## <a name="run-a-test-failover"></a>Yük devretme testi çalıştırma

Her şeyi kurduktan sonra emin olmak için bir yük devretme testi her şeyin beklendiği gibi çalışmaktadır.

- Yük devretmeden sonra RDP kullanarak Azure vm'lerine bağlanmak isterseniz [bağlamaya hazırlanmak](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover).
 - Tam anlamıyla test etmek için Active Directory ve DNS'in bir kopyasını test ortamınızda bulundurmanız gerekir. [Daha fazla bilgi edinin](site-recovery-active-directory.md#test-failover-considerations).
 - Yük devretme testi hakkında tam bilgi için okuma [bu makalede](site-recovery-test-failover-to-azure.md) makalesi.
- Başlamadan önce hızlı bir video genel bakış alın:


     >[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video4-Recovery-Plan-DR-Drill-and-Failover/player]


Şimdi, bir yük devretme çalıştırın:

1. İçinde tek bir makineye vermesine **ayarları** > **çoğaltılan öğeler**, VM tıklayın > **+ yük devretme testi** simgesi.

    ![Yük devretme sınaması](./media/vmware-walkthrough-test-failover/test-failover.png)

2. Kurtarma planında yük devretme için **Ayarlar** > **Kurtarma Planları** seçeneklerinde plana sağ tıklayıp **Yük Devretme Testi**'ne tıklayın. Kurtarma planı oluşturmak için [aşağıdaki yönergeleri uygulayın](site-recovery-create-recovery-plans.md).  

3. İçinde **yük devretme testi**, Azure Vm'lerinin Azure ağa bağlı olacak yük devretme gerçekleştikten sonra seçin.

4. Yük devretmeyi başlatmak için **Tamam**'a tıklayın. Özelliklerini açmak için VM'ye veya üzerinde tıklayarak ilerleme durumunu izleyebilirsiniz **yük devretme testi** kasa adı işinde > **ayarları** > **işleri** > **Site Recovery işleri**.

5. Yük devretme tamamlandıktan sonra çoğaltılan makineyi Azure portalı > **Sanal Makineler** kısmında da görmeniz gerekir. VM'nin uygun boyutta olduğundan, uygun bir ağa bağlandığından ve çalıştığından emin olmanız gerekir.

6. Yük devretme sonrasındaki bağlantılar için hazırlık yaptıysanız Azure VM'ye bağlanabilmeniz gerekir.

7. Bitirdikten sonra tıklayın **temizleme yük devretme testi** kurtarma planı üzerinde. İçinde **notları**, kaydetme ve yük devretme testiyle ilişkili gözlemlerinizi kaydetmek. Bu yük devretme testi sırasında oluşturulan sanal makineleri siler.



## <a name="next-steps"></a>Sonraki adımlar

- [Daha fazla bilgi edinin](site-recovery-failover.md) farklı türdeki yük devretmeler ve bunları çalıştırma hakkında.
- Makineleri çoğaltmak yerine ve geri, başarısız olan geçiş [daha fazla bilgi](site-recovery-migrate-to-azure.md#migrate-on-premises-vms-and-physical-servers).
- [Yeniden çalışma hakkında okuyun](site-recovery-failback-azure-to-vmware.md), geri dönecek ve Azure Vm'lerini geri içi birincil siteye çoğaltma.
