---
title: "aaaReplicate fiziksel şirket içi sunucuları tooAzure Azure Site Recovery ile | Microsoft Docs"
description: "Şirket içi Windows/Linux fiziksel sunucuları tooAzure hello Azure Site Recovery hizmeti ile çalışan iş yükleri çoğaltmak için hello adımlara genel bir bakış sağlar."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 20122f01-929a-4675-b85b-a9b99d2618bc
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: f801b9544072d4029ec06cc1abfd4ff370e852e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-physical-servers-tooazure-with-site-recovery"></a><span data-ttu-id="15c56-103">Site Recovery ile fiziksel sunucuları tooAzure Çoğalt</span><span class="sxs-lookup"><span data-stu-id="15c56-103">Replicate physical servers tooAzure with Site Recovery</span></span>

<span data-ttu-id="15c56-104">Bu makalede hello kullanarak hello adımları gerekli tooreplicate şirket içi Windows/Linux fiziksel sunucuları tooAzure, genel bir bakış sağlar [Azure Site Recovery](site-recovery-overview.md) hello Azure portal hizmeti.</span><span class="sxs-lookup"><span data-stu-id="15c56-104">This article provides an overview of hello steps required tooreplicate on-premises Windows/Linux physical servers tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>


## <a name="step-1-review-architecture-and-prerequisites"></a><span data-ttu-id="15c56-105">1. adım: mimarisi ve önkoşulları gözden geçirin</span><span class="sxs-lookup"><span data-stu-id="15c56-105">Step 1: Review architecture and prerequisites</span></span>

<span data-ttu-id="15c56-106">Dağıtıma başlamadan önce hello senaryo mimarisinin gözden geçirin ve hello dağıtım tooset gerek duyduğunuz tüm hello bileşenleri anladığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="15c56-106">Before you start deployment, review hello scenario architecture, and make sure you understand all hello components you need tooset up hello deployment.</span></span>

