---
title: "Azure Site kurtarma iki Azure bölgeleri arasında aaaNetwork eşleme | Microsoft Docs"
description: "Azure Site Recovery hello çoğaltma, yük devretme ve sanal makinelerin ve fiziksel sunucuları kurtarma düzenler. Yük devretme tooAzure veya ikincil veri merkezine hakkında bilgi edinin."
services: site-recovery
documentationcenter: 
author: prateek9us
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/11/2017
ms.author: pratshar
ms.openlocfilehash: 4f80c44e3f94eaf446bc01a7041d91fe34aa78d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="network-mapping-between-two-azure-regions"></a><span data-ttu-id="27237-104">İki Azure bölgeleri arasında ağ eşlemesi</span><span class="sxs-lookup"><span data-stu-id="27237-104">Network mapping between two Azure regions</span></span>


<span data-ttu-id="27237-105">Bu makalede nasıl toomap Azure sanal ağlar birbirlerine iki Azure bölgelerinin.</span><span class="sxs-lookup"><span data-stu-id="27237-105">This article describes how toomap Azure virtual networks of two Azure regions with each other.</span></span> <span data-ttu-id="27237-106">Ağ eşlemesi çoğaltılmış sanal makine hello hedef Azure bölgesi oluşturduğunuzda, onu eşlenen toovirtual ağ hello kaynak sanal makinenin hello sanal ağ üzerinde oluşturulur sağlar.</span><span class="sxs-lookup"><span data-stu-id="27237-106">Network mapping ensures that when replicated virtual machine is created in hello target Azure region, it is created on hello virtual network that is mapped toovirtual network of hello source virtual machine.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="27237-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="27237-107">Prerequisites</span></span>
<span data-ttu-id="27237-108">Eşledikten önce ağları oluşturduğunuzdan emin olun [Azure sanal ağlar](../virtual-network/virtual-networks-overview.md) hem de kaynak ve hedef Azure bölgeleri.</span><span class="sxs-lookup"><span data-stu-id="27237-108">Before you map networks make sure, you have created [Azure virtual networks](../virtual-network/virtual-networks-overview.md) in both source and target Azure regions.</span></span>

## <a name="map-networks"></a><span data-ttu-id="27237-109">Ağ eşleme</span><span class="sxs-lookup"><span data-stu-id="27237-109">Map networks</span></span>

<span data-ttu-id="27237-110">toomap bir Azure sanal ağı bir Azure bölgesi tooanother sanal ağdaki başka bir bölgede gidin tooSite kurtarma altyapı ağ eşlemesi (Azure Virtual Machines için) -> ve bir ağ eşlemesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="27237-110">toomap an Azure virtual network in one Azure region tooanother virtual network in another region, go tooSite Recovery Infrastructure -> Network Mapping (For Azure Virtual Machines) and create a network mapping.</span></span>

![Ağ eşlemesi](./media/site-recovery-network-mapping-azure-to-azure/network-mapping1.png)


<span data-ttu-id="27237-112">Hello aşağıdaki sanal Makinem Doğu Asya bölgesinde çalıştığından ve yüklenmekte olan örnek tooSoutheast Asya çoğaltılan.</span><span class="sxs-lookup"><span data-stu-id="27237-112">In hello example below my virtual machine is running in East Asia region and is being replicated tooSoutheast Asia.</span></span>

<span data-ttu-id="27237-113">Merhaba kaynak ve hedef ağ seçin ve Tamam toocreate Doğu Asya tooSoutheast Asya arasında ağ eşlemesi'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="27237-113">Select hello source and target network and then click OK toocreate a network mapping from East Asia tooSoutheast Asia.</span></span>

![Ağ eşlemesi](./media/site-recovery-network-mapping-azure-to-azure/network-mapping2.png)


<span data-ttu-id="27237-115">Aynı şey toocreate Güneydoğu Asya tooEast Asya arasında ağ eşlemesi hello.</span><span class="sxs-lookup"><span data-stu-id="27237-115">Do hello same thing toocreate a network mapping from Southeast Asia tooEast Asia.</span></span>  
![Ağ eşlemesi](./media/site-recovery-network-mapping-azure-to-azure/network-mapping3.png)


