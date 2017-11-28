---
title: "Hyper-V Vm'lerini (System Center VMM olmadan) tooAzure Azure Site Recovery ile çoğaltmak için aaaEnable çoğaltma | Microsoft Docs"
description: "Hyper-V sanal makineleri hello Azure Site Recovery hizmetini kullanarak için tooenable çoğaltma tooAzure gereken hello adımları özetler"
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
ms.openlocfilehash: 1589cb7aa1fe954e075cb7bf1f4a4ec199ed3ec7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-enable-replication-for-hyper-v-vms-replicating-tooazure"></a><span data-ttu-id="33dba-103">10. adım: Hyper-V sanal makinelerini tooAzure çoğaltmak için çoğaltmayı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="33dba-103">Step 10: Enable replication for Hyper-V VMs replicating tooAzure</span></span>


<span data-ttu-id="33dba-104">Bu makalede nasıl tooenable çoğaltma için Hyper-V sanal makineleri (System Center VMM tarafından yönetilmediğinden) şirket içi hello kullanarak tooAzure [Azure Site Recovery](site-recovery-overview.md) hello Azure portal hizmeti.</span><span class="sxs-lookup"><span data-stu-id="33dba-104">This article describes how tooenable replication for on-premises Hyper-V virtual machines (not managed by System Center VMM) tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="33dba-105">POST açıklamaları ve soruları hello altındaki bu makalenin veya hello [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="33dba-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>




## <a name="before-you-start"></a><span data-ttu-id="33dba-106">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="33dba-106">Before you start</span></span>

<span data-ttu-id="33dba-107">Başlamadan önce Azure kullanıcı hesabınızın gerekli hello sahip olduğundan emin olun [izinleri](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) yeni bir sanal makine tooAzure tooenable çoğaltması.</span><span class="sxs-lookup"><span data-stu-id="33dba-107">Before you start, ensure that your Azure user account has hello required [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replication of a new virtual machine tooAzure.</span></span>

## <a name="exclude-disks-from-replication"></a><span data-ttu-id="33dba-108">Diskleri çoğaltmanın dışında tutma</span><span class="sxs-lookup"><span data-stu-id="33dba-108">Exclude disks from replication</span></span>

<span data-ttu-id="33dba-109">Varsayılan olarak, bir makine üzerindeki tüm diskleri çoğaltılır.</span><span class="sxs-lookup"><span data-stu-id="33dba-109">By default all disks on a machine are replicated.</span></span> <span data-ttu-id="33dba-110">Diskleri çoğaltmanın dışında bırakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="33dba-110">You can exclude disks from replication.</span></span> <span data-ttu-id="33dba-111">Örneğin, geçici verileri ya da her zaman bir makine yeniledi veri tooreplicate disklerle istemeyebilirsiniz veya (örneğin pagefile.sys ya da SQL Server tempdb) uygulamasını yeniden başlatır.</span><span class="sxs-lookup"><span data-stu-id="33dba-111">For example you might not want tooreplicate disks with temporary data, or data that's refreshed each time a machine or application restarts (for example pagefile.sys or SQL Server tempdb).</span></span> [<span data-ttu-id="33dba-112">Daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="33dba-112">Learn more</span></span>](site-recovery-exclude-disk.md)


## <a name="replicate-vms"></a><span data-ttu-id="33dba-113">Vm'lerini çoğaltma</span><span class="sxs-lookup"><span data-stu-id="33dba-113">Replicate VMs</span></span>

<span data-ttu-id="33dba-114">VM'ler için çoğaltma gibi etkinleştirin:</span><span class="sxs-lookup"><span data-stu-id="33dba-114">Enable replication for VMs as follows:</span></span>          

1. <span data-ttu-id="33dba-115">Tıklatın **uygulama çoğaltma** > **kaynak**.</span><span class="sxs-lookup"><span data-stu-id="33dba-115">Click **Replicate application** > **Source**.</span></span> <span data-ttu-id="33dba-116">Çoğaltma hello için ilk kez ayarladıktan sonra tıklayabilirsiniz **+ Çoğalt** ilave makineler için tooenable çoğaltma.</span><span class="sxs-lookup"><span data-stu-id="33dba-116">After you've set up replication for hello first time, you can click **+Replicate** tooenable replication for additional machines.</span></span>

    ![Çoğaltmayı etkinleştirme](./media/hyper-v-site-walkthrough-enable-replication/enable-replication.png)
2. <span data-ttu-id="33dba-118">İçinde **kaynak**seçin hello Hyper-V sitesi.</span><span class="sxs-lookup"><span data-stu-id="33dba-118">In **Source**, select hello Hyper-V site.</span></span> <span data-ttu-id="33dba-119">Daha sonra, **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="33dba-119">Then click **OK**.</span></span>
3. <span data-ttu-id="33dba-120">İçinde **hedef**hello kasa abonelik seçin ve hello yük devretme sonrasında Azure (Klasik veya resource management) toouse istediğiniz yük devretme modeli.</span><span class="sxs-lookup"><span data-stu-id="33dba-120">In **Target**, select hello vault subscription, and hello failover model you want toouse in Azure (classic or resource management) after failover.</span></span>
4. <span data-ttu-id="33dba-121">Toouse istediğiniz hello depolama hesabını seçin.</span><span class="sxs-lookup"><span data-stu-id="33dba-121">Select hello storage account you want toouse.</span></span> <span data-ttu-id="33dba-122">Toouse istediğiniz bir hesabınız yoksa, şunları yapabilirsiniz [oluşturmak](#set-up-an-azure-storage-account).</span><span class="sxs-lookup"><span data-stu-id="33dba-122">If you don't have an account you want toouse, you can [create one](#set-up-an-azure-storage-account).</span></span> <span data-ttu-id="33dba-123">Daha sonra, **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="33dba-123">Then click **OK**.</span></span>
5. <span data-ttu-id="33dba-124">Yük devretme oluşturulduğunda select hello Azure ağ ve alt ağ toowhich Azure VM'ler bağlanır.</span><span class="sxs-lookup"><span data-stu-id="33dba-124">Select hello Azure network and subnet toowhich Azure VMs will connect when they're created failover.</span></span>

    - <span data-ttu-id="33dba-125">etkinleştirmeniz tooapply hello ağ ayarlarını tooall makineleri çoğaltma için seçin **seçili makineler için Şimdi Yapılandır**.</span><span class="sxs-lookup"><span data-stu-id="33dba-125">tooapply hello network settings tooall machines you enable for replication, select **Configure now for selected machines**.</span></span>
    - <span data-ttu-id="33dba-126">Seçin **daha sonra yapılandırma** tooselect hello makine başına Azure ağı.</span><span class="sxs-lookup"><span data-stu-id="33dba-126">Select **Configure later** tooselect hello Azure network per machine.</span></span>
    - <span data-ttu-id="33dba-127">Toouse istediğiniz ağ yoksa, şunları yapabilirsiniz [oluşturmak](#set-up-an-azure-network).</span><span class="sxs-lookup"><span data-stu-id="33dba-127">If you don't have a network you want toouse, you can [create one](#set-up-an-azure-network).</span></span> <span data-ttu-id="33dba-128">Bir alt ağ (varsa) seçin.</span><span class="sxs-lookup"><span data-stu-id="33dba-128">Select a subnet if applicable.</span></span> <span data-ttu-id="33dba-129">Daha sonra, **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="33dba-129">Then click **OK**.</span></span>

   ![Çoğaltmayı etkinleştirme](./media/hyper-v-site-walkthrough-enable-replication/enable-replication11.png)

6. <span data-ttu-id="33dba-131">İçinde **sanal makineleri** > **sanal makine Seç**, tıklatın ve tooreplicate istediğiniz her bir makine seçin.</span><span class="sxs-lookup"><span data-stu-id="33dba-131">In **Virtual Machines** > **Select virtual machines**, click and select each machine you want tooreplicate.</span></span> <span data-ttu-id="33dba-132">Yalnızca çoğaltmanın etkinleştirildiği makineleri seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="33dba-132">You can only select machines for which replication can be enabled.</span></span> <span data-ttu-id="33dba-133">Daha sonra, **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="33dba-133">Then click **OK**.</span></span>

    ![Çoğaltmayı etkinleştirme](./media/hyper-v-site-walkthrough-enable-replication/enable-replication5-for-exclude-disk.png)

7. <span data-ttu-id="33dba-135">İçinde **özellikleri** > **özelliklerini yapılandırma**, seçili hello VM'ler için hello işletim sistemini seçin ve işletim sistemi diski hello.</span><span class="sxs-lookup"><span data-stu-id="33dba-135">In **Properties** > **Configure properties**, select hello operating system for hello selected VMs, and hello OS disk.</span></span>
8. <span data-ttu-id="33dba-136">Bu hello Azure VM adı (hedef) uyumlu ile doğrulayın [Azure sanal makine gereksinimlerini](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="33dba-136">Verify that hello Azure VM name (target name) complies with [Azure virtual machine requirements](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>
9. <span data-ttu-id="33dba-137">Varsayılan olarak tüm hello diskleri hello VM, çoğaltma için seçilir.</span><span class="sxs-lookup"><span data-stu-id="33dba-137">By default all hello disks of hello VM are selected for replication.</span></span> <span data-ttu-id="33dba-138">Clear diskleri tooexclude bunları.</span><span class="sxs-lookup"><span data-stu-id="33dba-138">Clear disks tooexclude them.</span></span>
10. <span data-ttu-id="33dba-139">Tıklatın **Tamam** toosave değişiklikler.</span><span class="sxs-lookup"><span data-stu-id="33dba-139">Click **OK** toosave changes.</span></span> <span data-ttu-id="33dba-140">Daha sonra ek özellikleri ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="33dba-140">You can set additional properties later.</span></span>

    ![Çoğaltmayı etkinleştirme](./media/hyper-v-site-walkthrough-enable-replication/enable-replication6-with-exclude-disk.png)

11. <span data-ttu-id="33dba-142">İçinde **çoğaltma ayarları** > **çoğaltma ayarlarını yapılandırın**, istediğiniz tooapply hello VM'ler korumalı hello çoğaltma ilkesi seçin.</span><span class="sxs-lookup"><span data-stu-id="33dba-142">In **Replication settings** > **Configure replication settings**, select hello replication policy you want tooapply for hello protected VMs.</span></span> <span data-ttu-id="33dba-143">Daha sonra, **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="33dba-143">Then click **OK**.</span></span> <span data-ttu-id="33dba-144">Merhaba Çoğaltma İlkesi'nde değiştirebilirsiniz **çoğaltma ilkeleri** > ilke adı > **ayarlarını Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="33dba-144">You can modify hello replication policy in **Replication policies** > policy-name > **Edit Settings**.</span></span> <span data-ttu-id="33dba-145">Uyguladığınız değişiklikler, zaten çoğaltılmış olan makinelere ve yeni makinelere uygulanır.</span><span class="sxs-lookup"><span data-stu-id="33dba-145">Changes you apply will be used for machines that are already replicating, and new machines.</span></span>


   ![Çoğaltmayı etkinleştirme](./media/hyper-v-site-walkthrough-enable-replication/enable-replication7.png)

<span data-ttu-id="33dba-147">Merhaba ilerlemesini izleyebilirsiniz **korumayı etkinleştir** iş **işleri** > **Site Recovery işleri**.</span><span class="sxs-lookup"><span data-stu-id="33dba-147">You can track progress of hello **Enable Protection** job in **Jobs** > **Site Recovery jobs**.</span></span> <span data-ttu-id="33dba-148">Merhaba sonra **korumayı Sonlandır** iş çalıştırmaları hello makine yük devretme için hazır.</span><span class="sxs-lookup"><span data-stu-id="33dba-148">After hello **Finalize Protection** job runs hello machine is ready for failover.</span></span>


## <a name="next-steps"></a><span data-ttu-id="33dba-149">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="33dba-149">Next steps</span></span>


<span data-ttu-id="33dba-150">Çok Git[11. adım: yük devretme testi çalıştırma](hyper-v-site-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="33dba-150">Go too[Step 11: Run a test failover](hyper-v-site-walkthrough-test-failover.md)</span></span>
