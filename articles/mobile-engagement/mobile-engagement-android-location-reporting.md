---
title: "aaaLocation için Azure Mobile Engagement Android SDK raporlama"
description: "Açıklar nasıl Azure Mobile Engagement Android SDK için raporlama tooconfigure konumu"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 6cab5ed1-b767-46ac-9f0b-48a4e249d88c
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/12/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: c2cb097df2a77bee2d56ffe9509dc116548db408
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="location-reporting-for-azure-mobile-engagement-android-sdk"></a>Azure Mobile Engagement Android SDK'sı için raporlama konumu
> [!div class="op_single_selector"]
> * [Android](mobile-engagement-android-integrate-engagement.md)
> 
> 

Bu konuda açıklanmaktadır nasıl Android uygulamanız için raporlama toodo konumu.

## <a name="prerequisites"></a>Ön koşullar
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

## <a name="location-reporting"></a>Konum raporlama
Bildirilen konumları toobe istiyorsanız, birkaç satırlı yapılandırma tooadd gerekir (Merhaba arasında `<application>` ve `</application>` etiketleri).

### <a name="lazy-area-location-reporting"></a>Yavaş alan konumu raporlama
Yavaş alan konumu raporlama raporlama hello ülke, bölgeye ve yere göre cihazlarla ilişkilendirilmiş sağlar. Bu tür konumu raporlama yalnızca ağ konumlarını (hücre kimliği veya WIFI göre) kullanır. Merhaba aygıt alanına oturum başına en fazla bir kez bildirilir. Hello GPS hiçbir zaman kullanılmaz ve bu nedenle bu konumu rapor düşük etkisi hello pilde türü.

Kullanıcılar, oturumlar, olayları ve hataları ile ilgili kullanılan toocompute coğrafi istatistikleri bildirilen alanlarıdır. Reach kampanyaları ölçütü olarak de kullanılabilir.

Bu yordamda daha önce bahsedilen hello yapılandırmayı kullanarak raporlama yavaş alan konumu etkinleştirin:

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setLazyAreaLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

Ayrıca toospecify bir konuma izni gerekir. Bu kodu kullanır ``COARSE`` izin:

    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

Uygulamanızı gerektiriyorsa, kullanabileceğiniz ``ACCESS_FINE_LOCATION`` yerine.

### <a name="real-time-location-reporting"></a>Gerçek zamanlı konum raporlama
Gerçek zamanlı konum raporlama raporlama hello enlem ve boylam cihazlarla ilişkilendirilmiş sağlar. Varsayılan olarak, bu tür konumu raporlama yalnızca hücre kimliği veya WIFI göre ağ konumlarını kullanır. Merhaba raporlama Hello uygulama ön planda (örneğin, bir oturum sırasında) çalıştığında etkindir.

Gerçek zamanlı konumlarının *değil* toocompute istatistikleri kullanılır. Yalnızca amaçlarına tooallow hello gerçek zamanlı coğrafi yalıtma kullanımıdır \<Reach-İzleyici-bölge sınırlaması\> Reach kampanyaları ölçütü.

tooenable gerçek zamanlı konum raporlama, bir satır ekleyin kod toowhere hello Başlatıcısı etkinliğinde hello katılım bağlantı dizesini ayarlayın. Merhaba sonuç hello aşağıdaki gibi görünür:

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

        You also need toospecify a location permission. This code uses ``COARSE`` permission:

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

        If your app requires it, you can use ``ACCESS_FINE_LOCATION`` instead.

#### <a name="gps-based-reporting"></a>Raporlama GPS dayalı
Varsayılan olarak, gerçek zamanlı konum raporlama ağ tabanlı konum yalnızca kullanır. daha kesin, GPS tabanlı konumların tooenable hello kullanım hello yapılandırma nesnesi kullanın:

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setFineRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

Ayrıca izni eksikse aşağıdaki tooadd hello gerekir:

    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>

