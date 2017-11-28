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
# <a name="location-reporting-for-azure-mobile-engagement-android-sdk"></a><span data-ttu-id="1d28e-103">Azure Mobile Engagement Android SDK'sı için raporlama konumu</span><span class="sxs-lookup"><span data-stu-id="1d28e-103">Location Reporting for Azure Mobile Engagement Android SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1d28e-104">Android</span><span class="sxs-lookup"><span data-stu-id="1d28e-104">Android</span></span>](mobile-engagement-android-integrate-engagement.md)
> 
> 

<span data-ttu-id="1d28e-105">Bu konuda açıklanmaktadır nasıl Android uygulamanız için raporlama toodo konumu.</span><span class="sxs-lookup"><span data-stu-id="1d28e-105">This topic describes how toodo location reporting for your Android application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1d28e-106">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="1d28e-106">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

## <a name="location-reporting"></a><span data-ttu-id="1d28e-107">Konum raporlama</span><span class="sxs-lookup"><span data-stu-id="1d28e-107">Location reporting</span></span>
<span data-ttu-id="1d28e-108">Bildirilen konumları toobe istiyorsanız, birkaç satırlı yapılandırma tooadd gerekir (Merhaba arasında `<application>` ve `</application>` etiketleri).</span><span class="sxs-lookup"><span data-stu-id="1d28e-108">If you want locations toobe reported, you need tooadd a few lines of configuration (between hello `<application>` and `</application>` tags).</span></span>

### <a name="lazy-area-location-reporting"></a><span data-ttu-id="1d28e-109">Yavaş alan konumu raporlama</span><span class="sxs-lookup"><span data-stu-id="1d28e-109">Lazy area location reporting</span></span>
<span data-ttu-id="1d28e-110">Yavaş alan konumu raporlama raporlama hello ülke, bölgeye ve yere göre cihazlarla ilişkilendirilmiş sağlar.</span><span class="sxs-lookup"><span data-stu-id="1d28e-110">Lazy area location reporting enables reporting hello country, region, and locality associated with devices.</span></span> <span data-ttu-id="1d28e-111">Bu tür konumu raporlama yalnızca ağ konumlarını (hücre kimliği veya WIFI göre) kullanır.</span><span class="sxs-lookup"><span data-stu-id="1d28e-111">This type of location reporting only uses network locations (based on Cell ID or WIFI).</span></span> <span data-ttu-id="1d28e-112">Merhaba aygıt alanına oturum başına en fazla bir kez bildirilir.</span><span class="sxs-lookup"><span data-stu-id="1d28e-112">hello device area is reported at most once per session.</span></span> <span data-ttu-id="1d28e-113">Hello GPS hiçbir zaman kullanılmaz ve bu nedenle bu konumu rapor düşük etkisi hello pilde türü.</span><span class="sxs-lookup"><span data-stu-id="1d28e-113">hello GPS is never used, and thus this type of location report has low impact on hello battery.</span></span>

<span data-ttu-id="1d28e-114">Kullanıcılar, oturumlar, olayları ve hataları ile ilgili kullanılan toocompute coğrafi istatistikleri bildirilen alanlarıdır.</span><span class="sxs-lookup"><span data-stu-id="1d28e-114">Reported areas are used toocompute geographic statistics about users, sessions, events, and errors.</span></span> <span data-ttu-id="1d28e-115">Reach kampanyaları ölçütü olarak de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="1d28e-115">They can also be used as criterion in Reach campaigns.</span></span>

<span data-ttu-id="1d28e-116">Bu yordamda daha önce bahsedilen hello yapılandırmayı kullanarak raporlama yavaş alan konumu etkinleştirin:</span><span class="sxs-lookup"><span data-stu-id="1d28e-116">You enable lazy area location reporting by using hello configuration previously mentioned in this procedure:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setLazyAreaLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="1d28e-117">Ayrıca toospecify bir konuma izni gerekir.</span><span class="sxs-lookup"><span data-stu-id="1d28e-117">You also need toospecify a location permission.</span></span> <span data-ttu-id="1d28e-118">Bu kodu kullanır ``COARSE`` izin:</span><span class="sxs-lookup"><span data-stu-id="1d28e-118">This code uses ``COARSE`` permission:</span></span>

    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

<span data-ttu-id="1d28e-119">Uygulamanızı gerektiriyorsa, kullanabileceğiniz ``ACCESS_FINE_LOCATION`` yerine.</span><span class="sxs-lookup"><span data-stu-id="1d28e-119">If your app requires it, you can use ``ACCESS_FINE_LOCATION`` instead.</span></span>

