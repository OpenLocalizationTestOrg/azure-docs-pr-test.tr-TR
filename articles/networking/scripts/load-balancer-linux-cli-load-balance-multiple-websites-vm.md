---
title: "aaaAzure CLI komut dosyası örneği - yük dengelemesi hello Azure CLI ile birden çok Web siteleri | Microsoft Docs"
description: "Azure CLI komut dosyası örneği - yük dengelemesi birden çok Web siteleri toohello aynı sanal makine"
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
ms.openlocfilehash: 136da5d1783fb9f9dc87f1ffad8eec7b95c6bd7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-multiple-websites"></a><span data-ttu-id="085a6-103">Yük Dengelemesi birden çok Web sitesi</span><span class="sxs-lookup"><span data-stu-id="085a6-103">Load balance multiple websites</span></span>

<span data-ttu-id="085a6-104">Bu komut dosyası örneği iki sanal bir kullanılabilirlik kümesi üyesi olan makinelerle (VM) bir sanal ağ oluşturur.</span><span class="sxs-lookup"><span data-stu-id="085a6-104">This script sample creates a virtual network with two virtual machines (VM) that are members of an availability set.</span></span> <span data-ttu-id="085a6-105">Bir yük dengeleyici iki ayrı trafiğini yönlendiren IP adresleri toohello iki VM'ler.</span><span class="sxs-lookup"><span data-stu-id="085a6-105">A load balancer directs traffic for two separate IP addresses toohello two VMs.</span></span> <span data-ttu-id="085a6-106">Sonra çalışan hello komut dosyası, web sunucusu yazılım toohello VM'ler dağıtın ve her biri kendi IP adresiyle birden çok web sitesini barındırmak.</span><span class="sxs-lookup"><span data-stu-id="085a6-106">After running hello script, you could deploy web server software toohello VMs and host multiple web sites, each with its own IP address.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="085a6-107">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="085a6-107">Sample script</span></span>


[!code-azurecli-interactive[main](../../../cli_scripts/load-balancer/load-balance-multiple-web-sites-vm/load-balance-multiple-web-sites-vm.sh  "Load balance multiple web sites")]

## <a name="clean-up-deployment"></a><span data-ttu-id="085a6-108">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="085a6-108">Clean up deployment</span></span> 

<span data-ttu-id="085a6-109">Çalışma hello aşağıdaki tooremove hello kaynak grubu, VM ve tüm ilişkili kaynakları komutu.</span><span class="sxs-lookup"><span data-stu-id="085a6-109">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="085a6-110">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="085a6-110">Script explanation</span></span>

