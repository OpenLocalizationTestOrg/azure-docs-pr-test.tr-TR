---
title: "aaaManage StorSimple birimlerini (güncelleştirme 3) | Microsoft Docs"
description: "Nasıl tooadd, değiştirme, izlemek ve StorSimple birimleri silin ve nasıl açıklanmaktadır tootake gerekirse çevrimdışı."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/19/2017
ms.author: alkohli
ms.openlocfilehash: 6228c4486dd5a7887df670c4c4584c4edcdfc509
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-volumes-update-3-or-later"></a>Merhaba StorSimple cihaz Yöneticisi hizmeti toomanage birimler (güncelleştirme 3 veya üstü) kullanın

## <a name="overview"></a>Genel Bakış

Bu öğretici nasıl toouse StorSimple cihaz Yöneticisi hizmeti toocreate hello ve güncelleştirme 3 ve sonraki sürümleri çalıştıran hello StorSimple 8000 serisi cihazlar birimlerde yönetmek açıklanmaktadır.

Merhaba StorSimple cihaz Yöneticisi hizmeti hello StorSimple çözümünüzün bir tek web arabiriminden yönetmenizi sağlayan Azure portalı bir uzantıdır. Hello Azure portal toomanage birimleri tüm cihazlarınızda kullanın. Ayrıca oluşturun ve StorSimple hizmetleri yönetmek cihazları, yedekleme ilkeleri ve yedekleme kataloğu yönetmenize ve Uyarıları görüntüleyin.

## <a name="volume-types"></a>Birim türleri

StorSimple birimlerini olabilir:

* **Birimler'yerel olarak sabitlenmiş**: Bu birimleri veriler her zaman hello yerel StorSimple cihazda kalır.
* **Katmanlı birimlerin**: Bu birimlerdeki veriler toohello bulut sığdırmaya.

Katmanlı birim türü bir arşivleme birimdir. Arşivleme birimleri için kullanılan hello büyük yinelenenleri kaldırma öbek boyutu hello aygıt tootransfer büyük kesimleri veri toohello bulut sağlar.

