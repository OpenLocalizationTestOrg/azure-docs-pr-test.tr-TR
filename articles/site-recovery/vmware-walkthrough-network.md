---
title: "Azure çoğaltma için VMware ağ planı | Microsoft Docs"
description: "Bu makalede VMware Vm'lerini Azure'a çoğaltırken ağ gerekli planlama açıklanır"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 5578a0b4-0352-41c3-9cce-56beb17a4d97
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: f164ac68ba6ec650bb3996b4aa870e1b98533a23
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="step-4-plan-networking-for-vmware-to-azure-replication"></a><span data-ttu-id="58412-103">4. adım: Azure çoğaltma VMware için ağ planlama</span><span class="sxs-lookup"><span data-stu-id="58412-103">Step 4: Plan networking for VMware to Azure replication</span></span>

<span data-ttu-id="58412-104">Bu makalede ağ çoğaltmaya VMware Vm'lerini Azure kullanarak şirket içi zaman planlama konuları özetler [Azure Site Recovery](site-recovery-overview.md) hizmet.</span><span class="sxs-lookup"><span data-stu-id="58412-104">This article summarizes network planning considerations when replicating on-premises VMware VMs to Azure using the [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="58412-105">Tüm yorumlarınızı bu makalenin alt kısmında paylaşabilir veya [Azure Kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)'nda soru sorabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="58412-105">Post any comments at the bottom of this article, or ask questions in the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="connect-to-replica-vms"></a><span data-ttu-id="58412-106">Çoğaltma sanal makineleri Bağlan</span><span class="sxs-lookup"><span data-stu-id="58412-106">Connect to replica VMs</span></span>

<span data-ttu-id="58412-107">Çoğaltma ve yük devretme stratejinizi planlarken, önemli sorular yük devretme sonrasında Azure VM'ye bağlanma biridir.</span><span class="sxs-lookup"><span data-stu-id="58412-107">When planning your replication and failover strategy, one of the key questions is how to connect to the Azure VM after failover.</span></span> <span data-ttu-id="58412-108">Çoğaltma Azure VM'ler için ağ stratejinizi tasarlarken, birkaç seçeneğiniz vardır:</span><span class="sxs-lookup"><span data-stu-id="58412-108">There are a couple of choices when designing your network strategy for replica Azure VMs:</span></span>

- <span data-ttu-id="58412-109">**Farklı bir IP adresi kullanmak**: çoğaltılan Azure VM ağı için farklı bir IP adresi aralığı kullanmayı seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="58412-109">**Use different IP address**: You can select to use a different IP address range for the replicated Azure VM network.</span></span> <span data-ttu-id="58412-110">Bu senaryoda VM yük devretme sonrasında yeni bir IP adresi alır ve DNS güncelleştirme gereklidir.</span><span class="sxs-lookup"><span data-stu-id="58412-110">In this scenario the VM gets a new IP address after failover, and a DNS update is required.</span></span>
- <span data-ttu-id="58412-111">**Aynı IP adresini korumak**: aynı IP adresi aralığı olarak birincil şirket içi sitenizdeki yük devretme sonrasında Azure ağı için kullanmak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="58412-111">**Retain same IP address**: You might want to use the same IP address range as that in your primary on-premises site, for the Azure network after failover.</span></span> <span data-ttu-id="58412-112">Tutma aynı IP adreslerini basitleştirir kurtarma azaltarak ağ ile ilgili sorunları yük devretme sonrasında.</span><span class="sxs-lookup"><span data-stu-id="58412-112">Keeping the same IP addresses simplifies the recovery by reducing network related issues after failover.</span></span> <span data-ttu-id="58412-113">Ancak, Azure'a çoğaltma yapıyorsanız, yolları yeni konumunu IP adresleri ile yük devretme sonrasında güncelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="58412-113">However, when you're replicating to Azure, you will need to update routes with the new location of the IP addresses after failover.</span></span> 


## <a name="retain-ip-addresses"></a><span data-ttu-id="58412-114">IP adreslerini korur</span><span class="sxs-lookup"><span data-stu-id="58412-114">Retain IP addresses</span></span>

