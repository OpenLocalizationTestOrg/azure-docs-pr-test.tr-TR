---
title: "bir veri diski aaaExpand bağlı tooa Azure Windows VM | Microsoft Docs"
description: "PowerShell kullanarak ekli tooa Windows sanal makine bir veri diski Hello boyutunu genişletin."
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
ms.openlocfilehash: b16ad0da9cff9dfffc9dc9ec7dd72891e7ddd745
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="increase-hello-size-of-a-data-disk-attached-tooa-windows-vm"></a><span data-ttu-id="5cd6c-103">Bir veri bağlı disk tooa Windows VM Hello boyutunu artırın</span><span class="sxs-lookup"><span data-stu-id="5cd6c-103">Increase hello size of a data disk attached tooa Windows VM</span></span>

<span data-ttu-id="5cd6c-104">Tooincrease hello hello veri bağlı disk tooyour sanal makine boyutunu ihtiyacınız varsa, PowerShell kullanarak hello boyutunu artırabilir.</span><span class="sxs-lookup"><span data-stu-id="5cd6c-104">If you need tooincrease hello size of hello data disk attached tooyour virtual machine, you can increase hello size using PowerShell.</span></span> <span data-ttu-id="5cd6c-105">Merhaba veri diski hello Azure VM ayarlarında hello boyutunu artırın sonra da tooallocate hello hello VM içinde yeni disk alanı gerekir.</span><span class="sxs-lookup"><span data-stu-id="5cd6c-105">After you increase hello size of hello data disk in hello Azure VM settings, you also need tooallocate hello new disk space within hello VM.</span></span>


## <a name="use-powershell-tooincrease-hello-size-of-a-managed-data-disk"></a><span data-ttu-id="5cd6c-106">PowerShell tooincrease hello yönetilen veri diskin boyutunu kullanın</span><span class="sxs-lookup"><span data-stu-id="5cd6c-106">Use Powershell tooincrease hello size of a managed data disk</span></span>

<span data-ttu-id="5cd6c-107">yönetilen veri diski, PowerShell cmdlet'leri aşağıdaki kullanım hello tooincrease hello boyutu:</span><span class="sxs-lookup"><span data-stu-id="5cd6c-107">tooincrease hello size of a managed data disk, use hello following PowerShell cmdlets:</span></span>

|                                                                    |                                                            |
|--------------------------------------------------------------------|------------------------------------------------------------|
| [<span data-ttu-id="5cd6c-108">Get-AzureRMReseourceGroup</span><span class="sxs-lookup"><span data-stu-id="5cd6c-108">Get-AzureRMReseourceGroup</span></span>](/powershell/module/azurerm.resources/get-azurermresourcegroup) | [<span data-ttu-id="5cd6c-109">Get-AzureRMVM</span><span class="sxs-lookup"><span data-stu-id="5cd6c-109">Get-AzureRMVM</span></span>](/powershell/module/azurerm.compute/get-azurermvm)                 |
| [<span data-ttu-id="5cd6c-110">Stop-AzureRMVM</span><span class="sxs-lookup"><span data-stu-id="5cd6c-110">Stop-AzureRMVM</span></span>](/powershell/module/azurerm.compute/stop-azurermvm)                        | [<span data-ttu-id="5cd6c-111">Güncelleştirme AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="5cd6c-111">Update-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/Update-AzureRmDisk) |
 | [<span data-ttu-id="5cd6c-112">Start-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="5cd6c-112">Start-AzureRmVM</span></span>](/powershell/module/azurerm.compute/start-azurermvm)             |
<br>

<span data-ttu-id="5cd6c-113">Hello aşağıdaki betiği hello VM bilgi alma, hello veri diski seçme ve hello yeni boyutunu belirtme size yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="5cd6c-113">hello following script will walk you through getting hello VM information, selecting hello data disk and specifying hello new size.</span></span>

