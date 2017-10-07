---
title: "Microsoft Azure StorSimple 8600 aaaInstall aygıt | Microsoft Docs"
description: "Nasıl toounpack, rafa monte etme ve dağıtma ve hello yazılım yapılandırmadan önce StorSimple 8600 model Cihazınızı kablo açıklar."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 3d82ba5f-3e34-40dc-9c33-50f952bc6be8
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 10/24/2016
ms.author: alkohli
ms.openlocfilehash: 0fc0ddf076725fededdde33a260b950b72edc8db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="unpack-rack-mount-and-cable-your-storsimple-8600-device"></a>Kutusundan çıkarma, rafa monte ve StorSimple 8600 cihazınızın kablolarını bağlama
## <a name="overview"></a>Genel Bakış
Microsoft Azure StorSimple 8600 çift muhafaza cihaz ve birincil ve EBOD muhafazası oluşur. Bu öğretici hello StorSimple yazılım yapılandırmadan önce toounpack, rafa monte ve kablo StorSimple 8600 aygıt donanım nasıl hello açıklanmaktadır.

## <a name="unpack-your-storsimple-8600-device"></a>StorSimple 8600 model Cihazınızı paketinden çıkarma
Merhaba aşağıdaki adımları temizleyin, ayrıntılı yönergeler sağlamak toounpack StorSimple 8600 depolama cihazı. Bu aygıtın iki kutularında, bir hello birincil kasası için ve hello EBOD muhafazası için başka bir gönderilir. Bu iki kutu içinde tek bir kutu daha sonra yerleştirilir.

### <a name="prepare-toounpack-your-device"></a>Cihazınızı toounpack hazırlama
Cihazınızı paketinden çıkarma önce aşağıdaki bilgilerle hello gözden geçirin.

![Uyarı simgesi](./media/storsimple-safety/IC740879.png)![büyük ağırlık simgesi](./media/storsimple-8600-hardware-installation/HCS_HeavyWeight_Icon.png) **uyarı!**

1. El ile işleme, iki kişiler kullanılabilir toomanage hello ağırlığını hello cihaz olduğundan emin olun. Tam olarak yapılandırılmış bir kasa too32 kg (70 lb.) tartmanız.
2. Merhaba kutuya bir düz, düzey yüzeyine koyun.

Ardından, aşağıdaki adımları toounpack hello Cihazınızı tamamlayın.

#### <a name="toounpack-your-device"></a>toounpack Cihazınızı
1. Merhaba kutusu ve hello paketleme köpük zemine crushes, keser, su hasar ya da belirgin herhangi bir zarar için inceleyin. Merhaba kutusu veya paketleme sisteminize ciddi zarar görmüş hello kutusunu açmayın. Lütfen [Microsoft Support başvurun](storsimple-contact-microsoft-support.md) toohelp hello aygıt iyi çalışma sırayla olup olmadığını değerlendirin.
2. Merhaba dış kutusunu açın ve ardından tooprimary ve ebod karşılık gelen hello iki kutularını uygulayın. Şimdi hello birincil ve ebod da ayıklayın. Aşağıdaki şekilde hello hello kasaları birini açılmış hello görünümünü gösterir.
   
    ![Depolama Cihazınızı paketinden çıkarma](./media/storsimple-8600-hardware-installation/HCSUnpackyour4Udevice.png)
   
    **Depolama Cihazınızı paketten görünümü**
   
   | Etiket | Açıklama |
   | --- | --- |
   |   1 |Paketleme kutusu |
   |   2 |SAS kabloları (tepsisinde Donatılar ve kablolar) |
   |   3 |Alt köpük zemine |
   |   4 |Cihaz |
   |   5 |Üst köpük zemine |
   |   6 |Aksesuar kutusu |
3. Merhaba iki kutuları paketi açılırken sonra sahip olduğunuzdan emin olun:
   
   * 1 birincil kasası (Merhaba birincil muhafaza ve EBOD muhafazası olan iki ayrı kutularında)
   * 1 EBOD muhafazası
   * 4 güç kablosu, her kutusunda 2
   * 2 SAS kabloları (tooconnect hello birincil muhafaza tooEBOD muhafaza)
   * 1 çapraz Ethernet kablosu
   * 2 seri konsol kabloları
   * seri erişim için 1 seri USB dönüştürücü
   * 4 QSFP-için-SFP + bağdaştırıcılar 10 GbE ağ arabirimleri ile kullanmak için
   * 2 bağlama setleri (donanım, her 2 hello birincil muhafaza ve EBOD muhafazası bağlama ile 4 yan rayları), raf her kutusunda 1
   * Başlatılan belgeleri alma
     
     Yukarıda listelenen hello öğelerden herhangi birini almadı varsa [Microsoft Support başvurun](storsimple-contact-microsoft-support.md).  

