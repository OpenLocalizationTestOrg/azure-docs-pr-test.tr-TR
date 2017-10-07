---
title: "aaaStorSimple sanal dizinin güncelleştirme 0,4 sürüm notları | Microsoft Docs"
description: "Kritik açık açıklar sorunlar ve çözümleri hello StorSimple sanal dizinin çalıştırmak için 0.4 güncelleştirin."
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
ms.workload: NA
ms.date: 04/05/2017
ms.author: alkohli
ms.openlocfilehash: 1fd174ff483f4f7b1b4a7853c9d9573d1e948cb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-virtual-array-update-04-release-notes"></a>StorSimple sanal dizinin güncelleştirme 0,4 sürüm notları

## <a name="overview"></a>Genel Bakış

Merhaba aşağıdaki sürüm notları hello kritik açık sorunları belirlemek ve Microsoft Azure StorSimple sanal dizinin güncelleştirmeleri çözümlenen sorunları hello.

Merhaba sürüm notları sürekli olarak güncelleştirilir ve geçici bir çözüm gerektiren kritik sorunlar bulundukça olarak eklenir. StorSimple sanal dizinizi dağıtmadan önce hello Sürüm Notları'nda bulunan hello bilgileri dikkatle gözden geçirin.

Güncelleştirme 0.4 karşılık gelen toohello yazılım sürüm **10.0.10289.0**.

> [!NOTE]
> Güncelleştirmeleri dağıtıldığından ve aygıtınızı yeniden başlatın. G/ç sürüyor durumunda hello aygıt kapalı kalma süresi doğurur.


## <a name="whats-new-in-hello-update-04"></a>Merhaba güncelleştirme 0.4 yenilikler nelerdir?
0.4 öncelikle birkaç geliştirmeleri ile birlikte bir hata düzeltmesi yapı güncelleştirmesidir. Bu sürümde, yedekleme hataları hello önceki sürümde sonuçta çeşitli hatalar giderilmiştir. Merhaba ana geliştirmeler ve hata düzeltmeleri aşağıdaki gibidir:

- **Yedekleme performans geliştirmeleri** -bu sürüm tooimprove hello yedekleme performansının birkaç önemli geliştirmeler yaptı. Sonuç olarak, çok sayıda dosya içeren hello yedeklemeler, tam ve artımlı yedeklemeler için başlangıç saati toocomplete, önemli ölçüde azalma bakın.

- **Gelişmiş geri yükleme performans** -bu sürüm, çok sayıda dosya kullanırken hello geri yükleme performansı önemli ölçüde artırmak geliştirmeler içerir. 2-4 milyon dosyaları kullanıyorsanız, 16 GB RAM toosee hello geliştirmelerle sanal bir dizi sağlamanızı öneririz. 2 milyondan az dosyaları, hello sanal makine için en düşük gereksinim hello kullanarak toobe devam ettiğinde 8 GB RAM.

- **Geliştirmeleri tooSupport paket** -hello geliştirmeler disk, CPU, bellek, ağ ve dolayısıyla aygıt sorunları tanılama/ayıklama hello işlem artırma hello destek paketi bulutunu hello istatistiklerini günlüğü.

- **Sınır yerel olarak sabitlenmiş iSCSI birimleri too200 GB** -yerel olarak sabitlenmiş birimler için StorSimple sanal dizisinde tooa 200 GB iSCSI biriminde sınırlamak olan öneririz. Katmanlı birimlerin Hello yerel ayırma toobe % 10'hello birim boyutu sağlanan ancak 200 GB olarak tutulabilir devam eder. 

- **Yedeklemesine ilişkin hata düzeltmeleri** -yazılım önceki sürümlerinde, yedekleme hataları neden sorunları ilgili toobackups vardı. Bu hatalar bu sürümde giderilmiştir.


## <a name="issues-fixed-in-hello-update-04"></a>Merhaba güncelleştirme 0.4 giderilen sorunlar

Merhaba aşağıdaki tabloda bu sürümde giderilen sorunlar özetini sağlar.

