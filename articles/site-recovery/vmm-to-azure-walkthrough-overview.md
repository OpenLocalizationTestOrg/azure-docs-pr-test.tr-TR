---
title: vmm'de Hyper-V sanal makineleri aaaReplicate bulut Azure Site Recovery ile tooAzure | Microsoft Docs
description: "VMM Bulutları tooAzure hello Azure Site Recovery hizmetini kullanarak Hyper-V sanal makineleri çoğaltmak için genel bir bakış sağlar."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 8e7d868e-00f3-4e8b-9a9e-f23365abf6ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: raynew
ms.openlocfilehash: d6f729a49cc86ea07bebc4d7266fd7b58b3998f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooazure-using-site-recovery-in-hello-azure-portal"></a><span data-ttu-id="4bcbb-103">VMM Bulutları tooAzure hello Azure portalında Site Recovery kullanarak Hyper-V sanal makineleri Çoğalt</span><span class="sxs-lookup"><span data-stu-id="4bcbb-103">Replicate Hyper-V virtual machines in VMM clouds tooAzure using Site Recovery in hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4bcbb-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="4bcbb-104">Azure portal</span></span>](site-recovery-vmm-to-azure.md)
> * [<span data-ttu-id="4bcbb-105">Azure klasik</span><span class="sxs-lookup"><span data-stu-id="4bcbb-105">Azure classic</span></span>](site-recovery-vmm-to-azure-classic.md)
> * [<span data-ttu-id="4bcbb-106">PowerShell Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4bcbb-106">PowerShell Resource Manager</span></span>](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [<span data-ttu-id="4bcbb-107">PowerShell klasik</span><span class="sxs-lookup"><span data-stu-id="4bcbb-107">PowerShell classic</span></span>](site-recovery-deploy-with-powershell.md)


<span data-ttu-id="4bcbb-108">Bu makalede hello adımları gerekli tooreplicate genel bir bakış şirket içi Hyper-V sanal makineleri (VM'ler) System Center Virtual Machine Manager (VMM) Bulutlar tooAzure hello kullanarak yönetilen sağlar [Azure Site Recovery](site-recovery-overview.md) hizmeti Hello Azure portalı.</span><span class="sxs-lookup"><span data-stu-id="4bcbb-108">This article provides an overview of hello steps required tooreplicate on-premises Hyper-V virtual machines (VMs) managed in System Center Virtual Machine Manager (VMM) clouds tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="4bcbb-109">Bu makaleyi okuduktan sonra tüm yorumlar hello altındaki ya da hello sonrası [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="4bcbb-109">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="step-1-review-hello-scenario-architecture"></a><span data-ttu-id="4bcbb-110">1. adım: Gözden geçirme hello senaryo mimarisi</span><span class="sxs-lookup"><span data-stu-id="4bcbb-110">Step 1: Review hello scenario architecture</span></span>

<span data-ttu-id="4bcbb-111">Dağıtımı başlatmak hello senaryo mimarisinin gözden geçirin ve tüm hello bileşenleri anladığınızdan emin olun toodeploy olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="4bcbb-111">Before you start deployment, review hello scenario architecture, and make sure that you understand all hello components you need toodeploy.</span></span>

<span data-ttu-id="4bcbb-112">Çok Git[1. adım: gözden hello mimarisi](vmm-to-azure-walkthrough-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="4bcbb-112">Go too[Step 1: Review hello architecture](vmm-to-azure-walkthrough-architecture.md)</span></span>

## <a name="step-2-review-prerequisites-and-limitations"></a><span data-ttu-id="4bcbb-113">2. adım: Gözden geçirme Önkoşullar ve sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="4bcbb-113">Step 2: Review prerequisites and limitations</span></span>

<span data-ttu-id="4bcbb-114">Merhaba dağıtımının önkoşulları ve kısıtlamaları anladığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="4bcbb-114">Make sure that you understand hello deployment prerequisites and limitations.</span></span>

<span data-ttu-id="4bcbb-115">**Azure önkoşulları**: bir Microsoft Azure hesabı, Azure ağları ve depolama hesapları gerekir.</span><span class="sxs-lookup"><span data-stu-id="4bcbb-115">**Azure prerequisites**: You need a Microsoft Azure account, Azure networks, and storage accounts.</span></span>
<span data-ttu-id="4bcbb-116">**Şirket içi VMM sunucuları ve Hyper-V konakları**: VMM sunucuları ve Hyper-V konakları uyumlu ve Site Recovery dağıtımı için hazır olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="4bcbb-116">**On-premises VMM servers and Hyper-V hosts**: Make sure that VMM servers and Hyper-V hosts are compliant and prepared for Site Recovery deployment.</span></span>
<span data-ttu-id="4bcbb-117">**Çoğaltılan VM'ler**: tooreplicate istediğiniz sanal makineleri Azure gereksinimlerine uymak denetleyin.</span><span class="sxs-lookup"><span data-stu-id="4bcbb-117">**Replicated VMs**: Check that VMs you want tooreplicate comply with Azure requirements.</span></span>

<span data-ttu-id="4bcbb-118">Çok Git[2. adım: Önkoşullar ve sınırlamalar doğrulayın](vmm-to-azure-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="4bcbb-118">Go too[Step 2: Verify prerequisites and limitations](vmm-to-azure-walkthrough-prerequisites.md)</span></span>

## <a name="step-3-plan-capacity"></a><span data-ttu-id="4bcbb-119">3. adım: Planı kapasite</span><span class="sxs-lookup"><span data-stu-id="4bcbb-119">Step 3: Plan capacity</span></span>

<span data-ttu-id="4bcbb-120">Tam dağıtımını yaptığınız, ihtiyacınız hangi çoğaltma kaynakları çıkışı toofigure gerekir.</span><span class="sxs-lookup"><span data-stu-id="4bcbb-120">If you're doing a full deployment, you need toofigure out what replication resources you need.</span></span> <span data-ttu-id="4bcbb-121">Birkaç vardır Araçlar kullanılabilir toohelp bunu.</span><span class="sxs-lookup"><span data-stu-id="4bcbb-121">There are a couple of tools available toohelp you do this.</span></span> <span data-ttu-id="4bcbb-122">Tootest hello ortamını ayarlama hızlı yaptığınız varsa, bu adımı atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4bcbb-122">If you're doing a quick set up tootest hello environment, you can skip this step.</span></span>

<span data-ttu-id="4bcbb-123">Çok Git[3. adım: kapasite planlama](vmm-to-azure-walkthrough-capacity.md)</span><span class="sxs-lookup"><span data-stu-id="4bcbb-123">Go too[Step 3: Plan capacity](vmm-to-azure-walkthrough-capacity.md)</span></span>

## <a name="step-4-plan-networking"></a><span data-ttu-id="4bcbb-124">4. adım: ağ planlama</span><span class="sxs-lookup"><span data-stu-id="4bcbb-124">Step 4: Plan networking</span></span>

<span data-ttu-id="4bcbb-125">Azure VM'ler bağlı tooAzure sanal ağları yük devretme gerçekleştikten sonra uygun IP atanmış oldukları adresleri olacaktır toodo hello senaryo dağıttığınızda ağ eşlemesi yapılandırabilirsiniz tooensure planlama bazı ağ gerekir.</span><span class="sxs-lookup"><span data-stu-id="4bcbb-125">You need toodo some network planning tooensure that you can configure network mapping when you deploy hello scenario, that Azure VMs will be connected tooAzure virtual networks after failover occurs, and that that they're assigned appropriate IP addresses.</span></span>

<span data-ttu-id="4bcbb-126">Çok Git[4. adım: ağ planı](vmm-to-azure-walkthrough-network.md)</span><span class="sxs-lookup"><span data-stu-id="4bcbb-126">Go too[Step 4: Plan networking](vmm-to-azure-walkthrough-network.md)</span></span>


## <a name="step-5-prepare-azure-resources"></a><span data-ttu-id="4bcbb-127">5. adım: Azure kaynaklarını hazırlama</span><span class="sxs-lookup"><span data-stu-id="4bcbb-127">Step 5: Prepare Azure resources</span></span>

<span data-ttu-id="4bcbb-128">Bir Azure hesabı, ağlara ve depolama ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="4bcbb-128">Set up an Azure account, networks, and storage.</span></span> <span data-ttu-id="4bcbb-129">Dağıtım sırasında bunu yapabilirsiniz ancak başlamadan önce bunu öneririz.</span><span class="sxs-lookup"><span data-stu-id="4bcbb-129">You can do this during deployment, but we recommend you do this before you start.</span></span>

<span data-ttu-id="4bcbb-130">Çok Git[5. adım: Azure hazırlama](vmm-to-azure-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="4bcbb-130">Go too[Step 5: Prepare Azure](vmm-to-azure-walkthrough-prepare-azure.md)</span></span>

## <a name="step-6-prepare-vmm-and-hyper-v"></a><span data-ttu-id="4bcbb-131">6. adım: VMM ve Hyper-V hazırlama</span><span class="sxs-lookup"><span data-stu-id="4bcbb-131">Step 6: Prepare VMM and Hyper-V</span></span>

<span data-ttu-id="4bcbb-132">Merhaba şirket içi VMM sunucuları ve Hyper-V konakları Site Recovery dağıtımı için hazırlayın.</span><span class="sxs-lookup"><span data-stu-id="4bcbb-132">Prepare hello on-premises VMM servers and Hyper-V hosts for Site Recovery deployment.</span></span>

<span data-ttu-id="4bcbb-133">Çok Git[6. adım: şirket içi sunucuları hazırlama](vmm-to-azure-walkthrough-vmm-hyper-v.md)</span><span class="sxs-lookup"><span data-stu-id="4bcbb-133">Go too[Step 6: Prepare on-premises servers](vmm-to-azure-walkthrough-vmm-hyper-v.md)</span></span>

## <a name="step-7-set-up-a-vault"></a><span data-ttu-id="4bcbb-134">7. adım: Bir kasa ayarlama</span><span class="sxs-lookup"><span data-stu-id="4bcbb-134">Step 7: Set up a vault</span></span>

<span data-ttu-id="4bcbb-135">Kurtarma Hizmetleri kasasını ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="4bcbb-135">Set up a Recovery Services vault.</span></span> <span data-ttu-id="4bcbb-136">Merhaba kasası yapılandırma ayarlarını içeren, çoğaltma ve yönetir.</span><span class="sxs-lookup"><span data-stu-id="4bcbb-136">hello vault contains configuration settings, and orchestrates replication.</span></span>

[<span data-ttu-id="4bcbb-137">7. adım: Bir kasa ayarlama</span><span class="sxs-lookup"><span data-stu-id="4bcbb-137">Step 7: Set up a vault</span></span>](vmm-to-azure-walkthrough-create-vault.md)

## <a name="step-8-configure-source-and-target-settings"></a><span data-ttu-id="4bcbb-138">8. adım: kaynak ve hedef ayarlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="4bcbb-138">Step 8: Configure source and target settings</span></span>

<span data-ttu-id="4bcbb-139">Merhaba kaynak ve hedef çoğaltma konumları ayarlama.</span><span class="sxs-lookup"><span data-stu-id="4bcbb-139">Set up hello source and target replication locations.</span></span> <span data-ttu-id="4bcbb-140">Merhaba VMM server toohello kasası ekleyin ve Site Recovery bileşenlerini hello yükleme dosyalarını indirin.</span><span class="sxs-lookup"><span data-stu-id="4bcbb-140">Add hello VMM server toohello vault, and download hello installation files for Site Recovery components.</span></span> <span data-ttu-id="4bcbb-141">Merhaba VMM sunucusunda Azure Site kurtarma sağlayıcısı kurulumunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="4bcbb-141">Run Azure Site Recovery Provider setup on hello VMM server.</span></span> <span data-ttu-id="4bcbb-142">Kurulum hello VMM sunucusunda sağlayıcı hello yükler ve hello sunucu hello kasasına kaydeder.</span><span class="sxs-lookup"><span data-stu-id="4bcbb-142">Setup installs hello Provider on hello VMM server, and registers hello server in hello vault.</span></span> <span data-ttu-id="4bcbb-143">Her Hyper-V ana bilgisayarda hello Microsoft Kurtarma Hizmetleri aracısını yükleyin.</span><span class="sxs-lookup"><span data-stu-id="4bcbb-143">You install hello Microsoft Recovery Services agent on each Hyper-V host.</span></span>

<span data-ttu-id="4bcbb-144">Çok Git[adım 8: kaynak ve hedef ayarlarını yapılandırma](vmm-to-azure-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="4bcbb-144">Go too[Step 8: Configure source and target settings](vmm-to-azure-walkthrough-source-target.md)</span></span>

## <a name="step-9-configure-network-mapping"></a><span data-ttu-id="4bcbb-145">9. adım: ağ eşlemesini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="4bcbb-145">Step 9: Configure network mapping</span></span>

<span data-ttu-id="4bcbb-146">Harita VMM VM ağları tooAzure sanal ağlar şirket içi.</span><span class="sxs-lookup"><span data-stu-id="4bcbb-146">Map on-premises VMM VM networks tooAzure virtual networks.</span></span> <span data-ttu-id="4bcbb-147">Yük devretme sonrasında Azure Vm'lerinin hello hangi hello kaynak Hyper-V bulunduğu toohello şirket içi VM ağ eşlemeleri Azure ağı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="4bcbb-147">After failover, Azure VMs are created in hello Azure network that maps toohello on-premises VM network in which hello source Hyper-V is located.</span></span>

<span data-ttu-id="4bcbb-148">Çok Git[adım 9: ağ eşlemesini yapılandırma](vmm-to-azure-walkthrough-network-mapping.md)</span><span class="sxs-lookup"><span data-stu-id="4bcbb-148">Go too[Step 9: Configure network mapping](vmm-to-azure-walkthrough-network-mapping.md)</span></span>


## <a name="step-10-set-up-a-replication-policy"></a><span data-ttu-id="4bcbb-149">10. adım: Bir çoğaltma ilkesi ayarlama</span><span class="sxs-lookup"><span data-stu-id="4bcbb-149">Step 10: Set up a replication policy</span></span>

<span data-ttu-id="4bcbb-150">Şirket içi sanal makineleri çoğaltılmış tooAzure ne olacağını belirtin.</span><span class="sxs-lookup"><span data-stu-id="4bcbb-150">Specify how on-premises VMs will be replicated tooAzure.</span></span>

<span data-ttu-id="4bcbb-151">Çok Git[adım 10: bir çoğaltma ilkesini ayarlayın](vmm-to-azure-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="4bcbb-151">Go too[Step 10: Set up a replication policy](vmm-to-azure-walkthrough-replication.md)</span></span>


## <a name="step-11-enable-replication-for-vms"></a><span data-ttu-id="4bcbb-152">11. adım: sanal makineleri için çoğaltmayı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="4bcbb-152">Step 11: Enable replication for VMs</span></span>

<span data-ttu-id="4bcbb-153">Tooreplicate istediğiniz hello sanal makineleri seçin.</span><span class="sxs-lookup"><span data-stu-id="4bcbb-153">Select hello VMs you want tooreplicate.</span></span> <span data-ttu-id="4bcbb-154">Bir VM için çoğaltma Tetikleyicileri hello ilk çoğaltma tooAzure etkinleştirildikten sonra devam eden değişim çoğaltması tarafından kullanılıyordu.</span><span class="sxs-lookup"><span data-stu-id="4bcbb-154">ENabling a VM for replication triggers hello initial replication tooAzure, followed by ongoing delta replication.</span></span>

<span data-ttu-id="4bcbb-155">Çok Git[adım 11: çoğaltmasını etkinleştir](vmm-to-azure-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="4bcbb-155">Go too[Step 11: Enable replication](vmm-to-azure-walkthrough-enable-replication.md)</span></span>


## <a name="step-12-run-a-test-failover"></a><span data-ttu-id="4bcbb-156">12. adım: yük devretme testi çalıştırma</span><span class="sxs-lookup"><span data-stu-id="4bcbb-156">Step 12: Run a test failover</span></span>

<span data-ttu-id="4bcbb-157">Her şeyin beklendiği gibi çalıştığından emin bir test yük devretme toomake çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="4bcbb-157">Run a test failover toomake sure everything's working as expected.</span></span>

<span data-ttu-id="4bcbb-158">Çok Git[adım 12: yük devretme testi çalıştırma](vmm-to-azure-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="4bcbb-158">Go too[Step 12: Run a test failover](vmm-to-azure-walkthrough-test-failover.md)</span></span>


