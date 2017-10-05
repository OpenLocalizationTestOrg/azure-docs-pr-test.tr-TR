---
title: "Azure Site kurtarma iki Azure bölgeleri arasında ağ eşlemesi | Microsoft Docs"
description: "Azure Site Recovery, çoğaltma, yük devretme ve sanal makinelerin ve fiziksel sunucuları kurtarma düzenler. Azure veya ikincil veri merkezine yük devretme hakkında bilgi edinin."
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
ms.openlocfilehash: 9d6a806ec533259797080fbfee2c38f918ebd8a2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="network-mapping-between-two-azure-regions"></a><span data-ttu-id="25d26-104">İki Azure bölgeleri arasında ağ eşlemesi</span><span class="sxs-lookup"><span data-stu-id="25d26-104">Network mapping between two Azure regions</span></span>


<span data-ttu-id="25d26-105">Bu makalede, Azure sanal ağlar birbirlerine iki Azure bölgelerinin eşlemek açıklar.</span><span class="sxs-lookup"><span data-stu-id="25d26-105">This article describes how to map Azure virtual networks of two Azure regions with each other.</span></span> <span data-ttu-id="25d26-106">Ağ eşlemesi hedef Azure bölgesi çoğaltılmış sanal makine oluşturulduğunda, kaynak sanal makinenin sanal ağa eşlenen sanal ağda oluşturulduğunu sağlar.</span><span class="sxs-lookup"><span data-stu-id="25d26-106">Network mapping ensures that when replicated virtual machine is created in the target Azure region, it is created on the virtual network that is mapped to virtual network of the source virtual machine.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="25d26-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="25d26-107">Prerequisites</span></span>
<span data-ttu-id="25d26-108">Eşledikten önce ağları oluşturduğunuzdan emin olun [Azure sanal ağlar](../virtual-network/virtual-networks-overview.md) hem de kaynak ve hedef Azure bölgeleri.</span><span class="sxs-lookup"><span data-stu-id="25d26-108">Before you map networks make sure, you have created [Azure virtual networks](../virtual-network/virtual-networks-overview.md) in both source and target Azure regions.</span></span>

## <a name="map-networks"></a><span data-ttu-id="25d26-109">Ağ eşleme</span><span class="sxs-lookup"><span data-stu-id="25d26-109">Map networks</span></span>

<span data-ttu-id="25d26-110">Bir Azure bölgesindeki bir Azure sanal ağı başka bir bölgede başka bir sanal ağ eşlemek için bir ağ eşlemesi oluşturun ve Site Recovery altyapısı için Ağ eşlemesi (Azure Virtual Machines için) -> gidin.</span><span class="sxs-lookup"><span data-stu-id="25d26-110">To map an Azure virtual network in one Azure region to another virtual network in another region, go to Site Recovery Infrastructure -> Network Mapping (For Azure Virtual Machines) and create a network mapping.</span></span>

![Ağ eşlemesi](./media/site-recovery-network-mapping-azure-to-azure/network-mapping1.png)


<span data-ttu-id="25d26-112">Aşağıdaki örnekte sanal Makinem Doğu Asya bölgesinde çalıştığından ve Güneydoğu Asya çoğaltılır.</span><span class="sxs-lookup"><span data-stu-id="25d26-112">In the example below my virtual machine is running in East Asia region and is being replicated to Southeast Asia.</span></span>

<span data-ttu-id="25d26-113">Kaynak ve hedef ağ seçin ve ardından Güneydoğu Asya Doğu Asya ağ eşlemesi oluşturmak için Tamam'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="25d26-113">Select the source and target network and then click OK to create a network mapping from East Asia to Southeast Asia.</span></span>

![Ağ eşlemesi](./media/site-recovery-network-mapping-azure-to-azure/network-mapping2.png)


<span data-ttu-id="25d26-115">Ağ eşlemesi Güneydoğu Asya Doğu Asya oluşturmak için aynı işlevi görür.</span><span class="sxs-lookup"><span data-stu-id="25d26-115">Do the same thing to create a network mapping from Southeast Asia to East Asia.</span></span>  
![Ağ eşlemesi](./media/site-recovery-network-mapping-azure-to-azure/network-mapping3.png)


