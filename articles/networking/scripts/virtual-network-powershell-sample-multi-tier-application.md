---
title: "Azure PowerShell Betiği örnek - çok katmanlı uygulamalar için bir ağ oluşturun. | Microsoft Docs"
description: "Azure PowerShell Betiği örnek - çok katmanlı uygulamalar için bir sanal ağ oluşturun."
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
ms.openlocfilehash: ab49e78ef17b093d2bbe4e3276a1ece3a4247f91
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-network-for-multi-tier-applications"></a><span data-ttu-id="d919d-103">Çok katmanlı uygulamalar için bir ağ oluşturma</span><span class="sxs-lookup"><span data-stu-id="d919d-103">Create a network for multi-tier applications</span></span>

<span data-ttu-id="d919d-104">Bu komut dosyası örneği ön uç ve arka uç alt ağları ile bir sanal ağ oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d919d-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="d919d-105">Arka uç alt ağ trafiği MySQL, bağlantı noktası 3306 sınırlı olsa ön uç alt ağ trafiği HTTP ve SSH, ile sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="d919d-105">Traffic to the front-end subnet is limited to HTTP and SSH, while traffic to the back-end subnet is limited to MySQL, port 3306.</span></span> <span data-ttu-id="d919d-106">Betiği çalıştırdıktan sonra bir web sunucusu ve MySQL yazılım dağıtabilirsiniz her alt ağda iki sanal makineye sahip.</span><span class="sxs-lookup"><span data-stu-id="d919d-106">After running the script, you will have two virtual machines, one in each subnet that you can deploy web server and MySQL software to.</span></span>

<span data-ttu-id="d919d-107">Gerekirse, bulunan yönergeleri kullanarak Azure PowerShell'i yükleme [Azure PowerShell Kılavuzu](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/)ve ardından çalıştırın `Login-AzureRmAccount` Azure ile bir bağlantı oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="d919d-107">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="d919d-108">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="d919d-108">Sample script</span></span>


<span data-ttu-id="d919d-109">[!code-powershell[Ana](../../../powershell_scripts/virtual-network/virtual-network-multi-tier-application/virtual-network-multi-tier-application.ps1  "çok katmanlı uygulama için sanal ağ")]</span><span class="sxs-lookup"><span data-stu-id="d919d-109">[!code-powershell[main](../../../powershell_scripts/virtual-network/virtual-network-multi-tier-application/virtual-network-multi-tier-application.ps1  "Virtual network for multi-tier application")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="d919d-110">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="d919d-110">Clean up deployment</span></span> 

<span data-ttu-id="d919d-111">Kaynak grubu, VM ve tüm ilgili kaynaklar kaldırmak için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="d919d-111">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="d919d-112">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="d919d-112">Script explanation</span></span>

<span data-ttu-id="d919d-113">Bu komut, bir kaynak grubu, sanal ağ ve ağ güvenlik grupları oluşturmak için aşağıdaki komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="d919d-113">This script uses the following commands to create a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="d919d-114">Komut özgü belgelere Tablo bağlantıları her komut.</span><span class="sxs-lookup"><span data-stu-id="d919d-114">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="d919d-115">Komut</span><span class="sxs-lookup"><span data-stu-id="d919d-115">Command</span></span> | <span data-ttu-id="d919d-116">Notlar</span><span class="sxs-lookup"><span data-stu-id="d919d-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d919d-117">Yeni-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="d919d-117">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="d919d-118">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d919d-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="d919d-119">Yeni-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="d919d-119">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="d919d-120">Bir Azure sanal ağı ve ön uç alt ağı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d919d-120">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="d919d-121">AzureRmVirtualNetworkSubnetConfig yeni</span><span class="sxs-lookup"><span data-stu-id="d919d-121">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="d919d-122">Bir arka uç alt ağı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d919d-122">Creates a back-end subnet.</span></span> |
| [<span data-ttu-id="d919d-123">AzureRmPublicIpAddress yeni</span><span class="sxs-lookup"><span data-stu-id="d919d-123">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="d919d-124">VM Internet'ten erişmek için genel bir IP adresi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d919d-124">Creates a public IP address to access the VM from the Internet.</span></span> |
| [<span data-ttu-id="d919d-125">AzureRmNetworkInterface yeni</span><span class="sxs-lookup"><span data-stu-id="d919d-125">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="d919d-126">Sanal ağ arabirimi oluşturur ve bunları sanal ağın ön uç ve arka uç alt ağlara ekler.</span><span class="sxs-lookup"><span data-stu-id="d919d-126">Creates virtual network interfaces and attaches them to the virtual network's front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="d919d-127">AzureRmNetworkSecurityGroup yeni</span><span class="sxs-lookup"><span data-stu-id="d919d-127">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="d919d-128">Ağ ön uç ve arka uç alt ağlar için ilişkili güvenlik grupları (NSG) oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d919d-128">Creates network security groups (NSG) that are associated to the front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="d919d-129">AzureRmNetworkSecurityRuleConfig yeni</span><span class="sxs-lookup"><span data-stu-id="d919d-129">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) |<span data-ttu-id="d919d-130">İzin veren veya özel alt ağları için belirli bağlantı noktalarını engellemek NSG kuralları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d919d-130">Creates NSG rules that allow or block specific ports to specific subnets.</span></span> |
| [<span data-ttu-id="d919d-131">Yeni-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="d919d-131">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="d919d-132">Sanal makineler oluşturur ve her bir VM için bir NIC ekler.</span><span class="sxs-lookup"><span data-stu-id="d919d-132">Creates virtual machines and attaches a NIC to each VM.</span></span> <span data-ttu-id="d919d-133">Bu komut ayrıca kullanmak için sanal makine görüntüsü ve yönetici kimlik bilgilerini belirtir.</span><span class="sxs-lookup"><span data-stu-id="d919d-133">This command also specifies the virtual machine image to use and administrative credentials.</span></span> |
| [<span data-ttu-id="d919d-134">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="d919d-134">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="d919d-135">Bir kaynak grubu ve içerdiği tüm kaynakları siler.</span><span class="sxs-lookup"><span data-stu-id="d919d-135">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d919d-136">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d919d-136">Next steps</span></span>

<span data-ttu-id="d919d-137">Azure PowerShell hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d919d-137">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="d919d-138">Ek ağ PowerShell komut dosyası örnekleri bulunabilir [Azure ağ genel görünümü belgelerine](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d919d-138">Additional networking PowerShell script samples can be found in the [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>