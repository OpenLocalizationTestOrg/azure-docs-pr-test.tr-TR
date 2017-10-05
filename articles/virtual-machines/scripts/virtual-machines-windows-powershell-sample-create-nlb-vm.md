---
title: "Azure PowerShell Betiği örnek - Windows VM NLB oluşturun. | Microsoft Docs"
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
ms.openlocfilehash: 25bcbbcd1615e01a384825d7bd1582a528e91f71
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="load-balance-traffic-between-highly-available-virtual-machines"></a><span data-ttu-id="c3578-103">Yüksek oranda kullanılabilir sanal makineler arasında Yük Dengelemesi trafiği</span><span class="sxs-lookup"><span data-stu-id="c3578-103">Load balance traffic between highly available virtual machines</span></span>

<span data-ttu-id="c3578-104">Bu komut dosyası örneği yüksek oranda kullanılabilir yapılandırılmış birkaç Windows Server 2016 sanal makineleri çalıştırmak ve dengeli yapılandırma yüklemek için gereken her şeyi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c3578-104">This script sample creates everything needed to run several Windows Server 2016 virtual machines configured in a highly available and load balanced configuration.</span></span> <span data-ttu-id="c3578-105">Betiği çalıştırdıktan sonra üç sanal makineler, birleştirilmiş bir Azure kullanılabilirlik kümesi için ve bir Azure yük dengeleyici üzerinden erişilebilir olacaktır.</span><span class="sxs-lookup"><span data-stu-id="c3578-105">After running the script, you will have three virtual machines, joined to an Azure Availability Set, and accessible through an Azure Load Balancer.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="c3578-106">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="c3578-106">Sample script</span></span>

<span data-ttu-id="c3578-107">[!code-powershell[Ana](../../../powershell_scripts/virtual-machine/create-vm-nlb/create-vm-nlb.ps1 "VM NLB oluşturma")]</span><span class="sxs-lookup"><span data-stu-id="c3578-107">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-nlb/create-vm-nlb.ps1 "Create VM NLB")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="c3578-108">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="c3578-108">Clean up deployment</span></span> 

<span data-ttu-id="c3578-109">Kaynak grubu, VM ve tüm ilgili kaynaklar kaldırmak için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="c3578-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="c3578-110">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="c3578-110">Script explanation</span></span>

