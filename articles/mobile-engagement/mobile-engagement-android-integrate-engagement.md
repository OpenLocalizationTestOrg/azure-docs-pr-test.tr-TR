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
# <a name="how-toointegrate-engagement-on-android"></a><span data-ttu-id="45840-103">Nasıl tooIntegrate android'de katılım</span><span class="sxs-lookup"><span data-stu-id="45840-103">How tooIntegrate Engagement on Android</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="45840-104">Windows Evrensel</span><span class="sxs-lookup"><span data-stu-id="45840-104">Windows Universal</span></span>](mobile-engagement-windows-store-integrate-engagement.md)
> * [<span data-ttu-id="45840-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="45840-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="45840-106">iOS</span><span class="sxs-lookup"><span data-stu-id="45840-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="45840-107">Android</span><span class="sxs-lookup"><span data-stu-id="45840-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md)
> 
> 

<span data-ttu-id="45840-108">Bu yordam, hello en basit yolu tooactivate Engagement analizi ve izleme işlevlerine Android uygulamanızdaki açıklar.</span><span class="sxs-lookup"><span data-stu-id="45840-108">This procedure describes hello simplest way tooactivate Engagement's Analytics and Monitoring functions in your Android application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="45840-109">En düşük Android SDK API düzey 10 veya daha yüksek olmalıdır (Android 2.3.3 ya da daha yüksek).</span><span class="sxs-lookup"><span data-stu-id="45840-109">Your minimum Android SDK API level must be 10 or higher (Android 2.3.3 or higher).</span></span>
> 
> 

<span data-ttu-id="45840-110">Aşağıdaki adımları hello günlüklerinin yeterli tooactivates hello rapor kullanıcıları, oturumlar, etkinlikleri, kilitlenme ve Technicals ilgili tüm istatistikleri toocompute gerekli ' dir.</span><span class="sxs-lookup"><span data-stu-id="45840-110">hello following steps are enough tooactivates hello report of logs needed toocompute all statistics regarding Users, Sessions, Activities, Crashes and Technicals.</span></span> <span data-ttu-id="45840-111">Günlükler Hello rapor olaylar, hatalar ve işleri hello katılım API kullanarak el ile yapılmalıdır gibi bu toocompute diğer istatistiklerin gerekli (bkz [nasıl toouse hello Mobile Engagement, Android API etiketleme Gelişmiş](mobile-engagement-android-use-engagement-api.md) bu yana İstatistikleri uygulama bağımlı olan.</span><span class="sxs-lookup"><span data-stu-id="45840-111">hello report of logs needed toocompute other statistics like Events, Errors and Jobs must be done manually using hello Engagement API (see [How toouse hello advanced Mobile Engagement tagging API in your Android](mobile-engagement-android-use-engagement-api.md) since these statistics are application dependent.</span></span>

