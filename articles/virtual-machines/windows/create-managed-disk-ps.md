---
title: "Azure'da bir VHD'den yönetilen bir disk oluşturma | Microsoft Docs"
description: "Yönetilen bir disk Resource Manager dağıtım modelini kullanarak bir Azure depolama hesabında şu anda olan bir VHD'den oluşturun."
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
ms.openlocfilehash: c03ebf73f1090b595149daf2eb3e274b05822f4f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-managed-disks-from-unmanaged-disks-in-a-storage-account"></a>Bir depolama hesabı yönetilmeyen disklerden yönetilen diskleri oluşturma

Yönetilen bir disk, varolan bir veri diski veya bir Azure depolama hesabında şu anda olan işletim sistemi diski oluşturulabilir. Ayrıca, bir VM için yeni bir veri diski olarak kullanılabilmesi için boş bir disk oluşturabilirsiniz. 

## <a name="before-you-begin"></a>Başlamadan önce
PowerShell'i kullanırsanız, AzureRM.Compute PowerShell modülü en son sürümüne sahip olduğunuzdan emin olun. Yüklemek için aşağıdaki komutu çalıştırın.

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
Daha fazla bilgi için bkz: [Azure PowerShell sürüm](/powershell/azure/overview).


## <a name="create-a-managed-disk-from-a-vhd-in-an-azure-storage-account"></a>Bir Azure depolama hesabındaki bir VHD'den yönetilen bir disk oluşturma

Yönetilen disk olarak bir VHD'den disk oluştur ve parametreye atayın örnekte **$ disk 1** daha sonra kullanmak üzere. 

Yönetilen disk içinde oluşturulacak **Batı ABD** konumda adlı bir kaynak grubu **myResourceGroup**. Disk adında **myDisk** ve adlı bir VHD dosyasından oluşturulacak **myDisk.vhd** biz adlı bir depolama hesabı için daha önce karşıya **mystorageaccount**. Yönetilen disk premium yerel olarak yedekli depolama (LRS) oluşturulur. StandardLRS ve PremiumLRS olan tek **- AccountType** için kullanılabilir seçenekleri yönetilen diskler. 

1.  Bazı parametreler Ayarla

    ```powershell
    $rgName = "myResourceGroup"
    $location = "West Central US"
    $diskName = "myDisk"
    $vhdUri = "https://mystorageaccount.blob.core.windows.net/vhds/myDisk.vhd"
    ```

2. Veri diski oluşturun. 
    ```powershell
    $disk1 = New-AzureRmDisk -DiskName $diskName -Disk (New-AzureRmDiskConfig -AccountType PremiumLRS -Location $location -CreateOption Import -SourceUri $vhdUri) -ResourceGroupName $rgName
    ```
    
    

## <a name="create-an-empty-data-disk-as-a-managed-disk"></a>Boş veri diski yönetilen bir disk oluşturma

Boş veri diski yönetilen disk olarak oluşturun ve parametreye atayın örnekte **$dataDisk2** daha sonra kullanmak üzere. Boş veri diski başlatılmış VM'ye oturum açmayı ve diskmgmt.msc kullanarak olması gerekir veya [WinRM ve bir komut dosyası kullanarak uzaktan](attach-disk-ps.md#initialize-the-disk), çalışan bir VM bağlandıktan sonra.

Boş veri diski içinde oluşturulacak **Batı Orta ABD** konumda adlı bir kaynak grubu **myResourceGroup**. Disk adında **myEmptyDataDisk**. Premium yerel olarak yedekli depolama (LRS) boş disk oluşturulur. StandardLRS ve PremiumLRS olan tek **- AccountType** için kullanılabilir seçenekleri yönetilen diskler.

Bu örnekte disk boyutu, 128 GB olmakla birlikte, VM üzerinde çalışan uygulamaların gereksinimlerini karşılayan bir boyut seçmeniz gerekir.

1.  Bazı parametreler Ayarla

    ```powershell
    $rgName = "myResourceGroup"
    $location = "West Central US"
    $dataDiskName = "myEmptyDataDisk"
    ```

2. Veri diski oluşturun.
    ```powershell
    $dataDisk2 = New-AzureRmDisk -DiskName $dataDiskName -Disk (New-AzureRmDiskConfig -AccountType PremiumLRS -Location $location -CreateOption Empty -DiskSizeGB 128) -ResourceGroupName $rgName
    ```
    
## <a name="next-steps"></a>Sonraki Adımlar   
- Bir VM zaten varsa, [bir veri diskini](attach-disk-portal.md).
