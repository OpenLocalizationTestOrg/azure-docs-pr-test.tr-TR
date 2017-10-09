---
title: aaaManage StorSimple birimlerinizi | Microsoft Docs
description: "Nasıl tooadd, değiştirme, izlemek ve StorSimple birimleri silin ve nasıl açıklanmaktadır tootake gerekirse çevrimdışı."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: ccabd859-590c-4568-a81d-6ff38f125be3
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/11/2016
ms.author: v-sharos
ms.openlocfilehash: 8dc646261ee2ad8f2b80291518716f4de55b63f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-volumes"></a>Merhaba StorSimple Yöneticisi hizmeti toomanage birimleri kullanın
[!INCLUDE [storsimple-version-selector-manage-volumes](../../includes/storsimple-version-selector-manage-volumes.md)]

## <a name="overview"></a>Genel Bakış
Bu öğretici nasıl toouse StorSimple Yöneticisi hizmet toocreate hello ve birimler hello StorSimple cihazı ve StorSimple sanal cihazı yönetmek açıklanmaktadır.

Merhaba StorSimple Yöneticisi hizmeti hello StorSimple çözümünüzün bir tek web arabiriminden yönetmenizi sağlayan Klasik Azure portalında bir uzantısıdır. Toplama toomanaging birimlerinde hello StorSimple Yöneticisi hizmet toocreate kullanın ve StorSimple hizmetleri yönetmek, görüntülemek ve cihazları yönetmek, uyarıları görüntülemek ve görüntüleyebilir ve yedekleme ilkeleri ve hello yedekleme kataloğu yönetin.

> [!NOTE]
> Azure StorSimple yalnızca ölçülü kaynak kullanan birimler oluşturabilir. Tamamen sağlanan veya kısmen sağlanan oluşturulamıyor bir Azure StorSimple sistemi birimlerde.
> 
> Ölçülü kaynak sağlama kullanılabilir depolama alanı tooexceed fiziksel kaynaklar görünür bir sanallaştırma teknolojisidir. Yeterli depolama alanı önceden ayırma yerine Azure StorSimple tam olarak yeterli alanı toomeet geçerli gereksinimleri ince sağlama tooallocate kullanır. Azure StorSimple artırmak veya Bulut depolama toomeet değişen taleplerini azaltmak için bu yaklaşım bulut depolama esnek yapısını hello kolaylaştırır.
> 
> 

## <a name="hello-volumes-page"></a>Merhaba birimler sayfası
Merhaba **birimleri** sayfası hello Microsoft Azure StorSimple cihazı, başlatıcıları (Sunucuları) için sağlanan toomanage hello depolama birimleri sağlar. StorSimple Cihazınızda birimleri hello listesini gösterir.

 ![Birimler sayfası](./media/storsimple-manage-volumes/HCS_VolumesPage.png)

Bir birim öznitelikleri bir dizi oluşur:

* **Ad** – benzersiz olmalı ve hello birim tanımlamanıza yardımcı olan açıklayıcı bir ad. Bu ad Ayrıca belirli bir birimde filtre raporları izlemede kullanılır.
* **Durum** – çevrimiçi veya çevrimdışı olabilir. Bir birim varsa çevrimdışı olursa, erişim toouse hello birim izin görünür tooinitiators (sunucu) değil.
* **Kapasite** – ne kadar büyük hello birim belirtir, hello Başlatıcı (sunucu) tarafından algılanan aynıdır. Kapasite hello toplam hello Başlatıcı (sunucu) tarafından depolanan veri miktarını belirtir. Birimlerin ölçülü kaynak ve veri yinelenenleri kaldırılmış. Bu, Cihazınızı fiziksel depolama kapasitesi dahili olarak veya tooconfigured birim kapasitesi göre hello bulut üzerinde önceden ayırmanız değil anlamına gelir. Merhaba birim kapasitesi ayrılmış ve isteğe bağlı olarak tüketilen.
* **Tür** – hello birim türü katmanlı veya arşivleme olabilir (bir alt türü katmanlı)
* **Erişim** – erişim toothis birim izin hello başlatıcıları (Sunucuları) belirtir. Merhaba birimle ilişkilendirilen erişim denetimi kaydı (ACR) bir üyesi olmayan başlatıcıları hello birim görmezsiniz.
* **İzleme** – olsun veya olmasın bir birim izlenmekte belirtir. Bir birim izleme oluşturulduğunda varsayılan olarak etkin olacaktır. Olacaktır, ancak izleme, bir birim kopya için devre dışı. bir birim için izleme tooenable bir birim İzleyicisi'nde hello yönergeleri izleyin.

