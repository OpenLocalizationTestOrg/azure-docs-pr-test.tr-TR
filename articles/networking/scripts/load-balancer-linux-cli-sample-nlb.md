---
title: "Azure CLI komut dosyası örneği - yük trafiği dengelemek için sanal makineleri yüksek oranda kullanılabilirlik için | Microsoft Docs"
description: "Azure CLI komut dosyası örneği - yük trafiği dengelemek için sanal makineleri yüksek oranda kullanılabilirlik için"
services: load-balancer
documentationcenter: load-balancer
author: KumudD
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: load-balancer
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 07/07/2017
ms.author: kumud
ms.openlocfilehash: 69a7753cc75b028e2bf093053d9a5fc0890562e8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="load-balance-traffic-to-vms-for-high-availability"></a><span data-ttu-id="c285a-103">Yük trafiği dengelemek için sanal makineleri yüksek oranda kullanılabilirlik için</span><span class="sxs-lookup"><span data-stu-id="c285a-103">Load balance traffic to VMs for high availability</span></span>

<span data-ttu-id="c285a-104">Bu komut dosyası örneği yüksek oranda kullanılabilir yapılandırılmış birkaç Ubuntu sanal makineleri çalıştırmak ve dengeli yapılandırma yüklemek için gereken her şeyi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c285a-104">This script sample creates everything needed to run several Ubuntu virtual machines configured in a highly available and load balanced configuration.</span></span> <span data-ttu-id="c285a-105">Betiği çalıştırdıktan sonra üç sanal makineler, birleştirilmiş bir Azure kullanılabilirlik kümesi için ve bir Azure yük dengeleyici üzerinden erişilebilir olacaktır.</span><span class="sxs-lookup"><span data-stu-id="c285a-105">After running the script, you will have three virtual machines, joined to an Azure Availability Set, and accessible through an Azure Load Balancer.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="c285a-106">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="c285a-106">Sample script</span></span>

<span data-ttu-id="c285a-107">[!code-azurecli-interactive[Ana](../../../cli_scripts/virtual-machine/create-vm-nlb/create-vm-nlb.sh "hızlı VM oluştur")]</span><span class="sxs-lookup"><span data-stu-id="c285a-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nlb/create-vm-nlb.sh "Quick Create VM")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="c285a-108">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="c285a-108">Clean up deployment</span></span> 

<span data-ttu-id="c285a-109">Kaynak grubu, VM ve tüm ilgili kaynaklar kaldırmak için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="c285a-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="c285a-110">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="c285a-110">Script explanation</span></span>

