---
title: "PowerShell kullanarak Azure Windows VM için bir veri diski ekleme | Microsoft Docs"
description: "Windows PowerShell ile Resource Manager dağıtım modeli kullanarak bir VM yeni veya var olan veri diski ekleme yapma."
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
ms.openlocfilehash: 486e6a27fa28ec63001d824fe9f59c03a7aea5a7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="attach-a-data-disk-to-a-windows-vm-using-powershell"></a><span data-ttu-id="a6f16-103">Bir Windows PowerShell kullanarak bir VM için bir veri diski Ekle</span><span class="sxs-lookup"><span data-stu-id="a6f16-103">Attach a data disk to a Windows VM using PowerShell</span></span>

<span data-ttu-id="a6f16-104">Bu makalede bir Windows PowerShell kullanarak sanal makine için yeni ve mevcut diskleri ekleme gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="a6f16-104">This article shows you how to attach both new and existing disks to a Windows virtual machine using PowerShell.</span></span> <span data-ttu-id="a6f16-105">VM yönetilen diskleri kullanıyorsa, ek yönetilen veri disklerinin ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a6f16-105">If your VM uses managed disks, you can attach additional managed data disks.</span></span> <span data-ttu-id="a6f16-106">Bir depolama hesabında yönetilmeyen diskleri kullanan bir VM'yi yönetilmeyen veri diskleri ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a6f16-106">You can also attach unmanaged data disks to a VM that uses unmanaged disks in a storage account.</span></span>

