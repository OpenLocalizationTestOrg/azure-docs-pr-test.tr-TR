---
title: "Azure PowerShell Betiği örnek - yönetilen bir disk anlık görüntüden oluşturun. | Microsoft Docs"
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
ms.openlocfilehash: 9105d9dc06eea33b3a4e1eeea7fd793919166c9b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-managed-disk-from-a-snapshot-with-powershell"></a><span data-ttu-id="0b1f7-103">Anlık görüntü PowerShell ile yönetilen bir disk oluşturun</span><span class="sxs-lookup"><span data-stu-id="0b1f7-103">Create a managed disk from a snapshot with PowerShell</span></span>

<span data-ttu-id="0b1f7-104">Bu komut dosyasını bir anlık görüntüden yönetilen bir disk oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0b1f7-104">This script creates a managed disk from a snapshot.</span></span> <span data-ttu-id="0b1f7-105">Bir sanal makine işletim sistemi ve veri diskleri anlık görüntülerden geri yüklemek için kullanın.</span><span class="sxs-lookup"><span data-stu-id="0b1f7-105">Use it to restore a virtual machine from snapshots of OS and data disks.</span></span> <span data-ttu-id="0b1f7-106">İşletim sistemi oluşturun ve veri diskleri ilgili anlık görüntülerden yönetilen ve ardından yönetilen diskleri ekleyerek yeni bir sanal makine oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0b1f7-106">Create OS and data managed disks from respective snapshots and then create a new virtual machine by attaching managed disks.</span></span> <span data-ttu-id="0b1f7-107">Anlık görüntülerden oluşturulan veri diskleri ekleyerek, mevcut bir VM'yi veri diskleri geri yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0b1f7-107">You can also restore data disks of an existing VM by attaching data disks created from snapshots.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="0b1f7-108">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="0b1f7-108">Sample script</span></span>

<span data-ttu-id="0b1f7-109">[!code-powershell[Ana](../../../powershell_scripts/storage/create-managed-disk-from-snapshot/create-managed-disk-from-snapshot.ps1 "yönetilen diskten anlık görüntü oluşturma")]</span><span class="sxs-lookup"><span data-stu-id="0b1f7-109">[!code-powershell[main](../../../powershell_scripts/storage/create-managed-disk-from-snapshot/create-managed-disk-from-snapshot.ps1 "Create managed disk from snapshot")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="0b1f7-110">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="0b1f7-110">Script explanation</span></span>

<span data-ttu-id="0b1f7-111">Bu komut dosyasını bir anlık görüntüden yönetilen bir disk oluşturmak için komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="0b1f7-111">This script uses following commands to create a managed disk from a snapshot.</span></span> <span data-ttu-id="0b1f7-112">Komut belirli belgeleri tablo bağlanan her komut.</span><span class="sxs-lookup"><span data-stu-id="0b1f7-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="0b1f7-113">Komut</span><span class="sxs-lookup"><span data-stu-id="0b1f7-113">Command</span></span> | <span data-ttu-id="0b1f7-114">Notlar</span><span class="sxs-lookup"><span data-stu-id="0b1f7-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="0b1f7-115">Get-AzureRmSnapshot</span><span class="sxs-lookup"><span data-stu-id="0b1f7-115">Get-AzureRmSnapshot</span></span>](/powershell/module/azurerm.compute/Get-AzureRmSnapshot) | <span data-ttu-id="0b1f7-116">Anlık görüntü özelliklerini alır.</span><span class="sxs-lookup"><span data-stu-id="0b1f7-116">Gets snapshot properties.</span></span>  |
| [<span data-ttu-id="0b1f7-117">AzureRmDiskConfig yeni</span><span class="sxs-lookup"><span data-stu-id="0b1f7-117">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | <span data-ttu-id="0b1f7-118">Disk oluşturmak için kullanılan disk yapılandırması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0b1f7-118">Creates disk configuration that is used for disk creation.</span></span> <span data-ttu-id="0b1f7-119">Kaynak Kimliği üst anlık görüntü ve depolama türü konumu olarak aynı konuma üst anlık görüntü içerir.</span><span class="sxs-lookup"><span data-stu-id="0b1f7-119">It includes the resource Id of the parent snapshot, location that is same as the location of parent snapshot and the storage type.</span></span>  |
| [<span data-ttu-id="0b1f7-120">AzureRmDisk yeni</span><span class="sxs-lookup"><span data-stu-id="0b1f7-120">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="0b1f7-121">Disk yapılandırması, disk adı ve parametre olarak geçirilen kaynak grubu adı kullanarak bir disk oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0b1f7-121">Creates a disk using disk configuration, disk name, and resource group name passed as parameters.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="0b1f7-122">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0b1f7-122">Next steps</span></span>

[<span data-ttu-id="0b1f7-123">Yönetilen bir diskten bir sanal makine oluşturun</span><span class="sxs-lookup"><span data-stu-id="0b1f7-123">Create a virtual machine from a managed disk</span></span>](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="0b1f7-124">Azure PowerShell modülü hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="0b1f7-124">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="0b1f7-125">Ek sanal makine PowerShell komut dosyası örnekleri bulunabilir [Azure Windows VM belgelerine](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0b1f7-125">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>