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
# <a name="step-6-run-a-test-failover-for-azure-vm-replication"></a><span data-ttu-id="5a407-103">6. adım: bir yük devretme sınaması için Azure VM çoğaltma çalıştırma</span><span class="sxs-lookup"><span data-stu-id="5a407-103">Step 6: Run a test failover for Azure VM replication</span></span>

<span data-ttu-id="5a407-104">Azure sanal makinesi (VM) için çoğaltma etkinleştirdikten sonra hello toorun test hello kullanarak bir Azure bölgesi tooanother yük devretmeyi bu makaledeki adımları [Azure Site Recovery](site-recovery-overview.md) hello Azure portal hizmeti.</span><span class="sxs-lookup"><span data-stu-id="5a407-104">After you've enabled replication for Azure virtual machine (VMs), follow hello steps in this article, toorun test failover from one Azure region tooanother, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

- <span data-ttu-id="5a407-105">Hello makale bitirdikten sonra doğrulandı bir test yük devretmesi ile en az bir Azure VM tooyour ikincil Azure bölgesi başarısız olabilir.</span><span class="sxs-lookup"><span data-stu-id="5a407-105">When you finish hello article, you should have verified with a test failover, that at least one Azure VM can fail over tooyour secondary Azure region.</span></span> 
- <span data-ttu-id="5a407-106">Bu makalenin hello altındaki tüm yorumlar gönderin ya da hello sorular sormak [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span><span class="sxs-lookup"><span data-stu-id="5a407-106">Post any comments at hello bottom of this article, or ask questions in hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span></span>

>[!NOTE]
>
> <span data-ttu-id="5a407-107">Azure VM çoğaltma şu anda önizlemede değil.</span><span class="sxs-lookup"><span data-stu-id="5a407-107">Azure VM replication is currently in preview.</span></span>


## <a name="before-you-start"></a><span data-ttu-id="5a407-108">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="5a407-108">Before you start</span></span>

- <span data-ttu-id="5a407-109">Yük devretme testi çalıştırmadan önce hello VM özelliklerini doğrulayın ve istediğiniz değişiklikleri yapın öneririz.</span><span class="sxs-lookup"><span data-stu-id="5a407-109">Before you run a test failover, we recommend that you verify hello VM properties, and make any changes you need to.</span></span> <span data-ttu-id="5a407-110">Merhaba VM Özellikleri'nde erişebilirsiniz **öğeleri çoğaltılan**.</span><span class="sxs-lookup"><span data-stu-id="5a407-110">You can access hello VM properties in **Replicated items**.</span></span> <span data-ttu-id="5a407-111">Merhaba **Essentials** dikey makineler ayarlarını ve durumu hakkında bilgileri gösterir.</span><span class="sxs-lookup"><span data-stu-id="5a407-111">hello **Essentials** blade shows information about machines settings and status.</span></span>
- <span data-ttu-id="5a407-112">Merhaba test yük devretme ve değil hello ağ için ayrı bir Azure VM ağ kullanmanız önerilir (varsayılan veya özelleştirilmiş), ayarlanan üretim yük devretme için.</span><span class="sxs-lookup"><span data-stu-id="5a407-112">We recommend you use a separate Azure VM network for hello test failover, and not hello network (default or customized) that was set up for production failover.</span></span>
- <span data-ttu-id="5a407-113">Merhaba test yük devretme başarısız Azure Vm'leri (ve bunların depolama) üzerinden toohello ikincil Azure bölgesi.</span><span class="sxs-lookup"><span data-stu-id="5a407-113">hello test failover fails over Azure VMs (and their storage) toohello secondary Azure region.</span></span> <span data-ttu-id="5a407-114">Herhangi bir bağımlı uygulamaları veya kaynakları kopyalamaz.</span><span class="sxs-lookup"><span data-stu-id="5a407-114">It doesn't replicate any dependent apps or resources.</span></span> <span data-ttu-id="5a407-115">VM'ler başarısız çalışan uygulamaları Active Directory veya DNS gibi başka kaynaklar bağımlı olması durumunda zaten ikincil Bölgenizde kullanılabilir değillerse, tooreplicate bunlar de gerekir.</span><span class="sxs-lookup"><span data-stu-id="5a407-115">If apps running on failed over VMs are dependent on other resources, such as Active Directory or DNS, you need tooreplicate these too, if they're not already available in your secondary region.</span></span> [<span data-ttu-id="5a407-116">Daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="5a407-116">Learn more</span></span>](site-recovery-test-failover-to-azure.md#prepare-active-directory-and-dns)
- <span data-ttu-id="5a407-117">Bir şirket içi siteden yük devretme sonrasında tooaccess çoğaltılan VM'ler istiyorsanız, çok ihtiyacınız[tooconnect hazırlama](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover) toothese VM'ler.</span><span class="sxs-lookup"><span data-stu-id="5a407-117">If you want tooaccess replicated VMs after failover from an on-premises site, you need too[prepare tooconnect](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover) toothese VMs.</span></span>

## <a name="run-a-test-failover"></a><span data-ttu-id="5a407-118">Yük devretme testi çalıştırma</span><span class="sxs-lookup"><span data-stu-id="5a407-118">Run a test failover</span></span>

1. <span data-ttu-id="5a407-119">İçinde **ayarları** > **çoğaltılan öğeler**, hello VM tıklatın **+ yük devretme testi** simgesi.</span><span class="sxs-lookup"><span data-stu-id="5a407-119">In **Settings** > **Replicated Items**, click hello VM **+Test Failover** icon.</span></span> 

2. <span data-ttu-id="5a407-120">İçinde **yük devretme testi**, bir kurtarma noktası toouse hello yük devretme için seçin:</span><span class="sxs-lookup"><span data-stu-id="5a407-120">In **Test Failover**, Select a recovery point toouse for hello failover:</span></span>

    - <span data-ttu-id="5a407-121">**En son işlenen**: başarısız hello Site Recovery hizmeti tarafından işlenmiş toohello en son kurtarma noktası üzerinden VM hello.</span><span class="sxs-lookup"><span data-stu-id="5a407-121">**Latest processed**: Fails hello VM over toohello latest recovery point that was processed by hello Site Recovery service.</span></span> <span data-ttu-id="5a407-122">Merhaba zaman damgası gösterilir.</span><span class="sxs-lookup"><span data-stu-id="5a407-122">hello time stamp is shown.</span></span> <span data-ttu-id="5a407-123">Bu seçenek ile düşük RTO (Kurtarma süresi hedefi) sağlayan verileri işleme hiçbir zaman harcanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="5a407-123">With this option, no time is spent processing data, so it provides a low RTO (Recovery Time Objective).</span></span>
    - <span data-ttu-id="5a407-124">**Son uygulama tutarlı**: Bu seçenek tüm VM'ler toohello en son uygulama tutarlı bir kurtarma noktası başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="5a407-124">**Latest app-consistent**: This option fails over all VMs toohello latest app-consistent recovery point.</span></span> <span data-ttu-id="5a407-125">Merhaba zaman damgası gösterilir.</span><span class="sxs-lookup"><span data-stu-id="5a407-125">hello time stamp is shown.</span></span> 
    - <span data-ttu-id="5a407-126">**Özel**: herhangi bir kurtarma noktası seçin.</span><span class="sxs-lookup"><span data-stu-id="5a407-126">**Custom**: Select any recovery point.</span></span>
 
3. <span data-ttu-id="5a407-127">Merhaba yük devretme gerçekleştikten sonra select hello hedef Azure sanal ağı toowhich ikincil bölge'hello Azure Vm'lerde bağlanır.</span><span class="sxs-lookup"><span data-stu-id="5a407-127">Select hello target Azure virtual network toowhich Azure VMs in hello secondary region will be connected, after hello failover occurs.</span></span>
4. <span data-ttu-id="5a407-128">toostart yük devretme Merhaba, tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="5a407-128">toostart hello failover, click **OK**.</span></span> <span data-ttu-id="5a407-129">tootrack ilerleme, hello VM tooopen, Özellikler'i tıklatın.</span><span class="sxs-lookup"><span data-stu-id="5a407-129">tootrack progress, click hello VM tooopen its properties.</span></span> <span data-ttu-id="5a407-130">Veya hello tıklatabilirsiniz **yük devretme testi** hello kasa adı işinde > **ayarları** > **işleri** > **Site Recovery işleri**.</span><span class="sxs-lookup"><span data-stu-id="5a407-130">Or, you can click hello **Test Failover** job in hello vault name > **Settings** > **Jobs** > **Site Recovery jobs**.</span></span>
5. <span data-ttu-id="5a407-131">Merhaba sonra Yük devretme, hello çoğaltma Azure VM hello Azure portalında görünür bittikten > **sanal makineleri**.</span><span class="sxs-lookup"><span data-stu-id="5a407-131">After hello failover finishes, hello replica Azure VM appears in hello Azure portal > **Virtual Machines**.</span></span> <span data-ttu-id="5a407-132">Bu hello VM toohello uygun ağ ve çalıştığını bağlı hello uygun boyutta olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="5a407-132">Make sure that hello VM is hello appropriate size, that it's connected toohello appropriate network, and that it's running.</span></span>
6. <span data-ttu-id="5a407-133">toodelete hello hello test yük devretmesi sırasında oluşturulan VM'ler tıklatın **temizleme yük devretme sınaması** öğesi veya hello kurtarma planı üzerinde hello yinelenmiş.</span><span class="sxs-lookup"><span data-stu-id="5a407-133">toodelete hello VMs that were created during hello test failover, click **Cleanup test failover** on hello replicated item or hello recovery plan.</span></span> <span data-ttu-id="5a407-134">İçinde **notları**hello yük devretme testiyle ilişkili gözlemlerinizi kaydetmek ve kaydedin.</span><span class="sxs-lookup"><span data-stu-id="5a407-134">In **Notes**, record and save any observations associated with hello test failover.</span></span> 

<span data-ttu-id="5a407-135">[Daha fazla bilgi edinin](site-recovery-test-failover-to-azure.md) yük devretme sınaması işlemlerini hakkında.</span><span class="sxs-lookup"><span data-stu-id="5a407-135">[Learn more](site-recovery-test-failover-to-azure.md) about test failovers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5a407-136">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5a407-136">Next steps</span></span>

<span data-ttu-id="5a407-137">Yük devretme test ettikten sonra bu kılavuzda tamamlanır.</span><span class="sxs-lookup"><span data-stu-id="5a407-137">After you've tested failover, this walkthrough is complete.</span></span> <span data-ttu-id="5a407-138">Şimdi, yük devretme işlemlerini üretimde çalıştırma hakkında bilgi alın:</span><span class="sxs-lookup"><span data-stu-id="5a407-138">Now, learn about running failovers in production:</span></span>

- <span data-ttu-id="5a407-139">[Daha fazla bilgi edinin](site-recovery-failover.md) yerine, farklı türlerde hakkında ve nasıl toorun bunları.</span><span class="sxs-lookup"><span data-stu-id="5a407-139">[Learn more](site-recovery-failover.md) about different types of failovers, and how toorun them.</span></span>
- <span data-ttu-id="5a407-140">Birden çok VM başarısız hakkında daha fazla bilgi [bir kurtarma planı kullanarak](site-recovery-create-recovery-plans.md).</span><span class="sxs-lookup"><span data-stu-id="5a407-140">Learn more about failing over multiple VMs [using a recovery plan](site-recovery-create-recovery-plans.md).</span></span>
- <span data-ttu-id="5a407-141">Daha fazla bilgi edinmek [kurtarma planlarına kullanarak](site-recovery-create-recovery-plans.md).</span><span class="sxs-lookup"><span data-stu-id="5a407-141">Learn more about [using recovery plans](site-recovery-create-recovery-plans.md).</span></span>
- <span data-ttu-id="5a407-142">Daha fazla bilgi edinmek [Azure sanal makineleri yeniden korumayı](site-recovery-how-to-reprotect.md) yük devretme sonrasında.</span><span class="sxs-lookup"><span data-stu-id="5a407-142">Learn more about [reprotecting Azure  VMs](site-recovery-how-to-reprotect.md) after failover.</span></span>

