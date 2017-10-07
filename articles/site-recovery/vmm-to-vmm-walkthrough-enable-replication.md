---
title: "aaaEnable Hyper-V çoğaltma tooa Azure Site Recovery ile ikincil site | Microsoft Docs"
description: "Nasıl tooenable çoğaltma Hyper-V sanal makinelerini tooa çoğaltmak için ikincil System Center VMM site Azure Site Recovery ile açıklar."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d8782d14-9fef-4396-8912-ff945efc851b
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: b4484e0118cb23f343187fe867d9795d30926baf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-enable-replication-tooa-secondary-site-for-hyper-v-vms"></a><span data-ttu-id="2f2a8-103">9. adım: çoğaltma tooa ikincil site için Hyper-V sanal makineleri etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="2f2a8-103">Step 9: Enable replication tooa secondary site for Hyper-V VMs</span></span>


<span data-ttu-id="2f2a8-104">Bir çoğaltma ilkesi ayarladıktan sonra bu makale tooenable çoğaltma tooa ikincil System Center Virtual Machine Manager (VMM) site içi Hyper-V sanal kullanarak makineler için (VM) kullanmanız [Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2f2a8-104">After setting up a replication policy, use this article tooenable replication tooa secondary System Center Virtual Machine Manager (VMM) site for on-premises Hyper-V virtual machines (VM), using [Azure Site Recovery](site-recovery-overview.md).</span></span>

<span data-ttu-id="2f2a8-105">Bu makaleyi okuduktan sonra tüm yorumlar hello altındaki ya da hello sonrası [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="2f2a8-105">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>



## <a name="select-vms-tooreplicate"></a><span data-ttu-id="2f2a8-106">Sanal makineleri tooreplicate seçin</span><span class="sxs-lookup"><span data-stu-id="2f2a8-106">Select VMs tooreplicate</span></span>

1. <span data-ttu-id="2f2a8-107">**2. Adım: Uygulama çoğaltma** > **Kaynak** seçeneklerine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2f2a8-107">Click **Step 2: Replicate application** > **Source**.</span></span> 

    ![Çoğaltmayı etkinleştirme](./media/vmm-to-vmm-walkthrough-enable-replication/enable-replication1.png)

2. <span data-ttu-id="2f2a8-109">İçinde **kaynak**hello VMM sunucusunu seçin ve hello hangi hello tooreplicate istediğiniz Hyper-V konaklarının bulunduğu bulut.</span><span class="sxs-lookup"><span data-stu-id="2f2a8-109">In **Source**, select hello VMM server, and hello cloud in which hello Hyper-V hosts you want tooreplicate are located.</span></span> <span data-ttu-id="2f2a8-110">Daha sonra, **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2f2a8-110">Then click **OK**.</span></span>

    ![Çoğaltmayı etkinleştirme](./media/vmm-to-vmm-walkthrough-enable-replication/enable-replication2.png)
3. <span data-ttu-id="2f2a8-112">İçinde **hedef**, hello ikincil VMM sunucusu ve bulut doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="2f2a8-112">In **Target**, verify hello secondary VMM server and cloud.</span></span>
4. <span data-ttu-id="2f2a8-113">İçinde **sanal makineleri**, tooprotect hello listeden istediğiniz hello VM'ler seçin.</span><span class="sxs-lookup"><span data-stu-id="2f2a8-113">In **Virtual machines**, select hello VMs you want tooprotect from hello list.</span></span>

    ![Sanal makine korumasını etkinleştirme](./media/vmm-to-vmm-walkthrough-enable-replication/enable-replication5.png)

<span data-ttu-id="2f2a8-115">Merhaba ilerlemesini izleyebilirsiniz **korumayı etkinleştir** eylemde **işleri** > **Site Recovery işleri**.</span><span class="sxs-lookup"><span data-stu-id="2f2a8-115">You can track progress of hello **Enable Protection** action in **Jobs** > **Site Recovery jobs**.</span></span> <span data-ttu-id="2f2a8-116">Merhaba sonra **korumayı Sonlandır** işi tamamlandığında, hello ilk çoğaltma tamamlandıktan ve hello sanal makine yük devretme için hazır.</span><span class="sxs-lookup"><span data-stu-id="2f2a8-116">After hello **Finalize Protection** job completes, hello initial replication is complete, and hello virtual machine is ready for failover.</span></span>

<span data-ttu-id="2f2a8-117">Şunlara dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="2f2a8-117">Note that:</span></span>

- <span data-ttu-id="2f2a8-118">Merhaba VMM konsolunda sanal makineler için korumayı etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2f2a8-118">You can also enable protection for virtual machines in hello VMM console.</span></span> <span data-ttu-id="2f2a8-119">Tıklatın **korumayı etkinleştir** hello sanal makine Özellikleri'nde hello araç çubuğunda > **Azure Site Recovery** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="2f2a8-119">Click **Enable Protection** on hello toolbar in hello virtual machine properties > **Azure Site Recovery** tab.</span></span>
- <span data-ttu-id="2f2a8-120">Çoğaltma etkinleştirdikten sonra hello VM özelliklerini görüntüleyebilir, **çoğaltılan öğeler**.</span><span class="sxs-lookup"><span data-stu-id="2f2a8-120">After you've enabled replication, you can view properties for hello VM in **Replicated Items**.</span></span> <span data-ttu-id="2f2a8-121">Merhaba üzerinde **Essentials** panoyu hello çoğaltma ilkesi hello VM ve durumu hakkındaki bilgileri görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2f2a8-121">On hello **Essentials** dashboard, you can see information about hello replication policy for hello VM and its status.</span></span> <span data-ttu-id="2f2a8-122">Tıklatın **özellikleri** daha fazla ayrıntı için.</span><span class="sxs-lookup"><span data-stu-id="2f2a8-122">Click **Properties** for more details.</span></span>

## <a name="onboard-existing-vms"></a><span data-ttu-id="2f2a8-123">Yerleşik VM'ler</span><span class="sxs-lookup"><span data-stu-id="2f2a8-123">Onboard existing VMs</span></span>

<span data-ttu-id="2f2a8-124">Hyper-V çoğaltma ile çoğaltma mevcut sanal makineler VMM varsa, gerçekleştirebilir şekilde Azure Site Recovery çoğaltma için:</span><span class="sxs-lookup"><span data-stu-id="2f2a8-124">If you have existing virtual machines in VMM that are replicating with Hyper-V Replica, you can onboard them for Azure Site Recovery replication as follows:</span></span>

1. <span data-ttu-id="2f2a8-125">VM varolan hello barındıran hello Hyper-V server hello birincil bulutta bulunduğundan ve hello çoğaltma sanal makinesi barındıran bu hello Hyper-V server hello ikincil bulutta bulunduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="2f2a8-125">Ensure that hello Hyper-V server hosting hello existing VM is located in hello primary cloud, and that hello Hyper-V server hosting hello replica virtual machine is located in hello secondary cloud.</span></span>
2. <span data-ttu-id="2f2a8-126">Bir çoğaltma ilkesi hello birincil VMM bulutu için yapılandırılmış olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="2f2a8-126">Make sure a replication policy is configured for hello primary VMM cloud.</span></span>
3. <span data-ttu-id="2f2a8-127">Merhaba birincil sanal makine için çoğaltmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="2f2a8-127">Enable replication for hello primary virtual machine.</span></span> <span data-ttu-id="2f2a8-128">Azure Site Recovery ve VMM hello aynı çoğaltma konak ve sanal makine algılandığında, Azure Site Recovery yeniden kullanılacak ve hello kullanarak yeniden çoğaltma ayarları belirtilen emin olun.</span><span class="sxs-lookup"><span data-stu-id="2f2a8-128">Azure Site Recovery and VMM ensure that hello same replica host and virtual machine is detected, and Azure Site Recovery will reuse and reestablish replication using hello specified settings.</span></span>


## <a name="next-steps"></a><span data-ttu-id="2f2a8-129">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2f2a8-129">Next steps</span></span>

<span data-ttu-id="2f2a8-130">Çok Git[adım 10: bir yük devretme testi](vmm-to-vmm-walkthrough-test-failover.md).</span><span class="sxs-lookup"><span data-stu-id="2f2a8-130">Go too[Step 10: Run a test failover](vmm-to-vmm-walkthrough-test-failover.md).</span></span>
