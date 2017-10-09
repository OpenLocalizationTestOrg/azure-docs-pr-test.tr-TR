---
title: "Microsoft Azure StorSimple 8100 aaaInstall aygıt | Microsoft Docs"
description: "Nasıl toounpack, rafa monte etme ve dağıtma ve hello yazılım yapılandırmadan önce StorSimple 8100 cihazınız kablo açıklar."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 6098a01e-c031-488a-a8d7-0b607ce665e1
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 76b94e57318b6c25dc3333ae73edc9e4752b7d1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="unpack-rack-mount-and-cable-your-storsimple-8100-device"></a>Kutusundan çıkarma, rafa monte ve StorSimple 8100 cihazınızın kablolarını bağlama
## <a name="overview"></a>Genel Bakış
Microsoft Azure StorSimple 8100 tek kasası, rafa monte edilen aygıt olur. Bu öğretici, yapılandırmak ve hello StorSimple Cihazınızı dağıtma önce toounpack, rafa monte ve kablo StorSimple 8100 aygıt donanım nasıl hello açıklanmaktadır.

## <a name="unpack-your-storsimple-8100-device"></a>StorSimple 8100 model Cihazınızı kutusundan çıkarma
Merhaba aşağıdaki adımları temizleyin, hakkında ayrıntılı yönergeler sağlamak toounpack StorSimple 8100 depolama cihazı. Bu cihazı tek bir kutusunda geliyordu.

### <a name="prepare-toounpack-your-device"></a>Cihazınızı toounpack hazırlama
Cihazınızı paketinden çıkarma önce aşağıdaki bilgilerle hello gözden geçirin.

![Uyarı simgesi](./media/storsimple-safety/IC740879.png)![büyük ağırlık simgesi](./media/storsimple-8100-hardware-installation/HCS_HeavyWeight_Icon.png) **uyarı!**

1. El ile işleme, iki kişiler kullanılabilir toomanage hello ağırlığını hello muhafaza sahip olduğunuzdan emin olun. Tam olarak yapılandırılmış bir kasa too32 kg (70 lb.) tartmanız.
2. Merhaba kutuya bir düz, düzey yüzeyine koyun.

Ardından, aşağıdaki adımları toounpack hello Cihazınızı tamamlayın.

#### <a name="toounpack-your-device"></a>toounpack Cihazınızı
1. Merhaba kutusu ve hello paketleme köpük zemine crushes, keser, su hasar ya da belirgin herhangi bir zarar için inceleyin. Merhaba kutusu veya paketleme sisteminize ciddi zarar görmüş hello kutusunu açmayın. Lütfen [Microsoft Support başvurun](storsimple-contact-microsoft-support.md) toohelp hello aygıt iyi çalışma sırayla olup olmadığını değerlendirin.
2. Merhaba kutusunu ayıklayın. Görüntü aşağıdaki hello StorSimple Cihazınızı açılmış hello görünümünü gösterir.
   
     ![Depolama Cihazınızı paketinden çıkarma](./media/storsimple-8100-hardware-installation/HCSUnpackyour2Udevice.png)
   
    **Depolama Cihazınızı paketten görünümü**
   
   | Etiket | Açıklama |
   | --- | --- |
   |   1 |Paketleme kutusu |
   |   2 |Alt köpük zemine |
   |   3 |Cihaz |
   |   4 |Üst köpük zemine |
   |   5 |Aksesuar kutusu |
3. Merhaba kutusunu paketi açılırken sonra sahip olduğunuzdan emin olun:
   
   * 1 tek muhafaza cihaz
   * 2 güç kablosu
   * 1 çapraz Ethernet kablosu
   * 2 seri konsol kabloları
   * seri erişim için 1 seri USB dönüştürücü
   * 1 yetkisiz değiştirmeye karşı kanıt T10 tornavida
   * 4 QSFP-için-SFP + bağdaştırıcılar 10 GbE ağ arabirimleri ile kullanmak için
   * 1 raf-Seti (donanım bağlama ile 2 yan rayları) bağlama
   * Alma başlatıldı belgeleri
     
     Yukarıda listelenen hello öğelerden herhangi birini almadı varsa [Microsoft Support başvurun](storsimple-contact-microsoft-support.md).

