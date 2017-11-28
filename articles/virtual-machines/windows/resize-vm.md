---
title: "Azure Windows VM yeniden boyutlandırmak için PowerShell kullanın | Microsoft Docs"
description: "Azure Powershell kullanarak Resource Manager dağıtım modelinde oluşturulmuş bir Windows sanal makine yeniden boyutlandırın."
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
ms.openlocfilehash: 742efd1496de9ce76b1e5636297ef30f546bd108
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="resize-a-windows-vm"></a><span data-ttu-id="0ff77-103">Bir Windows VM yeniden boyutlandırma</span><span class="sxs-lookup"><span data-stu-id="0ff77-103">Resize a Windows VM</span></span>
<span data-ttu-id="0ff77-104">Bu makalede Windows Azure Powershell kullanarak Resource Manager dağıtım modelinde oluşturulan bir VM'yi yeniden boyutlandırın gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="0ff77-104">This article shows you how to resize a Windows VM, created in the Resource Manager deployment model using Azure Powershell.</span></span>

<span data-ttu-id="0ff77-105">Bir sanal makine (VM) oluşturduktan sonra VM boyutunu değiştirerek yukarı veya aşağı VM ölçeklendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0ff77-105">After you create a virtual machine (VM), you can scale the VM up or down by changing the VM size.</span></span> <span data-ttu-id="0ff77-106">Bazı durumlarda, ilk VM ayırması gerekir.</span><span class="sxs-lookup"><span data-stu-id="0ff77-106">In some cases, you must deallocate the VM first.</span></span> <span data-ttu-id="0ff77-107">Yeni boyutu VM'i şu anda barındırma donanım kümede kullanılabilir değilse, bu durum oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="0ff77-107">This can happen if the new size is not available on the hardware cluster that is currently hosting the VM.</span></span>

## <a name="resize-a-windows-vm-not-in-an-availability-set"></a><span data-ttu-id="0ff77-108">Bir kullanılabilirlik kümesinde olmayan bir Windows VM yeniden boyutlandırma</span><span class="sxs-lookup"><span data-stu-id="0ff77-108">Resize a Windows VM not in an availability set</span></span>
1. <span data-ttu-id="0ff77-109">VM barındırıldığı donanım kümede kullanılabilir VM boyutları listeler.</span><span class="sxs-lookup"><span data-stu-id="0ff77-109">List the VM sizes that are available on the hardware cluster where the VM is hosted.</span></span> 
   
    ```powershell
    Get-AzureRmVMSize -ResourceGroupName <resourceGroupName> -VMName <vmName> 
    ```
