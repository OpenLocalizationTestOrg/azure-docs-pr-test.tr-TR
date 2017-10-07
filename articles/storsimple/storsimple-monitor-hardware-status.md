---
title: "aaaStorSimple donanım bileşenleri ve durum | Microsoft Docs"
description: "Nasıl toomonitor hello StorSimple Cihazınızı hello StorSimple Yöneticisi hizmeti aracılığıyla donanım bileşenleri hakkında bilgi edinin."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 0d56a2ba-daf0-45ad-9610-8b8712dd5750
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2016
ms.author: alkohli
ms.openlocfilehash: 12a62c0ffc4a5b5e72a25e9e1d976009be03c598
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomonitor-hardware-components-and-status"></a>Merhaba StorSimple Yöneticisi hizmet toomonitor donanım bileşenleri ve durum kullanın
## <a name="overview"></a>Genel Bakış
Bu makalede hello şirket içi StorSimple Cihazınızı içinde çeşitli fiziksel ve mantıksal bileşenler. Ayrıca nasıl toomonitor hello aygıt bileşen durumu hello kullanarak açıklar **Bakım** hello StorSimple Yöneticisi hizmet sayfasında. 

Merhaba **Bakım** sayfası hello donanım tüm hello StorSimple cihaz bileşenlerinin durumunu gösterir. 

8100 bileşenlerin listesini Hello altında açıklamak üç bölüm bulunur:

* **Paylaşılan bileşenleri** – disk sürücüleri, kasası, PCM bileşenleri ve PCM sıcaklık satır voltaj ve geçerli algılayıcılar satır gibi bu hello denetleyicileri parçası olmayan.
* **Denetleyici 0 bileşenleri** – denetleyici 0, denetleyici, SAS genişletici ve bağlayıcısını gibi üzerinde denetleyicisi sıcaklık algılayıcıları bulunan ve çeşitli hello hello bileşenler ağ arabirimleri.
* **Denetleyici 1 bileşenleri** – hello Denetleyici 1, 0 denetleyicisi için ayrıntılı benzer toothose oluşturan bileşenleri.

8600 model Cihazınızı toohello genişletilmiş demet, diskleri (EBOD) kasası karşılık gelen ek bileşenleri içerir. Bileşenlerin listesi Hello altında beş bölümleri vardır. Bu, aynı toohello 8100 için açıklanan olanları hello birincil muhafazada hello bileşenleri içerir ve üç bölüm vardır. Açıklayan ek için iki bölüme hello EBOD muhafazası vardır:

* **EBOD muhafazası paylaşılan bileşenleri** – hello bileşenleri hello EBOD Muhafazası ve hello EBOD denetleyicisi parçası olmayan PCM sunar.
* **EBOD denetleyici 0 bileşenleri** – hello hello EBOD denetleyicisi gibi EBOD muhafazası 0, üzerinde SAS genişletici ve bağlayıcı ve denetleyici sıcaklık algılayıcıları bulunan bileşenleri.
* **EBOD denetleyicisi 1 bileşenleri** – hello EBOD muhafazası 1, oluşturan bileşenleri benzer toothose EBOD muhafazası 0 ayrıntılı.

> [!NOTE]
> **Merhaba donanım durum bölümü bir StorSimple sanal cihazı (1100) hello bakım sayfasında mevcut değil.**
> 
> 

## <a name="monitor-hello-hardware-status"></a>Merhaba donanım durumunu izleme
Adımları tooview hello donanım aygıtı bileşenin durumunu izleyen hello gerçekleştirin:

