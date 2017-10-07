---
title: aaaManage Azure diskleri hello Azure PowerShell ile | Microsoft Docs
description: "Öğretici - Azure diskleri hello Azure PowerShell ile yönetme"
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
ms.openlocfilehash: 2f61ad18bc94bab527d7ae593da603c6073adc89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-disks-with-powershell"></a>PowerShell ile Azure diskleri yönetme

Azure sanal makineleri diskleri toostore hello VM'ler işletim sistemi, uygulamaları ve verileri kullanın. Bir VM oluştururken önemli toochoose disk boyutu ve yapılandırma beklenen uygun toohello iş yüküne bağlıdır. Bu öğretici, dağıtma ve VM diskleri yönetme kapsar. Hakkında bilgi edinin:

> [!div class="checklist"]
> * İşletim sistemi ve geçici disklerle
> * Veri diskleri
> * Standart ve Premium diskleri
> * Disk performansı
> * Ekleme ve veri diskleri hazırlama

Bu öğretici hello Azure PowerShell modülü 3,6 veya sonraki bir sürümü gerektiriyor. Çalıştırma ` Get-Module -ListAvailable AzureRM` toofind hello sürümü. Tooupgrade gerekirse bkz [yükleme Azure PowerShell Modülü](/powershell/azure/install-azurerm-ps).

## <a name="default-azure-disks"></a>Azure diskleri varsayılan

Bir Azure sanal makine oluşturulduğunda, iki diskleri otomatik olarak eklenen toohello sanal makine içindir. 

**İşletim sistemi diski** - işletim sistemi disklerinde too1 terabayt boyutta ve ana hello VM'ler işletim sistemi.  Merhaba işletim sistemi diski bir sürücü harfi atanmış *c:* varsayılan olarak. Merhaba işletim sistemi disk yapılandırması önbelleğe alma hello disk işletim sistemi performans için optimize edilmiştir. Merhaba işletim sistemi disk **vermemelisiniz** konak uygulamalar veya veri. Uygulamalar ve veriler için bu makalenin sonraki bölümlerinde ayrıntılı bir veri diski kullanın.

**Geçici disk** -geçici diskler hello üzerinde bulunan bir katı hal sürücüsü kullanan aynı Azure ana bilgisayar hello VM olarak. Temp disklerinin yüksek oranda kullanıcı durumda ve geçici veri işleme gibi işlemler için kullanılabilir. Ancak, Hello VM taşınan tooa yeni ana bilgisayar ise, geçici bir diskte depolanan tüm verileri kaldırılır. Merhaba hello geçici disk boyutunu hello VM boyutu tarafından belirlenir. Geçici diskleri bir sürücü harfi atanmış *d:* varsayılan olarak.

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

Uygulama yükleme ve verilerini depolamak için ek veri disklerinin eklenebilir. Veri diskleri sağlam ve esnek veri depolama burada istenen herhangi bir durumda kullanılmalıdır. Her veri diski 1 terabayttan küçük maksimum kapasitesine sahiptir. kaç tane veri diskleri ekli tooa VM olabilir hello sanal makine Hello boyutunu belirler. Her VM çekirdek için iki veri diskleri eklenebilir. 

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

Premium diskler, SSD tabanlı yüksek performanslı, düşük gecikme süreli disk tarafından desteklenir. Üretim iş yükü çalıştıran VM'ler için mükemmel. Premium depolama destekleyen DS serisi, DSv2 serisi, GS serisi ve FS-serisi VM'ler. Üç tür (P10, P20, P30) Premium diskleri gelir, hello disk türü hello hello diskin boyutunu belirler. Seçerken, bir disk boyutu hello değeri toohello sonraki türü yuvarlanır. Örneğin, Hello boyutu 128 GB hello disk türü ise P10, 129 ve 512 P20 ve üzerinde 512 P30 arasında olacaktır. 

