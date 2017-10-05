---
title: "Hyper-V çoğaltma Azure Site Recovery ile ikincil VMM sitesi için ağ planı | Microsoft Docs"
description: "Bu makalede, Azure Site Recovery ile ikincil System Center VMM siteye Hyper-V sanal makineleri çoğaltırken ağ planlama açıklanır."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 095f2d73-994e-4fc0-96f2-e03a7d72e492
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: raynew
ms.openlocfilehash: a1f3f6e6cba074647195e2b0cbcdc7b4f3dec475
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="step-3-plan-networking-for-hyper-v-vm-replication-to-a-secondary-vmm-site"></a><span data-ttu-id="1c3bd-103">3. adım: ağ bağlantısı Hyper-V VM çoğaltma ikincil VMM sitesi için planlama</span><span class="sxs-lookup"><span data-stu-id="1c3bd-103">Step 3: Plan networking for Hyper-V VM replication to a secondary VMM site</span></span>

<span data-ttu-id="1c3bd-104">Dağıtım önkoşulları gözden geçirdikten sonra Hyper-V sanal makineleri (VM'ler) çoğaltma kullanarak bir ikincil site için System Center Virtual Machine Manager (VMM) bulutlarında yönetilen ağ planlamak için bu makaleyi okuyun [Azure Site Recovery](site-recovery-overview.md) Azure portalında.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-104">After reviewing deployment prerequisites, read this article to plan networking when replicating Hyper-V virtual machines (VMs) managed in System Center Virtual Machine Manager (VMM) clouds, to a secondary site using [Azure Site Recovery](site-recovery-overview.md) in the Azure portal.</span></span> 

<span data-ttu-id="1c3bd-105">Bu makaleyi okuduktan sonra yapmak istediğiniz tüm yorumları makalenin alt kısmında veya [Azure Kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)'nda paylaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-105">After reading this article, post any comments at the bottom, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="network-mapping-overview"></a><span data-ttu-id="1c3bd-106">Ağ eşlemesi genel bakış</span><span class="sxs-lookup"><span data-stu-id="1c3bd-106">Network mapping overview</span></span>

<span data-ttu-id="1c3bd-107">Ağ eşlemesi, Hyper-V Vm'lerini (VMM yönetilen) çoğaltırken ikincil veri merkezine için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-107">Network mapping is used when replicating Hyper-V VMs (managed in VMM) to a secondary datacenter.</span></span> <span data-ttu-id="1c3bd-108">Bir kaynak VMM sunucusunda VM ağları ve bir hedef VMM sunucusunda VM ağları arasında ağ eşlemesi eşler.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-108">Network mapping maps between VM networks on a source VMM server, and VM networks on a target VMM server.</span></span> <span data-ttu-id="1c3bd-109">Eşleme şunları yapar:</span><span class="sxs-lookup"><span data-stu-id="1c3bd-109">Mapping does the following:</span></span>

- <span data-ttu-id="1c3bd-110">**Ağ bağlantısı**— VM'ler yük devretme sonrasında uygun ağlara bağlanır.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-110">**Network connection**—Connects VMs to appropriate networks after failover.</span></span> <span data-ttu-id="1c3bd-111">Çoğaltma VM kaynak ağa eşlenmiş hedef ağa bağlanır.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-111">The replica VM will be connected to the target network that's mapped to the source network.</span></span>
- <span data-ttu-id="1c3bd-112">**En iyi yerleştirme**— çoğalma VM'ler Hyper-V ana bilgisayar sunucuları üzerinde en iyi şekilde yerleştirir.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-112">**Optimal placement**—Optimally places the replica VMs on Hyper-V host servers.</span></span> <span data-ttu-id="1c3bd-113">Çoğaltma sanal makineleri, eşlenen VM ağlarına erişebilen Konaklara yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-113">Replica VMs are placed on hosts that can access the mapped VM networks.</span></span>
- <span data-ttu-id="1c3bd-114">**Ağ eşleme**— ağ eşlemesini yapılandırmazsanız, çoğaltma sanal makineleri herhangi bir VM ağına yük devretme sonrasında bağlanmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-114">**No network mapping**—If you don’t configure network mapping, replica VMs won’t be connected to any VM networks after failover.</span></span>


### <a name="example"></a><span data-ttu-id="1c3bd-115">Örnek</span><span class="sxs-lookup"><span data-stu-id="1c3bd-115">Example</span></span>

<span data-ttu-id="1c3bd-116">Burada, bu mekanizma göstermek için bir örnek verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-116">Here’s an example to illustrate this mechanism.</span></span> <span data-ttu-id="1c3bd-117">New York ve Şikago iki konumda bulunduğu bir kuruluşta atalım.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-117">Let’s take an organization with two locations in New York and Chicago.</span></span>

<span data-ttu-id="1c3bd-118">**Konum**</span><span class="sxs-lookup"><span data-stu-id="1c3bd-118">**Location**</span></span> | <span data-ttu-id="1c3bd-119">**VMM sunucusu**</span><span class="sxs-lookup"><span data-stu-id="1c3bd-119">**VMM server**</span></span> | <span data-ttu-id="1c3bd-120">**VM ağları**</span><span class="sxs-lookup"><span data-stu-id="1c3bd-120">**VM networks**</span></span> | <span data-ttu-id="1c3bd-121">**Eşlenen**</span><span class="sxs-lookup"><span data-stu-id="1c3bd-121">**Mapped to**</span></span>
---|---|---|---
<span data-ttu-id="1c3bd-122">New York</span><span class="sxs-lookup"><span data-stu-id="1c3bd-122">New York</span></span> | <span data-ttu-id="1c3bd-123">VMM NewYork</span><span class="sxs-lookup"><span data-stu-id="1c3bd-123">VMM-NewYork</span></span>| <span data-ttu-id="1c3bd-124">VMNetwork1 NewYork</span><span class="sxs-lookup"><span data-stu-id="1c3bd-124">VMNetwork1-NewYork</span></span> | <span data-ttu-id="1c3bd-125">VMNetwork1 Şikago'eşlenmiş</span><span class="sxs-lookup"><span data-stu-id="1c3bd-125">Mapped to VMNetwork1-Chicago</span></span>
 |  | <span data-ttu-id="1c3bd-126">VMNetwork2 NewYork</span><span class="sxs-lookup"><span data-stu-id="1c3bd-126">VMNetwork2-NewYork</span></span> | <span data-ttu-id="1c3bd-127">Eşlenmedi</span><span class="sxs-lookup"><span data-stu-id="1c3bd-127">Not mapped</span></span>
<span data-ttu-id="1c3bd-128">Chicago</span><span class="sxs-lookup"><span data-stu-id="1c3bd-128">Chicago</span></span> | <span data-ttu-id="1c3bd-129">VMM Chicago</span><span class="sxs-lookup"><span data-stu-id="1c3bd-129">VMM-Chicago</span></span>| <span data-ttu-id="1c3bd-130">VMNetwork1 Chicago</span><span class="sxs-lookup"><span data-stu-id="1c3bd-130">VMNetwork1-Chicago</span></span> | <span data-ttu-id="1c3bd-131">VMNetwork1-NewYork eşlenmiş</span><span class="sxs-lookup"><span data-stu-id="1c3bd-131">Mapped to VMNetwork1-NewYork</span></span>
 | | <span data-ttu-id="1c3bd-132">VMNetwork1 Chicago</span><span class="sxs-lookup"><span data-stu-id="1c3bd-132">VMNetwork1-Chicago</span></span> | <span data-ttu-id="1c3bd-133">Eşlenmedi</span><span class="sxs-lookup"><span data-stu-id="1c3bd-133">Not mapped</span></span>

<span data-ttu-id="1c3bd-134">Bu örnekte:</span><span class="sxs-lookup"><span data-stu-id="1c3bd-134">In this example:</span></span>

- <span data-ttu-id="1c3bd-135">Bir çoğaltma sanal makinesi için VMNetwork1-NewYork bağlı herhangi bir sanal makine oluşturulduğunda, VMNetwork1 Şikago'bağlanır.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-135">When a replica virtual machine is created for any virtual machine that is connected to VMNetwork1-NewYork, it will be connected to VMNetwork1-Chicago.</span></span>
- <span data-ttu-id="1c3bd-136">Bir çoğaltma sanal makinesi VMNetwork2 NewYork veya VMNetwork2 Chicago oluşturulduğunda, herhangi bir ağa bağlı.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-136">When a replica virtual machine is created for VMNetwork2-NewYork or VMNetwork2-Chicago, it will not be connected to any network.</span></span>

<span data-ttu-id="1c3bd-137">İşte nasıl VMM Bulutları bizim örnek kuruluş ve bulutlarıyla ilişkili mantıksal ağlar olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-137">Here's how VMM clouds are set up in our example organization, and the logical networks associated with the clouds.</span></span>

#### <a name="cloud-protection-settings"></a><span data-ttu-id="1c3bd-138">Bulut koruma ayarlarını</span><span class="sxs-lookup"><span data-stu-id="1c3bd-138">Cloud protection settings</span></span>

<span data-ttu-id="1c3bd-139">**Korumalı bulut**</span><span class="sxs-lookup"><span data-stu-id="1c3bd-139">**Protected cloud**</span></span> | <span data-ttu-id="1c3bd-140">**Bulut koruma**</span><span class="sxs-lookup"><span data-stu-id="1c3bd-140">**Protecting cloud**</span></span> | <span data-ttu-id="1c3bd-141">**Mantıksal ağ (New York)**</span><span class="sxs-lookup"><span data-stu-id="1c3bd-141">**Logical network (New York)**</span></span>  
---|---|---
<span data-ttu-id="1c3bd-142">GoldCloud1</span><span class="sxs-lookup"><span data-stu-id="1c3bd-142">GoldCloud1</span></span> | <span data-ttu-id="1c3bd-143">GoldCloud2</span><span class="sxs-lookup"><span data-stu-id="1c3bd-143">GoldCloud2</span></span> |
<span data-ttu-id="1c3bd-144">SilverCloud1</span><span class="sxs-lookup"><span data-stu-id="1c3bd-144">SilverCloud1</span></span>| <span data-ttu-id="1c3bd-145">SilverCloud2</span><span class="sxs-lookup"><span data-stu-id="1c3bd-145">SilverCloud2</span></span> |
<span data-ttu-id="1c3bd-146">GoldCloud2</span><span class="sxs-lookup"><span data-stu-id="1c3bd-146">GoldCloud2</span></span> | <p><span data-ttu-id="1c3bd-147">NA</span><span class="sxs-lookup"><span data-stu-id="1c3bd-147">NA</span></span></p><p></p> | <p><span data-ttu-id="1c3bd-148">LogicalNetwork1 NewYork</span><span class="sxs-lookup"><span data-stu-id="1c3bd-148">LogicalNetwork1-NewYork</span></span></p><p><span data-ttu-id="1c3bd-149">LogicalNetwork1 Chicago</span><span class="sxs-lookup"><span data-stu-id="1c3bd-149">LogicalNetwork1-Chicago</span></span></p>
<span data-ttu-id="1c3bd-150">SilverCloud2</span><span class="sxs-lookup"><span data-stu-id="1c3bd-150">SilverCloud2</span></span> | <p><span data-ttu-id="1c3bd-151">NA</span><span class="sxs-lookup"><span data-stu-id="1c3bd-151">NA</span></span></p><p></p> | <p><span data-ttu-id="1c3bd-152">LogicalNetwork1 NewYork</span><span class="sxs-lookup"><span data-stu-id="1c3bd-152">LogicalNetwork1-NewYork</span></span></p><p><span data-ttu-id="1c3bd-153">LogicalNetwork1 Chicago</span><span class="sxs-lookup"><span data-stu-id="1c3bd-153">LogicalNetwork1-Chicago</span></span></p>

#### <a name="logical-and-vm-network-settings"></a><span data-ttu-id="1c3bd-154">Mantıksal ve VM ağ ayarları</span><span class="sxs-lookup"><span data-stu-id="1c3bd-154">Logical and VM network settings</span></span>

<span data-ttu-id="1c3bd-155">**Konum**</span><span class="sxs-lookup"><span data-stu-id="1c3bd-155">**Location**</span></span> | <span data-ttu-id="1c3bd-156">**Mantıksal ağ**</span><span class="sxs-lookup"><span data-stu-id="1c3bd-156">**Logical network**</span></span> | <span data-ttu-id="1c3bd-157">**İlişkili bir VM ağı**</span><span class="sxs-lookup"><span data-stu-id="1c3bd-157">**Associated VM network**</span></span>
---|---|---
<span data-ttu-id="1c3bd-158">New York</span><span class="sxs-lookup"><span data-stu-id="1c3bd-158">New York</span></span> | <span data-ttu-id="1c3bd-159">LogicalNetwork1 NewYork</span><span class="sxs-lookup"><span data-stu-id="1c3bd-159">LogicalNetwork1-NewYork</span></span> | <span data-ttu-id="1c3bd-160">VMNetwork1 NewYork</span><span class="sxs-lookup"><span data-stu-id="1c3bd-160">VMNetwork1-NewYork</span></span>
<span data-ttu-id="1c3bd-161">Chicago</span><span class="sxs-lookup"><span data-stu-id="1c3bd-161">Chicago</span></span> | <span data-ttu-id="1c3bd-162">LogicalNetwork1 Chicago</span><span class="sxs-lookup"><span data-stu-id="1c3bd-162">LogicalNetwork1-Chicago</span></span> | <span data-ttu-id="1c3bd-163">VMNetwork1 Chicago</span><span class="sxs-lookup"><span data-stu-id="1c3bd-163">VMNetwork1-Chicago</span></span>
 | <span data-ttu-id="1c3bd-164">LogicalNetwork2Chicago</span><span class="sxs-lookup"><span data-stu-id="1c3bd-164">LogicalNetwork2Chicago</span></span> | <span data-ttu-id="1c3bd-165">VMNetwork2 Chicago</span><span class="sxs-lookup"><span data-stu-id="1c3bd-165">VMNetwork2-Chicago</span></span>

#### <a name="target-network-settings"></a><span data-ttu-id="1c3bd-166">Hedef ağ ayarları</span><span class="sxs-lookup"><span data-stu-id="1c3bd-166">Target network settings</span></span>

<span data-ttu-id="1c3bd-167">Hedef VM ağ seçeneğini belirlediğinizde bu ayarları temel alarak, aşağıdaki tabloda kullanılabilir seçenekler gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-167">Based on these settings, when you select the target VM network, the following table shows the choices that will be available.</span></span>

<span data-ttu-id="1c3bd-168">**Seç**</span><span class="sxs-lookup"><span data-stu-id="1c3bd-168">**Select**</span></span> | <span data-ttu-id="1c3bd-169">**Korumalı bulut**</span><span class="sxs-lookup"><span data-stu-id="1c3bd-169">**Protected cloud**</span></span> | <span data-ttu-id="1c3bd-170">**Bulut koruma**</span><span class="sxs-lookup"><span data-stu-id="1c3bd-170">**Protecting cloud**</span></span> | <span data-ttu-id="1c3bd-171">**Hedef ağ yok**</span><span class="sxs-lookup"><span data-stu-id="1c3bd-171">**Target network available**</span></span>
---|---|---|---
<span data-ttu-id="1c3bd-172">VMNetwork1 Chicago</span><span class="sxs-lookup"><span data-stu-id="1c3bd-172">VMNetwork1-Chicago</span></span> | <span data-ttu-id="1c3bd-173">SilverCloud1</span><span class="sxs-lookup"><span data-stu-id="1c3bd-173">SilverCloud1</span></span> | <span data-ttu-id="1c3bd-174">SilverCloud2</span><span class="sxs-lookup"><span data-stu-id="1c3bd-174">SilverCloud2</span></span> | <span data-ttu-id="1c3bd-175">Kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="1c3bd-175">Available</span></span>
 | <span data-ttu-id="1c3bd-176">GoldCloud1</span><span class="sxs-lookup"><span data-stu-id="1c3bd-176">GoldCloud1</span></span> | <span data-ttu-id="1c3bd-177">GoldCloud2</span><span class="sxs-lookup"><span data-stu-id="1c3bd-177">GoldCloud2</span></span> | <span data-ttu-id="1c3bd-178">Kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="1c3bd-178">Available</span></span>
<span data-ttu-id="1c3bd-179">VMNetwork2 Chicago</span><span class="sxs-lookup"><span data-stu-id="1c3bd-179">VMNetwork2-Chicago</span></span> | <span data-ttu-id="1c3bd-180">SilverCloud1</span><span class="sxs-lookup"><span data-stu-id="1c3bd-180">SilverCloud1</span></span> | <span data-ttu-id="1c3bd-181">SilverCloud2</span><span class="sxs-lookup"><span data-stu-id="1c3bd-181">SilverCloud2</span></span> | <span data-ttu-id="1c3bd-182">Kullanılamıyor</span><span class="sxs-lookup"><span data-stu-id="1c3bd-182">Not available</span></span>
 | <span data-ttu-id="1c3bd-183">GoldCloud1</span><span class="sxs-lookup"><span data-stu-id="1c3bd-183">GoldCloud1</span></span> | <span data-ttu-id="1c3bd-184">GoldCloud2</span><span class="sxs-lookup"><span data-stu-id="1c3bd-184">GoldCloud2</span></span> | <span data-ttu-id="1c3bd-185">Kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="1c3bd-185">Available</span></span>


<span data-ttu-id="1c3bd-186">Hedef ağın birden çok alt ağı varsa ve bu alt ağlardan biri kaynak sanal makinenin bulunduğu alt ağ ile aynı ada sahip, ardından çoğaltma sanal makinesi yük devretme işleminden sonra hedef alt ağa bağlanır.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-186">If the target network has multiple subnets and one of those subnets has the same name as the subnet on which the source virtual machine is located, then the replica virtual machine will be connected to that target subnet after failover.</span></span> <span data-ttu-id="1c3bd-187">Eşleşen ada sahip bir hedef alt ağ yoksa sanal makine ağdaki ilk alt ağa bağlanır.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-187">If there’s no target subnet with a matching name, the virtual machine will be connected to the first subnet in the network.</span></span>


#### <a name="failback-behavior"></a><span data-ttu-id="1c3bd-188">Yeniden çalışma davranışı</span><span class="sxs-lookup"><span data-stu-id="1c3bd-188">Failback behavior</span></span>

<span data-ttu-id="1c3bd-189">Yeniden çalışma (çoğaltmayı tersine çevirme) söz konusu olduğunda neler görmek için VMNetwork1 NewYork VMNetwork1-Chicago, aşağıdaki ayarlarla eşleştiğinden emin varsayalım.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-189">To see what happens in the case of failback (reverse replication), let’s assume that VMNetwork1-NewYork is mapped to VMNetwork1-Chicago, with the following settings.</span></span>


<span data-ttu-id="1c3bd-190">**Sanal makine**</span><span class="sxs-lookup"><span data-stu-id="1c3bd-190">**Virtual machine**</span></span> | <span data-ttu-id="1c3bd-191">**VM ağına bağlı**</span><span class="sxs-lookup"><span data-stu-id="1c3bd-191">**Connected to VM network**</span></span>
---|---
<span data-ttu-id="1c3bd-192">VM1</span><span class="sxs-lookup"><span data-stu-id="1c3bd-192">VM1</span></span> | <span data-ttu-id="1c3bd-193">VMNetwork1 ağ</span><span class="sxs-lookup"><span data-stu-id="1c3bd-193">VMNetwork1-Network</span></span>
<span data-ttu-id="1c3bd-194">VM2 (VM1 çoğaltma)</span><span class="sxs-lookup"><span data-stu-id="1c3bd-194">VM2 (replica of VM1)</span></span> | <span data-ttu-id="1c3bd-195">VMNetwork1 Chicago</span><span class="sxs-lookup"><span data-stu-id="1c3bd-195">VMNetwork1-Chicago</span></span>

<span data-ttu-id="1c3bd-196">Şimdi bu ayarlarla olası senaryolar birkaç içinde neler gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-196">With these settings, let's review what happens in a couple of possible scenarios.</span></span>

<span data-ttu-id="1c3bd-197">**Senaryo**</span><span class="sxs-lookup"><span data-stu-id="1c3bd-197">**Scenario**</span></span> | <span data-ttu-id="1c3bd-198">**Sonucu**</span><span class="sxs-lookup"><span data-stu-id="1c3bd-198">**Outcome**</span></span>
---|---
<span data-ttu-id="1c3bd-199">Yük devretme işleminden sonra VM-2 Ağ özelliklerinde değişiklik.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-199">No change in the network properties of VM-2 after failover.</span></span> | <span data-ttu-id="1c3bd-200">VM 1 kaynak ağına bağlı kalır.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-200">VM-1 remains connected to the source network.</span></span>
<span data-ttu-id="1c3bd-201">VM-2 ağ özellikleri yük devretme işleminden sonra değiştirilir ve bağlantısı kesilir.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-201">Network properties of VM-2 are changed after failover and is disconnected.</span></span> | <span data-ttu-id="1c3bd-202">VM 1 kesilir.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-202">VM-1 is disconnected.</span></span>
<span data-ttu-id="1c3bd-203">VM-2 ağ özellikleri yük devretme işleminden sonra değiştirilir ve VMNetwork2 Şikago'bağlanır.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-203">Network properties of VM-2 are changed after failover and is connected to VMNetwork2-Chicago.</span></span> | <span data-ttu-id="1c3bd-204">VMNetwork2 Chicago eşlenmediği olduysa, VM-1 kesilecektir.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-204">If VMNetwork2-Chicago isn’t mapped, VM-1 will be disconnected.</span></span>
<span data-ttu-id="1c3bd-205">Ağ eşlemesi VMNetwork1 Chicago değiştirilir.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-205">Network mapping of VMNetwork1-Chicago is changed.</span></span> | <span data-ttu-id="1c3bd-206">VM-1, şimdi VMNetwork1 Şikago'eşlenen ağa bağlanır.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-206">VM-1 will be connected to the network now mapped to VMNetwork1-Chicago.</span></span>



## <a name="prepare-for-network-mapping"></a><span data-ttu-id="1c3bd-207">Ağ eşlemesi için hazırlanma</span><span class="sxs-lookup"><span data-stu-id="1c3bd-207">Prepare for network mapping</span></span>

1. <span data-ttu-id="1c3bd-208">Kaynak ve hedef VMM sunucularında kaynak ve hedef bulutlarıyla ilişkili bir mantıksal ağ olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-208">On the source and target VMM servers, you should have a logical network associated with the source and target clouds.</span></span> 
2. <span data-ttu-id="1c3bd-209">Kaynak ve hedef sunucuları, bir VM ağı mantıksal ağa bağlı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-209">In the source and target servers, you should have a VM network linked to the logical network.</span></span>
3. <span data-ttu-id="1c3bd-210">Kaynak konumun Hyper-V ana bilgisayarda sanal makineleri kaynak VM ağına bağlantılı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-210">VMs on Hyper-V hosts in the source location should be linked to the source VM network.</span></span> <span data-ttu-id="1c3bd-211">Yalnızca tek bir VMM sunucusu kullanıyorsanız, aynı sunucu üzerinde VM ağları arasındaki eşlemeyi yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-211">If you're only using a single VMM server, you can configure mapping between VM networks on the same server.</span></span>

<span data-ttu-id="1c3bd-212">Site Recovery dağıtımı sırasında ağ eşlemesini ayarladığınızda şunlar olur:</span><span class="sxs-lookup"><span data-stu-id="1c3bd-212">Here's what happens when you set up network mapping during Site Recovery deployment:</span></span>

- <span data-ttu-id="1c3bd-213">Ağ eşlemesi ayarlamanız ve bir hedef VM ağı seçtiğinizde, kaynak VM ağı kullanan VMM kaynak Bulutları, hedef bulut kullanılabilir hedef VM ağlarında birlikte görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-213">When you set up network mapping and select a target VM network, the VMM source clouds that use the source VM network will be displayed, along with the available target VM networks on the target clouds.</span></span>
- - <span data-ttu-id="1c3bd-214">Eşleme doğru bir şekilde yapılandırıldığından ve çoğaltma etkin olduğunda, bir kaynak VM kendi kaynak VM ağına bağlı olması ve onun çoğaltma hedef konumda, eşlenen VM ağına bağlı.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-214">When mapping is configured correctly and replication is enabled, a source VM will be connected to its source VM network, and its replica at the target location will be connected to its mapped VM network.</span></span>
- <span data-ttu-id="1c3bd-215">Hedef ağın birden çok alt ağı varsa ve bu alt ağlardan biri kaynak sanal makinenin bulunduğu alt ağ ile aynı ada sahip, ardından çoğaltma sanal makinesi yük devretme işleminden sonra hedef alt ağa bağlanır.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-215">If the target network has multiple subnets, and one of those subnets has the same name as the subnet on which the source virtual machine is located, then the replica virtual machine will be connected to that target subnet after failover.</span></span> <span data-ttu-id="1c3bd-216">Eşleşen ada sahip bir hedef alt ağ varsa, VM ağındaki ilk alt ağa bağlanır.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-216">If there’s no target subnet with a matching name, the VM will be connected to the first subnet in the network.</span></span>

## <a name="connect-to-vms-after-failover"></a><span data-ttu-id="1c3bd-217">VM'ler için yük devretme sonrasında Bağlan</span><span class="sxs-lookup"><span data-stu-id="1c3bd-217">Connect to VMs after failover</span></span>

<span data-ttu-id="1c3bd-218">Çoğaltma ve yük devretme stratejinizi planlarken, anahtar sorulardan biri çoğaltmaya yük devretme sonrasında bağlanmasıdır.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-218">When planning your replication and failover strategy, one of the key questions is how to connect to the replica after failover.</span></span> <span data-ttu-id="1c3bd-219">Birkaç seçeneğiniz vardır:</span><span class="sxs-lookup"><span data-stu-id="1c3bd-219">There are a couple of choices:</span></span> 

- <span data-ttu-id="1c3bd-220">**Farklı bir IP adresi kullanmak**: çoğaltılan VM için farklı bir IP adresi kullanmayı seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-220">**Use a different IP address**: You can select to use a different IP address for the replicated VM.</span></span> <span data-ttu-id="1c3bd-221">Bu senaryoda VM yük devretme sonrasında yeni bir IP adresi alır ve DNS güncelleştirme gereklidir.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-221">In this scenario the VM gets a new IP address after failover, and a DNS update is required.</span></span>
- <span data-ttu-id="1c3bd-222">**Aynı IP adresini korumak**: aynı IP adresi VM çoğaltması için kullanmak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-222">**Retain the same IP address**: You might want to use the same IP address for the replica VM.</span></span> <span data-ttu-id="1c3bd-223">Tutma aynı IP adreslerini basitleştirir kurtarma azaltarak ağ ile ilgili sorunları yük devretme sonrasında.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-223">Keeping the same IP addresses simplifies the recovery by reducing network related issues after failover.</span></span> 

## <a name="retain-ip-addresses"></a><span data-ttu-id="1c3bd-224">IP adreslerini korur</span><span class="sxs-lookup"><span data-stu-id="1c3bd-224">Retain IP addresses</span></span>

<span data-ttu-id="1c3bd-225">IP adreslerini birincil siteden ikincil siteye yük devretme sonrasında korumak istiyorsanız, tam alt ağ yük devretme işlemi gerçekleştirin ve IP adreslerini yeni konumunu belirtmek için bir yol güncelleştirmek veya alternatif Uzatılan bir alt birincil ve kurtarma siteler arasında dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-225">If you want to retain the IP addresses from the primary site after failover to the secondary site, you can do a full subnet failover, and update routes to indicate the new location of the IP addresses, or alternative deploy a stretched subnet between the primary and the recovery sites.</span></span>

### <a name="stretched-subnet"></a><span data-ttu-id="1c3bd-226">Esnetilen alt ağ</span><span class="sxs-lookup"><span data-stu-id="1c3bd-226">Stretched subnet</span></span>

<span data-ttu-id="1c3bd-227">Esnetilen bir alt ağında alt ağ aynı anda hem birincil ve ikincil sitede kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-227">In a stretched subnet, the subnet is available simultaneously in both the primary and secondary site.</span></span> <span data-ttu-id="1c3bd-228">Bir sunucu ve kendi (Katman 3) IP yapılandırmasını ikincil siteye taşırsanız, ağ trafiğini yeni konuma otomatik olarak yönlendirilecek.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-228">If you move a server and its IP (Layer 3) configuration to the secondary site, the network will route the traffic to the new location automatically.</span></span> 

<span data-ttu-id="1c3bd-229">Bir katman 2 (veri bağlantı katmanı) açısından Uzatılan bir VLAN yönetebilirsiniz ağ ekipmanları gerekir.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-229">From a Layer 2 (data link layer) perspective, you need networking equipment that can manage a stretched VLAN.</span></span> <span data-ttu-id="1c3bd-230">Buna ek olarak, VLAN yayarak olası hata etki alanı temelde tek hata noktası haline hem sitelere genişletir.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-230">In addition, by stretching the VLAN, the potential fault domain extends to both sites, essentially becoming a single point of failure.</span></span> <span data-ttu-id="1c3bd-231">Bu bir olası olmakla birlikte, bir yayın storm kullanmaya ve yalıtılmış olamaz meydana gelebilir.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-231">While this is an unlikely, it could happen that a broadcast storm started and cannot be isolated.</span></span> 


### <a name="subnet-failover"></a><span data-ttu-id="1c3bd-232">Alt ağ yük devretme</span><span class="sxs-lookup"><span data-stu-id="1c3bd-232">Subnet failover</span></span>

<span data-ttu-id="1c3bd-233">Gerçekte uzatma olmadan esnetilen alt avantajlarından yararlanabilmek için bir alt ağ yük devretme çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-233">You can run a subnet failover to obtain the benefits of the stretched subnet, without actually stretching it.</span></span> <span data-ttu-id="1c3bd-234">Bu çözümde, bir alt ağ kullanılabilir kaynak veya hedef sitede, ancak her ikisi de aynı anda.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-234">In this solution, a subnet will be available in the source or target site, but not at both simultaneously.</span></span> <span data-ttu-id="1c3bd-235">IP adres alanı bir yük devretme durumunda korumak için program aracılığıyla alt ağların bir siteden diğerine taşımak yönlendirici altyapı düzenleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-235">To maintain the IP address space in the event of a failover, you can programmatically arrange for the router infrastructure to move the subnets from one site to another.</span></span> <span data-ttu-id="1c3bd-236">Yük devretme oluştuğunda sonra alt ağlar ile ilişkili VM'ler taşıyabilir.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-236">After when failover occurs, subnets would move with the associated VMs.</span></span> <span data-ttu-id="1c3bd-237">Bir arıza olması durumunda olan asıl sakıncası, tüm alt ağı taşımanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-237">The main drawback is that in the event of a failure, you have to move the whole subnet.</span></span>

### <a name="example"></a><span data-ttu-id="1c3bd-238">Örnek</span><span class="sxs-lookup"><span data-stu-id="1c3bd-238">Example</span></span>

<span data-ttu-id="1c3bd-239">Tam alt ağ yük devretme bir örneği burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-239">Here's an example of complete subnet failover.</span></span> <span data-ttu-id="1c3bd-240">Birincil site alt 192.168.1.0/24 içinde çalışan uygulamalar vardır.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-240">The primary site has applications running in subnet 192.168.1.0/24.</span></span> <span data-ttu-id="1c3bd-241">Yük devretme, bu alt ağdaki tüm sanal makineleri ikincil siteye yük devredildi ve IP adreslerini korur.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-241">At failover, all the VMs in this subnet are failed over to the secondary site, and retain their IP addresses.</span></span> <span data-ttu-id="1c3bd-242">Yollar için alt ağ 192.168.1.0/24 ait tüm VM sanal makineler artık ikincil siteye taşınmış olgu yansıtacak şekilde değiştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-242">Routes need to be modified to reflect the fact that all the VM virtual machines belonging to subnet 192.168.1.0/24 have now moved to the secondary site.</span></span>

<span data-ttu-id="1c3bd-243">Aşağıdaki grafik önce ve yük devretme sonrasında alt ağları göster:</span><span class="sxs-lookup"><span data-stu-id="1c3bd-243">The following graphics show the subnets before and after failover:</span></span>

- <span data-ttu-id="1c3bd-244">Yük devretme önce alt 192.168.0.1/24 kaynak sitede yük devretme işleminden sonra ikincil sitede etkin hale etkindir.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-244">Before failover, subnet 192.168.0.1/24 is active on the source site, become active on the secondary site after failover.</span></span>
- <span data-ttu-id="1c3bd-245">Birincil site kurtarma sitesi, üçüncü sitesi ve birincil site ve üçüncü site ve kurtarma sitesi arasındaki yolları uygun şekilde değiştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-245">The routes between primary site and recovery site, third site and primary site, and third site and recovery site will have to be appropriately modified.</span></span>

<span data-ttu-id="1c3bd-246">**Önce yük devretme**</span><span class="sxs-lookup"><span data-stu-id="1c3bd-246">**Before failover**</span></span>

![Önce yük devretme](./media/vmm-to-vmm-walkthrough-network/network-design2.png)

<span data-ttu-id="1c3bd-248">**Yük devretme sonrasında**</span><span class="sxs-lookup"><span data-stu-id="1c3bd-248">**After failover**</span></span>

![Yük devretme sonrasında](./media/vmm-to-vmm-walkthrough-network/network-design3.png)

<span data-ttu-id="1c3bd-250">Yük devretme sonrasında, şunlar olur:</span><span class="sxs-lookup"><span data-stu-id="1c3bd-250">After failover, here's what happens:</span></span>

- <span data-ttu-id="1c3bd-251">Site Recovery ilgili ağındaki her VMM örneği için statik IP adres havuzundan VM üzerindeki her ağ arabirimi için bir IP adresi ayırır.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-251">Site Recovery allocates an IP address for each network interface on the VM, from the static IP address pool in the relevant network, for each VMM instance.</span></span>
- <span data-ttu-id="1c3bd-252">İkincil sitedeki IP adresi havuzu, aynı kaynak sitede ise Site Recovery aynı IP adresine (kaynak VM) VM çoğaltma ayırır.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-252">If the IP address pool in the secondary site is the same as that on the source site, Site Recovery allocates the same IP address (of the source VM) to the replica VM.</span></span> <span data-ttu-id="1c3bd-253">IP adresi VMM'de ayrılmış, ancak Hyper-V ana bilgisayarda yük devretme IP adresi olarak ayarlanmamış.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-253">The IP address is reserved in VMM, but it isn't set as the failover IP address on the Hyper-V host.</span></span> <span data-ttu-id="1c3bd-254">Bir Hyper-v konağı yük devretme IP adresi yalnızca yük devretme önce ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-254">The failover IP address on a Hyper-v host is set just before the failover.</span></span>
- <span data-ttu-id="1c3bd-255">Aynı IP adresi kullanılabilir değilse, Site Recovery başka bir kullanılabilir IP adresi havuzundan ayırır.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-255">If the same IP address isn't available, Site Recovery allocates another available IP address from the pool.</span></span>
- <span data-ttu-id="1c3bd-256">Sanal makineleri DHCP kullanıyorsanız, Site Recovery IP adreslerini yönetmek değil.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-256">If VMs use DHCP, Site Recovery doesn't manage the IP addresses.</span></span> <span data-ttu-id="1c3bd-257">Kaynak site ile aynı aralığından ikincil sitede DHCP sunucusu adresi ayırabilirsiniz denetlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-257">You need to check that the DHCP server on the secondary site can allocate address from the same range as the source site.</span></span>

### <a name="validate-the-ip-address"></a><span data-ttu-id="1c3bd-258">IP adresini doğrulayın</span><span class="sxs-lookup"><span data-stu-id="1c3bd-258">Validate the IP address</span></span>

<span data-ttu-id="1c3bd-259">Bir sanal makine için koruma etkinleştirildikten sonra VM'ye atanan adresi doğrulamak için örnek komut dosyası kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-259">After you enable protection for a VM, you can use following sample script to verify the address assigned to the VM.</span></span> <span data-ttu-id="1c3bd-260">Aynı IP adresi yük devretme IP adresi olarak ayarlayın ve yük devretme sırasında VM'ye atanan:</span><span class="sxs-lookup"><span data-stu-id="1c3bd-260">The same IP address will be set as the failover IP address, and assigned to the VM at the time of failover:</span></span>

    ```
    $vm = Get-SCVirtualMachine -Name <VM_NAME>
    $na = $vm[0].VirtualNetworkAdapters>
    $ip = Get-SCIPAddress -GrantToObjectID $na[0].id
    $ip.address 
    ```

## <a name="changing-ip-addresses"></a><span data-ttu-id="1c3bd-261">IP adreslerinin değiştirilmesi</span><span class="sxs-lookup"><span data-stu-id="1c3bd-261">Changing IP addresses</span></span>

<span data-ttu-id="1c3bd-262">Bu senaryoda, yük devri VM'ler IP adreslerini değiştirilir.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-262">In this scenario, the IP addresses of VMs that fail over are changed.</span></span> <span data-ttu-id="1c3bd-263">Bu çözüm dezavantajı, gerekli bakım olur.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-263">The drawback of this solution is the maintenance required.</span></span> <span data-ttu-id="1c3bd-264">Genellikle, çoğaltma sanal makineleri başlattıktan sonra DNS güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-264">Typically, DNS will be updated after replica VMs start.</span></span> <span data-ttu-id="1c3bd-265">DNS girdilerini değiştirilmesi veya gerekebilir fluster thenetwork ve önbelleğe alınan girdileri güncelleştirildi.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-265">DNS entries might need to be changed or fluster in thenetwork, and cached entries updated.</span></span> <span data-ttu-id="1c3bd-266">Bu, kapalı kalma sürelerine neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-266">This can result in downtime.</span></span> <span data-ttu-id="1c3bd-267">Kapalı kalma süresi gibi azaltılabilir:</span><span class="sxs-lookup"><span data-stu-id="1c3bd-267">Downtime can be mitigated as follows:</span></span>

- <span data-ttu-id="1c3bd-268">Düşük TTL değerleri için intranet uygulamalarını kullanın.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-268">Use low TTL values for intranet applications.</span></span>
- <span data-ttu-id="1c3bd-269">Aşağıdaki komut dosyasını bir Site Recovery kurtarma planında zamanında güncelleştirme sağlamak için DNS sunucusuna güncelleştirmek için kullanın.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-269">Use the following script in a Site Recovery recovery plan, to update the DNS server to ensure a timely update.</span></span> <span data-ttu-id="1c3bd-270">Dinamik DNS kaydını kullanırsanız, komut dosyası gerekmez.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-270">You don't need the script if you use dynamic DNS registration.</span></span>

    ```
    param(
    string]$Zone,
    [string]$name,
    [string]$IP
    )
    $Record = Get-DnsServerResourceRecord -ZoneName $zone -Name $name
    $newrecord = $record.clone()
    $newrecord.RecordData[0].IPv4Address  =  $IP
    Set-DnsServerResourceRecord -zonename $zone -OldInputObject $record -NewInputObject $Newrecord
    ```
    
### <a name="example"></a><span data-ttu-id="1c3bd-271">Örnek</span><span class="sxs-lookup"><span data-stu-id="1c3bd-271">Example</span></span> 

<span data-ttu-id="1c3bd-272">Birincil ve kurtarma siteler arasında farklı IP adreslerini kullanmak planlıyorsanız bir senaryo bakalım. Bu örnekte, farklı IP adreslerini birincil ve ikincil siteler arasında sahibiz ve vardır; s üçüncü bir site birincil veya kurtarma sitesinde barındırılan hangi uygulamalardan erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-272">Let's look at a scenario in which you're planning to use different IP addresses across the primary and the recovery sites.In this example we have different IP addresses across primary and secondary sites, and there;s a third site from which applications hosted on the primary or recovery site can be accessed.</span></span>

- <span data-ttu-id="1c3bd-273">Yük devretme önce uygulamalar barındırılan alt 192.168.1.0/24 birincil sitede ve alt ağ 172.16.1.0/24 ikincil sitedeki bir yük devretme sonrasında olması için yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-273">Before failover, apps are hosted subnet 192.168.1.0/24 on the primary site, and are configured to be in subnet 172.16.1.0/24 on the secondary site after a failover.</span></span>
- <span data-ttu-id="1c3bd-274">Tüm üç siteleri birbirine erişebilmesi için VPN bağlantıları/ağ yolları uygun şekilde yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-274">VPN connections/network routes have been configured appropriately so that all three sites can access each other.</span></span>
- <span data-ttu-id="1c3bd-275">Yük devretme sonrasında, uygulamalar kurtarma alt ağdaki geri yüklenir.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-275">After failover, apps will be restored in the recovery subnet.</span></span> <span data-ttu-id="1c3bd-276">Bu senaryoda tüm alt ağ vermesine gerek yoktur ve hiçbir değişiklik VPN veya ağ yolları yapılandırmak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-276">In this scenario there's no need to fail over the entire subnet, and no changes are needed to reconfigure VPN or network routes.</span></span> <span data-ttu-id="1c3bd-277">Yük devretme ve bazı DNS güncelleştirmeleri uygulamaları erişilebilir kaldığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-277">The failover, and some DNS updates, ensure that applications remain accessible.</span></span>
- <span data-ttu-id="1c3bd-278">DNS dinamik güncelleştirmelere izin verecek şekilde yapılandırılmışsa, sanal makineleri kendilerini yük devretme sonrasında başlattığınızda yeni IP adresini kullanarak kaydeder.</span><span class="sxs-lookup"><span data-stu-id="1c3bd-278">If DNS is configured to allow dynamic updates, then the VMs will register themselves using the new IP address, when they start after failover.</span></span>

<span data-ttu-id="1c3bd-279">**Önce yük devretme**</span><span class="sxs-lookup"><span data-stu-id="1c3bd-279">**Before failover**</span></span>

![Farklı bir IP - yük devretme önce](./media/vmm-to-vmm-walkthrough-network/network-design10.png)

<span data-ttu-id="1c3bd-281">**Yük devretme sonrasında**</span><span class="sxs-lookup"><span data-stu-id="1c3bd-281">**After failover**</span></span>

![Farklı bir IP - yük devretme sonrasında](./media/vmm-to-vmm-walkthrough-network/network-design11.png)



## <a name="next-steps"></a><span data-ttu-id="1c3bd-283">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1c3bd-283">Next steps</span></span>

<span data-ttu-id="1c3bd-284">Git [4. adım: VMM ve Hyper-V hazırlama](vmm-to-vmm-walkthrough-vmm-hyper-v.md).</span><span class="sxs-lookup"><span data-stu-id="1c3bd-284">Go to [Step 4: Prepare VMM and Hyper-V](vmm-to-vmm-walkthrough-vmm-hyper-v.md).</span></span>


