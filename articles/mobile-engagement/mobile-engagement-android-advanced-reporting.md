---
title: "Raporlama seçenekleri için Azure Mobile Engagement Android SDK aaaAdvanced"
description: "Nasıl toodo raporlama toocapture analizi için Azure Mobile Engagement Android SDK Gelişmiş açıklar"
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
ms.openlocfilehash: 5c8f4ea36c54715f4e09fd43c96132c15019a71b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-reporting-with-engagement-on-android"></a><span data-ttu-id="84747-103">Gelişmiş Android katılım ile raporlama</span><span class="sxs-lookup"><span data-stu-id="84747-103">Advanced Reporting with Engagement on Android</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="84747-104">Evrensel Windows</span><span class="sxs-lookup"><span data-stu-id="84747-104">Universal Windows</span></span>](mobile-engagement-windows-store-integrate-engagement.md)
> * [<span data-ttu-id="84747-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="84747-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="84747-106">iOS</span><span class="sxs-lookup"><span data-stu-id="84747-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="84747-107">Android</span><span class="sxs-lookup"><span data-stu-id="84747-107">Android</span></span>](mobile-engagement-android-advanced-reporting.md)
> 
> 

<span data-ttu-id="84747-108">Bu konuda, Android uygulamanızdaki ek raporlama senaryolar açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="84747-108">This topic describes additional reporting scenarios in your Android application.</span></span> <span data-ttu-id="84747-109">Hello oluşturulan bu seçenekleri toohello uygulaması uygulayabilirsiniz [Başlarken](mobile-engagement-android-get-started.md) Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="84747-109">You can apply these options toohello app created in hello [Getting Started](mobile-engagement-android-get-started.md) tutorial.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="84747-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="84747-110">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

<span data-ttu-id="84747-111">Başlangıç Öğreticisi, tamamlandı kasıtlı olarak doğrudan ve basit ancak Gelişmiş seçebileceğiniz seçenekleri.</span><span class="sxs-lookup"><span data-stu-id="84747-111">hello tutorial you completed was deliberately direct and simple, but there are advanced options you can choose.</span></span>

## <a name="modifying-your-activity-classes"></a><span data-ttu-id="84747-112">Değiştirme, `Activity` sınıfları</span><span class="sxs-lookup"><span data-stu-id="84747-112">Modifying your `Activity` classes</span></span>
<span data-ttu-id="84747-113">Merhaba, [Başlarken Öğreticisi](mobile-engagement-android-get-started.md), tüm toodo sahip olan toomake, `*Activity` alt sınıfların devral hello karşılık gelen `Engagement*Activity` sınıfları.</span><span class="sxs-lookup"><span data-stu-id="84747-113">In hello [Getting Started tutorial](mobile-engagement-android-get-started.md), all you had toodo was toomake your `*Activity` subclasses inherit from hello corresponding `Engagement*Activity` classes.</span></span> <span data-ttu-id="84747-114">Örneğin, eski etkinliklerinizi Genişletilmiş `ListActivity`, genişletme yapacağı `EngagementListActivity`.</span><span class="sxs-lookup"><span data-stu-id="84747-114">For example, if your legacy activity extended `ListActivity`, you would make it extend `EngagementListActivity`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="84747-115">Kullanırken `EngagementListActivity` veya `EngagementExpandableListActivity`, emin olun herhangi bir çağrıda çok`requestWindowFeature(...);` hello çağrısından önce çok yapılan`super.onCreate(...);`, aksi halde bir kilitlenme oluşur.</span><span class="sxs-lookup"><span data-stu-id="84747-115">When using `EngagementListActivity` or `EngagementExpandableListActivity`, make sure any call too`requestWindowFeature(...);` is made before hello call too`super.onCreate(...);`, otherwise a crash occurs.</span></span>
> 
> 

<span data-ttu-id="84747-116">Bu sınıfların hello bulabilirsiniz `src` klasörünü ve bunları projenize kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="84747-116">You can find these classes in hello `src` folder, and can copy them into your project.</span></span> <span data-ttu-id="84747-117">Merhaba sınıflardır ayrıca hello **JavaDoc**.</span><span class="sxs-lookup"><span data-stu-id="84747-117">hello classes are also in hello **JavaDoc**.</span></span>

## <a name="alternate-method-call-startactivity-and-endactivity-manually"></a><span data-ttu-id="84747-118">Alternatif yöntem: çağrı `startActivity()` ve `endActivity()` el ile</span><span class="sxs-lookup"><span data-stu-id="84747-118">Alternate method: call `startActivity()` and `endActivity()` manually</span></span>
<span data-ttu-id="84747-119">Olamaz ya da toooverload istiyor musunuz, `Activity` sınıfları, bunun yerine başlatabilir ve hello çağırarak etkinliklerinizi bitiş `EngagementAgent`'s doğrudan yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="84747-119">If you cannot or do not want toooverload your `Activity` classes, you can instead start and end your activities by calling hello `EngagementAgent`'s methods directly.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="84747-120">Merhaba Android SDK hiçbir zaman hello çağırır `endActivity()` Merhaba uygulaması kapalı olduğunda bile yöntemi (Android, uygulamaları hiçbir zaman kapalı).</span><span class="sxs-lookup"><span data-stu-id="84747-120">hello Android SDK never calls hello `endActivity()` method, even when hello application is closed (on Android, applications are never closed).</span></span> <span data-ttu-id="84747-121">Bu nedenle, olan *yüksek oranda* toocall hello önerilen `startActivity()` hello yönteminde `onResume` , geri çağırma *tüm* etkinlikleri ve hello `endActivity()` hello yönteminde `onPause()` geri arama, *tüm* etkinliklerinizi.</span><span class="sxs-lookup"><span data-stu-id="84747-121">Thus, it is *HIGHLY* recommended toocall hello `startActivity()` method in hello `onResume` callback of *ALL* your activities, and hello `endActivity()` method in hello `onPause()` callback of *ALL* your activities.</span></span> <span data-ttu-id="84747-122">Bu hello tek yolu toobe oturumları sızdırılmaz emin olur.</span><span class="sxs-lookup"><span data-stu-id="84747-122">This is hello only way toobe sure that sessions are not leaked.</span></span> <span data-ttu-id="84747-123">Bir oturum sızmasını varsa (bir oturum bekleyen olduğu sürece hello hizmet bağlı kalır bu yana) hello katılım hizmet hiçbir zaman hello katılım arka ucundan bağlantısını keser.</span><span class="sxs-lookup"><span data-stu-id="84747-123">If a session is leaked, hello Engagement service never disconnects from hello Engagement backend (since hello service stays connected as long as a session is pending).</span></span>
> 
> 

<span data-ttu-id="84747-124">Örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="84747-124">Here is an example:</span></span>

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

<span data-ttu-id="84747-125">Bu örnekte, benzer toohello `EngagementActivity` sınıfı ve kaynak kodu hello sağlanan türevleri `src` klasör.</span><span class="sxs-lookup"><span data-stu-id="84747-125">This example is similar toohello `EngagementActivity` class and its variants, whose source code is provided in hello `src` folder.</span></span>

## <a name="using-applicationoncreate"></a><span data-ttu-id="84747-126">Application.onCreate() kullanma</span><span class="sxs-lookup"><span data-stu-id="84747-126">Using Application.onCreate()</span></span>
<span data-ttu-id="84747-127">Yerleştirdiğiniz içinde herhangi bir kod `Application.onCreate()` ve başka bir uygulamada geri aramalar hello katılım hizmeti dahil olmak üzere tüm uygulama işlemleri için çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="84747-127">Any code you place in `Application.onCreate()` and in other application callbacks is run for all your application's processes, including hello Engagement service.</span></span> <span data-ttu-id="84747-128">Gereksiz bellek ayırma ve hello Engagement'ın işlemdeki iş parçacıklarını gibi istenmeyen yan etkileri olabilir veya yinelenen yayın alıcıları veya hizmetleri.</span><span class="sxs-lookup"><span data-stu-id="84747-128">It may have unwanted side effects, like unneeded memory allocations and threads in hello Engagement's process, or duplicate broadcast receivers or services.</span></span>

<span data-ttu-id="84747-129">Geçersiz kılarsanız `Application.onCreate()`, aşağıdaki kod parçacığını hello başında hello ekleme öneririz, `Application.onCreate()` işlevi:</span><span class="sxs-lookup"><span data-stu-id="84747-129">If you override `Application.onCreate()`, we recommend adding hello following code snippet at hello beginning of your `Application.onCreate()` function:</span></span>

     public void onCreate()
     {
       if (EngagementAgentUtils.isInDedicatedEngagementProcess(this))
         return;

       ... Your code...
     }

<span data-ttu-id="84747-130">Yapabileceğiniz hello aynı şeyi `Application.onTerminate()`, `Application.onLowMemory()`, ve `Application.onConfigurationChanged(...)`.</span><span class="sxs-lookup"><span data-stu-id="84747-130">You can do hello same thing for `Application.onTerminate()`, `Application.onLowMemory()`, and `Application.onConfigurationChanged(...)`.</span></span>

<span data-ttu-id="84747-131">Ayrıca genişletebilirsiniz `EngagementApplication` genişletme yerine `Application`: geri çağırma hello `Application.onCreate()` işlem denetimi ve çağrıları hello `Application.onApplicationProcessCreate()` hello geçerli işlem hello bir barındırma hello katılım hizmeti değil ise, hello aynı kuralları için yalnızca uygulama diğer geri aramalar hello.</span><span class="sxs-lookup"><span data-stu-id="84747-131">You can also extend `EngagementApplication` instead of extending `Application`: hello callback `Application.onCreate()` does hello process check and calls `Application.onApplicationProcessCreate()` only if hello current process is not hello one hosting hello Engagement service, hello same rules apply for hello other callbacks.</span></span>

## <a name="tags-in-hello-androidmanifestxml-file"></a><span data-ttu-id="84747-132">Merhaba AndroidManifest.xml dosyasında etiketleri</span><span class="sxs-lookup"><span data-stu-id="84747-132">Tags in hello AndroidManifest.xml file</span></span>
<span data-ttu-id="84747-133">Merhaba hizmet etiketine hello AndroidManifest.xml dosyasında hello `android:label` özniteliği verir toochoose hello hello katılım hizmet adını tooend kullanıcıların telefonlarını hello "Çalışan hizmetleri" ekranında göründüğü gibi.</span><span class="sxs-lookup"><span data-stu-id="84747-133">In hello service tag in hello AndroidManifest.xml file, hello `android:label` attribute allows you toochoose hello name of hello Engagement service as it appears tooend users in hello "Running services" screen of their phone.</span></span> <span data-ttu-id="84747-134">Bu öznitelik çok ayar önerilen`"<Your application name>Service"` (örneğin, `"AcmeFunGameService"`).</span><span class="sxs-lookup"><span data-stu-id="84747-134">We recommended setting this attribute too`"<Your application name>Service"` (for example, `"AcmeFunGameService"`).</span></span>

<span data-ttu-id="84747-135">Belirten hello `android:process` özniteliği (katılım aynı işlemi, uygulamanızın ana/kullanıcı Arabirimi iş parçacığı potansiyel olarak daha az yanıt getirir hello çalıştıran) kendi işleminde katılım hizmeti çalıştığında bu hello sağlar.</span><span class="sxs-lookup"><span data-stu-id="84747-135">Specifying hello `android:process` attribute ensures that hello Engagement service runs in its own process (running Engagement in hello same process as your application makes your main/UI thread potentially less responsive).</span></span>

## <a name="building-with-proguard"></a><span data-ttu-id="84747-136">ProGuard ile oluşturma</span><span class="sxs-lookup"><span data-stu-id="84747-136">Building with ProGuard</span></span>
<span data-ttu-id="84747-137">Uygulama paketinizi ProGuard ile yapılandırdıysanız, bazı sınıfları tookeep gerekir.</span><span class="sxs-lookup"><span data-stu-id="84747-137">If you build your application package with ProGuard, you need tookeep some classes.</span></span> <span data-ttu-id="84747-138">Yapılandırma parçacığını aşağıdaki hello kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="84747-138">You can use hello following configuration snippet:</span></span>

    -keep public class * extends android.os.IInterface
    -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {
    <methods>;
     }
