---
title: "aaaStorSimple sanal dizinin güncelleştirme 0,5 sürüm notları | Microsoft Docs"
description: "Kritik açık açıklar sorunlar ve çözümleri hello StorSimple sanal dizinin çalıştırmak için 0,5 güncelleştirin."
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
ms.date: 05/08/2017
ms.author: alkohli
ms.openlocfilehash: a249e2e8f0105dcf6cc02d3136dfa3e37ea615d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-virtual-array-update-05-release-notes"></a>StorSimple sanal dizinin güncelleştirme 0,5 sürüm notları

## <a name="overview"></a>Genel Bakış

Merhaba aşağıdaki sürüm notları hello kritik açık sorunları belirlemek ve Microsoft Azure StorSimple sanal dizinin güncelleştirmeleri çözümlenen sorunları hello.

Merhaba sürüm notları sürekli olarak güncelleştirilir ve geçici bir çözüm gerektiren kritik sorunlar bulundukça olarak eklenir. StorSimple sanal dizinizi dağıtmadan önce hello Sürüm Notları'nda bulunan hello bilgileri dikkatle gözden geçirin.

Güncelleştirme 0,5 karşılık gelen toohello yazılım sürüm **10.0.10290.0**.

> [!NOTE]
> Güncelleştirmeleri dağıtıldığından ve aygıtınızı yeniden başlatın. G/ç sürüyor durumunda hello aygıt kapalı kalma süresi doğurur. Nasıl tooapply hello güncelleştirme hakkında ayrıntılı yönergeler için çok Git[güncelleştirme 0,5](storsimple-virtual-array-install-update-05.md).


## <a name="whats-new-in-hello-update-05"></a>Merhaba güncelleştirme 0,5 yenilikler nelerdir?
Güncelleştirme 0,5 öncelikle bir hata düzeltmesi yapıdır. Merhaba ana geliştirmeler ve hata düzeltmeleri aşağıdaki gibidir:

- **Yedekleme dayanıklılık geliştirmeleri** -hello yedekleme dayanıklılığı artırmak düzeltmeleri bu sürüme sahip. Merhaba, önceki sürümler, yedeklemeler yalnızca belirli özel durumları için denenen. Bu sürümdeki tüm hello yedekleme özel durumlar yeniden dener ve yedeklemeleri daha esnektir yapar hello.

- **Depolama kullanımı izleme için güncelleştirmeleri** -30 Haziran 2017'dan başlayarak, StorSimple sanal cihaz seri Çekildi için depolama kullanımı izleme hello. Bu güncelleştirme 0,4 veya alt çalıştıran tüm hello sanal diziler grafiklerde izleme toohello geçerlidir. Bu güncelleştirme, toocontinue hello hello Azure portal izleme depolama alanı kullanımı için kullanılması gereken hello değişiklikleri içerir. Bu kritik güncelleştirmeyi 30 Haziran 2017 önce hello izleme özelliğini kullanarak toocontinue.


## <a name="issues-fixed-in-hello-update-05"></a>Merhaba güncelleştirme 0,5 giderilen sorunlar

Merhaba aşağıdaki tabloda bu sürümde giderilen sorunlar özetini sağlar.

| Hayır. | Özellik | Sorun |
| --- | --- | --- |
| 1 |Yedekleme dayanıklılık| Merhaba, önceki sürümler, yedeklemeler yalnızca belirli özel durumları için denenen. Bu sürüm, tüm hello yedekleme özel durumları denenerek daha esnek bir düzeltme toomake yedeklemeler içerir.|
| 2 |İzleme| Merhaba depolama kullanımı StorSimple sanal cihaz seri için izleme 30 Haziran 2017 başlayarak kullanım dışı kalacaktır. Bu eylemin hello StorSimple sanal diziler üzerinde çalışan hello StorSimple cihaz Yöneticisi hizmeti grafiklerde izleme etkiler (1200 modeli). Bu sürüm, 30 Haziran 2017 ötesinde hello sanal diziler üzerinde depolama kullanımı izleme hello kullanıcı toocontinue hello kullanılmasına izin güncelleştirme içerir.|
| 3 |Dosya sunucusu| Merhaba, önceki sürümlerde, bir kullanıcı şifrelenmiş dosyalar toohello sanal dizinin yanlışlıkla kopyalamak. Bu sürüm, şifrelenmiş dosyalar toovirtual dizisi kopyalama izin vermez bir düzeltme içerir. Cihazınızı güncelleştirmek, mevcut şifrelenmiş dosyaların önceki toohello varsa, tüm şifreli hello dosyaları hello sistemden silinene kadar yedeklemeler toofail devam eder. |


