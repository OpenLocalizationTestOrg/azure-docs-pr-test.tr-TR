---
title: "Azure Site Recovery ile Hyper-V (System Center VMM olmadan) tooAzure çoğaltma için ağ aaaPlan | Microsoft Docs"
description: "Bu makalede, Hyper-V Vm'lerini (VMM olmadan) tooAzure çoğaltırken gerekli ağ planlaması anlatılmaktadır."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 5ca12254-975d-48e8-a84d-422825dac9b2
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: a35de72b53ca921a7b9bfca00a0edcb9416d5aa2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="step-4-plan-networking-for-hyper-v-tooazure-replication"></a><span data-ttu-id="f3d79-103">4. adım: ağ bağlantısı Hyper-V tooAzure çoğaltma için planlama</span><span class="sxs-lookup"><span data-stu-id="f3d79-103">Step 4: Plan networking for Hyper-V tooAzure replication</span></span>

<span data-ttu-id="f3d79-104">Bu makalede ağ çoğaltmaya hello kullanarak Hyper-V Vm'lerini (System Center VMM olmadan) tooAzure şirket içi zaman planlama konuları özetler [Azure Site Recovery](site-recovery-overview.md) hizmet.</span><span class="sxs-lookup"><span data-stu-id="f3d79-104">This article summarizes network planning considerations when replicating on-premises Hyper-V VMs (without System Center VMM) tooAzure using hello [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="f3d79-105">Bu makalenin hello altındaki tüm yorumlar gönderin ya da hello sorular sormak [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="f3d79-105">Post any comments at hello bottom of this article, or ask questions in hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="connecting-tooreplica-vms-after-failover"></a><span data-ttu-id="f3d79-106">Yük devretme sonrasında tooreplica VM'ler bağlanma</span><span class="sxs-lookup"><span data-stu-id="f3d79-106">Connecting tooreplica VMs after failover</span></span>

<span data-ttu-id="f3d79-107">Çoğaltma ve yük devretme stratejinizi planlarken hello önemli sorular biri nasıl yük devretme sonrasında Azure VM'de tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="f3d79-107">When planning your replication and failover strategy, one of hello key questions is how tooconnect toohello Azure VM after failover.</span></span> <span data-ttu-id="f3d79-108">Çoğaltma Azure VM'ler için ağ stratejinizi tasarlarken, birkaç seçeneğiniz vardır:</span><span class="sxs-lookup"><span data-stu-id="f3d79-108">There are a couple of choices when designing your network strategy for replica Azure VMs:</span></span>

- <span data-ttu-id="f3d79-109">**Farklı bir IP adresi**: hello çoğaltılan Azure VM ağında için farklı bir IP adresi aralığı toouse seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f3d79-109">**Different IP address**: You can select toouse a different IP address range for hello replicated Azure VM network.</span></span> <span data-ttu-id="f3d79-110">Bu senaryo hello VM yük devretme sonrasında yeni bir IP adresi alır ve DNS güncelleştirme gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="f3d79-110">In this scenario hello VM gets a new IP address after failover, and a DNS update is required.</span></span> [<span data-ttu-id="f3d79-111">Daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="f3d79-111">Learn more</span></span>](site-recovery-test-failover-vmm-to-vmm.md#prepare-the-infrastructure-for-test-failover)
- <span data-ttu-id="f3d79-112">**Aynı IP adresini**: istiyor, birincil şirket içi, Merhaba Azure ağı yük devretme sonrasında ağ olarak toouse hello aynı IP adresi aralığı.</span><span class="sxs-lookup"><span data-stu-id="f3d79-112">**Same IP address**: You might want toouse hello same IP address range as that in your primary on-premises network, for hello Azure network after failover.</span></span>  <span data-ttu-id="f3d79-113">Aynı IP adreslerini basitleştirir tutma hello azaltarak hello kurtarma yük devretme sonrasında ilgili sorunlar ağ.</span><span class="sxs-lookup"><span data-stu-id="f3d79-113">Keeping hello same IP addresses simplifies hello recovery by reducing network related issues after failover.</span></span> <span data-ttu-id="f3d79-114">Ancak, tooAzure çoğaltırken, yük devretme sonrasında tooupdate yollar hello IP adreslerinin hello yeni konumla gerekir.</span><span class="sxs-lookup"><span data-stu-id="f3d79-114">However, when you're replicating tooAzure, you will need tooupdate routes with hello new location of hello IP addresses after failover.</span></span>


