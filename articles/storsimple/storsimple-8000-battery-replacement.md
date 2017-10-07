---
title: "Microsoft Azure StorSimple 8000 serisi aygıt aaaReplace pilde | Microsoft Docs"
description: "Nasıl tooremove, değiştirin ve StorSimple Cihazınızı hello yedek pil modülünü bakımını açıklar."
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
ms.openlocfilehash: 5ac767807e6c3fd817d8d522629db2aceaac9bdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="replace-hello-backup-battery-module-on-your-storsimple-device"></a>StorSimple Cihazınızda Hello yedek pil modülü değiştirin

## <a name="overview"></a>Genel Bakış
Merhaba birincil muhafaza güç ve soğutma Modülü (PCM), Microsoft Azure StorSimple Cihazınızda bir ek pil paketi vardır. Bu paketi güç sunar, böylece AC güç toohello birincil muhafaza kaybı ise hello StorSimple Cihazınızı veri kaydedebilirsiniz. Başvurulan tooas hello bu pil paketidir *yedek pil Modülü*. Merhaba yedek pil modülü var. yalnızca StorSimple Cihazınızı birincil muhafazada hello için (Merhaba EBOD muhafazası bir yedek pil modül içermiyor).

Bu öğretici açıklar nasıl yapılır:

* Merhaba yedek pil modülünü Kaldır
* Yeni bir yedek pil modülünü yükleme
* Merhaba yedek pil modülü koru

> [!IMPORTANT]
> Kaldırma ve bir yedek pil modül değiştirme gözden önce hello hello güvenlik bilgileri [giriş tooStorSimple donanım bileşeni değiştirme](storsimple-8000-hardware-component-replacement.md).


## <a name="remove-hello-backup-battery-module"></a>Merhaba yedek pil modülünü Kaldır
Merhaba yedek pil StorSimple cihazınız için bir alan değiştirebilen birim modülüdür. Merhaba PCM yüklenmeden önce hello pil modülü kendi özgün paketleme depolanması gerekir. Aşağıdaki adımları tooremove hello yedek pil hello gerçekleştirin.

