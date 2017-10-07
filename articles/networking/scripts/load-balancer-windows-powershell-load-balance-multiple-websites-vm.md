---
title: "PowerShell komut dosyası örneği - aaaAzure Yük Dengelemesi Azure PowerShell ile birden çok Web siteleri | Microsoft Docs"
description: "Azure PowerShell Betiği örnek - yük dengelemesi birden çok Web siteleri toohello aynı sanal makine"
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
ms.openlocfilehash: 316818964eb6928fe4163ef69eb7f05da2dc9636
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-multiple-websites"></a><span data-ttu-id="a1720-103">Yük Dengelemesi birden çok Web sitesi</span><span class="sxs-lookup"><span data-stu-id="a1720-103">Load balance multiple websites</span></span>

<span data-ttu-id="a1720-104">Bu komut dosyası örneği iki sanal bir kullanılabilirlik kümesi üyesi olan makinelerle (VM) bir sanal ağ oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a1720-104">This script sample creates a virtual network with two virtual machines (VM) that are members of an availability set.</span></span> <span data-ttu-id="a1720-105">Bir yük dengeleyici iki ayrı trafiğini yönlendiren IP adresleri toohello iki VM'ler.</span><span class="sxs-lookup"><span data-stu-id="a1720-105">A load balancer directs traffic for two separate IP addresses toohello two VMs.</span></span> <span data-ttu-id="a1720-106">Sonra çalışan hello komut dosyası, web sunucusu yazılım toohello VM'ler dağıtın ve her biri kendi IP adresiyle birden çok web sitesini barındırmak.</span><span class="sxs-lookup"><span data-stu-id="a1720-106">After running hello script, you could deploy web server software toohello VMs and host multiple web sites, each with its own IP address.</span></span>

<span data-ttu-id="a1720-107">Gerekirse, Azure PowerShell hello yönerge kullanarak bulunan hello hello yükleyin [Azure PowerShell Kılavuzu](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/)ve ardından çalıştırın `Login-AzureRmAccount` toocreate Azure ile bir bağlantı.</span><span class="sxs-lookup"><span data-stu-id="a1720-107">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="a1720-108">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="a1720-108">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/load-balancer/load-balance-multiple-web-sites-vm/load-balance-multiple-web-sites-vm.ps1  "Load balance multiple web sites")]

## <a name="clean-up-deployment"></a><span data-ttu-id="a1720-109">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="a1720-109">Clean up deployment</span></span> 

<span data-ttu-id="a1720-110">Çalışma hello aşağıdaki tooremove hello kaynak grubu, VM ve tüm ilişkili kaynakları komutu.</span><span class="sxs-lookup"><span data-stu-id="a1720-110">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="a1720-111">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="a1720-111">Script explanation</span></span>