## <a name="retain-ip-addresses"></a><span data-ttu-id="f3d79-115">IP adreslerini korur</span><span class="sxs-lookup"><span data-stu-id="f3d79-115">Retain IP addresses</span></span>

<span data-ttu-id="f3d79-116">Site Recovery, bir alt ağ yük devretme ile tooAzure üzerinden başarısız olduğunda hello yetenek tooretain sabit IP adresleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="f3d79-116">Site Recovery provides hello capability tooretain fixed IP addresses when failing over tooAzure, with a subnet failover.</span></span>

<span data-ttu-id="f3d79-117">Alt ağ yük devretmesi ile belirli bir alt aynı anda Site 1 veya her iki sitede ancak hiçbir Site 2 konumunda bulunur.</span><span class="sxs-lookup"><span data-stu-id="f3d79-117">With subnet failover, a specific subnet is present at Site 1 or Site 2, but never at both sites simultaneously.</span></span> <span data-ttu-id="f3d79-118">Sipariş toomaintain hello IP adres alanı bir yük devretme hello olaydaki, program aracılığıyla hello yönlendirici altyapı toomove hello alt ağlardan bir site tooanother için düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="f3d79-118">In order toomaintain hello IP address space in hello event of a failover, you programmatically arrange for hello router infrastructure toomove hello subnets from one site tooanother.</span></span> <span data-ttu-id="f3d79-119">Yük devretme sırasında korumalı VM'lerin hello alt ağlar taşıma hello ile ilişkilendirilmiş.</span><span class="sxs-lookup"><span data-stu-id="f3d79-119">During failover, hello subnets move with hello associated protected VMs.</span></span> <span data-ttu-id="f3d79-120">Merhaba asıl sakıncası bir hatanın hello olayı, toomove hello tüm alt ağı olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="f3d79-120">hello main drawback is that in hello event of a failure, you have toomove hello whole subnet.</span></span>


### <a name="failover-example"></a><span data-ttu-id="f3d79-121">Yük devretme örneği</span><span class="sxs-lookup"><span data-stu-id="f3d79-121">Failover example</span></span>

<span data-ttu-id="f3d79-122">Yük devretme tooAzure için bir örneğe bakalım.</span><span class="sxs-lookup"><span data-stu-id="f3d79-122">Let's look at an example for failover tooAzure.</span></span>

- <span data-ttu-id="f3d79-123">Ficticious şirket, Woodgrove Bank, iş uygulamalarını barındıran bir şirket içi altyapı sahiptir.</span><span class="sxs-lookup"><span data-stu-id="f3d79-123">A ficticious company, Woodgrove Bank, has an on-premises infrastructure hosting their business apps.</span></span> <span data-ttu-id="f3d79-124">Kullanıcıların mobil uygulamalar Azure üzerinde barındırılır.</span><span class="sxs-lookup"><span data-stu-id="f3d79-124">Their mobile applications are hosted on Azure.</span></span>
- <span data-ttu-id="f3d79-125">Azure ve şirket içi sunucularda Woodgrove Bank VM'ler arasında bağlantı hello şirket içi uç ağ hello Azure sanal ağı arasında bir siteden siteye (VPN) bağlantısı tarafından sağlanır.</span><span class="sxs-lookup"><span data-stu-id="f3d79-125">Connectivity between Woodgrove Bank VMs in Azure and on-premises servers is provided by a site-to-site (VPN) connection between hello on-premises edge network and hello Azure virtual network.</span></span>
- <span data-ttu-id="f3d79-126">Azure sanal ağında şirketin hello VPN deyişle kendi şirket içi ağ bir uzantısı olarak görünür.</span><span class="sxs-lookup"><span data-stu-id="f3d79-126">This VPN means that hello company's virtual network in Azure appears as an extension of their on-premises network.</span></span>
- <span data-ttu-id="f3d79-127">Woodgrove toouse Site Recovery tooreplicate şirket içi iş yüklerini tooAzure istemektedir.</span><span class="sxs-lookup"><span data-stu-id="f3d79-127">Woodgrove wants toouse Site Recovery tooreplicate on-premises workloads tooAzure.</span></span>
 - <span data-ttu-id="f3d79-128">Woodgrove toodeal uygulamaları ve IP adreslerini sabit kodlanmış bağlıdır ve dolayısıyla tooretain IP adresi için kendi uygulamalarında sonra Yük devretme tooAzure kullanması gereken yapılandırmaları vardır.</span><span class="sxs-lookup"><span data-stu-id="f3d79-128">Woodgrove has toodeal with applications and configurations which depend on hard-coded IP addresses, and thus need tooretain IP addresses for their applications after failover tooAzure.</span></span>
 - <span data-ttu-id="f3d79-129">Woodgrove atanmış IP adresleri aralığı 172.16.1.0/24 Azure'da çalışan 172.16.2.0/24 tooits kaynakları.</span><span class="sxs-lookup"><span data-stu-id="f3d79-129">Woodgrove has assigned IP addresses from range 172.16.1.0/24, 172.16.2.0/24 tooits resources running in Azure.</span></span>


