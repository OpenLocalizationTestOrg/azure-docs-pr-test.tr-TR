---
title: "Azure Site Recovery kullanarak çok katmanlı Citrix XenDesktop ve XenApp dağıtım aaaReplicate | Microsoft Docs"
description: "Bu makalede nasıl Azure Site Recovery kullanarak tooprotect ve kurtarma Citrix XenDesktop ve XenApp dağıtımları."
services: site-recovery
documentationcenter: 
author: ponatara
manager: abhemraj
editor: 
ms.assetid: 9126f5e8-e9ed-4c31-b6b4-bf969c12c184
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: ponatara
ms.openlocfilehash: c4ea9f95f91c585cdcf9d776b02c0967f4c16ab0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-a-multi-tier-citrix-xenapp-and-xendesktop-deployment-using-azure-site-recovery"></a><span data-ttu-id="2f80a-103">Azure Site Recovery kullanarak çok katmanlı Citrix XenApp ve XenDesktop dağıtım Çoğalt</span><span class="sxs-lookup"><span data-stu-id="2f80a-103">Replicate a multi-tier Citrix XenApp and XenDesktop deployment using Azure Site Recovery</span></span>

## <a name="overview"></a><span data-ttu-id="2f80a-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="2f80a-104">Overview</span></span>

<span data-ttu-id="2f80a-105">Citrix XenDesktop masaüstleri ve uygulamalar bir ondemand hizmet tooany kullanıcısı olarak, herhangi bir yere teslim eden bir Masaüstü Sanallaştırma çözümüdür.</span><span class="sxs-lookup"><span data-stu-id="2f80a-105">Citrix XenDesktop is a desktop virtualization solution that delivers desktops and applications as an ondemand service tooany user, anywhere.</span></span> <span data-ttu-id="2f80a-106">FlexCast teslim teknolojisiyle XenDesktop hızlı ve güvenli bir şekilde uygulamalar ve Masaüstü toousers sunabilir.</span><span class="sxs-lookup"><span data-stu-id="2f80a-106">With FlexCast delivery technology, XenDesktop can quickly and securely deliver applications and desktops toousers.</span></span>
<span data-ttu-id="2f80a-107">Bugün, Citrix XenApp herhangi olağanüstü durum kurtarma özellikleri sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="2f80a-107">Today, Citrix XenApp does not provide any disaster recovery capabilities.</span></span>

<span data-ttu-id="2f80a-108">İyi olağanüstü durum kurtarma çözümü kurtarma planları hello geçici modelleme karmaşık uygulama mimarilerindeki izin ver ve bu nedenle sağlayan çeşitli katmanları arasındaki hello özelliği özelleştirilmiş tooadd adımları toohandle uygulama eşlemeleri de bir tek çözüm hello tooa önde gelen bir olağanüstü durumda görüntüsü tıklatma emin RTO düşürün.</span><span class="sxs-lookup"><span data-stu-id="2f80a-108">A good disaster recovery solution, should allow modeling of recovery plans around hello above complex application architectures and also have hello ability tooadd customized steps toohandle application mappings between various tiers hence providing a single-click sure shot solution in hello event of a disaster leading tooa lower RTO.</span></span>

<span data-ttu-id="2f80a-109">Bu belge, Hyper-V ve VMware vSphere platformlarda Citrix XenApp dağıtımları için şirket içi olağanüstü durum kurtarma çözümü oluşturmak için adım adım yönergeler sağlar.</span><span class="sxs-lookup"><span data-stu-id="2f80a-109">This document provides a step-by-step guidance for building a disaster recovery solution for your on-premises Citrix XenApp deployments on Hyper-V and VMware vSphere platforms.</span></span> <span data-ttu-id="2f80a-110">Ayrıca bu belgede açıklanan nasıl tooperform yük devretme testi (olağanüstü durum kurtarma ayrıntıya) ve kurtarma planları, hello desteklenen yapılandırmalar ve önkoşullar kullanarak planlanmamış yük devretme tooAzure.</span><span class="sxs-lookup"><span data-stu-id="2f80a-110">This document also describes how tooperform a test failover(disaster recovery drill) and unplanned failover tooAzure using recovery plans, hello supported configurations and prerequisites.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="2f80a-111">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="2f80a-111">Prerequisites</span></span>

<span data-ttu-id="2f80a-112">Başlamadan önce hello aşağıdaki anladığınızdan emin olun:</span><span class="sxs-lookup"><span data-stu-id="2f80a-112">Before you start, make sure you understand hello following:</span></span>