## <a name="mapping-network-when-enabling-replication"></a><span data-ttu-id="25d26-117">Çoğaltma etkinleştirirken eşleme ağ</span><span class="sxs-lookup"><span data-stu-id="25d26-117">Mapping network when enabling replication</span></span>

<span data-ttu-id="25d26-118">Başka bir sanal makine için ilk zaman form bir Azure bölgesi çoğaltma yapıyorsanız, ağ eşlemesi yapılmazsa, hedef ağ aynı işleminin bir parçası olarak seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="25d26-118">If network mapping is not done when you are replicating a virtual machine for the first time form one Azure region to another, then you can choose target network as part of the same process.</span></span> <span data-ttu-id="25d26-119">Site Recovery, hedef bölgeye kaynak bölgesinden ve bu seçime dayalı kaynak bölge için hedef bölgesinden ağ eşlemeleri oluşturur.</span><span class="sxs-lookup"><span data-stu-id="25d26-119">Site Recovery creates network mappings from source region to target region and from target region to source region based on this selection.</span></span>   

![Ağ eşlemesi](./media/site-recovery-network-mapping-azure-to-azure/network-mapping4.png)

<span data-ttu-id="25d26-121">Varsayılan olarak, Site Recovery hedef bölgede kaynak ağa ve ekleyerek aynı olan bir ağ oluşturur '-asr' kaynak ağ adı için bir son eki olarak.</span><span class="sxs-lookup"><span data-stu-id="25d26-121">By default, Site Recovery creates a network in the target region that is identical to the source network and by adding '-asr' as a suffix to the name of the source network.</span></span> <span data-ttu-id="25d26-122">Önceden oluşturulmuş bir ağ Özelleştir'i tıklatarak seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="25d26-122">You can choose an already created network by clicking Customize.</span></span>

![Ağ eşlemesi](./media/site-recovery-network-mapping-azure-to-azure/network-mapping5.png)


<span data-ttu-id="25d26-124">Ağ eşlemesi zaten yapıldığında, çoğaltmayı etkinleştirirken hedef sanal ağ değiştiremezsiniz.</span><span class="sxs-lookup"><span data-stu-id="25d26-124">If the network mapping is already done, you can't change the target virtual network while enabling replication.</span></span> <span data-ttu-id="25d26-125">Değiştirmek için mevcut ağ eşlemesini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="25d26-125">To change it, modify existing network mapping.</span></span>  

![Ağ eşlemesi](./media/site-recovery-network-mapping-azure-to-azure/network-mapping6.png)

![Ağ eşlemesi](./media/site-recovery-network-mapping-azure-to-azure/modify-network-mapping.png)

> [!IMPORTANT]
> <span data-ttu-id="25d26-128">Bölge 2 bölge-1 arasında bir ağ eşlemesini değiştirirseniz, bölge 2 ağ eşlemesi bölge-1 de değiştirdiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="25d26-128">If you modify a network mapping from region-1 to region-2, make sure you modify the network mapping from region-2 to region-1 as well.</span></span>
>
>


## <a name="subnet-selection"></a><span data-ttu-id="25d26-129">Alt ağ seçimi</span><span class="sxs-lookup"><span data-stu-id="25d26-129">Subnet selection</span></span>
<span data-ttu-id="25d26-130">Hedef sanal makinenin, kaynak sanal makinenin adını temel alarak seçilir.</span><span class="sxs-lookup"><span data-stu-id="25d26-130">Subnet of the target virtual machine is selected based on the name of the subnet of the source virtual machine.</span></span> <span data-ttu-id="25d26-131">Hedef ağ kullanılabilir, kaynak sanal makine olarak aynı ada sahip bir alt ağ ise, hedef sanal makine için seçilir.</span><span class="sxs-lookup"><span data-stu-id="25d26-131">If there is a subnet of the same name as that of the source virtual machine available in the target network, then that is chosen for the target virtual machine.</span></span> <span data-ttu-id="25d26-132">Varsa hedef ağdaki aynı ada sahip bir alt ağ sonra alfabetik olarak ilk alt ağ hedef alt ağ seçilir.</span><span class="sxs-lookup"><span data-stu-id="25d26-132">If there is no subnet with the same name in the target network, then alphabetically first subnet is chosen as the target subnet.</span></span> <span data-ttu-id="25d26-133">Bu alt ağ, işlem ve ağ sanal makinenin ayarlarını giderek değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="25d26-133">You can modify this subnet by going to Compute and Network settings of the virtual machine.</span></span>

