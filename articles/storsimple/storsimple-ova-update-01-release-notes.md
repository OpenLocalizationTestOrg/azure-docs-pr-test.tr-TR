---
title: "aaaStorSimple sanal dizinin güncelleştirmeleri sürüm notları | Microsoft Docs"
description: "Açık kritik sorunlar ve çözümleri hello StorSimple sanal dizi için açıklar güncelleştirme 0.2 ve 0,1 çalışıyor."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 3993864d-2ddd-4302-a2f1-8d737fba6eab
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/16/2016
ms.author: alkohli
ms.openlocfilehash: dfd38890feeb667c95134f2adbb35ce2df165620
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-virtual-array-update-02-and-01-release-notes"></a>StorSimple sanal dizinin güncelleştirme 0.2 ve 0,1 sürüm notları
## <a name="overview"></a>Genel Bakış
Merhaba aşağıdaki sürüm notları hello kritik açık sorunları belirlemek ve Microsoft Azure StorSimple sanal dizinin güncelleştirmeleri çözümlenen sorunları hello. (Microsoft Azure StorSimple sanal olarak da bilinir hello StorSimple şirket içi sanal cihazı veya hello StorSimple sanal cihazı dizidir.) 

Merhaba sürüm notları sürekli olarak güncelleştirilir ve geçici bir çözüm gerektiren kritik sorunlar bulundukça olarak eklenir. StorSimple sanal Cihazınızı dağıtmadan önce hello Sürüm Notları'nda bulunan hello bilgileri dikkatle gözden geçirin.

Güncelleştirme 0.2 karşılık gelen toohello yazılım sürüm **10.0.10280.0**; Güncelleştirme 0.1 olduğu sürüm **10.0.10279.0**. Aşağıdaki Hello bölümler, her bir güncelleştirme hello değişir. 

> [!NOTE]
> Güncelleştirmeleri dağıtıldığından ve aygıtınızı yeniden başlatılır. G/ç sürüyor durumunda hello aygıt kapalı kalma süresi uygulanabilir.
> 
> 

## <a name="issues-fixed-in-hello-update-02"></a>Merhaba güncelleştirme 0.2 giderilen sorunlar
Güncelleştirme 0.2, aşağıdaki tablonun hello açıklanan ek toohello düzeltme güncelleştirme 0.1 tüm değişiklikleri içerir:

| Özellik | Sorun |
| --- | --- |
| Güncelleştirmeler |Yerel Web kullanıcı arabirimini tooinstall güncelleştirmeleri hello toouse vardı şekilde hello son sürümde, güncelleştirmeleri otomatik olarak hello Klasik Azure portalı algılanan doğru. Bu sürümde bu sorun düzeltilmiştir. Güncelleştirme 0.2 yükledikten sonra gelecekteki güncelleştirmeleri hello Klasik Azure portalı kullanarak yükleyebilirsiniz. |

## <a name="whats-new-in-hello-update-01"></a>Merhaba güncelleştirme 0.1 yenilikler nelerdir?
Güncelleştirme 0.1 hello aşağıdakileri içeren hata düzeltmeleri ve geliştirmeleri. 

* **Bulut kesintiler için geliştirilmiş dayanıklılık**: Bu sürüm çeşitli hata düzeltmeleri olağanüstü durum kurtarma, yedekleme, geri yükleme ve bir bulut bağlantı kesintisi hello olayda katmanlama çevresinde sahiptir. 
* **Geliştirilmiş geri yükleme performansı**: hello geri yükleme işlerinin tamamlanma süresini hello önemli ölçüde Kes hata düzeltmeleri bu sürüme sahip.
* **Alan geri kazanma iyileştirme otomatik**: veri ölçülü kaynak kullanan birimlerde silindiğinde, hello kullanılmamış depolama blokları iadesi toobe gerekir. Bu sürüm hello kullanılmayan kaynaklanan hello buluttan geliştirilmiş hello alan geri kazanma işlemin olma kullanılabilir daha hızlı olarak karşılaştırılan toohello önceki sürümler alanı vardır.
* **Yeni sanal disk görüntüleri**: yeni VHD ve VHDX VMDK şimdi hello Klasik Azure portalı kullanılabilir. Bu görüntüleri tooprovision yeni güncelleştirme 0.1 cihazlar indirebilirsiniz.
* **İş durumunu hello portalında Hello doğruluğu artırma**: hello yazılım, iş durumunu hello Portalı'nda raporlama önceki sürümünü ayrıntılı değildi. Bu sorun, bu sürümde çözümlenir.
* **Etki alanına katılım deneyimi**: hata düzeltmeleri ilgili toodomain birleştirme ve hello aygıtı yeniden adlandırılıyor.

