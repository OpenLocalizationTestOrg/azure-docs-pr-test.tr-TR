---
title: "Azure PowerShell komut dosyası örneği - rota trafiği ağ sanal gereç aracılığıyla | Microsoft Docs"
description: "Azure PowerShell komut dosyası örneği - güvenlik duvarı ağ sanal gereç yoluyla trafiği yönlendirme."
services: virtual-network
documentationcenter: virtual-network
author: georgewallace
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: powershell
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 05/16/2017
ms.author: gwallace
ms.openlocfilehash: 883d28dac72a66c2186d222f72b04d68e532cead
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="route-traffic-through-a-network-virtual-appliance"></a><span data-ttu-id="af10a-103">Bir ağ sanal gereç yoluyla trafiği yönlendirme</span><span class="sxs-lookup"><span data-stu-id="af10a-103">Route traffic through a network virtual appliance</span></span>

<span data-ttu-id="af10a-104">Bu komut dosyası örneği ön uç ve arka uç alt ağları ile bir sanal ağ oluşturur.</span><span class="sxs-lookup"><span data-stu-id="af10a-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="af10a-105">Ayrıca IP iletme iki alt ağlar arasında trafiği yönlendirmek için etkin olan bir VM oluşturur.</span><span class="sxs-lookup"><span data-stu-id="af10a-105">It also creates a VM with IP forwarding enabled to route traffic between the two subnets.</span></span> <span data-ttu-id="af10a-106">Komut dosyasını çalıştırdıktan sonra VM için bir güvenlik duvarı uygulaması gibi ağ yazılım dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="af10a-106">After running the script you can deploy network software, such as a firewall application, to the VM.</span></span>

<span data-ttu-id="af10a-107">Gerekirse, bulunan yönergeleri kullanarak Azure PowerShell'i yükleme [Azure PowerShell Kılavuzu](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/)ve ardından çalıştırın `Login-AzureRmAccount` Azure ile bir bağlantı oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="af10a-107">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="af10a-108">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="af10a-108">Sample script</span></span>


