---
title: "göstergeleri izleme aaaStorSimple | Microsoft Docs"
description: "Merhaba ışık – emitting diyotlar (LED'leri) ve kullanılan sesli uyarılar toomonitor hello hello StorSimple cihazı durumunu açıklar."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 59dee7b9-ca6d-4fd9-96e6-a0071e8d248e
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: alkohli
ms.openlocfilehash: e690b8f4727272f5fbb8886a594a046f794a1380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-monitoring-indicators-toomanage-your-device"></a>Göstergeleri toomanage izleme StorSimple Cihazınızı kullanın
## <a name="overview"></a>Genel Bakış
Modüller ve hello StorSimple cihazı genel durumunu toomonitor kullanabileceğiniz alarmlar hello ve StorSimple Cihazınızı ışık – emitting diyotlar (LED'leri) içerir. göstergeleri izleme hello hello donanım bileşenleri hello aygıtın birincil muhafaza ve hello EBOD muhafazası üzerinde bulunabilir. göstergeleri izleme hello LED'leri veya sesli uyarılar olabilir.

Üç LED kullanılan durumları tooindicate hello durumunu bir modülü vardır: yeşil, yeşil toored amber yanıp veya kırmızı amber.  

* Yeşil LED'leri işletim durumu sağlıklı temsil eder.  
* Yeşil toored amber yanıp LED'leri kullanıcı müdahalesi gerektirebilir kritik olmayan koşullar hello varlığını temsil eder.  
* Kırmızı amber LED'leri hello modülü içinde mevcut kritik bir hata olduğunu gösterir.  

Bu makalenin sonraki bölümlerinde Hello açıklar çeşitli izleme gösterge LED'lerinin, konumlarına hello StorSimple aygıtta Merhaba, hello Aygıt durumu temel üzerinde hello LED durumları ve sesli uyarılar ilişkilendirilen tüm.

## <a name="front-panel-indicator-leds"></a>Ön panel göstergesi LED'leri
hello da bilinen hello ön panelini *operations paneli* veya *ops paneli*, hello sistemde hello birleşik tüm hello modüllerinin durumunu görüntüler. Merhaba ön panel hello StorSimple birincil ve EBOD muhafazası hello aynıdır ve aşağıda gösterilmiştir.  

   ![Cihaz Panosu][1]

Merhaba ön panelini göstergeleri aşağıdaki hello içerir:  

1. Sessiz düğmesi
2. Güç göstergesi LED (kırmızı/yeşil-amber)
3. Modül hata göstergesi (kırmızı-amber/OFF üzerinde) neden
4. Mantıksal hata göstergesi (kırmızı-amber/OFF üzerinde neden
5. Birim kimliği görüntüleme  

Merhaba hello ön panel LED'leri hello aygıtın ve hello EBOD muhafazası için olanlar arasındaki temel farklardan olduğu hello **sistem birimi kimlik numarası** hello LED ekranda gösterilen. Merhaba aygıtta gösterilen kimliği hello varsayılan birim **00**, EBOD muhafazası hello üzerinde görüntülenen hello varsayılan birim kimliği iken **01**. Bu sayede tooquickly, hello EBOD muhafazası hello aygıt arasında hello cihaz açıldığında ayırt. Cihazınızı kapalıysa, sağlanan hello bilgileri kullanmak [üzerinde yeni bir aygıt Aç](storsimple-turn-device-on-or-off.md#turn-on-a-new-device) toodifferentiate hello hello EBOD muhafazası aygıttan.  

## <a name="front-panel-led-status"></a>Ön panel LED durumu
Tablo tooidentify hello durumu hello LED'leri hello aygıt veya hello EBOD muhafazası hello ön panelindeki belirtildiği aşağıdaki hello kullanın.  

| Sistem gücü | Modül hatası | Mantıksal hatası | Uyarı | Durum |
| --- | --- | --- | --- | --- |
| Kırmızı amber |KAPALI |KAPALI |Yok |Yedek güç veya AC güç üzerinde işletim AC güç kesildi ve hello denetleyicisi modülleri kaldırıldı. |
| Yeşil |AÇIK |AÇIK |Yok |OPS paneli (5s'dir) gücüyle test durumu |
| Yeşil |KAPALI |KAPALI |Yok |Açma, iyi tüm işlevleri |
| Yeşil |AÇIK |Yok |PCM hataya LED'leri, fan hataya LED'leri |Fan arıza, üzerinde veya altında sıcaklık herhangi PCM hatası |
| Yeşil |AÇIK |Yok |G/ç modülü LED'leri |Bir Denetleyici Modülü hatası |
| Yeşil |AÇIK |Yok |Yok |Muhafaza mantık hatası |
| Yeşil |Flash |Yok |Modül durumu Denetleyici Modülü GEREKTİRİYORDU. PCM hataya LED'leri, fan hataya LED'leri |Bilinmeyen Denetleyici Modülü türü yüklü, I2C veri yolu hatası, Denetleyici Modülü önemli ürün verilerini (VPD) yapılandırma hatası |

## <a name="power-cooling-module-pcm-indicator-leds"></a>Soğutma Modülü (PCM) göstergesi LED'leri güç
Güç soğutma Modülü (PCM) göstergesi LED'leri hello birincil muhafaza ya da her PCM modül EBOD muhafazası arkasına hello bulunabilir. Bu konuda ele alınmıştır nasıl LED'leri toomonitor hello StorSimple Cihazınızı durumunu izleyen toouse hello.  

* Merhaba birincil muhafaza PCM LED'leri
* Merhaba EBOD muhafazası PCM LED'leri

## <a name="pcm-leds-for-hello-primary-enclosure"></a>Merhaba birincil muhafaza PCM LED'leri
Merhaba StorSimple cihazı ek pil 764W PCM modülüyle sahiptir. Merhaba aşağıdaki çizimde hello LED paneli hello aygıtın gösterir.  

   ![Merhaba birincil kasası üzerinde PCM LED'leri][2]

LED Gösterge:

1. AC güç kesintisi
2. Fan hatası
3. Pil hatası
4. PCM TAMAM
5. DC hatası
6. İyi pil  

PCM hello üzerinde gösterilen hello Hello durumunu paneli GEREKTİRİYORDU. Merhaba cihaz PCM LED paneli altı LED'leri sahiptir. Bu LED'leri dördünü hello güç kaynağı ve hello fan hello durumunu görüntüleyin. iki LED'leri kalan hello hello yedek pil hello PCM modülünde hello durumunu gösterir. Tablolar toodetermine hello hello PCM durumunu izleyen hello kullanabilirsiniz.  

### <a name="pcm-indicator-leds-for-power-supply-and-fan"></a>Güç kaynağı ve fan PCM göstergesi LED'leri
| Durum | PCM hazır (yeşil) | AC başarısız (amber) | Fan başarısız (amber) | DC başarısız (amber) |
| --- | --- | --- | --- | --- |
| AC güç (tooenclosure) |KAPALI |KAPALI |KAPALI |KAPALI |
| AC güç (yalnızca bu PCM) |KAPALI |AÇIK |KAPALI |AÇIK |
| AC sunmak PCM ON - Tamam |AÇIK |KAPALI |KAPALI |KAPALI |
| PCM başarısız (fan başarısız) |KAPALI |KAPALI |AÇIK |Yok |
| PCM hataya (üzerinden geçerli üzerinden voltaj üzerinden amp) |KAPALI |AÇIK |AÇIK |AÇIK |
| PCM (fan tolerans dışı) |AÇIK |KAPALI |KAPALI |AÇIK |
| Bekleme modu |Yanıp |KAPALI |KAPALI |KAPALI |
| PCM üretici yazılımı yükleme |KAPALI |Yanıp |Yanıp |Yanıp |

### <a name="pcm-indicator-leds-for-hello-backup-battery"></a>Merhaba yedek pil için PCM göstergesi LED'leri
| Durum | Pil iyi (yeşil) | Pil hataya (amber) |
| --- | --- | --- |
| Pil mevcut değil |KAPALI |KAPALI |
| Pil mevcut ve dolu |AÇIK |KAPALI |
| Pil şarj veya bakım deşarj |Yanıp |KAPALI |
| Pil "yazılım" hatası (kurtarılabilir) |KAPALI |Yanıp |
| Pil "sabit" hata (kurtarılamaz) |KAPALI |AÇIK |
| Pil disarmed |Yanıp |KAPALI |

## <a name="pcm-leds-for-hello-ebod-enclosure"></a>Merhaba EBOD muhafazası PCM LED'leri
Merhaba EBOD muhafazası 580W PCM ve ek pil vardır. Merhaba EBOD muhafazası Hello PCM paneli yalnızca hello güç kaynakları ve hello fan için gösterge LED'lerinin sahiptir. Merhaba aşağıda bu LED'leri gösterilmektedir.

   ![Merhaba EBOD muhafazası üzerinde PCM LED'leri][3] 

Tablo toodetermine hello hello PCM durumunu izleyen hello kullanabilirsiniz.  

| Durum | PCM hazır (yeşil) | AC başarısız (amber) | Fan başarısız (amber) | DC başarısız (amber) |
| --- | --- | --- | --- | --- |
| AC güç (tooenclosure) |KAPALI |KAPALI |KAPALI |KAPALI |
| AC güç (yalnızca bu PCM) |KAPALI |AÇIK |KAPALI |AÇIK |
| AC sunmak PCM ON – Tamam |AÇIK |KAPALI |KAPALI |KAPALI |
| PCM başarısız (fan başarısız) |KAPALI |KAPALI |AÇIK |X |
| (Üzerinden geçerli üzerinden voltaj üzerinden amp PCM hatası |KAPALI |AÇIK |AÇIK |AÇIK |
| PCM (fan tolerans dışı) |AÇIK |KAPALI |KAPALI |AÇIK |
| Bekleme modeli |Yanıp |KAPALI |KAPALI |KAPALI |
| PCM üretici yazılımı yükleme |KAPALI |Yanıp |Yanıp |Yanıp |

## <a name="controller-module-indicator-leds"></a>Denetleyici Modülü göstergesi LED'leri
Merhaba StorSimple cihazı LED'leri hello birincil denetleyici ve hello EBOD denetleyicisi modüllerini içerir.   

### <a name="monitoring-leds-for-hello-primary-controller"></a>İçin birincil denetleyici hello LED'leri izleme
Merhaba aşağıdaki çizimde hello LED'leri hello birincil denetleyicisinde belirlemenize yardımcı olur. (Merhaba bileşenleri yönde listelenen tooaid tümü.)  

   ![İzleme LED'leri - birincil denetleyici][4]

Merhaba Denetleyici Modülü doğru şekilde çalıştığını olup olmadığını tablo toodetermine aşağıdaki hello kullanın.  

### <a name="controller-indicator-leds"></a>Denetleyici göstergesi LED'leri
| LED | Açıklama |
| --- | --- |
| Kimliği LED (mavi) |Bu hello modül tanımlanan gösterir. Merhaba mavi LED çalışan denetleyicisinde yanıp sönen, ardından hello denetleyicisi hello etkin denetleyicisi ve hello diğeri hello bekleme denetleyicisidir. Daha fazla bilgi için bkz: [tanımla hello etkin denetleyicisinde Cihazınızı](storsimple-8000-controller-replacement.md#identify-the-active-controller-on-your-device). |
| Hataya LED (amber) |Merhaba denetleyicisinde bir hata gösterir. |
| Tamam LED (yeşil) |Sürekli yeşil bu hello denetleyicisi Tamam olduğunu gösterir. Yeşil yanıp denetleyicisi VPD yapılandırma hatası gösterir. |
| SAS etkinlik LED'leri (yeşil) |Sürekli yeşil hiçbir geçerli etkinliği ile bir bağlantı gösterir. Yeşil yanıp devam eden etkinlik hello bağlantı olduğunu gösterir. |
| Ethernet durum LED'leri |Sağdaki bağlantıyı/ağ etkinliği gösterir: (sürekli yeşil) bağlantı (yeşil yanıp) etkin ağ etkinliği. Sol tarafta ağ hızını gösterir: (sarı) 1000 Mb/sn, (yeşil) 100 Mb/sn ve (Kapalı) 10 Mb/sn. Merhaba ağ arabirimi etkinleştirilmemiş olsa bile hello bileşen modeline bağlı olarak, bu ışık yanıp. |
| POST LED'leri |Merhaba denetleyicisi açıldığında hello önyükleme ilerleme durumunu gösterir. Merhaba StorSimple cihazı tooboot başarısız olursa, bu LED Microsoft hello hata gerçekleştiği hello önyükleme işleminde başlangıç noktasını tanımlamak Support yardımcı olur. |

> [!IMPORTANT]
> Merhaba hataya LED aydınlatma, hello denetleyicisi yeniden başlatarak çözülmüş hello Denetleyici Modülü ile ilgili bir sorun yoktur. Yeniden başlatma hello denetleyicisi bu sorunu çözmezse Microsoft Support temasa geçin.  
> 
> 

### <a name="monitoring-leds-for-hello-ebod-ebod-enclosure"></a>Merhaba EBOD (EBOD muhafazası) için izleme LED'leri
Her bir hello 6 Gb/s SAS EBOD denetleyicisi hello aşağıdaki çizimde gösterildiği gibi durumunu belirten LED'leri yüklü.  

  ![LED'leri - EBOD muhafazası izleme][5]

Merhaba EBOD Denetleyici Modülü normal olarak çalışıyor olup olmadığını tablo toodetermine aşağıdaki hello kullanın.  

### <a name="ebod-controller-module-indicator-leds"></a>EBOD denetleyicisi modülü göstergesi LED'leri
| Durum | G/ç modülü hazır (yeşil) | G/ç modülü hatası (amber) | Ana bilgisayar bağlantı noktası etkinliğini (yeşil) |
| --- | --- | --- | --- |
| Denetleyici Modülü Tamam |AÇIK |KAPALI |- |
| Denetleyici Modülü hatası |KAPALI |AÇIK |- |
| Hiçbir dış konak bağlantı |- |- |KAPALI |
| Dış konak bağlantı – etkinliği yok |- |- |AÇIK |
| Dış konak bağlantı - etkinliği |- |- |Yanıp |
| Denetleyici Modülü meta veri hatası |Yanıp |- |- |

## <a name="disk-drive-indicator-leds-for-hello-primary-enclosure-and-ebod-enclosure"></a>Merhaba birincil muhafaza ve EBOD muhafazası için disk sürücüsü göstergesi LED'leri
Merhaba StorSimple cihazı hello birincil muhafaza ve hello EBOD muhafazası bulunan sürücü yok. Bu bölümde açıklandığı gibi her disk sürücüsünü izleme gösterge LED'lerinin içerir. 

Merhaba disk sürücüleri için hello sürücü durumu yeşil gösterilir LED ve kırmızı amber LED bağlanan her sürücü taşıyıcı modülü hello ön. Merhaba aşağıda bu LED'leri gösterilmektedir.

  ![Disk sürücüsü LED'leri][6]

Tablo toodetermine hello sırayla hello genel ön panelini LED durumunu etkileyen her disk sürücüsünü, durumunu izleyen hello kullanın.  

### <a name="disk-drive-indicator-leds-for-hello-ebod-enclosure"></a>Merhaba EBOD muhafazası için disk sürücüsü göstergesi LED'leri
| Durum | Etkinlik Tamam LED (yeşil) | Hataya LED (kırmızı-amber) | OPS paneli LED ilişkili |
| --- | --- | --- | --- |
| Yüklü hiçbir sürücü |KAPALI |KAPALI |None |
| Sürücü yüklü ve çalışır durumda |Etkinliği ile yanıp açık/kapalı |X |None |
| SCSI muhafaza hizmetlerini (SES) aygıt kimlik kümesi |AÇIK |1 saniye üzerinde/ikinci kapalı 1 yanıp |None |
| SES aygıt hataya bit kümesi |AÇIK |AÇIK |Mantıksal hataya (kırmızı) |
| Güç denetimi devresi hatası |KAPALI |AÇIK |Modül hatası (kırmızı) |

## <a name="audible-alarms"></a>Sesli uyarılar
StorSimple cihazı hello birincil muhafaza ve hello EBOD muhafazası ilişkili sesli uyarılar içerir. İşitsel bir alarm hello ön panelini hem kasaları üzerinde (Merhaba ops paneli olarak da bilinir) bulunur. bir hata koşulu mevcut olduğunda Hello sesli alarm gösterir. Aşağıdaki koşullar hello hello alarm etkinleştirir:  

* Fan hatası veya hatası
* Voltaj aralık dışında
* Üzerinden veya sıcaklık koşul altında
* Isı taşması
* Sistem hatası
* Mantıksal hatası
* Güç kaynağı hatası
* Modül (PCM) soğutma güç kaldırılması  

Merhaba aşağıdaki tabloda açıklanmaktadır hello çeşitli alarm durumları.  

### <a name="alarm-states"></a>Uyarı durumları
| Uyarı durumu | Eylem | Sessiz düğmesine basıldı eylemiyle |
| --- | --- | --- |
| S0 |Normal modda: sessiz |İki kez bip |
| S1 |Hataya modu: 1 saniye üzerinde/ikinci kapalı 1 |Geçiş tooS2 veya S3 (notlara bakın) |
| S2 |Mod hatırlat: aralıklı bip |None |
| S3 |Yumuşak modu: sessiz |None |
| S4 |Kritik hata modu: sürekli Uyarısı |Kullanılabilir değil: sessiz etkin değil |

> [!NOTE]
> * 2 dakika içinde sessiz basmayın varsa uyarı durumda S1 hello durumu otomatik olarak tooS2 veya S3 geçer.  
> * Uyarı durumları S1 tooS4 hello hata koşulu temizlendikten sonra tooS0 döndürür.  
> * Kritik hata durumu S4 başka bir durumdan girilebilir.  


Merhaba ops panelde hello sessiz düğmesine basarak hello sesli alarm sessiz. Merhaba sessiz anahtar olmayan el ile çalıştırılır halinde otomatik ses kapatma iki dakika sonra ortaya çıkar. Merhaba alarm kapatıldığında toosound hala bir sorun var. kısa aralıklı bip tooindicate ile devam eder. Tüm hello sorunları kaldırıldığında hello alarm sessiz olacaktır.

Merhaba aşağıdaki tabloda açıklanmaktadır hello çeşitli alarm koşulları.

### <a name="alarm-conditions"></a>Uyarı koşulları
| Durum | Önem Derecesi | Uyarı | OPS LED paneli |
| --- | --- | --- | --- |
| PCM uyarı – tek bir PCM DC Güç kaybı |Hata – artıklık hiçbir kaybı |S1 |Modül hatası |
| PCM uyarı – tek bir PCM DC Güç kaybı |Hata – artıklık kaybı |S1 |Modül hatası |
| PCM fan başarısız |Hata – artıklık kaybı |S1 |Modül hatası |
| SBB modülü PCM hatası algılandı |Hata |S1 |Modül hatası |
| PCM kaldırıldı |Yapılandırma hatası |None |Modül hatası |
| Muhafaza yapılandırma hatası |Hata-kritik |S1 |Modül hatası |
| Düşük sıcaklık uyarı |Uyarı |S1 |Modül hatası |
| Yüksek sıcaklık uyarı |Uyarı |S1 |Modül hatası |
| Sıcaklık Uyarısı |Hata-kritik |S1 |Modül hatası |
| I2C veri yolu hatası |Hata – artıklık kaybı |S1 |Modül hatası |
| İletişim hatası (I2C) OPS paneli |Hata-kritik |S1 |Modül hatası |
| Denetleyici hatası |Hata-kritik |S1 |Modül hatası |
| SBB arabirimi modül hatası |Hata-kritik |S1 |Modül hatası |
| SBB arabirimi modülü hatası – kalan düzgün modülünüz |Hata-kritik |S4 |Modül hatası |
| Kaldırılan SBB arabirimi Modülü |Uyarı |None |Modül hatası |
| Güç denetimi hata sürücü |Uyarı – sürücü güç kaybı olmaksızın |S1 |Modül hatası |
| Güç denetimi hata sürücü |Hata – kritik; Sürücü güç kaybı |S1 |Modül hatası |
| Sürücü kaldırıldı |Uyarı |None |Modül hatası |
| Kullanılabilir yeterli güç yok |Uyarı |Yok |Modül hatası |

## <a name="next-steps"></a>Sonraki adımlar
Daha fazla bilgi edinmek [StorSimple donanım bileşenleri ve durum](storsimple-8000-monitor-hardware-status.md).

[1]: ./media/storsimple-monitoring-indicators/storsimple-monitoring-indicators-IMAGE01.png
[2]: ./media/storsimple-monitoring-indicators/storsimple-monitoring-indicators-IMAGE02.png
[3]: ./media/storsimple-monitoring-indicators/storsimple-monitoring-indicators-IMAGE03.png
[4]: ./media/storsimple-monitoring-indicators/storsimple-monitoring-indicators-IMAGE04.png
[5]: ./media/storsimple-monitoring-indicators/storsimple-monitoring-indicators-IMAGE05.png
[6]: ./media/storsimple-monitoring-indicators/storsimple-monitoring-indicators-IMAGE06.png


