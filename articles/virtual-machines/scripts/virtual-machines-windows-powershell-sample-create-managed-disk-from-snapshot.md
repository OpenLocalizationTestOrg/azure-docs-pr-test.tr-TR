---
title: "aaaAzure PowerShell komut dosyası örneği - yönetilen bir disk anlık görüntüden oluşturma | Microsoft Docs"
description: "Azure PowerShell Betiği örnek - bir anlık görüntüden yönetilen bir disk oluşturma"
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
ms.openlocfilehash: b99413b4c3e9a662a5fef74b7e4aeb5ecbb26af4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-disk-from-a-snapshot-with-powershell"></a><span data-ttu-id="d298d-103">Anlık görüntü PowerShell ile yönetilen bir disk oluşturun</span><span class="sxs-lookup"><span data-stu-id="d298d-103">Create a managed disk from a snapshot with PowerShell</span></span>

<span data-ttu-id="d298d-104">Bu komut dosyasını bir anlık görüntüden yönetilen bir disk oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d298d-104">This script creates a managed disk from a snapshot.</span></span> <span data-ttu-id="d298d-105">İşletim sistemi ve veri disklerin anlık görüntüleri sanal makineden toorestore kullanın.</span><span class="sxs-lookup"><span data-stu-id="d298d-105">Use it toorestore a virtual machine from snapshots of OS and data disks.</span></span> <span data-ttu-id="d298d-106">İşletim sistemi oluşturun ve veri diskleri ilgili anlık görüntülerden yönetilen ve ardından yönetilen diskleri ekleyerek yeni bir sanal makine oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d298d-106">Create OS and data managed disks from respective snapshots and then create a new virtual machine by attaching managed disks.</span></span> <span data-ttu-id="d298d-107">Anlık görüntülerden oluşturulan veri diskleri ekleyerek, mevcut bir VM'yi veri diskleri geri yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d298d-107">You can also restore data disks of an existing VM by attaching data disks created from snapshots.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="d298d-108">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="d298d-108">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-managed-disk-from-snapshot/create-managed-disk-from-snapshot.ps1 "Create managed disk from snapshot")]


## <a name="script-explanation"></a><span data-ttu-id="d298d-109">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="d298d-109">Script explanation</span></span>

<span data-ttu-id="d298d-110">Bu komut dosyasını komutları toocreate bir anlık görüntü yönetilen bir diskten kullanır.</span><span class="sxs-lookup"><span data-stu-id="d298d-110">This script uses following commands toocreate a managed disk from a snapshot.</span></span> <span data-ttu-id="d298d-111">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="d298d-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="d298d-112">Komut</span><span class="sxs-lookup"><span data-stu-id="d298d-112">Command</span></span> | <span data-ttu-id="d298d-113">Notlar</span><span class="sxs-lookup"><span data-stu-id="d298d-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d298d-114">Get-AzureRmSnapshot</span><span class="sxs-lookup"><span data-stu-id="d298d-114">Get-AzureRmSnapshot</span></span>](/powershell/module/azurerm.compute/Get-AzureRmSnapshot) | <span data-ttu-id="d298d-115">Anlık görüntü özelliklerini alır.</span><span class="sxs-lookup"><span data-stu-id="d298d-115">Gets snapshot properties.</span></span>  |
| [<span data-ttu-id="d298d-116">AzureRmDiskConfig yeni</span><span class="sxs-lookup"><span data-stu-id="d298d-116">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | <span data-ttu-id="d298d-117">Disk oluşturmak için kullanılan disk yapılandırması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d298d-117">Creates disk configuration that is used for disk creation.</span></span> <span data-ttu-id="d298d-118">Merhaba kaynak hello üst anlık görüntü, üst anlık görüntü ve hello depolama türü hello konumu olarak aynı konuma kimliğini içerir.</span><span class="sxs-lookup"><span data-stu-id="d298d-118">It includes hello resource Id of hello parent snapshot, location that is same as hello location of parent snapshot and hello storage type.</span></span>  |
| [<span data-ttu-id="d298d-119">AzureRmDisk yeni</span><span class="sxs-lookup"><span data-stu-id="d298d-119">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="d298d-120">Disk yapılandırması, disk adı ve parametre olarak geçirilen kaynak grubu adı kullanarak bir disk oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d298d-120">Creates a disk using disk configuration, disk name, and resource group name passed as parameters.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="d298d-121">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d298d-121">Next steps</span></span>

[<span data-ttu-id="d298d-122">Yönetilen bir diskten bir sanal makine oluşturun</span><span class="sxs-lookup"><span data-stu-id="d298d-122">Create a virtual machine from a managed disk</span></span>](./virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="d298d-123">Hello Azure PowerShell modülü hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d298d-123">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="d298d-124">Ek sanal makine PowerShell komut dosyası örnekleri hello bulunabilir [Azure Windows VM belgelerine](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d298d-124">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
