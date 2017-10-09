---
title: "aaaReplace StorSimple 8000 serisi aygıtınızda PCM | Microsoft Docs"
description: "Nasıl güç ve soğutma Modülü (PCM), StorSimple Cihazınızda tooremove ve Değiştir hello açıklar"
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
ms.date: 06/02/2017
ms.author: alkohli
ms.openlocfilehash: 474fd09787c5361a81efda4de74356027ac60f47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="replace-a-power-and-cooling-module-on-your-storsimple-device"></a>StorSimple Cihazınızda güç ve soğutma modülü değiştirin
## <a name="overview"></a>Genel Bakış
Merhaba güç ve soğutma Modülü (PCM) Microsoft Azure StorSimple Cihazınızı içinde oluşan bir güç ve soğutma fanları hello birincil ve ebod denetlenir. Her kasa için sertifikalı PCM, yalnızca bir model yok. Merhaba birincil muhafaza 764 W PCM için sertifikalı ve hello EBOD muhafazası 580 W PCM için sertifikalıdır. Merhaba PCMs hello birincil muhafaza ve hello EBOD muhafazası farklı olsa da hello değiştirme yordamı aynıdır.

Bu öğretici açıklar nasıl yapılır:

* Bir PCM Kaldır
* PCM yenisini yükleyin

> [!IMPORTANT]
> Kaldırma ve bir PCM değiştirme gözden önce hello güvenlik bilgileri [StorSimple donanım bileşeni değiştirme](storsimple-8000-hardware-component-replacement.md).


## <a name="before-you-replace-a-pcm"></a>Bir PCM değiştirmeden önce
Önemli sorunları, PCM değiştirmeden önce aşağıdaki Merhaba dikkat edin:

* Merhaba güç, sağlarsanız PCM başarısız olursa hello hello hatalı modül yüklü bırakır, ancak hello güç kablosu kaldırın. Merhaba fan hello muhafaza tooreceive gücünden devam ve tooprovide uygun soğutma devam edin. Merhaba fan başarısız olursa, hello PCM hemen yerini toobe gerekir.
* Merhaba PCM kaldırmadan önce hello güç PCM hello hello ana anahtarı (var olduğunda) kapatarak veya fiziksel olarak hello güç kablosu kaldırarak bağlantısını kesin. Bu güç kapatma uyaran bir uyarı tooyour sistemi sağlar.
* Değiştirme hello önce hatalı PCM emin olun için diğer PCM işlevseldir bu hello sistem işlemi devam eder. Hatalı PCM tarafından tam olarak işlevsel bir PCM mümkün olan en kısa sürede değiştirilmelidir.
* Yalnızca birkaç dakika toocomplete PCM modülü değiştirme alır, ancak başarısız hello PCM tooprevent aşırı kaldırmanın 10 dakika içinde tamamlanması gerekir.
* Not Hello fabrikası'ndan sevk hello değiştirme 764 W PCM modülleri hello yedek pil modülü içermez. Hatalı PCM'den tooremove hello pil gerekir ve hello değiştirme modülü önceki tooperforming hello değiştirme yerleştirin. Daha fazla bilgi için bkz. nasıl çok[kaldırın ve bir yedek pil Modül Ekle](storsimple-8000-battery-replacement.md).

## <a name="remove-a-pcm"></a>Bir PCM Kaldır
Microsoft Azure StorSimple Cihazınızı hazır tooremove güç ve soğutma Modülü (PCM) olduğunda bu yönergeleri izleyin.

> [!NOTE]
> PCM kaldırmadan önce doğru değiştirme (764 W hello birincil kasası için) veya 580 W hello EBOD muhafazası için sahip olduğunuzu doğrulayın.

#### <a name="tooremove-a-pcm"></a>tooremove bir PCM
1. Hello Klasik Azure portalı, tıklatın **ayarlar > İzleyici > donanım durumu**. Merhaba altındaki hello PCM bileşenlerinin durumunu denetleme **paylaşılan bileşenleri** PCM başarısız oldu tooidentify:
   
   * Güç kaynağı PCM 0 olarak başarısız olursa, durumunu hello **güç kaynağı PCM 0'ın** kırmızı olur.
   * Güç kaynağı PCM 1'de başarısız olursa, durumunu hello **güç kaynağı PCM 1** kırmızı olur.
   * Merhaba fan PCM 1'de başarısız olursa, ya da durumunu hello **PCM 0 0 soğutma** veya **PCM 0 için 1 soğutma** kırmızı olur.
2. Merhaba üzerinde başarısız PCM geri hello birincil kasası hello bulun. 8600 model çalıştırıyorsanız, hello birincil muhafaza hello sistem birimi kimlik numarası hello ön panelini LED ekranda gösterilen bakarak tanımlayın. Merhaba birimi hello birincil muhafaza görüntülenen kimliği varsayılan **00**, birim kimliği görüntülenen EBOD muhafazası hello üzerinde hello varsayılan iken **01**. Merhaba Aşağıdaki diyagramda ve tablo hello ön panelini hello LED görüntüsünün açıklanmaktadır.
   
    ![Ön OPS panelindeki sistem kimliği](./media/storsimple-power-cooling-module-replacement/IC740991.png)
   
     **Şekil 1** hello aygıt ön panelini  
   
   | Etiket | Açıklama |
   |:--- |:--- |
   | 1 |Sessiz düğmesi |
   | 2 |Sistem gücü |
   | 3 |Modül hatası |
   | 4 |Mantıksal hatası |
   | 5 |Birim kimliği görüntüleme |
