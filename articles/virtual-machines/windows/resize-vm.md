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
# <a name="resize-a-windows-vm"></a>Bir Windows VM yeniden boyutlandırma
Bu makalede nasıl tooresize bir Windows VM oluşturulan Azure Powershell kullanarak hello Resource Manager dağıtım modelinde gösterilmektedir.

Bir sanal makine (VM) oluşturduktan sonra hello VM boyutu değiştirerek yukarı veya aşağı hello VM ölçeklendirebilirsiniz. Bazı durumlarda, ilk hello VM ayırması gerekir. Merhaba yeni boyutu şu anda hello VM barındırma hello donanım kümede kullanılabilir değilse, bu durum oluşabilir.

## <a name="resize-a-windows-vm-not-in-an-availability-set"></a>Bir kullanılabilirlik kümesinde olmayan bir Windows VM yeniden boyutlandırma
1. Merhaba VM barındırıldığı hello donanım kümede kullanılabilir hello VM boyutları listeler. 
   
    ```powershell
    Get-AzureRmVMSize -ResourceGroupName <resourceGroupName> -VMName <vmName> 
    ```
2. Merhaba boyutu listelenen isterseniz, aşağıdaki komutları tooresize hello VM hello çalıştırın. Merhaba boyutu listelenmeyen isterseniz, 3 toostep üzerinde gidin.
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroupName> -VMName <vmName>
    $vm.HardwareProfile.VmSize = "<newVMsize>"
    Update-AzureRmVM -VM $vm -ResourceGroupName <resourceGroupName>
    ```
3. Merhaba boyutu listelenmeyen isterseniz, toodeallocate VM Merhaba, yeniden boyutlandırabilir ve hello VM yeniden başlatma komutlarını aşağıdaki hello çalıştırın.
   
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
> Serbest bırakma hello VM toohello VM atanan dinamik IP adreslerini serbest bırakır. Merhaba işletim sistemi ve veri diskleri etkilenmez. 
> 
> 

## <a name="resize-a-windows-vm-in-an-availability-set"></a>Bir kullanılabilirlik kümesinde Windows VM yeniden boyutlandırma
Merhaba yeni bir kullanılabilirlik kümesinde bir VM boyutu hello donanım kümede kullanılabilir değilse, şu anda hello barındırma VM sonra hello kullanılabilirlik kümesindeki tüm VM'ler tooresize hello VM serbest toobe gerekir. Merhaba kullanılabilirlik bir VM yeniden boyutlandırılmış sonra kümesindeki diğer VM'lerin tooupdate hello boyutu da gerekebilir. tooresize bir kullanılabilirlik kümesinde bir VM hello aşağıdaki adımları gerçekleştirin.

1. Merhaba VM barındırıldığı hello donanım kümede kullanılabilir hello VM boyutları listeler.
   
    ```powershell
    Get-AzureRmVMSize -ResourceGroupName <resourceGroupName> -VMName <vmName>
    ```
2. Merhaba boyutu listelenen isterseniz, aşağıdaki komutları tooresize hello VM hello çalıştırın. Listelenmiyorsa, toostep 3 gidin.
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroupName> -VMName <vmName>
    $vm.HardwareProfile.VmSize = "<newVmSize>"
    Update-AzureRmVM -VM $vm -ResourceGroupName <resourceGroupName>
    ```
3. Hello boyutu listelenmeyen isterseniz, tüm VM'ler hello kullanılabilirlik kümesindeki adımları toodeallocate aşağıdaki hello ile devam, sanal makineleri yeniden boyutlandırma ve bunları yeniden başlatın.
4. Merhaba kullanılabilirlik kümesindeki tüm VM'ler durdurun.
   
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
5. Yeniden boyutlandırma ve hello VM'ler hello kullanılabilirlik kümesinde yeniden başlatın.
   
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

## <a name="next-steps"></a>Sonraki adımlar
* Ek ölçeklenebilirlik için birden çok VM örnekleri çalıştırın ve ölçeğini. Daha fazla bilgi için bkz: [otomatik olarak bir sanal makine ölçek kümesindeki Windows makineler ölçekleme](../../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md).

