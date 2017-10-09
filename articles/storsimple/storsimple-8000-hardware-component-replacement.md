---
title: "aaaStorSimple 8000 serisi donanım bileşeni değiştirme | Microsoft Docs"
description: "Toosafely nasıl Değiştir hello PCMs, pil, denetleyici modülleri, EBOD denetleyicileri, disk sürücüleri ve StorSimple cihazını kasa açıklar."
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
ms.custom: 
ms.openlocfilehash: 5baca8ff630a1c064cb8bf7e1024b6590f0d6b81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="replace-a-hardware-component-on-your-storsimple-8000-series-device"></a>Donanım bileşeni, StorSimple 8000 serisi Cihazınızda Değiştir

## <a name="overview"></a>Genel Bakış
Merhaba donanım bileşeni değiştirme öğreticileri hello donanım bileşenleri, Microsoft Azure StorSimple 8000 serisi cihaz ve hello adımları gerekli tooremove açıklar ve bunları değiştirin. Bu makalede hello güvenliği simgelerini açıklar, işaretçileri sağlar toohello ayrıntılı öğreticiler ve listeleri hello değiştirebilen bileşenleri.

> [!IMPORTANT]
> Tooremove denemeden önce veya herhangi bir StorSimple bileşeni değiştirin, hello gözden emin olun [güvenliği simgesi kuralları](#safety-icon-conventions) ve diğer [güvenlik önlemlerini](storsimple-safety.md).


### <a name="safety-icon-conventions"></a>Güvenlik simgesi kuralları
Merhaba aşağıdaki tabloda bu öğreticileri kullanılan hello güvenliği simgeler açıklanmaktadır. Merhaba adımları tooremove gidin ve cihaz bileşenlerini değiştirmek gibi Kapat toothese güvenliği simgeler dikkat edin.

| Simgesi | Metin | Ek bilgiler |
|:--- |:--- |:--- |
| ![Uyarı simgesi](./media/storsimple-hardware-component-replacement/Warning.png) |**TEHLİKE!** |Kaçınılması değil, ölüm veya ciddi yaralanma neden olur, zararlı bir durumu gösterir. Sınırlı toohello en aşırı durumlarda bu sinyal sözcüğüdür. |
| ![Uyarı simgesi](./media/storsimple-hardware-component-replacement/Warning.png) |**UYARI!** |Kaçınılması değil, ölüm veya ciddi yaralanma neden olabilir, zararlı bir durumu gösterir. |
| ![Uyarı simgesi](./media/storsimple-hardware-component-replacement/Caution.png) |**DİKKAT!** |Kaçınılması değil, küçük veya Orta yaralanma neden olabilir, zararlı bir durumu gösterir. |
| ![Bildirim simgesi](./media/storsimple-hardware-component-replacement/NoticeIcon.png) |**UYARI:** |Önemli ancak hasar ilgili olmayan kabul bilgi gösterir. |
| ![Elektrik Şoku simgesi](./media/storsimple-hardware-component-replacement/Electric.png) |**Elektrik Şoku hasar** |Yüksek voltaj gösterir. |
| ![Büyük ağırlık simgesi](./media/storsimple-hardware-component-replacement/Weight.png) |**Büyük ağırlık** | |
| ![Hiçbir kullanıcı tarafından bakımı yapılabilen parça simgesi](./media/storsimple-hardware-component-replacement/NoUserServiceableParts.png) |**Hiçbir kullanıcı tarafından bakımı yapılabilen parça** |Düzgün şekilde eğitim almış sürece erişmez. |
| ![Okuma yönergeleri simgesi](./media/storsimple-hardware-component-replacement/ReadInstructions.png) |**Önce tüm yönergelerini okuyun** | |
| ![İpucu tehlike simgesi](./media/storsimple-hardware-component-replacement/TipHazard.png) |**İpucu tehlike** | |

### <a name="before-you-begin"></a>Başlamadan önce
Bu öğreticide kullanılan aygıt ve güvenliği simgelerini hello güvenlik bilgilerini tanıyın. Çok Git[güvenli bir şekilde yüklemek ve StorSimple Cihazınızı çalıştırmak](storsimple-safety.md) tam bilgi için. Emin tooreview hello olması [güvenlik önlemlerini](storsimple-safety.md#handling-precautions) StorSimple Cihazınızı işlemek önce.

Tooreplace bir bileşen çalışmadan önce aşağıdaki bilgilerle hello göz önünde bulundurun.

![Uyarı simgesi](./media/storsimple-hardware-component-replacement/Warning.png) ![elektrik Şoku simgesi](./media/storsimple-hardware-component-replacement/Electric.png) **uyarı!**

* Kendiniz düzgün modülleri ve StorSimple Cihazınızı bileşenlerinin işlerken bir Elektrostatik deşarj veya antistatic mat kullanarak plan.
* Tüm devresi touch değil. Sağlanan hello tanıtıcıları ve Kılavuzlar devresi kullanıma bileşenleri işlerken kullanın.

![Uyarı simgesi](./media/storsimple-hardware-component-replacement/Warning.png) ![fark simgesi](./media/storsimple-hardware-component-replacement/NoticeIcon.png) **dikkat edin:**

Bir modül değiştirdiğinizde **hiçbir zaman bir boş yuva hello muhafaza hello arkada ayrılmaz**. Değiştirme veya boş modülü hello sorun bölümü kaldırmadan önce edinin.

## <a name="hardware-component-replacement-procedures"></a>Donanım bileşeni değiştirme yordamları
StorSimple 8000 serisi Cihazınızı birkaç hello birincil eklenti modülleri ve/veya EBOD kutularının devre kartı oluşur. Merhaba 8600 birincil muhafaza ve EBOD muhafazası çift muhafaza aygıtla iken hello 8100 tek bir birincil muhafazada sahiptir.

Cihazınızı Hello ana donanım bileşenleri tabloları aşağıdaki hello özetlenmiştir. Merhaba Hello bağlantıya **değiştirme yordamı** sütun toogo toohello ilişkili öğretici.

| Bileşenler | # Var | Eklenti modülü? | Değiştirme yordamı |
|:--- |:--- |:--- |:--- |
| Kasa |1 |Hayır |[StorSimple Cihazınızda Hello kasa değiştirin](storsimple-8000-chassis-replacement.md) |
| Birincil denetleyicileri |2 |Evet |[Bir denetleyici modülü, StorSimple Cihazınızda değiştirin](storsimple-8000-controller-replacement.md) |
| 764W güç ve soğutma modülleri (PCMs) |2 |Evet |[StorSimple Cihazınızda güç ve soğutma modülü değiştirin](storsimple-8000-power-cooling-module-replacement.md) |
| Yedek pil |2 |Evet |[StorSimple Cihazınızda Hello yedek pil modülü değiştirin](storsimple-8000-battery-replacement.md) |
| Disk sürücüleri |12 |Evet |[StorSimple Cihazınızı disk sürücüsünde değiştirin](storsimple-8000-disk-drive-replacement.md) |

**Tablo 1** hello birincil muhafazada donanım bileşenleri

Merhaba birincil muhafaza ve hello EBOD muhafazası onların g/ç modülleri farklılık gösterir. Buna ek olarak hello PCMs farklı gücü sahiptir. Merhaba PCMs hello birincil muhafazada 764 W, hello EBOD muhafazası de hello PCMs hello birincil olarak W. 580 ise muhafaza de içeren bir yedek pil modül.

| Bileşenler | # Var | Eklenti modülü? | Değiştirme yordamı |
|:--- |:--- |:--- |:--- |
| Kasa |1 |Hayır |[StorSimple Cihazınızda Hello kasa değiştirin](storsimple-8000-chassis-replacement.md) |
| EBOD denetleyicisi |2 |Evet |[EBOD denetleyicisi, StorSimple Cihazınızda değiştirin](storsimple-8000-ebod-controller-replacement.md) |
| 580W güç ve soğutma modülleri (PCMs) |2 |Evet |[StorSimple Cihazınızda güç ve soğutma modülü değiştirin](storsimple-8000-power-cooling-module-replacement.md) |
| Disk sürücüleri |12 |Evet |[StorSimple Cihazınızı disk sürücüsünde değiştirin](storsimple-8000-disk-drive-replacement.md) |

**Tablo 2** hello EBOD muhafazası donanım bileşenleri

Merhaba eklenti modülleri hello aygıtta ön ve arka diyagramları aşağıdaki hello vurgulanır. Bir değişiklik olursa çeşitli eklenti modülleri hello bu diyagramları toodetermine hello konumunu kullanabilirsiniz. Merhaba ön diyagramı muhafaza ve hello birincil muhafazası eklenti modülleri hello Göster hello disk sürücülerini ve hello arka hello EBOD diyagramların gösterir.

![Disk sürücüleri ile cihazın ön düzlemi](./media/storsimple-hardware-component-replacement/IC741028.png)

**Şekil 1** hello cihazın ön

| Etiket | Açıklama |
|:--- |:--- |
| 0 - 11 |Disk sürücülerini (12 toplam) |

Merhaba birincil muhafaza ve hello EBOD muhafazası sürücü taşıyıcı modülleri vardır. Merhaba kasa on iki 3,5" disk 3 tarafından 4 biçiminde düzenlenmiş sürücüleri barındırır.

![Aygıt birincil muhafaza modüllerinin devre kartı](./media/storsimple-hardware-component-replacement/IC740994.png)

**Şekil 2** hello birincil muhafaza arkasına

| Etiket | Açıklama |
|:--- |:--- |
| 1 |PCM 0 |
| 2 |PCM 1 |
| 3 |Denetleyici 0 |
| 4 |Denetleyici 1 |

![Cihaz EBOD muhafazası eklenti modüllerinin devre kartı](./media/storsimple-hardware-component-replacement/IC769599.png)

**Şekil 3** hello EBOD muhafazası arkasına

| Etiket | Açıklama |
|:--- |:--- |
| 1 |PCM 0 |
| 2 |PCM 1 |
| 3 |EBOD denetleyici 0 |
| 4 |EBOD Denetleyici 1 |

## <a name="field-replaceable-units"></a>Alan değiştirebilen birim
alan değiştirebilen birim (FRU) aşağıdaki hello StorSimple cihazınız için kullanılabilir:

* Kasa (Merhaba tümleşik işlemleri panel dahil)
* 764 W AC PCM
* 580 W AC PCM
* Sürücü taşıyıcı modülü ile sabit disk sürücüsü
* Denetleyici Modülü
* EBOD Denetleyici Modülü
* Yedek pil Modülü
* Raylar Seti rafa

Lütfen [Microsoft Support başvurun](storsimple-8000-contact-microsoft-support.md) tooorder bu değiştirme birimleri hiçbirini.

## <a name="next-steps"></a>Sonraki adımlar
Tüm gözden [güvenlik bilgileri](storsimple-safety.md) tooreplace StorSimple donanım bileşeni çalışmadan önce.

