---
title: aaaManage StorSimple birimlerinizi (U2) | Microsoft Docs
description: "Nasıl tooadd, değiştirme, izlemek ve StorSimple birimleri silin ve nasıl açıklanmaktadır tootake gerekirse çevrimdışı."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 57896932-0aa5-4805-970c-d13403ae7551
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 10/28/2016
ms.author: alkohli
ms.openlocfilehash: 8b64f1d92023646cdf881882854d9bc5d7334a10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-volumes-update-2"></a>Merhaba StorSimple Yöneticisi hizmet toomanage birimler (güncelleştirme 2) kullanın
[!INCLUDE [storsimple-version-selector-manage-volumes](../../includes/storsimple-version-selector-manage-volumes.md)]

## <a name="overview"></a>Genel Bakış
Bu öğretici nasıl toouse StorSimple Yöneticisi hizmet toocreate hello ve birimler hello StorSimple cihazı ve StorSimple sanal cihazını güncelleştirme 2 yüklü yönetmek açıklanmaktadır.

Merhaba StorSimple Yöneticisi hizmeti hello StorSimple çözümünüzün bir tek web arabiriminden yönetmenizi sağlayan Klasik Azure portalı bir uzantıdır. Toplama toomanaging birimlerinde hello StorSimple Yöneticisi hizmet toocreate kullanın ve StorSimple hizmetleri yönetmek, görüntülemek ve cihazları yönetmek, uyarıları görüntülemek ve görüntüleyebilir ve yedekleme ilkeleri ve hello yedekleme kataloğu yönetin.

## <a name="volume-types"></a>Birim türleri
StorSimple birimlerini olabilir:

* **Birimler'yerel olarak sabitlenmiş**: Bu birimleri veriler her zaman hello yerel StorSimple cihazda kalır.
* **Katmanlı birimlerin**: Bu birimlerdeki veriler toohello bulut sığdırmaya.

Katmanlı birim türü bir arşivleme birimdir. Arşivleme birimleri için kullanılan hello büyük yinelenenleri kaldırma öbek boyutu hello aygıt tootransfer büyük kesimleri veri toohello bulut sağlar. 

