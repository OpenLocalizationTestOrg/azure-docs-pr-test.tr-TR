---
title: "Azure Mobile Engagement Android SDK'sı için raporlama konumu"
description: "Azure Mobile Engagement Android SDK için raporlama konumu yapılandırmayı açıklar"
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
ms.openlocfilehash: 777d5719cce505b55dfb61c91dcac7e713b077a9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="location-reporting-for-azure-mobile-engagement-android-sdk"></a><span data-ttu-id="5ed78-103">Azure Mobile Engagement Android SDK'sı için raporlama konumu</span><span class="sxs-lookup"><span data-stu-id="5ed78-103">Location Reporting for Azure Mobile Engagement Android SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5ed78-104">Android</span><span class="sxs-lookup"><span data-stu-id="5ed78-104">Android</span></span>](mobile-engagement-android-integrate-engagement.md)
> 
> 

<span data-ttu-id="5ed78-105">Bu konuda, Android uygulamanız için raporlama konumu yapmak açıklar.</span><span class="sxs-lookup"><span data-stu-id="5ed78-105">This topic describes how to do location reporting for your Android application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5ed78-106">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="5ed78-106">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

## <a name="location-reporting"></a><span data-ttu-id="5ed78-107">Konum raporlama</span><span class="sxs-lookup"><span data-stu-id="5ed78-107">Location reporting</span></span>
<span data-ttu-id="5ed78-108">Konumları bildirilmesini istiyorsanız, birkaç satırlı yapılandırma eklemeniz gerekir (arasında `<application>` ve `</application>` etiketleri).</span><span class="sxs-lookup"><span data-stu-id="5ed78-108">If you want locations to be reported, you need to add a few lines of configuration (between the `<application>` and `</application>` tags).</span></span>

### <a name="lazy-area-location-reporting"></a><span data-ttu-id="5ed78-109">Yavaş alan konumu raporlama</span><span class="sxs-lookup"><span data-stu-id="5ed78-109">Lazy area location reporting</span></span>
<span data-ttu-id="5ed78-110">Yavaş alan konumu raporlama ülke, bölgeye ve yere göre cihazlarla ilişkilendirilmiş raporlamayı etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="5ed78-110">Lazy area location reporting enables reporting the country, region, and locality associated with devices.</span></span> <span data-ttu-id="5ed78-111">Bu tür konumu raporlama yalnızca ağ konumlarını (hücre kimliği veya WIFI göre) kullanır.</span><span class="sxs-lookup"><span data-stu-id="5ed78-111">This type of location reporting only uses network locations (based on Cell ID or WIFI).</span></span> <span data-ttu-id="5ed78-112">Aygıt alanına oturum başına en fazla bir kez bildirilir.</span><span class="sxs-lookup"><span data-stu-id="5ed78-112">The device area is reported at most once per session.</span></span> <span data-ttu-id="5ed78-113">GPS hiçbir zaman kullanılmaz ve bu nedenle bu tür bir konum rapor düşük pil gücüyle etkisi.</span><span class="sxs-lookup"><span data-stu-id="5ed78-113">The GPS is never used, and thus this type of location report has low impact on the battery.</span></span>

<span data-ttu-id="5ed78-114">Bildirilen alanları kullanıcıları, oturumlar, olayları ve hataları ile ilgili coğrafi istatistikleri hesaplamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="5ed78-114">Reported areas are used to compute geographic statistics about users, sessions, events, and errors.</span></span> <span data-ttu-id="5ed78-115">Reach kampanyaları ölçütü olarak de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="5ed78-115">They can also be used as criterion in Reach campaigns.</span></span>

<span data-ttu-id="5ed78-116">Bu yordamda daha önce bahsedilen yapılandırmayı kullanarak raporlama yavaş alan konumu etkinleştirin:</span><span class="sxs-lookup"><span data-stu-id="5ed78-116">You enable lazy area location reporting by using the configuration previously mentioned in this procedure:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setLazyAreaLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="5ed78-117">Ayrıca bir konuma izni belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="5ed78-117">You also need to specify a location permission.</span></span> <span data-ttu-id="5ed78-118">Bu kodu kullanır ``COARSE`` izin:</span><span class="sxs-lookup"><span data-stu-id="5ed78-118">This code uses ``COARSE`` permission:</span></span>

    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

<span data-ttu-id="5ed78-119">Uygulamanızı gerektiriyorsa, kullanabileceğiniz ``ACCESS_FINE_LOCATION`` yerine.</span><span class="sxs-lookup"><span data-stu-id="5ed78-119">If your app requires it, you can use ``ACCESS_FINE_LOCATION`` instead.</span></span>