<span data-ttu-id="a6f16-107">Bunu önce bu ipuçlarını gözden geçirin:</span><span class="sxs-lookup"><span data-stu-id="a6f16-107">Before you do this, review these tips:</span></span>
* <span data-ttu-id="a6f16-108">Sanal makinenin boyutunu, iliştirebilirsiniz kaç tane veri diskleri denetler.</span><span class="sxs-lookup"><span data-stu-id="a6f16-108">The size of the virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="a6f16-109">Ayrıntılar için bkz [sanal makineler için Boyutlar](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a6f16-109">For details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="a6f16-110">Premium depolama kullanmak için bir Premium depolama ihtiyaç duyarsınız DS serisi veya GS serisi sanal makine gibi VM boyutu etkin.</span><span class="sxs-lookup"><span data-stu-id="a6f16-110">To use Premium storage, you'll need a Premium Storage enabled VM size like the DS-series or GS-series virtual machine.</span></span> <span data-ttu-id="a6f16-111">Bu sanal makinelerle Premium ve standart depolama hesapları arasından diskleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a6f16-111">You can use disks from both Premium and Standard storage accounts with these virtual machines.</span></span> <span data-ttu-id="a6f16-112">Premium depolama belirli bölgelerde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="a6f16-112">Premium storage is available in certain regions.</span></span> <span data-ttu-id="a6f16-113">Ayrıntılar için bkz [Premium Storage: Azure sanal makine iş yükleri için yüksek performanslı depolama](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a6f16-113">For details, see [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="a6f16-114">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="a6f16-114">Before you begin</span></span>
<span data-ttu-id="a6f16-115">PowerShell'i kullanırsanız, AzureRM.Compute PowerShell modülü en son sürümüne sahip olduğunuzdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="a6f16-115">If you use PowerShell, make sure that you have the latest version of the AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="a6f16-116">Yüklemek için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="a6f16-116">Run the following command to install it.</span></span>

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="a6f16-117">Daha fazla bilgi için bkz: [Azure PowerShell sürüm](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a6f16-117">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="add-an-empty-data-disk-to-a-virtual-machine"></a><span data-ttu-id="a6f16-118">Bir sanal makineye bir boş veri diski Ekle</span><span class="sxs-lookup"><span data-stu-id="a6f16-118">Add an empty data disk to a virtual machine</span></span>

<span data-ttu-id="a6f16-119">Bu örnek, varolan bir sanal makineye bir boş veri diski Ekle gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="a6f16-119">This example shows how to add an empty data disk to an existing virtual machine.</span></span>

### <a name="using-managed-disks"></a><span data-ttu-id="a6f16-120">Yönetilen diskleri kullanma</span><span class="sxs-lookup"><span data-stu-id="a6f16-120">Using managed disks</span></span>

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

### <a name="using-unmanaged-disks-in-a-storage-account"></a><span data-ttu-id="a6f16-121">Yönetilmeyen diskler bir depolama hesabını kullanma</span><span class="sxs-lookup"><span data-stu-id="a6f16-121">Using unmanaged disks in a storage account</span></span>

```powershell
    $vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
    Add-AzureRmVMDataDisk -VM $vm -Name "disk-name" -VhdUri "https://mystore1.blob.core.windows.net/vhds/datadisk1.vhd" -LUN 0 -Caching ReadWrite -DiskSizeinGB 1 -CreateOption Empty
    Update-AzureRmVM -ResourceGroupName $rgName -VM $vm
```


### <a name="initialize-the-disk"></a><span data-ttu-id="a6f16-122">Diski başlatın</span><span class="sxs-lookup"><span data-stu-id="a6f16-122">Initialize the disk</span></span>

<span data-ttu-id="a6f16-123">Boş disk ekledikten sonra bunu başlatmak için gerekir.</span><span class="sxs-lookup"><span data-stu-id="a6f16-123">After you add an empty disk, you need to initialize it.</span></span> <span data-ttu-id="a6f16-124">Diskini başlatmak için bir VM için oturum açın ve disk Yönetimi'ni kullanın.</span><span class="sxs-lookup"><span data-stu-id="a6f16-124">To initialize the disk, you can log in to a VM and use disk management.</span></span> <span data-ttu-id="a6f16-125">WinRM ve VM sertifikadaki etkinleştirilirse, oluşturduğunuz sırada diskini başlatmak için uzaktan PowerShell kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a6f16-125">If you enabled WinRM and a certificate on the VM when you created it, you can use remote PowerShell to initialize the disk.</span></span> <span data-ttu-id="a6f16-126">Bir özel betik uzantısı de kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a6f16-126">You can also use a custom script extension:</span></span> 

```powershell
    $location = "location-name"
    $scriptName = "script-name"
    $fileName = "script-file-name"
    Set-AzureRmVMCustomScriptExtension -ResourceGroupName $rgName -Location $locName -VMName $vmName -Name $scriptName -TypeHandlerVersion "1.4" -StorageAccountName "mystore1" -StorageAccountKey "primary-key" -FileName $fileName -ContainerName "scripts"
```
        
<span data-ttu-id="a6f16-127">Komut dosyası gibi bir diskleri başlatmak için bu kodu içerebilir:</span><span class="sxs-lookup"><span data-stu-id="a6f16-127">The script file can contain something like this code to initialize the disks:</span></span>

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


## <a name="attach-an-existing-data-disk-to-a-vm"></a><span data-ttu-id="a6f16-128">Varolan bir veri diski bir VM'e ekleyin</span><span class="sxs-lookup"><span data-stu-id="a6f16-128">Attach an existing data disk to a VM</span></span>

<span data-ttu-id="a6f16-129">Ayrıca, varolan bir VHD'yi yönetilen veri diski olarak bir sanal makineye ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a6f16-129">You can also attach an existing VHD as a managed data disk to a virtual machine.</span></span> 

### <a name="using-managed-disks"></a><span data-ttu-id="a6f16-130">Yönetilen diskleri kullanma</span><span class="sxs-lookup"><span data-stu-id="a6f16-130">Using managed disks</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="a6f16-131">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a6f16-131">Next steps</span></span>

<span data-ttu-id="a6f16-132">Oluşturma bir [anlık görüntü](snapshot-copy-managed-disk.md).</span><span class="sxs-lookup"><span data-stu-id="a6f16-132">Create a [snapshot](snapshot-copy-managed-disk.md).</span></span>
