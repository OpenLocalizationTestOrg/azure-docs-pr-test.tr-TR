---
title: "aaaMicrosoft Azure StorSimple sanal dizinin genel bakış | Microsoft Docs"
description: "Merhaba StorSimple sanal dizinin bir şirket içi sanal dizinin ve Microsoft Azure bulut depolama arasında depolama görevleri yöneten bir tümleşik depolama çözümü açıklanmaktadır."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 169c639b-1124-46a5-ae69-ba9695525b77
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 12/09/2016
ms.author: alkohli
ms.openlocfilehash: 8978e074142940748857150cc93b37272349d53d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toohello-storsimple-virtual-array"></a>Giriş toohello StorSimple sanal dizinin
## <a name="overview"></a>Genel Bakış
Merhaba Microsoft Azure StorSimple sanal dizinin bir hiper yönetici ve Microsoft Azure bulut depolama çalıştıran bir şirket içi sanal dizinin arasında depolama görevleri yöneten bir tümleşik depolama çözümüdür. Merhaba sanal bir verimli, uygun maliyetli ve kolayca yönetilen dosya sunucusu veya hello sorunlar ve Kurumsal Depolama ve veri koruma ile ilişkili giderleri birçoğunu ortadan iSCSI sunucu çözümü dizisidir. Merhaba sanal özellikle uzak office/şube ofisi senaryolarında için oldukça uygun dizisidir.

Bu konuda hello sanal dizinin genel bir bakış sağlar - diğer bazı kaynaklar aşağıda verilmiştir:

