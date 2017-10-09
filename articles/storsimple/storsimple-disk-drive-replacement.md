---
title: "StorSimple cihazı disk sürücüsünde aaaReplace | Microsoft Docs"
description: "Nasıl tooreplace bir disk sürücüsü bir StorSimple birincil muhafaza veya EBOD muhafazası açıklanmaktadır."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 98890d36-b613-40fd-994e-330dd907a8a1
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: d2c78a6d951b0f00ac42e74a34cf1bc83952a3c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="replace-a-disk-drive-on-your-storsimple-device"></a>StorSimple Cihazınızı disk sürücüsünde değiştirin
## <a name="overview"></a>Genel Bakış
Bu öğretici nasıl kaldırın ve bir hatalı çalışan veya başarısız sabit disk sürücüsünde bir Microsoft Azure StorSimple cihaz Değiştir açıklanmaktadır. tooreplace bir disk sürücüsü, şunları yapmanız gerekir:

* Merhaba antitamper kilit disengage
* Merhaba disk sürücüsünü Kaldır
* Merhaba değiştirme disk sürücüsü yükleyin

> [!IMPORTANT]
> Bir disk sürücüsü değiştirme ve kaldırma gözden önce hello güvenlik bilgileri [StorSimple donanım bileşeni değiştirme](storsimple-hardware-component-replacement.md).
> 
> 

## <a name="disengage-hello-antitamper-lock"></a>Merhaba antitamper kilit disengage
Bu yordam nasıl hello antitamper kilitleri, StorSimple Cihazınızda hello disk sürücüleri değiştirdiğinizde boşta veya açıklar. Hello antitamper kilitleri hello sürücü taşıyıcı tanıtıcılarını donatılmıştır ve küçük açıklığı hello tanıtıcının hello Mandal bölümdeki aracılığıyla erişilir. Sürücüleri hello kilitleri kümesi kilitli toohello konumu ile sağlanır.

#### <a name="toounlock-hello-antitamper-lock"></a>toounlock hello antitamper Kilitle
1. Dikkatli bir şekilde hello tanıtıcı içinde hello açıklığı ve onun yuva hello lock tuşunun (Microsoft sağlanan bir "tamperproof" T10 tornavida) ekleyin. 
   
   > [!NOTE]
   > Merhaba antitamper kilidi etkinleştirilmişse, hello kırmızı göstergesi hello açıklığı görünür olur.
   > 
   > 
   
    ![Kilitli disk sürücüsü](./media/storsimple-disk-drive-replacement/IC741056.png)
   
    **Şekil 1** koruma yetkisiz değiştirmeye karşı kilit gerçekleştiriliyor
   
   | Etiket | Açıklama |
   |:--- |:--- |
   | 1 |Gösterge açıklığı |
   | 2 |Antitamper Kilitle |
2. Merhaba kırmızı göstergesi hello açıklığı hello anahtarı yukarıda görünür değil kadar hello anahtar anticlockwise yönde döndürün.
3. Başlangıç anahtarı kaldırın.
   
    ![Kilidi açılmış disk sürücüsü](./media/storsimple-disk-drive-replacement/IC741057.png)
   
    **Şekil 2** kilitli değil disk sürücüsü
4. Merhaba disk sürücüsü artık kaldırılabilir.

Ters tooengage hello kilit Hello adımları izleyin.

## <a name="remove-hello-disk-drive"></a>Merhaba disk sürücüsünü Kaldır
StorSimple Cihazınızı bir RAID 10 benzeri depolama alanları yapılandırmasını destekler. Bu, başarısız olan bir diski, katı hal sürücüsü (SSD) normal olarak çalışabilir veya sabit disk sürücüsü (HDD) anlamına gelir. 

> [!IMPORTANT]
> * Sisteminizde birden fazla başarısız disk varsa, birden fazla SSD veya HDD herhangi bir noktada hello sisteminden zamanında kaldırmayın. Bunun yapılması, veri kaybına neden olabilir.
> * Daha önce bir SSD bulunan bir yuvada SSD yerine koyun emin olun. Benzer şekilde, daha önce bir HDD bulunan bir yuvada değiştirme HDD yerleştirin.
> * Hello Klasik Azure portalı, yuva 0'dan – numaralandırılır 11. Hello portal 2 yuvasındaki bir disk, hello aygıtta başarısız olduğunu gösteriyorsa bu nedenle, başarısız olan diskin hello hello üçüncü yuvasındaki hello üstten sol arayın.
> 
> 