<span data-ttu-id="15c56-107">Çok Git[1. adım: gözden hello mimarisi](physical-walkthrough-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="15c56-107">Go too[Step 1: Review hello architecture](physical-walkthrough-architecture.md)</span></span>


## <a name="step-2-review-prerequisites"></a><span data-ttu-id="15c56-108">2. adım: Gözden geçirme önkoşulları</span><span class="sxs-lookup"><span data-stu-id="15c56-108">Step 2: Review prerequisites</span></span>

<span data-ttu-id="15c56-109">Merhaba Önkoşullar her dağıtım bileşen için yerinde olduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="15c56-109">Make sure you have hello prerequisites in place for each deployment component:</span></span>

- <span data-ttu-id="15c56-110">**Azure önkoşulları**: bir Microsoft Azure hesabı, Azure ağları ve depolama hesapları gerekir.</span><span class="sxs-lookup"><span data-stu-id="15c56-110">**Azure prerequisites**: You need a Microsoft Azure account, Azure networks, and storage accounts.</span></span>
- <span data-ttu-id="15c56-111">**Şirket içi Site Recovery bileşenlerini**: şirket içi Site Recovery bileşenlerini çalıştıran bir makineye gerekir.</span><span class="sxs-lookup"><span data-stu-id="15c56-111">**On-premises Site Recovery components**: You need a machine running on-premises Site Recovery components.</span></span>
- <span data-ttu-id="15c56-112">**Makineler çoğaltılan**: tooreplicate istediğiniz sunucuları şirket içi ve Azure gereksinimleri ile toocomply gerekir.</span><span class="sxs-lookup"><span data-stu-id="15c56-112">**Replicated machines**: Servers you want tooreplicate need toocomply with on-premises and Azure requirements.</span></span>

<span data-ttu-id="15c56-113">Çok Git[2. adım: gözden Önkoşullar ve sınırlamalar](physical-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="15c56-113">Go too[Step 2: Review prerequisites and limitations](physical-walkthrough-prerequisites.md)</span></span>

## <a name="step-3-plan-capacity"></a><span data-ttu-id="15c56-114">3. adım: Planı kapasite</span><span class="sxs-lookup"><span data-stu-id="15c56-114">Step 3: Plan capacity</span></span>

<span data-ttu-id="15c56-115">Tam dağıtımını yaptığınız ihtiyacınız hangi çoğaltma kaynakları çıkışı toofigure gerekir.</span><span class="sxs-lookup"><span data-stu-id="15c56-115">If you're doing a full deployment you need toofigure out what replication resources you need.</span></span> <span data-ttu-id="15c56-116">Tootest hello ortamını ayarlama hızlı yaptığınız varsa, bu adımı atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="15c56-116">If you're doing a quick set up tootest hello environment, you can skip this step.</span></span>

<span data-ttu-id="15c56-117">Çok Git[3. adım: kapasite planlama](physical-walkthrough-capacity.md)</span><span class="sxs-lookup"><span data-stu-id="15c56-117">Go too[Step 3: Plan capacity](physical-walkthrough-capacity.md)</span></span>

## <a name="step-4-plan-networking"></a><span data-ttu-id="15c56-118">4. adım: ağ planlama</span><span class="sxs-lookup"><span data-stu-id="15c56-118">Step 4: Plan networking</span></span>

<span data-ttu-id="15c56-119">Yük devretme gerçekleştikten sonra Azure Vm'lerinin bağlı toonetworks olduğunu ve sahip oldukları hello doğru IP adreslerine tooensure planlama bazı ağ toodo gerekir.</span><span class="sxs-lookup"><span data-stu-id="15c56-119">You need toodo some network planning tooensure that Azure VMs are connected toonetworks after failover occurs, and  that that they have hello right IP addresses.</span></span>

<span data-ttu-id="15c56-120">Çok Git[4. adım: ağ planı](physical-walkthrough-network.md)</span><span class="sxs-lookup"><span data-stu-id="15c56-120">Go too[Step 4: Plan networking](physical-walkthrough-network.md)</span></span>

##  <a name="step-5-prepare-azure-resources"></a><span data-ttu-id="15c56-121">5. adım: Azure kaynaklarını hazırlama</span><span class="sxs-lookup"><span data-stu-id="15c56-121">Step 5: Prepare Azure resources</span></span>

<span data-ttu-id="15c56-122">Başlamadan önce Azure ağları ve depolama ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="15c56-122">Set up Azure networks and storage before you start.</span></span> 

<span data-ttu-id="15c56-123">Çok Git[5. adım: Azure hazırlama](physical-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="15c56-123">Go too[Step 5: Prepare Azure](physical-walkthrough-prepare-azure.md)</span></span>


## <a name="step-6-set-up-a-vault"></a><span data-ttu-id="15c56-124">6. adım: Bir kasa ayarlama</span><span class="sxs-lookup"><span data-stu-id="15c56-124">Step 6: Set up a vault</span></span>

<span data-ttu-id="15c56-125">Kurtarma Hizmetleri kasası tooorchestrate ayarlamak ve çoğaltmayı yönetme.</span><span class="sxs-lookup"><span data-stu-id="15c56-125">You set up a Recovery Services vault tooorchestrate and manage replication.</span></span> <span data-ttu-id="15c56-126">Merhaba kasasını ayarladığınızda, istediğinizi belirtin tooreplicate, ve tooreplicate istediğiniz şekilde.</span><span class="sxs-lookup"><span data-stu-id="15c56-126">When you set up hello vault, you specify what you want tooreplicate, and where you want tooreplicate it to.</span></span>

<span data-ttu-id="15c56-127">Çok Git[adım 6: bir kasasını oluşturup](physical-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="15c56-127">Go too[Step 6: Set up a vault](physical-walkthrough-create-vault.md)</span></span>

## <a name="step-7-configure-source-and-target-settings"></a><span data-ttu-id="15c56-128">7. adım: kaynak ve hedef ayarlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="15c56-128">Step 7: Configure source and target settings</span></span>

<span data-ttu-id="15c56-129">Merhaba kaynağı için ayarları yapılandırın ve hedef (Azure).</span><span class="sxs-lookup"><span data-stu-id="15c56-129">Configure settings for hello source and target (Azure) site.</span></span> <span data-ttu-id="15c56-130">Kaynak ayarları birleşik Kurulum tooinstall hello şirket içi Site Recovery bileşenlerini çalıştıran içerir.</span><span class="sxs-lookup"><span data-stu-id="15c56-130">Source settings includes running Unified Setup tooinstall hello on-premises Site Recovery components.</span></span>

<span data-ttu-id="15c56-131">Çok Git[adım 7: hello kaynak ve hedef ayarlama](physical-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="15c56-131">Go too[Step 7: Set up hello source and target](physical-walkthrough-source-target.md)</span></span>

## <a name="step-8-set-up-a-replication-policy"></a><span data-ttu-id="15c56-132">8. adım: Bir çoğaltma ilkesi ayarlama</span><span class="sxs-lookup"><span data-stu-id="15c56-132">Step 8: Set up a replication policy</span></span>

<span data-ttu-id="15c56-133">İlke toospecify nasıl fiziksel ayarladığınız sunucuları çoğaltır.</span><span class="sxs-lookup"><span data-stu-id="15c56-133">You set up a policy toospecify how physical servers should replicate.</span></span>

<span data-ttu-id="15c56-134">Çok Git[adım 8: bir çoğaltma ilkesini ayarlayın](physical-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="15c56-134">Go too[Step 8: Set up a replication policy](physical-walkthrough-replication.md)</span></span>

## <a name="step-9-install-hello-mobility-service"></a><span data-ttu-id="15c56-135">9. adım: hello Mobility hizmetini yükleme</span><span class="sxs-lookup"><span data-stu-id="15c56-135">Step 9: Install hello Mobility service</span></span>

<span data-ttu-id="15c56-136">Merhaba mobilite hizmetinin yüklenmesi tooreplicate istediğiniz her sunucuda.</span><span class="sxs-lookup"><span data-stu-id="15c56-136">hello Mobility service must be installed on each server you want tooreplicate.</span></span> <span data-ttu-id="15c56-137">Merhaba hizmetiyle iterek ister çekerek yükleme yukarı birkaç yolu tooset vardır.</span><span class="sxs-lookup"><span data-stu-id="15c56-137">There are a few ways tooset up hello service, with push or pull installation.</span></span>

<span data-ttu-id="15c56-138">Çok Git[adım 9: hello Mobility hizmetini yükleme](physical-walkthrough-install-mobility.md)</span><span class="sxs-lookup"><span data-stu-id="15c56-138">Go too[Step 9: Install hello Mobility service](physical-walkthrough-install-mobility.md)</span></span>

## <a name="step-10-enable-replication"></a><span data-ttu-id="15c56-139">10. adım: Çoğaltma etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="15c56-139">Step 10: Enable replication</span></span>

<span data-ttu-id="15c56-140">Merhaba Mobility hizmeti bir sunucuda çalıştırdıktan sonra çoğaltmayı etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="15c56-140">After hello Mobility service is running on a server, you can enable replication for it.</span></span> <span data-ttu-id="15c56-141">Etkinleştirdikten sonra ilk çoğaltma işlemi hello VM oluşur.</span><span class="sxs-lookup"><span data-stu-id="15c56-141">After enabling, initial replication of hello VM occurs.</span></span>

<span data-ttu-id="15c56-142">Çok Git[adım 10: çoğaltmasını etkinleştir](physical-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="15c56-142">Go too[Step 10: Enable replication](physical-walkthrough-enable-replication.md)</span></span>

## <a name="step-11-run-a-test-failover"></a><span data-ttu-id="15c56-143">11. adım: yük devretme testi çalıştırma</span><span class="sxs-lookup"><span data-stu-id="15c56-143">Step 11: Run a test failover</span></span>

<span data-ttu-id="15c56-144">İlk çoğaltma sonlandırıldıktan sonra değişim çoğaltması çalıştığından, bir test yük devretme toomake her şeyin beklendiği gibi çalıştığından emin çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="15c56-144">After initial replication finishes and delta replication is running, you can run a test failover toomake sure everything works as expected.</span></span>

<span data-ttu-id="15c56-145">Çok Git[11. adım: yük devretme testi çalıştırma](physical-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="15c56-145">Go too[Step 11: Run a test failover](physical-walkthrough-test-failover.md)</span></span>

