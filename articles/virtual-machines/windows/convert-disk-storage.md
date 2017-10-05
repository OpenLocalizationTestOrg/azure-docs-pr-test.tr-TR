---
title: "Azure Dönüştür yönetilen diskleri depolama standart, premium ve tersi yönde | Microsoft Docs"
description: "Azure dönüştürme diskleri standart Premium'a ve tersi, Azure PowerShell kullanarak tarafından yönetilir."
services: virtual-machines-windows
documentationcenter: 
author: ramankum
manager: kavithag
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: ramankum
ms.openlocfilehash: 9e5c73ceb0ff7d9c18c9cf7128b69e40b9796874
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="convert-azure-managed-disks-storage-from-standard-to-premium-and-vice-versa"></a><span data-ttu-id="47ccb-103">Azure Dönüştür yönetilen diskleri depolama standart, premium ve tersi yönde</span><span class="sxs-lookup"><span data-stu-id="47ccb-103">Convert Azure managed disks storage from standard to premium, and vice versa</span></span>

<span data-ttu-id="47ccb-104">Yönetilen diskleri iki depolama seçenekleri sunar: [Premium](../../storage/storage-premium-storage.md) (SSD tabanlı) ve [standart](../../storage/storage-standard-storage.md) (HDD tabanlı).</span><span class="sxs-lookup"><span data-stu-id="47ccb-104">Managed disks offers two storage options: [Premium](../../storage/storage-premium-storage.md) (SSD-based) and [Standard](../../storage/storage-standard-storage.md) (HDD-based).</span></span> <span data-ttu-id="47ccb-105">Performans ihtiyaçlarınıza göre en düşük kapalı kalma süresi ile iki seçenek arasında kolayca geçiş yapmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="47ccb-105">It allows you to easily switch between the two options with minimal downtime based on your performance needs.</span></span> <span data-ttu-id="47ccb-106">Bu özellik, yönetilmeyen diskler için kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="47ccb-106">This capability is not available for unmanaged disks.</span></span> <span data-ttu-id="47ccb-107">Ancak kolayca [yönetilen Diske Dönüştür](convert-unmanaged-to-managed-disks.md) kolayca iki seçenek arasında geçiş yapmak için.</span><span class="sxs-lookup"><span data-stu-id="47ccb-107">But you can easily [convert to managed disks](convert-unmanaged-to-managed-disks.md) to easily switch between the two options.</span></span>