| Hayır. | Özellik | Sorun |
| --- | --- | --- |
| 1 |Yedekleme performansı|Hello önceki sürümler, çok sayıda dosya içeren hello yedeklemeleri uzun süre toocomplete (Merhaba sırayla gün) alır. Bu sürümde, başlangıç saati toocompletion, önemli ölçüde azalma hello tam ve artımlı yedeklemeler bakın. |
| 2 |Destek Paketi|Disk, CPU, bellek, ağ ve bulut İstatistikleri şimdi hello destek paketleri cihaz sorunları gidermeye çok etkili yapma toohello destek günlükleri kaydedilir.|
| 3 |Backup |Önceki sürümlerde, yedeklemeleri uzun süre çalışan yedekleme hatalarına kaynaklanan hello aygıtta alanı crunch neden olabilir. Bu hata, bir seferde en fazla 5 yedeklemeleri tooqueue sağlayarak bu sürümde değinilmiştir.|
| 4 |iSCSI | Önceki sürümlerde, katmanlı ya da yerel olarak sabitlenmiş birimleri için yerel ayırma hello sağlanan hello birim boyutu % 10 idi. Bu sürümde, en fazla fazla ile sınırlı too10% hello yerel ayırma (yerel olarak sabitlenmiş veya katmanlı) tüm iSCSI birimleri için olan 200 GB (2 TB'den büyük katmanlı birimleri) hello yerel diskte daha fazla alan böylece boşaltma. Bu sürümde hello yerel olarak sabitlenmiş birimleri sınırlı too200 GB olmasını öneririz.|


## <a name="known-issues-in-hello-update-04"></a>Merhaba güncelleştirme 0.4 bilinen sorunlar

Merhaba aşağıdaki tabloda StorSimple sanal dizinin hello için bilinen sorunlar özetini sağlar ve hello sorunları hello önceki sürümlerden yayın-not ettiğiniz içerir. 

| Hayır. | Özellik | Sorun | Geçici çözüm/açıklamaları |
| --- | --- | --- | --- |
| **1.** |Güncelleştirmeler |Merhaba Önizleme sürümünde oluşturulan hello sanal aygıt desteklenen güncelleştirilmiş tooa genel kullanılabilirlik sürümü olamaz. |Bu sanal cihazlar Merhaba olağanüstü durum kurtarma (DR) iş akışını kullanarak genel kullanılabilirlik sürümü devredilir gerekir. |
| **2.** |Sağlanan veri diski |Belirli bir belirtilen boyutta bir veri diski kez sağlamış ve hello karşılık gelen StorSimple sanal cihaz oluşturulan, gerekir değil genişletin veya hello veri diski küçültmeye. Merhaba cihaz yerel katmanlarda hello tüm hello veri kaybıyla toodo sonuçları çalışıyor. | |
| **3.** |Grup İlkesi |Bir cihaz etki alanına katılmış olduğunda, bir Grup İlkesi uygulama hello aygıt işlemi olumsuz etkileyebilir. |Active Directory için kendi kuruluş biriminde (OU) sanal dizinizi olduğundan ve hiçbir Grup İlkesi nesneleri (GPO) uygulanan tooit olduğundan emin olun. |
| **4.** |Yerel web kullanıcı Arabirimi |Internet Explorer (IE ESC) Artırılmış güvenlik özellikleri etkinleştirilirse, sorun giderme veya bakım gibi bazı yerel web kullanıcı Arabirimi sayfalarını düzgün çalışmayabilir. Bu sayfaları düğmeleri de çalışmayabilir. |Internet Explorer Artırılmış güvenlik özelliklerini kapatın. |
| **5.** |Yerel web kullanıcı Arabirimi |Bir Hyper-V sanal makine ağ arabirimleri hello Web kullanıcı Arabirimi 10 GB/sn arabirimleri görüntülenen hello. |Hyper-V yansımasını davranıştır. Hyper-V sanal ağ bağdaştırıcıları için 10 GB/sn her zaman gösterir. |
| **6.** |Katmanlı birimler veya paylaşımlar |Bayt aralığı, katmanlı birimleri StorSimple hello ile çalışan uygulamalar için kilitleme desteklenmiyor. Bayt aralığı kilitleme etkinse, StorSimple katmanlama çalışmaz. |Önerilen ölçüleri içerir: <br></br>Uygulama mantığınızın kilitleme bayt aralığı kapatın.<br></br>Bu uygulama için tooput verileri yerel olarak sabitlenmiş birimleri olarak karşılıklı tootiered birimleri seçin.<br></br>*Uyarı*: hello geri yükleme tamamlamadan önce kullanarak yerel olarak sabitlenmiş birimleri ve bayt aralığı kilitleme etkin olduğunda, yerel olarak sabitlenmiş hello birimi çevrimiçi olabilir. Bir geri yükleme devam ediyor, böyle durumlarda, ardından hello geri yükleme toocomplete için beklemeniz gerekir. |
| **7.** |Katmanlı paylaşımları |Büyük dosyaları ile çalışma yavaş katmanı genişletmek neden olabilir. |Büyük dosyaları ile çalışırken, o hello en büyük dosya hello paylaşım boyutu %3 küçük öneririz. |
| **8.** |Kapasite paylaşımlar için kullanılan |Görebileceğiniz hello paylaşımında hiçbir veri olduğunda tüketim paylaşın. Paylaşımlar için kullanılan hello kapasite meta veriler içerdiğinden budur. | |
| **9.** |Olağanüstü durum kurtarma |Yalnızca bir dosya sunucusu toohello hello olağanüstü durum kurtarma gerçekleştirebilirsiniz aynı etki alanında, hello kaynak aygıt. Olağanüstü durum kurtarma tooa hedef aygıt başka bir etki alanındaki bu sürümde desteklenmiyor. |Bu, bir sonraki sürümde uygulanır. |
| **10.** |Azure PowerShell |Merhaba StorSimple sanal cihazlar, bu sürümde hello Azure PowerShell aracılığıyla yönetilemez. |Tüm hello yönetim hello sanal cihazların Merhaba Klasik Azure portalı ve hello yerel web kullanıcı Arabirimi aracılığıyla yapılmalıdır. |
| **11.** |Parola değiştirme |Merhaba sanal dizinin aygıt konsolu yalnızca en-US klavye biçiminde giriş kabul eder. | |
| **12.** |CHAP |CHAP kimlik oluşturulduktan sonra kaldırılamaz. Ayrıca, hello CHAP kimlik bilgilerini değiştirirseniz, tootake hello çevrimdışı birimler gerekir ve bunları çevrimiçi hello tootake değişikliğin için duruma getirin. |Bu sorunu sonraki bir sürümde değinilmiştir. |
| **13.** |iSCSI sunucusu |bir iSCSI birim için görüntülenen 'depolama kullanılan' hello hello StorSimple Yöneticisi hizmetiniz ve hello iSCSI konağının farklı olabilir. |Merhaba iSCSI konağının hello filesystem görünüme sahiptir.<br></br>Merhaba aygıt hello birim hello en büyük boyutta değiştirildiği ayrılan hello blok görür. |
| **14.** |Dosya sunucusu |Bir klasördeki bir dosyaya bir alternatif veri akışı (ilişkili ADS) varsa, hello ADS değil yedeklenemez veya olağanüstü durum kurtarma, kopyalama ve öğe düzeyinde Kurtarma geri. | |
| **15.** |Dosya sunucusu |Sembolik bağlantılar desteklenmez. | |
| **16.** |Dosya sunucusu |Dosyaları tarafından Windows şifreleme dosya sistemi (üzerinden kopyaladığınızda EFS) korumalı veya desteklenmeyen bir yapılandırmada StorSimple sanal dizinin dosya sunucusu sonucu hello üzerinde depolanan.  | |

## <a name="next-step"></a>Sonraki adım
[0.4 güncelleştirmesini](storsimple-virtual-array-install-update-04.md) , StorSimple sanal dizi.

## <a name="references"></a>Başvurular
Eski bir sürüm notu için mi arıyorsunuz? Şuraya gidin: 

* [StorSimple sanal dizinin güncelleştirme 0,3 sürüm notları](storsimple-ova-update-03-release-notes.md)
* [StorSimple sanal dizinin güncelleştirme 0,1 ve 0.2 sürüm notları](storsimple-ova-update-01-release-notes.md)
* [StorSimple sanal dizinin genel kullanılabilirlik sürüm notları](storsimple-ova-pp-release-notes.md)