2. <span data-ttu-id="0ff77-110">İstenen boyut listeleniyorsa, VM yeniden boyutlandırmak için aşağıdaki komutları çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="0ff77-110">If the desired size is listed, run the following commands to resize the VM.</span></span> <span data-ttu-id="0ff77-111">İstenen boyut listelenmemişse, 3. adıma geçin.</span><span class="sxs-lookup"><span data-stu-id="0ff77-111">If the desired size is not listed, go on to step 3.</span></span>
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroupName> -VMName <vmName>
    $vm.HardwareProfile.VmSize = "<newVMsize>"
    Update-AzureRmVM -VM $vm -ResourceGroupName <resourceGroupName>
    ```
3. <span data-ttu-id="0ff77-112">İstenen boyut, VM serbest bırakma için aşağıdaki komutları çalıştırın listelenmemişse yeniden boyutlandırabilir ve VM'yi yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="0ff77-112">If the desired size is not listed, run the following commands to deallocate the VM, resize it, and restart the VM.</span></span>
   
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
> <span data-ttu-id="0ff77-113">VM serbest bırakma VM'ye atanan dinamik IP adreslerini serbest bırakır.</span><span class="sxs-lookup"><span data-stu-id="0ff77-113">Deallocating the VM releases any dynamic IP addresses assigned to the VM.</span></span> <span data-ttu-id="0ff77-114">İşletim sistemi ve veri diskleri etkilenmez.</span><span class="sxs-lookup"><span data-stu-id="0ff77-114">The OS and data disks are not affected.</span></span> 
> 
> 

## <a name="resize-a-windows-vm-in-an-availability-set"></a><span data-ttu-id="0ff77-115">Bir kullanılabilirlik kümesinde Windows VM yeniden boyutlandırma</span><span class="sxs-lookup"><span data-stu-id="0ff77-115">Resize a Windows VM in an availability set</span></span>
<span data-ttu-id="0ff77-116">Yeni bir kullanılabilirlik kümesinde bir VM boyutu şu anda VM barındırma donanım kümede kullanılabilir durumda değilse, tüm sanal makineleri kullanılabilirlik kümesindeki VM yeniden boyutlandırmak için serbest gerekecektir.</span><span class="sxs-lookup"><span data-stu-id="0ff77-116">If the new size for a VM in an availability set is not available on the hardware cluster currently hosting the VM, then all VMs in the availability set will need to be deallocated to resize the VM.</span></span> <span data-ttu-id="0ff77-117">Bir VM yeniden boyutlandırılmış sonra kullanılabilirlik diğer VM'ler boyutunu güncelleştirme gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="0ff77-117">You also might need to update the size of other VMs in the availability set after one VM has been resized.</span></span> <span data-ttu-id="0ff77-118">Bir kullanılabilirlik kümesinde bir VM'yi yeniden boyutlandırmak için aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="0ff77-118">To resize a VM in an availability set, perform the following steps.</span></span>

1. <span data-ttu-id="0ff77-119">VM barındırıldığı donanım kümede kullanılabilir VM boyutları listeler.</span><span class="sxs-lookup"><span data-stu-id="0ff77-119">List the VM sizes that are available on the hardware cluster where the VM is hosted.</span></span>
   
    ```powershell
    Get-AzureRmVMSize -ResourceGroupName <resourceGroupName> -VMName <vmName>
    ```
2. <span data-ttu-id="0ff77-120">İstenen boyut listeleniyorsa, VM yeniden boyutlandırmak için aşağıdaki komutları çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="0ff77-120">If the desired size is listed, run the following commands to resize the VM.</span></span> <span data-ttu-id="0ff77-121">Listelenmiyorsa, 3. adıma gidin.</span><span class="sxs-lookup"><span data-stu-id="0ff77-121">If it is not listed, go to step 3.</span></span>
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroupName> -VMName <vmName>
    $vm.HardwareProfile.VmSize = "<newVmSize>"
    Update-AzureRmVM -VM $vm -ResourceGroupName <resourceGroupName>
    ```
3. <span data-ttu-id="0ff77-122">İstenen boyut listelenmemişse kullanılabilirlik kümesindeki tüm VM'ler ayırması, sanal makineleri yeniden boyutlandırma ve bunları yeniden başlatmak için aşağıdaki adımlarla devam edin.</span><span class="sxs-lookup"><span data-stu-id="0ff77-122">If the desired size is not listed, continue with the following steps to deallocate all VMs in the availability set, resize VMs, and restart them.</span></span>
4. <span data-ttu-id="0ff77-123">Kullanılabilirlik kümesindeki tüm VM'ler durdurun.</span><span class="sxs-lookup"><span data-stu-id="0ff77-123">Stop all VMs in the availability set.</span></span>
   
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
5. <span data-ttu-id="0ff77-124">Yeniden boyutlandırma ve kullanılabilirlik kümesindeki sanal makineleri yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="0ff77-124">Resize and restart the VMs in the availability set.</span></span>
   
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

## <a name="next-steps"></a><span data-ttu-id="0ff77-125">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0ff77-125">Next steps</span></span>
* <span data-ttu-id="0ff77-126">Ek ölçeklenebilirlik için birden çok VM örnekleri çalıştırın ve ölçeğini.</span><span class="sxs-lookup"><span data-stu-id="0ff77-126">For additional scalability, run multiple VM instances and scale out.</span></span> <span data-ttu-id="0ff77-127">Daha fazla bilgi için bkz: [otomatik olarak bir sanal makine ölçek kümesindeki Windows makineler ölçekleme](../../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md).</span><span class="sxs-lookup"><span data-stu-id="0ff77-127">For more information, see [Automatically scale Windows machines in a Virtual Machine Scale Set](../../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md).</span></span>

