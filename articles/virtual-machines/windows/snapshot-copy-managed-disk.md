---
title: "bir yedekleme için bir Azure yönetilen diski kopyasını aaaCreate | Microsoft Docs"
description: "Azure yönetilen diski toouse geri yukarı veya sorun giderme disk için bir kopyasını toocreate nasıl sorunları hakkında bilgi edinin."
documentationcenter: 
author: cwatson-cat
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 15eb778e-fc07-45ef-bdc8-9090193a6d20
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 2/9/2017
ms.author: cwatson
ms.openlocfilehash: 2f33dbbee624bcd813f3c7c3e3401072d0933714
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-vhd-stored-as-an-azure-managed-disk-by-using-managed-snapshots"></a>Yönetilen bir Azure diski yönetilen anlık görüntülerini kullanarak tarafından depolanan VHD bir kopyasını oluşturun
Yönetilen bir Disk Yedekleme için bir anlık görüntüsünü veya yönetilen bir Disk hello anlık görüntüden oluşturmak ve tooa test sanal makinesi tootroubleshoot ekleyin. Yönetilen bir anlık görüntü yönetilen bir VM Disk noktası zaman tam kopyasıdır. Bu, VHD salt okunur bir kopyasını oluşturur ve isteğe bağlı olarak varsayılan olarak, standart yönetilen Disk olarak depolar. Yönetilen diskler hakkında daha fazla bilgi için bkz: [Azure yönetilen diskleri genel bakış](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

Fiyatlandırma hakkında daha fazla bilgi için bkz: [Azure Storage fiyatlandırması](https://azure.microsoft.com/pricing/details/managed-disks/). 

## <a name="before-you-begin"></a>Başlamadan önce
PowerShell'i kullanırsanız, hello hello AzureRM.Compute PowerShell modülü en son sürümüne sahip olduğunuzdan emin olun. Çalıştırma hello komut tooinstall onu.

```
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
Daha fazla bilgi için bkz: [Azure PowerShell sürüm](/powershell/azure/overview).

## <a name="copy-hello-vhd-with-a-snapshot"></a>Merhaba VHD anlık görüntüleri kopyalama
Hello Azure portal veya PowerShell tootake hello yönetilen Disk görüntüsünü kullanın.

### <a name="use-azure-portal-tootake-a-snapshot"></a>Azure portal tootake bir anlık görüntü kullanın 

1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. Merhaba üst sol başlayarak, tıklatın **yeni** arayın ve **anlık görüntü**.
3. Başlangıç anlık görüntü dikey penceresinde tıklayın **oluşturma**.
4. Girin bir **adı** hello anlık görüntü için.
5. Var olan seçin [kaynak grubu](../../azure-resource-manager/resource-group-overview.md#resource-groups) veya yeni bir hello adını yazın. 
6. Azure veri merkezi konum seçin.  
7. İçin **kaynak disk**, hello yönetilen Disk toosnapshot seçin.
8. Select hello **hesap türü** toouse toostore hello anlık görüntü. Öneririz **Standard_LRS** yüksek performanslı bir diskte depolanan gerekmedikçe.
9. **Oluştur**'a tıklayın.

### <a name="use-powershell-tootake-a-snapshot"></a>PowerShell tootake bir anlık görüntü kullanın
Hello aşağıdaki adımları nasıl tooget hello VHD disk kopyalanan toobe Göster, anlık görüntü yapılandırmaları hello oluşturmak ve hello yeni AzureRmSnapshot cmdlet'ini kullanarak hello disk bir anlık görüntüsünü<!--Add link toocmdlet when available-->. 

1. Bazı parametreler ayarlayın. 

 ```powershell
$resourceGroupName = 'myResourceGroup' 
$location = 'southeastasia' 
$dataDiskName = 'ContosoMD_datadisk1' 
$snapshotName = 'ContosoMD_datadisk1_snapshot1'  
```
  Merhaba parametre değerlerini değiştirin:
  -  "contoso.com" Merhaba VM'in kaynak grubu ile.
  -  "southeastasia" yönetilen depolanan anlık hello coğrafi konumu ile. <!---How do you look these up? -->
  -  "ContosoMD_datadisk1" Merhaba adla hello VHD disk toocopy istiyor.
  -  "ContosoMD_datadisk1_snapshot1" Merhaba ile ad hello yeni bir anlık görüntü için toouse istiyor.

2. Kopyalanan hello VHD disk toobe alın.

 ```powershell
$disk = Get-AzureRmDisk -ResourceGroupName $resourceGroupName -DiskName $dataDiskName 
```
3. Merhaba, anlık görüntü yapılandırmaları oluşturun. 

 ```powershell
$snapshot =  New-AzureRmSnapshotConfig -SourceUri $disk.Id -CreateOption Copy -Location $location 
```
4. Başlangıç anlık görüntü alın.

 ```powershell
New-AzureRmSnapshot -Snapshot $snapshot -SnapshotName $snapshotName -ResourceGroupName $resourceGroupName 
```
Yönetilen bir Disk toouse hello anlık görüntü toocreate planlamak ve toobe yüksek performanslı gereken VM ekleme, hello parametresini kullanmanız `-AccountType Premium_LRS` hello yeni AzureRmSnapshot komutu. Merhaba parametre hello anlık görüntü oluşturur, böylece yönetilen bir Premium Disk depolanır. Premium yönetilen diskleri standart daha pahalıdır. Bu nedenle bu parametrenin kullanmadan önce Premium gerçekten ihtiyacınız emin olun.


