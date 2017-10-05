---
title: "Windows Phone Silverlight Engagement SDK tümleştirmesi"
description: "Azure Mobile Engagement Windows Phone Silverlight uygulamaları ile tümleştirme"
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
ms.openlocfilehash: 29b18aecff783cebf617995e2a19f16f0b68b51b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="windows-phone-silverlight-engagement-sdk-integration"></a><span data-ttu-id="d6f5e-103">Windows Phone Silverlight Engagement SDK tümleştirmesi</span><span class="sxs-lookup"><span data-stu-id="d6f5e-103">Windows Phone Silverlight Engagement SDK Integration</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d6f5e-104">Windows Evrensel</span><span class="sxs-lookup"><span data-stu-id="d6f5e-104">Windows Universal</span></span>](mobile-engagement-windows-store-integrate-engagement.md) 
> * [<span data-ttu-id="d6f5e-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="d6f5e-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md) 
> * [<span data-ttu-id="d6f5e-106">iOS</span><span class="sxs-lookup"><span data-stu-id="d6f5e-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md) 
> * [<span data-ttu-id="d6f5e-107">Android</span><span class="sxs-lookup"><span data-stu-id="d6f5e-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md) 
> 
> 

<span data-ttu-id="d6f5e-108">Bu yordam, Azure Mobile Engagement analizi ve izleme, Windows Phone Silverlight uygulamanızda işlevlerine etkinleştirmek için en basit yolu açıklar.</span><span class="sxs-lookup"><span data-stu-id="d6f5e-108">This procedure describes the simplest way to activate Azure Mobile Engagement's Analytics and Monitoring functions in your Windows Phone Silverlight application.</span></span>

<span data-ttu-id="d6f5e-109">Aşağıdaki adım kullanıcıları, oturumlar, etkinlikleri, kilitlenme ve Technicals ilgili tüm istatistikleri işlem için gereken günlükleri rapor etkinleştirmek için yeterli değildir.</span><span class="sxs-lookup"><span data-stu-id="d6f5e-109">The following steps are enough to activate the report of logs needed to compute all statistics regarding Users, Sessions, Activities, Crashes and Technicals.</span></span> <span data-ttu-id="d6f5e-110">Olaylar, hatalar ve işleri gibi diğer istatistikleri işlem için gereken günlükleri rapor katılım API kullanarak el ile yapılması gerekir (bkz [API, Windows Phone Silverlight uygulaması etiketleme Gelişmiş Mobile Engagement kullanmayı](mobile-engagement-windows-phone-use-engagement-api.md) aşağıda) Bu istatistikler uygulama bağımlı olduğundan.</span><span class="sxs-lookup"><span data-stu-id="d6f5e-110">The report of logs needed to compute other statistics like Events, Errors and Jobs must be done manually using the Engagement API (see [How to use the advanced Mobile Engagement tagging API in your Windows Phone Silverlight app](mobile-engagement-windows-phone-use-engagement-api.md) below) since these statistics are application-dependent.</span></span>

## <a name="supported-versions"></a><span data-ttu-id="d6f5e-111">Desteklenen sürümler</span><span class="sxs-lookup"><span data-stu-id="d6f5e-111">Supported versions</span></span>
<span data-ttu-id="d6f5e-112">Windows Silverlight için Mobile Engagement SDK'sı yalnızca hedefleme uygulamalara tümleştirilebilir:</span><span class="sxs-lookup"><span data-stu-id="d6f5e-112">The Mobile Engagement SDK for Windows Silverlight can only be integrated into applications targeting :</span></span>

* <span data-ttu-id="d6f5e-113">Windows Phone 8.0</span><span class="sxs-lookup"><span data-stu-id="d6f5e-113">Windows Phone 8.0</span></span>
* <span data-ttu-id="d6f5e-114">Windows Phone 8.1 Silverlight</span><span class="sxs-lookup"><span data-stu-id="d6f5e-114">Windows Phone 8.1 Silverlight</span></span>

> [!NOTE]
> <span data-ttu-id="d6f5e-115">Windows Phone 8.1 (Silverlight olmayan) hedefliyorsanız sonra başvurmak [Windows Evrensel tümleştirme yordamı](mobile-engagement-windows-store-integrate-engagement.md).</span><span class="sxs-lookup"><span data-stu-id="d6f5e-115">If you are targeting Windows Phone 8.1 (non-Silverlight) then refer to the [Windows Universal integration procedure](mobile-engagement-windows-store-integrate-engagement.md).</span></span>
> 
> 

## <a name="install-the-mobile-engagement-silverlight-sdk"></a><span data-ttu-id="d6f5e-116">Mobil katılım Silverlight SDK'sını yükleyin</span><span class="sxs-lookup"><span data-stu-id="d6f5e-116">Install the Mobile Engagement Silverlight SDK</span></span>
<span data-ttu-id="d6f5e-117">Windows Silverlight için Mobile Engagement SDK'sı olarak adlandırılan bir Nuget paketi olarak kullanılabilir *MicrosoftAzure.MobileEngagement*.</span><span class="sxs-lookup"><span data-stu-id="d6f5e-117">The Mobile Engagement SDK for Windows Silverlight is available as a Nuget package called *MicrosoftAzure.MobileEngagement*.</span></span> <span data-ttu-id="d6f5e-118">Visual Studio Nuget Paket Yöneticisi'nden yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d6f5e-118">You can install it from the Visual Studio Nuget Package Manager.</span></span> 

## <a name="add-the-capabilities"></a><span data-ttu-id="d6f5e-119">Yetenekleri ekleme</span><span class="sxs-lookup"><span data-stu-id="d6f5e-119">Add the capabilities</span></span>
<span data-ttu-id="d6f5e-120">Engagement SDK'SININ bazı özellikleri Windows Phone Silverlight SDK'ın düzgün çalışması için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="d6f5e-120">The Engagement SDK needs some capabilities of the Windows Phone Silverlight SDK in order to work properly.</span></span>

<span data-ttu-id="d6f5e-121">Açık, `WMAppManifest.xml` dosya ve aşağıdaki özellikleri de bildirilir emin `Capabilities` paneli:</span><span class="sxs-lookup"><span data-stu-id="d6f5e-121">Open your `WMAppManifest.xml` file and be sure that the following capabilities are declared in the `Capabilities` panel:</span></span>

* `ID_CAP_NETWORKING`
* `ID_CAP_IDENTITY_DEVICE`

## <a name="initialize-the-engagement-sdk"></a><span data-ttu-id="d6f5e-122">Engagement SDK'yı başlatma</span><span class="sxs-lookup"><span data-stu-id="d6f5e-122">Initialize the Engagement SDK</span></span>
### <a name="engagement-configuration"></a><span data-ttu-id="d6f5e-123">Katılım yapılandırma</span><span class="sxs-lookup"><span data-stu-id="d6f5e-123">Engagement configuration</span></span>
<span data-ttu-id="d6f5e-124">Katılım yapılandırma içinde Merkezi `Resources\EngagementConfiguration.xml` projenizin dosya.</span><span class="sxs-lookup"><span data-stu-id="d6f5e-124">The Engagement configuration is centralized in the `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="d6f5e-125">Belirtmek için bu dosyayı düzenleyin:</span><span class="sxs-lookup"><span data-stu-id="d6f5e-125">Edit this file to specify :</span></span>

* <span data-ttu-id="d6f5e-126">Uygulama bağlantı dizenizi etiketleri arasına `<connectionString>` ve `<\connectionString>`.</span><span class="sxs-lookup"><span data-stu-id="d6f5e-126">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span></span>

<span data-ttu-id="d6f5e-127">Bunun yerine çalışma zamanında belirtmek istiyorsanız, katılım aracı başlatmadan önce aşağıdaki yöntemini çağırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d6f5e-127">If you want to specify it at runtime instead, you can call the following method before the Engagement agent initialization:</span></span>

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(engagementConfiguration);

<span data-ttu-id="d6f5e-128">Bağlantı dizesi, uygulamanız için Azure Klasik Portalı'ndaki görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="d6f5e-128">The connection string for your application is displayed on the Azure Classic Portal.</span></span>

### <a name="engagement-initialization"></a><span data-ttu-id="d6f5e-129">Katılım başlatma</span><span class="sxs-lookup"><span data-stu-id="d6f5e-129">Engagement initialization</span></span>
<span data-ttu-id="d6f5e-130">Yeni bir proje oluşturduğunuzda, bir `App.xaml.cs` dosyası oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="d6f5e-130">When you create a new project, a `App.xaml.cs` file is generated.</span></span> <span data-ttu-id="d6f5e-131">Bu sınıf devraldığı `Application` ve birçok önemli yöntemler içerir.</span><span class="sxs-lookup"><span data-stu-id="d6f5e-131">This class inherits from `Application` and contains many important methods.</span></span> <span data-ttu-id="d6f5e-132">Engagement SDK'sı başlatmak için de kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d6f5e-132">It will also be used to initialize the Engagement SDK.</span></span>

<span data-ttu-id="d6f5e-133">Değiştirme `App.xaml.cs`:</span><span class="sxs-lookup"><span data-stu-id="d6f5e-133">Modify the `App.xaml.cs`:</span></span>

* <span data-ttu-id="d6f5e-134">Ekleme, `using` deyimleri:</span><span class="sxs-lookup"><span data-stu-id="d6f5e-134">Add to your `using` statements :</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="d6f5e-135">INSERT `EngagementAgent.Instance.Init` içinde `Application_Launching` yöntemi:</span><span class="sxs-lookup"><span data-stu-id="d6f5e-135">Insert `EngagementAgent.Instance.Init` in the `Application_Launching` method :</span></span>
  
      private void Application_Launching(object sender, LaunchingEventArgs e)
      {
        EngagementAgent.Instance.Init();
      }
* <span data-ttu-id="d6f5e-136">INSERT `EngagementAgent.Instance.OnActivated` içinde `Application_Activated` yöntemi:</span><span class="sxs-lookup"><span data-stu-id="d6f5e-136">Insert `EngagementAgent.Instance.OnActivated` in the `Application_Activated` method :</span></span>
  
      private void Application_Activated(object sender, ActivatedEventArgs e)
      {
         EngagementAgent.Instance.OnActivated(e);
      }

> [!WARNING]
> <span data-ttu-id="d6f5e-137">Katılım başlatma, uygulamanızın başka bir yere ekleyin kesinlikle önerilmemektedir.</span><span class="sxs-lookup"><span data-stu-id="d6f5e-137">We strongly discourage you to add the Engagement initialization in another place of your application.</span></span> <span data-ttu-id="d6f5e-138">Ancak, farkında olması, `EngagementAgent.Instance.Init` yöntemi, adanmış bir iş parçacığı üzerinde ve kullanıcı Arabirimi iş parçacığı üzerinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="d6f5e-138">However, be aware that the `EngagementAgent.Instance.Init` method runs on a dedicated thread, and not on the UI thread.</span></span>
> 
> 

## <a name="basic-reporting"></a><span data-ttu-id="d6f5e-139">Temel raporlama</span><span class="sxs-lookup"><span data-stu-id="d6f5e-139">Basic reporting</span></span>
### <a name="recommended-method--overload-your-phoneapplicationpage-classes"></a><span data-ttu-id="d6f5e-140">Önerilen yöntem: aşırı yükleme, `PhoneApplicationPage` sınıfları</span><span class="sxs-lookup"><span data-stu-id="d6f5e-140">Recommended method : overload your `PhoneApplicationPage` classes</span></span>
<span data-ttu-id="d6f5e-141">Rapor kullanıcıları, oturumlar, etkinlikleri, kilitlenme ve teknik istatistikleri işlem katılım tarafından gerekli tüm günlüklerin etkinleştirmek için yalnızca tüm yapabilirsiniz, `PhoneApplicationPage` alt sınıfları `EngagementPage` sınıfları.</span><span class="sxs-lookup"><span data-stu-id="d6f5e-141">In order to activate the report of all the logs required by Engagement to compute Users, Sessions, Activities, Crashes and Technical statistics, you can simply make all your `PhoneApplicationPage` sub-classes inherit from the `EngagementPage` classes.</span></span>

<span data-ttu-id="d6f5e-142">Bunu yapmak için uygulamanızın bir sayfa nasıl bir örneği burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="d6f5e-142">Here is an example of how to do this for a page of your application.</span></span> <span data-ttu-id="d6f5e-143">Uygulamanızın tüm sayfalar için aynı şey yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d6f5e-143">You can do the same thing for all pages of your application.</span></span>

#### <a name="c-source-file"></a><span data-ttu-id="d6f5e-144">C# kaynak dosyası</span><span class="sxs-lookup"><span data-stu-id="d6f5e-144">C# Source file</span></span>
<span data-ttu-id="d6f5e-145">Sayfanızı değiştirmek `.xaml.cs` dosyası:</span><span class="sxs-lookup"><span data-stu-id="d6f5e-145">Modify your page `.xaml.cs` file :</span></span>

* <span data-ttu-id="d6f5e-146">Ekleme, `using` deyimleri:</span><span class="sxs-lookup"><span data-stu-id="d6f5e-146">Add to your `using` statements :</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="d6f5e-147">Değiştir `PhoneApplicationPage` ile `EngagementPage` :</span><span class="sxs-lookup"><span data-stu-id="d6f5e-147">Replace `PhoneApplicationPage` with `EngagementPage` :</span></span>

<span data-ttu-id="d6f5e-148">**Katılım:**</span><span class="sxs-lookup"><span data-stu-id="d6f5e-148">**Without Engagement:**</span></span>

        namespace Example
        {
          public partial class ExamplePage : PhoneApplicationPage
          {
            [...]
          }
        }

<span data-ttu-id="d6f5e-149">**Katılım ile:**</span><span class="sxs-lookup"><span data-stu-id="d6f5e-149">**With Engagement:**</span></span>

        using Microsoft.Azure.Engagement;

        namespace Example
        {
          public partial class ExamplePage : EngagementPage 
          {
            [...]
          }
        }

> [!WARNING]
> <span data-ttu-id="d6f5e-150">Sayfanız devraldığı varsa `OnNavigatedTo` yöntemi, izin vermek dikkatli olun `base.OnNavigatedTo(e)` çağırın.</span><span class="sxs-lookup"><span data-stu-id="d6f5e-150">If your page inherits from the `OnNavigatedTo` method, be careful to let the `base.OnNavigatedTo(e)` call.</span></span> <span data-ttu-id="d6f5e-151">Aksi takdirde etkinlik raporlanmaz.</span><span class="sxs-lookup"><span data-stu-id="d6f5e-151">Otherwise, the activity will not be reported.</span></span> <span data-ttu-id="d6f5e-152">Aslında, `EngagementPage` arayan `StartActivity` içinde `OnNavigatedTo` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="d6f5e-152">Indeed, the `EngagementPage` is calling `StartActivity` inside the `OnNavigatedTo` method.</span></span>
> 
> 

#### <a name="xaml-file"></a><span data-ttu-id="d6f5e-153">XAML dosyası</span><span class="sxs-lookup"><span data-stu-id="d6f5e-153">XAML file</span></span>
<span data-ttu-id="d6f5e-154">Sayfanızı değiştirmek `.xaml` dosyası:</span><span class="sxs-lookup"><span data-stu-id="d6f5e-154">Modify your page `.xaml` file :</span></span>

* <span data-ttu-id="d6f5e-155">Ad alanı bildirimlerinize ekleyin:</span><span class="sxs-lookup"><span data-stu-id="d6f5e-155">Add to your namespaces declarations :</span></span>
  
      xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
* <span data-ttu-id="d6f5e-156">Değiştir `phone:PhoneApplicationPage` ile `engagement:EngagementPage` :</span><span class="sxs-lookup"><span data-stu-id="d6f5e-156">Replace `phone:PhoneApplicationPage` with `engagement:EngagementPage` :</span></span>

<span data-ttu-id="d6f5e-157">**Katılım:**</span><span class="sxs-lookup"><span data-stu-id="d6f5e-157">**Without Engagement:**</span></span>

        <phone:PhoneApplicationPage>
            <!-- layout -->
        </phone:PhoneApplicationPage>

<span data-ttu-id="d6f5e-158">**Katılım ile:**</span><span class="sxs-lookup"><span data-stu-id="d6f5e-158">**With Engagement:**</span></span>

        <engagement:EngagementPage 
            xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP">

            <!-- layout -->
        </engagement:EngagementPage >

#### <a name="override-the-default-behavior"></a><span data-ttu-id="d6f5e-159">Varsayılan davranışı geçersiz kılma</span><span class="sxs-lookup"><span data-stu-id="d6f5e-159">Override the default behavior</span></span>
<span data-ttu-id="d6f5e-160">Varsayılan olarak, sayfa sınıf adını etkinlik adıyla hiçbir ek olarak bildirilir.</span><span class="sxs-lookup"><span data-stu-id="d6f5e-160">By default, the class name of the page is reported as the activity name, with no extra.</span></span> <span data-ttu-id="d6f5e-161">Sınıf "Sayfa" soneki kullanıyorsa, katılım bunu de kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="d6f5e-161">If the class uses the "Page" suffix, Engagement will also remove it.</span></span>

<span data-ttu-id="d6f5e-162">Yalnızca ad varsayılan davranışı geçersiz kılmak istiyorsanız, bunu kodunuzu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="d6f5e-162">If you want to override the default behavior for the name, simply add this to your code:</span></span>

        // in the .xaml.cs file
        protected override string GetEngagementPageName()
        {
           /* your code */
           return "new name";
        }

<span data-ttu-id="d6f5e-163">Bazı ek bilgiler etkinliklerinizi ile rapor istiyorsanız, bu kodunuzu ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d6f5e-163">If you want to report some extra information with your activity, you can add this to your code:</span></span>

        // in the .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
           /* your code */
           return extra;
        }

<span data-ttu-id="d6f5e-164">Bu yöntemler içinden adlı `OnNavigatedTo` sayfanızın yöntemi.</span><span class="sxs-lookup"><span data-stu-id="d6f5e-164">These methods are called from within the `OnNavigatedTo` method of your page.</span></span>

### <a name="alternate-method-call-startactivity-manually"></a><span data-ttu-id="d6f5e-165">Alternatif yöntem: çağrı `StartActivity()` el ile</span><span class="sxs-lookup"><span data-stu-id="d6f5e-165">Alternate method: call `StartActivity()` manually</span></span>
<span data-ttu-id="d6f5e-166">Olamaz ya da tekrar etmek istiyor musunuz, `PhoneApplicationPage` sınıfları, bunun yerine, çağırarak etkinliklerinizi başlatabilirsiniz `EngagementAgent` doğrudan yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="d6f5e-166">If you cannot or do not want to overload your `PhoneApplicationPage` classes, you can instead start your activities by calling `EngagementAgent` methods directly.</span></span>

<span data-ttu-id="d6f5e-167">Arama öneririz `StartActivity` içinde `OnNavigatedTo` , mainpage yöntemi.</span><span class="sxs-lookup"><span data-stu-id="d6f5e-167">We recommend calling `StartActivity` inside your `OnNavigatedTo` method of your PhoneApplicationPage.</span></span>

        protected override void OnNavigatedTo(NavigationEventArgs e)
        {
           base.OnNavigatedTo(e);
           EngagementAgent.Instance.StartActivity("MyPage");
        }

> [!IMPORTANT]
> <span data-ttu-id="d6f5e-168">Doğru oturumunuzu sonlandırmak emin olun.</span><span class="sxs-lookup"><span data-stu-id="d6f5e-168">Ensure you end your session correctly.</span></span>
> 
> <span data-ttu-id="d6f5e-169">SDK'yı otomatik olarak çağırır `EndActivity` uygulama kapatıldığında yöntemi.</span><span class="sxs-lookup"><span data-stu-id="d6f5e-169">The SDK automatically calls the `EndActivity` method when the application is closed.</span></span> <span data-ttu-id="d6f5e-170">Bu nedenle, olan **yüksek oranda** çağırmak için önerilen `StartActivity` kullanıcı etkinliği değiştirdiğinizde, yöntemi ve **hiçbir zaman** çağrısı `EndActivity` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="d6f5e-170">Thus, it is **HIGHLY** recommended to call the `StartActivity` method whenever the activity of the user change, and to **NEVER** call the `EndActivity` method.</span></span> <span data-ttu-id="d6f5e-171">Bu yöntem geçerli kullanıcının uygulama ayrıldı ve bu tüm uygulama günlüklerini etkiler katılım sunucusuna bir ileti gönderir.</span><span class="sxs-lookup"><span data-stu-id="d6f5e-171">This method sends a message to the Engagement server that the current user has left the application and this impacts all application logs.</span></span>
> 
> 

## <a name="advanced-reporting"></a><span data-ttu-id="d6f5e-172">Gelişmiş raporlama</span><span class="sxs-lookup"><span data-stu-id="d6f5e-172">Advanced reporting</span></span>
<span data-ttu-id="d6f5e-173">İsteğe bağlı olarak, rapor uygulama belirli olaylar, hatalar ve işleri isteyebilirsiniz Bunu yapmak için diğer yöntemleri bulunan kullanın `EngagementAgent` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="d6f5e-173">Optionally, you may want to report application specific events, errors and jobs, to do so, use the others methods found in the `EngagementAgent` class.</span></span> <span data-ttu-id="d6f5e-174">Tüm Engagement'ın gelişmiş özelliklerinden kullanacak şekilde katılım API sağlar.</span><span class="sxs-lookup"><span data-stu-id="d6f5e-174">The Engagement API allows to use all of Engagement's advanced capabilities.</span></span>

<span data-ttu-id="d6f5e-175">Daha fazla bilgi için bkz: [API, Windows Phone Silverlight uygulaması etiketleme Gelişmiş Mobile Engagement kullanmayı](mobile-engagement-windows-phone-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="d6f5e-175">For further information, see [How to use the advanced Mobile Engagement tagging API in your Windows Phone Silverlight app](mobile-engagement-windows-phone-use-engagement-api.md).</span></span>

## <a name="advanced-configuration"></a><span data-ttu-id="d6f5e-176">Gelişmiş yapılandırma</span><span class="sxs-lookup"><span data-stu-id="d6f5e-176">Advanced configuration</span></span>
### <a name="disable-automatic-crash-reporting"></a><span data-ttu-id="d6f5e-177">Otomatik Kilitlenme bildirimini devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="d6f5e-177">Disable automatic crash reporting</span></span>
<span data-ttu-id="d6f5e-178">Otomatik Kilitlenme raporlama katılım özelliği devre dışı bırakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d6f5e-178">You can disable the automatic crash reporting feature of Engagement.</span></span> <span data-ttu-id="d6f5e-179">Ardından, işlenmeyen bir özel durum meydana gelir, katılım hiçbir şey olmaz.</span><span class="sxs-lookup"><span data-stu-id="d6f5e-179">Then, when an unhandled exception will occur, Engagement won't do anything.</span></span>

> [!WARNING]
> <span data-ttu-id="d6f5e-180">Bu özelliği devre dışı planlıyorsanız, uygulamanızda işlenmeyen bir kilitlenme meydana gelir, katılım kilitlenme göndermez unutmayın **ve** oturum ve işleri kapanmaz.</span><span class="sxs-lookup"><span data-stu-id="d6f5e-180">If you plan to disable this feature, be aware that when a unhandled crash will occur in your app, Engagement will not send the crash **AND** it will not close the session and jobs.</span></span>
> 
> 

<span data-ttu-id="d6f5e-181">Otomatik Kilitlenme bildirimini devre dışı bırakmak için yalnızca yapılandırmanıza bağlı olarak, bildirilen şekilde özelleştirin:</span><span class="sxs-lookup"><span data-stu-id="d6f5e-181">To disable automatic crash reporting, just customize your configuration depending on the way you declared it :</span></span>

#### <a name="from-engagementconfigurationxml-file"></a><span data-ttu-id="d6f5e-182">Gelen `EngagementConfiguration.xml` dosyası</span><span class="sxs-lookup"><span data-stu-id="d6f5e-182">From `EngagementConfiguration.xml` file</span></span>
<span data-ttu-id="d6f5e-183">Kümesine rapor kilitlenme `false` arasında `<reportCrash>` ve `</reportCrash>` etiketler.</span><span class="sxs-lookup"><span data-stu-id="d6f5e-183">Set report crash to `false` between `<reportCrash>` and `</reportCrash>` tags.</span></span>

#### <a name="from-engagementconfiguration-object-at-run-time"></a><span data-ttu-id="d6f5e-184">Gelen `EngagementConfiguration` çalışma zamanında nesne</span><span class="sxs-lookup"><span data-stu-id="d6f5e-184">From `EngagementConfiguration` object at run time</span></span>
<span data-ttu-id="d6f5e-185">Rapor kilitlenme EngagementConfiguration nesnesini kullanarak false olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="d6f5e-185">Set report crash to false using your EngagementConfiguration object.</span></span>

        /* Engagement configuration. */

        EngagementConfiguration engagementConfiguration = new EngagementConfiguration(); engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";
        /\* Disable Engagement crash reporting. \*/ engagementConfiguration.Agent.ReportCrash = false;

### <a name="burst-mode"></a><span data-ttu-id="d6f5e-186">Veri bloğu modu</span><span class="sxs-lookup"><span data-stu-id="d6f5e-186">Burst mode</span></span>
<span data-ttu-id="d6f5e-187">Varsayılan olarak, katılım hizmet raporları gerçek zamanlı olarak günlüğe kaydeder.</span><span class="sxs-lookup"><span data-stu-id="d6f5e-187">By default, the Engagement service reports logs in real time.</span></span> <span data-ttu-id="d6f5e-188">Uygulamanızı günlükleri çok sık bildirirse, günlükleri arabellek ve (Buna "veri bloğu modu" denir) tümünü bir defada bir normal zaman üzerinde temel bildirmek için daha iyi olur.</span><span class="sxs-lookup"><span data-stu-id="d6f5e-188">If your application reports logs very frequently, it is better to buffer the logs and to report them all at once on a regular time base (this is called the “burst mode”).</span></span>

<span data-ttu-id="d6f5e-189">Bunu yapmak için yöntemi çağırın:</span><span class="sxs-lookup"><span data-stu-id="d6f5e-189">To do so, call the method:</span></span>

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

<span data-ttu-id="d6f5e-190">Bağımsız değişkeni olarak bir değerdir **milisaniye**.</span><span class="sxs-lookup"><span data-stu-id="d6f5e-190">The argument is a value in **milliseconds**.</span></span> <span data-ttu-id="d6f5e-191">Gerçek zamanlı günlük yeniden etkinleştirmek isterseniz, herhangi bir zamanda yalnızca herhangi bir parametre olmadan veya 0 değeri yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="d6f5e-191">At any time, if you want to reactivate the real-time logging, just call the method without any parameter, or with the 0 value.</span></span>

<span data-ttu-id="d6f5e-192">Veri bloğu modu biraz pil ömrünün artırabilirsiniz ancak Engagement İzleyicisi üzerinde bir etkisi vardır: tüm oturumları ve işleri süre (dolayısıyla, oturumlar ve işleri veri bloğu eşik görünmeyebilir daha kısa) veri bloğu eşik yuvarlanır.</span><span class="sxs-lookup"><span data-stu-id="d6f5e-192">The burst mode slightly increase the battery life but has an impact on the Engagement Monitor: all sessions and jobs duration will be rounded to the burst threshold (thus, sessions and jobs shorter than the burst threshold may not be visible).</span></span> <span data-ttu-id="d6f5e-193">Bir veri bloğu eşikten artık 30000 (30s) kullanılması önerilir.</span><span class="sxs-lookup"><span data-stu-id="d6f5e-193">It is recommended to use a burst threshold no longer than 30000 (30s).</span></span> <span data-ttu-id="d6f5e-194">Günlükleri kaydedilen 300 öğelerle sınırlandırılır farkında olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d6f5e-194">You have to be aware that saved logs are limited to 300 items.</span></span> <span data-ttu-id="d6f5e-195">Gönderme çok uzunsa, bazı günlükleri kaybedebilir.</span><span class="sxs-lookup"><span data-stu-id="d6f5e-195">If sending is too long you can lose some logs.</span></span>

> [!WARNING]
> <span data-ttu-id="d6f5e-196">Veri bloğu eşiği daha düşük bir süre yapılandırılamaz bir saniye daha.</span><span class="sxs-lookup"><span data-stu-id="d6f5e-196">The burst threshold cannot be configured to a period lesser than one second.</span></span> <span data-ttu-id="d6f5e-197">SDK'yı otomatik olarak varsayılan değer olarak sıfırlamak olacaktır ve hata izleme gösterecektir bunun çalışırsanız, diğer bir deyişle, sıfır saniye.</span><span class="sxs-lookup"><span data-stu-id="d6f5e-197">If you try to do so, the SDK will show a trace with the error and will automatically reset to the default value, that is, zero seconds.</span></span> <span data-ttu-id="d6f5e-198">Bu günlükler gerçek zamanlı rapor için SDK tetikler.</span><span class="sxs-lookup"><span data-stu-id="d6f5e-198">This will trigger the SDK to report the logs in real-time.</span></span>
> 
> 

