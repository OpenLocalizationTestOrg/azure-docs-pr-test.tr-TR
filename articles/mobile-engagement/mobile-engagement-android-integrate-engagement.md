---
title: "Azure Mobile Engagement Android SDK tümleştirmesi"
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
ms.openlocfilehash: 35bd92e52b7a02f58620a03156902f9f91be57ae
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-integrate-engagement-on-android"></a><span data-ttu-id="f496a-103">Android'de katılım tümleştirme</span><span class="sxs-lookup"><span data-stu-id="f496a-103">How to Integrate Engagement on Android</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f496a-104">Windows Evrensel</span><span class="sxs-lookup"><span data-stu-id="f496a-104">Windows Universal</span></span>](mobile-engagement-windows-store-integrate-engagement.md)
> * [<span data-ttu-id="f496a-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="f496a-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="f496a-106">iOS</span><span class="sxs-lookup"><span data-stu-id="f496a-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="f496a-107">Android</span><span class="sxs-lookup"><span data-stu-id="f496a-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md)
> 
> 

<span data-ttu-id="f496a-108">Bu yordam, Engagement analizi ve izleme işlevlerine Android uygulamanızdaki etkinleştirmek için en basit yolu açıklar.</span><span class="sxs-lookup"><span data-stu-id="f496a-108">This procedure describes the simplest way to activate Engagement's Analytics and Monitoring functions in your Android application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f496a-109">En düşük Android SDK API düzey 10 veya daha yüksek olmalıdır (Android 2.3.3 ya da daha yüksek).</span><span class="sxs-lookup"><span data-stu-id="f496a-109">Your minimum Android SDK API level must be 10 or higher (Android 2.3.3 or higher).</span></span>
> 
> 

