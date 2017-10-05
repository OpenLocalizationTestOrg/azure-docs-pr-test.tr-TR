---
title: "Azure PowerShell Betiği örnek - yük dengelemesi Azure PowerShell ile birden çok Web siteleri | Microsoft Docs"
description: "Azure PowerShell Betiği örnek - yükünü dengelemek için aynı sanal makine birden çok Web sitesi"
services: load-balancer
documentationcenter: load-balancer
author: georgewallace
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: load-balancer
ms.devlang: powershell
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 05/16/2017
ms.author: gwallace
ms.openlocfilehash: d73cdc98ff279c3ee1b93443abe4b6c7c97786a2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="load-balance-multiple-websites"></a><span data-ttu-id="35f4e-103">Yük Dengelemesi birden çok Web sitesi</span><span class="sxs-lookup"><span data-stu-id="35f4e-103">Load balance multiple websites</span></span>

<span data-ttu-id="35f4e-104">Bu komut dosyası örneği iki sanal bir kullanılabilirlik kümesi üyesi olan makinelerle (VM) bir sanal ağ oluşturur.</span><span class="sxs-lookup"><span data-stu-id="35f4e-104">This script sample creates a virtual network with two virtual machines (VM) that are members of an availability set.</span></span> <span data-ttu-id="35f4e-105">Bir yük dengeleyici iki VM için iki ayrı IP adresleri için trafiğini yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="35f4e-105">A load balancer directs traffic for two separate IP addresses to the two VMs.</span></span> <span data-ttu-id="35f4e-106">Komut dosyasını çalıştırdıktan sonra web sunucusu yazılımı VM'ler ve ana bilgisayar, her biri kendi IP adresiyle birden çok web sitelerini dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="35f4e-106">After running the script, you could deploy web server software to the VMs and host multiple web sites, each with its own IP address.</span></span>

<span data-ttu-id="35f4e-107">Gerekirse, bulunan yönergeleri kullanarak Azure PowerShell'i yükleme [Azure PowerShell Kılavuzu](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/)ve ardından çalıştırın `Login-AzureRmAccount` Azure ile bir bağlantı oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="35f4e-107">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="35f4e-108">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="35f4e-108">Sample script</span></span>

