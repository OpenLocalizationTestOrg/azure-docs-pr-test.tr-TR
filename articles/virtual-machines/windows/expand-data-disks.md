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
# <a name="increase-the-size-of-a-data-disk-attached-to-a-windows-vm"></a><span data-ttu-id="0165d-103">Bir Windows VM'ye ekli bir veri diski boyutunu artırın</span><span class="sxs-lookup"><span data-stu-id="0165d-103">Increase the size of a data disk attached to a Windows VM</span></span>

<span data-ttu-id="0165d-104">Sanal makineye bağlı veri diskin boyutunu artırmak gerekiyorsa, PowerShell kullanarak boyutunu artırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0165d-104">If you need to increase the size of the data disk attached to your virtual machine, you can increase the size using PowerShell.</span></span> <span data-ttu-id="0165d-105">Azure VM Ayarları'nda veri diski boyutu artırdıktan sonra ayrıca VM dahilinde yeni disk alanı ayırmak üzere gerekir.</span><span class="sxs-lookup"><span data-stu-id="0165d-105">After you increase the size of the data disk in the Azure VM settings, you also need to allocate the new disk space within the VM.</span></span>


## <a name="use-powershell-to-increase-the-size-of-a-managed-data-disk"></a><span data-ttu-id="0165d-106">Yönetilen veri diskin boyutunu artırmak için PowerShell kullanın</span><span class="sxs-lookup"><span data-stu-id="0165d-106">Use Powershell to increase the size of a managed data disk</span></span>

<span data-ttu-id="0165d-107">Yönetilen veri diskin boyutunu artırmak için aşağıdaki PowerShell cmdlet'lerini kullanın:</span><span class="sxs-lookup"><span data-stu-id="0165d-107">To increase the size of a managed data disk, use the following PowerShell cmdlets:</span></span>

|                                                                    |                                                            |
|--------------------------------------------------------------------|------------------------------------------------------------|
| [<span data-ttu-id="0165d-108">Get-AzureRMReseourceGroup</span><span class="sxs-lookup"><span data-stu-id="0165d-108">Get-AzureRMReseourceGroup</span></span>](/powershell/module/azurerm.resources/get-azurermresourcegroup) | [<span data-ttu-id="0165d-109">Get-AzureRMVM</span><span class="sxs-lookup"><span data-stu-id="0165d-109">Get-AzureRMVM</span></span>](/powershell/module/azurerm.compute/get-azurermvm)                 |
| [<span data-ttu-id="0165d-110">Stop-AzureRMVM</span><span class="sxs-lookup"><span data-stu-id="0165d-110">Stop-AzureRMVM</span></span>](/powershell/module/azurerm.compute/stop-azurermvm)                        | [<span data-ttu-id="0165d-111">Güncelleştirme AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="0165d-111">Update-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/Update-AzureRmDisk) |
 | [<span data-ttu-id="0165d-112">Start-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="0165d-112">Start-AzureRmVM</span></span>](/powershell/module/azurerm.compute/start-azurermvm)             |
<br>

<span data-ttu-id="0165d-113">Aşağıdaki komut dosyası VM bilgi alma, veri diski seçerek ve yeni boyutunu belirterek size yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="0165d-113">The following script will walk you through getting the VM information, selecting the data disk and specifying the new size.</span></span>

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

## <a name="use-powershell-to-increase-the-size-of-an-unmanaged-data-disk"></a><span data-ttu-id="0165d-114">Bir yönetilmeyen veri diskin boyutunu artırmak için PowerShell kullanın</span><span class="sxs-lookup"><span data-stu-id="0165d-114">Use PowerShell to increase the size of an unmanaged data disk</span></span>

<span data-ttu-id="0165d-115">Yönetilmeyen veri diskleri depolama hesabındaki boyutunu artırmak için aşağıdaki PowerShell cmdlet'lerini kullanın:</span><span class="sxs-lookup"><span data-stu-id="0165d-115">To increase the size of unmanaged data disks in a storage account, use the following PowerShell cmdlets:</span></span>

