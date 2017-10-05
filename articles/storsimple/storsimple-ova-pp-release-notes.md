---
title: "StorSimple sanal dizinin sürüm notları | Microsoft Docs"
description: "StorSimple sanal dizi için açık kritik sorunlar ve çözümleri açıklar."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 84908160-2b8b-4f4f-a674-f39aaa0bd4de
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 05/13/2016
ms.author: alkohli
ms.openlocfilehash: f3ea83e32af4de2637d12766ee8c51adfbf0d3a3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="storsimple-virtual-array-release-notes"></a>StorSimple sanal dizinin sürüm notları
## <a name="overview"></a>Genel Bakış
Aşağıdaki sürüm notları Microsoft Azure StorSimple sanal dizinin (şirket içi StorSimple sanal cihazı veya StorSimple sanal cihazı olarak da bilinir) Mart 2016 genel kullanılabilirlik (GA) sürümü için önemli açık sorunlar tanımlayın. Bu sürüm 10.0.10271.0 yazılım sürümüne karşılık gelir.

Sürüm Notları sürekli olarak güncelleştirilir ve geçici bir çözüm gerektiren kritik sorunlar bulundukça olarak eklenir. StorSimple sanal Cihazınızı dağıtmadan önce dikkatle Sürüm Notları'nda yer alan bilgileri gözden geçirin. 

Aşağıdaki tabloda bu sürümdeki bilinen sorunlara özetini sağlar.

| Hayır. | Özellik | Sorun | Geçici çözüm/açıklamaları |
| --- | --- | --- | --- |
| **1.** |Güncellemeler |Önizleme sürümünde oluşturulan sanal cihazlar için desteklenen bir genel kullanılabilirlik sürümü güncelleştirilemiyor. |Bu sanal cihazlar üzerinden bir olağanüstü durum kurtarma (DR) iş akışı kullanarak genel kullanılabilirlik sürümü için başarısız gerekir. |
| **2.** |Sağlanan veri diski |Belirli bir belirtilen boyutta bir veri diski sağlamış ve karşılık gelen StorSimple sanal cihaz oluşturulan, gerekir değil genişletin veya veri diski küçültmeye sonra. Bunu yapmak çalışırken cihaz yerel katmanlarda tüm verilerin kaybıyla sonuçlanır. | |
| **3.** |Grup İlkesi |Bir cihaz etki alanına katılmış olduğunda, bir Grup İlkesi uygulama aygıt işlemi olumsuz etkileyebilir. |Sanal dizinizi kendi kuruluş biriminde (OU) için Active Directory ve hiçbir Grup İlkesi nesneleri (GPO) için uygulanan olduğundan emin olun. |
| **4.** |Yerel web kullanıcı Arabirimi |Internet Explorer (IE ESC) Artırılmış güvenlik özellikleri etkinleştirilirse, sorun giderme veya bakım gibi bazı yerel web kullanıcı Arabirimi sayfalarını düzgün çalışmayabilir. Bu sayfaları düğmeleri de çalışmayabilir. |Internet Explorer Artırılmış güvenlik özelliklerini kapatın. |
| **5.** |Yerel web kullanıcı Arabirimi |Bir Hyper-V sanal makine ağ kullanıcı Arabirimi olarak 10 görüntülenen Web Gbps arabirimleri. |Hyper-V yansımasını davranıştır. Hyper-V sanal ağ bağdaştırıcıları için 10 GB/sn her zaman gösterir. |
| **6.** |Katmanlı birimler veya paylaşımlar |Katmanlı birimlerin desteklenmiyor StorSimple ile çalışan uygulamalar için kilitleme bayt aralığı. Bayt aralığı kilitleme etkinse, StorSimple katmanlama çalışmaz. |Önerilen ölçüleri içerir: <br></br>Uygulama mantığınızın kilitleme bayt aralığı kapatın.<br></br>Yerel olarak sabitlenmiş birimlerin katmanlı birimleri aksine bu uygulama için veri koymak seçin.<br></br>*Uyarı*: kullanarak yerel olarak sabitlenmiş birimleri ve bayt aralığı kilitleme etkinse, geri yükleme tamamlamadan önce yerel olarak sabitlenmiş birimin çevrimiçi olabileceğini unutmayın. Bir geri yükleme devam ediyor, böyle durumlarda, daha sonra tamamlamak geri yüklemek için beklemeniz gerekir. |
| **7.** |Katmanlı paylaşımları |Büyük dosyaları ile çalışma yavaş katmanı genişletmek neden olabilir. |Büyük dosyaları ile çalışırken en büyük dosya paylaşımı boyutunu %3 küçüktür öneririz. |
| **8.** |Kapasite paylaşımlar için kullanılan |Görebileceğiniz paylaşmak paylaşımındaki herhangi bir veri olmadığında tüketiminin. Paylaşımlar için kullanılan kapasitesi meta veriler içerdiğinden budur. | |
| **9.** |Olağanüstü durum kurtarma |Yalnızca bir dosya sunucusu aynı etki alanında, kaynak cihaz için olağanüstü durum kurtarma gerçekleştirebilirsiniz. Başka bir etki alanındaki bir hedef cihaz için olağanüstü durum kurtarma, bu sürümde desteklenmiyor. |Bu, bir sonraki sürümde uygulanacaktır. |
| **10.** |Azure PowerShell |StorSimple sanal cihazlar, bu sürümde Azure PowerShell aracılığıyla yönetilemez. |Klasik Azure portalı ve yerel web kullanıcı Arabirimi sanal aygıtların tüm yönetim yapılması gerekir. |
| **11.** |Parola değiştirme |Sanal dizinin aygıt konsolu yalnızca en-US klavye biçiminde giriş kabul eder. | |
| **12.** |CHAP |CHAP kimlik oluşturulduktan sonra kaldırılamaz. Ayrıca, CHAP kimlik bilgilerini değiştirirseniz, birimlerin çevrimdışına alın ve ardından çevrimiçi bunları değişikliğin etkili olması çevrimiçine gerekir. |Bunlar daha sonraki bir sürümde ele alınacaktır. |
| **13.** |iSCSI sunucusu |' Depolama birimi için iSCSI biriminde görüntülenen kullanılan' StorSimple Yöneticisi hizmeti ve iSCSI konağının farklı olabilir. |İSCSI konağının filesystem görünüme sahiptir.<br></br>Cihaz en büyük boyutta birimi olduğu zaman ayrılan blok görür. |

