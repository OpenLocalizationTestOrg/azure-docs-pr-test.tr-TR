---
title: "aaaWindows Phone Silverlight Engagement SDK tümleştirmesi"
description: "Nasıl Azure Mobile Engagement Windows Phone Silverlight uygulamaları ile tooIntegrate"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 447fea8d-f4e3-4ad4-8ec0-8e3cf1ad3ab0
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: f65683a62e5256cea469a3a73d99ade4331cb6bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-phone-silverlight-engagement-sdk-integration"></a><span data-ttu-id="20ab4-103">Windows Phone Silverlight Engagement SDK tümleştirmesi</span><span class="sxs-lookup"><span data-stu-id="20ab4-103">Windows Phone Silverlight Engagement SDK Integration</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="20ab4-104">Windows Evrensel</span><span class="sxs-lookup"><span data-stu-id="20ab4-104">Windows Universal</span></span>](mobile-engagement-windows-store-integrate-engagement.md) 
> * [<span data-ttu-id="20ab4-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="20ab4-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md) 
> * [<span data-ttu-id="20ab4-106">iOS</span><span class="sxs-lookup"><span data-stu-id="20ab4-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md) 
> * [<span data-ttu-id="20ab4-107">Android</span><span class="sxs-lookup"><span data-stu-id="20ab4-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md) 
> 
> 

<span data-ttu-id="20ab4-108">Bu yordam, hello en basit yolu tooactivate Azure Mobile Engagement analizi ve izleme, Windows Phone Silverlight uygulamanızda işlevlerine açıklar.</span><span class="sxs-lookup"><span data-stu-id="20ab4-108">This procedure describes hello simplest way tooactivate Azure Mobile Engagement's Analytics and Monitoring functions in your Windows Phone Silverlight application.</span></span>

<span data-ttu-id="20ab4-109">Aşağıdaki adımları hello günlüklerinin yeterli tooactivate hello rapor kullanıcıları, oturumlar, etkinlikleri, kilitlenme ve Technicals ilgili tüm istatistikleri toocompute gerekli ' dir.</span><span class="sxs-lookup"><span data-stu-id="20ab4-109">hello following steps are enough tooactivate hello report of logs needed toocompute all statistics regarding Users, Sessions, Activities, Crashes and Technicals.</span></span> <span data-ttu-id="20ab4-110">Günlükler Hello rapor olaylar, hatalar ve işleri hello katılım API kullanarak el ile yapılmalıdır gibi bu toocompute diğer istatistiklerin gerekli (bkz [nasıl toouse hello Mobile Engagement Windows Phone Silverlight uygulamanızda API etiketleme Gelişmiş](mobile-engagement-windows-phone-use-engagement-api.md) Aşağıda) bu istatistikleri uygulama bağımlı olduğundan.</span><span class="sxs-lookup"><span data-stu-id="20ab4-110">hello report of logs needed toocompute other statistics like Events, Errors and Jobs must be done manually using hello Engagement API (see [How toouse hello advanced Mobile Engagement tagging API in your Windows Phone Silverlight app](mobile-engagement-windows-phone-use-engagement-api.md) below) since these statistics are application-dependent.</span></span>

## <a name="supported-versions"></a><span data-ttu-id="20ab4-111">Desteklenen sürümler</span><span class="sxs-lookup"><span data-stu-id="20ab4-111">Supported versions</span></span>
<span data-ttu-id="20ab4-112">Merhaba Windows Silverlight için Mobile Engagement SDK'sı yalnızca hedefleme uygulamalara tümleştirilebilir:</span><span class="sxs-lookup"><span data-stu-id="20ab4-112">hello Mobile Engagement SDK for Windows Silverlight can only be integrated into applications targeting :</span></span>

* <span data-ttu-id="20ab4-113">Windows Phone 8.0</span><span class="sxs-lookup"><span data-stu-id="20ab4-113">Windows Phone 8.0</span></span>
* <span data-ttu-id="20ab4-114">Windows Phone 8.1 Silverlight</span><span class="sxs-lookup"><span data-stu-id="20ab4-114">Windows Phone 8.1 Silverlight</span></span>

> [!NOTE]
> <span data-ttu-id="20ab4-115">Windows Phone 8.1 (Silverlight olmayan) hedefliyorsanız sonra toohello başvuran [Windows Evrensel tümleştirme yordamı](mobile-engagement-windows-store-integrate-engagement.md).</span><span class="sxs-lookup"><span data-stu-id="20ab4-115">If you are targeting Windows Phone 8.1 (non-Silverlight) then refer toohello [Windows Universal integration procedure](mobile-engagement-windows-store-integrate-engagement.md).</span></span>
> 
> 

## <a name="install-hello-mobile-engagement-silverlight-sdk"></a><span data-ttu-id="20ab4-116">Merhaba Mobile Engagement Silverlight SDK yükleme</span><span class="sxs-lookup"><span data-stu-id="20ab4-116">Install hello Mobile Engagement Silverlight SDK</span></span>
<span data-ttu-id="20ab4-117">Merhaba Windows Silverlight için Mobile Engagement SDK'sı olarak adlandırılan bir Nuget paketi olarak kullanılabilir *MicrosoftAzure.MobileEngagement*.</span><span class="sxs-lookup"><span data-stu-id="20ab4-117">hello Mobile Engagement SDK for Windows Silverlight is available as a Nuget package called *MicrosoftAzure.MobileEngagement*.</span></span> <span data-ttu-id="20ab4-118">Merhaba Visual Studio Nuget Paket Yöneticisi ' yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="20ab4-118">You can install it from hello Visual Studio Nuget Package Manager.</span></span> 

## <a name="add-hello-capabilities"></a><span data-ttu-id="20ab4-119">Merhaba yetenekleri ekleme</span><span class="sxs-lookup"><span data-stu-id="20ab4-119">Add hello capabilities</span></span>
<span data-ttu-id="20ab4-120">Merhaba Engagement SDK'sı hello Windows Phone Silverlight SDK sipariş toowork bazı özellikleri düzgün gerekir.</span><span class="sxs-lookup"><span data-stu-id="20ab4-120">hello Engagement SDK needs some capabilities of hello Windows Phone Silverlight SDK in order toowork properly.</span></span>

<span data-ttu-id="20ab4-121">Açık, `WMAppManifest.xml` dosya ve yetenekleri aşağıdaki o hello hello bildirildiğinden emin `Capabilities` paneli:</span><span class="sxs-lookup"><span data-stu-id="20ab4-121">Open your `WMAppManifest.xml` file and be sure that hello following capabilities are declared in hello `Capabilities` panel:</span></span>

* `ID_CAP_NETWORKING`
* `ID_CAP_IDENTITY_DEVICE`

## <a name="initialize-hello-engagement-sdk"></a><span data-ttu-id="20ab4-122">Merhaba Engagement SDK'yı başlatma</span><span class="sxs-lookup"><span data-stu-id="20ab4-122">Initialize hello Engagement SDK</span></span>
### <a name="engagement-configuration"></a><span data-ttu-id="20ab4-123">Katılım yapılandırma</span><span class="sxs-lookup"><span data-stu-id="20ab4-123">Engagement configuration</span></span>
<span data-ttu-id="20ab4-124">Merhaba katılım yapılandırma hello Merkezi `Resources\EngagementConfiguration.xml` projenizin dosya.</span><span class="sxs-lookup"><span data-stu-id="20ab4-124">hello Engagement configuration is centralized in hello `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="20ab4-125">Bu dosya toospecify düzenleyin:</span><span class="sxs-lookup"><span data-stu-id="20ab4-125">Edit this file toospecify :</span></span>

* <span data-ttu-id="20ab4-126">Uygulama bağlantı dizenizi etiketleri arasına `<connectionString>` ve `<\connectionString>`.</span><span class="sxs-lookup"><span data-stu-id="20ab4-126">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span></span>

<span data-ttu-id="20ab4-127">Çalışma zamanında, bunun yerine, çağırabilirsiniz hello aşağıdaki toospecify istiyorsanız yöntemi hello katılım aracı başlatmadan önce:</span><span class="sxs-lookup"><span data-stu-id="20ab4-127">If you want toospecify it at runtime instead, you can call hello following method before hello Engagement agent initialization:</span></span>

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(engagementConfiguration);

<span data-ttu-id="20ab4-128">Merhaba bağlantı dizesi, uygulamanız için Klasik Azure portalı hello üzerinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="20ab4-128">hello connection string for your application is displayed on hello Azure Classic Portal.</span></span>

### <a name="engagement-initialization"></a><span data-ttu-id="20ab4-129">Katılım başlatma</span><span class="sxs-lookup"><span data-stu-id="20ab4-129">Engagement initialization</span></span>
<span data-ttu-id="20ab4-130">Yeni bir proje oluşturduğunuzda, bir `App.xaml.cs` dosyası oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="20ab4-130">When you create a new project, a `App.xaml.cs` file is generated.</span></span> <span data-ttu-id="20ab4-131">Bu sınıf devraldığı `Application` ve birçok önemli yöntemler içerir.</span><span class="sxs-lookup"><span data-stu-id="20ab4-131">This class inherits from `Application` and contains many important methods.</span></span> <span data-ttu-id="20ab4-132">Ayrıca, kullanılan tooinitialize hello Engagement SDK'sı de olur.</span><span class="sxs-lookup"><span data-stu-id="20ab4-132">It will also be used tooinitialize hello Engagement SDK.</span></span>

<span data-ttu-id="20ab4-133">Merhaba değiştirme `App.xaml.cs`:</span><span class="sxs-lookup"><span data-stu-id="20ab4-133">Modify hello `App.xaml.cs`:</span></span>

* <span data-ttu-id="20ab4-134">Tooyour ekleme `using` deyimleri:</span><span class="sxs-lookup"><span data-stu-id="20ab4-134">Add tooyour `using` statements :</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="20ab4-135">INSERT `EngagementAgent.Instance.Init` hello içinde `Application_Launching` yöntemi:</span><span class="sxs-lookup"><span data-stu-id="20ab4-135">Insert `EngagementAgent.Instance.Init` in hello `Application_Launching` method :</span></span>
  
      private void Application_Launching(object sender, LaunchingEventArgs e)
      {
        EngagementAgent.Instance.Init();
      }
* <span data-ttu-id="20ab4-136">INSERT `EngagementAgent.Instance.OnActivated` hello içinde `Application_Activated` yöntemi:</span><span class="sxs-lookup"><span data-stu-id="20ab4-136">Insert `EngagementAgent.Instance.OnActivated` in hello `Application_Activated` method :</span></span>
  
      private void Application_Activated(object sender, ActivatedEventArgs e)
      {
         EngagementAgent.Instance.OnActivated(e);
      }

> [!WARNING]
> <span data-ttu-id="20ab4-137">Biz, tooadd hello katılım başlatma, uygulamanızın başka bir yerde kesinlikle önerilmemektedir.</span><span class="sxs-lookup"><span data-stu-id="20ab4-137">We strongly discourage you tooadd hello Engagement initialization in another place of your application.</span></span> <span data-ttu-id="20ab4-138">Ancak, farkında olmanız bu hello `EngagementAgent.Instance.Init` yöntemi, adanmış bir iş parçacığı üzerinde ve hello kullanıcı Arabirimi iş parçacığı üzerinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="20ab4-138">However, be aware that hello `EngagementAgent.Instance.Init` method runs on a dedicated thread, and not on hello UI thread.</span></span>
> 
> 

## <a name="basic-reporting"></a><span data-ttu-id="20ab4-139">Temel raporlama</span><span class="sxs-lookup"><span data-stu-id="20ab4-139">Basic reporting</span></span>
### <a name="recommended-method--overload-your-phoneapplicationpage-classes"></a><span data-ttu-id="20ab4-140">Önerilen yöntem: aşırı yükleme, `PhoneApplicationPage` sınıfları</span><span class="sxs-lookup"><span data-stu-id="20ab4-140">Recommended method : overload your `PhoneApplicationPage` classes</span></span>
<span data-ttu-id="20ab4-141">Sipariş tooactivate hello raporunda katılım toocompute kullanıcıları, oturumlar, etkinlikleri, kilitlenme ve teknik istatistikleri gerekli tüm hello günlükler, yalnızca tüm yapabileceğiniz, `PhoneApplicationPage` alt sınıfları devral hello `EngagementPage` sınıfları.</span><span class="sxs-lookup"><span data-stu-id="20ab4-141">In order tooactivate hello report of all hello logs required by Engagement toocompute Users, Sessions, Activities, Crashes and Technical statistics, you can simply make all your `PhoneApplicationPage` sub-classes inherit from hello `EngagementPage` classes.</span></span>

<span data-ttu-id="20ab4-142">Örneği nasıl toodo Bu, uygulamanızın bir sayfa için.</span><span class="sxs-lookup"><span data-stu-id="20ab4-142">Here is an example of how toodo this for a page of your application.</span></span> <span data-ttu-id="20ab4-143">Yapabileceğiniz Merhaba, uygulamanızın tüm sayfalar için aynı anlama.</span><span class="sxs-lookup"><span data-stu-id="20ab4-143">You can do hello same thing for all pages of your application.</span></span>

#### <a name="c-source-file"></a><span data-ttu-id="20ab4-144">C# kaynak dosyası</span><span class="sxs-lookup"><span data-stu-id="20ab4-144">C# Source file</span></span>
<span data-ttu-id="20ab4-145">Sayfanızı değiştirmek `.xaml.cs` dosyası:</span><span class="sxs-lookup"><span data-stu-id="20ab4-145">Modify your page `.xaml.cs` file :</span></span>

* <span data-ttu-id="20ab4-146">Tooyour ekleme `using` deyimleri:</span><span class="sxs-lookup"><span data-stu-id="20ab4-146">Add tooyour `using` statements :</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="20ab4-147">Değiştir `PhoneApplicationPage` ile `EngagementPage` :</span><span class="sxs-lookup"><span data-stu-id="20ab4-147">Replace `PhoneApplicationPage` with `EngagementPage` :</span></span>

<span data-ttu-id="20ab4-148">**Katılım:**</span><span class="sxs-lookup"><span data-stu-id="20ab4-148">**Without Engagement:**</span></span>

        namespace Example
        {
          public partial class ExamplePage : PhoneApplicationPage
          {
            [...]
          }
        }

<span data-ttu-id="20ab4-149">**Katılım ile:**</span><span class="sxs-lookup"><span data-stu-id="20ab4-149">**With Engagement:**</span></span>

        using Microsoft.Azure.Engagement;

        namespace Example
        {
          public partial class ExamplePage : EngagementPage 
          {
            [...]
          }
        }

> [!WARNING]
> <span data-ttu-id="20ab4-150">Sayfanız hello devralıyorsa `OnNavigatedTo` yöntemi, dikkatli toolet hello olması `base.OnNavigatedTo(e)` çağırın.</span><span class="sxs-lookup"><span data-stu-id="20ab4-150">If your page inherits from hello `OnNavigatedTo` method, be careful toolet hello `base.OnNavigatedTo(e)` call.</span></span> <span data-ttu-id="20ab4-151">Aksi takdirde hello etkinlik raporlanmaz.</span><span class="sxs-lookup"><span data-stu-id="20ab4-151">Otherwise, hello activity will not be reported.</span></span> <span data-ttu-id="20ab4-152">Aslında, hello `EngagementPage` arayan `StartActivity` hello içinde `OnNavigatedTo` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="20ab4-152">Indeed, hello `EngagementPage` is calling `StartActivity` inside hello `OnNavigatedTo` method.</span></span>
> 
> 

#### <a name="xaml-file"></a><span data-ttu-id="20ab4-153">XAML dosyası</span><span class="sxs-lookup"><span data-stu-id="20ab4-153">XAML file</span></span>
<span data-ttu-id="20ab4-154">Sayfanızı değiştirmek `.xaml` dosyası:</span><span class="sxs-lookup"><span data-stu-id="20ab4-154">Modify your page `.xaml` file :</span></span>

* <span data-ttu-id="20ab4-155">Tooyour ad alanları bildirimleri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="20ab4-155">Add tooyour namespaces declarations :</span></span>
  
      xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
* <span data-ttu-id="20ab4-156">Değiştir `phone:PhoneApplicationPage` ile `engagement:EngagementPage` :</span><span class="sxs-lookup"><span data-stu-id="20ab4-156">Replace `phone:PhoneApplicationPage` with `engagement:EngagementPage` :</span></span>

<span data-ttu-id="20ab4-157">**Katılım:**</span><span class="sxs-lookup"><span data-stu-id="20ab4-157">**Without Engagement:**</span></span>

        <phone:PhoneApplicationPage>
            <!-- layout -->
        </phone:PhoneApplicationPage>

<span data-ttu-id="20ab4-158">**Katılım ile:**</span><span class="sxs-lookup"><span data-stu-id="20ab4-158">**With Engagement:**</span></span>

        <engagement:EngagementPage 
            xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP">

            <!-- layout -->
        </engagement:EngagementPage >

#### <a name="override-hello-default-behavior"></a><span data-ttu-id="20ab4-159">Merhaba varsayılan davranışı geçersiz kılma</span><span class="sxs-lookup"><span data-stu-id="20ab4-159">Override hello default behavior</span></span>
<span data-ttu-id="20ab4-160">Varsayılan olarak, hiçbir ek ile Merhaba etkinlik adı olarak hello sınıf adı hello sayfasının bildirilir.</span><span class="sxs-lookup"><span data-stu-id="20ab4-160">By default, hello class name of hello page is reported as hello activity name, with no extra.</span></span> <span data-ttu-id="20ab4-161">Merhaba sınıfı hello "Sayfa" soneki kullanıyorsa, katılım bunu de kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="20ab4-161">If hello class uses hello "Page" suffix, Engagement will also remove it.</span></span>

<span data-ttu-id="20ab4-162">Merhaba adını toooverride hello varsayılan davranışı istiyorsanız, yalnızca bu tooyour kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="20ab4-162">If you want toooverride hello default behavior for hello name, simply add this tooyour code:</span></span>

        // in hello .xaml.cs file
        protected override string GetEngagementPageName()
        {
           /* your code */
           return "new name";
        }

<span data-ttu-id="20ab4-163">Etkinliği ile bazı ek bilgiler tooreport istiyorsanız, bu tooyour kodu ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="20ab4-163">If you want tooreport some extra information with your activity, you can add this tooyour code:</span></span>

        // in hello .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
           /* your code */
           return extra;
        }

<span data-ttu-id="20ab4-164">Bu yöntemler içinde hello denir `OnNavigatedTo` sayfanızın yöntemi.</span><span class="sxs-lookup"><span data-stu-id="20ab4-164">These methods are called from within hello `OnNavigatedTo` method of your page.</span></span>

### <a name="alternate-method-call-startactivity-manually"></a><span data-ttu-id="20ab4-165">Alternatif yöntem: çağrı `StartActivity()` el ile</span><span class="sxs-lookup"><span data-stu-id="20ab4-165">Alternate method: call `StartActivity()` manually</span></span>
<span data-ttu-id="20ab4-166">Olamaz ya da toooverload istiyor musunuz, `PhoneApplicationPage` sınıfları, bunun yerine, çağırarak etkinliklerinizi başlatabilirsiniz `EngagementAgent` doğrudan yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="20ab4-166">If you cannot or do not want toooverload your `PhoneApplicationPage` classes, you can instead start your activities by calling `EngagementAgent` methods directly.</span></span>

<span data-ttu-id="20ab4-167">Arama öneririz `StartActivity` içinde `OnNavigatedTo` , mainpage yöntemi.</span><span class="sxs-lookup"><span data-stu-id="20ab4-167">We recommend calling `StartActivity` inside your `OnNavigatedTo` method of your PhoneApplicationPage.</span></span>

        protected override void OnNavigatedTo(NavigationEventArgs e)
        {
           base.OnNavigatedTo(e);
           EngagementAgent.Instance.StartActivity("MyPage");
        }

> [!IMPORTANT]
> <span data-ttu-id="20ab4-168">Doğru oturumunuzu sonlandırmak emin olun.</span><span class="sxs-lookup"><span data-stu-id="20ab4-168">Ensure you end your session correctly.</span></span>
> 
> <span data-ttu-id="20ab4-169">Merhaba SDK otomatik olarak çağırır hello `EndActivity` hello uygulama kapatıldığında yöntemi.</span><span class="sxs-lookup"><span data-stu-id="20ab4-169">hello SDK automatically calls hello `EndActivity` method when hello application is closed.</span></span> <span data-ttu-id="20ab4-170">Bu nedenle, olan **yüksek oranda** toocall hello önerilen `StartActivity` hello kullanıcının hello etkinliği değiştirdiğinizde, yöntemi ve çok**hiçbir zaman** çağrısı hello `EndActivity` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="20ab4-170">Thus, it is **HIGHLY** recommended toocall hello `StartActivity` method whenever hello activity of hello user change, and too**NEVER** call hello `EndActivity` method.</span></span> <span data-ttu-id="20ab4-171">Bu yöntem hello geçerli kullanıcı Merhaba uygulaması ayrıldı ve bu tüm uygulama günlüklerini etkiler message toohello katılım Sunucusu'nun gönderir.</span><span class="sxs-lookup"><span data-stu-id="20ab4-171">This method sends a message toohello Engagement server that hello current user has left hello application and this impacts all application logs.</span></span>
> 
> 

## <a name="advanced-reporting"></a><span data-ttu-id="20ab4-172">Gelişmiş raporlama</span><span class="sxs-lookup"><span data-stu-id="20ab4-172">Advanced reporting</span></span>
<span data-ttu-id="20ab4-173">İsteğe bağlı olarak, böylece tooreport uygulama belirli olayları, hataları ve işleri, toodo isteyebilirsiniz, kullanım hello diğer yöntemleri bulunanlar hello `EngagementAgent` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="20ab4-173">Optionally, you may want tooreport application specific events, errors and jobs, toodo so, use hello others methods found in hello `EngagementAgent` class.</span></span> <span data-ttu-id="20ab4-174">Merhaba katılım API toouse tüm Engagement'ın gelişmiş özelliklerinden sağlar.</span><span class="sxs-lookup"><span data-stu-id="20ab4-174">hello Engagement API allows toouse all of Engagement's advanced capabilities.</span></span>

<span data-ttu-id="20ab4-175">Daha fazla bilgi için bkz: [nasıl toouse hello Mobile Engagement Windows Phone Silverlight uygulamanızda API etiketleme Gelişmiş](mobile-engagement-windows-phone-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="20ab4-175">For further information, see [How toouse hello advanced Mobile Engagement tagging API in your Windows Phone Silverlight app](mobile-engagement-windows-phone-use-engagement-api.md).</span></span>

## <a name="advanced-configuration"></a><span data-ttu-id="20ab4-176">Gelişmiş yapılandırma</span><span class="sxs-lookup"><span data-stu-id="20ab4-176">Advanced configuration</span></span>
### <a name="disable-automatic-crash-reporting"></a><span data-ttu-id="20ab4-177">Otomatik Kilitlenme bildirimini devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="20ab4-177">Disable automatic crash reporting</span></span>
<span data-ttu-id="20ab4-178">Merhaba otomatik kilitlenme raporlama katılım özelliği devre dışı bırakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="20ab4-178">You can disable hello automatic crash reporting feature of Engagement.</span></span> <span data-ttu-id="20ab4-179">Ardından, işlenmeyen bir özel durum meydana gelir, katılım hiçbir şey olmaz.</span><span class="sxs-lookup"><span data-stu-id="20ab4-179">Then, when an unhandled exception will occur, Engagement won't do anything.</span></span>

> [!WARNING]
> <span data-ttu-id="20ab4-180">Bu özellik toodisable planlıyorsanız, uygulamanızda işlenmeyen bir kilitlenme meydana gelir, katılım hello kilitlenme göndermez unutmayın **ve** hello oturum ve işleri kapanmaz.</span><span class="sxs-lookup"><span data-stu-id="20ab4-180">If you plan toodisable this feature, be aware that when a unhandled crash will occur in your app, Engagement will not send hello crash **AND** it will not close hello session and jobs.</span></span>
> 
> 

<span data-ttu-id="20ab4-181">Raporlama toodisable otomatik kilitlenme yalnızca yapılandırmanıza bağlı olarak, bildirilen hello şekilde özelleştirin:</span><span class="sxs-lookup"><span data-stu-id="20ab4-181">toodisable automatic crash reporting, just customize your configuration depending on hello way you declared it :</span></span>

#### <a name="from-engagementconfigurationxml-file"></a><span data-ttu-id="20ab4-182">Gelen `EngagementConfiguration.xml` dosyası</span><span class="sxs-lookup"><span data-stu-id="20ab4-182">From `EngagementConfiguration.xml` file</span></span>
<span data-ttu-id="20ab4-183">Raporu çökme çok Ayarla`false` arasında `<reportCrash>` ve `</reportCrash>` etiketler.</span><span class="sxs-lookup"><span data-stu-id="20ab4-183">Set report crash too`false` between `<reportCrash>` and `</reportCrash>` tags.</span></span>

#### <a name="from-engagementconfiguration-object-at-run-time"></a><span data-ttu-id="20ab4-184">Gelen `EngagementConfiguration` çalışma zamanında nesne</span><span class="sxs-lookup"><span data-stu-id="20ab4-184">From `EngagementConfiguration` object at run time</span></span>
<span data-ttu-id="20ab4-185">EngagementConfiguration nesnesini kullanarak rapor kilitlenme toofalse ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="20ab4-185">Set report crash toofalse using your EngagementConfiguration object.</span></span>

        /* Engagement configuration. */

        EngagementConfiguration engagementConfiguration = new EngagementConfiguration(); engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";
        /\* Disable Engagement crash reporting. \*/ engagementConfiguration.Agent.ReportCrash = false;

### <a name="burst-mode"></a><span data-ttu-id="20ab4-186">Veri bloğu modu</span><span class="sxs-lookup"><span data-stu-id="20ab4-186">Burst mode</span></span>
<span data-ttu-id="20ab4-187">Varsayılan olarak, hello katılım hizmet raporları gerçek zamanlı olarak günlüğe kaydeder.</span><span class="sxs-lookup"><span data-stu-id="20ab4-187">By default, hello Engagement service reports logs in real time.</span></span> <span data-ttu-id="20ab4-188">Uygulamanızı günlükleri çok sık raporları, daha iyi toobuffer hello günlükleri ve tooreport varsa, bunları (Merhaba "veri bloğu modu" denir) tümünü bir defada bir normal zaman temel üzerinde.</span><span class="sxs-lookup"><span data-stu-id="20ab4-188">If your application reports logs very frequently, it is better toobuffer hello logs and tooreport them all at once on a regular time base (this is called hello “burst mode”).</span></span>

<span data-ttu-id="20ab4-189">toodo, bu nedenle, hello yöntemi çağırın:</span><span class="sxs-lookup"><span data-stu-id="20ab4-189">toodo so, call hello method:</span></span>

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

<span data-ttu-id="20ab4-190">Merhaba bağımsız değişkeni olarak bir değerdir **milisaniye**.</span><span class="sxs-lookup"><span data-stu-id="20ab4-190">hello argument is a value in **milliseconds**.</span></span> <span data-ttu-id="20ab4-191">Tooreactivate hello gerçek zamanlı günlük tutma istiyorsanız, herhangi bir zamanda hello yöntemini hello 0 değerine sahip veya herhangi bir parametre olmadan yalnızca çağırın.</span><span class="sxs-lookup"><span data-stu-id="20ab4-191">At any time, if you want tooreactivate hello real-time logging, just call hello method without any parameter, or with hello 0 value.</span></span>

<span data-ttu-id="20ab4-192">Merhaba veri bloğu modu biraz artırmak hello pil ömrü ancak Engagement İzleyicisi Merhaba üzerinde bir etkisi vardır: tüm oturumları ve işleri süresi yuvarlak toohello veri bloğu eşiği (Bu nedenle, oturumlar ve işleri hello veri bloğu eşik görünmeyebilir daha kısa) olacaktır.</span><span class="sxs-lookup"><span data-stu-id="20ab4-192">hello burst mode slightly increase hello battery life but has an impact on hello Engagement Monitor: all sessions and jobs duration will be rounded toohello burst threshold (thus, sessions and jobs shorter than hello burst threshold may not be visible).</span></span> <span data-ttu-id="20ab4-193">Bu bir veri bloğu eşikten artık 30000 (30s) toouse önerilir.</span><span class="sxs-lookup"><span data-stu-id="20ab4-193">It is recommended toouse a burst threshold no longer than 30000 (30s).</span></span> <span data-ttu-id="20ab4-194">Toobe Günlükleri kaydedilen sınırlı too300 öğeleridir farkında olması.</span><span class="sxs-lookup"><span data-stu-id="20ab4-194">You have toobe aware that saved logs are limited too300 items.</span></span> <span data-ttu-id="20ab4-195">Gönderme çok uzunsa, bazı günlükleri kaybedebilir.</span><span class="sxs-lookup"><span data-stu-id="20ab4-195">If sending is too long you can lose some logs.</span></span>

> [!WARNING]
> <span data-ttu-id="20ab4-196">Merhaba veri bloğu eşik tooa süresi küçük yapılandırılamaz bir saniye daha.</span><span class="sxs-lookup"><span data-stu-id="20ab4-196">hello burst threshold cannot be configured tooa period lesser than one second.</span></span> <span data-ttu-id="20ab4-197">Toodo şekilde çalışırsanız, SDK izleme hello hatasıyla göstermek ve otomatik olarak hello toohello varsayılan değer, sıfırlama diğer bir deyişle, sıfır saniye.</span><span class="sxs-lookup"><span data-stu-id="20ab4-197">If you try toodo so, hello SDK will show a trace with hello error and will automatically reset toohello default value, that is, zero seconds.</span></span> <span data-ttu-id="20ab4-198">Bu hello SDK tooreport hello günlükler gerçek zamanlı tetikler.</span><span class="sxs-lookup"><span data-stu-id="20ab4-198">This will trigger hello SDK tooreport hello logs in real-time.</span></span>
> 
> 