### <a name="real-time-location-reporting"></a><span data-ttu-id="1d28e-120">Gerçek zamanlı konum raporlama</span><span class="sxs-lookup"><span data-stu-id="1d28e-120">Real-time location reporting</span></span>
<span data-ttu-id="1d28e-121">Gerçek zamanlı konum raporlama raporlama hello enlem ve boylam cihazlarla ilişkilendirilmiş sağlar.</span><span class="sxs-lookup"><span data-stu-id="1d28e-121">Real-time location reporting enables reporting hello latitude and longitude associated with devices.</span></span> <span data-ttu-id="1d28e-122">Varsayılan olarak, bu tür konumu raporlama yalnızca hücre kimliği veya WIFI göre ağ konumlarını kullanır.</span><span class="sxs-lookup"><span data-stu-id="1d28e-122">By default, this type of location reporting only uses network locations, based on Cell ID or WIFI.</span></span> <span data-ttu-id="1d28e-123">Merhaba raporlama Hello uygulama ön planda (örneğin, bir oturum sırasında) çalıştığında etkindir.</span><span class="sxs-lookup"><span data-stu-id="1d28e-123">hello reporting is only active when hello application runs in foreground (for example, during a session).</span></span>

<span data-ttu-id="1d28e-124">Gerçek zamanlı konumlarının *değil* toocompute istatistikleri kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1d28e-124">Real-time locations are *NOT* used toocompute statistics.</span></span> <span data-ttu-id="1d28e-125">Yalnızca amaçlarına tooallow hello gerçek zamanlı coğrafi yalıtma kullanımıdır \<Reach-İzleyici-bölge sınırlaması\> Reach kampanyaları ölçütü.</span><span class="sxs-lookup"><span data-stu-id="1d28e-125">Their only purpose is tooallow hello use of real-time geo-fencing \<Reach-Audience-geofencing\> criterion in Reach campaigns.</span></span>

<span data-ttu-id="1d28e-126">tooenable gerçek zamanlı konum raporlama, bir satır ekleyin kod toowhere hello Başlatıcısı etkinliğinde hello katılım bağlantı dizesini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="1d28e-126">tooenable real-time location reporting, add a line of code toowhere you set hello Engagement connection string in hello launcher activity.</span></span> <span data-ttu-id="1d28e-127">Merhaba sonuç hello aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="1d28e-127">hello result looks like hello following:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

        You also need toospecify a location permission. This code uses ``COARSE`` permission:

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

        If your app requires it, you can use ``ACCESS_FINE_LOCATION`` instead.

#### <a name="gps-based-reporting"></a><span data-ttu-id="1d28e-128">Raporlama GPS dayalı</span><span class="sxs-lookup"><span data-stu-id="1d28e-128">GPS based reporting</span></span>
<span data-ttu-id="1d28e-129">Varsayılan olarak, gerçek zamanlı konum raporlama ağ tabanlı konum yalnızca kullanır.</span><span class="sxs-lookup"><span data-stu-id="1d28e-129">By default, real-time location reporting only uses network-based locations.</span></span> <span data-ttu-id="1d28e-130">daha kesin, GPS tabanlı konumların tooenable hello kullanım hello yapılandırma nesnesi kullanın:</span><span class="sxs-lookup"><span data-stu-id="1d28e-130">tooenable hello use of GPS-based locations, which are far more precise, use hello configuration object:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setFineRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="1d28e-131">Ayrıca izni eksikse aşağıdaki tooadd hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="1d28e-131">You also need tooadd hello following permission if missing:</span></span>

    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>

#### <a name="background-reporting"></a><span data-ttu-id="1d28e-132">Arka plan raporlama</span><span class="sxs-lookup"><span data-stu-id="1d28e-132">Background reporting</span></span>
<span data-ttu-id="1d28e-133">Merhaba uygulama ön planda (örneğin, bir oturum sırasında) çalıştırdığında, varsayılan olarak, gerçek zamanlı konum raporlama yalnızca etkindir.</span><span class="sxs-lookup"><span data-stu-id="1d28e-133">By default, real-time location reporting is only active when hello application runs in foreground (for example, during a session).</span></span> <span data-ttu-id="1d28e-134">aynı zamanda arka planda raporlama tooenable hello bu yapılandırma nesnesini kullanın:</span><span class="sxs-lookup"><span data-stu-id="1d28e-134">tooenable hello reporting also in background, use this configuration object:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setBackgroundRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

