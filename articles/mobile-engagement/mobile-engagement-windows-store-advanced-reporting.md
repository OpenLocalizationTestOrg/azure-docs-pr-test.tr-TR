---
title: "Gelişmiş Raporlama ile MobileApps Engagement Windows Evrensel"
description: "Azure Mobile Engagement Windows Evrensel uygulamaları ile tümleştirme"
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
ms.openlocfilehash: feac309db1ffce0945012e293bfc1df417aed876
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="advanced-reporting-with-the-windows-universal-apps-engagement-sdk"></a><span data-ttu-id="39ad9-103">Gelişmiş Windows Evrensel uygulamaları Engagement SDK'sı raporlama</span><span class="sxs-lookup"><span data-stu-id="39ad9-103">Advanced Reporting with the Windows Universal Apps Engagement SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="39ad9-104">Evrensel Windows</span><span class="sxs-lookup"><span data-stu-id="39ad9-104">Universal Windows</span></span>](mobile-engagement-windows-store-advanced-reporting.md)
> * [<span data-ttu-id="39ad9-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="39ad9-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="39ad9-106">iOS</span><span class="sxs-lookup"><span data-stu-id="39ad9-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="39ad9-107">Android</span><span class="sxs-lookup"><span data-stu-id="39ad9-107">Android</span></span>](mobile-engagement-android-advanced-reporting.md)
> 
> 

<span data-ttu-id="39ad9-108">Bu konu Windows Evrensel uygulamanız ek raporlama senaryolarda açıklar.</span><span class="sxs-lookup"><span data-stu-id="39ad9-108">This topic describes additional reporting scenarios in your Windows Universal application.</span></span> <span data-ttu-id="39ad9-109">Bu senaryolar, oluşturduğunuz uygulama uygulamak için seçebileceğiniz seçenekleriniz [Başlarken](mobile-engagement-windows-store-dotnet-get-started.md) Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="39ad9-109">These scenarios include options that you can choose to apply to the app created in the [Getting Started](mobile-engagement-windows-store-dotnet-get-started.md) tutorial.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="39ad9-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="39ad9-110">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

<span data-ttu-id="39ad9-111">Bu öğreticiye başlamadan önce ilk tamamlamalısınız [Başlarken](mobile-engagement-windows-store-dotnet-get-started.md) kasıtlı olarak doğrudan ve basit öğretici.</span><span class="sxs-lookup"><span data-stu-id="39ad9-111">Before starting this tutorial, you must first complete the [Getting Started](mobile-engagement-windows-store-dotnet-get-started.md) tutorial, which is deliberately direct and simple.</span></span> <span data-ttu-id="39ad9-112">Bu öğretici aralarından seçim yapabileceğiniz ek seçenekler ele alınmaktadır.</span><span class="sxs-lookup"><span data-stu-id="39ad9-112">This tutorial covers additional options you can choose from.</span></span>

## <a name="specifying-engagement-configuration-at-runtime"></a><span data-ttu-id="39ad9-113">Çalışma zamanında katılım yapılandırmasını belirtme</span><span class="sxs-lookup"><span data-stu-id="39ad9-113">Specifying engagement configuration at runtime</span></span>
<span data-ttu-id="39ad9-114">Katılım yapılandırma içinde Merkezi `Resources\EngagementConfiguration.xml` Burada belirtilmiş olan projenizin dosya içinde [Başlarken](mobile-engagement-windows-store-dotnet-get-started.md) konu.</span><span class="sxs-lookup"><span data-stu-id="39ad9-114">The Engagement configuration is centralized in the `Resources\EngagementConfiguration.xml` file of your project, which is where it was specified in the [Getting Started](mobile-engagement-windows-store-dotnet-get-started.md) topic.</span></span>

<span data-ttu-id="39ad9-115">Ancak, ayrıca, çalışma zamanında belirtebilirsiniz: katılım aracı başlatmadan önce aşağıdaki yöntemini çağırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="39ad9-115">But you can also specify it at runtime: you can call the following method before the Engagement agent initialization:</span></span>

          /* Engagement configuration. */
          EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

          /* Set the Engagement connection string. */
          engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

          /* Initialize Engagement angent with above configuration. */
          EngagementAgent.Instance.Init(e, engagementConfiguration);



## <a name="recommended-method-overload-your-page-classes"></a><span data-ttu-id="39ad9-116">Önerilen yöntem: aşırı yükleme, `Page` sınıfları</span><span class="sxs-lookup"><span data-stu-id="39ad9-116">Recommended method: overload your `Page` classes</span></span>
<span data-ttu-id="39ad9-117">Kullanıcılar, oturumlar, etkinlikleri, kilitlenme ve teknik istatistikleri işlem katılım tarafından gerekli tüm günlükleri raporlama etkinleştirmek için tüm olun, `Page` alt sınıfları `EngagementPage` sınıfları.</span><span class="sxs-lookup"><span data-stu-id="39ad9-117">To activate the reporting of all the logs required by Engagement to compute Users, Sessions, Activities, Crashes and Technical statistics, make all your `Page` sub-classes inherit from the `EngagementPage` classes.</span></span>

<span data-ttu-id="39ad9-118">Burada, uygulamanızın bir sayfa için bir örnek verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="39ad9-118">Here is an example for a page of your application.</span></span> <span data-ttu-id="39ad9-119">Uygulamanızın tüm sayfalar için aynı şey yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="39ad9-119">You can do the same thing for all pages of your application.</span></span>

### <a name="c-source-file"></a><span data-ttu-id="39ad9-120">C# kaynak dosyası</span><span class="sxs-lookup"><span data-stu-id="39ad9-120">C# Source file</span></span>
<span data-ttu-id="39ad9-121">Sayfanızı değiştirmek `.xaml.cs` dosyası:</span><span class="sxs-lookup"><span data-stu-id="39ad9-121">Modify your page `.xaml.cs` file:</span></span>

* <span data-ttu-id="39ad9-122">Ekleme, `using` deyimleri:</span><span class="sxs-lookup"><span data-stu-id="39ad9-122">Add to your `using` statements:</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="39ad9-123">Değiştir `Page` ile `EngagementPage`:</span><span class="sxs-lookup"><span data-stu-id="39ad9-123">Replace `Page` with `EngagementPage`:</span></span>

<span data-ttu-id="39ad9-124">**Katılım:**</span><span class="sxs-lookup"><span data-stu-id="39ad9-124">**Without Engagement:**</span></span>

        namespace Example
        {
          public sealed partial class ExamplePage : Page
          {
            [...]
          }
        }

<span data-ttu-id="39ad9-125">**Katılım ile:**</span><span class="sxs-lookup"><span data-stu-id="39ad9-125">**With Engagement:**</span></span>

        using Microsoft.Azure.Engagement;

        namespace Example
        {
          public sealed partial class ExamplePage : EngagementPage
          {
            [...]
          }
        }

> [!IMPORTANT]
> <span data-ttu-id="39ad9-126">Sayfanız `OnNavigatedTo` yöntemini geçersiz kılıyorsa `base.OnNavigatedTo(e)` öğesini çağırdığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="39ad9-126">If your page overrides the `OnNavigatedTo` method, be sure to call `base.OnNavigatedTo(e)`.</span></span> <span data-ttu-id="39ad9-127">Aksi takdirde etkinlik olması bildirilmedi ( `EngagementPage` çağrıları `StartActivity` içinde kendi `OnNavigatedTo` yöntemi).</span><span class="sxs-lookup"><span data-stu-id="39ad9-127">Otherwise, the activity is not be reported (the `EngagementPage` calls `StartActivity` inside its `OnNavigatedTo` method).</span></span>
> 
> 

### <a name="xaml-file"></a><span data-ttu-id="39ad9-128">XAML dosyası</span><span class="sxs-lookup"><span data-stu-id="39ad9-128">XAML file</span></span>
<span data-ttu-id="39ad9-129">Sayfanızı değiştirmek `.xaml` dosyası:</span><span class="sxs-lookup"><span data-stu-id="39ad9-129">Modify your page `.xaml` file:</span></span>

* <span data-ttu-id="39ad9-130">Ad alanı bildirimlerinize aşağıdakini ekleyin:</span><span class="sxs-lookup"><span data-stu-id="39ad9-130">Add to your namespaces declarations:</span></span>
  
      xmlns:engagement="using:Microsoft.Azure.Engagement"
* <span data-ttu-id="39ad9-131">Değiştir `Page` ile `engagement:EngagementPage`:</span><span class="sxs-lookup"><span data-stu-id="39ad9-131">Replace `Page` with `engagement:EngagementPage`:</span></span>

<span data-ttu-id="39ad9-132">**Katılım:**</span><span class="sxs-lookup"><span data-stu-id="39ad9-132">**Without Engagement:**</span></span>

        <Page>
            <!-- layout -->
            ...
        </Page>

<span data-ttu-id="39ad9-133">**Katılım ile:**</span><span class="sxs-lookup"><span data-stu-id="39ad9-133">**With Engagement:**</span></span>

        <engagement:EngagementPage
            xmlns:engagement="using:Microsoft.Azure.Engagement">
            <!-- layout -->
            ...
        </engagement:EngagementPage >

### <a name="override-the-default-behaviour"></a><span data-ttu-id="39ad9-134">Varsayılan davranışı geçersiz kılma</span><span class="sxs-lookup"><span data-stu-id="39ad9-134">Override the default behaviour</span></span>
<span data-ttu-id="39ad9-135">Varsayılan olarak, sayfa sınıf adını etkinlik adıyla hiçbir ek olarak bildirilir.</span><span class="sxs-lookup"><span data-stu-id="39ad9-135">By default, the class name of the page is reported as the activity name, with no extra.</span></span> <span data-ttu-id="39ad9-136">Sınıf "Sayfa" soneki kullanıyorsa, katılım kaldırır.</span><span class="sxs-lookup"><span data-stu-id="39ad9-136">If the class uses the "Page" suffix, Engagement removes it.</span></span>

<span data-ttu-id="39ad9-137">Ad için varsayılan davranışı geçersiz kılma için bu kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="39ad9-137">To override the default behavior for the name, add this code:</span></span>

        // in the .xaml.cs file
        protected override string GetEngagementPageName()
        {
          /* your code */
          return "new name";
        }

<span data-ttu-id="39ad9-138">Etkinliğiniz ek bilgilerle bildirmek için bu kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="39ad9-138">To report extra information with your activity, add this code:</span></span>

        // in the .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
          /* your code */
          return extra;
        }