<span data-ttu-id="f3d79-130">Kendi sanal makineleri tooAzure korunuyor hello sırada IP adresleri Woodgrove toobe mümkün tooreplicate için işte hangi hello şirketin toodo gerekir:</span><span class="sxs-lookup"><span data-stu-id="f3d79-130">For Woodgrove toobe able tooreplicate its VMs tooAzure while retaining hello IP addresses, here's what hello company needs toodo:</span></span>

1. <span data-ttu-id="f3d79-131">Bir Azure sanal ağı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f3d79-131">Create an Azure virtual network.</span></span> <span data-ttu-id="f3d79-132">Böylece uygulamaları sorunsuz bir şekilde yük devredebildiğini hello uzantısı ağ, şirket içi olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f3d79-132">It should be an extension of hello on-premises network, so that applications can fail over seamlessly.</span></span>
2. <span data-ttu-id="f3d79-133">Azure, tooadd siteden siteye VPN bağlantısı, ayrıca Azure içinde oluşturulan toopoint site bağlantısı toohello sanal ağlar sağlar.</span><span class="sxs-lookup"><span data-stu-id="f3d79-133">Azure allows you tooadd site-to-site VPN connectivity, in addition toopoint-to-site connectivity toohello virtual networks created in Azure.</span></span>
3. <span data-ttu-id="f3d79-134">Merhaba siteden siteye bağlantı kurma, hello Azure ağ, başlangıç IP adresi aralığı hello şirket içi IP adresi aralığından farklı olduğunda trafiği toohello şirket içi konumu (yerel ağ) yönlendirebilir.</span><span class="sxs-lookup"><span data-stu-id="f3d79-134">When setting up hello site-to-site connection, in hello Azure network, you can route traffic toohello on-premises location (local-network) only if hello IP address range is different from hello on-premises IP address range.</span></span>
    - <span data-ttu-id="f3d79-135">Azure esnetilen alt ağları desteklemiyor olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="f3d79-135">This is because Azure doesn’t support stretched subnets.</span></span> <span data-ttu-id="f3d79-136">Bu nedenle içi 192.168.1.0/24 alt ağı varsa, bir yerel ağ 192.168.1.0/24 hello Azure ağı eklenemiyor.</span><span class="sxs-lookup"><span data-stu-id="f3d79-136">So if you have subnet 192.168.1.0/24 on-premises, you can’t add a local-network 192.168.1.0/24 in hello Azure network.</span></span>
    - <span data-ttu-id="f3d79-137">Azure hello alt ağda etkin VM yok ve yalnızca olağanüstü durum kurtarma için oluşturulan hello alt bilmiyor çünkü bu beklenir.</span><span class="sxs-lookup"><span data-stu-id="f3d79-137">This is expected because Azure doesn’t know that there are no active VMs in hello subnet, and that hello subnet is being created for disaster recovery only.</span></span>
    - <span data-ttu-id="f3d79-138">toobe mümkün toocorrectly ağ trafiğini yönlendirmek hello ağ ve hello yerel ağ bir Azure ağı hello alt dışında çakışma gerekir.</span><span class="sxs-lookup"><span data-stu-id="f3d79-138">toobe able toocorrectly route network traffic out of an Azure network hello subnets in hello network and hello local-network mustn't conflict.</span></span>

![Alt ağ yük devretme önce](./media/hyper-v-site-walkthrough-network/network-design7.png)

### <a name="before-failover"></a><span data-ttu-id="f3d79-140">Önce yük devretme</span><span class="sxs-lookup"><span data-stu-id="f3d79-140">Before failover</span></span>