Gerekirse, yerel tootiered veya katmanlı toolocal hello birim türünü değiştirebilirsiniz. Daha fazla bilgi için çok Git[değiştirmek hello birim türü](#change-the-volume-type).

### <a name="locally-pinned-volumes"></a>Yerel olarak sabitlenmiş birimleri
Yerel olarak sabitlenmiş birimlerin veri toohello bulut katmanı değil tam kaynak kullanan birimler olduğundan, böylelikle yerel sağlamak için birincil veri, bulut bağlantısını bağımsız garanti eder. Yerel olarak sabitlenmiş birimlerdeki veriler yinelenenleri kaldırılmış ve sıkıştırılmış değil; Ancak, yerel olarak sabitlenmiş birimlerin anlık görüntüleri yinelenenleri kaldırılmış. 

Yerel olarak sabitlenmiş birimlerin tam olarak sağlanır; Bu nedenle, bunları oluşturduğunuzda aygıtınızda yeterli alan olmalıdır. Yerel olarak sabitlenmiş birimleri 8 TB hello StorSimple 8100 cihazda ve 20 TB'ye hello 8600 aygıttaki en büyük boyutunu tooa sağlayabilirsiniz. StorSimple hello hello cihazda anlık görüntüler, meta verileri ve veri işleme için kalan yerel alan ayırır. Bir yerel olarak sabitlenmiş birim toohello maksimum alan kullanılabilir hello boyutunu artırabilirsiniz ancak hello oluşturulduktan sonra bir birimin boyutunu sayısından az olamaz.

Yerel olarak sabitlenmiş bir birim oluşturduğunuzda, katmanlı birimlerin oluşturması için hello kullanılabilir alan azalır. Merhaba ters doğruysa ayrıca: var olan katmanlı birimler varsa, oluşturma yerel olarak sabitlenmiş birimleri için kullanılabilir hello alanı hello maksimum sınırları yukarıda belirtildiği daha düşük olacaktır. Toohello yerel birimleri hakkında daha fazla bilgi için bkz [üzerinde yerel olarak sabitlenmiş birimlerin sık sorulan sorular](storsimple-local-volume-faq.md).   

### <a name="tiered-volumes"></a>Katmanlı birimleri
Katmanlı birimlerin ölçülü kaynak kullanan birimler erişilen verilerin hello cihazda yerel kalmasını ve daha az sık kullanılan veri otomatik olarak hangi hello sık toohello bulut katmanlı listelenmiştir. Ölçülü kaynak sağlama kullanılabilir depolama alanı tooexceed fiziksel kaynaklar görünür bir sanallaştırma teknolojisidir. Önceden yeterli depolama alanı ayırma yerine, StorSimple tam olarak yeterli alanı toomeet geçerli gereksinimleri ince sağlama tooallocate kullanır. StorSimple artırmak veya Bulut depolama toomeet değişen taleplerini azaltmak için bu yaklaşım bulut depolama esnek yapısını hello kolaylaştırır.

Kullanıyorsanız hello hello seçerek arşiv verileri için katmanlı birim **bu birimi daha az sıklıkta erişilen arşiv verileri için kullanın** onay kutusunu değişiklikleri hello yinelenenleri kaldırma öbek boyutunu biriminiz too512 KB. Bu seçeneği belirlemezseniz hello ilgili katmanlı birim 64 KB öbek boyutu kullanır. Daha büyük bir yinelenenleri kaldırma öbek boyutu hello aygıt tooexpedite hello büyük arşiv verilerinin toohello bulut aktarımını sağlar.

> [!NOTE]
> Bir güncelleştirme öncesi 2 sürümü StorSimple ile oluşturulan arşivleme birimler hello arşivleme onay kutusu seçili katmanlı alınan olacaktır.
> 
> 

### <a name="provisioned-capacity"></a>Sağlanan kapasite
Aşağıdaki tablonun her cihaz ve birim türü için en fazla sağlanan kapasite toohello bakın. (Yerel olarak sabitlenmiş birimleri sanal cihazda kullanılabilir olmadığını unutmayın.)

|  | En çok katmanlı birim boyutu | En fazla yerel olarak sabitlenmiş birim boyutu |
| --- | --- | --- |
| **Fiziksel cihazlar** | | |
| 8100 |64 TB |8 TB |
| 8600 |64 TB |20 TB |
| **Sanal cihazlar** | | |
| 8010 |30 TB |Yok |
| 8020 |64 TB |Yok |

## <a name="hello-volumes-page"></a>Merhaba birimler sayfası
Merhaba **birimleri** sayfası hello Microsoft Azure StorSimple cihazı, başlatıcıları (Sunucuları) için sağlanan toomanage hello depolama birimleri sağlar. StorSimple Cihazınızda birimleri hello listesini gösterir.

 ![Birimler sayfası](./media/storsimple-manage-volumes-u2/VolumePage.png)

Bir birim öznitelikleri bir dizi oluşur:

* **Birim adı** – benzersiz olmalı ve hello birim tanımlamanıza yardımcı olan açıklayıcı bir ad. Bu ad Ayrıca belirli bir birimde filtre raporları izlemede kullanılır.
* **Durum** – çevrimiçi veya çevrimdışı olabilir. Bir birim çevrimdışıysa, erişim toouse hello birim izin görünür tooinitiators (sunucu) değil.
* **Kapasite** – hello toplam hello Başlatıcı (sunucu) tarafından depolanan veri miktarını belirtir. Yerel olarak sabitlenmiş birimleri tam olarak sağlanır ve hello StorSimple cihazında bulunur. Katmanlı birimlerin ölçülü kaynak ve hello veri yinelenenleri kaldırılmış. Ölçülü kaynak kullanan birimler ile Cihazınızı fiziksel depolama kapasitesi dahili olarak veya tooconfigured birim kapasitesi göre hello bulut üzerinde önceden tahsis değil. Merhaba birim kapasitesi ayrılmış ve isteğe bağlı olarak tüketilen.
* **Tür** – hello birim olup olmadığını belirten **katmanlı** (Merhaba varsayılan) veya **yerel olarak sabitlenmiş**.
* **Yedekleme** – hello birim için varsayılan bir yedekleme ilkesi var olup olmadığını gösterir.
* **Erişim** – erişim toothis birim izin hello başlatıcıları (Sunucuları) belirtir. Merhaba birimle ilişkilendirilen erişim denetimi kaydı (ACR) bir üyesi olmayan başlatıcıları hello birim görmezsiniz.
* **İzleme** – olsun veya olmasın bir birim izlenmekte belirtir. Bir birim izleme oluşturulduğunda varsayılan olarak etkin olacaktır. Olacaktır, ancak izleme, bir birim kopya için devre dışı. bir birim için tooenable izleme hello yönergeleri izleyin [bir birimi izleyin](#monitor-a-volume). 

Bu öğretici tooperform hello görevleri aşağıdaki Hello yönergeleri kullanın:

* Birim Ekle 
* Bir birim değiştirme 
* Merhaba birim türünü değiştir
* Bir birim Sil 
* Bir birim çevrimdışı duruma getirin 
* Bir birimi izleyin 

## <a name="add-a-volume"></a>Birim Ekle
[Bir birim oluşturduğunuzda](storsimple-deployment-walkthrough-u2.md#step-6-create-a-volume) StorSimple çözümünüzün dağıtımı sırasında. Bir birim ekleme benzer bir yordamdır.

#### <a name="tooadd-a-volume"></a>tooadd bir birim
1. Merhaba üzerinde **aygıtları** sayfasında, hello cihaz seçin, çift tıklayın ve hello ardından **birim kapsayıcıları** sekmesi.
2. Birim kapsayıcısı hello listeden seçin ve çift tıklatarak tooaccess hello hello kapsayıcı ile ilişkili birimi.
3. Tıklatın **Ekle** hello sayfanın hello sonundaki. Merhaba Birim Ekleme sihirbazının başlatır.
   
     ![Birim temel ayarları Ekleme Sihirbazı](./media/storsimple-manage-volumes-u2/TieredVolEx.png)
4. Hello ekleme Birim Sihirbazı altında **temel ayarları**, aşağıdaki hello:
   
   1. Biriminize bir **Ad** verin.
   2. Seçin bir **kullanım türü** hello aşağı açılan listeden. Her zaman veri toobe hello cihazda yerel olarak kullanılabilir gerektiren iş yükleri için seçin **yerel olarak sabitlenmiş**. Tüm diğer veri türleri için seçin **katmanlı**. (**Katmanlı** hello varsayılandır.)
   3. Seçtiyseniz **katmanlı** 2. adımda hello seçebilirsiniz **bu birimi daha az sıklıkta erişilen arşiv verileri için kullanın** onay kutusunu tooconfigure arşivleme bir birim.
   4. Merhaba girin **sağlanan kapasite** biriminiz GB veya TB cinsinden. Bkz: [sağlanan kapasite](#provisioned-capacity) her cihaz ve birim türü için en büyük boyutlar için. Ara hello **kullanılabilir kapasite** toodetermine ne kadar depolama alanı aygıtınızda gerçekte kullanılabilir.
5. Merhaba ok simgesine tıklayın![Ok simgesi](./media/storsimple-manage-volumes-u2/HCS_ArrowIcon.png). Yerel olarak sabitlenmiş bir birim yapılandırıyorsanız, iletiden hello görürsünüz.
   
    ![Birim türü ileti değiştirin](./media/storsimple-manage-volumes-u2/LocalVolEx.png)
6. Merhaba ok simgesine tıklayın ![ok simgesi](./media/storsimple-manage-volumes-u2/HCS_ArrowIcon.png)yeniden toogo toohello **ek ayarlar** sayfası.
   
    ![Birim Sihirbazı ek ayarları ekleme](./media/storsimple-manage-volumes-u2/AddVolume2.png)<br>
7. Altında **ek ayarlar**, yeni bir erişim denetimi kaydı (ACR) ekleyin:
   
   1. Erişim denetimi kaydı (ACR) hello aşağı açılan listeden seçin. Alternatif olarak, yeni ACR ekleyebilirsiniz. ACRs belirlemek hangi ana bilgisayarların birimlerinizi tarafından eşleşen hello erişebilirsiniz IQN hello kaydında listelenen ile ana bilgisayar. Bir ACR belirtmezseniz iletiden hello görürsünüz.
      
        ![ACR belirtin](./media/storsimple-manage-volumes-u2/SpecifyACR.png)
   2. Merhaba seçmenizi öneririz **bu birim için varsayılan yedeklemeyi etkinleştir** onay kutusu.
   3. Merhaba onay simgesine tıklayın ![Onay simgesi](./media/storsimple-manage-volumes-u2/HCS_CheckIcon.png) Merhaba toocreate hello birimle ayarları belirtildi.

Yeni birim hazır toouse sunulmuştur.

> [!NOTE]
> Yerel olarak sabitlenmiş bir birim oluşturursanız ve ardından başka bir yerel olarak oluşturun, hello birim oluşturma işleri sırayla çalıştırmanız hemen birim sabitlenir. Merhaba sonraki birim oluşturma işi başlamadan önce hello ilk birim oluşturma işi bitmesi gerekir.
> 
> 

## <a name="modify-a-volume"></a>Bir birim değiştirme
Bir birim veya hello birime erişmek konakları hello değişiklik tooexpand gerektiğinde değiştirin.

> [!IMPORTANT]
> * Merhaba birim boyutu hello aygıtta değiştirirseniz, hello birim boyutu hello yanı sıra konak üzerinde değiştirilmiş toobe gerekir. 
> * Burada açıklanan hello konak tarafı Windows Server 2012 (2012R2) adımlardır. Yordamlar Linux veya diğer ana bilgisayar işletim sistemleri için farklı olacaktır. Hello birim başka bir işletim sistemi çalıştıran bir konağa değiştirirken tooyour ana bilgisayar işletim sistemi yönergelerine bakın. 
> 
> 

#### <a name="toomodify-a-volume"></a>toomodify bir birim
1. Merhaba üzerinde **aygıtları** sayfasında, hello cihaz seçin, çift tıklayın ve hello ardından **birim kapsayıcıları** sekmesi.
2. Birim kapsayıcısı hello listeden seçin ve çift tıklatarak hello kapsayıcı ile ilişkili tooview hello birimi.
3. Bir birim seçin ve başlangıç sayfasının hello altında tıklatın **Değiştir**. Merhaba Değiştir Birim Sihirbazı'nı başlatır.
4. Hello değiştirme Birim Sihirbazı'nı altında **temel ayarları**, yapabileceğiniz hello aşağıdaki:
   
   * Merhaba Düzenle **adı**.
   * Merhaba Dönüştür **kullanım türü** yerel olarak sabitlenmiş tootiered veya sabitlenmiş katmanlı toolocally (bkz [değiştirmek hello birim türü](#change-the-volume-type) daha fazla bilgi için).
   * Merhaba artırmak **sağlanan kapasite**. Merhaba **sağlanan kapasite** yalnızca artırılabilir. Oluşturulduktan sonra bir birim küçültülemez.
5. Altında **ek ayarlar**, hello birim çevrimdışı koşuluyla hello ACR, değiştirebilirsiniz. Merhaba birim çevrimiçi ise tootake gerekir, çevrimdışı ilk. Toohello adımlarda başvuran [bir birim çevrimdışına](#take-a-volume-offline) önceki toomodifying hello ACR.
   
   > [!NOTE]
   > Merhaba değiştiremezsiniz **varsayılan yedeklemeyi etkinleştir** hello biriminin seçeneği.
   > 
   > 
6. Merhaba onay simgesine tıklayarak yaptığınız değişiklikleri kaydedin ![onay simgesi](./media/storsimple-manage-volumes-u2/HCS_CheckIcon.png). Merhaba Klasik Azure portalı bir güncelleştirme birim iletisi görüntüler. Merhaba birimi başarıyla güncelleştirildiğinde bir başarı iletisi görüntüler.
7. Bir birim genişlettiğiniz Merhaba, Windows ana bilgisayarınızda aşağıdaki adımları izleyin:
   
   1. Çok Git**Bilgisayar Yönetimi** ->**Disk Yönetimi**.
   2. Sağ **Disk Yönetimi** seçip **diskleri**.
   3. Diskleri Hello listesinde, güncelleştirilmiş hello birim, sağ tıklatın ve ardından seçin **birimi Genişlet**. Merhaba birimi Genişlet Sihirbazı'nı başlatır. **İleri**’ye tıklayın.
   4. Merhaba varsayılan değerleri kabul ederek hello Sihirbazı tamamlayın. Merhaba Sihirbaz tamamlandıktan sonra hello birim artan hello boyutu göstermelidir.
      
      > [!NOTE]
      > Yerel olarak sabitlenmiş bir birim genişletin ve ardından genişletin, ardından hello Birim genişletme işler sırayla çalışır hemen yerel olarak başka bir birim sabitlenmiş. Merhaba sonraki Birim genişletme işi başlamadan önce hello ilk birim genişletme işi bitmesi gerekir.
      > 
      > 

![Video var](./media/storsimple-manage-volumes-u2/Video_icon.png) **Video var**

toowatch gösteren bir video nasıl tooexpand bir birim tıklatın [burada](https://azure.microsoft.com/documentation/videos/expand-a-storsimple-volume/).

## <a name="change-hello-volume-type"></a>Merhaba birim türünü değiştir
Sabitlenmiş katmanlı toolocally ya da yerel olarak sabitlenmiş tootiered hello birim türünü değiştirebilirsiniz. Ancak, bu dönüştürme sık oluşması olmamalıdır. Katmanlı toolocally sabitlenmiş bir birim dönüştürmek için bazı nedenler şunlardır:

* Yerel GARANTİLERİN veri kullanılabilirliği ve performansı ile ilgili
* Bulut gecikmeleri ve bulut bağlantı sorunları ortadan kaldırılması.

Genellikle, bunlar küçük tooaccess sık istediğiniz var olan birimler. Yerel olarak sabitlenmiş bir birim oluşturulduğunda tam olarak sağlanır. Bir katmanlı birim tooa yerel olarak sabitlenmiş birim dönüştürüyorsanız StorSimple hello dönüştürme başlamadan önce Cihazınızda yeterli alana sahip doğrular. Yeterli alanınız yoksa, bir hata alırsınız ve hello işlemi iptal edilecek. 

> [!NOTE]
> Sabitlenmiş katmanlı toolocally dönüştürme başlamadan önce diğer iş yüklerinin alanı gereksinimlerini hello düşünün emin olun. 
> 
> 

Ek alan tooprovision gerekiyorsa toochange yerel olarak sabitlenmiş birim tooa diğer birimlerin birim katmanlı isteyebilirsiniz. Merhaba yerel olarak sabitlenmiş birim tootiered dönüştürürken hello kullanılabilir kapasite hello aygıtta tarafından yayımlanan hello kapasitesi hello boyutu artar. Bağlantı sorunları olan bir birimin hello dönüştürme engelliyorsa hello yerel türü toohello türü katmanlı, hello dönüştürme tamamlanana kadar hello yerel birim katmanlı birim özelliklerini sergiler. Bu durum, bazı veriler toohello bulut geçmiş çünkü. Bu spilled veri hello işlemi tamamlandı ve yeniden kadar serbest bırakılamıyor hello cihazda yerel alan toooccupy devam eder.

> [!NOTE]
> Bir birim dönüştürme biraz zaman alabilir ve Dönüştürme başladıktan sonra iptal edemezsiniz. Hello birim hello dönüştürme sırasında çevrimiçi kalır ve yedek almadan, ancak genişletmek veya hello dönüştürme gerçekleşirken hello birimi geri yükleyin.  
> 
> 

Bir katmanlı tooa yerel olarak sabitlenmiş birim dönüştürme, cihaz performansı olumsuz etkileyebilir. Ayrıca, Etkenler aşağıdaki hello hello süresini toocomplete hello dönüştürme artırabilir:

* Yeterli bant genişliği yoktur.
* Geçerli bir yedekleme yoktur.

Bu etkenler olabilir toominimize hello etkiler:

* İlkeleri azaltma bant genişliğinizi gözden geçirin ve ayrılmış 40 MB/sn bant genişliği kullanılabilir olduğundan emin olun.
* Merhaba dönüştürme yoğun olmayan saatlere zamanlama.
* Merhaba dönüştürme işlemine başlamadan önce bir bulut anlık görüntüsünü alın.

(Farklı iş yükleri destekleme) birden çok birim dönüştürüyorsanız, böylece daha yüksek öncelik birimleri ilk dönüştürülür hello birim dönüştürme önceliğini. Örneğin, dosya paylaşımı iş yükleri birimlerle dönüştürmeden önce sanal makineleri (VM'ler) barındırmak birimlerini veya birimleri SQL iş yükleri ile dönüştürmeniz gerekir.

#### <a name="toochange-hello-volume-type"></a>toochange hello birim türü
1. Merhaba üzerinde **aygıtları** sayfasında, hello cihaz seçin, çift tıklayın ve hello ardından **birim kapsayıcıları** sekmesi.
2. Birim kapsayıcısı hello listeden seçin ve çift tıklatarak hello kapsayıcı ile ilişkili tooview hello birimi.
3. Bir birim seçin ve başlangıç sayfasının hello altında tıklatın **Değiştir**. Merhaba Değiştir Birim Sihirbazı'nı başlatır.
4. Merhaba üzerinde **temel ayarları** sayfasında, hello hello yeni türünü seçerek hello kullanım türünü değiştirme **kullanım türü** aşağı açılan liste.
   
   * Merhaba türü çok değiştiriyorsanız**yerel olarak sabitlenmiş**, StorSimple yeterli kapasitesi varsa toosee denetler.
   * Merhaba türü çok değiştiriyorsanız**katmanlı** ve bu birimi arşiv verileri için select hello kullanılacak **bu birimi daha az sıklıkta erişilen arşiv verileri için kullanın** onay kutusu.
     
       ![Arşiv onay kutusu](./media/storsimple-manage-volumes-u2/ModifyTieredVolEx.png)
5. Merhaba ok simgesine tıklayın ![ok simgesi](./media/storsimple-manage-volumes-u2/HCS_ArrowIcon.png) toogo toohello **ek ayarlar** sayfası. Yerel olarak sabitlenmiş bir birim yapılandırıyorsanız, hello aşağıdaki ileti görüntülenir.
   
    ![Birim türü ileti değiştirin](./media/storsimple-manage-volumes-u2/ModifyLocalVolEx.png)
6. Merhaba ok simgesine tıklayın ![ok simgesi](./media/storsimple-manage-volumes-u2/HCS_ArrowIcon.png) yeniden toocontinue.
7. Merhaba onay simgesine tıklayın ![Onay simgesi](./media/storsimple-manage-volumes-u2/HCS_CheckIcon.png) toostart hello dönüştürme işlemi. Hello Azure portalında bir güncelleştirme birim iletisi görüntüler. Merhaba birimi başarıyla güncelleştirildiğinde bir başarı iletisi görüntüler.

## <a name="take-a-volume-offline"></a>Bir birim çevrimdışı duruma getirin
Toomodify veya delete planlarken tootake çevrimdışı bir birim gerekebilir. Bir birim çevrimdışı olduğunda okuma-yazma erişimi için kullanılabilir değildir. Tootake hello birim çevrimdışı hello aygıt yanı sıra hello ana bilgisayar gerekir. 

#### <a name="tootake-a-volume-offline"></a>tootake çevrimdışı bir birim
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

#### <a name="toodelete-a-volume"></a>toodelete bir birim
1. Merhaba üzerinde **aygıtları** sayfasında, hello cihaz seçin, çift tıklayın ve hello ardından **birim kapsayıcıları** sekmesi.
2. Merhaba birimin toodelete istediğiniz hello birim kapsayıcısı seçin. Merhaba birim kapsayıcı tooaccess hello tıklatın **birimleri** sayfası.
3. Bu kapsayıcı ile ilişkili tüm hello birimi tablo biçiminde görüntülenir. Merhaba durumunu denetlemek hello hacmi toodelete istiyor. Merhaba birim toodelete istediğiniz çevrimdışı durumda değilse, bunu çevrimdışı ilk, aşağıdaki hello adımlar [bir birim çevrimdışına](#take-a-volume-offline).
4. Merhaba birimi çevrim dışı sonra tıklayın **silmek** hello sayfanın hello sonundaki.
5. Onayınız istendiğinde **Evet**’e tıklayın. Merhaba birim artık silinecek ve hello **birimleri** sayfa güncelleştirilmiş hello hello kapsayıcıdaki birimlerin listesini gösterir.
   
   > [!NOTE]
   > Yerel olarak sabitlenmiş bir birim silerseniz, yeni birimleri için kullanılabilir hello alanı hemen güncelleştirilmemiş. Merhaba StorSimple Yöneticisi hizmeti hello yerel alan kullanılabilir düzenli olarak güncelleştirir. Toocreate hello yeni birim denemeden önce birkaç dakika bekleyin öneririz.<br> Ayrıca, yerel olarak sabitlenmiş bir birim silin ve ardından başka bir yerel olarak silerseniz, hello toplu silme işlerini sırayla çalıştırmanız hemen birim sabitlenmiş. Merhaba sonraki toplu silme işi başlamadan önce hello ilk toplu silme işinin bitmesi gerekir.
   > 
   > 

## <a name="monitor-a-volume"></a>Bir birimi izleyin
Birim izleme, bir birim için toocollect g/Ç ile ilgili istatistikler sağlar. İzleme hello için varsayılan olarak etkindir, oluşturduğunuz ilk 32 birimler. Ek birimlerin izleme varsayılan olarak devre dışıdır. Kopyalanan birimlerin izleme varsayılan olarak devre dışıdır.

Aşağıdaki adımları tooenable hello gerçekleştirin veya bir birim için izlemeyi devre dışı bırakın.

#### <a name="tooenable-or-disable-volume-monitoring"></a>tooenable veya birim izleme devre dışı
1. Merhaba üzerinde **aygıtları** sayfasında, hello cihaz seçin, çift tıklayın ve hello ardından **birim kapsayıcıları** sekmesi.
2. Hangi hello birimin bulunduğu hello birim kapsayıcısı seçin ve hello birim kapsayıcı tooaccess hello ardından **birimleri** sayfası.
3. Bu kapsayıcı ile ilişkili tüm hello birimi hello Tablo görünümünde listelenir. ' I tıklatın ve hello birim veya toplu kopyalama seçin.
4. Merhaba sayfasının Hello altında tıklatın **Değiştir**.
5. Merhaba birim Değiştirme Sihirbazı'nda altında **temel ayarları**seçin **etkinleştirmek** veya **devre dışı** hello gelen **izleme** aşağı açılan liste.

## <a name="next-steps"></a>Sonraki adımlar
* Nasıl çok öğrenin[bir StorSimple biriminin kopyalama](storsimple-clone-volume.md).
* Nasıl çok öğrenin[kullanım StorSimple Cihazınızı StorSimple Yöneticisi hizmet tooadminister hello](storsimple-manager-service-administration.md).