<span data-ttu-id="f496a-110">Aşağıdaki adım etkinleştirir için kullanıcıları, oturumlar, etkinlikleri, kilitlenme ve Technicals ilgili tüm istatistikleri işlem için gereken günlükleri rapor yeterli değildir.</span><span class="sxs-lookup"><span data-stu-id="f496a-110">The following steps are enough to activates the report of logs needed to compute all statistics regarding Users, Sessions, Activities, Crashes and Technicals.</span></span> <span data-ttu-id="f496a-111">Olaylar, hatalar ve işleri gibi diğer istatistikleri işlem için gereken günlükleri rapor katılım API kullanarak el ile yapılması gerekir (bkz [, Android API etiketleme Gelişmiş Mobile Engagement kullanmayı](mobile-engagement-android-use-engagement-api.md) Bu istatistikler olduğundan uygulamaya bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="f496a-111">The report of logs needed to compute other statistics like Events, Errors and Jobs must be done manually using the Engagement API (see [How to use the advanced Mobile Engagement tagging API in your Android](mobile-engagement-android-use-engagement-api.md) since these statistics are application dependent.</span></span>

## <a name="embed-the-engagement-sdk-and-service-into-your-android-project"></a><span data-ttu-id="f496a-112">Hizmet ve Engagement SDK'sı Android projenize ekleme</span><span class="sxs-lookup"><span data-stu-id="f496a-112">Embed the Engagement SDK and service into your Android project</span></span>
<span data-ttu-id="f496a-113">Android SDK Yükle [burada](https://aka.ms/vq9mfn) almak `mobile-engagement-VERSION.jar` ve bunların içine yerleştirin `libs` klasörü Android projenizin (henüz yoksa libs klasörüne oluşturma).</span><span class="sxs-lookup"><span data-stu-id="f496a-113">Download the Android SDK from [here](https://aka.ms/vq9mfn) Get `mobile-engagement-VERSION.jar` and put them into the `libs` folder of your Android project (create the libs folder if it does not exist yet).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f496a-114">Uygulama paketinizi ProGuard ile yapılandırdıysanız, bazı sınıfları tutmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="f496a-114">If you build your application package with ProGuard, you need to keep some classes.</span></span> <span data-ttu-id="f496a-115">Aşağıdaki yapılandırma parçacığını kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f496a-115">You can use the following configuration snippet:</span></span>
> 
> <span data-ttu-id="f496a-116">-Ortak sınıfı tutmak * android.os.IInterface genişletir-sınıfı com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {tutun</span><span class="sxs-lookup"><span data-stu-id="f496a-116">-keep public class * extends android.os.IInterface -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {</span></span>
> 
> <span data-ttu-id="f496a-117"><methods>; }</span><span class="sxs-lookup"><span data-stu-id="f496a-117"><methods>; }</span></span>
> 
> 

<span data-ttu-id="f496a-118">Başlatıcı etkinliğin aşağıdaki yöntemini çağırarak katılım bağlantı dizenizi belirtin:</span><span class="sxs-lookup"><span data-stu-id="f496a-118">Specify your Engagement connection string by calling the following method in the launcher activity:</span></span>

            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
            EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="f496a-119">Bağlantı dizesi, uygulamanız için Azure portalında görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="f496a-119">The connection string for your application is displayed on Azure Portal.</span></span>

* <span data-ttu-id="f496a-120">Eksikse, aşağıdaki Android izinleri ekleyin (önce `<application>` etiketi):</span><span class="sxs-lookup"><span data-stu-id="f496a-120">If missing, add the following Android permissions (before the `<application>` tag):</span></span>
  
          <uses-permission android:name="android.permission.INTERNET"/>
          <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
* <span data-ttu-id="f496a-121">Aşağıdaki bölümde ekleyin (arasında `<application>` ve `</application>` etiketleri):</span><span class="sxs-lookup"><span data-stu-id="f496a-121">Add the following section (between the `<application>` and `</application>` tags):</span></span>
  
          <service
            android:name="com.microsoft.azure.engagement.service.EngagementService"
            android:exported="false"
            android:label="<Your application name>Service"
            android:process=":Engagement"/>
* <span data-ttu-id="f496a-122">Değişiklik `<Your application name>` , uygulamanızın adı.</span><span class="sxs-lookup"><span data-stu-id="f496a-122">Change `<Your application name>` by the name of your application.</span></span>

> [!TIP]
> <span data-ttu-id="f496a-123">`android:label` Özniteliği telefonlarını "Hizmetleri çalışır" ekranında son kullanıcılar için görünür olarak katılım hizmetin adını seçin olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="f496a-123">The `android:label` attribute allows you to choose the name of the Engagement service as it will appear to the end-users in the "Running services" screen of their phone.</span></span> <span data-ttu-id="f496a-124">Bu öznitelik ayarlamak için önerilen `"<Your application name>Service"` (örneğin `"AcmeFunGameService"`).</span><span class="sxs-lookup"><span data-stu-id="f496a-124">It is recommended to set this attribute to `"<Your application name>Service"` (e.g. `"AcmeFunGameService"`).</span></span>
> 
> 

<span data-ttu-id="f496a-125">Belirtme `android:process` özniteliği sağlar katılım hizmet (uygulamanızın ana/kullanıcı Arabirimi iş parçacığı potansiyel olarak daha az yanıt yapacak şekilde katılım aynı işlem içinde çalışan) kendi işleminde çalışır.</span><span class="sxs-lookup"><span data-stu-id="f496a-125">Specifying the `android:process` attribute ensures that the Engagement service will run in its own process (running Engagement in the same process as your application will make your main/UI thread potentially less responsive).</span></span>

> [!NOTE]
> <span data-ttu-id="f496a-126">Yerleştirdiğiniz içinde herhangi bir kod `Application.onCreate()` ve diğer uygulama geri aramalar katılım hizmeti dahil olmak üzere tüm uygulama işlemleri için çalışır.</span><span class="sxs-lookup"><span data-stu-id="f496a-126">Any code you place in `Application.onCreate()` and other application callbacks will be run for all your application's processes, including the Engagement service.</span></span> <span data-ttu-id="f496a-127">(Örneğin, gereksiz bellek ayırma ve Engagement'ın işlemde, yinelenen yayın alıcılar veya hizmetleri iş parçacıkları) istenmeyen yan etkileri olabilir.</span><span class="sxs-lookup"><span data-stu-id="f496a-127">It may have unwanted side effects (like unneeded memory allocations and threads in the Engagement's process, duplicate broadcast receivers or services).</span></span>
> 
> 

<span data-ttu-id="f496a-128">Geçersiz kılarsanız `Application.onCreate()`, aşağıdaki kod parçacığını başında eklemek için önerilen, `Application.onCreate()` işlevi:</span><span class="sxs-lookup"><span data-stu-id="f496a-128">If you override `Application.onCreate()`, it's recommended to add the following code snippet at the beginning of your `Application.onCreate()` function:</span></span>

             public void onCreate()
             {
               if (EngagementAgentUtils.isInDedicatedEngagementProcess(this))
                 return;

               ... Your code...
             }

<span data-ttu-id="f496a-129">Aynı şeyi yapmak `Application.onTerminate()`, `Application.onLowMemory()` ve `Application.onConfigurationChanged(...)`.</span><span class="sxs-lookup"><span data-stu-id="f496a-129">You can do the same thing for `Application.onTerminate()`, `Application.onLowMemory()` and `Application.onConfigurationChanged(...)`.</span></span>

<span data-ttu-id="f496a-130">Ayrıca genişletebilirsiniz `EngagementApplication` genişletme yerine `Application`: geri çağırma `Application.onCreate()` işlem denetimi yapar ve çağrıları `Application.onApplicationProcessCreate()` yalnızca geçerli işlem katılım hizmetini barındıran bir durumda değilse, aynı kuralları için diğer uygulama geri aramalar.</span><span class="sxs-lookup"><span data-stu-id="f496a-130">You can also extend `EngagementApplication` instead of extending `Application`: the callback `Application.onCreate()` does the process check and calls `Application.onApplicationProcessCreate()` only if the current process is not the one hosting the Engagement service, the same rules apply for the other callbacks.</span></span>

## <a name="basic-reporting"></a><span data-ttu-id="f496a-131">Temel raporlama</span><span class="sxs-lookup"><span data-stu-id="f496a-131">Basic reporting</span></span>
### <a name="recommended-method-overload-your-activity-classes"></a><span data-ttu-id="f496a-132">Önerilen yöntem: aşırı yükleme, `Activity` sınıfları</span><span class="sxs-lookup"><span data-stu-id="f496a-132">Recommended method: overload your `Activity` classes</span></span>
<span data-ttu-id="f496a-133">Rapor kullanıcıları, oturumlar, etkinlikleri, kilitlenme ve teknik istatistikleri işlem katılım tarafından gerekli tüm günlüklerin etkinleştirmek için yalnızca tüm yapmanız gerekir, `*Activity` alt sınıfları devralır denk gelen `Engagement*Activity` (örneğin sınıfları eski etkinliklerinizi geçerse `ListActivity`, onu genişletir yapma `EngagementListActivity`).</span><span class="sxs-lookup"><span data-stu-id="f496a-133">In order to activate the report of all the logs required by Engagement to compute Users, Sessions, Activities, Crashes and Technical statistics, you just have to make all your `*Activity` sub-classes inherit from the corresponding `Engagement*Activity` classes (e.g. if your legacy activity extends `ListActivity`, make it extends `EngagementListActivity`).</span></span>

<span data-ttu-id="f496a-134">**Katılım:**</span><span class="sxs-lookup"><span data-stu-id="f496a-134">**Without Engagement :**</span></span>

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

<span data-ttu-id="f496a-135">**Katılım ile:**</span><span class="sxs-lookup"><span data-stu-id="f496a-135">**With Engagement :**</span></span>

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
> <span data-ttu-id="f496a-136">Kullanırken `EngagementListActivity` veya `EngagementExpandableListActivity`, aşağıdakilerden emin olun çağrı `requestWindowFeature(...);` çağırmadan önce yapılan `super.onCreate(...);`, aksi takdirde bir kilitlenme meydana gelir.</span><span class="sxs-lookup"><span data-stu-id="f496a-136">When using `EngagementListActivity` or `EngagementExpandableListActivity`, make sure any call to `requestWindowFeature(...);` is made before the call to `super.onCreate(...);`, otherwise a crash will occur.</span></span>
> 
> 

<span data-ttu-id="f496a-137">Bu sınıfları bulabilirsiniz `src` klasörünü ve bunları projenize kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f496a-137">You can find these classes in the `src` folder, and can copy them into your project.</span></span> <span data-ttu-id="f496a-138">Ayrıca, sınıflardır **JavaDoc**.</span><span class="sxs-lookup"><span data-stu-id="f496a-138">The classes are also in the **JavaDoc**.</span></span>

### <a name="alternate-method-call-startactivity-and-endactivity-manually"></a><span data-ttu-id="f496a-139">Alternatif yöntem: çağrı `startActivity()` ve `endActivity()` el ile</span><span class="sxs-lookup"><span data-stu-id="f496a-139">Alternate method: call `startActivity()` and `endActivity()` manually</span></span>
<span data-ttu-id="f496a-140">Olamaz ya da tekrar etmek istiyor musunuz, `Activity` sınıfları, bunun yerine başlangıç ve çağırarak etkinliklerinizi bitiş `EngagementAgent`'s doğrudan yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="f496a-140">If you cannot or do not want to overload your `Activity` classes, you can instead start and end your activities by calling `EngagementAgent`'s methods directly.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f496a-141">Android SDK hiçbir zaman çağırır `endActivity()` uygulama kapalı olduğunda bile yöntemi (Android, uygulamaları gerçekte hiçbir zaman kapalı).</span><span class="sxs-lookup"><span data-stu-id="f496a-141">The Android SDK never calls the `endActivity()` method, even when the application is closed (on Android, applications are actually never closed).</span></span> <span data-ttu-id="f496a-142">Bu nedenle, olan *yüksek oranda* çağırmak için önerilen `startActivity()` yönteminde `onResume` , geri çağırma *tüm* , etkinlikler ve `endActivity()` yönteminde `onPause()` , geri çağırma *Tüm* etkinliklerinizi.</span><span class="sxs-lookup"><span data-stu-id="f496a-142">Thus, it is *HIGHLY* recommended to call the `startActivity()` method in the `onResume` callback of *ALL* your activities, and the `endActivity()` method in the `onPause()` callback of *ALL* your activities.</span></span> <span data-ttu-id="f496a-143">Bu oturumlar sızmaması emin olmak için tek yoludur.</span><span class="sxs-lookup"><span data-stu-id="f496a-143">This is the only way to be sure that sessions will not be leaked.</span></span> <span data-ttu-id="f496a-144">Bir oturum sızmasını varsa (bir oturum bekleyen olduğu sürece hizmet bağlı kalır bu yana) katılım hizmet hiçbir zaman katılım arka ucundan bağlantısını keser.</span><span class="sxs-lookup"><span data-stu-id="f496a-144">If a session is leaked, the Engagement service will never disconnect from the Engagement backend (since the service stays connected as long as a session is pending).</span></span>
> 
> 

<span data-ttu-id="f496a-145">Örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="f496a-145">Here is an example:</span></span>

            public class MyActivity extends Some3rdPartyActivity
            {
              @Override
              protected void onResume()
              {
                super.onResume();
                String activityNameOnEngagement = EngagementAgentUtils.buildEngagementActivityName(getClass()); // Uses short class name and removes "Activity" at the end.
                EngagementAgent.getInstance(this).startActivity(this, activityNameOnEngagement, null);
              }

              @Override
              protected void onPause()
              {
                super.onPause();
                EngagementAgent.getInstance(this).endActivity();
              }
            }

<span data-ttu-id="f496a-146">Bu örnek için çok benzer `EngagementActivity` sınıfı ve kaynak kodu sağlanır türevleri `src` klasör.</span><span class="sxs-lookup"><span data-stu-id="f496a-146">This example very similiar to the `EngagementActivity` class and its variants, whose source code is provided in the `src` folder.</span></span>

## <a name="test"></a><span data-ttu-id="f496a-147">Test etme</span><span class="sxs-lookup"><span data-stu-id="f496a-147">Test</span></span>
<span data-ttu-id="f496a-148">Şimdi bir öykünücü veya cihaz ve mobil uygulamanızı çalıştırarak ve bir oturum izleme sekmesinde kayıtları doğrulanıyor Lütfen tümleştirmenize doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="f496a-148">Now please verify your integration by running your mobile app in an emulator or device and verifying that it registers a session on the Monitor tab.</span></span>

<span data-ttu-id="f496a-149">Sonraki bölümlerde isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="f496a-149">The next sections are optional.</span></span>

## <a name="location-reporting"></a><span data-ttu-id="f496a-150">Konum raporlama</span><span class="sxs-lookup"><span data-stu-id="f496a-150">Location reporting</span></span>
<span data-ttu-id="f496a-151">Konumları bildirilmesini istiyorsanız, birkaç satırlı yapılandırma eklemeniz gerekir (arasında `<application>` ve `</application>` etiketleri).</span><span class="sxs-lookup"><span data-stu-id="f496a-151">If you want locations to be reported, you need to add a few lines of configuration (between the `<application>` and `</application>` tags).</span></span>

### <a name="lazy-area-location-reporting"></a><span data-ttu-id="f496a-152">Yavaş alan konumu raporlama</span><span class="sxs-lookup"><span data-stu-id="f496a-152">Lazy area location reporting</span></span>
<span data-ttu-id="f496a-153">Yavaş alan konumu raporlama ülke, bölgeye ve yere göre cihazlara ilişkili rapor oluşturmaya olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="f496a-153">Lazy area location reporting allows to report the country, region and locality associated to devices.</span></span> <span data-ttu-id="f496a-154">Bu tür konumu raporlama yalnızca ağ konumlarını (hücre kimliği veya WIFI göre) kullanır.</span><span class="sxs-lookup"><span data-stu-id="f496a-154">This type of location reporting only uses network locations (based on Cell ID or WIFI).</span></span> <span data-ttu-id="f496a-155">Aygıt alanına oturum başına en fazla bir kez bildirilir.</span><span class="sxs-lookup"><span data-stu-id="f496a-155">The device area is reported at most once per session.</span></span> <span data-ttu-id="f496a-156">GPS hiçbir zaman kullanılmaz ve bu nedenle bu konumu rapor çok az (no değil söylemeniz) türü pil üzerindeki etkisi.</span><span class="sxs-lookup"><span data-stu-id="f496a-156">The GPS is never used, and thus this type of location report has very few (not to say no) impact on the battery.</span></span>

<span data-ttu-id="f496a-157">Bildirilen alanları kullanıcıları, oturumlar, olayları ve hataları ile ilgili coğrafi istatistikleri hesaplamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f496a-157">Reported areas are used to compute geographic statistics about users, sessions, events and errors.</span></span> <span data-ttu-id="f496a-158">Reach kampanyaları ölçütü olarak de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="f496a-158">They can also be used as criterion in Reach campaigns.</span></span>

<span data-ttu-id="f496a-159">Yavaş alan konumu raporlama etkinleştirmek için bu yordamda daha önce bahsedilen yapılandırmayı kullanarak bunu yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f496a-159">To enable lazy area location reporting, you can do it by using the configuration previously mentioned in this procedure :</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setLazyAreaLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="f496a-160">Ayrıca aşağıdaki izni eksikse eklemeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="f496a-160">You also need to add the following permission if missing:</span></span>

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

<span data-ttu-id="f496a-161">Veya kullanmaya devam edebileceğiniz ``ACCESS_FINE_LOCATION`` zaten uygulamanızda kullanın.</span><span class="sxs-lookup"><span data-stu-id="f496a-161">Or you can keep using ``ACCESS_FINE_LOCATION`` if you already use it in your application.</span></span>

### <a name="real-time-location-reporting"></a><span data-ttu-id="f496a-162">Gerçek zamanlı konum raporlama</span><span class="sxs-lookup"><span data-stu-id="f496a-162">Real time location reporting</span></span>
<span data-ttu-id="f496a-163">Gerçek zamanlı konum raporlama enlem ve boylam cihazlara ilişkili rapor oluşturmaya olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="f496a-163">Real time location reporting allows to report the latitude and longitude associated to devices.</span></span> <span data-ttu-id="f496a-164">Varsayılan olarak, bu tür konumu raporlama yalnızca ağ konumlarını (hücre kimliği veya WIFI göre) kullanır ve uygulama ön planda (yani oturumu sırasında) çalıştığında raporlama yalnızca etkindir.</span><span class="sxs-lookup"><span data-stu-id="f496a-164">By default, this type of location reporting only uses network locations (based on Cell ID or WIFI), and the reporting is only active when the application runs in foreground (i.e. during a session).</span></span>

<span data-ttu-id="f496a-165">Gerçek zamanlı konumlarının *değil* istatistikleri hesaplamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f496a-165">Real time locations are *NOT* used to compute statistics.</span></span> <span data-ttu-id="f496a-166">Gerçek zamanlı coğrafi yalıtma kullanımına izin vermek için kendi tek amacı olan \<Reach-İzleyici-bölge sınırlaması\> Reach kampanyaları ölçütü.</span><span class="sxs-lookup"><span data-stu-id="f496a-166">Their only purpose is to allow the use of real time geo-fencing \<Reach-Audience-geofencing\> criterion in Reach campaigns.</span></span>

<span data-ttu-id="f496a-167">Gerçek zamanlı konum raporlama etkinleştirmek için bu yordamda daha önce bahsedilen yapılandırmayı kullanarak bunu yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f496a-167">To enable real time location reporting, you can do it by using the configuration previously mentioned in this procedure :</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="f496a-168">Ayrıca aşağıdaki izni eksikse eklemeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="f496a-168">You also need to add the following permission if missing:</span></span>

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

<span data-ttu-id="f496a-169">Veya kullanmaya devam edebileceğiniz ``ACCESS_FINE_LOCATION`` zaten uygulamanızda kullanın.</span><span class="sxs-lookup"><span data-stu-id="f496a-169">Or you can keep using ``ACCESS_FINE_LOCATION`` if you already use it in your application.</span></span>

#### <a name="gps-based-reporting"></a><span data-ttu-id="f496a-170">Raporlama GPS dayalı</span><span class="sxs-lookup"><span data-stu-id="f496a-170">GPS based reporting</span></span>
<span data-ttu-id="f496a-171">Varsayılan olarak, gerçek zamanlı konum raporlama ağ tabanlı konum yalnızca kullanır.</span><span class="sxs-lookup"><span data-stu-id="f496a-171">By default, real time location reporting only uses network based locations.</span></span> <span data-ttu-id="f496a-172">(Olan daha kesin) tabanlı GPS konumları kullanımını etkinleştirmek için yapılandırma nesnesi kullanın:</span><span class="sxs-lookup"><span data-stu-id="f496a-172">To enable the use of GPS based locations (which are far more precise), use the configuration object:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setFineRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="f496a-173">Ayrıca aşağıdaki izni eksikse eklemeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="f496a-173">You also need to add the following permission if missing:</span></span>

            <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>

#### <a name="background-reporting"></a><span data-ttu-id="f496a-174">Arka plan raporlama</span><span class="sxs-lookup"><span data-stu-id="f496a-174">Background reporting</span></span>
<span data-ttu-id="f496a-175">Uygulama ön planda (yani oturumu sırasında) çalıştırdığında, varsayılan olarak, gerçek zamanlı konum raporlama yalnızca etkindir.</span><span class="sxs-lookup"><span data-stu-id="f496a-175">By default, real time location reporting is only active when the application runs in foreground (i.e. during a session).</span></span> <span data-ttu-id="f496a-176">Aynı zamanda arka planda raporlamayı etkinleştirmek için yapılandırma nesnesi kullanın:</span><span class="sxs-lookup"><span data-stu-id="f496a-176">To enable the reporting also in background, use the configuration object:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setBackgroundRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

> [!NOTE]
> <span data-ttu-id="f496a-177">Tabanlı ağ konumları yalnızca uygulama arka planda çalıştığında raporlanır, GPS etkin olsa bile.</span><span class="sxs-lookup"><span data-stu-id="f496a-177">When the application runs in background, only network based locations are reported, even if you enabled the GPS.</span></span>
> 
> 

<span data-ttu-id="f496a-178">Kullanıcı, cihaz yeniden başlatılırsa, arka plan konum rapor durdurulur, önyükleme sırasında otomatik olarak yeniden sağlamak için bunu ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f496a-178">The background location report will be stopped if the user reboots its device, you can add this to make it automatically restart at boot time:</span></span>

            <receiver android:name="com.microsoft.azure.engagement.EngagementLocationBootReceiver"
               android:exported="false">
               <intent-filter>
                  <action android:name="android.intent.action.BOOT_COMPLETED" />
               </intent-filter>
            </receiver>

<span data-ttu-id="f496a-179">Ayrıca aşağıdaki izni eksikse eklemeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="f496a-179">You also need to add the following permission if missing:</span></span>

            <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />

### <a name="android-m-permissions"></a><span data-ttu-id="f496a-180">Android M izinleri</span><span class="sxs-lookup"><span data-stu-id="f496a-180">Android M permissions</span></span>
<span data-ttu-id="f496a-181">Android M ile başlayarak, bazı izinler çalışma zamanında yönetilir ve kullanıcı onayı gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="f496a-181">Starting with Android M, some permissions are managed at runtime and needs user approval.</span></span>

<span data-ttu-id="f496a-182">Android API düzeyi 23 hedefliyorsanız çalışma zamanı izinleri yeni uygulama yüklemeleri için varsayılan olarak kapatılır.</span><span class="sxs-lookup"><span data-stu-id="f496a-182">The runtime permissions will be turned off by default for new app installations if you target Android API level 23.</span></span> <span data-ttu-id="f496a-183">Aksi takdirde, varsayılan olarak açılır.</span><span class="sxs-lookup"><span data-stu-id="f496a-183">Otherwise it will be turned on by default.</span></span>

<span data-ttu-id="f496a-184">Kullanıcı etkinleştirebilir/aygıt ayarları menüsünden bu izinleri devre dışı bırakabilir.</span><span class="sxs-lookup"><span data-stu-id="f496a-184">The user can enable/disable those permissions from the device settings menu.</span></span> <span data-ttu-id="f496a-185">Arka plan işlemleri uygulamasının sistem menüsünden izinleri kapatma devre dışı bırakır, bu bir sistem davranıştır ve anında iletme arka planda alma yeteneğini üzerinde hiçbir etkisi olmaz.</span><span class="sxs-lookup"><span data-stu-id="f496a-185">Turning off permissions from system menu kills background processes of the application, this is a system behavior and has no impact on ability to receive push in background.</span></span>

<span data-ttu-id="f496a-186">Mobile Engagement bağlamında, çalışma zamanında onayı iste izinler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="f496a-186">In the context of Mobile Engagement, the permissions that require approval at runtime are:</span></span>

* `ACCESS_COARSE_LOCATION`
* `ACCESS_FINE_LOCATION`
* <span data-ttu-id="f496a-187">`WRITE_EXTERNAL_STORAGE`(yalnızca Android API düzeyini 23 bunu hedeflerken)</span><span class="sxs-lookup"><span data-stu-id="f496a-187">`WRITE_EXTERNAL_STORAGE` (only when targeting Android API level 23 for this one)</span></span>

<span data-ttu-id="f496a-188">Harici depolama yalnızca ulaşma büyük resmi özelliği için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f496a-188">The external storage is used only for Reach big picture feature.</span></span> <span data-ttu-id="f496a-189">Görürseniz yalnızca Mobile Engagement için ancak büyük resmi özelliği devre dışı bırakma, kullandıysanız kullanıcılar kesintiye uğratan olması için bu izin isteyen, kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f496a-189">If you find asking users this permission to be disruptive, you can remove it if you used it only for Mobile Engagement but at the cost of disabling big picture feature.</span></span>

<span data-ttu-id="f496a-190">Konum özellikler için standart sistem iletişim kutusunu kullanarak kullanıcı izni istemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="f496a-190">For the location features, you should request permissions to user using a standard system dialog.</span></span> <span data-ttu-id="f496a-191">Kullanıcı onaylarsa, bildirmeniz gerekir ``EngagementAgent`` gerçek zamanlı olarak bu değişikliği dikkate almak için (Aksi halde değişikliği kullanıcı başlatır uygulama başlatıldığında işlenir).</span><span class="sxs-lookup"><span data-stu-id="f496a-191">If the user approves, you need to tell ``EngagementAgent`` to take that change into account in real time (otherwise the change will be processed the next time the user launches the application).</span></span>

<span data-ttu-id="f496a-192">İzinleri istemek ve sonuç için pozitif varsa iletmek için uygulamanızın bir etkinlikte kullanılacak bir kod örneği işte ``EngagementAgent``:</span><span class="sxs-lookup"><span data-stu-id="f496a-192">Here is a code sample to use in an activity of your application to request permissions and forward the result if positive to ``EngagementAgent``:</span></span>

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
         * Request location permission, but this won't explain why it is needed to the user.
         * The standard Android documentation explains with more details how to display a rationale activity to explain the user why the permission is needed in your application.
         * Putting COARSE vs FINE has no impact here, they are part of the same group for runtime permission management.
         */
        if (checkSelfPermission(android.Manifest.permission.ACCESS_FINE_LOCATION) != PackageManager.PERMISSION_GRANTED)
          requestPermissions(new String[] { android.Manifest.permission.ACCESS_FINE_LOCATION }, 0);

        /* Only if you want to keep features using external storage */
        if (checkSelfPermission(android.Manifest.permission.WRITE_EXTERNAL_STORAGE) != PackageManager.PERMISSION_GRANTED)
          requestPermissions(new String[] { android.Manifest.permission.WRITE_EXTERNAL_STORAGE }, 1);
      }
    }

    @Override
    public void onRequestPermissionsResult(int requestCode, String[] permissions, int[] grantResults)
    {
      /* Only a positive location permission update requires engagement agent refresh, hence the request code matching from above function */
      if (requestCode == 0 && grantResults[0] == PackageManager.PERMISSION_GRANTED)
        getEngagementAgent().refreshPermissions();
    }

## <a name="advanced-reporting"></a><span data-ttu-id="f496a-193">Gelişmiş raporlama</span><span class="sxs-lookup"><span data-stu-id="f496a-193">Advanced reporting</span></span>
<span data-ttu-id="f496a-194">Uygulama belirli olaylar, hatalar ve işleri rapor istiyorsanız, isteğe bağlı olarak, katılım API yöntemlerini kullanmanız gerekebilir `EngagementAgent` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="f496a-194">Optionally, if you want to report application specific events, errors and jobs, you need to use the Engagement API through the methods of the `EngagementAgent` class.</span></span> <span data-ttu-id="f496a-195">Bu sınıfın bir nesnesi çağırarak alınma olabilir `EngagementAgent.getInstance()` statik yöntemi.</span><span class="sxs-lookup"><span data-stu-id="f496a-195">An object of this class can be retreived by calling the `EngagementAgent.getInstance()` static method.</span></span>

<span data-ttu-id="f496a-196">Katılım API tüm Engagement'ın gelişmiş özelliklerinden kullanacak şekilde sağlar ve nasıl ayrıntılı Android katılım API kullanmak için (teknik belgeleri olarak yanı `EngagementAgent` sınıfı).</span><span class="sxs-lookup"><span data-stu-id="f496a-196">The Engagement API allows to use all of Engagement's advanced capabilities and is detailed in the How to Use the Engagement API on Android (as well as in the technical documentation of the `EngagementAgent` class).</span></span>

## <a name="advanced-configuration-in-androidmanifestxml"></a><span data-ttu-id="f496a-197">Gelişmiş yapılandırmasında (AndroidManifest.xml)</span><span class="sxs-lookup"><span data-stu-id="f496a-197">Advanced configuration (in AndroidManifest.xml)</span></span>
### <a name="wake-locks"></a><span data-ttu-id="f496a-198">Uyandırma kilitleri</span><span class="sxs-lookup"><span data-stu-id="f496a-198">Wake locks</span></span>
<span data-ttu-id="f496a-199">İstatistikleri Wifi kullanırken gerçek zamanlı veya ekran kapalıyken gönderildiğinden emin olmak istiyorsanız, aşağıdaki isteğe bağlı iznini ekleyin:</span><span class="sxs-lookup"><span data-stu-id="f496a-199">If you want to be sure that statistics are sent in real time when using Wifi or when the screen is off, add the following optional permission:</span></span>

            <uses-permission android:name="android.permission.WAKE_LOCK"/>

### <a name="crash-report"></a><span data-ttu-id="f496a-200">Kilitlenme raporu</span><span class="sxs-lookup"><span data-stu-id="f496a-200">Crash report</span></span>
<span data-ttu-id="f496a-201">Kilitlenme raporları devre dışı bırakmak istiyorsanız, bunu ekleyin (arasında `<application>` ve `</application>` etiketleri):</span><span class="sxs-lookup"><span data-stu-id="f496a-201">If you want to disable crash reports, add this (between the `<application>` and `</application>` tags):</span></span>

            <meta-data android:name="engagement:reportCrash" android:value="false"/>

### <a name="burst-threshold"></a><span data-ttu-id="f496a-202">Eşik veri bloğu</span><span class="sxs-lookup"><span data-stu-id="f496a-202">Burst threshold</span></span>
<span data-ttu-id="f496a-203">Varsayılan olarak, katılım hizmet raporları gerçek zamanlı olarak günlüğe kaydeder.</span><span class="sxs-lookup"><span data-stu-id="f496a-203">By default, the Engagement service reports logs in real time.</span></span> <span data-ttu-id="f496a-204">Uygulamanızı günlükleri çok sık bildirirse, günlükleri arabellek ve (Buna "veri bloğu modu" denir) tümünü bir defada bir normal zaman üzerinde temel bildirmek için daha iyi olur.</span><span class="sxs-lookup"><span data-stu-id="f496a-204">If your application reports logs very frequently, it is better to buffer the logs and to report them all at once on a regular time base (this is called the "burst mode").</span></span> <span data-ttu-id="f496a-205">Bunu yapmak için bu ekleyin (arasında `<application>` ve `</application>` etiketleri):</span><span class="sxs-lookup"><span data-stu-id="f496a-205">To do so, add this (between the `<application>` and `</application>` tags):</span></span>

            <meta-data android:name="engagement:burstThreshold" android:value="{interval between too bursts (in milliseconds)}"/>

<span data-ttu-id="f496a-206">Veri bloğu modu biraz pil ömrünün artırabilirsiniz ancak Engagement İzleyicisi üzerinde bir etkisi vardır: tüm oturumları ve işleri süre (dolayısıyla, oturumlar ve işleri veri bloğu eşik görünmeyebilir daha kısa) veri bloğu eşik yuvarlanır.</span><span class="sxs-lookup"><span data-stu-id="f496a-206">The burst mode slightly increase the battery life but has an impact on the Engagement Monitor: all sessions and jobs duration will be rounded to the burst threshold (thus, sessions and jobs shorter than the burst threshold may not be visible).</span></span> <span data-ttu-id="f496a-207">Bir veri bloğu eşikten artık 30000 (30s) kullanılması önerilir.</span><span class="sxs-lookup"><span data-stu-id="f496a-207">It is recommended to use a burst threshold no longer than 30000 (30s).</span></span>

### <a name="session-timeout"></a><span data-ttu-id="f496a-208">Oturum zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="f496a-208">Session timeout</span></span>
<span data-ttu-id="f496a-209">Varsayılan olarak, bir oturum sona erdi 10'luk (oluşan genellikle ev veya Geri tuşuna basarak, telefon boşta ayarlayarak veya başka bir uygulamaya atlayarak), son etkinlik sonunda değil.</span><span class="sxs-lookup"><span data-stu-id="f496a-209">By default, a session is ended 10s after the end of its last activity (which usually occurs by pressing the Home or Back key, by setting the phone idle or by jumping into another application).</span></span> <span data-ttu-id="f496a-210">Bu (ki çekme bir görüntüyü oluşturan bağlandığınızda durum kontrol edebilirsiniz bir bildirim, vs.) her kullanıcı çıkış saat ve uygulamaya çok hızlı bir şekilde dönmek oturum bölme önlemek için yapılır.</span><span class="sxs-lookup"><span data-stu-id="f496a-210">This is to avoid a session split each time the user exit and return to the application very quickly (which can happen when he pick up a image, check a notification, etc.).</span></span> <span data-ttu-id="f496a-211">Bu parametre değiştirmek isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f496a-211">You may want to modify this parameter.</span></span> <span data-ttu-id="f496a-212">Bunu yapmak için bu ekleyin (arasında `<application>` ve `</application>` etiketleri):</span><span class="sxs-lookup"><span data-stu-id="f496a-212">To do so, add this (between the `<application>` and `</application>` tags):</span></span>

            <meta-data android:name="engagement:sessionTimeout" android:value="{session timeout (in milliseconds)}"/>

## <a name="disable-log-reporting"></a><span data-ttu-id="f496a-213">Günlük bildirimini devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="f496a-213">Disable log reporting</span></span>
### <a name="using-a-method-call"></a><span data-ttu-id="f496a-214">Yöntem çağrısı kullanma</span><span class="sxs-lookup"><span data-stu-id="f496a-214">Using a method call</span></span>
<span data-ttu-id="f496a-215">Engagement'ın günlükleri göndermek durdurmak istiyorsanız, çağırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f496a-215">If you want Engagement to stop sending logs, you can call:</span></span>

            EngagementAgent.getInstance(context).setEnabled(false);

<span data-ttu-id="f496a-216">Bu çağrı kalıcıdır: paylaşılan tercihleri dosyasını kullanır.</span><span class="sxs-lookup"><span data-stu-id="f496a-216">This call is persistent: it uses a shared preferences file.</span></span>

<span data-ttu-id="f496a-217">Bu işlev çağırdığınızda katılım etkinse durdurmak hizmet için 1 dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="f496a-217">If Engagement is active when you call this function, it may take 1 minute for the service to stop.</span></span> <span data-ttu-id="f496a-218">Hizmeti her başlatıldığında başlatın olmaz ancak uygulamayı başlatın.</span><span class="sxs-lookup"><span data-stu-id="f496a-218">However it won't launch the service at all the next time you launch the application.</span></span>

<span data-ttu-id="f496a-219">Yeniden ile aynı işlevini çağırarak raporlama günlüğü etkinleştirebilirsiniz `true`.</span><span class="sxs-lookup"><span data-stu-id="f496a-219">You can enable log reporting again by calling the same function with `true`.</span></span>

### <a name="integration-in-your-own-preferenceactivity"></a><span data-ttu-id="f496a-220">Kendi tümleştirme`PreferenceActivity`</span><span class="sxs-lookup"><span data-stu-id="f496a-220">Integration in your own `PreferenceActivity`</span></span>
<span data-ttu-id="f496a-221">Bu işlevi çağırmak yerine, ayrıca bu ayarı doğrudan var olan tümleştirebilirsiniz `PreferenceActivity`.</span><span class="sxs-lookup"><span data-stu-id="f496a-221">Instead of calling this function, you can also integrate this setting directly in your existing `PreferenceActivity`.</span></span>

<span data-ttu-id="f496a-222">Tercihler dosyanız (istenen moduyla) kullanmak için katılım yapılandırabileceğiniz `AndroidManifest.xml` ile dosya `application meta-data`:</span><span class="sxs-lookup"><span data-stu-id="f496a-222">You can configure Engagement to use your preferences file (with the desired mode) in the `AndroidManifest.xml` file with `application meta-data`:</span></span>

* <span data-ttu-id="f496a-223">`engagement:agent:settings:name` Anahtar paylaşılan tercihleri dosya adını tanımlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f496a-223">The `engagement:agent:settings:name` key is used to define the name of the shared preferences file.</span></span>
* <span data-ttu-id="f496a-224">`engagement:agent:settings:mode` Anahtar paylaşılan tercihleri dosya modunu tanımlamak için kullanıldığında, aynı modunda olarak kullanması gereken, `PreferenceActivity`.</span><span class="sxs-lookup"><span data-stu-id="f496a-224">The `engagement:agent:settings:mode` key is used to define the mode of the shared preferences file, you should use the same mode as in your `PreferenceActivity`.</span></span> <span data-ttu-id="f496a-225">Mod bir sayı olarak geçirilmelidir: kodunuzda sabit bayrakları birlikte kullanıyorsanız, toplam değerini denetleyin.</span><span class="sxs-lookup"><span data-stu-id="f496a-225">The mode must be passed as a number: if you are using a combination of constant flags in your code, check the total value.</span></span>

<span data-ttu-id="f496a-226">Her zaman engagement kullanmayı `engagement:key` boolean anahtarı bu ayarı yönetmek için Tercihler dosya içinde.</span><span class="sxs-lookup"><span data-stu-id="f496a-226">Engagement always use the `engagement:key` boolean key within the preferences file for managing this setting.</span></span>

<span data-ttu-id="f496a-227">Aşağıdaki örnekte `AndroidManifest.xml` varsayılan değerleri gösterir:</span><span class="sxs-lookup"><span data-stu-id="f496a-227">The following example of `AndroidManifest.xml` shows the default values:</span></span>

            <application>
                [...]
                <meta-data
                  android:name="engagement:agent:settings:name"
                  android:value="engagement.agent" />
                <meta-data
                  android:name="engagement:agent:settings:mode"
                  android:value="0" />

<span data-ttu-id="f496a-228">Ekleyebileceğiniz sonra bir `CheckBoxPreference` , tercih yerleşiminde aşağıdakine benzer:</span><span class="sxs-lookup"><span data-stu-id="f496a-228">Then you can add a `CheckBoxPreference` in your preference layout like the following one:</span></span>

            <CheckBoxPreference
              android:key="engagement:enabled"
              android:defaultValue="true"
              android:title="Use Engagement"
              android:summaryOn="Engagement is enabled."
              android:summaryOff="Engagement is disabled." />

<!-- URLs. -->
[Device API]: http://go.microsoft.com/?linkid=9876094
