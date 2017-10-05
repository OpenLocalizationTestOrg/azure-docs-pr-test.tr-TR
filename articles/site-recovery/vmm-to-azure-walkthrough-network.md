---
title: "Azure Site Recovery ile Azure çoğaltma için Hyper-V (withSystem Center VMM) ağ planı | Microsoft Docs"
description: "Bu makalede ele Azure'a Hyper-V Vm'lerini (VMM ile) çoğaltırken ağ gerekli planlama"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 41c3c83e-6b1a-496a-8179-498c552ef0c7
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: ef87cd82b021e40f0da05142878daff245cd9c62
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/29/2017
---
# <a name="step-4-plan-networking-for-hyper-v-with-vmm-to-azure-replication"></a><span data-ttu-id="37f62-103">4. adım: Azure çoğaltma (VMM ile) Hyper-V için ağ planlama</span><span class="sxs-lookup"><span data-stu-id="37f62-103">Step 4: Plan networking for Hyper-V (with VMM) to Azure replication</span></span>

<span data-ttu-id="37f62-104">Gerçekleştirdikten sonra [kapasite planlaması](vmm-to-azure-walkthrough-capacity.md) (tam dağıtımını yaptığınız varsa), ağ çoğaltma System Center Virtual Machine Manager (VMM) bulutlarında, Hyper-V sanal makineleri şirket içi zaman planlama konuları hakkında bilgi edinmek için bu makaleyi okuyun kullanarak [Azure Site Recovery](site-recovery-overview.md) hizmet.</span><span class="sxs-lookup"><span data-stu-id="37f62-104">After performing [capacity planning](vmm-to-azure-walkthrough-capacity.md) (if you're doing a full deployment), read this article to learn about network planning considerations when replicating on-premises Hyper-V VMs in System Center Virtual Machine Manager (VMM) clouds to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="37f62-105">Tüm yorumlarınızı bu makalenin alt kısmında paylaşabilir veya [Azure Kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)'nda soru sorabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="37f62-105">Post any comments at the bottom of this article, or ask questions in the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="network-mapping-for-replication-to-azure"></a><span data-ttu-id="37f62-106">Azure'a çoğaltma için Ağ eşlemesi</span><span class="sxs-lookup"><span data-stu-id="37f62-106">Network mapping for replication to Azure</span></span>

<span data-ttu-id="37f62-107">Ağ eşlemesi Hyper-V Vm'lerini (VMM yönetilen) çoğaltma Azure için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="37f62-107">Network mapping is used when replicating Hyper-V VMs (managed in VMM) to Azure.</span></span> <span data-ttu-id="37f62-108">Bir kaynak VMM sunucusunda VM ağları arasındaki eşlemeyi eşlemeleri ağ ve hedef Azure ağları.</span><span class="sxs-lookup"><span data-stu-id="37f62-108">Network mapping maps between VM networks on a source VMM server, and target Azure networks.</span></span> <span data-ttu-id="37f62-109">Eşleme şunları yapar:</span><span class="sxs-lookup"><span data-stu-id="37f62-109">Mapping does the following:</span></span>

- <span data-ttu-id="37f62-110">**Ağ bağlantısı**— yük devretme sonrasında, tüm çoğaltılan Azure Vm'lerinin eşlenen Azure ağına bağlanır.</span><span class="sxs-lookup"><span data-stu-id="37f62-110">**Network connection**—After failover, all replicated Azure VMs are connected to the mapped Azure network.</span></span> <span data-ttu-id="37f62-111">Bunlar farklı kurtarma planları devredilir olsa bile aynı ağda yük devri tüm makineler birbirine bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="37f62-111">All machines which fail over on the same network can connect to each other, even if they failed over in different recovery plans.</span></span>
- <span data-ttu-id="37f62-112">**Ağ geçidi**— bir ağ geçidi hedef Azure ağında ayarlanıp ayarlanmadığını VM'ler üzerinde premised eşlenen ağ diğer şirket içi sanal makinelere bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="37f62-112">**Network gateway**—If a network gateway is set up on the target Azure network, VMs can connect to other on-premises virtual machines in the mapped on-premised network.</span></span>

### <a name="prepare-vmm-for-network-mapping"></a><span data-ttu-id="37f62-113">VMM ağ eşlemesi için hazırlanma</span><span class="sxs-lookup"><span data-stu-id="37f62-113">Prepare VMM for network mapping</span></span>

<span data-ttu-id="37f62-114">VMM, ağ eşlemesi için aşağıdaki gibi hazırlayın:</span><span class="sxs-lookup"><span data-stu-id="37f62-114">Prepare VMM for network mapping as follows:</span></span>

1. <span data-ttu-id="37f62-115">Yoksa, hazırlama bir [VMM mantıksal ağı](https://docs.microsoft.com/system-center/vmm/network-logical) , Hyper-V konaklarının bulunduğu bulutla ilişkili.</span><span class="sxs-lookup"><span data-stu-id="37f62-115">If you don't have one, prepare a [VMM logical network](https://docs.microsoft.com/system-center/vmm/network-logical) that's associated with the cloud in which the Hyper-V hosts are located.</span></span>
2. <span data-ttu-id="37f62-116">Yoksa, oluşturulan bir [VM ağı](https://docs.microsoft.com/system-center/vmm/network-virtual) üzerinde hazırlanmış mantıksal ağ ile bağlantılı.</span><span class="sxs-lookup"><span data-stu-id="37f62-116">If you don't have one, created a [VM network](https://docs.microsoft.com/system-center/vmm/network-virtual) linked to the logical network you prepared above.</span></span>
3. <span data-ttu-id="37f62-117">Sanal makineleri Hyper-V konak kümesinde sunucu/VMM bulutta VM ağına bağlayın.</span><span class="sxs-lookup"><span data-stu-id="37f62-117">Connect VMs on the Hyper-V host server/cluster in the VMM cloud, to the VM network.</span></span>

 
<span data-ttu-id="37f62-118">Şunlara dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="37f62-118">Note that:</span></span> 
- <span data-ttu-id="37f62-119">Kaynak VM ağı'na yeni VM'ler eklendiğinde Çoğaltma gerçekleştiğinde eşlenen Azure ağına bağlanır.</span><span class="sxs-lookup"><span data-stu-id="37f62-119">New VMs are added to the source VM network are connected to the mapped Azure network when replication occurs.</span></span>
- <span data-ttu-id="37f62-120">Hedef ağın birden çok alt ağı varsa ve bu alt ağlardan biri kaynak sanal makinenin bulunduğu alt ağ ile aynı adı taşıyorsa, çoğaltılan sanal makine yük devretme işleminin ardından hedef alt ağa bağlanır.</span><span class="sxs-lookup"><span data-stu-id="37f62-120">If the target network has multiple subnets, and one of those subnets has the same name as subnet on which the source virtual machine is located, then the replica virtual machine connects to that target subnet after failover.</span></span>
- <span data-ttu-id="37f62-121">Eşleşen ada sahip bir hedef alt ağ yoksa sanal makine ağdaki ilk alt ağa bağlanır.</span><span class="sxs-lookup"><span data-stu-id="37f62-121">If there’s no target subnet with a matching name, the virtual machine connects to the first subnet in the network.</span></span>
- <span data-ttu-id="37f62-122">Bir Azure ağı hazırlamak ve bu senaryoyu dağıtmak gibi ağ eşlemeleri ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="37f62-122">You prepare an Azure network, and set up network mappings, as you deploy the scenario.</span></span>

## <a name="connecting-to-azure-vms-after-failover"></a><span data-ttu-id="37f62-123">Yük devretme sonrasında Azure Vm'lerinin bağlanma</span><span class="sxs-lookup"><span data-stu-id="37f62-123">Connecting to Azure VMs after failover</span></span>

<span data-ttu-id="37f62-124">Çoğaltma ve yük devretme stratejinizi planlarken, önemli sorular yük devretme sonrasında Azure VM'ye bağlanma biridir.</span><span class="sxs-lookup"><span data-stu-id="37f62-124">When planning your replication and failover strategy, one of the key questions is how to connect to the Azure VM after failover.</span></span> <span data-ttu-id="37f62-125">Çoğaltma Azure VM'ler için ağ stratejinizi tasarlarken, birkaç seçeneğiniz vardır:</span><span class="sxs-lookup"><span data-stu-id="37f62-125">There are a couple of choices when designing your network strategy for replica Azure VMs:</span></span>

- <span data-ttu-id="37f62-126">**Farklı bir IP adresi kullanmak**: çoğaltılan Azure VM ağı için farklı bir IP adresi aralığı kullanmayı seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="37f62-126">**Use a different IP address**: You can select to use a different IP address range for the replicated Azure VM network.</span></span> <span data-ttu-id="37f62-127">Bu senaryoda VM yük devretme sonrasında yeni bir IP adresi alır ve DNS güncelleştirme gereklidir.</span><span class="sxs-lookup"><span data-stu-id="37f62-127">In this scenario the VM gets a new IP address after failover, and a DNS update is required.</span></span>
- <span data-ttu-id="37f62-128">**Aynı IP adresini korumak**: aynı IP adresi aralığı olarak birincil şirket içi ağınızda yük devretme sonrasında Azure ağı için kullanmak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="37f62-128">**Retain the same IP address**: You might want to use the same IP address range as that in your primary on-premises network, for the Azure network after failover.</span></span>  <span data-ttu-id="37f62-129">Tutma aynı IP adreslerini basitleştirir kurtarma azaltarak ağ ile ilgili sorunları yük devretme sonrasında.</span><span class="sxs-lookup"><span data-stu-id="37f62-129">Keeping the same IP addresses simplifies the recovery by reducing network related issues after failover.</span></span> <span data-ttu-id="37f62-130">Ancak, Azure'a çoğaltma yapıyorsanız, yolları yeni konumunu IP adresleri ile yük devretme sonrasında güncelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="37f62-130">However, when you're replicating to Azure, you will need to update routes with the new location of the IP addresses after failover.</span></span>


## <a name="retain-ip-addresses"></a><span data-ttu-id="37f62-131">IP adreslerini korur</span><span class="sxs-lookup"><span data-stu-id="37f62-131">Retain IP addresses</span></span>

<span data-ttu-id="37f62-132">Site Recovery sabit IP korumak özelliği üzerinden Azure için bir alt ağ yük devretme kümelemesiyle başarısız olduğunda adresleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="37f62-132">Site Recovery provides the capability to retain fixed IP addresses when failing over to Azure, with a subnet failover.</span></span>

<span data-ttu-id="37f62-133">Alt ağ yük devretmesi ile belirli bir alt aynı anda Site 1 veya her iki sitede ancak hiçbir Site 2 konumunda bulunur.</span><span class="sxs-lookup"><span data-stu-id="37f62-133">With subnet failover, a specific subnet is present at Site 1 or Site 2, but never at both sites simultaneously.</span></span> <span data-ttu-id="37f62-134">IP adres alanı bir yük devretme durumunda korumak için program aracılığıyla alt ağların bir siteden diğerine taşımak yönlendirici altyapı düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="37f62-134">In order to maintain the IP address space in the event of a failover, you programmatically arrange for the router infrastructure to move the subnets from one site to another.</span></span> <span data-ttu-id="37f62-135">Yük devretme sırasında alt ağlar ile ilişkili korumalı sanal makineleri taşıyın.</span><span class="sxs-lookup"><span data-stu-id="37f62-135">During failover, the subnets move with the associated protected VMs.</span></span> <span data-ttu-id="37f62-136">Bir arıza olması durumunda olan asıl sakıncası, tüm alt ağı taşımanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="37f62-136">The main drawback is that in the event of a failure, you have to move the whole subnet.</span></span>



### <a name="failover-example"></a><span data-ttu-id="37f62-137">Yük devretme örneği</span><span class="sxs-lookup"><span data-stu-id="37f62-137">Failover example</span></span>

<span data-ttu-id="37f62-138">Azure'a yük devretme için bir örneğe bakalım.</span><span class="sxs-lookup"><span data-stu-id="37f62-138">Let's look at an example for failover to Azure.</span></span>

- <span data-ttu-id="37f62-139">Ficticious şirket, Woodgrove Bank, iş uygulamalarını barındıran bir şirket içi altyapı sahiptir.</span><span class="sxs-lookup"><span data-stu-id="37f62-139">A ficticious company, Woodgrove Bank, has an on-premises infrastructure hosting their business apps.</span></span> <span data-ttu-id="37f62-140">Kullanıcıların mobil uygulamalar Azure üzerinde barındırılır.</span><span class="sxs-lookup"><span data-stu-id="37f62-140">Their mobile applications are hosted on Azure.</span></span>
- <span data-ttu-id="37f62-141">Azure ve şirket içi sunucularda Woodgrove Bank VMs arasındaki bağlantıyı, şirket içi uç ağ ve Azure sanal ağı arasında bir siteden siteye (VPN) bağlantısı tarafından sağlanır.</span><span class="sxs-lookup"><span data-stu-id="37f62-141">Connectivity between Woodgrove Bank VMs in Azure and on-premises servers is provided by a site-to-site (VPN) connection between the on-premises edge network and the Azure virtual network.</span></span>
- <span data-ttu-id="37f62-142">Bu VPN Azure sanal ağında şirketin kendi şirket içi ağ bir uzantısı olarak görüneceği anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="37f62-142">This VPN means that the company's virtual network in Azure appears as an extension of their on-premises network.</span></span>
- <span data-ttu-id="37f62-143">Woodgrove şirket içi iş yüklerini Azure'a çoğaltmak için Site Recovery kullanmak istiyor.</span><span class="sxs-lookup"><span data-stu-id="37f62-143">Woodgrove wants to use Site Recovery to replicate on-premises workloads to Azure.</span></span>
 - <span data-ttu-id="37f62-144">Uygulamalar ve IP adreslerini sabit kodlanmış bağlıdır ve bu nedenle Azure için yük devretme sonrasında uygulamaları için IP adreslerini bekletmeniz gerekir yapılandırmalarını uğraşmanız Woodgrove sahiptir.</span><span class="sxs-lookup"><span data-stu-id="37f62-144">Woodgrove has to deal with applications and configurations which depend on hard-coded IP addresses, and thus need to retain IP addresses for their applications after failover to Azure.</span></span>
 - <span data-ttu-id="37f62-145">Woodgrove atanmış IP adresleri aralığı 172.16.1.0/24, Azure'da çalışan kendi kaynaklarına 172.16.2.0/24 gelen.</span><span class="sxs-lookup"><span data-stu-id="37f62-145">Woodgrove has assigned IP addresses from range 172.16.1.0/24, 172.16.2.0/24 to its resources running in Azure.</span></span>


<span data-ttu-id="37f62-146">Woodgrove olması için IP adresleri, burada 's ne korurken Vm'lerini Azure'a çoğaltmak için şirket yapması gerekir:</span><span class="sxs-lookup"><span data-stu-id="37f62-146">For Woodgrove to be able to replicate its VMs to Azure while retaining the IP addresses, here's what the company needs to do:</span></span>

1. <span data-ttu-id="37f62-147">Bir Azure sanal ağı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="37f62-147">Create an Azure virtual network.</span></span> <span data-ttu-id="37f62-148">Böylece uygulamaları sorunsuz bir şekilde yük devredebildiğini şirket içi ağ uzantısı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="37f62-148">It should be an extension of the on-premises network, so that applications can fail over seamlessly.</span></span>
2. <span data-ttu-id="37f62-149">Azure siteden siteye VPN bağlantısı, Azure üzerinde oluşturulan sanal ağlar için noktadan siteye bağlantı yanı sıra eklemenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="37f62-149">Azure allows you to add site-to-site VPN connectivity, in addition to point-to-site connectivity to the virtual networks created in Azure.</span></span>
3. <span data-ttu-id="37f62-150">Yalnızca şirket içi IP adres aralığından IP adresi aralığı farklıysa Azure ağında siteden siteye bağlantı kurarken şirket içi konumuna (yerel ağ) trafiği yönlendirebilir.</span><span class="sxs-lookup"><span data-stu-id="37f62-150">When setting up the site-to-site connection, in the Azure network, you can route traffic to the on-premises location (local-network) only if the IP address range is different from the on-premises IP address range.</span></span>
    - <span data-ttu-id="37f62-151">Azure esnetilen alt ağları desteklemiyor olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="37f62-151">This is because Azure doesn’t support stretched subnets.</span></span> <span data-ttu-id="37f62-152">Bu nedenle alt 192.168.1.0/24 şirket içi varsa, Azure ağında bir yerel ağ 192.168.1.0/24 ekleyemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="37f62-152">So if you have subnet 192.168.1.0/24 on-premises, you can’t add a local-network 192.168.1.0/24 in the Azure network.</span></span>
    - <span data-ttu-id="37f62-153">Azure alt ağda etkin VM yok ve yalnızca olağanüstü durum kurtarma için alt ağ oluşturulmaktadır bilmiyor çünkü bu beklenir.</span><span class="sxs-lookup"><span data-stu-id="37f62-153">This is expected because Azure doesn’t know that there are no active VMs in the subnet, and that the subnet is being created for disaster recovery only.</span></span>
    - <span data-ttu-id="37f62-154">Doğru alt ağ ve yerel ağ çakışma dpm'nin bir Azure ağı dışında ağ trafiğini yönlendirmek için.</span><span class="sxs-lookup"><span data-stu-id="37f62-154">To be able to correctly route network traffic out of an Azure network the subnets in the network and the local-network mustn't conflict.</span></span>

![Alt ağ yük devretme önce](./media/vmm-to-azure-walkthrough-network/network-design7.png)

### <a name="before-failover"></a><span data-ttu-id="37f62-156">Önce yük devretme</span><span class="sxs-lookup"><span data-stu-id="37f62-156">Before failover</span></span>

1. <span data-ttu-id="37f62-157">Ek bir ağa (örneğin kurtarma ağ) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="37f62-157">Create an additional network (for example Recovery Network).</span></span> <span data-ttu-id="37f62-158">Bu ağdır VM'ler başarısız olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="37f62-158">This is the network in which failed over VMs are created.</span></span>
2. <span data-ttu-id="37f62-159">Bir VM için IP adresi VM Özellikleri'nde, yük devretme sonrasında korunur emin olmak için > **yapılandırma**VM içi sahip aynı IP adresi belirtin ve tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="37f62-159">To ensure that the IP address for a VM is retained after a failover, in the VM properties > **Configure**, specify the same IP address that the VM has on-premises, and click **Save**.</span></span>
3. <span data-ttu-id="37f62-160">VM üzerinden başarısız olduğunda, Azure Site Recovery için sağlanan IP adresi atar.</span><span class="sxs-lookup"><span data-stu-id="37f62-160">When the VM is failed over, Azure Site Recovery will assign the provided IP address to it.</span></span>

    ![Ağ Özellikleri](./media/vmm-to-azure-walkthrough-network/network-design8.png)

4. <span data-ttu-id="37f62-162">Yük devretme tetikleyici tetiklenir ve gerekli IP adresi ile oluşturulan sanal makineleri Azure içinde olduktan sonra ağ kullanmaya bağlanabilir bir [Vnet vonnection Vnet'e](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).</span><span class="sxs-lookup"><span data-stu-id="37f62-162">After failover is trigger is triggered, and the VMs are created in Azure with the required IP address, you can connect to the network using a [Vnet to Vnet vonnection](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).</span></span> <span data-ttu-id="37f62-163">Bu eylem betiği yazılabilir.</span><span class="sxs-lookup"><span data-stu-id="37f62-163">This action can be scripted.</span></span>
5. <span data-ttu-id="37f62-164">Yollar uygun şekilde değiştirilmesi, bu 192.168.1.0/24 artık Azure'a taşındı yansıtacak şekilde gerekir.</span><span class="sxs-lookup"><span data-stu-id="37f62-164">Routes need to be appropriately modified, to reflect that 192.168.1.0/24 has now moved to Azure.</span></span>

    ![Alt ağ yük devretme sonrasında](./media/vmm-to-azure-walkthrough-network/network-design9.png)

### <a name="after-failover"></a><span data-ttu-id="37f62-166">Yük devretme sonrasında</span><span class="sxs-lookup"><span data-stu-id="37f62-166">After failover</span></span>

<span data-ttu-id="37f62-167">Yukarıda gösterildiği gibi bir Azure ağı yoksa, failvoer sonra birincil site ile Azure arasında siteden siteye VPN bağlantısı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="37f62-167">If you don't have an Azure network as illustrated above, you can create a site-to-site VPN connection between your primary site and Azure, after failvoer.</span></span>

## <a name="change-ip-addresses"></a><span data-ttu-id="37f62-168">IP adreslerini değiştirin</span><span class="sxs-lookup"><span data-stu-id="37f62-168">Change IP addresses</span></span>

<span data-ttu-id="37f62-169">Bu [blog gönderisi](http://azure.microsoft.com/blog/2014/09/04/networking-infrastructure-setup-for-microsoft-azure-as-a-disaster-recovery-site/) IP adreslerini yük devretme sonrasında korumak gerekmediğinde Azure ağ altyapısını ayarlamak açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="37f62-169">This [blog post](http://azure.microsoft.com/blog/2014/09/04/networking-infrastructure-setup-for-microsoft-azure-as-a-disaster-recovery-site/) explains how to set up the Azure networking infrastructure when you don't need to retain IP addresses after failover.</span></span> <span data-ttu-id="37f62-170">Uygulama açıklaması ile başlayan, şirket içi ağ yukarı ve Azure nasıl ayarlanacağını bakar ve yük devretme işlemleri çalıştırma hakkında bilgi ile sonlanır.</span><span class="sxs-lookup"><span data-stu-id="37f62-170">It starts with an application description, looks at how to set up networking on-premises and in Azure, and concludes with information about running failovers.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="37f62-171">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="37f62-171">Next steps</span></span>

<span data-ttu-id="37f62-172">Git [5. adım: Azure hazırlama](vmm-to-azure-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="37f62-172">Go to [Step 5: Prepare Azure](vmm-to-azure-walkthrough-prepare-azure.md)</span></span>
