---
title: "Azure Windows VM bağlı bir veri diski Genişlet | Microsoft Docs"
description: "Bir Windows PowerShell kullanarak sanal makine için bağlı bir veri diski boyutu genişletin."
services: virtual-machines-windows
documentationcenter: na
author: cynthn
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/02/2017
ms.author: cynthn
ms.openlocfilehash: 5529856c2ffcd2942fe3fc2b438f7e3fd16a67b2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="increase-the-size-of-a-data-disk-attached-to-a-windows-vm"></a>Bir Windows VM'ye ekli bir veri diski boyutunu artırın

Sanal makineye bağlı veri diskin boyutunu artırmak gerekiyorsa, PowerShell kullanarak boyutunu artırabilirsiniz. Azure VM Ayarları'nda veri diski boyutu artırdıktan sonra ayrıca VM dahilinde yeni disk alanı ayırmak üzere gerekir.


## <a name="use-powershell-to-increase-the-size-of-a-managed-data-disk"></a>Yönetilen veri diskin boyutunu artırmak için PowerShell kullanın

Yönetilen veri diskin boyutunu artırmak için aşağıdaki PowerShell cmdlet'lerini kullanın:

|                                                                    |                                                            |
|--------------------------------------------------------------------|------------------------------------------------------------|
| [Get-AzureRMReseourceGroup](/powershell/module/azurerm.resources/get-azurermresourcegroup) | [Get-AzureRMVM](/powershell/module/azurerm.compute/get-azurermvm)                 |
| [Stop-AzureRMVM](/powershell/module/azurerm.compute/stop-azurermvm)                        | [Güncelleştirme AzureRmDisk](/powershell/module/azurerm.compute/Update-AzureRmDisk) |
 | [Start-AzureRmVM](/powershell/module/azurerm.compute/start-azurermvm)             |
<br>

Aşağıdaki komut dosyası VM bilgi alma, veri diski seçerek ve yeni boyutunu belirterek size yol gösterir.

```powershell
# Select resource group

    $rg = Get-AzureRMResourceGroup | Out-GridView `
        -Title "Select the resource group" `
        -PassThru

    $rgName = $rg.ResourceGroupName

# Select the VM

    $vm = Get-AzureRMVM -ResourceGroupName $rgName `
        | Out-GridView `
            -Title "Select a VM" `
             -PassThru

# Select data disk

    $disk = $vm.StorageProfile.DataDisks | Out-GridView `
        -Title "Select a data disk" `
        -PassThru

# Specify a larger size for the data disk

    $size =  Read-Host `
        -Prompt "New size in GB"

# Stop and Deallocate VM prior to resizing data disk

    $vm | Stop-AzureRMVM -Force

# Set the new disk size

    $diskUpdateConfig = New-AzureRmDiskUpdateConfig -DiskSizeGB $size

# Update the configuration in Azure

    $managedDisk = Get-AzureRmResource -ResourceId $disk.ManagedDisk.Id
    Update-AzureRmDisk -DiskName $managedDisk.ResourceName -ResourceGroupName $managedDisk.ResourceGroupName -DiskUpdate $diskUpdateConfig

# Start the VM

    Start-AzureRmVM -ResourceGroupName $rgName -VMName $vm.name
```

## <a name="use-powershell-to-increase-the-size-of-an-unmanaged-data-disk"></a>Bir yönetilmeyen veri diskin boyutunu artırmak için PowerShell kullanın

Yönetilmeyen veri diskleri depolama hesabındaki boyutunu artırmak için aşağıdaki PowerShell cmdlet'lerini kullanın:

|                                                                    |                                                            |
|--------------------------------------------------------------------|------------------------------------------------------------|
| [Get-AzureRMStorageAccount](/powershell/module/azurerm.storage/get-azurermstorageaccount) | [Get-AzureRMVM](/powershell/module/azurerm.compute/get-azurermvm)                 |
| [Stop-AzureRMVM](/powershell/module/azurerm.compute/stop-azurermvm)                       | [Set-AzureRmVMDataDisk](/powershell/module/azurerm.compute/set-azurermvmdatadisk) |
| [Update-AzureRmVM](/powershell/module/azurerm.compute/update-azurermvm)                   | [Start-AzureRmVM](/powershell/module/azurerm.compute/start-azurermvm)             |

<br>

Aşağıdaki komut dosyası, veri diski seçerek ve yeni boyutunu belirterek VM ve depolama hesabı bilgileri alma size yol gösterir.

```powershell

# Select Azure Storage Account

    $storageAccount =
        Get-AzureRMStorageAccount | Out-GridView `
            -Title "Select Azure Storage Account" `
            -PassThru

    $rgName = $storageAccount.ResourceGroupName

# Select the VM

    $vm = Get-AzureRMVM `
    -ResourceGroupName $rgName | Out-GridView `
            -Title "Select a VM …" `
            -PassThru

# Select Data Disk to resize

    $disk =
        $vm.DataDiskNames | Out-GridView `
            -Title "Select a data disk to resize" `
            -PassThru


# Specify a larger data disk size

    $size =  Read-Host `
        -Prompt "New size in GB"

# Stop and Deallocate VM prior to resizing data disk

    $vm | Stop-AzureRMVM -Force

# Set the new disk size

    Set-AzureRmVMDataDisk -VM $vm -Name "$disk" `
        -DiskSizeInGB $size

# Update the configuration in Azure

    Update-AzureRmVM -VM $vm -ResourceGroupName $rgName

# Start the VM
    Start-AzureRmVM -ResourceGroupName $rgName `
    -VMName $vm.name

```

## <a name="allocate-the-unallocated-disk-space"></a>Ayrılmamış disk alanı Ayır

Sürücü büyük yaptıktan sonra yeni ayrılmamış alan VM dahilinde ayırması gerekmez. Alan ayırmak için VM kullanımı için Disk Yönetimi'ni (diskmgmt.msc) bağlanabilir. Veya WinRM ve VM sertifikadaki etkinleştirilirse, oluşturduğunuz sırada diskini başlatmak için uzaktan PowerShell kullanabilirsiniz. Bir özel betik uzantısı de kullanabilirsiniz:

```powershell
    $location = "location-name"
    $scriptName = "script-name"
    $fileName = "script-file-name"
    Set-AzureRmVMCustomScriptExtension -ResourceGroupName $rgName -Location $locName -VMName $vmName -Name $scriptName -TypeHandlerVersion "1.4" -StorageAccountName "mystore1" -StorageAccountKey "primary-key" -FileName $fileName -ContainerName "scripts"
```

Komut dosyası gibi bir sürücü için en büyük boyutunu artırmak için bu kodu diskleri içerebilir:

```powershell
$driveLetter= "F"

$MaxSize = (Get-PartitionSupportedSize -DriveLetter $driveLetter).sizeMax

Resize-Partition -DriveLetter $driveLetter -Size $MaxSize
```

## <a name="next-steps"></a>Sonraki Adımlar
- [Diskler ve VHD hakkında daha fazla bilgi edinin](../../storage/storage-about-disks-and-vhds-windows.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
