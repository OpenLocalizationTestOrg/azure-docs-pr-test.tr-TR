---
title: "PowerShell komut dosyası örneği - farklı bir bölgeye VHD tooa depolama hesabı olarak verme/kopyalama anlık görüntü aaaAzure | Microsoft Docs"
description: "Azure PowerShell Betiği örnek - VHD tooa depolama hesabıyla aynı farklı bölgede dışa aktarma/kopyalama anlık görüntü"
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
ms.openlocfilehash: 3b3e38c6b06bfa1e117f4e913dfc09443a795196
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="exportcopy-managed-snapshots-as-vhd-tooa-storage-account-in-different-region-with-powershell"></a><span data-ttu-id="7d195-103">Dışa aktarma/yönetilen anlık görüntüler VHD tooa farklı bir bölgeye PowerShell ile depolama hesabı olarak kopyalama</span><span class="sxs-lookup"><span data-stu-id="7d195-103">Export/Copy managed snapshots as VHD tooa storage account in different region with PowerShell</span></span>

<span data-ttu-id="7d195-104">Bu komut dosyasını farklı bir bölgeye yönetilen anlık görüntü tooa depolama hesabında dışa aktarır.</span><span class="sxs-lookup"><span data-stu-id="7d195-104">This script exports a managed snapshot tooa storage account in different region.</span></span> <span data-ttu-id="7d195-105">İlk hello hello anlık görüntü SAS URI'sini oluşturur ve toocopy kullanır, farklı bölgede tooa depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="7d195-105">It first generates hello SAS URI of hello snapshot and then uses it toocopy it tooa storage account in different region.</span></span> <span data-ttu-id="7d195-106">Bu komut dosyası toomaintain yedekleme yönetilen disklerinizi olağanüstü durum kurtarma için farklı bir bölge kullanın.</span><span class="sxs-lookup"><span data-stu-id="7d195-106">Use this script toomaintain backup of your managed disks in different region for disaster recovery.</span></span>  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="7d195-107">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="7d195-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/storage/copy-snapshot-to-storage-account/copy-snapshot-to-storage-account.ps1 "Copy snapshot")]


## <a name="script-explanation"></a><span data-ttu-id="7d195-108">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="7d195-108">Script explanation</span></span>

<span data-ttu-id="7d195-109">Bu komut dosyası komutları toogenerate aşağıdaki kullanır, SAS URI'sini kullanarak tooa depolama hesabı yönetilen anlık görüntülere veya kopyalara hello SAS URI'sini anlık görüntüsünü alın.</span><span class="sxs-lookup"><span data-stu-id="7d195-109">This script uses following commands toogenerate SAS URI for a managed snapshot and copies hello snapshot tooa storage account using SAS URI.</span></span> <span data-ttu-id="7d195-110">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="7d195-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="7d195-111">Komut</span><span class="sxs-lookup"><span data-stu-id="7d195-111">Command</span></span> | <span data-ttu-id="7d195-112">Notlar</span><span class="sxs-lookup"><span data-stu-id="7d195-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="7d195-113">GRANT-AzureRmSnapshotAccess</span><span class="sxs-lookup"><span data-stu-id="7d195-113">Grant-AzureRmSnapshotAccess</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="7d195-114">Kullanılan toocopy bir anlık görüntüyü için SAS URI'sini oluşturur, tooa depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="7d195-114">Generates SAS URI for a snapshot that is used toocopy it tooa storage account.</span></span> |
| [<span data-ttu-id="7d195-115">AzureStorageContext yeni</span><span class="sxs-lookup"><span data-stu-id="7d195-115">New-AzureStorageContext</span></span>](/powershell/module/azure.storage/New-AzureStorageContext) | <span data-ttu-id="7d195-116">Merhaba hesap adı ve anahtarı kullanarak bir depolama hesabı bağlamını oluşturur.</span><span class="sxs-lookup"><span data-stu-id="7d195-116">Creates a storage account context using hello account name and key.</span></span> <span data-ttu-id="7d195-117">Bu bağlamda kullanılan tooperform okuma/yazma işlemleri hello depolama hesabı üzerinde olabilir.</span><span class="sxs-lookup"><span data-stu-id="7d195-117">This context can be used tooperform read/write operations on hello storage account.</span></span> |
| [<span data-ttu-id="7d195-118">Start-AzureStorageBlobCopy</span><span class="sxs-lookup"><span data-stu-id="7d195-118">Start-AzureStorageBlobCopy</span></span>](/powershell/module/azure.storage/Start-AzureStorageBlobCopy) | <span data-ttu-id="7d195-119">Kopya bir anlık görüntü tooa depolama hesabının temel VHD hello</span><span class="sxs-lookup"><span data-stu-id="7d195-119">Copies hello underlying VHD of a snapshot tooa storage account</span></span> |

## <a name="next-steps"></a><span data-ttu-id="7d195-120">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7d195-120">Next steps</span></span>

[<span data-ttu-id="7d195-121">Bir VHD'den yönetilen bir disk oluştur</span><span class="sxs-lookup"><span data-stu-id="7d195-121">Create a managed disk from a VHD</span></span>](./../scripts/storage-windows-powershell-sample-create-managed-disk-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json)

[<span data-ttu-id="7d195-122">Yönetilen bir diskten bir sanal makine oluşturun</span><span class="sxs-lookup"><span data-stu-id="7d195-122">Create a virtual machine from a managed disk</span></span>](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="7d195-123">Hello Azure PowerShell modülü hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7d195-123">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="7d195-124">Ek sanal makine PowerShell komut dosyası örnekleri hello bulunabilir [Azure Windows VM belgelerine](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7d195-124">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
