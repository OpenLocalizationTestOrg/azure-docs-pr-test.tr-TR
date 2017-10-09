---
title: "aaaAzure PowerShell komut dosyası örneği - oluşturma anlık bir VHD toocreate birden çok özdeş yönetilen diskler kısa sürede | Microsoft Docs"
description: "Azure PowerShell Betiği örnek - bir anlık görüntü VHD toocreate birden çok özdeş yönetilen diskler küçük bir sürede oluşturun."
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
ms.openlocfilehash: 0a13e399b692f32b3772add39fe5b5c023808c5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-snapshot-from-a-vhd-toocreate-multiple-identical-managed-disks-in-small-amount-of-time-with-powershell"></a><span data-ttu-id="f98a4-103">Bir anlık görüntü VHD toocreate kısa sürede PowerShell ile birden çok özdeş yönetilen diskler oluşturma</span><span class="sxs-lookup"><span data-stu-id="f98a4-103">Create a snapshot from a VHD toocreate multiple identical managed disks in small amount of time with PowerShell</span></span>

<span data-ttu-id="f98a4-104">Bu komut dosyası, aynı veya farklı Abonelikteki depolama hesabındaki bir VHD dosyasından bir anlık görüntüsü oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f98a4-104">This script creates a snapshot from a VHD file in a storage account in same or different subscription.</span></span> <span data-ttu-id="f98a4-105">Bu komut dosyası tooimport özel (değil genelleştirilmiş/Sysprep kullanılarak hazırlanmış) VHD tooa anlık görüntü ve ardından hello anlık görüntü toocreate kısa sürede birden çok özdeş yönetilen diskler kullanın.</span><span class="sxs-lookup"><span data-stu-id="f98a4-105">Use this script tooimport a specialized (not generalized/sysprepped) VHD tooa snapshot and then use hello snapshot toocreate multiple identical managed disks in small amount of time.</span></span> <span data-ttu-id="f98a4-106">Ayrıca, tooimport veri VHD tooa anlık görüntü kullanın ve ardından hello anlık görüntü toocreate birden çok yönetilen diskleri kısa sürede kullanın.</span><span class="sxs-lookup"><span data-stu-id="f98a4-106">Also, use it tooimport a data VHD tooa snapshot and then use hello snapshot toocreate multiple managed disks in small amount of time.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="f98a4-107">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="f98a4-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/storage/create-snapshots-from-vhd-in-different-subscription/create-snapshots-from-vhd-in-different-subscription.ps1 "Create snapshot from VHD")]


## <a name="script-explanation"></a><span data-ttu-id="f98a4-108">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="f98a4-108">Script explanation</span></span>

<span data-ttu-id="f98a4-109">Bu komut dosyasını komutları toocreate farklı Abonelikteki bir VHD'den yönetilen bir diski kullanır.</span><span class="sxs-lookup"><span data-stu-id="f98a4-109">This script uses following commands toocreate a managed disk from a VHD in different subscription.</span></span> <span data-ttu-id="f98a4-110">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="f98a4-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="f98a4-111">Komut</span><span class="sxs-lookup"><span data-stu-id="f98a4-111">Command</span></span> | <span data-ttu-id="f98a4-112">Notlar</span><span class="sxs-lookup"><span data-stu-id="f98a4-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f98a4-113">AzureRmDiskConfig yeni</span><span class="sxs-lookup"><span data-stu-id="f98a4-113">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | <span data-ttu-id="f98a4-114">Disk oluşturmak için kullanılan disk yapılandırması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f98a4-114">Creates disk configuration that is used for disk creation.</span></span> <span data-ttu-id="f98a4-115">Depolama türü, konum, kaynak kimliği hello depolama hesabının hello üst VHD depolandığı ve VHD URİ'si hello üst VHD içerir.</span><span class="sxs-lookup"><span data-stu-id="f98a4-115">It includes storage type, location, resource Id of hello storage account where hello parent VHD is stored, and VHD URI of hello parent VHD.</span></span> |
| [<span data-ttu-id="f98a4-116">AzureRmDisk yeni</span><span class="sxs-lookup"><span data-stu-id="f98a4-116">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="f98a4-117">Disk yapılandırması, disk adı ve parametre olarak geçirilen kaynak grubu adı kullanarak bir disk oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f98a4-117">Creates a disk using disk configuration, disk name, and resource group name passed as parameters.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f98a4-118">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f98a4-118">Next steps</span></span>

[<span data-ttu-id="f98a4-119">Yönetilen bir disk anlık görüntüden oluşturma</span><span class="sxs-lookup"><span data-stu-id="f98a4-119">Create a managed disk from snapshot</span></span>](./../../storage/scripts/storage-windows-powershell-sample-create-managed-disk-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)


[<span data-ttu-id="f98a4-120">Yönetilen bir disk işletim sistemi diski olarak ekleyerek bir sanal makine oluşturun</span><span class="sxs-lookup"><span data-stu-id="f98a4-120">Create a virtual machine by attaching a managed disk as OS disk</span></span>](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="f98a4-121">Hello Azure PowerShell modülü hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f98a4-121">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="f98a4-122">Ek sanal makine PowerShell komut dosyası örnekleri hello bulunabilir [Azure Windows VM belgelerine](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f98a4-122">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