|                                                                    |                                                            |
|--------------------------------------------------------------------|------------------------------------------------------------|
| [<span data-ttu-id="0165d-116">Get-AzureRMStorageAccount</span><span class="sxs-lookup"><span data-stu-id="0165d-116">Get-AzureRMStorageAccount</span></span>](/powershell/module/azurerm.storage/get-azurermstorageaccount) | [<span data-ttu-id="0165d-117">Get-AzureRMVM</span><span class="sxs-lookup"><span data-stu-id="0165d-117">Get-AzureRMVM</span></span>](/powershell/module/azurerm.compute/get-azurermvm)                 |
| [<span data-ttu-id="0165d-118">Stop-AzureRMVM</span><span class="sxs-lookup"><span data-stu-id="0165d-118">Stop-AzureRMVM</span></span>](/powershell/module/azurerm.compute/stop-azurermvm)                       | [<span data-ttu-id="0165d-119">Set-AzureRmVMDataDisk</span><span class="sxs-lookup"><span data-stu-id="0165d-119">Set-AzureRmVMDataDisk</span></span>](/powershell/module/azurerm.compute/set-azurermvmdatadisk) |
| [<span data-ttu-id="0165d-120">Update-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="0165d-120">Update-AzureRmVM</span></span>](/powershell/module/azurerm.compute/update-azurermvm)                   | [<span data-ttu-id="0165d-121">Start-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="0165d-121">Start-AzureRmVM</span></span>](/powershell/module/azurerm.compute/start-azurermvm)             |

<br>

<span data-ttu-id="0165d-122">Aşağıdaki komut dosyası, veri diski seçerek ve yeni boyutunu belirterek VM ve depolama hesabı bilgileri alma size yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="0165d-122">The following script will walk you through getting the VM and storage account information, selecting the data disk and specifying the new size.</span></span>

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

## <a name="allocate-the-unallocated-disk-space"></a><span data-ttu-id="0165d-123">Ayrılmamış disk alanı Ayır</span><span class="sxs-lookup"><span data-stu-id="0165d-123">Allocate the unallocated disk space</span></span>

<span data-ttu-id="0165d-124">Sürücü büyük yaptıktan sonra yeni ayrılmamış alan VM dahilinde ayırması gerekmez.</span><span class="sxs-lookup"><span data-stu-id="0165d-124">Once you have made the drive larger, you need to allocate the new unallocated space from within the VM.</span></span> <span data-ttu-id="0165d-125">Alan ayırmak için VM kullanımı için Disk Yönetimi'ni (diskmgmt.msc) bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="0165d-125">To allocate the space, you can connect to the VM use Disk Management (diskmgmt.msc).</span></span> <span data-ttu-id="0165d-126">Veya WinRM ve VM sertifikadaki etkinleştirilirse, oluşturduğunuz sırada diskini başlatmak için uzaktan PowerShell kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0165d-126">Or, if you enabled WinRM and a certificate on the VM when you created it, you can use remote PowerShell to initialize the disk.</span></span> <span data-ttu-id="0165d-127">Bir özel betik uzantısı de kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="0165d-127">You can also use a custom script extension:</span></span>

```powershell
    $location = "location-name"
    $scriptName = "script-name"
    $fileName = "script-file-name"
    Set-AzureRmVMCustomScriptExtension -ResourceGroupName $rgName -Location $locName -VMName $vmName -Name $scriptName -TypeHandlerVersion "1.4" -StorageAccountName "mystore1" -StorageAccountKey "primary-key" -FileName $fileName -ContainerName "scripts"
```

<span data-ttu-id="0165d-128">Komut dosyası gibi bir sürücü için en büyük boyutunu artırmak için bu kodu diskleri içerebilir:</span><span class="sxs-lookup"><span data-stu-id="0165d-128">The script file can contain something like this code to increase the drive allocation to the maximum size the disks:</span></span>

```powershell
$driveLetter= "F"

$MaxSize = (Get-PartitionSupportedSize -DriveLetter $driveLetter).sizeMax

Resize-Partition -DriveLetter $driveLetter -Size $MaxSize
```

## <a name="next-steps"></a><span data-ttu-id="0165d-129">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="0165d-129">Next Steps</span></span>
- [<span data-ttu-id="0165d-130">Diskler ve VHD hakkında daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="0165d-130">Learn more about disks and VHDs</span></span>](../../storage/storage-about-disks-and-vhds-windows.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
