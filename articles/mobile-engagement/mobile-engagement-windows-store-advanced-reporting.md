---
title: "aaaWindows Gelişmiş Evrensel raporlama MobileApps engagement"
description: "Nasıl Azure Mobile Engagement Windows Evrensel uygulamaları ile tooIntegrate"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: ea5030bf-73ac-49b7-bc3e-c25fc10e945a
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/12/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 20968f238ef7ae9dc0b8bb6dac3fb8bdb9bc3a10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-reporting-with-hello-windows-universal-apps-engagement-sdk"></a><span data-ttu-id="24407-103">Merhaba Windows Evrensel uygulamaları Engagement SDK'sı ile Gelişmiş raporlama</span><span class="sxs-lookup"><span data-stu-id="24407-103">Advanced Reporting with hello Windows Universal Apps Engagement SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="24407-104">Evrensel Windows</span><span class="sxs-lookup"><span data-stu-id="24407-104">Universal Windows</span></span>](mobile-engagement-windows-store-advanced-reporting.md)
> * [<span data-ttu-id="24407-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="24407-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="24407-106">iOS</span><span class="sxs-lookup"><span data-stu-id="24407-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="24407-107">Android</span><span class="sxs-lookup"><span data-stu-id="24407-107">Android</span></span>](mobile-engagement-android-advanced-reporting.md)
> 
> 

<span data-ttu-id="24407-108">Bu konu Windows Evrensel uygulamanız ek raporlama senaryolarda açıklar.</span><span class="sxs-lookup"><span data-stu-id="24407-108">This topic describes additional reporting scenarios in your Windows Universal application.</span></span> <span data-ttu-id="24407-109">Bu senaryolar hello oluşturulan tooapply toohello uygulaması seçebileceği seçenekleriniz [Başlarken](mobile-engagement-windows-store-dotnet-get-started.md) Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="24407-109">These scenarios include options that you can choose tooapply toohello app created in hello [Getting Started](mobile-engagement-windows-store-dotnet-get-started.md) tutorial.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="24407-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="24407-110">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

<span data-ttu-id="24407-111">Bu öğreticiye başlamadan önce ilk hello tamamlamanız gereken [Başlarken](mobile-engagement-windows-store-dotnet-get-started.md) kasıtlı olarak doğrudan ve basit öğretici.</span><span class="sxs-lookup"><span data-stu-id="24407-111">Before starting this tutorial, you must first complete hello [Getting Started](mobile-engagement-windows-store-dotnet-get-started.md) tutorial, which is deliberately direct and simple.</span></span> <span data-ttu-id="24407-112">Bu öğretici aralarından seçim yapabileceğiniz ek seçenekler ele alınmaktadır.</span><span class="sxs-lookup"><span data-stu-id="24407-112">This tutorial covers additional options you can choose from.</span></span>

## <a name="specifying-engagement-configuration-at-runtime"></a><span data-ttu-id="24407-113">Çalışma zamanında katılım yapılandırmasını belirtme</span><span class="sxs-lookup"><span data-stu-id="24407-113">Specifying engagement configuration at runtime</span></span>
<span data-ttu-id="24407-114">Merhaba katılım yapılandırma hello Merkezi `Resources\EngagementConfiguration.xml` hello Burada belirtilmiş olan projenizin dosya [Başlarken](mobile-engagement-windows-store-dotnet-get-started.md) konu.</span><span class="sxs-lookup"><span data-stu-id="24407-114">hello Engagement configuration is centralized in hello `Resources\EngagementConfiguration.xml` file of your project, which is where it was specified in hello [Getting Started](mobile-engagement-windows-store-dotnet-get-started.md) topic.</span></span>

<span data-ttu-id="24407-115">Ancak, ayrıca, çalışma zamanında belirtebilirsiniz: yöntemi hello katılım aracı başlatmadan önce aşağıdaki hello çağırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="24407-115">But you can also specify it at runtime: you can call hello following method before hello Engagement agent initialization:</span></span>

          /* Engagement configuration. */
          EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

          /* Set hello Engagement connection string. */
          engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

          /* Initialize Engagement angent with above configuration. */
          EngagementAgent.Instance.Init(e, engagementConfiguration);



## <a name="recommended-method-overload-your-page-classes"></a><span data-ttu-id="24407-116">Önerilen yöntem: aşırı yükleme, `Page` sınıfları</span><span class="sxs-lookup"><span data-stu-id="24407-116">Recommended method: overload your `Page` classes</span></span>
<span data-ttu-id="24407-117">Katılım toocompute kullanıcıları, oturumlar, etkinlikleri, kilitlenme ve teknik istatistikleri, gerekli tüm hello günlüklerinin hello tooactivate raporlama tüm olun, `Page` alt sınıfları devral hello `EngagementPage` sınıfları.</span><span class="sxs-lookup"><span data-stu-id="24407-117">tooactivate hello reporting of all hello logs required by Engagement toocompute Users, Sessions, Activities, Crashes and Technical statistics, make all your `Page` sub-classes inherit from hello `EngagementPage` classes.</span></span>

<span data-ttu-id="24407-118">Burada, uygulamanızın bir sayfa için bir örnek verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="24407-118">Here is an example for a page of your application.</span></span> <span data-ttu-id="24407-119">Yapabileceğiniz Merhaba, uygulamanızın tüm sayfalar için aynı anlama.</span><span class="sxs-lookup"><span data-stu-id="24407-119">You can do hello same thing for all pages of your application.</span></span>

### <a name="c-source-file"></a><span data-ttu-id="24407-120">C# kaynak dosyası</span><span class="sxs-lookup"><span data-stu-id="24407-120">C# Source file</span></span>
<span data-ttu-id="24407-121">Sayfanızı değiştirmek `.xaml.cs` dosyası:</span><span class="sxs-lookup"><span data-stu-id="24407-121">Modify your page `.xaml.cs` file:</span></span>

* <span data-ttu-id="24407-122">Tooyour ekleme `using` deyimleri:</span><span class="sxs-lookup"><span data-stu-id="24407-122">Add tooyour `using` statements:</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="24407-123">Değiştir `Page` ile `EngagementPage`:</span><span class="sxs-lookup"><span data-stu-id="24407-123">Replace `Page` with `EngagementPage`:</span></span>

<span data-ttu-id="24407-124">**Katılım:**</span><span class="sxs-lookup"><span data-stu-id="24407-124">**Without Engagement:**</span></span>

        namespace Example
        {
          public sealed partial class ExamplePage : Page
          {
            [...]
          }
        }

<span data-ttu-id="24407-125">**Katılım ile:**</span><span class="sxs-lookup"><span data-stu-id="24407-125">**With Engagement:**</span></span>

        using Microsoft.Azure.Engagement;

        namespace Example
        {
          public sealed partial class ExamplePage : EngagementPage
          {
            [...]
          }
        }

> [!IMPORTANT]
> <span data-ttu-id="24407-126">Sayfanız hello kılıyorsa `OnNavigatedTo` yöntemi, emin toocall olması `base.OnNavigatedTo(e)`.</span><span class="sxs-lookup"><span data-stu-id="24407-126">If your page overrides hello `OnNavigatedTo` method, be sure toocall `base.OnNavigatedTo(e)`.</span></span> <span data-ttu-id="24407-127">Aksi takdirde hello etkinlik olması bildirilmedi (Merhaba `EngagementPage` çağrıları `StartActivity` içinde kendi `OnNavigatedTo` yöntemi).</span><span class="sxs-lookup"><span data-stu-id="24407-127">Otherwise, hello activity is not be reported (hello `EngagementPage` calls `StartActivity` inside its `OnNavigatedTo` method).</span></span>
> 
> 

### <a name="xaml-file"></a><span data-ttu-id="24407-128">XAML dosyası</span><span class="sxs-lookup"><span data-stu-id="24407-128">XAML file</span></span>
<span data-ttu-id="24407-129">Sayfanızı değiştirmek `.xaml` dosyası:</span><span class="sxs-lookup"><span data-stu-id="24407-129">Modify your page `.xaml` file:</span></span>

* <span data-ttu-id="24407-130">Tooyour ad alanları bildirimleri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="24407-130">Add tooyour namespaces declarations:</span></span>
  
      xmlns:engagement="using:Microsoft.Azure.Engagement"
* <span data-ttu-id="24407-131">Değiştir `Page` ile `engagement:EngagementPage`:</span><span class="sxs-lookup"><span data-stu-id="24407-131">Replace `Page` with `engagement:EngagementPage`:</span></span>

<span data-ttu-id="24407-132">**Katılım:**</span><span class="sxs-lookup"><span data-stu-id="24407-132">**Without Engagement:**</span></span>

        <Page>
            <!-- layout -->
            ...
        </Page>

<span data-ttu-id="24407-133">**Katılım ile:**</span><span class="sxs-lookup"><span data-stu-id="24407-133">**With Engagement:**</span></span>

        <engagement:EngagementPage
            xmlns:engagement="using:Microsoft.Azure.Engagement">
            <!-- layout -->
            ...
        </engagement:EngagementPage >

### <a name="override-hello-default-behaviour"></a><span data-ttu-id="24407-134">Merhaba varsayılan davranışı geçersiz kılma</span><span class="sxs-lookup"><span data-stu-id="24407-134">Override hello default behaviour</span></span>
<span data-ttu-id="24407-135">Varsayılan olarak, hiçbir ek ile Merhaba etkinlik adı olarak hello sınıf adı hello sayfasının bildirilir.</span><span class="sxs-lookup"><span data-stu-id="24407-135">By default, hello class name of hello page is reported as hello activity name, with no extra.</span></span> <span data-ttu-id="24407-136">Merhaba sınıfı hello "Sayfa" soneki kullanıyorsa, katılım kaldırır.</span><span class="sxs-lookup"><span data-stu-id="24407-136">If hello class uses hello "Page" suffix, Engagement removes it.</span></span>

<span data-ttu-id="24407-137">toooverride hello varsayılan davranışı hello adı için bu kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="24407-137">toooverride hello default behavior for hello name, add this code:</span></span>

        // in hello .xaml.cs file
        protected override string GetEngagementPageName()
        {
          /* your code */
          return "new name";
        }

<span data-ttu-id="24407-138">tooreport ek bilgilerle, etkinlik bu kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="24407-138">tooreport extra information with your activity, add this code:</span></span>

        // in hello .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
          /* your code */
          return extra;
        }

