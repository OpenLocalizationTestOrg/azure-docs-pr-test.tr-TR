---
title: bir veri diski tooa PowerShell kullanarak Azure Windows VM aaaAttach | Microsoft Docs
description: "Nasıl tooattach yeni veya var olan veri tooa Windows VM disk PowerShell ile Merhaba Resource Manager dağıtım modeli kullanarak."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/07/2017
ms.author: cynthn
ms.openlocfilehash: 12ffdd4ced791ba0948047d3af24ad73e36c7ad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="attach-a-data-disk-tooa-windows-vm-using-powershell"></a>Bir veri diski tooa Windows VM ekleme PowerShell'i kullanma

Bu makalede nasıl tooattach hem yeni hem de mevcut PowerShell kullanarak tooa Windows sanal makine disklerini gösterilmektedir. VM yönetilen diskleri kullanıyorsa, ek yönetilen veri disklerinin ekleyebilirsiniz. Yönetilmeyen veri diskleri tooa yönetilmeyen diskler bir depolama hesabını kullanan VM da ekleyebilirsiniz.

Bunu önce bu ipuçlarını gözden geçirin:
* Merhaba boyutunu hello sanal makine, iliştirebilirsiniz kaç tane veri diskleri denetler. Ayrıntılar için bkz [sanal makineler için Boyutlar](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Premium depolama toouse, Premium depolama gerekir DS serisi veya GS serisi sanal makine hello gibi VM boyutu etkin. Bu sanal makinelerle Premium ve standart depolama hesapları arasından diskleri kullanabilirsiniz. Premium depolama belirli bölgelerde kullanılabilir. Ayrıntılar için bkz [Premium Storage: Azure sanal makine iş yükleri için yüksek performanslı depolama](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="before-you-begin"></a>Başlamadan önce
PowerShell'i kullanırsanız, hello hello AzureRM.Compute PowerShell modülü en son sürümüne sahip olduğunuzdan emin olun. Çalıştırma hello komut tooinstall onu.

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
Daha fazla bilgi için bkz: [Azure PowerShell sürüm](/powershell/azure/overview).


## <a name="add-an-empty-data-disk-tooa-virtual-machine"></a>Bir boş veri diski tooa sanal makine ekleyin

Bu örnek nasıl tooadd boş bir veri diski tooan varolan sanal makine gösterir.

### <a name="using-managed-disks"></a>Yönetilen diskleri kullanma

```powershell
$rgName = 'myResourceGroup'
$vmName = 'myVM'
$location = 'West Central US' 
$storageType = 'PremiumLRS'
$dataDiskName = $vmName + '_datadisk1'

$diskConfig = New-AzureRmDiskConfig -AccountType $storageType -Location $location -CreateOption Empty -DiskSizeGB 128

$dataDisk1 = New-AzureRmDisk -DiskName $dataDiskName -Disk $diskConfig -ResourceGroupName $rgName

$vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $rgName 

$vm = Add-AzureRmVMDataDisk -VM $vm -Name $dataDiskName -CreateOption Attach -ManagedDiskId $dataDisk1.Id -Lun 1

Update-AzureRmVM -VM $vm -ResourceGroupName $rgName
```

### <a name="using-unmanaged-disks-in-a-storage-account"></a>Yönetilmeyen diskler bir depolama hesabını kullanma

```powershell
    $vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
    Add-AzureRmVMDataDisk -VM $vm -Name "disk-name" -VhdUri "https://mystore1.blob.core.windows.net/vhds/datadisk1.vhd" -LUN 0 -Caching ReadWrite -DiskSizeinGB 1 -CreateOption Empty
    Update-AzureRmVM -ResourceGroupName $rgName -VM $vm
```


### <a name="initialize-hello-disk"></a>Başlangıç diski başlatın

Boş disk ekledikten sonra tooinitialize gerekir. tooinitialize hello disk tooa VM ve kullanım disk Yönetimi'nde oturum açabilir. WinRM ve hello VM sertifikadaki etkinleştirilirse, oluşturduğunuz sırada uzak PowerShell tooinitialize hello disk kullanabilirsiniz. Bir özel betik uzantısı de kullanabilirsiniz: 

```powershell
    $location = "location-name"
    $scriptName = "script-name"
    $fileName = "script-file-name"
    Set-AzureRmVMCustomScriptExtension -ResourceGroupName $rgName -Location $locName -VMName $vmName -Name $scriptName -TypeHandlerVersion "1.4" -StorageAccountName "mystore1" -StorageAccountKey "primary-key" -FileName $fileName -ContainerName "scripts"
```
        
Merhaba komut dosyası gibi bir bu kodu tooinitialize hello diskleri içerebilir:

```powershell
    $disks = Get-Disk | Where partitionstyle -eq 'raw' | sort number

    $letters = 70..89 | ForEach-Object { [char]$_ }
    $count = 0
    $labels = "data1","data2"

    foreach ($disk in $disks) {
        $driveLetter = $letters[$count].ToString()
        $disk | 
        Initialize-Disk -PartitionStyle MBR -PassThru |
        New-Partition -UseMaximumSize -DriveLetter $driveLetter |
        Format-Volume -FileSystem NTFS -NewFileSystemLabel $labels[$count] -Confirm:$false -Force
    $count++
    }
```


## <a name="attach-an-existing-data-disk-tooa-vm"></a>Varolan bir veri diski tooa VM ekleme

Varolan bir VHD'yi yönetilen veri diski tooa sanal makine olarak da ekleyebilirsiniz. 

### <a name="using-managed-disks"></a>Yönetilen diskleri kullanma

```powershell
$rgName = 'myRG'
$vmName = 'ContosoMdPir3'
$location = 'West Central US' 
$storageType = 'PremiumLRS'
$dataDiskName = $vmName + '_datadisk2'
$dataVhdUri = 'https://mystorageaccount.blob.core.windows.net/vhds/managed_data_disk.vhd' 

$diskConfig = New-AzureRmDiskConfig -AccountType $storageType -Location $location -CreateOption Import -SourceUri $dataVhdUri -DiskSizeGB 128

$dataDisk2 = New-AzureRmDisk -DiskName $dataDiskName -Disk $diskConfig -ResourceGroupName $rgName

$vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $rgName 

$vm = Add-AzureRmVMDataDisk -VM $vm -Name $dataDiskName -CreateOption Attach -ManagedDiskId $dataDisk2.Id -Lun 2

Update-AzureRmVM -VM $vm -ResourceGroupName $rgName
```

## <a name="next-steps"></a>Sonraki adımlar

Oluşturma bir [anlık görüntü](snapshot-copy-managed-disk.md).
