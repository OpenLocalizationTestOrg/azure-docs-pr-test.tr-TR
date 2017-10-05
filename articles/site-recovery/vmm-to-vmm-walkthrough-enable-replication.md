---
title: "Hyper-V çoğaltma Azure Site Recovery ile ikincil siteye etkinleştirme | Microsoft Docs"
description: "Azure Site Recovery ile ikincil System Center VMM siteye Hyper-V Vm'lerini çoğaltma için çoğaltmayı etkinleştirmek açıklar."
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
ms.openlocfilehash: 6673d192dbc18bfc955d9e7e3c55893512511ffb
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="step-9-enable-replication-to-a-secondary-site-for-hyper-v-vms"></a><span data-ttu-id="bd062-103">9. adım: Hyper-V Vm'lerini ikincil bir site için çoğaltmayı etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="bd062-103">Step 9: Enable replication to a secondary site for Hyper-V VMs</span></span>


<span data-ttu-id="bd062-104">Bir çoğaltma ilkesi ayarlama kullandıktan sonra bu makalede bir ikincil şirket içi Hyper-V sanal makinelerini (VM) System Center Virtual Machine Manager (VMM) sitesine çoğaltmayı etkinleştirmek için kullanarak [Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bd062-104">After setting up a replication policy, use this article to enable replication to a secondary System Center Virtual Machine Manager (VMM) site for on-premises Hyper-V virtual machines (VM), using [Azure Site Recovery](site-recovery-overview.md).</span></span>

<span data-ttu-id="bd062-105">Bu makaleyi okuduktan sonra yapmak istediğiniz tüm yorumları makalenin alt kısmında veya [Azure Kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)'nda paylaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd062-105">After reading this article, post any comments at the bottom, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>



## <a name="select-vms-to-replicate"></a><span data-ttu-id="bd062-106">Çoğaltma sanal makineleri seçin</span><span class="sxs-lookup"><span data-stu-id="bd062-106">Select VMs to replicate</span></span>

1. <span data-ttu-id="bd062-107">**2. Adım: Uygulama çoğaltma** > **Kaynak** seçeneklerine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bd062-107">Click **Step 2: Replicate application** > **Source**.</span></span> 

    ![Çoğaltmayı etkinleştirme](./media/vmm-to-vmm-walkthrough-enable-replication/enable-replication1.png)

2. <span data-ttu-id="bd062-109">İçinde **kaynak**, VMM sunucusu ve çoğaltmak istediğiniz Hyper-V konakları olduğu bulunduğu Bulutu seçin.</span><span class="sxs-lookup"><span data-stu-id="bd062-109">In **Source**, select the VMM server, and the cloud in which the Hyper-V hosts you want to replicate are located.</span></span> <span data-ttu-id="bd062-110">Daha sonra, **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bd062-110">Then click **OK**.</span></span>

    ![Çoğaltmayı etkinleştirme](./media/vmm-to-vmm-walkthrough-enable-replication/enable-replication2.png)
3. <span data-ttu-id="bd062-112">İçinde **hedef**, ikincil VMM sunucusu ve bulut doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="bd062-112">In **Target**, verify the secondary VMM server and cloud.</span></span>
4. <span data-ttu-id="bd062-113">İçinde **sanal makineleri**, listeden korumak istediğiniz sanal makineleri seçin.</span><span class="sxs-lookup"><span data-stu-id="bd062-113">In **Virtual machines**, select the VMs you want to protect from the list.</span></span>

    ![Sanal makine korumasını etkinleştirme](./media/vmm-to-vmm-walkthrough-enable-replication/enable-replication5.png)

<span data-ttu-id="bd062-115">İlerleme durumunu izleyebilirsiniz **korumayı etkinleştir** eylemde **işleri** > **Site Recovery işleri**.</span><span class="sxs-lookup"><span data-stu-id="bd062-115">You can track progress of the **Enable Protection** action in **Jobs** > **Site Recovery jobs**.</span></span> <span data-ttu-id="bd062-116">Sonra **korumayı Sonlandır** işi tamamlandığında, ilk çoğaltma tamamlandıktan ve sanal makine yük devretme için hazırdır.</span><span class="sxs-lookup"><span data-stu-id="bd062-116">After the **Finalize Protection** job completes, the initial replication is complete, and the virtual machine is ready for failover.</span></span>

<span data-ttu-id="bd062-117">Şunlara dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="bd062-117">Note that:</span></span>

- <span data-ttu-id="bd062-118">VMM konsolunda sanal makineler için korumayı etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd062-118">You can also enable protection for virtual machines in the VMM console.</span></span> <span data-ttu-id="bd062-119">Tıklatın **korumayı etkinleştir** sanal makine özellikleri araç çubuğunda > **Azure Site Recovery** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="bd062-119">Click **Enable Protection** on the toolbar in the virtual machine properties > **Azure Site Recovery** tab.</span></span>
- <span data-ttu-id="bd062-120">Çoğaltma etkinleştirdikten sonra VM için özelliklerini görüntüleyebilirsiniz **çoğaltılan öğeler**.</span><span class="sxs-lookup"><span data-stu-id="bd062-120">After you've enabled replication, you can view properties for the VM in **Replicated Items**.</span></span> <span data-ttu-id="bd062-121">Üzerinde **Essentials** Pano, VM ve durumunu çoğaltma ilkesi hakkında bilgi görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd062-121">On the **Essentials** dashboard, you can see information about the replication policy for the VM and its status.</span></span> <span data-ttu-id="bd062-122">Tıklatın **özellikleri** daha fazla ayrıntı için.</span><span class="sxs-lookup"><span data-stu-id="bd062-122">Click **Properties** for more details.</span></span>

## <a name="onboard-existing-vms"></a><span data-ttu-id="bd062-123">Yerleşik VM'ler</span><span class="sxs-lookup"><span data-stu-id="bd062-123">Onboard existing VMs</span></span>

<span data-ttu-id="bd062-124">Hyper-V çoğaltma ile çoğaltma mevcut sanal makineler VMM varsa, gerçekleştirebilir şekilde Azure Site Recovery çoğaltma için:</span><span class="sxs-lookup"><span data-stu-id="bd062-124">If you have existing virtual machines in VMM that are replicating with Hyper-V Replica, you can onboard them for Azure Site Recovery replication as follows:</span></span>

1. <span data-ttu-id="bd062-125">Var olan VM barındıran Hyper-V server birincil buluta bulunur ve çoğaltma sanal makine barındıran Hyper-V sunucusu ikincil bulutta bulunduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="bd062-125">Ensure that the Hyper-V server hosting the existing VM is located in the primary cloud, and that the Hyper-V server hosting the replica virtual machine is located in the secondary cloud.</span></span>
2. <span data-ttu-id="bd062-126">Bir çoğaltma ilkesi birincil VMM bulutu için yapılandırılmış olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="bd062-126">Make sure a replication policy is configured for the primary VMM cloud.</span></span>
3. <span data-ttu-id="bd062-127">Birincil sanal makine çoğaltmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="bd062-127">Enable replication for the primary virtual machine.</span></span> <span data-ttu-id="bd062-128">Azure Site Recovery ile VMM aynı çoğaltma konak ve sanal makine algılandığında, ve Azure Site Recovery yeniden kullanmak ve belirtilen ayarları kullanarak çoğaltmayı yeniden oluşturmak emin olun.</span><span class="sxs-lookup"><span data-stu-id="bd062-128">Azure Site Recovery and VMM ensure that the same replica host and virtual machine is detected, and Azure Site Recovery will reuse and reestablish replication using the specified settings.</span></span>


## <a name="next-steps"></a><span data-ttu-id="bd062-129">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="bd062-129">Next steps</span></span>

<span data-ttu-id="bd062-130">Git [adım 10: bir yük devretme testi](vmm-to-vmm-walkthrough-test-failover.md).</span><span class="sxs-lookup"><span data-stu-id="bd062-130">Go to [Step 10: Run a test failover](vmm-to-vmm-walkthrough-test-failover.md).</span></span>
