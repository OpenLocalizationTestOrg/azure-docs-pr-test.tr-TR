---
title: "aaaAzure Mobile Engagement Android SDK tümleştirmesi"
description: "En son güncelleştirmeler ve yordamlar için Azure Mobile Engagement Android SDK"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a5487793-1a12-4f6c-a1cf-587c5a671e6b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 4f79936ea0fa6102023dec2b4682032a4a81fa9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-engagement-on-android"></a>Nasıl tooIntegrate android'de katılım
> [!div class="op_single_selector"]
> * [Windows Evrensel](mobile-engagement-windows-store-integrate-engagement.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
> * [iOS](mobile-engagement-ios-integrate-engagement.md)
> * [Android](mobile-engagement-android-integrate-engagement.md)
> 
> 

Bu yordam, hello en basit yolu tooactivate Engagement analizi ve izleme işlevlerine Android uygulamanızdaki açıklar.

> [!IMPORTANT]
> En düşük Android SDK API düzey 10 veya daha yüksek olmalıdır (Android 2.3.3 ya da daha yüksek).
> 
> 

Aşağıdaki adımları hello günlüklerinin yeterli tooactivates hello rapor kullanıcıları, oturumlar, etkinlikleri, kilitlenme ve Technicals ilgili tüm istatistikleri toocompute gerekli ' dir. Günlükler Hello rapor olaylar, hatalar ve işleri hello katılım API kullanarak el ile yapılmalıdır gibi bu toocompute diğer istatistiklerin gerekli (bkz [nasıl toouse hello Mobile Engagement, Android API etiketleme Gelişmiş](mobile-engagement-android-use-engagement-api.md) bu yana İstatistikleri uygulama bağımlı olan.

## <a name="embed-hello-engagement-sdk-and-service-into-your-android-project"></a>Merhaba Engagement SDK'sı ve hizmet Android projenize ekleme
İndirme hello Android SDK [burada](https://aka.ms/vq9mfn) almak `mobile-engagement-VERSION.jar` ve hello yerleştirin `libs` klasörü Android projenizin (henüz yoksa hello libs klasörüne oluşturma).

> [!IMPORTANT]
> Uygulama paketinizi ProGuard ile yapılandırdıysanız, bazı sınıfları tookeep gerekir. Yapılandırma parçacığını aşağıdaki hello kullanabilirsiniz:
> 
> -Ortak sınıfı tutmak * android.os.IInterface genişletir-sınıfı com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {tutun
> 
> <methods>; }
> 
> 

Merhaba Başlatıcısı etkinliğinde yöntemi aşağıdaki arama hello tarafından katılım bağlantı dizenizi belirtin:

            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
            EngagementAgent.getInstance(this).init(engagementConfiguration);

Merhaba bağlantı dizesi, uygulamanız için Azure portalında görüntülenir.

* Eksikse, aşağıdaki Android izinleri hello ekleyin (Merhaba önce `<application>` etiketi):
  
          <uses-permission android:name="android.permission.INTERNET"/>
          <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
* Ekle bölümden hello (Merhaba arasında `<application>` ve `</application>` etiketleri):
  
          <service
            android:name="com.microsoft.azure.engagement.service.EngagementService"
            android:exported="false"
            android:label="<Your application name>Service"
            android:process=":Engagement"/>
* Değişiklik `<Your application name>` uygulamanızın hello ada göre.

> [!TIP]
> Merhaba `android:label` özniteliği verir toochoose hello hello katılım hizmet adını toohello son kullanıcıların telefonlarını hello "Çalışan hizmetleri" ekranında görüneceğini. Bu tooset bu öznitelik çok önerilen`"<Your application name>Service"` (örneğin `"AcmeFunGameService"`).
> 
> 

Belirten hello `android:process` özniteliği sağlar, hello katılım hizmet (katılım aynı işlemi, uygulamanızın ana/kullanıcı Arabirimi iş parçacığı potansiyel olarak daha az yanıt yapacak şekilde hello çalıştıran) kendi işleminde çalışır.

> [!NOTE]
> Yerleştirdiğiniz içinde herhangi bir kod `Application.onCreate()` ve diğer uygulama geri aramalar hello katılım hizmeti dahil olmak üzere tüm uygulama işlemleri için çalışır. (Örneğin, gereksiz bellek ayırmaları ve hello Engagement'ın işlem, yinelenen yayın alıcıları veya hizmetleri iş parçacıkları) istenmeyen yan etkileri olabilir.
> 
> 

Geçersiz kılarsanız `Application.onCreate()`, önerilen tooadd hello aşağıdaki kod parçacığını hello başında olduğundan, `Application.onCreate()` işlevi:

             public void onCreate()
             {
               if (EngagementAgentUtils.isInDedicatedEngagementProcess(this))
                 return;

               ... Your code...
             }

Yapabileceğiniz hello aynı şeyi `Application.onTerminate()`, `Application.onLowMemory()` ve `Application.onConfigurationChanged(...)`.

Ayrıca genişletebilirsiniz `EngagementApplication` genişletme yerine `Application`: geri çağırma hello `Application.onCreate()` işlem denetimi ve çağrıları hello `Application.onApplicationProcessCreate()` hello geçerli işlem hello bir barındırma hello katılım hizmeti değil ise, hello aynı kuralları için yalnızca uygulama diğer geri aramalar hello.

## <a name="basic-reporting"></a>Temel raporlama
### <a name="recommended-method-overload-your-activity-classes"></a>Önerilen yöntem: aşırı yükleme, `Activity` sınıfları
Sipariş tooactivate hello raporunda katılım toocompute kullanıcıları, oturumlar, etkinlikleri, kilitlenme ve teknik istatistikleri gerekli tüm hello günlükler, yalnızca tüm toomake gerekir, `*Activity` alt sınıfları devral hello karşılık gelen `Engagement*Activity` sınıfları (örn, eski etkinlik geçerse `ListActivity`, onu genişletir yapma `EngagementListActivity`).

**Katılım:**

            package com.company.myapp;

            import android.app.Activity;
            import android.os.Bundle;

            public class MyApp extends Activity
            {
              @Override
              public void onCreate(Bundle savedInstanceState)
              {
                super.onCreate(savedInstanceState);
                setContentView(R.layout.main);
              }
            }

**Katılım ile:**

            package com.company.myapp;

            import com.microsoft.azure.engagement.activity.EngagementActivity;
            import android.os.Bundle;

            public class MyApp extends EngagementActivity
            {
              @Override
              public void onCreate(Bundle savedInstanceState)
              {
                super.onCreate(savedInstanceState);
                setContentView(R.layout.main);
              }
            }

> [!IMPORTANT]
> Kullanırken `EngagementListActivity` veya `EngagementExpandableListActivity`, emin olun herhangi bir çağrıda çok`requestWindowFeature(...);` hello çağrısından önce çok yapılan`super.onCreate(...);`, aksi takdirde bir kilitlenme meydana gelir.
> 
> 

Bu sınıfların hello bulabilirsiniz `src` klasörünü ve bunları projenize kopyalayabilirsiniz. Merhaba sınıflardır ayrıca hello **JavaDoc**.

### <a name="alternate-method-call-startactivity-and-endactivity-manually"></a>Alternatif yöntem: çağrı `startActivity()` ve `endActivity()` el ile
Olamaz ya da toooverload istiyor musunuz, `Activity` sınıfları, bunun yerine başlangıç ve çağırarak etkinliklerinizi bitiş `EngagementAgent`'s doğrudan yöntemleri.

> [!IMPORTANT]
> Merhaba Android SDK hiçbir zaman hello çağırır `endActivity()` Merhaba uygulaması kapalı olduğunda bile yöntemi (Android, uygulamaları gerçekte hiçbir zaman kapalı). Bu nedenle, olan *yüksek oranda* toocall hello önerilen `startActivity()` hello yönteminde `onResume` , geri çağırma *tüm* etkinlikleri ve hello `endActivity()` hello yönteminde `onPause()` geri arama, *tüm* etkinliklerinizi. Bu hello tek yolu toobe oturumları sızmaması emin olur. Bir oturum sızmasını varsa (bir oturum bekleyen olduğu sürece hello hizmet bağlı kalır bu yana) hello katılım hizmet hiçbir zaman hello katılım arka ucundan bağlantısını keser.
> 
> 

Örnek aşağıda verilmiştir:

            public class MyActivity extends Some3rdPartyActivity
            {
              @Override
              protected void onResume()
              {
                super.onResume();
                String activityNameOnEngagement = EngagementAgentUtils.buildEngagementActivityName(getClass()); // Uses short class name and removes "Activity" at hello end.
                EngagementAgent.getInstance(this).startActivity(this, activityNameOnEngagement, null);
              }

              @Override
              protected void onPause()
              {
                super.onPause();
                EngagementAgent.getInstance(this).endActivity();
              }
            }

Bu örnek çok benzer toohello `EngagementActivity` sınıfı ve kaynak kodu hello sağlanan türevleri `src` klasör.

## <a name="test"></a>Test etme
Şimdi bir öykünücü veya cihaz ve mobil uygulamanızı çalıştırarak ve hello İzleyici sekmesi oturum kayıtları doğrulanıyor Lütfen tümleştirmenize doğrulayın.

Merhaba sonraki bölümlerde isteğe bağlıdır.

## <a name="location-reporting"></a>Konum raporlama
Bildirilen konumları toobe istiyorsanız, birkaç satırlı yapılandırma tooadd gerekir (Merhaba arasında `<application>` ve `</application>` etiketleri).

### <a name="lazy-area-location-reporting"></a>Yavaş alan konumu raporlama
Yavaş alan konumu raporlama sağlar tooreport hello ülke, bölgeye ve yere göre ilişkili toodevices. Bu tür konumu raporlama yalnızca ağ konumlarını (hücre kimliği veya WIFI göre) kullanır. Merhaba aygıt alanına oturum başına en fazla bir kez bildirilir. Merhaba GPS hiçbir zaman kullanılmaz ve bu nedenle bu konumu rapor çok az türü (değil toosay yok) hello pil üzerindeki etkisi.

Kullanıcılar, oturumlar, olayları ve hataları ile ilgili kullanılan toocompute coğrafi istatistikleri bildirilen alanlarıdır. Reach kampanyaları ölçütü olarak de kullanılabilir.

tooenable yavaş alan konumu raporlama, bu yordamda daha önce bahsedilen hello yapılandırmayı kullanarak bunu yapabilirsiniz:

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setLazyAreaLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

Ayrıca izni eksikse aşağıdaki tooadd hello gerekir:

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

Veya kullanmaya devam edebileceğiniz ``ACCESS_FINE_LOCATION`` zaten uygulamanızda kullanın.

### <a name="real-time-location-reporting"></a>Gerçek zamanlı konum raporlama
Gerçek zamanlı konum raporlama sağlar tooreport hello enlem ve boylam ilişkili toodevices. Varsayılan olarak, bu tür konumu raporlama yalnızca ağ konumlarını (hücre kimliği veya WIFI göre) kullanır ve hello uygulama ön planda (yani oturumu sırasında) çalıştığında hello raporlama yalnızca etkindir.

Gerçek zamanlı konumlarının *değil* toocompute istatistikleri kullanılır. Yalnızca amaçlarına tooallow hello gerçek zamanlı coğrafi yalıtma kullanımıdır \<Reach-İzleyici-bölge sınırlaması\> Reach kampanyaları ölçütü.

tooenable gerçek zamanlı konum raporlama, bu yordamda daha önce bahsedilen hello yapılandırmayı kullanarak bunu yapabilirsiniz:

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

Ayrıca izni eksikse aşağıdaki tooadd hello gerekir:

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

Veya kullanmaya devam edebileceğiniz ``ACCESS_FINE_LOCATION`` zaten uygulamanızda kullanın.

#### <a name="gps-based-reporting"></a>Raporlama GPS dayalı
Varsayılan olarak, gerçek zamanlı konum raporlama ağ tabanlı konum yalnızca kullanır. GPS tooenable hello kullanımı (olan daha kesin) konumları tabanlı, hello yapılandırma nesnesi kullanın:

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setFineRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

Ayrıca izni eksikse aşağıdaki tooadd hello gerekir:

            <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>

#### <a name="background-reporting"></a>Arka plan raporlama
Merhaba uygulama ön planda (yani oturumu sırasında) çalıştırdığında, varsayılan olarak, gerçek zamanlı konum raporlama yalnızca etkindir. Merhaba tooenable raporlama arka planda de hello yapılandırma nesnesi:

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setBackgroundRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

> [!NOTE]
> Merhaba uygulaması arka planda çalıştığında, ağ tabanlı konumlar sadece bildirilir, etkinleştirilmiş olsa bile GPS hello.
> 
> 

Merhaba kullanıcı, cihaz yeniden başlatılırsa hello arka plan konum rapor durdurulur, önyükleme sırasında otomatik olarak yeniden bu toomake ekleyebilirsiniz:

            <receiver android:name="com.microsoft.azure.engagement.EngagementLocationBootReceiver"
               android:exported="false">
               <intent-filter>
                  <action android:name="android.intent.action.BOOT_COMPLETED" />
               </intent-filter>
            </receiver>

Ayrıca izni eksikse aşağıdaki tooadd hello gerekir:

            <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />

### <a name="android-m-permissions"></a>Android M izinleri
Android M ile başlayarak, bazı izinler çalışma zamanında yönetilir ve kullanıcı onayı gerekiyor.

Android API düzeyi 23 hedefliyorsanız hello çalışma zamanı izinleri yeni uygulama yüklemeleri için varsayılan olarak kapatılır. Aksi takdirde, varsayılan olarak açılır.

Merhaba kullanıcı etkinleştirebilir/hello aygıt ayarları menüsünden bu izinleri devre dışı bırakabilir. Arka plan işlemleri hello uygulamasının sistem menüsünden izinleri kapatma devre dışı bırakır, bu bir sistem davranıştır ve yeteneği tooreceive itme arka planda üzerinde hiçbir etkisi olmaz.

Mobile Engagement Hello bağlamında, çalışma zamanında onayı iste hello izinler şunlardır:

* `ACCESS_COARSE_LOCATION`
* `ACCESS_FINE_LOCATION`
* `WRITE_EXTERNAL_STORAGE`(yalnızca Android API düzeyini 23 bunu hedeflerken)

Merhaba harici depolama yalnızca ulaşma büyük resmi özelliği için kullanılır. Görürseniz yalnızca Mobile Engagement ancak büyük resmi özelliği devre dışı bırakma hello maliyetle kullandıysanız kullanıcılar kesintiye uğratan bu izni toobe isteyen, kaldırabilirsiniz.

Başlangıç konumu özellikler için standart sistem iletişim kutusunu kullanarak izinleri toouser istemeniz gerekir. Merhaba kullanıcı onaylarsa, tootell gerek ``EngagementAgent`` tootake hesaba (Aksi hello değişiklik işlenen hello sonraki zamanı hello kullanıcı başlatır hello uygulaması olacaktır) gerçek zamanlı değiştirin.

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
         * Request location permission, but this won't explain why it is needed toohello user.
         * hello standard Android documentation explains with more details how toodisplay a rationale activity tooexplain hello user why hello permission is needed in your application.
         * Putting COARSE vs FINE has no impact here, they are part of hello same group for runtime permission management.
         */
        if (checkSelfPermission(android.Manifest.permission.ACCESS_FINE_LOCATION) != PackageManager.PERMISSION_GRANTED)
          requestPermissions(new String[] { android.Manifest.permission.ACCESS_FINE_LOCATION }, 0);

        /* Only if you want tookeep features using external storage */
        if (checkSelfPermission(android.Manifest.permission.WRITE_EXTERNAL_STORAGE) != PackageManager.PERMISSION_GRANTED)
          requestPermissions(new String[] { android.Manifest.permission.WRITE_EXTERNAL_STORAGE }, 1);
      }
    }

    @Override
    public void onRequestPermissionsResult(int requestCode, String[] permissions, int[] grantResults)
    {
      /* Only a positive location permission update requires engagement agent refresh, hence hello request code matching from above function */
      if (requestCode == 0 && grantResults[0] == PackageManager.PERMISSION_GRANTED)
        getEngagementAgent().refreshPermissions();
    }

## <a name="advanced-reporting"></a>Gelişmiş raporlama
Tooreport uygulama belirli olaylar, hatalar ve işleri istiyorsanız, isteğe bağlı olarak, hello hello yöntemleri aracılığıyla toouse hello katılım API gerekir `EngagementAgent` sınıfı. Bu sınıfın bir nesnesi arama hello tarafından alınma olabilir `EngagementAgent.getInstance()` statik yöntemi.

Merhaba katılım API toouse tüm Engagement'ın gelişmiş özelliklerinden sağlar ve hello nasıl ayrıntılı tooUse android'de katılım API (Merhaba teknik belgelerine hello gibi yanı `EngagementAgent` sınıfı).

## <a name="advanced-configuration-in-androidmanifestxml"></a>Gelişmiş yapılandırmasında (AndroidManifest.xml)
### <a name="wake-locks"></a>Uyandırma kilitleri
Toobe istatistikleri Wifi kullanırken gerçek zamanlı veya Merhaba ekranında kapalıyken gönderildiğinden emin istiyorsanız, isteğe bağlı izni aşağıdaki hello ekleyin:

            <uses-permission android:name="android.permission.WAKE_LOCK"/>

### <a name="crash-report"></a>Kilitlenme raporu
Toodisable kilitlenme raporları istiyorsanız, bu ekleyin (Merhaba arasında `<application>` ve `</application>` etiketleri):

            <meta-data android:name="engagement:reportCrash" android:value="false"/>

### <a name="burst-threshold"></a>Eşik veri bloğu
Varsayılan olarak, hello katılım hizmet raporları gerçek zamanlı olarak günlüğe kaydeder. Uygulamanızı günlükleri çok sık raporları, daha iyi toobuffer hello günlükleri ve tooreport varsa, bunları (Merhaba "veri bloğu modu" denir) tümünü bir defada bir normal zaman temel üzerinde. toodo bu nedenle, ekleyin bu (Merhaba arasında `<application>` ve `</application>` etiketleri):

            <meta-data android:name="engagement:burstThreshold" android:value="{interval between too bursts (in milliseconds)}"/>

Merhaba veri bloğu modu biraz artırmak hello pil ömrü ancak Engagement İzleyicisi Merhaba üzerinde bir etkisi vardır: tüm oturumları ve işleri süresi yuvarlak toohello veri bloğu eşiği (Bu nedenle, oturumlar ve işleri hello veri bloğu eşik görünmeyebilir daha kısa) olacaktır. Bu bir veri bloğu eşikten artık 30000 (30s) toouse önerilir.

### <a name="session-timeout"></a>Oturum zaman aşımı
Varsayılan olarak (genellikle giriş tuşuna basarak hello tarafından oluşur veya telefonla ayarı hello boşta veya başka bir uygulamaya atlayarak anahtarı yedekleme), son etkinliklerine hello bitişinden sonra sona erdi 10'luk bir oturum değil. Tooavoid (ki çekme bir görüntüyü oluşturan bağlandığınızda durum kontrol edebilirsiniz bir bildirim, vs.) her zaman hello kullanıcı çıkmak ve toohello uygulama çok hızlı bir şekilde dönmek oturum bölme budur. Bu parametre toomodify isteyebilirsiniz. toodo bu nedenle, ekleyin bu (Merhaba arasında `<application>` ve `</application>` etiketleri):

            <meta-data android:name="engagement:sessionTimeout" android:value="{session timeout (in milliseconds)}"/>

## <a name="disable-log-reporting"></a>Günlük bildirimini devre dışı bırak
### <a name="using-a-method-call"></a>Yöntem çağrısı kullanma
Katılım toostop günlükleri göndermek istiyorsanız, çağırabilirsiniz:

            EngagementAgent.getInstance(context).setEnabled(false);

Bu çağrı kalıcıdır: paylaşılan tercihleri dosyasını kullanır.

Katılım etkin değilse, bu işlev çağırdığınızda hello hizmet toostop için 1 dakika sürebilir. Ancak tüm hello hello hizmeti Merhaba uygulaması sonraki başlatışınızda başlatın olmaz.

Aynı işlevi ile Merhaba çağırarak yeniden raporlama günlüğü etkinleştirebilirsiniz `true`.

### <a name="integration-in-your-own-preferenceactivity"></a>Kendi tümleştirme`PreferenceActivity`
Bu işlevi çağırmak yerine, ayrıca bu ayarı doğrudan var olan tümleştirebilirsiniz `PreferenceActivity`.

Hello tercihlerinizi dosya (Merhaba istenen mod ile) katılım toouse yapılandırabilirsiniz `AndroidManifest.xml` ile dosya `application meta-data`:

* Merhaba `engagement:agent:settings:name` kullanılan toodefine hello hello paylaşılan tercihleri dosyasının adını bir anahtardır.
* Merhaba `engagement:agent:settings:mode` anahtar kullanılan toodefine hello modu hello paylaşılan tercihleri dosyasının, hello kullanması gereken aynı modunda olarak, `PreferenceActivity`. bir sayı olarak Hello modu geçirildi: kodunuzda sabit bayrakları birlikte kullanıyorsanız, hello toplam değerini denetleyin.

Her zaman engagement kullanmayı hello `engagement:key` bu ayarı yönetmek için hello Tercihler dosyasındaki boolean anahtarı.

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

<!-- URLs. -->
[Device API]: http://go.microsoft.com/?linkid=9876094