1. Çok gidin**aygıtları**, belirli bir StorSimple cihazı seçin. Toogo hello cihaz düzeyinde menüsüne tıklayın ve ardından **Bakım**. 
2. Merhaba bulun **donanım durum** bölüm ve'hello kullanılabilir bileşenlerini (yukarıda açıklandığı gibi) seçin. Merhaba bileşen etiket tooexpand hello listesi ve görünümü hello durumunu hello önceki bir ok çeşitli aygıt bileşenlerini tıklamanız yeterlidir. Merhaba bkz [hello birincil kasa için ayrıntılı bileşen listesi](#component-list-for-primary-enclosure-of-storsimple-device) ve hello [hello EBOD muhafazası için ayrıntılı bileşen listesi](#component-list-for-ebod-enclosure-of-storsimple-device).
3. Renk düzenini toointerpret kodlama hello bileşen durumu aşağıdaki hello kullan:
   
   * **Yeşil onay** – Denotes bir **sağlıklı** veya **Tamam** bileşeni.
   * **Sarı** – bir bileşenin gösterir **uyarı** durumu.
   * **Kırmızı bir ünlem işareti** – Denotes sahip bir bileşen bir **hatası** veya **dikkat** durumu.
   * **Siyah metinle beyaz** – mevcut olmayan bir bileşeni gösterir.
4. Kullanımda olmayan bir bileşeni karşılaşırsanız bir **sağlıklı** durum, Microsoft Support başvurun. Uyarıları aygıtınızda etkinleştirilirse, bir e-posta uyarısı alırsınız. Tooreplace başarısız donanım bileşeni gerekirse bkz [StorSimple donanım bileşeni değiştirme](storsimple-hardware-component-replacement.md).

## <a name="component-list-for-primary-enclosure-of-storsimple-device"></a>StorSimple cihazı birincil kasası için bileşen listesi
Merhaba aşağıdaki tabloda ana hatlarını hello birincil şirket içi StorSimple Cihazınızı muhafazada yer alan fiziksel ve mantıksal bileşenleri hello.

