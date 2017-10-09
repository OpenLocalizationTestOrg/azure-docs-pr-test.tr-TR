---
title: "Azure bölgeler arasında Azure VM'ler, çoğaltma için aaaReview hello mimarisi | Microsoft Docs"
description: "Bu makalede, bileşenleri ve Azure Vm'leri hello Azure Site Recovery hizmetini kullanarak Azure bölgeler arasında çoğaltırken kullanılan mimariye genel bakış sağlar."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/12/2017
ms.author: raynew
ms.openlocfilehash: 4caab4e7a764040f317201d1345c40c73f836d81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="step-1-review-hello-architecture-for-azure-vm-replication-between-azure-regions"></a><span data-ttu-id="a1420-103">1. adım: Azure bölgeler arasında Azure VM çoğaltması için hello mimarisi gözden geçirin</span><span class="sxs-lookup"><span data-stu-id="a1420-103">Step 1: Review hello architecture for Azure VM replication between Azure regions</span></span>


<span data-ttu-id="a1420-104">Merhaba gözden geçirdikten sonra [genel bakış adımları](azure-to-azure-walkthrough-overview.md) bu dağıtım için bu makale toounderstand hello bileşenleri ve süreçleri çoğaltılması ve Azure sanal makineleri (VM'ler) bir Azure bölgesi tooanother, Kurtarma sırasında kullanılan okuma kullanma [Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a1420-104">After reviewing hello [overview steps](azure-to-azure-walkthrough-overview.md) for this deployment, read this article toounderstand hello components and processes used when replicating and recovering Azure virtual machines (VMs) from one Azure region tooanother, using [Azure Site Recovery](site-recovery-overview.md).</span></span>

- <span data-ttu-id="a1420-105">Merhaba makale bitirdikten sonra Azure VM çoğaltma tooanother bölge nasıl çalıştığını anlamak olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a1420-105">When you finish hello article, you should have a clear understanding of how Azure VM replication tooanother region works.</span></span>
- <span data-ttu-id="a1420-106">Bu makalenin hello altındaki tüm yorumlar gönderin ya da hello sorular sormak [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="a1420-106">Post any comments at hello bottom of this article, or ask questions in hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

>[!NOTE]
><span data-ttu-id="a1420-107">Azure VM çoğaltma hello Site Recovery hizmeti ile şu anda önizlemede değil.</span><span class="sxs-lookup"><span data-stu-id="a1420-107">Azure VM replication with hello Site Recovery service is currently in preview.</span></span>



## <a name="architectural-components"></a><span data-ttu-id="a1420-108">Mimari bileşenler</span><span class="sxs-lookup"><span data-stu-id="a1420-108">Architectural components</span></span>

<span data-ttu-id="a1420-109">Aşağıdaki diyagramda hello (Bu örnekte, Doğu ABD konumunda hello) belirli bir bölgede bir Azure VM ortamına üst düzey bir görünümünü sağlar.</span><span class="sxs-lookup"><span data-stu-id="a1420-109">hello following diagram provides a high-level view of an Azure VM environment in a specific region (in this example, hello East US location).</span></span> <span data-ttu-id="a1420-110">Bir Azure VM ortamda:</span><span class="sxs-lookup"><span data-stu-id="a1420-110">In an Azure VM environment:</span></span>
- <span data-ttu-id="a1420-111">Uygulamalar, diskleri depolama hesaplarında yayılan Vm'lerinde çalışıyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="a1420-111">Apps can be running on VMs with disks spread across storage accounts.</span></span>
- <span data-ttu-id="a1420-112">bir sanal ağ içindeki bir veya daha fazla alt ağlarda Hello VM'ler dahil edilebilir.</span><span class="sxs-lookup"><span data-stu-id="a1420-112">hello VMs can be included in one or more subnets within a virtual network.</span></span>

![Müşteri ortamı](./media/azure-to-azure-walkthrough-architecture/source-environment.png)

## <a name="replication-process"></a><span data-ttu-id="a1420-114">Çoğaltma işlemi</span><span class="sxs-lookup"><span data-stu-id="a1420-114">Replication process</span></span>

### <a name="step-1"></a><span data-ttu-id="a1420-115">1. Adım</span><span class="sxs-lookup"><span data-stu-id="a1420-115">Step 1</span></span>

<span data-ttu-id="a1420-116">Hello Azure portalında Azure VM çoğaltmasında etkinleştirdiğinizde, aşağıdaki hello diyagramı ve tablo hello hedef bölgede otomatik olarak oluşturulan gösterilen kaynakları hello.</span><span class="sxs-lookup"><span data-stu-id="a1420-116">When you enable Azure VM replication in hello Azure portal, hello resources shown in hello following diagram and table are automatically created in hello target region.</span></span> <span data-ttu-id="a1420-117">Varsayılan olarak, kaynakları kaynak bölge ayarları temel alınarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="a1420-117">By default, resources are created based on source region settings.</span></span> <span data-ttu-id="a1420-118">Merhaba hedef ayarları gerektiği gibi özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a1420-118">You can customize hello target settings as required.</span></span> <span data-ttu-id="a1420-119">[Daha fazla bilgi edinin](site-recovery-replicate-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="a1420-119">[Learn more](site-recovery-replicate-azure-to-azure.md).</span></span>

![Çoğaltma işlemi, 1. adım etkinleştir](./media/azure-to-azure-walkthrough-architecture/enable-replication-step-1.png)

<span data-ttu-id="a1420-121">**Kaynak**</span><span class="sxs-lookup"><span data-stu-id="a1420-121">**Resource**</span></span> | <span data-ttu-id="a1420-122">**Ayrıntılar**</span><span class="sxs-lookup"><span data-stu-id="a1420-122">**Details**</span></span>
--- | ---
<span data-ttu-id="a1420-123">**Hedef kaynak grubu**</span><span class="sxs-lookup"><span data-stu-id="a1420-123">**Target resource group**</span></span> | <span data-ttu-id="a1420-124">Yük devretme sonrasında çoğaltılmış sanal makineleri ait kaynak grubu toowhich hello.</span><span class="sxs-lookup"><span data-stu-id="a1420-124">hello resource group toowhich replicated VMs belong after failover.</span></span>
<span data-ttu-id="a1420-125">**Hedef sanal ağ**</span><span class="sxs-lookup"><span data-stu-id="a1420-125">**Target virtual network**</span></span> | <span data-ttu-id="a1420-126">Merhaba sanal ağ içinde çoğaltılmış VM'ler yük devretme sonrasında bulunur.</span><span class="sxs-lookup"><span data-stu-id="a1420-126">hello virtual network in which replicated VMs are located after failover.</span></span> <span data-ttu-id="a1420-127">Ağ eşlemesi, kaynak ve hedef sanal ağlar arasında ve tersi yönde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="a1420-127">A network mapping is created between source and target virtual networks, and vice versa.</span></span>
<span data-ttu-id="a1420-128">**Önbellek depolama hesapları**</span><span class="sxs-lookup"><span data-stu-id="a1420-128">**Cache storage accounts**</span></span> | <span data-ttu-id="a1420-129">Kaynak VM'ler üzerindeki değişiklikler toohello hedef depolama hesabı çoğaltılan önce bunlar izlenen ve toohello önbellek depolama hesabı hello hedef konumda gönderilen.</span><span class="sxs-lookup"><span data-stu-id="a1420-129">Before changes on source VMs are replicated toohello target storage account, they are tracked and sent toohello cache storage account in hello target location.</span></span> <span data-ttu-id="a1420-130">Bu VM hello üzerinde çalışan üretim uygulamalar üzerinde en az etki sağlar.</span><span class="sxs-lookup"><span data-stu-id="a1420-130">This ensures minimal impact on production apps running on hello VM.</span></span>
<span data-ttu-id="a1420-131">**Hedef depolama hesapları**</span><span class="sxs-lookup"><span data-stu-id="a1420-131">**Target storage accounts**</span></span>  | <span data-ttu-id="a1420-132">Merhaba hedef konum toowhich hello verileri depolama hesaplarında çoğaltılır.</span><span class="sxs-lookup"><span data-stu-id="a1420-132">Storage accounts in hello target location toowhich hello data is replicated.</span></span>
<span data-ttu-id="a1420-133">**Hedef kullanılabilirlik kümeleri**</span><span class="sxs-lookup"><span data-stu-id="a1420-133">**Target availability sets**</span></span>  | <span data-ttu-id="a1420-134">Kullanılabilirlik çoğaltılan hangi hello VM'ler yük devretme sonrasında bulunan ayarlar.</span><span class="sxs-lookup"><span data-stu-id="a1420-134">Availability sets in which hello replicated VMs are located after failover.</span></span>

### <a name="step-2"></a><span data-ttu-id="a1420-135">2. Adım</span><span class="sxs-lookup"><span data-stu-id="a1420-135">Step 2</span></span>

<span data-ttu-id="a1420-136">Çoğaltma etkin olarak hello Site Recovery uzantısı Mobility hizmeti hello VM üzerinde otomatik olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="a1420-136">As replication is enabled, hello Site Recovery extension Mobility service is automatically installed on hello VM.</span></span> <span data-ttu-id="a1420-137">Merhaba şunlar olur:</span><span class="sxs-lookup"><span data-stu-id="a1420-137">hello following occurs:</span></span>

1. <span data-ttu-id="a1420-138">Merhaba VM Site Recovery ile kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="a1420-138">hello VM is registered with Site Recovery.</span></span>

2. <span data-ttu-id="a1420-139">Sürekli çoğaltma VM hello için yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="a1420-139">Continuous replication is configured for hello VM.</span></span> <span data-ttu-id="a1420-140">Verileri yazar hello VM üzerinde disklerdir sürekli toohello önbellek depolama hesabı hello kaynak konumda aktarılan.</span><span class="sxs-lookup"><span data-stu-id="a1420-140">Data writes on hello VM disks are continuously transferred toohello cache storage account in hello source location.</span></span>

   ![Çoğaltma işlemi, 2. adım etkinleştir](./media/azure-to-azure-walkthrough-architecture/enable-replication-step-2.png)

  
  <span data-ttu-id="a1420-142">Site Recovery hiç bağlantı toohello VM gelen gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="a1420-142">Note that Site Recovery never needs inbound connectivity toohello VM.</span></span> <span data-ttu-id="a1420-143">Yalnızca bağlantı tooSite kurtarma hizmeti URL'leri/IP adresleri, Office 365 kimlik doğrulaması URL'lerini/IP adresleri ve önbellek depolama hesabı IP adresleri gerekli giden.</span><span class="sxs-lookup"><span data-stu-id="a1420-143">Only outbound connectivity tooSite Recovery service URLs/IP addresses, Office 365 authentication URLs/IP addresses, and cache storage account IP addresses is needed.</span></span> 

## <a name="continuous-replication-process"></a><span data-ttu-id="a1420-144">Sürekli çoğaltma işlemi</span><span class="sxs-lookup"><span data-stu-id="a1420-144">Continuous replication process</span></span>

<span data-ttu-id="a1420-145">Sürekli çoğaltma çalışmaya başladıktan sonra disk yazma hemen olan toohello önbellek depolama hesabı aktarılan.</span><span class="sxs-lookup"><span data-stu-id="a1420-145">After continuous replication is working, disk writes are immediately transferred toohello cache storage account.</span></span> <span data-ttu-id="a1420-146">Site Recovery hello verilerini işler ve toohello hedef depolama hesabı gönderir.</span><span class="sxs-lookup"><span data-stu-id="a1420-146">Site Recovery processes hello data and sends it toohello target storage account.</span></span> <span data-ttu-id="a1420-147">Merhaba veri işlendikten sonra kurtarma noktaları birkaç dakikada hello hedef depolama hesabı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="a1420-147">After hello data is processed, recovery points are generated in hello target storage account every few minutes.</span></span>

## <a name="failover-process"></a><span data-ttu-id="a1420-148">Yük devretme işlemi</span><span class="sxs-lookup"><span data-stu-id="a1420-148">Failover process</span></span>

<span data-ttu-id="a1420-149">Bir yük devretme başlatın, VM'ler oluşturulduktan hello hedef kaynak grubu, hedef sanal ağ, hedef alt hello ve hello kullanılabilirlik kümesi hedefleyin.</span><span class="sxs-lookup"><span data-stu-id="a1420-149">When you initiate a failover, hello VMs are created in hello target resource group, target virtual network, target subnet, and hello target availability set.</span></span> <span data-ttu-id="a1420-150">Bir yük devretme sırasında herhangi bir kurtarma noktası kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a1420-150">During a failover, you can use any recovery point.</span></span>

![Yük devretme işlemi](./media/azure-to-azure-walkthrough-architecture/failover.png)

## <a name="next-steps"></a><span data-ttu-id="a1420-152">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a1420-152">Next steps</span></span>

<span data-ttu-id="a1420-153">Çok Git[2. adım: Önkoşullar ve sınırlamalar doğrulayın](azure-to-azure-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="a1420-153">Go too[Step 2: Verify prerequisites and limitations](azure-to-azure-walkthrough-prerequisites.md)</span></span>
