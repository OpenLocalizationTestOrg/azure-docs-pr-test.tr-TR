---
title: "Ağ eşlemesi Site Recovery ile Hyper-V VM çoğaltması için planlama | Microsoft Docs"
description: "Hyper-V sanal makine çoğaltmasını bir şirket içi veri merkezi Azure'a veya ikincil bir site için Ağ eşlemesi ayarlayın."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: tysonn
ms.assetid: fcaa2f52-489d-4c1c-865f-9e78e000b351
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/23/2017
ms.author: raynew
ms.openlocfilehash: b1b8b1ebc013a5dfb69528f9353369e18f84e61f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="plan-network-mapping-for-hyper-v-vm-replication-with-site-recovery"></a><span data-ttu-id="a66ac-103">Ağ eşlemesi Site Recovery ile Hyper-V VM çoğaltması için planlama</span><span class="sxs-lookup"><span data-stu-id="a66ac-103">Plan network mapping for Hyper-V VM replication with Site Recovery</span></span>



<span data-ttu-id="a66ac-104">Bu makalede anlamak ve Hyper-V Vm'lerini azure'a veya ikincil bir siteye çoğaltma sırasında eşleme, kullanarak ağ için planlama yardımcı olacak [Azure Site Recovery hizmeti](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a66ac-104">This article helps you to understand and plan for network mapping during replication of Hyper-V VMs to Azure, or to a secondary site, using the [Azure Site Recovery service](site-recovery-overview.md).</span></span>

<span data-ttu-id="a66ac-105">Okuma sonra bu makalede bu makalenin sonundaki yorumları gönderin ya da teknik sorular [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="a66ac-105">After reading this article post any comments at the bottom of this article, or ask technical questions on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="network-mapping-for-replication-to-azure"></a><span data-ttu-id="a66ac-106">Azure'a çoğaltma için Ağ eşlemesi</span><span class="sxs-lookup"><span data-stu-id="a66ac-106">Network mapping for replication to Azure</span></span>

<span data-ttu-id="a66ac-107">Ağ eşlemesi Hyper-V Vm'lerini (VMM yönetilen) çoğaltma Azure için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a66ac-107">Network mapping is used when replicating Hyper-V VMs (managed in VMM) to Azure.</span></span> <span data-ttu-id="a66ac-108">Bir kaynak VMM sunucusunda VM ağları arasındaki eşlemeyi eşlemeleri ağ ve hedef Azure ağları.</span><span class="sxs-lookup"><span data-stu-id="a66ac-108">Network mapping maps between VM networks on a source VMM server, and target Azure networks.</span></span> <span data-ttu-id="a66ac-109">Eşleme şunları yapar:</span><span class="sxs-lookup"><span data-stu-id="a66ac-109">Mapping does the following:</span></span>

- <span data-ttu-id="a66ac-110">**Ağ bağlantısı**— çoğaltılan Azure Vm'lerinin eşlenen ağa bağlanmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="a66ac-110">**Network connection**—Ensures that replicated Azure VMs are connected to the mapped network.</span></span> <span data-ttu-id="a66ac-111">Bunlar farklı kurtarma planları devredilir olsa bile aynı ağda yük devri tüm makineler birbirine bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="a66ac-111">All machines which fail over on the same network can connect to each other, even if they failed over in different recovery plans.</span></span>
- <span data-ttu-id="a66ac-112">**Ağ geçidi**— bir ağ geçidi hedef Azure ağında ayarlanıp ayarlanmadığını VM'ler diğer şirket içi sanal makinelere bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="a66ac-112">**Network gateway**—If a network gateway is set up on the target Azure network, VMs can connect to other on-premises virtual machines.</span></span>

<span data-ttu-id="a66ac-113">Şunlara dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="a66ac-113">Note that:</span></span>

- <span data-ttu-id="a66ac-114">Bir Azure sanal ağı için bir kaynak VMM VM ağ eşleyin.</span><span class="sxs-lookup"><span data-stu-id="a66ac-114">You map a source VMM VM network to an Azure virtual network.</span></span>
- <span data-ttu-id="a66ac-115">Azure VM'ler kaynak yük devretme sonrasında ağ eşlenmiş hedef sanal ağa bağlanır.</span><span class="sxs-lookup"><span data-stu-id="a66ac-115">After failover Azure VMs in the source network will be connected to the mapped target virtual network.</span></span>
- <span data-ttu-id="a66ac-116">Kaynak VM ağı'na eklenen yeni VM'ler, Çoğaltma gerçekleştiğinde eşlenen Azure ağına bağlanır.</span><span class="sxs-lookup"><span data-stu-id="a66ac-116">New VMs added to the source VM network are connected to the mapped Azure network when replication occurs.</span></span>
- <span data-ttu-id="a66ac-117">Hedef ağın birden çok alt ağı varsa ve bu alt ağlardan biri kaynak sanal makinenin bulunduğu alt ağ ile aynı adı taşıyorsa, çoğaltılan sanal makine yük devretme işleminin ardından hedef alt ağa bağlanır.</span><span class="sxs-lookup"><span data-stu-id="a66ac-117">If the target network has multiple subnets, and one of those subnets has the same name as subnet on which the source virtual machine is located, then the replica virtual machine connects to that target subnet after failover.</span></span>
- <span data-ttu-id="a66ac-118">Eşleşen ada sahip bir hedef alt ağ yoksa sanal makine ağdaki ilk alt ağa bağlanır.</span><span class="sxs-lookup"><span data-stu-id="a66ac-118">If there’s no target subnet with a matching name, the virtual machine connects to the first subnet in the network.</span></span>


## <a name="network-mapping-for-replication-to-a-secondary-datacenter"></a><span data-ttu-id="a66ac-119">Ağ eşlemesi için ikincil veri merkezine çoğaltma</span><span class="sxs-lookup"><span data-stu-id="a66ac-119">Network mapping for replication to a secondary datacenter</span></span>

<span data-ttu-id="a66ac-120">Ağ eşleme (System Center Virtual Machine Manager (VMM) yönetilen) Hyper-V Vm'lerini ikincil bir veri merkezine çoğaltma yapılırken kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a66ac-120">Network mapping is used when replicating Hyper-V VMs (managed in System Center Virtual Machine Manager (VMM)) to a secondary datacenter.</span></span> <span data-ttu-id="a66ac-121">Bir kaynak VMM sunucusunda VM ağları ve bir hedef VMM sunucusunda VM ağları arasında ağ eşlemesi eşler.</span><span class="sxs-lookup"><span data-stu-id="a66ac-121">Network mapping maps between VM networks on a source VMM server, and VM networks on a target VMM server.</span></span> <span data-ttu-id="a66ac-122">Eşleme şunları yapar:</span><span class="sxs-lookup"><span data-stu-id="a66ac-122">Mapping does the following:</span></span>

- <span data-ttu-id="a66ac-123">**Ağ bağlantısı**— VM'ler yük devretme sonrasında uygun ağlara bağlanır.</span><span class="sxs-lookup"><span data-stu-id="a66ac-123">**Network connection**—Connects VMs to appropriate networks after failover.</span></span> <span data-ttu-id="a66ac-124">Çoğaltma VM kaynak ağa eşlenmiş hedef ağa bağlanır.</span><span class="sxs-lookup"><span data-stu-id="a66ac-124">The replica VM will be connected to the target network that's mapped to the source network.</span></span>
- <span data-ttu-id="a66ac-125">**En iyi yerleştirme**— çoğalma VM'ler Hyper-V ana bilgisayar sunucuları üzerinde en iyi şekilde yerleştirir.</span><span class="sxs-lookup"><span data-stu-id="a66ac-125">**Optimal placement**—Optimally places the replica VMs on Hyper-V host servers.</span></span> <span data-ttu-id="a66ac-126">Çoğaltma sanal makineleri, eşlenen VM ağlarına erişebilen Konaklara yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="a66ac-126">Replica VMs are placed on hosts that can access the mapped VM networks.</span></span>
- <span data-ttu-id="a66ac-127">**Ağ eşleme**— ağ eşlemesini yapılandırmazsanız, çoğaltma sanal makineleri herhangi bir VM ağına yük devretme sonrasında bağlanmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="a66ac-127">**No network mapping**—If you don’t configure network mapping, replica VMs won’t be connected to any VM networks after failover.</span></span>

<span data-ttu-id="a66ac-128">Şunlara dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="a66ac-128">Note that:</span></span>

- <span data-ttu-id="a66ac-129">İki VMM sunucusu veya iki site aynı sunucu tarafından yönetiliyorsa tek bir VMM sunucusunda VM ağları arasında ağ eşlemesi yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="a66ac-129">Network mapping can be configured between VM networks on two VMM servers, or on a single VMM server if two sites are managed by the same server.</span></span>
- <span data-ttu-id="a66ac-130">Ne zaman eşleme doğru bir şekilde yapılandırıldığından ve çoğaltma etkinleştirilmiş VM birincil konumda bir ağa bağlı olması ve onun çoğaltması hedef konumda eşlenen ağa bağlanır.</span><span class="sxs-lookup"><span data-stu-id="a66ac-130">When mapping is configured correctly and replication is enabled, a VM at the primary location will be connected to a network, and its replica at the target location will be connected to its mapped network.</span></span>
-
- <span data-ttu-id="a66ac-131">Bir hedef VM ağı sırasında ağ eşlemesini seçtiğinizde ağlar doğru VMM'de ayarlanan, kaynak VM ağı kullanan VMM kaynak Bulutları, koruma için kullanılan hedef bulut kullanılabilir hedef VM ağlarında birlikte görüntülenir .</span><span class="sxs-lookup"><span data-stu-id="a66ac-131">If networks have been set up correctly in VMM, when you select a target VM network during network mapping, the VMM source clouds that use the source VM network will be displayed, along with the available target VM networks on the target clouds that are used for protection.</span></span>
- <span data-ttu-id="a66ac-132">Hedef ağın birden çok alt ağı varsa ve bu alt ağlardan biri kaynak sanal makinenin bulunduğu alt ağ ile aynı ada sahip, ardından çoğaltma sanal makinesi yük devretme işleminden sonra hedef alt ağa bağlanır.</span><span class="sxs-lookup"><span data-stu-id="a66ac-132">If the target network has multiple subnets and one of those subnets has the same name as the subnet on which the source virtual machine is located, then the replica virtual machine will be connected to that target subnet after failover.</span></span> <span data-ttu-id="a66ac-133">Eşleşen ada sahip bir hedef alt ağ yoksa sanal makine ağdaki ilk alt ağa bağlanır.</span><span class="sxs-lookup"><span data-stu-id="a66ac-133">If there’s no target subnet with a matching name, the virtual machine will be connected to the first subnet in the network.</span></span>



### <a name="example"></a><span data-ttu-id="a66ac-134">Örnek</span><span class="sxs-lookup"><span data-stu-id="a66ac-134">Example</span></span>

<span data-ttu-id="a66ac-135">Burada, bu mekanizma göstermek için bir örnek verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="a66ac-135">Here’s an example to illustrate this mechanism.</span></span> <span data-ttu-id="a66ac-136">New York ve Şikago iki konumda bulunduğu bir kuruluşta atalım.</span><span class="sxs-lookup"><span data-stu-id="a66ac-136">Let’s take an organization with two locations in New York and Chicago.</span></span>

<span data-ttu-id="a66ac-137">**Konum**</span><span class="sxs-lookup"><span data-stu-id="a66ac-137">**Location**</span></span> | <span data-ttu-id="a66ac-138">**VMM sunucusu**</span><span class="sxs-lookup"><span data-stu-id="a66ac-138">**VMM server**</span></span> | <span data-ttu-id="a66ac-139">**VM ağları**</span><span class="sxs-lookup"><span data-stu-id="a66ac-139">**VM networks**</span></span> | <span data-ttu-id="a66ac-140">**Eşlenen**</span><span class="sxs-lookup"><span data-stu-id="a66ac-140">**Mapped to**</span></span>
---|---|---|---
<span data-ttu-id="a66ac-141">New York</span><span class="sxs-lookup"><span data-stu-id="a66ac-141">New York</span></span> | <span data-ttu-id="a66ac-142">VMM NewYork</span><span class="sxs-lookup"><span data-stu-id="a66ac-142">VMM-NewYork</span></span>| <span data-ttu-id="a66ac-143">VMNetwork1 NewYork</span><span class="sxs-lookup"><span data-stu-id="a66ac-143">VMNetwork1-NewYork</span></span> | <span data-ttu-id="a66ac-144">VMNetwork1 Şikago'eşlenmiş</span><span class="sxs-lookup"><span data-stu-id="a66ac-144">Mapped to VMNetwork1-Chicago</span></span>
 |  | <span data-ttu-id="a66ac-145">VMNetwork2 NewYork</span><span class="sxs-lookup"><span data-stu-id="a66ac-145">VMNetwork2-NewYork</span></span> | <span data-ttu-id="a66ac-146">Eşlenmedi</span><span class="sxs-lookup"><span data-stu-id="a66ac-146">Not mapped</span></span>
<span data-ttu-id="a66ac-147">Chicago</span><span class="sxs-lookup"><span data-stu-id="a66ac-147">Chicago</span></span> | <span data-ttu-id="a66ac-148">VMM Chicago</span><span class="sxs-lookup"><span data-stu-id="a66ac-148">VMM-Chicago</span></span>| <span data-ttu-id="a66ac-149">VMNetwork1 Chicago</span><span class="sxs-lookup"><span data-stu-id="a66ac-149">VMNetwork1-Chicago</span></span> | <span data-ttu-id="a66ac-150">VMNetwork1-NewYork eşlenmiş</span><span class="sxs-lookup"><span data-stu-id="a66ac-150">Mapped to VMNetwork1-NewYork</span></span>
 | | <span data-ttu-id="a66ac-151">VMNetwork1 Chicago</span><span class="sxs-lookup"><span data-stu-id="a66ac-151">VMNetwork1-Chicago</span></span> | <span data-ttu-id="a66ac-152">Eşlenmedi</span><span class="sxs-lookup"><span data-stu-id="a66ac-152">Not mapped</span></span>

<span data-ttu-id="a66ac-153">Bu örnekte:</span><span class="sxs-lookup"><span data-stu-id="a66ac-153">In this example:</span></span>

- <span data-ttu-id="a66ac-154">Bir çoğaltma sanal makinesi için VMNetwork1-NewYork bağlı herhangi bir sanal makine oluşturulduğunda, VMNetwork1 Şikago'bağlanır.</span><span class="sxs-lookup"><span data-stu-id="a66ac-154">When a replica virtual machine is created for any virtual machine that is connected to VMNetwork1-NewYork, it will be connected to VMNetwork1-Chicago.</span></span>
- <span data-ttu-id="a66ac-155">Bir çoğaltma sanal makinesi VMNetwork2 NewYork veya VMNetwork2 Chicago oluşturulduğunda, herhangi bir ağa bağlı.</span><span class="sxs-lookup"><span data-stu-id="a66ac-155">When a replica virtual machine is created for VMNetwork2-NewYork or VMNetwork2-Chicago, it will not be connected to any network.</span></span>

<span data-ttu-id="a66ac-156">İşte nasıl VMM Bulutları bizim örnek kuruluş ve bulutlarıyla ilişkili mantıksal ağlar olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="a66ac-156">Here's how VMM clouds are set up in our example organization, and the logical networks associated with the clouds.</span></span>

#### <a name="cloud-protection-settings"></a><span data-ttu-id="a66ac-157">Bulut koruma ayarlarını</span><span class="sxs-lookup"><span data-stu-id="a66ac-157">Cloud protection settings</span></span>

<span data-ttu-id="a66ac-158">**Korumalı bulut**</span><span class="sxs-lookup"><span data-stu-id="a66ac-158">**Protected cloud**</span></span> | <span data-ttu-id="a66ac-159">**Bulut koruma**</span><span class="sxs-lookup"><span data-stu-id="a66ac-159">**Protecting cloud**</span></span> | <span data-ttu-id="a66ac-160">**Mantıksal ağ (New York)**</span><span class="sxs-lookup"><span data-stu-id="a66ac-160">**Logical network (New York)**</span></span>  
---|---|---
<span data-ttu-id="a66ac-161">GoldCloud1</span><span class="sxs-lookup"><span data-stu-id="a66ac-161">GoldCloud1</span></span> | <span data-ttu-id="a66ac-162">GoldCloud2</span><span class="sxs-lookup"><span data-stu-id="a66ac-162">GoldCloud2</span></span> |
<span data-ttu-id="a66ac-163">SilverCloud1</span><span class="sxs-lookup"><span data-stu-id="a66ac-163">SilverCloud1</span></span>| <span data-ttu-id="a66ac-164">SilverCloud2</span><span class="sxs-lookup"><span data-stu-id="a66ac-164">SilverCloud2</span></span> |
<span data-ttu-id="a66ac-165">GoldCloud2</span><span class="sxs-lookup"><span data-stu-id="a66ac-165">GoldCloud2</span></span> | <p><span data-ttu-id="a66ac-166">NA</span><span class="sxs-lookup"><span data-stu-id="a66ac-166">NA</span></span></p><p></p> | <p><span data-ttu-id="a66ac-167">LogicalNetwork1 NewYork</span><span class="sxs-lookup"><span data-stu-id="a66ac-167">LogicalNetwork1-NewYork</span></span></p><p><span data-ttu-id="a66ac-168">LogicalNetwork1 Chicago</span><span class="sxs-lookup"><span data-stu-id="a66ac-168">LogicalNetwork1-Chicago</span></span></p>
<span data-ttu-id="a66ac-169">SilverCloud2</span><span class="sxs-lookup"><span data-stu-id="a66ac-169">SilverCloud2</span></span> | <p><span data-ttu-id="a66ac-170">NA</span><span class="sxs-lookup"><span data-stu-id="a66ac-170">NA</span></span></p><p></p> | <p><span data-ttu-id="a66ac-171">LogicalNetwork1 NewYork</span><span class="sxs-lookup"><span data-stu-id="a66ac-171">LogicalNetwork1-NewYork</span></span></p><p><span data-ttu-id="a66ac-172">LogicalNetwork1 Chicago</span><span class="sxs-lookup"><span data-stu-id="a66ac-172">LogicalNetwork1-Chicago</span></span></p>

#### <a name="logical-and-vm-network-settings"></a><span data-ttu-id="a66ac-173">Mantıksal ve VM ağ ayarları</span><span class="sxs-lookup"><span data-stu-id="a66ac-173">Logical and VM network settings</span></span>

<span data-ttu-id="a66ac-174">**Konum**</span><span class="sxs-lookup"><span data-stu-id="a66ac-174">**Location**</span></span> | <span data-ttu-id="a66ac-175">**Mantıksal ağ**</span><span class="sxs-lookup"><span data-stu-id="a66ac-175">**Logical network**</span></span> | <span data-ttu-id="a66ac-176">**İlişkili bir VM ağı**</span><span class="sxs-lookup"><span data-stu-id="a66ac-176">**Associated VM network**</span></span>
---|---|---
<span data-ttu-id="a66ac-177">New York</span><span class="sxs-lookup"><span data-stu-id="a66ac-177">New York</span></span> | <span data-ttu-id="a66ac-178">LogicalNetwork1 NewYork</span><span class="sxs-lookup"><span data-stu-id="a66ac-178">LogicalNetwork1-NewYork</span></span> | <span data-ttu-id="a66ac-179">VMNetwork1 NewYork</span><span class="sxs-lookup"><span data-stu-id="a66ac-179">VMNetwork1-NewYork</span></span>
<span data-ttu-id="a66ac-180">Chicago</span><span class="sxs-lookup"><span data-stu-id="a66ac-180">Chicago</span></span> | <span data-ttu-id="a66ac-181">LogicalNetwork1 Chicago</span><span class="sxs-lookup"><span data-stu-id="a66ac-181">LogicalNetwork1-Chicago</span></span> | <span data-ttu-id="a66ac-182">VMNetwork1 Chicago</span><span class="sxs-lookup"><span data-stu-id="a66ac-182">VMNetwork1-Chicago</span></span>
 | <span data-ttu-id="a66ac-183">LogicalNetwork2Chicago</span><span class="sxs-lookup"><span data-stu-id="a66ac-183">LogicalNetwork2Chicago</span></span> | <span data-ttu-id="a66ac-184">VMNetwork2 Chicago</span><span class="sxs-lookup"><span data-stu-id="a66ac-184">VMNetwork2-Chicago</span></span>

#### <a name="target-network-settings"></a><span data-ttu-id="a66ac-185">Hedef ağ ayarları</span><span class="sxs-lookup"><span data-stu-id="a66ac-185">Target network settings</span></span>

<span data-ttu-id="a66ac-186">Hedef VM ağ seçeneğini belirlediğinizde bu ayarları temel alarak, aşağıdaki tabloda kullanılabilir seçenekler gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="a66ac-186">Based on these settings, when you select the target VM network, the following table shows the choices that will be available.</span></span>

<span data-ttu-id="a66ac-187">**Seç**</span><span class="sxs-lookup"><span data-stu-id="a66ac-187">**Select**</span></span> | <span data-ttu-id="a66ac-188">**Korumalı bulut**</span><span class="sxs-lookup"><span data-stu-id="a66ac-188">**Protected cloud**</span></span> | <span data-ttu-id="a66ac-189">**Bulut koruma**</span><span class="sxs-lookup"><span data-stu-id="a66ac-189">**Protecting cloud**</span></span> | <span data-ttu-id="a66ac-190">**Hedef ağ yok**</span><span class="sxs-lookup"><span data-stu-id="a66ac-190">**Target network available**</span></span>
---|---|---|---
<span data-ttu-id="a66ac-191">VMNetwork1 Chicago</span><span class="sxs-lookup"><span data-stu-id="a66ac-191">VMNetwork1-Chicago</span></span> | <span data-ttu-id="a66ac-192">SilverCloud1</span><span class="sxs-lookup"><span data-stu-id="a66ac-192">SilverCloud1</span></span> | <span data-ttu-id="a66ac-193">SilverCloud2</span><span class="sxs-lookup"><span data-stu-id="a66ac-193">SilverCloud2</span></span> | <span data-ttu-id="a66ac-194">Kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="a66ac-194">Available</span></span>
 | <span data-ttu-id="a66ac-195">GoldCloud1</span><span class="sxs-lookup"><span data-stu-id="a66ac-195">GoldCloud1</span></span> | <span data-ttu-id="a66ac-196">GoldCloud2</span><span class="sxs-lookup"><span data-stu-id="a66ac-196">GoldCloud2</span></span> | <span data-ttu-id="a66ac-197">Kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="a66ac-197">Available</span></span>
<span data-ttu-id="a66ac-198">VMNetwork2 Chicago</span><span class="sxs-lookup"><span data-stu-id="a66ac-198">VMNetwork2-Chicago</span></span> | <span data-ttu-id="a66ac-199">SilverCloud1</span><span class="sxs-lookup"><span data-stu-id="a66ac-199">SilverCloud1</span></span> | <span data-ttu-id="a66ac-200">SilverCloud2</span><span class="sxs-lookup"><span data-stu-id="a66ac-200">SilverCloud2</span></span> | <span data-ttu-id="a66ac-201">Kullanılamıyor</span><span class="sxs-lookup"><span data-stu-id="a66ac-201">Not available</span></span>
 | <span data-ttu-id="a66ac-202">GoldCloud1</span><span class="sxs-lookup"><span data-stu-id="a66ac-202">GoldCloud1</span></span> | <span data-ttu-id="a66ac-203">GoldCloud2</span><span class="sxs-lookup"><span data-stu-id="a66ac-203">GoldCloud2</span></span> | <span data-ttu-id="a66ac-204">Kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="a66ac-204">Available</span></span>


<span data-ttu-id="a66ac-205">Hedef ağın birden çok alt ağı varsa ve bu alt ağlardan biri kaynak sanal makinenin bulunduğu alt ağ ile aynı ada sahip, ardından çoğaltma sanal makinesi yük devretme işleminden sonra hedef alt ağa bağlanır.</span><span class="sxs-lookup"><span data-stu-id="a66ac-205">If the target network has multiple subnets and one of those subnets has the same name as the subnet on which the source virtual machine is located, then the replica virtual machine will be connected to that target subnet after failover.</span></span> <span data-ttu-id="a66ac-206">Eşleşen ada sahip bir hedef alt ağ yoksa sanal makine ağdaki ilk alt ağa bağlanır.</span><span class="sxs-lookup"><span data-stu-id="a66ac-206">If there’s no target subnet with a matching name, the virtual machine will be connected to the first subnet in the network.</span></span>


#### <a name="failback-behavior"></a><span data-ttu-id="a66ac-207">Yeniden çalışma davranışı</span><span class="sxs-lookup"><span data-stu-id="a66ac-207">Failback behavior</span></span>

<span data-ttu-id="a66ac-208">Yeniden çalışma (çoğaltmayı tersine çevirme) söz konusu olduğunda neler görmek için VMNetwork1 NewYork VMNetwork1-Chicago, aşağıdaki ayarlarla eşleştiğinden emin varsayalım.</span><span class="sxs-lookup"><span data-stu-id="a66ac-208">To see what happens in the case of failback (reverse replication), let’s assume that VMNetwork1-NewYork is mapped to VMNetwork1-Chicago, with the following settings.</span></span>


<span data-ttu-id="a66ac-209">**Sanal makine**</span><span class="sxs-lookup"><span data-stu-id="a66ac-209">**Virtual machine**</span></span> | <span data-ttu-id="a66ac-210">**VM ağına bağlı**</span><span class="sxs-lookup"><span data-stu-id="a66ac-210">**Connected to VM network**</span></span>
---|---
<span data-ttu-id="a66ac-211">VM1</span><span class="sxs-lookup"><span data-stu-id="a66ac-211">VM1</span></span> | <span data-ttu-id="a66ac-212">VMNetwork1 ağ</span><span class="sxs-lookup"><span data-stu-id="a66ac-212">VMNetwork1-Network</span></span>
<span data-ttu-id="a66ac-213">VM2 (VM1 çoğaltma)</span><span class="sxs-lookup"><span data-stu-id="a66ac-213">VM2 (replica of VM1)</span></span> | <span data-ttu-id="a66ac-214">VMNetwork1 Chicago</span><span class="sxs-lookup"><span data-stu-id="a66ac-214">VMNetwork1-Chicago</span></span>

<span data-ttu-id="a66ac-215">Şimdi bu ayarlarla olası senaryolar birkaç içinde neler gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="a66ac-215">With these settings, let's review what happens in a couple of possible scenarios.</span></span>

<span data-ttu-id="a66ac-216">**Senaryo**</span><span class="sxs-lookup"><span data-stu-id="a66ac-216">**Scenario**</span></span> | <span data-ttu-id="a66ac-217">**Sonucu**</span><span class="sxs-lookup"><span data-stu-id="a66ac-217">**Outcome**</span></span>
---|---
<span data-ttu-id="a66ac-218">Yük devretme işleminden sonra VM-2 Ağ özelliklerinde değişiklik.</span><span class="sxs-lookup"><span data-stu-id="a66ac-218">No change in the network properties of VM-2 after failover.</span></span> | <span data-ttu-id="a66ac-219">VM 1 kaynak ağına bağlı kalır.</span><span class="sxs-lookup"><span data-stu-id="a66ac-219">VM-1 remains connected to the source network.</span></span>
<span data-ttu-id="a66ac-220">VM-2 ağ özellikleri yük devretme işleminden sonra değiştirilir ve bağlantısı kesilir.</span><span class="sxs-lookup"><span data-stu-id="a66ac-220">Network properties of VM-2 are changed after failover and is disconnected.</span></span> | <span data-ttu-id="a66ac-221">VM 1 kesilir.</span><span class="sxs-lookup"><span data-stu-id="a66ac-221">VM-1 is disconnected.</span></span>
<span data-ttu-id="a66ac-222">VM-2 ağ özellikleri yük devretme işleminden sonra değiştirilir ve VMNetwork2 Şikago'bağlanır.</span><span class="sxs-lookup"><span data-stu-id="a66ac-222">Network properties of VM-2 are changed after failover and is connected to VMNetwork2-Chicago.</span></span> | <span data-ttu-id="a66ac-223">VMNetwork2 Chicago eşlenmediği olduysa, VM-1 kesilecektir.</span><span class="sxs-lookup"><span data-stu-id="a66ac-223">If VMNetwork2-Chicago isn’t mapped, VM-1 will be disconnected.</span></span>
<span data-ttu-id="a66ac-224">Ağ eşlemesi VMNetwork1 Chicago değiştirilir.</span><span class="sxs-lookup"><span data-stu-id="a66ac-224">Network mapping of VMNetwork1-Chicago is changed.</span></span> | <span data-ttu-id="a66ac-225">VM-1, şimdi VMNetwork1 Şikago'eşlenen ağa bağlanır.</span><span class="sxs-lookup"><span data-stu-id="a66ac-225">VM-1 will be connected to the network now mapped to VMNetwork1-Chicago.</span></span>



## <a name="next-steps"></a><span data-ttu-id="a66ac-226">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a66ac-226">Next steps</span></span>

<span data-ttu-id="a66ac-227">Hakkında bilgi edinin [ağ altyapısını planlama](site-recovery-network-design.md).</span><span class="sxs-lookup"><span data-stu-id="a66ac-227">Learn about [planning the network infrastructure](site-recovery-network-design.md).</span></span>
