---
title: aaaReplicate Hyper-V sanal makineleri tooa ikincil VMM sitesi Azure Site Recovery ile | Microsoft Docs
description: "Hello Azure portal kullanarak Hyper-V sanal makineleri tooa ikincil VMM sitesi çoğaltmak için genel bir bakış sağlar."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 476ca82a-8f5c-4498-9dcf-e1011d60ed59
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: raynew
ms.openlocfilehash: 90e44bfc2237dfa7646fb2b7b1e533a7f6d83c50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooa-secondary-vmm-site"></a><span data-ttu-id="847f7-103">Hyper-V sanal makineleri VMM Bulutları tooa ikincil VMM sitesi Çoğalt</span><span class="sxs-lookup"><span data-stu-id="847f7-103">Replicate Hyper-V virtual machines in VMM clouds tooa secondary VMM site</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="847f7-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="847f7-104">Azure portal</span></span>](site-recovery-vmm-to-vmm.md)
> * [<span data-ttu-id="847f7-105">Klasik portal</span><span class="sxs-lookup"><span data-stu-id="847f7-105">Classic portal</span></span>](site-recovery-vmm-to-vmm-classic.md)
> * [<span data-ttu-id="847f7-106">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="847f7-106">PowerShell - Resource Manager</span></span>](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
>
>

<span data-ttu-id="847f7-107">Bu makalede adımlar gerekli tooreplicate şirket içi Hyper-V sanal makineleri (VM'ler) tooa ikincil VMM konum, System Center Virtual Machine Manager (VMM) bulutlarında yönetilen hello genel bir bakış sağlar kullanarak [Azure Site Recovery](site-recovery-overview.md)hello Azure Portalı'nda.</span><span class="sxs-lookup"><span data-stu-id="847f7-107">This article provides an overview of hello steps required tooreplicate on-premises Hyper-V virtual machines (VMs) managed in System Center Virtual Machine Manager (VMM) clouds, tooa secondary VMM location, using [Azure Site Recovery](site-recovery-overview.md) in hello Azure portal.</span></span>

<span data-ttu-id="847f7-108">Bu makaleyi okuduktan sonra tüm yorumlar hello altındaki ya da hello sonrası [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="847f7-108">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="step-1-review-hello-scenario-architecture"></a><span data-ttu-id="847f7-109">1. adım: Gözden geçirme hello senaryo mimarisi</span><span class="sxs-lookup"><span data-stu-id="847f7-109">Step 1: Review hello scenario architecture</span></span>

<span data-ttu-id="847f7-110">Dağıtımı başlatmak hello senaryo mimarisinin gözden geçirin ve tüm hello bileşenleri anladığınızdan emin olun toodeploy olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="847f7-110">Before you start deployment, review hello scenario architecture, and make sure that you understand all hello components you need toodeploy.</span></span>

<span data-ttu-id="847f7-111">Çok Git[1. adım: gözden hello mimarisi](vmm-to-vmm-walkthrough-architecture.md).</span><span class="sxs-lookup"><span data-stu-id="847f7-111">Go too[Step 1: Review hello architecture](vmm-to-vmm-walkthrough-architecture.md).</span></span>

## <a name="step-2-review-prerequisites-and-limitations"></a><span data-ttu-id="847f7-112">2. adım: Gözden geçirme Önkoşullar ve sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="847f7-112">Step 2: Review prerequisites and limitations</span></span>

<span data-ttu-id="847f7-113">Merhaba dağıtımının önkoşulları ve kısıtlamaları anladığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="847f7-113">Make sure that you understand hello deployment prerequisites and limitations.</span></span>

<span data-ttu-id="847f7-114">**Azure önkoşulları**: Microsoft Azure aboneliğinizin olması gerekir ve Azure kurtarma Hizmetleri kasası, tooorchestrate ve çoğaltmayı yönetme.</span><span class="sxs-lookup"><span data-stu-id="847f7-114">**Azure prerequisites**: You need a Microsoft Azure subscription, and Azure Recovery Services vault, tooorchestrate and manage replication.</span></span>
<span data-ttu-id="847f7-115">**Şirket içi VMM sunucuları ve Hyper-V konakları**: VMM sunucuları ve Hyper-V konakları uyumlu ve Site Recovery dağıtımı için hazır olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="847f7-115">**On-premises VMM servers and Hyper-V hosts**: Make sure that VMM servers and Hyper-V hosts are compliant and prepared for Site Recovery deployment.</span></span>

<span data-ttu-id="847f7-116">Çok Git[2. adım: Önkoşullar ve sınırlamalar doğrulayın](vmm-to-vmm-walkthrough-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="847f7-116">Go too[Step 2: Verify prerequisites and limitations](vmm-to-vmm-walkthrough-prerequisites.md).</span></span>

## <a name="step-3-plan-networking"></a><span data-ttu-id="847f7-117">3. adım: ağ planlama</span><span class="sxs-lookup"><span data-stu-id="847f7-117">Step 3: Plan networking</span></span>

<span data-ttu-id="847f7-118">Merhaba senaryo dağıttığınızda VMM VM ağları arasında ağ eşlemesi yapılandırabilirsiniz tooensure planlama bazı ağ toodo gerekir.</span><span class="sxs-lookup"><span data-stu-id="847f7-118">You need toodo some network planning tooensure that you can configure network mapping between VMM VM networks when you deploy hello scenario.</span></span>

<span data-ttu-id="847f7-119">Çok Git[3. adım: ağ planlama](vmm-to-vmm-walkthrough-network.md).</span><span class="sxs-lookup"><span data-stu-id="847f7-119">Go too[Step 3: Plan networking](vmm-to-vmm-walkthrough-network.md).</span></span>


## <a name="step-4-prepare-vmm-and-hyper-v"></a><span data-ttu-id="847f7-120">4. adım: VMM ve Hyper-V hazırlama</span><span class="sxs-lookup"><span data-stu-id="847f7-120">Step 4: Prepare VMM and Hyper-V</span></span>

<span data-ttu-id="847f7-121">Merhaba VMM sunucuları ve Hyper-V konakları Site Recovery dağıtımı için hazırlayın.</span><span class="sxs-lookup"><span data-stu-id="847f7-121">Prepare hello VMM servers and Hyper-V hosts for Site Recovery deployment.</span></span>

<span data-ttu-id="847f7-122">Çok Git[4. adım: şirket içi sunucuları hazırlama](vmm-to-vmm-walkthrough-vmm-hyper-v.md).</span><span class="sxs-lookup"><span data-stu-id="847f7-122">Go too[Step 4: Prepare on-premises servers](vmm-to-vmm-walkthrough-vmm-hyper-v.md).</span></span>

## <a name="step-5-set-up-a-vault"></a><span data-ttu-id="847f7-123">5. adım: Bir kasa ayarlama</span><span class="sxs-lookup"><span data-stu-id="847f7-123">Step 5: Set up a vault</span></span>

<span data-ttu-id="847f7-124">Kurtarma Hizmetleri kasasını ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="847f7-124">Set up a Recovery Services vault.</span></span> <span data-ttu-id="847f7-125">Merhaba kasası yapılandırma ayarlarını içeren, çoğaltma ve yönetir.</span><span class="sxs-lookup"><span data-stu-id="847f7-125">hello vault contains configuration settings, and orchestrates replication.</span></span>

<span data-ttu-id="847f7-126">[5. adım: bir kasasını oluşturup](vmm-to-vmm-walkthrough-create-vault.md).</span><span class="sxs-lookup"><span data-stu-id="847f7-126">[Step 5: Set up a vault](vmm-to-vmm-walkthrough-create-vault.md).</span></span>

## <a name="step-6-set-up-source-and-target-settings"></a><span data-ttu-id="847f7-127">6. adım: kaynak ve hedef ayarlarını belirleme</span><span class="sxs-lookup"><span data-stu-id="847f7-127">Step 6: Set up source and target settings</span></span>

<span data-ttu-id="847f7-128">Merhaba kaynak ve hedef çoğaltma VMM konumları ayarlama.</span><span class="sxs-lookup"><span data-stu-id="847f7-128">Set up hello source and target replication VMM locations.</span></span> <span data-ttu-id="847f7-129">Merhaba VMM sunucuları toohello kasası ekleyin ve Site Recovery bileşenlerini hello yükleme dosyalarını indirin.</span><span class="sxs-lookup"><span data-stu-id="847f7-129">Add hello VMM servers toohello vault, and download hello installation files for Site Recovery components.</span></span> <span data-ttu-id="847f7-130">Merhaba VMM sunucusunda Azure Site kurtarma sağlayıcısı kurulumunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="847f7-130">Run Azure Site Recovery Provider setup on hello VMM server.</span></span> <span data-ttu-id="847f7-131">Kurulum hello VMM sunucusunda sağlayıcı hello yükler ve hello sunucu hello kasasına kaydeder.</span><span class="sxs-lookup"><span data-stu-id="847f7-131">Setup installs hello Provider on hello VMM server, and registers hello server in hello vault.</span></span> <span data-ttu-id="847f7-132">Her Hyper-V ana bilgisayarda hello Microsoft Kurtarma Hizmetleri aracısını yükleyin.</span><span class="sxs-lookup"><span data-stu-id="847f7-132">You install hello Microsoft Recovery Services agent on each Hyper-V host.</span></span>

<span data-ttu-id="847f7-133">Çok Git[adım 6: hello kaynak ve hedef ayarlar](vmm-to-vmm-walkthrough-source-target.md).</span><span class="sxs-lookup"><span data-stu-id="847f7-133">Go too[Step 6: Set up hello source and target settings](vmm-to-vmm-walkthrough-source-target.md).</span></span>

## <a name="step-7-configure-network-mapping"></a><span data-ttu-id="847f7-134">7. Adım: Ağ eşlemesini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="847f7-134">Step 7: Configure network mapping</span></span>

<span data-ttu-id="847f7-135">Merhaba kaynak ve hedef konumların VMM VM ağlarında eşleyin.</span><span class="sxs-lookup"><span data-stu-id="847f7-135">Map VMM VM networks in hello source and target locations.</span></span> <span data-ttu-id="847f7-136">Yük devretme sonrasında VM'ler hello hedef ağ hangi hello kaynak Hyper-V VM bulunduğu eşlemeleri toohello kaynak bir VM ağı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="847f7-136">After failover, VMs are created in hello target network that maps toohello source VM network in which hello source Hyper-V VM is located.</span></span>

<span data-ttu-id="847f7-137">Çok Git[adım 7: ağ eşlemesini yapılandırma](vmm-to-vmm-walkthrough-network-mapping.md).</span><span class="sxs-lookup"><span data-stu-id="847f7-137">Go too[Step 7: Configure network mapping](vmm-to-vmm-walkthrough-network-mapping.md).</span></span>


## <a name="step-8-set-up-a-replication-policy"></a><span data-ttu-id="847f7-138">8. adım: Bir çoğaltma ilkesi ayarlama</span><span class="sxs-lookup"><span data-stu-id="847f7-138">Step 8: Set up a replication policy</span></span>

<span data-ttu-id="847f7-139">Sanal makineleri VMM konumlar arasında nasıl çoğaltılır belirtin.</span><span class="sxs-lookup"><span data-stu-id="847f7-139">Specify how  VMs will be replicated between VMM locations.</span></span>

<span data-ttu-id="847f7-140">Çok Git[adım 8: bir çoğaltma ilkesini ayarlayın](vmm-to-vmm-walkthrough-replication.md).</span><span class="sxs-lookup"><span data-stu-id="847f7-140">Go too[Step 8: Set up a replication policy](vmm-to-vmm-walkthrough-replication.md).</span></span>


## <a name="step-9-enable-replication-for-vms"></a><span data-ttu-id="847f7-141">9. adım: sanal makineleri için çoğaltmayı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="847f7-141">Step 9: Enable replication for VMs</span></span>

<span data-ttu-id="847f7-142">Tooreplicate istediğiniz hello sanal makineleri seçin.</span><span class="sxs-lookup"><span data-stu-id="847f7-142">Select hello VMs you want tooreplicate.</span></span> <span data-ttu-id="847f7-143">Çoğaltma Tetikleyicileri hello ilk çoğaltma toohello ikincil site için bir VM etkinleştirildikten sonra devam eden değişim çoğaltması tarafından kullanılıyordu.</span><span class="sxs-lookup"><span data-stu-id="847f7-143">Enabling a VM for replication triggers hello initial replication toohello secondary site, followed by ongoing delta replication.</span></span>

<span data-ttu-id="847f7-144">Çok Git[adım 9: çoğaltmasını etkinleştir](vmm-to-vmm-walkthrough-enable-replication.md).</span><span class="sxs-lookup"><span data-stu-id="847f7-144">Go too[Step 9: Enable replication](vmm-to-vmm-walkthrough-enable-replication.md).</span></span>


## <a name="step-10-run-a-test-failover"></a><span data-ttu-id="847f7-145">10. adım: yük devretme testi çalıştırma</span><span class="sxs-lookup"><span data-stu-id="847f7-145">Step 10: Run a test failover</span></span>

<span data-ttu-id="847f7-146">Her şeyin beklendiği gibi çalıştığından emin bir test yük devretme toomake çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="847f7-146">Run a test failover toomake sure everything's working as expected.</span></span>

<span data-ttu-id="847f7-147">Çok Git[adım 10: bir yük devretme testi](vmm-to-vmm-walkthrough-test-failover.md).</span><span class="sxs-lookup"><span data-stu-id="847f7-147">Go too[Step 10: Run a test failover](vmm-to-vmm-walkthrough-test-failover.md).</span></span>