1. <span data-ttu-id="f3d79-141">Ek bir ağa (örneğin kurtarma ağ) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f3d79-141">Create an additional network (for example Recovery Network).</span></span> <span data-ttu-id="f3d79-142">Bu hello ağdır VM'ler başarısız olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="f3d79-142">This is hello network in which failed over VMs are created.</span></span>
2. <span data-ttu-id="f3d79-143">IP adresi için bir VM hello tooensure hello VM Özellikleri'nde, yük devretme sonrasında tutulur > **yapılandırma**, aynı IP adresi VM içi sahip ve'ı tıklatın, hello hello belirtin **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="f3d79-143">tooensure that hello IP address for a VM is retained after a failover, in hello VM properties > **Configure**, specify hello same IP address that hello VM has on-premises, and click **Save**.</span></span>
3. <span data-ttu-id="f3d79-144">Merhaba VM üzerinden başarısız olduğunda, Azure Site Recovery IP adresi tooit sağlanan hello atayın.</span><span class="sxs-lookup"><span data-stu-id="f3d79-144">When hello VM is failed over, Azure Site Recovery will assign hello provided IP address tooit.</span></span>

    ![Ağ Özellikleri](./media/hyper-v-site-walkthrough-network/network-design8.png)

4. <span data-ttu-id="f3d79-146">Yük devretme tetikleyici tetiklenir ve hello VM'ler Azure'da hello gerekli IP adresi ile oluşturulur olduktan sonra ağ toohello kullanarak bağlanabilir bir [Vnet tooVnet vonnection](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).</span><span class="sxs-lookup"><span data-stu-id="f3d79-146">After failover is trigger is triggered, and hello VMs are created in Azure with hello required IP address, you can connect toohello network using a [Vnet tooVnet vonnection](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).</span></span> <span data-ttu-id="f3d79-147">Bu eylem betiği yazılabilir.</span><span class="sxs-lookup"><span data-stu-id="f3d79-147">This action can be scripted.</span></span>
5. <span data-ttu-id="f3d79-148">Yollar uygun şekilde değiştirilmiş toobe tooreflect gerekir, 192.168.1.0/24 şimdi tooAzure taşındı.</span><span class="sxs-lookup"><span data-stu-id="f3d79-148">Routes need toobe appropriately modified, tooreflect that 192.168.1.0/24 has now moved tooAzure.</span></span>

    ![Alt ağ yük devretme sonrasında](./media/hyper-v-site-walkthrough-network/network-design9.png)

### <a name="after-failover"></a><span data-ttu-id="f3d79-150">Yük devretme sonrasında</span><span class="sxs-lookup"><span data-stu-id="f3d79-150">After failover</span></span>

<span data-ttu-id="f3d79-151">Yukarıda gösterildiği gibi bir Azure ağı yoksa, failvoer sonra birincil site ile Azure arasında siteden siteye VPN bağlantısı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f3d79-151">If you don't have an Azure network as illustrated above, you can create a site-to-site VPN connection between your primary site and Azure, after failvoer.</span></span>

## <a name="change-ip-addresses"></a><span data-ttu-id="f3d79-152">IP adreslerini değiştirin</span><span class="sxs-lookup"><span data-stu-id="f3d79-152">Change IP addresses</span></span>

<span data-ttu-id="f3d79-153">Bu [blog gönderisi](http://azure.microsoft.com/blog/2014/09/04/networking-infrastructure-setup-for-microsoft-azure-as-a-disaster-recovery-site/) tooset hello tooretain IP gerekmediğinde Azure ağ altyapısı yukarı yük devretme sonrasında nasıl ele açıklar.</span><span class="sxs-lookup"><span data-stu-id="f3d79-153">This [blog post](http://azure.microsoft.com/blog/2014/09/04/networking-infrastructure-setup-for-microsoft-azure-as-a-disaster-recovery-site/) explains how tooset up hello Azure networking infrastructure when you don't need tooretain IP addresses after failover.</span></span> <span data-ttu-id="f3d79-154">Uygulama açıklaması ile başlayan, nasıl tooset ağ şirket içi ve Azure arar ve yük devretme işlemleri çalıştırma hakkında bilgi ile sonlanır.</span><span class="sxs-lookup"><span data-stu-id="f3d79-154">It starts with an application description, looks at how tooset up networking on-premises and in Azure, and concludes with information about running failovers.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="f3d79-155">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f3d79-155">Next steps</span></span>

<span data-ttu-id="f3d79-156">Çok Git[5. adım: Azure hazırlama](hyper-v-site-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="f3d79-156">Go too[Step 5: Prepare Azure](hyper-v-site-walkthrough-prepare-azure.md)</span></span>
