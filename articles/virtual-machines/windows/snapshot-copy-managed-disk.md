---
title: "Yönetilen bir Azure diski geri için bir kopyasını oluştur | Microsoft Docs"
description: "Yedekleme için kullanılacak bir Azure yönetilen Disk veya disk sorunlarını giderme bir kopyasını oluşturmayı öğrenin."
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
ms.openlocfilehash: a7527b12f4f0d2b45713a0c0109d81ff51293fd8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-copy-of-a-vhd-stored-as-an-azure-managed-disk-by-using-managed-snapshots"></a>Yönetilen bir Azure diski yönetilen anlık görüntülerini kullanarak tarafından depolanan VHD bir kopyasını oluşturun
Yönetilen bir Disk Yedekleme için bir anlık görüntüsünü veya yönetilen bir Disk anlık görüntüden oluşturabilir ve sorun giderme için test sanal makineye Ekle. Yönetilen bir anlık görüntü yönetilen bir VM Disk noktası zaman tam kopyasıdır. Bu, VHD salt okunur bir kopyasını oluşturur ve isteğe bağlı olarak varsayılan olarak, standart yönetilen Disk olarak depolar. Yönetilen diskler hakkında daha fazla bilgi için bkz: [Azure yönetilen diskleri genel bakış](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

Fiyatlandırma hakkında daha fazla bilgi için bkz: [Azure Storage fiyatlandırması](https://azure.microsoft.com/pricing/details/managed-disks/). 

## <a name="before-you-begin"></a>Başlamadan önce
PowerShell'i kullanırsanız, AzureRM.Compute PowerShell modülü en son sürümüne sahip olduğunuzdan emin olun. Yüklemek için aşağıdaki komutu çalıştırın.

```
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
Daha fazla bilgi için bkz: [Azure PowerShell sürüm](/powershell/azure/overview).

## <a name="copy-the-vhd-with-a-snapshot"></a>VHD bir anlık görüntü ile kopyalama
Yönetilen diskin anlık görüntüsünü almak için Azure portal veya PowerShell kullanın.

### <a name="use-azure-portal-to-take-a-snapshot"></a>Bir anlık görüntüsünü için Azure portalını kullanma 

1. [Azure Portal](https://portal.azure.com) oturum açın.
2. Sol üst başlayarak, tıklatın **yeni** arayın ve **anlık görüntü**.
3. Anlık görüntü dikey penceresinde tıklayın **oluşturma**.
4. Girin bir **adı** anlık görüntü için.
5. Varolan [Kaynak grubunu](../../azure-resource-manager/resource-group-overview.md#resource-groups) seçin veya yenisi için adı yazın. 
6. Azure veri merkezi konum seçin.  
7. İçin **kaynak disk**, anlık görüntü için yönetilen diski seçin.
8. Seçin **hesap türü** anlık görüntü deposu için kullanılacak. Öneririz **Standard_LRS** yüksek performanslı bir diskte depolanan gerekmedikçe.
9. **Oluştur**'a tıklayın.

### <a name="use-powershell-to-take-a-snapshot"></a>Bir anlık görüntüsünü için PowerShell kullanma
Aşağıdaki adımlar VHD diskin kopyalanması, anlık görüntü yapılandırmaları oluşturmak ve yeni AzureRmSnapshot cmdlet'ini kullanarak bir disk anlık görüntüsünü alma gösterir<!--Add link to cmdlet when available-->. 

1. Bazı parametreler ayarlayın. 

 ```powershell
$resourceGroupName = 'myResourceGroup' 
$location = 'southeastasia' 
$dataDiskName = 'ContosoMD_datadisk1' 
$snapshotName = 'ContosoMD_datadisk1_snapshot1'  
```
  Parametre değerleri değiştirin:
  -  VM kaynak grubuyla "contoso.com".
  -  "southeastasia" yönetilen depolanan anlık coğrafi konumu ile. <!---How do you look these up? -->
  -  Kopyalamak istediğiniz VHD disk adı "ContosoMD_datadisk1".
  -  Yeni anlık görüntü için kullanmak istediğiniz adla "ContosoMD_datadisk1_snapshot1".

2. Kopyalanacak VHD disk alın.

 ```powershell
$disk = Get-AzureRmDisk -ResourceGroupName $resourceGroupName -DiskName $dataDiskName 
```
3. Anlık görüntü yapılandırmaları oluşturun. 

 ```powershell
$snapshot =  New-AzureRmSnapshotConfig -SourceUri $disk.Id -CreateOption Copy -Location $location 
```
4. Anlık görüntü alın.

 ```powershell
New-AzureRmSnapshot -Snapshot $snapshot -SnapshotName $snapshotName -ResourceGroupName $resourceGroupName 
```
Yönetilen bir Disk oluşturmak ve yüksek performanslı olması gereken bir VM eklemek için anlık görüntü kullanmayı planlıyorsanız, parametresini kullanın `-AccountType Premium_LRS` yeni AzureRmSnapshot komutu. Parametre anlık görüntü oluşturur, böylece yönetilen bir Premium Disk depolanır. Premium yönetilen diskleri standart daha pahalıdır. Bu nedenle bu parametrenin kullanmadan önce Premium gerçekten ihtiyacınız emin olun.