Sürücüleri kaldırılır ve hello sistem çalışırken değiştirilir.

#### <a name="tooremove-a-drive"></a>tooremove bir sürücü
1. tooidentify hello başarısız diski yeniden, buna Klasik Azure portalı Merhaba, çok Git**aygıtları** > **Bakım** > **donanım durum**. Bir disk hello birincil muhafazada ve/veya bir EBOD muhafazası (8600 model kullanıyorsanız) içinde başarısız olabileceğinden altında hello disklerin hello durumu bakmak **paylaşılan bileşenleri** ve altında **EBOD muhafazası paylaşılan bileşenleri**. Başarısız disk ya da muhafazada kırmızı bir duruma sahip gösterilir.
2. Merhaba sürücüleri hello birincil muhafaza veya hello EBOD muhafazası hello önüne bulun. 
3. Merhaba disk kilidi ise toohello sonraki adıma geçin. Merhaba disk kilitliyse hello yordamı izleyerek kilidini [hello antitamper kilit Disengage](#disengage-the-antitamper-lock).
4. Tuşuna hello siyah hello sürücü taşıyıcı modülünü Mandal ve hello sürücü taşıyıcı tanıtıcı çekerek out ve hello kasa hello Önden çıkartın. 
   
    ![Disk sürücüsü işleyici bırakılıyor](./media/storsimple-disk-drive-replacement/IC741051.png)
   
    **Şekil 3** gönderilirler hello sürücüsü işleyici
5. Merhaba sürücü taşıyıcı tanıtıcı tam olarak genişletildiğinde hello sürücü taşıyıcı hello gövdeden kaydırın. 
   
    ![Disk sürücüsünden kayan disk](./media/storsimple-disk-drive-replacement/IC741052.png)
   
    **Şekil 4** hello disk sürücüsü hello taşıyıcı dışında kayan

## <a name="install-hello-replacement-disk-drive"></a>Merhaba değiştirme disk sürücüsü yükleyin
Bir sürücü StorSimple Cihazınızı başarısız oldu ve kaldırıldı sonra bu yordamı tooreplace izleyin, yeni bir sürücüye sahip.

#### <a name="tooinsert-a-drive"></a>tooinsert bir sürücü
1. Merhaba sürücü taşıyıcı tanıtıcı tam olarak genişletilmiş, hello görüntü aşağıdaki gösterildiği gibi emin olun.
   
    ![İşleyicisi genişletilmiş disk sürücüsü](./media/storsimple-disk-drive-replacement/IC741044.png)
   
    **Şekil 5** işleyicisi genişletilmiş sürücü
2. Merhaba sürücü taşıyıcı tüm hello şekilde hello kasaya kaydırın. 
   
    ![Disk sürücüsü taşıyıcı kayan diskine](./media/storsimple-disk-drive-replacement/IC741045.png)
   
    **Şekil 6** hareketli hello sürücü taşıyıcı hello kasa içine
3. Hello sürücü taşıyıcı eklenen, Kapat hello sürücü taşıyıcı tanıtıcısıyla hello sürücü taşıyıcı tanıtıcı kilitli bir konumda tutturur kadar hello kasa içine devam ediliyor toopush hello sürücü taşıyıcı oluştu.
4. Microsoft (tamperproof Torx tornavida) toosecure hello taşıyıcı tanıtıcıyla yerine hello kilit Vidayı Çeyrek Aç yönünde kapatarak sağlanan hello lock tuşunun kullanın.
5. Merhaba değiştirme başarılı oldu ve hello Klasik Azure portalına erişme ve çok gezinme hello sürücü işletimsel olduğundan emin olun**Bakım** > **donanım durum**. Altında **paylaşılan bileşenleri** veya **EBOD muhafazası paylaşılan bileşenleri**, hello sürücü durumu sağlıklı olduğunu gösteren yeşil.
   
   > [!NOTE]
   > Bunu hello disk durumu tooturn birkaç saat sonra hello değiştirme yeşil sürebilir.
   > 
   > 

## <a name="next-steps"></a>Sonraki adımlar
Daha fazla bilgi edinmek [StorSimple donanım bileşeni değiştirme](storsimple-hardware-component-replacement.md).

