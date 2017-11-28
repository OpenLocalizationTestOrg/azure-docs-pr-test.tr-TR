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
# <a name="attach-a-data-disk-tooa-windows-vm-using-powershell"></a><span data-ttu-id="5860d-103">Bir veri diski tooa Windows VM ekleme PowerShell'i kullanma</span><span class="sxs-lookup"><span data-stu-id="5860d-103">Attach a data disk tooa Windows VM using PowerShell</span></span>

<span data-ttu-id="5860d-104">Bu makalede nasıl tooattach hem yeni hem de mevcut PowerShell kullanarak tooa Windows sanal makine disklerini gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="5860d-104">This article shows you how tooattach both new and existing disks tooa Windows virtual machine using PowerShell.</span></span> <span data-ttu-id="5860d-105">VM yönetilen diskleri kullanıyorsa, ek yönetilen veri disklerinin ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5860d-105">If your VM uses managed disks, you can attach additional managed data disks.</span></span> <span data-ttu-id="5860d-106">Yönetilmeyen veri diskleri tooa yönetilmeyen diskler bir depolama hesabını kullanan VM da ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5860d-106">You can also attach unmanaged data disks tooa VM that uses unmanaged disks in a storage account.</span></span>

<span data-ttu-id="5860d-107">Bunu önce bu ipuçlarını gözden geçirin:</span><span class="sxs-lookup"><span data-stu-id="5860d-107">Before you do this, review these tips:</span></span>
* <span data-ttu-id="5860d-108">Merhaba boyutunu hello sanal makine, iliştirebilirsiniz kaç tane veri diskleri denetler.</span><span class="sxs-lookup"><span data-stu-id="5860d-108">hello size of hello virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="5860d-109">Ayrıntılar için bkz [sanal makineler için Boyutlar](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5860d-109">For details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="5860d-110">Premium depolama toouse, Premium depolama gerekir DS serisi veya GS serisi sanal makine hello gibi VM boyutu etkin.</span><span class="sxs-lookup"><span data-stu-id="5860d-110">toouse Premium storage, you'll need a Premium Storage enabled VM size like hello DS-series or GS-series virtual machine.</span></span> <span data-ttu-id="5860d-111">Bu sanal makinelerle Premium ve standart depolama hesapları arasından diskleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5860d-111">You can use disks from both Premium and Standard storage accounts with these virtual machines.</span></span> <span data-ttu-id="5860d-112">Premium depolama belirli bölgelerde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="5860d-112">Premium storage is available in certain regions.</span></span> <span data-ttu-id="5860d-113">Ayrıntılar için bkz [Premium Storage: Azure sanal makine iş yükleri için yüksek performanslı depolama](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5860d-113">For details, see [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="5860d-114">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="5860d-114">Before you begin</span></span>
<span data-ttu-id="5860d-115">PowerShell'i kullanırsanız, hello hello AzureRM.Compute PowerShell modülü en son sürümüne sahip olduğunuzdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="5860d-115">If you use PowerShell, make sure that you have hello latest version of hello AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="5860d-116">Çalıştırma hello komut tooinstall onu.</span><span class="sxs-lookup"><span data-stu-id="5860d-116">Run hello following command tooinstall it.</span></span>

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="5860d-117">Daha fazla bilgi için bkz: [Azure PowerShell sürüm](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5860d-117">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="add-an-empty-data-disk-tooa-virtual-machine"></a><span data-ttu-id="5860d-118">Bir boş veri diski tooa sanal makine ekleyin</span><span class="sxs-lookup"><span data-stu-id="5860d-118">Add an empty data disk tooa virtual machine</span></span>

<span data-ttu-id="5860d-119">Bu örnek nasıl tooadd boş bir veri diski tooan varolan sanal makine gösterir.</span><span class="sxs-lookup"><span data-stu-id="5860d-119">This example shows how tooadd an empty data disk tooan existing virtual machine.</span></span>

### <a name="using-managed-disks"></a><span data-ttu-id="5860d-120">Yönetilen diskleri kullanma</span><span class="sxs-lookup"><span data-stu-id="5860d-120">Using managed disks</span></span>

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

### <a name="using-unmanaged-disks-in-a-storage-account"></a><span data-ttu-id="5860d-121">Yönetilmeyen diskler bir depolama hesabını kullanma</span><span class="sxs-lookup"><span data-stu-id="5860d-121">Using unmanaged disks in a storage account</span></span>

```powershell
    $vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
    Add-AzureRmVMDataDisk -VM $vm -Name "disk-name" -VhdUri "https://mystore1.blob.core.windows.net/vhds/datadisk1.vhd" -LUN 0 -Caching ReadWrite -DiskSizeinGB 1 -CreateOption Empty
    Update-AzureRmVM -ResourceGroupName $rgName -VM $vm
```


### <a name="initialize-hello-disk"></a><span data-ttu-id="5860d-122">Başlangıç diski başlatın</span><span class="sxs-lookup"><span data-stu-id="5860d-122">Initialize hello disk</span></span>

<span data-ttu-id="5860d-123">Boş disk ekledikten sonra tooinitialize gerekir.</span><span class="sxs-lookup"><span data-stu-id="5860d-123">After you add an empty disk, you need tooinitialize it.</span></span> <span data-ttu-id="5860d-124">tooinitialize hello disk tooa VM ve kullanım disk Yönetimi'nde oturum açabilir.</span><span class="sxs-lookup"><span data-stu-id="5860d-124">tooinitialize hello disk, you can log in tooa VM and use disk management.</span></span> <span data-ttu-id="5860d-125">WinRM ve hello VM sertifikadaki etkinleştirilirse, oluşturduğunuz sırada uzak PowerShell tooinitialize hello disk kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5860d-125">If you enabled WinRM and a certificate on hello VM when you created it, you can use remote PowerShell tooinitialize hello disk.</span></span> <span data-ttu-id="5860d-126">Bir özel betik uzantısı de kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="5860d-126">You can also use a custom script extension:</span></span> 

```powershell
    $location = "location-name"
    $scriptName = "script-name"
    $fileName = "script-file-name"
    Set-AzureRmVMCustomScriptExtension -ResourceGroupName $rgName -Location $locName -VMName $vmName -Name $scriptName -TypeHandlerVersion "1.4" -StorageAccountName "mystore1" -StorageAccountKey "primary-key" -FileName $fileName -ContainerName "scripts"
```
        
<span data-ttu-id="5860d-127">Merhaba komut dosyası gibi bir bu kodu tooinitialize hello diskleri içerebilir:</span><span class="sxs-lookup"><span data-stu-id="5860d-127">hello script file can contain something like this code tooinitialize hello disks:</span></span>

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


## <a name="attach-an-existing-data-disk-tooa-vm"></a><span data-ttu-id="5860d-128">Varolan bir veri diski tooa VM ekleme</span><span class="sxs-lookup"><span data-stu-id="5860d-128">Attach an existing data disk tooa VM</span></span>

<span data-ttu-id="5860d-129">Varolan bir VHD'yi yönetilen veri diski tooa sanal makine olarak da ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5860d-129">You can also attach an existing VHD as a managed data disk tooa virtual machine.</span></span> 

### <a name="using-managed-disks"></a><span data-ttu-id="5860d-130">Yönetilen diskleri kullanma</span><span class="sxs-lookup"><span data-stu-id="5860d-130">Using managed disks</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="5860d-131">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5860d-131">Next steps</span></span>

<span data-ttu-id="5860d-132">Oluşturma bir [anlık görüntü](snapshot-copy-managed-disk.md).</span><span class="sxs-lookup"><span data-stu-id="5860d-132">Create a [snapshot](snapshot-copy-managed-disk.md).</span></span>
