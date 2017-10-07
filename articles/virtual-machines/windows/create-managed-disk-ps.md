---
title: "aaaCreate Azure VHD'yi yönetilen bir diskten | Microsoft Docs"
description: "Yönetilen bir disk hello Resource Manager dağıtım modelini kullanarak bir Azure depolama hesabında şu anda olan bir VHD'den oluşturun."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/05/2017
ms.author: cynthn
ms.openlocfilehash: 77adaac5419186ff85039fe2c4752f021aa5e448
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-managed-disks-from-unmanaged-disks-in-a-storage-account"></a>Bir depolama hesabı yönetilmeyen disklerden yönetilen diskleri oluşturma

Yönetilen bir disk, varolan bir veri diski veya bir Azure depolama hesabında şu anda olan işletim sistemi diski oluşturulabilir. Ayrıca, bir VM için yeni bir veri diski olarak kullanılabilmesi için boş bir disk oluşturabilirsiniz. 

## <a name="before-you-begin"></a>Başlamadan önce
PowerShell'i kullanırsanız, hello hello AzureRM.Compute PowerShell modülü en son sürümüne sahip olduğunuzdan emin olun. Çalıştırma hello komut tooinstall onu.

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
Daha fazla bilgi için bkz: [Azure PowerShell sürüm](/powershell/azure/overview).


## <a name="create-a-managed-disk-from-a-vhd-in-an-azure-storage-account"></a>Bir Azure depolama hesabındaki bir VHD'den yönetilen bir disk oluşturma

Yönetilen disk olarak bir VHD'den disk oluştur ve toohello parametresi atamak hello örnekte **$ disk 1** toouse daha sonra. 

Merhaba yönetilen disk hello oluşturulacak **Batı ABD** konumda adlı bir kaynak grubu **myResourceGroup**. Merhaba disk adlı **myDisk** ve adlı bir VHD dosyasından oluşturulacak **myDisk.vhd** biz adlı tooa depolama hesabı daha önce karşıya **mystorageaccount**. Merhaba yönetilen disk premium yerel olarak yedekli depolama (LRS) oluşturulur. StandardLRS ve PremiumLRS olan hello yalnızca **- AccountType** için kullanılabilir seçenekleri yönetilen diskler. 

1.  Bazı parametreler Ayarla

    ```powershell
    $rgName = "myResourceGroup"
    $location = "West Central US"
    $diskName = "myDisk"
    $vhdUri = "https://mystorageaccount.blob.core.windows.net/vhds/myDisk.vhd"
    ```

2. Merhaba veri diski oluşturun. 
    ```powershell
    $disk1 = New-AzureRmDisk -DiskName $diskName -Disk (New-AzureRmDiskConfig -AccountType PremiumLRS -Location $location -CreateOption Import -SourceUri $vhdUri) -ResourceGroupName $rgName
    ```
    
    

## <a name="create-an-empty-data-disk-as-a-managed-disk"></a>Boş veri diski yönetilen bir disk oluşturma

Boş veri diski yönetilen disk olarak oluşturun ve toohello parametresi atamak hello örnekte **$dataDisk2** toouse daha sonra. Boş veri diskini toohello VM günlüğe kaydetme ve diskmgmt.msc kullanarak başlatılmış toobe gerekir veya [WinRM ve bir komut dosyası kullanarak uzaktan](attach-disk-ps.md#initialize-the-disk), VM çalıştıran ekli tooa olduğunda.

Merhaba boş veri diski hello oluşturulacak **Batı Orta ABD** konumda adlı bir kaynak grubu **myResourceGroup**. Merhaba disk adlı **myEmptyDataDisk**. Merhaba boş disk premium yerel olarak yedekli depolama (LRS) oluşturulur. StandardLRS ve PremiumLRS olan hello yalnızca **- AccountType** için kullanılabilir seçenekleri yönetilen diskler.

Bu örnekte Hello disk boyutu, 128 GB olmakla birlikte, VM'de çalışan herhangi bir uygulama, hello gereksinimlerini karşılayan bir boyut seçmeniz gerekir.

1.  Bazı parametreler Ayarla

    ```powershell
    $rgName = "myResourceGroup"
    $location = "West Central US"
    $dataDiskName = "myEmptyDataDisk"
    ```

2. Merhaba veri diski oluşturun.
    ```powershell
    $dataDisk2 = New-AzureRmDisk -DiskName $dataDiskName -Disk (New-AzureRmDiskConfig -AccountType PremiumLRS -Location $location -CreateOption Empty -DiskSizeGB 128) -ResourceGroupName $rgName
    ```
    
## <a name="next-steps"></a>Sonraki Adımlar   
- Bir VM zaten varsa, [bir veri diskini](attach-disk-portal.md).