<span data-ttu-id="a1720-112">Bu komut dosyası toocreate bir kaynak grubu, sanal ağ, yük dengeleyici ve tüm ilişkili kaynakları komutları aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="a1720-112">This script uses hello following commands toocreate a resource group, virtual network, load balancer, and all related resources.</span></span> <span data-ttu-id="a1720-113">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="a1720-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="a1720-114">Komut</span><span class="sxs-lookup"><span data-stu-id="a1720-114">Command</span></span> | <span data-ttu-id="a1720-115">Notlar</span><span class="sxs-lookup"><span data-stu-id="a1720-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a1720-116">Yeni-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="a1720-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="a1720-117">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a1720-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="a1720-118">AzureRmAvailabilitySet yeni</span><span class="sxs-lookup"><span data-stu-id="a1720-118">New-AzureRmAvailabilitySet</span></span>](/powershell/module/azurerm.compute/new-azurermavailabilityset) | <span data-ttu-id="a1720-119">Bir Azure kullanılabilirlik kümesi tooprovide yüksek kullanılabilirlik oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a1720-119">Creates an Azure availability set tooprovide high availability.</span></span> |
| [<span data-ttu-id="a1720-120">AzureRmVirtualNetworkSubnetConfig yeni</span><span class="sxs-lookup"><span data-stu-id="a1720-120">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="a1720-121">Bir alt ağ yapılandırması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a1720-121">Creates a subnet configuration.</span></span> <span data-ttu-id="a1720-122">Bu yapılandırma ile Merhaba sanal ağ oluşturma işleminde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a1720-122">This configuration is used with hello virtual network creation process.</span></span> |
| [<span data-ttu-id="a1720-123">Yeni-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="a1720-123">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="a1720-124">Sanal ağ oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a1720-124">Creates a virtual network.</span></span> |
| [<span data-ttu-id="a1720-125">AzureRmPublicIpAddress yeni</span><span class="sxs-lookup"><span data-stu-id="a1720-125">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="a1720-126">Bir ortak IP adresi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a1720-126">Creates a public IP address.</span></span> |
| [<span data-ttu-id="a1720-127">AzureRmLoadBalancerFrontendIpConfig yeni</span><span class="sxs-lookup"><span data-stu-id="a1720-127">New-AzureRmLoadBalancerFrontendIpConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig) | <span data-ttu-id="a1720-128">Bir yük dengeleyici için bir ön uç IP yapılandırması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a1720-128">Creates a front end IP config for a load balancer.</span></span> |
| [<span data-ttu-id="a1720-129">AzureRmLoadBalancerBackendAddressPoolConfig yeni</span><span class="sxs-lookup"><span data-stu-id="a1720-129">New-AzureRmLoadBalancerBackendAddressPoolConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig) | <span data-ttu-id="a1720-130">Bir yük dengeleyici için arka uç adres havuzu yapılandırması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a1720-130">Creates a backend address pool configuration for a load balancer.</span></span> |
| [<span data-ttu-id="a1720-131">AzureRmLoadBalancerProbeConfig yeni</span><span class="sxs-lookup"><span data-stu-id="a1720-131">New-AzureRmLoadBalancerProbeConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerprobeconfig) | <span data-ttu-id="a1720-132">Bir NLB araştırması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a1720-132">Creates an NLB probe.</span></span> <span data-ttu-id="a1720-133">Bir NLB araştırması hello NLB kümesindeki her bir VM kullanılan toomonitor değil.</span><span class="sxs-lookup"><span data-stu-id="a1720-133">An NLB probe is used toomonitor each VM in hello NLB set.</span></span> <span data-ttu-id="a1720-134">Tüm VM erişilemez hale gelirse, trafik yönlendirilmiş toohello VM değildir.</span><span class="sxs-lookup"><span data-stu-id="a1720-134">If any VM becomes inaccessible, traffic is not routed toohello VM.</span></span> |
| [<span data-ttu-id="a1720-135">AzureRmLoadBalancerRuleConfig yeni</span><span class="sxs-lookup"><span data-stu-id="a1720-135">New-AzureRmLoadBalancerRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerruleconfig) | <span data-ttu-id="a1720-136">Bir NLB kuralı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a1720-136">Creates an NLB rule.</span></span> <span data-ttu-id="a1720-137">Bu örnekte, bağlantı noktası 80 için bir kural oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="a1720-137">In this sample, a rule is created for port 80.</span></span> <span data-ttu-id="a1720-138">HTTP trafiği NLB hello sırasında ulaştığında, yönlendirilmiş tooport 80 olur hello VM'ler hello NLB kümesindeki biri.</span><span class="sxs-lookup"><span data-stu-id="a1720-138">As HTTP traffic arrives at hello NLB, it is routed tooport 80 one of hello VMs in hello NLB set.</span></span> |
| [<span data-ttu-id="a1720-139">AzureRmLoadBalancer yeni</span><span class="sxs-lookup"><span data-stu-id="a1720-139">New-AzureRmLoadBalancer</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancer) | <span data-ttu-id="a1720-140">Bir yük dengeleyici oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a1720-140">Creates a load balancer.</span></span> |
| [<span data-ttu-id="a1720-141">AzureRmNetworkInterfaceIpConfig yeni</span><span class="sxs-lookup"><span data-stu-id="a1720-141">New-AzureRmNetworkInterfaceIpConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterfaceipconfig) | <span data-ttu-id="a1720-142">Bir sanal ağ arabirimi için gelişmiş özelliklerini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="a1720-142">Defines advanced features for a virtual network interface.</span></span> |
| [<span data-ttu-id="a1720-143">AzureRmNetworkInterface yeni</span><span class="sxs-lookup"><span data-stu-id="a1720-143">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="a1720-144">Bir ağ arabirimi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a1720-144">Creates a network interface.</span></span> |
| [<span data-ttu-id="a1720-145">AzureRmVMConfig yeni</span><span class="sxs-lookup"><span data-stu-id="a1720-145">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="a1720-146">Bir VM yapılandırması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a1720-146">Creates a VM configuration.</span></span> <span data-ttu-id="a1720-147">Bu yapılandırma VM adı, işletim sistemi ve yönetici kimlik bilgileri gibi bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="a1720-147">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="a1720-148">Merhaba yapılandırma VM oluşturma sırasında kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a1720-148">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="a1720-149">Yeni-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="a1720-149">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="a1720-150">Bir sanal makine oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a1720-150">Create a virtual machine.</span></span> |
|[<span data-ttu-id="a1720-151">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="a1720-151">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="a1720-152">Bir kaynak grubu ve içerdiği tüm kaynaklar kaldırır.</span><span class="sxs-lookup"><span data-stu-id="a1720-152">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a1720-153">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a1720-153">Next steps</span></span>

<span data-ttu-id="a1720-154">Hello Azure PowerShell hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a1720-154">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="a1720-155">Ek ağ PowerShell komut dosyası örnekleri hello bulunabilir [Azure ağ genel görünümü belgelerine](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a1720-155">Additional networking PowerShell script samples can be found in hello [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
