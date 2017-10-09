---
title: "aaaAzure CLI komut dosyası örneği - yönetilen bir disk anlık görüntüden oluşturma | Microsoft Docs"
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
ms.openlocfilehash: 549692f5027b3f50b0dd89fe701ebbf0f51d6031
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-disk-from-a-snapshot-with-cli"></a><span data-ttu-id="006e5-103">Anlık görüntü CLI ile yönetilen bir disk oluşturun</span><span class="sxs-lookup"><span data-stu-id="006e5-103">Create a managed disk from a snapshot with CLI</span></span>

<span data-ttu-id="006e5-104">Bu komut dosyasını bir anlık görüntüden yönetilen bir disk oluşturur.</span><span class="sxs-lookup"><span data-stu-id="006e5-104">This script creates a managed disk from a snapshot.</span></span> <span data-ttu-id="006e5-105">İşletim sistemi ve veri disklerin anlık görüntüleri sanal makineden toorestore kullanın.</span><span class="sxs-lookup"><span data-stu-id="006e5-105">Use it toorestore a virtual machine from snapshots of OS and data disks.</span></span> <span data-ttu-id="006e5-106">İşletim sistemi oluşturun ve veri diskleri ilgili anlık görüntülerden yönetilen ve ardından yönetilen diskleri ekleyerek yeni bir sanal makine oluşturun.</span><span class="sxs-lookup"><span data-stu-id="006e5-106">Create OS and data managed disks from respective snapshots and then create a new virtual machine by attaching managed disks.</span></span> <span data-ttu-id="006e5-107">Anlık görüntülerden oluşturulan veri diskleri ekleyerek, mevcut bir VM'yi veri diskleri geri yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="006e5-107">You can also restore data disks of an existing VM by attaching data disks created from snapshots.</span></span>


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="006e5-108">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="006e5-108">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-managed-disks-from-snapshot/create-managed-disks-from-snapshot.sh "Create managed disk from snapshot")]


## <a name="script-explanation"></a><span data-ttu-id="006e5-109">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="006e5-109">Script explanation</span></span>

<span data-ttu-id="006e5-110">Bu komut dosyasını komutları toocreate bir anlık görüntü yönetilen bir diskten kullanır.</span><span class="sxs-lookup"><span data-stu-id="006e5-110">This script uses following commands toocreate a managed disk from a snapshot.</span></span> <span data-ttu-id="006e5-111">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="006e5-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="006e5-112">Komut</span><span class="sxs-lookup"><span data-stu-id="006e5-112">Command</span></span> | <span data-ttu-id="006e5-113">Notlar</span><span class="sxs-lookup"><span data-stu-id="006e5-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="006e5-114">az anlık görüntü Göster</span><span class="sxs-lookup"><span data-stu-id="006e5-114">az snapshot show</span></span>](https://docs.microsoft.com/cli/azure/snapshot#show) | <span data-ttu-id="006e5-115">Tüm hello adını kullanarak bir anlık görüntü hello özelliklerini ve kaynak grubu özellikleri hello anlık görüntü alır.</span><span class="sxs-lookup"><span data-stu-id="006e5-115">Gets all hello properties of a snapshot using hello name and resource group properties of hello snapshot.</span></span> <span data-ttu-id="006e5-116">ID özelliği kullanılan toocreate yönetilen disktir.</span><span class="sxs-lookup"><span data-stu-id="006e5-116">Id property is used toocreate managed disk.</span></span>  |
| [<span data-ttu-id="006e5-117">az disketi oluşturma</span><span class="sxs-lookup"><span data-stu-id="006e5-117">az disk create</span></span>](https://docs.microsoft.com/cli/azure/disk#create) | <span data-ttu-id="006e5-118">Yönetilen oluşturur diski kullanarak, yönetilen bir anlık görüntü kimliğini anlık görüntüsünü alın</span><span class="sxs-lookup"><span data-stu-id="006e5-118">Creates a managed disk using snapshot Id of a managed snapshot</span></span> |

## <a name="next-steps"></a><span data-ttu-id="006e5-119">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="006e5-119">Next steps</span></span>

[<span data-ttu-id="006e5-120">Yönetilen bir disk işletim sistemi diski olarak ekleyerek bir sanal makine oluşturun</span><span class="sxs-lookup"><span data-stu-id="006e5-120">Create a virtual machine by attaching a managed disk as OS disk</span></span>](./virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="006e5-121">Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="006e5-121">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="006e5-122">Ek bir sanal makine ve yönetilen diskleri CLI kod örnekleri hello bulunan [Azure Linux VM'de belgelerine](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="006e5-122">Additional virtual machine and managed disks CLI script samples can be found in hello [Azure Linux VM documentation](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