<span data-ttu-id="58412-115">Site Recovery sabit IP korumak özelliği üzerinden Azure için bir alt ağ yük devretme kümelemesiyle başarısız olduğunda adresleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="58412-115">Site Recovery provides the capability to retain fixed IP addresses when failing over to Azure, with a subnet failover.</span></span>

<span data-ttu-id="58412-116">Alt ağ yük devretmesi ile belirli bir alt aynı anda Site 1 veya her iki sitede ancak hiçbir Site 2 konumunda bulunur.</span><span class="sxs-lookup"><span data-stu-id="58412-116">With subnet failover, a specific subnet is present at Site 1 or Site 2, but never at both sites simultaneously.</span></span> <span data-ttu-id="58412-117">IP adres alanı bir yük devretme durumunda korumak için program aracılığıyla alt ağların bir siteden diğerine taşımak yönlendirici altyapı düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="58412-117">In order to maintain the IP address space in the event of a failover, you programmatically arrange for the router infrastructure to move the subnets from one site to another.</span></span> <span data-ttu-id="58412-118">Yük devretme sırasında alt ağlar ile ilişkili korumalı sanal makineleri taşıyın.</span><span class="sxs-lookup"><span data-stu-id="58412-118">During failover, the subnets move with the associated protected VMs.</span></span> <span data-ttu-id="58412-119">Bir arıza olması durumunda olan asıl sakıncası, tüm alt ağı taşımanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="58412-119">The main drawback is that in the event of a failure, you have to move the whole subnet.</span></span>


### <a name="failover-example"></a><span data-ttu-id="58412-120">Yük devretme örneği</span><span class="sxs-lookup"><span data-stu-id="58412-120">Failover example</span></span>

<span data-ttu-id="58412-121">Azure'a yük devretme için bir örneğe bakalım.</span><span class="sxs-lookup"><span data-stu-id="58412-121">Let's look at an example for failover to Azure.</span></span>

- <span data-ttu-id="58412-122">Ficticious şirket, Woodgrove Bank, iş uygulamalarını barındıran bir şirket içi altyapı sahiptir.</span><span class="sxs-lookup"><span data-stu-id="58412-122">A ficticious company, Woodgrove Bank, has an on-premises infrastructure hosting their business apps.</span></span> <span data-ttu-id="58412-123">Kullanıcıların mobil uygulamalar Azure üzerinde barındırılır.</span><span class="sxs-lookup"><span data-stu-id="58412-123">Their mobile applications are hosted on Azure.</span></span>
- <span data-ttu-id="58412-124">Azure ve şirket içi sunucularda Woodgrove Bank VMs arasındaki bağlantıyı, şirket içi uç ağ ve Azure sanal ağı arasında bir siteden siteye (VPN) bağlantısı tarafından sağlanır.</span><span class="sxs-lookup"><span data-stu-id="58412-124">Connectivity between Woodgrove Bank VMs in Azure and on-premises servers is provided by a site-to-site (VPN) connection between the on-premises edge network and the Azure virtual network.</span></span>
- <span data-ttu-id="58412-125">Bu VPN Azure sanal ağında şirketin kendi şirket içi ağ bir uzantısı olarak görüneceği anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="58412-125">This VPN means that the company's virtual network in Azure appears as an extension of their on-premises network.</span></span>
- <span data-ttu-id="58412-126">Woodgrove şirket içi iş yüklerini Azure'a çoğaltmak için Site Recovery kullanmak istiyor.</span><span class="sxs-lookup"><span data-stu-id="58412-126">Woodgrove wants to use Site Recovery to replicate on-premises workloads to Azure.</span></span>
 - <span data-ttu-id="58412-127">Uygulamalar ve IP adreslerini sabit kodlanmış bağlıdır ve bu nedenle Azure için yük devretme sonrasında uygulamaları için IP adreslerini bekletmeniz gerekir yapılandırmalarını uğraşmanız Woodgrove sahiptir.</span><span class="sxs-lookup"><span data-stu-id="58412-127">Woodgrove has to deal with applications and configurations which depend on hard-coded IP addresses, and thus need to retain IP addresses for their applications after failover to Azure.</span></span>
 - <span data-ttu-id="58412-128">Woodgrove atanmış IP adresleri aralığı 172.16.1.0/24, Azure'da çalışan kendi kaynaklarına 172.16.2.0/24 gelen.</span><span class="sxs-lookup"><span data-stu-id="58412-128">Woodgrove has assigned IP addresses from range 172.16.1.0/24, 172.16.2.0/24 to its resources running in Azure.</span></span>


