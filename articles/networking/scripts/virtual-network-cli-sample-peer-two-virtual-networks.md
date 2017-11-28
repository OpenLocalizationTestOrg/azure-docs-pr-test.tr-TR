---
title: "aaaAzure CLI komut dosyası örneği - iki sanal ağ eş | Microsoft Docs"
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
ms.openlocfilehash: 54dabb2b9e05951d10f1b6b4f61ca592ce11d364
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="peer-two-virtual-networks"></a><span data-ttu-id="8dc95-103">Eş iki sanal ağlar</span><span class="sxs-lookup"><span data-stu-id="8dc95-103">Peer two virtual networks</span></span>

<span data-ttu-id="8dc95-104">Bu komut dosyası oluşturur ve hello içindeki iki sanal ağları birbirine bağlayan aynı bölge trhough hello Azure ağı.</span><span class="sxs-lookup"><span data-stu-id="8dc95-104">This script creates and connects two virtual networks in hello same region trhough hello Azure network.</span></span> <span data-ttu-id="8dc95-105">Merhaba komut dosyasını çalıştırdıktan sonra iki sanal ağ arasında eşleme oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8dc95-105">After running hello script, you will create a peering between two virtual networks.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


## <a name="sample-script"></a><span data-ttu-id="8dc95-106">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="8dc95-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/peer-two-virtual-networks/peer-two-virtual-networks.sh "Peer two networks")]

## <a name="clean-up-deployment"></a><span data-ttu-id="8dc95-107">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="8dc95-107">Clean up deployment</span></span> 

<span data-ttu-id="8dc95-108">Çalışma hello aşağıdaki tooremove hello kaynak grubu, VM ve tüm ilişkili kaynakları komutu.</span><span class="sxs-lookup"><span data-stu-id="8dc95-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="8dc95-109">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="8dc95-109">Script explanation</span></span>

<span data-ttu-id="8dc95-110">Bu komut dosyası komutları toocreate bir kaynak grubu, sanal makine aşağıdaki hello kullanır ve ilişkili tüm kaynakları.</span><span class="sxs-lookup"><span data-stu-id="8dc95-110">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="8dc95-111">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="8dc95-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="8dc95-112">Komut</span><span class="sxs-lookup"><span data-stu-id="8dc95-112">Command</span></span> | <span data-ttu-id="8dc95-113">Notlar</span><span class="sxs-lookup"><span data-stu-id="8dc95-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="8dc95-114">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="8dc95-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="8dc95-115">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8dc95-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="8dc95-116">az ağ vnet oluşturma</span><span class="sxs-lookup"><span data-stu-id="8dc95-116">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="8dc95-117">Bir Azure sanal ağ ve alt ağ oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8dc95-117">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="8dc95-118">az ağ vnet eşlemesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="8dc95-118">az network vnet peering create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet/peering#create) | <span data-ttu-id="8dc95-119">İki sanal ağ arasında eşleme oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8dc95-119">Creates a peering between two virtual networks.</span></span>  |
| [<span data-ttu-id="8dc95-120">az grubu Sil</span><span class="sxs-lookup"><span data-stu-id="8dc95-120">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="8dc95-121">Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler.</span><span class="sxs-lookup"><span data-stu-id="8dc95-121">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="8dc95-122">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8dc95-122">Next steps</span></span>

<span data-ttu-id="8dc95-123">Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8dc95-123">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="8dc95-124">Ek ağ CLI kod örnekleri hello bulunabilir [Azure ağ genel görünümü belgelerine](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="8dc95-124">Additional networking CLI script samples can be found in hello [Azure Networking Overview documentation](../cli-samples.md).</span></span>
