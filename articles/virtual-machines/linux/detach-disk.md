---
title: bir Linux VM - Azure veri diskten aaaDetach | Microsoft Docs
description: "Toodetach CLI 2.0 veya hello Azure portal kullanarak azure'da bir sanal makineden bir veri diski öğrenin."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: azurecli
ms.topic: article
ms.date: 03/21/2017
ms.author: cynthn
ms.openlocfilehash: 1c6145fc97f13179457225e93e0fb7adc261a65b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodetach-a-data-disk-from-a-linux-virtual-machine"></a>Nasıl toodetach bir veri diski bir Linux sanal makineden

Ekli tooa sanal makine veri diski artık ihtiyacınız olduğunda, kolayca ayırabilirsiniz. Bu hello disk hello sanal makineden kaldırır, ancak depolama biriminden kaldırmaz. 

> [!WARNING]
> Bir disk ayırırsanız otomatik olarak silinmez. TooPremium depolama abone hello disk için tooincur depolama ücretleri devam eder. Daha fazla bilgi için çok başvurun[fiyatlandırma ve faturalama Premium depolama kullanırken](../../storage/common/storage-premium-storage.md#pricing-and-billing). 
> 
> 

Merhaba disk üzerindeki toouse hello mevcut verileri yeniden istiyorsanız, toohello iliştirebilirsiniz aynı sanal makine ya da başka bir.  

## <a name="detach-a-data-disk-using-cli-20"></a>CLI 2.0 kullanan bir veri diskini

```azurecli
az vm disk detach -g myResourceGroup --vm-name myVm -n myDataDisk
```

Merhaba disk depolama alanında kalır, ancak artık ekli tooa sanal makine değil.


## <a name="detach-a-data-disk-using-hello-portal"></a>Merhaba portalı kullanarak bir veri diskini
1. Merhaba portal hub, seçin **sanal makineleri**.
2. Toodetach istediğiniz hello veri diski Hello sanal makine seçin **durdurmak** toodeallocate hello VM.
3. Merhaba sanal makine dikey penceresinde, seçin **diskleri**.
4. Merhaba hello üstündeki **diskleri** dikey penceresinde, select **Düzenle**.
5. Merhaba, **diskleri** dikey, sağda hello veri diski toodetach, istediğiniz toohello tıklayın hello ![ayırma düğme görüntüsü](./media/detach-disk/detach.png) düğmesi ayırma.
5. Merhaba disk kaldırıldıktan sonra hello dikey penceresinde hello üstündeki Kaydet.
6. Merhaba sanal makine dikey penceresinde tıklayın **genel bakış** ve hello ardından **Başlat** hello dikey toorestart hello VM hello üstündeki düğmesi.

Merhaba disk depolama alanında kalır, ancak artık ekli tooa sanal makine değil.








## <a name="next-steps"></a>Sonraki adımlar
Tooreuse hello veri diski istiyorsanız, yeni [tooanother VM ekleme](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

