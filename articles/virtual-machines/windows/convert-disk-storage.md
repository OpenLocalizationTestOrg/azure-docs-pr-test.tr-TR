---
title: "aaaConvert Azure yönetilen diskleri depolama standart toopremium ve tersi | Microsoft Docs"
description: "Nasıl tooconvert Azure standart toopremium ve tersi, Azure PowerShell kullanarak yönetilen disklerde."
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
ms.openlocfilehash: 11f35cde216e91c0599d3619682686e8eb162fad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="convert-azure-managed-disks-storage-from-standard-toopremium-and-vice-versa"></a>Azure Dönüştür yönetilen diskleri depolama standart toopremium ve tersi

Yönetilen diskleri iki depolama seçenekleri sunar: [Premium](../../storage/storage-premium-storage.md) (SSD tabanlı) ve [standart](../../storage/storage-standard-storage.md) (HDD tabanlı). Performans ihtiyaçlarınıza göre en düşük kapalı kalma süresi ile Merhaba iki seçenekten tooeasily anahtar sağlar. Bu özellik, yönetilmeyen diskler için kullanılamaz. Ancak kolayca [Dönüştür toomanaged diskleri](convert-unmanaged-to-managed-disks.md) hello iki seçenekten tooeasily anahtar.

Bu makalede, standart toopremium ve bunun tersi de Azure PowerShell kullanarak tooconvert diskleri nasıl yönetileceğini gösterir. Yükseltmek veya tooinstall gerekir, bkz: [yükleyin ve Azure PowerShell yapılandırma](/powershell/azure/install-azurerm-ps.md).

## <a name="before-you-begin"></a>Başlamadan önce

* Merhaba dönüştürme hello VM yeniden başlatılmasını gerektirir, bu nedenle, diskleri depolama hello geçiş önceden var olan bir bakım penceresi sırasında zamanlayın. 
* Yönetilmeyen diskler, ilk kez kullanıyorsanız, [Dönüştür toomanaged diskleri](convert-unmanaged-to-managed-disks.md) toouse Bu makale tooswitch hello iki depolama seçenekleri arasında. 


## <a name="convert-all-hello-managed-disks-of-a-vm-from-standard-toopremium-and-vice-versa"></a>Tüm hello dönüştürme yönetilen VM diskleri standart toopremium ve tersi

Aşağıdaki örneğine hello gösteriyoruz nasıl tooswitch tüm standart toopremium depolama biriminden bir VM diskleri hello. toouse premium disklerin yönetilen, VM'yi kullanmalısınız bir [VM boyutu](sizes.md) premium storage destekler. Bu örnek ayrıca premium depolama destekleyen tooa boyutu geçer.

```powershell
# Name of hello resource group that contains hello VM
$rgName = 'yourResourceGroup'

# Name of hello your virtual machine
$vmName = 'yourVM'

# Choose between StandardLRS and PremiumLRS based on your scenario
$storageType = 'PremiumLRS'

# Premium capable size
# Required only if converting storage from standard toopremium
$size = 'Standard_DS2_v2'
$vm = Get-AzureRmVM -Name $vmName -resourceGroupName $rgName

# Stop and deallocate hello VM before changing hello size
Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force

# Change hello VM size tooa size that supports premium storage
# Skip this step if converting storage from premium toostandard
$vm.HardwareProfile.VmSize = $size
Update-AzureRmVM -VM $vm -ResourceGroupName $rgName

# Get all disks in hello resource group of hello VM
$vmDisks = Get-AzureRmDisk -ResourceGroupName $rgName 

# For disks that belong toohello selected VM, convert toopremium storage
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
## <a name="convert-a-managed-disk-from-standard-toopremium-and-vice-versa"></a>Yönetilen bir diske Dönüştür standart toopremium ve tersi

Geliştirme ve test iş yükü için standart ve premium disklerin tooreduce toohave karışımını maliyetinizi isteyebilirsiniz. Bu, daha iyi performans gerektiren hello disk toopremium depolama yükselterek gerçekleştirebilirsiniz. Aşağıdaki örneğine hello gösteriyoruz nasıl tooswitch bir VM tek bir disk standart toopremium depolama biriminden ve tersi. toouse premium disklerin yönetilen, VM'yi kullanmalısınız bir [VM boyutu](sizes.md) premium storage destekler. Bu örnek ayrıca premium depolama destekleyen tooa boyutu geçer.

```powershell

$diskName = 'yourDiskName'
# resource group that contains hello managed disk
$rgName = 'yourResourceGroupName'
# Choose between StandardLRS and PremiumLRS based on your scenario
$storageType = 'PremiumLRS'
# Premium capable size 
$size = 'Standard_DS2_v2'

$disk = Get-AzureRmDisk -DiskName $diskName -ResourceGroupName $rgName

# Get hello ARM resource tooget name and resource group of hello VM
$vmResource = Get-AzureRmResource -ResourceId $disk.OwnerId
$vm = Get-AzureRmVM $vmResource.ResourceGroupName -Name $vmResource.ResourceName 

# Stop and deallocate hello VM before changing hello storage type
Stop-AzureRmVM -ResourceGroupName $vm.ResourceGroupName -Name $vm.Name -Force

# Change hello VM size tooa size that supports premium storage
# Skip this step if converting storage from premium toostandard
$vm.HardwareProfile.VmSize = $size
Update-AzureRmVM -VM $vm -ResourceGroupName $rgName

# Update hello storage type
$diskUpdateConfig = New-AzureRmDiskUpdateConfig –AccountType $storageType
Update-AzureRmDisk -DiskUpdate $diskUpdateConfig -ResourceGroupName $rgName `
-DiskName $disk.Name

Start-AzureRmVM -ResourceGroupName $vm.ResourceGroupName -Name $vm.Name
```

## <a name="next-steps"></a>Sonraki adımlar

Kullanarak bir VM salt okunur bir kopyasını alın [anlık görüntüleri](snapshot-copy-managed-disk.md).

