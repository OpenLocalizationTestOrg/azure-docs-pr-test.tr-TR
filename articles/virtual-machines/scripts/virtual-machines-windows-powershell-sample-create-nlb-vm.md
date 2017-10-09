---
title: "PowerShell komut dosyası örneği - aaaAzure bir Windows VM NLB oluşturun | Microsoft Docs"
description: "Azure PowerShell Betiği örnek - Windows VM NLB oluşturma"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 06/05/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 60a48c5f243c8ff3ab886437ae45b21ce069ea4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-traffic-between-highly-available-virtual-machines"></a><span data-ttu-id="69c5b-103">Yüksek oranda kullanılabilir sanal makineler arasında Yük Dengelemesi trafiği</span><span class="sxs-lookup"><span data-stu-id="69c5b-103">Load balance traffic between highly available virtual machines</span></span>

<span data-ttu-id="69c5b-104">Bu komut dosyası örneği gereken her şeyi oluşturur toorun birkaç Windows Server 2016 sanal makineleri yüksek oranda kullanılabilir yapılandırılmış ve yük dengeli yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="69c5b-104">This script sample creates everything needed toorun several Windows Server 2016 virtual machines configured in a highly available and load balanced configuration.</span></span> <span data-ttu-id="69c5b-105">Çalışan hello betik sonra üç sanal makineler, birleştirilmiş tooan Azure kullanılabilirlik kümesi, sahip olur ve bir Azure yük dengeleyici üzerinden erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="69c5b-105">After running hello script, you will have three virtual machines, joined tooan Azure Availability Set, and accessible through an Azure Load Balancer.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="69c5b-106">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="69c5b-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-nlb/create-vm-nlb.ps1 "Create VM NLB")]

## <a name="clean-up-deployment"></a><span data-ttu-id="69c5b-107">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="69c5b-107">Clean up deployment</span></span> 

<span data-ttu-id="69c5b-108">Çalışma hello aşağıdaki tooremove hello kaynak grubu, VM ve tüm ilişkili kaynakları komutu.</span><span class="sxs-lookup"><span data-stu-id="69c5b-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="69c5b-109">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="69c5b-109">Script explanation</span></span>