1. [<span data-ttu-id="2f80a-113">Bir sanal makine tooAzure çoğaltma</span><span class="sxs-lookup"><span data-stu-id="2f80a-113">Replicating a virtual machine tooAzure</span></span>](site-recovery-vmware-to-azure.md)
1. <span data-ttu-id="2f80a-114">Nasıl çok[kurtarma ağını tasarlama](site-recovery-network-design.md)</span><span class="sxs-lookup"><span data-stu-id="2f80a-114">How too[design a recovery network](site-recovery-network-design.md)</span></span>
1. [<span data-ttu-id="2f80a-115">Bir test yük devretme tooAzure yapılması</span><span class="sxs-lookup"><span data-stu-id="2f80a-115">Doing a test failover tooAzure</span></span>](site-recovery-test-failover-to-azure.md)
1. [<span data-ttu-id="2f80a-116">Bir yük devretme tooAzure yapılması</span><span class="sxs-lookup"><span data-stu-id="2f80a-116">Doing a failover tooAzure</span></span>](site-recovery-failover.md)
1. <span data-ttu-id="2f80a-117">Nasıl çok[bir etki alanı denetleyicisi çoğaltma](site-recovery-active-directory.md)</span><span class="sxs-lookup"><span data-stu-id="2f80a-117">How too[replicate a domain controller](site-recovery-active-directory.md)</span></span>
1. <span data-ttu-id="2f80a-118">Nasıl çok[SQL Server çoğaltma](site-recovery-sql.md)</span><span class="sxs-lookup"><span data-stu-id="2f80a-118">How too[replicate SQL Server](site-recovery-sql.md)</span></span>

## <a name="deployment-patterns"></a><span data-ttu-id="2f80a-119">Dağıtım modelleri</span><span class="sxs-lookup"><span data-stu-id="2f80a-119">Deployment patterns</span></span>

<span data-ttu-id="2f80a-120">Citrix XenApp ve XenDesktop grubu genel dağıtım desen aşağıdaki hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="2f80a-120">A Citrix XenApp and XenDesktop farm typically has hello following deployment pattern:</span></span>

<span data-ttu-id="2f80a-121">**Dağıtım modeli**</span><span class="sxs-lookup"><span data-stu-id="2f80a-121">**Deployment pattern**</span></span>

<span data-ttu-id="2f80a-122">Citrix XenApp ve XenDesktop dağıtımı ile AD DNS sunucusu, SQL veritabanı sunucusu, Citrix teslim denetleyicisi mağaza sunucusu XenApp ana (VDA), Citrix XenApp lisans</span><span class="sxs-lookup"><span data-stu-id="2f80a-122">Citrix XenApp and XenDesktop deployment with AD DNS server, SQL database server, Citrix Delivery Controller, StoreFront server, XenApp Master (VDA), Citrix XenApp License Server</span></span>

![Dağıtım modeli 1](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-deployment.png)


## <a name="site-recovery-support"></a><span data-ttu-id="2f80a-124">Site kurtarma desteği</span><span class="sxs-lookup"><span data-stu-id="2f80a-124">Site Recovery support</span></span>

<span data-ttu-id="2f80a-125">Merhaba amacı, bu makalenin için VMware sanal makineleri Citrix dağıtımlarında 6.0 vSphere tarafından yönetilen / System Center VMM 2012 R2 olan kullanılan toosetup DR.</span><span class="sxs-lookup"><span data-stu-id="2f80a-125">For hello purpose of this article, Citrix deployments on VMware virtual machines managed by vSphere 6.0 / System Center VMM 2012 R2 were used toosetup DR.</span></span>

### <a name="source-and-target"></a><span data-ttu-id="2f80a-126">Kaynak ve hedef</span><span class="sxs-lookup"><span data-stu-id="2f80a-126">Source and target</span></span>

<span data-ttu-id="2f80a-127">**Senaryo**</span><span class="sxs-lookup"><span data-stu-id="2f80a-127">**Scenario**</span></span> | <span data-ttu-id="2f80a-128">**tooa ikincil site**</span><span class="sxs-lookup"><span data-stu-id="2f80a-128">**tooa secondary site**</span></span> | <span data-ttu-id="2f80a-129">**tooAzure**</span><span class="sxs-lookup"><span data-stu-id="2f80a-129">**tooAzure**</span></span>
--- | --- | ---
<span data-ttu-id="2f80a-130">**Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="2f80a-130">**Hyper-V**</span></span> | <span data-ttu-id="2f80a-131">Kapsamda değil</span><span class="sxs-lookup"><span data-stu-id="2f80a-131">Not in scope</span></span> | <span data-ttu-id="2f80a-132">Evet</span><span class="sxs-lookup"><span data-stu-id="2f80a-132">Yes</span></span>
<span data-ttu-id="2f80a-133">**VMware**</span><span class="sxs-lookup"><span data-stu-id="2f80a-133">**VMware**</span></span> | <span data-ttu-id="2f80a-134">Kapsamda değil</span><span class="sxs-lookup"><span data-stu-id="2f80a-134">Not in scope</span></span> | <span data-ttu-id="2f80a-135">Evet</span><span class="sxs-lookup"><span data-stu-id="2f80a-135">Yes</span></span>
<span data-ttu-id="2f80a-136">**Fiziksel sunucu**</span><span class="sxs-lookup"><span data-stu-id="2f80a-136">**Physical server**</span></span> | <span data-ttu-id="2f80a-137">Kapsamda değil</span><span class="sxs-lookup"><span data-stu-id="2f80a-137">Not in scope</span></span> | <span data-ttu-id="2f80a-138">Evet</span><span class="sxs-lookup"><span data-stu-id="2f80a-138">Yes</span></span>