| Bileşen | Modül | Tür | Konum | Alan değiştirilebilen biriminin (FRU)? | Açıklama |
| --- | --- | --- | --- | --- | --- |
| [0-11] yuvasında sürücü |Disk sürücüleri |Fiziksel |Paylaşılan |Evet |Tek bir çizgi her hello SSD için sunulan veya hello HDD hello birincil muhafazada sürücüler. |
| Ortam sıcaklık algılayıcısı |Kasası |Fiziksel |Paylaşılan |Hayır |Ölçüler hello kasa içinde sıcaklık hello. |
| Orta düzlemi sıcaklık algılayıcısı |Kasası |Fiziksel |Paylaşılan |Hayır |Ölçüler hello Orta düzlemi sıcaklığını hello. |
| Sesli Uyarısı |Kasası |Fiziksel |Paylaşılan |Hayır |Merhaba sesli alarm alt hello kasa içinde işlev olup olmadığını gösterir. |
| Kasası |Kasası |Fiziksel |Paylaşılan |Evet |Bir kasa Hello varlığını gösterir. |
| Kasa ayarları |Kasası |Fiziksel |Paylaşılan |Hayır |Merhaba kasa ön panelini toohello başvuruyor. |
| Satır voltaj algılayıcı |PCM |Fiziksel |Paylaşılan |Hayır |Çok sayıda satırı voltaj algılayıcıları voltaj hello ölçülen tolerans dahilinde olup gösteren görüntülenen durumlarına sahip. |
| Satır geçerli algılayıcılar |PCM |Fiziksel |Paylaşılan |Hayır |Çok sayıda satırı geçerli algılayıcılar hello ölçülen geçerli tolerans dahilinde olup olmadığını gösteren görüntülenen durumlarına sahip. |
| Sıcaklık algılayıcı PCM içinde |PCM |Fiziksel |Paylaşılan |Hayır |Çok sayıda sıcaklık algılayıcıları gibi giriş ve etkin nokta algılayıcılar hello sıcaklık ölçülen olup olmadığını belirten görüntülenen durumlarına tolerans dahilinde olduğu. |
| Güç kaynağı [0-1] |PCM |Fiziksel |Paylaşılan |Evet |Tek bir çizgi hello hello aygıtın arkasında bulunan iki PCMs her hello güç kaynakları hello olarak sunulur. |
| Soğutma [0-1] |PCM |Fiziksel |Paylaşılan |Evet |Tek bir çizgi her Merhaba için iki PCMs hello bulunan dört soğutma fanları sunulur. |
| Pil [0-1] |PCM |Fiziksel |Paylaşılan |Evet |Tek bir çizgi her hello PCM yerleştirildiğinden hello yedek pil modüllerin sunulur. |
| Metis |Yok |Mantıksal |Paylaşılan |Yok |Merhaba piller hello durumunu görüntüler: olup şarj ihtiyaç duydukları ve yaşam sonu yaklaşan. |
| Küme |Yok |Mantıksal |Paylaşılan |Yok |Oluşturulan hello kümenin hello iki Tümleşik Denetleyici modülleri arasında durumunu görüntüler hello. |
| Küme düğümü |Yok |Mantıksal |Paylaşılan |Yok |Merhaba denetleyicisi hello kümesinin parçası olarak Hello durumunu gösterir. |
| Küme Çekirdeği |Yok |Mantıksal | |Yok |Merhaba çoğunluğu hello HDD depolama havuzu disk üyelik Hello varlığını gösterir. |
| HDD veri alanı |Yok |Mantıksal |Paylaşılan |Yok |Merhaba sabit disk sürücüsü (HDD) depolama Havuzu'ndaki verileri için kullanılan hello depolama alanı. |
| HDD yönetim alanı |Yok |Mantıksal |Paylaşılan |Yok |Merhaba alan hello HDD depolama havuzu yönetim görevleri için ayrılmış. |
| HDD çekirdek alanı |Yok |Mantıksal |Paylaşılan |Yok |Merhaba alan hello HDD depolama havuzu küme çekirdeği için ayrılmış. |
| HDD değiştirme alanı |Yok |Mantıksal |Paylaşılan |Yok |Merhaba alan hello HDD depolama havuzu denetleyicisi değiştirme için ayrılmış. |
| SSD veri alanı |Yok |Mantıksal |Paylaşılan |Yok |Merhaba katı hal sürücüsü (SSD) depolama Havuzu'ndaki verileri için kullanılan hello depolama alanı. |
| SSD NVRAM alanı |Yok |Mantıksal |Paylaşılan |Yok |Merhaba NVRAM mantığı için ayrılmış SSD depolama havuzu Hello depolama alanı. |
| HDD depolama havuzu |Yok |Mantıksal |Paylaşılan |Yok |Görüntüler HDD aygıttan oluşturulan hello mantıksal depolama havuzunun durumu hello. |
| SSD depolama havuzu |Yok |Mantıksal |Paylaşılan |Yok |Görüntüler SSD aygıttan oluşturulan hello mantıksal depolama havuzunun durumu hello. |
| Denetleyici [0-1] [state] |G/Ç |Fiziksel |Denetleyici |Evet |Merhaba denetleyicisinin hello durumunu görüntüler ve etkin ya da bekleme moduna hello kasa içinde olup. |
| Sıcaklık algılayıcı denetleyicideki |G/Ç |Fiziksel |Denetleyici |Hayır |G/ç modülü, CPU sıcaklık, DIMM ve PCIe algılayıcılar gibi çok sayıda sıcaklık algılayıcıları karşılaştı hello sıcaklık tolerans dahilinde olup olmadığını gösteren görüntülenen durumlarına sahip. |
| SAS genişletici |G/Ç |Fiziksel |Denetleyici |Hayır |Kullanılan tooconnect hello tümleşik depolama toohello denetleyicisi olan hello seri ekli SCSI (SAS) genişletici, Hello durumunu gösterir. |
| SAS Bağlayıcısı [0-1] |G/Ç |Fiziksel |Denetleyici |Hayır |Tümleşik kullanılan tooconnect depolama toohello SAS genişletici olan her bir SAS Bağlayıcısı Hello durumunu gösterir. |
| SBB Orta düzlemi bağlantı |G/Ç |Fiziksel |Denetleyici |Hayır |Kullanılan tooconnect olan hello Orta düzlemi bağlayıcı Hello durumunu her denetleyici toohello Orta düzlemi gösterir. |
| İşlemci çekirdeği |G/Ç |Fiziksel |Denetleyici |Hayır |Merhaba işlemci çekirdeği her denetleyici içinde Hello durumunu gösterir. |
| Muhafaza elektronik gücü |G/Ç |Fiziksel |Denetleyici |Hayır |Merhaba hello kasası tarafından kullanılan hello güç sistem durumunu gösterir. |
| Muhafaza elektronik tanılama |G/Ç |Fiziksel |Denetleyici |Hayır |Merhaba tanılama alt sistemleri hello denetleyicisi tarafından sağlanan Hello durumunu gösterir. |
| Temel kart yönetim denetleyicisi (BMC) |G/Ç |Fiziksel |Denetleyici |Hayır |Algılayıcılar hello donanım aygıtı izler ve hello Sistem Yöneticisi bağımsız bir bağlantı üzerinden iletişim kuran bir özel hizmet işlemci olan hello temel kart yönetim denetleyicisi (BMC) Hello durumunu gösterir. |
| Ethernet |G/Ç |Fiziksel |Denetleyici |Hayır |Her hello ağ arabirimleri, diğer bir deyişle, hello yönetimi ve veri bağlantı noktaları hello denetleyicisinde sağlanan Hello durumunu gösterir. |
| NVRAM |G/Ç |Fiziksel |Denetleyici |Hayır |NVRAM, güç kesintisi hello olayda tooretain uygulama kritik bilgilerin hizmet hello pil tarafından yedeklenen bir geçici olmayan rasgele erişim belleği Hello durumunu gösterir. |