<span data-ttu-id="58412-129">Woodgrove olması için IP adresleri, burada 's ne korurken VM'LERİNİ Azure'a çoğaltmak için şirket yapması gerekir:</span><span class="sxs-lookup"><span data-stu-id="58412-129">For Woodgrove to be able to replicate its VMS to Azure while retaining the IP addresses, here's what the company needs to do:</span></span>

1. <span data-ttu-id="58412-130">Bir Azure sanal ağı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="58412-130">Create an Azure virtual network.</span></span> <span data-ttu-id="58412-131">Böylece uygulamaları sorunsuz bir şekilde yük devredebildiğini şirket içi ağ uzantısı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="58412-131">It should be an extension of the on-premises network, so that applications can fail over seamlessly.</span></span>
2. <span data-ttu-id="58412-132">Azure siteden siteye VPN bağlantısı, Azure üzerinde oluşturulan sanal ağlar için noktadan siteye bağlantı yanı sıra eklemenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="58412-132">Azure allows you to add site-to-site VPN connectivity, in addition to point-to-site connectivity to the virtual networks created in Azure.</span></span>
3. <span data-ttu-id="58412-133">Yalnızca şirket içi IP adres aralığından IP adresi aralığı farklıysa Azure ağında siteden siteye bağlantı kurarken şirket içi konumuna (yerel ağ) trafiği yönlendirebilir.</span><span class="sxs-lookup"><span data-stu-id="58412-133">When setting up the site-to-site connection, in the Azure network, you can route traffic to the on-premises location (local-network) only if the IP address range is different from the on-premises IP address range.</span></span>
    - <span data-ttu-id="58412-134">Azure esnetilen alt ağları desteklemiyor olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="58412-134">This is because Azure doesn’t support stretched subnets.</span></span> <span data-ttu-id="58412-135">Bu nedenle alt 192.168.1.0/24 şirket içi varsa, Azure ağında bir yerel ağ 192.168.1.0/24 ekleyemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="58412-135">So if you have subnet 192.168.1.0/24 on-premises, you can’t add a local-network 192.168.1.0/24 in the Azure network.</span></span>
    - <span data-ttu-id="58412-136">Azure alt ağda etkin VM yok ve yalnızca olağanüstü durum kurtarma için alt ağ oluşturulmaktadır bilmiyor çünkü bu beklenir.</span><span class="sxs-lookup"><span data-stu-id="58412-136">This is expected because Azure doesn’t know that there are no active VMs in the subnet, and that the subnet is being created for disaster recovery only.</span></span>
    - <span data-ttu-id="58412-137">Doğru alt ağ ve yerel ağ çakışma dpm'nin bir Azure ağı dışında ağ trafiğini yönlendirmek için.</span><span class="sxs-lookup"><span data-stu-id="58412-137">To be able to correctly route network traffic out of an Azure network the subnets in the network and the local-network mustn't conflict.</span></span>

![Alt ağ yük devretme önce](./media/site-recovery-network-design/network-design7.png)

### <a name="before-failover"></a><span data-ttu-id="58412-139">Önce yük devretme</span><span class="sxs-lookup"><span data-stu-id="58412-139">Before failover</span></span>