### <a name="versions"></a><span data-ttu-id="2f80a-139">Sürümler</span><span class="sxs-lookup"><span data-stu-id="2f80a-139">Versions</span></span>
<span data-ttu-id="2f80a-140">Müşteriler XenApp bileşenlerini Hyper-V veya VMware üzerinde çalışan sanal makineleri veya fiziksel sunucuları olarak dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2f80a-140">Customers can deploy XenApp components as Virtual Machines running on Hyper-V or VMware or as Physical Servers.</span></span> <span data-ttu-id="2f80a-141">Azure Site Recovery hem fiziksel ve sanal dağıtımları tooAzure koruyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2f80a-141">Azure Site Recovery can protect both physical and virtual deployments tooAzure.</span></span>
<span data-ttu-id="2f80a-142">Azure'da XenApp 7.7 veya sonraki desteklenen olduğundan, yalnızca bu sürümleri dağıtımlar olağanüstü durum kurtarma veya geçiş için tooAzure çalışılabilir.</span><span class="sxs-lookup"><span data-stu-id="2f80a-142">Since XenApp 7.7 or later is supported in Azure, only deployments with these versions can be failed over tooAzure for Disaster Recovery or migration.</span></span>

### <a name="things-tookeep-in-mind"></a><span data-ttu-id="2f80a-143">Şeyler tookeep unutmayın</span><span class="sxs-lookup"><span data-stu-id="2f80a-143">Things tookeep in mind</span></span>

1. <span data-ttu-id="2f80a-144">Koruma ve kurtarma şirket içi sunucu işletim sistemi makineler toodeliver kullanarak XenApp yayımlanan uygulama ve XenApp yayımlanan Masaüstü dağıtımları desteklenir.</span><span class="sxs-lookup"><span data-stu-id="2f80a-144">Protection and recovery of on-premises deployments using Server OS machines toodeliver XenApp published apps and XenApp published desktops is supported.</span></span>