Gerekirse, yerel tootiered veya katmanlı toolocal hello birim türünü değiştirebilirsiniz. Daha fazla bilgi için çok Git[değiştirmek hello birim türü](#change-the-volume-type).

### <a name="locally-pinned-volumes"></a>Yerel olarak sabitlenmiş birimleri

Yerel olarak sabitlenmiş birimlerin veri toohello bulut katmanı değil tam kaynak kullanan birimler olduğundan, böylelikle yerel sağlamak için birincil veri, bulut bağlantısını bağımsız garanti eder. Yerel olarak sabitlenmiş birimlerdeki veriler yinelenenleri kaldırılmış ve sıkıştırılmış değil; Ancak, yerel olarak sabitlenmiş birimlerin anlık görüntüleri yinelenenleri kaldırılmış. 

Yerel olarak sabitlenmiş birimlerin tam olarak sağlanır; Bu nedenle, bunları oluşturduğunuzda aygıtınızda yeterli alan olmalıdır. Yerel olarak sabitlenmiş birimleri 8 TB hello StorSimple 8100 cihazda ve 20 TB'ye hello 8600 aygıttaki en büyük boyutunu tooa sağlayabilirsiniz. StorSimple hello hello cihazda anlık görüntüler, meta verileri ve veri işleme için kalan yerel alan ayırır. Bir yerel olarak sabitlenmiş birim toohello maksimum alan kullanılabilir hello boyutunu artırabilirsiniz ancak hello oluşturulduktan sonra bir birimin boyutunu sayısından az olamaz.

Yerel olarak sabitlenmiş bir birim oluşturduğunuzda, katmanlı birimlerin oluşturması için hello kullanılabilir alan azalır. Merhaba ters doğruysa ayrıca: var olan katmanlı birimler varsa, oluşturma yerel olarak sabitlenmiş birimleri için kullanılabilir hello alanı hello maksimum sınırları yukarıda belirtildiği daha düşük olacaktır. Toohello yerel birimleri hakkında daha fazla bilgi için bkz [üzerinde yerel olarak sabitlenmiş birimlerin sık sorulan sorular](storsimple-8000-local-volume-faq.md).

### <a name="tiered-volumes"></a>Katmanlı birimleri

Katmanlı birimlerin ölçülü kaynak kullanan birimler erişilen verilerin hello cihazda yerel kalmasını ve daha az sık kullanılan veri otomatik olarak hangi hello sık toohello bulut katmanlı listelenmiştir. Ölçülü kaynak sağlama kullanılabilir depolama alanı tooexceed fiziksel kaynaklar görünür bir sanallaştırma teknolojisidir. Önceden yeterli depolama alanı ayırma yerine, StorSimple tam olarak yeterli alanı toomeet geçerli gereksinimleri ince sağlama tooallocate kullanır. StorSimple artırmak veya Bulut depolama toomeet değişen taleplerini azaltmak için bu yaklaşım bulut depolama esnek yapısını hello kolaylaştırır.

Kullanıyorsanız hello select Merhaba, arşiv verileri için katmanlı birim **bu birimi daha az sıklıkta erişilen arşiv verileri için kullanın** onay kutusunu toochange hello yinelenenleri kaldırma öbek boyutunu biriminiz too512 KB. Bu seçeneği belirlemezseniz hello ilgili katmanlı birim 64 KB öbek boyutu kullanır. Daha büyük bir yinelenenleri kaldırma öbek boyutu hello aygıt tooexpedite hello büyük arşiv verilerinin toohello bulut aktarımını sağlar.


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

## <a name="hello-volumes-blade"></a>Merhaba birimleri dikey penceresi

Merhaba **birimleri** dikey penceresinde hello Microsoft Azure StorSimple cihazı, başlatıcıları (Sunucuları) için sağlanan toomanage hello depolama birimleri sağlar. Merhaba StorSimple cihazları bağlı tooyour hizmette hello birimlerin listesini gösterir.

 ![Birimler sayfası](./media/storsimple-8000-manage-volumes-u2/volumeslist.png)

Bir birim öznitelikleri bir dizi oluşur:

* **Birim adı** – benzersiz olmalı ve hello birim tanımlamanıza yardımcı olan açıklayıcı bir ad. Bu ad Ayrıca belirli bir birimde filtre raporları izlemede kullanılır. Merhaba birim oluşturulduktan sonra adı değiştirilemez.
* **Durum** – çevrimiçi veya çevrimdışı olabilir. Bir birim çevrimdışıysa, erişim toouse hello birim izin görünür tooinitiators (sunucu) değil.
* **Kapasite** – hello toplam hello Başlatıcı (sunucu) tarafından depolanan veri miktarını belirtir. Yerel olarak sabitlenmiş birimleri tam olarak sağlanır ve hello StorSimple cihazında bulunur. Katmanlı birimlerin ölçülü kaynak ve hello veri yinelenenleri kaldırılmış. Ölçülü kaynak kullanan birimler ile Cihazınızı fiziksel depolama kapasitesi dahili olarak veya tooconfigured birim kapasitesi göre hello bulut üzerinde önceden tahsis değil. Merhaba birim kapasitesi ayrılmış ve isteğe bağlı olarak tüketilen.
* **Tür** – hello birim olup olmadığını belirten **katmanlı** (Merhaba varsayılan) veya **yerel olarak sabitlenmiş**.

Bu öğretici tooperform hello görevleri aşağıdaki Hello yönergeleri kullanın:

* Birim Ekle 
* Bir birim değiştirme 
* Merhaba birim türünü değiştir
* Bir birim Sil 
* Bir birim çevrimdışı duruma getirin 
* Bir birimi izleyin 

## <a name="add-a-volume"></a>Birim Ekle

[Bir birim oluşturduğunuzda](storsimple-8000-deployment-walkthrough-u2.md#step-6-create-a-volume) StorSimple 8000 serisi cihazınızın dağıtım sırasında. Bir birim ekleme benzer bir yordamdır.

#### <a name="tooadd-a-volume"></a>tooadd bir birim

1. Merhaba hello cihazları Tablo listesi hello gelen **aygıtları** dikey penceresinde, Cihazınızı seçin. **+ Birim ekle**’ye tıklayın.

    ![Yeni birim ekleme](./media/storsimple-8000-manage-volumes-u2/step5createvol1.png)

2. Merhaba, **birim Ekle** dikey penceresinde:
   
    1. Merhaba **aygıt seçin** alanı, geçerli cihazınız ile otomatik olarak doldurulur.

    2. Merhaba aşağı açılan listeden hello birim kapsayıcısı tooadd bir birim gereken yeri seçin.

    3.  Biriminiz için bir **Ad** yazın. Merhaba birim oluşturulduktan sonra hello birim yeniden adlandırılamıyor.

    4. Hello Hello aşağı açılan listesinde seçin **türü** biriminiz için. Yerel garantilerin, düşük gecikme sürelerinin ve yüksek performansın gerektiği iş yükleri için **Yerel olarak sabitlenmiş** bir birim seçin. Diğer tüm veriler için **Katmanlı** bir birim seçin. Bu birimi arşiv verileri için kullanıyorsanız **Bu birimi daha az sıklıkta erişilen arşiv verileri için kullanın**’ı işaretleyin.
      
       Katmanlı birim ölçülü sayıda kaynak kullanarak sağlanır ve hızlı oluşturulabilir. Seçme **bu birimi daha az sıklıkta erişilen arşiv verileri için kullanın** arşiv verileri değişiklikleri hello yinelenenleri kaldırma öbek boyutunu biriminiz için hedeflenen katmanlı birim için too512 KB. Bu alan işaretli değilse hello ilgili katmanlı birim 64 KB öbek boyutu kullanır. Daha büyük bir yinelenenleri kaldırma öbek boyutu hello aygıt tooexpedite hello büyük arşiv verilerinin toohello bulut aktarımını sağlar.
       
       Yerel olarak sabitlenmiş bir birim sıkı hazırlanmıştır ve hello birincil veri hello birimde yerel toohello aygıt kalır ve toohello buluta dağıtılmamasını sağlar.  Yerel olarak sabitlenmiş bir birim oluşturursanız, hello aygıt hello yerel katmanlarda kullanılabilir alanı denetler tooprovision hello hello hacmi istenen boyutu. yerel olarak sabitlenmiş bir birim oluşturma işleminin hello hello cihaz toohello bulut varolan veriler dağılmasını neden ve toocreate hello birim geçen hello süre uzun olabilir. Merhaba toplam süre sağlanan hello birim, kullanılabilir ağ bant genişliği ve hello veri aygıtınızda hello boyutuna bağlıdır.

    5. Merhaba belirtin **sağlanan kapasite** biriminiz için. Seçili hello birim türünü temel alan kullanılabilir hello kapasiteyi not edin. Merhaba, birim boyutu hello kullanılabilir alanı aşmamalıdır belirtilmiş.
      
       Yerel olarak sabitlenmiş birimleri too8.5 TB yedeklemek veya hello 8100 cihazda too200 TB katmanlı birimleri sağlayabilirsiniz. Merhaba büyük 8600 cihazında yerel olarak sabitlenmiş birimleri too22.5 TB yedeklemek veya too500 TB katmanlı birimleri sağlayabilirsiniz. Katmanlı birimlerin çalışma gerekli toohost hello hello cihazda yerel alan olduğu gibi yerel olarak sabitlenmiş birimlerin oluşturması katmanlı birimlerin sağlanması için kullanılabilir hello alanı etkiler. Bu nedenle, yerel olarak sabitlenmiş birim oluşturursanız, katmanlı birimlerin oluşturulması için gereken boş alan azalır. Benzer şekilde, katmanlı birim oluşturulduysa, yerel olarak sabitlenmiş birimlerin oluşturması için hello kullanılabilir alan azalır.
      
       8100 Cihazınızda 8,5 TB (izin verilen boyut sınırı) yerel olarak sabitlenmiş bir birim hazırlıyorsanız, hello aygıtta kullanılabilir tüm yerel hello alanı tükendi. Merhaba aygıt toohost hello çalışma kümesine hello yerel alan olmadığından bu noktadan herhangi bir katmanlı birim oluşturamazsınız katmanlı birim. Var olan katmanlı birimler kullanılabilir hello alanı de etkiler. Örneğin, zaten 106 TB boyutunda katmanlı birimlerin bulunduğu bir 8100 cihazınız varsa, yerel olarak sabitlenmiş birimlerin kullanabileceği yalnızca 4 TB’lık alan kalır.

    6. Merhaba, **bağlı Konaklar** alan, hello oka tıklayın. 

        ![Bağlı konaklar](./media/storsimple-8000-manage-volumes-u2/step5createvol2.png)

    7. Merhaba, **bağlı Konaklar** dikey penceresinde, varolan bir ACR seçin veya yeni bir ACR ekleyin. Yeni ACR seçerseniz, ardından tedarik bir **adı** , ACR için hello sağlamak **iSCSI Qualified Name** (IQN), Windows konağınızın. Merhaba IQN yoksa, çok Git[Get hello bir Windows Server konağının IQN'ini](#get-the-iqn-of-a-windows-server-host). **Oluştur**'a tıklayın. Bir birim belirtilen hello ile oluşturulan ayarlar.

        ![Oluştur’a tıklayın](./media/storsimple-8000-manage-volumes-u2/step5createvol3.png)

Yeni birim hazır toouse sunulmuştur.

> [!NOTE]
> Yerel olarak sabitlenmiş bir birim oluşturursanız ve ardından başka bir yerel olarak oluşturun, hello birim oluşturma işleri sırayla çalıştırmanız hemen birim sabitlenir. Merhaba sonraki birim oluşturma işi başlamadan önce hello ilk birim oluşturma işi bitmesi gerekir.

## <a name="modify-a-volume"></a>Bir birim değiştirme

Bir birim veya hello birime erişmek konakları hello değişiklik tooexpand gerektiğinde değiştirin.

> [!IMPORTANT]
> * Merhaba birim boyutu hello aygıtta değiştirirseniz, hello birim boyutu hello yanı sıra konak üzerinde değiştirilmiş toobe gerekir.
> * Burada açıklanan hello konak tarafı Windows Server 2012 (2012R2) adımlardır. Yordamlar Linux veya diğer ana bilgisayar işletim sistemleri için farklı olacaktır. Hello birim başka bir işletim sistemi çalıştıran bir konağa değiştirirken tooyour ana bilgisayar işletim sistemi yönergelerine bakın.

#### <a name="toomodify-a-volume"></a>toomodify bir birim

1. Tooyour StorSimple cihaz Yöneticisi hizmeti gidin ve ardından **aygıtları**. Merhaba Tablo listesindeki hello aygıtların, toomodify düşündüğünüz hello birimin hello cihazı seçin. Tıklatın **ayarlar > birimleri**.

    ![TooVolumes dikey penceresine gidin](./media/storsimple-8000-manage-volumes-u2/modifyvol2.png)

2. Hello birimlerin listeleme tablo, hello birim seçin ve tooinvoke hello bağlam menüsü sağ tıklayın. Seçin **çevrimdışına** tootake hello birim çevrimdışı değiştirir.

    ![Seçin ve birim çevrimdışı duruma getirin](./media/storsimple-8000-manage-volumes-u2/modifyvol4.png)

3. Merhaba, **çevrimdışına** dikey penceresinde hello birim çevrimdışı duruma getirmeden hello etkisi gözden geçirin ve hello karşılık gelen onay kutusunu seçin. Merhaba karşılık gelen hello konak biriminde ilk çevrimdışı olduğundan emin olun. Tootake çevrimdışı bir birim, ana bilgisayar sunucusunda tooStorSimple nasıl bağlanacağını hakkında daha fazla bilgi için toooperating sistemi belirli yönergelerine bakın. Tıklatın **çevrimdışına**.

    ![Birim çevrimdışı duruma getirmeden etkisini gözden geçirin](./media/storsimple-8000-manage-volumes-u2/modifyvol5.png)

4. Çevrimdışı (Merhaba birim durumu tarafından gösterildiği gibi) Hello birimdir sonra hello birim seçin ve tooinvoke hello bağlam menüsü sağ tıklayın. Seçin **birim değiştirmek**.

    ![Birim seçin değiştirme](./media/storsimple-8000-manage-volumes-u2/modifyvol9.png)


5. Merhaba, **birim değiştirmek** dikey penceresinde hello aşağıdaki değişiklikler yapabilir:
   
   1. Merhaba birim **adı** düzenlenemez.
   2. Merhaba Dönüştür **türü** yerel olarak sabitlenmiş tootiered veya sabitlenmiş katmanlı toolocally (bkz [değiştirmek hello birim türü](#change-the-volume-type) daha fazla bilgi için).
   3. Merhaba artırmak **sağlanan kapasite**. Merhaba **sağlanan kapasite** yalnızca artırılabilir. Oluşturulduktan sonra bir birim küçültülemez.
   4. Altında **bağlı Konaklar**, hello ACR değiştirebilirsiniz. toomodify bir ACR, hello birim çevrimdışı olması gerekir.

       ![Birim çevrimdışı duruma getirmeden etkisini gözden geçirin](./media/storsimple-8000-manage-volumes-u2/modifyvol11.png)

5. Tıklatın **kaydetmek** toosave değişikliklerinizi. Onayınız istendiğinde **Evet**’e tıklayın. Hello Azure portalında bir güncelleştirme birim iletisi görüntüler. Merhaba birimi başarıyla güncelleştirildiğinde bir başarı iletisi görüntüler.

    ![Birim çevrimdışı duruma getirmeden etkisini gözden geçirin](./media/storsimple-8000-manage-volumes-u2/modifyvol5.png)

7. Bir birim genişlettiğiniz Merhaba, Windows ana bilgisayarınızda aşağıdaki adımları izleyin:
   
   1. Çok Git**Bilgisayar Yönetimi** ->**Disk Yönetimi**.
   2. Sağ **Disk Yönetimi** seçip **diskleri**.
   3. Diskleri Hello listesinde, güncelleştirilmiş hello birim, sağ tıklatın ve ardından seçin **birimi Genişlet**. Merhaba birimi Genişlet Sihirbazı'nı başlatır. **İleri**’ye tıklayın.
   4. Merhaba varsayılan değerleri kabul ederek hello Sihirbazı tamamlayın. Merhaba Sihirbaz tamamlandıktan sonra hello birim artan hello boyutu göstermelidir.
      
      > [!NOTE]
      > Yerel olarak sabitlenmiş bir birim genişletin ve ardından genişletin, ardından hello Birim genişletme işler sırayla çalışır hemen yerel olarak başka bir birim sabitlenmiş. Merhaba sonraki Birim genişletme işi başlamadan önce hello ilk birim genişletme işi bitmesi gerekir.
      

## <a name="change-hello-volume-type"></a>Merhaba birim türünü değiştir

Sabitlenmiş katmanlı toolocally ya da yerel olarak sabitlenmiş tootiered hello birim türünü değiştirebilirsiniz. Ancak, bu dönüştürme sık oluşması olmamalıdır.

### <a name="tiered-toolocal-volume-conversion-considerations"></a>Katmanlı toolocal birim dönüştürme konuları

Katmanlı toolocally sabitlenmiş bir birim dönüştürmek için bazı nedenler şunlardır:

* Yerel GARANTİLERİN veri kullanılabilirliği ve performansı ile ilgili
* Bulut gecikmeleri ve bulut bağlantı sorunları ortadan kaldırılması.

Genellikle, bunlar küçük tooaccess sık istediğiniz var olan birimler. Yerel olarak sabitlenmiş bir birim oluşturulduğunda tam olarak sağlanır. 

Bir katmanlı birim tooa yerel olarak sabitlenmiş birim dönüştürüyorsanız StorSimple hello dönüştürme başlamadan önce Cihazınızda yeterli alana sahip doğrular. Yeterli alanınız yoksa, bir hata alırsınız ve hello işlemi iptal edilecek. 

> [!NOTE]
> Sabitlenmiş katmanlı toolocally dönüştürme başlamadan önce diğer iş yüklerinin alanı gereksinimlerini hello düşünün emin olun. 

Bir katmanlı tooa yerel olarak sabitlenmiş birim dönüştürme, cihaz performansı olumsuz etkileyebilir. Ayrıca, Etkenler aşağıdaki hello hello süresini toocomplete hello dönüştürme artırabilir:

* Yeterli bant genişliği yoktur.
* Geçerli bir yedekleme yoktur.

Bu etkenler olabilir toominimize hello etkiler:

* İlkeleri azaltma bant genişliğinizi gözden geçirin ve ayrılmış 40 MB/sn bant genişliği kullanılabilir olduğundan emin olun.
* Merhaba dönüştürme yoğun olmayan saatlere zamanlama.
* Merhaba dönüştürme işlemine başlamadan önce bir bulut anlık görüntüsünü alın.

(Farklı iş yükleri destekleme) birden çok birim dönüştürüyorsanız, böylece daha yüksek öncelik birimleri ilk dönüştürülür hello birim dönüştürme önceliğini. Örneğin, dosya paylaşımı iş yükleri birimlerle dönüştürmeden önce sanal makineleri (VM'ler) barındırmak birimlerini veya birimleri SQL iş yükleri ile dönüştürmeniz gerekir.

### <a name="local-tootiered-volume-conversion-considerations"></a>Yerel tootiered birim dönüştürme konuları

Ek alan tooprovision gerekiyorsa toochange yerel olarak sabitlenmiş birim tooa diğer birimlerin birim katmanlı isteyebilirsiniz. Merhaba yerel olarak sabitlenmiş birim tootiered dönüştürürken hello kullanılabilir kapasite hello aygıtta tarafından yayımlanan hello kapasitesi hello boyutu artar. Bağlantı sorunları olan bir birimin hello dönüştürme engelliyorsa hello yerel türü toohello türü katmanlı, hello dönüştürme işlemi tamamlanana kadar hello yerel birim katmanlı birim özelliklerini sergiler. Bu durum, bazı veriler toohello bulut geçmiş çünkü. Bu spilled veri hello işlemi tamamlandı ve yeniden kadar serbest bırakılamıyor hello cihazda yerel alan toooccupy devam eder.

> [!NOTE]
> Bir birim dönüştürme biraz zaman alabilir ve Dönüştürme başladıktan sonra iptal edemezsiniz. Hello birim hello dönüştürme sırasında çevrimiçi kalır ve yedek almadan, ancak genişletmek veya hello dönüştürme gerçekleşirken hello birimi geri yükleyin.


#### <a name="toochange-hello-volume-type"></a>toochange hello birim türü

1. Tooyour StorSimple cihaz Yöneticisi hizmeti gidin ve ardından **aygıtları**. Merhaba Tablo listesindeki hello aygıtların, toomodify düşündüğünüz hello birimin hello cihazı seçin. Tıklatın **ayarlar > birimleri**.

    ![TooVolumes dikey penceresine gidin](./media/storsimple-8000-manage-volumes-u2/modifyvol2.png)

3. Hello birimlerin listeleme tablo, hello birim seçin ve tooinvoke hello bağlam menüsü sağ tıklayın. Seçin **değiştirmek**.

    ![Bağlam menüsünden seçin değiştirme](./media/storsimple-8000-manage-volumes-u2/changevoltype2.png)

4. Merhaba üzerinde **birim değiştirme** dikey penceresinde hello hello yeni türünü seçerek hello birim türünü değiştirme **türü** aşağı açılan liste.
   
   * Merhaba türü çok değiştiriyorsanız**yerel olarak sabitlenmiş**, StorSimple yeterli kapasitesi varsa toosee denetler.
   * Merhaba türü çok değiştiriyorsanız**katmanlı** ve bu birimi arşiv verileri için select hello kullanılacak **bu birimi daha az sıklıkta erişilen arşiv verileri için kullanın** onay kutusu.
   * Yerel olarak sabitlenmiş bir birim katmanlı gibi yapılandırıyorsanız veya _tam tersini_, hello aşağıdaki ileti görüntülenir.
   
    ![Değişiklik birim türü iletisi](./media/storsimple-8000-manage-volumes-u2/changevoltype3.png)

7. Tıklatın **kaydetmek** toosave hello değişiklikleri. Onayınız istendiğinde tıklatın **Evet** toostart hello dönüştürme işlemi. 

    ![Kaydet ve onaylayın](./media/storsimple-8000-manage-volumes-u2/modifyvol11.png)

8. Hello Azure portal hello birimi güncelleştirmek hello işi oluşturmak için bir bildirim görüntüler. Merhaba bildirim toomonitor hello hello toplu dönüştürme işinin durumunu üzerinde'ı tıklatın.

    ![İş için toplu dönüştürme](./media/storsimple-8000-manage-volumes-u2/changevoltype5.png)

## <a name="take-a-volume-offline"></a>Bir birim çevrimdışı duruma getirin

Toomodify planlanırken veya hello birimde tootake çevrimdışı bir birim gerekebilir. Bir birim çevrimdışı olduğunda okuma-yazma erişimi için kullanılabilir değildir. Merhaba birimde çevrimdışı hello konak ve hello cihaz almanız gerekir.

#### <a name="tootake-a-volume-offline"></a>tootake çevrimdışı bir birim

1. Söz konusu Hello birim çevrimdışı duruma getirmeden önce kullanımda olmadığından emin olun.
2. Çevrimdışı Hello birim hello konakta ilk alın. Bu, olası tüm hello birimdeki veri bozulması riskini ortadan kaldırır. Belirli adımlar için işletim sistemi için toohello yönergeler bakın.
3. Hello ana bilgisayar çevrimdışıysa, hello birim çevrimdışı hello aygıtta hello aşağıdaki adımları gerçekleştirerek başlatıldıktan sonra:
   
    1. Tooyour StorSimple cihaz Yöneticisi hizmeti gidin ve ardından **aygıtları**. Merhaba Tablo listesindeki hello aygıtların, toomodify düşündüğünüz hello birimin hello cihazı seçin. Tıklatın **ayarlar > birimleri**.

        ![TooVolumes dikey penceresine gidin](./media/storsimple-8000-manage-volumes-u2/modifyvol2.png)

    2. Hello birimlerin listeleme tablo, hello birim seçin ve tooinvoke hello bağlam menüsü sağ tıklayın. Seçin **çevrimdışına** tootake hello birim çevrimdışı değiştirir.

        ![Seçin ve birim çevrimdışı duruma getirin](./media/storsimple-8000-manage-volumes-u2/modifyvol4.png)

3. Merhaba, **çevrimdışına** dikey penceresinde hello birim çevrimdışı duruma getirmeden hello etkisi gözden geçirin ve hello karşılık gelen onay kutusunu seçin. Tıklatın **çevrimdışına**. 

    ![Birim çevrimdışı duruma getirmeden etkisini gözden geçirin](./media/storsimple-8000-manage-volumes-u2/modifyvol5.png)
      
      Merhaba birim çevrimdışı olduğunda size bildirilir. Merhaba birim durumu ayrıca tooOffline güncelleştirir.
      
4. Bir birim hello birim ve sağ tıklatın, seçerseniz çevrimdışı olduğunda **çevrimiçine** seçeneği hello bağlam menüsünde kullanılabilir olur.

> [!NOTE]
> Merhaba **Çevrimdışına Al** komutu bir istek toohello aygıt tootake hello birim çevrimdışı gönderir. Konaklar hello birim kullanmaya devam ediyorsanız bu bozuk bağlantıları olur ancak hello birim çevrimdışı duruma getirmeden değil başarısız olur.

## <a name="delete-a-volume"></a>Bir birim Sil

> [!IMPORTANT]
> Yalnızca çevrimdışı ise, bir birim silebilirsiniz.

Aşağıdaki adımları toodelete bir birim hello tamamlayın.

#### <a name="toodelete-a-volume"></a>toodelete bir birim

1. Tooyour StorSimple cihaz Yöneticisi hizmeti gidin ve ardından **aygıtları**. Merhaba Tablo listesindeki hello aygıtların, toomodify düşündüğünüz hello birimin hello cihazı seçin. Tıklatın **ayarlar > birimleri**.

    ![TooVolumes dikey penceresine gidin](./media/storsimple-8000-manage-volumes-u2/modifyvol2.png)

3. Merhaba durumunu denetlemek hello hacmi toodelete istiyor. Merhaba birim istiyorsanız toodelete çevrimdışı değil, ilk çevrimdışı duruma getirin. Merhaba adımları [bir birim çevrimdışına](#take-a-volume-offline).
4. Merhaba birim çevrimdışı olduktan sonra hello birimi seçin, tooinvoke hello bağlam menüsü sağ tıklayın ve ardından **silmek**.

    ![Bağlam menüsünden seçin Sil](./media/storsimple-8000-manage-volumes-u2/deletevol1.png)

5. Merhaba, **silmek** dikey penceresinde, gözden geçirme ve bir birim silindiğinde hello etkisi karşı select hello onay kutusu. Bir birim sildiğinizde, hello biriminde bulunan tüm hello verileri kaybolur. 

    ![Kaydet ve değişiklikleri onaylayın](./media/storsimple-8000-manage-volumes-u2/deletevol2.png)

6. Merhaba birim silindikten sonra tooindicate hello silme hello tablo birimlerin listesini güncelleştirir.

    ![Güncelleştirilmiş birim listesi](./media/storsimple-8000-manage-volumes-u2/deletevol3.png)
   
   > [!NOTE]
   > Yerel olarak sabitlenmiş bir birim silerseniz, yeni birimleri için kullanılabilir hello alanı hemen güncelleştirilmemiş. Merhaba StorSimple cihaz Yöneticisi hizmeti hello yerel alan kullanılabilir düzenli olarak güncelleştirir. Toocreate hello yeni birim denemeden önce birkaç dakika bekleyin öneririz.
   >
   > Ayrıca, yerel olarak sabitlenmiş bir birim silin ve ardından başka bir yerel olarak silerseniz, hello toplu silme işlerini sırayla çalıştırmanız hemen birim sabitlenmiş. Merhaba sonraki toplu silme işi başlamadan önce hello ilk toplu silme işinin bitmesi gerekir.

## <a name="monitor-a-volume"></a>Bir birimi izleyin

Birim izleme, bir birim için toocollect g/Ç ile ilgili istatistikler sağlar. İzleme hello için varsayılan olarak etkindir, oluşturduğunuz ilk 32 birimler. Ek birimlerin izleme varsayılan olarak devre dışıdır. 

> [!NOTE]
> Kopyalanan birimlerin izleme varsayılan olarak devre dışıdır.


Aşağıdaki adımları tooenable hello gerçekleştirin veya bir birim için izlemeyi devre dışı bırakın.

#### <a name="tooenable-or-disable-volume-monitoring"></a>tooenable veya birim izleme devre dışı

1. Tooyour StorSimple cihaz Yöneticisi hizmeti gidin ve ardından **aygıtları**. Merhaba Tablo listesindeki hello aygıtların, toomodify düşündüğünüz hello birimin hello cihazı seçin. Tıklatın **ayarlar > birimleri**.
2. Hello birimlerin listeleme tablo, hello birim seçin ve tooinvoke hello bağlam menüsü sağ tıklayın. Seçin **değiştirmek**.
3. Hello içinde **birim değiştirmek** dikey penceresinde için **izleme** seçin **etkinleştirmek** veya **devre dışı** tooenable veya izleme devre dışı bırakın.

    ![İzleme devre dışı bırak](./media/storsimple-8000-manage-volumes-u2/monitorvol1.png) 

4. Tıklatın **kaydetmek** tıklatıp onaylamanız istendiğinde, **Evet**. Hello Azure portal hello birimi başarıyla güncelleştirildikten sonra hello birim ve ardından bir başarı iletisi güncelleştirmek için bir bildirim görüntüler.

## <a name="next-steps"></a>Sonraki adımlar

* Nasıl çok öğrenin[bir StorSimple biriminin kopyalama](storsimple-8000-clone-volume-u2.md).
* Nasıl çok öğrenin[kullanım StorSimple Cihazınızı StorSimple cihaz Yöneticisi hizmeti tooadminister hello](storsimple-8000-manager-service-administration.md).

