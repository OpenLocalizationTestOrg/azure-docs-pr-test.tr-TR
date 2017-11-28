---
title: "aaaAzure PowerShell komut dosyası örneği - filtre VM ağ trafiğini | Microsoft Docs"
description: "Azure PowerShell Betiği örnek - gelen ve giden VM ağ trafiğini filtre."
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
ms.openlocfilehash: 39eae6a43a8dc7f9fc616ef3ec50f95443fd3547
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="filter-inbound-and-outbound-vm-network-traffic"></a><span data-ttu-id="c68b2-103">Gelen ve giden VM ağ trafiği filtreleme</span><span class="sxs-lookup"><span data-stu-id="c68b2-103">Filter inbound and outbound VM network traffic</span></span>

<span data-ttu-id="c68b2-104">Bu komut dosyası örneği ön uç ve arka uç alt ağları ile bir sanal ağ oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c68b2-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="c68b2-105">Gelen ağ trafiğini toohello ön uç alt sınırlı tooHTTP ve HTTPS, giden sırada trafik toohello hello arka uç alt ağından Internet izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="c68b2-105">Inbound network traffic toohello front-end subnet is limited tooHTTP, and HTTPS, while outbound traffic toohello Internet from hello back-end subnet is not permitted.</span></span> <span data-ttu-id="c68b2-106">Merhaba komut dosyasını çalıştırdıktan sonra iki NIC içeren bir sanal makine gerekir.</span><span class="sxs-lookup"><span data-stu-id="c68b2-106">After running hello script, you will have one virtual machine with two NICs.</span></span> <span data-ttu-id="c68b2-107">Her NIC'nin bağlı tooa farklı alt değil.</span><span class="sxs-lookup"><span data-stu-id="c68b2-107">Each NIC is connected tooa different subnet.</span></span>

<span data-ttu-id="c68b2-108">Gerekirse, Azure PowerShell hello yönerge kullanarak bulunan hello hello yükleyin [Azure PowerShell Kılavuzu](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/)ve ardından çalıştırın `Login-AzureRmAccount` toocreate Azure ile bir bağlantı.</span><span class="sxs-lookup"><span data-stu-id="c68b2-108">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="c68b2-109">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="c68b2-109">Sample script</span></span>


[!code-powershell[main](../../../powershell_scripts/virtual-network/filter-network-traffic/filter-network-traffic.ps1  "Filter VM network traffic")]

## <a name="clean-up-deployment"></a><span data-ttu-id="c68b2-110">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="c68b2-110">Clean up deployment</span></span> 

<span data-ttu-id="c68b2-111">Çalışma hello aşağıdaki tooremove hello kaynak grubu, VM ve tüm ilişkili kaynakları komutu.</span><span class="sxs-lookup"><span data-stu-id="c68b2-111">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="c68b2-112">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="c68b2-112">Script explanation</span></span>

<span data-ttu-id="c68b2-113">Bu komut dosyası komutları toocreate aşağıdaki hello bir kaynak grubu, sanal ağ ve ağ güvenlik grupları kullanır.</span><span class="sxs-lookup"><span data-stu-id="c68b2-113">This script uses hello following commands toocreate a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="c68b2-114">Her komut hello tablosundaki toocommand özgü belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="c68b2-114">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="c68b2-115">Komut</span><span class="sxs-lookup"><span data-stu-id="c68b2-115">Command</span></span> | <span data-ttu-id="c68b2-116">Notlar</span><span class="sxs-lookup"><span data-stu-id="c68b2-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c68b2-117">Yeni-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c68b2-117">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="c68b2-118">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c68b2-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="c68b2-119">AzureRmVirtualNetworkSubnetConfig yeni</span><span class="sxs-lookup"><span data-stu-id="c68b2-119">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="c68b2-120">Bir alt ağ yapılandırma nesnesi oluşturur</span><span class="sxs-lookup"><span data-stu-id="c68b2-120">Creates a subnet configuration object</span></span> |
| [<span data-ttu-id="c68b2-121">Yeni-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="c68b2-121">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="c68b2-122">Bir Azure sanal ağı ve ön uç alt ağı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c68b2-122">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="c68b2-123">AzureRmNetworkSecurityRuleConfig yeni</span><span class="sxs-lookup"><span data-stu-id="c68b2-123">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="c68b2-124">Tooa ağ güvenlik grubuna atanmış güvenlik kuralları toobe oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c68b2-124">Creates security rules toobe assigned tooa network security group.</span></span> |
| [<span data-ttu-id="c68b2-125">AzureRmNetworkSecurityGroup yeni</span><span class="sxs-lookup"><span data-stu-id="c68b2-125">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) |<span data-ttu-id="c68b2-126">İzin verme veya engelleme belirli bağlantı noktalarını toospecific alt NSG kuralları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c68b2-126">Creates NSG rules that allow or block specific ports toospecific subnets.</span></span> |
| [<span data-ttu-id="c68b2-127">Set-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="c68b2-127">Set-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="c68b2-128">Nsg'ler toosubnets ilişkilendirir.</span><span class="sxs-lookup"><span data-stu-id="c68b2-128">Associates NSGs toosubnets.</span></span> |
| [<span data-ttu-id="c68b2-129">AzureRmPublicIpAddress yeni</span><span class="sxs-lookup"><span data-stu-id="c68b2-129">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="c68b2-130">Ortak IP adresi tooaccess hello VM Internet hello oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c68b2-130">Creates a public IP address tooaccess hello VM from hello Internet.</span></span> |
| [<span data-ttu-id="c68b2-131">AzureRmNetworkInterface yeni</span><span class="sxs-lookup"><span data-stu-id="c68b2-131">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="c68b2-132">Sanal ağ arabirimi oluşturur ve bunları toohello sanal ağın ön uç ve arka uç alt ekler.</span><span class="sxs-lookup"><span data-stu-id="c68b2-132">Creates virtual network interfaces and attaches them toohello virtual network's front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="c68b2-133">AzureRmVMConfig yeni</span><span class="sxs-lookup"><span data-stu-id="c68b2-133">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="c68b2-134">Bir VM yapılandırması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c68b2-134">Creates a VM configuration.</span></span> <span data-ttu-id="c68b2-135">Bu yapılandırma VM adı, işletim sistemi ve yönetici kimlik bilgileri gibi bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="c68b2-135">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="c68b2-136">Merhaba yapılandırma VM oluşturma sırasında kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c68b2-136">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="c68b2-137">Yeni-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="c68b2-137">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="c68b2-138">Bir sanal makine oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c68b2-138">Create a virtual machine.</span></span> |
|[<span data-ttu-id="c68b2-139">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c68b2-139">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="c68b2-140">Bir kaynak grubu ve içerdiği tüm kaynaklar kaldırır.</span><span class="sxs-lookup"><span data-stu-id="c68b2-140">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c68b2-141">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c68b2-141">Next steps</span></span>

<span data-ttu-id="c68b2-142">Hello Azure PowerShell hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c68b2-142">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="c68b2-143">Ek ağ PowerShell komut dosyası örnekleri hello bulunabilir [Azure ağ genel görünümü belgelerine](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c68b2-143">Additional networking PowerShell script samples can be found in hello [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
