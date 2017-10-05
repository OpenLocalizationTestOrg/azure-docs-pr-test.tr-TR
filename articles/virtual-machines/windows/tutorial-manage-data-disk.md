---
title: "Azure PowerShell ile Azure diskleri yönetme | Microsoft Docs"
description: "Öğretici - Azure PowerShell ile Azure diskleri yönetme"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 6f1bc9361745adc211f22416a7ba8ac1b8dc614e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-azure-disks-with-powershell"></a>PowerShell ile Azure diskleri yönetme

Azure sanal makineleri diskleri sanal makineleri işletim sistemi, uygulamaları ve verileri depolamak için kullanır. Bir VM oluşturulurken bir disk boyutu ve beklenen iş yükü için uygun yapılandırma seçmek önemlidir. Bu öğretici, dağıtma ve VM diskleri yönetme kapsar. Hakkında bilgi edinin:

> [!div class="checklist"]
> * İşletim sistemi ve geçici disklerle
> * Veri diskleri
> * Standart ve Premium diskleri
> * Disk performansı
> * Ekleme ve veri diskleri hazırlama

Bu öğretici, Azure PowerShell modülü 3.6 veya sonraki bir sürümü gerektirir. Sürümü bulmak için ` Get-Module -ListAvailable AzureRM` komutunu çalıştırın. Yükseltme gerekiyorsa, bkz: [yükleme Azure PowerShell Modülü](/powershell/azure/install-azurerm-ps).

## <a name="default-azure-disks"></a>Azure diskleri varsayılan

Bir Azure sanal makine oluşturulduğunda, iki disk otomatik olarak sanal makineye bağlanmış. 

**İşletim sistemi diski** -işletim sistemi disklerinde en fazla 1 terabayttan küçük boyuta sahip ve VM'ler işletim sistemi barındırır.  İşletim sistemi diski bir sürücü harfi atanmış *c:* varsayılan olarak. İşletim sistemi disk yapılandırması önbelleğe alma disk işletim sistemi performans için optimize edilmiştir. İşletim sistemi diski **vermemelisiniz** konak uygulamalar veya veri. Uygulamalar ve veriler için bu makalenin sonraki bölümlerinde ayrıntılı bir veri diski kullanın.

**Geçici disk** -geçici diskleri VM ile aynı Azure konakta bulunan bir katı hal sürücüsü kullanın. Temp disklerinin yüksek oranda kullanıcı durumda ve geçici veri işleme gibi işlemler için kullanılabilir. Ancak, VM yeni bir ana bilgisayara taşındığında, geçici bir diskte depolanan tüm verileri kaldırılır. Geçici disk boyutunu VM boyutu tarafından belirlenir. Geçici diskleri bir sürücü harfi atanmış *d:* varsayılan olarak.

### <a name="temporary-disk-sizes"></a>Geçici disk boyutları

| Tür | VM boyutu | En büyük geçici disk boyutu (GB) |
|----|----|----|
| [Genel amaçlı](sizes-general.md) | A ve D serisi | 800 |
| [İşlem için iyileştirilmiş](sizes-compute.md) | F serisi | 800 |
| [Bellek için iyileştirilmiş](../virtual-machines-windows-sizes-memory.md) | D ve G serisi | 6144 |
| [Depolama için iyileştirilmiş](../virtual-machines-windows-sizes-storage.md) | L serisi | 5630 |
| [GPU](sizes-gpu.md) | N serisi | 1440 |
| [Yüksek performans](sizes-hpc.md) | A ve H serisi | 2000 |

## <a name="azure-data-disks"></a>Azure veri diski

Uygulama yükleme ve verilerini depolamak için ek veri disklerinin eklenebilir. Veri diskleri sağlam ve esnek veri depolama burada istenen herhangi bir durumda kullanılmalıdır. Her veri diski 1 terabayttan küçük maksimum kapasitesine sahiptir. Kaç tane veri diskleri için bir VM eklenebilecek sanal makine boyutunu belirler. Her VM çekirdek için iki veri diskleri eklenebilir. 

### <a name="max-data-disks-per-vm"></a>VM başına en fazla veri diski

| Tür | VM boyutu | VM başına en fazla veri diski |
|----|----|----|
| [Genel amaçlı](sizes-general.md) | A ve D serisi | 32 |
| [İşlem için iyileştirilmiş](sizes-compute.md) | F serisi | 32 |
| [Bellek için iyileştirilmiş](../virtual-machines-windows-sizes-memory.md) | D ve G serisi | 64 |
| [Depolama için iyileştirilmiş](../virtual-machines-windows-sizes-storage.md) | L serisi | 64 |
| [GPU](sizes-gpu.md) | N serisi | 48 |
| [Yüksek performans](sizes-hpc.md) | A ve H serisi | 32 |

## <a name="vm-disk-types"></a>VM disk türleri

Azure disk iki tür sağlar.

### <a name="standard-disk"></a>Standart disk

Standart Depolama, HDD’ler ile desteklenir ve yüksek performans sunarken uygun maliyetli depolama sağlar. Standart diskler için uygun maliyetli geliştirme idealdir ve iş yükü test.

