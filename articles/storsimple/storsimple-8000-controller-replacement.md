---
title: aaaReplace StorSimple 8000 serisi cihaz denetleyicisi | Microsoft Docs
description: "Açıklar nasıl tooremove ve StorSimple 8000 serisi aygıtınızda biri veya her ikisi denetleyicisi modülleri değiştirin."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: alkohli
ms.openlocfilehash: 76d42529da42dff2a214fb840a52392a7f1a97ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="replace-a-controller-module-on-your-storsimple-device"></a>Bir denetleyici modülü, StorSimple Cihazınızda değiştirin
## <a name="overview"></a>Genel Bakış
Bu öğretici açıklar nasıl tooremove ve StorSimple cihazını biri veya her ikisi denetleyicisi modüllerde değiştirin. Ayrıca, hello tek ve çift denetleyicisi değiştirme senaryoları için logic temel hello anlatılmaktadır.

> [!NOTE]
> Önceki tooperforming denetleyicisi değiştirme, her zaman, denetleyici bellenim toohello en son sürümüne güncelleştirmenizi öneririz.
> 
> tooprevent tooyour StorSimple cihazı zarar, hello LED'leri atandığını gösteren kadar hello aşağıdakilerden biri olarak hello denetleyicisi çıkarmayın:
> 
> * Tüm ışık OFF ' dir.
> * LED 3 ![yeşil onay simgesi](./media/storsimple-controller-replacement/HCS_GreenCheckIcon.png), ve ![kırmızı çarpı simgesi](./media/storsimple-controller-replacement/HCS_RedCrossIcon.png) yanıp olan ve LED 0 ve LED 7 **ON**.


Aşağıdaki tablonun hello desteklenen hello denetleyicisi değiştirme senaryolar gösterilmektedir.