* En iyi yöntemler için bkz: [StorSimple sanal dizinin en iyi yöntemler](storsimple-ova-best-practices.md).
* Merhaba StorSimple 8000 serisi cihazlar genel bakış için çok Git[StorSimple 8000 serisi: karma bulut çözümünün](storsimple-overview.md). 
* Merhaba StorSimple 5000/7000 Serisi cihazlar hakkında daha fazla bilgi için çok gidin[StorSimple çevrimiçi Yardım](http://onlinehelp.storsimple.com/).

Merhaba sanal dizinin hello iSCSI veya sunucu ileti bloğu (SMB) protokolünü destekler. Varolan hiper yönetici altyapınızda çalıştırır ve katmanlama toohello bulut, bulut yedekleme, hızlı geri yükleme, öğe düzeyinde kurtarma ve olağanüstü durum kurtarma özellikleri sağlar.

Merhaba aşağıdaki tabloda hello StorSimple sanal dizinin hello önemli özellikleri özetlenmektedir.

| Özellik | StorSimple Sanal Dizisi |
| --- | --- |
| Yükleme gereksinimleri |Sanallaştırma (Hyper-V veya VMware) altyapısını kullanır |
| Kullanılabilirlik |Tek düğüm |
| Toplam Kapasite (bulut dahil) |Too64 TB kullanılabilir kapasiteyi sanal dizi başına |
| Yerel kapasite |Sanal dizinin (gerek tooprovision 500 GB too8 TB disk alanı) başına 390 GB too6.4 TB kullanılabilir kapasite |
| Yerel protokolleri |iSCSI veya SMB |
| Kurtarma süresi hedefi (RTO) |iSCSI: 2 dakikadan daha kısa bir süre boyutu ne olursa olsun |
| Kurtarma noktası hedefi (RPO) |Günlük yedeklemeler ve isteğe bağlı yedeklemeler |
| Depolama katmanlamayı |Hangi verilerin, giriş veya çıkış katmanlı eşleme toodetermine kullandığı ısı |
| Destek |Merhaba sağlayıcı tarafından desteklenen sanallaştırma altyapısı |
| Performans |Temel alınan altyapınıza bağlı olarak değişir |
| Veri mobility |Toohello geri yükleyebilmeniz için aynı cihaz veya (dosya sunucusu) düzeyinde |
| Depolama katmanları |Yerel hiper yönetici depolama ve bulut |
| Paylaşım boyutu |Katmanlı: too20 TB; yerel olarak sabitlenmiş: Yukarı too2 TB |
| Birim boyutu |Katmanlı: 500 GB too5 TB; yerel olarak sabitlenmiş: 50 GB too500 GB |
| Birim boyutu |Katmanlı: too5 TB; yerel olarak sabitlenmiş: too500 GB'a |
| Anlık görüntüler |Kilitlenme tutarlı |
| Öğe düzeyinde kurtarma |Evet; Kullanıcılar paylaşımlarından geri yükleyebilir |

## <a name="why-use-storsimple"></a>StorSimple neden kullanılır?
StorSimple kullanıcı ve sunucu tooAzure depolama dakika cinsinden herhangi bir uygulama değişiklik olmadan bağlanır.

Merhaba aşağıdaki tabloda bazı hello avantajları bu hello StorSimple sanal bir çözümdür dizi açıklanmaktadır.

| Özellik | Avantaj |
| --- | --- |
| Saydam tümleştirme |Merhaba sanal dizinin hello iSCSI veya hello SMB protokolünü destekler. Merhaba veri taşıma hello yerel katmanı ve hello bulut katmanı arasındaki sorunsuz ve saydam toohello kullanıcıdır. |
| Azaltılmış depolama maliyetleri |StorSimple ile en sık kullanılan hello etkin verileri için yeterli yerel depolama toomeet geçerli taleplerini sağlayın. Büyüme depolama gereksinimlerine göre uygun maliyetli uygulamasına StorSimple katmanları soğuk veri depolama bulut. Merhaba veri yinelenenleri kaldırılmış sıkıştırılmış ve toohello bulut göndermeden önce toofurther azaltmak depolama gereksinimleri ve gider. |
| Basitleştirilmiş Depolama Yönetimi |StorSimple birden çok aygıt StorSimple Aygıt Yöneticisi'ni toomanage kullanarak hello bulutta merkezi yönetim sağlar. |
| Geliştirilmiş olağanüstü durum kurtarma ve uyumluluk |StorSimple daha hızlı olağanüstü durum kurtarma hello meta veriler hemen geri yükleme ve gerektiği gibi hello veri geri yükleme işlemini kolaylaştırır. Başka bir deyişle, normal işlemleri en az kesintiyi ile devam edebilirsiniz. |
| Veri mobility |Veri kurtarma ve geçiş amaçları için diğer sitelerdeki katmanlı toohello bulut erişilebilir. Verileri yalnızca toohello özgün sanal dizinin geri yükleyebilirsiniz unutmayın. Ancak, olağanüstü durum kurtarma özellikleri toorestore hello tüm sanal dizinin tooanother sanal dizinin kullanın. |

## <a name="storsimple-workload-summary"></a>StorSimple iş yükü özeti

Desteklenen StorSimple iş yükleri özetini aşağıdaki tabloda verilmiştir.

|Senaryo     |İş yükü     |Destekleniyor      |Kısıtlamaları               |
|-------------|-------------|---------------|---------------------------|
|ROBO işbirliği |Dosya Paylaşımı     |Evet      |Bkz: [dosya sunucusu için en fazla sınırları](storsimple-ova-limits.md).<br></br>Bkz: [desteklenen SMB sürümleri için sistem gereksinimleri](storsimple-ova-system-requirements.md).| Tüm sürümler     |

## <a name="workflows"></a>İş akışları
Merhaba StorSimple sanal dizinin özellikle iş akışları şu hello için uygundur:

* [Bulut tabanlı depolama yönetimi](#cloud-based-storage-management)
* [Konumdan bağımsız yedekleme](#location-independent-backup)
* [Veri koruma ve olağanüstü durum kurtarma](#data-protection-and-disaster-recovery)

### <a name="cloud-based-storage-management"></a>bulut tabanlı depolama yönetimi
Merhaba birden fazla cihazda depolanan Azure portal toomanage verileri ve birden fazla konumda çalışan hello StorSimple cihaz Yöneticisi hizmeti kullanabilirsiniz. Bu dağıtılmış şube senaryolarında özellikle kullanışlıdır. Merhaba StorSimple cihaz Yöneticisi hizmeti toomanage sanal dizileri ve fiziksel StorSimple cihazları ayrı örnekleri oluşturmalısınız unutmayın. Ayrıca bu hello sanal dizinin hello yeni Azure portalına hello yerine Klasik Azure portalı artık kullanır. unutmayın.

![bulut tabanlı depolama yönetimi](./media/storsimple-ova-overview/cloud-based-storage-management.png)

### <a name="location-independent-backup"></a>Konumdan bağımsız yedekleme
Merhaba sanal diziyle bulut anlık görüntüleri bir birim veya paylaşım konumu-bağımsız, zaman içinde nokta kopyasını sağlar. Bulut anlık görüntüleri, varsayılan olarak etkinleştirilir ve devre dışı bırakılamaz. Tüm birim ve paylaşımların yukarı yedekleme sırasında hello aynı zaman tek bir günlük yedekleme İlkesi aracılığıyla ve ek geçici yedeklemeler gerektiğinde alabilir.

### <a name="data-protection-and-disaster-recovery"></a>Veri koruma ve olağanüstü durum kurtarma
Merhaba sanal dizinin veri koruma ve olağanüstü durum kurtarma senaryoları aşağıdaki hello destekler:

* **Birimi veya paylaşımı geri yükleme** – yeni iş akışı toorecover bir birim hello restore kullanın veya paylaşın. Bu yaklaşım toorecover hello tüm birim veya paylaşım kullanın.
* **Öğe düzeyinde kurtarma** – paylaşımları toorecent yedeklemeleri Basitleştirilmiş erişim izni. Bir özel tek bir dosyayı kolayca kurtarabilirsiniz *.backup* hello bulutta klasör. Bu geri yükleme yeteneği kullanıcı odaklı ve hiçbir yönetim müdahalesi gerekli değildir.
* **Olağanüstü durum kurtarma** – kullanım hello yük devretme özelliği toorecover tüm birimler veya paylaşımlar tooa yeni sanal bir dizi. Merhaba yeni sanal dizinin oluşturun ve hello StorSimple cihaz Yöneticisi hizmeti ile kaydetme sonra hello özgün sanal dizinin başarısız. Merhaba yeni sanal dizinin ardından sağlanan hello kaynakları varsayar. 

## <a name="storsimple-virtual-array-components"></a>StorSimple sanal dizinin bileşenleri
Merhaba sanal dizinin hello aşağıdaki bileşenleri içerir:

* [Sanal dizinin](#virtual-array) – sanallaştırılmış ortamı ya da hiper yönetici sağlanan bir sanal makine temel bir karma bulut depolama cihazı.  
* [StorSimple cihaz Yöneticisi hizmeti](#storsimple-device-manager-service) – hello bir veya daha fazla StorSimple cihazlar farklı coğrafi konumlardan erişebilmeniz için tek bir web arabiriminden yönetmenizi sağlayan Azure portalı uzantısı bir. Merhaba StorSimple cihaz Yöneticisi hizmeti toocreate kullanın ve hizmetleri yönetmek, görüntüleyin ve aygıtları ve Uyarıları yönetebilir ve birimler, paylaşımlar ve varolan anlık görüntüleri yönetin.
* [Yerel web kullanıcı arabirimi](#local-web-user-interface) – toohello yerel ağa bağlanmak ve ardından hello aygıt hello StorSimple cihaz Yöneticisi Hizmeti'ne kaydedin ve böylece kullanılan tooconfigure hello aygıt bir web tabanlı bir kullanıcı Arabirimi. 
* [Komut satırı arabirimi](#command-line-interface) – bir Windows PowerShell arabirimi hello sanal dizisinde bir destek oturumu toostart kullanabilirsiniz.
  Merhaba aşağıdaki bölümlerde daha ayrıntılı bu bileşenlerin her birini açıklayan ve nasıl hello çözüm verileri düzenler, depolama ayırır ve Depolama Yönetimi ve veri koruması kolaylaştıran açıklanmaktadır.

### <a name="virtual-array"></a>Sanal dizi
Merhaba sanal dizinin birincil depolama sağlayan, bulut depolama ile iletişim yönetir ve tooensure hello güvenlik ve hello cihazda depolanan tüm verileri gizliliğini yardımcı olan bir tek düğümlü depolama çözümüdür.

Merhaba sanal dizinin indirme için kullanılabilir bir modeli mevcuttur. Merhaba sanal dizi depolama bulut maksimum kapasitesi 6.4 TB'lık hello aygıtla (bir temel alınan depolama gereksinimi 8 TB) ve 64 TB dahil olmak üzere sahiptir. 

Merhaba sanal dizinin özellikler aşağıdaki hello sahiptir:

* Uygun maliyetli olması. Bu bağdaştırıcılar var olan sanallaştırma altyapınızın kullanır ve var olan Hyper-V veya VMware hiper yöneticide dağıtılabilir.
* Merhaba veri merkezinde yer alır ve bir iSCSI sunucusu veya bir dosya sunucusu yapılandırılabilir. 
* Merhaba bulut ile tümleşiktir.
* Yedeklemeler, olağanüstü durum kurtarma kolaylaştırmak ve öğe düzeyinde Kurtarma (ILR) basitleştirmek hello bulutta depolanır. 
* Yalnızca bunları tooa fiziksel aygıt uygulanacak şekilde güncelleştirmeleri toohello sanal dizinin uygulayabilirsiniz.

> [!NOTE]
> Sanal bir dizi genişletilemiyor. Bu nedenle, hello sanal dizinin oluşturduğunuzda önemli tooprovision yeterli depolama olur. 
> 
> 

### <a name="storsimple-device-manager-service"></a>StorSimple cihaz Yöneticisi hizmeti
Microsoft Azure StorSimple sağlayan bir web tabanlı kullanıcı arabirimi Merhaba, toocentrally sağlayan StorSimple cihaz Yöneticisi hizmeti, StorSimple depolama yönetin. Merhaba StorSimple cihaz Yöneticisi hizmeti tooperform hello görevleri aşağıdaki kullanabilirsiniz:

* Birden çok StorSimple sanal dizisi tek bir hizmetten yönetin. 
* Yapılandırmak ve StorSimple sanal diziler için güvenlik ayarlarını yönetin. (Şifreleme hello bulutta Microsoft Azure API bağlıdır.)
* Depolama hesabının kimlik bilgilerini ve özelliklerini yapılandırın.
* Yapılandırın ve birimler veya paylaşımlar yönetin.
* Yedekleme ve birimler veya paylaşımlar verilerini geri yükleyin.
* Performans İzleyici.
* Sistem ayarlarını gözden geçirin ve olası sorunları tanımlar.

Merhaba StorSimple Aygıt Yöneticisi'ni service tooperform günlük yönetim sanal dizinin kullanın.

Daha fazla bilgi için çok Git[kullanım StorSimple Cihazınızı StorSimple cihaz Yöneticisi hizmeti tooadminister hello](storsimple-virtual-array-manager-service-administration.md).

### <a name="local-web-user-interface"></a>Yerel web kullanıcı arabirimi
Merhaba sanal dizinin tek seferlik yapılandırma ve hello StorSimple cihaz Yöneticisi hizmeti ile Merhaba aygıt kaydı için kullanılan bir web tabanlı bir kullanıcı Arabirimi içerir. Aşağı tooshut kullanın ve hello sanal dizinin yeniden başlatın, tanılama testleri çalıştırmak, yazılım güncelleştirmesi, hello cihaz Yöneticisi parolasını değiştirme, sistem günlüklerini görüntüleyebilir ve Microsoft Support toofile bir hizmet isteği başvurun. 

Kullanma hakkında bilgi için web tabanlı UI Merhaba, çok Git[kullanın, StorSimple sanal dizinizi web tabanlı UI tooadminister hello](storsimple-ova-web-ui-admin.md).

### <a name="command-line-interface"></a>Komut satırı arabirimi
hello dahil Windows PowerShell arabirimi ve sanal dizinizi karşılaşabileceğiniz sorunları gidermek, Yardım için destek oturumu Microsoft Support tooinitiate sağlar.

## <a name="storage-management-technologies"></a>Depolama yönetimi teknolojileri
Ayrıca toohello sanal dizinin ve diğer bileşenleri, çözümü kullanan yazılım teknolojileri tooprovide hızlı erişim tooimportant verileri aşağıdaki Merhaba, depolama tüketimini azaltabilir ve sanal dizinizi depolanmış verileri korumak StorSimple hello:

* [Otomatik depolama katmanlama](#automatic-storage-tiering) 
* [Yerel olarak sabitlenmiş paylaşımları ve birimler](#locally-pinned-shares-and-volumes)
* [Yinelenenleri kaldırma ve veri sıkıştırma katmanlı toohello bulut desteklenen veya](#deduplication-and-compression-for-data-tiered/backed-up-to-the-cloud) 
* [Zamanlanmış ve isteğe bağlı yedeklemeler](#scheduled-and-on-demand-backups)

### <a name="automatic-storage-tiering"></a>Otomatik depolama katmanlama
Merhaba sanal dizi hello sanal dizinin ve hello bulut üzerinde yeni bir katmanlama mekanizması toomanage depolanan verileri kullanır. Yalnızca iki katmanı vardır: hello yerel sanal dizinin ve Azure bulut depolama. Merhaba StorSimple sanal dizinin veri geçerli kullanımı, geçerlilik süresi ve ilişkileri tooother verileri izler ve ısı Haritası üzerinde temel hello katmanları içine otomatik olarak düzenler. Daha az etkin ve etkin olmayan verileri otomatik olarak ederken çoğu etkin (yeni) yerel olarak depolanan veriler toohello bulut geçirildi. (Tüm yedeklemeler hello bulutta depolanır.) StorSimple ayarlar ve verileri yeniden düzenler ve kullanım düzenlerini olarak depolama atamalarını değiştirin. Örneğin, bazı bilgiler zaman içinde daha az etkin hale gelebilir. Aşamalı olarak daha az etkin hale geldiğinde, toohello bulut katmanlı. Bu aynı verileri tekrar etkin hale gelirse, toohello Depolama dizisinde katmanlı.

Belirli katmanlı paylaşım veya birim için verileri kendi yerel katmanı alanı garanti edilmez. (yaklaşık alanın % 10 hello toplam sağlanan o paylaşımı veya birimi için). Bu paylaşım veya birim için sanal dizisindeki hello hello kullanılabilir depolama alanı azaltır, ancak bir paylaşımı veya birimi katmanlama hello katmanlama ihtiyaçlarını diğer paylaşımları veya birimler tarafından etkilenmez, sağlar. Bu nedenle bir paylaşımı veya birimi çok meşgul bir iş yükünü diğer iş yükleri toohello bulut zorlayamaz. 

![Otomatik depolama katmanlama](./media/storsimple-ova-overview/automatic-storage-tiering.png)

> [!NOTE]
> Yerel olarak sabitlenmiş bir birim belirtebilirsiniz, bu durumda hello veri hello sanal dizisinde kalır ve hiçbir zaman toohello bulut katmanlı. Daha fazla bilgi için çok Git[yerel olarak sabitlenmiş paylaşımları ve birimler](#locally-pinned-shares-and-volumes).
> 
> 

### <a name="locally-pinned-shares-and-volumes"></a>Yerel olarak sabitlenmiş paylaşımları ve birimler
Uygun paylaşımları ve yerel olarak sabitlenmiş birimler oluşturabilirsiniz. Kritik uygulamalar tarafından gerekli veri hello sanal dizisinde kalmasını ve hiçbir zaman bu yeteneği sağlar katmanlı toohello bulut. Yerel olarak sabitlenmiş paylaşımları ve birimler özellikler aşağıdaki hello vardır: 

* Bunlar konu toocloud gecikmeleri veya bağlantı sorunları olup olmadığı.
* Bunlar, yedekleme ve olağanüstü durum kurtarma özelliklerinden StorSimple bulut hala yararlanır.

Yerel olarak sabitlenmiş bir paylaşımı veya katmanlı gibi birim veya bir katmanlı paylaşımı geri yükleyebilirsiniz veya toplu olarak yerel olarak sabitlenmiş. 

Yerel olarak sabitlenmiş birimleri hakkında daha fazla bilgi için çok Git[hello StorSimple cihaz Yöneticisi hizmeti toomanage birimler kullanmak](storsimple-virtual-array-manage-volumes.md).

### <a name="deduplication-and-compression-for-data-tiered-or-backed-up-toohello-cloud"></a>Yinelenenleri kaldırma ve veri sıkıştırma katmanlı toohello bulut desteklenen veya
StorSimple kullandığı yinelenenleri kaldırma ve veri sıkıştırma toofurther hello bulutta depolama gereksinimlerini azaltır. Yinelenenleri kaldırma azaltır hello genel hello depolanan veri kümesi içinde artıklık ortadan kaldırarak depolanan veri miktarı. Bilgi değiştikçe değişmeden hello veri StorSimple yoksayar ve yakalamaları değişiklikler yalnızca hello. Ayrıca, StorSimple tanımlama ve yinelenen bilgileri kaldırma depolanan verilerin hello miktarını azaltır. 

> [!NOTE]
> Merhaba sanal dizisinde depolanan verileri yinelenenleri kaldırılmış veya sıkıştırılmış değil. Tüm yinelenenleri kaldırma ve sıkıştırma hello veri toohello bulut yalnızca gönderilmeden önce gerçekleşir.
> 
> 

### <a name="scheduled-and-on-demand-backups"></a>Zamanlanmış ve isteğe bağlı yedeklemeler
StorSimple veri koruma özelliklerine toocreate isteğe bağlı yedeklemeler sağlar. Ayrıca, bir varsayılan yedekleme zamanlaması günlük yedek yedeklenen verileri sağlar. Yedeklemeleri hello formunda hello bulutta depolanan artımlı anlık görüntü alınır. Yalnızca hello değişiklikler hello son yedeklemeden sonra kaydedin, anlık görüntü oluşturulur ve hızlı bir şekilde geri. Bu anlık görüntüler, çünkü bunlar ikincil depolama sistemleri (örneğin, bant yedekleme) değiştirin ve gerekirse toorestore, veri tooyour datacenter veya tooalternate sitelerin izin olağanüstü durum kurtarma senaryolarında kritik düzeyde önemli olabilir.

## <a name="next-steps"></a>Sonraki adımlar
Nasıl çok öğrenin[hello sanal dizinin portal hazırlama](storsimple-virtual-array-deploy1-portal-prep.md).