### <a name="real-time-location-reporting"></a><span data-ttu-id="5ed78-120">Gerçek zamanlı konum raporlama</span><span class="sxs-lookup"><span data-stu-id="5ed78-120">Real-time location reporting</span></span>
<span data-ttu-id="5ed78-121">Gerçek zamanlı konum raporlama enlem ve boylam cihazlarla ilişkilendirilmiş raporlamayı etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="5ed78-121">Real-time location reporting enables reporting the latitude and longitude associated with devices.</span></span> <span data-ttu-id="5ed78-122">Varsayılan olarak, bu tür konumu raporlama yalnızca hücre kimliği veya WIFI göre ağ konumlarını kullanır.</span><span class="sxs-lookup"><span data-stu-id="5ed78-122">By default, this type of location reporting only uses network locations, based on Cell ID or WIFI.</span></span> <span data-ttu-id="5ed78-123">Raporlama uygulama ön planda (örneğin, bir oturum sırasında) çalıştığında etkindir.</span><span class="sxs-lookup"><span data-stu-id="5ed78-123">The reporting is only active when the application runs in foreground (for example, during a session).</span></span>

<span data-ttu-id="5ed78-124">Gerçek zamanlı konumlarının *değil* istatistikleri hesaplamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="5ed78-124">Real-time locations are *NOT* used to compute statistics.</span></span> <span data-ttu-id="5ed78-125">Gerçek zamanlı coğrafi yalıtma kullanımına izin vermek için kendi tek amacı olan \<Reach-İzleyici-bölge sınırlaması\> Reach kampanyaları ölçütü.</span><span class="sxs-lookup"><span data-stu-id="5ed78-125">Their only purpose is to allow the use of real-time geo-fencing \<Reach-Audience-geofencing\> criterion in Reach campaigns.</span></span>

<span data-ttu-id="5ed78-126">Gerçek zamanlı konum raporlama etkinleştirmek için katılım bağlantı dizesi Başlatıcısı etkinliğinde ayarladığınız bir kod satırını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="5ed78-126">To enable real-time location reporting, add a line of code to where you set the Engagement connection string in the launcher activity.</span></span> <span data-ttu-id="5ed78-127">Sonuç aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="5ed78-127">The result looks like the following:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

        You also need to specify a location permission. This code uses ``COARSE`` permission:

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

        If your app requires it, you can use ``ACCESS_FINE_LOCATION`` instead.

#### <a name="gps-based-reporting"></a><span data-ttu-id="5ed78-128">Raporlama GPS dayalı</span><span class="sxs-lookup"><span data-stu-id="5ed78-128">GPS based reporting</span></span>
<span data-ttu-id="5ed78-129">Varsayılan olarak, gerçek zamanlı konum raporlama ağ tabanlı konum yalnızca kullanır.</span><span class="sxs-lookup"><span data-stu-id="5ed78-129">By default, real-time location reporting only uses network-based locations.</span></span> <span data-ttu-id="5ed78-130">Daha kesin, GPS tabanlı konumlarda kullanımını etkinleştirmek için yapılandırma nesnesi kullanın:</span><span class="sxs-lookup"><span data-stu-id="5ed78-130">To enable the use of GPS-based locations, which are far more precise, use the configuration object:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setFineRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="5ed78-131">Ayrıca aşağıdaki izni eksikse eklemeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="5ed78-131">You also need to add the following permission if missing:</span></span>

    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>

#### <a name="background-reporting"></a><span data-ttu-id="5ed78-132">Arka plan raporlama</span><span class="sxs-lookup"><span data-stu-id="5ed78-132">Background reporting</span></span>
<span data-ttu-id="5ed78-133">Uygulama ön planda (örneğin, bir oturum sırasında) çalıştırdığında, varsayılan olarak, gerçek zamanlı konum raporlama yalnızca etkindir.</span><span class="sxs-lookup"><span data-stu-id="5ed78-133">By default, real-time location reporting is only active when the application runs in foreground (for example, during a session).</span></span> <span data-ttu-id="5ed78-134">Ayrıca raporlama arka planda etkinleştirmek için bu yapılandırma nesnesini kullanın:</span><span class="sxs-lookup"><span data-stu-id="5ed78-134">To enable the reporting also in background, use this configuration object:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setBackgroundRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

> [!NOTE]
> <span data-ttu-id="5ed78-135">Arka planda uygulamayı çalıştırdığında, yalnızca ağ tabanlı konumlar raporlanır, GPS etkin olsa bile.</span><span class="sxs-lookup"><span data-stu-id="5ed78-135">When the application runs in background, only network-based locations are reported, even if you enabled the GPS.</span></span>
> 
> 

<span data-ttu-id="5ed78-136">Kullanıcı cihazını yeniden başlatılırsa, arka plan konum rapor durdurulur.</span><span class="sxs-lookup"><span data-stu-id="5ed78-136">If the user reboots their device, the background location report is stopped.</span></span> <span data-ttu-id="5ed78-137">Önyükleme sırasında otomatik olarak yeniden yapmak için bu kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="5ed78-137">To make it automatically restart at boot time, add this code.</span></span>

    <receiver android:name="com.microsoft.azure.engagement.EngagementLocationBootReceiver"
           android:exported="false">
        <intent-filter>
            <action android:name="android.intent.action.BOOT_COMPLETED" />
        </intent-filter>
    </receiver>

