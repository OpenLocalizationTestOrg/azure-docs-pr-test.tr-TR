---
title: bir Windows VM - Azure veri diskten aaaDetach | Microsoft Docs
description: "Toodetach hello Resource Manager dağıtım modelini kullanarak azure'da bir sanal makineden bir veri diski öğrenin."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 13180343-ac49-4a3a-85d8-0ead95e2028c
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/21/2017
ms.author: cynthn
ms.openlocfilehash: f3f581d3f33329db2ecb7d25a68bc59af7361aad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodetach-a-data-disk-from-a-windows-virtual-machine"></a>Nasıl toodetach bir veri diski bir Windows sanal makineden
Ekli tooa sanal makine veri diski artık ihtiyacınız olduğunda, kolayca ayırabilirsiniz. Bu hello disk hello sanal makineden kaldırır, ancak depolama biriminden kaldırmaz.

> [!WARNING]
> Bir disk ayırırsanız otomatik olarak silinmez. TooPremium depolama abone hello disk için tooincur depolama ücretleri devam eder. Daha fazla bilgi için çok başvurun[fiyatlandırma ve faturalama Premium depolama kullanırken](../../storage/common/storage-premium-storage.md#pricing-and-billing).
>
>

Merhaba disk üzerindeki toouse hello mevcut verileri yeniden istiyorsanız, toohello iliştirebilirsiniz aynı sanal makine ya da başka bir.

## <a name="detach-a-data-disk-using-hello-portal"></a>Merhaba portalı kullanarak bir veri diskini
1. Merhaba portal hub, seçin **sanal makineleri**.
2. Toodetach istediğiniz hello veri diski Hello sanal makine seçin **durdurmak** toodeallocate hello VM.
3. Merhaba sanal makine dikey penceresinde, seçin **diskleri**.
4. Merhaba hello üstündeki **diskleri** dikey penceresinde, select **Düzenle**.
5. Merhaba, **diskleri** dikey, sağda hello veri diski toodetach, istediğiniz toohello tıklayın hello ![ayırma düğme görüntüsü](./media/detach-disk/detach.png) düğmesi ayırma.
5. Merhaba disk kaldırıldıktan sonra hello dikey penceresinde hello üstündeki Kaydet.
6. Merhaba sanal makine dikey penceresinde tıklayın **genel bakış** ve hello ardından **Başlat** hello dikey toorestart hello VM hello üstündeki düğmesi.



Merhaba disk depolama alanında kalır, ancak artık ekli tooa sanal makine değil.

## <a name="detach-a-data-disk-using-powershell"></a>PowerShell kullanarak bir veri diskini
Bu örnekte, ilk komut alır hello adlı sanal makineye hello **MyVM07** hello içinde **RG11** hello Get-AzureRmVM cmdlet'ini kullanarak kaynak grubu. Merhaba depoları hello hello sanal makinede komut **$VirtualMachine** değişkeni.

Merhaba ikinci komut hello sanal makineden DataDisk3 adlı hello veri diski kaldırır.

Merhaba son komut hello veri diski kaldırmanın hello sanal makine toocomplete hello işlemi hello durumunu güncelleştirir.

```powershell
$VirtualMachine = Get-AzureRmVM -ResourceGroupName "RG11" -Name "MyVM07"
Remove-AzureRmVMDataDisk -VM $VirtualMachine -Name "DataDisk3"
Update-AzureRmVM -ResourceGroupName "RG11" -Name "MyVM07" -VM $VirtualMachine
```

Daha fazla bilgi için bkz: [Kaldır AzureRmVMDataDisk](/powershell/module/azurerm.compute/remove-azurermvmdatadisk).

## <a name="next-steps"></a>Sonraki adımlar
Tooreuse hello veri diski istiyorsanız, yeni [tooanother VM ekleme](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

