---
title: "Olağanüstü durum kurtarma gereksinimleri için Azure bölgeler arasında Azure Vm'lerini çoğaltma: Azure tooAzure | Microsoft Docs"
description: "Olağanüstü durum kurtarma gereksinimleri için hello Azure Site Recovery hizmeti ile Azure bölgeler (Azure-Azure) arasında tooreplicate Azure VM'ler gereken hello adımları özetler."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: dab98aa5-9c41-4475-b7dc-2e07ab1cfd18
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: raynew
ms.openlocfilehash: c4c425af260a9bcc3dd4dcc13da26109e20f03bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-azure-vms-between-regions-with-azure-site-recovery"></a><span data-ttu-id="efa9d-103">Azure Site Recovery ile bölgeler arasında Azure Vm'lerini çoğaltma</span><span class="sxs-lookup"><span data-stu-id="efa9d-103">Replicate Azure VMs between regions with Azure Site Recovery</span></span>

>[!NOTE]
>
> <span data-ttu-id="efa9d-104">Azure sanal makineleri (VM'ler) için Azure Site Recovery çoğaltma şu anda önizlemede değil.</span><span class="sxs-lookup"><span data-stu-id="efa9d-104">Azure Site Recovery replication for Azure virtual machines (VMs) is currently in preview.</span></span>

<span data-ttu-id="efa9d-105">Nasıl kullanarak Azure bölgeler arasında Azure VM'ler tooreplicate hello bu makalede [Site Recovery](site-recovery-overview.md) hello Azure portal hizmeti.</span><span class="sxs-lookup"><span data-stu-id="efa9d-105">This article describes how tooreplicate Azure VMs between Azure regions by using hello [Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="efa9d-106">POST açıklamaları ve soruları hello altındaki bu makalenin veya hello [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="efa9d-106">Post comments and questions at hello bottom of this article or on hello [Azure Recovery Services forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="disaster-recovery-in-azure"></a><span data-ttu-id="efa9d-107">Azure olağanüstü durum kurtarma</span><span class="sxs-lookup"><span data-stu-id="efa9d-107">Disaster recovery in Azure</span></span>

<span data-ttu-id="efa9d-108">Yerleşik Azure altyapı yetenekleri ve özellikleri Azure Vm'lerinde çalışan iş yüklerini tooa sağlam ve esnek kullanılabilir stratejiyi katkıda.</span><span class="sxs-lookup"><span data-stu-id="efa9d-108">Built-in Azure infrastructure capabilities and features contribute tooa robust and resilient availability strategy for workloads that run on Azure VMs.</span></span> <span data-ttu-id="efa9d-109">Ancak, birçok nedenden neden tooplan Azure bölgeler arasında olağanüstü durum kurtarma için kendiniz ihtiyacınız vardır:</span><span class="sxs-lookup"><span data-stu-id="efa9d-109">However, there are many reasons why you need tooplan for disaster recovery between Azure regions yourself:</span></span>

- <span data-ttu-id="efa9d-110">Belirli uygulamalar ve iş devamlılığı ve olağanüstü durum kurtarma (BCDR) stratejinize gerektiren iş yükleri için toomeet uyumluluk yönergelerine gerekir.</span><span class="sxs-lookup"><span data-stu-id="efa9d-110">You need toomeet compliance guidelines for specific apps and workloads that require a business continuity and disaster recovery (BCDR) strategy.</span></span>
- <span data-ttu-id="efa9d-111">Azure VM'ler, iş kararları göre ve değil yalnızca yerleşik Azure işlevselliğine bağlı kurtarmak ve hello özelliği tooprotect istiyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="efa9d-111">You want hello ability tooprotect and recover Azure VMs based on your business decisions, and not only based on inbuilt Azure functionality.</span></span>
- <span data-ttu-id="efa9d-112">Üretim üzerinde hiçbir etkisi olmadan, iş ve uyumluluk gereksinimlerinize uygun olarak tootest yük devretme ve kurtarma gerekir.</span><span class="sxs-lookup"><span data-stu-id="efa9d-112">You need tootest failover and recovery in accordance with your business and compliance needs, with no impact on production.</span></span>
- <span data-ttu-id="efa9d-113">Geri toohello özgün kaynak bölge sorunsuz bir şekilde başarısız ve hello olayı bir olağanüstü durum kurtarma bölgede toohello üzerinden toofail gerekir.</span><span class="sxs-lookup"><span data-stu-id="efa9d-113">You need toofail over toohello recovery region in hello event of a disaster and fail back toohello original source region seamlessly.</span></span>

<span data-ttu-id="efa9d-114">Site Recovery kullanan tüm bu görevleri gerçekleştirmek için Azure Azure VM çoğaltma toohelp.</span><span class="sxs-lookup"><span data-stu-id="efa9d-114">Use Site Recovery for Azure-to-Azure VM replication toohelp you do all these tasks.</span></span>


## <a name="why-use-site-recovery"></a><span data-ttu-id="efa9d-115">Neden Site Recovery kullanmalısınız?</span><span class="sxs-lookup"><span data-stu-id="efa9d-115">Why use Site Recovery?</span></span>      

<span data-ttu-id="efa9d-116">Site Recovery basit yol tooreplicate bölgeler arasında Azure VM'ler sunar:</span><span class="sxs-lookup"><span data-stu-id="efa9d-116">Site Recovery provides a simple way tooreplicate Azure VMs between regions:</span></span>

- <span data-ttu-id="efa9d-117">**Otomatik dağıtım**.</span><span class="sxs-lookup"><span data-stu-id="efa9d-117">**Automatic deployment**.</span></span> <span data-ttu-id="efa9d-118">Etkin-etkin çoğaltma modeli, ikincil bölge'hello pahalı ve karmaşık bir altyapıda için gerek yoktur.</span><span class="sxs-lookup"><span data-stu-id="efa9d-118">Unlike an active-active replication model, there's no need for an expensive and complex infrastructure in hello secondary region.</span></span> <span data-ttu-id="efa9d-119">Çoğaltmayı etkinleştirmek, Site Recovery otomatik olarak hello gerekli kaynakları hello hedef bölgede Kaynak bölgesi ayarlarınızı temel alan oluşturur.</span><span class="sxs-lookup"><span data-stu-id="efa9d-119">When you enable replication, Site Recovery automatically creates hello required resources in hello target region, based on source region settings.</span></span>
- <span data-ttu-id="efa9d-120">**Denetim bölgeleri**.</span><span class="sxs-lookup"><span data-stu-id="efa9d-120">**Control regions**.</span></span> <span data-ttu-id="efa9d-121">Site Recovery ile bir kıtada içinde hiçbir bölge tooany bölgesinden çoğaltabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="efa9d-121">With Site Recovery, you can replicate from any region tooany region within a continent.</span></span> <span data-ttu-id="efa9d-122">Bu standart arasında zaman uyumsuz olarak çoğaltır okuma erişimli coğrafi olarak yedekli depolama karşılaştırmak [eşleştirilmiş bölgeleri](https://docs.microsoft.com/azure/best-practices-availability-paired-regions) yalnızca.</span><span class="sxs-lookup"><span data-stu-id="efa9d-122">Compare this with read-access geo-redundant storage, which replicates asynchronously between standard [paired regions](https://docs.microsoft.com/azure/best-practices-availability-paired-regions) only.</span></span> <span data-ttu-id="efa9d-123">Coğrafi olarak yedekli depolamaya okuma erişimi hello hedef bölgede salt okunur erişim toohello verileri sağlar.</span><span class="sxs-lookup"><span data-stu-id="efa9d-123">Read-access geo-redundant storage provides read-only access toohello data in hello target region.</span></span>
- <span data-ttu-id="efa9d-124">**Çoğaltma otomatik**.</span><span class="sxs-lookup"><span data-stu-id="efa9d-124">**Automated replication**.</span></span> <span data-ttu-id="efa9d-125">Site Recovery otomatik sürekli çoğaltma sağlar.</span><span class="sxs-lookup"><span data-stu-id="efa9d-125">Site Recovery provides automated continuous replication.</span></span> <span data-ttu-id="efa9d-126">Yük devretme ve yeniden çalışma tek bir tıklatmayla tetiklenebilir.</span><span class="sxs-lookup"><span data-stu-id="efa9d-126">Failover and failback can be triggered with a single click.</span></span>
- <span data-ttu-id="efa9d-127">**RTO ve RPO**.</span><span class="sxs-lookup"><span data-stu-id="efa9d-127">**RTO and RPO**.</span></span> <span data-ttu-id="efa9d-128">Site Recovery bölgeleri tookeep bağlayan hello Azure ağ altyapısı avantajlarından yararlanır RTO ve RPO çok düşük.</span><span class="sxs-lookup"><span data-stu-id="efa9d-128">Site Recovery takes advantage of hello Azure network infrastructure that connects regions tookeep RTO and RPO very low.</span></span>
- <span data-ttu-id="efa9d-129">**Sınama**.</span><span class="sxs-lookup"><span data-stu-id="efa9d-129">**Testing**.</span></span> <span data-ttu-id="efa9d-130">Olağanüstü durum kurtarma ayrıntısına gerektiğinde, üretim iş yükleri veya devam eden çoğaltmayı etkilemeden gereken isteğe bağlı yük devretme testlerini çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="efa9d-130">You can run disaster-recovery drills with on-demand test failovers, as and when needed, without affecting your production workloads or ongoing replication.</span></span>
- <span data-ttu-id="efa9d-131">**Kurtarma planları**.</span><span class="sxs-lookup"><span data-stu-id="efa9d-131">**Recovery plans**.</span></span> <span data-ttu-id="efa9d-132">Kurtarma planları tooorchestrate yük devretme ve yeniden çalışma hello tüm uygulamanın birden çok VM'ler üzerinde çalıştırılan kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="efa9d-132">You can use recovery plans tooorchestrate failover and failback of hello entire application running on multiple VMs.</span></span> <span data-ttu-id="efa9d-133">Azure Otomasyonu runbook'ları ile zengin birinci sınıf tümleştirme Hello kurtarma planı özelliği vardır.</span><span class="sxs-lookup"><span data-stu-id="efa9d-133">hello recovery plan feature has rich first-class integration with Azure automation runbooks.</span></span>


## <a name="deployment-summary"></a><span data-ttu-id="efa9d-134">Dağıtım özeti</span><span class="sxs-lookup"><span data-stu-id="efa9d-134">Deployment summary</span></span>

<span data-ttu-id="efa9d-135">İhtiyacınız olan bir özeti aşağıda verilmiştir toodo tooset VM'ler çoğaltma Azure bölgeler arasında:</span><span class="sxs-lookup"><span data-stu-id="efa9d-135">Here's a summary of what you need toodo tooset up replication of VMs between Azure regions:</span></span>

1. <span data-ttu-id="efa9d-136">Kurtarma Hizmetleri kasası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="efa9d-136">Create a Recovery Services vault.</span></span> <span data-ttu-id="efa9d-137">Merhaba kasası yapılandırma ayarlarını içeren çoğaltma ve yönetir.</span><span class="sxs-lookup"><span data-stu-id="efa9d-137">hello vault contains configuration settings and orchestrates replication.</span></span>
2. <span data-ttu-id="efa9d-138">Hello Azure VM'ler çoğaltmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="efa9d-138">Enable replication for hello Azure VMs.</span></span>
3. <span data-ttu-id="efa9d-139">Her şeyin beklendiği gibi çalıştığından emin bir test yük devretme toomake çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="efa9d-139">Run a test failover toomake sure that everything's working as expected.</span></span>

>[!IMPORTANT]
>
> <span data-ttu-id="efa9d-140">Merhaba denetleyebilirsiniz [Azure VM çoğaltması için destek matrisi](./site-recovery-support-matrix-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="efa9d-140">You can check hello [support matrix for Azure VM replication](./site-recovery-support-matrix-azure-to-azure.md).</span></span>

>[!IMPORTANT]
>
> <span data-ttu-id="efa9d-141">Merhaba tooconfigure hello ağ giden bağlantı Azure VM'ler için Site Recovery çoğaltma için nasıl gereken hakkında daha fazla bilgi için bkz [Ağ Kılavuzu belge](./site-recovery-azure-to-azure-networking-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="efa9d-141">For information on how tooconfigure hello required network outbound connectivity for Azure VMs for Site Recovery replication, see hello [networking guidance document](./site-recovery-azure-to-azure-networking-guidance.md).</span></span>

### <a name="before-you-start"></a><span data-ttu-id="efa9d-142">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="efa9d-142">Before you start</span></span>

* <span data-ttu-id="efa9d-143">Azure kullanıcı hesabınızın toohave belirli gereken [izinleri](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) bir Azure sanal makinesinin tooenable çoğaltma.</span><span class="sxs-lookup"><span data-stu-id="efa9d-143">Your Azure user account needs toohave certain [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replication of an Azure virtual machine.</span></span>
* <span data-ttu-id="efa9d-144">Azure aboneliğinizde etkin toocreate VM'ler toouse hello olağanüstü durum kurtarma bölge olarak istediğiniz hello hedef konumda olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="efa9d-144">Your Azure subscription should be enabled toocreate VMs in hello target location that you want toouse as hello disaster recovery region.</span></span> <span data-ttu-id="efa9d-145">Desteğe başvurun tooenable hello gerekli kotası.</span><span class="sxs-lookup"><span data-stu-id="efa9d-145">Contact support tooenable hello required quota.</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="efa9d-146">Kurtarma Hizmetleri kasası oluşturma</span><span class="sxs-lookup"><span data-stu-id="efa9d-146">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

>[!NOTE]
>
> <span data-ttu-id="efa9d-147">Merhaba kurtarma Hizmetleri kasası, VM'ler tooreplicate istediğiniz hello konumda oluşturmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="efa9d-147">We recommend that you create hello Recovery Services vault in hello location where you want your VMs tooreplicate.</span></span> <span data-ttu-id="efa9d-148">Hedef konumunuz olan hello Orta BİZE, örneğin, hello kasasına oluşturun **Orta ABD**.</span><span class="sxs-lookup"><span data-stu-id="efa9d-148">For example, if your target location is hello central US, create hello vault in **Central US**.</span></span>

## <a name="enable-replication"></a><span data-ttu-id="efa9d-149">Çoğaltmayı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="efa9d-149">Enable replication</span></span>

<span data-ttu-id="efa9d-150">İçinde **kurtarma Hizmetleri kasaları**, hello kasa adını tıklatın.</span><span class="sxs-lookup"><span data-stu-id="efa9d-150">In **Recovery Services vaults**, click hello vault name.</span></span> <span data-ttu-id="efa9d-151">Merhaba Hello kasaya tıklayın **+ Çoğalt** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="efa9d-151">In hello vault, click hello **+Replicate** button.</span></span>

### <a name="step-1-configure-hello-source"></a><span data-ttu-id="efa9d-152">1. Adım</span><span class="sxs-lookup"><span data-stu-id="efa9d-152">Step 1.</span></span> <span data-ttu-id="efa9d-153">Merhaba kaynağı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="efa9d-153">Configure hello source</span></span>
1. <span data-ttu-id="efa9d-154">İçinde **kaynak**seçin **Azure - Önizleme**.</span><span class="sxs-lookup"><span data-stu-id="efa9d-154">In **Source**, select **Azure - PREVIEW**.</span></span>
2. <span data-ttu-id="efa9d-155">İçinde **kaynak konumu**seçin hello kaynak çalışmakta her yere Vm'lerinizi Azure bölgesi.</span><span class="sxs-lookup"><span data-stu-id="efa9d-155">In **Source location**, select hello source Azure region where your VMs are currently running.</span></span>
3. <span data-ttu-id="efa9d-156">Select hello dağıtım modeli, VM'lerin: **Resource Manager** veya **Klasik**.</span><span class="sxs-lookup"><span data-stu-id="efa9d-156">Select hello deployment model of your VMs: **Resource Manager** or **Classic**.</span></span>
4. <span data-ttu-id="efa9d-157">Select hello **kaynak kaynak grubu** Resource Manager VM'ler için veya **bulut hizmeti** Klasik VM'ler için.</span><span class="sxs-lookup"><span data-stu-id="efa9d-157">Select hello **Source resource group** for Resource Manager VMs or **cloud service** for classic VMs.</span></span>

    ![Merhaba kaynağı yapılandırın](./media/site-recovery-azure-to-azure/source.png)

### <a name="step-2-select-virtual-machines"></a><span data-ttu-id="efa9d-159">2. Adım</span><span class="sxs-lookup"><span data-stu-id="efa9d-159">Step 2.</span></span> <span data-ttu-id="efa9d-160">Sanal makineleri seçin</span><span class="sxs-lookup"><span data-stu-id="efa9d-160">Select virtual machines</span></span>

* <span data-ttu-id="efa9d-161">Tooreplicate istediğiniz ve ardından hello VM'ler seçin **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="efa9d-161">Select hello VMs you want tooreplicate, and then click **OK**.</span></span>

    ![Sanal makineleri seçin](./media/site-recovery-azure-to-azure/vms.png)

### <a name="step-3-configure-settings"></a><span data-ttu-id="efa9d-163">3. Adım</span><span class="sxs-lookup"><span data-stu-id="efa9d-163">Step 3.</span></span> <span data-ttu-id="efa9d-164">Ayarları yapılandırma</span><span class="sxs-lookup"><span data-stu-id="efa9d-164">Configure settings</span></span>

1. <span data-ttu-id="efa9d-165">toooverride hello varsayılan hedef ayarları ve hello ayarlarını belirtme, seçimine tıklayın **Özelleştir**.</span><span class="sxs-lookup"><span data-stu-id="efa9d-165">toooverride hello default target settings and specify hello settings of your choice, click **Customize**.</span></span> <span data-ttu-id="efa9d-166">Daha fazla bilgi için bkz: [hedef kaynakları özelleştirme](site-recovery-replicate-azure-to-azure.md##customize-target-resources).</span><span class="sxs-lookup"><span data-stu-id="efa9d-166">For more information, see [Customize target resources](site-recovery-replicate-azure-to-azure.md##customize-target-resources).</span></span>

    ![Ayarları yapılandırma](./media/site-recovery-azure-to-azure/settings.png)


2. <span data-ttu-id="efa9d-168">Varsayılan olarak, Site Recovery uygulamayla tutarlı anlık görüntüleri 4 saatte alır ve 24 saat için kurtarma noktalarını korur bir çoğaltma ilkesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="efa9d-168">By default, Site Recovery creates a replication policy that takes app-consistent snapshots every 4 hours and retains recovery points for 24 hours.</span></span> <span data-ttu-id="efa9d-169">toocreate farklı ayarlara sahip bir ilke tıklatın **Özelleştir** sonraki çok**Çoğaltma İlkesi**.</span><span class="sxs-lookup"><span data-stu-id="efa9d-169">toocreate a policy with different settings, click **Customize** next too**Replication Policy**.</span></span>

    ![İlke özelleştirme](./media/site-recovery-azure-to-azure/customize-policy.png)

3. <span data-ttu-id="efa9d-171">toostart sağlama hello hedef kaynaklar,'ı **hedef kaynakları oluşturmak**.</span><span class="sxs-lookup"><span data-stu-id="efa9d-171">toostart provisioning hello target resources, click **Create target resources**.</span></span> <span data-ttu-id="efa9d-172">Sağlama veya bunu bir dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="efa9d-172">Provisioning takes a minute or so.</span></span> <span data-ttu-id="efa9d-173">Sağlama işlemi sırasında Hello dikey penceresini kapatmayın veya üzerinden toostart gerek vardır.</span><span class="sxs-lookup"><span data-stu-id="efa9d-173">Don't close hello blade during provisioning, or you need toostart over.</span></span>

4. <span data-ttu-id="efa9d-174">Merhaba tootrigger çoğaltmasını seçili VM, tıklatın **çoğaltmasını etkinleştir**.</span><span class="sxs-lookup"><span data-stu-id="efa9d-174">tootrigger replication of hello selected VM, click **Enable replication**.</span></span>

5. <span data-ttu-id="efa9d-175">Merhaba ilerlemesini izleyebilirsiniz **korumayı etkinleştir** iş **ayarları** > **işleri** > **Site Recovery işleri**.</span><span class="sxs-lookup"><span data-stu-id="efa9d-175">You can track progress of hello **Enable protection** job in **Settings** > **Jobs** > **Site Recovery Jobs**.</span></span>

6. <span data-ttu-id="efa9d-176">İçinde **ayarları** > **çoğaltılan öğeler**, VM'lerin hello durumunu görüntüleyin ve ilk çoğaltma işleminin ilerleme durumunu hello.</span><span class="sxs-lookup"><span data-stu-id="efa9d-176">In **Settings** > **Replicated Items**, you can view hello status of VMs and hello initial replication progress.</span></span> <span data-ttu-id="efa9d-177">Merhaba VM toodrill ayarlarına farklı Kapat'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="efa9d-177">Click hello VM toodrill down into its settings.</span></span>

## <a name="run-a-test-failover"></a><span data-ttu-id="efa9d-178">Yük devretme testi çalıştırma</span><span class="sxs-lookup"><span data-stu-id="efa9d-178">Run a test failover</span></span>

<span data-ttu-id="efa9d-179">Her şeyi ayarladıktan sonra bir test yük devretme toomake her şeyin beklendiği gibi çalıştığından emin çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="efa9d-179">After you set up everything, run a test failover toomake sure everything's working as expected:</span></span>

1. <span data-ttu-id="efa9d-180">tek bir makineye üzerinden toofail içinde **ayarları** > **çoğaltılan öğeler**, hello VM tıklatın **+ yük devretme testi** simgesi.</span><span class="sxs-lookup"><span data-stu-id="efa9d-180">toofail over a single machine, in **Settings** > **Replicated Items**, click hello VM **+Test Failover** icon.</span></span>

2. <span data-ttu-id="efa9d-181">bir kurtarma üzerinden toofail planlama **ayarları** > **kurtarma planları**, sağ hello planı **yük devretme testi**.</span><span class="sxs-lookup"><span data-stu-id="efa9d-181">toofail over a recovery plan, in **Settings** > **Recovery Plans**, right-click hello plan **Test Failover**.</span></span> <span data-ttu-id="efa9d-182">bir kurtarma planı toocreate [bu yönergeleri izleyin](site-recovery-create-recovery-plans.md).</span><span class="sxs-lookup"><span data-stu-id="efa9d-182">toocreate a recovery plan, [follow these instructions](site-recovery-create-recovery-plans.md).</span></span> 

3. <span data-ttu-id="efa9d-183">İçinde **yük devretme testi**seçin hello hedef Azure sanal ağı toowhich Azure VM'ler hello yük devretme gerçekleştikten sonra bağlanır.</span><span class="sxs-lookup"><span data-stu-id="efa9d-183">In **Test Failover**, select hello target Azure virtual network toowhich Azure VMs are connected after hello failover occurs.</span></span>

4. <span data-ttu-id="efa9d-184">toostart yük devretme Merhaba, tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="efa9d-184">toostart hello failover, click **OK**.</span></span> <span data-ttu-id="efa9d-185">tootrack ilerleme, hello VM tooopen, Özellikler'i tıklatın.</span><span class="sxs-lookup"><span data-stu-id="efa9d-185">tootrack progress, click hello VM tooopen its properties.</span></span> <span data-ttu-id="efa9d-186">Veya hello tıklatabilirsiniz **yük devretme testi** hello kasa adı işinde > **ayarları** > **işleri** > **Site Recovery işleri**.</span><span class="sxs-lookup"><span data-stu-id="efa9d-186">Or you can click hello **Test Failover** job in hello vault name > **Settings** > **Jobs** > **Site Recovery jobs**.</span></span>

5. <span data-ttu-id="efa9d-187">Merhaba sonra Yük devretme, hello çoğaltma Azure makine hello Azure portalında görünür bittikten > **sanal makineleri**.</span><span class="sxs-lookup"><span data-stu-id="efa9d-187">After hello failover finishes, hello replica Azure machine appears in hello Azure portal > **Virtual Machines**.</span></span> <span data-ttu-id="efa9d-188">Bu hello VM toohello uygun ağ ve çalıştığını bağlı hello uygun boyutta olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="efa9d-188">Make sure that hello VM is hello appropriate size, that it's connected toohello appropriate network, and that it's running.</span></span>

6. <span data-ttu-id="efa9d-189">toodelete hello hello test yük devretmesi sırasında oluşturulan VM'ler tıklatın **temizleme yük devretme sınaması** öğesi veya hello kurtarma planı üzerinde hello yinelenmiş.</span><span class="sxs-lookup"><span data-stu-id="efa9d-189">toodelete hello VMs that were created during hello test failover, click **Cleanup test failover** on hello replicated item or hello recovery plan.</span></span> <span data-ttu-id="efa9d-190">İçinde **notları**hello yük devretme testiyle ilişkili gözlemlerinizi kaydetmek ve kaydedin.</span><span class="sxs-lookup"><span data-stu-id="efa9d-190">In **Notes**, record and save any observations associated with hello test failover.</span></span> 

<span data-ttu-id="efa9d-191">[Daha fazla bilgi edinin](site-recovery-test-failover-to-azure.md) yük devretme sınaması işlemlerini hakkında.</span><span class="sxs-lookup"><span data-stu-id="efa9d-191">[Learn more](site-recovery-test-failover-to-azure.md) about test failovers.</span></span>


## <a name="next-steps"></a><span data-ttu-id="efa9d-192">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="efa9d-192">Next steps</span></span>

<span data-ttu-id="efa9d-193">Sonra hello dağıtımı test etme:</span><span class="sxs-lookup"><span data-stu-id="efa9d-193">After you test hello deployment:</span></span>

- <span data-ttu-id="efa9d-194">[Daha fazla bilgi edinin](site-recovery-failover.md) yerine farklı türleri hakkında ve nasıl toorun bunları.</span><span class="sxs-lookup"><span data-stu-id="efa9d-194">[Learn more](site-recovery-failover.md) about different types of failovers and how toorun them.</span></span>
- <span data-ttu-id="efa9d-195">Daha fazla bilgi edinmek [kurtarma planlarına kullanarak](site-recovery-create-recovery-plans.md) tooreduce RTO.</span><span class="sxs-lookup"><span data-stu-id="efa9d-195">Learn more about [using recovery plans](site-recovery-create-recovery-plans.md) tooreduce RTO.</span></span>
