---
title: "Azure Site Recovery ile azure'a (System Center VMM olmadan) Hyper-V Vm'lerini çoğaltma için çoğaltma etkinleştirme | Microsoft Docs"
description: "Azure VM'ler için çoğaltma Hyper-V Azure Site Recovery hizmetini kullanarak etkinleştirmek için gereken adımları özetler"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: bd31ef01-69f1-4591-a519-e42510a6e2f4
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: aabe99dbd375b80e4a87ca7a067927008672b4ed
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="step-10-enable-replication-for-hyper-v-vms-replicating-to-azure"></a><span data-ttu-id="fda73-103">10. adım: Hyper-V Vm'lerini Azure'a çoğaltma için çoğaltmayı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="fda73-103">Step 10: Enable replication for Hyper-V VMs replicating to Azure</span></span>


<span data-ttu-id="fda73-104">Bu makalede Azure, şirket içi Hyper-V sanal (System Center VMM tarafından yönetilmediğinden) makineler için çoğaltma etkinleştirme kullanarak [Azure Site Recovery](site-recovery-overview.md) Azure portalında hizmet.</span><span class="sxs-lookup"><span data-stu-id="fda73-104">This article describes how to enable replication for on-premises Hyper-V virtual machines (not managed by System Center VMM) to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="fda73-105">POST açıklamaları ve soruları alt bu makalenin veya üzerinde [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="fda73-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>




## <a name="before-you-start"></a><span data-ttu-id="fda73-106">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="fda73-106">Before you start</span></span>

<span data-ttu-id="fda73-107">Başlamadan önce Azure kullanıcı hesabınızın gerekli olduğundan emin olun [izinleri](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) yeni bir sanal makineye Azure çoğaltmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="fda73-107">Before you start, ensure that your Azure user account has the required [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) to enable replication of a new virtual machine to Azure.</span></span>

## <a name="exclude-disks-from-replication"></a><span data-ttu-id="fda73-108">Diskleri çoğaltmanın dışında tutma</span><span class="sxs-lookup"><span data-stu-id="fda73-108">Exclude disks from replication</span></span>

<span data-ttu-id="fda73-109">Varsayılan olarak, bir makine üzerindeki tüm diskleri çoğaltılır.</span><span class="sxs-lookup"><span data-stu-id="fda73-109">By default all disks on a machine are replicated.</span></span> <span data-ttu-id="fda73-110">Diskleri çoğaltmanın dışında bırakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fda73-110">You can exclude disks from replication.</span></span> <span data-ttu-id="fda73-111">Örneğin, geçici veriler veya her zaman bir makine yeniledi veri disklerini çoğaltmak istemeyebilirsiniz veya (örneğin pagefile.sys ya da SQL Server tempdb) uygulamasını yeniden başlatır.</span><span class="sxs-lookup"><span data-stu-id="fda73-111">For example you might not want to replicate disks with temporary data, or data that's refreshed each time a machine or application restarts (for example pagefile.sys or SQL Server tempdb).</span></span> [<span data-ttu-id="fda73-112">Daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="fda73-112">Learn more</span></span>](site-recovery-exclude-disk.md)


## <a name="replicate-vms"></a><span data-ttu-id="fda73-113">Vm'lerini çoğaltma</span><span class="sxs-lookup"><span data-stu-id="fda73-113">Replicate VMs</span></span>

<span data-ttu-id="fda73-114">VM'ler için çoğaltma gibi etkinleştirin:</span><span class="sxs-lookup"><span data-stu-id="fda73-114">Enable replication for VMs as follows:</span></span>          

1. <span data-ttu-id="fda73-115">Tıklatın **uygulama çoğaltma** > **kaynak**.</span><span class="sxs-lookup"><span data-stu-id="fda73-115">Click **Replicate application** > **Source**.</span></span> <span data-ttu-id="fda73-116">Çoğaltma ilk kez ayarladıktan sonra tıklayabilirsiniz **+ Çoğalt** ilave makineler için çoğaltmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="fda73-116">After you've set up replication for the first time, you can click **+Replicate** to enable replication for additional machines.</span></span>

    ![Çoğaltmayı etkinleştirme](./media/hyper-v-site-walkthrough-enable-replication/enable-replication.png)
2. <span data-ttu-id="fda73-118">İçinde **kaynak**, Hyper-V sitesi seçin.</span><span class="sxs-lookup"><span data-stu-id="fda73-118">In **Source**, select the Hyper-V site.</span></span> <span data-ttu-id="fda73-119">Daha sonra, **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fda73-119">Then click **OK**.</span></span>
3. <span data-ttu-id="fda73-120">İçinde **hedef**, kasa aboneliği seçin ve yük devretme modelini yük devretme sonrasında Azure (Klasik veya resource management) kullanmak istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="fda73-120">In **Target**, select the vault subscription, and the failover model you want to use in Azure (classic or resource management) after failover.</span></span>
4. <span data-ttu-id="fda73-121">Kullanmak istediğiniz depolama hesabını seçin.</span><span class="sxs-lookup"><span data-stu-id="fda73-121">Select the storage account you want to use.</span></span> <span data-ttu-id="fda73-122">Kullanmak istediğiniz bir hesabınız yoksa, şunları yapabilirsiniz [oluşturmak](#set-up-an-azure-storage-account).</span><span class="sxs-lookup"><span data-stu-id="fda73-122">If you don't have an account you want to use, you can [create one](#set-up-an-azure-storage-account).</span></span> <span data-ttu-id="fda73-123">Daha sonra, **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fda73-123">Then click **OK**.</span></span>
5. <span data-ttu-id="fda73-124">Azure ağı ve yük devretme oluşturulduğunda Azure Vm'lerinin bağlanacağı alt ağı seçin.</span><span class="sxs-lookup"><span data-stu-id="fda73-124">Select the Azure network and subnet to which Azure VMs will connect when they're created failover.</span></span>

    - <span data-ttu-id="fda73-125">Etkinleştirmeniz tüm makineleri çoğaltma için ağ ayarlarını uygulamak için seçin **seçili makineler için Şimdi Yapılandır**.</span><span class="sxs-lookup"><span data-stu-id="fda73-125">To apply the network settings to all machines you enable for replication, select **Configure now for selected machines**.</span></span>
    - <span data-ttu-id="fda73-126">Makineler için Azure ağını ayrı ayrı seçmek için **Daha sonra yapılandır**'ı seçin.</span><span class="sxs-lookup"><span data-stu-id="fda73-126">Select **Configure later** to select the Azure network per machine.</span></span>
    - <span data-ttu-id="fda73-127">Kullanmak istediğiniz ağ yoksa, şunları yapabilirsiniz [oluşturmak](#set-up-an-azure-network).</span><span class="sxs-lookup"><span data-stu-id="fda73-127">If you don't have a network you want to use, you can [create one](#set-up-an-azure-network).</span></span> <span data-ttu-id="fda73-128">Bir alt ağ (varsa) seçin.</span><span class="sxs-lookup"><span data-stu-id="fda73-128">Select a subnet if applicable.</span></span> <span data-ttu-id="fda73-129">Daha sonra, **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fda73-129">Then click **OK**.</span></span>

   ![Çoğaltmayı etkinleştirme](./media/hyper-v-site-walkthrough-enable-replication/enable-replication11.png)

6. <span data-ttu-id="fda73-131">**Sanal Makineler** > **Sanal makine seçin** seçeneklerine tıklayın ve çoğaltmak istediğiniz makineleri seçin.</span><span class="sxs-lookup"><span data-stu-id="fda73-131">In **Virtual Machines** > **Select virtual machines**, click and select each machine you want to replicate.</span></span> <span data-ttu-id="fda73-132">Yalnızca çoğaltmanın etkinleştirildiği makineleri seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fda73-132">You can only select machines for which replication can be enabled.</span></span> <span data-ttu-id="fda73-133">Daha sonra, **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fda73-133">Then click **OK**.</span></span>

    ![Çoğaltmayı etkinleştirme](./media/hyper-v-site-walkthrough-enable-replication/enable-replication5-for-exclude-disk.png)

7. <span data-ttu-id="fda73-135">**Özellikler** > **Özellikleri yapılandır** seçeneklerinde, seçili VM'ler için işletme sistemini ve OS diskini seçin.</span><span class="sxs-lookup"><span data-stu-id="fda73-135">In **Properties** > **Configure properties**, select the operating system for the selected VMs, and the OS disk.</span></span>
8. <span data-ttu-id="fda73-136">Azure VM adının (hedef ad) [Azure sanal makine gereksinimlerine](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) uygun olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="fda73-136">Verify that the Azure VM name (target name) complies with [Azure virtual machine requirements](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>
9. <span data-ttu-id="fda73-137">Varsayılan olarak VM'nin tüm diskleri çoğaltma için seçilir.</span><span class="sxs-lookup"><span data-stu-id="fda73-137">By default all the disks of the VM are selected for replication.</span></span> <span data-ttu-id="fda73-138">İçermeyecek şekilde Temizle diskler.</span><span class="sxs-lookup"><span data-stu-id="fda73-138">Clear disks to exclude them.</span></span>
10. <span data-ttu-id="fda73-139">Değişiklikleri kaydetmek için **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fda73-139">Click **OK** to save changes.</span></span> <span data-ttu-id="fda73-140">Daha sonra ek özellikleri ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fda73-140">You can set additional properties later.</span></span>

    ![Çoğaltmayı etkinleştirme](./media/hyper-v-site-walkthrough-enable-replication/enable-replication6-with-exclude-disk.png)

11. <span data-ttu-id="fda73-142">**Çoğaltma ayarları** > **Çoğaltma ayarlarını yapılandır** seçeneklerinde, korumalı VM'lere uygulamak istediğiniz çoğaltma ilkesini seçin.</span><span class="sxs-lookup"><span data-stu-id="fda73-142">In **Replication settings** > **Configure replication settings**, select the replication policy you want to apply for the protected VMs.</span></span> <span data-ttu-id="fda73-143">Daha sonra, **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fda73-143">Then click **OK**.</span></span> <span data-ttu-id="fda73-144">Çoğaltma ilkesini değiştirebilirsiniz **çoğaltma ilkeleri** > ilke adı > **ayarlarını Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="fda73-144">You can modify the replication policy in **Replication policies** > policy-name > **Edit Settings**.</span></span> <span data-ttu-id="fda73-145">Uyguladığınız değişiklikler, zaten çoğaltılmış olan makinelere ve yeni makinelere uygulanır.</span><span class="sxs-lookup"><span data-stu-id="fda73-145">Changes you apply will be used for machines that are already replicating, and new machines.</span></span>


   ![Çoğaltmayı etkinleştirme](./media/hyper-v-site-walkthrough-enable-replication/enable-replication7.png)

<span data-ttu-id="fda73-147">**İşler** > **Site Recovery işleri** üzerinden **Korumayı Etkinleştir** işinin ilerleyişini izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fda73-147">You can track progress of the **Enable Protection** job in **Jobs** > **Site Recovery jobs**.</span></span> <span data-ttu-id="fda73-148">**Korumayı Sonlandır** işi çalıştırıldıktan sonra makine yük devretme için hazırdır.</span><span class="sxs-lookup"><span data-stu-id="fda73-148">After the **Finalize Protection** job runs the machine is ready for failover.</span></span>


## <a name="next-steps"></a><span data-ttu-id="fda73-149">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="fda73-149">Next steps</span></span>


<span data-ttu-id="fda73-150">Git [11. adım: yük devretme testi çalıştırma](hyper-v-site-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="fda73-150">Go to [Step 11: Run a test failover](hyper-v-site-walkthrough-test-failover.md)</span></span>