```powershell
# Select resource group

    $rg = Get-AzureRMResourceGroup | Out-GridView `
        -Title "Select hello resource group" `
        -PassThru

    $rgName = $rg.ResourceGroupName

# Select hello VM

    $vm = Get-AzureRMVM -ResourceGroupName $rgName `
        | Out-GridView `
            -Title "Select a VM" `
             -PassThru

# Select data disk

    $disk = $vm.StorageProfile.DataDisks | Out-GridView `
        -Title "Select a data disk" `
        -PassThru

# Specify a larger size for hello data disk

    $size =  Read-Host `
        -Prompt "New size in GB"

# Stop and Deallocate VM prior tooresizing data disk

    $vm | Stop-AzureRMVM -Force

# Set hello new disk size

    $diskUpdateConfig = New-AzureRmDiskUpdateConfig -DiskSizeGB $size

# Update hello configuration in Azure

    $managedDisk = Get-AzureRmResource -ResourceId $disk.ManagedDisk.Id
    Update-AzureRmDisk -DiskName $managedDisk.ResourceName -ResourceGroupName $managedDisk.ResourceGroupName -DiskUpdate $diskUpdateConfig

# Start hello VM

    Start-AzureRmVM -ResourceGroupName $rgName -VMName $vm.name
```

## <a name="use-powershell-tooincrease-hello-size-of-an-unmanaged-data-disk"></a><span data-ttu-id="5cd6c-114">PowerShell tooincrease hello yönetilmeyen veri diskin boyutunu kullanın</span><span class="sxs-lookup"><span data-stu-id="5cd6c-114">Use PowerShell tooincrease hello size of an unmanaged data disk</span></span>

<span data-ttu-id="5cd6c-115">bir depolama hesabı, PowerShell cmdlet'leri aşağıdaki kullanım hello yönetilmeyen veri diskleri tooincrease hello boyutu:</span><span class="sxs-lookup"><span data-stu-id="5cd6c-115">tooincrease hello size of unmanaged data disks in a storage account, use hello following PowerShell cmdlets:</span></span>

|                                                                    |                                                            |
|--------------------------------------------------------------------|------------------------------------------------------------|
| [<span data-ttu-id="5cd6c-116">Get-AzureRMStorageAccount</span><span class="sxs-lookup"><span data-stu-id="5cd6c-116">Get-AzureRMStorageAccount</span></span>](/powershell/module/azurerm.storage/get-azurermstorageaccount) | [<span data-ttu-id="5cd6c-117">Get-AzureRMVM</span><span class="sxs-lookup"><span data-stu-id="5cd6c-117">Get-AzureRMVM</span></span>](/powershell/module/azurerm.compute/get-azurermvm)                 |
| [<span data-ttu-id="5cd6c-118">Stop-AzureRMVM</span><span class="sxs-lookup"><span data-stu-id="5cd6c-118">Stop-AzureRMVM</span></span>](/powershell/module/azurerm.compute/stop-azurermvm)                       | [<span data-ttu-id="5cd6c-119">Set-AzureRmVMDataDisk</span><span class="sxs-lookup"><span data-stu-id="5cd6c-119">Set-AzureRmVMDataDisk</span></span>](/powershell/module/azurerm.compute/set-azurermvmdatadisk) |
| [<span data-ttu-id="5cd6c-120">Update-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="5cd6c-120">Update-AzureRmVM</span></span>](/powershell/module/azurerm.compute/update-azurermvm)                   | [<span data-ttu-id="5cd6c-121">Start-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="5cd6c-121">Start-AzureRmVM</span></span>](/powershell/module/azurerm.compute/start-azurermvm)             |

<br>

<span data-ttu-id="5cd6c-122">Merhaba aşağıdaki betiği hello VM ve depolama hesabı bilgileri alınırken, hello veri diski seçme ve hello yeni boyutunu belirtme size yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="5cd6c-122">hello following script will walk you through getting hello VM and storage account information, selecting hello data disk and specifying hello new size.</span></span>