### <a name="premium-disk-performance"></a>Premium disk performansı

|Premium depolama disk türü | P10 | P20 | P30 |
| --- | --- | --- | --- |
| Disk boyutu (yukarı yuvarlar) | 128 GB | 512 GB | 1.024 GB (1 TB) |
| Disk başına IOPS | 500 | 2,300 | 5,000 |
Disk başına aktarım hızı | 100 MB/s | 150 MB/s | 200 MB/sn |

Disk başına maksimum IOPS Merhaba tablonun yukarısındaki tanımlayan olsa da, daha yüksek düzeyde performans birden çok veri diskleri bölümlemesine tarafından elde edilebilir. Örneğin, 64 veri diskleri olabilir tooStandard_GS5 VM bağlı. Her bu disklerin P30 boyuta sahip değilse, en fazla 80.000 IOPS elde edilebilir. VM başına maksimum IOPS hakkında ayrıntılı bilgi için bkz: [Linux VM boyutları](./sizes.md).

## <a name="create-and-attach-disks"></a>Oluşturma ve diskleri ekleme

Bu öğreticide toocomplete hello örnek, mevcut bir sanal makine olması gerekir. Gerekirse, bu [komut dosyası örneği](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) sizin için bir tane oluşturabilirsiniz. Çalışma hello öğretici aracılığıyla değiştirdiğinizde hello kaynak grubu VM adları ve gerektiğinde.

Merhaba ilk yapılandırma ile oluşturmayı [yeni AzureRmDiskConfig](/powershell/module/azurerm.compute/new-azurermdiskconfig). Aşağıdaki örnek hello 128 gigabayt cinsinden boyutu olan bir disk yapılandırır.

```powershell
$diskConfig = New-AzureRmDiskConfig -Location EastUS -CreateOption Empty -DiskSizeGB 128
```

Merhaba ile Merhaba veri diski oluşturma [yeni AzureRmDisk](/powershell/module/azurerm.compute/new-azurermdisk) komutu.

```powershell
$dataDisk = New-AzureRmDisk -ResourceGroupName myResourceGroup -DiskName myDataDisk -Disk $diskConfig
```

Tooadd hello veri diski toowith hello istediğiniz Get hello sanal makine [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) komutu.

```powershell
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroup -Name myVM
```

Ekle hello veri disk toohello sanal makine yapılandırmasıyla hello [Ekle AzureRmVMDataDisk](/powershell/module/azurerm.compute/add-azurermvmdatadisk) komutu.

```powershell
$vm = Add-AzureRmVMDataDisk -VM $vm -Name myDataDisk -CreateOption Attach -ManagedDiskId $dataDisk.Id -Lun 1
```

Merhaba sanal makine ile Merhaba güncelleştirme [güncelleştirme-AzureRmVM](/powershell/module/azurerm.compute/add-azurermvmdatadisk) komutu.

```powershell
Update-AzureRmVM -ResourceGroupName myResourceGroup -VM $vm
```

## <a name="prepare-data-disks"></a>Veri diskleri hazırlama

Bir disk ekli toohello sanal makine sağlandıktan sonra yapılandırılmış toobe toouse hello disk hello işletim sistemi gerekir. Merhaba aşağıdaki örnekte nasıl toomanually yapılandırmak hello ilk disk eklenen gösterir toohello VM. Bu işlem ayrıca hello kullanarak otomatikleştirilebilir [özel betik uzantısı](./tutorial-automate-vm-deployment.md).

### <a name="manual-configuration"></a>El ile yapılandırma

RDP bağlantısı ile Merhaba sanal makine oluşturun. PowerShell'i açın ve bu komut dosyasını çalıştırın.

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

VM yapılandırması otomatikleştirme hakkında toohello sonraki öğretici toolearn ilerleyin.

> [!div class="nextstepaction"]
> [VM yapılandırmasını otomatikleştirme](./tutorial-automate-vm-deployment.md)
