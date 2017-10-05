---
title: "Olağanüstü durum kurtarma gereksinimleri için Azure bölgeler arasında Azure Vm'lerini çoğaltma: Azure için Azure | Microsoft Docs"
description: "Olağanüstü durum kurtarma gereksinimleri için Azure Site Recovery hizmetiyle (Azure-Azure) Azure bölgeler arasında Azure sanal makineleri çoğaltmak için gereken adımları özetler."
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
ms.openlocfilehash: 9ca33057f6030fdcc233f6053fdc392d62f8f9f4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-azure-vms-between-regions-with-azure-site-recovery"></a><span data-ttu-id="3823a-103">Azure Site Recovery ile bölgeler arasında Azure Vm'lerini çoğaltma</span><span class="sxs-lookup"><span data-stu-id="3823a-103">Replicate Azure VMs between regions with Azure Site Recovery</span></span>

>[!NOTE]
>
> <span data-ttu-id="3823a-104">Azure sanal makineleri (VM'ler) için Azure Site Recovery çoğaltma şu anda önizlemede değil.</span><span class="sxs-lookup"><span data-stu-id="3823a-104">Azure Site Recovery replication for Azure virtual machines (VMs) is currently in preview.</span></span>

<span data-ttu-id="3823a-105">Bu makalede kullanarak Azure bölgeler arasında Azure Vm'lerini çoğaltma açıklar [Site Recovery](site-recovery-overview.md) Azure portalında hizmet.</span><span class="sxs-lookup"><span data-stu-id="3823a-105">This article describes how to replicate Azure VMs between Azure regions by using the [Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="3823a-106">Bu makalenin veya üzerinde altındaki açıklamaları ve soruları sonrası [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="3823a-106">Post comments and questions at the bottom of this article or on the [Azure Recovery Services forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="disaster-recovery-in-azure"></a><span data-ttu-id="3823a-107">Azure olağanüstü durum kurtarma</span><span class="sxs-lookup"><span data-stu-id="3823a-107">Disaster recovery in Azure</span></span>

<span data-ttu-id="3823a-108">Yerleşik Azure altyapı yetenekleri ve özellikleri Azure Vm'lerinde çalışan iş yüklerini için sağlam ve esnek kullanılabilirlik stratejisi katkıda bulunun.</span><span class="sxs-lookup"><span data-stu-id="3823a-108">Built-in Azure infrastructure capabilities and features contribute to a robust and resilient availability strategy for workloads that run on Azure VMs.</span></span> <span data-ttu-id="3823a-109">Ancak, Azure bölgeler arasında olağanüstü durum kurtarma için kendiniz planlama yapmanız neden pek çok nedeni vardır:</span><span class="sxs-lookup"><span data-stu-id="3823a-109">However, there are many reasons why you need to plan for disaster recovery between Azure regions yourself:</span></span>

- <span data-ttu-id="3823a-110">Belirli uygulamalar ve iş devamlılığı ve olağanüstü durum kurtarma (BCDR) stratejinize gerektiren iş yükleri için özel uyumluluk yönergelerine karşılaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="3823a-110">You need to meet compliance guidelines for specific apps and workloads that require a business continuity and disaster recovery (BCDR) strategy.</span></span>
- <span data-ttu-id="3823a-111">Koruma ve yerleşik Azure işlevselliğine bağlı Azure VM'ler, iş kararları göre ve değil yalnızca kurtarma olanağı istiyor.</span><span class="sxs-lookup"><span data-stu-id="3823a-111">You want the ability to protect and recover Azure VMs based on your business decisions, and not only based on inbuilt Azure functionality.</span></span>
- <span data-ttu-id="3823a-112">Yük devretme ve kurtarma üretim üzerinde hiçbir etkisi olmadan, iş ve uyumluluk gereksinimlerinize uygun olarak test etmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="3823a-112">You need to test failover and recovery in accordance with your business and compliance needs, with no impact on production.</span></span>
- <span data-ttu-id="3823a-113">Üzerinden bir olağanüstü durumda kurtarma bölgesine başarısız ve özgün kaynak bölge sorunsuz bir şekilde başarısız gerekir.</span><span class="sxs-lookup"><span data-stu-id="3823a-113">You need to fail over to the recovery region in the event of a disaster and fail back to the original source region seamlessly.</span></span>

<span data-ttu-id="3823a-114">Bu görevleri gerçekleştirmenize yardımcı olmak için Site Recovery Azure Azure VM çoğaltması için kullanın.</span><span class="sxs-lookup"><span data-stu-id="3823a-114">Use Site Recovery for Azure-to-Azure VM replication to help you do all these tasks.</span></span>


## <a name="why-use-site-recovery"></a><span data-ttu-id="3823a-115">Neden Site Recovery kullanmalısınız?</span><span class="sxs-lookup"><span data-stu-id="3823a-115">Why use Site Recovery?</span></span>      

<span data-ttu-id="3823a-116">Site Recovery bölgeler arasında Azure Vm'lerini çoğaltma için basit bir yol sunar:</span><span class="sxs-lookup"><span data-stu-id="3823a-116">Site Recovery provides a simple way to replicate Azure VMs between regions:</span></span>

- <span data-ttu-id="3823a-117">**Otomatik dağıtım**.</span><span class="sxs-lookup"><span data-stu-id="3823a-117">**Automatic deployment**.</span></span> <span data-ttu-id="3823a-118">Etkin-etkin çoğaltma modeli, ikincil bölge pahalı ve karmaşık bir altyapıda için gerek yoktur.</span><span class="sxs-lookup"><span data-stu-id="3823a-118">Unlike an active-active replication model, there's no need for an expensive and complex infrastructure in the secondary region.</span></span> <span data-ttu-id="3823a-119">Çoğaltmayı etkinleştirmek, Site Recovery otomatik olarak gerekli kaynakları hedef bölgede Kaynak bölgesi ayarlarınızı temel alan oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3823a-119">When you enable replication, Site Recovery automatically creates the required resources in the target region, based on source region settings.</span></span>
- <span data-ttu-id="3823a-120">**Denetim bölgeleri**.</span><span class="sxs-lookup"><span data-stu-id="3823a-120">**Control regions**.</span></span> <span data-ttu-id="3823a-121">Site Recovery ile bir kıtada içinde herhangi bir bölgeyi herhangi bölgesinden çoğaltabilir.</span><span class="sxs-lookup"><span data-stu-id="3823a-121">With Site Recovery, you can replicate from any region to any region within a continent.</span></span> <span data-ttu-id="3823a-122">Bu standart arasında zaman uyumsuz olarak çoğaltır okuma erişimli coğrafi olarak yedekli depolama karşılaştırmak [eşleştirilmiş bölgeleri](https://docs.microsoft.com/azure/best-practices-availability-paired-regions) yalnızca.</span><span class="sxs-lookup"><span data-stu-id="3823a-122">Compare this with read-access geo-redundant storage, which replicates asynchronously between standard [paired regions](https://docs.microsoft.com/azure/best-practices-availability-paired-regions) only.</span></span> <span data-ttu-id="3823a-123">Coğrafi olarak yedekli depolamaya okuma erişimi hedef bölgedeki veri salt okunur erişim sağlar.</span><span class="sxs-lookup"><span data-stu-id="3823a-123">Read-access geo-redundant storage provides read-only access to the data in the target region.</span></span>
- <span data-ttu-id="3823a-124">**Çoğaltma otomatik**.</span><span class="sxs-lookup"><span data-stu-id="3823a-124">**Automated replication**.</span></span> <span data-ttu-id="3823a-125">Site Recovery otomatik sürekli çoğaltma sağlar.</span><span class="sxs-lookup"><span data-stu-id="3823a-125">Site Recovery provides automated continuous replication.</span></span> <span data-ttu-id="3823a-126">Yük devretme ve yeniden çalışma tek bir tıklatmayla tetiklenebilir.</span><span class="sxs-lookup"><span data-stu-id="3823a-126">Failover and failback can be triggered with a single click.</span></span>
- <span data-ttu-id="3823a-127">**RTO ve RPO**.</span><span class="sxs-lookup"><span data-stu-id="3823a-127">**RTO and RPO**.</span></span> <span data-ttu-id="3823a-128">Site Recovery RTO ve RPO çok düşük tutmak için bölgeler bağlanan Azure ağ altyapısı yararlanır.</span><span class="sxs-lookup"><span data-stu-id="3823a-128">Site Recovery takes advantage of the Azure network infrastructure that connects regions to keep RTO and RPO very low.</span></span>
- <span data-ttu-id="3823a-129">**Sınama**.</span><span class="sxs-lookup"><span data-stu-id="3823a-129">**Testing**.</span></span> <span data-ttu-id="3823a-130">Olağanüstü durum kurtarma ayrıntısına gerektiğinde, üretim iş yükleri veya devam eden çoğaltmayı etkilemeden gereken isteğe bağlı yük devretme testlerini çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3823a-130">You can run disaster-recovery drills with on-demand test failovers, as and when needed, without affecting your production workloads or ongoing replication.</span></span>
- <span data-ttu-id="3823a-131">**Kurtarma planları**.</span><span class="sxs-lookup"><span data-stu-id="3823a-131">**Recovery plans**.</span></span> <span data-ttu-id="3823a-132">Kurtarma planları, yük devretme ve yeniden çalışma birden çok VM'ler üzerinde çalıştırılan tüm uygulamasının düzenlemek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3823a-132">You can use recovery plans to orchestrate failover and failback of the entire application running on multiple VMs.</span></span> <span data-ttu-id="3823a-133">Kurtarma planı Özelliği Azure Otomasyonu runbook'ları ile zengin birinci sınıf tümleştirme vardır.</span><span class="sxs-lookup"><span data-stu-id="3823a-133">The recovery plan feature has rich first-class integration with Azure automation runbooks.</span></span>


## <a name="deployment-summary"></a><span data-ttu-id="3823a-134">Dağıtım özeti</span><span class="sxs-lookup"><span data-stu-id="3823a-134">Deployment summary</span></span>

<span data-ttu-id="3823a-135">Sanal makineleri çoğaltma Azure bölgeler arasında ayarlamak için yapmanız gerekenler, bir özeti aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="3823a-135">Here's a summary of what you need to do to set up replication of VMs between Azure regions:</span></span>

1. <span data-ttu-id="3823a-136">Kurtarma Hizmetleri kasası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3823a-136">Create a Recovery Services vault.</span></span> <span data-ttu-id="3823a-137">Kasa yapılandırma ayarlarını içeren çoğaltma ve yönetir.</span><span class="sxs-lookup"><span data-stu-id="3823a-137">The vault contains configuration settings and orchestrates replication.</span></span>
2. <span data-ttu-id="3823a-138">Azure sanal makinelerini çoğaltmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="3823a-138">Enable replication for the Azure VMs.</span></span>
3. <span data-ttu-id="3823a-139">Her şeyin beklendiği gibi çalıştığından emin olmak için yük devretme testi çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="3823a-139">Run a test failover to make sure that everything's working as expected.</span></span>

>[!IMPORTANT]
>
> <span data-ttu-id="3823a-140">Kontrol edebilirsiniz [Azure VM çoğaltması için destek matrisi](./site-recovery-support-matrix-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="3823a-140">You can check the [support matrix for Azure VM replication](./site-recovery-support-matrix-azure-to-azure.md).</span></span>

>[!IMPORTANT]
>
> <span data-ttu-id="3823a-141">Site Recovery çoğaltma için Azure VM'ler için gerekli ağ giden bağlantı yapılandırma hakkında daha fazla bilgi için bkz: [Ağ Kılavuzu belge](./site-recovery-azure-to-azure-networking-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="3823a-141">For information on how to configure the required network outbound connectivity for Azure VMs for Site Recovery replication, see the [networking guidance document](./site-recovery-azure-to-azure-networking-guidance.md).</span></span>

### <a name="before-you-start"></a><span data-ttu-id="3823a-142">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="3823a-142">Before you start</span></span>

* <span data-ttu-id="3823a-143">Azure kullanıcı hesabınızın belirli sahip olması [izinleri](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) bir Azure sanal makinesi çoğaltmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="3823a-143">Your Azure user account needs to have certain [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) to enable replication of an Azure virtual machine.</span></span>
* <span data-ttu-id="3823a-144">Olağanüstü durum kurtarma bölge kullanmak istediğiniz hedef konumda VM'ler oluşturmak için Azure aboneliğinizin etkinleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="3823a-144">Your Azure subscription should be enabled to create VMs in the target location that you want to use as the disaster recovery region.</span></span> <span data-ttu-id="3823a-145">Gerekli Kotayı etkinleştirmek için desteğe başvurun.</span><span class="sxs-lookup"><span data-stu-id="3823a-145">Contact support to enable the required quota.</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="3823a-146">Kurtarma Hizmetleri kasası oluşturma</span><span class="sxs-lookup"><span data-stu-id="3823a-146">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

>[!NOTE]
>
> <span data-ttu-id="3823a-147">Kurtarma Hizmetleri kasası, sanal makineleri çoğaltmak istediğiniz konumda oluşturmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="3823a-147">We recommend that you create the Recovery Services vault in the location where you want your VMs to replicate.</span></span> <span data-ttu-id="3823a-148">Örneğin, hedef konumunuz Orta ise ABD, kasaya oluşturma **Orta ABD**.</span><span class="sxs-lookup"><span data-stu-id="3823a-148">For example, if your target location is the central US, create the vault in **Central US**.</span></span>

## <a name="enable-replication"></a><span data-ttu-id="3823a-149">Çoğaltmayı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="3823a-149">Enable replication</span></span>

<span data-ttu-id="3823a-150">İçinde **kurtarma Hizmetleri kasaları**, kasa adını tıklatın.</span><span class="sxs-lookup"><span data-stu-id="3823a-150">In **Recovery Services vaults**, click the vault name.</span></span> <span data-ttu-id="3823a-151">Kasaya tıklayın **+ Çoğalt** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="3823a-151">In the vault, click the **+Replicate** button.</span></span>

### <a name="step-1-configure-the-source"></a><span data-ttu-id="3823a-152">1. Adım</span><span class="sxs-lookup"><span data-stu-id="3823a-152">Step 1.</span></span> <span data-ttu-id="3823a-153">Kaynak yapılandırma</span><span class="sxs-lookup"><span data-stu-id="3823a-153">Configure the source</span></span>
1. <span data-ttu-id="3823a-154">İçinde **kaynak**seçin **Azure - Önizleme**.</span><span class="sxs-lookup"><span data-stu-id="3823a-154">In **Source**, select **Azure - PREVIEW**.</span></span>
2. <span data-ttu-id="3823a-155">İçinde **kaynak konumu**, çalışmakta her yere Vm'lerinizi Azure bölgesinde bir kaynak seçin.</span><span class="sxs-lookup"><span data-stu-id="3823a-155">In **Source location**, select the source Azure region where your VMs are currently running.</span></span>
3. <span data-ttu-id="3823a-156">Vm'leriniz dağıtım modelini seçin: **Resource Manager** veya **Klasik**.</span><span class="sxs-lookup"><span data-stu-id="3823a-156">Select the deployment model of your VMs: **Resource Manager** or **Classic**.</span></span>
4. <span data-ttu-id="3823a-157">Seçin **kaynak kaynak grubu** Resource Manager VM'ler için veya **bulut hizmeti** Klasik VM'ler için.</span><span class="sxs-lookup"><span data-stu-id="3823a-157">Select the **Source resource group** for Resource Manager VMs or **cloud service** for classic VMs.</span></span>

    ![Kaynak yapılandırma](./media/site-recovery-azure-to-azure/source.png)

### <a name="step-2-select-virtual-machines"></a><span data-ttu-id="3823a-159">2. Adım</span><span class="sxs-lookup"><span data-stu-id="3823a-159">Step 2.</span></span> <span data-ttu-id="3823a-160">Sanal makineleri seçin</span><span class="sxs-lookup"><span data-stu-id="3823a-160">Select virtual machines</span></span>

* <span data-ttu-id="3823a-161">Çoğaltma ve ardından istediğiniz sanal makineleri seçin **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="3823a-161">Select the VMs you want to replicate, and then click **OK**.</span></span>

    ![Sanal makineleri seçin](./media/site-recovery-azure-to-azure/vms.png)

### <a name="step-3-configure-settings"></a><span data-ttu-id="3823a-163">3. Adım</span><span class="sxs-lookup"><span data-stu-id="3823a-163">Step 3.</span></span> <span data-ttu-id="3823a-164">Ayarları yapılandırma</span><span class="sxs-lookup"><span data-stu-id="3823a-164">Configure settings</span></span>

1. <span data-ttu-id="3823a-165">Varsayılan hedef ayarları geçersiz kılar ve tercih ettiğiniz ayarları belirtmek için tıklatın **Özelleştir**.</span><span class="sxs-lookup"><span data-stu-id="3823a-165">To override the default target settings and specify the settings of your choice, click **Customize**.</span></span> <span data-ttu-id="3823a-166">Daha fazla bilgi için bkz: [hedef kaynakları özelleştirme](site-recovery-replicate-azure-to-azure.md##customize-target-resources).</span><span class="sxs-lookup"><span data-stu-id="3823a-166">For more information, see [Customize target resources](site-recovery-replicate-azure-to-azure.md##customize-target-resources).</span></span>

    ![Ayarları yapılandırma](./media/site-recovery-azure-to-azure/settings.png)


2. <span data-ttu-id="3823a-168">Varsayılan olarak, Site Recovery uygulamayla tutarlı anlık görüntüleri 4 saatte alır ve 24 saat için kurtarma noktalarını korur bir çoğaltma ilkesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3823a-168">By default, Site Recovery creates a replication policy that takes app-consistent snapshots every 4 hours and retains recovery points for 24 hours.</span></span> <span data-ttu-id="3823a-169">Farklı ayarlarla bir ilke oluşturmak için tıklatın **Özelleştir** yanına **Çoğaltma İlkesi**.</span><span class="sxs-lookup"><span data-stu-id="3823a-169">To create a policy with different settings, click **Customize** next to **Replication Policy**.</span></span>

    ![İlke özelleştirme](./media/site-recovery-azure-to-azure/customize-policy.png)

3. <span data-ttu-id="3823a-171">Hedef kaynakları hazırlamaya başlamak için tıklatın **hedef kaynakları oluşturmak**.</span><span class="sxs-lookup"><span data-stu-id="3823a-171">To start provisioning the target resources, click **Create target resources**.</span></span> <span data-ttu-id="3823a-172">Sağlama veya bunu bir dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="3823a-172">Provisioning takes a minute or so.</span></span> <span data-ttu-id="3823a-173">Sağlama işlemi sırasında dikey pencereyi kapatmayın veya baştan başlamanız gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="3823a-173">Don't close the blade during provisioning, or you need to start over.</span></span>

4. <span data-ttu-id="3823a-174">Seçilen VM çoğaltmasını tetiklemek için tıklatın **çoğaltmasını etkinleştir**.</span><span class="sxs-lookup"><span data-stu-id="3823a-174">To trigger replication of the selected VM, click **Enable replication**.</span></span>

5. <span data-ttu-id="3823a-175">İlerleme durumunu izleyebilirsiniz **korumayı etkinleştir** iş **ayarları** > **işleri** > **Site Recovery işleri**.</span><span class="sxs-lookup"><span data-stu-id="3823a-175">You can track progress of the **Enable protection** job in **Settings** > **Jobs** > **Site Recovery Jobs**.</span></span>

6. <span data-ttu-id="3823a-176">İçinde **ayarları** > **çoğaltılan öğeler**, VM'ler ve ilk çoğaltma ilerleme durumunu görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3823a-176">In **Settings** > **Replicated Items**, you can view the status of VMs and the initial replication progress.</span></span> <span data-ttu-id="3823a-177">VM ayarlarına detaya gitmek için tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3823a-177">Click the VM to drill down into its settings.</span></span>

## <a name="run-a-test-failover"></a><span data-ttu-id="3823a-178">Yük devretme testi çalıştırma</span><span class="sxs-lookup"><span data-stu-id="3823a-178">Run a test failover</span></span>

<span data-ttu-id="3823a-179">Her şeyi ayarladıktan sonra her şeyin beklendiği gibi çalıştığından emin olmak için yük devretme testi çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="3823a-179">After you set up everything, run a test failover to make sure everything's working as expected:</span></span>

1. <span data-ttu-id="3823a-180">İçinde tek bir makineye vermesine **ayarları** > **çoğaltılan öğeler**, VM tıklatın **+ yük devretme testi** simgesi.</span><span class="sxs-lookup"><span data-stu-id="3823a-180">To fail over a single machine, in **Settings** > **Replicated Items**, click the VM **+Test Failover** icon.</span></span>

2. <span data-ttu-id="3823a-181">Kurtarma planında yük devretme için **ayarları** > **kurtarma planları**, plana sağ **yük devretme testi**.</span><span class="sxs-lookup"><span data-stu-id="3823a-181">To fail over a recovery plan, in **Settings** > **Recovery Plans**, right-click the plan **Test Failover**.</span></span> <span data-ttu-id="3823a-182">Kurtarma planı oluşturmak için [aşağıdaki yönergeleri uygulayın](site-recovery-create-recovery-plans.md).</span><span class="sxs-lookup"><span data-stu-id="3823a-182">To create a recovery plan, [follow these instructions](site-recovery-create-recovery-plans.md).</span></span> 

3. <span data-ttu-id="3823a-183">İçinde **yük devretme testi**, hedef Azure sanal ağı seçin yük devretme gerçekleştikten sonra hangi Azure VM'ler bağlı.</span><span class="sxs-lookup"><span data-stu-id="3823a-183">In **Test Failover**, select the target Azure virtual network to which Azure VMs are connected after the failover occurs.</span></span>

4. <span data-ttu-id="3823a-184">Yük devretmeyi başlatmak için tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="3823a-184">To start the failover, click **OK**.</span></span> <span data-ttu-id="3823a-185">İlerleme durumunu izlemek için VM özelliklerini açmak için tıklatın.</span><span class="sxs-lookup"><span data-stu-id="3823a-185">To track progress, click the VM to open its properties.</span></span> <span data-ttu-id="3823a-186">Veya tıklatabilirsiniz **yük devretme testi** kasa adını işinde > **ayarları** > **işleri** > **Site Recovery işleri**.</span><span class="sxs-lookup"><span data-stu-id="3823a-186">Or you can click the **Test Failover** job in the vault name > **Settings** > **Jobs** > **Site Recovery jobs**.</span></span>

5. <span data-ttu-id="3823a-187">Yük devretme işlemi tamamlandıktan sonra Azure portalında Azure makine çoğaltma görünür > **sanal makineleri**.</span><span class="sxs-lookup"><span data-stu-id="3823a-187">After the failover finishes, the replica Azure machine appears in the Azure portal > **Virtual Machines**.</span></span> <span data-ttu-id="3823a-188">VM, uygun bir ağa bağlı olduğu uygun boyutta olduğundan ve çalıştığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="3823a-188">Make sure that the VM is the appropriate size, that it's connected to the appropriate network, and that it's running.</span></span>

6. <span data-ttu-id="3823a-189">Yük devretme testi sırasında oluşturulan sanal makineleri silmek için tıklatın **temizleme yük devretme testi** çoğaltılmış öğesi ya da kurtarma planı.</span><span class="sxs-lookup"><span data-stu-id="3823a-189">To delete the VMs that were created during the test failover, click **Cleanup test failover** on the replicated item or the recovery plan.</span></span> <span data-ttu-id="3823a-190">İçinde **notları**, kaydetme ve yük devretme testiyle ilişkili gözlemlerinizi kaydetmek.</span><span class="sxs-lookup"><span data-stu-id="3823a-190">In **Notes**, record and save any observations associated with the test failover.</span></span> 

<span data-ttu-id="3823a-191">[Daha fazla bilgi edinin](site-recovery-test-failover-to-azure.md) yük devretme sınaması işlemlerini hakkında.</span><span class="sxs-lookup"><span data-stu-id="3823a-191">[Learn more](site-recovery-test-failover-to-azure.md) about test failovers.</span></span>


## <a name="next-steps"></a><span data-ttu-id="3823a-192">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3823a-192">Next steps</span></span>

<span data-ttu-id="3823a-193">Sonra dağıtımı test etme:</span><span class="sxs-lookup"><span data-stu-id="3823a-193">After you test the deployment:</span></span>

- <span data-ttu-id="3823a-194">Farklı yük devretme türleri ve onları çalıştırma hakkında [daha fazla bilgi edinin](site-recovery-failover.md).</span><span class="sxs-lookup"><span data-stu-id="3823a-194">[Learn more](site-recovery-failover.md) about different types of failovers and how to run them.</span></span>
- <span data-ttu-id="3823a-195">Daha fazla bilgi edinmek [kurtarma planlarına kullanarak](site-recovery-create-recovery-plans.md) RTO azaltmak için.</span><span class="sxs-lookup"><span data-stu-id="3823a-195">Learn more about [using recovery plans](site-recovery-create-recovery-plans.md) to reduce RTO.</span></span>
