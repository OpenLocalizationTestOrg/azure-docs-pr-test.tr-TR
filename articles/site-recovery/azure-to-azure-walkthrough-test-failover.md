---
title: "Azure Site Recovery ile yük devretme sınaması Azure VM çoğaltması için çalıştırma | Microsoft Docs"
description: "Azure Site Recovery hizmetini kullanarak başka bir Azure bölgesine Azure Vm'lerini çoğaltma için bir yük devretme testi çalıştırmak için gereken adımları özetler."
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
ms.openlocfilehash: 8babb0d016729f318442af93596d206c38d91206
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="step-6-run-a-test-failover-for-azure-vm-replication"></a><span data-ttu-id="b4d64-103">6. adım: bir yük devretme sınaması için Azure VM çoğaltma çalıştırma</span><span class="sxs-lookup"><span data-stu-id="b4d64-103">Step 6: Run a test failover for Azure VM replication</span></span>

<span data-ttu-id="b4d64-104">Azure sanal makinesi (VM) için çoğaltma etkinleştirdikten sonra bir Azure bölgesinden diğerine kullanarak yük devretme testi çalıştırmak için bu makaledeki adımları [Azure Site Recovery](site-recovery-overview.md) Azure portalında hizmet.</span><span class="sxs-lookup"><span data-stu-id="b4d64-104">After you've enabled replication for Azure virtual machine (VMs), follow the steps in this article, to run test failover from one Azure region to another, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