## <a name="known-issues-in-hello-update-05"></a>Merhaba güncelleştirme 0,5 bilinen sorunlar

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
| **8.** |Kapasite paylaşımlar için kullanılan |Görebileceğiniz hello paylaşımında hiçbir veri olduğunda tüketim paylaşın. Paylaşımlar için kullanılan hello kapasite meta veriler içerdiğinden bu tüketim ' dir. | |
| **9.** |Olağanüstü durum kurtarma |Yalnızca bir dosya sunucusu toohello hello olağanüstü durum kurtarma gerçekleştirebilirsiniz aynı etki alanında, hello kaynak aygıt. Olağanüstü durum kurtarma tooa hedef aygıt başka bir etki alanındaki bu sürümde desteklenmiyor. |Bu, bir sonraki sürümde uygulanır. Daha fazla bilgi için çok Git[, StorSimple sanal dizisi için yük devretme ve olağanüstü durum kurtarma](storsimple-virtual-array-failover-dr.md) |
| **10.** |Azure PowerShell |Merhaba StorSimple sanal cihazlar, bu sürümde hello Azure PowerShell aracılığıyla yönetilemez. |Merhaba sanal aygıtların tüm hello yönetim Azure portal ve hello yerel web kullanıcı Arabirimi hello yapılmalıdır. |
| **11.** |Parola değiştirme |Merhaba sanal dizinin cihaz konsoluna yalnızca tr girişinde kabul-bize biçimi klavye. | |
| **12.** |CHAP |CHAP kimlik oluşturulduktan sonra kaldırılamaz. Ayrıca, hello CHAP kimlik bilgilerini değiştirirseniz, tootake hello çevrimdışı birimler gerekir ve bunları çevrimiçi hello tootake değişikliğin için duruma getirin. |Bu sorunu sonraki bir sürümde değinilmiştir. |
| **13.** |iSCSI sunucusu |bir iSCSI birim için görüntülenen 'depolama kullanılan' hello hello StorSimple cihaz Yöneticisi hizmeti ve hello iSCSI konağının farklı olabilir. |Merhaba iSCSI konağının hello filesystem görünüme sahiptir.<br></br>Merhaba aygıt hello birim hello en büyük boyutta değiştirildiği ayrılan hello blok görür. |
| **14.** |Dosya sunucusu |Bir klasördeki bir dosyaya bir alternatif veri akışı (ilişkili ADS) varsa, hello ADS değil yedeklenemez veya olağanüstü durum kurtarma, kopyalama ve öğe düzeyinde Kurtarma geri. | |
| **15.** |Dosya sunucusu |Sembolik bağlantılar desteklenmez. | |
| **16.** |Dosya sunucusu |Dosyaları tarafından Windows şifreleme dosya sistemi (üzerinden kopyaladığınızda EFS) korumalı veya desteklenmeyen bir yapılandırmada StorSimple sanal dizinin dosya sunucusu sonucu hello üzerinde depolanan.  | |

## <a name="next-step"></a>Sonraki adım
[0,5 güncelleştirmesini](storsimple-virtual-array-install-update-05.md) , StorSimple sanal dizi.

## <a name="references"></a>Başvurular
Eski bir sürüm notu için mi arıyorsunuz? Şuraya gidin:

* [StorSimple sanal dizinin güncelleştirme 0,4 sürüm notları](storsimple-virtual-array-update-04-release-notes.md)
* [StorSimple sanal dizinin güncelleştirme 0,3 sürüm notları](storsimple-ova-update-03-release-notes.md)
* [StorSimple sanal dizinin güncelleştirme 0,1 ve 0.2 sürüm notları](storsimple-ova-update-01-release-notes.md)
* [StorSimple sanal dizinin genel kullanılabilirlik sürüm notları](storsimple-ova-pp-release-notes.md)