## <a name="issues-fixed-in-hello-update-01"></a>Merhaba güncelleştirme 0.1 giderilen sorunlar
Merhaba aşağıdaki tabloda bu sürümde giderilen sorunlar özetini sağlar.

| Hayır. | Özellik | Sorun |
| --- | --- | --- |
| 1 |VMDK |Bazı VMware sürümleri hello işletim sistemi diski seyrek uyarıya neden ve normal işlemlerin kesintiye olarak görüldü. Bu, bu sürümde giderilmiştir. |
| 2 |iSCSI sunucusu |Merhaba son sürümde hello kullanıcı gerekli toospecify her etkin ağ arabiriminin, StorSimple sanal cihazınız için bir ağ geçidi oluştu. Böylece Hello kullanıcının sahip tooconfigure Bu davranış bu sürümde değiştirildi tüm etkin hello ağ arabirimleri için en az bir ağ geçidi. |
| 3 |Destek Paketi |İçinde yazılım önceki sürümünü Merhaba, paket koleksiyonu hello paket boyutu 1 GB'den büyük olduğunda başarısız destekler. Bu sürümde bu sorun düzeltilmiştir. |
| 4 |Bulut erişimi |Merhaba StorSimple sanal dizinin ağ bağlantısı yok ve yeniden başlatıldı hello son sürümde hello yerel UI bağlantı sorunları gerekir. Bu sürümde bu sorun düzeltilmiştir. |
| 5 |İzleme grafikleri |Bir aygıt yük devretme aşağıdaki hello önceki sürümde hello bulut kapasite kullanımı grafikleri hello Klasik Azure portalı yanlış değerleri görüntülenir. Bu hello geçerli sürümde düzeltilmiştir. |

## <a name="known-issues-in-hello-update-01"></a>Merhaba güncelleştirme 0.1 bilinen sorunlar
Merhaba aşağıdaki tabloda StorSimple sanal dizinin hello için bilinen sorunlar özetini sağlar ve hello sorunları hello önceki sürümlerden yayın-not ettiğiniz içerir. **Merhaba bu sürümde not ettiğiniz yayımlanan sorunlar işaretlenir yıldızla. Bu listedeki neredeyse tüm hello sorunları StorSimple sanal dizinin hello GA sürümü devreden.**