- <span data-ttu-id="b4d64-105">Makaleyi tamamladığınızda, doğrulandı bir test yük devretmesi ile en az bir Azure VM, ikincil bir Azure bölgesine yük devredebildiğini.</span><span class="sxs-lookup"><span data-stu-id="b4d64-105">When you finish the article, you should have verified with a test failover, that at least one Azure VM can fail over to your secondary Azure region.</span></span> 
- <span data-ttu-id="b4d64-106">Bu makalenin sonundaki yorumları gönderin ya da sorular sormak [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span><span class="sxs-lookup"><span data-stu-id="b4d64-106">Post any comments at the bottom of this article, or ask questions in the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span></span>

>[!NOTE]
>
> <span data-ttu-id="b4d64-107">Azure VM çoğaltma şu anda önizlemede değil.</span><span class="sxs-lookup"><span data-stu-id="b4d64-107">Azure VM replication is currently in preview.</span></span>


## <a name="before-you-start"></a><span data-ttu-id="b4d64-108">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="b4d64-108">Before you start</span></span>

- <span data-ttu-id="b4d64-109">Yük devretme testi çalıştırmadan önce VM özelliklerini doğrulayın ve istediğiniz değişiklikleri yapın öneririz.</span><span class="sxs-lookup"><span data-stu-id="b4d64-109">Before you run a test failover, we recommend that you verify the VM properties, and make any changes you need to.</span></span> <span data-ttu-id="b4d64-110">VM Özellikleri'nde erişebilirsiniz **öğeleri çoğaltılan**.</span><span class="sxs-lookup"><span data-stu-id="b4d64-110">You can access the VM properties in **Replicated items**.</span></span> <span data-ttu-id="b4d64-111">**Essentials** dikey makineler ayarlarını ve durumu hakkında bilgileri gösterir.</span><span class="sxs-lookup"><span data-stu-id="b4d64-111">The **Essentials** blade shows information about machines settings and status.</span></span>
- <span data-ttu-id="b4d64-112">Yük devretme sınaması ve ağ için ayrı bir Azure VM ağ kullanmanız önerilir (varsayılan veya özelleştirilmiş), ayarlanan üretim yük devretme için.</span><span class="sxs-lookup"><span data-stu-id="b4d64-112">We recommend you use a separate Azure VM network for the test failover, and not the network (default or customized) that was set up for production failover.</span></span>
- <span data-ttu-id="b4d64-113">İkincil bir Azure bölgesine Azure Vm'leri (ve bunların depolama) yük devretme sınaması başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="b4d64-113">The test failover fails over Azure VMs (and their storage) to the secondary Azure region.</span></span> <span data-ttu-id="b4d64-114">Herhangi bir bağımlı uygulamaları veya kaynakları kopyalamaz.</span><span class="sxs-lookup"><span data-stu-id="b4d64-114">It doesn't replicate any dependent apps or resources.</span></span> <span data-ttu-id="b4d64-115">VM'ler başarısız çalışan uygulamaları Active Directory veya DNS gibi başka kaynaklar bağımlı olması durumunda zaten ikincil Bölgenizde kullanılabilir değillerse, bunlar çok, çoğaltma gerekir.</span><span class="sxs-lookup"><span data-stu-id="b4d64-115">If apps running on failed over VMs are dependent on other resources, such as Active Directory or DNS, you need to replicate these too, if they're not already available in your secondary region.</span></span> [<span data-ttu-id="b4d64-116">Daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="b4d64-116">Learn more</span></span>](site-recovery-test-failover-to-azure.md#prepare-active-directory-and-dns)
- <span data-ttu-id="b4d64-117">Bir şirket içi siteden yük devretme sonrasında çoğaltılmış VM'ler erişmek isterseniz, gerek [bağlamaya hazırlanmak](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover) bu VM'ler için.</span><span class="sxs-lookup"><span data-stu-id="b4d64-117">If you want to access replicated VMs after failover from an on-premises site, you need to [prepare to connect](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover) to these VMs.</span></span>

## <a name="run-a-test-failover"></a><span data-ttu-id="b4d64-118">Yük devretme testi çalıştırma</span><span class="sxs-lookup"><span data-stu-id="b4d64-118">Run a test failover</span></span>

1. <span data-ttu-id="b4d64-119">İçinde **ayarları** > **çoğaltılan öğeler**, VM tıklatın **+ yük devretme testi** simgesi.</span><span class="sxs-lookup"><span data-stu-id="b4d64-119">In **Settings** > **Replicated Items**, click the VM **+Test Failover** icon.</span></span> 

2. <span data-ttu-id="b4d64-120">İçinde **yük devretme testi**, yük devretme için kullanılacak bir kurtarma noktası seçin:</span><span class="sxs-lookup"><span data-stu-id="b4d64-120">In **Test Failover**, Select a recovery point to use for the failover:</span></span>

    - <span data-ttu-id="b4d64-121">**En son işlenen**: VM üzerinden Site Recovery hizmeti tarafından işlenen en son kurtarma noktası başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="b4d64-121">**Latest processed**: Fails the VM over to the latest recovery point that was processed by the Site Recovery service.</span></span> <span data-ttu-id="b4d64-122">Zaman damgası gösterilir.</span><span class="sxs-lookup"><span data-stu-id="b4d64-122">The time stamp is shown.</span></span> <span data-ttu-id="b4d64-123">Bu seçenek ile düşük RTO (Kurtarma süresi hedefi) sağlayan verileri işleme hiçbir zaman harcanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="b4d64-123">With this option, no time is spent processing data, so it provides a low RTO (Recovery Time Objective).</span></span>
    - <span data-ttu-id="b4d64-124">**Son uygulama tutarlı**: tüm sanal makineleri en son uygulamayla tutarlı kurtarma noktası için bu seçeneği yöneltilir.</span><span class="sxs-lookup"><span data-stu-id="b4d64-124">**Latest app-consistent**: This option fails over all VMs to the latest app-consistent recovery point.</span></span> <span data-ttu-id="b4d64-125">Zaman damgası gösterilir.</span><span class="sxs-lookup"><span data-stu-id="b4d64-125">The time stamp is shown.</span></span> 
    - <span data-ttu-id="b4d64-126">**Özel**: herhangi bir kurtarma noktası seçin.</span><span class="sxs-lookup"><span data-stu-id="b4d64-126">**Custom**: Select any recovery point.</span></span>
 
3. <span data-ttu-id="b4d64-127">Hedef Azure seçin ikincil bölge içindeki Azure Vm'lerinin sanal ağa bağlı olacak, yük devretme gerçekleştikten sonra.</span><span class="sxs-lookup"><span data-stu-id="b4d64-127">Select the target Azure virtual network to which Azure VMs in the secondary region will be connected, after the failover occurs.</span></span>
4. <span data-ttu-id="b4d64-128">Yük devretmeyi başlatmak için tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="b4d64-128">To start the failover, click **OK**.</span></span> <span data-ttu-id="b4d64-129">İlerleme durumunu izlemek için VM özelliklerini açmak için tıklatın.</span><span class="sxs-lookup"><span data-stu-id="b4d64-129">To track progress, click the VM to open its properties.</span></span> <span data-ttu-id="b4d64-130">Ya da tıklayabilirsiniz **yük devretme testi** kasa adını işinde > **ayarları** > **işleri** > **Site Recovery işleri**.</span><span class="sxs-lookup"><span data-stu-id="b4d64-130">Or, you can click the **Test Failover** job in the vault name > **Settings** > **Jobs** > **Site Recovery jobs**.</span></span>
5. <span data-ttu-id="b4d64-131">Yük devretme işlemi tamamlandıktan sonra çoğaltma Azure VM Azure portalında görünür. > **sanal makineleri**.</span><span class="sxs-lookup"><span data-stu-id="b4d64-131">After the failover finishes, the replica Azure VM appears in the Azure portal > **Virtual Machines**.</span></span> <span data-ttu-id="b4d64-132">VM, uygun bir ağa bağlı olduğu uygun boyutta olduğundan ve çalıştığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="b4d64-132">Make sure that the VM is the appropriate size, that it's connected to the appropriate network, and that it's running.</span></span>
6. <span data-ttu-id="b4d64-133">Yük devretme testi sırasında oluşturulan sanal makineleri silmek için tıklatın **temizleme yük devretme testi** çoğaltılmış öğesi ya da kurtarma planı.</span><span class="sxs-lookup"><span data-stu-id="b4d64-133">To delete the VMs that were created during the test failover, click **Cleanup test failover** on the replicated item or the recovery plan.</span></span> <span data-ttu-id="b4d64-134">İçinde **notları**, kaydetme ve yük devretme testiyle ilişkili gözlemlerinizi kaydetmek.</span><span class="sxs-lookup"><span data-stu-id="b4d64-134">In **Notes**, record and save any observations associated with the test failover.</span></span> 

<span data-ttu-id="b4d64-135">[Daha fazla bilgi edinin](site-recovery-test-failover-to-azure.md) yük devretme sınaması işlemlerini hakkında.</span><span class="sxs-lookup"><span data-stu-id="b4d64-135">[Learn more](site-recovery-test-failover-to-azure.md) about test failovers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b4d64-136">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b4d64-136">Next steps</span></span>

<span data-ttu-id="b4d64-137">Yük devretme test ettikten sonra bu kılavuzda tamamlanır.</span><span class="sxs-lookup"><span data-stu-id="b4d64-137">After you've tested failover, this walkthrough is complete.</span></span> <span data-ttu-id="b4d64-138">Şimdi, yük devretme işlemlerini üretimde çalıştırma hakkında bilgi alın:</span><span class="sxs-lookup"><span data-stu-id="b4d64-138">Now, learn about running failovers in production:</span></span>

- <span data-ttu-id="b4d64-139">[Daha fazla bilgi edinin](site-recovery-failover.md) farklı türdeki yük devretmeler ve bunları çalıştırma hakkında.</span><span class="sxs-lookup"><span data-stu-id="b4d64-139">[Learn more](site-recovery-failover.md) about different types of failovers, and how to run them.</span></span>
- <span data-ttu-id="b4d64-140">Birden çok VM başarısız hakkında daha fazla bilgi [bir kurtarma planı kullanarak](site-recovery-create-recovery-plans.md).</span><span class="sxs-lookup"><span data-stu-id="b4d64-140">Learn more about failing over multiple VMs [using a recovery plan](site-recovery-create-recovery-plans.md).</span></span>
- <span data-ttu-id="b4d64-141">Daha fazla bilgi edinmek [kurtarma planlarına kullanarak](site-recovery-create-recovery-plans.md).</span><span class="sxs-lookup"><span data-stu-id="b4d64-141">Learn more about [using recovery plans](site-recovery-create-recovery-plans.md).</span></span>
- <span data-ttu-id="b4d64-142">Daha fazla bilgi edinmek [Azure sanal makineleri yeniden korumayı](site-recovery-how-to-reprotect.md) yük devretme sonrasında.</span><span class="sxs-lookup"><span data-stu-id="b4d64-142">Learn more about [reprotecting Azure  VMs](site-recovery-how-to-reprotect.md) after failover.</span></span>

