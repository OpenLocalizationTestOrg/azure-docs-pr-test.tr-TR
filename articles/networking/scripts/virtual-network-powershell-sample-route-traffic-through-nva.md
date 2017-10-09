---
title: "aaaAzure PowerShell komut dosyası örneği - rota trafiği ağ sanal gereç aracılığıyla | Microsoft Docs"
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
ms.openlocfilehash: 3b999f3289d654c00d5becb973e2883896457d52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="route-traffic-through-a-network-virtual-appliance"></a><span data-ttu-id="9668a-103">Bir ağ sanal gereç yoluyla trafiği yönlendirme</span><span class="sxs-lookup"><span data-stu-id="9668a-103">Route traffic through a network virtual appliance</span></span>

<span data-ttu-id="9668a-104">Bu komut dosyası örneği ön uç ve arka uç alt ağları ile bir sanal ağ oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9668a-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="9668a-105">Ayrıca hello iki alt ağlar arasında etkin tooroute trafiğinin iletme IP ile VM oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9668a-105">It also creates a VM with IP forwarding enabled tooroute traffic between hello two subnets.</span></span> <span data-ttu-id="9668a-106">Merhaba komut dosyasını çalıştırdıktan sonra bir güvenlik duvarı uygulaması toohello VM gibi ağ yazılım dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9668a-106">After running hello script you can deploy network software, such as a firewall application, toohello VM.</span></span>

<span data-ttu-id="9668a-107">Gerekirse, Azure PowerShell hello yönerge kullanarak bulunan hello hello yükleyin [Azure PowerShell Kılavuzu](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/)ve ardından çalıştırın `Login-AzureRmAccount` toocreate Azure ile bir bağlantı.</span><span class="sxs-lookup"><span data-stu-id="9668a-107">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="9668a-108">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="9668a-108">Sample script</span></span>


[!code-powershell[main](../../../powershell_scripts/virtual-network/route-traffic-through-nva/route-traffic-through-nva.ps1 "Route traffic through a network virtual appliance")]

## <a name="clean-up-deployment"></a><span data-ttu-id="9668a-109">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="9668a-109">Clean up deployment</span></span> 

<span data-ttu-id="9668a-110">Çalışma hello aşağıdaki tooremove hello kaynak grubu, VM ve tüm ilişkili kaynakları komutu.</span><span class="sxs-lookup"><span data-stu-id="9668a-110">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```
## <a name="script-explanation"></a><span data-ttu-id="9668a-111">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="9668a-111">Script explanation</span></span>

<span data-ttu-id="9668a-112">Bu komut dosyası komutları toocreate aşağıdaki hello bir kaynak grubu, sanal ağ ve ağ güvenlik grupları kullanır.</span><span class="sxs-lookup"><span data-stu-id="9668a-112">This script uses hello following commands toocreate a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="9668a-113">Her komut hello tablosundaki toocommand özgü belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="9668a-113">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="9668a-114">Komut</span><span class="sxs-lookup"><span data-stu-id="9668a-114">Command</span></span> | <span data-ttu-id="9668a-115">Notlar</span><span class="sxs-lookup"><span data-stu-id="9668a-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="9668a-116">Yeni-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="9668a-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup)  | <span data-ttu-id="9668a-117">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9668a-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="9668a-118">Yeni-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="9668a-118">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="9668a-119">Bir Azure sanal ağı ve ön uç alt ağı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9668a-119">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="9668a-120">AzureRmVirtualNetworkSubnetConfig yeni</span><span class="sxs-lookup"><span data-stu-id="9668a-120">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="9668a-121">Arka uç ve DMZ alt ağlar oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9668a-121">Creates back-end and DMZ subnets.</span></span> |
| [<span data-ttu-id="9668a-122">AzureRmPublicIpAddress yeni</span><span class="sxs-lookup"><span data-stu-id="9668a-122">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="9668a-123">Ortak IP adresi tooaccess hello VM Internet hello oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9668a-123">Creates a public IP address tooaccess hello VM from hello Internet.</span></span> |
| [<span data-ttu-id="9668a-124">AzureRmNetworkInterface yeni</span><span class="sxs-lookup"><span data-stu-id="9668a-124">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="9668a-125">Bir sanal ağ arabirimi ve onu için IP iletimini etkinleştirme oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9668a-125">Creates a virtual network interface and enable IP forwarding for it.</span></span> |
| [<span data-ttu-id="9668a-126">AzureRmNetworkSecurityGroup yeni</span><span class="sxs-lookup"><span data-stu-id="9668a-126">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="9668a-127">Bir ağ güvenlik grubu (NSG) oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9668a-127">Creates a network security group (NSG).</span></span> |
| [<span data-ttu-id="9668a-128">AzureRmNetworkSecurityRuleConfig yeni</span><span class="sxs-lookup"><span data-stu-id="9668a-128">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="9668a-129">HTTP ve HTTPS bağlantı noktalarını toohello VM gelene izin ver NSG kuralları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9668a-129">Creates NSG rules that allow HTTP and HTTPS ports inbound toohello VM.</span></span> |
| [<span data-ttu-id="9668a-130">Set-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="9668a-130">Set-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig)| <span data-ttu-id="9668a-131">Nsg'ler ilişkilendirilmiş bir hello ve rota toosubnets tabloları.</span><span class="sxs-lookup"><span data-stu-id="9668a-131">Associates hello NSGs and route tables toosubnets.</span></span> |
| [<span data-ttu-id="9668a-132">AzureRmRouteTable yeni</span><span class="sxs-lookup"><span data-stu-id="9668a-132">New-AzureRmRouteTable</span></span>](/powershell/module/azurerm.network/new-azurermroutetable)| <span data-ttu-id="9668a-133">Tüm yollar için yol tablosu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9668a-133">Creates a route table for all routes.</span></span> |
| [<span data-ttu-id="9668a-134">AzureRMRouteConfig yeni</span><span class="sxs-lookup"><span data-stu-id="9668a-134">New-AzureRMRouteConfig</span></span>](/powershell/module/azurerm.network/new-azurermrouteconfig)| <span data-ttu-id="9668a-135">Yollar tooroute trafiği alt ağlar arasında ve hello Internet üzerinden hello VM oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9668a-135">Creates routes tooroute traffic between subnets and hello Internet through hello VM.</span></span> |
| [<span data-ttu-id="9668a-136">Yeni-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="9668a-136">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="9668a-137">Bir sanal makine oluşturur ve hello NIC tooit ekler.</span><span class="sxs-lookup"><span data-stu-id="9668a-137">Creates a virtual machine and attaches hello NIC tooit.</span></span> <span data-ttu-id="9668a-138">Bu komut ayrıca hello sanal makine görüntü toouse ve yönetici kimlik bilgilerini belirtir.</span><span class="sxs-lookup"><span data-stu-id="9668a-138">This command also specifies hello virtual machine image toouse and administrative credentials.</span></span> |
| [<span data-ttu-id="9668a-139">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="9668a-139">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup)  | <span data-ttu-id="9668a-140">Bir kaynak grubu ve içerdiği tüm kaynakları siler.</span><span class="sxs-lookup"><span data-stu-id="9668a-140">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9668a-141">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9668a-141">Next steps</span></span>

<span data-ttu-id="9668a-142">Hello Azure PowerShell hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9668a-142">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="9668a-143">Ek ağ PowerShell komut dosyası örnekleri hello bulunabilir [Azure ağ genel görünümü belgelerine](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9668a-143">Additional networking PowerShell script samples can be found in hello [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