<span data-ttu-id="af10a-109">[!code-powershell[Ana](../../../powershell_scripts/virtual-network/route-traffic-through-nva/route-traffic-through-nva.ps1 "trafiği ağ sanal gereç aracılığıyla yönlendirmek")]</span><span class="sxs-lookup"><span data-stu-id="af10a-109">[!code-powershell[main](../../../powershell_scripts/virtual-network/route-traffic-through-nva/route-traffic-through-nva.ps1 "Route traffic through a network virtual appliance")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="af10a-110">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="af10a-110">Clean up deployment</span></span> 

<span data-ttu-id="af10a-111">Kaynak grubu, VM ve tüm ilgili kaynaklar kaldırmak için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="af10a-111">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```
## <a name="script-explanation"></a><span data-ttu-id="af10a-112">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="af10a-112">Script explanation</span></span>

<span data-ttu-id="af10a-113">Bu komut, bir kaynak grubu, sanal ağ ve ağ güvenlik grupları oluşturmak için aşağıdaki komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="af10a-113">This script uses the following commands to create a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="af10a-114">Komut özgü belgelere Tablo bağlantıları her komut.</span><span class="sxs-lookup"><span data-stu-id="af10a-114">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="af10a-115">Komut</span><span class="sxs-lookup"><span data-stu-id="af10a-115">Command</span></span> | <span data-ttu-id="af10a-116">Notlar</span><span class="sxs-lookup"><span data-stu-id="af10a-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="af10a-117">Yeni-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="af10a-117">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup)  | <span data-ttu-id="af10a-118">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="af10a-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="af10a-119">Yeni-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="af10a-119">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="af10a-120">Bir Azure sanal ağı ve ön uç alt ağı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="af10a-120">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="af10a-121">AzureRmVirtualNetworkSubnetConfig yeni</span><span class="sxs-lookup"><span data-stu-id="af10a-121">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="af10a-122">Arka uç ve DMZ alt ağlar oluşturur.</span><span class="sxs-lookup"><span data-stu-id="af10a-122">Creates back-end and DMZ subnets.</span></span> |
| [<span data-ttu-id="af10a-123">AzureRmPublicIpAddress yeni</span><span class="sxs-lookup"><span data-stu-id="af10a-123">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="af10a-124">VM Internet'ten erişmek için genel bir IP adresi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="af10a-124">Creates a public IP address to access the VM from the Internet.</span></span> |
| [<span data-ttu-id="af10a-125">AzureRmNetworkInterface yeni</span><span class="sxs-lookup"><span data-stu-id="af10a-125">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="af10a-126">Bir sanal ağ arabirimi ve onu için IP iletimini etkinleştirme oluşturur.</span><span class="sxs-lookup"><span data-stu-id="af10a-126">Creates a virtual network interface and enable IP forwarding for it.</span></span> |
| [<span data-ttu-id="af10a-127">AzureRmNetworkSecurityGroup yeni</span><span class="sxs-lookup"><span data-stu-id="af10a-127">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="af10a-128">Bir ağ güvenlik grubu (NSG) oluşturur.</span><span class="sxs-lookup"><span data-stu-id="af10a-128">Creates a network security group (NSG).</span></span> |
| [<span data-ttu-id="af10a-129">AzureRmNetworkSecurityRuleConfig yeni</span><span class="sxs-lookup"><span data-stu-id="af10a-129">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="af10a-130">HTTP ve HTTPS bağlantı noktalarını VM'ye gelen izin NSG kuralları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="af10a-130">Creates NSG rules that allow HTTP and HTTPS ports inbound to the VM.</span></span> |
| [<span data-ttu-id="af10a-131">Set-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="af10a-131">Set-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig)| <span data-ttu-id="af10a-132">Nsg'ler ve alt ağlara yol tablolarını ilişkilendirir.</span><span class="sxs-lookup"><span data-stu-id="af10a-132">Associates the NSGs and route tables to subnets.</span></span> |
| [<span data-ttu-id="af10a-133">AzureRmRouteTable yeni</span><span class="sxs-lookup"><span data-stu-id="af10a-133">New-AzureRmRouteTable</span></span>](/powershell/module/azurerm.network/new-azurermroutetable)| <span data-ttu-id="af10a-134">Tüm yollar için yol tablosu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="af10a-134">Creates a route table for all routes.</span></span> |
| [<span data-ttu-id="af10a-135">AzureRMRouteConfig yeni</span><span class="sxs-lookup"><span data-stu-id="af10a-135">New-AzureRMRouteConfig</span></span>](/powershell/module/azurerm.network/new-azurermrouteconfig)| <span data-ttu-id="af10a-136">Alt ağlar ve VM ile Internet arasında trafiği yönlendirmek için yollar oluşturur.</span><span class="sxs-lookup"><span data-stu-id="af10a-136">Creates routes to route traffic between subnets and the Internet through the VM.</span></span> |
| [<span data-ttu-id="af10a-137">Yeni-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="af10a-137">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="af10a-138">Bir sanal makine oluşturur ve NIC ekler.</span><span class="sxs-lookup"><span data-stu-id="af10a-138">Creates a virtual machine and attaches the NIC to it.</span></span> <span data-ttu-id="af10a-139">Bu komut ayrıca kullanmak için sanal makine görüntüsü ve yönetici kimlik bilgilerini belirtir.</span><span class="sxs-lookup"><span data-stu-id="af10a-139">This command also specifies the virtual machine image to use and administrative credentials.</span></span> |
| [<span data-ttu-id="af10a-140">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="af10a-140">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup)  | <span data-ttu-id="af10a-141">Bir kaynak grubu ve içerdiği tüm kaynakları siler.</span><span class="sxs-lookup"><span data-stu-id="af10a-141">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="af10a-142">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="af10a-142">Next steps</span></span>

<span data-ttu-id="af10a-143">Azure PowerShell hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="af10a-143">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="af10a-144">Ek ağ PowerShell komut dosyası örnekleri bulunabilir [Azure ağ genel görünümü belgelerine](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="af10a-144">Additional networking PowerShell script samples can be found in the [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>