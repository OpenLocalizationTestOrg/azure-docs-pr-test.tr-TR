---
title: "Azure CLI betik örnek - yönetilen bir disk anlık görüntüden oluşturun. | Microsoft Docs"
description: "Azure CLI betik örnek - bir anlık görüntüden yönetilen bir disk oluşturma"
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
ms.openlocfilehash: 030fa06bc5819443dac5832172a93c2dca28d1ff
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-managed-disk-from-a-snapshot-with-cli"></a><span data-ttu-id="512f3-103">Anlık görüntü CLI ile yönetilen bir disk oluşturun</span><span class="sxs-lookup"><span data-stu-id="512f3-103">Create a managed disk from a snapshot with CLI</span></span>

<span data-ttu-id="512f3-104">Bu komut dosyasını bir anlık görüntüden yönetilen bir disk oluşturur.</span><span class="sxs-lookup"><span data-stu-id="512f3-104">This script creates a managed disk from a snapshot.</span></span> <span data-ttu-id="512f3-105">Bir sanal makine işletim sistemi ve veri diskleri anlık görüntülerden geri yüklemek için kullanın.</span><span class="sxs-lookup"><span data-stu-id="512f3-105">Use it to restore a virtual machine from snapshots of OS and data disks.</span></span> <span data-ttu-id="512f3-106">İşletim sistemi oluşturun ve veri diskleri ilgili anlık görüntülerden yönetilen ve ardından yönetilen diskleri ekleyerek yeni bir sanal makine oluşturun.</span><span class="sxs-lookup"><span data-stu-id="512f3-106">Create OS and data managed disks from respective snapshots and then create a new virtual machine by attaching managed disks.</span></span> <span data-ttu-id="512f3-107">Anlık görüntülerden oluşturulan veri diskleri ekleyerek, mevcut bir VM'yi veri diskleri geri yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="512f3-107">You can also restore data disks of an existing VM by attaching data disks created from snapshots.</span></span>


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="512f3-108">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="512f3-108">Sample script</span></span>

<span data-ttu-id="512f3-109">[!code-azurecli[Ana](../../../cli_scripts/storage/create-managed-disks-from-snapshot/create-managed-disks-from-snapshot.sh "yönetilen diskten anlık görüntü oluşturma")]</span><span class="sxs-lookup"><span data-stu-id="512f3-109">[!code-azurecli[main](../../../cli_scripts/storage/create-managed-disks-from-snapshot/create-managed-disks-from-snapshot.sh "Create managed disk from snapshot")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="512f3-110">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="512f3-110">Script explanation</span></span>

<span data-ttu-id="512f3-111">Bu komut dosyasını bir anlık görüntüden yönetilen bir disk oluşturmak için komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="512f3-111">This script uses following commands to create a managed disk from a snapshot.</span></span> <span data-ttu-id="512f3-112">Komut belirli belgeleri tablo bağlanan her komut.</span><span class="sxs-lookup"><span data-stu-id="512f3-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="512f3-113">Komut</span><span class="sxs-lookup"><span data-stu-id="512f3-113">Command</span></span> | <span data-ttu-id="512f3-114">Notlar</span><span class="sxs-lookup"><span data-stu-id="512f3-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="512f3-115">az anlık görüntü Göster</span><span class="sxs-lookup"><span data-stu-id="512f3-115">az snapshot show</span></span>](https://docs.microsoft.com/cli/azure/snapshot#show) | <span data-ttu-id="512f3-116">Tüm ad kullanarak bir anlık görüntü özelliklerini ve kaynak grubu özellikleri anlık görüntü alır.</span><span class="sxs-lookup"><span data-stu-id="512f3-116">Gets all the properties of a snapshot using the name and resource group properties of the snapshot.</span></span> <span data-ttu-id="512f3-117">ID özelliği, yönetilen disk oluşturmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="512f3-117">Id property is used to create managed disk.</span></span>  |
| [<span data-ttu-id="512f3-118">az disketi oluşturma</span><span class="sxs-lookup"><span data-stu-id="512f3-118">az disk create</span></span>](https://docs.microsoft.com/cli/azure/disk#create) | <span data-ttu-id="512f3-119">Yönetilen oluşturur diski kullanarak, yönetilen bir anlık görüntü kimliğini anlık görüntüsünü alın</span><span class="sxs-lookup"><span data-stu-id="512f3-119">Creates a managed disk using snapshot Id of a managed snapshot</span></span> |

## <a name="next-steps"></a><span data-ttu-id="512f3-120">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="512f3-120">Next steps</span></span>

[<span data-ttu-id="512f3-121">Yönetilen bir disk işletim sistemi diski olarak ekleyerek bir sanal makine oluşturun</span><span class="sxs-lookup"><span data-stu-id="512f3-121">Create a virtual machine by attaching a managed disk as OS disk</span></span>](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="512f3-122">Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="512f3-122">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="512f3-123">Ek bir sanal makine ve yönetilen diskleri CLI kod örnekleri bulunabilir [Azure Linux VM'de belgelerine](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="512f3-123">Additional virtual machine and managed disks CLI script samples can be found in the [Azure Linux VM documentation](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
