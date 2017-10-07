---
title: "PowerShell komut dosyası örneği - aaaAzure çok katmanlı uygulamalar için bir ağ oluşturma | Microsoft Docs"
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
ms.openlocfilehash: 46d6d16dc5dbc8be467359f31346f017727b1abe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-network-for-multi-tier-applications"></a><span data-ttu-id="7696f-103">Çok katmanlı uygulamalar için bir ağ oluşturma</span><span class="sxs-lookup"><span data-stu-id="7696f-103">Create a network for multi-tier applications</span></span>

<span data-ttu-id="7696f-104">Bu komut dosyası örneği ön uç ve arka uç alt ağları ile bir sanal ağ oluşturur.</span><span class="sxs-lookup"><span data-stu-id="7696f-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="7696f-105">Trafik toohello ön uç alt sınırlı tooHTTP ve SSH, trafik toohello sırasında arka uç alt sınırlı tooMySQL, bağlantı noktası 3306.</span><span class="sxs-lookup"><span data-stu-id="7696f-105">Traffic toohello front-end subnet is limited tooHTTP and SSH, while traffic toohello back-end subnet is limited tooMySQL, port 3306.</span></span> <span data-ttu-id="7696f-106">Çalışan hello betik sonra iki sanal makine, bir web sunucusu ve MySQL yazılım dağıtabilirsiniz her alt ağda gerekir.</span><span class="sxs-lookup"><span data-stu-id="7696f-106">After running hello script, you will have two virtual machines, one in each subnet that you can deploy web server and MySQL software to.</span></span>

<span data-ttu-id="7696f-107">Gerekirse, Azure PowerShell hello yönerge kullanarak bulunan hello hello yükleyin [Azure PowerShell Kılavuzu](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/)ve ardından çalıştırın `Login-AzureRmAccount` toocreate Azure ile bir bağlantı.</span><span class="sxs-lookup"><span data-stu-id="7696f-107">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="7696f-108">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="7696f-108">Sample script</span></span>


[!code-powershell[main](../../../powershell_scripts/virtual-network/virtual-network-multi-tier-application/virtual-network-multi-tier-application.ps1  "Virtual network for multi-tier application")]

## <a name="clean-up-deployment"></a><span data-ttu-id="7696f-109">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="7696f-109">Clean up deployment</span></span> 

<span data-ttu-id="7696f-110">Çalışma hello aşağıdaki tooremove hello kaynak grubu, VM ve tüm ilişkili kaynakları komutu.</span><span class="sxs-lookup"><span data-stu-id="7696f-110">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="7696f-111">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="7696f-111">Script explanation</span></span>

<span data-ttu-id="7696f-112">Bu komut dosyası komutları toocreate aşağıdaki hello bir kaynak grubu, sanal ağ ve ağ güvenlik grupları kullanır.</span><span class="sxs-lookup"><span data-stu-id="7696f-112">This script uses hello following commands toocreate a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="7696f-113">Her komut hello tablosundaki toocommand özgü belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="7696f-113">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="7696f-114">Komut</span><span class="sxs-lookup"><span data-stu-id="7696f-114">Command</span></span> | <span data-ttu-id="7696f-115">Notlar</span><span class="sxs-lookup"><span data-stu-id="7696f-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="7696f-116">Yeni-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="7696f-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="7696f-117">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="7696f-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="7696f-118">Yeni-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="7696f-118">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="7696f-119">Bir Azure sanal ağı ve ön uç alt ağı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="7696f-119">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="7696f-120">AzureRmVirtualNetworkSubnetConfig yeni</span><span class="sxs-lookup"><span data-stu-id="7696f-120">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="7696f-121">Bir arka uç alt ağı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="7696f-121">Creates a back-end subnet.</span></span> |
| [<span data-ttu-id="7696f-122">AzureRmPublicIpAddress yeni</span><span class="sxs-lookup"><span data-stu-id="7696f-122">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="7696f-123">Ortak IP adresi tooaccess hello VM Internet hello oluşturur.</span><span class="sxs-lookup"><span data-stu-id="7696f-123">Creates a public IP address tooaccess hello VM from hello Internet.</span></span> |
| [<span data-ttu-id="7696f-124">AzureRmNetworkInterface yeni</span><span class="sxs-lookup"><span data-stu-id="7696f-124">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="7696f-125">Sanal ağ arabirimi oluşturur ve bunları toohello sanal ağın ön uç ve arka uç alt ekler.</span><span class="sxs-lookup"><span data-stu-id="7696f-125">Creates virtual network interfaces and attaches them toohello virtual network's front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="7696f-126">AzureRmNetworkSecurityGroup yeni</span><span class="sxs-lookup"><span data-stu-id="7696f-126">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="7696f-127">İlişkili toohello ön uç ve arka uç alt ağlar, ağ güvenlik gruplarını (NSG) oluşturur.</span><span class="sxs-lookup"><span data-stu-id="7696f-127">Creates network security groups (NSG) that are associated toohello front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="7696f-128">AzureRmNetworkSecurityRuleConfig yeni</span><span class="sxs-lookup"><span data-stu-id="7696f-128">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) |<span data-ttu-id="7696f-129">İzin verme veya engelleme belirli bağlantı noktalarını toospecific alt NSG kuralları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="7696f-129">Creates NSG rules that allow or block specific ports toospecific subnets.</span></span> |
| [<span data-ttu-id="7696f-130">Yeni-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="7696f-130">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="7696f-131">Sanal makineler oluşturur ve NIC tooeach VM ekler.</span><span class="sxs-lookup"><span data-stu-id="7696f-131">Creates virtual machines and attaches a NIC tooeach VM.</span></span> <span data-ttu-id="7696f-132">Bu komut ayrıca hello sanal makine görüntü toouse ve yönetici kimlik bilgilerini belirtir.</span><span class="sxs-lookup"><span data-stu-id="7696f-132">This command also specifies hello virtual machine image toouse and administrative credentials.</span></span> |
| [<span data-ttu-id="7696f-133">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="7696f-133">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="7696f-134">Bir kaynak grubu ve içerdiği tüm kaynakları siler.</span><span class="sxs-lookup"><span data-stu-id="7696f-134">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="7696f-135">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7696f-135">Next steps</span></span>

<span data-ttu-id="7696f-136">Hello Azure PowerShell hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7696f-136">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="7696f-137">Ek ağ PowerShell komut dosyası örnekleri hello bulunabilir [Azure ağ genel görünümü belgelerine](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7696f-137">Additional networking PowerShell script samples can be found in hello [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