## <a name="component-list-for-ebod-enclosure-of-storsimple-device"></a>StorSimple cihaz EBOD muhafazası için bileşen listesi
Merhaba aşağıdaki tabloda ana hatlarını hello EBOD muhafazası şirket içi StorSimple cihazınızın yer alan fiziksel ve mantıksal bileşenleri hello.

| Bileşen | Modül | Tür | Konum | FRU? | Açıklama |
| --- | --- | --- | --- | --- | --- |
| [0-11] yuvasında sürücü |Disk sürücüleri |Fiziksel |Paylaşılan |Evet |Tek bir çizgi her hello EBOD muhafazası Merhaba öne HDD sürücülerini hello sunulur. |
| Ortam sıcaklık algılayıcısı |Kasası |Fiziksel |Paylaşılan |Hayır |Ölçüler hello kasa içinde sıcaklık hello. |
| Orta düzlemi sıcaklık algılayıcısı |Kasası |Fiziksel |Paylaşılan |Hayır |Ölçüler hello Orta düzlemi sıcaklığını hello. |
| Sesli Uyarısı |Kasası |Fiziksel |Paylaşılan |Hayır |Merhaba sesli alarm alt hello kasa içinde işlev olup olmadığını gösterir. |
| Kasası |Kasası |Fiziksel |Paylaşılan |Evet |Bir kasa Hello varlığını gösterir. |
| Kasa ayarları |Kasası |Fiziksel |Paylaşılan |Hayır |Toohello OPS veya hello kasa ön panelini hello anlamına gelir. |
| Satır voltaj algılayıcı |PCM |Fiziksel |Paylaşılan |Hayır |Çok sayıda satırı voltaj algılayıcıları voltaj hello ölçülen tolerans dahilinde olup gösteren görüntülenen durumlarına sahip. |
| Satır geçerli algılayıcılar |PCM |Fiziksel |Paylaşılan |Hayır |Çok sayıda satırı geçerli algılayıcılar hello ölçülen geçerli tolerans dahilinde olup olmadığını gösteren görüntülenen durumlarına sahip. |
| Sıcaklık algılayıcı PCM içinde |PCM |Fiziksel |Paylaşılan |Hayır |Çok sayıda sıcaklık algılayıcıları gibi giriş ve etkin nokta algılayıcılar hello sıcaklık ölçülen olup olmadığını gösteren görüntülenen durumlarına tolerans dahilinde olduğu. |
| Güç kaynağı [0-1] |PCM |Fiziksel |Paylaşılan |Evet |Tek bir çizgi hello hello aygıtın arkasında bulunan iki PCMs her hello güç kaynakları hello olarak sunulur. |
| Soğutma [0-1] |PCM |Fiziksel |Paylaşılan |Evet |Tek bir çizgi her Merhaba için iki PCMs hello bulunan dört soğutma fanları sunulur. |
| Yerel depolama [HDD] |Yok |Mantıksal |Paylaşılan |Yok |Görüntüler HDD aygıttan oluşturulan hello mantıksal depolama havuzunun durumu hello. |
| Denetleyici [0-1] [state] |G/Ç |Fiziksel |Denetleyici |Evet |Merhaba EBOD modülü hello denetleyicilerinin durumunu görüntüler hello. |
| EBOD sıcaklık algılayıcıları |G/Ç |Fiziksel |Denetleyici |Hayır |Çok sayıda sıcaklık algılayıcıları her denetleyicisinden karşılaştı hello sıcaklık tolerans dahilinde olup olmadığını gösteren görüntülenen durumlarına sahip. |
| SAS genişletici |G/Ç |Fiziksel |Denetleyici |Hayır |Kullanılan tooconnect hello tümleşik depolama toohello denetleyicisidir hello SAS genişletici Hello durumunu gösterir. |
| SAS Bağlayıcısı [0-2] |G/Ç |Fiziksel |Denetleyici |Hayır |Tümleşik kullanılan tooconnect depolama toohello SAS genişletici olan her bir SAS Bağlayıcısı Hello durumunu gösterir. |
| SBB Orta düzlemi bağlantı |G/Ç |Fiziksel |Denetleyici |Hayır |Kullanılan tooconnect olan hello Orta düzlemi bağlayıcı Hello durumunu her denetleyici toohello Orta düzlemi gösterir. |
| Muhafaza elektronik gücü |G/Ç |Fiziksel |Denetleyici |Hayır |Merhaba hello kasası tarafından kullanılan hello güç sistem durumunu gösterir. |
| Muhafaza elektronik tanılama |G/Ç |Fiziksel |Denetleyici |Hayır |Merhaba tanılama alt sistemleri hello denetleyicisi tarafından sağlanan Hello durumunu gösterir. |
| Bağlantı toodevice denetleyicisi |G/Ç |Fiziksel |Denetleyici |Hayır |Merhaba hello EBOD g/ç modülü hello aygıt denetleyicisi arasındaki hello bağlantı durumunu gösterir. |

## <a name="next-steps"></a>Sonraki adımlar
* toouse StorSimple Yöneticisi hizmet tooadminister çok gidin, aygıtınız hello[kullanım StorSimple Cihazınızı StorSimple Yöneticisi hizmet tooadminister hello](storsimple-manager-service-administration.md).
* Tootroubleshoot düşürülmüş veya başarısız durumuna sahip bir aygıt bileşeni gereksinim duyarsanız, çok başvurun [göstergeleri izleme StorSimple](storsimple-monitoring-indicators.md). 
* tooreplace başarısız donanım bileşeni Bkz [StorSimple donanım bileşeni değiştirme](storsimple-hardware-component-replacement.md).
* Tooexperience aygıt sorunları devam ederse [Microsoft Support başvurun](storsimple-contact-microsoft-support.md).