Merhaba sonraki adıma toorack bağlama, aygıttır.

## <a name="rack-mount-your-storsimple-8600-device"></a>Rafa monte StorSimple 8600 model Cihazınızı
Merhaba sonraki adımları tooinstall StorSimple 8600 depolama cihazınız bir standart 19 inç dolapta ön ve arka gönderileri izleyin. Bu aygıtın iki kasa ile gelir: birincil muhafaza ve EBOD muhafazası. Bunların her ikisi de, rafa monte edilen toobe gerekir.

birden çok adımı, her biri aşağıdaki yordamlarını hello açıklanan Hello yükleme oluşur.

> [!IMPORTANT]
> StorSimple cihazları düzgün çalışması için rafa monte edilen olması gerekir.
> 
> 

### <a name="site-preparation"></a>Site hazırlama
Merhaba kasaları ön ve arka gönderileri sahip standart bir 19 inç rafa yüklü olması gerekir. Raf yükleme yordamı tooprepare aşağıdaki hello kullanın.

#### <a name="tooprepare-hello-site-for-rack-installation"></a>tooprepare hello site raf yükleme için
1. Bu hello birincil emin olun ve EBOD kutularının işi olmayan bir düz, kararlı ve düzey çalışma yüzeyinde güvenle (veya benzeri).
2. Burada düşündüğünüz yukarı tooset sahip standart AC hello site doğrulayın güç bağımsız bir kaynak veya bir kesintisiz güç kaynağı (UPS) ile bir rafa monte güç dağıtım birimi (PDU).
3. Bu bir 4U (2 X 2U) yuvası hello rafa monte toomount hello kasaları düşündüğünüz kullanılabilir olduğundan emin olun.

![Uyarı simgesi](./media/storsimple-safety/IC740879.png)![büyük ağırlık simgesi](./media/storsimple-8600-hardware-installation/HCS_HeavyWeight_Icon.png) **uyarı!**

 Merhaba aygıt ayarları el ile işleniyorsa iki kişiler kullanılabilir toomanage hello ağırlığa sahip olduğunuzdan emin olun. Tam olarak yapılandırılmış bir kasa too32 kg (70 lb.) tartmanız.

### <a name="rack-prerequisites"></a>Raf önkoşulları
Merhaba kasaları ile dolap bir standart 19 inç dolapta yüklemesi için tasarlanmıştır:

* Raf 27.84 inç minimum derinliği toopost sonrası
* En yüksek ağırlığı hello cihaz için 32 kg
* 5 Pascal (0,5 mm su ölçer), en fazla arka baskısı

### <a name="rack-mounting-rail-kit"></a>Raf bağlama raylar Seti
Rayları takma kümesi hello 19 inç raf dolap ile kullanım için sağlanır. Merhaba rayları olmuştur test toohandle hello maksimum muhafaza ağırlığı. Bu rayları alanı hello raf içinde kaybı olmadan birden fazla kasaları yüklemesini de izin verir. Merhaba EBOD muhafazası ilk yükleyin.

#### <a name="tooinstall-hello-ebod-enclosure-on-hello-rails"></a>tooinstall hello EBOD muhafazası hello rayları üzerinde
1. Yalnızca iç rayları aygıtınızda yüklü değilse bu adımı gerçekleştirin. Genellikle, hello iç rayları hello fabrikada yüklenir. Rayları yüklü değilse hello raylar sol ve sağ raylar slayt toohello hello muhafaza kasa yanlarından yükleyin. Bunlar, her bir tarafta altı ölçüm Vida kullanarak ekleyin. yönlendirmeyle, slayt işaretlenir hello raylar toohelp **LH – ön** ve **RH – ön**, ve hello muhafaza hello arka yapıştırılmış hello son Konik bitiş vardır.
   
    ![Tooenclosure kasa bağlanmasını raylar slayt](./media/storsimple-8600-hardware-installation/HCSAttachingRailSlidestoEnclosureChassis.png)
   
    **Merhaba muhafaza toohello yanlarından bağlanmasını raylar slayt**
   
   | Etiket | Açıklama |
   | --- | --- |
   |  1 |M 3 x 4 düğmesi head Vida |
   |  2 |Kasa slayt |