#### <a name="tooremove-hello-backup-battery-module"></a>tooremove hello yedek pil Modülü
1. Hello Azure portal, tooyour StorSimple cihaz Yöneticisi hizmeti dikey penceresine gidin. Çok Git**aygıtları** ve cihazların Merhaba listeden Cihazınızı seçin. Çok gidin**İzleyici** > **donanım durumu**. Altında **paylaşılan bileşenleri**, hello pil hello durum öğesine bakın.
2. Hangi hello pil başarısız oldu hello PCM tanımlayın. Şekil 1'hello StorSimple cihazı arkasına hello gösterir.
   
    ![Aygıt birincil muhafaza modüllerinin devre kartı](./media/storsimple-battery-replacement/IC740994.png)
   
    **Şekil 1** PCM ve denetleyici modülleri gösteren birincil cihaz arkasına
   
   | Etiket | Açıklama |
   |:--- |:--- |
   | 1 |PCM 0 |
   | 2 |PCM 1 |
   | 3 |Denetleyici 0 |
   | 4 |Denetleyici 1 |
   
    Gösterge izleme hello numarası 3 hello Şekil 2'de gösterildiği gibi çok karşılık gelen PCM üzerinde 0 neden**pil hataya** aydınlatma.
   
    ![Cihaz PCM izleme gösterge LED'lerinin devre kartı](./media/storsimple-battery-replacement/IC740992.png)
   
    **Şekil 2** geri of PCM gösteren hello gösterge LED'lerinin izleme
   
   | Etiket | Açıklama |
   |:--- |:--- |
   | 1 |AC güç kesintisi |
   | 2 |Fan hatası |
   | 3 |Pil hatası |
   | 4 |PCM TAMAM |
   | 5 |DC Güç kesintisi |
   | 6 |Sağlıklı pil |
3. başarısız bir pil ile tooremove hello PCM izleyin hello adımlarda [bir PCM kaldırmak](storsimple-power-cooling-module-replacement.md#remove-a-pcm).
4. Hello PCM kaldırıldı, yükseltme ve döndürme hello pil modülü yukarı hello aşağıdaki şekilde gösterildiği gibi işler ve tooremove hello pil çeker.
   
    ![PCM'den pil çıkarılıyor](./media/storsimple-battery-replacement/IC741019.png)
   
    **Şekil 3** hello pil hello PCM ' kaldırma
5. Merhaba modülü paketleme hello değiştirilebilen birimine yerleştirin.
6. Uygun Bakım ve işleme için hello arızalı ünite tooMicrosoft döndürür.

## <a name="install-a-new-backup-battery-module"></a>Yeni bir yedek pil modülünü yükleme
Aşağıdaki adımları tooinstall hello değiştirme pil modülünde hello PCM StorSimple cihazınızın hello birincil muhafazada hello gerçekleştirin.

#### <a name="tooinstall-hello-battery-module"></a>tooinstall hello pil Modülü
1. Merhaba yedek pil modülü hello uygun hello PCM yönde yerleştirin.
2. Merhaba pil modülü aşağı tuşuna tüm hello yolu tooseat hello bağlayıcı işleyin.
3. Değiştir hello yönergeleri izleyerek hello birincil muhafazada PCM hello [güç ve soğutma modülü StorSimple Cihazınızda Değiştir](storsimple-power-cooling-module-replacement.md).
4. Merhaba değiştirme tamamlandıktan sonra Git tooyour cihaz ve çok Git**İzleyici** > **donanım durumu** hello Azure portal'ın. Merhaba pil toomake hello yüklemenin başarılı olduğunu emin Hello durumunu doğrulayın. Yeşil durum hello pil sağlıklı olduğunu gösterir.

## <a name="maintain-hello-backup-battery-module"></a>Merhaba yedek pil modülü koru
StorSimple Cihazınızı hello yedek pil modülü güç kaybı olayı sırasında güç toohello denetleyicisi sunar. Merhaba StorSimple cihaz toosave kritik verilerin önceki tooshutting aşağı denetimli bir biçimde izin verir. Merhaba PCMs içinde iki tam dolu pil ile Merhaba sistem iki ardışık kaybı olayları işleyebilir.

Hello Azure portal, hello **donanım durumu** hello altında **İzleyici** dikey penceresinde hello pil arızalı ya da hello son yaşam yaklaşan gösterir. Merhaba pil durumu tarafından belirtilir **PCM 0 pil** veya **pil PCM 1** altında **paylaşılan bileşenleri**. Bu dikey gösterecek bir **DEGRADED** ömrü sonu yaklaşan için durum ve **başarısız** ömrü son ulaştı.

> [!NOTE]
> Merhaba pil raporlama yapabilir **başarısız** , yalnızca gerektiği zaman toobe ücretlendirilir.


Merhaba, **DEGRADED** durumu görünür, aşağıdaki eylemin hello öneririz:

* Merhaba sistem son güç kaybı karşılaşmış veya hello piller düzenli bakım altında. Devam etmeden önce 12 saat Hello sistem gözlemleyin.
  
  * Merhaba durum hala ise **DEGRADED** denetleyicileri ve PCMs çalıştıran, sürekli bağlantı tooAC güç hello ile 12 saat sonra hello sonra değiştirilen toobe pil gerekir. Lütfen [Microsoft Support başvurun](storsimple-8000-contact-microsoft-support.md) yedek yedek pil modülü için.
  * Merhaba durumu Tamam 12 saat sonra olursa, hello pil işlevseldir ve yalnızca bir bakım ücret gereklidir.
* Değil yapıldıysa ilişkili kaybına AC gücü ve hello PCM açık olduğundan ve tooAC güç bağlı, hello pil yerini toobe gerekir. [Microsoft Support başvurun](storsimple-8000-contact-microsoft-support.md) tooorder bir yedek yedek pil modül.

> [!IMPORTANT]
> Merhaba Dispose toonational ve bölgesel düzenlemelere göre pil başarısız oldu.

## <a name="next-steps"></a>Sonraki adımlar
Daha fazla bilgi edinmek [StorSimple donanım bileşeni değiştirme](storsimple-8000-hardware-component-replacement.md).