## <a name="embed-hello-engagement-sdk-and-service-into-your-android-project"></a><span data-ttu-id="45840-112">Merhaba Engagement SDK'sı ve hizmet Android projenize ekleme</span><span class="sxs-lookup"><span data-stu-id="45840-112">Embed hello Engagement SDK and service into your Android project</span></span>
<span data-ttu-id="45840-113">İndirme hello Android SDK [burada](https://aka.ms/vq9mfn) almak `mobile-engagement-VERSION.jar` ve hello yerleştirin `libs` klasörü Android projenizin (henüz yoksa hello libs klasörüne oluşturma).</span><span class="sxs-lookup"><span data-stu-id="45840-113">Download hello Android SDK from [here](https://aka.ms/vq9mfn) Get `mobile-engagement-VERSION.jar` and put them into hello `libs` folder of your Android project (create hello libs folder if it does not exist yet).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="45840-114">Uygulama paketinizi ProGuard ile yapılandırdıysanız, bazı sınıfları tookeep gerekir.</span><span class="sxs-lookup"><span data-stu-id="45840-114">If you build your application package with ProGuard, you need tookeep some classes.</span></span> <span data-ttu-id="45840-115">Yapılandırma parçacığını aşağıdaki hello kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="45840-115">You can use hello following configuration snippet:</span></span>
> 
> <span data-ttu-id="45840-116">-Ortak sınıfı tutmak * android.os.IInterface genişletir-sınıfı com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {tutun</span><span class="sxs-lookup"><span data-stu-id="45840-116">-keep public class * extends android.os.IInterface -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {</span></span>
> 
> <span data-ttu-id="45840-117"><methods>; }</span><span class="sxs-lookup"><span data-stu-id="45840-117"><methods>; }</span></span>
> 
> 

<span data-ttu-id="45840-118">Merhaba Başlatıcısı etkinliğinde yöntemi aşağıdaki arama hello tarafından katılım bağlantı dizenizi belirtin:</span><span class="sxs-lookup"><span data-stu-id="45840-118">Specify your Engagement connection string by calling hello following method in hello launcher activity:</span></span>

            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
            EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="45840-119">Merhaba bağlantı dizesi, uygulamanız için Azure portalında görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="45840-119">hello connection string for your application is displayed on Azure Portal.</span></span>

* <span data-ttu-id="45840-120">Eksikse, aşağıdaki Android izinleri hello ekleyin (Merhaba önce `<application>` etiketi):</span><span class="sxs-lookup"><span data-stu-id="45840-120">If missing, add hello following Android permissions (before hello `<application>` tag):</span></span>
  
          <uses-permission android:name="android.permission.INTERNET"/>
          <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
* <span data-ttu-id="45840-121">Ekle bölümden hello (Merhaba arasında `<application>` ve `</application>` etiketleri):</span><span class="sxs-lookup"><span data-stu-id="45840-121">Add hello following section (between hello `<application>` and `</application>` tags):</span></span>
  
          <service
            android:name="com.microsoft.azure.engagement.service.EngagementService"
            android:exported="false"
            android:label="<Your application name>Service"
            android:process=":Engagement"/>
* <span data-ttu-id="45840-122">Değişiklik `<Your application name>` uygulamanızın hello ada göre.</span><span class="sxs-lookup"><span data-stu-id="45840-122">Change `<Your application name>` by hello name of your application.</span></span>

> [!TIP]
> <span data-ttu-id="45840-123">Merhaba `android:label` özniteliği verir toochoose hello hello katılım hizmet adını toohello son kullanıcıların telefonlarını hello "Çalışan hizmetleri" ekranında görüneceğini.</span><span class="sxs-lookup"><span data-stu-id="45840-123">hello `android:label` attribute allows you toochoose hello name of hello Engagement service as it will appear toohello end-users in hello "Running services" screen of their phone.</span></span> <span data-ttu-id="45840-124">Bu tooset bu öznitelik çok önerilen`"<Your application name>Service"` (örneğin `"AcmeFunGameService"`).</span><span class="sxs-lookup"><span data-stu-id="45840-124">It is recommended tooset this attribute too`"<Your application name>Service"` (e.g. `"AcmeFunGameService"`).</span></span>
> 
> 

<span data-ttu-id="45840-125">Belirten hello `android:process` özniteliği sağlar, hello katılım hizmet (katılım aynı işlemi, uygulamanızın ana/kullanıcı Arabirimi iş parçacığı potansiyel olarak daha az yanıt yapacak şekilde hello çalıştıran) kendi işleminde çalışır.</span><span class="sxs-lookup"><span data-stu-id="45840-125">Specifying hello `android:process` attribute ensures that hello Engagement service will run in its own process (running Engagement in hello same process as your application will make your main/UI thread potentially less responsive).</span></span>

> [!NOTE]
> <span data-ttu-id="45840-126">Yerleştirdiğiniz içinde herhangi bir kod `Application.onCreate()` ve diğer uygulama geri aramalar hello katılım hizmeti dahil olmak üzere tüm uygulama işlemleri için çalışır.</span><span class="sxs-lookup"><span data-stu-id="45840-126">Any code you place in `Application.onCreate()` and other application callbacks will be run for all your application's processes, including hello Engagement service.</span></span> <span data-ttu-id="45840-127">(Örneğin, gereksiz bellek ayırmaları ve hello Engagement'ın işlem, yinelenen yayın alıcıları veya hizmetleri iş parçacıkları) istenmeyen yan etkileri olabilir.</span><span class="sxs-lookup"><span data-stu-id="45840-127">It may have unwanted side effects (like unneeded memory allocations and threads in hello Engagement's process, duplicate broadcast receivers or services).</span></span>
> 
> 

<span data-ttu-id="45840-128">Geçersiz kılarsanız `Application.onCreate()`, önerilen tooadd hello aşağıdaki kod parçacığını hello başında olduğundan, `Application.onCreate()` işlevi:</span><span class="sxs-lookup"><span data-stu-id="45840-128">If you override `Application.onCreate()`, it's recommended tooadd hello following code snippet at hello beginning of your `Application.onCreate()` function:</span></span>

             public void onCreate()
             {
               if (EngagementAgentUtils.isInDedicatedEngagementProcess(this))
                 return;

               ... Your code...
             }

<span data-ttu-id="45840-129">Yapabileceğiniz hello aynı şeyi `Application.onTerminate()`, `Application.onLowMemory()` ve `Application.onConfigurationChanged(...)`.</span><span class="sxs-lookup"><span data-stu-id="45840-129">You can do hello same thing for `Application.onTerminate()`, `Application.onLowMemory()` and `Application.onConfigurationChanged(...)`.</span></span>

<span data-ttu-id="45840-130">Ayrıca genişletebilirsiniz `EngagementApplication` genişletme yerine `Application`: geri çağırma hello `Application.onCreate()` işlem denetimi ve çağrıları hello `Application.onApplicationProcessCreate()` hello geçerli işlem hello bir barındırma hello katılım hizmeti değil ise, hello aynı kuralları için yalnızca uygulama diğer geri aramalar hello.</span><span class="sxs-lookup"><span data-stu-id="45840-130">You can also extend `EngagementApplication` instead of extending `Application`: hello callback `Application.onCreate()` does hello process check and calls `Application.onApplicationProcessCreate()` only if hello current process is not hello one hosting hello Engagement service, hello same rules apply for hello other callbacks.</span></span>

## <a name="basic-reporting"></a><span data-ttu-id="45840-131">Temel raporlama</span><span class="sxs-lookup"><span data-stu-id="45840-131">Basic reporting</span></span>
### <a name="recommended-method-overload-your-activity-classes"></a><span data-ttu-id="45840-132">Önerilen yöntem: aşırı yükleme, `Activity` sınıfları</span><span class="sxs-lookup"><span data-stu-id="45840-132">Recommended method: overload your `Activity` classes</span></span>
<span data-ttu-id="45840-133">Sipariş tooactivate hello raporunda katılım toocompute kullanıcıları, oturumlar, etkinlikleri, kilitlenme ve teknik istatistikleri gerekli tüm hello günlükler, yalnızca tüm toomake gerekir, `*Activity` alt sınıfları devral hello karşılık gelen `Engagement*Activity` sınıfları (örn, eski etkinlik geçerse `ListActivity`, onu genişletir yapma `EngagementListActivity`).</span><span class="sxs-lookup"><span data-stu-id="45840-133">In order tooactivate hello report of all hello logs required by Engagement toocompute Users, Sessions, Activities, Crashes and Technical statistics, you just have toomake all your `*Activity` sub-classes inherit from hello corresponding `Engagement*Activity` classes (e.g. if your legacy activity extends `ListActivity`, make it extends `EngagementListActivity`).</span></span>

<span data-ttu-id="45840-134">**Katılım:**</span><span class="sxs-lookup"><span data-stu-id="45840-134">**Without Engagement :**</span></span>

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

<span data-ttu-id="45840-135">**Katılım ile:**</span><span class="sxs-lookup"><span data-stu-id="45840-135">**With Engagement :**</span></span>

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
> <span data-ttu-id="45840-136">Kullanırken `EngagementListActivity` veya `EngagementExpandableListActivity`, emin olun herhangi bir çağrıda çok`requestWindowFeature(...);` hello çağrısından önce çok yapılan`super.onCreate(...);`, aksi takdirde bir kilitlenme meydana gelir.</span><span class="sxs-lookup"><span data-stu-id="45840-136">When using `EngagementListActivity` or `EngagementExpandableListActivity`, make sure any call too`requestWindowFeature(...);` is made before hello call too`super.onCreate(...);`, otherwise a crash will occur.</span></span>
> 
> 

<span data-ttu-id="45840-137">Bu sınıfların hello bulabilirsiniz `src` klasörünü ve bunları projenize kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="45840-137">You can find these classes in hello `src` folder, and can copy them into your project.</span></span> <span data-ttu-id="45840-138">Merhaba sınıflardır ayrıca hello **JavaDoc**.</span><span class="sxs-lookup"><span data-stu-id="45840-138">hello classes are also in hello **JavaDoc**.</span></span>

### <a name="alternate-method-call-startactivity-and-endactivity-manually"></a><span data-ttu-id="45840-139">Alternatif yöntem: çağrı `startActivity()` ve `endActivity()` el ile</span><span class="sxs-lookup"><span data-stu-id="45840-139">Alternate method: call `startActivity()` and `endActivity()` manually</span></span>
<span data-ttu-id="45840-140">Olamaz ya da toooverload istiyor musunuz, `Activity` sınıfları, bunun yerine başlangıç ve çağırarak etkinliklerinizi bitiş `EngagementAgent`'s doğrudan yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="45840-140">If you cannot or do not want toooverload your `Activity` classes, you can instead start and end your activities by calling `EngagementAgent`'s methods directly.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="45840-141">Merhaba Android SDK hiçbir zaman hello çağırır `endActivity()` Merhaba uygulaması kapalı olduğunda bile yöntemi (Android, uygulamaları gerçekte hiçbir zaman kapalı).</span><span class="sxs-lookup"><span data-stu-id="45840-141">hello Android SDK never calls hello `endActivity()` method, even when hello application is closed (on Android, applications are actually never closed).</span></span> <span data-ttu-id="45840-142">Bu nedenle, olan *yüksek oranda* toocall hello önerilen `startActivity()` hello yönteminde `onResume` , geri çağırma *tüm* etkinlikleri ve hello `endActivity()` hello yönteminde `onPause()` geri arama, *tüm* etkinliklerinizi.</span><span class="sxs-lookup"><span data-stu-id="45840-142">Thus, it is *HIGHLY* recommended toocall hello `startActivity()` method in hello `onResume` callback of *ALL* your activities, and hello `endActivity()` method in hello `onPause()` callback of *ALL* your activities.</span></span> <span data-ttu-id="45840-143">Bu hello tek yolu toobe oturumları sızmaması emin olur.</span><span class="sxs-lookup"><span data-stu-id="45840-143">This is hello only way toobe sure that sessions will not be leaked.</span></span> <span data-ttu-id="45840-144">Bir oturum sızmasını varsa (bir oturum bekleyen olduğu sürece hello hizmet bağlı kalır bu yana) hello katılım hizmet hiçbir zaman hello katılım arka ucundan bağlantısını keser.</span><span class="sxs-lookup"><span data-stu-id="45840-144">If a session is leaked, hello Engagement service will never disconnect from hello Engagement backend (since hello service stays connected as long as a session is pending).</span></span>
> 
> 

<span data-ttu-id="45840-145">Örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="45840-145">Here is an example:</span></span>

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

<span data-ttu-id="45840-146">Bu örnek çok benzer toohello `EngagementActivity` sınıfı ve kaynak kodu hello sağlanan türevleri `src` klasör.</span><span class="sxs-lookup"><span data-stu-id="45840-146">This example very similiar toohello `EngagementActivity` class and its variants, whose source code is provided in hello `src` folder.</span></span>

## <a name="test"></a><span data-ttu-id="45840-147">Test etme</span><span class="sxs-lookup"><span data-stu-id="45840-147">Test</span></span>
<span data-ttu-id="45840-148">Şimdi bir öykünücü veya cihaz ve mobil uygulamanızı çalıştırarak ve hello İzleyici sekmesi oturum kayıtları doğrulanıyor Lütfen tümleştirmenize doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="45840-148">Now please verify your integration by running your mobile app in an emulator or device and verifying that it registers a session on hello Monitor tab.</span></span>

<span data-ttu-id="45840-149">Merhaba sonraki bölümlerde isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="45840-149">hello next sections are optional.</span></span>

## <a name="location-reporting"></a><span data-ttu-id="45840-150">Konum raporlama</span><span class="sxs-lookup"><span data-stu-id="45840-150">Location reporting</span></span>
<span data-ttu-id="45840-151">Bildirilen konumları toobe istiyorsanız, birkaç satırlı yapılandırma tooadd gerekir (Merhaba arasında `<application>` ve `</application>` etiketleri).</span><span class="sxs-lookup"><span data-stu-id="45840-151">If you want locations toobe reported, you need tooadd a few lines of configuration (between hello `<application>` and `</application>` tags).</span></span>

### <a name="lazy-area-location-reporting"></a><span data-ttu-id="45840-152">Yavaş alan konumu raporlama</span><span class="sxs-lookup"><span data-stu-id="45840-152">Lazy area location reporting</span></span>
<span data-ttu-id="45840-153">Yavaş alan konumu raporlama sağlar tooreport hello ülke, bölgeye ve yere göre ilişkili toodevices.</span><span class="sxs-lookup"><span data-stu-id="45840-153">Lazy area location reporting allows tooreport hello country, region and locality associated toodevices.</span></span> <span data-ttu-id="45840-154">Bu tür konumu raporlama yalnızca ağ konumlarını (hücre kimliği veya WIFI göre) kullanır.</span><span class="sxs-lookup"><span data-stu-id="45840-154">This type of location reporting only uses network locations (based on Cell ID or WIFI).</span></span> <span data-ttu-id="45840-155">Merhaba aygıt alanına oturum başına en fazla bir kez bildirilir.</span><span class="sxs-lookup"><span data-stu-id="45840-155">hello device area is reported at most once per session.</span></span> <span data-ttu-id="45840-156">Merhaba GPS hiçbir zaman kullanılmaz ve bu nedenle bu konumu rapor çok az türü (değil toosay yok) hello pil üzerindeki etkisi.</span><span class="sxs-lookup"><span data-stu-id="45840-156">hello GPS is never used, and thus this type of location report has very few (not toosay no) impact on hello battery.</span></span>

<span data-ttu-id="45840-157">Kullanıcılar, oturumlar, olayları ve hataları ile ilgili kullanılan toocompute coğrafi istatistikleri bildirilen alanlarıdır.</span><span class="sxs-lookup"><span data-stu-id="45840-157">Reported areas are used toocompute geographic statistics about users, sessions, events and errors.</span></span> <span data-ttu-id="45840-158">Reach kampanyaları ölçütü olarak de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="45840-158">They can also be used as criterion in Reach campaigns.</span></span>

<span data-ttu-id="45840-159">tooenable yavaş alan konumu raporlama, bu yordamda daha önce bahsedilen hello yapılandırmayı kullanarak bunu yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="45840-159">tooenable lazy area location reporting, you can do it by using hello configuration previously mentioned in this procedure :</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setLazyAreaLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="45840-160">Ayrıca izni eksikse aşağıdaki tooadd hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="45840-160">You also need tooadd hello following permission if missing:</span></span>

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

<span data-ttu-id="45840-161">Veya kullanmaya devam edebileceğiniz ``ACCESS_FINE_LOCATION`` zaten uygulamanızda kullanın.</span><span class="sxs-lookup"><span data-stu-id="45840-161">Or you can keep using ``ACCESS_FINE_LOCATION`` if you already use it in your application.</span></span>

### <a name="real-time-location-reporting"></a><span data-ttu-id="45840-162">Gerçek zamanlı konum raporlama</span><span class="sxs-lookup"><span data-stu-id="45840-162">Real time location reporting</span></span>
<span data-ttu-id="45840-163">Gerçek zamanlı konum raporlama sağlar tooreport hello enlem ve boylam ilişkili toodevices.</span><span class="sxs-lookup"><span data-stu-id="45840-163">Real time location reporting allows tooreport hello latitude and longitude associated toodevices.</span></span> <span data-ttu-id="45840-164">Varsayılan olarak, bu tür konumu raporlama yalnızca ağ konumlarını (hücre kimliği veya WIFI göre) kullanır ve hello uygulama ön planda (yani oturumu sırasında) çalıştığında hello raporlama yalnızca etkindir.</span><span class="sxs-lookup"><span data-stu-id="45840-164">By default, this type of location reporting only uses network locations (based on Cell ID or WIFI), and hello reporting is only active when hello application runs in foreground (i.e. during a session).</span></span>

<span data-ttu-id="45840-165">Gerçek zamanlı konumlarının *değil* toocompute istatistikleri kullanılır.</span><span class="sxs-lookup"><span data-stu-id="45840-165">Real time locations are *NOT* used toocompute statistics.</span></span> <span data-ttu-id="45840-166">Yalnızca amaçlarına tooallow hello gerçek zamanlı coğrafi yalıtma kullanımıdır \<Reach-İzleyici-bölge sınırlaması\> Reach kampanyaları ölçütü.</span><span class="sxs-lookup"><span data-stu-id="45840-166">Their only purpose is tooallow hello use of real time geo-fencing \<Reach-Audience-geofencing\> criterion in Reach campaigns.</span></span>

<span data-ttu-id="45840-167">tooenable gerçek zamanlı konum raporlama, bu yordamda daha önce bahsedilen hello yapılandırmayı kullanarak bunu yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="45840-167">tooenable real time location reporting, you can do it by using hello configuration previously mentioned in this procedure :</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="45840-168">Ayrıca izni eksikse aşağıdaki tooadd hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="45840-168">You also need tooadd hello following permission if missing:</span></span>

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

<span data-ttu-id="45840-169">Veya kullanmaya devam edebileceğiniz ``ACCESS_FINE_LOCATION`` zaten uygulamanızda kullanın.</span><span class="sxs-lookup"><span data-stu-id="45840-169">Or you can keep using ``ACCESS_FINE_LOCATION`` if you already use it in your application.</span></span>

#### <a name="gps-based-reporting"></a><span data-ttu-id="45840-170">Raporlama GPS dayalı</span><span class="sxs-lookup"><span data-stu-id="45840-170">GPS based reporting</span></span>
<span data-ttu-id="45840-171">Varsayılan olarak, gerçek zamanlı konum raporlama ağ tabanlı konum yalnızca kullanır.</span><span class="sxs-lookup"><span data-stu-id="45840-171">By default, real time location reporting only uses network based locations.</span></span> <span data-ttu-id="45840-172">GPS tooenable hello kullanımı (olan daha kesin) konumları tabanlı, hello yapılandırma nesnesi kullanın:</span><span class="sxs-lookup"><span data-stu-id="45840-172">tooenable hello use of GPS based locations (which are far more precise), use hello configuration object:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setFineRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="45840-173">Ayrıca izni eksikse aşağıdaki tooadd hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="45840-173">You also need tooadd hello following permission if missing:</span></span>

            <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>

#### <a name="background-reporting"></a><span data-ttu-id="45840-174">Arka plan raporlama</span><span class="sxs-lookup"><span data-stu-id="45840-174">Background reporting</span></span>
<span data-ttu-id="45840-175">Merhaba uygulama ön planda (yani oturumu sırasında) çalıştırdığında, varsayılan olarak, gerçek zamanlı konum raporlama yalnızca etkindir.</span><span class="sxs-lookup"><span data-stu-id="45840-175">By default, real time location reporting is only active when hello application runs in foreground (i.e. during a session).</span></span> <span data-ttu-id="45840-176">Merhaba tooenable raporlama arka planda de hello yapılandırma nesnesi:</span><span class="sxs-lookup"><span data-stu-id="45840-176">tooenable hello reporting also in background, use hello configuration object:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setBackgroundRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

> [!NOTE]
> <span data-ttu-id="45840-177">Merhaba uygulaması arka planda çalıştığında, ağ tabanlı konumlar sadece bildirilir, etkinleştirilmiş olsa bile GPS hello.</span><span class="sxs-lookup"><span data-stu-id="45840-177">When hello application runs in background, only network based locations are reported, even if you enabled hello GPS.</span></span>
> 
> 

<span data-ttu-id="45840-178">Merhaba kullanıcı, cihaz yeniden başlatılırsa hello arka plan konum rapor durdurulur, önyükleme sırasında otomatik olarak yeniden bu toomake ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="45840-178">hello background location report will be stopped if hello user reboots its device, you can add this toomake it automatically restart at boot time:</span></span>

            <receiver android:name="com.microsoft.azure.engagement.EngagementLocationBootReceiver"
               android:exported="false">
               <intent-filter>
                  <action android:name="android.intent.action.BOOT_COMPLETED" />
               </intent-filter>
            </receiver>

<span data-ttu-id="45840-179">Ayrıca izni eksikse aşağıdaki tooadd hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="45840-179">You also need tooadd hello following permission if missing:</span></span>

            <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />

### <a name="android-m-permissions"></a><span data-ttu-id="45840-180">Android M izinleri</span><span class="sxs-lookup"><span data-stu-id="45840-180">Android M permissions</span></span>
<span data-ttu-id="45840-181">Android M ile başlayarak, bazı izinler çalışma zamanında yönetilir ve kullanıcı onayı gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="45840-181">Starting with Android M, some permissions are managed at runtime and needs user approval.</span></span>

<span data-ttu-id="45840-182">Android API düzeyi 23 hedefliyorsanız hello çalışma zamanı izinleri yeni uygulama yüklemeleri için varsayılan olarak kapatılır.</span><span class="sxs-lookup"><span data-stu-id="45840-182">hello runtime permissions will be turned off by default for new app installations if you target Android API level 23.</span></span> <span data-ttu-id="45840-183">Aksi takdirde, varsayılan olarak açılır.</span><span class="sxs-lookup"><span data-stu-id="45840-183">Otherwise it will be turned on by default.</span></span>

<span data-ttu-id="45840-184">Merhaba kullanıcı etkinleştirebilir/hello aygıt ayarları menüsünden bu izinleri devre dışı bırakabilir.</span><span class="sxs-lookup"><span data-stu-id="45840-184">hello user can enable/disable those permissions from hello device settings menu.</span></span> <span data-ttu-id="45840-185">Arka plan işlemleri hello uygulamasının sistem menüsünden izinleri kapatma devre dışı bırakır, bu bir sistem davranıştır ve yeteneği tooreceive itme arka planda üzerinde hiçbir etkisi olmaz.</span><span class="sxs-lookup"><span data-stu-id="45840-185">Turning off permissions from system menu kills background processes of hello application, this is a system behavior and has no impact on ability tooreceive push in background.</span></span>

<span data-ttu-id="45840-186">Mobile Engagement Hello bağlamında, çalışma zamanında onayı iste hello izinler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="45840-186">In hello context of Mobile Engagement, hello permissions that require approval at runtime are:</span></span>

* `ACCESS_COARSE_LOCATION`
* `ACCESS_FINE_LOCATION`
* <span data-ttu-id="45840-187">`WRITE_EXTERNAL_STORAGE`(yalnızca Android API düzeyini 23 bunu hedeflerken)</span><span class="sxs-lookup"><span data-stu-id="45840-187">`WRITE_EXTERNAL_STORAGE` (only when targeting Android API level 23 for this one)</span></span>

<span data-ttu-id="45840-188">Merhaba harici depolama yalnızca ulaşma büyük resmi özelliği için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="45840-188">hello external storage is used only for Reach big picture feature.</span></span> <span data-ttu-id="45840-189">Görürseniz yalnızca Mobile Engagement ancak büyük resmi özelliği devre dışı bırakma hello maliyetle kullandıysanız kullanıcılar kesintiye uğratan bu izni toobe isteyen, kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="45840-189">If you find asking users this permission toobe disruptive, you can remove it if you used it only for Mobile Engagement but at hello cost of disabling big picture feature.</span></span>

<span data-ttu-id="45840-190">Başlangıç konumu özellikler için standart sistem iletişim kutusunu kullanarak izinleri toouser istemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="45840-190">For hello location features, you should request permissions toouser using a standard system dialog.</span></span> <span data-ttu-id="45840-191">Merhaba kullanıcı onaylarsa, tootell gerek ``EngagementAgent`` tootake hesaba (Aksi hello değişiklik işlenen hello sonraki zamanı hello kullanıcı başlatır hello uygulaması olacaktır) gerçek zamanlı değiştirin.</span><span class="sxs-lookup"><span data-stu-id="45840-191">If hello user approves, you need tootell ``EngagementAgent`` tootake that change into account in real time (otherwise hello change will be processed hello next time hello user launches hello application).</span></span>

<span data-ttu-id="45840-192">Burada ise bir kod örnek toouse uygulama toorequest izinleri ve iletme hello sonuç bir etkinlikte pozitif çok``EngagementAgent``:</span><span class="sxs-lookup"><span data-stu-id="45840-192">Here is a code sample toouse in an activity of your application toorequest permissions and forward hello result if positive too``EngagementAgent``:</span></span>

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

## <a name="advanced-reporting"></a><span data-ttu-id="45840-193">Gelişmiş raporlama</span><span class="sxs-lookup"><span data-stu-id="45840-193">Advanced reporting</span></span>
<span data-ttu-id="45840-194">Tooreport uygulama belirli olaylar, hatalar ve işleri istiyorsanız, isteğe bağlı olarak, hello hello yöntemleri aracılığıyla toouse hello katılım API gerekir `EngagementAgent` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="45840-194">Optionally, if you want tooreport application specific events, errors and jobs, you need toouse hello Engagement API through hello methods of hello `EngagementAgent` class.</span></span> <span data-ttu-id="45840-195">Bu sınıfın bir nesnesi arama hello tarafından alınma olabilir `EngagementAgent.getInstance()` statik yöntemi.</span><span class="sxs-lookup"><span data-stu-id="45840-195">An object of this class can be retreived by calling hello `EngagementAgent.getInstance()` static method.</span></span>

<span data-ttu-id="45840-196">Merhaba katılım API toouse tüm Engagement'ın gelişmiş özelliklerinden sağlar ve hello nasıl ayrıntılı tooUse android'de katılım API (Merhaba teknik belgelerine hello gibi yanı `EngagementAgent` sınıfı).</span><span class="sxs-lookup"><span data-stu-id="45840-196">hello Engagement API allows toouse all of Engagement's advanced capabilities and is detailed in hello How tooUse the Engagement API on Android (as well as in hello technical documentation of hello `EngagementAgent` class).</span></span>

## <a name="advanced-configuration-in-androidmanifestxml"></a><span data-ttu-id="45840-197">Gelişmiş yapılandırmasında (AndroidManifest.xml)</span><span class="sxs-lookup"><span data-stu-id="45840-197">Advanced configuration (in AndroidManifest.xml)</span></span>
### <a name="wake-locks"></a><span data-ttu-id="45840-198">Uyandırma kilitleri</span><span class="sxs-lookup"><span data-stu-id="45840-198">Wake locks</span></span>
<span data-ttu-id="45840-199">Toobe istatistikleri Wifi kullanırken gerçek zamanlı veya Merhaba ekranında kapalıyken gönderildiğinden emin istiyorsanız, isteğe bağlı izni aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="45840-199">If you want toobe sure that statistics are sent in real time when using Wifi or when hello screen is off, add hello following optional permission:</span></span>

            <uses-permission android:name="android.permission.WAKE_LOCK"/>

### <a name="crash-report"></a><span data-ttu-id="45840-200">Kilitlenme raporu</span><span class="sxs-lookup"><span data-stu-id="45840-200">Crash report</span></span>
<span data-ttu-id="45840-201">Toodisable kilitlenme raporları istiyorsanız, bu ekleyin (Merhaba arasında `<application>` ve `</application>` etiketleri):</span><span class="sxs-lookup"><span data-stu-id="45840-201">If you want toodisable crash reports, add this (between hello `<application>` and `</application>` tags):</span></span>

            <meta-data android:name="engagement:reportCrash" android:value="false"/>

### <a name="burst-threshold"></a><span data-ttu-id="45840-202">Eşik veri bloğu</span><span class="sxs-lookup"><span data-stu-id="45840-202">Burst threshold</span></span>
<span data-ttu-id="45840-203">Varsayılan olarak, hello katılım hizmet raporları gerçek zamanlı olarak günlüğe kaydeder.</span><span class="sxs-lookup"><span data-stu-id="45840-203">By default, hello Engagement service reports logs in real time.</span></span> <span data-ttu-id="45840-204">Uygulamanızı günlükleri çok sık raporları, daha iyi toobuffer hello günlükleri ve tooreport varsa, bunları (Merhaba "veri bloğu modu" denir) tümünü bir defada bir normal zaman temel üzerinde.</span><span class="sxs-lookup"><span data-stu-id="45840-204">If your application reports logs very frequently, it is better toobuffer hello logs and tooreport them all at once on a regular time base (this is called hello "burst mode").</span></span> <span data-ttu-id="45840-205">toodo bu nedenle, ekleyin bu (Merhaba arasında `<application>` ve `</application>` etiketleri):</span><span class="sxs-lookup"><span data-stu-id="45840-205">toodo so, add this (between hello `<application>` and `</application>` tags):</span></span>

            <meta-data android:name="engagement:burstThreshold" android:value="{interval between too bursts (in milliseconds)}"/>

<span data-ttu-id="45840-206">Merhaba veri bloğu modu biraz artırmak hello pil ömrü ancak Engagement İzleyicisi Merhaba üzerinde bir etkisi vardır: tüm oturumları ve işleri süresi yuvarlak toohello veri bloğu eşiği (Bu nedenle, oturumlar ve işleri hello veri bloğu eşik görünmeyebilir daha kısa) olacaktır.</span><span class="sxs-lookup"><span data-stu-id="45840-206">hello burst mode slightly increase hello battery life but has an impact on hello Engagement Monitor: all sessions and jobs duration will be rounded toohello burst threshold (thus, sessions and jobs shorter than hello burst threshold may not be visible).</span></span> <span data-ttu-id="45840-207">Bu bir veri bloğu eşikten artık 30000 (30s) toouse önerilir.</span><span class="sxs-lookup"><span data-stu-id="45840-207">It is recommended toouse a burst threshold no longer than 30000 (30s).</span></span>

### <a name="session-timeout"></a><span data-ttu-id="45840-208">Oturum zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="45840-208">Session timeout</span></span>
<span data-ttu-id="45840-209">Varsayılan olarak (genellikle giriş tuşuna basarak hello tarafından oluşur veya telefonla ayarı hello boşta veya başka bir uygulamaya atlayarak anahtarı yedekleme), son etkinliklerine hello bitişinden sonra sona erdi 10'luk bir oturum değil.</span><span class="sxs-lookup"><span data-stu-id="45840-209">By default, a session is ended 10s after hello end of its last activity (which usually occurs by pressing hello Home or Back key, by setting hello phone idle or by jumping into another application).</span></span> <span data-ttu-id="45840-210">Tooavoid (ki çekme bir görüntüyü oluşturan bağlandığınızda durum kontrol edebilirsiniz bir bildirim, vs.) her zaman hello kullanıcı çıkmak ve toohello uygulama çok hızlı bir şekilde dönmek oturum bölme budur.</span><span class="sxs-lookup"><span data-stu-id="45840-210">This is tooavoid a session split each time hello user exit and return toohello application very quickly (which can happen when he pick up a image, check a notification, etc.).</span></span> <span data-ttu-id="45840-211">Bu parametre toomodify isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="45840-211">You may want toomodify this parameter.</span></span> <span data-ttu-id="45840-212">toodo bu nedenle, ekleyin bu (Merhaba arasında `<application>` ve `</application>` etiketleri):</span><span class="sxs-lookup"><span data-stu-id="45840-212">toodo so, add this (between hello `<application>` and `</application>` tags):</span></span>

            <meta-data android:name="engagement:sessionTimeout" android:value="{session timeout (in milliseconds)}"/>

## <a name="disable-log-reporting"></a><span data-ttu-id="45840-213">Günlük bildirimini devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="45840-213">Disable log reporting</span></span>
### <a name="using-a-method-call"></a><span data-ttu-id="45840-214">Yöntem çağrısı kullanma</span><span class="sxs-lookup"><span data-stu-id="45840-214">Using a method call</span></span>
<span data-ttu-id="45840-215">Katılım toostop günlükleri göndermek istiyorsanız, çağırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="45840-215">If you want Engagement toostop sending logs, you can call:</span></span>

            EngagementAgent.getInstance(context).setEnabled(false);

<span data-ttu-id="45840-216">Bu çağrı kalıcıdır: paylaşılan tercihleri dosyasını kullanır.</span><span class="sxs-lookup"><span data-stu-id="45840-216">This call is persistent: it uses a shared preferences file.</span></span>

<span data-ttu-id="45840-217">Katılım etkin değilse, bu işlev çağırdığınızda hello hizmet toostop için 1 dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="45840-217">If Engagement is active when you call this function, it may take 1 minute for hello service toostop.</span></span> <span data-ttu-id="45840-218">Ancak tüm hello hello hizmeti Merhaba uygulaması sonraki başlatışınızda başlatın olmaz.</span><span class="sxs-lookup"><span data-stu-id="45840-218">However it won't launch hello service at all hello next time you launch hello application.</span></span>

<span data-ttu-id="45840-219">Aynı işlevi ile Merhaba çağırarak yeniden raporlama günlüğü etkinleştirebilirsiniz `true`.</span><span class="sxs-lookup"><span data-stu-id="45840-219">You can enable log reporting again by calling hello same function with `true`.</span></span>

### <a name="integration-in-your-own-preferenceactivity"></a><span data-ttu-id="45840-220">Kendi tümleştirme`PreferenceActivity`</span><span class="sxs-lookup"><span data-stu-id="45840-220">Integration in your own `PreferenceActivity`</span></span>
<span data-ttu-id="45840-221">Bu işlevi çağırmak yerine, ayrıca bu ayarı doğrudan var olan tümleştirebilirsiniz `PreferenceActivity`.</span><span class="sxs-lookup"><span data-stu-id="45840-221">Instead of calling this function, you can also integrate this setting directly in your existing `PreferenceActivity`.</span></span>

<span data-ttu-id="45840-222">Hello tercihlerinizi dosya (Merhaba istenen mod ile) katılım toouse yapılandırabilirsiniz `AndroidManifest.xml` ile dosya `application meta-data`:</span><span class="sxs-lookup"><span data-stu-id="45840-222">You can configure Engagement toouse your preferences file (with hello desired mode) in hello `AndroidManifest.xml` file with `application meta-data`:</span></span>

* <span data-ttu-id="45840-223">Merhaba `engagement:agent:settings:name` kullanılan toodefine hello hello paylaşılan tercihleri dosyasının adını bir anahtardır.</span><span class="sxs-lookup"><span data-stu-id="45840-223">hello `engagement:agent:settings:name` key is used toodefine hello name of hello shared preferences file.</span></span>
* <span data-ttu-id="45840-224">Merhaba `engagement:agent:settings:mode` anahtar kullanılan toodefine hello modu hello paylaşılan tercihleri dosyasının, hello kullanması gereken aynı modunda olarak, `PreferenceActivity`.</span><span class="sxs-lookup"><span data-stu-id="45840-224">hello `engagement:agent:settings:mode` key is used toodefine hello mode of hello shared preferences file, you should use hello same mode as in your `PreferenceActivity`.</span></span> <span data-ttu-id="45840-225">bir sayı olarak Hello modu geçirildi: kodunuzda sabit bayrakları birlikte kullanıyorsanız, hello toplam değerini denetleyin.</span><span class="sxs-lookup"><span data-stu-id="45840-225">hello mode must be passed as a number: if you are using a combination of constant flags in your code, check hello total value.</span></span>

<span data-ttu-id="45840-226">Her zaman engagement kullanmayı hello `engagement:key` bu ayarı yönetmek için hello Tercihler dosyasındaki boolean anahtarı.</span><span class="sxs-lookup"><span data-stu-id="45840-226">Engagement always use hello `engagement:key` boolean key within hello preferences file for managing this setting.</span></span>

<span data-ttu-id="45840-227">Merhaba örneği `AndroidManifest.xml` hello varsayılan değerleri gösterir:</span><span class="sxs-lookup"><span data-stu-id="45840-227">hello following example of `AndroidManifest.xml` shows hello default values:</span></span>

            <application>
                [...]
                <meta-data
                  android:name="engagement:agent:settings:name"
                  android:value="engagement.agent" />
                <meta-data
                  android:name="engagement:agent:settings:mode"
                  android:value="0" />

<span data-ttu-id="45840-228">Ekleyebileceğiniz sonra bir `CheckBoxPreference` hello bir aşağıdaki gibi tercih düzeninde:</span><span class="sxs-lookup"><span data-stu-id="45840-228">Then you can add a `CheckBoxPreference` in your preference layout like hello following one:</span></span>

            <CheckBoxPreference
              android:key="engagement:enabled"
              android:defaultValue="true"
              android:title="Use Engagement"
              android:summaryOn="Engagement is enabled."
              android:summaryOff="Engagement is disabled." />

<!-- URLs. -->
[Device API]: http://go.microsoft.com/?linkid=9876094
