---
title: "aaaAzure CLI komut dosyası örneği - NLB ile bir Windows Server 2016 VM oluşturma | Microsoft Docs"
description: "Azure CLI örnek komut dosyası - NLB ile bir Windows Server 2016 VM oluşturma"
services: virtual-machines-Windows
documentationcenter: virtual-machines
author: rickstercdn
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-machines-Windows
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 02/23/2017
ms.author: rclaus
ms.openlocfilehash: aaaac0c2cc32ce0cac21417926399d848bd6fa09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-traffic-between-highly-available-virtual-machines"></a><span data-ttu-id="3d671-103">Yüksek oranda kullanılabilir sanal makineler arasında Yük Dengelemesi trafiği</span><span class="sxs-lookup"><span data-stu-id="3d671-103">Load balance traffic between highly available virtual machines</span></span>

<span data-ttu-id="3d671-104">Bu komut dosyası örneği gereken her şeyi oluşturur toorun birkaç Ubuntu sanal makineleri yüksek oranda kullanılabilir yapılandırılmış ve yük dengeli yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="3d671-104">This script sample creates everything needed toorun several Ubuntu virtual machines configured in a highly available and load balanced configuration.</span></span> <span data-ttu-id="3d671-105">Çalışan hello betik sonra üç sanal makineler, birleştirilmiş tooan Azure kullanılabilirlik kümesi, sahip olur ve bir Azure yük dengeleyici üzerinden erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="3d671-105">After running hello script, you will have three virtual machines, joined tooan Azure Availability Set, and accessible through an Azure Load Balancer.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="3d671-106">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="3d671-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nlb/create-windows-vm-nlb.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="3d671-107">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="3d671-107">Clean up deployment</span></span> 

<span data-ttu-id="3d671-108">Çalışma hello aşağıdaki tooremove hello kaynak grubu, VM ve tüm ilişkili kaynakları komutu.</span><span class="sxs-lookup"><span data-stu-id="3d671-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="3d671-109">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="3d671-109">Script explanation</span></span>

