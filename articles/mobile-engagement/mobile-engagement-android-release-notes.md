---
title: "aaaAzure Mobile Engagement Android SDK tümleştirmesi"
description: "En son güncelleştirmeler ve yordamlar için Azure Mobile Engagement Android SDK"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 585341f9-3f39-459a-af42-864e400a0128
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 07/17/2017
ms.author: piyushjo
ms.openlocfilehash: 16b098198674c49567d720d0c01d984cb763ed8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="release-notes"></a>Sürüm notları

## <a name="431-07172017"></a>4.3.1 (07/17/2017)
* Çağrılırken nadiren bir kilitlenme düzeltme `EngagementAgentUtils.isInDedicatedEngagementProcess`, ayrıca hello tarafından kullanılan `EngagementApplication` sınıfı.

## <a name="430-06272017"></a>4.3.0 (06/27/2017)
* Android 8 desteği (SDK'sı üzerinde Android 8 çalışmaz hello önceki sürümler).
* Daha fazla hiçbir bağımlılık destek kitaplığı.
* Kaldırma `EngagementFragmentActivity` sınıfı.
* Son çok[arka plan yürütme sınırları](https://developer.android.com/preview/features/background.html) hello kullanıcı hello aygıt ile etkileşim kadar arka planda günlükleri Android 8'de Gecikmeli, bu bir itme kampanya etkileyecek **teslim edildi** ve **Sistem bildirimi görüntülenir** hello Aygıt uyku durumunda erteleniyor istatistikleri (Merhaba bildirim görüntülenmeye devam eder, halka ve gerçek zamanlı sorun olmadan Titret).
* Son çok[arka plan konum sınırları](https://developer.android.com/preview/features/background-location-limits.html), arka planda hello gerçek zamanlı konum güncelleştirilmeyecek sık üzerinde Android 8.

## <a name="424-03302017"></a>4.2.4 (03/30/2017)
* Uygulama içi bildirim Android 7 toobe metin renkleri aynı eski Android sürümler olarak hello düzeltin.

## <a name="423-08102016"></a>4.2.3 (08/10/2016)
* Daha fazla WIFI kilit yok.
* Init (hata 4.2.0 içinde sunulan) önce getDeviceId çağrılırken bir kilitlenme düzeltin.

## <a name="422-05172016"></a>4.2.2 (05/17/2016)
* İstikrara yönelik iyileştirmeler.

## <a name="421-05102016"></a>4.2.1 (05/10/2016)
* Güvenlik: web görünümü yerel dosya erişimini devre dışı bırakın.
* Güvenliği: kaldırma `EngagementPreferenceActivity` artık kullanılmayan ve güvenli olmayan genişleten sınıf `PreferenceActivity` sınıfı.
* Güvenlik: etkinliklerdir şimdi ulaşma toouse belgelenen `exported="false"`, bu bayrak, önceki SDK sürümlerinde kullanılabilir.

## <a name="420-03112016"></a>4.2.0 (03/11/2016)
* Merhaba SDK şimdi MIT altında lisanslanmıştır.
* Bir özel cihaz tanımlayıcısı SDK başlatma zamanında belirtmeye izin.

## <a name="415-02012016"></a>4.1.5 (02/01/2016)
* İstikrara yönelik iyileştirmeler.

## <a name="414-01262016"></a>4.1.4 (01/26/2016)
* İstikrara yönelik iyileştirmeler.

## <a name="413-1292015"></a>4.1.3 (12/9/2015)
* İstikrara yönelik iyileştirmeler.

## <a name="412-11252015"></a>4.1.2 (11/25/2015)
* İstikrara yönelik iyileştirmeler.

## <a name="411-11042015"></a>4.1.1 (11/04/2015)
* İstikrara yönelik iyileştirmeler.

## <a name="410-08252015"></a>4.1.0 (08/25/2015)
* Yeni izni modeli için Android M işleyin.
* Yerine çalışma zamanında konumu özellikleri artık yapılandırabilirsiniz `AndroidManifest.xml`.
* Bir izin hatayı düzeltmek: kullanırsanız `ACCESS_FINE_LOCATION`, ardından `ACCESS_COARSE_LOCATION` artık gerekli değildir.
* İstikrara yönelik iyileştirmeler.

## <a name="400-07062015"></a>4.0.0 (07/06/2015)
* İç protokol toomake analizler ve anında iletme daha güvenilir değiştirir.
* İtme kampanya herhangi bir türde hello yerel gönderim kimlik bilgilerini yapılandırmak için yerel gönderim (GCM/ADM) şimdi de için uygulama içi Bildirimlerde kullanılır.
* Büyük resim bildirim düzeltin: gönderilen sonra görüntülenen yalnızca 10'luk oldukları.
* Web görünümünde bir hatayı düzeltmek: bir bağlantıyı tıklatmak olduğu da yürütülürken hello varsayılan eylem URL'si.
* Nadir çökmeyle düzeltme ilgili toolocal Depolama Yönetimi.
* Dinamik yapılandırma dizesi yönetim düzeltin.
* EULA güncelleştirin.

## <a name="300-02172015"></a>3.0.0 (02/17/2015)
* Azure Mobile Engagement ilk sürümünü
* AppID yapılandırma bağlantı dizesini yapılandırma tarafından değiştirilir.
* Rastgele XMPP varlıklardan rasgele XMPP ileti alıp API toosend kaldırıldı.
* Cihazlar arasında ileti alıp API toosend kaldırıldı.
* Güvenlik geliştirmeleri.
* Google Play ve SmartAd izleme kaldırıldı.

