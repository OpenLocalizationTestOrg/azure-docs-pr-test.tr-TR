---
title: "aaaAzure CLI komut dosyası örneği - kopyalama (Taşı) yönetilen diskleri toosame veya farklı bir abonelik | Microsoft Docs"
description: "Azure CLI komut dosyası örneği - yönetilen kopyalama (Taşı) diskleri toosame veya farklı bir abonelik"
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
ms.openlocfilehash: 8581169baa0fd0e0eec1c72eab77b657f48b1cfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-managed-disks-toosame-or-different-subscription-with-cli"></a><span data-ttu-id="22be5-103">Yönetilen diskleri toosame veya farklı bir abonelik CLI ile kopyalama</span><span class="sxs-lookup"><span data-stu-id="22be5-103">Copy managed disks toosame or different subscription with CLI</span></span>

<span data-ttu-id="22be5-104">Bu komut dosyasını bir yönetilen disk toosame veya farklı bir abonelik kopyalar ancak içinde aynı hello bölgesi.</span><span class="sxs-lookup"><span data-stu-id="22be5-104">This script copies a managed disk toosame or different subscription but in hello same region.</span></span> 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="22be5-105">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="22be5-105">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/storage/copy-managed-disks-to-same-or-different-subscription/copy-managed-disks-to-same-or-different-subscription.sh "Copy managed disk")]


## <a name="script-explanation"></a><span data-ttu-id="22be5-106">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="22be5-106">Script explanation</span></span>

<span data-ttu-id="22be5-107">Aşağıdaki komutları toocreate kullanır hello hedef abonelik kullanarak yeni bir yönetilen disk hello hello kaynak kimliğini bu komut dosyası disk yönetilen.</span><span class="sxs-lookup"><span data-stu-id="22be5-107">This script uses following commands toocreate a new managed disk in hello target subscription using hello Id of hello source managed disk.</span></span> <span data-ttu-id="22be5-108">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="22be5-108">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="22be5-109">Komut</span><span class="sxs-lookup"><span data-stu-id="22be5-109">Command</span></span> | <span data-ttu-id="22be5-110">Notlar</span><span class="sxs-lookup"><span data-stu-id="22be5-110">Notes</span></span> |
|---|---|
| [<span data-ttu-id="22be5-111">az disk Göster</span><span class="sxs-lookup"><span data-stu-id="22be5-111">az disk show</span></span>](https://docs.microsoft.com/cli/azure/disk#show) | <span data-ttu-id="22be5-112">Merhaba yönetilen disk hello ad ve kaynak grubu özellikleri kullanılarak yönetilen bir disk tüm hello özelliklerini alır.</span><span class="sxs-lookup"><span data-stu-id="22be5-112">Gets all hello properties of a managed disk using hello name and resource group properties of hello managed disk.</span></span> <span data-ttu-id="22be5-113">Kullanılan toocopy yönetilen hello disk toodifferent abonelik kimliği özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="22be5-113">Id property is used toocopy hello managed disk toodifferent subscription.</span></span>  |
| [<span data-ttu-id="22be5-114">az disketi oluşturma</span><span class="sxs-lookup"><span data-stu-id="22be5-114">az disk create</span></span>](https://docs.microsoft.com/cli/azure/disk#create) | <span data-ttu-id="22be5-115">Yönetilen bir disk kimliği ve adını kullanarak farklı abonelikte yeni bir yönetilen disk oluşturarak kopyalar hello üst disk yönetilen.</span><span class="sxs-lookup"><span data-stu-id="22be5-115">Copies a managed disk by creating a new managed disk in different subscription using Id and name hello parent managed disk.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="22be5-116">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="22be5-116">Next steps</span></span>

[<span data-ttu-id="22be5-117">Yönetilen bir diskten bir sanal makine oluşturun</span><span class="sxs-lookup"><span data-stu-id="22be5-117">Create a virtual machine from a managed disk</span></span>](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="22be5-118">Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="22be5-118">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="22be5-119">Ek bir sanal makine ve yönetilen diskleri CLI kod örnekleri hello bulunan [Azure Linux VM'de belgelerine](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="22be5-119">Additional virtual machine and managed disks CLI script samples can be found in hello [Azure Linux VM documentation](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
