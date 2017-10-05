---
title: "Replicate fiziksel şirket içi sunucular Azure Site Recovery ile azure'a | Microsoft Docs"
description: "Azure Site Recovery hizmeti ile Azure için şirket içi Windows/Linux fiziksel sunucularında çalışan iş yüklerini çoğaltmak için adımlara genel bir bakış sağlar."
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
ms.openlocfilehash: 0a09b35e98dc0b2f5283c2a707a3a2b8ac9a39f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-physical-servers-to-azure-with-site-recovery"></a><span data-ttu-id="c90d7-103">Azure Site Recovery ile fiziksel sunucuları çoğaltma</span><span class="sxs-lookup"><span data-stu-id="c90d7-103">Replicate physical servers to Azure with Site Recovery</span></span>

<span data-ttu-id="c90d7-104">Bu makalede Azure için şirket içi Windows/Linux fiziksel sunucuları çoğaltmak için gerekli adımlar genel bir bakış sağlar kullanarak [Azure Site Recovery](site-recovery-overview.md) Azure portalında hizmet.</span><span class="sxs-lookup"><span data-stu-id="c90d7-104">This article provides an overview of the steps required to replicate on-premises Windows/Linux physical servers to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>


## <a name="step-1-review-architecture-and-prerequisites"></a><span data-ttu-id="c90d7-105">1. adım: mimarisi ve önkoşulları gözden geçirin</span><span class="sxs-lookup"><span data-stu-id="c90d7-105">Step 1: Review architecture and prerequisites</span></span>

<span data-ttu-id="c90d7-106">Dağıtıma başlamadan önce senaryo mimarisinin gözden geçirin ve dağıtımı ayarlamak için gereken tüm bileşenleri anladığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="c90d7-106">Before you start deployment, review the scenario architecture, and make sure you understand all the components you need to set up the deployment.</span></span>