<span data-ttu-id="3d671-110">Bu komut dosyası komutları toocreate bir kaynak grubu, sanal makine, kullanılabilirlik kümesi, yük dengeleyici ve tüm ilgili kaynaklar aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="3d671-110">This script uses hello following commands toocreate a resource group, virtual machine, availability set, load balancer, and all related resources.</span></span> <span data-ttu-id="3d671-111">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="3d671-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="3d671-112">Komut</span><span class="sxs-lookup"><span data-stu-id="3d671-112">Command</span></span> | <span data-ttu-id="3d671-113">Notlar</span><span class="sxs-lookup"><span data-stu-id="3d671-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="3d671-114">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="3d671-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="3d671-115">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3d671-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="3d671-116">az ağ vnet oluşturma</span><span class="sxs-lookup"><span data-stu-id="3d671-116">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="3d671-117">Bir Azure sanal ağ ve alt ağ oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3d671-117">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="3d671-118">az ağ genel IP oluşturun</span><span class="sxs-lookup"><span data-stu-id="3d671-118">az network public-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#create) | <span data-ttu-id="3d671-119">Bir ortak IP adresi statik bir IP adresi ve ilişkili bir DNS adı ile oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3d671-119">Creates a public IP address with a static IP address and an associated DNS name.</span></span> |
| [<span data-ttu-id="3d671-120">az ağ lb oluşturma</span><span class="sxs-lookup"><span data-stu-id="3d671-120">az network lb create</span></span>](https://docs.microsoft.com/cli/azure/network/lb#create) | <span data-ttu-id="3d671-121">Bir Azure ağı yük dengeleyici (NLB) oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3d671-121">Creates an Azure Network Load Balancer (NLB).</span></span> |
| [<span data-ttu-id="3d671-122">az ağ lb araştırması oluştur</span><span class="sxs-lookup"><span data-stu-id="3d671-122">az network lb probe create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/probe#create) | <span data-ttu-id="3d671-123">Bir NLB araştırması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3d671-123">Creates an NLB probe.</span></span> <span data-ttu-id="3d671-124">Bir NLB araştırması hello NLB kümesindeki her bir VM kullanılan toomonitor değil.</span><span class="sxs-lookup"><span data-stu-id="3d671-124">An NLB probe is used toomonitor each VM in hello NLB set.</span></span> <span data-ttu-id="3d671-125">Tüm VM erişilemez hale gelirse, trafik yönlendirilmiş toohello VM değildir.</span><span class="sxs-lookup"><span data-stu-id="3d671-125">If any VM becomes inaccessible, traffic is not routed toohello VM.</span></span> |
| [<span data-ttu-id="3d671-126">az ağ lb kuralı oluşturma</span><span class="sxs-lookup"><span data-stu-id="3d671-126">az network lb rule create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="3d671-127">Bir NLB kuralı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3d671-127">Creates an NLB rule.</span></span> <span data-ttu-id="3d671-128">Bu örnekte, bağlantı noktası 80 için bir kural oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="3d671-128">In this sample, a rule is created for port 80.</span></span> <span data-ttu-id="3d671-129">HTTP trafiği NLB hello sırasında ulaştığında, yönlendirilmiş tooport 80 olur hello VM'ler hello NLB kümesindeki biri.</span><span class="sxs-lookup"><span data-stu-id="3d671-129">As HTTP traffic arrives at hello NLB, it is routed tooport 80 one of hello VMs in hello NLB set.</span></span> |
| [<span data-ttu-id="3d671-130">az ağ lb gelen nat-kuralı oluşturma</span><span class="sxs-lookup"><span data-stu-id="3d671-130">az network lb inbound-nat-rule create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/inbound-nat-rule#create) | <span data-ttu-id="3d671-131">Bir NLB ağ adresi çevirisi (NAT) kuralı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3d671-131">Creates an NLB Network Address Translation (NAT) rule.</span></span>  <span data-ttu-id="3d671-132">NAT kuralları hello NLB tooa bağlantı noktası bir VM üzerinde bir bağlantı noktası eşleme.</span><span class="sxs-lookup"><span data-stu-id="3d671-132">NAT rules map a port of hello NLB tooa port on a VM.</span></span> <span data-ttu-id="3d671-133">Bu örnekte, hello NLB kümesindeki SSH trafiği tooeach VM için NAT kuralı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="3d671-133">In this sample, a NAT rule is created for SSH traffic tooeach VM in hello NLB set.</span></span>  |
| [<span data-ttu-id="3d671-134">az ağ nsg oluşturma</span><span class="sxs-lookup"><span data-stu-id="3d671-134">az network nsg create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg#create) | <span data-ttu-id="3d671-135">Merhaba Internet ve hello sanal makine arasında bir güvenlik sınırı olan bir ağ güvenlik grubu (NSG) oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3d671-135">Creates a network security group (NSG), which is a security boundary between hello internet and hello virtual machine.</span></span> |
| [<span data-ttu-id="3d671-136">az ağ nsg kuralı oluşturma</span><span class="sxs-lookup"><span data-stu-id="3d671-136">az network nsg rule create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | <span data-ttu-id="3d671-137">Bir NSG kural tooallow oluşturur gelen trafiği.</span><span class="sxs-lookup"><span data-stu-id="3d671-137">Creates an NSG rule tooallow inbound traffic.</span></span> <span data-ttu-id="3d671-138">Bu örnekte, bağlantı noktası 22 SSH trafiği için açıldı.</span><span class="sxs-lookup"><span data-stu-id="3d671-138">In this sample, port 22 is opened for SSH traffic.</span></span> |
| [<span data-ttu-id="3d671-139">az ağ NIC oluşturun</span><span class="sxs-lookup"><span data-stu-id="3d671-139">az network nic create</span></span>](https://docs.microsoft.com/cli/azure/network/nic#create) | <span data-ttu-id="3d671-140">Bir sanal ağ kartı oluşturur ve toohello sanal ağ, alt ağ ve NSG ekler.</span><span class="sxs-lookup"><span data-stu-id="3d671-140">Creates a virtual network card and attaches it toohello virtual network, subnet, and NSG.</span></span> |
| [<span data-ttu-id="3d671-141">az vm kullanılabilirlik kümesi oluştur</span><span class="sxs-lookup"><span data-stu-id="3d671-141">az vm availability-set create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="3d671-142">Bir kullanılabilirlik kümesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3d671-142">Creates an availability set.</span></span> <span data-ttu-id="3d671-143">Kullanılabilirlik kümeleri, sağlayacak şekilde hello kümesinin tamamını değil hatası oluşursa, etkilenen hello sanal makineler arasında fiziksel kaynakları yayarak uygulama çalışma süresi emin olun.</span><span class="sxs-lookup"><span data-stu-id="3d671-143">Availability sets ensure application uptime by spreading hello virtual machines across physical resources such that if failure occurs, hello entire set is not effected.</span></span> |
| [<span data-ttu-id="3d671-144">az vm oluşturma</span><span class="sxs-lookup"><span data-stu-id="3d671-144">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | <span data-ttu-id="3d671-145">Merhaba sanal makine oluşturur ve toohello ağ kartı, sanal ağ, alt ağ ve NSG bağlanır.</span><span class="sxs-lookup"><span data-stu-id="3d671-145">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="3d671-146">Bu komut ayrıca kullanılan hello sanal makine görüntü toobe belirtir ve yönetici kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="3d671-146">This command also specifies hello virtual machine image toobe used and administrative credentials.</span></span>  |
| [<span data-ttu-id="3d671-147">az grubu Sil</span><span class="sxs-lookup"><span data-stu-id="3d671-147">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="3d671-148">Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler.</span><span class="sxs-lookup"><span data-stu-id="3d671-148">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="3d671-149">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3d671-149">Next steps</span></span>

<span data-ttu-id="3d671-150">Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3d671-150">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="3d671-151">Ek sanal makine CLI kod örnekleri hello bulunabilir [Azure Windows VM belgelerine](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3d671-151">Additional virtual machine CLI script samples can be found in hello [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
