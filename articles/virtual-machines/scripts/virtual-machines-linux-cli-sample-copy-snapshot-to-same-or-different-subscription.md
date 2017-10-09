---
title: "aaaAzure CLI komut dosyası örneği - yönetilen disk toosame veya CLI ile farklı bir abonelik kopya (Taşı) anlık | Microsoft Docs"
description: "Azure CLI komut dosyası örneği - yönetilen disk toosame veya CLI ile farklı bir abonelik kopya (Taşı) anlık"
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
ms.openlocfilehash: f214ab1fc1cb2cb42479d82e455f20a8cc55c83d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-snapshot-of-a-managed-disk-toosame-or-different-subscription-with-cli"></a><span data-ttu-id="fb68c-103">Yönetilen disk toosame veya farklı bir abonelik CLI ile anlık kopyalama</span><span class="sxs-lookup"><span data-stu-id="fb68c-103">Copy snapshot of a managed disk toosame or different subscription with CLI</span></span>

<span data-ttu-id="fb68c-104">Bu komut, yönetilen disk toosame veya farklı bir abonelik anlık kopyalar.</span><span class="sxs-lookup"><span data-stu-id="fb68c-104">This script copies a snapshot of a managed disk toosame or different subscription.</span></span> <span data-ttu-id="fb68c-105">Bu komut dosyası toomove bir anlık görüntü toodifferent abonelik hello kullan hello üst anlık görüntü ile aynı bölgeye.</span><span class="sxs-lookup"><span data-stu-id="fb68c-105">Use this script toomove a snapshot toodifferent subscription in hello same region as hello parent snapshot.</span></span>


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="fb68c-106">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="fb68c-106">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/virtual-machine/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.sh "Copy snapshot")]


## <a name="script-explanation"></a><span data-ttu-id="fb68c-107">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="fb68c-107">Script explanation</span></span>

<span data-ttu-id="fb68c-108">Bu komut dosyası komutları toocreate aşağıdaki kullanır hello hedef abonelik kullanarak bir anlık görüntü hello hello kaynak anlık görüntü kimliği.</span><span class="sxs-lookup"><span data-stu-id="fb68c-108">This script uses following commands toocreate a snapshot in hello target subscription using hello Id of hello source snapshot.</span></span> <span data-ttu-id="fb68c-109">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="fb68c-109">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="fb68c-110">Komut</span><span class="sxs-lookup"><span data-stu-id="fb68c-110">Command</span></span> | <span data-ttu-id="fb68c-111">Notlar</span><span class="sxs-lookup"><span data-stu-id="fb68c-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="fb68c-112">az anlık görüntü Göster</span><span class="sxs-lookup"><span data-stu-id="fb68c-112">az snapshot show</span></span>](https://docs.microsoft.com/cli/azure/snapshot#show) | <span data-ttu-id="fb68c-113">Tüm hello adını kullanarak bir anlık görüntü hello özelliklerini ve kaynak grubu özellikleri hello anlık görüntü alır.</span><span class="sxs-lookup"><span data-stu-id="fb68c-113">Gets all hello properties of a snapshot using hello name and resource group properties of hello snapshot.</span></span> <span data-ttu-id="fb68c-114">Kullanılan toocopy hello anlık görüntü toodifferent abonelik kimliği özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="fb68c-114">Id property is used toocopy hello snapshot toodifferent subscription.</span></span>  |
| [<span data-ttu-id="fb68c-115">az anlık görüntü oluşturma</span><span class="sxs-lookup"><span data-stu-id="fb68c-115">az snapshot create</span></span>](https://docs.microsoft.com/cli/azure/snapshot#create) | <span data-ttu-id="fb68c-116">Farklı bir abonelik kullanarak bir anlık görüntü oluşturarak bir anlık görüntü hello kimliği ve adını kopya üst anlık görüntü hello.</span><span class="sxs-lookup"><span data-stu-id="fb68c-116">Copies a snapshot by creating a snapshot in different subscription using hello Id and name of hello parent snapshot.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="fb68c-117">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="fb68c-117">Next steps</span></span>

[<span data-ttu-id="fb68c-118">Bir sanal makine bir anlık görüntüden oluşturun</span><span class="sxs-lookup"><span data-stu-id="fb68c-118">Create a virtual machine from a snapshot</span></span>](./virtual-machines-linux-cli-sample-create-vm-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="fb68c-119">Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="fb68c-119">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="fb68c-120">Ek bir sanal makine ve yönetilen diskleri CLI kod örnekleri hello bulunan [Azure Linux VM'de belgelerine](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fb68c-120">Additional virtual machine and managed disks CLI script samples can be found in hello [Azure Linux VM documentation](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
