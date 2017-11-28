---
title: "Azure bölgeler arasında Azure Vm'leri aaaReplicate | Microsoft Docs"
description: "Merhaba adımlar, gerekli hello Azure portal'deki hello Azure Site Recovery hizmeti ile Azure bölgeler arasında tooreplicate Azure VM'ler özetler"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: 6dd36239-4363-4538-bf80-a18e71b8ec67
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: raynew
ms.openlocfilehash: f4ac386f040945131f8a10f02143437f4441e298
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-azure-vms-between-regions-with-azure-site-recovery"></a><span data-ttu-id="5f688-103">Azure Site Recovery ile bölgeler arasında Azure Vm'lerini çoğaltma</span><span class="sxs-lookup"><span data-stu-id="5f688-103">Replicate Azure VMs between regions with Azure Site Recovery</span></span>

><span data-ttu-id="5f688-104">Bu makale bir Azure bölgesi tooAzure sanal makineleri farklı bir bölgede Azure sanal makinelerde (VM'ler) hello adımları gerekli tooreplicate genel bir bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="5f688-104">This article provides an overview of hello steps required tooreplicate Azure virtual machines (VMs) in one Azure region tooAzure VMs in a different region.</span></span> 

>[!NOTE]
>
> <span data-ttu-id="5f688-105">Azure VM çoğaltma şu anda önizlemede değil.</span><span class="sxs-lookup"><span data-stu-id="5f688-105">Azure VM replication is currently in preview.</span></span>

<span data-ttu-id="5f688-106">POST açıklamaları ve soruları hello altındaki bu makalenin veya hello [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="5f688-106">Post comments and questions at hello bottom of this article or on hello [Azure Recovery Services forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="step-1-review-architecture"></a><span data-ttu-id="5f688-107">1. adım: Gözden geçirme mimarisi</span><span class="sxs-lookup"><span data-stu-id="5f688-107">Step 1: Review architecture</span></span>

<span data-ttu-id="5f688-108">Dağıtıma başlamadan önce hello senaryo mimarisi ve toodeploy gereksinim hello bileşenleri gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="5f688-108">Before you start deployment, review hello scenario architecture, and hello components you need toodeploy.</span></span>

<span data-ttu-id="5f688-109">Çok Git[1. adım: gözden hello mimarisi](azure-to-azure-walkthrough-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="5f688-109">Go too[Step 1: Review hello architecture](azure-to-azure-walkthrough-architecture.md)</span></span>


## <a name="step-2-review-prerequisites"></a><span data-ttu-id="5f688-110">2. adım: Gözden geçirme önkoşulları</span><span class="sxs-lookup"><span data-stu-id="5f688-110">Step 2: Review prerequisites</span></span>

<span data-ttu-id="5f688-111">Sahip Merhaba, bir abonelik, sanal ağlar, depolama hesapları ve VM gereksinimleri çeşitli yerlerde Azure önkoşulları denetleyin.</span><span class="sxs-lookup"><span data-stu-id="5f688-111">Check that you have hello Azure prerequisites in places, including a subscription, virtual networks, storage accounts, and VM requirements.</span></span>

<span data-ttu-id="5f688-112">Çok Git[2. adım: Önkoşullar ve sınırlamalar doğrulayın](azure-to-azure-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="5f688-112">Go too[Step 2: Verify prerequisites and limitations](azure-to-azure-walkthrough-prerequisites.md)</span></span>


## <a name="step-3-plan-networking"></a><span data-ttu-id="5f688-113">3. adım: ağ planlama</span><span class="sxs-lookup"><span data-stu-id="5f688-113">Step 3: Plan networking</span></span>

<span data-ttu-id="5f688-114">Giden bağlantı tooreplicate ve şirket içi bağlantılarından ayarlanır istediğiniz Azure vm'lerinde kurulduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="5f688-114">Check that outbound connectivity is set up on Azure VMs you want tooreplicate, and that connections from on-premises are set up.</span></span>

<span data-ttu-id="5f688-115">Çok Git[4. adım: ağ planı](azure-to-azure-walkthrough-network.md)</span><span class="sxs-lookup"><span data-stu-id="5f688-115">Go too[Step 4: Plan networking](azure-to-azure-walkthrough-network.md)</span></span>



## <a name="step-4-create-a-vault"></a><span data-ttu-id="5f688-116">4. adım: bir kasa oluşturma</span><span class="sxs-lookup"><span data-stu-id="5f688-116">Step 4: Create a vault</span></span> 

<span data-ttu-id="5f688-117">Kurtarma Hizmetleri kasası tooorchestrate yukarı tooset gerekir ve çoğaltmayı yönetmek ve hello kaynak bölge belirtin.</span><span class="sxs-lookup"><span data-stu-id="5f688-117">You need tooset up a Recovery Services vault tooorchestrate and manage replication, and specify hello source region.</span></span>

<span data-ttu-id="5f688-118">Çok Git[4. adım: bir kasa oluşturun](azure-to-azure-walkthrough-vault.md)</span><span class="sxs-lookup"><span data-stu-id="5f688-118">Go too[Step 4: Create a vault](azure-to-azure-walkthrough-vault.md)</span></span>


## <a name="step-5-enable-replication"></a><span data-ttu-id="5f688-119">5. adım: Çoğaltma etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="5f688-119">Step 5: Enable replication</span></span>


<span data-ttu-id="5f688-120">tooenable çoğaltma hedef konumu ayarları yapılandırmak, bir çoğaltma ilkesini ayarlayın ve hello Azure tooreplicate istediğiniz sanal makineleri seçin.</span><span class="sxs-lookup"><span data-stu-id="5f688-120">tooenable replication, you configure target location settings, set up a replication policy, and select hello Azure VMs that you want tooreplicate.</span></span> <span data-ttu-id="5f688-121">Etkinleştirdikten sonra ilk çoğaltma işlemi hello VM oluşur.</span><span class="sxs-lookup"><span data-stu-id="5f688-121">After enabling, initial replication of hello VM occurs.</span></span>

<span data-ttu-id="5f688-122">Çok Git[5. adım: çoğaltmasını etkinleştir](azure-to-azure-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="5f688-122">Go too[Step 5: Enable replication](azure-to-azure-walkthrough-enable-replication.md)</span></span>


## <a name="step-6-run-a-test-failover"></a><span data-ttu-id="5f688-123">6. adım: yük devretme testi çalıştırma</span><span class="sxs-lookup"><span data-stu-id="5f688-123">Step 6: Run a test failover</span></span>

<span data-ttu-id="5f688-124">İlk çoğaltma sonlandırıldıktan ve değişim çoğaltması çalıştıran sonra her şeyin beklendiği gibi çalıştığından emin bir test yük devretme toomake çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5f688-124">After initial replication finishes, and delta replication is running, you can run a test failover toomake sure everything works as expected.</span></span>

<span data-ttu-id="5f688-125">Çok Git[6. adım: yük devretme testi çalıştırma](azure-to-azure-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="5f688-125">Go too[Step 6: Run a test failover](azure-to-azure-walkthrough-test-failover.md)</span></span>