2. Merhaba sol raylar ve sağda derlemeleri toohello raf dolap dikey üye ekleyebilir. Merhaba köşeli işaretlenir **LH**, **RH**, ve **bu tarafı yukarı** tooguide doğru yönlendirme ile.
3. Merhaba raylar PIN'ler hello ön ve arka hello raylar derlemenin bulun. Merhaba raylar toofit hello raf gönderimleri arasında genişletmek ve hello PIN'ler hello ön ve arka raf post dikey üye delik yerleştirin. Merhaba raylar derleme düzeyi olduğundan emin olun.
4. Merhaba raylar derleme toohello raf iki hello ölçüm Vida kullanarak dikey üyeleri sağlanan güvenli hale getirin. Merhaba öne ve hello arka birinde bir Vidayı kullanın.
5. Bu adımları diğer raylar derleme hello için yineleyin.
   
     ![Düğmelere raylar slayt toorack dolap](./media/storsimple-8600-hardware-installation/HCSAttachingRailSlidestoRackCabinet.png)
   
    **Raylar derlemeleri toohello raf ekleme**
   
   | Etiket | Açıklama |
   | --- | --- |
   |   1 |Vidayı clamping |
   |   2 |Kare delik ön raf post Vidayı |
   |   3 |Ön raylar konumu PIN'ler sol |
   |   4 |Vidayı clamping |
   |   5 |Sol arka raylar konumu PIN'ler |

### <a name="mounting-hello-ebod-enclosure-in-hello-rack"></a>Merhaba EBOD muhafazası hello dolapta bağlama
Yeni yüklenen hello raf rayları adımları toomount hello EBOD muhafazası hello dolapta aşağıdaki hello gerçekleştirin.

#### <a name="toomount-hello-ebod-enclosure"></a>toomount hello EBOD muhafazası
1. Bir Yardımcısı ile Merhaba muhafaza kaldırın ve hello raf rayları ile Hizala.
2. Dikkatli bir şekilde hello muhafaza hello rayları yerleştirin ve sonra tamamen hello rafa dolap kullanıcılarıma.
   
    ![Cihaz hello rafa yerleştirme](./media/storsimple-8600-hardware-installation/HCSInsertingDeviceintheRack.png)
   
    **Merhaba dolapta Hello kasası oluşturma**
3. Merhaba sol ve sağ ön Flanş başlıklarını hello caps ücretsiz çekerek kaldırın. Merhaba Flanş başlıklarını yalnızca hello çıkıntıları ek.
4. Merhaba kasası, sol ve sağ her Flanş aracılığıyla sağlanan bir yıldız head Vidayı yükleyerek hello rafa güvenliğini sağlayın.
5. Konumda basarak ve yerine tutturma Hello Flanş başlıklarını yükleyin.
   
     ![Flanş başlıklarını takma](./media/storsimple-8600-hardware-installation/HCSInstallingFlangeCaps.png)
   
    **Merhaba Flanş başlıklarını takma**
   
   | Etiket | Açıklama |
   | --- | --- |
   |   1 |Muhafaza birleşme Vidayı |

### <a name="mounting-hello-primary-enclosure-in-hello-rack"></a>Merhaba dolapta Hello birincil kasası oluşturma
Merhaba EBOD muhafazası takma tamamladıktan sonra toomount hello birincil muhafaza gerekir aşağıdaki hello aynı adımları.

> [!NOTE]
> * Merhaba birkaç boş yuvalarında hello birincil kasası ile Merhaba EBOD muhafazası arasında raf olası toohave olur.
> * Sağlanan hello 2 m SAS kablosu tooconnect hello birincil muhafaza toohello EBOD muhafazası kullanın.
> * Hello göreli yerleşimini hello baş birim toohello EBOD birim üzerinde hiç bir kısıtlama yoktur. Bu nedenle, hello birincil muhafaza hello üst yuvası ve hello EBOD muhafazası aşağıdaki yerleştirilir — veya tam tersi.
> 
> 

Merhaba sonraki adım, cihaz güç, ağ ve seri erişim için toocable olduğunu.

## <a name="cable-your-storsimple-8600-device"></a>StorSimple 8600 cihazınızın kablolarını bağlama
Merhaba aşağıdaki yordamlar açıklamaktadır nasıl toocable StorSimple 8600 model Cihazınızı güç, ağ ve seri bağlantılar için.

### <a name="prerequisites"></a>Ön koşullar
Cihazınızı toocable başlamadan önce ihtiyacınız:

