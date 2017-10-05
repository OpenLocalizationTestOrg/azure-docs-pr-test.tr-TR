---
title: "Azure Site Recovery ve PowerShell (Resource Manager) kullanarak VMM bulutlarındaki Hyper-V sanal makineleri çoğaltmak | Microsoft Docs"
description: "Azure Site Recovery ve PowerShell kullanarak VMM bulutlarındaki Hyper-V sanal makinelerini çoğaltma"
services: site-recovery
documentationcenter: 
author: Rajani-Janaki-Ram
manager: rochakm
editor: raynew
ms.assetid: 6ac509ad-5024-43d8-b621-d8fec019b9a9
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: rajanaki
ms.openlocfilehash: 34086044db752f09f1282517b59856091e85c2fc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-to-azure-using-powershell-and-azure-resource-manager"></a><span data-ttu-id="82fe1-103">VMM bulutlarındaki Hyper-V sanal makineleri PowerShell ve Azure Resource Manager kullanarak azure'a</span><span class="sxs-lookup"><span data-stu-id="82fe1-103">Replicate Hyper-V virtual machines in VMM clouds to Azure using PowerShell and Azure Resource Manager</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="82fe1-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="82fe1-104">Azure Portal</span></span>](site-recovery-vmm-to-azure.md)
> * [<span data-ttu-id="82fe1-105">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="82fe1-105">PowerShell - Resource Manager</span></span>](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [<span data-ttu-id="82fe1-106">Klasik Portal</span><span class="sxs-lookup"><span data-stu-id="82fe1-106">Classic Portal</span></span>](site-recovery-vmm-to-azure-classic.md)
> * [<span data-ttu-id="82fe1-107">PowerShell - Klasik</span><span class="sxs-lookup"><span data-stu-id="82fe1-107">PowerShell - Classic</span></span>](site-recovery-deploy-with-powershell.md)
>
>

## <a name="overview"></a><span data-ttu-id="82fe1-108">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="82fe1-108">Overview</span></span>
<span data-ttu-id="82fe1-109">Azure Site Recovery, çoğaltma, yük devretme ve kurtarma çeşitli dağıtım senaryolarında sanal makinelerin düzenleyerek iş sürekliliği ve olağanüstü durum kurtarma (BCDR) stratejinize katkı sağlar.</span><span class="sxs-lookup"><span data-stu-id="82fe1-109">Azure Site Recovery contributes to your business continuity and disaster recovery (BCDR) strategy by orchestrating replication, failover and recovery of virtual machines in a number of deployment scenarios.</span></span> <span data-ttu-id="82fe1-110">Dağıtım tam listesi için bkz: senaryoları [Azure Site Recovery genel bakış](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="82fe1-110">For a full list of deployment scenarios see the [Azure Site Recovery overview](site-recovery-overview.md).</span></span>

<span data-ttu-id="82fe1-111">Bu makalede Azure depolama alanına System Center VMM bulutlarındaki Hyper-V sanal makineleri çoğaltmak için Azure Site Recovery ayarladığınızda, yapmanız gereken ortak görevleri otomatik hale getirmek için PowerShell kullanmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="82fe1-111">This article shows you how to use PowerShell to automate common tasks you need to perform when you set up Azure Site Recovery to replicate Hyper-V virtual machines in System Center VMM clouds to Azure storage.</span></span>

<span data-ttu-id="82fe1-112">Makaleyi senaryonun önkoşulları içerir ve gösterir</span><span class="sxs-lookup"><span data-stu-id="82fe1-112">The article includes prerequisites for the scenario, and shows you</span></span>

* <span data-ttu-id="82fe1-113">Bir kurtarma Hizmetleri kasasını nasıl kurulur</span><span class="sxs-lookup"><span data-stu-id="82fe1-113">How to set up a Recovery Services Vault</span></span>
* <span data-ttu-id="82fe1-114">Kaynak VMM sunucusunda Azure Site kurtarma Sağlayıcısı'nı yükleme</span><span class="sxs-lookup"><span data-stu-id="82fe1-114">Install the Azure Site Recovery Provider on the source VMM server</span></span>
* <span data-ttu-id="82fe1-115">Sunucuyu kasaya kaydetmek, bir Azure depolama hesabı ekleme</span><span class="sxs-lookup"><span data-stu-id="82fe1-115">Register the server in the vault, add an Azure storage account</span></span>
* <span data-ttu-id="82fe1-116">Azure kurtarma Hizmetleri aracısını Hyper-V ana bilgisayar sunucularına yükleyin</span><span class="sxs-lookup"><span data-stu-id="82fe1-116">Install the Azure Recovery Services agent on Hyper-V host servers</span></span>
* <span data-ttu-id="82fe1-117">Tüm korumalı sanal makinelere uygulanacak VMM Bulutları için koruma ayarlarını yapılandırın</span><span class="sxs-lookup"><span data-stu-id="82fe1-117">Configure protection settings for VMM clouds, that will be applied to all protected virtual machines</span></span>
* <span data-ttu-id="82fe1-118">Bu sanal makineler için korumayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="82fe1-118">Enable protection for those virtual machines.</span></span>
* <span data-ttu-id="82fe1-119">Her şeyin beklendiği gibi çalıştığından emin olmak için yük devretme testi.</span><span class="sxs-lookup"><span data-stu-id="82fe1-119">Test the fail-over to make sure everything's working as expected.</span></span>

<span data-ttu-id="82fe1-120">Bu senaryoyu oluşturan ayarlama sorunlarını alıyorsanız, üzerinde sorularınızı [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="82fe1-120">If you run into problems setting up this scenario, post your questions on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

> [!NOTE]
> <span data-ttu-id="82fe1-121">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="82fe1-121">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="82fe1-122">Bu makalede, Resource Manager dağıtım modeli kullanılarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="82fe1-122">This article covers using the Resource Manager deployment model.</span></span>
>
>

## <a name="before-you-start"></a><span data-ttu-id="82fe1-123">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="82fe1-123">Before you start</span></span>
<span data-ttu-id="82fe1-124">Bu Önkoşullar sağladığınızdan emin olun:</span><span class="sxs-lookup"><span data-stu-id="82fe1-124">Make sure you have these prerequisites in place:</span></span>

### <a name="azure-prerequisites"></a><span data-ttu-id="82fe1-125">Azure önkoşulları</span><span class="sxs-lookup"><span data-stu-id="82fe1-125">Azure prerequisites</span></span>
* <span data-ttu-id="82fe1-126">Bir [Microsoft Azure](https://azure.microsoft.com/) hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="82fe1-126">You'll need a [Microsoft Azure](https://azure.microsoft.com/) account.</span></span> <span data-ttu-id="82fe1-127">Yoksa, başlayan bir [ücretsiz bir hesap](https://azure.microsoft.com/free).</span><span class="sxs-lookup"><span data-stu-id="82fe1-127">If you don't have one, start with a [free account](https://azure.microsoft.com/free).</span></span> <span data-ttu-id="82fe1-128">Ayrıca, hakkında bilgi edinebilirsiniz [Azure Site Recovery Manager fiyatlandırma](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="82fe1-128">In addition, you can read about the [Azure Site Recovery Manager pricing](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
* <span data-ttu-id="82fe1-129">Bir CSP abonelik senaryosuna çoğaltma çıkışı çalışıyorsanız, CSP aboneliğine sahip olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="82fe1-129">You'll need a CSP subscription if you are trying out the replication to a CSP subscription scenario.</span></span> <span data-ttu-id="82fe1-130">CSP programı hakkında daha fazla bilgi [CSP programa nasıl](https://msdn.microsoft.com/library/partnercenter/mt156995.aspx).</span><span class="sxs-lookup"><span data-stu-id="82fe1-130">Learn more about the CSP program in [how to enroll in the CSP program](https://msdn.microsoft.com/library/partnercenter/mt156995.aspx).</span></span>
* <span data-ttu-id="82fe1-131">Azure'a çoğaltılan verileri depolamak için bir Azure v2 (Resource Manager) depolama hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="82fe1-131">You'll need an Azure v2 storage (Resource Manager) account to store data replicated to Azure.</span></span> <span data-ttu-id="82fe1-132">Hesap coğrafi çoğaltmanın etkinleştirilmiş olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="82fe1-132">The account needs geo-replication enabled.</span></span> <span data-ttu-id="82fe1-133">Azure Site Recovery hizmeti ile aynı bölgede olması ve aynı abonelik veya CSP abonelik ile ilişkilendirilmiş olması.</span><span class="sxs-lookup"><span data-stu-id="82fe1-133">It should be in the same region as the Azure Site Recovery service, and be associated with the same subscription or the CSP subscription.</span></span> <span data-ttu-id="82fe1-134">Azure depolama ortamını ayarlama hakkında daha fazla bilgi için bkz: [Microsoft Azure Storage'a giriş](../storage/common/storage-introduction.md) başvuru.</span><span class="sxs-lookup"><span data-stu-id="82fe1-134">To learn more about setting up Azure storage, see the [Introduction to Microsoft Azure Storage](../storage/common/storage-introduction.md) for reference.</span></span>
* <span data-ttu-id="82fe1-135">Korumak istediğiniz sanal makineleri ile uyumlu olduğundan emin olmak gerekir [Azure sanal makine önkoşulları](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="82fe1-135">You'll need to make sure that virtual machines you want to protect comply with the [Azure virtual machine prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>

> [!NOTE]
> <span data-ttu-id="82fe1-136">Şu anda yalnızca VM düzeyinde işlemleri Powershell aracılığıyla mümkündür.</span><span class="sxs-lookup"><span data-stu-id="82fe1-136">Currently, only VM level operations are possible through Powershell.</span></span> <span data-ttu-id="82fe1-137">Kurtarma planı düzeyi işlemleri için destek yakında sunulacaktır.</span><span class="sxs-lookup"><span data-stu-id="82fe1-137">Support for recovery plan level operations will be made soon.</span></span>  <span data-ttu-id="82fe1-138">Şu an için başarısız-belirlemez yalnızca 'VM korumalı' ayrıntı düzeyi ve düzeyinde bir kurtarma planı gerçekleştirmeye sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="82fe1-138">For now, you are limited to performing fail-overs only at a ‘protected VM’ granularity and not at a Recovery Plan level.</span></span>
>
>

### <a name="vmm-prerequisites"></a><span data-ttu-id="82fe1-139">VMM önkoşulları</span><span class="sxs-lookup"><span data-stu-id="82fe1-139">VMM prerequisites</span></span>
* <span data-ttu-id="82fe1-140">System Center 2012 R2 üzerinde çalışan VMM sunucusu gerekir.</span><span class="sxs-lookup"><span data-stu-id="82fe1-140">You'll need VMM server running on System Center 2012 R2.</span></span>
* <span data-ttu-id="82fe1-141">Korumak istediğiniz sanal makineleri içeren herhangi bir VMM sunucusuna Azure Site kurtarma Sağlayıcısı'nı çalıştırması gerekir.</span><span class="sxs-lookup"><span data-stu-id="82fe1-141">Any VMM server containing virtual machines you want to protect must be running the Azure Site Recovery Provider.</span></span> <span data-ttu-id="82fe1-142">Bu Azure Site Recovery dağıtımı sırasında yüklenir.</span><span class="sxs-lookup"><span data-stu-id="82fe1-142">This is installed during the Azure Site Recovery deployment.</span></span>
* <span data-ttu-id="82fe1-143">Korumak istediğiniz VMM sunucusunda en az bir bulut gerekir.</span><span class="sxs-lookup"><span data-stu-id="82fe1-143">You'll need at least one cloud on the VMM server you want to protect.</span></span> <span data-ttu-id="82fe1-144">Bulut içermelidir:</span><span class="sxs-lookup"><span data-stu-id="82fe1-144">The cloud should contain:</span></span>
  * <span data-ttu-id="82fe1-145">Bir veya birden çok VMM ana bilgisayar grubu.</span><span class="sxs-lookup"><span data-stu-id="82fe1-145">One or more VMM host groups.</span></span>
  * <span data-ttu-id="82fe1-146">Her ana bilgisayar grubunda bir veya daha fazla Hyper-V sunucusu ya da kümesi.</span><span class="sxs-lookup"><span data-stu-id="82fe1-146">One or more Hyper-V host servers or clusters in each host group.</span></span>
  * <span data-ttu-id="82fe1-147">Kaynak Hyper-V sunucu üzerindeki bir veya daha fazla sanal makineler.</span><span class="sxs-lookup"><span data-stu-id="82fe1-147">One or more virtual machines on the source Hyper-V server.</span></span>
* <span data-ttu-id="82fe1-148">VMM bulutlarını ayarlama hakkında daha fazla bilgi edinin:</span><span class="sxs-lookup"><span data-stu-id="82fe1-148">Learn more about setting up VMM clouds:</span></span>
  * <span data-ttu-id="82fe1-149">Özel VMM bulutlarındaki hakkında daha fazla bilgiyi [System Center 2012 R2 VMM ile özel bulut yenilikler](http://go.microsoft.com/fwlink/?LinkId=324952) ve [VMM 2012 ve Bulutları](http://go.microsoft.com/fwlink/?LinkId=324956).</span><span class="sxs-lookup"><span data-stu-id="82fe1-149">Read more about private VMM clouds in [What’s New in Private Cloud with System Center 2012 R2 VMM](http://go.microsoft.com/fwlink/?LinkId=324952) and in [VMM 2012 and the clouds](http://go.microsoft.com/fwlink/?LinkId=324956).</span></span>
  * <span data-ttu-id="82fe1-150">Hakkında bilgi edinin [VMM bulut yapı](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric)</span><span class="sxs-lookup"><span data-stu-id="82fe1-150">Learn about [Configuring the VMM cloud fabric](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric)</span></span>
  * <span data-ttu-id="82fe1-151">Bulut doku öğelerinizi hazır olduktan sonra özel bulutta oluşturma hakkında bilgi edinin [VMM'de özel bulut oluşturma](http://go.microsoft.com/fwlink/p/?LinkId=324953) ve [izlenecek yol: System Center 2012 SP1 VMM içeren özel bulut oluşturma](http://go.microsoft.com/fwlink/p/?LinkId=324954).</span><span class="sxs-lookup"><span data-stu-id="82fe1-151">After your cloud fabric elements are in place learn about creating private clouds in [Creating a private cloud in VMM](http://go.microsoft.com/fwlink/p/?LinkId=324953) and in [Walkthrough: Creating private clouds with System Center 2012 SP1 VMM](http://go.microsoft.com/fwlink/p/?LinkId=324954).</span></span>

### <a name="hyper-v-prerequisites"></a><span data-ttu-id="82fe1-152">Hyper-V önkoşulları</span><span class="sxs-lookup"><span data-stu-id="82fe1-152">Hyper-V prerequisites</span></span>
* <span data-ttu-id="82fe1-153">Hyper-V ana bilgisayar sunucuları en az çalıştırmalıdır **Windows Server 2012** Hyper-V rolüne sahip veya **Microsoft Hyper-V Server 2012** ve en son güncelleştirmelerin yüklü olması.</span><span class="sxs-lookup"><span data-stu-id="82fe1-153">The host Hyper-V servers must be running at least **Windows Server 2012** with Hyper-V role or **Microsoft Hyper-V Server 2012** and have the latest updates installed.</span></span>
* <span data-ttu-id="82fe1-154">Hyper-V'yi bir kümede çalıştırıyorsanız statik IP adresi temelli bir kümeye sahip olmanız durumunda küme aracısının otomatik olarak oluşturulamayacağını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="82fe1-154">If you're running Hyper-V in a cluster note that cluster broker isn't created automatically if you have a static IP address-based cluster.</span></span> <span data-ttu-id="82fe1-155">Küme aracısını sizin yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="82fe1-155">You'll need to configure the cluster broker manually.</span></span> <span data-ttu-id="82fe1-156">için</span><span class="sxs-lookup"><span data-stu-id="82fe1-156">For</span></span>
* <span data-ttu-id="82fe1-157">Yönergeler için bkz [Hyper-V çoğaltma aracısı yapılandırma nasıl](http://blogs.technet.com/b/haroldwong/archive/2013/03/27/server-virtualization-series-hyper-v-replica-broker-explained-part-15-of-20-by-yung-chou.aspx).</span><span class="sxs-lookup"><span data-stu-id="82fe1-157">For instructions see [How to Configure Hyper-V Replica Broker](http://blogs.technet.com/b/haroldwong/archive/2013/03/27/server-virtualization-series-hyper-v-replica-broker-explained-part-15-of-20-by-yung-chou.aspx).</span></span>
* <span data-ttu-id="82fe1-158">Herhangi bir Hyper-V konak sunucusu veya küme koruma yönetmek istediğiniz bir VMM bulutunda eklenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="82fe1-158">Any Hyper-V host server or cluster for which you want to manage protection must be included in a VMM cloud.</span></span>

### <a name="network-mapping-prerequisites"></a><span data-ttu-id="82fe1-159">Ağ eşlemesi önkoşulları</span><span class="sxs-lookup"><span data-stu-id="82fe1-159">Network mapping prerequisites</span></span>
<span data-ttu-id="82fe1-160">Ne zaman Azure, kaynak VMM sunucusunda sanal makine ağları ağ eşlemesi eşlemeleri sanal makinelerin korunmasına ve hedef Azure ağları aşağıdaki etkinleştirmek için:</span><span class="sxs-lookup"><span data-stu-id="82fe1-160">When you protect virtual machines in Azure, the network mapping  maps the virtual machine networks on the source VMM server and target Azure networks to enable the following:</span></span>

* <span data-ttu-id="82fe1-161">Aynı ağda yük devri tüm makineler birbirine, hangi kurtarma planında yer aldıklarına bulundukları bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="82fe1-161">All machines which fail over on the same network can connect to each other, irrespective of which recovery plan they are in.</span></span>
* <span data-ttu-id="82fe1-162">Bir ağ geçidi hedef Azure ağında ayarlanırsa sanal makineler diğer şirket içi sanal makinelere bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="82fe1-162">If a network gateway is setup on the target Azure network, virtual machines can connect to other on-premises virtual machines.</span></span>
* <span data-ttu-id="82fe1-163">Ağ eşlemesini yapılandırmazsanız yalnızca aynı kurtarma planında yük devri sanal makineleri azure'a yük devretme sonrasında birbirine kuramaz.</span><span class="sxs-lookup"><span data-stu-id="82fe1-163">If you don’t configure network mapping, only the virtual machines that fail over in the same recovery plan will be able to connect to each other after fail-over to Azure.</span></span>

<span data-ttu-id="82fe1-164">Ağ eşlemesi dağıtmak isterseniz şunlara ihtiyaç duyarsınız:</span><span class="sxs-lookup"><span data-stu-id="82fe1-164">If you want to deploy network mapping you'll need the following:</span></span>

* <span data-ttu-id="82fe1-165">Kaynak VMM sunucusunda korumak istediğinizde sanal makinelerin bir VM ağına bağlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="82fe1-165">The virtual machines you want to protect on the source VMM server should be connected to a VM network.</span></span> <span data-ttu-id="82fe1-166">Bu ağın, bulutla ilişkilendirilen mantıksal bir ağ ile bağlantılı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="82fe1-166">That network should be linked to a logical network that is associated with the cloud.</span></span>
* <span data-ttu-id="82fe1-167">Yük devretme çoğaltılmış sanal makinelerin bağlanabileceği bir Azure ağı.</span><span class="sxs-lookup"><span data-stu-id="82fe1-167">An Azure network to which replicated virtual machines can connect after fail-over.</span></span> <span data-ttu-id="82fe1-168">Yük devretme aynı anda bu ağ seçersiniz.</span><span class="sxs-lookup"><span data-stu-id="82fe1-168">You'll select this network at the time of fail-over.</span></span> <span data-ttu-id="82fe1-169">Ağın Azure Site Recovery aboneliğinizle aynı bölgede olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="82fe1-169">The network should be in the same region as your Azure Site Recovery subscription.</span></span>

<span data-ttu-id="82fe1-170">Ağ eşlemesi hakkında daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="82fe1-170">Learn more about network mapping in</span></span>

* [<span data-ttu-id="82fe1-171">VMM'de Mantıksal ağlar yapılandırma</span><span class="sxs-lookup"><span data-stu-id="82fe1-171">How to configure logical networks in VMM</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=386307)
* [<span data-ttu-id="82fe1-172">VMM'de VM ağları ve ağ geçitlerini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="82fe1-172">How to configure VM networks and gateways in VMM</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=386308)
* [<span data-ttu-id="82fe1-173">Nasıl yapılandırılacağı ve Azure sanal ağları izleme</span><span class="sxs-lookup"><span data-stu-id="82fe1-173">How to configure and monitor virtual networks in Azure</span></span>](https://azure.microsoft.com/documentation/services/virtual-network/)

### <a name="powershell-prerequisites"></a><span data-ttu-id="82fe1-174">PowerShell önkoşulları</span><span class="sxs-lookup"><span data-stu-id="82fe1-174">PowerShell prerequisites</span></span>
<span data-ttu-id="82fe1-175">Azure PowerShell davranmaya hazır olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="82fe1-175">Make sure you have Azure PowerShell ready to go.</span></span> <span data-ttu-id="82fe1-176">PowerShell zaten kullanıyorsanız, 0.8.10 sürümüne yükseltme veya üstü gerekir.</span><span class="sxs-lookup"><span data-stu-id="82fe1-176">If you are already using PowerShell, you'll need to upgrade to version 0.8.10 or later.</span></span> <span data-ttu-id="82fe1-177">PowerShell ayarlama hakkında daha fazla bilgi için bkz: [Azure PowerShell'i yükleme ve yapılandırma için kılavuz](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="82fe1-177">For information about setting up PowerShell, see the [Guide to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="82fe1-178">Ayarlama ve PowerShell yapılandırılmış sonra tüm kullanılabilir cmdlet'leri hizmeti görüntüleyebilirsiniz [burada](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="82fe1-178">Once you have set up and configured PowerShell, you can view all of the available cmdlets for the service [here](/powershell/azure/overview).</span></span>

<span data-ttu-id="82fe1-179">Parametre değerleri, girişleri ve çıkışları genellikle Azure PowerShell'de işlenme gibi cmdlet'leri kullanın yardımcı olabilecek ipuçları hakkında bilgi edinmek için bkz [Azure cmdlet'leri kullanmaya başlama Kılavuzu](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="82fe1-179">To learn about tips that can help you use the cmdlets, such as how parameter values, inputs, and outputs are typically handled in Azure PowerShell, see the [Guide to get Started with Azure Cmdlets](/powershell/azure/get-started-azureps).</span></span>

## <a name="step-1-set-the-subscription"></a><span data-ttu-id="82fe1-180">1. adım: Abonelik ayarlama</span><span class="sxs-lookup"><span data-stu-id="82fe1-180">Step 1: Set the subscription</span></span>
1. <span data-ttu-id="82fe1-181">Azure powershell'den Azure hesabınızda oturum açın: aşağıdaki cmdlet'leri kullanarak</span><span class="sxs-lookup"><span data-stu-id="82fe1-181">From Azure powershell, login to your Azure account: using the following cmdlets</span></span>

        $UserName = "<user@live.com>"
        $Password = "<password>"
        $SecurePassword = ConvertTo-SecureString -AsPlainText $Password -Force
        $Cred = New-Object System.Management.Automation.PSCredential -ArgumentList $UserName, $SecurePassword
        Login-AzureRmAccount #-Credential $Cred
2. <span data-ttu-id="82fe1-182">Aboneliklerinizi listesini alın.</span><span class="sxs-lookup"><span data-stu-id="82fe1-182">Get a list of your subscriptions.</span></span> <span data-ttu-id="82fe1-183">Bu da subscriptionIDs her abonelik için listeler.</span><span class="sxs-lookup"><span data-stu-id="82fe1-183">This will also list the subscriptionIDs for each of the subscriptions.</span></span> <span data-ttu-id="82fe1-184">Kurtarma Hizmetleri kasası oluşturmak istediğiniz aboneliği Subscriptionıd unutmayın</span><span class="sxs-lookup"><span data-stu-id="82fe1-184">Note down the subscriptionID of the subscription in which you wish to create the recovery services vault</span></span>

        Get-AzureRmSubscription
3. <span data-ttu-id="82fe1-185">Kurtarma Hizmetleri kasası abonelik kimliği söz tarafından oluşturulacak olan abonelik ayarlayın</span><span class="sxs-lookup"><span data-stu-id="82fe1-185">Set the subscription in which the recovery services vault is to be created by mentioning the subscription ID</span></span>

        Set-AzureRmContext –SubscriptionID <subscriptionId>

## <a name="step-2-create-a-recovery-services-vault"></a><span data-ttu-id="82fe1-186">2. Adım: Bir Kurtarma Hizmetleri kasası oluşturma</span><span class="sxs-lookup"><span data-stu-id="82fe1-186">Step 2: Create a Recovery Services vault</span></span>
1. <span data-ttu-id="82fe1-187">Zaten yoksa, Azure Kaynak Yöneticisi'nde bir kaynak grubu oluştur</span><span class="sxs-lookup"><span data-stu-id="82fe1-187">Create a resource group  in Azure Resource Manager if you don't have one already</span></span>

        New-AzureRmResourceGroup -Name #ResourceGroupName -Location #location
2. <span data-ttu-id="82fe1-188">Yeni bir kurtarma Hizmetleri kasası oluşturun ve oluşturulan ASR kasası nesnesi (daha sonra kullanılacak) bir değişkene kaydedin.</span><span class="sxs-lookup"><span data-stu-id="82fe1-188">Create a new Recovery Services vault and save the created ASR vault object in a variable (will be used later).</span></span> <span data-ttu-id="82fe1-189">Get-AzureRMRecoveryServicesVault cmdlet'ini kullanarak ASR kasası nesne post oluşturma de alabilirsiniz:-</span><span class="sxs-lookup"><span data-stu-id="82fe1-189">You can also retrieve the ASR vault object post creation using the Get-AzureRMRecoveryServicesVault cmdlet:-</span></span>

        $vault = New-AzureRmRecoveryServicesVault -Name #vaultname -ResouceGroupName #ResourceGroupName -Location #location

## <a name="step-3-set-the-recovery-services-vault-context"></a><span data-ttu-id="82fe1-190">3. adım: Kurtarma Hizmetleri kasası bağlamını ayarlayın</span><span class="sxs-lookup"><span data-stu-id="82fe1-190">Step 3: Set the Recovery Services Vault context</span></span>

<span data-ttu-id="82fe1-191">Çalıştırarak kasası bağlamını ayarlayın aşağıda komutu.</span><span class="sxs-lookup"><span data-stu-id="82fe1-191">Set the vault context by running the below command.</span></span>

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-install-the-azure-site-recovery-provider"></a><span data-ttu-id="82fe1-192">4. adım: Azure Site kurtarma Sağlayıcısı'nı yükleme</span><span class="sxs-lookup"><span data-stu-id="82fe1-192">Step 4: Install the Azure Site Recovery Provider</span></span>
1. <span data-ttu-id="82fe1-193">VMM makinesinde aşağıdaki komutu çalıştırarak bir dizin oluşturun:</span><span class="sxs-lookup"><span data-stu-id="82fe1-193">On the VMM machine, create a directory by running the following command:</span></span>

       New-Item c:\ASR -type directory
2. <span data-ttu-id="82fe1-194">Aşağıdaki komutu çalıştırarak indirilen sağlayıcısını kullanarak dosyaları ayıklayın</span><span class="sxs-lookup"><span data-stu-id="82fe1-194">Extract the files using the downloaded provider by running the following command</span></span>

       pushd C:\ASR\
       .\AzureSiteRecoveryProvider.exe /x:. /q
3. <span data-ttu-id="82fe1-195">Aşağıdaki komutları kullanarak sağlayıcısını yükleyin:</span><span class="sxs-lookup"><span data-stu-id="82fe1-195">Install the provider using the following commands:</span></span>

       .\SetupDr.exe /i
       $installationRegPath = "hklm:\software\Microsoft\Microsoft System Center Virtual Machine Manager Server\DRAdapter"
       do
       {
         $isNotInstalled = $true;
         if(Test-Path $installationRegPath)
         {
           $isNotInstalled = $false;
         }
       }While($isNotInstalled)

   <span data-ttu-id="82fe1-196">Yüklemesinin tamamlanması için bekleyin.</span><span class="sxs-lookup"><span data-stu-id="82fe1-196">Wait for the installation to finish.</span></span>
4. <span data-ttu-id="82fe1-197">Sunucu aşağıdaki komutu kullanarak kasaya kaydedin:</span><span class="sxs-lookup"><span data-stu-id="82fe1-197">Register the server in the vault using the following command:</span></span>

       $BinPath = $env:SystemDrive+"\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin"
       pushd $BinPath
       $encryptionFilePath = "C:\temp\".\DRConfigurator.exe /r /Credentials $VaultSettingFilePath /vmmfriendlyname $env:COMPUTERNAME /dataencryptionenabled $encryptionFilePath /startvmmservice

## <a name="step-5-create-an-azure-storage-account"></a><span data-ttu-id="82fe1-198">5. adım: Azure storage hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="82fe1-198">Step 5: Create an Azure storage account</span></span>

<span data-ttu-id="82fe1-199">Bir Azure depolama hesabınız yoksa, bir coğrafi çoğaltmanın etkinleştirilmiş hesabı kasa ile aynı coğrafi bölgede aşağıdaki komutu çalıştırarak oluşturun:</span><span class="sxs-lookup"><span data-stu-id="82fe1-199">If you don't have an Azure storage account, create a geo-replication enabled account in the same geo as the vault by running the following command:</span></span>

        $StorageAccountName = "teststorageacc1"    #StorageAccountname
        $StorageAccountGeo  = "Southeast Asia"     
        $ResourceGroupName =  “myRG”             #ResourceGroupName
        $RecoveryStorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageAccountName -Type “StandardGRS” -Location $StorageAccountGeo

<span data-ttu-id="82fe1-200">Depolama hesabı gerekir Azure Site Recovery hizmeti ile aynı bölgede olması ve aynı abonelikle ilişkilendirilmiş olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="82fe1-200">Note that the storage account must be in the same region as the Azure Site Recovery service, and be associated with the same subscription.</span></span>

## <a name="step-6-install-the-azure-recovery-services-agent"></a><span data-ttu-id="82fe1-201">6. adım: Azure kurtarma Hizmetleri Aracısı yükleme</span><span class="sxs-lookup"><span data-stu-id="82fe1-201">Step 6: Install the Azure Recovery Services Agent</span></span>
1. <span data-ttu-id="82fe1-202">Konumundaki Azure kurtarma Hizmetleri Aracısı'nı indirme [http://aka.ms/latestmarsagent](http://aka.ms/latestmarsagent) ve korumak istediğiniz VMM bulutlarında yer alan her Hyper-V ana bilgisayar sunucusunda yükleyin.</span><span class="sxs-lookup"><span data-stu-id="82fe1-202">Download the Azure Recovery Services agent at [http://aka.ms/latestmarsagent](http://aka.ms/latestmarsagent) and install it on each Hyper-V host server located in the VMM clouds you want to protect.</span></span>
2. <span data-ttu-id="82fe1-203">Tüm VMM ana bilgisayarlarda aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="82fe1-203">Run the following command on all VMM hosts:</span></span>

       marsagentinstaller.exe /q /nu

## <a name="step-7-configure-cloud-protection-settings"></a><span data-ttu-id="82fe1-204">7. adım: Bulut yapılandırma koruma ayarları</span><span class="sxs-lookup"><span data-stu-id="82fe1-204">Step 7: Configure cloud protection settings</span></span>
1. <span data-ttu-id="82fe1-205">Aşağıdaki komutu çalıştırarak Azure bir çoğaltma ilkesi oluşturun:</span><span class="sxs-lookup"><span data-stu-id="82fe1-205">Create a replication policy to Azure by running the following command:</span></span>

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $Recoverypoints = 6                    #specify the number of recovery points

        $policryresult = New-AzureRmSiteRecoveryPolicy -Name $policyname -ReplicationProvider HyperVReplicaAzure -ReplicationFrequencyInSeconds $replicationfrequencyinseconds -RecoveryPoints $recoverypoints -ApplicationConsistentSnapshotFrequencyInHours 1 -RecoveryAzureStorageAccountId "/subscriptions/q1345667/resourceGroups/test/providers/Microsoft.Storage/storageAccounts/teststorageacc1"

1. <span data-ttu-id="82fe1-206">Koruma kapsayıcısı aşağıdaki komutları çalıştırarak alın:</span><span class="sxs-lookup"><span data-stu-id="82fe1-206">Get a protection container by running the following commands:</span></span>

       $PrimaryCloud = "testcloud"
       $protectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloud;  
2. <span data-ttu-id="82fe1-207">Oluşturulan iş kullanarak ve kolay ilke adı söz bir değişkene ilke ayrıntıları alın:</span><span class="sxs-lookup"><span data-stu-id="82fe1-207">Get the policy details to a variable using the job that was created and mentioning the friendly policy name:</span></span>

       $policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $policyname
3. <span data-ttu-id="82fe1-208">Koruma kapsayıcısı ilişkisini çoğaltma ilkesiyle başlatın:</span><span class="sxs-lookup"><span data-stu-id="82fe1-208">Start the association of the protection container with the replication policy:</span></span>

       $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy     $Policy -PrimaryProtectionContainer $protectionContainer  
4. <span data-ttu-id="82fe1-209">İş tamamlandıktan sonra aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="82fe1-209">After the job has finished, run the following command:</span></span>

       $job = Get-AzureRmSiteRecoveryJob -Job $associationJob

       if($job -eq $null -or $job.StateDescription -ne "Completed")
       {
         $isJobLeftForProcessing = $true;
       }
5. <span data-ttu-id="82fe1-210">İş işlemeyi bitirdikten sonra aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="82fe1-210">After the job has finished processing, run the following command:</span></span>

       if($isJobLeftForProcessing)
       {
         Start-Sleep -Seconds 60
       }
       }While($isJobLeftForProcessing)

<span data-ttu-id="82fe1-211">İşlemin tamamlanması denetlemek için adımları [etkinliğini izleme](#monitor).</span><span class="sxs-lookup"><span data-stu-id="82fe1-211">To check the completion of the operation, follow the steps in [Monitor Activity](#monitor).</span></span>

## <a name="step-8-configure-network-mapping"></a><span data-ttu-id="82fe1-212">8. adım: ağ eşlemesini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="82fe1-212">Step 8: Configure network mapping</span></span>
<span data-ttu-id="82fe1-213">Ağ eşlemesine başlamadan önce kaynak VMM sunucusundaki sanal makinelerin bir VM ağına bağlı olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="82fe1-213">Before you begin network mapping verify that virtual machines on the source VMM server are connected to a VM network.</span></span> <span data-ttu-id="82fe1-214">Ayrıca, bir veya daha fazla Azure sanal ağı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="82fe1-214">In addition, create one or more Azure virtual networks.</span></span>

<span data-ttu-id="82fe1-215">Azure Resource Manager ve PowerShell kullanarak bir sanal ağ oluşturma hakkında daha fazla bilgi [Azure Resource Manager ve PowerShell kullanarak siteden siteye VPN bağlantısı olan bir sanal ağ oluşturma](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="82fe1-215">Learn more about how to create a virtual network using Azure Resource Manager and PowerShell, in [Create a virtual network with a site-to-site VPN connection using Azure Resource Manager and PowerShell](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)</span></span>

<span data-ttu-id="82fe1-216">Birden çok sanal makine ağları tek bir Azure ağına eşlenebileceğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="82fe1-216">Note that multiple Virtual Machine networks can be mapped to a single Azure network.</span></span> <span data-ttu-id="82fe1-217">Hedef ağın birden çok alt ağı varsa ve bu alt ağlardan biri kaynak sanal makinenin bulunduğu alt ağ ile aynı ada sahip, ardından çoğaltma sanal makinesi yük devretme, hedef alt ağa bağlanır.</span><span class="sxs-lookup"><span data-stu-id="82fe1-217">If the target network has multiple subnets and one of those subnets has the same name as subnet on which the source virtual machine is located, then the replica virtual machine will be connected to that target subnet after fail-over.</span></span> <span data-ttu-id="82fe1-218">Eşleşen ada sahip bir hedef alt ağ ise sanal makine ağdaki ilk alt ağa bağlanır.</span><span class="sxs-lookup"><span data-stu-id="82fe1-218">If there is no target subnet with a matching name, the virtual machine will be connected to the first subnet in the network.</span></span>

1. <span data-ttu-id="82fe1-219">İlk komut sunucuları için geçerli Azure Site Recovery kasası alır.</span><span class="sxs-lookup"><span data-stu-id="82fe1-219">The first command gets servers for the current Azure Site Recovery vault.</span></span> <span data-ttu-id="82fe1-220">Komut Microsoft Azure Site Recovery sunucuları $Servers dizi değişkeninde depolar.</span><span class="sxs-lookup"><span data-stu-id="82fe1-220">The command stores the Microsoft Azure Site Recovery servers in the $Servers array variable.</span></span>

        $Servers = Get-AzureRmSiteRecoveryServer
2. <span data-ttu-id="82fe1-221">İkinci komut site kurtarma ağ $Servers dizinin ilk sunucusunu alır.</span><span class="sxs-lookup"><span data-stu-id="82fe1-221">The second command gets the site recovery network for the first server in the $Servers array.</span></span> <span data-ttu-id="82fe1-222">Komut ağları $Networks değişkeninde depolar.</span><span class="sxs-lookup"><span data-stu-id="82fe1-222">The command stores the networks in the $Networks variable.</span></span>

        $Networks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[0]

1. <span data-ttu-id="82fe1-223">Üçüncü komut $AzureVmNetworks değişkeninde Azure sanal ağlar ve bu değeri alır.</span><span class="sxs-lookup"><span data-stu-id="82fe1-223">The third command gets Azure virtual networks, and then that value in the $AzureVmNetworks variable.</span></span>

        $AzureVmNetworks =  Get-AzureRmVirtualNetwork
2. <span data-ttu-id="82fe1-224">Son cmdlet birincil ağ ve Azure sanal makine ağı arasında bir eşleme oluşturur.</span><span class="sxs-lookup"><span data-stu-id="82fe1-224">The final cmdlet creates a mapping between the primary network and the Azure virtual machine network.</span></span> <span data-ttu-id="82fe1-225">Cmdlet $Networks ilk öğe birincil ağı belirtir.</span><span class="sxs-lookup"><span data-stu-id="82fe1-225">The cmdlet specifies the primary network as the first element of $Networks.</span></span> <span data-ttu-id="82fe1-226">Cmdlet, bir sanal makine ağına $AzureVmNetworks ilk öğe belirtir.</span><span class="sxs-lookup"><span data-stu-id="82fe1-226">The cmdlet specifies a virtual machine network as the first element of $AzureVmNetworks.</span></span>

        New-AzureRmSiteRecoveryNetworkMapping -PrimaryNetwork $Networks[0] -AzureVMNetworkId $AzureVmNetworks[0]

## <a name="step-9-enable-protection-for-virtual-machines"></a><span data-ttu-id="82fe1-227">9. adım: sanal makineler için korumayı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="82fe1-227">Step 9: Enable protection for virtual machines</span></span>
<span data-ttu-id="82fe1-228">Sunucular, Bulutlar ve ağlar doğru şekilde yapılandırıldıktan sonra buluttaki sanal makineler için korumayı etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="82fe1-228">After the servers, clouds and networks are configured correctly, you can enable protection for virtual machines in the cloud.</span></span>

 <span data-ttu-id="82fe1-229">Şunlara dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="82fe1-229">Note the following:</span></span>

* <span data-ttu-id="82fe1-230">Sanal makineler Azure gereksinimleri karşılaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="82fe1-230">Virtual machines must meet Azure requirements.</span></span> <span data-ttu-id="82fe1-231">Bu iade [Önkoşullar ve Destek](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) Planlama Kılavuzu'nda.</span><span class="sxs-lookup"><span data-stu-id="82fe1-231">Check these in [Prerequisites and Support](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) in the planning guide.</span></span>
* <span data-ttu-id="82fe1-232">Koruma, işletim sistemi ve işletim sistemi etkinleştirmek için sanal makine için disk özellikleri de ayarlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="82fe1-232">To enable protection, the operating system and operating system disk properties must be set for the virtual machine.</span></span> <span data-ttu-id="82fe1-233">Sana makine şablonu kullanarak VMM'de bir sanal makine oluşturduğunuzda özelliği de ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="82fe1-233">When you create a virtual machine in VMM using a virtual machine template you can set the property.</span></span> <span data-ttu-id="82fe1-234">Ayrıca var olan sanal makineler için bu özellikleri, sanal makinenin **Genel** ve **Donanım Yapılandırması** sekmelerinde de ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="82fe1-234">You can also set these properties for existing virtual machines on the **General** and **Hardware Configuration** tabs of the virtual machine properties.</span></span> <span data-ttu-id="82fe1-235">Özellikleri VMM'de ayarlamazsanız Azure Site Recovery portalından da yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="82fe1-235">If you don't set these properties in VMM you'll be able to configure them in the Azure Site Recovery portal.</span></span>

1. <span data-ttu-id="82fe1-236">Korumayı etkinleştirmek için koruma kapsayıcısı almak için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="82fe1-236">To enable protection, run the following command to get the protection container:</span></span>

          $ProtectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $CloudName
2. <span data-ttu-id="82fe1-237">Korunan varlık (VM), aşağıdaki komutu çalıştırarak alın:</span><span class="sxs-lookup"><span data-stu-id="82fe1-237">Get the protection entity (VM) by running the following command:</span></span>

           $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -friendlyName $VMName -ProtectionContainer $protectionContainer
3. <span data-ttu-id="82fe1-238">DR VM için aşağıdaki komutu çalıştırarak etkinleştirin:</span><span class="sxs-lookup"><span data-stu-id="82fe1-238">Enable the DR for the VM by running the following command:</span></span>

          $jobResult = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionentity -Protection Enable –Force -Policy $policy -RecoveryAzureStorageAccountId  $storageID "/subscriptions/217653172865hcvkchgvd/resourceGroups/rajanirgps/providers/Microsoft.Storage/storageAccounts/teststorageacc1

## <a name="test-your-deployment"></a><span data-ttu-id="82fe1-239">Dağıtımınızı test edin</span><span class="sxs-lookup"><span data-stu-id="82fe1-239">Test your deployment</span></span>
<span data-ttu-id="82fe1-240">Dağıtımınızı test etmek için test yük devretme için tek bir sanal makine çalıştırmak veya birden çok sanal makine içeren bir kurtarma planı oluşturmak ve test yük devretme plan için çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="82fe1-240">To test your deployment you can run a test fail-over for a single virtual machine, or create a recovery plan consisting of multiple virtual machines and run a test fail-over for the plan.</span></span> <span data-ttu-id="82fe1-241">Test yük devretme, yük devretme ve kurtarma mekanizmanızı yalıtılmış bir ağda benzetimini yapar.</span><span class="sxs-lookup"><span data-stu-id="82fe1-241">Test fail-over simulates your fail-over and recovery mechanism in an isolated network.</span></span> <span data-ttu-id="82fe1-242">Şunlara dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="82fe1-242">Note that:</span></span>

* <span data-ttu-id="82fe1-243">Sonra Yük devretme Uzak Masaüstü'nü kullanarak azure'daki sanal makineye bağlanmak istiyorsanız, yük devretme testini çalıştırmadan önce sanal makinede Uzak Masaüstü Bağlantısı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="82fe1-243">If you want to connect to the virtual machine in Azure using Remote Desktop after the fail-over, enable Remote Desktop Connection on the virtual machine before you run the test failover.</span></span>
* <span data-ttu-id="82fe1-244">Yük devretme, Uzak Masaüstü'nü kullanarak azure'daki sanal makineye bağlanmak için bir ortak IP adresini kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="82fe1-244">After fail-over, you'll use a public IP address to connect to the virtual machine in Azure using Remote Desktop.</span></span> <span data-ttu-id="82fe1-245">Bu işlemi gerçekleştirmek isterseniz genel bir adres kullanarak sanal makineye bağlanmanızı engelleyecek etki alanı ilkelerine sahip olmadığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="82fe1-245">If you want to do this, ensure you don't have any domain policies that prevent you from connecting to a virtual machine using a public address.</span></span>

<span data-ttu-id="82fe1-246">İşlemin tamamlanması denetlemek için adımları [etkinliğini izleme](#monitor).</span><span class="sxs-lookup"><span data-stu-id="82fe1-246">To check the completion of the operation, follow the steps in [Monitor Activity](#monitor).</span></span>

### <a name="run-a-test-failover"></a><span data-ttu-id="82fe1-247">Yük devretme testi çalıştırma</span><span class="sxs-lookup"><span data-stu-id="82fe1-247">Run a test failover</span></span>
- <span data-ttu-id="82fe1-248">Aşağıdaki komutu çalıştırarak test yük devretme başlatın:</span><span class="sxs-lookup"><span data-stu-id="82fe1-248">Start the test failover by running the following command:</span></span>

       $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

### <a name="run-a-planned-failover"></a><span data-ttu-id="82fe1-249">Planlı yük devretmeyi çalıştırma</span><span class="sxs-lookup"><span data-stu-id="82fe1-249">Run a planned failover</span></span>
- <span data-ttu-id="82fe1-250">Aşağıdaki komutu çalıştırarak planlanmış yük devretme başlatın:</span><span class="sxs-lookup"><span data-stu-id="82fe1-250">Start the planned failover by running the following command:</span></span>

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

### <a name="run-an-unplanned-failover"></a><span data-ttu-id="82fe1-251">Planlanmamış bir yük devretmeyi çalıştırma</span><span class="sxs-lookup"><span data-stu-id="82fe1-251">Run an unplanned failover</span></span>
- <span data-ttu-id="82fe1-252">Aşağıdaki komutu çalıştırarak planlanmamış yük devretme başlatın:</span><span class="sxs-lookup"><span data-stu-id="82fe1-252">Start the unplanned failover by running the following command:</span></span>

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

## <span data-ttu-id="82fe1-253"><a name=monitor></a>Etkinliğini izleme</span><span class="sxs-lookup"><span data-stu-id="82fe1-253"><a name=monitor></a> Monitor Activity</span></span>
<span data-ttu-id="82fe1-254">Etkinliğini izlemek için aşağıdaki komutları kullanın.</span><span class="sxs-lookup"><span data-stu-id="82fe1-254">Use the following commands to monitor the activity.</span></span> <span data-ttu-id="82fe1-255">Bitirmek işleme işleri arasında beklemek zorunda unutmayın.</span><span class="sxs-lookup"><span data-stu-id="82fe1-255">Note that you have to wait in between jobs for the processing to finish.</span></span>

    Do
    {
        $job = Get-AzureSiteRecoveryJob -Id $associationJob.JobId;
        Write-Host "Job State:{0}, StateDescription:{1}" -f Job.State, $job.StateDescription;
        if($job -eq $null -or $job.StateDescription -ne "Completed")
        {
            $isJobLeftForProcessing = $true;
        }

    if($isJobLeftForProcessing)
        {
            Start-Sleep -Seconds 60
        }
    }While($isJobLeftForProcessing)



## <a name="next-steps"></a><span data-ttu-id="82fe1-256">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="82fe1-256">Next steps</span></span>
<span data-ttu-id="82fe1-257">[Daha fazla bilgi](/powershell/module/azurerm.recoveryservices.backup/#recovery) Azure Site Recovery ile Azure Resource Manager PowerShell cmdlet'leri hakkında.</span><span class="sxs-lookup"><span data-stu-id="82fe1-257">[Read more](/powershell/module/azurerm.recoveryservices.backup/#recovery) about Azure Site Recovery with Azure Resource Manager PowerShell cmdlets.</span></span>
