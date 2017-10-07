---
title: "aaaConvert yönetilmeyenden Windows sanal makine disklerini toomanaged diskler - Azure yönetilen disk | Microsoft Docs"
description: "Merhaba Resource Manager dağıtım modelinde PowerShell kullanarak nasıl tooconvert yönetilmeyen diskleri toomanaged Windows VM'den diskler"
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
ms.date: 06/23/2017
ms.author: cynthn
ms.openlocfilehash: e8ed8694b0e776d22df26261e2fc8340bfe5cafa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="convert-a-windows-virtual-machine-from-unmanaged-disks-toomanaged-disks"></a>Windows sanal makine yönetilmeyen diskleri toomanaged disklerden Dönüştür

Yönetilmeyen diskleri kullanan bir mevcut Windows sanal makineleri (VM'ler) varsa, hello aracılığıyla hello VM'ler yönetilen toouse diskler dönüştürülebilir [Azure yönetilen diskleri](managed-disks-overview.md) hizmet. Bu işlem hello işletim sistemi disk ve tüm eklenen veri disklerini dönüştürür.

Bu makale size nasıl gösterir Azure PowerShell kullanarak sanal makineleri tooconvert. Yükseltmek veya tooinstall gerekir, bkz: [yükleyin ve Azure PowerShell yapılandırma](/powershell/azure/install-azurerm-ps.md).

## <a name="before-you-begin"></a>Başlamadan önce


* Gözden geçirme [planlama hello geçiş için tooManaged diskleri](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks).

[!INCLUDE [virtual-machines-common-convert-disks-considerations](../../../includes/virtual-machines-common-convert-disks-considerations.md)]




## <a name="convert-single-instance-vms"></a>Tek Örnekli VM'ler Dönüştür
Bu bölüm, nasıl tooconvert Tek Örnekli yönetilmeyenden Azure VM'ler toomanaged diskleri kapsar. (Bir kullanılabilirlik kümesine Vm'leriniz varsa hello sonraki bölüme bakın.) 

1. Hello kullanarak Hello VM serbest bırakma [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) cmdlet'i. Merhaba aşağıdaki örnek kaldırır hello adlı VM `myVM` adlı hello kaynak grubunda `myResourceGroup`: 

  ```powershell
  $rgName = "myResourceGroup"
  $vmName = "myVM"
  Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
  ```

2. Hello kullanarak Hello VM toomanaged diskleri dönüştürme [ConvertTo-AzureRmVMManagedDisk](/powershell/module/azurerm.compute/convertto-azurermvmmanageddisk) cmdlet'i. işlem dönüştürür aşağıdaki hello hello işletim sistemi diski ve veri diskleri dahil önceki VM hello:

  ```powershell
  ConvertTo-AzureRmVMManagedDisk -ResourceGroupName $rgName -VMName $vmName
  ```

3. Merhaba VM hello dönüştürme toomanaged diskleri sonra başlamayı [Start-AzureRmVM](/powershell/module/azurerm.compute/start-azurermvm). Aşağıdaki örnek yeniden hello önceki VM hello:

  ```powershell
  Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
  ```


## <a name="convert-vms-in-an-availability-set"></a>Sanal makineleri bir kullanılabilirlik kümesine Dönüştür

Tooconvert toomanaged disklerdir bir kullanılabilirlik kümesinde istediğiniz hello VM'ler, ilk tooconvert hello kullanılabilirlik kümesi tooa yönetilen ihtiyacınız varsa kullanılabilirlik kümesi.

1. Merhaba kullanılabilirlik Hello kullanarak kümesi Dönüştür [güncelleştirme AzureRmAvailabilitySet](/powershell/module/azurerm.compute/update-azurermavailabilityset) cmdlet'i. Aşağıdaki güncelleştirmeler hello kullanılabilirlik adlandırılmış kümesi örneğine hello `myAvailabilitySet` adlı hello kaynak grubunda `myResourceGroup`:

  ```powershell
  $rgName = 'myResourceGroup'
  $avSetName = 'myAvailabilitySet'

  $avSet = Get-AzureRmAvailabilitySet -ResourceGroupName $rgName -Name $avSetName
  Update-AzureRmAvailabilitySet -AvailabilitySet $avSet -Sku Aligned 
  ```

  Yalnızca 2 yönetilen hata etki alanı kullanılabilirlik kümesi bulunduğu hello bölge vardır ancak hello numarası yönetilmeyen hata etki alanı 3, bu komutu bir hata benzer gösterir çok "Merhaba hata etki alanı sayısı 3 hello aralığı 1 too2 dönmesi gerekir belirtilirse." hata, güncelleştirme hello hata etki alanı too2 ve güncelleştirme tooresolve hello `Sku` çok`Aligned` gibi:

  ```powershell
  $avSet.PlatformFaultDomainCount = 2
  Update-AzureRmAvailabilitySet -AvailabilitySet $avSet -Sku Aligned
  ```

2. Deallocate ve hello VM'ler hello kullanılabilirlik kümesindeki dönüştürün. Merhaba aşağıdaki komut dosyası her VM hello kullanarak kaldırır [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) cmdlet'ini dönüştürür onu kullanarak [ConvertTo-AzureRmVMManagedDisk](/powershell/module/azurerm.compute/convertto-azurermvmmanageddisk)ve kullanarak yeniden [Start-AzureRmVM ](/powershell/module/azurerm.compute/start-azurermvm):

  ```powershell
  $avSet = Get-AzureRmAvailabilitySet -ResourceGroupName $rgName -Name $avSetName

  foreach($vmInfo in $avSet.VirtualMachinesReferences)
  {
     $vm = Get-AzureRmVM -ResourceGroupName $rgName | Where-Object {$_.Id -eq $vmInfo.id}
     Stop-AzureRmVM -ResourceGroupName $rgName -Name $vm.Name -Force
     ConvertTo-AzureRmVMManagedDisk -ResourceGroupName $rgName -VMName $vm.Name
     Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
  }
  ```


## <a name="troubleshooting"></a>Sorun giderme

Dönüştürme sırasında bir hata varsa veya bir VM önceki dönüştürme sorunları nedeniyle başarısız bir durumda ise, hello çalıştırın `ConvertTo-AzureRmVMManagedDisk` cmdlet'ini yeniden. Basit bir yeniden deneme genellikle hello durum kaldırır.


## <a name="next-steps"></a>Sonraki adımlar

[Standart yönetilen disk toopremium Dönüştür](convert-disk-storage.md)

Kullanarak bir VM salt okunur bir kopyasını alın [anlık görüntüleri](snapshot-copy-managed-disk.md).

