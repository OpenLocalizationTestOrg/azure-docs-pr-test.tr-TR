---
title: aaaAttach disk tooa Klasik Azure VM | Microsoft Docs
description: "Bir veri diski tooa Windows hello Klasik dağıtım modeliyle oluşturulan sanal makinenin ekleyin ve onu başlatın."
services: virtual-machines-windows, storage
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: be4e3e74-05bc-4527-969f-84f10a1d66a7
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/21/2017
ms.author: cynthn
ms.openlocfilehash: bfe1b0fa066277d28d3862a18da4b1023cb4452d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="attach-a-data-disk-tooa-windows-virtual-machine-created-with-hello-classic-deployment-model"></a>Bir veri diski tooa Windows hello Klasik dağıtım modeliyle oluşturulan sanal makinenin ekleme
<!--
Refernce article:
    If you want toouse hello new portal, see [How tooattach a data disk tooa Windows VM in hello Azure portal](../../virtual-machines-windows-attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
-->

Bu makalede tooattach yeni ve mevcut diskleri hello Klasik dağıtım modeli tooa Windows hello kullanarak sanal makine ile Azure portalına nasıl oluşturulacağını gösterir.

Ayrıca [hello Azure portal'ın bir veri diski tooa Linux VM ekleme](../../linux/attach-disk-portal.md).

Bir disk eklemeden önce bu ipuçlarını gözden geçirin:

* Merhaba boyutunu hello sanal makine, iliştirebilirsiniz kaç tane veri diskleri denetler. Ayrıntılar için bkz [sanal makineler için Boyutlar](../../virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

* Premium depolama toouse, DS serisi veya GS serisi bir sanal makine gerekir. Bu sanal makinelerle Premium ve standart depolama hesapları arasından diskleri kullanabilirsiniz. Premium depolama belirli bölgelerde kullanılabilir. Ayrıntılar için bkz [Premium Storage: Azure sanal makine iş yükleri için yüksek performanslı depolama](../../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

* Yeni bir disk için toocreate gerekmez, ilk bunu eklediğinizde Azure bunu oluşturduğundan.

Ayrıca [Powershell kullanarak bir veri diskini](../../virtual-machines-windows-attach-disk-ps.md).

> [!IMPORTANT]
> Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md).

## <a name="find-hello-virtual-machine"></a>Merhaba sanal makine bulunamadı
1. İçinde toohello oturum [Azure portal](https://portal.azure.com/).
2. Sanal makineden hello Panoda listelenen hello Kaynak Seç hello.
3. Merhaba sol bölmede altında **ayarları**, tıklatın **diskleri**.

    ![Disk Ayarları'nı açın](./media/attach-disk/virtualmachinedisks.png)

Ya da eklemek için aşağıdaki yönergeleri tarafından devam bir [yeni disk](#option-1-attach-a-new-disk) veya bir [mevcut disk](#option-2-attach-an-existing-disk).

## <a name="option-1-attach-and-initialize-a-new-disk"></a>Seçenek 1: Eklemek ve yeni bir disk başlatma

1. Merhaba üzerinde **diskleri** dikey penceresinde tıklatın **Attach yeni**.
2. Merhaba varsayılan ayarları gözden geçirin, gerektiği gibi güncelleştirin ve ardından **Tamam**.

   ![Disk ayarlarını gözden geçirin](./media/attach-disk/attach-new.png)

3. Azure hello disk oluşturur ve toohello sanal makineye iliştirir sonra hello yeni disk hello sanal makinenin disk ayarları altında listelenen **veri diskleri**.

### <a name="initialize-a-new-data-disk"></a>Yeni bir veri diski başlatın

1. Toohello sanal makineye bağlanın. Yönergeler için bkz: [nasıl Windows çalıştıran tooconnect ve oturum açma tooan Azure sanal makine](../../virtual-machines-windows-connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
2. Toohello sanal makinede oturum sonra açmak **Sunucu Yöneticisi'ni**. Merhaba sol bölmesinde seçin **dosya ve depolama hizmetleri**.

    ![Sunucu Yöneticisi'ni açma](../media/attach-disk-portal/fileandstorageservices.png)

3. Seçin **diskleri**.
4. Merhaba **diskleri** bölümü hello diskleri listeler. Genellikle, bir sanal makine disk 0, 1 disk ve disk 2 ' var. Disk 0 hello işletim sistemi diski, disk 1 hello geçici diski olduğundan ve disk 2 hello veri diski yeni toohello sanal makineye bağlı. Merhaba veri diski listeleri hello bölümü olarak **bilinmeyen**.

 Başlangıç diski sağ tıklatın ve seçin **başlatma**.

5. Merhaba disk başlatıldığında tüm veriler silinecek bildirim. Tıklatın **Evet** tooacknowledge hello uyarı ve başlatma hello disk. Tamamlandıktan sonra hello bölüm olarak listelenmez. **GPT**. Başlangıç diski yeniden sağ tıklatın ve seçin **yeni birim**.

6. Merhaba varsayılan değerleri kullanarak hello Sihirbazı tamamlayın. Merhaba Sihirbazı tamamlandığında, hello **birimleri** bölümü hello yeni birim listeler. Merhaba disk artık çevrimiçi olduğunu ve hazır toostore verilerdir.

    ![Birimi başarıyla başlatıldı](./media/attach-disk/newdiskafterinitialization.png)

## <a name="option-2-attach-an-existing-disk"></a>Seçenek 2: var olan bir diski kullanıma açın
1. Merhaba üzerinde **diskleri** dikey penceresinde tıklatın **Attach varolan**.
2. Altında **varolan bir diski İlişti**, tıklatın **konumu**.

   ![Varolan bir diski kullanıma açın](./media/attach-disk/attachexistingdisksettings.png)
3. Altında **depolama hesapları**, hello hesabınızı ve hello .vhd dosyası tutan kapsayıcı.

   ![VHD konumunu bulma](./media/attach-disk/existdiskstorageaccountandcontainer.png)

4. Merhaba .vhd dosyasını seçin.
5. Altında **varolan bir diski İlişti**, seçtiğiniz hello dosya altında listelenen **VHD dosyasını**. **Tamam** düğmesine tıklayın.
6. Disk toohello sanal makine Azure ekler hello sonra hello sanal makinenin disk ayarları altında listelenen **veri diskleri**.

## <a name="use-trim-with-standard-storage"></a>Standart depolama ile kullanmak üzere KIRPMA

Standart depolama (HDD) kullanırsanız, KIRPMA etkinleştirmeniz gerekir. Yalnızca gerçekten kullandığınız depolama için faturalandırılır şekilde KIRPMA hello diskte kullanılmayan blokları atar. KIRPMA kullanarak büyük dosyaların silinmesi neden kullanılmayan blokları dahil, maliyetleri kaydedebilirsiniz.

Bu komut toocheck hello KIRPMA ayarı çalıştırabilirsiniz. Windows VM ve türü bir komut istemi açın:

```
fsutil behavior query DisableDeleteNotify
```

Merhaba komut 0 döndürürse, KIRPMA doğru şekilde etkinleştirilir. 1 değeri döndürülürse, komut tooenable KIRPMA aşağıdaki hello çalıştırın:
```
fsutil behavior set DisableDeleteNotify 0
```

## <a name="next-steps"></a>Sonraki adımlar
Uygulamanızı toouse hello D: sürücü toostore veri gerekiyorsa, yapabilecekleriniz [hello Windows geçici disk hello sürücü harfini değiştirin](../../virtual-machines-windows-change-drive-letter.md).

## <a name="additional-resources"></a>Ek kaynaklar
[Diskleri ve sanal makineler için VHD'ler hakkında](../../virtual-machines-linux-about-disks-vhds.md)
