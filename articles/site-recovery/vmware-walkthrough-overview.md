---
title: Azure Site Recovery ile aaaReplicate VMware Vm'lerini tooAzure | Microsoft Docs
description: "VMware Vm'leri tooAzure üzerinde çalışan iş yüklerini çoğaltmak için hello adımlara genel bir bakış sağlar"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: dab98aa5-9c41-4475-b7dc-2e07ab1cfd18
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 7104f67a3635b916048dcb61bca770c89f0c77fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-vmware-vms-tooazure-with-site-recovery"></a><span data-ttu-id="7d4ac-103">Site Recovery ile VMware Vm'lerini tooAzure Çoğalt</span><span class="sxs-lookup"><span data-stu-id="7d4ac-103">Replicate VMware VMs tooAzure with Site Recovery</span></span>

<span data-ttu-id="7d4ac-104">Bu makalede hello kullanarak hello adımları gerekli tooreplicate şirket içi VMware sanal makineleri tooAzure, genel bir bakış sağlar [Azure Site Recovery](site-recovery-overview.md) hello Azure portal hizmeti.</span><span class="sxs-lookup"><span data-stu-id="7d4ac-104">This article provides an overview of hello steps required tooreplicate on-premises VMware virtual machines tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>


![Dağıtım işlemi](./media/vmware-walkthrough-overview/vmware-to-azure-process.png)

<span data-ttu-id="7d4ac-106">**Şekil 1: Dağıtım işlemi özeti**</span><span class="sxs-lookup"><span data-stu-id="7d4ac-106">**Figure 1: Deployment process summary**</span></span>

## <a name="step-1-review-architecture-and-prerequisites"></a><span data-ttu-id="7d4ac-107">1. adım: mimarisi ve önkoşulları gözden geçirin</span><span class="sxs-lookup"><span data-stu-id="7d4ac-107">Step 1: Review architecture and prerequisites</span></span>

<span data-ttu-id="7d4ac-108">Dağıtıma başlamadan önce hello senaryo mimarisinin gözden geçirin ve toodeploy gerek duyduğunuz tüm hello bileşenleri anladığınızdan emin olun</span><span class="sxs-lookup"><span data-stu-id="7d4ac-108">Before you start deployment, review hello scenario architecture, and make sure you understand all hello components you need toodeploy</span></span>

