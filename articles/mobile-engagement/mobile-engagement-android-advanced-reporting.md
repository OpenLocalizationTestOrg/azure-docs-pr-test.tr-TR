---
title: "Gelişmiş Azure Mobile Engagement Android SDK için raporlama seçenekleri"
description: "Analiz için Azure Mobile Engagement Android SDK yakalamak için Gelişmiş raporlama yapmak açıklar"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 7da7abd5-19d6-4892-94d8-818e5424b2cd
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/10/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 2a1445afa2c2fca1a31ad9c012b9c8a917ebf65c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="advanced-reporting-with-engagement-on-android"></a><span data-ttu-id="b91b3-103">Gelişmiş Android katılım ile raporlama</span><span class="sxs-lookup"><span data-stu-id="b91b3-103">Advanced Reporting with Engagement on Android</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b91b3-104">Evrensel Windows</span><span class="sxs-lookup"><span data-stu-id="b91b3-104">Universal Windows</span></span>](mobile-engagement-windows-store-integrate-engagement.md)
> * [<span data-ttu-id="b91b3-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="b91b3-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="b91b3-106">iOS</span><span class="sxs-lookup"><span data-stu-id="b91b3-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="b91b3-107">Android</span><span class="sxs-lookup"><span data-stu-id="b91b3-107">Android</span></span>](mobile-engagement-android-advanced-reporting.md)
> 
> 

<span data-ttu-id="b91b3-108">Bu konuda, Android uygulamanızdaki ek raporlama senaryolar açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="b91b3-108">This topic describes additional reporting scenarios in your Android application.</span></span> <span data-ttu-id="b91b3-109">Bu seçenekler oluşturduğunuz uygulama uygulayabileceğiniz [Başlarken](mobile-engagement-android-get-started.md) Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="b91b3-109">You can apply these options to the app created in the [Getting Started](mobile-engagement-android-get-started.md) tutorial.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b91b3-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="b91b3-110">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

<span data-ttu-id="b91b3-111">Tamamlandı öğretici kasıtlı olarak doğrudan ve basit ancak Gelişmiş seçebileceğiniz seçenekleri.</span><span class="sxs-lookup"><span data-stu-id="b91b3-111">The tutorial you completed was deliberately direct and simple, but there are advanced options you can choose.</span></span>

## <a name="modifying-your-activity-classes"></a><span data-ttu-id="b91b3-112">Değiştirme, `Activity` sınıfları</span><span class="sxs-lookup"><span data-stu-id="b91b3-112">Modifying your `Activity` classes</span></span>
<span data-ttu-id="b91b3-113">İçinde [Başlarken Öğreticisi](mobile-engagement-android-get-started.md), tüm yapmak için var olan yapmak için `*Activity` alt sınıfların devralır denk gelen `Engagement*Activity` sınıfları.</span><span class="sxs-lookup"><span data-stu-id="b91b3-113">In the [Getting Started tutorial](mobile-engagement-android-get-started.md), all you had to do was to make your `*Activity` subclasses inherit from the corresponding `Engagement*Activity` classes.</span></span> <span data-ttu-id="b91b3-114">Örneğin, eski etkinliklerinizi Genişletilmiş `ListActivity`, genişletme yapacağı `EngagementListActivity`.</span><span class="sxs-lookup"><span data-stu-id="b91b3-114">For example, if your legacy activity extended `ListActivity`, you would make it extend `EngagementListActivity`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b91b3-115">Kullanırken `EngagementListActivity` veya `EngagementExpandableListActivity`, aşağıdakilerden emin olun çağrı `requestWindowFeature(...);` çağırmadan önce yapılan `super.onCreate(...);`, aksi halde bir kilitlenme oluşur.</span><span class="sxs-lookup"><span data-stu-id="b91b3-115">When using `EngagementListActivity` or `EngagementExpandableListActivity`, make sure any call to `requestWindowFeature(...);` is made before the call to `super.onCreate(...);`, otherwise a crash occurs.</span></span>
> 
> 

<span data-ttu-id="b91b3-116">Bu sınıfları bulabilirsiniz `src` klasörünü ve bunları projenize kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b91b3-116">You can find these classes in the `src` folder, and can copy them into your project.</span></span> <span data-ttu-id="b91b3-117">Ayrıca, sınıflardır **JavaDoc**.</span><span class="sxs-lookup"><span data-stu-id="b91b3-117">The classes are also in the **JavaDoc**.</span></span>

## <a name="alternate-method-call-startactivity-and-endactivity-manually"></a><span data-ttu-id="b91b3-118">Alternatif yöntem: çağrı `startActivity()` ve `endActivity()` el ile</span><span class="sxs-lookup"><span data-stu-id="b91b3-118">Alternate method: call `startActivity()` and `endActivity()` manually</span></span>
<span data-ttu-id="b91b3-119">Olamaz ya da tekrar etmek istiyor musunuz, `Activity` sınıfları, bunun yerine başlangıç ve çağırarak etkinliklerinizi bitiş `EngagementAgent`'s doğrudan yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="b91b3-119">If you cannot or do not want to overload your `Activity` classes, you can instead start and end your activities by calling the `EngagementAgent`'s methods directly.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b91b3-120">Android SDK hiçbir zaman çağırır `endActivity()` uygulama kapalı olduğunda bile yöntemi (Android, uygulamaları hiçbir zaman kapalı).</span><span class="sxs-lookup"><span data-stu-id="b91b3-120">The Android SDK never calls the `endActivity()` method, even when the application is closed (on Android, applications are never closed).</span></span> <span data-ttu-id="b91b3-121">Bu nedenle, olan *yüksek oranda* çağırmak için önerilen `startActivity()` yönteminde `onResume` , geri çağırma *tüm* , etkinlikler ve `endActivity()` yönteminde `onPause()` , geri çağırma *Tüm* etkinliklerinizi.</span><span class="sxs-lookup"><span data-stu-id="b91b3-121">Thus, it is *HIGHLY* recommended to call the `startActivity()` method in the `onResume` callback of *ALL* your activities, and the `endActivity()` method in the `onPause()` callback of *ALL* your activities.</span></span> <span data-ttu-id="b91b3-122">Bu oturumlar sızdırılmaz emin olmak için tek yoludur.</span><span class="sxs-lookup"><span data-stu-id="b91b3-122">This is the only way to be sure that sessions are not leaked.</span></span> <span data-ttu-id="b91b3-123">Bir oturum sızmasını varsa (bir oturum bekleyen olduğu sürece hizmet bağlı kalır bu yana) katılım hizmet hiçbir zaman katılım arka ucundan bağlantısını keser.</span><span class="sxs-lookup"><span data-stu-id="b91b3-123">If a session is leaked, the Engagement service never disconnects from the Engagement backend (since the service stays connected as long as a session is pending).</span></span>
> 
> 

<span data-ttu-id="b91b3-124">Örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="b91b3-124">Here is an example:</span></span>

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

<span data-ttu-id="b91b3-125">Bu örnek benzer `EngagementActivity` sınıfı ve kaynak kodu sağlanır türevleri `src` klasör.</span><span class="sxs-lookup"><span data-stu-id="b91b3-125">This example is similar to the `EngagementActivity` class and its variants, whose source code is provided in the `src` folder.</span></span>

## <a name="using-applicationoncreate"></a><span data-ttu-id="b91b3-126">Application.onCreate() kullanma</span><span class="sxs-lookup"><span data-stu-id="b91b3-126">Using Application.onCreate()</span></span>
<span data-ttu-id="b91b3-127">Yerleştirdiğiniz içinde herhangi bir kod `Application.onCreate()` ve başka bir uygulamada geri aramalar katılım hizmeti dahil olmak üzere tüm uygulama işlemleri için çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="b91b3-127">Any code you place in `Application.onCreate()` and in other application callbacks is run for all your application's processes, including the Engagement service.</span></span> <span data-ttu-id="b91b3-128">Gereksiz bellek ayırma ve iş parçacıkları Engagement'ın işlemi veya yinelenen yayın alıcıları ya da Hizmetleri gibi istenmeyen yan etkileri olabilir.</span><span class="sxs-lookup"><span data-stu-id="b91b3-128">It may have unwanted side effects, like unneeded memory allocations and threads in the Engagement's process, or duplicate broadcast receivers or services.</span></span>

<span data-ttu-id="b91b3-129">Geçersiz kılarsanız `Application.onCreate()`, aşağıdaki kod parçacığını başında ekleme öneririz, `Application.onCreate()` işlevi:</span><span class="sxs-lookup"><span data-stu-id="b91b3-129">If you override `Application.onCreate()`, we recommend adding the following code snippet at the beginning of your `Application.onCreate()` function:</span></span>

     public void onCreate()
     {
       if (EngagementAgentUtils.isInDedicatedEngagementProcess(this))
         return;

       ... Your code...
     }

<span data-ttu-id="b91b3-130">Aynı şeyi yapmak `Application.onTerminate()`, `Application.onLowMemory()`, ve `Application.onConfigurationChanged(...)`.</span><span class="sxs-lookup"><span data-stu-id="b91b3-130">You can do the same thing for `Application.onTerminate()`, `Application.onLowMemory()`, and `Application.onConfigurationChanged(...)`.</span></span>

<span data-ttu-id="b91b3-131">Ayrıca genişletebilirsiniz `EngagementApplication` genişletme yerine `Application`: geri çağırma `Application.onCreate()` işlem denetimi yapar ve çağrıları `Application.onApplicationProcessCreate()` yalnızca geçerli işlem katılım hizmetini barındıran bir durumda değilse, aynı kuralları için diğer uygulama geri aramalar.</span><span class="sxs-lookup"><span data-stu-id="b91b3-131">You can also extend `EngagementApplication` instead of extending `Application`: the callback `Application.onCreate()` does the process check and calls `Application.onApplicationProcessCreate()` only if the current process is not the one hosting the Engagement service, the same rules apply for the other callbacks.</span></span>

## <a name="tags-in-the-androidmanifestxml-file"></a><span data-ttu-id="b91b3-132">AndroidManifest.xml dosyasında etiketleri</span><span class="sxs-lookup"><span data-stu-id="b91b3-132">Tags in the AndroidManifest.xml file</span></span>
<span data-ttu-id="b91b3-133">AndroidManifest.xml dosyasında hizmet etiketinde `android:label` özniteliği telefonlarını "Hizmetleri çalışır" ekranında son kullanıcılara göründüğü gibi katılım hizmetin adını seçmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="b91b3-133">In the service tag in the AndroidManifest.xml file, the `android:label` attribute allows you to choose the name of the Engagement service as it appears to end users in the "Running services" screen of their phone.</span></span> <span data-ttu-id="b91b3-134">Bu özniteliği ayarlamak önerilen `"<Your application name>Service"` (örneğin, `"AcmeFunGameService"`).</span><span class="sxs-lookup"><span data-stu-id="b91b3-134">We recommended setting this attribute to `"<Your application name>Service"` (for example, `"AcmeFunGameService"`).</span></span>

<span data-ttu-id="b91b3-135">Belirtme `android:process` özniteliği sağlar katılım hizmet (uygulamanızın ana/kullanıcı Arabirimi iş parçacığı potansiyel olarak daha az yanıt getirir katılım aynı işlem içinde çalışan) kendi işleminde çalışır.</span><span class="sxs-lookup"><span data-stu-id="b91b3-135">Specifying the `android:process` attribute ensures that the Engagement service runs in its own process (running Engagement in the same process as your application makes your main/UI thread potentially less responsive).</span></span>

## <a name="building-with-proguard"></a><span data-ttu-id="b91b3-136">ProGuard ile oluşturma</span><span class="sxs-lookup"><span data-stu-id="b91b3-136">Building with ProGuard</span></span>
<span data-ttu-id="b91b3-137">Uygulama paketinizi ProGuard ile yapılandırdıysanız, bazı sınıfları tutmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b91b3-137">If you build your application package with ProGuard, you need to keep some classes.</span></span> <span data-ttu-id="b91b3-138">Aşağıdaki yapılandırma parçacığını kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b91b3-138">You can use the following configuration snippet:</span></span>

    -keep public class * extends android.os.IInterface
    -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {
    <methods>;
     }