<span data-ttu-id="24407-139">Bu yöntemler içinde hello denir `OnNavigatedTo` sayfanızın yöntemi.</span><span class="sxs-lookup"><span data-stu-id="24407-139">These methods are called from within hello `OnNavigatedTo` method of your page.</span></span>

### <a name="alternate-method-call-startactivity-manually"></a><span data-ttu-id="24407-140">Alternatif yöntem: çağrı `StartActivity()` el ile</span><span class="sxs-lookup"><span data-stu-id="24407-140">Alternate method: call `StartActivity()` manually</span></span>
<span data-ttu-id="24407-141">Olamaz ya da toooverload istiyor musunuz, `Page` sınıfları, bunun yerine, çağırarak etkinliklerinizi başlatabilirsiniz `EngagementAgent` doğrudan yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="24407-141">If you cannot or do not want toooverload your `Page` classes, you can instead start your activities by calling `EngagementAgent` methods directly.</span></span>

<span data-ttu-id="24407-142">Arama öneririz `StartActivity` içinde `OnNavigatedTo` sayfanızın yöntemi.</span><span class="sxs-lookup"><span data-stu-id="24407-142">We recommend calling `StartActivity` inside your `OnNavigatedTo` method of your Page.</span></span>

            protected override void OnNavigatedTo(NavigationEventArgs e)
            {
              base.OnNavigatedTo(e);
              EngagementAgent.Instance.StartActivity("MyPage");
            }

