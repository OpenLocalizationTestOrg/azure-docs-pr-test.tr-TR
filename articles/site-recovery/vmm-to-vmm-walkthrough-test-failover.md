---
title: "Azure Site Recovery ile ikincil site için bir yük devretme sınaması için Hyper-V VM çoğaltma çalıştırın | Microsoft Docs"
description: "Azure Site Recovery ile ikincil System Center VMM siteye bir yük devretme sınaması için Hyper-V VM çoğaltma çalıştırılacağını açıklar."
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
ms.openlocfilehash: 23d235d326273e7ec59feee6588a39f685401e52
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="step-10-run-a-test-failover-for-hyper-v-replication-to-a-secondary-site"></a><span data-ttu-id="f76ee-103">10. adım: yük devretme sınaması Hyper-V çoğaltma için ikincil bir siteye çalıştırma</span><span class="sxs-lookup"><span data-stu-id="f76ee-103">Step 10: Run a test failover for Hyper-V replication to a secondary site</span></span>


<span data-ttu-id="f76ee-104">Hyper-V sanal makineleri (VM'ler) için çoğaltma ile etkinleştirdikten sonra [Azure Site Recovery](site-recovery-overview.md), yük devretme testi çalıştırmak için bu makaleyi kullanın.</span><span class="sxs-lookup"><span data-stu-id="f76ee-104">After you enable replication for Hyper-V virtual machines (VMs) with [Azure Site Recovery](site-recovery-overview.md), use this article to run a test failover.</span></span> <span data-ttu-id="f76ee-105">Yük devretme testi çoğaltmanın üretim ortamınızı etkilemeden düzgün çalıştığını doğrular.</span><span class="sxs-lookup"><span data-stu-id="f76ee-105">A test failover verifies that replication is working, without impacting your production environment.</span></span> 


<span data-ttu-id="f76ee-106">Bu makaleyi okuduktan sonra yapmak istediğiniz tüm yorumları makalenin alt kısmında veya [Azure Kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)'nda paylaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f76ee-106">After reading this article, post any comments at the bottom, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="before-you-start"></a><span data-ttu-id="f76ee-107">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="f76ee-107">Before you start</span></span>

- <span data-ttu-id="f76ee-108">Yük devretme testi tetiklendiğinde test çoğaltma sanal makineleri bağlanacağı ağ belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f76ee-108">When you're triggering a test failover, you can specify the network to which the test replica VMs will connect.</span></span> <span data-ttu-id="f76ee-109">[Daha fazla bilgi edinin](site-recovery-test-failover-vmm-to-vmm.md#network-options-in-site-recovery) ağ seçenekleri hakkında.</span><span class="sxs-lookup"><span data-stu-id="f76ee-109">[Learn more](site-recovery-test-failover-vmm-to-vmm.md#network-options-in-site-recovery) about the network options.</span></span>
- <span data-ttu-id="f76ee-110">Ağ eşleme sırasında seçtiğiniz bir ağ seçmeyin öneririz.</span><span class="sxs-lookup"><span data-stu-id="f76ee-110">We recommend that you don't choose a network that you selected during network mapping.</span></span>
- <span data-ttu-id="f76ee-111">Bu makaledeki yönergeleri, tek bir VM vermesine açıklar.</span><span class="sxs-lookup"><span data-stu-id="f76ee-111">The instructions in this article describe how to fail over a single VM.</span></span> <span data-ttu-id="f76ee-112">Hakkında bilgi edinin [kurtarma planları oluşturma](site-recovery-create-recovery-plans.md) birden çok VM birlikte başarısız istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="f76ee-112">Read about [creating recovery plans](site-recovery-create-recovery-plans.md) if you want to fail over multiple VMs together.</span></span>
- <span data-ttu-id="f76ee-113">Hakkında bilgi edinin [yük devretme sınaması işlemlerini sınırlamalar](site-recovery-test-failover-vmm-to-vmm.md#things-to-note).</span><span class="sxs-lookup"><span data-stu-id="f76ee-113">Read about [limitations for test failovers](site-recovery-test-failover-vmm-to-vmm.md#things-to-note).</span></span>
- <span data-ttu-id="f76ee-114">Bir VM'ye yük devretme testi sırasında verilen IP adresi, VM alacağı aynı IP adresidir (IP adresi test yük devretme ağda kullanılabilir olduğunu pek fazla) planlanmış veya planlanmamış bir yük devretme için.</span><span class="sxs-lookup"><span data-stu-id="f76ee-114">The IP address given to a VM during test failover is the same IP address that the VM would receive for a planned or unplanned failover (presuming that the IP address is available in the test failover network).</span></span> <span data-ttu-id="f76ee-115">IP adresi test yük devretme ağda kullanılabilir değilse, VM test yük devretme ağı testinde kullanılabilirse başka bir IP adresi alır.</span><span class="sxs-lookup"><span data-stu-id="f76ee-115">If the IP address isn't available in the test failover network, the VM receives another IP address that is available in the test failover network.</span></span>
- <span data-ttu-id="f76ee-116">Yük devretme sınaması için uçtan uca ağ bağlantısı makinenin tam validatation, üretim ağınıza yapmak istiyorsanız, dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="f76ee-116">If you do want to do a test failover in your production network, for full validatation of end-to-end network connectivity machine, note that:</span></span>
    - <span data-ttu-id="f76ee-117">Test yük devretme yapılırken birincil VM kapatılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f76ee-117">The primary VM should be shut down when you're doing the test failover.</span></span> <span data-ttu-id="f76ee-118">Aksi takdirde, aynı kimliğe sahip iki VM aynı ağda birlikte aynı anda çalıştırırsınız.</span><span class="sxs-lookup"><span data-stu-id="f76ee-118">Otherwise, two VMs with the same identity will be running in the same network at the same time.</span></span> 
    - <span data-ttu-id="f76ee-119">Yük devretmeyi temiz olduğunda VM'ler test etmek için değişiklikler yapmak isterseniz, bu değişiklikler kaybolur.</span><span class="sxs-lookup"><span data-stu-id="f76ee-119">If you make changes to test VMs, those changes are lost when you clean up the test failover.</span></span> <span data-ttu-id="f76ee-120">Bu değişiklikler birincil VM çoğaltılmadığından.</span><span class="sxs-lookup"><span data-stu-id="f76ee-120">These changes aren't replicated back to the primary VM.</span></span>
    - <span data-ttu-id="f76ee-121">Testleri bir üretim ağı üretim iş yükleri için kapalı kalma süresi yol açar.</span><span class="sxs-lookup"><span data-stu-id="f76ee-121">Testing a a production network leads to downtime for your production workloads.</span></span> <span data-ttu-id="f76ee-122">Olağanüstü durum kurtarma ayrıntıya devam ederken uygulama kullanmamayı kullanıcılar isteyin.</span><span class="sxs-lookup"><span data-stu-id="f76ee-122">Ask users not to use the app when the disaster recovery drill is in progress.</span></span>  


## <a name="run-a-test-failover-for-a-vm"></a><span data-ttu-id="f76ee-123">Bir VM için yük devretme testi çalıştırma</span><span class="sxs-lookup"><span data-stu-id="f76ee-123">Run a test failover for a VM</span></span>

1. <span data-ttu-id="f76ee-124">Tek bir VM'ye yük devretme için **çoğaltılan öğeler**, VM tıklayın > **yük devretme testi**.</span><span class="sxs-lookup"><span data-stu-id="f76ee-124">To fail over a single VM, in **Replicated Items**, click the VM > **Test Failover**.</span></span>
2. <span data-ttu-id="f76ee-125">İçinde **sınama yük devretmesi**, test yük devretme sonrasında nasıl test sanal makineleri ağa bağlanacak belirtin.</span><span class="sxs-lookup"><span data-stu-id="f76ee-125">In **Test Failover**, specify how test VMs will be connected to networks after the test failover.</span></span> 
3. <span data-ttu-id="f76ee-126">Yük devretmeyi başlatmak için **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f76ee-126">Click **OK** to begin the failover.</span></span> <span data-ttu-id="f76ee-127">İlerleme durumunu izlemek **işleri** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="f76ee-127">Track progress on the **Jobs** tab.</span></span>
5. <span data-ttu-id="f76ee-128">Yük devretme işlemi tamamlandıktan sonra test sanal makineleri başarıyla başlatıldığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="f76ee-128">After failover is complete, verify that the test VMs start successfully.</span></span>
6. <span data-ttu-id="f76ee-129">İşiniz bittiğinde tıklatın **temizleme yük devretme testi** kurtarma planı üzerinde.</span><span class="sxs-lookup"><span data-stu-id="f76ee-129">When you're done, click **Cleanup test failover** on the recovery plan.</span></span>
7. <span data-ttu-id="f76ee-130">İçinde **notları**, kaydetme ve yük devretme testiyle ilişkili gözlemlerinizi kaydetmek.</span><span class="sxs-lookup"><span data-stu-id="f76ee-130">In **Notes**, record and save any observations associated with the test failover.</span></span> <span data-ttu-id="f76ee-131">Bu adım, yük devretme testi sırasında oluşturulan ağlar ve sanal makinelere siler.</span><span class="sxs-lookup"><span data-stu-id="f76ee-131">This step deletes the virtual machines and networks that were created during test failover.</span></span>


## <a name="next-steps"></a><span data-ttu-id="f76ee-132">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f76ee-132">Next steps</span></span>

<span data-ttu-id="f76ee-133">Dağıtımı test ettikten sonra diğer türleri hakkında daha fazla bilgi [yük devretme](site-recovery-failover.md).</span><span class="sxs-lookup"><span data-stu-id="f76ee-133">After you've tested the deployment, learn more about other types of [failover](site-recovery-failover.md).</span></span>
