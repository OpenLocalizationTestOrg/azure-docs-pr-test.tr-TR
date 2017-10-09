---
title: "Azure VM'ler tooanother Azure Site Recovery ile Azure bölgesi için aaaEnable çoğaltma | Microsoft Docs"
description: "Tooenable çoğaltma tooanother Azure bölgesi hello Azure Site Recovery hizmetini kullanan Azure VM'ler için gereken hello adımları özetler"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: a309644f-d36b-4188-bba7-ad45a2d9bede
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 8/01/2017
ms.author: raynew
ms.openlocfilehash: 2fa03db45a18ccb8b9f31ed05589be0dd6d5f031
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-enable-replication-for-azure-vms"></a><span data-ttu-id="8af7b-103">5. adım: Azure VM'ler için çoğaltma etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="8af7b-103">Step 5: Enable replication for Azure VMs</span></span>


<span data-ttu-id="8af7b-104">Ayarladıktan sonra bir [kurtarma Hizmetleri kasası](azure-to-azure-walkthrough-vault.md), bu makale tooenable çoğaltma sanal makineleri (VM'ler) tooanother Azure bölgesi kullanmak [Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8af7b-104">After setting up a [Recovery Services vault](azure-to-azure-walkthrough-vault.md), use this article tooenable replication of virtual machines (VMs), tooanother Azure region, with [Azure Site Recovery](site-recovery-overview.md).</span></span> <span data-ttu-id="8af7b-105">tooenable çoğaltma, kaynak ve hedef ayarlar, hello çoğaltma ilkesini doğrulamak ve tooreplicate istediğiniz sanal makineleri seçin.</span><span class="sxs-lookup"><span data-stu-id="8af7b-105">tooenable replication, you set up source and target settings, verify hello replication policy, and select VMs you want tooreplicate.</span></span>

- <span data-ttu-id="8af7b-106">Merhaba makale, Azure Vm'leriniz tamamladığınızda toohello ikincil Azure bölgesi çoğaltılması.</span><span class="sxs-lookup"><span data-stu-id="8af7b-106">When you finish hello article, your Azure VMs should be replicating toohello secondary Azure region.</span></span>
- <span data-ttu-id="8af7b-107">Bu makalenin hello altındaki tüm yorumlar gönderin ya da hello sorular sormak [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span><span class="sxs-lookup"><span data-stu-id="8af7b-107">Post any comments at hello bottom of this article, or ask questions in hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span></span>

>[!NOTE]
>
> <span data-ttu-id="8af7b-108">Azure VM çoğaltma şu anda önizlemede değil.</span><span class="sxs-lookup"><span data-stu-id="8af7b-108">Azure VM replication is currently in preview.</span></span>


## <a name="select-hello-source"></a><span data-ttu-id="8af7b-109">Merhaba kaynağını seçin</span><span class="sxs-lookup"><span data-stu-id="8af7b-109">Select hello source</span></span> 

1. <span data-ttu-id="8af7b-110">Kurtarma Hizmetleri kasalarının içinde hello kasa adına tıklayın > **+ Çoğalt**.</span><span class="sxs-lookup"><span data-stu-id="8af7b-110">In Recovery Services vaults, click hello vault name > **+Replicate**.</span></span>
2. <span data-ttu-id="8af7b-111">İçinde **kaynak**seçin **Azure - Önizleme**.</span><span class="sxs-lookup"><span data-stu-id="8af7b-111">In **Source**, select **Azure - PREVIEW**.</span></span>
2. <span data-ttu-id="8af7b-112">İçinde **kaynak konumu**seçin hello kaynak çalışmakta her yere Vm'lerinizi Azure bölgesi.</span><span class="sxs-lookup"><span data-stu-id="8af7b-112">In **Source location**, select hello source Azure region where your VMs are currently running.</span></span>
3. <span data-ttu-id="8af7b-113">Select hello **Azure sanal makine dağıtım modeli** VM'ler için: **Resource Manager** veya **Klasik**.</span><span class="sxs-lookup"><span data-stu-id="8af7b-113">Select hello **Azure virtual machine deployment model** for VMs: **Resource Manager** or **Classic**.</span></span>
4. <span data-ttu-id="8af7b-114">Select hello **kaynak kaynak grubu** Resource Manager VM'ler için veya **bulut hizmeti** Klasik VM'ler için.</span><span class="sxs-lookup"><span data-stu-id="8af7b-114">Select hello **Source resource group** for Resource Manager VMs, or **cloud service** for classic VMs.</span></span>
5. <span data-ttu-id="8af7b-115">Tıklatın **Tamam** toosave hello ayarları.</span><span class="sxs-lookup"><span data-stu-id="8af7b-115">Click **OK** toosave hello settings.</span></span>

    ![Merhaba kaynağı yapılandırın](./media/azure-to-azure-walkthrough-enable-replication/source.png)

## <a name="select-hello-vms"></a><span data-ttu-id="8af7b-117">Merhaba sanal makineleri seçin</span><span class="sxs-lookup"><span data-stu-id="8af7b-117">Select hello VMs</span></span>

<span data-ttu-id="8af7b-118">Site Recovery hello VM'ler hello abonelik ve kaynak grubu/bulut hizmeti ile ilişkili bir listesini alır.</span><span class="sxs-lookup"><span data-stu-id="8af7b-118">Site Recovery retrieves a list of hello VMs associated with hello subscription and resource group/cloud service.</span></span>

1. <span data-ttu-id="8af7b-119">İçinde **sanal makineleri**, tooreplicate istediğiniz hello sanal makineleri seçin.</span><span class="sxs-lookup"><span data-stu-id="8af7b-119">In **Virtual Machines**, select hello VMs you want tooreplicate.</span></span>
2. <span data-ttu-id="8af7b-120">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8af7b-120">Click **OK**.</span></span>

    ![Sanal makineleri seçin](./media/azure-to-azure-walkthrough-enable-replication/vms.png)


## <a name="configure-settings"></a><span data-ttu-id="8af7b-122">Ayarları yapılandırma</span><span class="sxs-lookup"><span data-stu-id="8af7b-122">Configure settings</span></span>

<span data-ttu-id="8af7b-123">Site Recovery (Merhaba Kaynak bölgesi ayarlarına dayanarak) hello hedef bölgesi için varsayılan ayarları sağlar ve hello Çoğaltma İlkesi:</span><span class="sxs-lookup"><span data-stu-id="8af7b-123">Site Recovery provisions default settings for hello target region (based on hello source region settings), and hello replication policy:</span></span>

   - <span data-ttu-id="8af7b-124">**Hedef konum**: hello hedef bölgesi olağanüstü durum kurtarma için toouse istiyor.</span><span class="sxs-lookup"><span data-stu-id="8af7b-124">**Target location**: hello target region you want toouse for disaster recovery.</span></span> <span data-ttu-id="8af7b-125">Merhaba hedef konumu hello Site Recovery kasası hello konumunu eşleştiğini öneririz.</span><span class="sxs-lookup"><span data-stu-id="8af7b-125">We recommend that hello target location matches hello location of hello Site Recovery vault.</span></span>
   - <span data-ttu-id="8af7b-126">**Hedef kaynak grubu**: kaynak grubu toowhich hello hedef bölgede Azure Vm'lerinin yük devretme sonrasında ait olur.</span><span class="sxs-lookup"><span data-stu-id="8af7b-126">**Target resource group**: Resource group toowhich Azure VMs in hello target region will belong after failover.</span></span> <span data-ttu-id="8af7b-127">Varsayılan olarak, Site Recovery "asr" soneki ile Merhaba hedef bölgede yeni bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8af7b-127">By default, Site Recovery creates a new resource group in hello target region with an "asr" suffix.</span></span> 
   - <span data-ttu-id="8af7b-128">**Hedef sanal ağ**: hello hangi Azure Vm'lerde içinde hedef bölgesi konumlandırılacağı yük devretme sonrasında hello ağ.</span><span class="sxs-lookup"><span data-stu-id="8af7b-128">**Target virtual network**: hello network in which Azure VMs in hello target region will be located after failover.</span></span> <span data-ttu-id="8af7b-129">Varsayılan olarak, Site Recovery, bir "asr" soneki ile Merhaba hedef bölgede yeni bir sanal ağ (ve alt ağlar) oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8af7b-129">By default, Site Recovery creates a new virtual network (and subnets) in hello target region with an "asr" suffix.</span></span> <span data-ttu-id="8af7b-130">Bu ağ eşlenen tooyour kaynak ağdır.</span><span class="sxs-lookup"><span data-stu-id="8af7b-130">This network is mapped tooyour source network.</span></span> <span data-ttu-id="8af7b-131">VM yük devretme sonrasında belirli bir IP adresi atayabilirsiniz, tooretain hello gerekiyorsa aynı IP adresi hello kaynak ve hedef konumların dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="8af7b-131">Note that you can assign a specific IP address after failover of a VM, if you need tooretain hello same IP address in hello source and target locations.</span></span> 
   - <span data-ttu-id="8af7b-132">**Önbellek depolama hesapları**: hello kaynak bölgede Site Recovery kullanan bir depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="8af7b-132">**Cache storage accounts**: Site Recovery uses a storage account in hello source region.</span></span> <span data-ttu-id="8af7b-133">Kaynak VM'ler üzerindeki değişiklikler önce çoğaltma toohello hedef konumu toothis hesabı gönderilir.</span><span class="sxs-lookup"><span data-stu-id="8af7b-133">Changes on source VMs are sent toothis account, before replication toohello target location.</span></span> 
   - <span data-ttu-id="8af7b-134">**Hedef depolama hesapları**: varsayılan olarak, Site Recovery yeni bir depolama hesabı hello hedef bölgesi toomirror hello kaynak VM depolama hesabı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8af7b-134">**Target storage accounts**: By default, Site Recovery creates a new storage account in hello target region, toomirror hello source VM storage account.</span></span>
   -  <span data-ttu-id="8af7b-135">**Hedef kullanılabilirlik kümeleri**: varsayılan olarak, Site Recovery hello "asr" soneki ile Merhaba hedef bölgede yeni bir kullanılabilirlik oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8af7b-135">**Target availability sets**: By default, Site Recovery creates a new availability set in hello target region, with hello "asr" suffix.</span></span> 
   - <span data-ttu-id="8af7b-136">**Çoğaltma İlkesi adı**: İlke adı.</span><span class="sxs-lookup"><span data-stu-id="8af7b-136">**Replication policy name**: Policy name.</span></span>
   - <span data-ttu-id="8af7b-137">**Kurtarma noktası bekletme**: varsayılan olarak Site Recovery kurtarma noktalarına 24 saat tutar.</span><span class="sxs-lookup"><span data-stu-id="8af7b-137">**Recovery point retention**: By default Site Recovery keeps recovery points for 24 hours.</span></span> <span data-ttu-id="8af7b-138">1 ila 72 saat arasında bir değer yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8af7b-138">You can configure a value between 1 and 72 hours.</span></span>
   - <span data-ttu-id="8af7b-139">**Uygulamayla tutarlı anlık görüntü sıklığı**: varsayılan olarak Site Recovery 4 saatte bir uygulamayla tutarlı anlık görüntü alır.</span><span class="sxs-lookup"><span data-stu-id="8af7b-139">**App-consistent snapshot frequency**: By default Site Recovery takes an app-consistent snapshot every 4 hours.</span></span> <span data-ttu-id="8af7b-140">1 ve 12 saat arasında herhangi bir değer yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8af7b-140">You can configure any value between 1 and 12 hours.</span></span> <span data-ttu-id="8af7b-141">Verileri sürekli olarak çoğaltılır:</span><span class="sxs-lookup"><span data-stu-id="8af7b-141">Data is replicated continuously:</span></span>
    - <span data-ttu-id="8af7b-142">Kilitlenme tutarlı kurtarma noktalarına tutarlı veri yazma-sırası oluşturduğunuzda korur.</span><span class="sxs-lookup"><span data-stu-id="8af7b-142">Crash-consistent recovery points maintain consistent data write-order when created.</span></span> <span data-ttu-id="8af7b-143">Bu tür bir kurtarma noktası, uygulamanızın veri tutarsızlıkları olmadan bir kilitlenme gelen tasarlanmış toorecover ise genellikle yeterli olur</span><span class="sxs-lookup"><span data-stu-id="8af7b-143">This type of recovery point is usually sufficient if your app is designed toorecover from a crash without data inconsistencies</span></span>
    - <span data-ttu-id="8af7b-144">Kilitlenme tutarlı kurtarma noktalarına birkaç dakikada üretilir.</span><span class="sxs-lookup"><span data-stu-id="8af7b-144">Crash-consistent recovery points are generated every few minutes.</span></span> <span data-ttu-id="8af7b-145">Bu kurtarma noktaları toofail kullanılarak üzerinden ve kurtarma Vm'leriniz bir kurtarma noktası hedefi (RPO) dakika hello sırasına sağlar.</span><span class="sxs-lookup"><span data-stu-id="8af7b-145">Using these recovery points toofail over and recover your VMs provides a Recovery Point Objective (RPO) in hello order of minutes.</span></span>
    - <span data-ttu-id="8af7b-146">Uygulamayla tutarlı kurtarma noktaları (içinde toplama toowrite sipariş tutarlılık) çalışan uygulamalar tüm işlemleri tamamlamak ve arabellekleri toodisk (uygulama sessiz moda) flush emin olun.</span><span class="sxs-lookup"><span data-stu-id="8af7b-146">App-consistent recovery points (in addition toowrite-order consistency) ensure that running apps complete all operations and flush buffers toodisk (application quiescing).</span></span> <span data-ttu-id="8af7b-147">SQL Server, Oracle ve Exchange gibi veritabanı uygulamaları için bu kurtarma noktalarını kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="8af7b-147">We recommend you use these recovery points for database apps such as SQL Server, Oracle, and Exchange.</span></span>
        
    ![Ayarları yapılandırma](./media/azure-to-azure-walkthrough-enable-replication/settings.png)


### <a name="modify-settings"></a><span data-ttu-id="8af7b-149">Ayarları değiştirme</span><span class="sxs-lookup"><span data-stu-id="8af7b-149">Modify settings</span></span>

<span data-ttu-id="8af7b-150">Toomodify hedef ve çoğaltma ilkesi ayarları istiyorsanız, aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="8af7b-150">If you want toomodify target and replication policy settings, do hello following:</span></span>

1. <span data-ttu-id="8af7b-151">tooview veya hedef ayarlarını değiştir, tıklatın **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="8af7b-151">tooview or modify target settings, click **Settings**.</span></span>
2. <span data-ttu-id="8af7b-152">toooverride hello varsayılan hedef ayarlar'ı **Özelleştir**.</span><span class="sxs-lookup"><span data-stu-id="8af7b-152">toooverride hello default target settings, click **Customize**.</span></span> <span data-ttu-id="8af7b-153">Hedef kaynak grubu, sanal ağ, kullanılabilirlik kümesi ve hedef depolama hesabı belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8af7b-153">You can specify a target resource group, virtual network, availability set, and target storage account.</span></span> <span data-ttu-id="8af7b-154">Sanal makineleri hello kaynak bölge kümesinde parçası ise yalnızca kullanılabilirlik kümeleri ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8af7b-154">You can only add availability sets if VMs are part of a set in hello source region.</span></span>

    ![Ayarları yapılandırma](./media/azure-to-azure-walkthrough-enable-replication/customize-target.png)

3. <span data-ttu-id="8af7b-156">Kurtarma noktaları ve uygulamayla tutarlı anlık görüntüler için toooverride çoğaltma ayarları **Özelleştir** sonraki çok**Çoğaltma İlkesi**.</span><span class="sxs-lookup"><span data-stu-id="8af7b-156">toooverride replication settings for recovery points and app-consistent snapshots, click **Customize** next too**Replication Policy**.</span></span>
 
    ![Ayarları yapılandırma](./media/azure-to-azure-walkthrough-enable-replication/customize-policy.png)

4. <span data-ttu-id="8af7b-158">toostart sağlama hello hedef kaynaklar,'ı **hedef kaynakları oluşturmak**.</span><span class="sxs-lookup"><span data-stu-id="8af7b-158">toostart provisioning hello target resources, click **Create target resources**.</span></span> <span data-ttu-id="8af7b-159">Sağlama veya bunu bir dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="8af7b-159">Provisioning takes a minute or so.</span></span> <span data-ttu-id="8af7b-160">Sağlama işlemi sırasında Hello dikey penceresini kapatmayın veya üzerinden toostart sahip olacaksınız.</span><span class="sxs-lookup"><span data-stu-id="8af7b-160">Don't close hello blade during provisioning, or you'll have toostart over.</span></span>




## <a name="enable-replication"></a><span data-ttu-id="8af7b-161">Çoğaltmayı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="8af7b-161">Enable replication</span></span>

1. <span data-ttu-id="8af7b-162">İçinde **ayarları**, tıklatın **çoğaltmasını etkinleştir**.</span><span class="sxs-lookup"><span data-stu-id="8af7b-162">In **Settings**, click **Enable replication**.</span></span> <span data-ttu-id="8af7b-163">Merhaba, seçili VM'ler ilk çoğaltmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="8af7b-163">This enables initial replication of hello VMs you selected.</span></span> <span data-ttu-id="8af7b-164">İlk çoğaltma durumu bazı zaman toorefresh alabilir.</span><span class="sxs-lookup"><span data-stu-id="8af7b-164">Initial replication status might take some time toorefresh.</span></span> <span data-ttu-id="8af7b-165">Tıklatın **yenileme** tooget hello son durumu.</span><span class="sxs-lookup"><span data-stu-id="8af7b-165">Click **Refresh** tooget hello latest status.</span></span>

2. <span data-ttu-id="8af7b-166">Merhaba ilerlemesini izleyebilirsiniz **korumayı etkinleştir** iş **ayarları** > **işleri** > **Site Recovery işleri**.</span><span class="sxs-lookup"><span data-stu-id="8af7b-166">You can track progress of hello **Enable protection** job in **Settings** > **Jobs** > **Site Recovery Jobs**.</span></span>

3. <span data-ttu-id="8af7b-167">İçinde **ayarları** > **çoğaltılan öğeler**, VM'lerin hello durumunu görüntüleyin ve ilk çoğaltma işleminin ilerleme durumunu hello.</span><span class="sxs-lookup"><span data-stu-id="8af7b-167">In **Settings** > **Replicated Items**, you can view hello status of VMs and hello initial replication progress.</span></span> <span data-ttu-id="8af7b-168">Merhaba VM toodrill ayarlarına farklı Kapat'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="8af7b-168">Click hello VM toodrill down into its settings.</span></span>



## <a name="next-steps"></a><span data-ttu-id="8af7b-169">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8af7b-169">Next steps</span></span>

<span data-ttu-id="8af7b-170">Çok Git[6. adım: yük devretme testi çalıştırma](azure-to-azure-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="8af7b-170">Go too[Step 6: Run a test failover](azure-to-azure-walkthrough-test-failover.md)</span></span>