2. <span data-ttu-id="2f80a-145">Koruma ve Windows 10 ' da dahil olmak üzere istemci sanal masaüstleri için masaüstü işletim sistemi makineler toodeliver Masaüstü VDI kullanarak şirket içi dağıtımları kurtarma desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="2f80a-145">Protection and recovery of on-premises deployments using desktop OS machines toodeliver Desktop VDI for client virtual desktops, including Windows 10, is not supported.</span></span> <span data-ttu-id="2f80a-146">ASR Masaüstü OS'es makinelerle hello kurtarılmasını desteklemediğinden budur.</span><span class="sxs-lookup"><span data-stu-id="2f80a-146">This is because ASR does not support hello recovery of machines with desktop OS’es.</span></span>  <span data-ttu-id="2f80a-147">Ayrıca, bazı istemci sanal masaüstü (ör. flavours</span><span class="sxs-lookup"><span data-stu-id="2f80a-147">Also, some client virtual desktop flavours (eg.</span></span> <span data-ttu-id="2f80a-148">Windows 7), Azure'da lisans için henüz desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="2f80a-148">Windows 7) are not yet supported for licensing in Azure.</span></span> <span data-ttu-id="2f80a-149">Azure’da istemci/sunucu masaüstlerini lisanslama hakkında [daha fazla bilgi edinin](https://azure.microsoft.com/pricing/licensing-faq/).</span><span class="sxs-lookup"><span data-stu-id="2f80a-149">[Learn More](https://azure.microsoft.com/pricing/licensing-faq/) about licensing for client/server desktops in Azure.</span></span>

3.  <span data-ttu-id="2f80a-150">Azure Site Recovery çoğaltabilir ve mevcut şirket içi MCS veya PV'ler klonlar koruyun.</span><span class="sxs-lookup"><span data-stu-id="2f80a-150">Azure Site Recovery cannot replicate and protect existing on-premises MCS or PVS clones.</span></span>
<span data-ttu-id="2f80a-151">Azure RM teslim denetleyicisinden sağlama kullanarak bu klonlar toorecreate gerekir.</span><span class="sxs-lookup"><span data-stu-id="2f80a-151">You need toorecreate these clones using Azure RM provisioning from Delivery controller.</span></span>

4. <span data-ttu-id="2f80a-152">NetScaler NetScaler FreeBSD üzerinde temel alır ve Azure Site Recovery koruması FreeBSD işletim sistemi desteklemiyor gibi Azure Site Recovery kullanarak korunamaz.</span><span class="sxs-lookup"><span data-stu-id="2f80a-152">NetScaler cannot be protected using Azure Site Recovery as NetScaler is based on FreeBSD and Azure Site Recovery does not support protection of FreeBSD OS.</span></span> <span data-ttu-id="2f80a-153">Toodeploy gerekir ve yük devretme tooAzure sonra yeni bir NetScaler Gereci Azure Market yerden yapılandırmak.</span><span class="sxs-lookup"><span data-stu-id="2f80a-153">You would need toodeploy and configure a new NetScaler appliance from Azure Market place after failover tooAzure.</span></span>


## <a name="replicating-virtual-machines"></a><span data-ttu-id="2f80a-154">Çoğaltma sanal makineler</span><span class="sxs-lookup"><span data-stu-id="2f80a-154">Replicating virtual machines</span></span>

<span data-ttu-id="2f80a-155">Merhaba Citrix XenApp dağıtım bileşenlerini aşağıdaki hello korumalı toobe tooenable çoğaltma ve kurtarma gerekir.</span><span class="sxs-lookup"><span data-stu-id="2f80a-155">hello following components of hello Citrix XenApp deployment need toobe protected tooenable replication and recovery.</span></span>

* <span data-ttu-id="2f80a-156">AD DNS sunucusunun koruma</span><span class="sxs-lookup"><span data-stu-id="2f80a-156">Protection of AD DNS server</span></span>
* <span data-ttu-id="2f80a-157">SQL veritabanı sunucusuna koruma</span><span class="sxs-lookup"><span data-stu-id="2f80a-157">Protection of SQL database server</span></span>
* <span data-ttu-id="2f80a-158">Citrix teslim denetleyicisinin koruma</span><span class="sxs-lookup"><span data-stu-id="2f80a-158">Protection of Citrix Delivery Controller</span></span>
* <span data-ttu-id="2f80a-159">Mağaza sunucusunun korumasını.</span><span class="sxs-lookup"><span data-stu-id="2f80a-159">Protection of StoreFront server.</span></span>
* <span data-ttu-id="2f80a-160">Koruma XenApp yöneticisinin (VDA)</span><span class="sxs-lookup"><span data-stu-id="2f80a-160">Protection of XenApp Master (VDA)</span></span>
* <span data-ttu-id="2f80a-161">Citrix XenApp lisans sunucusu koruma</span><span class="sxs-lookup"><span data-stu-id="2f80a-161">Protection of Citrix XenApp License Server</span></span>


<span data-ttu-id="2f80a-162">**AD DNS sunucusu çoğaltma**</span><span class="sxs-lookup"><span data-stu-id="2f80a-162">**AD DNS server replication**</span></span>

<span data-ttu-id="2f80a-163">Lütfen çok başvurun[korumak Active Directory ve Azure Site Recovery ile DNS](site-recovery-active-directory.md) çoğaltma ve bir etki alanı denetleyicisi Azure'da yapılandırma kılavuzu üzerinde.</span><span class="sxs-lookup"><span data-stu-id="2f80a-163">Please refer too[Protect Active Directory and DNS with Azure Site Recovery](site-recovery-active-directory.md) on guidance for replicating and configuring a domain controller in Azure.</span></span>

<span data-ttu-id="2f80a-164">**SQL veritabanı sunucusu çoğaltma**</span><span class="sxs-lookup"><span data-stu-id="2f80a-164">**SQL database Server replication**</span></span>

<span data-ttu-id="2f80a-165">Lütfen çok başvurun[SQL Server olağanüstü durum kurtarma ve Azure Site Recovery ile SQL Server'ı koruma](site-recovery-sql.md) hello ayrıntılı teknik kılavuzluk etmesi için önerilen SQL sunucuları koruma için Seçenekler.</span><span class="sxs-lookup"><span data-stu-id="2f80a-165">Please refer too[Protect SQL Server with SQL Server disaster recovery and Azure Site Recovery](site-recovery-sql.md) for detailed technical guidance on hello recommended options for protecting SQL servers.</span></span>

<span data-ttu-id="2f80a-166">İzleyin [bu kılavuz](site-recovery-vmware-to-azure.md) hello diğer bileşen sanal makineleri tooAzure toostart çoğaltılıyor.</span><span class="sxs-lookup"><span data-stu-id="2f80a-166">Follow [this guidance](site-recovery-vmware-to-azure.md) toostart replicating hello other component virtual machines tooAzure.</span></span>

![XenApp bileşenlerinin koruma](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-enablereplication.png)

<span data-ttu-id="2f80a-168">**İşlem ve ağ ayarları**</span><span class="sxs-lookup"><span data-stu-id="2f80a-168">**Compute and Network Settings**</span></span>

<span data-ttu-id="2f80a-169">Merhaba makineler korunduktan sonra (durum gösterildiği çoğaltılan öğeler altında "korumalı" gibi), hello işlem ve ağ ayarlarını yapılandırılmış toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="2f80a-169">After hello machines are protected (status shows as “Protected” under Replicated Items), hello Compute and Network settings need toobe configured.</span></span>
<span data-ttu-id="2f80a-170">Buna işlem ve ağ > işlem özellikleri, hello Azure VM adını ve hedef boyutu belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2f80a-170">In Compute and Network > Compute properties, you can specify hello Azure VM name and target size.</span></span>
<span data-ttu-id="2f80a-171">Gerekirse hello adı toocomply Azure gereksinimleri ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="2f80a-171">Modify hello name toocomply with Azure requirements if you need to.</span></span> <span data-ttu-id="2f80a-172">Ayrıca, görüntülemek ve hello hedef ağ, alt ağ ve toohello Azure VM atanacak IP adresi hakkında bilgi ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2f80a-172">You can also view and add information about hello target network, subnet, and IP address that will be assigned toohello Azure VM.</span></span>

<span data-ttu-id="2f80a-173">Merhaba aşağıdakileri göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="2f80a-173">Note hello following:</span></span>

* <span data-ttu-id="2f80a-174">Merhaba hedef IP adresini ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2f80a-174">You can set hello target IP address.</span></span> <span data-ttu-id="2f80a-175">Bir adresi sağlamazsanız, yükü devredilen makine üzerinde hello DHCP kullanır.</span><span class="sxs-lookup"><span data-stu-id="2f80a-175">If you don't provide an address, hello failed over machine will use DHCP.</span></span> <span data-ttu-id="2f80a-176">Yük devretmede kullanılamayan bir adres ayarlarsanız hello yük devretme çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="2f80a-176">If you set an address that isn't available at failover, hello failover won't work.</span></span> <span data-ttu-id="2f80a-177">Merhaba hello test yük devretme ağı testinde Hello adresi varsa, yük devretme sınaması için aynı hedef IP adresi kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="2f80a-177">hello same target IP address can be used for test failover if hello address is available in hello test failover network.</span></span>

* <span data-ttu-id="2f80a-178">Merhaba AD/DNS sunucusu için hello korunuyor hello hello Azure sanal ağı için DNS sunucusu olarak aynı adres hello belirtmenizi adres sağlar şirket içi.</span><span class="sxs-lookup"><span data-stu-id="2f80a-178">For hello AD/DNS server, retaining hello on-premises address lets you specify hello same address as hello DNS server for hello Azure Virtual network.</span></span>

<span data-ttu-id="2f80a-179">ağ bağdaştırıcısı Hello sayısını hello hedef sanal makine için aşağıdaki gibi belirtin hello boyuta göre dikte edilir:</span><span class="sxs-lookup"><span data-stu-id="2f80a-179">hello number of network adapters is dictated by hello size you specify for hello target virtual machine, as follows:</span></span>

*   <span data-ttu-id="2f80a-180">Merhaba hello kaynak makinedeki ağ bağdaştırıcısı sayısı küçük veya buna eşit ise toohello bağdaştırıcı sayısı hello hedef makine boyutu için izin verilen sonra hello hedef olacaktır hello aynı sayıda bağdaştırıcıya hello kaynağı olarak.</span><span class="sxs-lookup"><span data-stu-id="2f80a-180">If hello number of network adapters on hello source machine is less than or equal toohello number of adapters allowed for hello target machine size, then hello target will have hello same number of adapters as hello source.</span></span>
*   <span data-ttu-id="2f80a-181">Merhaba hello kaynak sanal makinenin bağdaştırıcı sayısı hello hedef boyutu sonra hello maksimum hedef boyutu kullanılır için izin verilen hello sayıyı aşarsa.</span><span class="sxs-lookup"><span data-stu-id="2f80a-181">If hello number of adapters for hello source virtual machine exceeds hello number allowed for hello target size then hello target size maximum will be used.</span></span>
* <span data-ttu-id="2f80a-182">Örneğin, kaynak makinenin iki bağdaştırıcısı varsa ve hello hedef makine boyutu dört adet bağdaştırıcıyı destekliyorsa hello hedef makinenin iki bağdaştırıcısı gerekir.</span><span class="sxs-lookup"><span data-stu-id="2f80a-182">For example, if a source machine has two network adapters and hello target machine size supports four, hello target machine will have two adapters.</span></span> <span data-ttu-id="2f80a-183">Merhaba kaynak makinenin iki bağdaştırıcısı varsa, ancak hello hedef boyut yalnızca bir destekler hello hedef makine yalnızca bir bağdaştırıcısı olur.</span><span class="sxs-lookup"><span data-stu-id="2f80a-183">If hello source machine has two adapters but hello supported target size only supports one then hello target machine will have only one adapter.</span></span>
*   <span data-ttu-id="2f80a-184">Merhaba sanal makinede birden fazla ağ bağdaştırıcısı varsa bunların tümü toohello bağlanır aynı ağ.</span><span class="sxs-lookup"><span data-stu-id="2f80a-184">If hello virtual machine has multiple network adapters they will all connect toohello same network.</span></span>
*   <span data-ttu-id="2f80a-185">Merhaba sanal makinede birden fazla ağ bağdaştırıcısı varsa, daha sonra hello birinci hello listede gösterilen hello varsayılan hello Azure sanal makine ağ bağdaştırıcısı olur.</span><span class="sxs-lookup"><span data-stu-id="2f80a-185">If hello virtual machine has multiple network adapters, then hello first one shown in hello list becomes hello Default network adapter in hello Azure virtual machine.</span></span>


## <a name="creating-a-recovery-plan"></a><span data-ttu-id="2f80a-186">Bir kurtarma planı oluşturma</span><span class="sxs-lookup"><span data-stu-id="2f80a-186">Creating a recovery plan</span></span>

<span data-ttu-id="2f80a-187">Çoğaltma hello XenApp bileşen VM'ler için etkinleştirildikten sonra hello sonraki toocreate bir kurtarma planı adımdır.</span><span class="sxs-lookup"><span data-stu-id="2f80a-187">After replication is enabled for hello XenApp component VMs, hello next step is toocreate a recovery plan.</span></span>
<span data-ttu-id="2f80a-188">Bir kurtarma grupları birlikte sanal makinelerle yük devretme ve kurtarma için benzer gereksinimlerini planlayın.</span><span class="sxs-lookup"><span data-stu-id="2f80a-188">A recovery plan groups together virtual machines with similar requirements for failover and recovery.</span></span>  

<span data-ttu-id="2f80a-189">**Adımları toocreate bir kurtarma planı**</span><span class="sxs-lookup"><span data-stu-id="2f80a-189">**Steps toocreate a recovery plan**</span></span>

1. <span data-ttu-id="2f80a-190">Merhaba XenApp bileşen sanal makineleri hello Kurtarma planlaması ekleyin.</span><span class="sxs-lookup"><span data-stu-id="2f80a-190">Add hello XenApp component virtual machines in hello Recovery Plan.</span></span>
2. <span data-ttu-id="2f80a-191">Kurtarma planları tıklatın -> + kurtarma planı.</span><span class="sxs-lookup"><span data-stu-id="2f80a-191">Click Recovery Plans -> + Recovery Plan.</span></span> <span data-ttu-id="2f80a-192">Hello kurtarma planı için kullanımı kolay bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="2f80a-192">Provide an intuitive name for hello recovery plan.</span></span>
3. <span data-ttu-id="2f80a-193">VMware sanal makineler için: VMware işlem sunucusu, hedef olarak Microsoft Azure ve Resource Manager ve öğeleri seçebilir tıklayarak dağıtım modeli olarak kaynak seçme.</span><span class="sxs-lookup"><span data-stu-id="2f80a-193">For VMware virtual machines: Select source as VMware process server, target as Microsoft Azure, and deployment model as Resource Manager and click on Select items.</span></span>
4. <span data-ttu-id="2f80a-194">Hyper-V sanal makineleri için: kaynak VMM sunucusunu seçin, hedef Microsoft Azure ve olarak Resource Manager dağıtım modeli olarak ve Select öğelerde'ı tıklatın ve ardından hello XenApp dağıtım VM'ler seçin.</span><span class="sxs-lookup"><span data-stu-id="2f80a-194">For Hyper-V virtual machines: Select source as VMM server, target as Microsoft Azure, and deployment model as Resource Manager and click on Select items and then select hello XenApp deployment VMs.</span></span>

### <a name="adding-virtual-machines-toofailover-groups"></a><span data-ttu-id="2f80a-195">Sanal makineler toofailover grupları ekleme</span><span class="sxs-lookup"><span data-stu-id="2f80a-195">Adding virtual machines toofailover groups</span></span>

<span data-ttu-id="2f80a-196">Kurtarma planları belirli başlangıç düzeni, komut dosyaları veya el ile eylemler için özelleştirilmiş tooadd yük devretme grupları olabilir.</span><span class="sxs-lookup"><span data-stu-id="2f80a-196">Recovery plans can be customized tooadd failover groups for specific startup order, scripts or manual actions.</span></span> <span data-ttu-id="2f80a-197">grupları aşağıdaki hello toobe eklenen toohello kurtarma planına ihtiyacınız vardır.</span><span class="sxs-lookup"><span data-stu-id="2f80a-197">hello following groups need toobe added toohello recovery plan.</span></span>

1. <span data-ttu-id="2f80a-198">Yük devretme Group1: AD DNS</span><span class="sxs-lookup"><span data-stu-id="2f80a-198">Failover Group1: AD DNS</span></span>
2. <span data-ttu-id="2f80a-199">Yük devretme grup2: SQL Server Vm'leri</span><span class="sxs-lookup"><span data-stu-id="2f80a-199">Failover Group2: SQL Server VMs</span></span>
2. <span data-ttu-id="2f80a-200">Yük devretme Group3: VDA ana görüntü VM</span><span class="sxs-lookup"><span data-stu-id="2f80a-200">Failover Group3: VDA Master Image VM</span></span>
3. <span data-ttu-id="2f80a-201">Yük devretme Grup4: Teslim denetleyici ve mağaza server Vm'leri</span><span class="sxs-lookup"><span data-stu-id="2f80a-201">Failover Group4: Delivery Controller and StoreFront server VMs</span></span>


### <a name="adding-scripts-toohello-recovery-plan"></a><span data-ttu-id="2f80a-202">Toohello kurtarma planı komutlar ekleme</span><span class="sxs-lookup"><span data-stu-id="2f80a-202">Adding scripts toohello recovery plan</span></span>

<span data-ttu-id="2f80a-203">Komut dosyaları önce veya sonra belirli bir grubu bir kurtarma planı çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2f80a-203">Scripts can be run before or after a specific group in a recovery plan.</span></span> <span data-ttu-id="2f80a-204">El ile yapılan eylemler olabilir de dahil ve yük devretme sırasında gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="2f80a-204">Manual actions can be also be included and performed during failover.</span></span>

<span data-ttu-id="2f80a-205">Merhaba özelleştirilmiş kurtarma planı hello aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="2f80a-205">hello customized recovery plan looks like hello below:</span></span>

1. <span data-ttu-id="2f80a-206">Yük devretme Group1: AD DNS</span><span class="sxs-lookup"><span data-stu-id="2f80a-206">Failover Group1: AD DNS</span></span>
2. <span data-ttu-id="2f80a-207">Yük devretme grup2: SQL Server Vm'leri</span><span class="sxs-lookup"><span data-stu-id="2f80a-207">Failover Group2: SQL Server VMs</span></span>
3. <span data-ttu-id="2f80a-208">Yük devretme Group3: VDA ana görüntü VM</span><span class="sxs-lookup"><span data-stu-id="2f80a-208">Failover Group3: VDA Master Image VM</span></span>

   >[!NOTE]     
   ><span data-ttu-id="2f80a-209">Adım 4, 6 ve 7 el ile veya komut dosyası eylemleri içeren olan geçerli tooonly bir şirket içi XenApp > MCS/PV'ler kataloglarıyla ortamı.</span><span class="sxs-lookup"><span data-stu-id="2f80a-209">Steps 4, 6 and 7 containing manual or script actions are applicable tooonly an on-premises XenApp >environment with MCS/PVS catalogs.</span></span>

4. <span data-ttu-id="2f80a-210">Grup 3 el ile veya komut dosyası eylemi: kapatma ana VDA VM hello ana VDA tooAzure başarısız olduğunda VM çalışır durumda olacaktır.</span><span class="sxs-lookup"><span data-stu-id="2f80a-210">Group 3 Manual or script action: Shutdown master VDA VM hello Master VDA VM when failed over tooAzure will be in a running state.</span></span> <span data-ttu-id="2f80a-211">Azure ARM barındırma kullanarak toocreate yeni MCS kataloglar, hello VDA VM durduruldu (ayrılan de) içinde gerekli toobe yöneticisidir durumu.</span><span class="sxs-lookup"><span data-stu-id="2f80a-211">toocreate new MCS catalogs using Azure ARM hosting, hello master VDA VM is required toobe in Stopped (de allocated) state.</span></span> <span data-ttu-id="2f80a-212">Kapatma hello Azure portalından VM.</span><span class="sxs-lookup"><span data-stu-id="2f80a-212">Shutdown hello VM from Azure Portal.</span></span>

5. <span data-ttu-id="2f80a-213">Yük devretme Grup4: Teslim denetleyici ve mağaza server Vm'leri</span><span class="sxs-lookup"><span data-stu-id="2f80a-213">Failover Group4: Delivery Controller and StoreFront server VMs</span></span>
6. <span data-ttu-id="2f80a-214">Group3 el ile veya komut dosyası eylemi 1:</span><span class="sxs-lookup"><span data-stu-id="2f80a-214">Group3 manual or script action 1:</span></span>

    <span data-ttu-id="2f80a-215">***Azure RM ana bilgisayar bağlantı Ekle***</span><span class="sxs-lookup"><span data-stu-id="2f80a-215">***Add Azure RM host connection***</span></span>

    <span data-ttu-id="2f80a-216">Azure ARM ana bilgisayar bağlantı teslim denetleyicisi makine tooprovision Azure yeni MCS kataloglarında oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2f80a-216">Create Azure ARM host connection in Delivery Controller machine tooprovision new MCS catalogs in Azure.</span></span> <span data-ttu-id="2f80a-217">Bu konuda açıklandığı gibi Hello adımları [makale](https://www.citrix.com/blogs/2016/07/21/connecting-to-azure-resource-manager-in-xenapp-xendesktop/).</span><span class="sxs-lookup"><span data-stu-id="2f80a-217">Follow hello steps as explained in this [article](https://www.citrix.com/blogs/2016/07/21/connecting-to-azure-resource-manager-in-xenapp-xendesktop/).</span></span>

7. <span data-ttu-id="2f80a-218">Group3 el ile veya komut dosyası eylemi 2:</span><span class="sxs-lookup"><span data-stu-id="2f80a-218">Group3 manual or script action 2:</span></span>

    <span data-ttu-id="2f80a-219">***MCS kataloglar azure'da yeniden oluşturun***</span><span class="sxs-lookup"><span data-stu-id="2f80a-219">***Re-create MCS Catalogs in Azure***</span></span>

    <span data-ttu-id="2f80a-220">MCS veya PV'ler klonlar hello birincil sitede mevcut hello çoğaltılmış tooAzure olmaz.</span><span class="sxs-lookup"><span data-stu-id="2f80a-220">hello existing MCS or PVS clones on hello primary site will not be replicated tooAzure.</span></span> <span data-ttu-id="2f80a-221">Hello kullanarak bu klonlar ana VDA ve Azure sağlama ARM teslim denetleyicisinden çoğaltılan toorecreate gerekir. Bu konuda açıklandığı gibi Hello adımları [makale](https://www.citrix.com/blogs/2016/09/12/using-xenapp-xendesktop-in-azure-resource-manager/) toocreate MCS Azure'da kataloglar.</span><span class="sxs-lookup"><span data-stu-id="2f80a-221">You need toorecreate these clones using hello replicated master VDA and Azure ARM provisioning from Delivery controller.Follow hello steps as explained in this [article](https://www.citrix.com/blogs/2016/09/12/using-xenapp-xendesktop-in-azure-resource-manager/) toocreate MCS catalogs in Azure.</span></span>

![Kurtarma planı XenApp bileşenleri](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-recoveryplan.png)


   >[!NOTE]
   ><span data-ttu-id="2f80a-223">Komut dosyalarını en kullanabilirsiniz [konumu](https://github.com/Azure/azure-quickstart-templates/blob/>master/asr-automation-recovery/scripts) Merhaba, yeni IP başarısız üzerinden hello ile tooupdate hello DNS > sanal makine ya da tooattach hello yük dengeleyicide gerekirse, sanal makine üzerinde başarısız.</span><span class="sxs-lookup"><span data-stu-id="2f80a-223">You can use scripts at [location](https://github.com/Azure/azure-quickstart-templates/blob/>master/asr-automation-recovery/scripts) tooupdate hello DNS with hello new IPs of hello failed over >virtual machines or tooattach a load balancer on hello failed over virtual machine, if needed.</span></span>


## <a name="doing-a-test-failover"></a><span data-ttu-id="2f80a-224">Yük devretme sınamasını yapmak</span><span class="sxs-lookup"><span data-stu-id="2f80a-224">Doing a test failover</span></span>

<span data-ttu-id="2f80a-225">İzleyin [bu kılavuz](site-recovery-test-failover-to-azure.md) toodo yük devretme sınaması.</span><span class="sxs-lookup"><span data-stu-id="2f80a-225">Follow [this guidance](site-recovery-test-failover-to-azure.md) toodo a test failover.</span></span>

![Kurtarma planı](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-tfo.png)


## <a name="doing-a-failover"></a><span data-ttu-id="2f80a-227">Bir yük devretme işleminden</span><span class="sxs-lookup"><span data-stu-id="2f80a-227">Doing a failover</span></span>

<span data-ttu-id="2f80a-228">İzleyin [bu kılavuz](site-recovery-failover.md) , yaparken bir yük devretme.</span><span class="sxs-lookup"><span data-stu-id="2f80a-228">Follow [this guidance](site-recovery-failover.md) when you are doing a failover.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2f80a-229">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2f80a-229">Next steps</span></span>

<span data-ttu-id="2f80a-230">Yapabilecekleriniz [daha fazla bilgi edinin](https://aka.ms/citrix-xenapp-xendesktop-with-asr) Bu teknik incelemede Citrix XenApp ve XenDesktop dağıtımlarda çoğaltma hakkında.</span><span class="sxs-lookup"><span data-stu-id="2f80a-230">You can [learn more](https://aka.ms/citrix-xenapp-xendesktop-with-asr) about replicating Citrix XenApp and XenDesktop deployments  in this white paper.</span></span> <span data-ttu-id="2f80a-231">Merhaba Kılavuzu çok Ara[diğer uygulamaları çoğaltmak](site-recovery-workload.md) Site RECOVERY'yi kullanarak.</span><span class="sxs-lookup"><span data-stu-id="2f80a-231">Look at hello guidance too[replicate other applications](site-recovery-workload.md) using Site Recovery.</span></span>
