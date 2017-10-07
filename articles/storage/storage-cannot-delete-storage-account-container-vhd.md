---
title: "Azure depolama hesapları, kapsayıcıları veya VHD'leri klasik bir dağıtımda silme aaaTroubleshoot | Microsoft Docs"
description: "Azure depolama hesapları, kapsayıcıları veya VHD'leri klasik bir dağıtımda silme sorunlarını giderme"
services: storage
documentationcenter: 
author: genlin
manager: felixwu
editor: tysonn
tags: storage
ms.assetid: 0f7a8243-d8dc-432a-9d37-1272a0cb3a5c
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: genli
ms.openlocfilehash: 6bbfa032e1968718c623227bb426d553e2951075
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deleting-azure-storage-accounts-containers-or-vhds-in-a-classic-deployment"></a>Azure depolama hesapları, kapsayıcıları veya VHD'leri klasik bir dağıtımda silme sorunlarını giderme
[!INCLUDE [storage-selector-cannot-delete-storage-account-container-vhd](../../includes/storage-selector-cannot-delete-storage-account-container-vhd.md)]

Hello toodelete hello Azure depolama hesabı, kapsayıcısı veya VHD çalıştığınızda hata alabilirsiniz [Azure portal](https://portal.azure.com/) veya hello [Klasik Azure portalı](https://manage.windowsazure.com/). Merhaba sorunları koşullar aşağıdaki hello tarafından kaynaklanabilir:

* Bir VM sildiğinizde, hello disk ve VHD otomatik olarak silinmez. Bu depolama hesabı silme hatası hello neden olabilir. Başka bir VM hello disk toomount kullanabilmesi biz hello disk silmeyin.
* Olduğundan hala bir kira hello diskle ilişkili bir disk veya hello blob.
* Hala bir blob, kapsayıcısı veya depolama hesabı kullanarak bir VM görüntüsü yok.

Bu makalede Azure sorunu ele alınmamışsa ziyaret üzerinde Azure forumları hello [MSDN ve yığın taşması hello](https://azure.microsoft.com/support/forums/). Bu forumlar sorununuzu nakledebilirsiniz veya too@AzureSupport Twitter'da. Ayrıca, size bir Azure destek isteği seçerek dosya **alma desteği** hello üzerinde [Azure Destek](https://azure.microsoft.com/support/options/) site.

## <a name="symptoms"></a>Belirtiler
bölümden hello toodelete hello Azure depolama hesapları, kapsayıcıları veya VHD'leri çalıştığınızda alabileceğiniz yaygın hataları listeler.

### <a name="scenario-1-unable-toodelete-a-storage-account"></a>Senaryo 1: Oluşturulamıyor toodelete bir depolama hesabı
Merhaba toohello Klasik depolama hesabında gidin zaman [Azure portal](https://portal.azure.com/) seçip **silmek**, hello depolama hesabı silinmesini engelliyor nesnelerin bir listesini sunulan:

  ![Hata görüntüsü zaman hello depolama hesabını silme](./media/storage-cannot-delete-storage-account-container-vhd/newerror.png)

Merhaba toohello depolama hesabında gidin zaman [Klasik Azure portalı](https://manage.windowsazure.com/) seçip **silmek**, aşağıdaki hatalar hello birini görebilirsiniz:

- *Depolama hesabı StorageAccountName VM görüntüleri içeriyor. Bu depolama hesabını silmeden önce bu VM görüntülerinin kaldırıldığından emin olun.*

- *Toodelete depolama hesabı < vm-storage-account-name > başarısız oldu. %S toodelete depolama hesabı < vm-storage-hesap-adı >: ' < vm-storage-account-name > depolama hesabı bazı etkin görüntülere ve/veya disklerin sahiptir. Bu görüntülerin ve/veya diskleri bu depolama hesabını silmeden önce kaldırıldığından emin olun.'.*

- *Depolama hesabı < vm-storage-account-name > bazı etkin görüntülere ve/veya disklerin, örneğin xxxxxxxxx-xxxxxxxxx-O-209490240936090599 sahiptir. Bu görüntülerin ve/veya diskleri bu depolama hesabını silmeden önce kaldırıldığından emin olun.*

- *Depolama hesabı < vm-storage-account-name > etkin bir görüntü ve/veya disk yapıları olan 1 kaldırıldığından sahiptir. Bu depolama hesabını silmeden önce bu yapıların hello görüntü deposundan kaldırıldığından emin olmak*.

- *Etkin bir görüntü ve/veya disk yapıları olan 1 kaldırıldığından başarısız depolama hesabının < vm-storage-account-name > sahip gönderin. Bu depolama hesabını silmeden önce yapıların hello görüntü deposundan kaldırıldığından emin olun. Toodelete bir depolama hesabı dener ve onunla ilişkili hala etkin disk olduğunda silinmiş toobe gereken etkin disk söyleyen bir ileti görürsünüz*.

### <a name="scenario-2-unable-toodelete-a-container"></a>Senaryo 2: Oluşturulamıyor toodelete bir kapsayıcı
Toodelete hello depolama kapsayıcısı denediğinizde aşağıdaki hata hello görebilirsiniz:

*Başarısız toodelete depolama kapsayıcısı <container name>. Hata: ' hello kapsayıcısı üzerinde şu anda bir kira yoktur ve hiçbir kiralama kimliği hello istekte belirtilen*.

Veya

*sanal makine disklerini aşağıdaki hello hello kapsayıcı silinemez bu kapsayıcıdaki blobları kullanın: VirtualMachineDiskName1, VirtualMachineDiskName2,...*

### <a name="scenario-3-unable-toodelete-a-vhd"></a>Senaryo 3: Oluşturulamıyor toodelete VHD
Bir VM silin ve ardından VHD try toodelete hello BLOB'lar hello için ilişkilendirilmiş sonra iletiden hello alabilirsiniz:

*Başarısız toodelete blob ' yolu/XXXXXX-XXXXXX-os-1447379084699.vhd'. Hata: ' hello blob üzerinde şu anda bir kira yoktur ve hiçbir kiralama kimliği hello istekte belirtildi.*

Veya

*Merhaba blob silinemez blob 'BlobName.vhd' sanal makine diski 'VirtualMachineDiskName' olarak kullanılıyor.*

## <a name="solution"></a>Çözüm
tooresolve hello en sık karşılaşılan sorunları, yöntem aşağıdaki hello deneyin:

### <a name="step-1-delete-any-disks-that-are-preventing-deletion-of-hello-storage-account-container-or-vhd"></a>1. adım: hello depolama hesabı, kapsayıcısı veya VHD silinmesini engelliyor diskler Sil
1. Geçiş toohello [Klasik Azure portalı](https://manage.windowsazure.com/).
2. Seçin **sanal makine** > **DİSKLERİ**.

    ![Klasik Azure portalı sanal makinelerde disklerde görüntüsü.](./media/storage-cannot-delete-storage-account-container-vhd/VMUI.png)
3. Merhaba depolama hesabı, kapsayıcısı veya toodelete istediğiniz VHD ile ilişkilendirilmiş hello diskleri bulun. Merhaba disk hello konumunu işaretlediğinizde, depolama hesabı, kapsayıcısı veya VHD hello ilişkili bulacaksınız.

    ![Konum bilgileri diskler için Azure Klasik portalında gösteren resim](./media/storage-cannot-delete-storage-account-container-vhd/DiskLocation.png)
4. Merhaba diskleri yöntemler aşağıdaki hello birini kullanarak silin:

  - Varsa hiçbir VM üzerinde hello listelenen **bağlı** alan hello disk, hello disk doğrudan silebilirsiniz.

  - Başlangıç diski bir veri diski ise, şu adımları izleyin:

    1. Disk hello VM iliştirildiği hello Hello adını kontrol edin.
    2. Çok Git**sanal makineleri** > **örnekleri**ve hello VM bulun.
    3. Hiçbir şey etkin şekilde hello disk kullandığından emin olun.
    4. Seçin **diski Ayır** hello portal toodetach hello disk hello sonundaki.
    5. Çok Git**sanal makineleri** > **diskleri**ve Merhaba bekleyin **bağlı** alan tooturn boş. Bu hello disk hello VM ' başarıyla ayrıldı olduğunu gösterir.
    6. Seçin **silmek** hello altındaki **sanal makineleri** > **diskleri** toodelete hello disk.

  - Merhaba disk işletim sistemi diski ise (Merhaba **içeren işletim sistemi** alanı, Windows gibi bir değer içeriyor) ve ekli tooa VM, şu adımları izleyin toodelete hello VM. toodelete hello VM toorelease hello kira sahibiz şekilde hello işletim sistemi diski ayrılamıyor.

    1. Veri diski bağlı hello sanal makine hello Hello adını kontrol edin.  
    2. Çok Git**sanal makineleri** > **örnekleri**, ve ardından select hello disk hello VM bağlı.
    3. Hiçbir şey etkin şekilde hello sanal makine ve sanal makine artık hello kullandığından emin olun.
    4. Select hello VM hello disk eklendiği, ardından **silmek** > **Delete hello bağlı diskler**.
    5. Çok Git**sanal makineleri** > **diskleri**ve hello disk toodisappear için bekleyin.  Bu toooccur birkaç dakika sürebilir ve toorefresh hello sayfa gerekebilir.
    6. Merhaba disk kayboluyor değil, hello için bekleyin. **bağlı** alan tooturn boş. Bu hello disk tam olarak VM hello ayrıldı olduğunu gösterir.  Sonra hello disk seçin ve Seç **silmek** hello sayfa toodelete hello disk hello sonundaki.


   > [!NOTE]
   > Bir disk ekli tooa VM ise mümkün toodelete olmaz. Diskleri silinmiş bir VM'den zaman uyumsuz olarak ayrılır. Bu alan tooclear için hello VM silindikten sonra birkaç dakika sürebilir.
   >
   >


### <a name="step-2-delete-any-vm-images-that-are-preventing-deletion-of-hello-storage-account-or-container"></a>2. adım: hello depolama hesabı veya kapsayıcı silinmesine engelleyen tüm VM görüntüleri silin
1. Geçiş toohello [Klasik Azure portalı](https://manage.windowsazure.com/).
2. Seçin **sanal makine** > **GÖRÜNTÜLERİ**ve ardından hello depolama hesabı, kapsayıcısı veya VHD ile ilişkilendirilmiş hello görüntüleri silin.

    Bundan sonra toodelete hello depolama hesabı, kapsayıcısı veya VHD yeniden deneyin.

> [!WARNING]
> Merhaba hesabı silmeden önce emin tooback herhangi bir şey olması toosave istiyor. VHD, blob, tablo, kuyruk veya dosya sildiğinizde, kalıcı olarak silinir. Merhaba kaynak kullanımda olmadığından emin olun.
>
>

## <a name="about-hello-stopped-deallocated-status"></a>Merhaba durduruldu (serbest bırakıldı) durumu hakkında
Merhaba Klasik dağıtım modelinde oluşturulmuş ve, korundu VM'ler hello olacaktır **durduruldu (serbest bırakıldı)** ya da hello durumuna [Azure portal](https://portal.azure.com/) veya [Klasik Azure portalı ](https://manage.windowsazure.com/).

**Klasik Azure portalı**:

![(Deallocated) durum VM'ler için Azure Portal'da durduruldu.](./media/storage-cannot-delete-storage-account-container-vhd/moreinfo2.png)

**Azure portal**:

![Durduruldu (serbest bırakıldığında) durum VM'ler için Klasik Azure portalı.](./media/storage-cannot-delete-storage-account-container-vhd/moreinfo1.png)

"Durduruldu (serbest bırakıldı)" durumu hello CPU, bellek ve ağ gibi hello bilgisayar kaynakları serbest bırakır. Böylece, hızlı bir şekilde hello VM gerekirse yeniden oluşturabilirsiniz hello diskler, ancak hala korunur. Bu diskleri Azure Depolama tarafından yedeklenen VHD'ler üzerinde oluşturulur. Merhaba depolama hesabı bu VHD ve hello diskleri kiraları bu VHD'lerde sahip.

## <a name="next-steps"></a>Sonraki adımlar
* [Bir depolama hesabını silme](storage-create-storage-account.md#delete-a-storage-account)
