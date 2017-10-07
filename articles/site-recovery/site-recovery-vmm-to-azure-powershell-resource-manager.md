---
title: "PowerShell (Resource Manager) ve Azure Site Recovery kullanarak VMM bulutlarındaki aaaReplicate Hyper-V sanal makinelerini | Microsoft Docs"
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
ms.openlocfilehash: b0f641de4e10a600ead415ceb9bd488fb4d1659d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooazure-using-powershell-and-azure-resource-manager"></a><span data-ttu-id="a95c5-103">Hyper-V sanal makineleri PowerShell ve Azure Resource Manager kullanarak VMM Bulutları tooAzure Çoğalt</span><span class="sxs-lookup"><span data-stu-id="a95c5-103">Replicate Hyper-V virtual machines in VMM clouds tooAzure using PowerShell and Azure Resource Manager</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a95c5-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="a95c5-104">Azure Portal</span></span>](site-recovery-vmm-to-azure.md)
> * [<span data-ttu-id="a95c5-105">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a95c5-105">PowerShell - Resource Manager</span></span>](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [<span data-ttu-id="a95c5-106">Klasik Portal</span><span class="sxs-lookup"><span data-stu-id="a95c5-106">Classic Portal</span></span>](site-recovery-vmm-to-azure-classic.md)
> * [<span data-ttu-id="a95c5-107">PowerShell - Klasik</span><span class="sxs-lookup"><span data-stu-id="a95c5-107">PowerShell - Classic</span></span>](site-recovery-deploy-with-powershell.md)
>
>

## <a name="overview"></a><span data-ttu-id="a95c5-108">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="a95c5-108">Overview</span></span>
<span data-ttu-id="a95c5-109">Azure Site Recovery, çoğaltma, yük devretme ve kurtarma çeşitli dağıtım senaryolarında sanal makinelerin düzenleyerek tooyour iş sürekliliği ve olağanüstü durum kurtarma (BCDR) stratejinize katkı sağlar.</span><span class="sxs-lookup"><span data-stu-id="a95c5-109">Azure Site Recovery contributes tooyour business continuity and disaster recovery (BCDR) strategy by orchestrating replication, failover and recovery of virtual machines in a number of deployment scenarios.</span></span> <span data-ttu-id="a95c5-110">Dağıtım tam listesi için bkz: hello senaryoları [Azure Site Recovery genel bakış](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a95c5-110">For a full list of deployment scenarios see hello [Azure Site Recovery overview](site-recovery-overview.md).</span></span>

<span data-ttu-id="a95c5-111">Bu makalede, Azure Site Recovery tooreplicate Hyper-V sanal makineleri System Center VMM Bulutları tooAzure depolama ayarlarken nasıl toouse PowerShell tooautomate ortak görevleri tooperform ihtiyacınız gösterir.</span><span class="sxs-lookup"><span data-stu-id="a95c5-111">This article shows you how toouse PowerShell tooautomate common tasks you need tooperform when you set up Azure Site Recovery tooreplicate Hyper-V virtual machines in System Center VMM clouds tooAzure storage.</span></span>

<span data-ttu-id="a95c5-112">Merhaba makale hello senaryonun önkoşulları içerir ve gösterir</span><span class="sxs-lookup"><span data-stu-id="a95c5-112">hello article includes prerequisites for hello scenario, and shows you</span></span>

* <span data-ttu-id="a95c5-113">Nasıl tooset bir kurtarma Hizmetleri kasası ayarlama</span><span class="sxs-lookup"><span data-stu-id="a95c5-113">How tooset up a Recovery Services Vault</span></span>
* <span data-ttu-id="a95c5-114">Hello Azure Site Recovery sağlayıcısı hello kaynak VMM sunucusuna yükleyin</span><span class="sxs-lookup"><span data-stu-id="a95c5-114">Install hello Azure Site Recovery Provider on hello source VMM server</span></span>
* <span data-ttu-id="a95c5-115">Merhaba sunucu hello kasaya kaydetmek, bir Azure depolama hesabı ekleme</span><span class="sxs-lookup"><span data-stu-id="a95c5-115">Register hello server in hello vault, add an Azure storage account</span></span>
* <span data-ttu-id="a95c5-116">Hyper-V ana bilgisayar sunucuları üzerinde Hello Azure kurtarma Hizmetleri aracısını yükleme</span><span class="sxs-lookup"><span data-stu-id="a95c5-116">Install hello Azure Recovery Services agent on Hyper-V host servers</span></span>
* <span data-ttu-id="a95c5-117">Uygulanan tooall korumalı sanal makineleri olacak VMM Bulutları için koruma ayarlarını yapılandırın</span><span class="sxs-lookup"><span data-stu-id="a95c5-117">Configure protection settings for VMM clouds, that will be applied tooall protected virtual machines</span></span>
* <span data-ttu-id="a95c5-118">Bu sanal makineler için korumayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="a95c5-118">Enable protection for those virtual machines.</span></span>
* <span data-ttu-id="a95c5-119">Merhaba yük devretme toomake her şeyin beklendiği gibi çalıştığından emin sınayın.</span><span class="sxs-lookup"><span data-stu-id="a95c5-119">Test hello fail-over toomake sure everything's working as expected.</span></span>

<span data-ttu-id="a95c5-120">Bu senaryoyu oluşturan ayarlama sorunlarını alıyorsanız, üzerinde hello sorularınızı [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="a95c5-120">If you run into problems setting up this scenario, post your questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

> [!NOTE]
> <span data-ttu-id="a95c5-121">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="a95c5-121">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="a95c5-122">Bu makalede, hello Resource Manager dağıtım modelini kullanarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="a95c5-122">This article covers using hello Resource Manager deployment model.</span></span>
>
>

## <a name="before-you-start"></a><span data-ttu-id="a95c5-123">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="a95c5-123">Before you start</span></span>
<span data-ttu-id="a95c5-124">Bu Önkoşullar sağladığınızdan emin olun:</span><span class="sxs-lookup"><span data-stu-id="a95c5-124">Make sure you have these prerequisites in place:</span></span>

### <a name="azure-prerequisites"></a><span data-ttu-id="a95c5-125">Azure önkoşulları</span><span class="sxs-lookup"><span data-stu-id="a95c5-125">Azure prerequisites</span></span>
* <span data-ttu-id="a95c5-126">Bir [Microsoft Azure](https://azure.microsoft.com/) hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a95c5-126">You'll need a [Microsoft Azure](https://azure.microsoft.com/) account.</span></span> <span data-ttu-id="a95c5-127">Yoksa, başlayan bir [ücretsiz bir hesap](https://azure.microsoft.com/free).</span><span class="sxs-lookup"><span data-stu-id="a95c5-127">If you don't have one, start with a [free account](https://azure.microsoft.com/free).</span></span> <span data-ttu-id="a95c5-128">Ayrıca, hello hakkında bilgi edinebilirsiniz [Azure Site Recovery Manager fiyatlandırma](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="a95c5-128">In addition, you can read about hello [Azure Site Recovery Manager pricing](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
* <span data-ttu-id="a95c5-129">Merhaba çoğaltma tooa CSP abonelik senaryo çalışıyorsanız, CSP aboneliğine sahip olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a95c5-129">You'll need a CSP subscription if you are trying out hello replication tooa CSP subscription scenario.</span></span> <span data-ttu-id="a95c5-130">Merhaba CSP programı hakkında daha fazla bilgi [nasıl hello CSP programında tooenroll](https://msdn.microsoft.com/library/partnercenter/mt156995.aspx).</span><span class="sxs-lookup"><span data-stu-id="a95c5-130">Learn more about hello CSP program in [how tooenroll in hello CSP program](https://msdn.microsoft.com/library/partnercenter/mt156995.aspx).</span></span>
* <span data-ttu-id="a95c5-131">Bir Azure v2 (Resource Manager) depolama hesabı toostore çoğaltılmış verileri tooAzure gerekir.</span><span class="sxs-lookup"><span data-stu-id="a95c5-131">You'll need an Azure v2 storage (Resource Manager) account toostore data replicated tooAzure.</span></span> <span data-ttu-id="a95c5-132">Merhaba hesabının coğrafi çoğaltmanın etkinleştirilmiş olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a95c5-132">hello account needs geo-replication enabled.</span></span> <span data-ttu-id="a95c5-133">Merhaba hello Azure Site Recovery hizmeti ile aynı bölgeye ve hello ile ilişkili olmalıdır aynı abonelik veya hello CSP abonelik.</span><span class="sxs-lookup"><span data-stu-id="a95c5-133">It should be in hello same region as hello Azure Site Recovery service, and be associated with hello same subscription or hello CSP subscription.</span></span> <span data-ttu-id="a95c5-134">Azure depolama birimini kurma hakkında daha fazla toolearn bkz hello [giriş tooMicrosoft Azure Storage](../storage/common/storage-introduction.md) başvuru.</span><span class="sxs-lookup"><span data-stu-id="a95c5-134">toolearn more about setting up Azure storage, see hello [Introduction tooMicrosoft Azure Storage](../storage/common/storage-introduction.md) for reference.</span></span>
* <span data-ttu-id="a95c5-135">Toomake tooprotect istediğiniz sanal makineleri hello ile uyumlu olduğundan emin olmanız gerekir [Azure sanal makine önkoşulları](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="a95c5-135">You'll need toomake sure that virtual machines you want tooprotect comply with hello [Azure virtual machine prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>

> [!NOTE]
> <span data-ttu-id="a95c5-136">Şu anda yalnızca VM düzeyinde işlemleri Powershell aracılığıyla mümkündür.</span><span class="sxs-lookup"><span data-stu-id="a95c5-136">Currently, only VM level operations are possible through Powershell.</span></span> <span data-ttu-id="a95c5-137">Kurtarma planı düzeyi işlemleri için destek yakında sunulacaktır.</span><span class="sxs-lookup"><span data-stu-id="a95c5-137">Support for recovery plan level operations will be made soon.</span></span>  <span data-ttu-id="a95c5-138">Şimdilik, sınırlı tooperforming başarısız-belirlemez yalnızca 'VM korumalı' ayrıntı düzeyi ve düzeyinde bir kurtarma planı demektir.</span><span class="sxs-lookup"><span data-stu-id="a95c5-138">For now, you are limited tooperforming fail-overs only at a ‘protected VM’ granularity and not at a Recovery Plan level.</span></span>
>
>

### <a name="vmm-prerequisites"></a><span data-ttu-id="a95c5-139">VMM önkoşulları</span><span class="sxs-lookup"><span data-stu-id="a95c5-139">VMM prerequisites</span></span>
* <span data-ttu-id="a95c5-140">System Center 2012 R2 üzerinde çalışan VMM sunucusu gerekir.</span><span class="sxs-lookup"><span data-stu-id="a95c5-140">You'll need VMM server running on System Center 2012 R2.</span></span>
* <span data-ttu-id="a95c5-141">Sanal makineler içeren herhangi bir VMM sunucusuna tooprotect hello Azure Site Recovery sağlayıcısı çalıştırmalıdır istiyor.</span><span class="sxs-lookup"><span data-stu-id="a95c5-141">Any VMM server containing virtual machines you want tooprotect must be running hello Azure Site Recovery Provider.</span></span> <span data-ttu-id="a95c5-142">Bu hello Azure Site Recovery dağıtımı sırasında yüklenir.</span><span class="sxs-lookup"><span data-stu-id="a95c5-142">This is installed during hello Azure Site Recovery deployment.</span></span>
* <span data-ttu-id="a95c5-143">Merhaba tooprotect istediğiniz VMM sunucusu üzerinde en az bir bulut gerekir.</span><span class="sxs-lookup"><span data-stu-id="a95c5-143">You'll need at least one cloud on hello VMM server you want tooprotect.</span></span> <span data-ttu-id="a95c5-144">Merhaba bulut içermelidir:</span><span class="sxs-lookup"><span data-stu-id="a95c5-144">hello cloud should contain:</span></span>
  * <span data-ttu-id="a95c5-145">Bir veya birden çok VMM ana bilgisayar grubu.</span><span class="sxs-lookup"><span data-stu-id="a95c5-145">One or more VMM host groups.</span></span>
  * <span data-ttu-id="a95c5-146">Her ana bilgisayar grubunda bir veya daha fazla Hyper-V sunucusu ya da kümesi.</span><span class="sxs-lookup"><span data-stu-id="a95c5-146">One or more Hyper-V host servers or clusters in each host group.</span></span>
  * <span data-ttu-id="a95c5-147">Merhaba kaynak Hyper-V sunucu üzerindeki bir veya daha fazla sanal makineler.</span><span class="sxs-lookup"><span data-stu-id="a95c5-147">One or more virtual machines on hello source Hyper-V server.</span></span>
* <span data-ttu-id="a95c5-148">VMM bulutlarını ayarlama hakkında daha fazla bilgi edinin:</span><span class="sxs-lookup"><span data-stu-id="a95c5-148">Learn more about setting up VMM clouds:</span></span>
  * <span data-ttu-id="a95c5-149">Özel VMM bulutlarındaki hakkında daha fazla bilgiyi [System Center 2012 R2 VMM ile özel bulut yenilikler](http://go.microsoft.com/fwlink/?LinkId=324952) ve [VMM 2012 ve hello Bulutları](http://go.microsoft.com/fwlink/?LinkId=324956).</span><span class="sxs-lookup"><span data-stu-id="a95c5-149">Read more about private VMM clouds in [What’s New in Private Cloud with System Center 2012 R2 VMM](http://go.microsoft.com/fwlink/?LinkId=324952) and in [VMM 2012 and hello clouds](http://go.microsoft.com/fwlink/?LinkId=324956).</span></span>
  * <span data-ttu-id="a95c5-150">Hakkında bilgi edinin [yapılandırma hello VMM bulut yapı](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric)</span><span class="sxs-lookup"><span data-stu-id="a95c5-150">Learn about [Configuring hello VMM cloud fabric](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric)</span></span>
  * <span data-ttu-id="a95c5-151">Bulut doku öğelerinizi hazır olduktan sonra özel bulutta oluşturma hakkında bilgi edinin [VMM'de özel bulut oluşturma](http://go.microsoft.com/fwlink/p/?LinkId=324953) ve [izlenecek yol: System Center 2012 SP1 VMM içeren özel bulut oluşturma](http://go.microsoft.com/fwlink/p/?LinkId=324954).</span><span class="sxs-lookup"><span data-stu-id="a95c5-151">After your cloud fabric elements are in place learn about creating private clouds in [Creating a private cloud in VMM](http://go.microsoft.com/fwlink/p/?LinkId=324953) and in [Walkthrough: Creating private clouds with System Center 2012 SP1 VMM](http://go.microsoft.com/fwlink/p/?LinkId=324954).</span></span>

### <a name="hyper-v-prerequisites"></a><span data-ttu-id="a95c5-152">Hyper-V önkoşulları</span><span class="sxs-lookup"><span data-stu-id="a95c5-152">Hyper-V prerequisites</span></span>
* <span data-ttu-id="a95c5-153">Merhaba Hyper-V ana bilgisayar sunucuları en az çalıştırmalıdır **Windows Server 2012** Hyper-V rolüne sahip veya **Microsoft Hyper-V Server 2012** ve hello son güncelleştirmelerin yüklü olması.</span><span class="sxs-lookup"><span data-stu-id="a95c5-153">hello host Hyper-V servers must be running at least **Windows Server 2012** with Hyper-V role or **Microsoft Hyper-V Server 2012** and have hello latest updates installed.</span></span>
* <span data-ttu-id="a95c5-154">Hyper-V'yi bir kümede çalıştırıyorsanız statik IP adresi temelli bir kümeye sahip olmanız durumunda küme aracısının otomatik olarak oluşturulamayacağını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="a95c5-154">If you're running Hyper-V in a cluster note that cluster broker isn't created automatically if you have a static IP address-based cluster.</span></span> <span data-ttu-id="a95c5-155">El ile tooconfigure hello küme Aracısı gerekir.</span><span class="sxs-lookup"><span data-stu-id="a95c5-155">You'll need tooconfigure hello cluster broker manually.</span></span> <span data-ttu-id="a95c5-156">için</span><span class="sxs-lookup"><span data-stu-id="a95c5-156">For</span></span>
* <span data-ttu-id="a95c5-157">Yönergeler için bkz [nasıl tooConfigure Hyper-V çoğaltma aracısı](http://blogs.technet.com/b/haroldwong/archive/2013/03/27/server-virtualization-series-hyper-v-replica-broker-explained-part-15-of-20-by-yung-chou.aspx).</span><span class="sxs-lookup"><span data-stu-id="a95c5-157">For instructions see [How tooConfigure Hyper-V Replica Broker](http://blogs.technet.com/b/haroldwong/archive/2013/03/27/server-virtualization-series-hyper-v-replica-broker-explained-part-15-of-20-by-yung-chou.aspx).</span></span>
* <span data-ttu-id="a95c5-158">Herhangi bir Hyper-V konak sunucusu veya küme toomanage koruma istediğiniz VMM Bulutu eklenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="a95c5-158">Any Hyper-V host server or cluster for which you want toomanage protection must be included in a VMM cloud.</span></span>

### <a name="network-mapping-prerequisites"></a><span data-ttu-id="a95c5-159">Ağ eşlemesi önkoşulları</span><span class="sxs-lookup"><span data-stu-id="a95c5-159">Network mapping prerequisites</span></span>
<span data-ttu-id="a95c5-160">Azure sanal makineleri koruduğunuzda, hello ağ eşlemesi hello sanal makine ağları hello kaynak VMM sunucuda ve hedef Azure ağları tooenable hello aşağıdaki eşler:</span><span class="sxs-lookup"><span data-stu-id="a95c5-160">When you protect virtual machines in Azure, hello network mapping  maps hello virtual machine networks on hello source VMM server and target Azure networks tooenable hello following:</span></span>

* <span data-ttu-id="a95c5-161">Merhaba üzerinde aynı yük devri tüm makineler ağ tooeach bulundukları hangi kurtarma planı yedeklemiş diğer bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="a95c5-161">All machines which fail over on hello same network can connect tooeach other, irrespective of which recovery plan they are in.</span></span>
* <span data-ttu-id="a95c5-162">Bir ağ geçidi Kurulum hello hedef Azure ağını üzerinde ise, sanal makineleri tooother şirket içi sanal makinelere bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="a95c5-162">If a network gateway is setup on hello target Azure network, virtual machines can connect tooother on-premises virtual machines.</span></span>
* <span data-ttu-id="a95c5-163">Ağ eşlemesini yapılandırmazsanız, yalnızca sanal makineler, hello aynı yük devri hello kurtarma planı yük devretme tooAzure sonra diğer mümkün tooconnect tooeach olacaktır.</span><span class="sxs-lookup"><span data-stu-id="a95c5-163">If you don’t configure network mapping, only hello virtual machines that fail over in hello same recovery plan will be able tooconnect tooeach other after fail-over tooAzure.</span></span>

<span data-ttu-id="a95c5-164">Toodeploy ağ eşlemesi istiyorsanız hello aşağıdakiler gerekir:</span><span class="sxs-lookup"><span data-stu-id="a95c5-164">If you want toodeploy network mapping you'll need hello following:</span></span>

* <span data-ttu-id="a95c5-165">Merhaba kaynak VMM sunucusunda tooprotect istediğiniz Hello sanal makineleri bağlı tooa VM ağı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a95c5-165">hello virtual machines you want tooprotect on hello source VMM server should be connected tooa VM network.</span></span> <span data-ttu-id="a95c5-166">Bu ağ hello Bulutu ile ilişkili mantıksal ağ bağlantılı tooa olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a95c5-166">That network should be linked tooa logical network that is associated with hello cloud.</span></span>
* <span data-ttu-id="a95c5-167">Bir Azure ağı toowhich çoğaltılan sanal makineler, yük devretme bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="a95c5-167">An Azure network toowhich replicated virtual machines can connect after fail-over.</span></span> <span data-ttu-id="a95c5-168">Yük devretme hello aynı anda bu ağ seçersiniz.</span><span class="sxs-lookup"><span data-stu-id="a95c5-168">You'll select this network at hello time of fail-over.</span></span> <span data-ttu-id="a95c5-169">Merhaba ağ hello olmalıdır, Azure Site Recovery abonelik aynı bölgede.</span><span class="sxs-lookup"><span data-stu-id="a95c5-169">hello network should be in hello same region as your Azure Site Recovery subscription.</span></span>

<span data-ttu-id="a95c5-170">Ağ eşlemesi hakkında daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="a95c5-170">Learn more about network mapping in</span></span>

* [<span data-ttu-id="a95c5-171">Nasıl tooconfigure vmm'de Mantıksal ağlar</span><span class="sxs-lookup"><span data-stu-id="a95c5-171">How tooconfigure logical networks in VMM</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=386307)
* [<span data-ttu-id="a95c5-172">Nasıl tooconfigure VM ağları ve ağ geçitlerini vmm'de</span><span class="sxs-lookup"><span data-stu-id="a95c5-172">How tooconfigure VM networks and gateways in VMM</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=386308)
* [<span data-ttu-id="a95c5-173">Nasıl Azure sanal ağları tooconfigure ve İzleyicisi</span><span class="sxs-lookup"><span data-stu-id="a95c5-173">How tooconfigure and monitor virtual networks in Azure</span></span>](https://azure.microsoft.com/documentation/services/virtual-network/)

### <a name="powershell-prerequisites"></a><span data-ttu-id="a95c5-174">PowerShell önkoşulları</span><span class="sxs-lookup"><span data-stu-id="a95c5-174">PowerShell prerequisites</span></span>
<span data-ttu-id="a95c5-175">Azure PowerShell hazır toogo olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="a95c5-175">Make sure you have Azure PowerShell ready toogo.</span></span> <span data-ttu-id="a95c5-176">PowerShell zaten kullanıyorsanız, tooupgrade tooversion 0.8.10 gerekir ya da daha sonra.</span><span class="sxs-lookup"><span data-stu-id="a95c5-176">If you are already using PowerShell, you'll need tooupgrade tooversion 0.8.10 or later.</span></span> <span data-ttu-id="a95c5-177">Merhaba PowerShell ayarlama hakkında daha fazla bilgi için bkz [Kılavuzu tooinstall ve Azure PowerShell yapılandırma](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="a95c5-177">For information about setting up PowerShell, see hello [Guide tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="a95c5-178">Ayarlama ve PowerShell yapılandırılmış sonra tüm hello hizmeti için kullanılabilir cmdlet'leri hello görüntüleyebilirsiniz [burada](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a95c5-178">Once you have set up and configured PowerShell, you can view all of hello available cmdlets for hello service [here](/powershell/azure/overview).</span></span>

<span data-ttu-id="a95c5-179">parametre değerleri, girişleri ve çıkışları genellikle Azure PowerShell'de işlenme gibi hello cmdlet'leri kullanmanıza yardımcı olabilecek ipuçları hakkında toolearn bkz hello [tooget Azure cmdlet'leri ile Başlarken Kılavuzu](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="a95c5-179">toolearn about tips that can help you use hello cmdlets, such as how parameter values, inputs, and outputs are typically handled in Azure PowerShell, see hello [Guide tooget Started with Azure Cmdlets](/powershell/azure/get-started-azureps).</span></span>

## <a name="step-1-set-hello-subscription"></a><span data-ttu-id="a95c5-180">1. adım: hello abonelik ayarlama</span><span class="sxs-lookup"><span data-stu-id="a95c5-180">Step 1: Set hello subscription</span></span>
1. <span data-ttu-id="a95c5-181">Azure powershell, oturum açma tooyour Azure hesabı üzerinden: hello aşağıdaki cmdlet'leri kullanarak</span><span class="sxs-lookup"><span data-stu-id="a95c5-181">From Azure powershell, login tooyour Azure account: using hello following cmdlets</span></span>

        $UserName = "<user@live.com>"
        $Password = "<password>"
        $SecurePassword = ConvertTo-SecureString -AsPlainText $Password -Force
        $Cred = New-Object System.Management.Automation.PSCredential -ArgumentList $UserName, $SecurePassword
        Login-AzureRmAccount #-Credential $Cred
2. <span data-ttu-id="a95c5-182">Aboneliklerinizi listesini alın.</span><span class="sxs-lookup"><span data-stu-id="a95c5-182">Get a list of your subscriptions.</span></span> <span data-ttu-id="a95c5-183">Bu da hello subscriptionIDs her hello abonelikler için listeler.</span><span class="sxs-lookup"><span data-stu-id="a95c5-183">This will also list hello subscriptionIDs for each of hello subscriptions.</span></span> <span data-ttu-id="a95c5-184">Toocreate hello kurtarma Hizmetleri kasası istediğiniz hello aboneliğin Hello Subscriptionıd unutmayın</span><span class="sxs-lookup"><span data-stu-id="a95c5-184">Note down hello subscriptionID of hello subscription in which you wish toocreate hello recovery services vault</span></span>

        Get-AzureRmSubscription
3. <span data-ttu-id="a95c5-185">Hangi hello kurtarma Hizmetleri kasası hello abonelik kimliği söz tarafından oluşturulan toobe olan hello abonelik ayarlayın</span><span class="sxs-lookup"><span data-stu-id="a95c5-185">Set hello subscription in which hello recovery services vault is toobe created by mentioning hello subscription ID</span></span>

        Set-AzureRmContext –SubscriptionID <subscriptionId>

## <a name="step-2-create-a-recovery-services-vault"></a><span data-ttu-id="a95c5-186">2. Adım: Bir Kurtarma Hizmetleri kasası oluşturma</span><span class="sxs-lookup"><span data-stu-id="a95c5-186">Step 2: Create a Recovery Services vault</span></span>
1. <span data-ttu-id="a95c5-187">Zaten yoksa, Azure Kaynak Yöneticisi'nde bir kaynak grubu oluştur</span><span class="sxs-lookup"><span data-stu-id="a95c5-187">Create a resource group  in Azure Resource Manager if you don't have one already</span></span>

        New-AzureRmResourceGroup -Name #ResourceGroupName -Location #location
2. <span data-ttu-id="a95c5-188">Yeni bir kurtarma Hizmetleri kasası oluşturun ve ASR kasası nesne (daha sonra kullanılacak) bir değişkende oluşturulan hello kaydedin.</span><span class="sxs-lookup"><span data-stu-id="a95c5-188">Create a new Recovery Services vault and save hello created ASR vault object in a variable (will be used later).</span></span> <span data-ttu-id="a95c5-189">Merhaba ASR kasası nesne post oluşturma hello Get-AzureRMRecoveryServicesVault cmdlet'ini kullanarak elde edebilirsiniz:-</span><span class="sxs-lookup"><span data-stu-id="a95c5-189">You can also retrieve hello ASR vault object post creation using hello Get-AzureRMRecoveryServicesVault cmdlet:-</span></span>

        $vault = New-AzureRmRecoveryServicesVault -Name #vaultname -ResouceGroupName #ResourceGroupName -Location #location

## <a name="step-3-set-hello-recovery-services-vault-context"></a><span data-ttu-id="a95c5-190">3. adım: hello kurtarma Hizmetleri kasası bağlamını ayarlayın</span><span class="sxs-lookup"><span data-stu-id="a95c5-190">Step 3: Set hello Recovery Services Vault context</span></span>

<span data-ttu-id="a95c5-191">Hello aşağıdaki komutu çalıştırarak Hello kasası bağlamını ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="a95c5-191">Set hello vault context by running hello below command.</span></span>

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-install-hello-azure-site-recovery-provider"></a><span data-ttu-id="a95c5-192">Adım 4: hello Azure Site Recovery sağlayıcısı yükleme</span><span class="sxs-lookup"><span data-stu-id="a95c5-192">Step 4: Install hello Azure Site Recovery Provider</span></span>
1. <span data-ttu-id="a95c5-193">Merhaba VMM makinede hello aşağıdaki komutu çalıştırarak bir dizin oluşturun:</span><span class="sxs-lookup"><span data-stu-id="a95c5-193">On hello VMM machine, create a directory by running hello following command:</span></span>

       New-Item c:\ASR -type directory
2. <span data-ttu-id="a95c5-194">Merhaba aşağıdaki komutu çalıştırarak indirilen hello sağlayıcısını kullanarak hello dosyaları ayıklayın</span><span class="sxs-lookup"><span data-stu-id="a95c5-194">Extract hello files using hello downloaded provider by running hello following command</span></span>

       pushd C:\ASR\
       .\AzureSiteRecoveryProvider.exe /x:. /q
3. <span data-ttu-id="a95c5-195">Merhaba Sağlayıcı komutları aşağıdaki hello kullanarak yükleyin:</span><span class="sxs-lookup"><span data-stu-id="a95c5-195">Install hello provider using hello following commands:</span></span>

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

   <span data-ttu-id="a95c5-196">Merhaba yükleme toofinish bekleyin.</span><span class="sxs-lookup"><span data-stu-id="a95c5-196">Wait for hello installation toofinish.</span></span>
4. <span data-ttu-id="a95c5-197">Hello sunucu komutu aşağıdaki hello kullanarak hello kasasına kaydedin:</span><span class="sxs-lookup"><span data-stu-id="a95c5-197">Register hello server in hello vault using hello following command:</span></span>

       $BinPath = $env:SystemDrive+"\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin"
       pushd $BinPath
       $encryptionFilePath = "C:\temp\".\DRConfigurator.exe /r /Credentials $VaultSettingFilePath /vmmfriendlyname $env:COMPUTERNAME /dataencryptionenabled $encryptionFilePath /startvmmservice

## <a name="step-5-create-an-azure-storage-account"></a><span data-ttu-id="a95c5-198">5. adım: Azure storage hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a95c5-198">Step 5: Create an Azure storage account</span></span>

<span data-ttu-id="a95c5-199">Bir Azure depolama hesabınız yoksa, bir coğrafi çoğaltmanın etkinleştirilmiş hesabı oluşturmak hello hello aynı coğrafi bölgede kasa hello aşağıdaki komutu çalıştırarak:</span><span class="sxs-lookup"><span data-stu-id="a95c5-199">If you don't have an Azure storage account, create a geo-replication enabled account in hello same geo as hello vault by running hello following command:</span></span>

        $StorageAccountName = "teststorageacc1"    #StorageAccountname
        $StorageAccountGeo  = "Southeast Asia"     
        $ResourceGroupName =  “myRG”             #ResourceGroupName
        $RecoveryStorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageAccountName -Type “StandardGRS” -Location $StorageAccountGeo

<span data-ttu-id="a95c5-200">Merhaba depolama hesabı olması gerektiğini unutmayın hello hello Azure Site Recovery hizmeti ile aynı bölgeye ve ilişkilendirilmesi hello aynı abonelik.</span><span class="sxs-lookup"><span data-stu-id="a95c5-200">Note that hello storage account must be in hello same region as hello Azure Site Recovery service, and be associated with hello same subscription.</span></span>

## <a name="step-6-install-hello-azure-recovery-services-agent"></a><span data-ttu-id="a95c5-201">6. adım: hello Azure kurtarma Hizmetleri Aracısı yükleme</span><span class="sxs-lookup"><span data-stu-id="a95c5-201">Step 6: Install hello Azure Recovery Services Agent</span></span>
1. <span data-ttu-id="a95c5-202">Konumundaki Hello Azure kurtarma Hizmetleri Aracısı'nı indirme [http://aka.ms/latestmarsagent](http://aka.ms/latestmarsagent) ve hello VMM bulunan her Hyper-V konak sunucusu üzerinde Bulutlar yükleme tooprotect istiyor.</span><span class="sxs-lookup"><span data-stu-id="a95c5-202">Download hello Azure Recovery Services agent at [http://aka.ms/latestmarsagent](http://aka.ms/latestmarsagent) and install it on each Hyper-V host server located in hello VMM clouds you want tooprotect.</span></span>
2. <span data-ttu-id="a95c5-203">Tüm VMM konaklarda komutu aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="a95c5-203">Run hello following command on all VMM hosts:</span></span>

       marsagentinstaller.exe /q /nu

## <a name="step-7-configure-cloud-protection-settings"></a><span data-ttu-id="a95c5-204">7. adım: Bulut yapılandırma koruma ayarları</span><span class="sxs-lookup"><span data-stu-id="a95c5-204">Step 7: Configure cloud protection settings</span></span>
1. <span data-ttu-id="a95c5-205">Bir çoğaltma ilkesi tooAzure hello aşağıdaki komutu çalıştırarak oluşturun:</span><span class="sxs-lookup"><span data-stu-id="a95c5-205">Create a replication policy tooAzure by running hello following command:</span></span>

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $Recoverypoints = 6                    #specify hello number of recovery points

        $policryresult = New-AzureRmSiteRecoveryPolicy -Name $policyname -ReplicationProvider HyperVReplicaAzure -ReplicationFrequencyInSeconds $replicationfrequencyinseconds -RecoveryPoints $recoverypoints -ApplicationConsistentSnapshotFrequencyInHours 1 -RecoveryAzureStorageAccountId "/subscriptions/q1345667/resourceGroups/test/providers/Microsoft.Storage/storageAccounts/teststorageacc1"

1. <span data-ttu-id="a95c5-206">Koruma kapsayıcısı hello aşağıdaki komutları çalıştırarak alın:</span><span class="sxs-lookup"><span data-stu-id="a95c5-206">Get a protection container by running hello following commands:</span></span>

       $PrimaryCloud = "testcloud"
       $protectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloud;  
2. <span data-ttu-id="a95c5-207">Oluşturulan hello işlemini kullanarak ve hello kolay ilke adı söz hello ilkesi ayrıntıları tooa değişkeni alın:</span><span class="sxs-lookup"><span data-stu-id="a95c5-207">Get hello policy details tooa variable using hello job that was created and mentioning hello friendly policy name:</span></span>

       $policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $policyname
3. <span data-ttu-id="a95c5-208">Merhaba koruma kapsayıcısı Hello ilişkilendirmesini hello çoğaltma ilkesiyle başlatın:</span><span class="sxs-lookup"><span data-stu-id="a95c5-208">Start hello association of hello protection container with hello replication policy:</span></span>

       $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy     $Policy -PrimaryProtectionContainer $protectionContainer  
4. <span data-ttu-id="a95c5-209">Merhaba işi tamamlandıktan sonra hello aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="a95c5-209">After hello job has finished, run hello following command:</span></span>

       $job = Get-AzureRmSiteRecoveryJob -Job $associationJob

       if($job -eq $null -or $job.StateDescription -ne "Completed")
       {
         $isJobLeftForProcessing = $true;
       }
5. <span data-ttu-id="a95c5-210">Hello iş işlemeyi bitirdikten sonra hello aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="a95c5-210">After hello job has finished processing, run hello following command:</span></span>

       if($isJobLeftForProcessing)
       {
         Start-Sleep -Seconds 60
       }
       }While($isJobLeftForProcessing)

<span data-ttu-id="a95c5-211">Merhaba işleminin toocheck hello tamamlanması izleyin hello adımlarda [etkinliğini izleme](#monitor).</span><span class="sxs-lookup"><span data-stu-id="a95c5-211">toocheck hello completion of hello operation, follow hello steps in [Monitor Activity](#monitor).</span></span>

## <a name="step-8-configure-network-mapping"></a><span data-ttu-id="a95c5-212">8. adım: ağ eşlemesini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a95c5-212">Step 8: Configure network mapping</span></span>
<span data-ttu-id="a95c5-213">Başlamadan önce Ağ eşlemesi hello kaynak VMM sunucusundaki sanal makineleri bağlı tooa VM ağı olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="a95c5-213">Before you begin network mapping verify that virtual machines on hello source VMM server are connected tooa VM network.</span></span> <span data-ttu-id="a95c5-214">Ayrıca, bir veya daha fazla Azure sanal ağı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a95c5-214">In addition, create one or more Azure virtual networks.</span></span>

<span data-ttu-id="a95c5-215">Toocreate sanal bir ağ Azure Resource Manager ve PowerShell kullanılarak nasıl hakkında daha fazla bilgi [Azure Resource Manager ve PowerShell kullanarak siteden siteye VPN bağlantısı olan bir sanal ağ oluşturma](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="a95c5-215">Learn more about how toocreate a virtual network using Azure Resource Manager and PowerShell, in [Create a virtual network with a site-to-site VPN connection using Azure Resource Manager and PowerShell](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)</span></span>

<span data-ttu-id="a95c5-216">Birden çok sanal makine ağları eşlenen tooa tek Azure ağ olabileceğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="a95c5-216">Note that multiple Virtual Machine networks can be mapped tooa single Azure network.</span></span> <span data-ttu-id="a95c5-217">Hello hedef ağın birden çok alt ağı varsa ve bu alt ağlardan biri olan hello adıyla aynı alt ağda hangi hello kaynak sanal makinenin bulunduğu sonra hello çoğaltma sanal makinesi yük devretme bağlı toothat hedef alt olacaktır.</span><span class="sxs-lookup"><span data-stu-id="a95c5-217">If hello target network has multiple subnets and one of those subnets has hello same name as subnet on which hello source virtual machine is located, then hello replica virtual machine will be connected toothat target subnet after fail-over.</span></span> <span data-ttu-id="a95c5-218">Eşleşen ada sahip bir hedef alt ağ ise hello sanal makineye bağlı toohello hello ağdaki ilk alt ağ olacaktır.</span><span class="sxs-lookup"><span data-stu-id="a95c5-218">If there is no target subnet with a matching name, hello virtual machine will be connected toohello first subnet in hello network.</span></span>

1. <span data-ttu-id="a95c5-219">Merhaba ilk komut sunucuları için geçerli Azure Site Recovery kasası hello alır.</span><span class="sxs-lookup"><span data-stu-id="a95c5-219">hello first command gets servers for hello current Azure Site Recovery vault.</span></span> <span data-ttu-id="a95c5-220">Merhaba komut hello Microsoft Azure Site Recovery sunucuları hello $Servers dizi değişkeninde depolar.</span><span class="sxs-lookup"><span data-stu-id="a95c5-220">hello command stores hello Microsoft Azure Site Recovery servers in hello $Servers array variable.</span></span>

        $Servers = Get-AzureRmSiteRecoveryServer
2. <span data-ttu-id="a95c5-221">Merhaba ikinci komut hello site kurtarma ağ hello ilk sunucu için hello $Servers dizisini alır.</span><span class="sxs-lookup"><span data-stu-id="a95c5-221">hello second command gets hello site recovery network for hello first server in hello $Servers array.</span></span> <span data-ttu-id="a95c5-222">Merhaba komut hello ağları hello $Networks değişkeninde depolar.</span><span class="sxs-lookup"><span data-stu-id="a95c5-222">hello command stores hello networks in hello $Networks variable.</span></span>

        $Networks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[0]

1. <span data-ttu-id="a95c5-223">Merhaba üçüncü komut hello $AzureVmNetworks değişkeninde Azure sanal ağlar ve bu değeri alır.</span><span class="sxs-lookup"><span data-stu-id="a95c5-223">hello third command gets Azure virtual networks, and then that value in hello $AzureVmNetworks variable.</span></span>

        $AzureVmNetworks =  Get-AzureRmVirtualNetwork
2. <span data-ttu-id="a95c5-224">Merhaba son cmdlet'i hello birincil ağ ve hello Azure sanal makine ağı arasında bir eşleme oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a95c5-224">hello final cmdlet creates a mapping between hello primary network and hello Azure virtual machine network.</span></span> <span data-ttu-id="a95c5-225">Merhaba cmdlet hello birincil ağ hello ilk öğesi $Networks belirtir.</span><span class="sxs-lookup"><span data-stu-id="a95c5-225">hello cmdlet specifies hello primary network as hello first element of $Networks.</span></span> <span data-ttu-id="a95c5-226">Merhaba cmdlet'i bir sanal makine ağına hello ilk öğesi $AzureVmNetworks belirtir.</span><span class="sxs-lookup"><span data-stu-id="a95c5-226">hello cmdlet specifies a virtual machine network as hello first element of $AzureVmNetworks.</span></span>

        New-AzureRmSiteRecoveryNetworkMapping -PrimaryNetwork $Networks[0] -AzureVMNetworkId $AzureVmNetworks[0]

## <a name="step-9-enable-protection-for-virtual-machines"></a><span data-ttu-id="a95c5-227">9. adım: sanal makineler için korumayı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="a95c5-227">Step 9: Enable protection for virtual machines</span></span>
<span data-ttu-id="a95c5-228">Merhaba sunucular, Bulutlar ve ağlar doğru şekilde yapılandırıldıktan sonra hello bulutta sanal makineler için korumayı etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a95c5-228">After hello servers, clouds and networks are configured correctly, you can enable protection for virtual machines in hello cloud.</span></span>

 <span data-ttu-id="a95c5-229">Merhaba aşağıdakileri göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="a95c5-229">Note hello following:</span></span>

* <span data-ttu-id="a95c5-230">Sanal makineler Azure gereksinimleri karşılaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a95c5-230">Virtual machines must meet Azure requirements.</span></span> <span data-ttu-id="a95c5-231">Bu iade [Önkoşullar ve Destek](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) hello Planlama Kılavuzu'nda.</span><span class="sxs-lookup"><span data-stu-id="a95c5-231">Check these in [Prerequisites and Support](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) in hello planning guide.</span></span>
* <span data-ttu-id="a95c5-232">tooenable koruma, hello işletim sistemi ve işletim sistemi disk özellikleri hello sanal makine için ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a95c5-232">tooenable protection, hello operating system and operating system disk properties must be set for hello virtual machine.</span></span> <span data-ttu-id="a95c5-233">Bir sanal makine şablonu kullanarak VMM'de bir sanal makine oluşturduğunuzda hello özelliğini ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a95c5-233">When you create a virtual machine in VMM using a virtual machine template you can set hello property.</span></span> <span data-ttu-id="a95c5-234">Bu özellikleri mevcut sanal makineler üzerinde hello ayarlayabilirsiniz **genel** ve **donanım yapılandırması** sekmeleri hello sanal makine özellikleri.</span><span class="sxs-lookup"><span data-stu-id="a95c5-234">You can also set these properties for existing virtual machines on hello **General** and **Hardware Configuration** tabs of hello virtual machine properties.</span></span> <span data-ttu-id="a95c5-235">Bu özellikleri VMM'de ayarlamazsanız mümkün tooconfigure olacak hello Azure Site Recovery portalında bunları.</span><span class="sxs-lookup"><span data-stu-id="a95c5-235">If you don't set these properties in VMM you'll be able tooconfigure them in hello Azure Site Recovery portal.</span></span>

1. <span data-ttu-id="a95c5-236">tooenable koruma, çalıştırma hello aşağıdaki tooget hello koruma kapsayıcısı komutu:</span><span class="sxs-lookup"><span data-stu-id="a95c5-236">tooenable protection, run hello following command tooget hello protection container:</span></span>

          $ProtectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $CloudName
2. <span data-ttu-id="a95c5-237">Merhaba koruma varlık (VM) hello aşağıdaki komutu çalıştırarak alın:</span><span class="sxs-lookup"><span data-stu-id="a95c5-237">Get hello protection entity (VM) by running hello following command:</span></span>

           $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -friendlyName $VMName -ProtectionContainer $protectionContainer
3. <span data-ttu-id="a95c5-238">Merhaba DR hello VM için komutu aşağıdaki hello çalıştırarak etkinleştirin:</span><span class="sxs-lookup"><span data-stu-id="a95c5-238">Enable hello DR for hello VM by running hello following command:</span></span>

          $jobResult = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionentity -Protection Enable –Force -Policy $policy -RecoveryAzureStorageAccountId  $storageID "/subscriptions/217653172865hcvkchgvd/resourceGroups/rajanirgps/providers/Microsoft.Storage/storageAccounts/teststorageacc1

## <a name="test-your-deployment"></a><span data-ttu-id="a95c5-239">Dağıtımınızı test edin</span><span class="sxs-lookup"><span data-stu-id="a95c5-239">Test your deployment</span></span>
<span data-ttu-id="a95c5-240">tootest bir test çalıştırabilirsiniz dağıtımınız tek bir sanal makine için yük devretme veya birden çok sanal makine içeren bir kurtarma planı oluşturun ve test yük devretme hello planı için çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="a95c5-240">tootest your deployment you can run a test fail-over for a single virtual machine, or create a recovery plan consisting of multiple virtual machines and run a test fail-over for hello plan.</span></span> <span data-ttu-id="a95c5-241">Test yük devretme, yük devretme ve kurtarma mekanizmanızı yalıtılmış bir ağda benzetimini yapar.</span><span class="sxs-lookup"><span data-stu-id="a95c5-241">Test fail-over simulates your fail-over and recovery mechanism in an isolated network.</span></span> <span data-ttu-id="a95c5-242">Şunlara dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="a95c5-242">Note that:</span></span>

* <span data-ttu-id="a95c5-243">Hello yük devretme Uzak Masaüstü'nü kullanarak azure'daki tooconnect toohello sanal makine istiyorsanız, Uzak Masaüstü Bağlantısı hello test yük devretmesi çalıştırmadan önce hello sanal makinesinde etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="a95c5-243">If you want tooconnect toohello virtual machine in Azure using Remote Desktop after hello fail-over, enable Remote Desktop Connection on hello virtual machine before you run hello test failover.</span></span>
* <span data-ttu-id="a95c5-244">Yük devretme, Uzak Masaüstü kullanarak Azure'da bir ortak IP adresi tooconnect toohello sanal makine kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="a95c5-244">After fail-over, you'll use a public IP address tooconnect toohello virtual machine in Azure using Remote Desktop.</span></span> <span data-ttu-id="a95c5-245">Bu toodo istiyorsanız, bağlanan tooa sanal genel bir adres kullanarak makineden engelleyecek etki alanı ilkelerine sahip olmadığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="a95c5-245">If you want toodo this, ensure you don't have any domain policies that prevent you from connecting tooa virtual machine using a public address.</span></span>

<span data-ttu-id="a95c5-246">Merhaba işleminin toocheck hello tamamlanması izleyin hello adımlarda [etkinliğini izleme](#monitor).</span><span class="sxs-lookup"><span data-stu-id="a95c5-246">toocheck hello completion of hello operation, follow hello steps in [Monitor Activity](#monitor).</span></span>

### <a name="run-a-test-failover"></a><span data-ttu-id="a95c5-247">Yük devretme testi çalıştırma</span><span class="sxs-lookup"><span data-stu-id="a95c5-247">Run a test failover</span></span>
- <span data-ttu-id="a95c5-248">Merhaba aşağıdaki komutu çalıştırarak Hello test yük devretme başlatın:</span><span class="sxs-lookup"><span data-stu-id="a95c5-248">Start hello test failover by running hello following command:</span></span>

       $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

### <a name="run-a-planned-failover"></a><span data-ttu-id="a95c5-249">Planlı yük devretmeyi çalıştırma</span><span class="sxs-lookup"><span data-stu-id="a95c5-249">Run a planned failover</span></span>
- <span data-ttu-id="a95c5-250">Başlangıç hello hello aşağıdaki komutu çalıştırarak planlanan yük devretme:</span><span class="sxs-lookup"><span data-stu-id="a95c5-250">Start hello planned failover by running hello following command:</span></span>

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

### <a name="run-an-unplanned-failover"></a><span data-ttu-id="a95c5-251">Planlanmamış bir yük devretmeyi çalıştırma</span><span class="sxs-lookup"><span data-stu-id="a95c5-251">Run an unplanned failover</span></span>
- <span data-ttu-id="a95c5-252">Başlat komutu aşağıdaki hello çalıştırarak planlanmamış yük devretme hello:</span><span class="sxs-lookup"><span data-stu-id="a95c5-252">Start hello unplanned failover by running hello following command:</span></span>

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

## <span data-ttu-id="a95c5-253"><a name=monitor></a>Etkinliğini izleme</span><span class="sxs-lookup"><span data-stu-id="a95c5-253"><a name=monitor></a> Monitor Activity</span></span>
<span data-ttu-id="a95c5-254">Aşağıdaki komutları toomonitor hello etkinlik hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="a95c5-254">Use hello following commands toomonitor hello activity.</span></span> <span data-ttu-id="a95c5-255">Merhaba işleme toofinish işleri arasında toowait gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="a95c5-255">Note that you have toowait in between jobs for hello processing toofinish.</span></span>

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



## <a name="next-steps"></a><span data-ttu-id="a95c5-256">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a95c5-256">Next steps</span></span>
<span data-ttu-id="a95c5-257">[Daha fazla bilgi](/powershell/module/azurerm.recoveryservices.backup/#recovery) Azure Site Recovery ile Azure Resource Manager PowerShell cmdlet'leri hakkında.</span><span class="sxs-lookup"><span data-stu-id="a95c5-257">[Read more](/powershell/module/azurerm.recoveryservices.backup/#recovery) about Azure Site Recovery with Azure Resource Manager PowerShell cmdlets.</span></span>
