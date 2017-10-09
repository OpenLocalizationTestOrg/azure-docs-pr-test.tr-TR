---
title: "aaaStorSimple sanal dizinin güncelleştirmeleri sürüm notları | Microsoft Docs"
description: "Kritik açık açıklar sorunlar ve çözümleri hello StorSimple sanal dizinin çalışması için Update 0.3."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: b197651a-3c40-4185-b23d-4c8f22cfa8f4
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 09/15/2016
ms.author: alkohli
ms.openlocfilehash: 305e6419b248fde134abae65f3d2c241d72ffa18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-virtual-array-update-03-release-notes"></a>StorSimple sanal dizinin güncelleştirme 0,3 sürüm notları
## <a name="overview"></a>Genel Bakış
Merhaba aşağıdaki sürüm notları hello kritik açık sorunları belirlemek ve Microsoft Azure StorSimple sanal dizinin güncelleştirmeleri çözümlenen sorunları hello.

Merhaba sürüm notları sürekli olarak güncelleştirilir ve geçici bir çözüm gerektiren kritik sorunlar bulundukça olarak eklenir. StorSimple sanal dizinizi dağıtmadan önce hello Sürüm Notları'nda bulunan hello bilgileri dikkatle gözden geçirin.

Güncelleştirme 0.3 karşılık gelen toohello yazılım sürüm **10.0.10288.0**.

> [!NOTE]
> Güncelleştirmeleri dağıtıldığından ve aygıtınızı yeniden başlatın. G/ç sürüyor durumunda hello aygıt kapalı kalma süresi doğurur.
> 
> 

## <a name="whats-new-in-hello-update-03"></a>Merhaba güncelleştirme 0.3 yenilikler nelerdir?
Güncelleştirme 0.3 öncelikle bir hata düzeltmesi yapıdır. Bu sürümde, yedekleme hataları hello önceki sürümde sonuçta çeşitli hatalar giderilmiştir.

## <a name="issues-fixed-in-hello-update-03"></a>Merhaba güncelleştirme 0.3 giderilen sorunlar
Merhaba aşağıdaki tabloda bu sürümde giderilen sorunlar özetini sağlar.

| Hayır. | Özellik | Sorun |
| --- | --- | --- |
| 1 |Yedeklemeler |Bir sorun hello görülen burada hello yedeklemeler başarısız olurdu toocomplete bir dosya paylaşımı için önceki sürümü. Bu sorun oluşursa, hello yedekleme işi başarısız olur ve kritik uyarı hello StorSimple Yöneticisi hizmet toonotify hello kullanıcı oluşturuldu. Bu sorunu hello paylaşımlarında hello veri etkilemez veya toohello veri erişim. Merhaba kök nedeni tanımlanır ve bu sürümde sabit. <br></br> Merhaba düzeltme firmalarda geriye dönük zaten bu sorunu görüyorsunuz tooshares geçerli değildir. Bu sorunu görüyorsunuz müşteriler ilk güncelleştirme 0.3 uygulamak ve sonra Microsoft Support tooperform bir tam sistem yedekleme toofix hello sorunu başvurun. Microsoft Support iletişim yerine müşterileri de tooa yeni paylaşım etkilenen hello paylaşımları için iyi bir yedekten geri yükleyebilirsiniz. |
| 2 |iSCSI |Bir sorun hello görülen burada hello birimleri kayboluyor veri tooa hello StorSimple sanal dizinin birimde kopyalarken önceki sürüm. Bu sürümde bu sorun giderilmiştir. <br></br> Merhaba düzeltmeleri yalnızca birimleri yeni oluşturulan etkili. Merhaba düzeltmeleri firmalarda geriye dönük zaten bu sorunu görüyorsunuz toovolumes geçerli değildir. Müşterilerin toobring etkilenen hello birimleri çevrimiçi hello Klasik Azure Portalı aracılığıyla bu birimler için bir yedekleme gerçekleştirmek ve daha sonra bu birimleri toonew birimler geri önerilir. |

## <a name="known-issues-in-hello-update-03"></a>Merhaba güncelleştirme 0.3 bilinen sorunlar
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

## <a name="next-step"></a>Sonraki adım
[Güncelleştirme 0.3 yüklemek](storsimple-ova-install-update-01.md) , StorSimple sanal dizi.

## <a name="references"></a>Başvurular
Eski bir sürüm notu için mi arıyorsunuz? Şuraya gidin: 

* [StorSimple sanal dizinin güncelleştirme 0,1 ve 0.2 sürüm notları](storsimple-ova-update-01-release-notes.md)
* [StorSimple sanal dizinin genel kullanılabilirlik sürüm notları](storsimple-ova-pp-release-notes.md)

