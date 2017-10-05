---
title: "VMware Vm'lerini Azure Site Recovery ile Azure'a çoğaltma | Microsoft Docs"
description: "Azure'da VMware Vm'lerinde çalışan iş yükleri çoğaltmak için adımlara genel bir bakış sağlar."
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
ms.openlocfilehash: db6f5f95929503e82a529dba26b56af1edb0767f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-vmware-vms-to-azure-with-site-recovery"></a><span data-ttu-id="13bd4-103">VMware sanal makinelerini Site Recovery ile Azure'a çoğaltma</span><span class="sxs-lookup"><span data-stu-id="13bd4-103">Replicate VMware VMs to Azure with Site Recovery</span></span>

<span data-ttu-id="13bd4-104">Bu makalede şirket içi VMware sanal makinelerini Azure'a çoğaltma için gereken adımlar genel bir bakış sağlar kullanarak [Azure Site Recovery](site-recovery-overview.md) Azure portalında hizmet.</span><span class="sxs-lookup"><span data-stu-id="13bd4-104">This article provides an overview of the steps required to replicate on-premises VMware virtual machines to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>


![Dağıtım işlemi](./media/vmware-walkthrough-overview/vmware-to-azure-process.png)

<span data-ttu-id="13bd4-106">**Şekil 1: Dağıtım işlemi özeti**</span><span class="sxs-lookup"><span data-stu-id="13bd4-106">**Figure 1: Deployment process summary**</span></span>

## <a name="step-1-review-architecture-and-prerequisites"></a><span data-ttu-id="13bd4-107">1. adım: mimarisi ve önkoşulları gözden geçirin</span><span class="sxs-lookup"><span data-stu-id="13bd4-107">Step 1: Review architecture and prerequisites</span></span>

<span data-ttu-id="13bd4-108">Dağıtıma başlamadan önce senaryo mimarisinin gözden geçirin ve dağıtmak için gereken tüm bileşenleri anladığınızdan emin olun</span><span class="sxs-lookup"><span data-stu-id="13bd4-108">Before you start deployment, review the scenario architecture, and make sure you understand all the components you need to deploy</span></span>