Merhaba sonraki adıma toorack bağlama, aygıttır.

## <a name="rack-mount-your-storsimple-8100-device"></a>Rafa monte StorSimple 8100 cihazınız
Merhaba sonraki adımları tooinstall StorSimple 8100 depolama cihazınız bir standart 19 inç dolapta ön ve arka gönderileri izleyin. Merhaba StorSimple 8100 cihazı tek bir birincil muhafazada var.

birden çok adımı, her biri aşağıdaki yordamlarını hello açıklanan Hello yükleme oluşur.

> [!IMPORTANT]
> StorSimple cihazları düzgün çalışması için rafa monte edilen olması gerekir.
> 
> 

### <a name="prepare-hello-site"></a>Merhaba site hazırlama
Merhaba aygıt ön ve arka gönderileri sahip standart bir 19 inç rafa yüklü olması gerekir. Raf yükleme yordamı tooprepare aşağıdaki hello kullanın.

#### <a name="tooprepare-hello-site-for-rack-installation"></a>tooprepare hello site raf yükleme için
1. Merhaba cihazın güvenli bir şekilde bir düz, kararlı ve düzey çalışmaları yüzey (veya benzeri) ye dayanıyorsa emin olun.
2. Burada tooset yukarı düşündüğünüz hello site standart AC bağımsız bir kaynaktan yetkileri veya raf güç dağıtım sahip bir birimi (PDU) bir kesintisiz güç kaynağı (UPS) doğrulayın.
3. Bu bir 2U yuvası hello rafa monte toomount hello aygıt düşündüğünüz kullanılabilir olduğundan emin olun.

![Uyarı simgesi](./media/storsimple-safety/IC740879.png)![büyük ağırlık simgesi](./media/storsimple-8100-hardware-installation/HCS_HeavyWeight_Icon.png) **uyarı!**

Merhaba aygıt ayarları el ile işleniyorsa iki kişiler kullanılabilir toomanage hello ağırlığa sahip olduğunuzdan emin olun. Tam olarak yapılandırılmış bir kasa too32 kg (70 lb.) tartmanız.

### <a name="rack-prerequisites"></a>Raf önkoşulları
Merhaba 8100 kasası ile dolap bir standart 19 inç dolapta yüklemesi için tasarlanmıştır:

* Raf 27.84 inç minimum derinliği toopost gönderin.
* En yüksek ağırlığı hello cihaz için 32 kg
* 5 Pascal (0,5 mm su ölçer) en fazla arka baskısı.

### <a name="rack-mounting-rail-kit"></a>Raf bağlama raylar Seti
Rayları takma kümesi hello 19 inç raf dolap ile kullanım için sağlanır. Merhaba rayları olmuştur test toohandle hello maksimum muhafaza ağırlığı. Bu rayları alanı hello raf içinde herhangi bir kayıp olmadan birden fazla kasaları yüklemesini de izin verir.

#### <a name="tooinstall-hello-device-on-hello-rails"></a>Merhaba rayları tooinstall hello aygıtta
1. Yalnızca iç rayları aygıtınızda yüklü değilse bu adımı gerçekleştirin. Genellikle, hello iç rayları hello fabrikada yüklenir. Rayları yüklü değilse hello raylar sol ve sağ raylar slayt toohello hello muhafaza kasa yanlarından yükleyin. Bunlar, her bir tarafta altı ölçüm Vida kullanarak ekleyin. yönlendirmeyle, slayt işaretlenir hello raylar toohelp **LH – ön** ve **RH – ön**, ve hello muhafaza hello arka yapıştırılmış hello son Konik bitiş vardır.<br/>
   
    ![Tooenclosure kasa bağlanmasını raylar slayt](./media/storsimple-8100-hardware-installation/HCSAttachingRailSlidestoEnclosureChassis.png)

    **Merhaba muhafaza toohello yanlarından bağlanmasını iç raylar slayt**
   
    Etiket | Açıklama
    ----- | -----------
    1     | M 3 x 4 düğmesi head Vida
    2     | Kasa slayt