<span data-ttu-id="c3578-111">Bu komut dosyası dağıtımı oluşturmak için aşağıdaki komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="c3578-111">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="c3578-112">Komut belirli belgeleri tablo bağlanan her öğe.</span><span class="sxs-lookup"><span data-stu-id="c3578-112">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="c3578-113">Komut</span><span class="sxs-lookup"><span data-stu-id="c3578-113">Command</span></span> | <span data-ttu-id="c3578-114">Notlar</span><span class="sxs-lookup"><span data-stu-id="c3578-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c3578-115">Yeni-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c3578-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="c3578-116">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c3578-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="c3578-117">AzureRmVirtualNetworkSubnetConfig yeni</span><span class="sxs-lookup"><span data-stu-id="c3578-117">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="c3578-118">Bir alt ağ yapılandırması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c3578-118">Creates a subnet configuration.</span></span> <span data-ttu-id="c3578-119">Bu yapılandırma sanal ağ oluşturma işlemine kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c3578-119">This configuration is used with the virtual network creation process.</span></span> |
| [<span data-ttu-id="c3578-120">Yeni-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="c3578-120">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="c3578-121">Sanal ağ oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c3578-121">Creates a virtual network.</span></span> |
| [<span data-ttu-id="c3578-122">AzureRmPublicIpAddress yeni</span><span class="sxs-lookup"><span data-stu-id="c3578-122">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="c3578-123">Bir ortak IP adresi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c3578-123">Creates a public IP address.</span></span> |
| [<span data-ttu-id="c3578-124">AzureRmLoadBalancerFrontendIpConfig yeni</span><span class="sxs-lookup"><span data-stu-id="c3578-124">New-AzureRmLoadBalancerFrontendIpConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig) | <span data-ttu-id="c3578-125">Bir yük dengeleyici için bir ön uç IP yapılandırmasını oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c3578-125">Creates a front-end IP configuration for a load balancer.</span></span> |
| [<span data-ttu-id="c3578-126">AzureRmLoadBalancerBackendAddressPoolConfig yeni</span><span class="sxs-lookup"><span data-stu-id="c3578-126">New-AzureRmLoadBalancerBackendAddressPoolConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig) | <span data-ttu-id="c3578-127">Bir yük dengeleyici için arka uç adres havuzu yapılandırması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c3578-127">Creates a backend address pool configuration for a load balancer.</span></span> |
| [<span data-ttu-id="c3578-128">AzureRmLoadBalancerProbeConfig yeni</span><span class="sxs-lookup"><span data-stu-id="c3578-128">New-AzureRmLoadBalancerProbeConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerprobeconfig) | <span data-ttu-id="c3578-129">Bir yük dengeleyici için bir araştırma yapılandırma oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c3578-129">Creates a probe configuration for a load balancer.</span></span> |
| [<span data-ttu-id="c3578-130">AzureRmLoadBalancerRuleConfig yeni</span><span class="sxs-lookup"><span data-stu-id="c3578-130">New-AzureRmLoadBalancerRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerruleconfig) | <span data-ttu-id="c3578-131">Bir yük dengeleyici için bir kural yapılandırma oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c3578-131">Creates a rule configuration for a load balancer.</span></span> |
| [<span data-ttu-id="c3578-132">AzureRmLoadBalancerInboundNatRuleConfig yeni</span><span class="sxs-lookup"><span data-stu-id="c3578-132">New-AzureRmLoadBalancerInboundNatRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerinboundnatruleconfig) | <span data-ttu-id="c3578-133">Bir yük dengeleyici için bir gelen NAT kuralı yapılandırmasını oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c3578-133">Creates an inbound NAT rule configuration for a load balancer.</span></span> |
| [<span data-ttu-id="c3578-134">AzureRmLoadBalancer yeni</span><span class="sxs-lookup"><span data-stu-id="c3578-134">New-AzureRmLoadBalancer</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancer) | <span data-ttu-id="c3578-135">Bir yük dengeleyici oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c3578-135">Creates a load balancer.</span></span> |
| [<span data-ttu-id="c3578-136">AzureRmNetworkSecurityRuleConfig yeni</span><span class="sxs-lookup"><span data-stu-id="c3578-136">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="c3578-137">Bir ağ güvenlik grubu kural yapılandırması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c3578-137">Creates a network security group rule configuration.</span></span> <span data-ttu-id="c3578-138">Bu yapılandırma, NSG oluşturulduğunda bir NSG kuralı oluşturmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c3578-138">This configuration is used to create an NSG rule when the NSG is created.</span></span> |
| [<span data-ttu-id="c3578-139">AzureRmNetworkSecurityGroup yeni</span><span class="sxs-lookup"><span data-stu-id="c3578-139">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="c3578-140">Bir ağ güvenlik grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c3578-140">Creates a network security group.</span></span> |
| [<span data-ttu-id="c3578-141">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="c3578-141">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="c3578-142">Alt ağ bilgilerini alır.</span><span class="sxs-lookup"><span data-stu-id="c3578-142">Gets subnet information.</span></span> <span data-ttu-id="c3578-143">Bu bilgiler, bir ağ arabirimi oluşturulurken kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c3578-143">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="c3578-144">AzureRmNetworkInterface yeni</span><span class="sxs-lookup"><span data-stu-id="c3578-144">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="c3578-145">Bir ağ arabirimi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c3578-145">Creates a network interface.</span></span> |
| [<span data-ttu-id="c3578-146">AzureRmVMConfig yeni</span><span class="sxs-lookup"><span data-stu-id="c3578-146">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="c3578-147">Bir VM yapılandırması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c3578-147">Creates a VM configuration.</span></span> <span data-ttu-id="c3578-148">Bu yapılandırma VM adı, işletim sistemi ve yönetici kimlik bilgileri gibi bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="c3578-148">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="c3578-149">Yapılandırma VM oluşturma sırasında kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c3578-149">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="c3578-150">Yeni-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="c3578-150">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="c3578-151">Bir sanal makine oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c3578-151">Create a virtual machine.</span></span> |
|[<span data-ttu-id="c3578-152">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c3578-152">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="c3578-153">Bir kaynak grubu ve içerdiği tüm kaynaklar kaldırır.</span><span class="sxs-lookup"><span data-stu-id="c3578-153">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c3578-154">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c3578-154">Next steps</span></span>

<span data-ttu-id="c3578-155">Azure PowerShell modülü hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c3578-155">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="c3578-156">Ek sanal makine PowerShell komut dosyası örnekleri bulunabilir [Azure Windows VM belgelerine](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c3578-156">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
