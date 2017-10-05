---
title: "Azure CLI komut dosyası örneği - farklı bir bölgeye depolama hesabında VHD olarak verme/kopyalama anlık görüntü | Microsoft Docs"
description: "Azure CLI komut dosyası örneği - bir depolama hesabı aynı veya farklı Abonelikteki VHD olarak verme/kopyalama anlık görüntü"
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
ms.openlocfilehash: a6ea65aba91641ece415db4df6ae9c17b42a0954
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="exportcopy-managed-snapshots-as-vhd-to-a-storage-account-in-different-region-with-cli"></a><span data-ttu-id="571bf-103">Dışa aktarma/yönetilen anlık görüntüler VHD CLI ile farklı bir bölgeye depolama hesabında kopyalama</span><span class="sxs-lookup"><span data-stu-id="571bf-103">Export/Copy managed snapshots as VHD to a storage account in different region with CLI</span></span>

<span data-ttu-id="571bf-104">Bu komut dosyasını farklı bir bölgeye depolama hesabında yönetilen bir anlık görüntü verir.</span><span class="sxs-lookup"><span data-stu-id="571bf-104">This script exports a managed snapshot to a storage account in different region.</span></span> <span data-ttu-id="571bf-105">İlk anlık görüntü SAS URI'sini oluşturur ve farklı bölgede bulunan bir depolama hesabına kopyalamak için kullanır.</span><span class="sxs-lookup"><span data-stu-id="571bf-105">It first generates the SAS URI of the snapshot and then uses it to copy it to a storage account in different region.</span></span> <span data-ttu-id="571bf-106">Olağanüstü durum kurtarma için farklı bölgede yönetilen disklerinizi yedekleme korumak için bu komut dosyasını kullanın.</span><span class="sxs-lookup"><span data-stu-id="571bf-106">Use this script to maintain backup of your managed disks in different region for disaster recovery.</span></span> 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="571bf-107">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="571bf-107">Sample script</span></span>

<span data-ttu-id="571bf-108">[!code-azurecli[Ana](../../../cli_scripts/virtual-machine/copy-snapshots-to-storage-account/copy-snapshots-to-storage-account.sh "kopyalama anlık görüntü")]</span><span class="sxs-lookup"><span data-stu-id="571bf-108">[!code-azurecli[main](../../../cli_scripts/virtual-machine/copy-snapshots-to-storage-account/copy-snapshots-to-storage-account.sh "Copy snapshot")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="571bf-109">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="571bf-109">Script explanation</span></span>

<span data-ttu-id="571bf-110">Bu komut dosyası SAS URI'si için yönetilen bir anlık görüntü oluşturmak için komutları kullanır ve anlık görüntü SAS URI'sini kullanarak bir depolama hesabı kopyalar.</span><span class="sxs-lookup"><span data-stu-id="571bf-110">This script uses following commands to generate SAS URI for a managed snapshot and copies the snapshot to a storage account using SAS URI.</span></span> <span data-ttu-id="571bf-111">Komut belirli belgeleri tablo bağlanan her komut.</span><span class="sxs-lookup"><span data-stu-id="571bf-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="571bf-112">Komut</span><span class="sxs-lookup"><span data-stu-id="571bf-112">Command</span></span> | <span data-ttu-id="571bf-113">Notlar</span><span class="sxs-lookup"><span data-stu-id="571bf-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="571bf-114">erişim izni ver az anlık görüntüsünü alın</span><span class="sxs-lookup"><span data-stu-id="571bf-114">az snapshot grant-access</span></span>](https://docs.microsoft.com/cli/azure/snapshot#grant-access) | <span data-ttu-id="571bf-115">Bir depolama hesabına temel VHD dosyasını kopyalayın veya şirket içi indirmek için kullanılan salt okunur SAS oluşturur</span><span class="sxs-lookup"><span data-stu-id="571bf-115">Generates read-only SAS that is used to copy underlying VHD file to a storage account or download it to on-premises</span></span>  |
| [<span data-ttu-id="571bf-116">az depolama blob kopyalama Başlat</span><span class="sxs-lookup"><span data-stu-id="571bf-116">az storage blob copy start</span></span>](https://docs.microsoft.com/en-us/cli/azure/storage/blob/copy#start) | <span data-ttu-id="571bf-117">Bir blob zaman uyumsuz olarak bir depolama hesabından başka bir konuma kopyalar</span><span class="sxs-lookup"><span data-stu-id="571bf-117">Copies a blob asynchronously from one storage account to another</span></span> |

## <a name="next-steps"></a><span data-ttu-id="571bf-118">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="571bf-118">Next steps</span></span>

[<span data-ttu-id="571bf-119">Bir VHD'den yönetilen bir disk oluştur</span><span class="sxs-lookup"><span data-stu-id="571bf-119">Create a managed disk from a VHD</span></span>](virtual-machines-linux-cli-sample-create-managed-disk-from-vhd.md?toc=%2fcli%2fmodule%2ftoc.json)

[<span data-ttu-id="571bf-120">Yönetilen bir diskten bir sanal makine oluşturun</span><span class="sxs-lookup"><span data-stu-id="571bf-120">Create a virtual machine from a managed disk</span></span>](./virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="571bf-121">Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="571bf-121">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="571bf-122">Ek bir sanal makine ve yönetilen diskleri CLI kod örnekleri bulunabilir [Azure Linux VM'de belgelerine](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="571bf-122">Additional virtual machine and managed disks CLI script samples can be found in the [Azure Linux VM documentation](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