2. Merhaba dış sol raylar ve dış sağda derlemeleri toohello raf dolap dikey üye ekleyebilir. Merhaba köşeli işaretlenir **LH**, **RH**, ve **bu tarafı yukarı** tooguide yönlendirmesini hello size düzeltin.
3. Merhaba raylar PIN'ler hello ön ve arka hello raylar derlemenin bulun. Merhaba raylar toofit hello raf gönderimleri arasında genişletmek ve hello PIN'ler hello ön ve arka raf post dikey üye delik yerleştirin. Merhaba raylar derleme düzeyi olduğundan emin olun.
4. İki sağlanan hello ölçüm Vida toosecure hello raylar derleme toohello raf dikey üyelerinin kullanın. Merhaba öne ve hello arka birinde bir Vidayı kullanın.
5. Bu adımları diğer raylar derleme hello için yineleyin.<br/>
   
     ![Düğmelere raylar slayt toorack dolap](./media/storsimple-8100-hardware-installation/HCSAttachingRailSlidestoRackCabinet.png)
   
    **Dış raylar derlemeleri toohello raf ekleme**
   
   | Etiket | Açıklama |
   | --- | --- |
   |   1 |Vidayı clamping |
   |   2 |Kare delik ön raf post Vidayı |
   |   3 |Sol raylar ön konumu PIN'ler |
   |   4 |Vidayı clamping |
   |   5 |Sol raylar arka konumu PIN'ler |

### <a name="mounting-hello-device-in-hello-rack"></a>Merhaba dolapta Hello cihaz takma
Yeni yüklenen hello raf rayları adımları toomount hello aygıt hello dolapta aşağıdaki hello gerçekleştirin.

#### <a name="toomount-hello-device"></a>toomount hello cihaz
1. Bir Yardımcısı ile Merhaba muhafaza kaldırın ve hello raf rayları ile Hizala.
2. Dikkatle hello aygıt hello rayları yerleştirin ve ardından hello aygıt tamamen hello rafa dolap itme.<br/>
   
    ![Cihaz hello rafa yerleştirme](./media/storsimple-8100-hardware-installation/HCSInsertingDeviceintheRack.png)
   
    **Merhaba dolapta Hello cihaz takma**
3. Merhaba sol ve sağ ön Flanş başlıklarını hello caps ücretsiz çekerek kaldırın. Merhaba Flanş başlıklarını yalnızca hello çıkıntıları ek.
4. Sol ve sağ her Flanş aracılığıyla sağlanan bir yıldız head Vidayı yükleyerek Hello muhafaza hello dolapta güvenli.
5. Konumda basarak ve yerinde tutturma Hello Flanş başlıklarını yükleyin.<br/>
   
     ![Flanş başlıklarını takma](./media/storsimple-8100-hardware-installation/HCSInstallingFlangeCaps.png)
   
    **Merhaba Flanş başlıklarını takma**
   
   | Etiket | Açıklama |
   | --- | --- |
   |   1 |Muhafaza birleşme Vidayı |

Merhaba sonraki adım, cihaz güç, ağ ve seri erişim için toocable olduğunu.

## <a name="cable-your-storsimple-8100-device"></a>StorSimple 8100 cihazınızın kablolarını bağlama
Merhaba aşağıdaki yordamlar açıklamaktadır nasıl toocable StorSimple 8100 cihazınız güç, ağ ve seri bağlantılar için.

### <a name="prerequisites"></a>Ön koşullar
Merhaba Cihazınızı kablo başlamadan önce ihtiyacınız:

* Depolama aygıtı, tamamen açılmış ve raf bağladı.
* cihazınızla birlikte gelen 2 güç kabloları
* Erişim too2 güç dağıtım (önerilen) birimleri.
* Ağ kabloları
* Seri kablolar sağlanan
* Seri USB dönüştürücü hello uygun sürücüsü (gerekirse) Bilgisayarınızda yüklü
* 4 QSFP sağlanan-için-SFP + bağdaştırıcılar 10 GbE ağ arabirimleri ile kullanmak için
* [StorSimple Cihazınızda hello 10 GbE ağ arabirimleri için desteklenen donanım](storsimple-supported-hardware-for-10-gbe-network-interfaces.md)

