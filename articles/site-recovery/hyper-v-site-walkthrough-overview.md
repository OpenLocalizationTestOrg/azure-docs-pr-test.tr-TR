---
title: "Hyper-V sanal makineleri Azure Site Recovery ile Azure'a çoğaltma | Microsoft Docs"
description: "Çoğaltma, yük devretme ve şirket içi Hyper-V sanal makineleri kurtarma Azure düzenlendiğini açıklar"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: efddd986-bc13-4a1d-932d-5484cdc7ad8d
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: da10b213bc2543942b5ac77cf5c5d8547c00220c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-hyper-v-virtual-machines-without-vmm-to-azure"></a><span data-ttu-id="777a4-103">Hyper-V sanal makinelerini (VMM olmadan) Azure'a çoğaltma</span><span class="sxs-lookup"><span data-stu-id="777a4-103">Replicate Hyper-V virtual machines (without VMM) to Azure</span></span> 

> [!div class="op_single_selector"]
> * [<span data-ttu-id="777a4-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="777a4-104">Azure portal</span></span>](site-recovery-hyper-v-site-to-azure.md)
> * [<span data-ttu-id="777a4-105">Azure klasik</span><span class="sxs-lookup"><span data-stu-id="777a4-105">Azure classic</span></span>](site-recovery-hyper-v-site-to-azure-classic.md)
> * [<span data-ttu-id="777a4-106">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="777a4-106">PowerShell - Resource Manager</span></span>](site-recovery-deploy-with-powershell-resource-manager.md)
>
>

<span data-ttu-id="777a4-107">Bu makalede Azure için şirket içi Hyper-V sanal makineleri çoğaltmak için gerekli olan adımları genel bir bakış sağlar kullanarak [Azure Site Recovery](site-recovery-overview.md) Azure portalında.</span><span class="sxs-lookup"><span data-stu-id="777a4-107">This article provides an overview of the steps required to replicate on-premises Hyper-V virtual machines to Azure, using the [Azure Site Recovery](site-recovery-overview.md) in the Azure portal.</span></span> <span data-ttu-id="777a4-108">Bu dağıtım Hyper-V VM System Center Virtual Machine Manager (VMM) tarafından yönetilmiyor.</span><span class="sxs-lookup"><span data-stu-id="777a4-108">In this deployment Hyper-V VMs aren't managed by System Center Virtual Machine Manager (VMM).</span></span>


<span data-ttu-id="777a4-109">Bu makaleyi okuduktan sonra altındaki bir yorum gönderin ya da teknik sorular [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="777a4-109">After reading this article, post any comments at the bottom, or ask technical questions on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="step-1-review-architecture-and-prerequisites"></a><span data-ttu-id="777a4-110">1. adım: mimarisi ve önkoşulları gözden geçirin</span><span class="sxs-lookup"><span data-stu-id="777a4-110">Step 1: Review architecture and prerequisites</span></span>

<span data-ttu-id="777a4-111">Dağıtıma başlamadan önce senaryo mimarisinin gözden geçirin ve dağıtmak için gereken tüm bileşenleri anladığınızdan emin olun</span><span class="sxs-lookup"><span data-stu-id="777a4-111">Before you start deployment, review the scenario architecture, and make sure you understand all the components you need to deploy</span></span>

<span data-ttu-id="777a4-112">Git [1. adım: mimarisi gözden geçirin](hyper-v-site-walkthrough-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="777a4-112">Go to [Step 1: Review the architecture](hyper-v-site-walkthrough-architecture.md)</span></span>


## <a name="step-2-review-prerequisites"></a><span data-ttu-id="777a4-113">2. adım: Gözden geçirme önkoşulları</span><span class="sxs-lookup"><span data-stu-id="777a4-113">Step 2: Review prerequisites</span></span>

<span data-ttu-id="777a4-114">Önkoşullar her dağıtım bileşen için yerinde olduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="777a4-114">Make sure you have the prerequisites in place for each deployment component:</span></span>

- <span data-ttu-id="777a4-115">**Azure önkoşulları**: bir Microsoft Azure hesabı, Azure ağları ve depolama hesapları gerekir.</span><span class="sxs-lookup"><span data-stu-id="777a4-115">**Azure prerequisites**: You need a Microsoft Azure account, Azure networks, and storage accounts.</span></span>
- <span data-ttu-id="777a4-116">**Şirket içi Hyper-V önkoşulları**: Hyper-V konakları Site Recovery dağıtımı için hazır olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="777a4-116">**On-premises Hyper-V prerequisites**: Make sure Hyper-V hosts are prepared for Site Recovery deployment.</span></span>
- <span data-ttu-id="777a4-117">**Çoğaltılan VM'ler**: çoğaltmak istediğiniz sanal makineleri gereken Azure gereksinimlerine uymak.</span><span class="sxs-lookup"><span data-stu-id="777a4-117">**Replicated VMs**: VMs you want to replicate need to comply with Azure requirements.</span></span>

<span data-ttu-id="777a4-118">Git [2. adım: Önkoşullar ve sınırlamalar doğrulayın](hyper-v-site-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="777a4-118">Go to [Step 2: Verify prerequisites and limitations](hyper-v-site-walkthrough-prerequisites.md)</span></span>

## <a name="step-3-plan-capacity"></a><span data-ttu-id="777a4-119">3. adım: Planı kapasite</span><span class="sxs-lookup"><span data-stu-id="777a4-119">Step 3: Plan capacity</span></span>

<span data-ttu-id="777a4-120">Tam dağıtımını yaptığınız ihtiyacınız hangi çoğaltma kaynakları şekil gerekir.</span><span class="sxs-lookup"><span data-stu-id="777a4-120">If you're doing a full deployment you need to figure out what replication resources you need.</span></span> <span data-ttu-id="777a4-121">Birkaç bu yapmanıza yardımcı olmak için kullanılabilen araçlar vardır.</span><span class="sxs-lookup"><span data-stu-id="777a4-121">There are a couple of tools available to help you do this.</span></span> <span data-ttu-id="777a4-122">2. adıma geçin.</span><span class="sxs-lookup"><span data-stu-id="777a4-122">Go to Step 2.</span></span> <span data-ttu-id="777a4-123">Hızlı kümesi yaptığınız yukarı test ortamı için bu adımı atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="777a4-123">If you're doing a quick set up to test the environment you can skip this step.</span></span>

<span data-ttu-id="777a4-124">[3. Adım: Kapasiteyi planlama](hyper-v-site-walkthrough-capacity.md)’ya gidin.</span><span class="sxs-lookup"><span data-stu-id="777a4-124">Go to [Step 3: Plan capacity](hyper-v-site-walkthrough-capacity.md)</span></span>

## <a name="step-4-plan-networking"></a><span data-ttu-id="777a4-125">4. adım: ağ planlama</span><span class="sxs-lookup"><span data-stu-id="777a4-125">Step 4: Plan networking</span></span>

<span data-ttu-id="777a4-126">Bazı ağ yük devretme gerçekleştikten sonra sahip oldukları doğru IP adreslerini Azure Vm'lerinin ağlara bağlandığından emin olmak planlama yapmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="777a4-126">You need to do some network planning to ensure that Azure VMs are connected to networks after failover occurs, and  that that they have the right IP addresses.</span></span>

<span data-ttu-id="777a4-127">Git [4. adım: ağ planı](hyper-v-site-walkthrough-network.md)</span><span class="sxs-lookup"><span data-stu-id="777a4-127">Go to [Step 4: Plan networking](hyper-v-site-walkthrough-network.md)</span></span>

##  <a name="step-5-prepare-azure-resources"></a><span data-ttu-id="777a4-128">5. adım: Azure kaynaklarını hazırlama</span><span class="sxs-lookup"><span data-stu-id="777a4-128">Step 5: Prepare Azure resources</span></span>

<span data-ttu-id="777a4-129">Başlamadan önce Azure ağları ve depolama ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="777a4-129">Set up Azure networks and storage before you start.</span></span> <span data-ttu-id="777a4-130">Dağıtım sırasında bunu yapabilirsiniz ancak başlamadan önce bunu öneririz.</span><span class="sxs-lookup"><span data-stu-id="777a4-130">You can do this during deployment, but we recommend you do this before you start.</span></span>

<span data-ttu-id="777a4-131">Git [5. adım: Azure hazırlama](hyper-v-site-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="777a4-131">Go to [Step 5: Prepare Azure](hyper-v-site-walkthrough-prepare-azure.md)</span></span>


## <a name="step-6-prepare-hyper-v"></a><span data-ttu-id="777a4-132">6. adım: Hyper-V hazırlama</span><span class="sxs-lookup"><span data-stu-id="777a4-132">Step 6: Prepare Hyper-V</span></span>

<span data-ttu-id="777a4-133">Hyper-V sunucuları Site Recovery dağıtım gereksinimleri karşıladığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="777a4-133">Make sure that Hyper-V servers meet Site Recovery deployment requirements.</span></span>

<span data-ttu-id="777a4-134">Git [6. adım: Hyper-V hazırlama](hyper-v-site-walkthrough-prepare-hyper-v.md)</span><span class="sxs-lookup"><span data-stu-id="777a4-134">Go to [Step 6: Prepare Hyper-V](hyper-v-site-walkthrough-prepare-hyper-v.md)</span></span>

## <a name="step-7-set-up-a-vault"></a><span data-ttu-id="777a4-135">7. adım: Bir kasa ayarlama</span><span class="sxs-lookup"><span data-stu-id="777a4-135">Step 7: Set up a vault</span></span>

<span data-ttu-id="777a4-136">Düzenlemek ve çoğaltmayı yönetmek için bir kurtarma Hizmetleri kasasını ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="777a4-136">You need to set up a Recovery Services vault to orchestrate and manage replication.</span></span> <span data-ttu-id="777a4-137">Kasasını ayarladığınızda, çoğaltmak istediğiniz ve kendisine çoğaltmak istediğiniz yeri belirtin.</span><span class="sxs-lookup"><span data-stu-id="777a4-137">When you set up the vault, you specify what you want to replicate, and where you want to replicate it to.</span></span>

<span data-ttu-id="777a4-138">Git [adım 7: bir kasa oluşturun](hyper-v-site-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="777a4-138">Go to [Step 7: Create a vault](hyper-v-site-walkthrough-create-vault.md)</span></span>

## <a name="step-8-configure-source-and-target-settings"></a><span data-ttu-id="777a4-139">8. adım: kaynak ve hedef ayarlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="777a4-139">Step 8: Configure source and target settings</span></span>

<span data-ttu-id="777a4-140">Kaynak ve çoğaltma için kullanılan hedef ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="777a4-140">Set up the source and target that's used for replication.</span></span> <span data-ttu-id="777a4-141">Kaynak ayarları kurma, bir Hyper-V sitesi için Site Recovery sağlayıcısı ve kurtarma Hizmetleri Aracısı her Hyper-V ana bilgisayarda yükleme ve site kurtarma Hizmetleri kasaya kaydetmeyi Hyper-V konakları eklemeyi içerir.</span><span class="sxs-lookup"><span data-stu-id="777a4-141">Setting up source settings includes adding Hyper-V hosts to a Hyper-V site, installing the Site Recovery Provider and Recovery Services agent on each Hyper-V host, and registering the site in the Recovery Services vault.</span></span>

<span data-ttu-id="777a4-142">Git [adım 8: kaynak ve hedef ayarlama](hyper-v-site-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="777a4-142">Go to [Step 8: Set up the source and target](hyper-v-site-walkthrough-source-target.md)</span></span>

## <a name="step-9-set-up-a-replication-policy"></a><span data-ttu-id="777a4-143">9. adım: Bir çoğaltma ilkesi ayarlama</span><span class="sxs-lookup"><span data-stu-id="777a4-143">Step 9: Set up a replication policy</span></span>

<span data-ttu-id="777a4-144">Hyper-V sanal makineleri için çoğaltma ayarlarını kasaya belirtmek için bir ilke ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="777a4-144">You set up a policy to specify replication settings for Hyper-V VMs in the vault.</span></span>

<span data-ttu-id="777a4-145">Git [adım 9: bir çoğaltma ilkesini ayarlayın](hyper-v-site-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="777a4-145">Go to [Step 9: Set up a replication policy](hyper-v-site-walkthrough-replication.md)</span></span>


## <a name="step-10-enable-replication"></a><span data-ttu-id="777a4-146">10. adım: Çoğaltma etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="777a4-146">Step 10: Enable replication</span></span>

<span data-ttu-id="777a4-147">Etkinleştirildikten sonra bir çoğaltma ilkesi yerinde aldıktan sonra VM başlangıç çoğaltması gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="777a4-147">After you have a replication policy in place,  After enabling, initial replication of the VM occurs.</span></span>

<span data-ttu-id="777a4-148">Git [adım 10: çoğaltmasını etkinleştir](hyper-v-site-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="777a4-148">Go to [Step 10: Enable replication](hyper-v-site-walkthrough-enable-replication.md)</span></span>

## <a name="step-11-run-a-test-failover"></a><span data-ttu-id="777a4-149">11. adım: yük devretme testi çalıştırma</span><span class="sxs-lookup"><span data-stu-id="777a4-149">Step 11: Run a test failover</span></span>

<span data-ttu-id="777a4-150">İlk çoğaltma sonlandırıldıktan ve değişim çoğaltması çalıştıran sonra her şeyin beklendiği gibi çalıştığından emin olmak için yük devretme testi çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="777a4-150">After initial replication finishes, and delta replication is running, you can run a test failover to make sure everything works as expected.</span></span>

<span data-ttu-id="777a4-151">Git [11. adım: yük devretme testi çalıştırma](hyper-v-site-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="777a4-151">Go to [Step 11: Run a test failover](hyper-v-site-walkthrough-test-failover.md)</span></span>
