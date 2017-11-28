---
title: "VMware Vm'leri tooAzure Azure Site Recovery ile çoğaltmak için aaaEnable çoğaltma | Microsoft Docs"
description: "Tooenable çoğaltma tooAzure hello Azure Site Recovery hizmetini kullanarak VMware Vm'leri için gereken hello adımları özetler"
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 519c5559-7032-4954-b8b5-f24f5242a954
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 490782bbbfa3dd92c626d3985c75d771df53d566
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="step-11-enable-replication-for-vmware-virtual-machines-tooazure"></a><span data-ttu-id="8205a-103">11. adım: VMware sanal makineleri tooAzure için çoğaltmayı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="8205a-103">Step 11: Enable replication for VMware virtual machines tooAzure</span></span>


<span data-ttu-id="8205a-104">Nasıl hello kullanarak tooAzure tooenable çoğaltma için şirket içi VMware sanal makineleri bu makalede [Azure Site Recovery](site-recovery-overview.md) hello Azure portal hizmeti.</span><span class="sxs-lookup"><span data-stu-id="8205a-104">This article describes how tooenable replication for on-premises VMware virtual machines tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="8205a-105">POST açıklamaları ve soruları hello altındaki bu makalenin veya hello [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="8205a-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="before-you-start"></a><span data-ttu-id="8205a-106">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="8205a-106">Before you start</span></span>

- <span data-ttu-id="8205a-107">VMware Vm'leri hello olmalıdır [Mobility hizmeti bileşeninin yüklü](vmware-walkthrough-install-mobility.md).</span><span class="sxs-lookup"><span data-stu-id="8205a-107">VMware VMs must have hello [Mobility service component installed](vmware-walkthrough-install-mobility.md).</span></span> <span data-ttu-id="8205a-108">-Bir VM gönderme yüklemesi için hazırlanmış, çoğaltma etkinleştirdiğinizde hello işlem sunucusu otomatik olarak hello Mobility hizmetini yükler.</span><span class="sxs-lookup"><span data-stu-id="8205a-108">- If a VM is prepared for push installation, hello process server automatically installs hello Mobility service when you enable replication.</span></span>
- <span data-ttu-id="8205a-109">Azure kullanıcı hesabınızın belirli gereken [izinleri](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) VM tooAzure tooenable çoğaltması</span><span class="sxs-lookup"><span data-stu-id="8205a-109">Your Azure user account needs specific [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replication of a VM tooAzure</span></span>
- <span data-ttu-id="8205a-110">Ekleyin veya VM'ler değiştirdiğinizde, too15 dakika veya daha uzun değişiklikler tootake etkisi ve bunları alabilir tooappear hello Portalı'nda.</span><span class="sxs-lookup"><span data-stu-id="8205a-110">When you add or modify VMs, it can take up too15 minutes or longer for changes tootake effect, and for them tooappear in hello portal.</span></span>
- <span data-ttu-id="8205a-111">VM için en son bulunan hello zaman denetimi **yapılandırma sunucularına** > **en son kişi**.</span><span class="sxs-lookup"><span data-stu-id="8205a-111">You can check hello last discovered time for VMs in **Configuration Servers** > **Last Contact At**.</span></span>
- <span data-ttu-id="8205a-112">Merhaba zamanlanmış bulma Vurgu hello yapılandırma sunucusu bekleyen olmadan VM'ler tooadd (tıklatın yok), tıklatıp **yenileme**.</span><span class="sxs-lookup"><span data-stu-id="8205a-112">tooadd VMs without waiting for hello scheduled discovery, highlight hello configuration server (don’t click it), and click **Refresh**.</span></span>



## <a name="exclude-disks-from-replication"></a><span data-ttu-id="8205a-113">Diskleri çoğaltmanın dışında tutma</span><span class="sxs-lookup"><span data-stu-id="8205a-113">Exclude disks from replication</span></span>

<span data-ttu-id="8205a-114">Varsayılan olarak, bir makine üzerindeki tüm diskleri çoğaltılır.</span><span class="sxs-lookup"><span data-stu-id="8205a-114">By default all disks on a machine are replicated.</span></span> <span data-ttu-id="8205a-115">Diskleri çoğaltmanın dışında bırakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8205a-115">You can exclude disks from replication.</span></span> <span data-ttu-id="8205a-116">Örneğin, geçici verileri ya da her zaman bir makine yeniledi veri tooreplicate disklerle istemeyebilirsiniz veya (örneğin pagefile.sys ya da SQL Server tempdb) uygulamasını yeniden başlatır.</span><span class="sxs-lookup"><span data-stu-id="8205a-116">For example you might not want tooreplicate disks with temporary data, or data that's refreshed each time a machine or application restarts (for example pagefile.sys or SQL Server tempdb).</span></span> [<span data-ttu-id="8205a-117">Daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="8205a-117">Learn more</span></span>](site-recovery-exclude-disk.md)

## <a name="replicate-vms"></a><span data-ttu-id="8205a-118">Vm'lerini çoğaltma</span><span class="sxs-lookup"><span data-stu-id="8205a-118">Replicate VMs</span></span>

<span data-ttu-id="8205a-119">Başlamadan önce hızlı bir video genel bakış izleyin</span><span class="sxs-lookup"><span data-stu-id="8205a-119">Before you start, watch a quick video overview</span></span>

>[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video3-Protect-VMware-Virtual-Machines/player]

1. <span data-ttu-id="8205a-120">**2. Adım: Uygulama çoğaltma** > **Kaynak** seçeneklerine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8205a-120">Click **Step 2: Replicate application** > **Source**.</span></span>
2. <span data-ttu-id="8205a-121">İçinde **kaynak**seçin hello yapılandırma sunucusu.</span><span class="sxs-lookup"><span data-stu-id="8205a-121">In **Source**, select hello configuration server.</span></span>
3. <span data-ttu-id="8205a-122">İçinde **makine türü**seçin **sanal makineleri**.</span><span class="sxs-lookup"><span data-stu-id="8205a-122">In **Machine type**, select **Virtual Machines**.</span></span>
4. <span data-ttu-id="8205a-123">İçinde **vCenter/vSphere hiper yönetici**hello vSphere ana yöneten hello vCenter sunucusu seçin veya hello konak seçin.</span><span class="sxs-lookup"><span data-stu-id="8205a-123">In **vCenter/vSphere Hypervisor**, select hello vCenter server that manages hello vSphere host, or select hello host.</span></span>
5. <span data-ttu-id="8205a-124">Merhaba işlem sunucusunu seçin.</span><span class="sxs-lookup"><span data-stu-id="8205a-124">Select hello process server.</span></span> <span data-ttu-id="8205a-125">Herhangi bir ek işlem sunucusu oluşturmadıysanız bu hello yapılandırma sunucusu olacaktır.</span><span class="sxs-lookup"><span data-stu-id="8205a-125">If you haven't created any additional process servers this will be hello configuration server.</span></span> <span data-ttu-id="8205a-126">Daha sonra, **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8205a-126">Then click **OK**.</span></span>

    ![Çoğaltmayı etkinleştirme](./media/vmware-walkthrough-enable-replication/enable-replication2.png)

6. <span data-ttu-id="8205a-128">İçinde **hedef**hello aboneliği seçin ve hello vm'lerinde toocreate hello istediğiniz kaynak grubunu.</span><span class="sxs-lookup"><span data-stu-id="8205a-128">In **Target**, select hello subscription and hello resource group in which you want toocreate hello failed over VMs.</span></span> <span data-ttu-id="8205a-129">Toouse (Yönetim), Klasik veya resource azure'da hello vm'lerinde için istediğiniz hello dağıtım modelini seçin.</span><span class="sxs-lookup"><span data-stu-id="8205a-129">Choose hello deployment model that you want toouse in Azure (classic or resource management), for hello failed over VMs.</span></span>


7. <span data-ttu-id="8205a-130">Veri çoğaltmak için toouse istediğiniz hello Azure depolama hesabı seçin.</span><span class="sxs-lookup"><span data-stu-id="8205a-130">Select hello Azure storage account you want toouse for replicating data.</span></span> <span data-ttu-id="8205a-131">Toouse ayarlamış bir hesap istemiyorsanız, yeni bir tane oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8205a-131">If you don't want toouse an account you've already set up, you can create a new one.</span></span>

8. <span data-ttu-id="8205a-132">Yük devretme sonrasında oluşturulduğunda select hello Azure ağ ve alt ağ toowhich Azure VM'ler bağlanır.</span><span class="sxs-lookup"><span data-stu-id="8205a-132">Select hello Azure network and subnet toowhich Azure VMs will connect, when they're created after failover.</span></span> <span data-ttu-id="8205a-133">Seçin **seçili makineler için Şimdi Yapılandır**, seçtiğiniz tooapply hello ağ ayarı tooall makineler için koruma.</span><span class="sxs-lookup"><span data-stu-id="8205a-133">Select **Configure now for selected machines**, tooapply hello network setting tooall machines you select for protection.</span></span> <span data-ttu-id="8205a-134">Seçin **daha sonra yapılandırma** tooselect hello makine başına Azure ağı.</span><span class="sxs-lookup"><span data-stu-id="8205a-134">Select **Configure later** tooselect hello Azure network per machine.</span></span> <span data-ttu-id="8205a-135">Varolan bir ağ toouse istemiyorsanız, bir tane oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8205a-135">If you don't want toouse an existing network, you can create one.</span></span>

    ![Çoğaltmayı etkinleştirme](./media/vmware-walkthrough-enable-replication/enable-rep3.png)
9. <span data-ttu-id="8205a-137">İçinde **sanal makineleri** > **sanal makine Seç**, tıklatın ve tooreplicate istediğiniz her bir makine seçin.</span><span class="sxs-lookup"><span data-stu-id="8205a-137">In **Virtual Machines** > **Select virtual machines**, click and select each machine you want tooreplicate.</span></span> <span data-ttu-id="8205a-138">Yalnızca çoğaltmanın etkinleştirildiği makineleri seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8205a-138">You can only select machines for which replication can be enabled.</span></span> <span data-ttu-id="8205a-139">Daha sonra, **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8205a-139">Then click **OK**.</span></span>

    ![Çoğaltmayı etkinleştirme](./media/vmware-walkthrough-enable-replication/enable-replication5.png)
10. <span data-ttu-id="8205a-141">İçinde **özellikleri** > **özelliklerini yapılandırmak**seçin hello işlem sunucusu tooautomatically tarafından kullanılacak hello hesap hello makinede hello Mobility hizmeti yükleyin.</span><span class="sxs-lookup"><span data-stu-id="8205a-141">In **Properties** > **Configure properties**, select hello account that will be used by hello process server tooautomatically install hello Mobility service on hello machine.</span></span>
11. <span data-ttu-id="8205a-142">Varsayılan olarak tüm diskler çoğaltılır.</span><span class="sxs-lookup"><span data-stu-id="8205a-142">By default all disks are replicated.</span></span> <span data-ttu-id="8205a-143">Tıklatın **tüm diskleri** ve tooreplicate istemediğiniz tüm diskleri temizleyin.</span><span class="sxs-lookup"><span data-stu-id="8205a-143">Click **All Disks** and clear any disks you don't want tooreplicate.</span></span> <span data-ttu-id="8205a-144">Daha sonra, **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8205a-144">Then click **OK**.</span></span> <span data-ttu-id="8205a-145">Ek VM özellikleri daha sonra ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8205a-145">You can set additional VM properties later.</span></span>

    ![Çoğaltmayı etkinleştirme](./media/vmware-walkthrough-enable-replication/enable-replication6.png)
11. <span data-ttu-id="8205a-147">İçinde **çoğaltma ayarları** > **çoğaltma ayarlarını yapılandırın**, o hello çoğaltma ilkesi seçili doğru doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="8205a-147">In **Replication settings** > **Configure replication settings**, verify that hello correct replication policy is selected.</span></span> <span data-ttu-id="8205a-148">Bir ilkeyi değiştirirseniz, değişiklikler uygulanan tooreplicating makine ve toonew makineleri olacaktır.</span><span class="sxs-lookup"><span data-stu-id="8205a-148">If you modify a policy, changes will be applied tooreplicating machine, and toonew machines.</span></span>
12. <span data-ttu-id="8205a-149">Etkinleştirme **çoklu VM tutarlılığını** toogather makineler çoğaltma grubuna isterseniz ve hello grubu için bir ad belirtin.</span><span class="sxs-lookup"><span data-stu-id="8205a-149">Enable **Multi-VM consistency** if you want toogather machines into a replication group, and specify a name for hello group.</span></span> <span data-ttu-id="8205a-150">Daha sonra, **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8205a-150">Then click **OK**.</span></span> <span data-ttu-id="8205a-151">Şunlara dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="8205a-151">Note that:</span></span>

    * <span data-ttu-id="8205a-152">Çoğaltma gruplarındaki makineler birlikte çoğaltılır ve kilitlenme tutarlı ve uygulamayla tutarlı kurtarma noktaları üzerinden başarısız olduğunda paylaşılan.</span><span class="sxs-lookup"><span data-stu-id="8205a-152">Machines in replication groups replicate together, and have shared crash-consistent and app-consistent recovery points when they fail over.</span></span>
    * <span data-ttu-id="8205a-153">Böylece, iş yüklerini yansıtma sanal makineleri ve fiziksel sunucuları araya toplamak öneririz.</span><span class="sxs-lookup"><span data-stu-id="8205a-153">We recommend that you gather VMs and physical servers together so that they mirror your workloads.</span></span> <span data-ttu-id="8205a-154">Çoklu VM tutarlılığını etkinleştirmek iş yükü performansını etkileyebilir ve yalnızca makineler hello çalışıyorsa kullanılmalıdır aynı iş yükünü ve tutarlılık gerekir.</span><span class="sxs-lookup"><span data-stu-id="8205a-154">Enabling multi-VM consistency can impact workload performance, and should only be used if machines are running hello same workload and you need consistency.</span></span>

    ![Çoğaltmayı etkinleştirme](./media/vmware-walkthrough-enable-replication/enable-replication7.png)
13. <span data-ttu-id="8205a-156">Tıklatın **çoğaltmasını etkinleştir**.</span><span class="sxs-lookup"><span data-stu-id="8205a-156">Click **Enable Replication**.</span></span> <span data-ttu-id="8205a-157">Merhaba ilerlemesini izleyebilirsiniz **korumayı etkinleştir** iş **ayarları** > **işleri** > **Site Recovery işleri**.</span><span class="sxs-lookup"><span data-stu-id="8205a-157">You can track progress of hello **Enable Protection** job in **Settings** > **Jobs** > **Site Recovery Jobs**.</span></span> <span data-ttu-id="8205a-158">Merhaba sonra **korumayı Sonlandır** iş çalıştırmaları hello makine yük devretme için hazır.</span><span class="sxs-lookup"><span data-stu-id="8205a-158">After hello **Finalize Protection** job runs hello machine is ready for failover.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8205a-159">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8205a-159">Next steps</span></span>

<span data-ttu-id="8205a-160">Çok Git[adım 12: yük devretme testi çalıştırma](vmware-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="8205a-160">Go too[Step 12: Run a test failover](vmware-walkthrough-test-failover.md)</span></span>
