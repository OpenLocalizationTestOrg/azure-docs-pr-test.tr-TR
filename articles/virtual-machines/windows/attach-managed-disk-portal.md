---
title: "aaaAttach bir yönetilen veri diski tooa Windows VM - Azure | Microsoft Docs"
description: "Veri diski tooa tooattach yeni yönetilen nasıl hello Azure portal kullanarak Windows VM Resource Manager dağıtım modeli hello."
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
ms.date: 05/09/2017
ms.author: cynthn
ms.openlocfilehash: bacc0589ad2d93e4d3d055c8f837f8db27291ead
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooattach-a-managed-data-disk-tooa-windows-vm-in-hello-azure-portal"></a>Nasıl tooattach yönetilen bir veri diski hello Azure portal'ın Windows VM tooa

Bu makale size nasıl tooattach yeni yönetilen bir veri diski hello Azure portal ile tooWindows sanal makineleri gösterir. Bunu önce bu ipuçlarını gözden geçirin:

* Merhaba boyutunu hello sanal makine, iliştirebilirsiniz kaç tane veri diskleri denetler. Ayrıntılar için bkz [sanal makineler için Boyutlar](sizes.md).
* Yeni bir disk için toocreate gerekmez, ilk bunu eklediğinizde Azure bunu oluşturduğundan.

Ayrıca [Powershell kullanarak bir veri diskini](attach-disk-ps.md).



## <a name="add-a-data-disk"></a>Bir veri diski Ekle
1. Merhaba soldaki Hello menüde tıklatın **sanal makineleri**.
2. Merhaba sanal makine hello listeden seçin.
3. Merhaba sanal makine dikey penceresinde **diskleri**.
   4. Merhaba üzerinde **diskleri** dikey penceresinde tıklatın **+ Ekle veri diski**.
5. Hello açılan hello yeni disk için seçin **boş oluşturma**.
6. Merhaba, **oluşturma yönetilen disk** dikey penceresinde hello disk için bir ad yazın ve Ayarla diğer ayarları gerektiği gibi hello. İşiniz bittiğinde tıklatın **oluşturma**.
7. Merhaba, **diskleri** dikey penceresinde, toosave hello hello VM için yeni disk yapılandırması Kaydet.
6. Azure hello disk oluşturur ve toohello sanal makineye iliştirir sonra hello yeni disk hello sanal makinenin disk ayarları altında listelenen **veri diskleri**.


## <a name="initialize-a-new-data-disk"></a>Yeni bir veri diski başlatın

1. Toohello VM bağlayın.
1. Merhaba VM içinde Hello Başlat menüsünde ve türünü tıklatın **diskmgmt.msc** ve isabet **Enter**. Bu, hello Disk Yönetimi ek bileşenini başlatır.
2. Disk Yönetimi yeni ve başlatılmamış bir disk varsa ve hello diski başlatma penceresini kalkar algılar.
3. Merhaba yeni disk seçildiğinden emin olun ve tıklayın **Tamam** tooinitialize onu.
4. Merhaba yeni bir disk olarak artık görünür **ayrılmamış**. Merhaba disk üzerinde herhangi bir yere sağ tıklatıp **yeni basit birim**. Merhaba **Yeni Basit Birim Sihirbazı** başlar.
5. Seçim yapıldığında hello Varsayılanları tümünün tutma hello Sihirbazı aracılığıyla gidin **son**.
6. Disk Yönetimi'ni kapatın.
7. Açılır pencere, alırsınız, kullanmadan önce tooformat hello yeni bir disk gerekir. Tıklatın **biçimi disk**.
8. Merhaba, **biçimi yeni disk** iletişim, hello ayarlarını denetleyin ve ardından **Başlat**.
9. Merhaba diskleri biçimlendirme hello verilerin tümünü siler, bir uyarı alırsınız tıklatın **Tamam**.
10. Hello biçimi tamamlandığında tıklatın **Tamam**.

## <a name="use-trim-with-standard-storage"></a>Standart depolama ile kullanmak üzere KIRPMA

Standart depolama (HDD) kullanırsanız, KIRPMA etkinleştirmeniz gerekir. Yalnızca gerçekten kullandığınız depolama için faturalandırılır şekilde KIRPMA hello diskte kullanılmayan blokları atar. Büyük dosyaları oluşturmak ve bunları silerseniz bu maliyetleri kaydedebilirsiniz. 

Bu komut toocheck hello KIRPMA ayarı çalıştırabilirsiniz. Windows VM ve türü bir komut istemi açın:

```
fsutil behavior query DisableDeleteNotify
```

Merhaba komut 0 döndürürse, KIRPMA doğru şekilde etkinleştirilir. 1 değeri döndürülürse, komut tooenable KIRPMA aşağıdaki hello çalıştırın:
```
fsutil behavior set DisableDeleteNotify 0
```

Veri diskinizden sildikten sonra hello KIRPMA işlemleri düzgün çalıştırarak temizleme KIRPMA ile birleştirme sağlayabilirsiniz:

```
defrag.exe <volume:> -l
```

Ayrıca, birimin tamamını hello hello birim biçimlendirme kırpılır emin olabilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar
Uygulama, toouse hello D: sürücü toostore veri gerekiyorsa, yapabilecekleriniz [hello Windows geçici disk hello sürücü harfini değiştirin](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).