<span data-ttu-id="13bd4-109">Git [1. adım: mimarisi gözden geçirin](vmware-walkthrough-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="13bd4-109">Go to [Step 1: Review the architecture](vmware-walkthrough-architecture.md)</span></span>


## <a name="step-2-review-prerequisites"></a><span data-ttu-id="13bd4-110">2. adım: Gözden geçirme önkoşulları</span><span class="sxs-lookup"><span data-stu-id="13bd4-110">Step 2: Review prerequisites</span></span>

<span data-ttu-id="13bd4-111">Önkoşullar her dağıtım bileşen için yerinde olduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="13bd4-111">Make sure you have the prerequisites in place for each deployment component:</span></span>

- <span data-ttu-id="13bd4-112">**Azure önkoşulları**: bir Microsoft Azure hesabı, Azure ağları ve depolama hesapları gerekir.</span><span class="sxs-lookup"><span data-stu-id="13bd4-112">**Azure prerequisites**: You need a Microsoft Azure account, Azure networks, and storage accounts.</span></span>
- <span data-ttu-id="13bd4-113">**Şirket içi Site Recovery bileşenlerini**: şirket içi Site Recovery bileşenlerini çalıştıran bir makineye gerekir.</span><span class="sxs-lookup"><span data-stu-id="13bd4-113">**On-premises Site Recovery components**: You need a machine running on-premises Site Recovery components.</span></span>
- <span data-ttu-id="13bd4-114">**Şirket içi VMware Önkoşullar**: Site Recovery VMware sunucularını ve Vm'leri erişebilmesi için hesapları ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="13bd4-114">**On-premises VMware prerequisites**: You need to set up accounts so that Site Recovery can access VMware servers and VMs.</span></span>
- <span data-ttu-id="13bd4-115">**Çoğaltılan VM'ler**: çoğaltmak istediğiniz sanal makineleri gereken Azure gereksinimlerine uymak ve Mobility hizmeti bileşeninin yüklü olması.</span><span class="sxs-lookup"><span data-stu-id="13bd4-115">**Replicated VMs**: VMs you want to replicate need to comply with Azure requirements, and have the Mobility service component installed.</span></span>

<span data-ttu-id="13bd4-116">Git [2. adım: gözden Önkoşullar ve sınırlamalar](vmware-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="13bd4-116">Go to [Step 2: Review prerequisites and limitations](vmware-walkthrough-prerequisites.md)</span></span>

## <a name="step-3-plan-capacity"></a><span data-ttu-id="13bd4-117">3. adım: Planı kapasite</span><span class="sxs-lookup"><span data-stu-id="13bd4-117">Step 3: Plan capacity</span></span>

<span data-ttu-id="13bd4-118">Tam dağıtımını yaptığınız ihtiyacınız hangi çoğaltma kaynakları şekil gerekir.</span><span class="sxs-lookup"><span data-stu-id="13bd4-118">If you're doing a full deployment you need to figure out what replication resources you need.</span></span> <span data-ttu-id="13bd4-119">Birkaç bu yapmanıza yardımcı olmak için kullanılabilen araçlar vardır.</span><span class="sxs-lookup"><span data-stu-id="13bd4-119">There are a couple of tools available to help you do this.</span></span> <span data-ttu-id="13bd4-120">2. adıma geçin.</span><span class="sxs-lookup"><span data-stu-id="13bd4-120">Go to Step 2.</span></span> <span data-ttu-id="13bd4-121">Hızlı kümesi yaptığınız yukarı test ortamı için bu adımı atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="13bd4-121">If you're doing a quick set up to test the environment you can skip this step.</span></span>

<span data-ttu-id="13bd4-122">[3. Adım: Kapasiteyi planlama](vmware-walkthrough-capacity.md)’ya gidin.</span><span class="sxs-lookup"><span data-stu-id="13bd4-122">Go to [Step 3: Plan capacity](vmware-walkthrough-capacity.md)</span></span>

## <a name="step-4-plan-networking"></a><span data-ttu-id="13bd4-123">4. adım: ağ planlama</span><span class="sxs-lookup"><span data-stu-id="13bd4-123">Step 4: Plan networking</span></span>

<span data-ttu-id="13bd4-124">Bazı ağ yük devretme gerçekleştikten sonra sahip oldukları doğru IP adreslerini Azure Vm'lerinin ağlara bağlandığından emin olmak planlama yapmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="13bd4-124">You need to do some network planning to ensure that Azure VMs are connected to networks after failover occurs, and  that that they have the right IP addresses.</span></span>

<span data-ttu-id="13bd4-125">Git [4. adım: ağ planı](vmware-walkthrough-network.md)</span><span class="sxs-lookup"><span data-stu-id="13bd4-125">Go to [Step 4: Plan networking](vmware-walkthrough-network.md)</span></span>

##  <a name="step-5-prepare-azure-resources"></a><span data-ttu-id="13bd4-126">5. adım: Azure kaynaklarını hazırlama</span><span class="sxs-lookup"><span data-stu-id="13bd4-126">Step 5: Prepare Azure resources</span></span>

<span data-ttu-id="13bd4-127">Başlamadan önce Azure ağları ve depolama ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="13bd4-127">Set up Azure networks and storage before you start.</span></span> <span data-ttu-id="13bd4-128">Dağıtım sırasında bunu yapabilirsiniz ancak başlamadan önce bunu öneririz.</span><span class="sxs-lookup"><span data-stu-id="13bd4-128">You can do this during deployment, but we recommend you do this before you start.</span></span>

<span data-ttu-id="13bd4-129">Git [5. adım: Azure hazırlama](vmware-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="13bd4-129">Go to [Step 5: Prepare Azure](vmware-walkthrough-prepare-azure.md)</span></span>


## <a name="step-6-prepare-vmware"></a><span data-ttu-id="13bd4-130">6. adım: VMware hazırlama</span><span class="sxs-lookup"><span data-stu-id="13bd4-130">Step 6: Prepare VMware</span></span>

<span data-ttu-id="13bd4-131">Site Recovery için kullanacağınız hesaplar ayarlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="13bd4-131">You need to set up accounts that Site Recovery will use to:</span></span>

- <span data-ttu-id="13bd4-132">Sanal makineleri otomatik olarak algılamak için erişim VMware sanallaştırma sunucuları.</span><span class="sxs-lookup"><span data-stu-id="13bd4-132">Access VMware virtualization servers to automatically detect VMs.</span></span>
- <span data-ttu-id="13bd4-133">Mobilite hizmetinin yüklenmesi için erişim VM'ler.</span><span class="sxs-lookup"><span data-stu-id="13bd4-133">Access VMs to install the Mobility service.</span></span> <span data-ttu-id="13bd4-134">Çoğaltmak istediğiniz her bir VM Mobility Hizmeti Aracısı çoğaltmayı etkinleştirmeden önce yüklü olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="13bd4-134">Each VM you want to replicate must have the Mobility service agent installed before you can enable replication for it.</span></span>

<span data-ttu-id="13bd4-135">Git [6. adım: VMware hazırlama](vmware-walkthrough-prepare-vmware.md)</span><span class="sxs-lookup"><span data-stu-id="13bd4-135">Go to [Step 6: Prepare VMware](vmware-walkthrough-prepare-vmware.md)</span></span>

## <a name="step-7-set-up-a-vault"></a><span data-ttu-id="13bd4-136">7. adım: Bir kasa ayarlama</span><span class="sxs-lookup"><span data-stu-id="13bd4-136">Step 7: Set up a vault</span></span>

<span data-ttu-id="13bd4-137">Düzenlemek ve çoğaltmayı yönetmek için bir kurtarma Hizmetleri kasasını ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="13bd4-137">You need to set up a Recovery Services vault to orchestrate and manage replication.</span></span> <span data-ttu-id="13bd4-138">Kasasını ayarladığınızda, çoğaltmak istediğiniz ve kendisine çoğaltmak istediğiniz yeri belirtin.</span><span class="sxs-lookup"><span data-stu-id="13bd4-138">When you set up the vault, you specify what you want to replicate, and where you want to replicate it to.</span></span>

<span data-ttu-id="13bd4-139">Git [adım 7: bir kasasını oluşturup](vmware-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="13bd4-139">Go to [Step 7: Set up a vault](vmware-walkthrough-create-vault.md)</span></span>

## <a name="step-8-configure-source-and-target-settings"></a><span data-ttu-id="13bd4-140">8. adım: kaynak ve hedef ayarlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="13bd4-140">Step 8: Configure source and target settings</span></span>

<span data-ttu-id="13bd4-141">Kaynak ve çoğaltma için kullanılan hedef ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="13bd4-141">Set up the source and target that's used for replication.</span></span> <span data-ttu-id="13bd4-142">Kaynak ayarları ayarı birleşik şirket içi Site Recovery bileşenlerini yüklemek için Kurulum'u çalıştırmayı içerir.</span><span class="sxs-lookup"><span data-stu-id="13bd4-142">Setting up source settings includes running Unified Setup to install the on-premises Site Recovery components.</span></span>

<span data-ttu-id="13bd4-143">Git [adım 8: kaynak ve hedef ayarlama](vmware-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="13bd4-143">Go to [Step 8: Set up the source and target](vmware-walkthrough-source-target.md)</span></span>

## <a name="step-9-set-up-a-replication-policy"></a><span data-ttu-id="13bd4-144">9. adım: Bir çoğaltma ilkesi ayarlama</span><span class="sxs-lookup"><span data-stu-id="13bd4-144">Step 9: Set up a replication policy</span></span>

<span data-ttu-id="13bd4-145">VMware Vm'leri için çoğaltma ayarlarını kasaya belirtmek için bir ilke ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="13bd4-145">You set up a policy to specify replication settings for VMware VMs in the vault.</span></span>

<span data-ttu-id="13bd4-146">Git [adım 9: bir çoğaltma ilkesini ayarlayın](vmware-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="13bd4-146">Go to [Step 9: Set up a replication policy](vmware-walkthrough-replication.md)</span></span>

## <a name="step-10-install-the-mobility-service"></a><span data-ttu-id="13bd4-147">10. adım: mobilite hizmeti yükleme</span><span class="sxs-lookup"><span data-stu-id="13bd4-147">Step 10: Install the Mobility service</span></span>

<span data-ttu-id="13bd4-148">Mobility hizmetinin çoğaltmak istediğiniz her bir VM üzerinde yüklü olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="13bd4-148">The Mobility service must be installed on each VM you want to replicate.</span></span> <span data-ttu-id="13bd4-149">Anında iletme ve çekme yükleme hizmetiyle ayarlamak için birkaç yolu vardır.</span><span class="sxs-lookup"><span data-stu-id="13bd4-149">There are a few ways to set up the service with push or pull installation.</span></span>

<span data-ttu-id="13bd4-150">Git [adım 10: Mobility hizmetini yükleme](vmware-walkthrough-install-mobility.md)</span><span class="sxs-lookup"><span data-stu-id="13bd4-150">Go to [Step 10: Install the Mobility service](vmware-walkthrough-install-mobility.md)</span></span>

## <a name="step-11-enable-replication"></a><span data-ttu-id="13bd4-151">11. adım: Çoğaltma etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="13bd4-151">Step 11: Enable replication</span></span>

<span data-ttu-id="13bd4-152">Mobility hizmeti bir VM üzerinde çalışmaya başladıktan sonra çoğaltmayı etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="13bd4-152">After the Mobility service is running on a VM you can enable replication for it.</span></span> <span data-ttu-id="13bd4-153">Etkinleştirdikten sonra VM başlangıç çoğaltması gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="13bd4-153">After enabling, initial replication of the VM occurs.</span></span>

<span data-ttu-id="13bd4-154">Git [adım 11: çoğaltmasını etkinleştir](vmware-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="13bd4-154">Go to [Step 11: Enable replication](vmware-walkthrough-enable-replication.md)</span></span>

## <a name="step-12-run-a-test-failover"></a><span data-ttu-id="13bd4-155">12. adım: yük devretme testi çalıştırma</span><span class="sxs-lookup"><span data-stu-id="13bd4-155">Step 12: Run a test failover</span></span>

<span data-ttu-id="13bd4-156">İlk çoğaltma sonlandırıldıktan ve değişim çoğaltması çalıştıran sonra her şeyin beklendiği gibi çalıştığından emin olmak için yük devretme testi çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="13bd4-156">After initial replication finishes, and delta replication is running, you can run a test failover to make sure everything works as expected.</span></span>

<span data-ttu-id="13bd4-157">Git [adım 12: yük devretme testi çalıştırma](vmware-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="13bd4-157">Go to [Step 12: Run a test failover](vmware-walkthrough-test-failover.md)</span></span>