### <a name="power-cabling"></a>Güç kabloları
Cihazınızı yedek güç ve soğutma modüllerini (PCMs) içerir. Hem PCMs yüklenmelidir ve toodifferent güç kaynakları tooensure yüksek kullanılabilirlik bağlı.

Aşağıdaki adımları toocable hello cihazınız için güç gerçekleştirin.

[!INCLUDE [storsimple-cable-8100-for-power](../../includes/storsimple-cable-8100-for-power.md)]

### <a name="network-cabling"></a>Ağ kabloları
Cihazınızı bir etkin bekleme yapılandırmadır: belirli bir zamanda bir denetleyici modülü etkin ve tüm disk ve ağ hello sırasında işlemlerinde diğer Denetleyici Modülü bekleme. Bir denetleyici başarısız olursa, hello bekleme denetleyicisi hemen etkinleştirilir ve tüm hello disk ve ağ işlemleri devam eder.

toosupport bu yedek denetleyici yük devretmesi Cihazınızı ağ aşağıdaki adımları hello açıklandığı gibi toocable gerekir.

#### <a name="toocable-for-network-connection"></a>ağ bağlantısı için toocable
1. Cihazınızı her denetleyicisinde altı ağ arabirimi bulunur: dört 1 GB/sn, ve iki 10 GB/sn Ethernet bağlantı noktaları. Çeşitli veri noktaları Cihazınızı hello devre kartı hello tanımlayın.
   
    ![8100 aygıt devre kartı](./media/storsimple-8100-hardware-installation/HCSBackplaneof2UDevicewithPortsLabeled.jpg)
   
    **Geri hello aygıtın veri bağlantı noktalarını gösterme**
   
   | Etiket | Açıklama |
   | --- | --- |
   |   0,1,4,5 |1 GbE ağ arabirimleri |
   |   2,3 |10 GbE ağ arabirimleri |
   |   6 |Seri bağlantı noktaları |
2. Ağ kablosunun için diyagram aşağıdaki hello bakın. (Merhaba minimum ağ yapılandırması düz mavi çizgilerle gösterilir. Yüksek kullanılabilirlik ve performans için gereken ek yapılandırma noktalı çizgilerle gösterilir.)

    ![Kabloyla 2U cihazınızın ağ bağlantısını yapma](./media/storsimple-8100-hardware-installation/HCSCableYour2UDeviceforNetwork.png)

    **Cihazınız için kablo ağ**

   |Etiket | Açıklama |
   |----- | ----------- |
   | A    | Internet erişimi olan LAN |
   | B    | Denetleyici 0 |
   | C    | PCM 0 |
   | D    | Denetleyici 1 |
   | E    | PCM 1 |
   | F, G | Ana bilgisayarlar |
   | 0-5  | Ağ arabirimleri |



Merhaba aygıt kablo kullanırken hello en düşük yapılandırma gerektirir:

* En az iki ağ arabirimi her denetleyicisi bulut erişimi için diğeri için iSCSI ile bağlı. başlangıç bağlantı noktası otomatik olarak etkinleştirilmiş ve hello hello cihaz seri Konsolu yapılandırılmış veri 0. Veri 0 dışında başka bir veri bağlantı noktası da toobe hello Klasik Azure portalı yapılandırılması gerekir. Bu durumda, veri 0 bağlantı noktası toohello birincil LAN (Internet erişimi olan ağ) bağlayın. Merhaba bağlantı noktaları olabilir diğer veri tooSAN/iSCSI LAN (VLAN) segment hedeflenen hello rol bağlı olarak hello ağın bağlı.
* Bir denetleyici yük devretme gerçekleşirse aynı her bağlı denetleyicisi toohello üzerinde aynı tooensure kullanılabilirlik ağ arabirimleri. Örneğin, tooconnect veri 0'ı seçin ve veri 3 hello denetleyicilerinden biri için veri 0 ve veri 3 üzerinde karşılık gelen tooconnect hello ihtiyacınız varsa diğer denetleyicisi hello.

