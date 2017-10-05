---
title: "Azure CLI örnek komut dosyası - NLB ile bir Linux VM oluşturma | Microsoft Docs"
description: "Azure CLI örnek komut dosyası - NLB ile bir Linux VM oluşturma"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: a0052605da9f0023d11cc9253d8aecfb1d452e1a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-highly-available-vm"></a><span data-ttu-id="6d408-103">Yüksek oranda kullanılabilir bir VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="6d408-103">Create a highly available VM</span></span>

<span data-ttu-id="6d408-104">Bu komut dosyası örneği yüksek oranda kullanılabilir yapılandırılmış birkaç Ubuntu sanal makineleri çalıştırmak ve dengeli yapılandırma yüklemek için gereken her şeyi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="6d408-104">This script sample creates everything needed to run several Ubuntu virtual machines configured in a highly available and load balanced configuration.</span></span> <span data-ttu-id="6d408-105">Betiği çalıştırdıktan sonra üç sanal makineler, birleştirilmiş bir Azure kullanılabilirlik kümesi için ve bir Azure yük dengeleyici üzerinden erişilebilir olacaktır.</span><span class="sxs-lookup"><span data-stu-id="6d408-105">After running the script, you will have three virtual machines, joined to an Azure Availability Set, and accessible through an Azure Load Balancer.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="6d408-106">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="6d408-106">Sample script</span></span>

<span data-ttu-id="6d408-107">[!code-azurecli-interactive[Ana](../../../cli_scripts/virtual-machine/create-vm-nlb/create-vm-nlb.sh "hızlı VM oluştur")]</span><span class="sxs-lookup"><span data-stu-id="6d408-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nlb/create-vm-nlb.sh "Quick Create VM")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="6d408-108">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="6d408-108">Clean up deployment</span></span> 

<span data-ttu-id="6d408-109">Kaynak grubu, VM ve tüm ilgili kaynaklar kaldırmak için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="6d408-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="6d408-110">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="6d408-110">Script explanation</span></span>

