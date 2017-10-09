---
title: bir StorSimple EBOD denetleyicisi aaaReplace | Microsoft Docs
description: "Açıklar nasıl tooremove ve StorSimple 8600 model Cihazınızı biri veya her ikisi EBOD denetleyicilerinde değiştirin."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 8cbfa507-1a56-4e24-99dd-7db9abd3b850
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 5d29de2ee30bfdd70910050eee5cfa1d293d444f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="replace-an-ebod-controller-on-your-storsimple-device"></a>EBOD denetleyicisi, StorSimple Cihazınızda değiştirin
## <a name="overview"></a>Genel Bakış
Bu öğretici açıklar nasıl tooreplace hatalı EBOD Denetleyici Modülü, Microsoft Azure StorSimple Cihazınızda. EBOD Denetleyici Modülü tooreplace, şunları yapmanız gerekir:

* Merhaba hatalı EBOD denetleyicisi Kaldır
* Yeni bir EBOD denetleyicisi yükleme

Başlamadan önce aşağıdaki bilgilerle hello göz önünde bulundurun:

* Boş EBOD modülleri tüm kullanılmayan yuvaları eklenmesi gerekir. bir yuva açık olarak bırakılırsa hello muhafaza düzgün seyrek erişimli değil.
* Merhaba EBOD denetleyicisi hot Swap ve yerini veya kaldırılabilir. Yenisini elde edene kadar başarısız bir modül kaldırmayın. Merhaba değiştirme işlemini başlattığınızda, 10 dakika içinde bitmesi gerekir.

> [!IMPORTANT]
> Tooremove denemeden önce veya herhangi bir StorSimple bileşeni değiştirin, hello gözden emin olun [güvenliği simgesi kuralları](storsimple-safety.md#safety-icon-conventions) ve diğer [güvenlik önlemlerini](storsimple-safety.md).
> 
> 

## <a name="remove-an-ebod-controller"></a>EBOD denetleyicisi Kaldır
EBOD denetleyicisi StorSimple Cihazınızı modülünde Hello değiştirme başarısız oldu önce o hello emin olun diğer EBOD denetleyici modülü etkin ve çalışır durumda. Merhaba aşağıdaki yordamı ve tabloyu nasıl tooremove hello EBOD Denetleyici Modülü açıklanmaktadır.

#### <a name="tooremove-an-ebod-module"></a>tooremove EBOD Modülü
1. Açık hello Klasik Azure portalı.
2. Çok gidin**aygıtları** > **Bakım** > **donanım durum**ve hello hello durumu için KILAVUZLUK doğrulayın etkin EBOD hello Denetleyici Modülü yeşil ve hello LED başarısız hello EBOD Denetleyici Modülü için kırmızı.
3. Merhaba cihaz arkasına hello adresindeki başarısız hello EBOD Denetleyici Modülü bulun.
4. Merhaba EBOD modülü hello sistem dışı çıkarmadan önce hello EBOD denetleyicisi modülü toohello denetleyicisi bağlanmak hello kabloları kaldırın.
5. Merhaba tam SAS bağlantı noktasına bağlı toohello denetleyicisi olduğundan hello EBOD Denetleyici Modülü not edin. Merhaba EBOD modülü değiştirdikten sonra gerekli toorestore hello sistem toothis yapılandırması olacaktır. 
   
   > [!NOTE]
   > Genellikle, bu olarak etiketli bağlantı noktası A olacaktır **içinde ana bilgisayar** diyagramı aşağıdaki hello içinde.
   > 
   > 
   
    ![Devre kartı olarak EBOD denetleyicisi](./media/storsimple-ebod-controller-replacement/IC741049.png)
   
     **Şekil 1** geri of EBOD Modülü
   
   | Etiket | Açıklama |
   |:--- |:--- |
   | 1 |Hata Işığı |
   | 2 |Güç ışığı |
   | 3 |SAS Bağlayıcısı |
   | 4 |SAS LED'leri |
   | 5 |Yalnızca Fabrika kullanımı için seri bağlantı noktaları |
   | 6 |(Ana), bağlantı noktası |
   | 7 |Bağlantı noktası B (ana bilgisayarı devre dışı) |
   | 8 |Bağlantı noktası C (yalnızca Fabrika kullanın) |

## <a name="install-a-new-ebod-controller"></a>Yeni bir EBOD denetleyicisi yükleme
Merhaba aşağıdaki yordamı ve tabloyu açıklayan nasıl tooinstall bir StorSimple Cihazınızı EBOD denetleyicisi modülünde.

#### <a name="tooinstall-an-ebod-controller"></a>tooinstall EBOD denetleyicisi
1. Merhaba EBOD aygıt zarar, özellikle toohello arabirimi bağlayıcı için denetleyin. Tüm PIN'ler Bükülü hello yeni EBOD denetleyicisi yüklemeyin.
2. Merhaba tutma hello içinde konumu, slayt hello hello tutma devreye kadar hello muhafaza modüle açın.
   
    ![EBOD denetleyicisi yükleniyor](./media/storsimple-ebod-controller-replacement/IC741050.png)
   
    **Şekil 2** yükleme hello EBOD Denetleyici Modülü
3. Kapat hello Mandal. Merhaba Mandal prosese gibi bir tıklama sesi.
   
    ![EBOD mandalı bırakılıyor](./media/storsimple-ebod-controller-replacement/IC741047.png)
   
    **Şekil 3** hello EBOD modülü mandalı kapatılıyor
4. Merhaba kabloları yeniden bağlanın. Merhaba değiştirme önce mevcut hello tam yapılandırmasını kullanın. Diyagram aşağıdaki hello bakın ve tablo hakkında ayrıntılar için tooconnect hello kabloları.
   
    ![Kabloyla 4U cihazınızın güç bağlantısını yapma](./media/storsimple-ebod-controller-replacement/IC770723.png)
   
    **Şekil 4**. Yeniden bağlanan kabloları
   
   | Etiket | Açıklama |
   |:--- |:--- |
   | 1 |Birincil kasası |
   | 2 |PCM 0 |
   | 3 |PCM 1 |
   | 4 |Denetleyici 0 |
   | 5 |Denetleyici 1 |
   | 6 |EBOD denetleyici 0 |
   | 7 |EBOD Denetleyici 1 |
   | 8 |EBOD muhafazası |
   | 9 |Güç Dağıtım birimleri |

## <a name="next-steps"></a>Sonraki adımlar
Daha fazla bilgi edinmek [StorSimple donanım bileşeni değiştirme](storsimple-hardware-component-replacement.md).

