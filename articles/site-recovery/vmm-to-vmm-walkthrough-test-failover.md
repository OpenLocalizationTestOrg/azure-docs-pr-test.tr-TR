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
# <a name="step-10-run-a-test-failover-for-hyper-v-replication-tooa-secondary-site"></a><span data-ttu-id="37276-103">10. adım: bir yük devretme sınaması için Hyper-V çoğaltma tooa ikincil site çalıştırma</span><span class="sxs-lookup"><span data-stu-id="37276-103">Step 10: Run a test failover for Hyper-V replication tooa secondary site</span></span>


<span data-ttu-id="37276-104">Hyper-V sanal makineleri (VM'ler) için çoğaltma ile etkinleştirdikten sonra [Azure Site Recovery](site-recovery-overview.md), bu makale toorun yük devretme testi kullanın.</span><span class="sxs-lookup"><span data-stu-id="37276-104">After you enable replication for Hyper-V virtual machines (VMs) with [Azure Site Recovery](site-recovery-overview.md), use this article toorun a test failover.</span></span> <span data-ttu-id="37276-105">Yük devretme testi çoğaltmanın üretim ortamınızı etkilemeden düzgün çalıştığını doğrular.</span><span class="sxs-lookup"><span data-stu-id="37276-105">A test failover verifies that replication is working, without impacting your production environment.</span></span> 


<span data-ttu-id="37276-106">Bu makaleyi okuduktan sonra tüm yorumlar hello altındaki ya da hello sonrası [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="37276-106">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="before-you-start"></a><span data-ttu-id="37276-107">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="37276-107">Before you start</span></span>

- <span data-ttu-id="37276-108">Yük devretme testi tetiklendiğinde hello ağ toowhich hello test çoğaltma sanal makineleri bağlanacak belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="37276-108">When you're triggering a test failover, you can specify hello network toowhich hello test replica VMs will connect.</span></span> <span data-ttu-id="37276-109">[Daha fazla bilgi edinin](site-recovery-test-failover-vmm-to-vmm.md#network-options-in-site-recovery) hello ağ seçenekleri hakkında.</span><span class="sxs-lookup"><span data-stu-id="37276-109">[Learn more](site-recovery-test-failover-vmm-to-vmm.md#network-options-in-site-recovery) about hello network options.</span></span>
- <span data-ttu-id="37276-110">Ağ eşleme sırasında seçtiğiniz bir ağ seçmeyin öneririz.</span><span class="sxs-lookup"><span data-stu-id="37276-110">We recommend that you don't choose a network that you selected during network mapping.</span></span>
- <span data-ttu-id="37276-111">Bu makaledeki yönergeleri Hello açıklamak nasıl toofail tek bir VM üzerinde.</span><span class="sxs-lookup"><span data-stu-id="37276-111">hello instructions in this article describe how toofail over a single VM.</span></span> <span data-ttu-id="37276-112">Hakkında bilgi edinin [kurtarma planları oluşturma](site-recovery-create-recovery-plans.md) toofail birden çok VM birlikte istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="37276-112">Read about [creating recovery plans](site-recovery-create-recovery-plans.md) if you want toofail over multiple VMs together.</span></span>
- <span data-ttu-id="37276-113">Hakkında bilgi edinin [yük devretme sınaması işlemlerini sınırlamalar](site-recovery-test-failover-vmm-to-vmm.md#things-to-note).</span><span class="sxs-lookup"><span data-stu-id="37276-113">Read about [limitations for test failovers](site-recovery-test-failover-vmm-to-vmm.md#things-to-note).</span></span>
- <span data-ttu-id="37276-114">Merhaba tooa VM yük devretme testi sırasında verilen IP adresi olduğundan hello VM hello aynı IP adresi almasını (Merhaba IP adresi hello test yük devretme ağda kullanılabilir olduğunu pek fazla) planlanmış veya planlanmamış bir yük devretme için.</span><span class="sxs-lookup"><span data-stu-id="37276-114">hello IP address given tooa VM during test failover is hello same IP address that hello VM would receive for a planned or unplanned failover (presuming that hello IP address is available in hello test failover network).</span></span> <span data-ttu-id="37276-115">Başlangıç IP adresi hello test yük devretme ağında kullanılabilir değilse, hello VM hello test yük devretme ağı testinde kullanılabilirse başka bir IP adresi alır.</span><span class="sxs-lookup"><span data-stu-id="37276-115">If hello IP address isn't available in hello test failover network, hello VM receives another IP address that is available in hello test failover network.</span></span>
- <span data-ttu-id="37276-116">Üretim ağınızda toodo yük devretme sınaması için uçtan uca ağ bağlantısı makinenin tam validatation istiyorsanız, dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="37276-116">If you do want toodo a test failover in your production network, for full validatation of end-to-end network connectivity machine, note that:</span></span>
    - <span data-ttu-id="37276-117">Merhaba hello test yük devretme yapılırken birincil VM kapatılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="37276-117">hello primary VM should be shut down when you're doing hello test failover.</span></span> <span data-ttu-id="37276-118">Aksi durumda, iki VM aynı kimlik hello çalıştıran hello ile aynı hello ağ aynı anda.</span><span class="sxs-lookup"><span data-stu-id="37276-118">Otherwise, two VMs with hello same identity will be running in hello same network at hello same time.</span></span> 
    - <span data-ttu-id="37276-119">Yük devretme hello temizleme test ettiğinizde tootest VM'ler değişiklik yaparsanız, bu değişiklikler kaybolur.</span><span class="sxs-lookup"><span data-stu-id="37276-119">If you make changes tootest VMs, those changes are lost when you clean up hello test failover.</span></span> <span data-ttu-id="37276-120">Bu değişiklikler çoğaltılmış geri toohello olmayan birincil VM.</span><span class="sxs-lookup"><span data-stu-id="37276-120">These changes aren't replicated back toohello primary VM.</span></span>
    - <span data-ttu-id="37276-121">Testleri bir üretim ağı toodowntime üretim iş yükleri için yol açar.</span><span class="sxs-lookup"><span data-stu-id="37276-121">Testing a a production network leads toodowntime for your production workloads.</span></span> <span data-ttu-id="37276-122">Kullanıcıların değil toouse ister hello olağanüstü durum kurtarma ayrıntıya devam ederken hello uygulama.</span><span class="sxs-lookup"><span data-stu-id="37276-122">Ask users not toouse hello app when hello disaster recovery drill is in progress.</span></span>  


## <a name="run-a-test-failover-for-a-vm"></a><span data-ttu-id="37276-123">Bir VM için yük devretme testi çalıştırma</span><span class="sxs-lookup"><span data-stu-id="37276-123">Run a test failover for a VM</span></span>

1. <span data-ttu-id="37276-124">tek bir VM üzerinde toofail içinde **çoğaltılan öğeler**, hello VM tıklayın > **yük devretme testi**.</span><span class="sxs-lookup"><span data-stu-id="37276-124">toofail over a single VM, in **Replicated Items**, click hello VM > **Test Failover**.</span></span>
2. <span data-ttu-id="37276-125">İçinde **sınama yük devretmesi**, test sanal makineleri bağlı toonetworks hello test yük devretme sonrasında nasıl olacağını belirtin.</span><span class="sxs-lookup"><span data-stu-id="37276-125">In **Test Failover**, specify how test VMs will be connected toonetworks after hello test failover.</span></span> 
3. <span data-ttu-id="37276-126">Tıklatın **Tamam** toobegin hello yük devretme.</span><span class="sxs-lookup"><span data-stu-id="37276-126">Click **OK** toobegin hello failover.</span></span> <span data-ttu-id="37276-127">Merhaba üzerinde ilerleme durumunu izlemek **işleri** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="37276-127">Track progress on hello **Jobs** tab.</span></span>
5. <span data-ttu-id="37276-128">Yük devretme işlemi tamamlandıktan sonra o hello test sanal makineleri Başlat başarıyla doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="37276-128">After failover is complete, verify that hello test VMs start successfully.</span></span>
6. <span data-ttu-id="37276-129">İşiniz bittiğinde tıklatın **temizleme yük devretme testi** hello kurtarma planı üzerinde.</span><span class="sxs-lookup"><span data-stu-id="37276-129">When you're done, click **Cleanup test failover** on hello recovery plan.</span></span>
7. <span data-ttu-id="37276-130">İçinde **notları**hello yük devretme testiyle ilişkili gözlemlerinizi kaydetmek ve kaydedin.</span><span class="sxs-lookup"><span data-stu-id="37276-130">In **Notes**, record and save any observations associated with hello test failover.</span></span> <span data-ttu-id="37276-131">Bu adım hello sanal makineler ve yük devretme testi sırasında oluşturulan ağlar siler.</span><span class="sxs-lookup"><span data-stu-id="37276-131">This step deletes hello virtual machines and networks that were created during test failover.</span></span>


## <a name="next-steps"></a><span data-ttu-id="37276-132">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="37276-132">Next steps</span></span>

<span data-ttu-id="37276-133">Merhaba dağıtımı test ettikten sonra diğer türleri hakkında daha fazla bilgi [yük devretme](site-recovery-failover.md).</span><span class="sxs-lookup"><span data-stu-id="37276-133">After you've tested hello deployment, learn more about other types of [failover](site-recovery-failover.md).</span></span>
