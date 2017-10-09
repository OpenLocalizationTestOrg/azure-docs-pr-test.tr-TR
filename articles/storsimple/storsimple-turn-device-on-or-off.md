---
title: "aaaTurn açmak veya kapatmak StorSimple 8000 serisi Cihazınızı | Microsoft Docs"
description: "Nasıl yeni bir StorSimple cihazda tooturn kapatıldı veya güç kesintisi bir cihazda kapatın ve çalışan bir aygıtı devre dışı açıklanmaktadır."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 8e9c6e6c-965c-4a81-81bd-e1c523a14c82
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/29/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 85434bde9377e330cd6ba4797fd5fd68bcee944d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="turn-on-or-turn-off-your-storsimple-8000-series-device"></a>Açma veya StorSimple 8000 serisi aygıtınızı kapatın
## <a name="overview"></a>Genel Bakış
Bir Microsoft Azure StorSimple cihazı kapatmak normal sistem işleminin bir parçası olarak gerekli değildir. Ancak, yeni bir cihaz veya kapatma toobe sahip olan bir aygıtta tooturn gerekebilir. Genellikle, bir kapanma içinde gerekir başarısız donanımı değiştirmeniz, fiziksel olarak bir birimi taşıdığınızda veya bir aygıt hizmet dışına ele durumlarda gereklidir. Bu öğreticide gerekli hello yordamı açma ve StorSimple Cihazınızı farklı senaryolarında kapatma açıklamaktadır.

## <a name="turn-on-a-new-device"></a>Yeni bir aygıtı açın
Merhaba StorSimple cihazı hello için ilk kez kapatma adımları hello aygıtın bir 8100 olup veya 8600 model bağlı olarak farklılık gösterir. Merhaba 8600 birincil muhafaza ve EBOD muhafazası çift muhafaza aygıtla iken hello 8100 tek bir birincil muhafazada sahiptir. Merhaba ayrıntılı adımlar her iki modeli için aşağıdaki bölümlerde hello anlatılacaktır.