<span data-ttu-id="7d4ac-109">Çok Git[1. adım: gözden hello mimarisi](vmware-walkthrough-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="7d4ac-109">Go too[Step 1: Review hello architecture](vmware-walkthrough-architecture.md)</span></span>


## <a name="step-2-review-prerequisites"></a><span data-ttu-id="7d4ac-110">2. adım: Gözden geçirme önkoşulları</span><span class="sxs-lookup"><span data-stu-id="7d4ac-110">Step 2: Review prerequisites</span></span>

<span data-ttu-id="7d4ac-111">Merhaba Önkoşullar her dağıtım bileşen için yerinde olduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="7d4ac-111">Make sure you have hello prerequisites in place for each deployment component:</span></span>

- <span data-ttu-id="7d4ac-112">**Azure önkoşulları**: bir Microsoft Azure hesabı, Azure ağları ve depolama hesapları gerekir.</span><span class="sxs-lookup"><span data-stu-id="7d4ac-112">**Azure prerequisites**: You need a Microsoft Azure account, Azure networks, and storage accounts.</span></span>
- <span data-ttu-id="7d4ac-113">**Şirket içi Site Recovery bileşenlerini**: şirket içi Site Recovery bileşenlerini çalıştıran bir makineye gerekir.</span><span class="sxs-lookup"><span data-stu-id="7d4ac-113">**On-premises Site Recovery components**: You need a machine running on-premises Site Recovery components.</span></span>
- <span data-ttu-id="7d4ac-114">**Şirket içi VMware Önkoşullar**: Site Recovery VMware sunucularını ve Vm'leri erişebilmesi için hesaplarını tooset gerekir.</span><span class="sxs-lookup"><span data-stu-id="7d4ac-114">**On-premises VMware prerequisites**: You need tooset up accounts so that Site Recovery can access VMware servers and VMs.</span></span>
- <span data-ttu-id="7d4ac-115">**Çoğaltılan VM'ler**: tooreplicate gerek toocomply Azure gereksinimleri ile istediğiniz ve hello Mobility hizmeti bileşeninin yüklü olan VM'ler.</span><span class="sxs-lookup"><span data-stu-id="7d4ac-115">**Replicated VMs**: VMs you want tooreplicate need toocomply with Azure requirements, and have hello Mobility service component installed.</span></span>

<span data-ttu-id="7d4ac-116">Çok Git[2. adım: gözden Önkoşullar ve sınırlamalar](vmware-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="7d4ac-116">Go too[Step 2: Review prerequisites and limitations](vmware-walkthrough-prerequisites.md)</span></span>

## <a name="step-3-plan-capacity"></a><span data-ttu-id="7d4ac-117">3. adım: Planı kapasite</span><span class="sxs-lookup"><span data-stu-id="7d4ac-117">Step 3: Plan capacity</span></span>

<span data-ttu-id="7d4ac-118">Tam dağıtımını yaptığınız ihtiyacınız hangi çoğaltma kaynakları çıkışı toofigure gerekir.</span><span class="sxs-lookup"><span data-stu-id="7d4ac-118">If you're doing a full deployment you need toofigure out what replication resources you need.</span></span> <span data-ttu-id="7d4ac-119">Birkaç vardır Araçlar kullanılabilir toohelp bunu.</span><span class="sxs-lookup"><span data-stu-id="7d4ac-119">There are a couple of tools available toohelp you do this.</span></span> <span data-ttu-id="7d4ac-120">TooStep 2 gidin.</span><span class="sxs-lookup"><span data-stu-id="7d4ac-120">Go tooStep 2.</span></span> <span data-ttu-id="7d4ac-121">Tootest hello ortamını ayarlama hızlı yaptığınız varsa bu adımı atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7d4ac-121">If you're doing a quick set up tootest hello environment you can skip this step.</span></span>

<span data-ttu-id="7d4ac-122">Çok Git[3. adım: kapasite planlama](vmware-walkthrough-capacity.md)</span><span class="sxs-lookup"><span data-stu-id="7d4ac-122">Go too[Step 3: Plan capacity](vmware-walkthrough-capacity.md)</span></span>

## <a name="step-4-plan-networking"></a><span data-ttu-id="7d4ac-123">4. adım: ağ planlama</span><span class="sxs-lookup"><span data-stu-id="7d4ac-123">Step 4: Plan networking</span></span>

<span data-ttu-id="7d4ac-124">Yük devretme gerçekleştikten sonra Azure Vm'lerinin bağlı toonetworks olduğunu ve sahip oldukları hello doğru IP adreslerine tooensure planlama bazı ağ toodo gerekir.</span><span class="sxs-lookup"><span data-stu-id="7d4ac-124">You need toodo some network planning tooensure that Azure VMs are connected toonetworks after failover occurs, and  that that they have hello right IP addresses.</span></span>

<span data-ttu-id="7d4ac-125">Çok Git[4. adım: ağ planı](vmware-walkthrough-network.md)</span><span class="sxs-lookup"><span data-stu-id="7d4ac-125">Go too[Step 4: Plan networking](vmware-walkthrough-network.md)</span></span>

##  <a name="step-5-prepare-azure-resources"></a><span data-ttu-id="7d4ac-126">5. adım: Azure kaynaklarını hazırlama</span><span class="sxs-lookup"><span data-stu-id="7d4ac-126">Step 5: Prepare Azure resources</span></span>

<span data-ttu-id="7d4ac-127">Başlamadan önce Azure ağları ve depolama ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="7d4ac-127">Set up Azure networks and storage before you start.</span></span> <span data-ttu-id="7d4ac-128">Dağıtım sırasında bunu yapabilirsiniz ancak başlamadan önce bunu öneririz.</span><span class="sxs-lookup"><span data-stu-id="7d4ac-128">You can do this during deployment, but we recommend you do this before you start.</span></span>

<span data-ttu-id="7d4ac-129">Çok Git[5. adım: Azure hazırlama](vmware-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="7d4ac-129">Go too[Step 5: Prepare Azure](vmware-walkthrough-prepare-azure.md)</span></span>


## <a name="step-6-prepare-vmware"></a><span data-ttu-id="7d4ac-130">6. adım: VMware hazırlama</span><span class="sxs-lookup"><span data-stu-id="7d4ac-130">Step 6: Prepare VMware</span></span>

<span data-ttu-id="7d4ac-131">Site Recovery için kullanacağı hesaplarını tooset gerekir:</span><span class="sxs-lookup"><span data-stu-id="7d4ac-131">You need tooset up accounts that Site Recovery will use to:</span></span>

- <span data-ttu-id="7d4ac-132">Erişim VMware sanallaştırma sunucuları tooautomatically VM'ler algıla.</span><span class="sxs-lookup"><span data-stu-id="7d4ac-132">Access VMware virtualization servers tooautomatically detect VMs.</span></span>
- <span data-ttu-id="7d4ac-133">Sanal makineleri tooinstall hello Mobility hizmeti erişin.</span><span class="sxs-lookup"><span data-stu-id="7d4ac-133">Access VMs tooinstall hello Mobility service.</span></span> <span data-ttu-id="7d4ac-134">Tooreplicate hello Mobility Hizmeti Aracısı önce yüklü olması gerekir istediğiniz her bir VM çoğaltmayı etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7d4ac-134">Each VM you want tooreplicate must have hello Mobility service agent installed before you can enable replication for it.</span></span>

<span data-ttu-id="7d4ac-135">Çok Git[adım 6: VMware hazırlama](vmware-walkthrough-prepare-vmware.md)</span><span class="sxs-lookup"><span data-stu-id="7d4ac-135">Go too[Step 6: Prepare VMware](vmware-walkthrough-prepare-vmware.md)</span></span>

## <a name="step-7-set-up-a-vault"></a><span data-ttu-id="7d4ac-136">7. adım: Bir kasa ayarlama</span><span class="sxs-lookup"><span data-stu-id="7d4ac-136">Step 7: Set up a vault</span></span>

<span data-ttu-id="7d4ac-137">Çoğaltmayı yönetmek ve bir kurtarma Hizmetleri kasası tooorchestrate yukarı tooset gerekir.</span><span class="sxs-lookup"><span data-stu-id="7d4ac-137">You need tooset up a Recovery Services vault tooorchestrate and manage replication.</span></span> <span data-ttu-id="7d4ac-138">Merhaba kasasını ayarladığınızda, istediğinizi belirtin tooreplicate, ve tooreplicate istediğiniz şekilde.</span><span class="sxs-lookup"><span data-stu-id="7d4ac-138">When you set up hello vault, you specify what you want tooreplicate, and where you want tooreplicate it to.</span></span>

<span data-ttu-id="7d4ac-139">Çok Git[adım 7: bir kasasını oluşturup](vmware-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="7d4ac-139">Go too[Step 7: Set up a vault](vmware-walkthrough-create-vault.md)</span></span>

## <a name="step-8-configure-source-and-target-settings"></a><span data-ttu-id="7d4ac-140">8. adım: kaynak ve hedef ayarlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="7d4ac-140">Step 8: Configure source and target settings</span></span>

<span data-ttu-id="7d4ac-141">Merhaba kaynak ve çoğaltma için kullanılan hedef ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="7d4ac-141">Set up hello source and target that's used for replication.</span></span> <span data-ttu-id="7d4ac-142">Kaynak ayarları ayarı birleşik Kurulum tooinstall hello şirket içi Site Recovery bileşenlerini çalıştıran içerir.</span><span class="sxs-lookup"><span data-stu-id="7d4ac-142">Setting up source settings includes running Unified Setup tooinstall hello on-premises Site Recovery components.</span></span>

<span data-ttu-id="7d4ac-143">Çok Git[adım 8: hello kaynak ve hedef ayarlama](vmware-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="7d4ac-143">Go too[Step 8: Set up hello source and target](vmware-walkthrough-source-target.md)</span></span>

## <a name="step-9-set-up-a-replication-policy"></a><span data-ttu-id="7d4ac-144">9. adım: Bir çoğaltma ilkesi ayarlama</span><span class="sxs-lookup"><span data-stu-id="7d4ac-144">Step 9: Set up a replication policy</span></span>

<span data-ttu-id="7d4ac-145">Merhaba kasasına VMware Vm'leri için bir ilke toospecify çoğaltma ayarlarını belirleme.</span><span class="sxs-lookup"><span data-stu-id="7d4ac-145">You set up a policy toospecify replication settings for VMware VMs in hello vault.</span></span>

<span data-ttu-id="7d4ac-146">Çok Git[adım 9: bir çoğaltma ilkesini ayarlayın](vmware-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="7d4ac-146">Go too[Step 9: Set up a replication policy](vmware-walkthrough-replication.md)</span></span>

## <a name="step-10-install-hello-mobility-service"></a><span data-ttu-id="7d4ac-147">10. adım: hello Mobility hizmetini yükleme</span><span class="sxs-lookup"><span data-stu-id="7d4ac-147">Step 10: Install hello Mobility service</span></span>

<span data-ttu-id="7d4ac-148">Merhaba mobilite hizmetinin yüklenmesi tooreplicate istediğiniz her VM.</span><span class="sxs-lookup"><span data-stu-id="7d4ac-148">hello Mobility service must be installed on each VM you want tooreplicate.</span></span> <span data-ttu-id="7d4ac-149">Birkaç yolu tooset iterek ister çekerek yükleme hello hizmetiyle yukarı vardır.</span><span class="sxs-lookup"><span data-stu-id="7d4ac-149">There are a few ways tooset up hello service with push or pull installation.</span></span>

<span data-ttu-id="7d4ac-150">Çok Git[adım 10: hello Mobility hizmetini yükleme](vmware-walkthrough-install-mobility.md)</span><span class="sxs-lookup"><span data-stu-id="7d4ac-150">Go too[Step 10: Install hello Mobility service](vmware-walkthrough-install-mobility.md)</span></span>

## <a name="step-11-enable-replication"></a><span data-ttu-id="7d4ac-151">11. adım: Çoğaltma etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="7d4ac-151">Step 11: Enable replication</span></span>

<span data-ttu-id="7d4ac-152">Merhaba Mobility hizmeti bir VM üzerinde çalışmaya başladıktan sonra çoğaltmayı etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7d4ac-152">After hello Mobility service is running on a VM you can enable replication for it.</span></span> <span data-ttu-id="7d4ac-153">Etkinleştirdikten sonra ilk çoğaltma işlemi hello VM oluşur.</span><span class="sxs-lookup"><span data-stu-id="7d4ac-153">After enabling, initial replication of hello VM occurs.</span></span>

<span data-ttu-id="7d4ac-154">Çok Git[adım 11: çoğaltmasını etkinleştir](vmware-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="7d4ac-154">Go too[Step 11: Enable replication](vmware-walkthrough-enable-replication.md)</span></span>

## <a name="step-12-run-a-test-failover"></a><span data-ttu-id="7d4ac-155">12. adım: yük devretme testi çalıştırma</span><span class="sxs-lookup"><span data-stu-id="7d4ac-155">Step 12: Run a test failover</span></span>

<span data-ttu-id="7d4ac-156">İlk çoğaltma sonlandırıldıktan ve değişim çoğaltması çalıştıran sonra her şeyin beklendiği gibi çalıştığından emin bir test yük devretme toomake çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7d4ac-156">After initial replication finishes, and delta replication is running, you can run a test failover toomake sure everything works as expected.</span></span>

<span data-ttu-id="7d4ac-157">Çok Git[adım 12: yük devretme testi çalıştırma](vmware-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="7d4ac-157">Go too[Step 12: Run a test failover](vmware-walkthrough-test-failover.md)</span></span>
