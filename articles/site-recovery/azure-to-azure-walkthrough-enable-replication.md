---
title: "Azure Site Recovery ile başka bir Azure bölgesine Azure VM'ler için çoğaltma etkinleştirme | Microsoft Docs"
description: "Azure Site Recovery hizmetini kullanan Azure VM'ler için başka bir Azure bölgesine çoğaltmayı etkinleştirmek için gereken adımları özetler"
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
ms.openlocfilehash: f426ba4341e61d3c7da820d7d5097b217e94ca0e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="step-5-enable-replication-for-azure-vms"></a><span data-ttu-id="1afe7-103">5. adım: Azure VM'ler için çoğaltma etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="1afe7-103">Step 5: Enable replication for Azure VMs</span></span>


<span data-ttu-id="1afe7-104">Ayarladıktan sonra bir [kurtarma Hizmetleri kasası](azure-to-azure-walkthrough-vault.md), başka bir Azure bölgesine, sanal makineleri (VM'ler), çoğaltılması etkinleştirmek için bu makaleyi kullanın [Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1afe7-104">After setting up a [Recovery Services vault](azure-to-azure-walkthrough-vault.md), use this article to enable replication of virtual machines (VMs), to another Azure region, with [Azure Site Recovery](site-recovery-overview.md).</span></span> <span data-ttu-id="1afe7-105">Çoğaltmayı etkinleştirmek için kaynak ve hedef ayarlarını yapın, çoğaltma ilkesini doğrulayın ve çoğaltmak istediğiniz sanal makineleri seçin.</span><span class="sxs-lookup"><span data-stu-id="1afe7-105">To enable replication, you set up source and target settings, verify the replication policy, and select VMs you want to replicate.</span></span>

- <span data-ttu-id="1afe7-106">Makale, Azure Vm'leriniz tamamladığınızda ikincil bir Azure bölgesine çoğaltılması.</span><span class="sxs-lookup"><span data-stu-id="1afe7-106">When you finish the article, your Azure VMs should be replicating to the secondary Azure region.</span></span>
- <span data-ttu-id="1afe7-107">Bu makalenin sonundaki yorumları gönderin ya da sorular sormak [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span><span class="sxs-lookup"><span data-stu-id="1afe7-107">Post any comments at the bottom of this article, or ask questions in the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span></span>

>[!NOTE]
>
> <span data-ttu-id="1afe7-108">Azure VM çoğaltma şu anda önizlemede değil.</span><span class="sxs-lookup"><span data-stu-id="1afe7-108">Azure VM replication is currently in preview.</span></span>


## <a name="select-the-source"></a><span data-ttu-id="1afe7-109">Bir kaynak seçin</span><span class="sxs-lookup"><span data-stu-id="1afe7-109">Select the source</span></span> 

1. <span data-ttu-id="1afe7-110">Kurtarma Hizmetleri kasalarının kasa adını tıklatın > **+ Çoğalt**.</span><span class="sxs-lookup"><span data-stu-id="1afe7-110">In Recovery Services vaults, click the vault name > **+Replicate**.</span></span>
2. <span data-ttu-id="1afe7-111">İçinde **kaynak**seçin **Azure - Önizleme**.</span><span class="sxs-lookup"><span data-stu-id="1afe7-111">In **Source**, select **Azure - PREVIEW**.</span></span>
2. <span data-ttu-id="1afe7-112">İçinde **kaynak konumu**, çalışmakta her yere Vm'lerinizi Azure bölgesinde bir kaynak seçin.</span><span class="sxs-lookup"><span data-stu-id="1afe7-112">In **Source location**, select the source Azure region where your VMs are currently running.</span></span>
3. <span data-ttu-id="1afe7-113">Seçin **Azure sanal makine dağıtım modeli** VM'ler için: **Resource Manager** veya **Klasik**.</span><span class="sxs-lookup"><span data-stu-id="1afe7-113">Select the **Azure virtual machine deployment model** for VMs: **Resource Manager** or **Classic**.</span></span>
4. <span data-ttu-id="1afe7-114">Seçin **kaynak kaynak grubu** Resource Manager VM'ler için veya **bulut hizmeti** Klasik VM'ler için.</span><span class="sxs-lookup"><span data-stu-id="1afe7-114">Select the **Source resource group** for Resource Manager VMs, or **cloud service** for classic VMs.</span></span>
5. <span data-ttu-id="1afe7-115">Ayarları kaydetmek için **Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1afe7-115">Click **OK** to save the settings.</span></span>

    ![Kaynak yapılandırma](./media/azure-to-azure-walkthrough-enable-replication/source.png)

## <a name="select-the-vms"></a><span data-ttu-id="1afe7-117">Sanal makineleri seçin</span><span class="sxs-lookup"><span data-stu-id="1afe7-117">Select the VMs</span></span>

<span data-ttu-id="1afe7-118">Site Recovery abonelik ve kaynak grubu/bulut hizmeti ile ilişkili sanal makinelerin listesini alır.</span><span class="sxs-lookup"><span data-stu-id="1afe7-118">Site Recovery retrieves a list of the VMs associated with the subscription and resource group/cloud service.</span></span>

1. <span data-ttu-id="1afe7-119">İçinde **sanal makineleri**, çoğaltmak istediğiniz sanal makineleri seçin.</span><span class="sxs-lookup"><span data-stu-id="1afe7-119">In **Virtual Machines**, select the VMs you want to replicate.</span></span>
2. <span data-ttu-id="1afe7-120">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1afe7-120">Click **OK**.</span></span>

    ![Sanal makineleri seçin](./media/azure-to-azure-walkthrough-enable-replication/vms.png)


## <a name="configure-settings"></a><span data-ttu-id="1afe7-122">Ayarları yapılandırma</span><span class="sxs-lookup"><span data-stu-id="1afe7-122">Configure settings</span></span>

<span data-ttu-id="1afe7-123">Varsayılan ayarlar (Kaynak bölgesi ayarlarına dayanarak) hedef bölgesi ve çoğaltma ilkesi için site kurtarma sağlar:</span><span class="sxs-lookup"><span data-stu-id="1afe7-123">Site Recovery provisions default settings for the target region (based on the source region settings), and the replication policy:</span></span>

   - <span data-ttu-id="1afe7-124">**Hedef konum**: olağanüstü durum kurtarma için kullanmak istediğiniz hedef bölgesi.</span><span class="sxs-lookup"><span data-stu-id="1afe7-124">**Target location**: The target region you want to use for disaster recovery.</span></span> <span data-ttu-id="1afe7-125">Hedef konumu Site Recovery kasası konumu eşleştiğini öneririz.</span><span class="sxs-lookup"><span data-stu-id="1afe7-125">We recommend that the target location matches the location of the Site Recovery vault.</span></span>
   - <span data-ttu-id="1afe7-126">**Hedef kaynak grubu**: hedef Azure vm'lerinin bölgeye ait olur yük devretme işleminden sonra kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="1afe7-126">**Target resource group**: Resource group to which Azure VMs in the target region will belong after failover.</span></span> <span data-ttu-id="1afe7-127">Varsayılan olarak, Site Recovery "asr" soneki ile hedef bölgede yeni bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1afe7-127">By default, Site Recovery creates a new resource group in the target region with an "asr" suffix.</span></span> 
   - <span data-ttu-id="1afe7-128">**Hedef sanal ağ**: hedef hangi Azure VM'de bölge konumlandırılacağı yük devretme sonrasında ağ.</span><span class="sxs-lookup"><span data-stu-id="1afe7-128">**Target virtual network**: The network in which Azure VMs in the target region will be located after failover.</span></span> <span data-ttu-id="1afe7-129">Varsayılan olarak, Site Recovery, bir "asr" soneki ile hedef bölgede yeni bir sanal ağ (ve alt ağlar) oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1afe7-129">By default, Site Recovery creates a new virtual network (and subnets) in the target region with an "asr" suffix.</span></span> <span data-ttu-id="1afe7-130">Bu ağ kaynağı ağınıza eşlenir.</span><span class="sxs-lookup"><span data-stu-id="1afe7-130">This network is mapped to your source network.</span></span> <span data-ttu-id="1afe7-131">Kaynak ve hedef konumları aynı IP adresi silmemeniz gerekiyorsa, bir VM yük devretme sonrasında belirli bir IP adresi atayabilirsiniz unutmayın.</span><span class="sxs-lookup"><span data-stu-id="1afe7-131">Note that you can assign a specific IP address after failover of a VM, if you need to retain the same IP address in the source and target locations.</span></span> 
   - <span data-ttu-id="1afe7-132">**Önbellek depolama hesapları**: kaynak bölgede Site Recovery kullanan bir depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="1afe7-132">**Cache storage accounts**: Site Recovery uses a storage account in the source region.</span></span> <span data-ttu-id="1afe7-133">Kaynak VM'ler üzerindeki değişiklikler çoğaltma hedef konumu için önce bu hesaba gönderilir.</span><span class="sxs-lookup"><span data-stu-id="1afe7-133">Changes on source VMs are sent to this account, before replication to the target location.</span></span> 
   - <span data-ttu-id="1afe7-134">**Hedef depolama hesapları**: varsayılan olarak, Site Recovery VM depolama hesabı kaynak yansıtmak üzere hedef bölgede yeni bir depolama hesabı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1afe7-134">**Target storage accounts**: By default, Site Recovery creates a new storage account in the target region, to mirror the source VM storage account.</span></span>
   -  <span data-ttu-id="1afe7-135">**Hedef kullanılabilirlik kümeleri**: varsayılan olarak, Site Recovery hedef bölgesindeki "asr" son ekini içeren yeni bir kullanılabilirlik oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1afe7-135">**Target availability sets**: By default, Site Recovery creates a new availability set in the target region, with the "asr" suffix.</span></span> 
   - <span data-ttu-id="1afe7-136">**Çoğaltma İlkesi adı**: İlke adı.</span><span class="sxs-lookup"><span data-stu-id="1afe7-136">**Replication policy name**: Policy name.</span></span>
   - <span data-ttu-id="1afe7-137">**Kurtarma noktası bekletme**: varsayılan olarak Site Recovery kurtarma noktalarına 24 saat tutar.</span><span class="sxs-lookup"><span data-stu-id="1afe7-137">**Recovery point retention**: By default Site Recovery keeps recovery points for 24 hours.</span></span> <span data-ttu-id="1afe7-138">1 ila 72 saat arasında bir değer yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1afe7-138">You can configure a value between 1 and 72 hours.</span></span>
   - <span data-ttu-id="1afe7-139">**Uygulamayla tutarlı anlık görüntü sıklığı**: varsayılan olarak Site Recovery 4 saatte bir uygulamayla tutarlı anlık görüntü alır.</span><span class="sxs-lookup"><span data-stu-id="1afe7-139">**App-consistent snapshot frequency**: By default Site Recovery takes an app-consistent snapshot every 4 hours.</span></span> <span data-ttu-id="1afe7-140">1 ve 12 saat arasında herhangi bir değer yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1afe7-140">You can configure any value between 1 and 12 hours.</span></span> <span data-ttu-id="1afe7-141">Verileri sürekli olarak çoğaltılır:</span><span class="sxs-lookup"><span data-stu-id="1afe7-141">Data is replicated continuously:</span></span>
    - <span data-ttu-id="1afe7-142">Kilitlenme tutarlı kurtarma noktalarına tutarlı veri yazma-sırası oluşturduğunuzda korur.</span><span class="sxs-lookup"><span data-stu-id="1afe7-142">Crash-consistent recovery points maintain consistent data write-order when created.</span></span> <span data-ttu-id="1afe7-143">Bu tür bir kurtarma noktası uygulamanızı çökmeyle veri tutarsızlıkları olmadan kurtarılır tasarlandıysa genellikle yeterli olur</span><span class="sxs-lookup"><span data-stu-id="1afe7-143">This type of recovery point is usually sufficient if your app is designed to recover from a crash without data inconsistencies</span></span>
    - <span data-ttu-id="1afe7-144">Kilitlenme tutarlı kurtarma noktalarına birkaç dakikada üretilir.</span><span class="sxs-lookup"><span data-stu-id="1afe7-144">Crash-consistent recovery points are generated every few minutes.</span></span> <span data-ttu-id="1afe7-145">Yük devri ve Vm'lerinizi kurtarmak için bu kurtarma noktalarını kullanarak bir kurtarma noktası hedefi (RPO) dakika sırasına göre sağlar.</span><span class="sxs-lookup"><span data-stu-id="1afe7-145">Using these recovery points to fail over and recover your VMs provides a Recovery Point Objective (RPO) in the order of minutes.</span></span>
    - <span data-ttu-id="1afe7-146">Uygulamayla tutarlı kurtarma noktaları (ek olarak yazma sipariş tutarlılık) çalışan uygulamalar tüm işlemleri tamamlamak ve arabellekler (uygulama sessiz moda) diske temizleme emin olun.</span><span class="sxs-lookup"><span data-stu-id="1afe7-146">App-consistent recovery points (in addition to write-order consistency) ensure that running apps complete all operations and flush buffers to disk (application quiescing).</span></span> <span data-ttu-id="1afe7-147">SQL Server, Oracle ve Exchange gibi veritabanı uygulamaları için bu kurtarma noktalarını kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="1afe7-147">We recommend you use these recovery points for database apps such as SQL Server, Oracle, and Exchange.</span></span>
        
    ![Ayarları yapılandırma](./media/azure-to-azure-walkthrough-enable-replication/settings.png)


### <a name="modify-settings"></a><span data-ttu-id="1afe7-149">Ayarları değiştirme</span><span class="sxs-lookup"><span data-stu-id="1afe7-149">Modify settings</span></span>

<span data-ttu-id="1afe7-150">Hedef ve çoğaltma ilkesi ayarlarını değiştirmek istiyorsanız aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="1afe7-150">If you want to modify target and replication policy settings, do the following:</span></span>

1. <span data-ttu-id="1afe7-151">Hedef ayarlarını görüntülemek veya değiştirmek için tıklatın **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="1afe7-151">To view or modify target settings, click **Settings**.</span></span>
2. <span data-ttu-id="1afe7-152">Varsayılan hedefi ayarlarını geçersiz kılmak için tıklatın **Özelleştir**.</span><span class="sxs-lookup"><span data-stu-id="1afe7-152">To override the default target settings, click **Customize**.</span></span> <span data-ttu-id="1afe7-153">Hedef kaynak grubu, sanal ağ, kullanılabilirlik kümesi ve hedef depolama hesabı belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1afe7-153">You can specify a target resource group, virtual network, availability set, and target storage account.</span></span> <span data-ttu-id="1afe7-154">Vm'leri kaynak bölge kümesinde parçası ise yalnızca kullanılabilirlik kümeleri ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1afe7-154">You can only add availability sets if VMs are part of a set in the source region.</span></span>

    ![Ayarları yapılandırma](./media/azure-to-azure-walkthrough-enable-replication/customize-target.png)

3. <span data-ttu-id="1afe7-156">Kurtarma noktaları ve uygulamayla tutarlı anlık görüntüler için çoğaltma ayarlarını geçersiz kılmak için tıklatın **Özelleştir** yanına **Çoğaltma İlkesi**.</span><span class="sxs-lookup"><span data-stu-id="1afe7-156">To override replication settings for recovery points and app-consistent snapshots, click **Customize** next to **Replication Policy**.</span></span>
 
    ![Ayarları yapılandırma](./media/azure-to-azure-walkthrough-enable-replication/customize-policy.png)

4. <span data-ttu-id="1afe7-158">Hedef kaynakları hazırlamaya başlamak için tıklatın **hedef kaynakları oluşturmak**.</span><span class="sxs-lookup"><span data-stu-id="1afe7-158">To start provisioning the target resources, click **Create target resources**.</span></span> <span data-ttu-id="1afe7-159">Sağlama veya bunu bir dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="1afe7-159">Provisioning takes a minute or so.</span></span> <span data-ttu-id="1afe7-160">Sağlama işlemi sırasında dikey pencereyi kapatmayın veya baştan başlamak zorunda kalırsınız.</span><span class="sxs-lookup"><span data-stu-id="1afe7-160">Don't close the blade during provisioning, or you'll have to start over.</span></span>




## <a name="enable-replication"></a><span data-ttu-id="1afe7-161">Çoğaltmayı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="1afe7-161">Enable replication</span></span>

1. <span data-ttu-id="1afe7-162">İçinde **ayarları**, tıklatın **çoğaltmasını etkinleştir**.</span><span class="sxs-lookup"><span data-stu-id="1afe7-162">In **Settings**, click **Enable replication**.</span></span> <span data-ttu-id="1afe7-163">Bu, seçili sanal makinelerin ilk çoğaltmasının sağlar.</span><span class="sxs-lookup"><span data-stu-id="1afe7-163">This enables initial replication of the VMs you selected.</span></span> <span data-ttu-id="1afe7-164">İlk çoğaltma durumunu yenilemek için biraz zaman alabilir.</span><span class="sxs-lookup"><span data-stu-id="1afe7-164">Initial replication status might take some time to refresh.</span></span> <span data-ttu-id="1afe7-165">Tıklatın **yenileme** en son durumunu almak için.</span><span class="sxs-lookup"><span data-stu-id="1afe7-165">Click **Refresh** to get the latest status.</span></span>

2. <span data-ttu-id="1afe7-166">İlerleme durumunu izleyebilirsiniz **korumayı etkinleştir** iş **ayarları** > **işleri** > **Site Recovery işleri**.</span><span class="sxs-lookup"><span data-stu-id="1afe7-166">You can track progress of the **Enable protection** job in **Settings** > **Jobs** > **Site Recovery Jobs**.</span></span>

3. <span data-ttu-id="1afe7-167">İçinde **ayarları** > **çoğaltılan öğeler**, VM'ler ve ilk çoğaltma ilerleme durumunu görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1afe7-167">In **Settings** > **Replicated Items**, you can view the status of VMs and the initial replication progress.</span></span> <span data-ttu-id="1afe7-168">VM ayarlarına detaya gitmek için tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1afe7-168">Click the VM to drill down into its settings.</span></span>



## <a name="next-steps"></a><span data-ttu-id="1afe7-169">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1afe7-169">Next steps</span></span>

<span data-ttu-id="1afe7-170">Git [6. adım: yük devretme testi çalıştırma](azure-to-azure-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="1afe7-170">Go to [Step 6: Run a test failover](azure-to-azure-walkthrough-test-failover.md)</span></span>