<span data-ttu-id="39ad9-139">Bu yöntemler içinden adlı `OnNavigatedTo` sayfanızın yöntemi.</span><span class="sxs-lookup"><span data-stu-id="39ad9-139">These methods are called from within the `OnNavigatedTo` method of your page.</span></span>

### <a name="alternate-method-call-startactivity-manually"></a><span data-ttu-id="39ad9-140">Alternatif yöntem: çağrı `StartActivity()` el ile</span><span class="sxs-lookup"><span data-stu-id="39ad9-140">Alternate method: call `StartActivity()` manually</span></span>
<span data-ttu-id="39ad9-141">Olamaz ya da tekrar etmek istiyor musunuz, `Page` sınıfları, bunun yerine, çağırarak etkinliklerinizi başlatabilirsiniz `EngagementAgent` doğrudan yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="39ad9-141">If you cannot or do not want to overload your `Page` classes, you can instead start your activities by calling `EngagementAgent` methods directly.</span></span>

<span data-ttu-id="39ad9-142">Arama öneririz `StartActivity` içinde `OnNavigatedTo` sayfanızın yöntemi.</span><span class="sxs-lookup"><span data-stu-id="39ad9-142">We recommend calling `StartActivity` inside your `OnNavigatedTo` method of your Page.</span></span>

            protected override void OnNavigatedTo(NavigationEventArgs e)
            {
              base.OnNavigatedTo(e);
              EngagementAgent.Instance.StartActivity("MyPage");
            }

