---
title: "Azure PowerShell Betiği örnek - farklı bir bölgeye depolama hesabında VHD olarak verme/kopyalama anlık görüntü | Microsoft Docs"
description: "Azure PowerShell Betiği örnek - bir depolama hesabı aynı farklı bölgede VHD olarak verme/kopyalama anlık görüntü"
services: virtual-machines-windows
documentationcenter: storage
author: ramankumarlive
manager: kavithag
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 06/05/2017
ms.author: ramankum
ms.openlocfilehash: 80f83f4b66165ddd2bdd0edca2be5d026cb11a9b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="exportcopy-managed-snapshots-as-vhd-to-a-storage-account-in-different-region-with-powershell"></a><span data-ttu-id="dc3c6-103">Dışa aktarma/yönetilen anlık görüntüler VHD farklı bir bölgeye PowerShell ile depolama hesabında kopyalama</span><span class="sxs-lookup"><span data-stu-id="dc3c6-103">Export/Copy managed snapshots as VHD to a storage account in different region with PowerShell</span></span>

<span data-ttu-id="dc3c6-104">Bu komut dosyasını farklı bir bölgeye depolama hesabında yönetilen bir anlık görüntü verir.</span><span class="sxs-lookup"><span data-stu-id="dc3c6-104">This script exports a managed snapshot to a storage account in different region.</span></span> <span data-ttu-id="dc3c6-105">İlk anlık görüntü SAS URI'sini oluşturur ve farklı bölgede bulunan bir depolama hesabına kopyalamak için kullanır.</span><span class="sxs-lookup"><span data-stu-id="dc3c6-105">It first generates the SAS URI of the snapshot and then uses it to copy it to a storage account in different region.</span></span> <span data-ttu-id="dc3c6-106">Olağanüstü durum kurtarma için farklı bölgede yönetilen disklerinizi yedekleme korumak için bu komut dosyasını kullanın.</span><span class="sxs-lookup"><span data-stu-id="dc3c6-106">Use this script to maintain backup of your managed disks in different region for disaster recovery.</span></span>  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="dc3c6-107">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="dc3c6-107">Sample script</span></span>

<span data-ttu-id="dc3c6-108">[!code-powershell[Ana](../../../powershell_scripts/storage/copy-snapshot-to-storage-account/copy-snapshot-to-storage-account.ps1 "kopyalama anlık görüntü")]</span><span class="sxs-lookup"><span data-stu-id="dc3c6-108">[!code-powershell[main](../../../powershell_scripts/storage/copy-snapshot-to-storage-account/copy-snapshot-to-storage-account.ps1 "Copy snapshot")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="dc3c6-109">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="dc3c6-109">Script explanation</span></span>

<span data-ttu-id="dc3c6-110">Bu komut dosyası SAS URI'si için yönetilen bir anlık görüntü oluşturmak için komutları kullanır ve anlık görüntü SAS URI'sini kullanarak bir depolama hesabı kopyalar.</span><span class="sxs-lookup"><span data-stu-id="dc3c6-110">This script uses following commands to generate SAS URI for a managed snapshot and copies the snapshot to a storage account using SAS URI.</span></span> <span data-ttu-id="dc3c6-111">Komut belirli belgeleri tablo bağlanan her komut.</span><span class="sxs-lookup"><span data-stu-id="dc3c6-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="dc3c6-112">Komut</span><span class="sxs-lookup"><span data-stu-id="dc3c6-112">Command</span></span> | <span data-ttu-id="dc3c6-113">Notlar</span><span class="sxs-lookup"><span data-stu-id="dc3c6-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="dc3c6-114">GRANT-AzureRmSnapshotAccess</span><span class="sxs-lookup"><span data-stu-id="dc3c6-114">Grant-AzureRmSnapshotAccess</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="dc3c6-115">Bir depolama hesabına kopyalamak için kullanılan bir anlık görüntü için SAS URI'sini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="dc3c6-115">Generates SAS URI for a snapshot that is used to copy it to a storage account.</span></span> |
| [<span data-ttu-id="dc3c6-116">AzureStorageContext yeni</span><span class="sxs-lookup"><span data-stu-id="dc3c6-116">New-AzureStorageContext</span></span>](/powershell/module/azure.storage/New-AzureStorageContext) | <span data-ttu-id="dc3c6-117">Hesap adı ve anahtarı kullanarak bir depolama hesabı bağlamını oluşturur.</span><span class="sxs-lookup"><span data-stu-id="dc3c6-117">Creates a storage account context using the account name and key.</span></span> <span data-ttu-id="dc3c6-118">Bu bağlam, depolama hesabı üzerinde okuma/yazma işlemleri gerçekleştirmek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="dc3c6-118">This context can be used to perform read/write operations on the storage account.</span></span> |
| [<span data-ttu-id="dc3c6-119">Start-AzureStorageBlobCopy</span><span class="sxs-lookup"><span data-stu-id="dc3c6-119">Start-AzureStorageBlobCopy</span></span>](/powershell/module/azure.storage/Start-AzureStorageBlobCopy) | <span data-ttu-id="dc3c6-120">Bir depolama hesabı, bir anlık görüntüsü temel VHD kopyalar.</span><span class="sxs-lookup"><span data-stu-id="dc3c6-120">Copies the underlying VHD of a snapshot to a storage account</span></span> |

## <a name="next-steps"></a><span data-ttu-id="dc3c6-121">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="dc3c6-121">Next steps</span></span>

[<span data-ttu-id="dc3c6-122">Bir VHD'den yönetilen bir disk oluştur</span><span class="sxs-lookup"><span data-stu-id="dc3c6-122">Create a managed disk from a VHD</span></span>](./../scripts/storage-windows-powershell-sample-create-managed-disk-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json)

[<span data-ttu-id="dc3c6-123">Yönetilen bir diskten bir sanal makine oluşturun</span><span class="sxs-lookup"><span data-stu-id="dc3c6-123">Create a virtual machine from a managed disk</span></span>](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="dc3c6-124">Azure PowerShell modülü hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="dc3c6-124">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="dc3c6-125">Ek sanal makine PowerShell komut dosyası örnekleri bulunabilir [Azure Windows VM belgelerine](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="dc3c6-125">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>