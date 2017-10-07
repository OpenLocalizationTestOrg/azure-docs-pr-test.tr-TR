---
title: "aaaAzure PowerShell komut dosyası örneği - aynı veya farklı Abonelikteki depolama hesabındaki bir VHD dosyasından yönetilen bir disk oluşturma | Microsoft Docs"
description: "Azure PowerShell Betiği örnek - aynı veya farklı Abonelikteki depolama hesabındaki bir VHD dosyasından yönetilen bir disk oluşturma"
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
ms.openlocfilehash: 93157823eb3b8cddba5e0af455d16bff1d42ce00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-disk-from-a-vhd-file-in-a-storage-account-in-same-or-different-subscription-with-powershell"></a><span data-ttu-id="c588e-103">PowerShell ile aynı veya farklı Abonelikteki depolama hesabındaki bir VHD dosyasından yönetilen bir disk oluşturma</span><span class="sxs-lookup"><span data-stu-id="c588e-103">Create a managed disk from a VHD file in a storage account in same or different subscription with PowerShell</span></span>

<span data-ttu-id="c588e-104">Bu komut dosyası, aynı veya farklı Abonelikteki depolama hesabındaki bir VHD dosyasından yönetilen bir disk oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c588e-104">This script creates a managed disk from a VHD file in a storage account in same or different subscription.</span></span> <span data-ttu-id="c588e-105">Bu komut dosyası tooimport bir özel (değil genelleştirilmiş/Sysprep kullanılarak hazırlanmış) VHD toomanaged işletim sistemi disk toocreate bir sanal makine kullanın.</span><span class="sxs-lookup"><span data-stu-id="c588e-105">Use this script tooimport a specialized (not generalized/sysprepped) VHD toomanaged OS disk toocreate a virtual machine.</span></span> <span data-ttu-id="c588e-106">Ayrıca, bir veri VHD toomanaged veri diski tooimport kullanın.</span><span class="sxs-lookup"><span data-stu-id="c588e-106">Also, use it tooimport a data VHD toomanaged data disk.</span></span> 

<span data-ttu-id="c588e-107">Birden çok özdeş yönetilen diskler bir VHD dosyasından kısa sürede oluşturmayın.</span><span class="sxs-lookup"><span data-stu-id="c588e-107">Don't create multiple identical managed disks from a VHD file in small amount of time.</span></span> <span data-ttu-id="c588e-108">bir vhd dosyasından toocreate yönetilen disklerde, blob anlık görüntü hello vhd dosyasının oluşturulur ve yönetilen kullanılan toocreate diskler ise.</span><span class="sxs-lookup"><span data-stu-id="c588e-108">toocreate managed disks from a vhd file, blob snapshot of hello vhd file is created and then it is used toocreate managed disks.</span></span> <span data-ttu-id="c588e-109">Yalnızca bir blob anlık görüntü disk oluşturma hataları neden olan bir dakika içinde oluşturulabilir son toothrottling.</span><span class="sxs-lookup"><span data-stu-id="c588e-109">Only one blob snapshot can be created in a minute that causes disk creation failures due toothrottling.</span></span> <span data-ttu-id="c588e-110">tooavoid bu kısıtlama, oluşturma bir [yönetilen anlık görüntüden hello vhd dosyasını](./../scripts/storage-windows-powershell-sample-create-snapshot-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json) ve kullanım hello anlık görüntü toocreate birden çok yönetilen diskleri kısa sürede sonra yönetilir.</span><span class="sxs-lookup"><span data-stu-id="c588e-110">tooavoid this throttling, create a [managed snapshot from hello vhd file](./../scripts/storage-windows-powershell-sample-create-snapshot-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json) and then use hello managed snapshot toocreate multiple managed disks in short amount of time.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="c588e-111">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="c588e-111">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/storage/create-managed-disks-from-vhd-in-different-subscription/create-managed-disks-from-vhd-in-different-subscription.ps1 "Create managed disk from VHD")]


## <a name="script-explanation"></a><span data-ttu-id="c588e-112">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="c588e-112">Script explanation</span></span>

<span data-ttu-id="c588e-113">Bu komut dosyasını komutları toocreate farklı Abonelikteki bir VHD'den yönetilen bir diski kullanır.</span><span class="sxs-lookup"><span data-stu-id="c588e-113">This script uses following commands toocreate a managed disk from a VHD in different subscription.</span></span> <span data-ttu-id="c588e-114">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="c588e-114">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="c588e-115">Komut</span><span class="sxs-lookup"><span data-stu-id="c588e-115">Command</span></span> | <span data-ttu-id="c588e-116">Notlar</span><span class="sxs-lookup"><span data-stu-id="c588e-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c588e-117">AzureRmDiskConfig yeni</span><span class="sxs-lookup"><span data-stu-id="c588e-117">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | <span data-ttu-id="c588e-118">Disk oluşturmak için kullanılan disk yapılandırması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c588e-118">Creates disk configuration that is used for disk creation.</span></span> <span data-ttu-id="c588e-119">Depolama türü, konum, kaynak hello üst VHD depolandığı hello depolama hesabını VHD URİ'si hello üst VHD kimliğini içerir.</span><span class="sxs-lookup"><span data-stu-id="c588e-119">It includes storage type, location, resource Id of hello storage account where hello parent VHD is stored, VHD URI of hello parent VHD.</span></span> |
| [<span data-ttu-id="c588e-120">AzureRmDisk yeni</span><span class="sxs-lookup"><span data-stu-id="c588e-120">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="c588e-121">Disk yapılandırması, disk adı ve parametre olarak geçirilen kaynak grubu adı kullanarak bir disk oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c588e-121">Creates a disk using disk configuration, disk name, and resource group name passed as parameters.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c588e-122">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c588e-122">Next steps</span></span>

[<span data-ttu-id="c588e-123">Yönetilen bir disk işletim sistemi diski olarak ekleyerek bir sanal makine oluşturun</span><span class="sxs-lookup"><span data-stu-id="c588e-123">Create a virtual machine by attaching a managed disk as OS disk</span></span>](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="c588e-124">Hello Azure PowerShell modülü hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c588e-124">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="c588e-125">Ek sanal makine PowerShell komut dosyası örnekleri hello bulunabilir [Azure Windows VM belgelerine](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c588e-125">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
