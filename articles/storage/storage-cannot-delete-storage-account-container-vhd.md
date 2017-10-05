---
title: "Azure depolama hesapları, kapsayıcıları veya VHD'leri klasik bir dağıtımda silme sorunlarını giderme | Microsoft Docs"
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
ms.openlocfilehash: 9f3e824414ad6c1a0aba98a3d549ee63ddc7272f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-deleting-azure-storage-accounts-containers-or-vhds-in-a-classic-deployment"></a>Azure depolama hesapları, kapsayıcıları veya VHD'leri klasik bir dağıtımda silme sorunlarını giderme
[!INCLUDE [storage-selector-cannot-delete-storage-account-container-vhd](../../includes/storage-selector-cannot-delete-storage-account-container-vhd.md)]

Azure depolama hesabı, kapsayıcı ya da VHD silmeye çalıştığınızda hata alabilirsiniz [Azure portal](https://portal.azure.com/) veya [Klasik Azure portalı](https://manage.windowsazure.com/). Bu sorunlar aşağıdaki durumlarda oluşabilir:

* Bir VM’yi sildiğinizde disk ve VHD otomatik olarak silinmez. Depolama hesabını silmede başarısızlık bundan kaynaklanıyor olabilir. Başka bir VM bağlamak için disk kullanabilmeleri biz disk silmeyin.
* Disk veya diskle ilişkili blob üzerinde kiralama hala devam ediyor.
* Hala bir blob, kapsayıcısı veya depolama hesabı kullanarak bir VM görüntüsü yok.

Bu makalede Azure sorunu ele alınmamışsa Azure forumları ziyaret [MSDN ve yığın taşması](https://azure.microsoft.com/support/forums/). Bu forumları veya çok sorununuzu nakledebilirsiniz @AzureSupport Twitter'da. Ayrıca, size bir Azure destek isteği seçerek dosya **alma desteği** üzerinde [Azure Destek](https://azure.microsoft.com/support/options/) site.

## <a name="symptoms"></a>Belirtiler
Aşağıdaki bölümde Azure depolama hesapları, kapsayıcıları veya VHD'leri silmeye çalıştığınızda alabileceğiniz yaygın hataları listeler.

### <a name="scenario-1-unable-to-delete-a-storage-account"></a>Senaryo 1: Depolama hesabı silinemedi
Klasik depolama hesabına gidin zaman [Azure portal](https://portal.azure.com/) seçip **silmek**, depolama hesabı silinmesini engelliyor nesnelerin bir listesini sunulan:

  ![Hata görüntüsü zaman depolama hesabını silme](./media/storage-cannot-delete-storage-account-container-vhd/newerror.png)

Depolama hesabına gidin zaman [Klasik Azure portalı](https://manage.windowsazure.com/) seçip **silmek**, aşağıdaki hatalardan birini görebilirsiniz:

- *Depolama hesabı StorageAccountName VM görüntüleri içeriyor. Bu depolama hesabını silmeden önce bu VM görüntülerinin kaldırıldığından emin olun.*

- *Depolama hesabı < vm-storage-account-name > silinemedi. Depolama hesabı < vm-storage-account-name > silinemiyor: ' < vm-storage-account-name > depolama hesabı bazı etkin görüntülere ve/veya disklerin sahiptir. Bu görüntülerin ve/veya diskleri bu depolama hesabını silmeden önce kaldırıldığından emin olun.'.*

- *Depolama hesabı < vm-storage-account-name > bazı etkin görüntülere ve/veya disklerin, örneğin xxxxxxxxx-xxxxxxxxx-O-209490240936090599 sahiptir. Bu görüntülerin ve/veya diskleri bu depolama hesabını silmeden önce kaldırıldığından emin olun.*

- *Depolama hesabı < vm-storage-account-name > etkin bir görüntü ve/veya disk yapıları olan 1 kaldırıldığından sahiptir. Bu depolama hesabını silmeden önce bu yapıların görüntü deposundan kaldırıldığından emin olmak*.

- *Etkin bir görüntü ve/veya disk yapıları olan 1 kaldırıldığından başarısız depolama hesabının < vm-storage-account-name > sahip gönderin. Bu depolama hesabını silmeden önce bu yapıların görüntü deposundan kaldırıldığından emin olun. Bir depolama hesabı silme girişimi ve onunla ilişkili hala etkin disk olduğunda silinmesi gereken etkin disk söyleyen bir ileti görürsünüz*.

### <a name="scenario-2-unable-to-delete-a-container"></a>2. Senaryo: Bir kapsayıcı silinemedi
Depolama kapsayıcısı silmeye çalıştığınızda, aşağıdaki hatayı görebilirsiniz:

*Depolama kapsayıcısı silinemedi <container name>. Hata: ' kapsayıcısı üzerinde şu anda bir kira yoktur ve hiçbir kiralama kimliği istekte belirtilen*.

Veya

*Kapsayıcı silinemez aşağıdaki sanal makine disklerini BLOB'ları bu kapsayıcıda kullanın: VirtualMachineDiskName1, VirtualMachineDiskName2,...*

### <a name="scenario-3-unable-to-delete-a-vhd"></a>Senaryo 3: Bir VHD silinemiyor
Bir VM silin ve ardından BLOB'lar için ilişkili VHD'leri silmeyi deneyin sonra aşağıdaki iletiyi alabilirsiniz:

*BLOB silinemedi ' yolu/XXXXXX-XXXXXX-os-1447379084699.vhd'. Hata: ' blob üzerindeki şu anda bir kira yoktur ve istekte hiçbir kiralama kimliği belirtildi.*

Veya

*Blob silinemez blob 'BlobName.vhd' sanal makine diski 'VirtualMachineDiskName' olarak kullanılıyor.*

## <a name="solution"></a>Çözüm
En sık karşılaşılan sorunları gidermek için aşağıdaki yöntemi deneyin:

### <a name="step-1-delete-any-disks-that-are-preventing-deletion-of-the-storage-account-container-or-vhd"></a>1. adım: depolama hesabı, kapsayıcısı veya VHD silinmesini engelliyor diskler Sil
1. Geçiş [Klasik Azure portalı](https://manage.windowsazure.com/).
2. Seçin **sanal makine** > **DİSKLERİ**.

    ![Klasik Azure portalı sanal makinelerde disklerde görüntüsü.](./media/storage-cannot-delete-storage-account-container-vhd/VMUI.png)
3. Silmek istediğiniz depolama hesabı, kapsayıcı ya da VHD ile ilişkilendirilmiş diskleri bulun. Disklerin konumunu denetlediğinizde, ilişkili olduğu depolama hesabı, kapsayıcı veya VHD’yi bulacaksınız.

    ![Konum bilgileri diskler için Azure Klasik portalında gösteren resim](./media/storage-cannot-delete-storage-account-container-vhd/DiskLocation.png)
4. Aşağıdaki yöntemlerden birini kullanarak diskleri silin:

  - Hiçbir VM varsa listelenen **bağlı** alan diskin, disk doğrudan silebilirsiniz.

  - Disk bir veri diski ise, şu adımları izleyin:

    1. Diski bağlı VM adını kontrol edin.
    2. Git **sanal makineleri** > **örnekleri**ve ardından VM bulun.
    3. Hiçbir şey etkin olarak disk kullandığından emin olun.
    4. Seçin **diski Ayır** diski kullanımdan çıkarmak için portalın altındaki.
    5. Git **sanal makineleri** > **diskleri**ve bekleyin **bağlı** boş açmak için alan. Bu diski sanal makineden başarıyla ayrıldı olduğunu gösterir.
    6. Seçin **silmek** alt kısmındaki **sanal makineleri** > **diskleri** disk silmek için.

  - Disk bir işletim sistemi diski ise ( **içeren işletim sistemi** alanı, Windows gibi bir değer içeriyor) ve bir VM'ye bağlı, VM silmek için aşağıdaki adımları izleyin. İşletim sistemi diski ayrılamıyor, bu nedenle biz kira serbest bırakmak için VM silmeniz gerekir.

    1. Veri diski bağlı sanal makine adını denetleyin.  
    2. Git **sanal makineleri** > **örnekleri**ve ardından diski bağlı VM seçin.
    3. Hiçbir şey etkin olarak sanal makinenin kullandığından emin olun ve sanal makine artık gerekir.
    4. Disk VM eklendiği, ardından seçin **silmek** > **ekli disklerini silmeyi**.
    5. Git **sanal makineleri** > **diskleri**ve disk kayboluyor bekleyin.  Bunun gerçekleşmesi birkaç dakika sürebilir ve sayfayı yenilemeniz gerekebilir.
    6. Disk kayboluyor değil, bekleyin **bağlı** boş açmak için alan. Bu diski sanal makineden tam olarak ayrılmış gösterir.  Sonra disk seçin ve Seç **silmek** disk silmek için sayfanın altındaki.


   > [!NOTE]
   > Bir VM'ye bir disk bağlıysa silmek mümkün olmaz. Diskleri silinmiş bir VM'den zaman uyumsuz olarak ayrılır. VM temizlemek Bu alan için silindikten sonra birkaç dakika sürebilir.
   >
   >


### <a name="step-2-delete-any-vm-images-that-are-preventing-deletion-of-the-storage-account-or-container"></a>2. adım: depolama hesabı veya kapsayıcı silinmesine engelleyen tüm VM görüntüleri silin
1. Geçiş [Klasik Azure portalı](https://manage.windowsazure.com/).
2. Seçin **sanal makine** > **GÖRÜNTÜLERİ**ve ardından depolama hesabı, kapsayıcısı veya VHD ile ilişkilendirilmiş görüntüleri silin.

    Bundan sonra depolama hesabı, kapsayıcısı veya VHD silmeyi tekrar deneyin.

> [!WARNING]
> Hesabı silmeden önce kaydetmek istediğiniz şeyleri yedeklediğinizden emin olun. VHD, blob, tablo, kuyruk veya dosya sildiğinizde, kalıcı olarak silinir. Kaynak kullanımda olmadığından emin olun.
>
>

## <a name="about-the-stopped-deallocated-status"></a>Durduruldu (serbest bırakıldı) durumu hakkında
Klasik dağıtım modelinde oluşturulmuş ve, korundu VM'ler olacaktır **durduruldu (serbest bırakıldı)** ya da durum [Azure portal](https://portal.azure.com/) veya [Klasik Azure portalı](https://manage.windowsazure.com/).

**Klasik Azure portalı**:

![(Deallocated) durum VM'ler için Azure Portal'da durduruldu.](./media/storage-cannot-delete-storage-account-container-vhd/moreinfo2.png)

**Azure portal**:

![Durduruldu (serbest bırakıldığında) durum VM'ler için Klasik Azure portalı.](./media/storage-cannot-delete-storage-account-container-vhd/moreinfo1.png)

"Durduruldu (serbest bırakıldı)" durumu CPU, bellek ve ağ gibi bilgisayar kaynaklarını serbest bırakır. Böylece, hızlı bir şekilde VM gerekirse yeniden oluşturabilirsiniz diskleri ancak hala korunur. Bu diskleri Azure Depolama tarafından yedeklenen VHD'ler üzerinde oluşturulur. Depolama hesabı bu VHD ve diskleri kiraları bu VHD'lerde sahip.

## <a name="next-steps"></a>Sonraki adımlar
* [Bir depolama hesabını silme](storage-create-storage-account.md#delete-a-storage-account)
