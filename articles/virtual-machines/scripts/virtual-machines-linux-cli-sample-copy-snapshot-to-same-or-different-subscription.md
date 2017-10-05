---
title: "Azure CLI komut dosyası örneği - CLI ile aynı veya farklı abonelik yönetilen bir diske kopyalama (Taşı) görüntüsünü | Microsoft Docs"
description: "Azure CLI komut dosyası örneği - CLI ile aynı veya farklı abonelik yönetilen bir diske görüntüsünü kopyala (taşıma)"
services: virtual-machines-linux
documentationcenter: storage
author: ramankumarlive
manager: kavithag
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/19/2017
ms.author: ramankum
ms.openlocfilehash: 6cc0125c08ccb77d014b4642d702c556fffdc8bf
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="copy-snapshot-of-a-managed-disk-to-same-or-different-subscription-with-cli"></a><span data-ttu-id="8de67-103">Yönetilen bir disk görüntüsünü CLI ile aynı veya farklı abonelik kopyalayın</span><span class="sxs-lookup"><span data-stu-id="8de67-103">Copy snapshot of a managed disk to same or different subscription with CLI</span></span>

<span data-ttu-id="8de67-104">Bu komut dosyası, aynı veya farklı aboneliğine yönetilen bir disk görüntüsünü kopyalar.</span><span class="sxs-lookup"><span data-stu-id="8de67-104">This script copies a snapshot of a managed disk to same or different subscription.</span></span> <span data-ttu-id="8de67-105">Farklı bir abonelik üst anlık görüntü ile aynı bölgede bir anlık görüntü taşımak için bu komut dosyasını kullanın.</span><span class="sxs-lookup"><span data-stu-id="8de67-105">Use this script to move a snapshot to different subscription in the same region as the parent snapshot.</span></span>


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="8de67-106">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="8de67-106">Sample script</span></span>

<span data-ttu-id="8de67-107">[!code-azurecli[Ana](../../../cli_scripts/virtual-machine/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.sh "kopyalama anlık görüntü")]</span><span class="sxs-lookup"><span data-stu-id="8de67-107">[!code-azurecli[main](../../../cli_scripts/virtual-machine/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.sh "Copy snapshot")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="8de67-108">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="8de67-108">Script explanation</span></span>

<span data-ttu-id="8de67-109">Bu komut dosyası kaynağı anlık görüntü kimliğini kullanarak hedef abonelikte bir anlık görüntü oluşturmak için komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="8de67-109">This script uses following commands to create a snapshot in the target subscription using the Id of the source snapshot.</span></span> <span data-ttu-id="8de67-110">Komut belirli belgeleri tablo bağlanan her komut.</span><span class="sxs-lookup"><span data-stu-id="8de67-110">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="8de67-111">Komut</span><span class="sxs-lookup"><span data-stu-id="8de67-111">Command</span></span> | <span data-ttu-id="8de67-112">Notlar</span><span class="sxs-lookup"><span data-stu-id="8de67-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="8de67-113">az anlık görüntü Göster</span><span class="sxs-lookup"><span data-stu-id="8de67-113">az snapshot show</span></span>](https://docs.microsoft.com/cli/azure/snapshot#show) | <span data-ttu-id="8de67-114">Tüm ad kullanarak bir anlık görüntü özelliklerini ve kaynak grubu özellikleri anlık görüntü alır.</span><span class="sxs-lookup"><span data-stu-id="8de67-114">Gets all the properties of a snapshot using the name and resource group properties of the snapshot.</span></span> <span data-ttu-id="8de67-115">ID özelliği, farklı aboneliğe anlık görüntüyü kopyalamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8de67-115">Id property is used to copy the snapshot to different subscription.</span></span>  |
| [<span data-ttu-id="8de67-116">az anlık görüntü oluşturma</span><span class="sxs-lookup"><span data-stu-id="8de67-116">az snapshot create</span></span>](https://docs.microsoft.com/cli/azure/snapshot#create) | <span data-ttu-id="8de67-117">Bir anlık görüntü üst anlık görüntünün adını ve kimlik numarasını kullanarak farklı abonelikte bir anlık görüntü oluşturarak kopyalar.</span><span class="sxs-lookup"><span data-stu-id="8de67-117">Copies a snapshot by creating a snapshot in different subscription using the Id and name of the parent snapshot.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="8de67-118">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8de67-118">Next steps</span></span>

[<span data-ttu-id="8de67-119">Bir sanal makine bir anlık görüntüden oluşturun</span><span class="sxs-lookup"><span data-stu-id="8de67-119">Create a virtual machine from a snapshot</span></span>](./virtual-machines-linux-cli-sample-create-vm-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="8de67-120">Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8de67-120">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="8de67-121">Ek bir sanal makine ve yönetilen diskleri CLI kod örnekleri bulunabilir [Azure Linux VM'de belgelerine](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8de67-121">Additional virtual machine and managed disks CLI script samples can be found in the [Azure Linux VM documentation](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