<span data-ttu-id="35f4e-109">[!code-powershell[Ana](../../../powershell_scripts/load-balancer/load-balance-multiple-web-sites-vm/load-balance-multiple-web-sites-vm.ps1  "Yük Dengelemesi birden çok web siteleri")]</span><span class="sxs-lookup"><span data-stu-id="35f4e-109">[!code-powershell[main](../../../powershell_scripts/load-balancer/load-balance-multiple-web-sites-vm/load-balance-multiple-web-sites-vm.ps1  "Load balance multiple web sites")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="35f4e-110">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="35f4e-110">Clean up deployment</span></span> 

<span data-ttu-id="35f4e-111">Kaynak grubu, VM ve tüm ilgili kaynaklar kaldırmak için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="35f4e-111">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="35f4e-112">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="35f4e-112">Script explanation</span></span>

<span data-ttu-id="35f4e-113">Bu komut, bir kaynak grubu, sanal ağ, yük dengeleyici ve tüm ilişkili kaynakları oluşturmak için aşağıdaki komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="35f4e-113">This script uses the following commands to create a resource group, virtual network, load balancer, and all related resources.</span></span> <span data-ttu-id="35f4e-114">Komut belirli belgeleri tablo bağlanan her komut.</span><span class="sxs-lookup"><span data-stu-id="35f4e-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="35f4e-115">Komut</span><span class="sxs-lookup"><span data-stu-id="35f4e-115">Command</span></span> | <span data-ttu-id="35f4e-116">Notlar</span><span class="sxs-lookup"><span data-stu-id="35f4e-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="35f4e-117">Yeni-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="35f4e-117">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="35f4e-118">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="35f4e-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="35f4e-119">AzureRmAvailabilitySet yeni</span><span class="sxs-lookup"><span data-stu-id="35f4e-119">New-AzureRmAvailabilitySet</span></span>](/powershell/module/azurerm.compute/new-azurermavailabilityset) | <span data-ttu-id="35f4e-120">Yüksek kullanılabilirlik sağlamak üzere bir Azure kullanılabilirlik kümesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="35f4e-120">Creates an Azure availability set to provide high availability.</span></span> |
| [<span data-ttu-id="35f4e-121">AzureRmVirtualNetworkSubnetConfig yeni</span><span class="sxs-lookup"><span data-stu-id="35f4e-121">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="35f4e-122">Bir alt ağ yapılandırması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="35f4e-122">Creates a subnet configuration.</span></span> <span data-ttu-id="35f4e-123">Bu yapılandırma sanal ağ oluşturma işlemine kullanılır.</span><span class="sxs-lookup"><span data-stu-id="35f4e-123">This configuration is used with the virtual network creation process.</span></span> |
| [<span data-ttu-id="35f4e-124">Yeni-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="35f4e-124">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="35f4e-125">Sanal ağ oluşturur.</span><span class="sxs-lookup"><span data-stu-id="35f4e-125">Creates a virtual network.</span></span> |
| [<span data-ttu-id="35f4e-126">AzureRmPublicIpAddress yeni</span><span class="sxs-lookup"><span data-stu-id="35f4e-126">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="35f4e-127">Bir ortak IP adresi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="35f4e-127">Creates a public IP address.</span></span> |
| [<span data-ttu-id="35f4e-128">AzureRmLoadBalancerFrontendIpConfig yeni</span><span class="sxs-lookup"><span data-stu-id="35f4e-128">New-AzureRmLoadBalancerFrontendIpConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig) | <span data-ttu-id="35f4e-129">Bir yük dengeleyici için bir ön uç IP yapılandırması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="35f4e-129">Creates a front end IP config for a load balancer.</span></span> |
| [<span data-ttu-id="35f4e-130">AzureRmLoadBalancerBackendAddressPoolConfig yeni</span><span class="sxs-lookup"><span data-stu-id="35f4e-130">New-AzureRmLoadBalancerBackendAddressPoolConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig) | <span data-ttu-id="35f4e-131">Bir yük dengeleyici için arka uç adres havuzu yapılandırması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="35f4e-131">Creates a backend address pool configuration for a load balancer.</span></span> |
| [<span data-ttu-id="35f4e-132">AzureRmLoadBalancerProbeConfig yeni</span><span class="sxs-lookup"><span data-stu-id="35f4e-132">New-AzureRmLoadBalancerProbeConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerprobeconfig) | <span data-ttu-id="35f4e-133">Bir NLB araştırması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="35f4e-133">Creates an NLB probe.</span></span> <span data-ttu-id="35f4e-134">Bir NLB araştırması NLB kümesindeki her bir VM izlemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="35f4e-134">An NLB probe is used to monitor each VM in the NLB set.</span></span> <span data-ttu-id="35f4e-135">Tüm VM erişilemez hale gelirse VM trafik yönlendirilmez.</span><span class="sxs-lookup"><span data-stu-id="35f4e-135">If any VM becomes inaccessible, traffic is not routed to the VM.</span></span> |
| [<span data-ttu-id="35f4e-136">AzureRmLoadBalancerRuleConfig yeni</span><span class="sxs-lookup"><span data-stu-id="35f4e-136">New-AzureRmLoadBalancerRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerruleconfig) | <span data-ttu-id="35f4e-137">Bir NLB kuralı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="35f4e-137">Creates an NLB rule.</span></span> <span data-ttu-id="35f4e-138">Bu örnekte, bağlantı noktası 80 için bir kural oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="35f4e-138">In this sample, a rule is created for port 80.</span></span> <span data-ttu-id="35f4e-139">NLB HTTP trafiği ulaşan gibi 80 numaralı bağlantı noktasına yönlendirilir NLB kümesindeki sanal makineleri biri.</span><span class="sxs-lookup"><span data-stu-id="35f4e-139">As HTTP traffic arrives at the NLB, it is routed to port 80 one of the VMs in the NLB set.</span></span> |
| [<span data-ttu-id="35f4e-140">AzureRmLoadBalancer yeni</span><span class="sxs-lookup"><span data-stu-id="35f4e-140">New-AzureRmLoadBalancer</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancer) | <span data-ttu-id="35f4e-141">Bir yük dengeleyici oluşturur.</span><span class="sxs-lookup"><span data-stu-id="35f4e-141">Creates a load balancer.</span></span> |
| [<span data-ttu-id="35f4e-142">AzureRmNetworkInterfaceIpConfig yeni</span><span class="sxs-lookup"><span data-stu-id="35f4e-142">New-AzureRmNetworkInterfaceIpConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterfaceipconfig) | <span data-ttu-id="35f4e-143">Bir sanal ağ arabirimi için gelişmiş özelliklerini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="35f4e-143">Defines advanced features for a virtual network interface.</span></span> |
| [<span data-ttu-id="35f4e-144">AzureRmNetworkInterface yeni</span><span class="sxs-lookup"><span data-stu-id="35f4e-144">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="35f4e-145">Bir ağ arabirimi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="35f4e-145">Creates a network interface.</span></span> |
| [<span data-ttu-id="35f4e-146">AzureRmVMConfig yeni</span><span class="sxs-lookup"><span data-stu-id="35f4e-146">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="35f4e-147">Bir VM yapılandırması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="35f4e-147">Creates a VM configuration.</span></span> <span data-ttu-id="35f4e-148">Bu yapılandırma VM adı, işletim sistemi ve yönetici kimlik bilgileri gibi bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="35f4e-148">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="35f4e-149">Yapılandırma VM oluşturma sırasında kullanılır.</span><span class="sxs-lookup"><span data-stu-id="35f4e-149">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="35f4e-150">Yeni-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="35f4e-150">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="35f4e-151">Bir sanal makine oluşturun.</span><span class="sxs-lookup"><span data-stu-id="35f4e-151">Create a virtual machine.</span></span> |
|[<span data-ttu-id="35f4e-152">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="35f4e-152">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="35f4e-153">Bir kaynak grubu ve içerdiği tüm kaynaklar kaldırır.</span><span class="sxs-lookup"><span data-stu-id="35f4e-153">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="35f4e-154">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="35f4e-154">Next steps</span></span>

<span data-ttu-id="35f4e-155">Azure PowerShell hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="35f4e-155">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="35f4e-156">Ek ağ PowerShell komut dosyası örnekleri bulunabilir [Azure ağ genel görünümü belgelerine](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="35f4e-156">Additional networking PowerShell script samples can be found in the [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
