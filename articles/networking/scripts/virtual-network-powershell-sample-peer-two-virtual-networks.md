---
title: "PowerShell komut dosyası örneği - aaaAzure eş iki sanal ağ | Microsoft Docs"
description: "Azure PowerShell Betiği örnek - eş iki sanal ağlar"
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
ms.openlocfilehash: 8b66085c35de2fc30bcef57a00d7d370911d1f3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="peer-two-virtual-networks"></a><span data-ttu-id="389b0-103">Eş iki sanal ağlar</span><span class="sxs-lookup"><span data-stu-id="389b0-103">Peer two virtual networks</span></span>

<span data-ttu-id="389b0-104">Bu komut dosyası oluşturur ve hello içindeki iki sanal ağları birbirine bağlayan aynı bölge trhough hello Azure ağı.</span><span class="sxs-lookup"><span data-stu-id="389b0-104">This script creates and connects two virtual networks in hello same region trhough hello Azure network.</span></span> <span data-ttu-id="389b0-105">Merhaba komut dosyasını çalıştırdıktan sonra iki sanal ağ arasında eşleme oluşturur.</span><span class="sxs-lookup"><span data-stu-id="389b0-105">After running hello script, you will create a peering between two virtual networks.</span></span>

<span data-ttu-id="389b0-106">Gerekirse, Azure PowerShell hello yönerge kullanarak bulunan hello hello yükleyin [Azure PowerShell Kılavuzu](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/)ve ardından çalıştırın `Login-AzureRmAccount` toocreate Azure ile bir bağlantı.</span><span class="sxs-lookup"><span data-stu-id="389b0-106">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="389b0-107">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="389b0-107">Sample script</span></span>

[!code-azurepowershell[main](../../../powershell_scripts/virtual-network/peer-two-virtual-networks/peer-two-virtual-networks.ps1 "Peer two networks")]

## <a name="clean-up-deployment"></a><span data-ttu-id="389b0-108">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="389b0-108">Clean up deployment</span></span> 

<span data-ttu-id="389b0-109">Çalışma hello aşağıdaki tooremove hello kaynak grubu, VM ve tüm ilişkili kaynakları komutu.</span><span class="sxs-lookup"><span data-stu-id="389b0-109">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="389b0-110">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="389b0-110">Script explanation</span></span>

<span data-ttu-id="389b0-111">Bu komut dosyası komutları toocreate bir kaynak grubu, sanal makine aşağıdaki hello kullanır ve ilişkili tüm kaynakları.</span><span class="sxs-lookup"><span data-stu-id="389b0-111">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="389b0-112">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="389b0-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="389b0-113">Komut</span><span class="sxs-lookup"><span data-stu-id="389b0-113">Command</span></span> | <span data-ttu-id="389b0-114">Notlar</span><span class="sxs-lookup"><span data-stu-id="389b0-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="389b0-115">Yeni-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="389b0-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="389b0-116">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="389b0-116">Creates a resource group in which all resources are stored.</span></span> | 
| [<span data-ttu-id="389b0-117">Yeni-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="389b0-117">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork)| <span data-ttu-id="389b0-118">Bir Azure sanal ağ ve alt ağ oluşturur.</span><span class="sxs-lookup"><span data-stu-id="389b0-118">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="389b0-119">Ekleme AzureRmVirtualNetworkPeering</span><span class="sxs-lookup"><span data-stu-id="389b0-119">Add-AzureRmVirtualNetworkPeering</span></span>](/powershell/module/azurerm.network/add-azurermvirtualnetworkpeering) | <span data-ttu-id="389b0-120">İki sanal ağ arasında eşleme oluşturur.</span><span class="sxs-lookup"><span data-stu-id="389b0-120">Creates a peering between two virtual networks.</span></span>  |
| [<span data-ttu-id="389b0-121">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="389b0-121">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="389b0-122">Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler.</span><span class="sxs-lookup"><span data-stu-id="389b0-122">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="389b0-123">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="389b0-123">Next steps</span></span>

<span data-ttu-id="389b0-124">Hello Azure PowerShell hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="389b0-124">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="389b0-125">Ek ağ PowerShell komut dosyası örnekleri hello bulunabilir [Azure ağ genel görünümü belgelerine](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="389b0-125">Additional networking PowerShell script samples can be found in hello [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