> [!NOTE]
> <span data-ttu-id="1d28e-135">Merhaba uygulaması arka planda çalıştığında, yalnızca ağ tabanlı konumlar bildirilir, etkinleştirilmiş olsa bile GPS hello.</span><span class="sxs-lookup"><span data-stu-id="1d28e-135">When hello application runs in background, only network-based locations are reported, even if you enabled hello GPS.</span></span>
> 
> 

<span data-ttu-id="1d28e-136">Merhaba kullanıcı cihazını yeniden başlatılırsa, hello arka plan konum rapor durdurulur.</span><span class="sxs-lookup"><span data-stu-id="1d28e-136">If hello user reboots their device, hello background location report is stopped.</span></span> <span data-ttu-id="1d28e-137">önyükleme sırasında otomatik olarak yeniden toomake bu kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="1d28e-137">toomake it automatically restart at boot time, add this code.</span></span>

    <receiver android:name="com.microsoft.azure.engagement.EngagementLocationBootReceiver"
           android:exported="false">
        <intent-filter>
            <action android:name="android.intent.action.BOOT_COMPLETED" />
        </intent-filter>
    </receiver>

<span data-ttu-id="1d28e-138">Ayrıca izni eksikse aşağıdaki tooadd hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="1d28e-138">You also need tooadd hello following permission if missing:</span></span>

    <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />

## <a name="android-m-permissions"></a><span data-ttu-id="1d28e-139">Android M izinleri</span><span class="sxs-lookup"><span data-stu-id="1d28e-139">Android M permissions</span></span>
<span data-ttu-id="1d28e-140">Android M ile başlayarak, bazı izinler çalışma zamanında yönetilir ve kullanıcı onayı gerekir.</span><span class="sxs-lookup"><span data-stu-id="1d28e-140">Starting with Android M, some permissions are managed at runtime and need user approval.</span></span>

<span data-ttu-id="1d28e-141">Android API düzeyi 23 hedefliyorsanız, hello çalışma zamanı izinleri yeni uygulama yüklemeleri için varsayılan olarak kapalıdır.</span><span class="sxs-lookup"><span data-stu-id="1d28e-141">If you target Android API level 23, hello runtime permissions are turned off by default for new app installations.</span></span> <span data-ttu-id="1d28e-142">Aksi halde bunlar varsayılan olarak etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="1d28e-142">Otherwise they are turned on by default.</span></span>

<span data-ttu-id="1d28e-143">Etkinleştirebilir/hello aygıt ayarları menüsünden bu izinleri devre dışı bırakabilir.</span><span class="sxs-lookup"><span data-stu-id="1d28e-143">You can enable/disable those permissions from hello device settings menu.</span></span> <span data-ttu-id="1d28e-144">İzinleri hello sistem menüsünden kapatma sistem davranıştır ve yeteneği tooreceive itme arka planda üzerinde hiçbir etkisi olmaz hello uygulamanın hello arka plan işlemleri sonlandırır.</span><span class="sxs-lookup"><span data-stu-id="1d28e-144">Turning off permissions from hello system menu kills hello background processes of hello application, which is a system behavior, and has no impact on ability tooreceive push in background.</span></span>

<span data-ttu-id="1d28e-145">Mobile Engagement konumu raporlama Hello bağlamında, çalışma zamanında onayı iste hello izinler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="1d28e-145">In hello context of Mobile Engagement location reporting, hello permissions that require approval at runtime are:</span></span>

* `ACCESS_COARSE_LOCATION`
* `ACCESS_FINE_LOCATION`

<span data-ttu-id="1d28e-146">İzinleri standart sistem iletişim kutusunu kullanarak hello kullanıcıdan isteyin.</span><span class="sxs-lookup"><span data-stu-id="1d28e-146">Request permissions from hello user using a standard system dialog.</span></span> <span data-ttu-id="1d28e-147">Merhaba kullanıcı onaylarsa, söyleyin ``EngagementAgent`` gerçek zamanlı hesaba değiştirmek tootake.</span><span class="sxs-lookup"><span data-stu-id="1d28e-147">If hello user approves, tell ``EngagementAgent`` tootake that change into account in real-time.</span></span> <span data-ttu-id="1d28e-148">Aksi takdirde hello değişiklik işlenen hello sonraki zaman hello kullanıcı başlatır hello uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="1d28e-148">Otherwise hello change is processed hello next time hello user launches hello application.</span></span>

<span data-ttu-id="1d28e-149">Burada ise bir kod örnek toouse uygulama toorequest izinleri ve iletme hello sonuç bir etkinlikte pozitif çok``EngagementAgent``:</span><span class="sxs-lookup"><span data-stu-id="1d28e-149">Here is a code sample toouse in an activity of your application toorequest permissions and forward hello result if positive too``EngagementAgent``:</span></span>

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
