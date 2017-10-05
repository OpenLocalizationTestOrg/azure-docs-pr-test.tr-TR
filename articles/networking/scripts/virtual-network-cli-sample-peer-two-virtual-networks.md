---
title: "Azure CLI komut dosyası örneği - eş iki sanal ağlar | Microsoft Docs"
description: "Azure CLI komut dosyası örneği - eş iki sanal ağlar"
services: virtual-network
documentationcenter: virtual-network
author: KumudD
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 07/07/2017
ms.author: kumud
ms.openlocfilehash: a2b8fda288072e2fb0087988bbd68d3e4d9031d8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="peer-two-virtual-networks"></a><span data-ttu-id="e5b5f-103">Eş iki sanal ağlar</span><span class="sxs-lookup"><span data-stu-id="e5b5f-103">Peer two virtual networks</span></span>

<span data-ttu-id="e5b5f-104">Bu komut dosyasını oluşturur ve iki sanal ağlarda aynı bölge trhough Azure ağı bağlanır.</span><span class="sxs-lookup"><span data-stu-id="e5b5f-104">This script creates and connects two virtual networks in the same region trhough the Azure network.</span></span> <span data-ttu-id="e5b5f-105">Komut dosyasını çalıştırdıktan sonra iki sanal ağ arasında eşleme oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e5b5f-105">After running the script, you will create a peering between two virtual networks.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


## <a name="sample-script"></a><span data-ttu-id="e5b5f-106">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="e5b5f-106">Sample script</span></span>

<span data-ttu-id="e5b5f-107">[!code-azurecli-interactive[Ana](../../../cli_scripts/virtual-network/peer-two-virtual-networks/peer-two-virtual-networks.sh "iki ağ eş")]</span><span class="sxs-lookup"><span data-stu-id="e5b5f-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/peer-two-virtual-networks/peer-two-virtual-networks.sh "Peer two networks")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="e5b5f-108">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="e5b5f-108">Clean up deployment</span></span> 

<span data-ttu-id="e5b5f-109">Kaynak grubu, VM ve tüm ilgili kaynaklar kaldırmak için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e5b5f-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="e5b5f-110">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="e5b5f-110">Script explanation</span></span>

<span data-ttu-id="e5b5f-111">Bu komut, bir kaynak grubu, sanal makine ve tüm ilgili kaynaklar oluşturmak için aşağıdaki komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="e5b5f-111">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="e5b5f-112">Komut belirli belgeleri tablo bağlanan her komut.</span><span class="sxs-lookup"><span data-stu-id="e5b5f-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="e5b5f-113">Komut</span><span class="sxs-lookup"><span data-stu-id="e5b5f-113">Command</span></span> | <span data-ttu-id="e5b5f-114">Notlar</span><span class="sxs-lookup"><span data-stu-id="e5b5f-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e5b5f-115">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="e5b5f-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="e5b5f-116">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e5b5f-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="e5b5f-117">az ağ vnet oluşturma</span><span class="sxs-lookup"><span data-stu-id="e5b5f-117">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="e5b5f-118">Bir Azure sanal ağ ve alt ağ oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e5b5f-118">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="e5b5f-119">az ağ vnet eşlemesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="e5b5f-119">az network vnet peering create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet/peering#create) | <span data-ttu-id="e5b5f-120">İki sanal ağ arasında eşleme oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e5b5f-120">Creates a peering between two virtual networks.</span></span>  |
| [<span data-ttu-id="e5b5f-121">az grubu Sil</span><span class="sxs-lookup"><span data-stu-id="e5b5f-121">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="e5b5f-122">Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler.</span><span class="sxs-lookup"><span data-stu-id="e5b5f-122">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e5b5f-123">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e5b5f-123">Next steps</span></span>

<span data-ttu-id="e5b5f-124">Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e5b5f-124">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="e5b5f-125">Ek ağ CLI kod örnekleri bulunabilir [Azure ağ genel görünümü belgelerine](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="e5b5f-125">Additional networking CLI script samples can be found in the [Azure Networking Overview documentation](../cli-samples.md).</span></span>