<span data-ttu-id="47ccb-108">Bu makalede yönetilen diskleri standart dönüştürme Premium'a ve bunun tersi de Azure PowerShell kullanarak gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="47ccb-108">This article shows you how to convert managed disks from standard to premium, and vice versa by using Azure PowerShell.</span></span> <span data-ttu-id="47ccb-109">Gerekirse yüklemek veya yükseltmek için bkz: [Azure PowerShell'i yükleme ve yapılandırma](/powershell/azure/install-azurerm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="47ccb-109">If you need to install or upgrade it, see [Install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="47ccb-110">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="47ccb-110">Before you begin</span></span>

* <span data-ttu-id="47ccb-111">Dönüştürme VM yeniden başlatma gerektiriyorsa, bu nedenle, diskleri depolama geçiş önceden var olan bir bakım penceresi sırasında zamanlayın.</span><span class="sxs-lookup"><span data-stu-id="47ccb-111">The conversion requires a restart of the VM, so schedule the migration of your disks storage during a pre-existing maintenance window.</span></span> 
* <span data-ttu-id="47ccb-112">Yönetilmeyen diskler, ilk kez kullanıyorsanız, [yönetilen Diske Dönüştür](convert-unmanaged-to-managed-disks.md) iki depolama seçenekleri arasında geçiş yapmak için bu makalede kullanılacak.</span><span class="sxs-lookup"><span data-stu-id="47ccb-112">If you are using unmanaged disks, first [convert to managed disks](convert-unmanaged-to-managed-disks.md) to use this article to switch between the two storage options.</span></span> 


## <a name="convert-all-the-managed-disks-of-a-vm-from-standard-to-premium-and-vice-versa"></a><span data-ttu-id="47ccb-113">Yönetilen tüm diskleri bir VM, standart, premium dönüştürmek ve tersi yönde</span><span class="sxs-lookup"><span data-stu-id="47ccb-113">Convert all the managed disks of a VM from standard to premium, and vice versa</span></span>

<span data-ttu-id="47ccb-114">Aşağıdaki örnekte, standart bir VM'den premium depolama için tüm disklerin geçiş yapma gösterir.</span><span class="sxs-lookup"><span data-stu-id="47ccb-114">In the following example, we show how to switch all the disks of a VM from standard to premium storage.</span></span> <span data-ttu-id="47ccb-115">Yönetilen premium diskleri kullanmak için VM kullanmanız gerekir bir [VM boyutu](sizes.md) premium storage destekler.</span><span class="sxs-lookup"><span data-stu-id="47ccb-115">To use premium managed disks, your VM must use a [VM size](sizes.md) that supports premium storage.</span></span> <span data-ttu-id="47ccb-116">Bu örnek ayrıca premium depolama destekleyen bir boyuta geçer.</span><span class="sxs-lookup"><span data-stu-id="47ccb-116">This example also switches to a size that supports premium storage.</span></span>

```powershell
# Name of the resource group that contains the VM
$rgName = 'yourResourceGroup'

# Name of the your virtual machine
$vmName = 'yourVM'

# Choose between StandardLRS and PremiumLRS based on your scenario
$storageType = 'PremiumLRS'

# Premium capable size
# Required only if converting storage from standard to premium
$size = 'Standard_DS2_v2'
$vm = Get-AzureRmVM -Name $vmName -resourceGroupName $rgName

# Stop and deallocate the VM before changing the size
Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force

# Change the VM size to a size that supports premium storage
# Skip this step if converting storage from premium to standard
$vm.HardwareProfile.VmSize = $size
Update-AzureRmVM -VM $vm -ResourceGroupName $rgName

# Get all disks in the resource group of the VM
$vmDisks = Get-AzureRmDisk -ResourceGroupName $rgName 

# For disks that belong to the selected VM, convert to premium storage
foreach ($disk in $vmDisks)
{
    if ($disk.OwnerId -eq $vm.Id)
    {
        $diskUpdateConfig = New-AzureRmDiskUpdateConfig –AccountType $storageType
        Update-AzureRmDisk -DiskUpdate $diskUpdateConfig -ResourceGroupName $rgName `
        -DiskName $disk.Name
    }
}

Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
```
## <a name="convert-a-managed-disk-from-standard-to-premium-and-vice-versa"></a><span data-ttu-id="47ccb-117">Premium için standart yönetilen disk dönüştürmek ve tersi yönde</span><span class="sxs-lookup"><span data-stu-id="47ccb-117">Convert a managed disk from standard to premium, and vice versa</span></span>

<span data-ttu-id="47ccb-118">Geliştirme ve test iş yükü için maliyetini azaltmak için standart ve premium disklerin karışımına sahip isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="47ccb-118">For your dev/test workload, you may want to have mixture of standard and premium disks to reduce your cost.</span></span> <span data-ttu-id="47ccb-119">Premium depolama alanına, daha iyi performans gerektiren disk yükselterek gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="47ccb-119">You can accomplish it by upgrading to premium storage, only the disks that require better performance.</span></span> <span data-ttu-id="47ccb-120">Aşağıdaki örnekte, tek bir disk standardı VM premium Depolama'ya geçiş yapma gösteriyoruz tersi.</span><span class="sxs-lookup"><span data-stu-id="47ccb-120">In the following example, we show how to switch a single disk of a VM from standard to premium storage, and vice versa.</span></span> <span data-ttu-id="47ccb-121">Yönetilen premium diskleri kullanmak için VM kullanmanız gerekir bir [VM boyutu](sizes.md) premium storage destekler.</span><span class="sxs-lookup"><span data-stu-id="47ccb-121">To use premium managed disks, your VM must use a [VM size](sizes.md) that supports premium storage.</span></span> <span data-ttu-id="47ccb-122">Bu örnek ayrıca premium depolama destekleyen bir boyuta geçer.</span><span class="sxs-lookup"><span data-stu-id="47ccb-122">This example also switches to a size that supports premium storage.</span></span>

```powershell

$diskName = 'yourDiskName'
# resource group that contains the managed disk
$rgName = 'yourResourceGroupName'
# Choose between StandardLRS and PremiumLRS based on your scenario
$storageType = 'PremiumLRS'
# Premium capable size 
$size = 'Standard_DS2_v2'

$disk = Get-AzureRmDisk -DiskName $diskName -ResourceGroupName $rgName

# Get the ARM resource to get name and resource group of the VM
$vmResource = Get-AzureRmResource -ResourceId $disk.OwnerId
$vm = Get-AzureRmVM $vmResource.ResourceGroupName -Name $vmResource.ResourceName 

# Stop and deallocate the VM before changing the storage type
Stop-AzureRmVM -ResourceGroupName $vm.ResourceGroupName -Name $vm.Name -Force

# Change the VM size to a size that supports premium storage
# Skip this step if converting storage from premium to standard
$vm.HardwareProfile.VmSize = $size
Update-AzureRmVM -VM $vm -ResourceGroupName $rgName

# Update the storage type
$diskUpdateConfig = New-AzureRmDiskUpdateConfig –AccountType $storageType
Update-AzureRmDisk -DiskUpdate $diskUpdateConfig -ResourceGroupName $rgName `
-DiskName $disk.Name

Start-AzureRmVM -ResourceGroupName $vm.ResourceGroupName -Name $vm.Name
```

## <a name="next-steps"></a><span data-ttu-id="47ccb-123">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="47ccb-123">Next steps</span></span>

<span data-ttu-id="47ccb-124">Kullanarak bir VM salt okunur bir kopyasını alın [anlık görüntüleri](snapshot-copy-managed-disk.md).</span><span class="sxs-lookup"><span data-stu-id="47ccb-124">Take a read-only copy of a VM by using [snapshots](snapshot-copy-managed-disk.md).</span></span>