## <a name="mapping-network-when-enabling-replication"></a><span data-ttu-id="27237-117">Çoğaltma etkinleştirirken eşleme ağ</span><span class="sxs-lookup"><span data-stu-id="27237-117">Mapping network when enabling replication</span></span>

<span data-ttu-id="27237-118">Bir sanal makine için hello ilk saat biçiminde bir Azure bölgesi tooanother çoğaltırken ağ eşlemesi yapılmazsa sonra hedef ağ hello bir parçası olarak seçebileceğiniz aynı işlemi.</span><span class="sxs-lookup"><span data-stu-id="27237-118">If network mapping is not done when you are replicating a virtual machine for hello first time form one Azure region tooanother, then you can choose target network as part of hello same process.</span></span> <span data-ttu-id="27237-119">Site Recovery ağ eşlemeleri Kaynak bölgesi tootarget bölge ve bu seçime dayalı hedef bölge toosource bölgesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="27237-119">Site Recovery creates network mappings from source region tootarget region and from target region toosource region based on this selection.</span></span>   

![Ağ eşlemesi](./media/site-recovery-network-mapping-azure-to-azure/network-mapping4.png)

<span data-ttu-id="27237-121">Varsayılan olarak, Site Recovery ağ aynı toohello kaynak ağ hello hedef bölgesi ve ekleyerek oluşturur '-asr' hello kaynak ağ bir sonek toohello adından farklı.</span><span class="sxs-lookup"><span data-stu-id="27237-121">By default, Site Recovery creates a network in hello target region that is identical toohello source network and by adding '-asr' as a suffix toohello name of hello source network.</span></span> <span data-ttu-id="27237-122">Önceden oluşturulmuş bir ağ Özelleştir'i tıklatarak seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="27237-122">You can choose an already created network by clicking Customize.</span></span>

![Ağ eşlemesi](./media/site-recovery-network-mapping-azure-to-azure/network-mapping5.png)


<span data-ttu-id="27237-124">Merhaba ağ eşlemesi zaten yapıldığında, çoğaltmayı etkinleştirirken hello hedef sanal ağ değiştiremezsiniz.</span><span class="sxs-lookup"><span data-stu-id="27237-124">If hello network mapping is already done, you can't change hello target virtual network while enabling replication.</span></span> <span data-ttu-id="27237-125">toochange, mevcut ağ eşlemesini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="27237-125">toochange it, modify existing network mapping.</span></span>  

![Ağ eşlemesi](./media/site-recovery-network-mapping-azure-to-azure/network-mapping6.png)

![Ağ eşlemesi](./media/site-recovery-network-mapping-azure-to-azure/modify-network-mapping.png)

> [!IMPORTANT]
> <span data-ttu-id="27237-128">Bölge 1 tooregion-2 ağ eşlemesini değiştirirseniz, bölge 2 tooregion-1'de hello ağ eşlemesi değiştirdiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="27237-128">If you modify a network mapping from region-1 tooregion-2, make sure you modify hello network mapping from region-2 tooregion-1 as well.</span></span>
>
>


## <a name="subnet-selection"></a><span data-ttu-id="27237-129">Alt ağ seçimi</span><span class="sxs-lookup"><span data-stu-id="27237-129">Subnet selection</span></span>
<span data-ttu-id="27237-130">Merhaba hedef sanal makinenin hello hello alt hello kaynak sanal makinenin adına göre seçilir.</span><span class="sxs-lookup"><span data-stu-id="27237-130">Subnet of hello target virtual machine is selected based on hello name of hello subnet of hello source virtual machine.</span></span> <span data-ttu-id="27237-131">Merhaba alt ise hello hedef sanal makine için seçilen sonra aynı hello kaynak sanal makinenin hello hedef ağ kullanılabilir olarak adlandırın.</span><span class="sxs-lookup"><span data-stu-id="27237-131">If there is a subnet of hello same name as that of hello source virtual machine available in hello target network, then that is chosen for hello target virtual machine.</span></span> <span data-ttu-id="27237-132">Merhaba bir alt ağ ise alfabetik olarak ilk alt ağ hedef alt hello olarak seçilen aynı hello hedef ağ adı.</span><span class="sxs-lookup"><span data-stu-id="27237-132">If there is no subnet with hello same name in hello target network, then alphabetically first subnet is chosen as hello target subnet.</span></span> <span data-ttu-id="27237-133">Bu alt ağ tooCompute ve hello sanal makinesinin ağ ayarları giderek değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="27237-133">You can modify this subnet by going tooCompute and Network settings of hello virtual machine.</span></span>