3. Merhaba birincil muhafaza arkasına hello gösterge LED'lerinin İzleme hello de kullanılabilir tooidentify hello hatalı PCM. Diyagram ve toounderstand nasıl tablo hello aşağıdakilere bakın toouse hello LED'leri toolocate hello hatalı PCM. Örneğin, karşılık gelen toohello hello varsa neden **Fan başarısız** olan aydınlatma, hello fan başarısız oldu. Merhaba, karşılık gelen çok benzer şekilde, neden**AC başarısız** olan aydınlatma, hello güç kaynağı başarısız oldu. 
   
    ![Cihaz PCM izleme gösterge LED'leri devre kartı](./media/storsimple-power-cooling-module-replacement/IC740992.png)
   
     **Şekil 2** geri of PCM LED'leri göstergesi
   
   | Etiket | Açıklama |
   |:--- |:--- |
   | 1 |AC güç kesintisi |
   | 2 |Fan hatası |
   | 3 |Pil hatası |
   | 4 |PCM TAMAM |
   | 5 |DC Güç kesintisi |
   | 6 |Sağlıklı pil |
4. Merhaba StorSimple cihaz toolocate başarısız hello PCM modülü arkasına hello diyagramı aşağıdaki toohello bakın. PCM 0 hello solda ve PCM 1 hello doğru. izleyen hello tablo hello modülleri açıklar.
   
     ![Aygıt birincil muhafaza modüllerinin devre kartı](./media/storsimple-power-cooling-module-replacement/IC740994.png)
   
     **Şekil 3** eklenti modülleri aygıtla arkasına 
   
   | Etiket | Açıklama |
   |:--- |:--- |
   | 1 |PCM 0 |
   | 2 |PCM 1 |
   | 3 |Denetleyici 0 |
   | 4 |Denetleyici 1 |
5. Kapatma kapalı hatalı PCM hello ve hello güç kaynağı kablosunun bağlantısını kesin. Merhaba PCM şimdi kaldırabilirsiniz.
6. Merhaba Mandal ve PCM işlemek, Flash ve erişebildiğinizden arasında hello hello tarafında kavramak ve birlikte tooopen hello tanıtıcı sığdırması.
   
    ![PCM tanıtıcısı açılıyor](./media/storsimple-power-cooling-module-replacement/IC740995.png)
   
    **Şekil 4** açılış hello PCM işleme
7. Tutamacı hello işlemek ve hello PCM kaldırın.
   
    ![Cihaz PCM'i kaldırılıyor](./media/storsimple-power-cooling-module-replacement/IC740996.png)
   
    **Şekil 5** kaldırma hello PCM

## <a name="install-a-replacement-pcm"></a>PCM yenisini yükleyin
Bu yönergeler tooinstall PCM StorSimple Cihazınızı içinde izleyin. Merhaba yedek pil modülü önceki tooinstalling hello değiştirme (yalnızca W PCMs too764 geçerlidir) PCM eklediğiniz emin olun. Daha fazla bilgi için bkz. nasıl çok[kaldırın ve bir yedek pil Modül Ekle](storsimple-8000-battery-replacement.md).

#### <a name="tooinstall-a-pcm"></a>tooinstall bir PCM
1. Bu kutu için hello doğru değiştirme PCM sahip olduğunuzu doğrulayın. 764 W PCM Hello birincil muhafaza gerekir ve hello EBOD muhafazası 580 W PCM gerekiyor. Toouse çalışmamalısınız hello birincil muhafazada 580 W PCM hello veya hello EBOD muhafazası içinde 764 W PCM hello. Görüntü aşağıdaki hello burada hello bu bilgileri etiket yani tooidentify toohello PCM yapıştırılmış gösterir.
   
    ![Cihaz PCM etiketi](./media/storsimple-power-cooling-module-replacement/IC740973.png)
   
    **Şekil 6** PCM etiketi
2. Özellikle dikkat toohello bağlayıcılar ödeme zarar toohello kasası için denetleyin. 
   
   > [!NOTE]
   > **Tüm bağlayıcı PIN'ler Bükülü hello modülü yüklemeyin.**
   > 
   > 
3. PCM işlemek hello hello konumu, slayt hello hello muhafaza modüle açın.
   
    ![Cihaz PCM'i yükleniyor](./media/storsimple-power-cooling-module-replacement/IC740975.png)
   
    **Şekil 7** yükleme hello PCM
4. Merhaba PCM tanıtıcısı el ile kapatın. Merhaba tanıtıcı Mandal prosese gibi bir tıklama sesi.
   
   > [!NOTE]
   > Bağlayıcı PIN'ler hello tooensure gerçekleştiriliyor, hello tutamacı hello mandalı bırakılıyor olmadan hafifçe tug. Out Hello PCM slayt, hello bağlayıcılar gerçekleştiriliyor önce o hello Mandal kapatıldı anlamına gelir.
   
5. Merhaba güç kabloları toohello güç kaynağı ve toohello PCM bağlayın.
6. Merhaba yükü Tahliye bales güvenli hale getirin.
7. PCM Hello üzerinde etkinleştirin.
8. Hello değiştirme işleminin başarılı olduğunu doğrulayın: hello StorSimple Aygıt Yöneticisi'ni hizmetinizin Azure portal, tooyour aygıt gidin ve ardından çok**Ayarları > İzleyici > donanım durumu**. Merhaba altında **paylaşılan bileşenleri**, hello PCM hello durumu yeşil.
   
   > [!NOTE]
   > Merhaba değiştirme PCM toocompletely başlatma için birkaç dakika sürebilir.

## <a name="next-steps"></a>Sonraki adımlar
Daha fazla bilgi edinmek [StorSimple donanım bileşeni değiştirme](storsimple-8000-hardware-component-replacement.md).