Yüksek kullanılabilirlik ve performans için göz önünde bulundurun:

* Mümkün olduğunda, bir çift ağ arabiriminin bulut erişim (1 GbE) ve iSCSI (10 GbE önerilen) için başka bir çifti her denetleyicisinde yapılandırın.
* Mümkün olduğunda, ağ arabirimlerinin her denetleyici tootwo farklı anahtarlara tooensure kullanılabilirlik anahtar arızasına karşı bağlanması. Merhaba şekilde hello iki 10 GbE ağ arabirimleri, veri 2 ve veri 3, her bağlı denetleyicisi tootwo farklı anahtarlarından gösterilmektedir.

Daha fazla bilgi için toohello başvuran **ağ arabirimleri** hello altında [StorSimple cihazınız için yüksek kullanılabilirlik gereksinimlerini](storsimple-system-requirements.md#high-availability-requirements-for-storsimple).

> [!NOTE]
> 10 GbE Ağ arabirimleriyle SFP + vericilerinin kullanıyorsanız, kullanım hello QSFP sağlanan-SFP + bağdaştırıcıları. Daha fazla bilgi için çok Git[hello 10 GbE ağ arabirimleri, StorSimple Cihazınızda için desteklenen donanım](storsimple-supported-hardware-for-10-gbe-network-interfaces.md).
> 
> 

### <a name="serial-port-cabling"></a>Seri bağlantı kabloları
Aşağıdaki adımları toocable hello seri bağlantı noktanızın gerçekleştirin.

#### <a name="toocable-for-serial-connection"></a>seri bağlantı için toocable
1. Cihazınızı bir İngiliz anahtarı simgesi tarafından tanımlanan her denetleyicisinde seri bağlantı noktası var. Merhaba toohello çizimde başvuran [ağ kablo](#network-cabling) bölümünde toolocate hello seri bağlantı noktalarına Cihazınızı hello devre kartı.
2. Merhaba, aygıt devre kartı etkin denetleyicisinde tanımlayın. Yanıp sönen bir mavi LED bu hello denetleyicisi etkin olduğunu gösterir.
3. (Gerekirse, dizüstü bilgisayarınız için hello USB seri dönüştürücü) sağlanan hello seri kablolar ve konsol veya bilgisayar (terminal öykünme toohello aygıtla) bağlayın toohello hello etkin denetleyicisinin seri bağlantı noktası.
4. Merhaba seri USB sürücüleri (Merhaba aygıtla birlikte gelen) bilgisayarınıza yükleyin.
5. Merhaba seri bağlantı kurma aşağıdaki gibi ayarlayın: 115.200 baud, 8 veri bitleri, 1 dur biti, eşlik yok ve akış denetimi tooNone ayarlayın.
6. Merhaba bağlantı hello konsolunda Enter tuşuna basarak çalışmakta olduğunu doğrulayın. Seri konsol menüsünde görüntülenmelidir.

> [!NOTE]
> **Uzaktan Yönetim**: hello aygıt bir uzak veri merkezinde veya sınırlı erişimi olan bir bilgisayar odada yüklendiğinde hello seri bağlantılar tooboth denetleyicileri her zaman bağlı tooa seri konsol anahtar veya benzer ekipman olduğundan emin olun. Ağ kesintilerine veya beklenmeyen arıza varsa bu bant dışı uzaktan denetim ve Destek işlemler sağlar.
> 
> 

Cihazınız artık güç, ağ erişimi ve seri bağlantı kablolu. Merhaba sonraki adıma tooconfigure hello yazılımdır ve Cihazınızı dağıtın.

## <a name="next-steps"></a>Sonraki adımlar
Nasıl çok öğrenin[şirket içi StorSimple Cihazınızı yapılandırmak ve dağıtmak](storsimple-deployment-walkthrough-u2.md).

