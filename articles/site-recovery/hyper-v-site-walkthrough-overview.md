---
title: Azure Site Recovery ile aaaReplicate Hyper-V sanal makineleri tooAzure | Microsoft Docs
description: "Açıklar nasıl tooorchestrate çoğaltma, yük devretme ve kurtarma işlemlerini şirket içi Hyper-V sanal makineleri tooAzure"
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
ms.openlocfilehash: ab9cd14149ef32a416428d0f4327aa18b042e9c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-without-vmm-tooazure"></a><span data-ttu-id="71155-103">Hyper-V sanal makineleri (VMM olmadan) tooAzure Çoğalt</span><span class="sxs-lookup"><span data-stu-id="71155-103">Replicate Hyper-V virtual machines (without VMM) tooAzure</span></span> 

> [!div class="op_single_selector"]
> * [<span data-ttu-id="71155-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="71155-104">Azure portal</span></span>](site-recovery-hyper-v-site-to-azure.md)
> * [<span data-ttu-id="71155-105">Azure klasik</span><span class="sxs-lookup"><span data-stu-id="71155-105">Azure classic</span></span>](site-recovery-hyper-v-site-to-azure-classic.md)
> * [<span data-ttu-id="71155-106">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="71155-106">PowerShell - Resource Manager</span></span>](site-recovery-deploy-with-powershell-resource-manager.md)
>
>

<span data-ttu-id="71155-107">Bu makalede hello kullanarak hello gerekli adımları tooreplicate şirket içi Hyper-V sanal makineleri tooAzure, genel bir bakış sağlar [Azure Site Recovery](site-recovery-overview.md) hello Azure Portalı'nda.</span><span class="sxs-lookup"><span data-stu-id="71155-107">This article provides an overview of hello steps required tooreplicate on-premises Hyper-V virtual machines tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) in hello Azure portal.</span></span> <span data-ttu-id="71155-108">Bu dağıtım Hyper-V VM System Center Virtual Machine Manager (VMM) tarafından yönetilmiyor.</span><span class="sxs-lookup"><span data-stu-id="71155-108">In this deployment Hyper-V VMs aren't managed by System Center Virtual Machine Manager (VMM).</span></span>


<span data-ttu-id="71155-109">Bu makaleyi okuduktan sonra hello altındaki tüm yorumlar post veya üzerinde hello teknik sorular sormak [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="71155-109">After reading this article, post any comments at hello bottom, or ask technical questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="step-1-review-architecture-and-prerequisites"></a><span data-ttu-id="71155-110">1. adım: mimarisi ve önkoşulları gözden geçirin</span><span class="sxs-lookup"><span data-stu-id="71155-110">Step 1: Review architecture and prerequisites</span></span>

<span data-ttu-id="71155-111">Dağıtıma başlamadan önce hello senaryo mimarisinin gözden geçirin ve toodeploy gerek duyduğunuz tüm hello bileşenleri anladığınızdan emin olun</span><span class="sxs-lookup"><span data-stu-id="71155-111">Before you start deployment, review hello scenario architecture, and make sure you understand all hello components you need toodeploy</span></span>

<span data-ttu-id="71155-112">Çok Git[1. adım: gözden hello mimarisi](hyper-v-site-walkthrough-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="71155-112">Go too[Step 1: Review hello architecture](hyper-v-site-walkthrough-architecture.md)</span></span>


## <a name="step-2-review-prerequisites"></a><span data-ttu-id="71155-113">2. adım: Gözden geçirme önkoşulları</span><span class="sxs-lookup"><span data-stu-id="71155-113">Step 2: Review prerequisites</span></span>

<span data-ttu-id="71155-114">Merhaba Önkoşullar her dağıtım bileşen için yerinde olduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="71155-114">Make sure you have hello prerequisites in place for each deployment component:</span></span>

- <span data-ttu-id="71155-115">**Azure önkoşulları**: bir Microsoft Azure hesabı, Azure ağları ve depolama hesapları gerekir.</span><span class="sxs-lookup"><span data-stu-id="71155-115">**Azure prerequisites**: You need a Microsoft Azure account, Azure networks, and storage accounts.</span></span>
- <span data-ttu-id="71155-116">**Şirket içi Hyper-V önkoşulları**: Hyper-V konakları Site Recovery dağıtımı için hazır olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="71155-116">**On-premises Hyper-V prerequisites**: Make sure Hyper-V hosts are prepared for Site Recovery deployment.</span></span>
- <span data-ttu-id="71155-117">**Çoğaltılan VM'ler**: istediğiniz tooreplicate gerek toocomply Azure gereksinimleri olan VM'ler.</span><span class="sxs-lookup"><span data-stu-id="71155-117">**Replicated VMs**: VMs you want tooreplicate need toocomply with Azure requirements.</span></span>

<span data-ttu-id="71155-118">Çok Git[2. adım: Önkoşullar ve sınırlamalar doğrulayın](hyper-v-site-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="71155-118">Go too[Step 2: Verify prerequisites and limitations](hyper-v-site-walkthrough-prerequisites.md)</span></span>

## <a name="step-3-plan-capacity"></a><span data-ttu-id="71155-119">3. adım: Planı kapasite</span><span class="sxs-lookup"><span data-stu-id="71155-119">Step 3: Plan capacity</span></span>

<span data-ttu-id="71155-120">Tam dağıtımını yaptığınız ihtiyacınız hangi çoğaltma kaynakları çıkışı toofigure gerekir.</span><span class="sxs-lookup"><span data-stu-id="71155-120">If you're doing a full deployment you need toofigure out what replication resources you need.</span></span> <span data-ttu-id="71155-121">Birkaç vardır Araçlar kullanılabilir toohelp bunu.</span><span class="sxs-lookup"><span data-stu-id="71155-121">There are a couple of tools available toohelp you do this.</span></span> <span data-ttu-id="71155-122">TooStep 2 gidin.</span><span class="sxs-lookup"><span data-stu-id="71155-122">Go tooStep 2.</span></span> <span data-ttu-id="71155-123">Tootest hello ortamını ayarlama hızlı yaptığınız varsa bu adımı atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="71155-123">If you're doing a quick set up tootest hello environment you can skip this step.</span></span>

<span data-ttu-id="71155-124">Çok Git[3. adım: kapasite planlama](hyper-v-site-walkthrough-capacity.md)</span><span class="sxs-lookup"><span data-stu-id="71155-124">Go too[Step 3: Plan capacity](hyper-v-site-walkthrough-capacity.md)</span></span>

## <a name="step-4-plan-networking"></a><span data-ttu-id="71155-125">4. adım: ağ planlama</span><span class="sxs-lookup"><span data-stu-id="71155-125">Step 4: Plan networking</span></span>

<span data-ttu-id="71155-126">Yük devretme gerçekleştikten sonra Azure Vm'lerinin bağlı toonetworks olduğunu ve sahip oldukları hello doğru IP adreslerine tooensure planlama bazı ağ toodo gerekir.</span><span class="sxs-lookup"><span data-stu-id="71155-126">You need toodo some network planning tooensure that Azure VMs are connected toonetworks after failover occurs, and  that that they have hello right IP addresses.</span></span>

<span data-ttu-id="71155-127">Çok Git[4. adım: ağ planı](hyper-v-site-walkthrough-network.md)</span><span class="sxs-lookup"><span data-stu-id="71155-127">Go too[Step 4: Plan networking](hyper-v-site-walkthrough-network.md)</span></span>

##  <a name="step-5-prepare-azure-resources"></a><span data-ttu-id="71155-128">5. adım: Azure kaynaklarını hazırlama</span><span class="sxs-lookup"><span data-stu-id="71155-128">Step 5: Prepare Azure resources</span></span>

<span data-ttu-id="71155-129">Başlamadan önce Azure ağları ve depolama ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="71155-129">Set up Azure networks and storage before you start.</span></span> <span data-ttu-id="71155-130">Dağıtım sırasında bunu yapabilirsiniz ancak başlamadan önce bunu öneririz.</span><span class="sxs-lookup"><span data-stu-id="71155-130">You can do this during deployment, but we recommend you do this before you start.</span></span>

<span data-ttu-id="71155-131">Çok Git[5. adım: Azure hazırlama](hyper-v-site-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="71155-131">Go too[Step 5: Prepare Azure](hyper-v-site-walkthrough-prepare-azure.md)</span></span>


## <a name="step-6-prepare-hyper-v"></a><span data-ttu-id="71155-132">6. adım: Hyper-V hazırlama</span><span class="sxs-lookup"><span data-stu-id="71155-132">Step 6: Prepare Hyper-V</span></span>

<span data-ttu-id="71155-133">Hyper-V sunucuları Site Recovery dağıtım gereksinimleri karşıladığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="71155-133">Make sure that Hyper-V servers meet Site Recovery deployment requirements.</span></span>

<span data-ttu-id="71155-134">Çok Git[adım 6: Hyper-V hazırlama](hyper-v-site-walkthrough-prepare-hyper-v.md)</span><span class="sxs-lookup"><span data-stu-id="71155-134">Go too[Step 6: Prepare Hyper-V](hyper-v-site-walkthrough-prepare-hyper-v.md)</span></span>

## <a name="step-7-set-up-a-vault"></a><span data-ttu-id="71155-135">7. adım: Bir kasa ayarlama</span><span class="sxs-lookup"><span data-stu-id="71155-135">Step 7: Set up a vault</span></span>

<span data-ttu-id="71155-136">Çoğaltmayı yönetmek ve bir kurtarma Hizmetleri kasası tooorchestrate yukarı tooset gerekir.</span><span class="sxs-lookup"><span data-stu-id="71155-136">You need tooset up a Recovery Services vault tooorchestrate and manage replication.</span></span> <span data-ttu-id="71155-137">Merhaba kasasını ayarladığınızda, istediğinizi belirtin tooreplicate, ve tooreplicate istediğiniz şekilde.</span><span class="sxs-lookup"><span data-stu-id="71155-137">When you set up hello vault, you specify what you want tooreplicate, and where you want tooreplicate it to.</span></span>

<span data-ttu-id="71155-138">Çok Git[adım 7: bir kasa oluşturun](hyper-v-site-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="71155-138">Go too[Step 7: Create a vault](hyper-v-site-walkthrough-create-vault.md)</span></span>

## <a name="step-8-configure-source-and-target-settings"></a><span data-ttu-id="71155-139">8. adım: kaynak ve hedef ayarlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="71155-139">Step 8: Configure source and target settings</span></span>

<span data-ttu-id="71155-140">Merhaba kaynak ve çoğaltma için kullanılan hedef ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="71155-140">Set up hello source and target that's used for replication.</span></span> <span data-ttu-id="71155-141">Kaynak ayarları ayarı, her Hyper-V ana bilgisayarda hello Site Recovery sağlayıcısı ve kurtarma Hizmetleri aracısını yükleme ve hello site kurtarma Hizmetleri kasası hello kaydetme Hyper-V konakları tooa Hyper-V sitesi eklemeyi içerir.</span><span class="sxs-lookup"><span data-stu-id="71155-141">Setting up source settings includes adding Hyper-V hosts tooa Hyper-V site, installing hello Site Recovery Provider and Recovery Services agent on each Hyper-V host, and registering hello site in hello Recovery Services vault.</span></span>

<span data-ttu-id="71155-142">Çok Git[adım 8: hello kaynak ve hedef ayarlama](hyper-v-site-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="71155-142">Go too[Step 8: Set up hello source and target](hyper-v-site-walkthrough-source-target.md)</span></span>

## <a name="step-9-set-up-a-replication-policy"></a><span data-ttu-id="71155-143">9. adım: Bir çoğaltma ilkesi ayarlama</span><span class="sxs-lookup"><span data-stu-id="71155-143">Step 9: Set up a replication policy</span></span>

<span data-ttu-id="71155-144">Merhaba kasasına Hyper-V VM'ler için bir ilke toospecify çoğaltma ayarlarını belirleme.</span><span class="sxs-lookup"><span data-stu-id="71155-144">You set up a policy toospecify replication settings for Hyper-V VMs in hello vault.</span></span>

<span data-ttu-id="71155-145">Çok Git[adım 9: bir çoğaltma ilkesini ayarlayın](hyper-v-site-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="71155-145">Go too[Step 9: Set up a replication policy](hyper-v-site-walkthrough-replication.md)</span></span>


## <a name="step-10-enable-replication"></a><span data-ttu-id="71155-146">10. adım: Çoğaltma etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="71155-146">Step 10: Enable replication</span></span>

<span data-ttu-id="71155-147">Etkinleştirdikten sonra yerinde bir çoğaltma ilkesi oluşturduktan sonra ilk çoğaltmasının hello VM oluşur.</span><span class="sxs-lookup"><span data-stu-id="71155-147">After you have a replication policy in place,  After enabling, initial replication of hello VM occurs.</span></span>

<span data-ttu-id="71155-148">Çok Git[adım 10: çoğaltmasını etkinleştir](hyper-v-site-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="71155-148">Go too[Step 10: Enable replication](hyper-v-site-walkthrough-enable-replication.md)</span></span>

## <a name="step-11-run-a-test-failover"></a><span data-ttu-id="71155-149">11. adım: yük devretme testi çalıştırma</span><span class="sxs-lookup"><span data-stu-id="71155-149">Step 11: Run a test failover</span></span>

<span data-ttu-id="71155-150">İlk çoğaltma sonlandırıldıktan ve değişim çoğaltması çalıştıran sonra her şeyin beklendiği gibi çalıştığından emin bir test yük devretme toomake çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="71155-150">After initial replication finishes, and delta replication is running, you can run a test failover toomake sure everything works as expected.</span></span>

<span data-ttu-id="71155-151">Çok Git[11. adım: yük devretme testi çalıştırma](hyper-v-site-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="71155-151">Go too[Step 11: Run a test failover](hyper-v-site-walkthrough-test-failover.md)</span></span>
