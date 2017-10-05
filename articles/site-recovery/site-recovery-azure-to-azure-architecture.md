---
title: "Azure sanal makine çoğaltmasını Azure bölgeler arasında Azure Site Recovery nasıl çalışır?  | Microsoft Belgeleri"
description: "Bu makalede, bileşenleri ve Azure Site Recovery hizmetini kullanarak Azure bölgeler arasında Azure sanal makineleri çoğaltırken kullanılan mimariye genel bakış sağlar."
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/29/2017
ms.author: sujayt
ms.openlocfilehash: ec397eaeda963f257d1bd996f1f57189bcde17ca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-does-azure-vm-replication-work-in-site-recovery"></a><span data-ttu-id="d10b8-104">Azure VM çoğaltma Site Recovery nasıl çalışır?</span><span class="sxs-lookup"><span data-stu-id="d10b8-104">How does Azure VM replication work in Site Recovery?</span></span>


<span data-ttu-id="d10b8-105">Bu makalede bileşenleri ve işlemler çoğaltma ve Azure sanal makinelerini (VM'ler) Kurtarma bir bölgesinden diğerine kullanarak söz konusu [Azure Site Recovery](site-recovery-overview.md) hizmet.</span><span class="sxs-lookup"><span data-stu-id="d10b8-105">This article describes the components and processes involved in replicating and recovering Azure virtual machines (VMs) from one region to another by using the [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

>[!NOTE]
><span data-ttu-id="d10b8-106">Site Recovery hizmeti ile Azure VM çoğaltma şu anda önizlemede değil.</span><span class="sxs-lookup"><span data-stu-id="d10b8-106">Azure VM replication with the Site Recovery service is currently in preview.</span></span>

<span data-ttu-id="d10b8-107">Tüm yorumlarınızı bu makalenin alt kısmında paylaşabilir veya [Azure Kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)'nda soru sorabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d10b8-107">Post any comments at the bottom of this article, or ask questions in the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="architectural-components"></a><span data-ttu-id="d10b8-108">Mimari bileşenler</span><span class="sxs-lookup"><span data-stu-id="d10b8-108">Architectural components</span></span>

<span data-ttu-id="d10b8-109">Aşağıdaki diyagramda (Bu örnekte, Doğu ABD konumunda) belirli bir bölgede bir Azure VM ortamına üst düzey bir görünümünü sağlar.</span><span class="sxs-lookup"><span data-stu-id="d10b8-109">The following diagram provides a high-level view of an Azure VM environment in a specific region (in this example, the East US location).</span></span> <span data-ttu-id="d10b8-110">Bir Azure VM ortamda:</span><span class="sxs-lookup"><span data-stu-id="d10b8-110">In an Azure VM environment:</span></span>
- <span data-ttu-id="d10b8-111">Uygulamalar, diskleri depolama hesaplarında yayılan Vm'lerinde çalışıyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="d10b8-111">Apps can be running on VMs with disks spread across storage accounts.</span></span>
- <span data-ttu-id="d10b8-112">Sanal makineleri, sanal ağ içindeki bir veya daha fazla alt ağlarda eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="d10b8-112">The VMs can be included in one or more subnets within a virtual network.</span></span>

![Müşteri ortamı](./media/site-recovery-azure-to-azure-architecture/source-environment.png)

<span data-ttu-id="d10b8-114">Dağıtım önkoşulları ve gereksinimleri hakkında bilgi edinin [destek matrisi](site-recovery-support-matrix-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="d10b8-114">Learn about the deployment prerequisites and requirements in the [support matrix](site-recovery-support-matrix-azure-to-azure.md).</span></span>

## <a name="replication-process"></a><span data-ttu-id="d10b8-115">Çoğaltma işlemi</span><span class="sxs-lookup"><span data-stu-id="d10b8-115">Replication process</span></span>

### <a name="step-1"></a><span data-ttu-id="d10b8-116">1. Adım</span><span class="sxs-lookup"><span data-stu-id="d10b8-116">Step 1</span></span>

<span data-ttu-id="d10b8-117">Azure portalında Azure VM çoğaltma etkinleştirdiğinizde, aşağıdaki diyagramda ve tabloda gösterilen kaynakları otomatik olarak hedef bölgede oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="d10b8-117">When you enable Azure VM replication in the Azure portal, the resources shown in the following diagram and table are automatically created in the target region.</span></span> <span data-ttu-id="d10b8-118">Varsayılan olarak, kaynakları kaynak bölge ayarları temel alınarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="d10b8-118">By default, resources are created based on source region settings.</span></span> <span data-ttu-id="d10b8-119">Hedef ayarları gerektiği gibi özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d10b8-119">You can customize the target settings as required.</span></span> <span data-ttu-id="d10b8-120">[Daha fazla bilgi edinin](site-recovery-replicate-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="d10b8-120">[Learn more](site-recovery-replicate-azure-to-azure.md).</span></span>

![Çoğaltma işlemi, 1. adım etkinleştir](./media/site-recovery-azure-to-azure-architecture/enable-replication-step-1.png)

<span data-ttu-id="d10b8-122">**Kaynak**</span><span class="sxs-lookup"><span data-stu-id="d10b8-122">**Resource**</span></span> | <span data-ttu-id="d10b8-123">**Ayrıntılar**</span><span class="sxs-lookup"><span data-stu-id="d10b8-123">**Details**</span></span>
--- | ---
<span data-ttu-id="d10b8-124">**Hedef kaynak grubu**</span><span class="sxs-lookup"><span data-stu-id="d10b8-124">**Target resource group**</span></span> | <span data-ttu-id="d10b8-125">Yük devretme sonrasında çoğaltılmış sanal makineleri ait olduğu kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="d10b8-125">The resource group to which replicated VMs belong after failover.</span></span>
<span data-ttu-id="d10b8-126">**Hedef sanal ağ**</span><span class="sxs-lookup"><span data-stu-id="d10b8-126">**Target virtual network**</span></span> | <span data-ttu-id="d10b8-127">Sanal ağ içinde çoğaltılmış VM'ler yük devretme sonrasında bulunur.</span><span class="sxs-lookup"><span data-stu-id="d10b8-127">The virtual network in which replicated VMs are located after failover.</span></span> <span data-ttu-id="d10b8-128">Ağ eşlemesi, kaynak ve hedef sanal ağlar arasında ve tersi yönde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="d10b8-128">A network mapping is created between source and target virtual networks, and vice versa.</span></span>
<span data-ttu-id="d10b8-129">**Önbellek depolama hesapları**</span><span class="sxs-lookup"><span data-stu-id="d10b8-129">**Cache storage accounts**</span></span> | <span data-ttu-id="d10b8-130">Kaynak sanal makineleri üzerinde yapılan değişiklikler için hedef depolama hesabı çoğaltılır önce bunlar izlenen ve hedef konumu önbelleği depolama hesabında gönderilir.</span><span class="sxs-lookup"><span data-stu-id="d10b8-130">Before changes on source VMs are replicated to the target storage account, they are tracked and sent to the cache storage account in the target location.</span></span> <span data-ttu-id="d10b8-131">Bu VM'de çalıştırılan üretim uygulamalar üzerinde en az etki sağlar.</span><span class="sxs-lookup"><span data-stu-id="d10b8-131">This ensures minimal impact on production apps running on the VM.</span></span>
<span data-ttu-id="d10b8-132">**Hedef depolama hesapları**</span><span class="sxs-lookup"><span data-stu-id="d10b8-132">**Target storage accounts**</span></span>  | <span data-ttu-id="d10b8-133">Veri çoğaltılan hedef konumdaki depolama hesapları.</span><span class="sxs-lookup"><span data-stu-id="d10b8-133">Storage accounts in the target location to which the data is replicated.</span></span>
<span data-ttu-id="d10b8-134">**Hedef kullanılabilirlik kümeleri**</span><span class="sxs-lookup"><span data-stu-id="d10b8-134">**Target availability sets**</span></span>  | <span data-ttu-id="d10b8-135">Kullanılabilirlik kümeleri, yük devretme sonrasında çoğaltılmış VM'ler bulunur.</span><span class="sxs-lookup"><span data-stu-id="d10b8-135">Availability sets in which the replicated VMs are located after failover.</span></span>

### <a name="step-2"></a><span data-ttu-id="d10b8-136">2. Adım</span><span class="sxs-lookup"><span data-stu-id="d10b8-136">Step 2</span></span>

<span data-ttu-id="d10b8-137">Çoğaltma etkin olarak Site Recovery uzantısı Mobility hizmeti VM üzerinde otomatik olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="d10b8-137">As replication is enabled, the Site Recovery extension Mobility service is automatically installed on the VM.</span></span> <span data-ttu-id="d10b8-138">Aşağıdakiler gerçekleşir:</span><span class="sxs-lookup"><span data-stu-id="d10b8-138">The following occurs:</span></span>

1. <span data-ttu-id="d10b8-139">VM Site Recovery ile kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="d10b8-139">The VM is registered with Site Recovery.</span></span>

2. <span data-ttu-id="d10b8-140">Sürekli çoğaltma VM için yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="d10b8-140">Continuous replication is configured for the VM.</span></span> <span data-ttu-id="d10b8-141">VM disklerde veri yazma sürekli olarak kaynak konumu önbelleği depolama hesabında aktarılır.</span><span class="sxs-lookup"><span data-stu-id="d10b8-141">Data writes on the VM disks are continuously transferred to the cache storage account in the source location.</span></span>

   ![Çoğaltma işlemi, 2. adım etkinleştir](./media/site-recovery-azure-to-azure-architecture/enable-replication-step-2.png)

   >[!IMPORTANT]
   > <span data-ttu-id="d10b8-143">Site Recovery hiçbir zaman VM'ye gelen bağlantısı gerekir.</span><span class="sxs-lookup"><span data-stu-id="d10b8-143">Site Recovery never needs inbound connectivity to the VM.</span></span> <span data-ttu-id="d10b8-144">VM Site Recovery hizmeti URL'leri/IP adresleri, Office 365 kimlik doğrulaması URL'lerini/IP adresleri ve önbellek depolama hesabı IP adresleri yalnızca giden bağlantı gerekir.</span><span class="sxs-lookup"><span data-stu-id="d10b8-144">The VM needs only outbound connectivity to Site Recovery service URLs/IP addresses, Office 365 authentication URLs/IP addresses, and cache storage account IP addresses.</span></span> <span data-ttu-id="d10b8-145">Daha fazla bilgi için bkz: [Azure sanal makineleri çoğaltmak için Ağ Kılavuzu](site-recovery-azure-to-azure-networking-guidance.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="d10b8-145">For more information, see the [Networking guidance for replicating Azure virtual machines](site-recovery-azure-to-azure-networking-guidance.md) article.</span></span>

## <a name="continuous-replication-process"></a><span data-ttu-id="d10b8-146">Sürekli çoğaltma işlemi</span><span class="sxs-lookup"><span data-stu-id="d10b8-146">Continuous replication process</span></span>

<span data-ttu-id="d10b8-147">Sürekli çoğaltma çalışmaya başladıktan sonra disk yazma işlemleri için önbellek depolama hesabı hemen aktarılır.</span><span class="sxs-lookup"><span data-stu-id="d10b8-147">After continuous replication is working, disk writes are immediately transferred to the cache storage account.</span></span> <span data-ttu-id="d10b8-148">Site Recovery verileri işler ve hedef depolama hesabı gönderir.</span><span class="sxs-lookup"><span data-stu-id="d10b8-148">Site Recovery processes the data and sends it to the target storage account.</span></span> <span data-ttu-id="d10b8-149">Verilerin işlendikten sonra kurtarma noktaları birkaç dakikada bir hedef depolama hesabı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="d10b8-149">After the data is processed, recovery points are generated in the target storage account every few minutes.</span></span>

## <a name="failover-process"></a><span data-ttu-id="d10b8-150">Yük devretme işlemi</span><span class="sxs-lookup"><span data-stu-id="d10b8-150">Failover process</span></span>

<span data-ttu-id="d10b8-151">Bir yük devretme başlatın, VM'ler hedef kaynak grubu içinde hedef sanal ağ, hedef alt oluşturulur ve hedef kullanılabilirlik kümesi.</span><span class="sxs-lookup"><span data-stu-id="d10b8-151">When you initiate a failover, the VMs are created in the target resource group, target virtual network, target subnet, and the target availability set.</span></span> <span data-ttu-id="d10b8-152">Bir yük devretme sırasında herhangi bir kurtarma noktası kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d10b8-152">During a failover, you can use any recovery point.</span></span>

![Yük devretme işlemi](./media/site-recovery-azure-to-azure-architecture/failover.png)

## <a name="next-steps"></a><span data-ttu-id="d10b8-154">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d10b8-154">Next steps</span></span>

- <span data-ttu-id="d10b8-155">Hakkında bilgi edinin [ağ](site-recovery-azure-to-azure-networking-guidance.md) Azure VM çoğaltması için.</span><span class="sxs-lookup"><span data-stu-id="d10b8-155">Learn about [networking](site-recovery-azure-to-azure-networking-guidance.md) for Azure VM replication.</span></span>
- <span data-ttu-id="d10b8-156">Bir kılavuz izleyin [Azure Vm'lerini çoğaltma.](site-recovery-azure-to-azure.md)</span><span class="sxs-lookup"><span data-stu-id="d10b8-156">Follow a walkthrough to [replicate Azure VMs.](site-recovery-azure-to-azure.md)</span></span>