<span data-ttu-id="085a6-111">Bu komut dosyası toocreate bir kaynak grubu, sanal ağ, yük dengeleyici ve tüm ilişkili kaynakları komutları aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="085a6-111">This script uses hello following commands toocreate a resource group, virtual network, load balancer, and all related resources.</span></span> <span data-ttu-id="085a6-112">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="085a6-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="085a6-113">Komut</span><span class="sxs-lookup"><span data-stu-id="085a6-113">Command</span></span> | <span data-ttu-id="085a6-114">Notlar</span><span class="sxs-lookup"><span data-stu-id="085a6-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="085a6-115">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="085a6-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="085a6-116">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="085a6-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="085a6-117">az ağ vnet oluşturma</span><span class="sxs-lookup"><span data-stu-id="085a6-117">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="085a6-118">Bir Azure sanal ağ ve alt ağ oluşturur.</span><span class="sxs-lookup"><span data-stu-id="085a6-118">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="085a6-119">az ağ genel IP oluşturun</span><span class="sxs-lookup"><span data-stu-id="085a6-119">az network public-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#create) | <span data-ttu-id="085a6-120">Bir ortak IP adresi statik bir IP adresi ve ilişkili bir DNS adı ile oluşturur.</span><span class="sxs-lookup"><span data-stu-id="085a6-120">Creates a public IP address with a static IP address and an associated DNS name.</span></span> |
| [<span data-ttu-id="085a6-121">az ağ lb oluşturma</span><span class="sxs-lookup"><span data-stu-id="085a6-121">az network lb create</span></span>](https://docs.microsoft.com/cli/azure/network/lb#create) | <span data-ttu-id="085a6-122">Bir Azure yük dengeleyici oluşturur.</span><span class="sxs-lookup"><span data-stu-id="085a6-122">Creates an Azure Load Balancer.</span></span> |
| [<span data-ttu-id="085a6-123">az ağ lb araştırması oluştur</span><span class="sxs-lookup"><span data-stu-id="085a6-123">az network lb probe create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/probe#create) | <span data-ttu-id="085a6-124">Bir yük dengeleyici araştırması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="085a6-124">Creates a load balancer probe.</span></span> <span data-ttu-id="085a6-125">Yük Dengeleyici araştırmasını hello yük dengeleyici kümesindeki her bir VM kullanılan toomonitor değil.</span><span class="sxs-lookup"><span data-stu-id="085a6-125">A load balancer probe is used toomonitor each VM in hello load balancer set.</span></span> <span data-ttu-id="085a6-126">Tüm VM erişilemez hale gelirse, trafik yönlendirilmiş toohello VM değildir.</span><span class="sxs-lookup"><span data-stu-id="085a6-126">If any VM becomes inaccessible, traffic is not routed toohello VM.</span></span> |
| [<span data-ttu-id="085a6-127">az ağ lb kuralı oluşturma</span><span class="sxs-lookup"><span data-stu-id="085a6-127">az network lb rule create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="085a6-128">Yük Dengeleyici kuralı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="085a6-128">Creates a load balancer rule.</span></span> <span data-ttu-id="085a6-129">Bu örnekte, bağlantı noktası 80 için bir kural oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="085a6-129">In this sample, a rule is created for port 80.</span></span> <span data-ttu-id="085a6-130">HTTP trafiği hello yük dengeleyicide ulaştığında, yönlendirilmiş tooport 80 olur hello VM'ler hello yük dengeleyici kümesindeki biri.</span><span class="sxs-lookup"><span data-stu-id="085a6-130">As HTTP traffic arrives at hello load balancer, it is routed tooport 80 one of hello VMs in hello load balancer set.</span></span> |
| [<span data-ttu-id="085a6-131">az ağ lb ön uç-IP oluşturun</span><span class="sxs-lookup"><span data-stu-id="085a6-131">az network lb frontend-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/frontend-ip#create) | <span data-ttu-id="085a6-132">Merhaba yük dengeleyici için bir ön uç IP adresi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="085a6-132">Create a frontend IP address for hello Load Balancer.</span></span> |
| [<span data-ttu-id="085a6-133">az ağ lb adres havuzu oluşturma</span><span class="sxs-lookup"><span data-stu-id="085a6-133">az network lb address-pool create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/address-pool#create) | <span data-ttu-id="085a6-134">Arka uç adres havuzu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="085a6-134">Creates a backend address pool.</span></span> |
| [<span data-ttu-id="085a6-135">az ağ NIC oluşturun</span><span class="sxs-lookup"><span data-stu-id="085a6-135">az network nic create</span></span>](https://docs.microsoft.com/cli/azure/network/nic#create) | <span data-ttu-id="085a6-136">Bir sanal ağ kartı oluşturur ve toohello sanal ağ ve alt ekler.</span><span class="sxs-lookup"><span data-stu-id="085a6-136">Creates a virtual network card and attaches it toohello virtual network, and subnet.</span></span> |
| [<span data-ttu-id="085a6-137">az vm kullanılabilirlik kümesi oluştur</span><span class="sxs-lookup"><span data-stu-id="085a6-137">az vm availability-set create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="085a6-138">Bir kullanılabilirlik kümesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="085a6-138">Creates an availability set.</span></span> <span data-ttu-id="085a6-139">Kullanılabilirlik kümeleri, sağlayacak şekilde hello kümesinin tamamını değil hatası oluşursa, etkilenen hello sanal makineler arasında fiziksel kaynakları yayarak uygulama çalışma süresi emin olun.</span><span class="sxs-lookup"><span data-stu-id="085a6-139">Availability sets ensure application uptime by spreading hello virtual machines across physical resources such that if failure occurs, hello entire set is not effected.</span></span> |
| [<span data-ttu-id="085a6-140">az ağ NIC IP-config oluşturma</span><span class="sxs-lookup"><span data-stu-id="085a6-140">az network nic ip-config create</span></span>](https://docs.microsoft.com/cli/azure/network/nic/ip-config#create) | <span data-ttu-id="085a6-141">Bir IP confiuration oluşturur.</span><span class="sxs-lookup"><span data-stu-id="085a6-141">Creates an IP confiuration.</span></span> <span data-ttu-id="085a6-142">Merhaba Microsoft.Network/AllowMultipleIpConfigurationsPerNic özelliği, aboneliğiniz için etkin olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="085a6-142">You must have hello Microsoft.Network/AllowMultipleIpConfigurationsPerNic feature enabled for your subscription.</span></span> <span data-ttu-id="085a6-143">Merhaba birincil IP yapılandırması hello--yapma birincil bayrağı kullanarak NIC başına yalnızca bir yapılandırma atanabilir.</span><span class="sxs-lookup"><span data-stu-id="085a6-143">Only one configuration may be designated as hello primary IP configuration per NIC, using hello --make-primary flag.</span></span> |
| [<span data-ttu-id="085a6-144">az vm oluşturma</span><span class="sxs-lookup"><span data-stu-id="085a6-144">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | <span data-ttu-id="085a6-145">Merhaba sanal makine oluşturur ve toohello ağ kartı, sanal ağ, alt ağ ve NSG bağlanır.</span><span class="sxs-lookup"><span data-stu-id="085a6-145">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="085a6-146">Bu komut ayrıca kullanılan hello sanal makine görüntü toobe belirtir ve yönetici kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="085a6-146">This command also specifies hello virtual machine image toobe used and administrative credentials.</span></span>  |
| [<span data-ttu-id="085a6-147">az grubu Sil</span><span class="sxs-lookup"><span data-stu-id="085a6-147">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="085a6-148">Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler.</span><span class="sxs-lookup"><span data-stu-id="085a6-148">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="085a6-149">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="085a6-149">Next steps</span></span>

<span data-ttu-id="085a6-150">Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="085a6-150">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="085a6-151">Ek ağ CLI kod örnekleri hello bulunabilir [Azure ağ genel görünümü belgelerine](../cli-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="085a6-151">Additional networking CLI script samples can be found in hello [Azure Networking Overview documentation](../cli-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