![Alt ağ değiştirme](./media/site-recovery-network-mapping-azure-to-azure/modify-subnet.png)


## <a name="ip-address"></a><span data-ttu-id="25d26-135">IP adresi</span><span class="sxs-lookup"><span data-stu-id="25d26-135">IP address</span></span>

<span data-ttu-id="25d26-136">Her hedef sanal makinenin ağ arabirimi için IP adresi gibi seçilir:</span><span class="sxs-lookup"><span data-stu-id="25d26-136">IP address for each of the network interface of the target virtual machine is chosen as follows:</span></span>

### <a name="dhcp"></a><span data-ttu-id="25d26-137">DHCP</span><span class="sxs-lookup"><span data-stu-id="25d26-137">DHCP</span></span>
<span data-ttu-id="25d26-138">Kaynak sanal makinenin Ağ arabiriminin DHCP kullanıyorsanız, hedef sanal makinenin ağ arabirimi Ayrıca DHCP ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="25d26-138">If the network interface of the source virtual machine is using DHCP, then network interface of the target virtual machine is also set as DHCP.</span></span>

### <a name="static-ip"></a><span data-ttu-id="25d26-139">Statik IP</span><span class="sxs-lookup"><span data-stu-id="25d26-139">Static IP</span></span>
<span data-ttu-id="25d26-140">Kaynak sanal makinenin Ağ arabiriminin statik IP kullanıyorsanız, ardından hedef sanal makinenin ağ arabirimi de statik IP kullanmak üzere ayarlanmış.</span><span class="sxs-lookup"><span data-stu-id="25d26-140">If the network interface of the source virtual machine is using Static IP, then network interface of the target virtual machine is also set to use Static IP.</span></span> <span data-ttu-id="25d26-141">Statik IP şu şekilde seçilir:</span><span class="sxs-lookup"><span data-stu-id="25d26-141">Static IP is chosen as follows:</span></span>

#### <a name="same-address-space"></a><span data-ttu-id="25d26-142">Aynı adres alanı</span><span class="sxs-lookup"><span data-stu-id="25d26-142">Same address space</span></span>

<span data-ttu-id="25d26-143">Kaynak alt ağı ve hedef alt aynı adres alanı varsa, hedef IP aynı kaynak sanal makinenin Ağ arabiriminin IP ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="25d26-143">If the source subnet and the target subnet have the same address space, then target IP is set same as the IP of  the network interface of the source virtual machine.</span></span> <span data-ttu-id="25d26-144">Aynı IP kullanılabilir durumda değilse, başka bir kullanılabilir IP hedef IP olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="25d26-144">If same IP is not available, then some other available IP is set as the target IP.</span></span>

#### <a name="different-address-space"></a><span data-ttu-id="25d26-145">Farklı bir adres alanı</span><span class="sxs-lookup"><span data-stu-id="25d26-145">Different address space</span></span>

<span data-ttu-id="25d26-146">Kaynak alt ağı ve hedef alt farklı bir adres alanı varsa, hedef IP hedef alt ağdaki kullanılabilir herhangi bir IP'yi olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="25d26-146">If the source subnet and the target subnet have different address space, then target IP is set as any available IP in the target subnet.</span></span>

<span data-ttu-id="25d26-147">Her ağ arabiriminin hedef IP, sanal makinenin işlem ve ağ ayarlarına giderek değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="25d26-147">You can modify the target IP on each network interface by going to Compute and Network settings of the virtual machine.</span></span>

## <a name="next-steps"></a><span data-ttu-id="25d26-148">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="25d26-148">Next steps</span></span>

- <span data-ttu-id="25d26-149">Hakkında bilgi edinin [Azure Vm'lerini çoğaltma kılavuz ağ](site-recovery-azure-to-azure-networking-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="25d26-149">Learn about [networking guidance for replicating Azure VMs](site-recovery-azure-to-azure-networking-guidance.md).</span></span>