#### <a name="background-reporting"></a>Arka plan raporlama
Merhaba uygulama ön planda (örneğin, bir oturum sırasında) çalıştırdığında, varsayılan olarak, gerçek zamanlı konum raporlama yalnızca etkindir. aynı zamanda arka planda raporlama tooenable hello bu yapılandırma nesnesini kullanın:

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setBackgroundRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

> [!NOTE]
> Merhaba uygulaması arka planda çalıştığında, yalnızca ağ tabanlı konumlar bildirilir, etkinleştirilmiş olsa bile GPS hello.
> 
> 

Merhaba kullanıcı cihazını yeniden başlatılırsa, hello arka plan konum rapor durdurulur. önyükleme sırasında otomatik olarak yeniden toomake bu kodu ekleyin.

    <receiver android:name="com.microsoft.azure.engagement.EngagementLocationBootReceiver"
           android:exported="false">
        <intent-filter>
            <action android:name="android.intent.action.BOOT_COMPLETED" />
        </intent-filter>
    </receiver>

Ayrıca izni eksikse aşağıdaki tooadd hello gerekir:

    <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />

## <a name="android-m-permissions"></a>Android M izinleri
Android M ile başlayarak, bazı izinler çalışma zamanında yönetilir ve kullanıcı onayı gerekir.

Android API düzeyi 23 hedefliyorsanız, hello çalışma zamanı izinleri yeni uygulama yüklemeleri için varsayılan olarak kapalıdır. Aksi halde bunlar varsayılan olarak etkinleştirilir.

Etkinleştirebilir/hello aygıt ayarları menüsünden bu izinleri devre dışı bırakabilir. İzinleri hello sistem menüsünden kapatma sistem davranıştır ve yeteneği tooreceive itme arka planda üzerinde hiçbir etkisi olmaz hello uygulamanın hello arka plan işlemleri sonlandırır.

Mobile Engagement konumu raporlama Hello bağlamında, çalışma zamanında onayı iste hello izinler şunlardır:

* `ACCESS_COARSE_LOCATION`
* `ACCESS_FINE_LOCATION`

İzinleri standart sistem iletişim kutusunu kullanarak hello kullanıcıdan isteyin. Merhaba kullanıcı onaylarsa, söyleyin ``EngagementAgent`` gerçek zamanlı hesaba değiştirmek tootake. Aksi takdirde hello değişiklik işlenen hello sonraki zaman hello kullanıcı başlatır hello uygulamasıdır.

Burada ise bir kod örnek toouse uygulama toorequest izinleri ve iletme hello sonuç bir etkinlikte pozitif çok``EngagementAgent``:

    @Override
    public void onCreate(Bundle savedInstanceState)
    {
      /* Other code... */

      /* Request permissions */
      requestPermissions();
    }

    @TargetApi(Build.VERSION_CODES.M)
    private void requestPermissions()
    {
      /* Avoid crashing if not on Android M */
      if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.M)
      {
        /*
         * Request location permission, but this doesn't explain why it is needed toohello user.
         * hello standard Android documentation explains with more details how toodisplay a rationale activity tooexplain hello user why hello permission is needed in your application.
         * Putting COARSE vs FINE has no impact here, they are part of hello same group for runtime permission management.
         */
        if (checkSelfPermission(android.Manifest.permission.ACCESS_FINE_LOCATION) != PackageManager.PERMISSION_GRANTED)
          requestPermissions(new String[] { android.Manifest.permission.ACCESS_FINE_LOCATION }, 0);

      }
    }

    @Override
    public void onRequestPermissionsResult(int requestCode, String[] permissions, int[] grantResults)
    {
      /* Only a positive location permission update requires engagement agent refresh, hence hello request code matching from above function */
      if (requestCode == 0 && grantResults[0] == PackageManager.PERMISSION_GRANTED)
        getEngagementAgent().refreshPermissions();
    }