```powershell

# Select Azure Storage Account

    $storageAccount =
        Get-AzureRMStorageAccount | Out-GridView `
            -Title "Select Azure Storage Account" `
            -PassThru

    $rgName = $storageAccount.ResourceGroupName

# Select hello VM

    $vm = Get-AzureRMVM `
    -ResourceGroupName $rgName | Out-GridView `
            -Title "Select a VM …" `
            -PassThru

# Select Data Disk tooresize

    $disk =
        $vm.DataDiskNames | Out-GridView `
            -Title "Select a data disk tooresize" `
            -PassThru


# Specify a larger data disk size

    $size =  Read-Host `
        -Prompt "New size in GB"

# Stop and Deallocate VM prior tooresizing data disk

    $vm | Stop-AzureRMVM -Force

# Set hello new disk size

    Set-AzureRmVMDataDisk -VM $vm -Name "$disk" `
        -DiskSizeInGB $size

# Update hello configuration in Azure

    Update-AzureRmVM -VM $vm -ResourceGroupName $rgName

# Start hello VM
    Start-AzureRmVM -ResourceGroupName $rgName `
    -VMName $vm.name

```

## <a name="allocate-hello-unallocated-disk-space"></a><span data-ttu-id="5cd6c-123">Merhaba ayrılmamış disk alanı Ayır</span><span class="sxs-lookup"><span data-stu-id="5cd6c-123">Allocate hello unallocated disk space</span></span>

<span data-ttu-id="5cd6c-124">Merhaba sürücü büyük yaptıktan sonra tooallocate hello yeni ayrılmamış alan hello VM içinde gerekir.</span><span class="sxs-lookup"><span data-stu-id="5cd6c-124">Once you have made hello drive larger, you need tooallocate hello new unallocated space from within hello VM.</span></span> <span data-ttu-id="5cd6c-125">tooallocate hello alanı toohello VM kullanım Disk Yönetimi'ni (diskmgmt.msc) bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="5cd6c-125">tooallocate hello space, you can connect toohello VM use Disk Management (diskmgmt.msc).</span></span> <span data-ttu-id="5cd6c-126">Veya, oluşturduğunuz sırada WinRM ve hello VM sertifikadaki etkinleştirilirse, uzak PowerShell tooinitialize hello disk kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5cd6c-126">Or, if you enabled WinRM and a certificate on hello VM when you created it, you can use remote PowerShell tooinitialize hello disk.</span></span> <span data-ttu-id="5cd6c-127">Bir özel betik uzantısı de kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="5cd6c-127">You can also use a custom script extension:</span></span>

```powershell
    $location = "location-name"
    $scriptName = "script-name"
    $fileName = "script-file-name"
    Set-AzureRmVMCustomScriptExtension -ResourceGroupName $rgName -Location $locName -VMName $vmName -Name $scriptName -TypeHandlerVersion "1.4" -StorageAccountName "mystore1" -StorageAccountKey "primary-key" -FileName $fileName -ContainerName "scripts"
```

<span data-ttu-id="5cd6c-128">Merhaba komut dosyası gibi bir bu kodu tooincrease hello sürücü ayırma toohello en büyük boyutu hello diskleri içerebilir:</span><span class="sxs-lookup"><span data-stu-id="5cd6c-128">hello script file can contain something like this code tooincrease hello drive allocation toohello maximum size hello disks:</span></span>

```powershell
$driveLetter= "F"

$MaxSize = (Get-PartitionSupportedSize -DriveLetter $driveLetter).sizeMax

Resize-Partition -DriveLetter $driveLetter -Size $MaxSize
```

## <a name="next-steps"></a><span data-ttu-id="5cd6c-129">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="5cd6c-129">Next Steps</span></span>
- [<span data-ttu-id="5cd6c-130">Diskler ve VHD hakkında daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="5cd6c-130">Learn more about disks and VHDs</span></span>](../../storage/storage-about-disks-and-vhds-windows.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
