---
title: "bir yönetilmeyen veri diski tooa Windows VM - Azure aaaAttach | Microsoft Docs"
description: "Nasıl tooattach yeni veya var olan yönetilmeyen veri diski tooa Windows VM Azure portal kullanarak hello Resource Manager dağıtım modeli hello."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3790fc59-7264-41df-b7a3-8d1226799885
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/09/2017
ms.author: cynthn
ms.openlocfilehash: 923a6663974143bf359970f9b0eb0d36cabcba9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooattach-an-unmanaged-data-disk-tooa-windows-vm-in-hello-azure-portal"></a>Nasıl tooattach yönetilmeyen bir veri diski hello Azure portal'ın Windows VM tooa

Bu makale size gösterir nasıl tooattach hem yeni hem de mevcut yönetilmeyen hello Azure portal aracılığıyla tooWindows sanal makineler diskler. Ayrıca [PowerShell kullanarak bir veri diskini](./attach-disk-ps.md). Bunu önce bu ipuçlarını gözden geçirin:

* Merhaba boyutunu hello sanal makine, iliştirebilirsiniz kaç tane veri diskleri denetler. Ayrıntılar için bkz [sanal makineler için Boyutlar](sizes.md).
* Premium depolama toouse, DS serisi veya GS serisi bir sanal makine gerekir. Bu sanal makinelerle Premium ve standart depolama hesapları arasından diskleri kullanabilirsiniz. Premium depolama belirli bölgelerde kullanılabilir. Ayrıntılar için bkz [Premium Storage: Azure sanal makine iş yükleri için yüksek performanslı depolama](../../storage/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Yeni bir disk için toocreate gerekmez, ilk bunu eklediğinizde Azure bunu oluşturduğundan.


Ayrıca [Powershell kullanarak bir veri diskini](attach-disk-ps.md).


## <a name="find-hello-virtual-machine"></a>Merhaba sanal makine bulunamadı
1. İçinde toohello oturum [Azure portal](https://portal.azure.com/).
2. Merhaba soldaki Hello menüde tıklatın **sanal makineleri**.
3. Merhaba sanal makine hello listeden seçin.
4. Merhaba sanal makineleri dikey penceresinde tıklayın **diskleri**.
   
Ya da eklemek için aşağıdaki yönergeleri tarafından devam bir [yeni disk](#option-1-attach-a-new-disk) veya bir [mevcut disk](#option-2-attach-an-existing-disk).

## <a name="option-1-attach-and-initialize-a-new-disk"></a>Seçenek 1: Eklemek ve yeni bir disk başlatma
1. Merhaba üzerinde **diskleri** dikey penceresinde tıklatın **+ Ekle veri diski**.
2. Merhaba, **Attach yönetilen disk** dikey penceresinde hello disk için bir ad yazın **adı** ve ardından **yeni (boş disk)** içinde **kaynak türünü**.
3. Altında **depolama kapsayıcısı**, hello tıklatın **Gözat** düğmesine tıklayın ve toohello depolama hesabı ve burada depolanan hello yeni VHD toobe ister ve ardından kapsayıcı Gözat **seçin**. 
  
   ![Disk ayarlarını gözden geçirin](./media/attach-disk-portal/attach-empty-unmanaged.png)
   
3. Merhaba veri diski hello ayarları ile işiniz bittiğinde tıklatın **Tamam**.
4. Merhaba edilene **diskleri** dikey penceresinde tıklatın **kaydetmek** tooadd hello disk toohello VM yapılandırması.


### <a name="initialize-a-new-data-disk"></a>Yeni bir veri diski başlatın

1. Toohello sanal makineye bağlanın. Yönergeler için bkz: [nasıl Windows çalıştıran tooconnect ve oturum açma tooan Azure sanal makine](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
1. Merhaba tıklatın **Başlat** menüsünün hello VM ve türü içinde **diskmgmt.msc** ve isabet **Enter**. Bu, hello Disk Yönetimi ek bileşenini başlatır.
2. Disk Yönetimi yeni ve başlatılmamış bir disk varsa ve hello diski başlatma penceresini kalkar tanır.
3. Merhaba yeni disk seçildiğinden emin olun ve tıklayın **Tamam** tooinitialize onu.
4. Merhaba yeni disk şimdi olarak görünür **ayrılmamış**. Merhaba disk üzerinde herhangi bir yere sağ tıklatıp **yeni basit birim**. Merhaba **Yeni Basit Birim Sihirbazı** başlatır.
5. Seçim yapıldığında hello Varsayılanları tümünün tutma hello Sihirbazı aracılığıyla gidin **son**.
6. Disk Yönetimi'ni kapatın.
7. Açılır pencere alma kullanabilmeniz için önce tooformat hello yeni bir disk gerekir. Tıklatın **biçimi disk**.
8. Merhaba, **biçimi yeni disk** iletişim, hello ayarlarını denetleyin ve ardından **Başlat**.
9. Merhaba diskleri biçimlendirme hello verilerin tümünü siler, bir uyarı almak, tıklatın **Tamam**.
10. Hello biçimi tamamlandığında tıklatın **Tamam**.


## <a name="option-2-attach-an-existing-disk"></a>Seçenek 2: var olan bir diski kullanıma açın
1. Merhaba üzerinde **diskleri** dikey penceresinde tıklatın **+ Ekle veri diski**.
2. Merhaba üzerinde **Attach yönetilmeyen disk** dikey penceresinde, **kaynak türünü** seçin **varolan blob**.

    ![Disk ayarlarını gözden geçirin](./media/attach-disk-portal/attach-existing-unmanaged.png)

    3. Tıklatın **Gözat** toonavigate toohello depolama hesabı ve kapsayıcı hello varolan bir VHD'yi bulunduğu. Tıklayın ve VHD hello ve ardından **seçin**.
4. Tıklatın **Tamam** hello içinde **Attach yönetilmeyen disk** dikey.
5. Merhaba, **diskleri** dikey penceresinde tıklatın **kaydetmek** hello VM için tooadd hello disk toohello yapılandırması.
   


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