![Alt ağ değiştirme](./media/site-recovery-network-mapping-azure-to-azure/modify-subnet.png)


## <a name="ip-address"></a><span data-ttu-id="27237-135">IP adresi</span><span class="sxs-lookup"><span data-stu-id="27237-135">IP address</span></span>

<span data-ttu-id="27237-136">Her hello ağ arabiriminin hello hedef sanal makine için IP adresi gibi seçilir:</span><span class="sxs-lookup"><span data-stu-id="27237-136">IP address for each of hello network interface of hello target virtual machine is chosen as follows:</span></span>

### <a name="dhcp"></a><span data-ttu-id="27237-137">DHCP</span><span class="sxs-lookup"><span data-stu-id="27237-137">DHCP</span></span>
<span data-ttu-id="27237-138">Merhaba ağ arabirimi hello kaynak sanal makinenin DHCP kullanıyorsanız, hello hedef sanal makinenin ağ arabirimi Ayrıca DHCP ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="27237-138">If hello network interface of hello source virtual machine is using DHCP, then network interface of hello target virtual machine is also set as DHCP.</span></span>

### <a name="static-ip"></a><span data-ttu-id="27237-139">Statik IP</span><span class="sxs-lookup"><span data-stu-id="27237-139">Static IP</span></span>
<span data-ttu-id="27237-140">Merhaba ağ arabirimi hello kaynak sanal makinenin statik IP kullanıyorsanız, ağ arabiriminin hello hedef sanal makine de toouse statik IP ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="27237-140">If hello network interface of hello source virtual machine is using Static IP, then network interface of hello target virtual machine is also set toouse Static IP.</span></span> <span data-ttu-id="27237-141">Statik IP şu şekilde seçilir:</span><span class="sxs-lookup"><span data-stu-id="27237-141">Static IP is chosen as follows:</span></span>

#### <a name="same-address-space"></a><span data-ttu-id="27237-142">Aynı adres alanı</span><span class="sxs-lookup"><span data-stu-id="27237-142">Same address space</span></span>

<span data-ttu-id="27237-143">Merhaba kaynak alt ağı ve hello hedef alt hello varsa, hedef IP hello IP hello ağ arabiriminin hello kaynak sanal makinenin aynı ayarlayın daha sonra aynı adres alanı.</span><span class="sxs-lookup"><span data-stu-id="27237-143">If hello source subnet and hello target subnet have hello same address space, then target IP is set same as hello IP of  hello network interface of hello source virtual machine.</span></span> <span data-ttu-id="27237-144">Aynı IP kullanılabilir durumda değilse, başka bir kullanılabilir IP hello hedef IP ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="27237-144">If same IP is not available, then some other available IP is set as hello target IP.</span></span>

#### <a name="different-address-space"></a><span data-ttu-id="27237-145">Farklı bir adres alanı</span><span class="sxs-lookup"><span data-stu-id="27237-145">Different address space</span></span>

<span data-ttu-id="27237-146">Merhaba kaynak alt ağı ve hello hedef alt farklı bir adres alanı varsa, hedef IP hello hedef alt ağda kullanılabilir herhangi bir IP'yi olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="27237-146">If hello source subnet and hello target subnet have different address space, then target IP is set as any available IP in hello target subnet.</span></span>

<span data-ttu-id="27237-147">Her ağ arabiriminde hello hedef IP tooCompute ve hello sanal makinesinin ağ ayarları giderek değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="27237-147">You can modify hello target IP on each network interface by going tooCompute and Network settings of hello virtual machine.</span></span>

## <a name="next-steps"></a><span data-ttu-id="27237-148">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="27237-148">Next steps</span></span>

- <span data-ttu-id="27237-149">Hakkında bilgi edinin [Azure Vm'lerini çoğaltma kılavuz ağ](site-recovery-azure-to-azure-networking-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="27237-149">Learn about [networking guidance for replicating Azure VMs](site-recovery-azure-to-azure-networking-guidance.md).</span></span>
