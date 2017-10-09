---
title: aaaUse PowerShell tooresize Azure Windows VM | Microsoft Docs
description: "Azure Powershell kullanarak hello Resource Manager dağıtım modelinde oluşturulmuş bir Windows sanal makinenin yeniden boyutlandırın."
services: virtual-machines-windows
documentationcenter: 
author: Drewm3
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 057ff274-6dad-415e-891c-58f8eea9ed78
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 10/19/2016
ms.author: drewm
ms.openlocfilehash: a4a80f3bc99911e4f1a095f0ce63aca00fa50694
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="resize-a-windows-vm"></a><span data-ttu-id="1d1e7-103">Bir Windows VM yeniden boyutlandırma</span><span class="sxs-lookup"><span data-stu-id="1d1e7-103">Resize a Windows VM</span></span>
<span data-ttu-id="1d1e7-104">Bu makalede nasıl tooresize bir Windows VM oluşturulan Azure Powershell kullanarak hello Resource Manager dağıtım modelinde gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="1d1e7-104">This article shows you how tooresize a Windows VM, created in hello Resource Manager deployment model using Azure Powershell.</span></span>

<span data-ttu-id="1d1e7-105">Bir sanal makine (VM) oluşturduktan sonra hello VM boyutu değiştirerek yukarı veya aşağı hello VM ölçeklendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1d1e7-105">After you create a virtual machine (VM), you can scale hello VM up or down by changing hello VM size.</span></span> <span data-ttu-id="1d1e7-106">Bazı durumlarda, ilk hello VM ayırması gerekir.</span><span class="sxs-lookup"><span data-stu-id="1d1e7-106">In some cases, you must deallocate hello VM first.</span></span> <span data-ttu-id="1d1e7-107">Merhaba yeni boyutu şu anda hello VM barındırma hello donanım kümede kullanılabilir değilse, bu durum oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="1d1e7-107">This can happen if hello new size is not available on hello hardware cluster that is currently hosting hello VM.</span></span>

## <a name="resize-a-windows-vm-not-in-an-availability-set"></a><span data-ttu-id="1d1e7-108">Bir kullanılabilirlik kümesinde olmayan bir Windows VM yeniden boyutlandırma</span><span class="sxs-lookup"><span data-stu-id="1d1e7-108">Resize a Windows VM not in an availability set</span></span>
1. <span data-ttu-id="1d1e7-109">Merhaba VM barındırıldığı hello donanım kümede kullanılabilir hello VM boyutları listeler.</span><span class="sxs-lookup"><span data-stu-id="1d1e7-109">List hello VM sizes that are available on hello hardware cluster where hello VM is hosted.</span></span> 
   
    ```powershell
    Get-AzureRmVMSize -ResourceGroupName <resourceGroupName> -VMName <vmName> 
    ```