bir birimle ilişkilendirilen hello en yaygın görevleri şunlardır:

* Birim Ekle
* Bir birim değiştirme
* Bir birim Sil
* Bir birim çevrimdışı duruma getirin
* Bir birimi izleyin

## <a name="add-a-volume"></a>Birim Ekle
[Bir birim oluşturduğunuzda](storsimple-deployment-walkthrough-u1.md#step-6-create-a-volume) StorSimple çözümünüzün dağıtımı sırasında. Bir birim ekleme benzer bir yordamdır.

### <a name="tooadd-a-volume"></a>tooadd bir birim
1. Merhaba üzerinde **aygıtları** sayfasında, hello cihaz seçin, çift tıklayın ve hello ardından **birim kapsayıcıları** sekmesi.
2. Birim kapsayıcısı seçin ve hello karşılık gelen satır tooaccess hello birimler hello kapsayıcı ile ilişkili hello oku tıklatın.
3. Tıklatın **Ekle** hello sayfanın hello sonundaki. Merhaba Birim Ekleme sihirbazının başlatır.
   
     ![Birim temel ayarları Ekleme Sihirbazı](./media/storsimple-manage-volumes/AddVolume1.png)
4. Hello ekleme Birim Sihirbazı altında **temel ayarları**, aşağıdaki hello:
   
   1. Biriminize bir **Ad** verin.
   2. Merhaba belirtin **sağlanan kapasite** biriminiz GB veya TB cinsinden. Merhaba kapasitesi, fiziksel aygıt için 1 GB ile 64 TB arasında olmalıdır. StorSimple sanal cihaz üzerindeki bir birimi için sağlanan hello maksimum kapasite 30 TB'tır.
   3. Select hello **kullanım türü** biriminiz için. Kullanıyorsanız hello hello seçerek arşiv verileri için katmanlı birim **bu birimi daha az sıklıkta erişilen arşiv verileri için kullanın** onay kutusunu değişiklikleri hello yinelenenleri kaldırma öbek boyutunu biriminiz too512 KB. Bu seçeneği belirlemezseniz hello ilgili katmanlı birim 64 KB öbek boyutu kullanır. Daha büyük bir yinelenenleri kaldırma öbek boyutu hello aygıt tooexpedite hello büyük arşiv verilerinin toohello bulut aktarımını sağlar. (Katmanlı birimleri eski birincil birimler adı veriliyordu.)
   4. Merhaba ok simgesine tıklayın ![ok simgesi](./media/storsimple-manage-volumes/HCS_ArrowIcon.png)toogo toohello **ek ayarlar** sayfası.
      
        ![Birim Sihirbazı ek ayarları ekleme](./media/storsimple-manage-volumes/AddVolume2.png)
5. Altında **ek ayarlar**, yeni bir erişim denetimi kaydı (ACR) ekleyin:
   
   1. Erişim denetimi kaydı (ACR) hello aşağı açılan listeden seçin. Alternatif olarak, yeni ACR ekleyebilirsiniz. ACRs belirlemek hangi ana bilgisayarların birimlerinizi tarafından eşleşen hello erişebilirsiniz IQN hello kaydında listelenen ile ana bilgisayar.
   2. Merhaba seçerek varsayılan yedeği etkinleştirmenizi öneririz **bu birim için varsayılan yedeklemeyi etkinleştir** onay kutusu.
   3. Merhaba onay simgesine tıklayın ![Onay simgesi](./media/storsimple-manage-volumes/HCS_CheckIcon.png) Merhaba toocreate hello birimle ayarları belirtildi.

Yeni birim hazır toouse sunulmuştur.

## <a name="modify-a-volume"></a>Bir birim değiştirme
Bir birim veya hello birime erişmek konakları hello değişiklik tooexpand gerektiğinde değiştirin.

> [!IMPORTANT]
> * Merhaba birim boyutu hello aygıtta değiştirirseniz, hello birim boyutu hello yanı sıra konak üzerinde değiştirilmiş toobe gerekir.
> * Burada açıklanan hello konak tarafı Windows Server 2012 (2012R2) adımlardır. Yordamlar Linux veya diğer ana bilgisayar işletim sistemleri için farklı olacaktır. Hello birim başka bir işletim sistemi çalıştıran bir konağa değiştirirken tooyour ana bilgisayar işletim sistemi yönergelerine bakın.
> 
> 

### <a name="toomodify-a-volume"></a>toomodify bir birim
1. Merhaba üzerinde **aygıtları** sayfasında, hello cihaz seçin, çift tıklayın ve hello ardından **birim kapsayıcısı** sekmesi. Bu sayfa tablo biçiminde hello aygıtla ilişkili tüm hello birim kapsayıcıları listeler.
2. Birim kapsayıcısı seçin ve toodisplay hello hello kapsayıcıdaki tüm hello birimlerin listesini tıklatın.
3. Merhaba üzerinde **birimleri** sayfasında, bir birim seçin ve tıklayın **Değiştir**.
4. Hello değiştirme Birim Sihirbazı'nı altında **temel ayarları**, yapabileceğiniz hello aşağıdaki:
   
   * Merhaba Düzenle **adı** ve **türü** hello seçerek toomodify katmanlı birim tooan arşivleme birim isterseniz **bu birimi daha az sıklıkta erişilen arşiv verileri için kullanın** onay kutusu toochange hello yinelenenleri kaldırma öbek boyutunu biriminiz too512 KB.
   * Merhaba artırmak **sağlanan kapasite**. Merhaba **sağlanan kapasite** yalnızca artırılabilir. Oluşturulduktan sonra bir birim küçültülemez.
     
     > [!NOTE]
     > Tooa birim atandıktan sonra hello birim kapsayıcısı değiştiremezsiniz.
     > 
     > 
5. Altında **ek ayarlar**, yapabileceğiniz hello aşağıdaki:
   
   * Merhaba birim çevrimdışı koşuluyla hello ACRs değiştirin. Merhaba birim çevrimiçi ise tootake gerekir, çevrimdışı ilk. Toohello adımlarda başvuran [bir birim çevrimdışına](#take-a-volume-offline) önceki toomodifying hello ACR.
   * Merhaba birim çevrimdışı olduğunda ACRs hello listesini değiştirin.
     
     > [!NOTE]
     > Merhaba değiştiremezsiniz **bu birim için varsayılan yedeklemeyi etkinleştir** hello biriminin seçeneği.
     > 
     > 
6. Merhaba onay simgesine tıklayarak yaptığınız değişiklikleri kaydedin ![onay simgesi](./media/storsimple-manage-volumes/HCS_CheckIcon.png). Merhaba Klasik Azure portalı bir güncelleştirme birim iletisi görüntüler. Merhaba birimi başarıyla güncelleştirildiğinde bir başarı iletisi görüntüler.
7. Bir birim genişlettiğiniz Merhaba, Windows ana bilgisayarınızda aşağıdaki adımları izleyin:
   
   1. Çok Git**Bilgisayar Yönetimi** ->**Disk Yönetimi**.
   2. Sağ **Disk Yönetimi** seçip **diskleri**.
   3. Diskleri Hello listesinde, güncelleştirilmiş hello birim, sağ tıklatın ve ardından seçin **birimi Genişlet**. Merhaba birimi Genişlet Sihirbazı'nı başlatır. **İleri**’ye tıklayın.
   4. Merhaba varsayılan değerleri kabul ederek hello Sihirbazı tamamlayın. Merhaba Sihirbaz tamamlandıktan sonra hello birim artan hello boyutu göstermelidir.

![Video var](./media/storsimple-manage-volumes/Video_icon.png) **Video var**

toowatch gösteren bir video nasıl tooexpand bir birim tıklatın [burada](https://azure.microsoft.com/documentation/videos/expand-a-storsimple-volume/).

## <a name="take-a-volume-offline"></a>Bir birim çevrimdışı duruma getirin
Toomodify veya delete planlarken tootake çevrimdışı bir birim gerekebilir. Bir birim çevrimdışı olduğunda okuma-yazma erişimi için kullanılabilir değildir. Tootake hello birim çevrimdışı hello aygıt yanı sıra hello ana bilgisayar gerekir. Aşağıdaki adımları tootake çevrimdışı bir birim hello gerçekleştirin.

### <a name="tootake-a-volume-offline"></a>tootake çevrimdışı bir birim
1. Söz konusu Hello birim çevrimdışı duruma getirmeden önce kullanımda olmadığından emin olun.
2. Çevrimdışı Hello birim hello konakta ilk alın. Bu, olası tüm hello birimdeki veri bozulması riskini ortadan kaldırır. Belirli adımlar için işletim sistemi için toohello yönergeler bakın.
3. Hello ana bilgisayar çevrimdışıysa, hello birim çevrimdışı hello aygıtta hello aşağıdaki adımları gerçekleştirerek başlatıldıktan sonra:
   
   1. Merhaba üzerinde **aygıtları** sayfasında, hello cihaz seçin, çift tıklayın ve hello ardından **birim kapsayıcıları** sekmesini hello **birim kapsayıcıları** sekmesinde tüm tablo biçiminde listeler Merhaba aygıtla ilişkili hello birim kapsayıcıları.
   2. Birim kapsayıcısı seçin ve toodisplay hello hello kapsayıcıdaki tüm hello birimlerin listesini tıklatın.
   3. Bir birim seçin ve tıklatın **çevrimdışına**.
   4. Onayınız istendiğinde **Evet**’e tıklayın. Merhaba birim artık çevrimdışı olması gerekir.
      
      Bir birim çevrimdışı olduktan sonra hello **çevrimiçine** seçeneği kullanılabilir olur.

> [!NOTE]
> Merhaba **Çevrimdışına Al** komutu bir istek toohello aygıt tootake hello birim çevrimdışı gönderir. Konaklar hello birim kullanmaya devam ediyorsanız bu bozuk bağlantıları olur ancak hello birim çevrimdışı duruma getirmeden değil başarısız olur.
> 
> 

## <a name="delete-a-volume"></a>Bir birim Sil
> [!IMPORTANT]
> Yalnızca çevrimdışı ise, bir birim silebilirsiniz.
> 
> 

Aşağıdaki adımları toodelete bir birim hello tamamlayın.

### <a name="toodelete-a-volume"></a>toodelete bir birim
1. Merhaba üzerinde **aygıtları** sayfasında, hello cihaz seçin, çift tıklayın ve hello ardından **birim kapsayıcıları** sekmesi.
2. Merhaba birimin toodelete istediğiniz hello birim kapsayıcısı seçin. Merhaba birim kapsayıcı tooaccess hello tıklatın **birimleri** sayfası.
3. Bu kapsayıcı ile ilişkili tüm hello birimi tablo biçiminde görüntülenir. Merhaba durumunu denetlemek hello hacmi toodelete istiyor. Merhaba birim toodelete istediğiniz çevrimdışı durumda değilse, bunu çevrimdışı ilk, aşağıdaki hello adımlar [bir birim çevrimdışına](#take-a-volume-offline).
4. Merhaba birimi çevrim dışı sonra tıklayın **silmek** hello sayfanın hello sonundaki.
5. Onayınız istendiğinde **Evet**’e tıklayın. Merhaba birim artık silinecek ve hello **birimleri** sayfa güncelleştirilmiş hello hello kapsayıcıdaki birimlerin listesini gösterir.

## <a name="monitor-a-volume"></a>Bir birimi izleyin
Birim izleme, bir birim için toocollect g/Ç ile ilgili istatistikler sağlar. İzleme hello için varsayılan olarak etkindir, oluşturduğunuz ilk 32 birimler. Ek birimlerin izleme varsayılan olarak devre dışıdır. Kopyalanan birimlerin izleme varsayılan olarak devre dışıdır.

Aşağıdaki adımları tooenable hello gerçekleştirin veya bir birim için izlemeyi devre dışı bırakın.

### <a name="tooenable-or-disable-volume-monitoring"></a>tooenable veya birim izleme devre dışı
1. Merhaba üzerinde **aygıtları** sayfasında, hello cihaz seçin, çift tıklayın ve hello ardından **birim kapsayıcıları** sekmesi.
2. Hangi hello birimin bulunduğu hello birim kapsayıcısı seçin ve hello birim kapsayıcı tooaccess hello ardından **birimleri** sayfası.
3. Bu kapsayıcı ile ilişkili tüm hello birimi hello Tablo görünümünde listelenir. ' I tıklatın ve hello birim veya toplu kopyalama seçin.
4. Merhaba sayfasının Hello altında tıklatın **Değiştir**.
5. Merhaba birim Değiştirme Sihirbazı'nda altında **temel ayarları**seçin **etkinleştirmek** veya **devre dışı** hello gelen **izleme** aşağı açılan liste.
   
    ![Bir birim temel ayarlarını değiştirme](./media/storsimple-manage-volumes/HCS_MonitorVolumeM.png)

## <a name="next-steps"></a>Sonraki adımlar
* Nasıl çok öğrenin[bir StorSimple biriminin kopyalama](storsimple-clone-volume.md).
* Nasıl çok öğrenin[kullanım StorSimple Cihazınızı StorSimple Yöneticisi hizmet tooadminister hello](storsimple-manager-service-administration.md).