### <a name="premium-disk"></a>Premium disk

Premium diskler, SSD tabanlı yüksek performanslı, düşük gecikme süreli disk tarafından desteklenir. Üretim iş yükü çalıştıran VM'ler için mükemmel. Premium depolama destekleyen DS serisi, DSv2 serisi, GS serisi ve FS-serisi VM'ler. Üç tür (P10, P20, P30) Premium diskleri gelir, disk türü disk boyutunu belirler. Disk boyutu değeri seçerken, sonraki türü yuvarlanır. 128 GB boyutu ise, örneğin, disk türünü P10, 129 ve 512 P20 ve üzerinde 512 P30 arasında olacaktır. 

### <a name="premium-disk-performance"></a>Premium disk performansı

|Premium depolama disk türü | P10 | P20 | P30 |
| --- | --- | --- | --- |
| Disk boyutu (yukarı yuvarlar) | 128 GB | 512 GB | 1.024 GB (1 TB) |
| Disk başına IOPS | 500 | 2,300 | 5,000 |
Disk başına aktarım hızı | 100 MB/s | 150 MB/s | 200 MB/sn |

Yukarıdaki tabloda, disk başına maksimum IOPS tanımlanmaktadır olsa da, daha yüksek düzeyde performans birden çok veri diskleri bölümlemesine tarafından elde edilebilir. Örneğin, 64 veri diskleri Standard_GS5 VM eklenebilir. Her bu disklerin P30 boyuta sahip değilse, en fazla 80.000 IOPS elde edilebilir. VM başına maksimum IOPS hakkında ayrıntılı bilgi için bkz: [Linux VM boyutları](./sizes.md).

## <a name="create-and-attach-disks"></a>Oluşturma ve diskleri ekleme

Örneğin bu öğreticiyi tamamlamak için var olan bir sanal makine olması gerekir. Gerekirse, bu [komut dosyası örneği](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) sizin için bir tane oluşturabilirsiniz. Çalışma öğretici aracılığıyla değiştirdiğinizde VM ve kaynak grubu adları gerektiğinde.

İlk yapılandırma ile oluşturmayı [yeni AzureRmDiskConfig](/powershell/module/azurerm.compute/new-azurermdiskconfig). Aşağıdaki örnek boyutu 128 gigabayt bir disk yapılandırır.

```powershell
$diskConfig = New-AzureRmDiskConfig -Location EastUS -CreateOption Empty -DiskSizeGB 128
```

Sahip veri diski oluşturma [yeni AzureRmDisk](/powershell/module/azurerm.compute/new-azurermdisk) komutu.

```powershell
$dataDisk = New-AzureRmDisk -ResourceGroupName myResourceGroup -DiskName myDataDisk -Disk $diskConfig
```

İle verileri diske eklemek istediğiniz sanal makine Al [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) komutu.

```powershell
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroup -Name myVM
```

Sanal makine yapılandırması için veri diski Ekle [Ekle AzureRmVMDataDisk](/powershell/module/azurerm.compute/add-azurermvmdatadisk) komutu.

```powershell
$vm = Add-AzureRmVMDataDisk -VM $vm -Name myDataDisk -CreateOption Attach -ManagedDiskId $dataDisk.Id -Lun 1
```

Sanal makineyle güncelleştirme [güncelleştirme-AzureRmVM](/powershell/module/azurerm.compute/add-azurermvmdatadisk) komutu.

```powershell
Update-AzureRmVM -ResourceGroupName myResourceGroup -VM $vm
```

## <a name="prepare-data-disks"></a>Veri diskleri hazırlama

Bir disk sanal makineye bağlandıktan sonra işletim sistemi diski kullanacak şekilde yapılandırılması gerekir. Aşağıdaki örnek VM eklenen ilk diski el ile yapılandırmak nasıl gösterir. Bu işlem ayrıca kullanarak otomatikleştirilebilir [özel betik uzantısı](./tutorial-automate-vm-deployment.md).

### <a name="manual-configuration"></a>El ile yapılandırma

RDP bağlantısı ile sanal makine oluşturun. PowerShell'i açın ve bu komut dosyasını çalıştırın.

```powershell
Get-Disk | Where partitionstyle -eq 'raw' | `
Initialize-Disk -PartitionStyle MBR -PassThru | `
New-Partition -AssignDriveLetter -UseMaximumSize | `
Format-Volume -FileSystem NTFS -NewFileSystemLabel "myDataDisk" -Confirm:$false
```

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide, VM diskleri konuları hakkında gibi öğrenilen:

> [!div class="checklist"]
> * İşletim sistemi ve geçici disklerle
> * Veri diskleri
> * Standart ve Premium diskleri
> * Disk performansı
> * Ekleme ve veri diskleri hazırlama

VM yapılandırması otomatikleştirme hakkında bilgi edinmek için sonraki öğretici ilerleyin.

> [!div class="nextstepaction"]
> [VM yapılandırmasını otomatikleştirme](./tutorial-automate-vm-deployment.md)