> [!IMPORTANT]
> <span data-ttu-id="39ad9-143">Doğru oturumunuzu sonlandırmak emin olun.</span><span class="sxs-lookup"><span data-stu-id="39ad9-143">Ensure you end your session correctly.</span></span>
> 
> <span data-ttu-id="39ad9-144">Windows Evrensel SDK'yı otomatik olarak çağırır `EndActivity` uygulama kapatıldığında yöntemi.</span><span class="sxs-lookup"><span data-stu-id="39ad9-144">The Windows Universal SDK automatically calls the `EndActivity` method when the application is closed.</span></span> <span data-ttu-id="39ad9-145">Bu nedenle, olan **yüksek oranda** çağırmak için önerilen `StartActivity` kullanıcı etkinliği değiştirdiğinizde, yöntemi ve **hiçbir zaman** çağrısı `EndActivity` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="39ad9-145">Thus, it is **HIGHLY** recommended to call the `StartActivity` method whenever the activity of the user change, and to **NEVER** call the `EndActivity` method.</span></span> <span data-ttu-id="39ad9-146">Bu yöntem, geçerli kullanıcının tüm uygulama günlüklerini etkiler uygulama ayrıldı katılım sunucusu bildirir.</span><span class="sxs-lookup"><span data-stu-id="39ad9-146">This method notifies the Engagement server that the current user has left the application, which will impact all application logs.</span></span>
> 
> 

## <a name="advanced-reporting"></a><span data-ttu-id="39ad9-147">Gelişmiş raporlama</span><span class="sxs-lookup"><span data-stu-id="39ad9-147">Advanced reporting</span></span>
<span data-ttu-id="39ad9-148">İsteğe bağlı olarak, uygulamaya özgü olaylar, hatalar ve bunu yapmak için işleri, kullanın diğer yöntemleri bulunan rapor isteyebilirsiniz `EngagementAgent` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="39ad9-148">Optionally, you may want to report application-specific events, errors and jobs, to do so, use the others methods found in the `EngagementAgent` class.</span></span> <span data-ttu-id="39ad9-149">Katılım API tüm Engagement'ın gelişmiş özelliklerini kullanılmasına izin verir.</span><span class="sxs-lookup"><span data-stu-id="39ad9-149">The Engagement API allows use of all Engagement's advanced capabilities.</span></span>

<span data-ttu-id="39ad9-150">Daha fazla bilgi için bkz: [Gelişmiş Mobile Engagement Windows Evrensel uygulamanız API etiketleme kullanmayı](mobile-engagement-windows-store-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="39ad9-150">For further information, see [How to use the advanced Mobile Engagement tagging API in your Windows Universal app](mobile-engagement-windows-store-use-engagement-api.md).</span></span>

