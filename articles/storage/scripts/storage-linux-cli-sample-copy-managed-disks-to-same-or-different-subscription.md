---
title: "Azure CLI komut dosyası örneği - kopyalama (Taşı) yönetilen aynı veya farklı bir abonelik disklere | Microsoft Docs"
description: "Azure CLI komut dosyası örneği - kopyalama (Taşı) yönetilen aynı veya farklı bir abonelik disklere"
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
ms.openlocfilehash: 784ad81db2c83da14665fa926425928f12a15c27
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="copy-managed-disks-to-same-or-different-subscription-with-cli"></a><span data-ttu-id="8f36a-103">CLI ile aynı veya farklı aboneliğe yönetilen diskleri kopyalama</span><span class="sxs-lookup"><span data-stu-id="8f36a-103">Copy managed disks to same or different subscription with CLI</span></span>

<span data-ttu-id="8f36a-104">Bu komut dosyası, aynı veya farklı bir abonelik ancak aynı bölgede yönetilen bir diske kopyalar.</span><span class="sxs-lookup"><span data-stu-id="8f36a-104">This script copies a managed disk to same or different subscription but in the same region.</span></span> 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="8f36a-105">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="8f36a-105">Sample script</span></span>

<span data-ttu-id="8f36a-106">[!code-azurecli[Ana](../../../cli_scripts/storage/copy-managed-disks-to-same-or-different-subscription/copy-managed-disks-to-same-or-different-subscription.sh "kopya disk yönetilen")]</span><span class="sxs-lookup"><span data-stu-id="8f36a-106">[!code-azurecli[main](../../../cli_scripts/storage/copy-managed-disks-to-same-or-different-subscription/copy-managed-disks-to-same-or-different-subscription.sh "Copy managed disk")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="8f36a-107">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="8f36a-107">Script explanation</span></span>

<span data-ttu-id="8f36a-108">Bu komut dosyasını yeni bir yönetilen disk kaynağı yönetilen disk kimliğini kullanarak hedef abonelikte oluşturmak için komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="8f36a-108">This script uses following commands to create a new managed disk in the target subscription using the Id of the source managed disk.</span></span> <span data-ttu-id="8f36a-109">Komut belirli belgeleri tablo bağlanan her komut.</span><span class="sxs-lookup"><span data-stu-id="8f36a-109">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="8f36a-110">Komut</span><span class="sxs-lookup"><span data-stu-id="8f36a-110">Command</span></span> | <span data-ttu-id="8f36a-111">Notlar</span><span class="sxs-lookup"><span data-stu-id="8f36a-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="8f36a-112">az disk Göster</span><span class="sxs-lookup"><span data-stu-id="8f36a-112">az disk show</span></span>](https://docs.microsoft.com/cli/azure/disk#show) | <span data-ttu-id="8f36a-113">Tüm adını kullanarak yönetilen bir diskin özelliklerini ve kaynak grubu yönetilen diskin özelliklerini alır.</span><span class="sxs-lookup"><span data-stu-id="8f36a-113">Gets all the properties of a managed disk using the name and resource group properties of the managed disk.</span></span> <span data-ttu-id="8f36a-114">ID özelliği, yönetilen disk farklı aboneliğe kopyalamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8f36a-114">Id property is used to copy the managed disk to different subscription.</span></span>  |
| [<span data-ttu-id="8f36a-115">az disketi oluşturma</span><span class="sxs-lookup"><span data-stu-id="8f36a-115">az disk create</span></span>](https://docs.microsoft.com/cli/azure/disk#create) | <span data-ttu-id="8f36a-116">Kopya yeni oluşturma tarafından yönetilen bir disk disk kimliğini kullanarak farklı Abonelikteki yönetilen ve üst yönetilen disk adlandırın.</span><span class="sxs-lookup"><span data-stu-id="8f36a-116">Copies a managed disk by creating a new managed disk in different subscription using Id and name the parent managed disk.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="8f36a-117">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8f36a-117">Next steps</span></span>

[<span data-ttu-id="8f36a-118">Yönetilen bir diskten bir sanal makine oluşturun</span><span class="sxs-lookup"><span data-stu-id="8f36a-118">Create a virtual machine from a managed disk</span></span>](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="8f36a-119">Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8f36a-119">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="8f36a-120">Ek bir sanal makine ve yönetilen diskleri CLI kod örnekleri bulunabilir [Azure Linux VM'de belgelerine](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8f36a-120">Additional virtual machine and managed disks CLI script samples can be found in the [Azure Linux VM documentation](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