* Birincil muhafaza ve hello EBOD muhafazası, tamamen açılmış
* cihazınızla birlikte gelen 4 güç kabloları (2 her hello birincil ve EBOD muhafazası hello için)
* Merhaba aygıt tooconnect hello EBOD muhafazası toohello birincil kasası ile sağlanan 2 SAS kabloları
* Erişim too2 güç dağıtım (önerilen) birimleri (Pdu'lar)
* Ağ kabloları
* Seri kablolar sağlanan
* Seri USB dönüştürücü hello uygun sürücüsü (gerekirse) Bilgisayarınızda yüklü
* 4 QSFP sağlanan-için-SFP + bağdaştırıcılar 10 GbE ağ arabirimleri ile kullanmak için
* [StorSimple Cihazınızda hello 10 GbE ağ arabirimleri için desteklenen donanım](storsimple-supported-hardware-for-10-gbe-network-interfaces.md)

### <a name="sas-and-power-cabling"></a>SAS ve güç kabloları
Cihazınızı birincil muhafaza ve EBOD muhafazası sahiptir. Bu seri bağlı SCSI (SAS) bağlantısı ve güç için birlikte kablolu hello birimleri toobe gerektirir.

Bu cihaz hello için ilk kez ayarlarken, SAS ilk kablo ve ardından tam hello adımları güç kablo için hello adımları gerçekleştirin.

[!INCLUDE [storsimple-cable-8600-for-SAS](../../includes/storsimple-sas-cable-8600.md)]

[!INCLUDE [storsimple-cable-8600-for-power](../../includes/storsimple-cable-8600-for-power.md)]

### <a name="network-cabling"></a>Ağ kabloları
Cihazınızı bir etkin bekleme yapılandırmasında olduğu: belirli bir zamanda bir denetleyici modülü etkin ve tüm disk ve ağ hello sırasında işlemlerinde diğer Denetleyici Modülü bekleme. Bir denetleyici hatası oluşursa, hello bekleme denetleyicisi hemen etkinleştirir ve tüm hello disk ve ağ işlemleri devam eder.

toosupport bu yedek denetleyici yük devretmesi Cihazınızı ağ aşağıdaki adımları hello gösterildiği gibi toocable gerekir.

#### <a name="toocable-for-network-connection"></a>ağ bağlantısı için toocable
1. Cihazınızı her denetleyicisinde altı ağ arabirimi bulunur: dört 1 GB/sn ve iki 10 GB/sn Ethernet bağlantı noktası. Cihazınızı hello devre kartı çizim tooidentify hello veri bağlantı noktaları aşağıdaki toohello bakın.
   
     ![8600 aygıt devre kartı](./media/storsimple-8600-hardware-installation/HCSBackplaneof2UDevicewithPortsLabeled.jpg)
   
    **Geri Cihazınızı hello veri bağlantı noktalarını gösterme**
   
   | Etiket | Açıklama |
   | --- | --- |
   |   0,1,4,5 |1 GbE ağ arabirimleri |
   |   2,3 |10 GbE ağ arabirimleri |
   |   6 |Seri bağlantı noktaları |
2. Ağ kablosunun için diyagram aşağıdaki hello bakın. (Merhaba minimum ağ yapılandırması düz mavi çizgilerle gösterilir. "Yüksek kullanılabilirlik ve performans için gereken ek yapılandırma noktalı çizgilerle gösterilir.)

![Kabloyla 4U cihazınızın ağ bağlantısını yapma](./media/storsimple-8600-hardware-installation/HCSCableYour4UDeviceforNetwork.png)

**Cihazınız için kablo ağ**

| Etiket | Açıklama |
| --- | --- |
| A |Internet erişimi olan LAN |
| B |Denetleyici 0 |
| C |PCM 0 |
| D |Denetleyici 1 |
| E |PCM 1 |
| F |EBOD denetleyici 0 |
| G |EBOD Denetleyici 1 |
| H T |Ana bilgisayar (örneğin, dosya sunucuları) |
| 0-5 |Ağ arabirimleri |
| 6 |Birincil kasası |
| 7 |EBOD muhafazası |

Merhaba aygıt kablo kullanırken hello en düşük yapılandırma gerektirir:

* En az iki ağ arabirimi her denetleyicisi bulut erişimi için diğeri için iSCSI ile bağlı. başlangıç bağlantı noktası otomatik olarak etkinleştirilmiş ve hello hello cihaz seri Konsolu yapılandırılmış veri 0. Veri 0 dışında başka bir veri bağlantı noktası da toobe hello Klasik Azure portalı yapılandırılması gerekir. Bu durumda, veri 0 bağlantı noktası toohello birincil LAN (Internet erişimi olan ağ) bağlayın. Merhaba bağlantı noktaları olabilir diğer veri tooSAN/iSCSI LAN (VLAN) segment hedeflenen hello rol bağlı olarak hello ağın bağlı.
* Bir denetleyici yük devretme gerçekleşirse aynı her bağlı denetleyicisi toohello üzerinde aynı tooensure kullanılabilirlik ağ arabirimleri. Örneğin, tooconnect veri 0'ı seçin ve veri 3 hello denetleyicilerinden biri için veri 0 ve veri 3 üzerinde karşılık gelen tooconnect hello ihtiyacınız varsa diğer denetleyicisi hello.

Yüksek kullanılabilirlik ve performans için göz önünde bulundurun:

* Mümkün olduğunda, bir çift ağ arabiriminin bulut erişim (1 GbE) ve iSCSI (10 GbE önerilen) için başka bir çifti her denetleyicisinde yapılandırın.
* Mümkün olduğunda, ağ arabirimlerinin her denetleyici tootwo farklı anahtarlara tooensure kullanılabilirlik anahtar arızasına karşı bağlanması. Merhaba şekilde hello iki 10 GbE ağ arabirimleri, veri 2 ve veri 3, her bağlı denetleyicisi tootwo farklı anahtarlarından gösterilmektedir. Daha fazla bilgi için toohello başvuran **ağ arabirimleri** hello altında [StorSimple cihazınız için yüksek kullanılabilirlik gereksinimlerini](storsimple-system-requirements.md#high-availability-requirements-for-storsimple).

> [!NOTE]
> SFP + vericilerinin, 10 GbE ağ arabirimleri ile kullanıyorsanız, kullanım hello QSFP sağlanan-SFP + bağdaştırıcıları. Daha fazla bilgi için çok Git[hello 10 GbE ağ arabirimleri, StorSimple Cihazınızda için desteklenen donanım](storsimple-supported-hardware-for-10-gbe-network-interfaces.md).
> 
> 

### <a name="serial-port-cabling"></a>Seri bağlantı kabloları
Aşağıdaki adımları toocable hello seri bağlantı noktanızın gerçekleştirin.

#### <a name="toocable-for-serial-connection"></a>seri bağlantı için toocable
1. Cihazınızı bir İngiliz anahtarı simgesi tarafından tanımlanan her denetleyicisinde seri bağlantı noktası var. toolocate hello seri bağlantı noktaları, Cihazınızı arkasına hello üzerinde hello veri bağlantı noktalarını gösteren toohello Çizim bakın.
2. Merhaba, aygıt devre kartı etkin denetleyicisinde tanımlayın. Yanıp sönen bir mavi LED bu hello denetleyicisi etkin olduğunu gösterir.
3. (Gerekirse, dizüstü bilgisayarınız için hello USB seri dönüştürücü) sağlanan hello seri kabloyu ve konsol veya bilgisayar (terminal öykünme toohello aygıtla) bağlayın toohello hello etkin denetleyicisinin seri bağlantı noktası.
4. Merhaba seri USB sürücüleri (Merhaba aygıtla birlikte gelen) bilgisayarınıza yükleyin.
5. Merhaba seri bağlantı kurma aşağıdaki gibi ayarlayın:
   
   * 115.200 baud
   * 8 veri bitleri
   * 1 dur biti
   * Eşlik yok
   * Akış denetiminin ayarlanıp çok**yok**
6. Merhaba bağlantı hello konsolunda Enter tuşuna basarak çalışmakta olduğunu doğrulayın. Seri konsol menüsünde görüntülenmelidir.

> [!NOTE]
> **Uzaktan Yönetimi:** hello aygıt bir uzak veri merkezinde veya sınırlı erişimi olan bir bilgisayar odada yüklendiğinde hello seri bağlantılar tooboth denetleyicileri her zaman bağlı tooa seri konsol anahtar veya benzer ekipman olduğundan emin olun. Bu, bant dışı uzaktan denetim ve ağ kesintisi veya beklenmeyen arıza durumunda destek işlemler sağlar.
> 
> 

Cihazınız güç, ağ erişimi için kablo tamamlamış ve seri connection.hello sonraki adıma tooconfigure hello aygıtınızda bir yazılımdır.

## <a name="next-steps"></a>Sonraki adımlar
Artık çok hazırsınız[şirket içi StorSimple Cihazınızı yapılandırmak ve dağıtmak](storsimple-deployment-walkthrough-u2.md).

