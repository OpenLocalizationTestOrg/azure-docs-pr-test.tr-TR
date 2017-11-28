---
title: "Azure sanal makine çoğaltmasını Azure bölgeleri iş Azure Site kurtarma arasında aaaHow mu?  | Microsoft Belgeleri"
description: "Bu makalede, bileşenleri ve hello Azure Site Recovery hizmetini kullanarak Azure bölgeler arasında Azure sanal makineleri çoğaltırken kullanılan mimariye genel bakış sağlar."
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
ms.openlocfilehash: 01eda83e490821f8afc8a2973c18a19453a2e84a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-azure-vm-replication-work-in-site-recovery"></a><span data-ttu-id="a0c48-104">Azure VM çoğaltma Site Recovery nasıl çalışır?</span><span class="sxs-lookup"><span data-stu-id="a0c48-104">How does Azure VM replication work in Site Recovery?</span></span>


<span data-ttu-id="a0c48-105">Bu makalede hello bileşenleri ve süreçleri çoğaltılması ve Azure sanal makinelerini (VM'ler) kurtarma hello kullanarak tek bir bölge tooanother söz konusu [Azure Site Recovery](site-recovery-overview.md) hizmet.</span><span class="sxs-lookup"><span data-stu-id="a0c48-105">This article describes hello components and processes involved in replicating and recovering Azure virtual machines (VMs) from one region tooanother by using hello [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

>[!NOTE]
><span data-ttu-id="a0c48-106">Azure VM çoğaltma hello Site Recovery hizmeti ile şu anda önizlemede değil.</span><span class="sxs-lookup"><span data-stu-id="a0c48-106">Azure VM replication with hello Site Recovery service is currently in preview.</span></span>

<span data-ttu-id="a0c48-107">Bu makalenin hello altındaki tüm yorumlar gönderin ya da hello sorular sormak [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="a0c48-107">Post any comments at hello bottom of this article, or ask questions in hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="architectural-components"></a><span data-ttu-id="a0c48-108">Mimari bileşenler</span><span class="sxs-lookup"><span data-stu-id="a0c48-108">Architectural components</span></span>

<span data-ttu-id="a0c48-109">Aşağıdaki diyagramda hello (Bu örnekte, Doğu ABD konumunda hello) belirli bir bölgede bir Azure VM ortamına üst düzey bir görünümünü sağlar.</span><span class="sxs-lookup"><span data-stu-id="a0c48-109">hello following diagram provides a high-level view of an Azure VM environment in a specific region (in this example, hello East US location).</span></span> <span data-ttu-id="a0c48-110">Bir Azure VM ortamda:</span><span class="sxs-lookup"><span data-stu-id="a0c48-110">In an Azure VM environment:</span></span>
- <span data-ttu-id="a0c48-111">Uygulamalar, diskleri depolama hesaplarında yayılan Vm'lerinde çalışıyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="a0c48-111">Apps can be running on VMs with disks spread across storage accounts.</span></span>
- <span data-ttu-id="a0c48-112">bir sanal ağ içindeki bir veya daha fazla alt ağlarda Hello VM'ler dahil edilebilir.</span><span class="sxs-lookup"><span data-stu-id="a0c48-112">hello VMs can be included in one or more subnets within a virtual network.</span></span>

![Müşteri ortamı](./media/site-recovery-azure-to-azure-architecture/source-environment.png)

<span data-ttu-id="a0c48-114">Merhaba dağıtımının önkoşulları ve hello gereksinimleri hakkında bilgi edinin [destek matrisi](site-recovery-support-matrix-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="a0c48-114">Learn about hello deployment prerequisites and requirements in hello [support matrix](site-recovery-support-matrix-azure-to-azure.md).</span></span>

## <a name="replication-process"></a><span data-ttu-id="a0c48-115">Çoğaltma işlemi</span><span class="sxs-lookup"><span data-stu-id="a0c48-115">Replication process</span></span>

### <a name="step-1"></a><span data-ttu-id="a0c48-116">1. Adım</span><span class="sxs-lookup"><span data-stu-id="a0c48-116">Step 1</span></span>

<span data-ttu-id="a0c48-117">Hello Azure portalında Azure VM çoğaltmasında etkinleştirdiğinizde, aşağıdaki hello diyagramı ve tablo hello hedef bölgede otomatik olarak oluşturulan gösterilen kaynakları hello.</span><span class="sxs-lookup"><span data-stu-id="a0c48-117">When you enable Azure VM replication in hello Azure portal, hello resources shown in hello following diagram and table are automatically created in hello target region.</span></span> <span data-ttu-id="a0c48-118">Varsayılan olarak, kaynakları kaynak bölge ayarları temel alınarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="a0c48-118">By default, resources are created based on source region settings.</span></span> <span data-ttu-id="a0c48-119">Merhaba hedef ayarları gerektiği gibi özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a0c48-119">You can customize hello target settings as required.</span></span> <span data-ttu-id="a0c48-120">[Daha fazla bilgi edinin](site-recovery-replicate-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="a0c48-120">[Learn more](site-recovery-replicate-azure-to-azure.md).</span></span>

![Çoğaltma işlemi, 1. adım etkinleştir](./media/site-recovery-azure-to-azure-architecture/enable-replication-step-1.png)

<span data-ttu-id="a0c48-122">**Kaynak**</span><span class="sxs-lookup"><span data-stu-id="a0c48-122">**Resource**</span></span> | <span data-ttu-id="a0c48-123">**Ayrıntılar**</span><span class="sxs-lookup"><span data-stu-id="a0c48-123">**Details**</span></span>
--- | ---
<span data-ttu-id="a0c48-124">**Hedef kaynak grubu**</span><span class="sxs-lookup"><span data-stu-id="a0c48-124">**Target resource group**</span></span> | <span data-ttu-id="a0c48-125">Yük devretme sonrasında çoğaltılmış sanal makineleri ait kaynak grubu toowhich hello.</span><span class="sxs-lookup"><span data-stu-id="a0c48-125">hello resource group toowhich replicated VMs belong after failover.</span></span>
<span data-ttu-id="a0c48-126">**Hedef sanal ağ**</span><span class="sxs-lookup"><span data-stu-id="a0c48-126">**Target virtual network**</span></span> | <span data-ttu-id="a0c48-127">Merhaba sanal ağ içinde çoğaltılmış VM'ler yük devretme sonrasında bulunur.</span><span class="sxs-lookup"><span data-stu-id="a0c48-127">hello virtual network in which replicated VMs are located after failover.</span></span> <span data-ttu-id="a0c48-128">Ağ eşlemesi, kaynak ve hedef sanal ağlar arasında ve tersi yönde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="a0c48-128">A network mapping is created between source and target virtual networks, and vice versa.</span></span>
<span data-ttu-id="a0c48-129">**Önbellek depolama hesapları**</span><span class="sxs-lookup"><span data-stu-id="a0c48-129">**Cache storage accounts**</span></span> | <span data-ttu-id="a0c48-130">Kaynak VM'ler üzerindeki değişiklikler toohello hedef depolama hesabı çoğaltılan önce bunlar izlenen ve toohello önbellek depolama hesabı hello hedef konumda gönderilen.</span><span class="sxs-lookup"><span data-stu-id="a0c48-130">Before changes on source VMs are replicated toohello target storage account, they are tracked and sent toohello cache storage account in hello target location.</span></span> <span data-ttu-id="a0c48-131">Bu VM hello üzerinde çalışan üretim uygulamalar üzerinde en az etki sağlar.</span><span class="sxs-lookup"><span data-stu-id="a0c48-131">This ensures minimal impact on production apps running on hello VM.</span></span>
<span data-ttu-id="a0c48-132">**Hedef depolama hesapları**</span><span class="sxs-lookup"><span data-stu-id="a0c48-132">**Target storage accounts**</span></span>  | <span data-ttu-id="a0c48-133">Merhaba hedef konum toowhich hello verileri depolama hesaplarında çoğaltılır.</span><span class="sxs-lookup"><span data-stu-id="a0c48-133">Storage accounts in hello target location toowhich hello data is replicated.</span></span>
<span data-ttu-id="a0c48-134">**Hedef kullanılabilirlik kümeleri**</span><span class="sxs-lookup"><span data-stu-id="a0c48-134">**Target availability sets**</span></span>  | <span data-ttu-id="a0c48-135">Kullanılabilirlik çoğaltılan hangi hello VM'ler yük devretme sonrasında bulunan ayarlar.</span><span class="sxs-lookup"><span data-stu-id="a0c48-135">Availability sets in which hello replicated VMs are located after failover.</span></span>

### <a name="step-2"></a><span data-ttu-id="a0c48-136">2. Adım</span><span class="sxs-lookup"><span data-stu-id="a0c48-136">Step 2</span></span>

<span data-ttu-id="a0c48-137">Çoğaltma etkin olarak hello Site Recovery uzantısı Mobility hizmeti hello VM üzerinde otomatik olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="a0c48-137">As replication is enabled, hello Site Recovery extension Mobility service is automatically installed on hello VM.</span></span> <span data-ttu-id="a0c48-138">Merhaba şunlar olur:</span><span class="sxs-lookup"><span data-stu-id="a0c48-138">hello following occurs:</span></span>

1. <span data-ttu-id="a0c48-139">Merhaba VM Site Recovery ile kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="a0c48-139">hello VM is registered with Site Recovery.</span></span>

2. <span data-ttu-id="a0c48-140">Sürekli çoğaltma VM hello için yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="a0c48-140">Continuous replication is configured for hello VM.</span></span> <span data-ttu-id="a0c48-141">Verileri yazar hello VM üzerinde disklerdir sürekli toohello önbellek depolama hesabı hello kaynak konumda aktarılan.</span><span class="sxs-lookup"><span data-stu-id="a0c48-141">Data writes on hello VM disks are continuously transferred toohello cache storage account in hello source location.</span></span>

   ![Çoğaltma işlemi, 2. adım etkinleştir](./media/site-recovery-azure-to-azure-architecture/enable-replication-step-2.png)

   >[!IMPORTANT]
   > <span data-ttu-id="a0c48-143">Site kurtarma hiçbir zaman gelen bağlantı toohello VM gerekir.</span><span class="sxs-lookup"><span data-stu-id="a0c48-143">Site Recovery never needs inbound connectivity toohello VM.</span></span> <span data-ttu-id="a0c48-144">Merhaba VM yalnızca giden bağlantı tooSite kurtarma hizmeti URL'leri/IP adresleri, Office 365 kimlik doğrulaması URL'lerini/IP adresleri ve önbellek depolama hesabı IP adresi gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="a0c48-144">hello VM needs only outbound connectivity tooSite Recovery service URLs/IP addresses, Office 365 authentication URLs/IP addresses, and cache storage account IP addresses.</span></span> <span data-ttu-id="a0c48-145">Daha fazla bilgi için bkz: Merhaba [Azure sanal makineleri çoğaltmak için Ağ Kılavuzu](site-recovery-azure-to-azure-networking-guidance.md) makale.</span><span class="sxs-lookup"><span data-stu-id="a0c48-145">For more information, see hello [Networking guidance for replicating Azure virtual machines](site-recovery-azure-to-azure-networking-guidance.md) article.</span></span>

## <a name="continuous-replication-process"></a><span data-ttu-id="a0c48-146">Sürekli çoğaltma işlemi</span><span class="sxs-lookup"><span data-stu-id="a0c48-146">Continuous replication process</span></span>

<span data-ttu-id="a0c48-147">Sürekli çoğaltma çalışmaya başladıktan sonra disk yazma hemen olan toohello önbellek depolama hesabı aktarılan.</span><span class="sxs-lookup"><span data-stu-id="a0c48-147">After continuous replication is working, disk writes are immediately transferred toohello cache storage account.</span></span> <span data-ttu-id="a0c48-148">Site Recovery hello verilerini işler ve toohello hedef depolama hesabı gönderir.</span><span class="sxs-lookup"><span data-stu-id="a0c48-148">Site Recovery processes hello data and sends it toohello target storage account.</span></span> <span data-ttu-id="a0c48-149">Merhaba veri işlendikten sonra kurtarma noktaları birkaç dakikada hello hedef depolama hesabı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="a0c48-149">After hello data is processed, recovery points are generated in hello target storage account every few minutes.</span></span>

## <a name="failover-process"></a><span data-ttu-id="a0c48-150">Yük devretme işlemi</span><span class="sxs-lookup"><span data-stu-id="a0c48-150">Failover process</span></span>

<span data-ttu-id="a0c48-151">Bir yük devretme başlatın, VM'ler oluşturulduktan hello hedef kaynak grubu, hedef sanal ağ, hedef alt hello ve hello kullanılabilirlik kümesi hedefleyin.</span><span class="sxs-lookup"><span data-stu-id="a0c48-151">When you initiate a failover, hello VMs are created in hello target resource group, target virtual network, target subnet, and hello target availability set.</span></span> <span data-ttu-id="a0c48-152">Bir yük devretme sırasında herhangi bir kurtarma noktası kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a0c48-152">During a failover, you can use any recovery point.</span></span>

![Yük devretme işlemi](./media/site-recovery-azure-to-azure-architecture/failover.png)

## <a name="next-steps"></a><span data-ttu-id="a0c48-154">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a0c48-154">Next steps</span></span>

- <span data-ttu-id="a0c48-155">Hakkında bilgi edinin [ağ](site-recovery-azure-to-azure-networking-guidance.md) Azure VM çoğaltması için.</span><span class="sxs-lookup"><span data-stu-id="a0c48-155">Learn about [networking](site-recovery-azure-to-azure-networking-guidance.md) for Azure VM replication.</span></span>
- <span data-ttu-id="a0c48-156">İzlenecek yollar çok izleyin[Azure Vm'lerini çoğaltma.](site-recovery-azure-to-azure.md)</span><span class="sxs-lookup"><span data-stu-id="a0c48-156">Follow a walkthrough too[replicate Azure VMs.](site-recovery-azure-to-azure.md)</span></span>