> [!IMPORTANT]
> <span data-ttu-id="24407-143">Doğru oturumunuzu sonlandırmak emin olun.</span><span class="sxs-lookup"><span data-stu-id="24407-143">Ensure you end your session correctly.</span></span>
> 
> <span data-ttu-id="24407-144">Merhaba Windows Evrensel SDK otomatik olarak çağırır hello `EndActivity` hello uygulama kapatıldığında yöntemi.</span><span class="sxs-lookup"><span data-stu-id="24407-144">hello Windows Universal SDK automatically calls hello `EndActivity` method when hello application is closed.</span></span> <span data-ttu-id="24407-145">Bu nedenle, olan **yüksek oranda** toocall hello önerilen `StartActivity` hello kullanıcının hello etkinliği değiştirdiğinizde, yöntemi ve çok**hiçbir zaman** çağrısı hello `EndActivity` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="24407-145">Thus, it is **HIGHLY** recommended toocall hello `StartActivity` method whenever hello activity of hello user change, and too**NEVER** call hello `EndActivity` method.</span></span> <span data-ttu-id="24407-146">Bu yöntem hello geçerli kullanıcının tüm uygulama günlüklerini etkiler Merhaba uygulaması ayrıldı hello katılım sunucusuna bildirir.</span><span class="sxs-lookup"><span data-stu-id="24407-146">This method notifies hello Engagement server that hello current user has left hello application, which will impact all application logs.</span></span>
> 
> 

## <a name="advanced-reporting"></a><span data-ttu-id="24407-147">Gelişmiş raporlama</span><span class="sxs-lookup"><span data-stu-id="24407-147">Advanced reporting</span></span>
<span data-ttu-id="24407-148">İsteğe bağlı olarak, böylece tooreport uygulamaya özgü olaylar, hatalar ve işleri, toodo isteyebilirsiniz, kullanım hello diğer yöntemleri bulunanlar hello `EngagementAgent` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="24407-148">Optionally, you may want tooreport application-specific events, errors and jobs, toodo so, use hello others methods found in hello `EngagementAgent` class.</span></span> <span data-ttu-id="24407-149">Merhaba katılım API tüm Engagement'ın gelişmiş özelliklerini kullanılmasına izin verir.</span><span class="sxs-lookup"><span data-stu-id="24407-149">hello Engagement API allows use of all Engagement's advanced capabilities.</span></span>

<span data-ttu-id="24407-150">Daha fazla bilgi için bkz: [nasıl toouse hello Mobile Engagement Windows Evrensel uygulamanız API etiketleme Gelişmiş](mobile-engagement-windows-store-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="24407-150">For further information, see [How toouse hello advanced Mobile Engagement tagging API in your Windows Universal app](mobile-engagement-windows-store-use-engagement-api.md).</span></span>

