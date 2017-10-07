---
title: "aaaAzure CLI komut dosyası örneği - farklı bir bölgeye VHD tooa depolama hesabı olarak verme/kopyalama anlık görüntü | Microsoft Docs"
description: "Azure CLI komut dosyası örneği - VHD tooa depolama hesabıyla aynı veya farklı Abonelikteki dışa aktarma/kopyalama anlık görüntü"
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
ms.openlocfilehash: 027c5e588c4f10d64d125c17f4c78a7d8e1ef060
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="exportcopy-managed-snapshots-as-vhd-tooa-storage-account-in-different-region-with-cli"></a><span data-ttu-id="3967d-103">Dışa aktarma/yönetilen anlık görüntüler CLI ile farklı bir bölgeye VHD tooa depolama hesabı olarak kopyalama</span><span class="sxs-lookup"><span data-stu-id="3967d-103">Export/Copy managed snapshots as VHD tooa storage account in different region with CLI</span></span>

<span data-ttu-id="3967d-104">Bu komut dosyasını farklı bir bölgeye yönetilen anlık görüntü tooa depolama hesabında dışa aktarır.</span><span class="sxs-lookup"><span data-stu-id="3967d-104">This script exports a managed snapshot tooa storage account in different region.</span></span> <span data-ttu-id="3967d-105">İlk hello hello anlık görüntü SAS URI'sini oluşturur ve toocopy kullanır, farklı bölgede tooa depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="3967d-105">It first generates hello SAS URI of hello snapshot and then uses it toocopy it tooa storage account in different region.</span></span> <span data-ttu-id="3967d-106">Bu komut dosyası toomaintain yedekleme yönetilen disklerinizi olağanüstü durum kurtarma için farklı bir bölge kullanın.</span><span class="sxs-lookup"><span data-stu-id="3967d-106">Use this script toomaintain backup of your managed disks in different region for disaster recovery.</span></span> 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="3967d-107">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="3967d-107">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/storage/copy-snapshots-to-storage-account/copy-snapshots-to-storage-account.sh "Copy snapshot")]


## <a name="script-explanation"></a><span data-ttu-id="3967d-108">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="3967d-108">Script explanation</span></span>

<span data-ttu-id="3967d-109">Bu komut dosyası komutları toogenerate aşağıdaki kullanır, SAS URI'sini kullanarak tooa depolama hesabı yönetilen anlık görüntülere veya kopyalara hello SAS URI'sini anlık görüntüsünü alın.</span><span class="sxs-lookup"><span data-stu-id="3967d-109">This script uses following commands toogenerate SAS URI for a managed snapshot and copies hello snapshot tooa storage account using SAS URI.</span></span> <span data-ttu-id="3967d-110">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="3967d-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="3967d-111">Komut</span><span class="sxs-lookup"><span data-stu-id="3967d-111">Command</span></span> | <span data-ttu-id="3967d-112">Notlar</span><span class="sxs-lookup"><span data-stu-id="3967d-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="3967d-113">erişim izni ver az anlık görüntüsünü alın</span><span class="sxs-lookup"><span data-stu-id="3967d-113">az snapshot grant-access</span></span>](https://docs.microsoft.com/cli/azure/snapshot#grant-access) | <span data-ttu-id="3967d-114">VHD dosyası tooa depolama hesabını temel kullanılan toocopy veya karşıdan salt okunur SAS tooon içi oluşturur</span><span class="sxs-lookup"><span data-stu-id="3967d-114">Generates read-only SAS that is used toocopy underlying VHD file tooa storage account or download it tooon-premises</span></span>  |
| [<span data-ttu-id="3967d-115">az depolama blob kopyalama Başlat</span><span class="sxs-lookup"><span data-stu-id="3967d-115">az storage blob copy start</span></span>](https://docs.microsoft.com/en-us/cli/azure/storage/blob/copy#start) | <span data-ttu-id="3967d-116">Bir blobu bir depolama hesabı tooanother zaman uyumsuz olarak kopyalar.</span><span class="sxs-lookup"><span data-stu-id="3967d-116">Copies a blob asynchronously from one storage account tooanother</span></span> |

## <a name="next-steps"></a><span data-ttu-id="3967d-117">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3967d-117">Next steps</span></span>

[<span data-ttu-id="3967d-118">Bir VHD'den yönetilen bir disk oluştur</span><span class="sxs-lookup"><span data-stu-id="3967d-118">Create a managed disk from a VHD</span></span>](./../scripts/storage-linux-cli-sample-create-managed-disk-from-vhd.md?toc=%2fcli%2fmodule%2ftoc.json)

[<span data-ttu-id="3967d-119">Yönetilen bir diskten bir sanal makine oluşturun</span><span class="sxs-lookup"><span data-stu-id="3967d-119">Create a virtual machine from a managed disk</span></span>](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="3967d-120">Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3967d-120">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="3967d-121">Ek bir sanal makine ve yönetilen diskleri CLI kod örnekleri hello bulunan [Azure Linux VM'de belgelerine](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3967d-121">Additional virtual machine and managed disks CLI script samples can be found in hello [Azure Linux VM documentation](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