1. <span data-ttu-id="58412-140">Ek bir ağa (örneğin kurtarma ağ) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="58412-140">Create an additional network (for example Recovery Network).</span></span> <span data-ttu-id="58412-141">Bu ağdır VM'ler başarısız olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="58412-141">This is the network in which failed over VMs are created.</span></span>
2. <span data-ttu-id="58412-142">Bir VM için IP adresi VM Özellikleri'nde, yük devretme sonrasında korunur emin olmak için > **yapılandırma**VM içi sahip aynı IP adresi belirtin ve tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="58412-142">To ensure that the IP address for a VM is retained after a failover, in the VM properties > **Configure**, specify the same IP address that the VM has on-premises, and click **Save**.</span></span>
3. <span data-ttu-id="58412-143">VM üzerinden başarısız olduğunda, Azure Site Recovery için sağlanan IP adresi atar.</span><span class="sxs-lookup"><span data-stu-id="58412-143">When the VM is failed over, Azure Site Recovery will assign the provided IP address to it.</span></span>

    ![Ağ Özellikleri](./media/site-recovery-network-design/network-design8.png)

4. <span data-ttu-id="58412-145">Yük devretme tetikleyici tetiklenir ve gerekli IP adresi ile oluşturulan sanal makineleri Azure içinde olduktan sonra ağ kullanmaya bağlanabilir bir [Vnet'e bağlantı](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).</span><span class="sxs-lookup"><span data-stu-id="58412-145">After failover is trigger is triggered, and the VMs are created in Azure with the required IP address, you can connect to the network using a [Vnet to Vnet connection](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).</span></span> <span data-ttu-id="58412-146">Bu eylem betiği yazılabilir.</span><span class="sxs-lookup"><span data-stu-id="58412-146">This action can be scripted.</span></span>
5. <span data-ttu-id="58412-147">Yollar uygun şekilde değiştirilmesi, bu 192.168.1.0/24 artık Azure'a taşındı yansıtacak şekilde gerekir.</span><span class="sxs-lookup"><span data-stu-id="58412-147">Routes need to be appropriately modified, to reflect that 192.168.1.0/24 has now moved to Azure.</span></span>

    ![Alt ağ yük devretme sonrasında](./media/site-recovery-network-design/network-design9.png)

### <a name="after-failover"></a><span data-ttu-id="58412-149">Yük devretme sonrasında</span><span class="sxs-lookup"><span data-stu-id="58412-149">After failover</span></span>

<span data-ttu-id="58412-150">Yukarıda gösterildiği gibi bir Azure ağı yoksa, yük devretme sonrasında birincil site ile Azure arasında siteden siteye VPN bağlantısı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="58412-150">If you don't have an Azure network as illustrated above, you can create a site-to-site VPN connection between your primary site and Azure, after failover.</span></span>

## <a name="change-ip-addresses"></a><span data-ttu-id="58412-151">IP adreslerini değiştirin</span><span class="sxs-lookup"><span data-stu-id="58412-151">Change IP addresses</span></span>

<span data-ttu-id="58412-152">Bu [blog gönderisi](http://azure.microsoft.com/blog/2014/09/04/networking-infrastructure-setup-for-microsoft-azure-as-a-disaster-recovery-site/) IP adreslerini yük devretme sonrasında korumak gerekmediğinde Azure ağ altyapısını ayarlamak açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="58412-152">This [blog post](http://azure.microsoft.com/blog/2014/09/04/networking-infrastructure-setup-for-microsoft-azure-as-a-disaster-recovery-site/) explains how to set up the Azure networking infrastructure when you don't need to retain IP addresses after failover.</span></span> <span data-ttu-id="58412-153">Uygulama açıklaması ile başlayan, şirket içi ağ yukarı ve Azure nasıl ayarlanacağını bakar ve yük devretme işlemleri çalıştırma hakkında bilgi ile sonlanır.</span><span class="sxs-lookup"><span data-stu-id="58412-153">It starts with an application description, looks at how to set up networking on-premises and in Azure, and concludes with information about running failovers.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="58412-154">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="58412-154">Next steps</span></span>

<span data-ttu-id="58412-155">Git [5. adım: Azure hazırlama](vmware-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="58412-155">Go to [Step 5: Prepare Azure](vmware-walkthrough-prepare-azure.md)</span></span>