<span data-ttu-id="c285a-111">Bu komut, bir kaynak grubu, sanal makine, kullanılabilirlik kümesi, yük dengeleyici ve tüm ilişkili kaynakları oluşturmak için aşağıdaki komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="c285a-111">This script uses the following commands to create a resource group, virtual machine, availability set, load balancer, and all related resources.</span></span> <span data-ttu-id="c285a-112">Komut belirli belgeleri tablo bağlanan her komut.</span><span class="sxs-lookup"><span data-stu-id="c285a-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="c285a-113">Komut</span><span class="sxs-lookup"><span data-stu-id="c285a-113">Command</span></span> | <span data-ttu-id="c285a-114">Notlar</span><span class="sxs-lookup"><span data-stu-id="c285a-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c285a-115">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="c285a-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="c285a-116">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c285a-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="c285a-117">az ağ vnet oluşturma</span><span class="sxs-lookup"><span data-stu-id="c285a-117">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="c285a-118">Bir Azure sanal ağ ve alt ağ oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c285a-118">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="c285a-119">az ağ genel IP oluşturun</span><span class="sxs-lookup"><span data-stu-id="c285a-119">az network public-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#create) | <span data-ttu-id="c285a-120">Bir ortak IP adresi statik bir IP adresi ve ilişkili bir DNS adı ile oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c285a-120">Creates a public IP address with a static IP address and an associated DNS name.</span></span> |
| [<span data-ttu-id="c285a-121">az ağ lb oluşturma</span><span class="sxs-lookup"><span data-stu-id="c285a-121">az network lb create</span></span>](https://docs.microsoft.com/cli/azure/network/lb#create) | <span data-ttu-id="c285a-122">Bir Azure yük dengeleyici oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c285a-122">Creates an Azure load balancer.</span></span> |
| [<span data-ttu-id="c285a-123">az ağ lb araştırması oluştur</span><span class="sxs-lookup"><span data-stu-id="c285a-123">az network lb probe create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/probe#create) | <span data-ttu-id="c285a-124">Bir yük dengeleyici araştırması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c285a-124">Creates a load balancer probe.</span></span> <span data-ttu-id="c285a-125">Yük Dengeleyici araştırmasını yük dengeleyici kümesindeki her bir VM izlemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c285a-125">A load balancer probe is used to monitor each VM in the load balancer set.</span></span> <span data-ttu-id="c285a-126">Tüm VM erişilemez hale gelirse VM trafik yönlendirilmez.</span><span class="sxs-lookup"><span data-stu-id="c285a-126">If any VM becomes inaccessible, traffic is not routed to the VM.</span></span> |
| [<span data-ttu-id="c285a-127">az ağ lb kuralı oluşturma</span><span class="sxs-lookup"><span data-stu-id="c285a-127">az network lb rule create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="c285a-128">Yük Dengeleyici kuralı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c285a-128">Creates a load balancer rule.</span></span> <span data-ttu-id="c285a-129">Bu örnekte, bağlantı noktası 80 için bir kural oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="c285a-129">In this sample, a rule is created for port 80.</span></span> <span data-ttu-id="c285a-130">HTTP trafiği yük dengeleyicide ulaşan gibi 80 numaralı bağlantı noktasına yönlendirilir LB kümesindeki sanal makineleri biri.</span><span class="sxs-lookup"><span data-stu-id="c285a-130">As HTTP traffic arrives at the load balancer, it is routed to port 80 one of the VMs in the LB set.</span></span> |
| [<span data-ttu-id="c285a-131">az ağ lb gelen nat-kuralı oluşturma</span><span class="sxs-lookup"><span data-stu-id="c285a-131">az network lb inbound-nat-rule create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/inbound-nat-rule#create) | <span data-ttu-id="c285a-132">Yük Dengeleyici ağ adresi çevirisi (NAT) kuralı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c285a-132">Creates load balancer Network Address Translation (NAT) rule.</span></span>  <span data-ttu-id="c285a-133">NAT kuralları, bir VM üzerinde bir bağlantı noktasına bir bağlantı noktası yük dengeleyicinin eşleyin.</span><span class="sxs-lookup"><span data-stu-id="c285a-133">NAT rules map a port of the load balancer to a port on a VM.</span></span> <span data-ttu-id="c285a-134">Bu örnekte, SSH trafiği yük dengeleyici kümesindeki her bir VM için NAT kuralı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="c285a-134">In this sample, a NAT rule is created for SSH traffic to each VM in the load balancer set.</span></span>  |
| [<span data-ttu-id="c285a-135">az ağ nsg oluşturma</span><span class="sxs-lookup"><span data-stu-id="c285a-135">az network nsg create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg#create) | <span data-ttu-id="c285a-136">Internet ve sanal makine arasında bir güvenlik sınırı olan bir ağ güvenlik grubu (NSG) oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c285a-136">Creates a network security group (NSG), which is a security boundary between the internet and the virtual machine.</span></span> |
| [<span data-ttu-id="c285a-137">az ağ nsg kuralı oluşturma</span><span class="sxs-lookup"><span data-stu-id="c285a-137">az network nsg rule create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | <span data-ttu-id="c285a-138">Gelen trafiğe izin veren bir NSG kuralı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c285a-138">Creates an NSG rule to allow inbound traffic.</span></span> <span data-ttu-id="c285a-139">Bu örnekte, bağlantı noktası 22 SSH trafiği için açıldı.</span><span class="sxs-lookup"><span data-stu-id="c285a-139">In this sample, port 22 is opened for SSH traffic.</span></span> |
| [<span data-ttu-id="c285a-140">az ağ NIC oluşturun</span><span class="sxs-lookup"><span data-stu-id="c285a-140">az network nic create</span></span>](https://docs.microsoft.com/cli/azure/network/nic#create) | <span data-ttu-id="c285a-141">Bir sanal ağ kartı oluşturur ve sanal ağ, alt ağ ve NSG ekler.</span><span class="sxs-lookup"><span data-stu-id="c285a-141">Creates a virtual network card and attaches it to the virtual network, subnet, and NSG.</span></span> |
| [<span data-ttu-id="c285a-142">az vm kullanılabilirlik kümesi oluştur</span><span class="sxs-lookup"><span data-stu-id="c285a-142">az vm availability-set create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="c285a-143">Bir kullanılabilirlik kümesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c285a-143">Creates an availability set.</span></span> <span data-ttu-id="c285a-144">Kullanılabilirlik kümeleri uygulama çalışma süresi hatası oluşursa, kümesinin tamamını değil parametreden şekilde sanal makineler arasında fiziksel kaynakları yayarak emin olun.</span><span class="sxs-lookup"><span data-stu-id="c285a-144">Availability sets ensure application uptime by spreading the virtual machines across physical resources such that if failure occurs, the entire set is not effected.</span></span> |
| [<span data-ttu-id="c285a-145">az vm oluşturma</span><span class="sxs-lookup"><span data-stu-id="c285a-145">az vm create</span></span>](/cli/azure/vm#create) | <span data-ttu-id="c285a-146">Sanal makine oluşturur ve ağ kartı, sanal ağ, alt ağ ve NSG bağlanır.</span><span class="sxs-lookup"><span data-stu-id="c285a-146">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="c285a-147">Bu komut ayrıca kullanılan ve yönetici kimlik bilgileri olması için sanal makine görüntüsü belirtir.</span><span class="sxs-lookup"><span data-stu-id="c285a-147">This command also specifies the virtual machine image to be used and administrative credentials.</span></span>  |
| [<span data-ttu-id="c285a-148">az grubu Sil</span><span class="sxs-lookup"><span data-stu-id="c285a-148">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="c285a-149">Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler.</span><span class="sxs-lookup"><span data-stu-id="c285a-149">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c285a-150">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c285a-150">Next steps</span></span>

<span data-ttu-id="c285a-151">Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c285a-151">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="c285a-152">Ek ağ Azure CLI kod örnekleri bulunabilir [Azure ağ belgeleri](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="c285a-152">Additional Azure Networking CLI script samples can be found in the [Azure Networking documentation](../cli-samples.md).</span></span>