| Durumu | Değiştirme senaryosu | Geçerli ilgili yordamı |
|:--- |:--- |:--- |
| 1 |Bir denetleyici başarısız durumda, hello diğer denetleyicisi sağlam ve etkin. |[Tek bir denetleyici değiştirme](#replace-a-single-controller), hello açıklayan [tek denetleyici değiştirme ardındaki mantığı](#single-controller-replacement-logic), hello yanı sıra [değiştirme adımları](#single-controller-replacement-steps). |
| 2 |Her iki hello denetleyicileri başarısız olmuş ve değiştirme gerektirir. Merhaba kasa, diskleri ve disk kasası iyi durumda. |[Çift denetleyici değiştirme](#replace-both-controllers), hello açıklayan [çift denetleyici değiştirme ardındaki mantığı](#dual-controller-replacement-logic), hello yanı sıra [değiştirme adımları](#dual-controller-replacement-steps). |
| 3 |Denetleyicilerinden hello aynı cihaz veya farklı cihazlardan takas. Merhaba kasa, diskleri ve disk kasaları iyi durumda. |Bir yuva uyuşmazlığı uyarı iletisi görüntülenir. |
| 4 |Bir denetleyici yok ve diğer denetleyicisi başarısız hello. |[Çift denetleyici değiştirme](#replace-both-controllers), hello açıklayan [çift denetleyici değiştirme ardındaki mantığı](#dual-controller-replacement-logic), hello yanı sıra [değiştirme adımları](#dual-controller-replacement-steps). |
| 5 |Bir veya iki denetleyicileri başarısız oldu. Merhaba aygıt hello seri konsolu veya Windows PowerShell uzaktan iletişimini erişemez. |[Microsoft Support başvurun](storsimple-8000-contact-microsoft-support.md) el ile denetleyicisi değiştirme yordamı. |
| 6 |Merhaba denetleyicileri nedeniyle olabilir farklı yapım sürümüne sahip:<ul><li>Denetleyicileri farklı yazılım sürümüne sahip.</li><li>Denetleyicileri farklı üretici yazılımı sürümüne sahip.</li></ul> |Merhaba denetleyicisi yazılım sürümleri farklıysa, hello değiştirme mantığı algılar ve yazılım sürümü hello değiştirme denetleyicisinde güncelleştirmeleri hello.<br><br>Merhaba denetleyicisi bellenim sürümleri farklıdır ve bellenim sürümü eski hello **değil** otomatik olarak yükseltilebilir bir uyarı iletisi hello Azure portalında da görüntülenir. Güncelleştirmeleri taramak ve hello Bellenim güncelleştirmeleri yüklemeniz gerekir.</br></br>Hello denetleyicisi bellenim sürümleri farklıdır ve hello eski bellenim sürümü otomatik olarak yükseltilebilir ise, hello denetleyicisi değiştirme mantığı bunu algılar ve hello denetleyicisi başladıktan sonra hello üretici yazılımı otomatik olarak güncelleştirilir. |

Bu başarısız olursa tooremove Denetleyici Modülü gerekir. Bir tek denetleyici değiştirme ya da çift denetleyici değiştirme sonuçlanabilir biri veya her ikisi hello denetleyicisi modülleri başarısız olabilir. Değiştirme yordamlar ve bunları arkasındaki hello mantığı için hello aşağıdakilere bakın:

* [Tek bir denetleyiciyi değiştirme](#replace-a-single-controller)
* [Hem denetleyicileri Değiştir](#replace-both-controllers)
* [Bir denetleyici Kaldır](#remove-a-controller)
* [Bir denetleyici Ekle](#insert-a-controller)
* [Cihazınızı etkin denetleyicisinde Hello tanımlayın](#identify-the-active-controller-on-your-device)

> [!IMPORTANT]
> Bir denetleyici değiştirme ve kaldırma gözden önce hello güvenlik bilgileri [StorSimple donanım bileşeni değiştirme](storsimple-8000-hardware-component-replacement.md).
> 
> 

## <a name="replace-a-single-controller"></a>Tek bir denetleyici değiştirin
Merhaba Microsoft Azure StorSimple cihaz hello iki denetleyicilerinde biri başarısız oldu, arızalı veya eksik tooreplace tek bir denetleyici gerekir.

### <a name="single-controller-replacement-logic"></a>Tek denetleyici değiştirme mantığı
Tek denetleyici yenisini hello başarısız denetleyicisi ilk kaldırmanız gerekir. (Merhaba kalan denetleyicisi hello aygıtta hello etkin denetleyicisidir.) Merhaba değiştirme denetleyicisi eklediğinizde, hello aşağıdaki eylemler gerçekleşir:

1. Merhaba yedek denetleyicisini hemen hello StorSimple cihazı ile iletişim başlatır.
2. Bir anlık görüntüsünü hello sanal sabit disk (VHD) için hello etkin denetleyicisi hello değiştirme denetleyicisinde kopyalanır.
3. böylece bu VHD'den Hello değiştirme Denetleyicisi başlatıldığında, bu bekleme denetleyicisi olarak tanınır hello anlık görüntü değiştirilir.
4. Merhaba değişiklikler tamamlandığında hello yedek denetleyicisini hello bekleme denetleyicisi olarak başlar.
5. Hem hello denetleyicileri çalıştırırken, hello küme çevrimiçi olur.

### <a name="single-controller-replacement-steps"></a>Tek denetleyici değiştirme adımları
Merhaba Microsoft Azure StorSimple Cihazınızı hello denetleyicilerinden biri başarısız olursa aşağıdaki adımları tamamlayın. (Merhaba diğer denetleyicisi etkin ve çalışıyor olması gerekir. Her iki denetleyicileri başarısız veya arıza durumunda çok Git[çift denetleyici değiştirme adımları](#dual-controller-replacement-steps).)

> [!NOTE]
> Bunu hello denetleyicisi toorestart için 30 – 45 dakika sürer ve tamamen hello tek denetleyici değiştirme yordamdan kurtarın. Merhaba kabloları ekleme de dahil olmak üzere hello tüm yordamı için toplam süreyi Hello yaklaşık 2 saattir.


#### <a name="tooremove-a-single-failed-controller-module"></a>tooremove tek başarısız Denetleyici Modülü
1. Portal, Git toohello StorSimple cihaz Yöneticisi hizmeti Hello Azure'ı tıklatın **aygıtları**ve ardından toomonitor istediğiniz hello aygıtı hello adına tıklayın.
2. Çok Git**İzleyici > donanım durumu**. Denetleyici 0 veya denetleyici 1 Hello durumu hata gösterir kırmızı, olması gerekir.
   
   > [!NOTE]
   > başarısız olan denetleyici Hello tek denetleyici değiştirme, her zaman bir bekleme denetleyicisi değil.
   
3. Şekil 1 ve tablo toolocate hello başarısız Denetleyici Modülü aşağıdaki hello kullanın.
   
    ![Aygıt birincil muhafaza modüllerinin devre kartı](./media/storsimple-controller-replacement/IC740994.png)
   
    **Şekil 1** geri of StorSimple cihazı
   
   | Etiket | Açıklama |
   |:--- |:--- |
   | 1 |PCM 0 |
   | 2 |PCM 1 |
   | 3 |Denetleyici 0 |
   | 4 |Denetleyici 1 |
4. Merhaba başarısız denetleyicisinde, tüm bağlı hello ağ kablolarını hello veri noktalarından kaldırın. 8600 model kullanıyorsanız, aynı zamanda hello denetleyicisi toohello EBOD denetleyicisi bağlanma SAS kabloları hello kaldırın.
5. Merhaba adımları [bir denetleyici kaldırmak](#remove-a-controller) tooremove hello denetleyicisi başarısız oldu.
6. Yükleme hello Fabrika değişimini aynı yuva hangi hello başarısız denetleyicisinden hello kaldırıldı. Merhaba tek denetleyici değiştirme mantığı tetikler. Daha fazla bilgi için bkz: [tek denetleyicisi değiştirme mantığı](#single-controller-replacement-logic).
7. Merhaba tek denetleyici değiştirme mantığı hello arka planda ilerler olsa da, hello kabloları yeniden bağlanın. Tüm hello kabloların tam olarak hello dikkatli tooconnect aynı şekilde hello değiştirme önce bağlanmış alın.
8. Merhaba denetleyicisi yeniden başlatıldıktan sonra hello denetleyin **denetleyicisi durumunu** ve hello **küme durumu** hello Azure denetleyicisi hello portal tooverify geri tooa sağlıklı bir durumda ve bekleme modunda.

> [!NOTE]
> Merhaba aygıt hello seri Konsolu aracılığıyla izliyorsanız, hello denetleyicisi hello değiştirme yordamdan Kurtarma sırasında birden çok kez yeniden görebilirsiniz. Ardından Hello seri konsol menüsünde sunulduğunda hello değiştirme tam olduğunu bildiğiniz. Merhaba menü hello denetleyicisi değiştirme başlatmanın iki saat içinde görünmüyorsa, lütfen [Microsoft Support başvurun](storsimple-8000-contact-microsoft-support.md).
>
> Güncelleştirme 4'ten başlayarak, hello cmdlet'ini de kullanabilirsiniz `Get-HCSControllerReplacementStatus` hello Windows PowerShell arabiriminde hello aygıt toomonitor hello hello denetleyicisi değiştirme işleminin durumunu.
> 

## <a name="replace-both-controllers"></a>Hem denetleyicileri Değiştir
Her iki denetleyicileri hello Microsoft Azure StorSimple cihaz üzerinde başarısız oldu, arızalı olan ya da eksik. hem denetleyicileri tooreplace gerekir. 

### <a name="dual-controller-replacement-logic"></a>Çift denetleyici değiştirme mantığı
Çift denetleyici değiştirme hem başarısız denetleyicileri kaldırın ve değişiklik ekleyin. Merhaba iki değiştirme denetleyicisi eklediğinizde, hello aşağıdaki eylemler gerçekleşir:

1. Merhaba değiştirme denetleyici 0 yuvadaki hello aşağıdakileri denetler:
   
   1. Geçerli hello bellenim ve yazılım sürümlerini kullanıyor mu?
   2. Bu hello kümenin parçası?
   3. Çalıştıran hello eş denetleyicisi ve kümelenmiş olur?
      
      Bu koşulların hiçbiri doğruysa hello denetleyicisi hello en son günlük yedekleme için görünüyor (hello bulunan **nonDOMstorage** sürücüde S). Merhaba denetleyicisi hello son anlık görüntüsünü hello VHD hello yedekten kopyalar.
2. Yuva 0 Hello denetleyicisi hello anlık görüntü tooimage kendisini kullanır.
3. Bu sırada, denetleyici 0 toocomplete hello görüntüleme ve başlangıç için 1 yuvadaki hello denetleyicisi bekler.
4. Denetleyici 0 başlatıldıktan sonra Denetleyici 1 0, denetleyici tarafından oluşturulan hello tek denetleyici değiştirme mantığı tetikler hello küme algılar. Daha fazla bilgi için bkz: [tek denetleyicisi değiştirme mantığı](#single-controller-replacement-logic).
5. Daha sonra hem denetleyicileri çalıştıran ve hello küme çevrimiçi duruma gelir.

> [!IMPORTANT]
> Çift denetleyici yerini daha Hello StorSimple cihaz yapılandırıldıktan sonra bile el ile Merhaba aygıtına yedekleme ele temel alır. 24 saat geçtikten sonra günlük aygıt yapılandırma yedeklerini kadar tetiklenir değil. Çalışmak [Microsoft Support](storsimple-8000-contact-microsoft-support.md) toomake aygıtınızın el ile yedekleme.


### <a name="dual-controller-replacement-steps"></a>Çift denetleyici değiştirme adımları
Microsoft Azure StorSimple Cihazınızı hello denetleyicileri her ikisi de başarısız olduğunda bu iş akışı gereklidir. Bu, bir veri merkezinde hello soğutma sistem çalışmayı durdurur ve sonuç olarak, hem hello denetleyicileri kısa bir süre içinde başarısız olabilir. Bağlı olarak açık olup olmadığı hello StorSimple cihazı kapalı veya açık ve olup bir 8600 kullanıyorsanız veya adımları farklı bir dizi bir 8100 model gereklidir.

> [!IMPORTANT]
> Bu hello denetleyicisi toorestart 45 dakika too1 saat alabilir ve tamamen çift denetleyici değiştirme yordamdan kurtarma. Merhaba kabloları ekleme de dahil olmak üzere hello tüm yordamı için toplam süreyi Hello yaklaşık 2,5 saattir.

#### <a name="tooreplace-both-controller-modules"></a>tooreplace hem denetleyicisi modülleri
1. Merhaba aygıt devre dışı bırakılırsa, bu adımı atlayın ve toohello sonraki adıma devam edin. Hello aygıt açıksa, hello aygıt devre dışı bırakın.
   
   1. 8600 model kullanıyorsanız, devre dışı hello birincil muhafaza ilk kapatın ve ardından EBOD muhafazası hello devre dışı.
   2. Merhaba aygıt tamamen kapatıldı kadar bekleyin. Tüm hello LED'leri hello hello cihaz arkasına, kapalı olacaktır.
2. Bağlı toohello veri bağlantı noktaları tüm hello ağ kablolarını kaldırın. 8600 model kullanıyorsanız, aynı zamanda hello birincil muhafaza toohello EBOD muhafazası bağlanma SAS kabloları hello kaldırın.
3. Hem denetleyicileri hello StorSimple cihazınızdan kaldırın. Daha fazla bilgi için bkz: [bir denetleyici kaldırmak](#remove-a-controller).
4. Hello Fabrika değiştirme denetleyici 0 için önce ekleyin ve denetleyici 1'i takın. Daha fazla bilgi için bkz: [bir denetleyici Ekle](#insert-a-controller). Merhaba çift denetleyici değiştirme mantığı tetikler. Daha fazla bilgi için bkz: [çift denetleyici değiştirme mantığı](#dual-controller-replacement-logic).
5. Merhaba denetleyicisi değiştirme mantığı hello arka planda ilerler olsa da, hello kabloları yeniden bağlanın. Tüm hello kabloların tam olarak hello dikkatli tooconnect aynı şekilde hello değiştirme önce bağlanmış alın. Merhaba ayrıntılı yönergeler hello kablosu modelinizde için cihaz bölümünü [StorSimple 8100 cihazınız yüklemek](storsimple-8100-hardware-installation.md) veya [StorSimple 8600 model Cihazınızı yüklemek](storsimple-8600-hardware-installation.md).
6. Merhaba StorSimple cihazında açın. 8600 model kullanıyorsanız:
   
   1. Bu hello EBOD muhafazası ilk açık olduğundan emin olun.
   2. Merhaba EBOD muhafazası çalışıncaya kadar bekleyin.
   3. Merhaba birincil muhafaza açın.
   4. Merhaba ilk denetleyicisi yeniden başlatır ve iyi durumda sonra hello sistem çalıştırırsınız.
      
      > [!NOTE]
      > Merhaba aygıt hello seri Konsolu aracılığıyla izliyorsanız, hello denetleyicisi hello değiştirme yordamdan Kurtarma sırasında birden çok kez yeniden görebilirsiniz. Ardından Hello seri konsol menüsünde görüntülendiğinde, hello değiştirme tam olduğunu bildiğiniz. Merhaba menü hello denetleyicisi değiştirme başlatma 2,5 saat içinde görünmüyorsa, lütfen [Microsoft Support başvurun](storsimple-8000-contact-microsoft-support.md).
     
## <a name="remove-a-controller"></a>Bir denetleyici Kaldır
StorSimple Cihazınızı yordamı tooremove hatalı Denetleyici Modülü aşağıdaki hello kullanın.

> [!NOTE]
> Aşağıdaki çizimler hello denetleyici 0 ' dir. Denetleyici 1 için bu ters.


#### <a name="tooremove-a-controller-module"></a>tooremove Denetleyici Modülü
1. Kaydırma kutusu ve erişebildiğinizden arasında Hello modülü Mandal kavrayın.
2. Hafifçe, Flash ve erişebildiğinizden birlikte toorelease hello denetleyici mandalı sığdırması.
   
    ![Denetleyici mandalı bırakılıyor](./media/storsimple-controller-replacement/IC741047.png)
   
    **Şekil 2** gönderilirler denetleyici mandalı
3. Bir tanıtıcı tooslide hello denetleyicisi hello gövdeden Hello Mandal kullanın.
   
    ![Denetleyiciyi kaydırarak gövdeden çıkarma](./media/storsimple-controller-replacement/IC741048.png)
   
    **Şekil 3** hello gövdeden hareketli hello denetleyicisi

## <a name="insert-a-controller"></a>Bir denetleyici Ekle
StorSimple Cihazınızı hatalı bir modül kaldırdıktan sonra yordamı tooinstall denetleyici üretecini sağlanan Modülü aşağıdaki hello kullanın.

#### <a name="tooinstall-a-controller-module"></a>tooinstall Denetleyici Modülü
1. Arabirim bağlayıcılar hiçbir zarar toohello ise toosee kontrol edin. Merhaba bağlayıcı PIN'ler hiçbirini zarar görmüş veya Bükülü hello modülü yüklemeyin.
2. Merhaba Mandal tam olarak yayımlanan sırada hello Denetleyici Modülü hello kasaya kaydırın.
   
    ![Denetleyiciyi kaydırarak gövdeye](./media/storsimple-controller-replacement/IC741053.png)
   
    **Şekil 4** hareketli denetleyicisi hello kasa ile
3. Merhaba kasaya devam ediliyor toopush hello Denetleyici Modülü sırasında hello mandalı kapatılıyor eklenen hello Denetleyici Modülü ile başlar. Merhaba Mandal tooguide hello denetleyicisi yerine devreye.
   
    ![Denetleyici mandalı kapatılıyor](./media/storsimple-controller-replacement/IC741054.png)
   
    **Şekil 5** hello denetleyici mandalı kapatılıyor
4. Merhaba Mandal yerine tutturur zaman bitirdiniz. Merhaba **Tamam** LED üzerinde şimdi olmalıdır.
   
   > [!NOTE]
   > Merhaba denetleyici ve hello LED tooactivate too5 dakika yukarı alabilir.
  
5. Merhaba değiştirme hello Azure portal, başarılı olduğunu tooverify tooyour aygıt gidin ve ardından çok gidin**İzleyici** > **donanım durumu**, emin olun iki denetleyici 0 ve Denetleyici 1 Sağlıklı (durum yeşil).

## <a name="identify-hello-active-controller-on-your-device"></a>Cihazınızı etkin denetleyicisinde Hello tanımlayın
Toolocate hello etkin denetleyicisinde StorSimple cihazı gerektiren pek çok durumda, ilk kez aygıt kaydı veya denetleyicisi değiştirme gibi vardır. Merhaba etkin denetleyicisi tüm hello disk bellenim ve ağ işlemleri işler. Yöntemleri tooidentify hello etkin denetleyicisi aşağıdaki hello birini kullanabilirsiniz:

* [Hello Azure portal tooidentify hello etkin denetleyicisi kullanın](#use-the-azure-portal-to-identify-the-active-controller)
* [StorSimple tooidentify hello etkin denetleyici için Windows PowerShell'i kullanma](#use-windows-powershell-for-storsimple-to-identify-the-active-controller)
* [Onay hello fiziksel aygıt tooidentify hello etkin denetleyicisi](#check-the-physical-device-to-identify-the-active-controller)

Bu yordamların her biri sonraki açıklanmıştır.

### <a name="use-hello-azure-portal-tooidentify-hello-active-controller"></a>Hello Azure portal tooidentify hello etkin denetleyicisi kullanın
İçinde Azure portal Merhaba, tooyour aygıt gidin ve ardından çok**İzleyici** > **donanım sistem durumu**ve toohello kaydırma **denetleyicileri** bölümü. Burada, hangi denetleyicisi etkindir doğrulayabilirsiniz.

![Azure Portalı'nda etkin denetleyiciyi belirle](./media/storsimple-controller-replacement/IC752072.png)

**Şekil 6** Azure portal gösteren hello etkin denetleyicisi

### <a name="use-windows-powershell-for-storsimple-tooidentify-hello-active-controller"></a>StorSimple tooidentify hello etkin denetleyici için Windows PowerShell'i kullanma
Cihazınızı hello seri konsol üzerinden erişirken bir başlık iletisi görüntülenir. Merhaba başlık iletisi hello modeli, ad, yüklü yazılım sürümü ve eriştiğiniz hello denetleyicisi durumunu gibi temel aygıt bilgileri içerir. Görüntü aşağıdaki hello bir başlık iletisi örneği gösterilmektedir:

![Seri tanıtıcı iletisi](./media/storsimple-controller-replacement/IC741098.png)

**Şekil 7** etkin olarak başlık iletisi gösteren denetleyici 0

Merhaba denetleyici olup olmadığına hello başlık iletisi toodetermine kullanabilirsiniz bağlı toois etkin veya edilgen.

### <a name="check-hello-physical-device-tooidentify-hello-active-controller"></a>Onay hello fiziksel aygıt tooidentify hello etkin denetleyicisi
tooidentify hello etkin denetleyicisinde Cihazınızı bulun hello mavi LED hello birincil muhafaza arkasına hello hello veri 5 bağlantı noktası üzerinde.

Bu ışığı yanıp sönen, hello denetleyicisi etkindir ve hello diğer bekleme modunda denetleyicisidir. Diyagram aşağıdaki hello kullanın ve yardımcı tablo.

![Veri bağlantı noktalarına sahip cihaz birincil muhafaza devre kartı](./media/storsimple-controller-replacement/IC741055.png)

**Şekil 8** veri bağlantı noktası ve izleme LED'leri birincil muhafaza arkasına

| Etiket | Açıklama |
|:--- |:--- |
| 1-6 |Veri 0 – 5 ağ bağlantı noktaları |
| 7 |Mavi LED |

## <a name="next-steps"></a>Sonraki adımlar
Daha fazla bilgi edinmek [StorSimple donanım bileşeni değiştirme](storsimple-8000-hardware-component-replacement.md).