<span data-ttu-id="c90d7-107">Git [1. adım: mimarisi gözden geçirin](physical-walkthrough-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="c90d7-107">Go to [Step 1: Review the architecture](physical-walkthrough-architecture.md)</span></span>


## <a name="step-2-review-prerequisites"></a><span data-ttu-id="c90d7-108">2. adım: Gözden geçirme önkoşulları</span><span class="sxs-lookup"><span data-stu-id="c90d7-108">Step 2: Review prerequisites</span></span>

<span data-ttu-id="c90d7-109">Önkoşullar her dağıtım bileşen için yerinde olduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="c90d7-109">Make sure you have the prerequisites in place for each deployment component:</span></span>

- <span data-ttu-id="c90d7-110">**Azure önkoşulları**: bir Microsoft Azure hesabı, Azure ağları ve depolama hesapları gerekir.</span><span class="sxs-lookup"><span data-stu-id="c90d7-110">**Azure prerequisites**: You need a Microsoft Azure account, Azure networks, and storage accounts.</span></span>
- <span data-ttu-id="c90d7-111">**Şirket içi Site Recovery bileşenlerini**: şirket içi Site Recovery bileşenlerini çalıştıran bir makineye gerekir.</span><span class="sxs-lookup"><span data-stu-id="c90d7-111">**On-premises Site Recovery components**: You need a machine running on-premises Site Recovery components.</span></span>
- <span data-ttu-id="c90d7-112">**Makineler çoğaltılan**: sunucuları çoğaltmak istediğiniz şirket içi ve Azure gereksinimleri uymak gerekir.</span><span class="sxs-lookup"><span data-stu-id="c90d7-112">**Replicated machines**: Servers you want to replicate need to comply with on-premises and Azure requirements.</span></span>

<span data-ttu-id="c90d7-113">Git [2. adım: gözden Önkoşullar ve sınırlamalar](physical-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="c90d7-113">Go to [Step 2: Review prerequisites and limitations](physical-walkthrough-prerequisites.md)</span></span>

## <a name="step-3-plan-capacity"></a><span data-ttu-id="c90d7-114">3. adım: Planı kapasite</span><span class="sxs-lookup"><span data-stu-id="c90d7-114">Step 3: Plan capacity</span></span>

<span data-ttu-id="c90d7-115">Tam dağıtımını yaptığınız ihtiyacınız hangi çoğaltma kaynakları şekil gerekir.</span><span class="sxs-lookup"><span data-stu-id="c90d7-115">If you're doing a full deployment you need to figure out what replication resources you need.</span></span> <span data-ttu-id="c90d7-116">Test ortamı için ayarladığınız hızlı yaptığınız varsa, bu adımı atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c90d7-116">If you're doing a quick set up to test the environment, you can skip this step.</span></span>

<span data-ttu-id="c90d7-117">[3. Adım: Kapasiteyi planlama](physical-walkthrough-capacity.md)’ya gidin.</span><span class="sxs-lookup"><span data-stu-id="c90d7-117">Go to [Step 3: Plan capacity](physical-walkthrough-capacity.md)</span></span>

## <a name="step-4-plan-networking"></a><span data-ttu-id="c90d7-118">4. adım: ağ planlama</span><span class="sxs-lookup"><span data-stu-id="c90d7-118">Step 4: Plan networking</span></span>

<span data-ttu-id="c90d7-119">Bazı ağ yük devretme gerçekleştikten sonra sahip oldukları doğru IP adreslerini Azure Vm'lerinin ağlara bağlandığından emin olmak planlama yapmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c90d7-119">You need to do some network planning to ensure that Azure VMs are connected to networks after failover occurs, and  that that they have the right IP addresses.</span></span>

<span data-ttu-id="c90d7-120">Git [4. adım: ağ planı](physical-walkthrough-network.md)</span><span class="sxs-lookup"><span data-stu-id="c90d7-120">Go to [Step 4: Plan networking](physical-walkthrough-network.md)</span></span>

##  <a name="step-5-prepare-azure-resources"></a><span data-ttu-id="c90d7-121">5. adım: Azure kaynaklarını hazırlama</span><span class="sxs-lookup"><span data-stu-id="c90d7-121">Step 5: Prepare Azure resources</span></span>

<span data-ttu-id="c90d7-122">Başlamadan önce Azure ağları ve depolama ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="c90d7-122">Set up Azure networks and storage before you start.</span></span> 

<span data-ttu-id="c90d7-123">Git [5. adım: Azure hazırlama](physical-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="c90d7-123">Go to [Step 5: Prepare Azure](physical-walkthrough-prepare-azure.md)</span></span>


## <a name="step-6-set-up-a-vault"></a><span data-ttu-id="c90d7-124">6. adım: Bir kasa ayarlama</span><span class="sxs-lookup"><span data-stu-id="c90d7-124">Step 6: Set up a vault</span></span>

<span data-ttu-id="c90d7-125">Düzenlemek ve çoğaltmayı yönetmek için bir kurtarma Hizmetleri kasasını ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="c90d7-125">You set up a Recovery Services vault to orchestrate and manage replication.</span></span> <span data-ttu-id="c90d7-126">Kasasını ayarladığınızda, çoğaltmak istediğiniz ve kendisine çoğaltmak istediğiniz yeri belirtin.</span><span class="sxs-lookup"><span data-stu-id="c90d7-126">When you set up the vault, you specify what you want to replicate, and where you want to replicate it to.</span></span>

<span data-ttu-id="c90d7-127">Git [adım 6: bir kasasını oluşturup](physical-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="c90d7-127">Go to [Step 6: Set up a vault](physical-walkthrough-create-vault.md)</span></span>

## <a name="step-7-configure-source-and-target-settings"></a><span data-ttu-id="c90d7-128">7. adım: kaynak ve hedef ayarlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="c90d7-128">Step 7: Configure source and target settings</span></span>

<span data-ttu-id="c90d7-129">(Azure) site hedef ve kaynak için ayarları yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="c90d7-129">Configure settings for the source and target (Azure) site.</span></span> <span data-ttu-id="c90d7-130">Kaynak ayarları birleşik şirket içi Site Recovery bileşenlerini yüklemek için Kurulumu çalıştıran içerir.</span><span class="sxs-lookup"><span data-stu-id="c90d7-130">Source settings includes running Unified Setup to install the on-premises Site Recovery components.</span></span>

<span data-ttu-id="c90d7-131">Git [adım 7: kaynak ve hedef ayarlama](physical-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="c90d7-131">Go to [Step 7: Set up the source and target](physical-walkthrough-source-target.md)</span></span>

## <a name="step-8-set-up-a-replication-policy"></a><span data-ttu-id="c90d7-132">8. adım: Bir çoğaltma ilkesi ayarlama</span><span class="sxs-lookup"><span data-stu-id="c90d7-132">Step 8: Set up a replication policy</span></span>

<span data-ttu-id="c90d7-133">Ayarladığınız nasıl fiziksel sunucuları belirtmek için bir ilke çoğaltılması.</span><span class="sxs-lookup"><span data-stu-id="c90d7-133">You set up a policy to specify how physical servers should replicate.</span></span>

<span data-ttu-id="c90d7-134">Git [adım 8: bir çoğaltma ilkesini ayarlayın](physical-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="c90d7-134">Go to [Step 8: Set up a replication policy](physical-walkthrough-replication.md)</span></span>

## <a name="step-9-install-the-mobility-service"></a><span data-ttu-id="c90d7-135">9. adım: mobilite hizmeti yükleme</span><span class="sxs-lookup"><span data-stu-id="c90d7-135">Step 9: Install the Mobility service</span></span>

<span data-ttu-id="c90d7-136">Mobility hizmetinin çoğaltmak istediğiniz her sunucuda yüklenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="c90d7-136">The Mobility service must be installed on each server you want to replicate.</span></span> <span data-ttu-id="c90d7-137">Hizmetle iterek ister çekerek yükleme ayarlamak için birkaç yolu vardır.</span><span class="sxs-lookup"><span data-stu-id="c90d7-137">There are a few ways to set up the service, with push or pull installation.</span></span>

<span data-ttu-id="c90d7-138">Git [adım 9: Mobility hizmetini yükleme](physical-walkthrough-install-mobility.md)</span><span class="sxs-lookup"><span data-stu-id="c90d7-138">Go to [Step 9: Install the Mobility service](physical-walkthrough-install-mobility.md)</span></span>

## <a name="step-10-enable-replication"></a><span data-ttu-id="c90d7-139">10. adım: Çoğaltma etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="c90d7-139">Step 10: Enable replication</span></span>

<span data-ttu-id="c90d7-140">Mobility hizmeti bir sunucuda çalışmaya başladıktan sonra çoğaltmayı etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c90d7-140">After the Mobility service is running on a server, you can enable replication for it.</span></span> <span data-ttu-id="c90d7-141">Etkinleştirdikten sonra VM başlangıç çoğaltması gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="c90d7-141">After enabling, initial replication of the VM occurs.</span></span>

<span data-ttu-id="c90d7-142">Git [adım 10: çoğaltmasını etkinleştir](physical-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="c90d7-142">Go to [Step 10: Enable replication](physical-walkthrough-enable-replication.md)</span></span>

## <a name="step-11-run-a-test-failover"></a><span data-ttu-id="c90d7-143">11. adım: yük devretme testi çalıştırma</span><span class="sxs-lookup"><span data-stu-id="c90d7-143">Step 11: Run a test failover</span></span>

<span data-ttu-id="c90d7-144">İlk çoğaltma sonlandırıldıktan sonra değişim çoğaltması çalıştığından, her şeyin beklendiği gibi çalıştığından emin olmak için yük devretme testi çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c90d7-144">After initial replication finishes and delta replication is running, you can run a test failover to make sure everything works as expected.</span></span>

<span data-ttu-id="c90d7-145">Git [11. adım: yük devretme testi çalıştırma](physical-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="c90d7-145">Go to [Step 11: Run a test failover](physical-walkthrough-test-failover.md)</span></span>