<span data-ttu-id="6d408-111">Bu komut, bir kaynak grubu, sanal makine, kullanılabilirlik kümesi, yük dengeleyici ve tüm ilişkili kaynakları oluşturmak için aşağıdaki komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="6d408-111">This script uses the following commands to create a resource group, virtual machine, availability set, load balancer, and all related resources.</span></span> <span data-ttu-id="6d408-112">Komut belirli belgeleri tablo bağlanan her komut.</span><span class="sxs-lookup"><span data-stu-id="6d408-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="6d408-113">Komut</span><span class="sxs-lookup"><span data-stu-id="6d408-113">Command</span></span> | <span data-ttu-id="6d408-114">Notlar</span><span class="sxs-lookup"><span data-stu-id="6d408-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="6d408-115">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="6d408-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="6d408-116">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="6d408-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="6d408-117">az ağ vnet oluşturma</span><span class="sxs-lookup"><span data-stu-id="6d408-117">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="6d408-118">Bir Azure sanal ağ ve alt ağ oluşturur.</span><span class="sxs-lookup"><span data-stu-id="6d408-118">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="6d408-119">az ağ genel IP oluşturun</span><span class="sxs-lookup"><span data-stu-id="6d408-119">az network public-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#create) | <span data-ttu-id="6d408-120">Bir ortak IP adresi statik bir IP adresi ve ilişkili bir DNS adı ile oluşturur.</span><span class="sxs-lookup"><span data-stu-id="6d408-120">Creates a public IP address with a static IP address and an associated DNS name.</span></span> |
| [<span data-ttu-id="6d408-121">az ağ lb oluşturma</span><span class="sxs-lookup"><span data-stu-id="6d408-121">az network lb create</span></span>](https://docs.microsoft.com/cli/azure/network/lb#create) | <span data-ttu-id="6d408-122">Bir Azure ağı yük dengeleyici (NLB) oluşturur.</span><span class="sxs-lookup"><span data-stu-id="6d408-122">Creates an Azure Network Load Balancer (NLB).</span></span> |
| [<span data-ttu-id="6d408-123">az ağ lb araştırması oluştur</span><span class="sxs-lookup"><span data-stu-id="6d408-123">az network lb probe create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/probe#create) | <span data-ttu-id="6d408-124">Bir NLB araştırması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="6d408-124">Creates an NLB probe.</span></span> <span data-ttu-id="6d408-125">Bir NLB araştırması NLB kümesindeki her bir VM izlemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="6d408-125">An NLB probe is used to monitor each VM in the NLB set.</span></span> <span data-ttu-id="6d408-126">Tüm VM erişilemez hale gelirse VM trafik yönlendirilmez.</span><span class="sxs-lookup"><span data-stu-id="6d408-126">If any VM becomes inaccessible, traffic is not routed to the VM.</span></span> |
| [<span data-ttu-id="6d408-127">az ağ lb kuralı oluşturma</span><span class="sxs-lookup"><span data-stu-id="6d408-127">az network lb rule create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="6d408-128">Bir NLB kuralı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="6d408-128">Creates an NLB rule.</span></span> <span data-ttu-id="6d408-129">Bu örnekte, bağlantı noktası 80 için bir kural oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="6d408-129">In this sample, a rule is created for port 80.</span></span> <span data-ttu-id="6d408-130">NLB HTTP trafiği ulaşan gibi 80 numaralı bağlantı noktasına yönlendirilir NLB kümesindeki sanal makineleri biri.</span><span class="sxs-lookup"><span data-stu-id="6d408-130">As HTTP traffic arrives at the NLB, it is routed to port 80 one of the VMs in the NLB set.</span></span> |
| [<span data-ttu-id="6d408-131">az ağ lb gelen nat-kuralı oluşturma</span><span class="sxs-lookup"><span data-stu-id="6d408-131">az network lb inbound-nat-rule create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/inbound-nat-rule#create) | <span data-ttu-id="6d408-132">Bir NLB ağ adresi çevirisi (NAT) kuralı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="6d408-132">Creates an NLB Network Address Translation (NAT) rule.</span></span>  <span data-ttu-id="6d408-133">NAT kuralları bir VM üzerinde bir bağlantı noktasına bir bağlantı noktası, NLB eşleyin.</span><span class="sxs-lookup"><span data-stu-id="6d408-133">NAT rules map a port of the NLB to a port on a VM.</span></span> <span data-ttu-id="6d408-134">Bu örnekte, SSH trafiği NLB kümesindeki her bir VM için NAT kuralı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="6d408-134">In this sample, a NAT rule is created for SSH traffic to each VM in the NLB set.</span></span>  |
| [<span data-ttu-id="6d408-135">az ağ nsg oluşturma</span><span class="sxs-lookup"><span data-stu-id="6d408-135">az network nsg create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg#create) | <span data-ttu-id="6d408-136">Internet ve sanal makine arasında bir güvenlik sınırı olan bir ağ güvenlik grubu (NSG) oluşturur.</span><span class="sxs-lookup"><span data-stu-id="6d408-136">Creates a network security group (NSG), which is a security boundary between the internet and the virtual machine.</span></span> |
| [<span data-ttu-id="6d408-137">az ağ nsg kuralı oluşturma</span><span class="sxs-lookup"><span data-stu-id="6d408-137">az network nsg rule create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | <span data-ttu-id="6d408-138">Gelen trafiğe izin veren bir NSG kuralı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="6d408-138">Creates an NSG rule to allow inbound traffic.</span></span> <span data-ttu-id="6d408-139">Bu örnekte, bağlantı noktası 22 SSH trafiği için açıldı.</span><span class="sxs-lookup"><span data-stu-id="6d408-139">In this sample, port 22 is opened for SSH traffic.</span></span> |
| [<span data-ttu-id="6d408-140">az ağ NIC oluşturun</span><span class="sxs-lookup"><span data-stu-id="6d408-140">az network nic create</span></span>](https://docs.microsoft.com/cli/azure/network/nic#create) | <span data-ttu-id="6d408-141">Bir sanal ağ kartı oluşturur ve sanal ağ, alt ağ ve NSG ekler.</span><span class="sxs-lookup"><span data-stu-id="6d408-141">Creates a virtual network card and attaches it to the virtual network, subnet, and NSG.</span></span> |
| [<span data-ttu-id="6d408-142">az vm kullanılabilirlik kümesi oluştur</span><span class="sxs-lookup"><span data-stu-id="6d408-142">az vm availability-set create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="6d408-143">Bir kullanılabilirlik kümesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="6d408-143">Creates an availability set.</span></span> <span data-ttu-id="6d408-144">Kullanılabilirlik kümeleri uygulama çalışma süresi hatası oluşursa, kümesinin tamamını değil parametreden şekilde sanal makineler arasında fiziksel kaynakları yayarak emin olun.</span><span class="sxs-lookup"><span data-stu-id="6d408-144">Availability sets ensure application uptime by spreading the virtual machines across physical resources such that if failure occurs, the entire set is not effected.</span></span> |
| [<span data-ttu-id="6d408-145">az vm oluşturma</span><span class="sxs-lookup"><span data-stu-id="6d408-145">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | <span data-ttu-id="6d408-146">Sanal makine oluşturur ve ağ kartı, sanal ağ, alt ağ ve NSG bağlanır.</span><span class="sxs-lookup"><span data-stu-id="6d408-146">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="6d408-147">Bu komut ayrıca kullanılan ve yönetici kimlik bilgileri olması için sanal makine görüntüsü belirtir.</span><span class="sxs-lookup"><span data-stu-id="6d408-147">This command also specifies the virtual machine image to be used and administrative credentials.</span></span>  |
| [<span data-ttu-id="6d408-148">az grubu Sil</span><span class="sxs-lookup"><span data-stu-id="6d408-148">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="6d408-149">Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler.</span><span class="sxs-lookup"><span data-stu-id="6d408-149">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6d408-150">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6d408-150">Next steps</span></span>

<span data-ttu-id="6d408-151">Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6d408-151">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="6d408-152">Ek sanal makine CLI kod örnekleri bulunabilir [Azure Linux VM'de belgelerine](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6d408-152">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