<span data-ttu-id="69c5b-110">Bu komut dosyası komutları toocreate hello dağıtım aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="69c5b-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="69c5b-111">Merhaba tablosundaki her öğesi toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="69c5b-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="69c5b-112">Komut</span><span class="sxs-lookup"><span data-stu-id="69c5b-112">Command</span></span> | <span data-ttu-id="69c5b-113">Notlar</span><span class="sxs-lookup"><span data-stu-id="69c5b-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="69c5b-114">Yeni-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="69c5b-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="69c5b-115">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="69c5b-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="69c5b-116">AzureRmVirtualNetworkSubnetConfig yeni</span><span class="sxs-lookup"><span data-stu-id="69c5b-116">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="69c5b-117">Bir alt ağ yapılandırması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="69c5b-117">Creates a subnet configuration.</span></span> <span data-ttu-id="69c5b-118">Bu yapılandırma ile Merhaba sanal ağ oluşturma işleminde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="69c5b-118">This configuration is used with hello virtual network creation process.</span></span> |
| [<span data-ttu-id="69c5b-119">Yeni-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="69c5b-119">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="69c5b-120">Sanal ağ oluşturur.</span><span class="sxs-lookup"><span data-stu-id="69c5b-120">Creates a virtual network.</span></span> |
| [<span data-ttu-id="69c5b-121">AzureRmPublicIpAddress yeni</span><span class="sxs-lookup"><span data-stu-id="69c5b-121">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="69c5b-122">Bir ortak IP adresi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="69c5b-122">Creates a public IP address.</span></span> |
| [<span data-ttu-id="69c5b-123">AzureRmLoadBalancerFrontendIpConfig yeni</span><span class="sxs-lookup"><span data-stu-id="69c5b-123">New-AzureRmLoadBalancerFrontendIpConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig) | <span data-ttu-id="69c5b-124">Bir yük dengeleyici için bir ön uç IP yapılandırmasını oluşturur.</span><span class="sxs-lookup"><span data-stu-id="69c5b-124">Creates a front-end IP configuration for a load balancer.</span></span> |
| [<span data-ttu-id="69c5b-125">AzureRmLoadBalancerBackendAddressPoolConfig yeni</span><span class="sxs-lookup"><span data-stu-id="69c5b-125">New-AzureRmLoadBalancerBackendAddressPoolConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig) | <span data-ttu-id="69c5b-126">Bir yük dengeleyici için arka uç adres havuzu yapılandırması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="69c5b-126">Creates a backend address pool configuration for a load balancer.</span></span> |
| [<span data-ttu-id="69c5b-127">AzureRmLoadBalancerProbeConfig yeni</span><span class="sxs-lookup"><span data-stu-id="69c5b-127">New-AzureRmLoadBalancerProbeConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerprobeconfig) | <span data-ttu-id="69c5b-128">Bir yük dengeleyici için bir araştırma yapılandırma oluşturur.</span><span class="sxs-lookup"><span data-stu-id="69c5b-128">Creates a probe configuration for a load balancer.</span></span> |
| [<span data-ttu-id="69c5b-129">AzureRmLoadBalancerRuleConfig yeni</span><span class="sxs-lookup"><span data-stu-id="69c5b-129">New-AzureRmLoadBalancerRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerruleconfig) | <span data-ttu-id="69c5b-130">Bir yük dengeleyici için bir kural yapılandırma oluşturur.</span><span class="sxs-lookup"><span data-stu-id="69c5b-130">Creates a rule configuration for a load balancer.</span></span> |
| [<span data-ttu-id="69c5b-131">AzureRmLoadBalancerInboundNatRuleConfig yeni</span><span class="sxs-lookup"><span data-stu-id="69c5b-131">New-AzureRmLoadBalancerInboundNatRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerinboundnatruleconfig) | <span data-ttu-id="69c5b-132">Bir yük dengeleyici için bir gelen NAT kuralı yapılandırmasını oluşturur.</span><span class="sxs-lookup"><span data-stu-id="69c5b-132">Creates an inbound NAT rule configuration for a load balancer.</span></span> |
| [<span data-ttu-id="69c5b-133">AzureRmLoadBalancer yeni</span><span class="sxs-lookup"><span data-stu-id="69c5b-133">New-AzureRmLoadBalancer</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancer) | <span data-ttu-id="69c5b-134">Bir yük dengeleyici oluşturur.</span><span class="sxs-lookup"><span data-stu-id="69c5b-134">Creates a load balancer.</span></span> |
| [<span data-ttu-id="69c5b-135">AzureRmNetworkSecurityRuleConfig yeni</span><span class="sxs-lookup"><span data-stu-id="69c5b-135">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="69c5b-136">Bir ağ güvenlik grubu kural yapılandırması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="69c5b-136">Creates a network security group rule configuration.</span></span> <span data-ttu-id="69c5b-137">Merhaba NSG oluşturulduğunda bu kullanılan toocreate bir NSG kuralı yapılandırmadır.</span><span class="sxs-lookup"><span data-stu-id="69c5b-137">This configuration is used toocreate an NSG rule when hello NSG is created.</span></span> |
| [<span data-ttu-id="69c5b-138">AzureRmNetworkSecurityGroup yeni</span><span class="sxs-lookup"><span data-stu-id="69c5b-138">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="69c5b-139">Bir ağ güvenlik grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="69c5b-139">Creates a network security group.</span></span> |
| [<span data-ttu-id="69c5b-140">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="69c5b-140">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="69c5b-141">Alt ağ bilgilerini alır.</span><span class="sxs-lookup"><span data-stu-id="69c5b-141">Gets subnet information.</span></span> <span data-ttu-id="69c5b-142">Bu bilgiler, bir ağ arabirimi oluşturulurken kullanılır.</span><span class="sxs-lookup"><span data-stu-id="69c5b-142">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="69c5b-143">AzureRmNetworkInterface yeni</span><span class="sxs-lookup"><span data-stu-id="69c5b-143">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="69c5b-144">Bir ağ arabirimi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="69c5b-144">Creates a network interface.</span></span> |
| [<span data-ttu-id="69c5b-145">AzureRmVMConfig yeni</span><span class="sxs-lookup"><span data-stu-id="69c5b-145">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="69c5b-146">Bir VM yapılandırması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="69c5b-146">Creates a VM configuration.</span></span> <span data-ttu-id="69c5b-147">Bu yapılandırma VM adı, işletim sistemi ve yönetici kimlik bilgileri gibi bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="69c5b-147">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="69c5b-148">Merhaba yapılandırma VM oluşturma sırasında kullanılır.</span><span class="sxs-lookup"><span data-stu-id="69c5b-148">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="69c5b-149">Yeni-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="69c5b-149">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="69c5b-150">Bir sanal makine oluşturun.</span><span class="sxs-lookup"><span data-stu-id="69c5b-150">Create a virtual machine.</span></span> |
|[<span data-ttu-id="69c5b-151">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="69c5b-151">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="69c5b-152">Bir kaynak grubu ve içerdiği tüm kaynaklar kaldırır.</span><span class="sxs-lookup"><span data-stu-id="69c5b-152">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="69c5b-153">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="69c5b-153">Next steps</span></span>

<span data-ttu-id="69c5b-154">Hello Azure PowerShell modülü hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="69c5b-154">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="69c5b-155">Ek sanal makine PowerShell komut dosyası örnekleri hello bulunabilir [Azure Windows VM belgelerine](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="69c5b-155">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