| Hayır. | Özellik | Sorun | Geçici çözüm/açıklamaları |
| --- | --- | --- | --- |
| **1.** |Güncelleştirmeler |Merhaba Önizleme sürümünde oluşturulan hello sanal aygıt desteklenen güncelleştirilmiş tooa genel kullanılabilirlik sürümü olamaz. |Bu sanal cihazlar Merhaba olağanüstü durum kurtarma (DR) iş akışını kullanarak genel kullanılabilirlik sürümü devredilir gerekir. |
| **2.** |Sağlanan veri diski |Belirli bir belirtilen boyutta bir veri diski kez sağlamış ve hello karşılık gelen StorSimple sanal cihaz oluşturulan, gerekir değil genişletin veya hello veri diski küçültmeye. Toodo çalışırken şekilde hello yerel katmanlarında hello cihazın tüm hello veri kaybına neden olur. | |
| **3.** |Grup İlkesi |Bir cihaz etki alanına katılmış olduğunda, bir Grup İlkesi uygulama hello aygıt işlemi olumsuz etkileyebilir. |Active Directory için kendi kuruluş biriminde (OU) sanal dizinizi olduğundan ve hiçbir Grup İlkesi nesneleri (GPO) uygulanan tooit olduğundan emin olun. |
| **4.** |Yerel web kullanıcı Arabirimi |Internet Explorer (IE ESC) Artırılmış güvenlik özellikleri etkinleştirilirse, sorun giderme veya bakım gibi bazı yerel web kullanıcı Arabirimi sayfalarını düzgün çalışmayabilir. Bu sayfaları düğmeleri de çalışmayabilir. |Internet Explorer Artırılmış güvenlik özelliklerini kapatın. |
| **5.** |Yerel web kullanıcı Arabirimi |Bir Hyper-V sanal makine ağ arabirimleri hello Web kullanıcı Arabirimi 10 GB/sn arabirimleri görüntülenen hello. |Hyper-V yansımasını davranıştır. Hyper-V sanal ağ bağdaştırıcıları için 10 GB/sn her zaman gösterir. |
| **6.** |Katmanlı birimler veya paylaşımlar |Bayt aralığı, katmanlı birimleri StorSimple hello ile çalışan uygulamalar için kilitleme desteklenmiyor. Bayt aralığı kilitleme etkinse, StorSimple katmanlama çalışmaz. |Önerilen ölçüleri içerir: <br></br>Uygulama mantığınızın kilitleme bayt aralığı kapatın.<br></br>Bu uygulama için tooput verileri yerel olarak sabitlenmiş birimleri olarak karşılıklı tootiered birimleri seçin.<br></br>*Uyarı*: kullanarak yerel olarak sabitlenmiş birimleri ve bayt aralığı kilitleme etkinse, hatta hello geri yükleme tamamlanmadan önce hello yerel olarak sabitlenmiş birimin çevrimiçi olabileceğini unutmayın. Bir geri yükleme devam ediyor, böyle durumlarda, ardından hello geri yükleme toocomplete için beklemeniz gerekir. |
| **7.** |Katmanlı paylaşımları |Büyük dosyaları ile çalışma yavaş katmanı genişletmek neden olabilir. |Büyük dosyaları ile çalışırken, o hello en büyük dosya hello paylaşım boyutu %3 küçük öneririz. |
| **8.** |Kapasite paylaşımlar için kullanılan |Görebileceğiniz tüketim hello paylaşımında herhangi bir veri hello yokluğu paylaşım. Paylaşımlar için kullanılan hello kapasite meta veriler içerdiğinden budur. | |
| **9.** |Olağanüstü durum kurtarma |Yalnızca bir dosya sunucusu toohello hello olağanüstü durum kurtarma gerçekleştirebilirsiniz aynı etki alanında, hello kaynak aygıt. Olağanüstü durum kurtarma tooa hedef aygıt başka bir etki alanındaki bu sürümde desteklenmiyor. |Bu, bir sonraki sürümde uygulanacaktır. |
| **10.** |Azure PowerShell |Merhaba StorSimple sanal cihazlar, bu sürümde hello Azure PowerShell aracılığıyla yönetilemez. |Tüm hello yönetim hello sanal cihazların Merhaba Klasik Azure portalı ve hello yerel web kullanıcı Arabirimi aracılığıyla yapılmalıdır. |
| **11.** |Parola değiştirme |Merhaba sanal dizinin aygıt konsolu yalnızca en-US klavye biçiminde giriş kabul eder. | |
| **12.** |CHAP |CHAP kimlik oluşturulduktan sonra kaldırılamaz. Ayrıca, hello CHAP kimlik bilgilerini değiştirirseniz, tootake hello çevrimdışı birimler gerekir ve bunları çevrimiçi hello tootake değişikliğin için duruma getirmeden. |Bunlar daha sonraki bir sürümde ele alınacaktır. |
| **13.** |iSCSI sunucusu |bir iSCSI birim için görüntülenen 'depolama kullanılan' hello hello StorSimple Yöneticisi hizmetiniz ve hello iSCSI konağının farklı olabilir. |Merhaba iSCSI konağının hello filesystem görünüme sahiptir.<br></br>Merhaba aygıt hello birim hello en büyük boyutta değiştirildiği ayrılan hello blok görür. |
| **14.** |Dosya sunucusu * |Bir klasördeki bir dosyaya bir alternatif veri akışı (ilişkili ADS) varsa, hello ADS değil yedeklenemez veya olağanüstü durum kurtarma, kopyalama ve öğe düzeyinde Kurtarma geri. | |

## <a name="next-step"></a>Sonraki adım
[Güncelleştirmeleri yüklemek](storsimple-ova-install-update-01.md) , StorSimple sanal dizi.