<span data-ttu-id="5ed78-138">Ayrıca aşağıdaki izni eksikse eklemeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="5ed78-138">You also need to add the following permission if missing:</span></span>

    <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />

## <a name="android-m-permissions"></a><span data-ttu-id="5ed78-139">Android M izinleri</span><span class="sxs-lookup"><span data-stu-id="5ed78-139">Android M permissions</span></span>
<span data-ttu-id="5ed78-140">Android M ile başlayarak, bazı izinler çalışma zamanında yönetilir ve kullanıcı onayı gerekir.</span><span class="sxs-lookup"><span data-stu-id="5ed78-140">Starting with Android M, some permissions are managed at runtime and need user approval.</span></span>

<span data-ttu-id="5ed78-141">Android API düzeyi 23 hedefliyorsanız, çalışma zamanı izinleri yeni uygulama yüklemeleri için varsayılan olarak kapalıdır.</span><span class="sxs-lookup"><span data-stu-id="5ed78-141">If you target Android API level 23, the runtime permissions are turned off by default for new app installations.</span></span> <span data-ttu-id="5ed78-142">Aksi halde bunlar varsayılan olarak etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="5ed78-142">Otherwise they are turned on by default.</span></span>

<span data-ttu-id="5ed78-143">Etkinleştirebilir/aygıt ayarları menüsünden bu izinleri devre dışı bırakabilir.</span><span class="sxs-lookup"><span data-stu-id="5ed78-143">You can enable/disable those permissions from the device settings menu.</span></span> <span data-ttu-id="5ed78-144">Sistem menüsünden izinleri kapatma sistem davranıştır ve anında iletme arka planda alma yeteneğini üzerinde hiçbir etkisi olmaz uygulamasının arka plan işlemleri sonlandırır.</span><span class="sxs-lookup"><span data-stu-id="5ed78-144">Turning off permissions from the system menu kills the background processes of the application, which is a system behavior, and has no impact on ability to receive push in background.</span></span>

<span data-ttu-id="5ed78-145">Mobile Engagement konumu raporlama bağlamında, çalışma zamanında onayı iste izinler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="5ed78-145">In the context of Mobile Engagement location reporting, the permissions that require approval at runtime are:</span></span>

* `ACCESS_COARSE_LOCATION`
* `ACCESS_FINE_LOCATION`

<span data-ttu-id="5ed78-146">İzinleri standart sistem iletişim kutusunu kullanarak kullanıcıdan isteyin.</span><span class="sxs-lookup"><span data-stu-id="5ed78-146">Request permissions from the user using a standard system dialog.</span></span> <span data-ttu-id="5ed78-147">Kullanıcı onaylarsa, söyleyin ``EngagementAgent`` hesaba bu değişikliği gerçek zamanlı gerçekleştirilecek.</span><span class="sxs-lookup"><span data-stu-id="5ed78-147">If the user approves, tell ``EngagementAgent`` to take that change into account in real-time.</span></span> <span data-ttu-id="5ed78-148">Aksi takdirde değişikliği kullanıcı uygulamayı başlatır sonraki zaman işlenir.</span><span class="sxs-lookup"><span data-stu-id="5ed78-148">Otherwise the change is processed the next time the user launches the application.</span></span>

<span data-ttu-id="5ed78-149">İzinleri istemek ve sonuç için pozitif varsa iletmek için uygulamanızın bir etkinlikte kullanılacak bir kod örneği işte ``EngagementAgent``:</span><span class="sxs-lookup"><span data-stu-id="5ed78-149">Here is a code sample to use in an activity of your application to request permissions and forward the result if positive to ``EngagementAgent``:</span></span>

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
         * Request location permission, but this doesn't explain why it is needed to the user.
         * The standard Android documentation explains with more details how to display a rationale activity to explain the user why the permission is needed in your application.
         * Putting COARSE vs FINE has no impact here, they are part of the same group for runtime permission management.
         */
        if (checkSelfPermission(android.Manifest.permission.ACCESS_FINE_LOCATION) != PackageManager.PERMISSION_GRANTED)
          requestPermissions(new String[] { android.Manifest.permission.ACCESS_FINE_LOCATION }, 0);

      }
    }

    @Override
    public void onRequestPermissionsResult(int requestCode, String[] permissions, int[] grantResults)
    {
      /* Only a positive location permission update requires engagement agent refresh, hence the request code matching from above function */
      if (requestCode == 0 && grantResults[0] == PackageManager.PERMISSION_GRANTED)
        getEngagementAgent().refreshPermissions();
    }