* [Yalnızca birincil kasası ile yeni cihaz](#new-device-with-primary-enclosure-only)
* [Yeni cihaz EBOD muhafazası ile](#new-device-with-ebod-enclosure)

### <a name="new-device-with-primary-enclosure-only"></a>Yalnızca birincil kasası ile yeni cihaz
Merhaba StorSimple 8100 model tek muhafaza aygıttır. Cihazınızı yedek güç ve soğutma modüllerini (PCMs) içerir. Hem PCMs yüklenmelidir ve toodifferent güç kaynakları tooensure yüksek kullanılabilirlik bağlı.

Aşağıdaki adımları toocable hello cihazınız için güç gerçekleştirin.

[!INCLUDE [storsimple-cable-8100-for-power](../../includes/storsimple-cable-8100-for-power.md)]

> [!NOTE]
> Tam cihaz kurulumu ve yönergeleri kablo için çok Git[StorSimple 8100 cihazınız yüklemek](storsimple-8100-hardware-installation.md). Tam olarak hello yönergeleri izlediğinizden emin olun.
> 
> 

### <a name="new-device-with-ebod-enclosure"></a>Yeni cihaz EBOD muhafazası ile
Merhaba StorSimple 8600 model birincil muhafaza ve EBOD muhafazası sahiptir. Bu seri bağlı SCSI (SAS) bağlantısı ve güç için birlikte kablolu hello birimleri toobe gerektirir.

Bu cihaz hello için ilk kez ayarlarken, SAS ilk kablo ve ardından tam hello adımları güç kablo için hello adımları gerçekleştirin.

[!INCLUDE [storsimple-sas-cable-8600](../../includes/storsimple-sas-cable-8600.md)]

[!INCLUDE [storsimple-cable-8600-for-power](../../includes/storsimple-cable-8600-for-power.md)]

> [!NOTE]
> Tam cihaz kurulumu ve yönergeleri kablo için çok Git[StorSimple 8600 model Cihazınızı yüklemek](storsimple-8600-hardware-installation.md). Tam olarak hello yönergeleri izlediğinizden emin olun.

## <a name="turn-on-a-device-after-shutdown"></a>Bir aygıtı kapatıldıktan sonra açın
Bunu kapatıldı sonra için StorSimple cihazında kapatma hello hello aygıtın bir 8100 olup veya 8600 model bağlı olarak farklı adımlardır. Merhaba 8600 birincil muhafaza ve EBOD muhafazası çift muhafaza aygıtla iken hello 8100 tek bir birincil muhafazada sahiptir.

* [Yalnızca birincil muhafaza aygıtla](#device-with-primary-enclosure-only)
* [Cihaz EBOD muhafazası ile](#device-with-ebod-enclosure)

### <a name="device-with-primary-enclosure-only"></a>Yalnızca birincil muhafaza aygıtla
Bir kapanma sonra birincil muhafaza ve EBOD muhafazası bir StorSimple cihazına yordamı tooturn aşağıdaki hello kullanın.

#### <a name="tooturn-on-a-device-with-a-primary-enclosure-only"></a>yalnızca birincil kasası ile bir cihazda tooturn
1. Her iki gücüyle Hello güç geçer ve soğutma modülleri (PCMs) hello OFF konumunda olduğundan emin olun. Hello anahtarları hello OFF konumda değilse, sonra bunları toohello OFF konumu ve hello ışık toogo bekle kapalı döndür.
2. Her iki PCMs toohello ON konumuna hello güç anahtarları döndürerek Hello aygıtı açın. Merhaba aygıt etkinleştirmeniz gerekir.
3. Cihaz hello tooverify aşağıdaki onay hello tam olarak açıktır:
   
   1. Her iki PCM modülleri üzerinde Hello Tamam LED'leri yeşil.
   2. Itanium tabanlı sistemler için Hello durumu LED'leri hem denetleyicilerinde Düz yeşil hazırdır.
   3. Bu hello denetleyicisi etkindir gösteren mavi LED hello denetleyicilerinden biri üzerinde yanıp sönen, hello.
      
      Bu koşulların herhangi biri karşılanmazsa, Cihazınızı sağlıklı değil. Lütfen [Microsoft Support başvurun](storsimple-8000-contact-microsoft-support.md).

### <a name="device-with-ebod-enclosure"></a>Cihaz EBOD muhafazası ile
Bir kapanma sonra birincil muhafaza ve EBOD muhafazası bir StorSimple cihazına yordamı tooturn aşağıdaki hello kullanın. Her adım sırayla açıklandığı gibi tam olarak gerçekleştirir. Hata toodo, bu nedenle veri kaybına neden olabilir.

#### <a name="tooturn-on-a-device-with-a-primary-and-an-ebod-enclosure"></a>birincil ve EBOD muhafazası olan bir aygıtta tooturn
1. Bu hello EBOD muhafazası bağlı toohello birincil muhafaza olduğundan emin olun. Daha fazla bilgi için bkz: [StorSimple 8600 model Cihazınızı yüklemek](storsimple-8600-hardware-installation.md).
2. Bu hello güç ve soğutma modülleri (PCMs) hem EBOD hello ve olduğundan emin olun birincil kasaları hello OFF konumu. Hello anahtarları hello OFF konumda değilse, sonra bunları toohello OFF konumu ve hello ışık toogo bekle kapalı döndür.
3. EBOD muhafazası Hello üzerinde hem PCMs toohello ON konumuna hello güç anahtarları döndürerek önce etkinleştirin. Merhaba PCM LED'leri yeşil olması gerekir. Bu birimi bir yeşil EBOD denetleyicisi LED hello EBOD muhafazası üzerinde olduğunu gösterir.
4. Her iki PCMs toohello ON konumuna hello güç anahtarları döndürerek Hello birincil muhafaza açın. Merhaba tüm sistem artık üzerinde olması gerekir.
5. Merhaba SAS LED'leri yeşil hello EBOD muhafazası arasındaki bu hello bağlantı da sağlar ve hello birincil muhafaza iyi olduğunu doğrulayın.

## <a name="turn-on-a-device-after-a-power-loss"></a>Bir aygıtı sonra güç kaybı açın
Bir güç kesintisi ya da kesinti bir StorSimple cihazı kapatmanız yeterlidir. Merhaba güç kesintisi hello güç kaynakları birini veya her iki güç kaynakları gerçekleşebilir. Merhaba kurtarma adımları hello aygıtın bir 8100 olup veya 8600 model bağlı olarak farklılık gösterir. Merhaba 8600 birincil muhafaza ve EBOD muhafazası çift muhafaza aygıtla iken hello 8100 tek bir birincil muhafazada sahiptir. Bu bölümde, her senaryo için hello kurtarma yordamı açıklanmaktadır.

* [Yalnızca birincil muhafaza aygıtla](#8100)
* [Cihaz EBOD muhafazası ile](#8600)

### <a name="device-with-primary-enclosure-only-a-name8100"></a>Yalnızca birincil muhafaza aygıtla<a name="8100">
kendi güç kaynakları, güç kaybı tooone ise hello sistem normal işlem devam edebilirsiniz. Ancak, tooensure yüksek kullanılabilirlik hello aygıtının, geri yükleme güç toohello güç kaynağı mümkün olan en kısa sürede.

Merhaba sistem bir güç kesintisi veya her iki güç kaynakları üzerinde güç kesintisi ise düzenli ve denetimli bir şekilde kapanır. Merhaba güç geri yüklendiğinde hello sistem otomatik olarak aç.

### <a name="device-with-ebod-enclosure-a-name8600"></a>Cihaz EBOD muhafazası ile<a name="8600">
#### <a name="power-loss-on-one-power-supply"></a>Güç kaybı bir güç kaynağı
Merhaba birincil muhafaza veya hello EBOD muhafazası, güç kaynakları, güç kaybı tooone ise hello sistem normal işlem devam edebilirsiniz. Ancak, tooensure yüksek kullanılabilirlik hello aygıtının, lütfen geri güç toohello güç kaynağı mümkün olan en kısa sürede.

#### <a name="power-loss-on-both-power-supplies-on-primary-and-ebod-enclosures"></a>Birincil ve EBOD kutularının hem güç kaynakları güç kaybı
Bir güç kesintisi veya güç kesintisi hem güç kaynakları üzerinde ise hello EBOD muhafazası hemen kapanacak ve hello birincil muhafaza düzenli ve denetimli bir şekilde kapanacak. Güç geri yüklendiğinde hello Gereci otomatik olarak başlatılacak.

Merhaba güç el ile kapalı verirseniz, aşağıdaki adımları toorestore güç toohello sistem hello gerçekleştirin.

1. EBOD muhafazası Hello üzerinde etkinleştirin.
2. Merhaba EBOD muhafazası açıktır sonra hello birincil muhafaza açın.

### <a name="power-loss-on-both-power-supplies-on-ebod-enclosure"></a>Her iki güç kaynakları EBOD muhafazası üzerinde güç kaybı
, Kablolar ayarladığınızda, EBOD olan hiçbir zaman bu hello bağlı tek başına tooa emin olmalısınız PDU ayırın. Merhaba EBOD ve birincil muhafaza hello sırasında başarısız olursa hello sistem aynı anda kurtarır.

Yalnızca her iki güç kaynakları Hello EBOD muhafazası başarısız hello sistem otomatik olarak kurtarılacak değil. Hello sistemde adımları tooturn aşağıdaki hello ele ve tooa sağlıklı duruma geri yükleyebilirsiniz:

1. Merhaba birincil muhafaza açıksa, güç ve soğutma modülleri (PCMs) kapalı geçin.
2. Merhaba sistem tooshut için bir kaç dakika bekleyin.
3. EBOD muhafazası Hello üzerinde etkinleştirin.
4. Merhaba EBOD muhafazası açıktır sonra hello birincil muhafaza açın.

## <a name="turn-on-a-device-after-hello-primary-and-ebod-enclosure-connection-is-lost"></a>Bir aygıtı hello sonra birincil açın ve EBOD muhafazası bağlantı kaybolur
Merhaba bekleme denetleyicisi ile Merhaba karşılık gelen EBOD denetleyici arasında Hello bağlantısı kaybolursa hello aygıt toowork devam eder. Merhaba sistem etkin denetleyici ve hello karşılık gelen EBOD denetleyici arasında Hello bağlantısı kaybolursa, yük devretme gerçekleşeceğini ve hello aygıt toowork normal olarak devam etmelidir.

Merhaba EBOD muhafazası hello birincil muhafaza arasında hello bağlantı zarar görmesi veya hem seri bağlı SCSI (SAS) kabloları kaldırılır, hello aygıt çalışmayı durdurur. Bu noktada, hello aşağıdaki adımları gerçekleştirin.

### <a name="tooturn-on-hello-device-after-connection-is-lost"></a>bağlantı kaybedildikten sonra hello aygıtta tooturn
1. Erişim hello hello cihazı arkasına.
2. Merhaba hello EBOD muhafazası hello birincil muhafaza arasında SAS kablosu bağlantısı kesildiğinde, tüm SAS lane LED'leri hello EBOD muhafazası üzerinde devre dışı olacaktır.
3. Güç ve soğutma modülleri (PCMs) aşağı hello EBOD Muhafazası ve hello birincil muhafaza kapatın.
4. Her iki hello kasaları arkasına hello üzerindeki tüm hello ışık kapatmak kadar bekleyin.
5. Merhaba SAS kabloları takın ve hello EBOD muhafazası hello birincil muhafaza arasında iyi bir bağlantı olduğundan emin olun.
6. EBOD muhafazası Hello üzerinde hem PCM anahtarları toohello ON konumu döndürerek önce etkinleştirin.
7. Merhaba EBOD muhafazası üzerinde hello yeşil ışığı açık olduğunu denetleyerek olduğundan emin olun.
8. Merhaba birincil muhafaza açın.
9. Merhaba birincil kasası üzerinde hello denetleyicisi yeşil ışığı açık olduğunu denetleyerek olduğundan emin olun.
10. Bu hello EBOD muhafazası hello birincil muhafaza bağlantıyla bu hello SAS lane LED'leri (dört EBOD denetleyici başına) denetleyerek üzerinde tümü iyi olduğunu doğrulayın.

> [!IMPORTANT]
> Merhaba SAS kabloları bozuk ya da hello sistemde etkinleştirdiğinizde hello EBOD muhafazası hello birincil muhafaza arasında hello bağlantısı iyi olmayan kurtarma moduna geçer. Lütfen [Microsoft Support başvurun](storsimple-8000-contact-microsoft-support.md) böyle bir durumda.


## <a name="turn-off-a-running-device"></a>Çalışan bir aygıtı kapatın
Çalışan StorSimple cihazını toobe gerekebilir hizmet dışı gerçekleştirilecek taşındığı veya değiştirilen toobe gereken düzgün çalışmayan bir bileşen olup olmadığını kapatıldı. Merhaba adımları hello StorSimple cihazı bir 8100 olup veya 8600 model bağlı olarak farklılık gösterir. Merhaba 8600 birincil muhafaza ve EBOD muhafazası çift muhafaza aygıtla iken hello 8100 tek bir birincil muhafazada sahiptir. Bu bölümde hello adımları tooshut çalışan aygıt aşağı ayrıntılarını verir.

* [Birincil muhafaza aygıtla](#8100a)
* [Cihaz EBOD muhafazası ile](#8600a)

### <a name="device-with-primary-enclosure-a-name8100a"></a>Birincil muhafaza aygıtla<a name="8100a">
tooshut düzenli ve denetimli bir şekilde hello aygıtı aşağı hello Klasik Azure portalı veya hello Windows PowerShell aracılığıyla StorSimple için bunu yapabilirsiniz. 

> [!IMPORTANT]
> Bir çalışan aygıtı hello cihaz arkasına hello hello güç düğmesini kullanarak kapatmayı değil.
> 
> Merhaba cihazı kapatmadan önce tüm hello aygıt bileşenlerinin sağlıklı olduğundan emin olun. Buna Klasik Azure portalı Merhaba, çok gidin**aygıtları** > **Bakım** > **donanım durum**ve tüm hello durumu doğrulayın bileşenleri yeşil olur. Bu, yalnızca sağlıklı bir sistem için geçerlidir. Merhaba sistemi ise olma kapatmanız tooreplace düzgün çalışmayan bir bileşeni, başarısız (kırmızı) görür veya hello ilgili hello bileşeninde (sarı) durumunun düşürülmüş **donanım durum**.
> 
> 

StorSimple veya hello Klasik Azure portalı için Windows PowerShell hello eriştikten sonra hello adımları [bir StorSimple cihazı kapatmanız](storsimple-manage-device-controller.md#shut-down-a-storsimple-device). 

### <a name="device-with-ebod-enclosure-a-name8600a"></a>Cihaz EBOD muhafazası ile<a name="8600a">
> [!IMPORTANT]
> Merhaba birincil muhafaza ve hello EBOD muhafazası aşağı kapatmadan önce tüm hello aygıt bileşenlerinin sağlıklı olduğundan emin olun. İçinde Azure portal Merhaba, çok gidin**aygıtları** > **İzleyici** > **donanım sistem durumu**, tüm hello bileşenleri sağlıklı olduğunu doğrulayın.


#### <a name="tooshut-down-a-running-device-with-ebod-enclosure"></a>EBOD muhafazası çalışan bir aygıtla aşağı tooshut
1. Tüm hello adımları listelenen [bir StorSimple cihazı kapatmanız](storsimple-8000-manage-device-controller.md#shut-down-a-storsimple-device) hello birincil kasası için.
2. Merhaba sonra birincil muhafaza güç ve soğutma Modülü (PCM) anahtarları döndürerek EBOD hello Kapat kapalı olduğundan.
3. EBOD hello tooverify kapatıldı, tüm ışık olduğunu hello EBOD muhafazası arkasına hello üzerinde denetimi devre dışı.

> [!NOTE]
> Merhaba sistemi kapatıldığında sonra kullanılan tooconnect hello EBOD muhafazası toohello birincil muhafaza olan hello SAS kabloları kadar kaldırılmaması gerekir.

## <a name="next-steps"></a>Sonraki adımlar
[Microsoft Support başvurun](storsimple-8000-contact-microsoft-support.md) açma veya bir StorSimple cihazı kapatmak sorunlarla karşılaşırsanız.

