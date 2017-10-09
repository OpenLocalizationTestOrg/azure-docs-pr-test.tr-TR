---
title: "Azure Mobile Engagement Android SDK aaaAdvanced yapılandırma"
description: "Gelişmiş yapılandırma seçenekleri Hello Azure Mobile Engagement Android SDK'sı Android derleme bildirimi de dahil olmak üzere hello açıklar"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 37d2c09a-86fa-473d-8987-c7e35a0eb3e8
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 10/04/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 757abf362021fd018f444cae6305524623e77062
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-configuration-for-azure-mobile-engagement-android-sdk"></a>Gelişmiş yapılandırma için Azure Mobile Engagement Android SDK
> [!div class="op_single_selector"]
> * [Evrensel Windows](mobile-engagement-windows-store-advanced-configuration.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
> * [iOS](mobile-engagement-ios-integrate-engagement.md)
> * [Android](mobile-engagement-android-advanced-configuration.md)
>
>

Bu yordam açıklar nasıl tooconfigure Azure Mobile Engagement Android uygulamaları için çeşitli yapılandırma seçenekleri.

## <a name="prerequisites"></a>Ön koşullar
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

## <a name="permission-requirements"></a>İzin gereksinimleri
Bazı seçenekler tümü burada başvuru ve satır içi hello belirli özelliği için listelenen belirli izinler gerektirir. Bu izinleri toohello projenizin AndroidManifest.xml hemen önce veya sonra hello eklemek `<application>` etiketi.

Merhaba izni kodu nereye hello uygun izni izleyen hello tablosundan doldurmanız hello aşağıdaki gibi toolook gerekir.

    <uses-permission android:name="android.permission.[specific permission]"/>


| İzin | Kullanıldığında |
| --- | --- |
| INTERNET |Gereklidir. Temel raporlama için |
| ACCESS_NETWORK_STATE |Gereklidir. Temel raporlama için |
| RECEIVE_BOOT_COMPLETED |Gereklidir. tooshow hello bildirimleri merkezi aygıt yeniden başlatma işleminden sonra |
| WAKE_LOCK |Önerilir. WiFi kullanırken veya ekran kapalı olduğunda verilerin toplanmasını sağlar |
| TİTRET |İsteğe bağlı. Bildirim alındığında titreşimi sağlar |
| DOWNLOAD_WITHOUT_NOTIFICATION |İsteğe bağlı. Android büyük resmi bildirim sağlar |
| WRITE_EXTERNAL_STORAGE |İsteğe bağlı. Android büyük resmi bildirim sağlar |
| ACCESS_COARSE_LOCATION |İsteğe bağlı. Gerçek zamanlı konum raporlama sağlar |
| ACCESS_FINE_LOCATION |İsteğe bağlı. GPS tabanlı konum raporlama sağlar |

Android M ile başlayan [bazı izinler çalışma zamanında yönetilen](mobile-engagement-android-location-reporting.md#android-m-permissions).

Zaten kullanıyorsanız, ``ACCESS_FINE_LOCATION``, sonra da tooalso gerekmeyen kullanmak ``ACCESS_COARSE_LOCATION``.

## <a name="android-manifest-configuration-options"></a>Android bildirim yapılandırma seçenekleri
### <a name="crash-report"></a>Kilitlenme raporu
toodisable kilitlenme rapor, bu kod hello arasında ekleme `<application>` ve `</application>` etiketler:

    <meta-data android:name="engagement:reportCrash" android:value="false"/>

### <a name="burst-threshold"></a>Eşik veri bloğu
Varsayılan olarak, hello katılım hizmet raporları gerçek zamanlı olarak günlüğe kaydeder. Uygulama rapor günlüklerinizi sık farklılık, daha iyi toobuffer hello günlükleri ve tooreport varsa, bunları ("modu veri bloğu" olarak adlandırılır) tümünü bir defada bir normal zaman temel üzerinde. toodo, bu nedenle, bu kod hello arasında ekleyin `<application>` ve `</application>` etiketler:

    <meta-data android:name="engagement:burstThreshold" android:value="{interval between too bursts (in milliseconds)}"/>

Veri bloğu modu biraz hello pil ömrünün artırır ancak Engagement İzleyicisi Merhaba üzerinde bir etkisi vardır: tüm oturumları ve işleri süresi yuvarlak toohello veri bloğu eşiği (Bu nedenle, oturumlar ve işleri hello veri bloğu eşik görünmeyebilir daha kısa) olan. Veri bloğu eşiği 30000 (30s) uzun olmalıdır.

### <a name="session-timeout"></a>Oturum zaman aşımı
 Bir etkinlik tarafından tuşuna basarak hello sonlandırabilirsiniz **giriş** veya **geri** telefonla ayarı hello boşta veya başka bir uygulamaya atlayarak anahtar. Varsayılan olarak, son etkinlik hello sonunda on saniye oturum sona erer. Bu görüntüyü oluşturan hello kullanıcı Çekmeleri bağlandığınızda durum denetler bildirim, vb. her zaman hello kullanıcı çıkar ve toohello uygulama hızla döner oturum bölme önler. Bu parametre toomodify isteyebilirsiniz. toodo, bu nedenle, bu kod hello arasında ekleyin `<application>` ve `</application>` etiketler:

    <meta-data android:name="engagement:sessionTimeout" android:value="{session timeout (in milliseconds)}"/>

## <a name="disable-log-reporting"></a>Günlük bildirimini devre dışı bırak
### <a name="using-a-method-call"></a>Yöntem çağrısı kullanma
Katılım toostop günlükleri göndermek istiyorsanız, çağırabilirsiniz:

    EngagementAgent.getInstance(context).setEnabled(false);

Bu çağrı kalıcıdır: paylaşılan tercihleri dosyasını kullanır.

Bu işlev çağırdığınızda katılım etkinse hello hizmet toostop bir dakika sürebilir. Ancak tüm hello hello hizmeti Merhaba uygulaması sonraki başlatışınızda başlatın olmaz.

Aynı işlevi ile Merhaba çağırarak yeniden raporlama günlüğü etkinleştirebilirsiniz `true`.

### <a name="integration-in-your-own-preferenceactivity"></a>Kendi tümleştirme`PreferenceActivity`
Bu işlevi çağırmak yerine, ayrıca bu ayarı doğrudan var olan tümleştirebilirsiniz `PreferenceActivity`.

Hello tercihlerinizi dosya (Merhaba istenen mod ile) katılım toouse yapılandırabilirsiniz `AndroidManifest.xml` ile dosya `application meta-data`:

* Merhaba `engagement:agent:settings:name` kullanılan toodefine hello hello paylaşılan tercihleri dosyasının adını bir anahtardır.
* Merhaba `engagement:agent:settings:mode` kullanılan toodefine hello modu hello paylaşılan tercihleri dosyasının bir anahtardır. Kullanım hello aynı modunda olarak, `PreferenceActivity`. bir sayı olarak Hello modu geçirildi: kodunuzda sabit bayrakları birlikte kullanıyorsanız, hello toplam değerini denetleyin.

Her zaman katılım kullanan hello `engagement:key` bu ayarı yönetmek için hello Tercihler dosyasındaki boolean anahtarı.

Merhaba örneği `AndroidManifest.xml` hello varsayılan değerleri gösterir:

    <application>
        [...]
        <meta-data
          android:name="engagement:agent:settings:name"
          android:value="engagement.agent" />
        <meta-data
          android:name="engagement:agent:settings:mode"
          android:value="0" />

Ekleyebileceğiniz sonra bir `CheckBoxPreference` hello bir aşağıdaki gibi tercih düzeninde:

    <CheckBoxPreference
      android:key="engagement:enabled"
      android:defaultValue="true"
      android:title="Use Engagement"
      android:summaryOn="Engagement is enabled."
      android:summaryOff="Engagement is disabled." />