2. <span data-ttu-id="1d1e7-110">Merhaba boyutu listelenen isterseniz, aşağıdaki komutları tooresize hello VM hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="1d1e7-110">If hello desired size is listed, run hello following commands tooresize hello VM.</span></span> <span data-ttu-id="1d1e7-111">Merhaba boyutu listelenmeyen isterseniz, 3 toostep üzerinde gidin.</span><span class="sxs-lookup"><span data-stu-id="1d1e7-111">If hello desired size is not listed, go on toostep 3.</span></span>
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroupName> -VMName <vmName>
    $vm.HardwareProfile.VmSize = "<newVMsize>"
    Update-AzureRmVM -VM $vm -ResourceGroupName <resourceGroupName>
    ```
3. <span data-ttu-id="1d1e7-112">Merhaba boyutu listelenmeyen isterseniz, toodeallocate VM Merhaba, yeniden boyutlandırabilir ve hello VM yeniden başlatma komutlarını aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="1d1e7-112">If hello desired size is not listed, run hello following commands toodeallocate hello VM, resize it, and restart hello VM.</span></span>
   
    ```powershell
    $rgname = "<resourceGroupName>"
    $vmname = "<vmName>"
    Stop-AzureRmVM -ResourceGroupName $rgname -VMName $vmname -Force
    $vm = Get-AzureRmVM -ResourceGroupName $rgname -VMName $vmname
    $vm.HardwareProfile.VmSize = "<newVMSize>"
    Update-AzureRmVM -VM $vm -ResourceGroupName $rgname
    Start-AzureRmVM -ResourceGroupName $rgname -Name $vmname
    ```

> [!WARNING]
> <span data-ttu-id="1d1e7-113">Serbest bırakma hello VM toohello VM atanan dinamik IP adreslerini serbest bırakır.</span><span class="sxs-lookup"><span data-stu-id="1d1e7-113">Deallocating hello VM releases any dynamic IP addresses assigned toohello VM.</span></span> <span data-ttu-id="1d1e7-114">Merhaba işletim sistemi ve veri diskleri etkilenmez.</span><span class="sxs-lookup"><span data-stu-id="1d1e7-114">hello OS and data disks are not affected.</span></span> 
> 
> 

## <a name="resize-a-windows-vm-in-an-availability-set"></a><span data-ttu-id="1d1e7-115">Bir kullanılabilirlik kümesinde Windows VM yeniden boyutlandırma</span><span class="sxs-lookup"><span data-stu-id="1d1e7-115">Resize a Windows VM in an availability set</span></span>
<span data-ttu-id="1d1e7-116">Merhaba yeni bir kullanılabilirlik kümesinde bir VM boyutu hello donanım kümede kullanılabilir değilse, şu anda hello barındırma VM sonra hello kullanılabilirlik kümesindeki tüm VM'ler tooresize hello VM serbest toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="1d1e7-116">If hello new size for a VM in an availability set is not available on hello hardware cluster currently hosting hello VM, then all VMs in hello availability set will need toobe deallocated tooresize hello VM.</span></span> <span data-ttu-id="1d1e7-117">Merhaba kullanılabilirlik bir VM yeniden boyutlandırılmış sonra kümesindeki diğer VM'lerin tooupdate hello boyutu da gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="1d1e7-117">You also might need tooupdate hello size of other VMs in hello availability set after one VM has been resized.</span></span> <span data-ttu-id="1d1e7-118">tooresize bir kullanılabilirlik kümesinde bir VM hello aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="1d1e7-118">tooresize a VM in an availability set, perform hello following steps.</span></span>

1. <span data-ttu-id="1d1e7-119">Merhaba VM barındırıldığı hello donanım kümede kullanılabilir hello VM boyutları listeler.</span><span class="sxs-lookup"><span data-stu-id="1d1e7-119">List hello VM sizes that are available on hello hardware cluster where hello VM is hosted.</span></span>
   
    ```powershell
    Get-AzureRmVMSize -ResourceGroupName <resourceGroupName> -VMName <vmName>
    ```
2. <span data-ttu-id="1d1e7-120">Merhaba boyutu listelenen isterseniz, aşağıdaki komutları tooresize hello VM hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="1d1e7-120">If hello desired size is listed, run hello following commands tooresize hello VM.</span></span> <span data-ttu-id="1d1e7-121">Listelenmiyorsa, toostep 3 gidin.</span><span class="sxs-lookup"><span data-stu-id="1d1e7-121">If it is not listed, go toostep 3.</span></span>
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroupName> -VMName <vmName>
    $vm.HardwareProfile.VmSize = "<newVmSize>"
    Update-AzureRmVM -VM $vm -ResourceGroupName <resourceGroupName>
    ```
3. <span data-ttu-id="1d1e7-122">Hello boyutu listelenmeyen isterseniz, tüm VM'ler hello kullanılabilirlik kümesindeki adımları toodeallocate aşağıdaki hello ile devam, sanal makineleri yeniden boyutlandırma ve bunları yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="1d1e7-122">If hello desired size is not listed, continue with hello following steps toodeallocate all VMs in hello availability set, resize VMs, and restart them.</span></span>
4. <span data-ttu-id="1d1e7-123">Merhaba kullanılabilirlik kümesindeki tüm VM'ler durdurun.</span><span class="sxs-lookup"><span data-stu-id="1d1e7-123">Stop all VMs in hello availability set.</span></span>
   
   ```powershell
   $rg = "<resourceGroupName>"
   $as = Get-AzureRmAvailabilitySet -ResourceGroupName $rg
   $vmIds = $as.VirtualMachinesReferences
   foreach ($vmId in $vmIDs){
     $string = $vmID.Id.Split("/")
     $vmName = $string[8]
     Stop-AzureRmVM -ResourceGroupName $rg -Name $vmName -Force
   } 
   ```
5. <span data-ttu-id="1d1e7-124">Yeniden boyutlandırma ve hello VM'ler hello kullanılabilirlik kümesinde yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="1d1e7-124">Resize and restart hello VMs in hello availability set.</span></span>
   
   ```powershell
   $rg = "<resourceGroupName>"
   $newSize = "<newVmSize>"
   $as = Get-AzureRmAvailabilitySet -ResourceGroupName $rg
   $vmIds = $as.VirtualMachinesReferences
   foreach ($vmId in $vmIDs){
     $string = $vmID.Id.Split("/")
     $vmName = $string[8]
     $vm = Get-AzureRmVM -ResourceGroupName $rg -Name $vmName
     $vm.HardwareProfile.VmSize = $newSize
     Update-AzureRmVM -ResourceGroupName $rg -VM $vm
     Start-AzureRmVM -ResourceGroupName $rg -Name $vmName
   }
   ```

## <a name="next-steps"></a><span data-ttu-id="1d1e7-125">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1d1e7-125">Next steps</span></span>
* <span data-ttu-id="1d1e7-126">Ek ölçeklenebilirlik için birden çok VM örnekleri çalıştırın ve ölçeğini. Daha fazla bilgi için bkz: [otomatik olarak bir sanal makine ölçek kümesindeki Windows makineler ölçekleme](../../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md).</span><span class="sxs-lookup"><span data-stu-id="1d1e7-126">For additional scalability, run multiple VM instances and scale out. For more information, see [Automatically scale Windows machines in a Virtual Machine Scale Set](../../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md).</span></span>

