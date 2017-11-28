---
title: "aaaWindows Evrensel uygulamalar Engagement SDK tümleştirmesi"
description: "Nasıl Azure Mobile Engagement Windows Evrensel uygulamaları ile tooIntegrate"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 71236b68-5ebd-44aa-8c82-c7ca8098ea05
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 18543798099c233dbe55cc387ba0216e369c8596
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-universal-apps-engagement-sdk-integration"></a><span data-ttu-id="aa4b1-103">Windows Evrensel uygulamaları Engagement SDK tümleştirmesi</span><span class="sxs-lookup"><span data-stu-id="aa4b1-103">Windows Universal Apps Engagement SDK Integration</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="aa4b1-104">Evrensel Windows</span><span class="sxs-lookup"><span data-stu-id="aa4b1-104">Universal Windows</span></span>](mobile-engagement-windows-store-integrate-engagement.md) 
> * [<span data-ttu-id="aa4b1-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="aa4b1-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md) 
> * [<span data-ttu-id="aa4b1-106">iOS</span><span class="sxs-lookup"><span data-stu-id="aa4b1-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md) 
> * [<span data-ttu-id="aa4b1-107">Android</span><span class="sxs-lookup"><span data-stu-id="aa4b1-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md) 
> 
> 

<span data-ttu-id="aa4b1-108">Bu yordam, hello en basit yolu tooactivate Engagement analizi ve Windows Evrensel uygulamanız işlevlerde izleme açıklar.</span><span class="sxs-lookup"><span data-stu-id="aa4b1-108">This procedure describes hello simplest way tooactivate Engagement's Analytics and Monitoring functions in your Windows Universal application.</span></span>

<span data-ttu-id="aa4b1-109">Aşağıdaki adımları hello günlüklerinin yeterli tooactivate hello rapor kullanıcıları, oturumlar, etkinlikleri, kilitlenme ve Technicals ilgili tüm istatistikleri toocompute gerekli ' dir.</span><span class="sxs-lookup"><span data-stu-id="aa4b1-109">hello following steps are enough tooactivate hello report of logs needed toocompute all statistics regarding Users, Sessions, Activities, Crashes and Technicals.</span></span> <span data-ttu-id="aa4b1-110">Günlükler Hello rapor olaylar, hatalar ve işleri hello katılım API kullanarak el ile yapılmalıdır gibi bu toocompute diğer istatistiklerin gerekli (bkz [nasıl toouse hello Mobile Engagement Windows Evrensel uygulamanız API etiketleme Gelişmiş](mobile-engagement-windows-store-use-engagement-api.md) beri Bu istatistikler uygulamanın bağımlı olduğu.</span><span class="sxs-lookup"><span data-stu-id="aa4b1-110">hello report of logs needed toocompute other statistics like Events, Errors and Jobs must be done manually using hello Engagement API (see [How toouse hello advanced Mobile Engagement tagging API in your Windows Universal app](mobile-engagement-windows-store-use-engagement-api.md) since these statistics are application dependent.</span></span>

## <a name="supported-versions"></a><span data-ttu-id="aa4b1-111">Desteklenen sürümler</span><span class="sxs-lookup"><span data-stu-id="aa4b1-111">Supported versions</span></span>
<span data-ttu-id="aa4b1-112">Merhaba Mobile Engagement SDK'sı Windows Evrensel uygulamaları için yalnızca Windows çalışma zamanı ve hedefleyen Evrensel Windows platformu uygulamaları tümleştirilebilir:</span><span class="sxs-lookup"><span data-stu-id="aa4b1-112">hello Mobile Engagement SDK for Windows Universal Apps can only be integrated into Windows Runtime and Universal Windows Platform applications targeting :</span></span>

* <span data-ttu-id="aa4b1-113">Windows 8</span><span class="sxs-lookup"><span data-stu-id="aa4b1-113">Windows 8</span></span>
* <span data-ttu-id="aa4b1-114">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="aa4b1-114">Windows 8.1</span></span>
* <span data-ttu-id="aa4b1-115">Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="aa4b1-115">Windows Phone 8.1</span></span>
* <span data-ttu-id="aa4b1-116">Windows 10 (Masaüstü ve mobil aileleri)</span><span class="sxs-lookup"><span data-stu-id="aa4b1-116">Windows 10 (desktop and mobile families)</span></span>

> [!NOTE]
> <span data-ttu-id="aa4b1-117">Windows Phone Silverlight hedefleme sonra toohello başvuran [Windows Phone Silverlight tümleştirme yordamı](mobile-engagement-windows-phone-integrate-engagement.md).</span><span class="sxs-lookup"><span data-stu-id="aa4b1-117">If you are targeting Windows Phone Silverlight then refer toohello [Windows Phone Silverlight integration procedure](mobile-engagement-windows-phone-integrate-engagement.md).</span></span>
> 
> 

## <a name="install-hello-mobile-engagement-universal-apps-sdk"></a><span data-ttu-id="aa4b1-118">Merhaba Mobile Engagement Evrensel uygulamaları SDK yükleme</span><span class="sxs-lookup"><span data-stu-id="aa4b1-118">Install hello Mobile Engagement Universal Apps SDK</span></span>
### <a name="all-platforms"></a><span data-ttu-id="aa4b1-119">Tüm platformlar</span><span class="sxs-lookup"><span data-stu-id="aa4b1-119">All platforms</span></span>
<span data-ttu-id="aa4b1-120">Merhaba Mobile Engagement SDK'sı için Windows Evrensel uygulaması olarak adlandırılan bir Nuget paketi olarak kullanılabilir *MicrosoftAzure.MobileEngagement*.</span><span class="sxs-lookup"><span data-stu-id="aa4b1-120">hello Mobile Engagement SDK for Windows Universal App is available as a Nuget package called *MicrosoftAzure.MobileEngagement*.</span></span> <span data-ttu-id="aa4b1-121">Merhaba Visual Studio Nuget Paket Yöneticisi ' yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aa4b1-121">You can install it from hello Visual Studio Nuget Package Manager.</span></span>

### <a name="windows-8x-and-windows-phone-81"></a><span data-ttu-id="aa4b1-122">Windows 8.x ve Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="aa4b1-122">Windows 8.x and Windows Phone 8.1</span></span>
<span data-ttu-id="aa4b1-123">NuGet hello hello SDK kaynakları otomatik olarak dağıtan `Resources` uygulama projenizin hello kökünde klasör.</span><span class="sxs-lookup"><span data-stu-id="aa4b1-123">NuGet automatically deploys hello SDK resources in hello `Resources` folder at hello root of your application project.</span></span>

### <a name="windows-10-universal-windows-platform-applications"></a><span data-ttu-id="aa4b1-124">Windows 10 Evrensel Windows platformu uygulamaları</span><span class="sxs-lookup"><span data-stu-id="aa4b1-124">Windows 10 Universal Windows Platform applications</span></span>
<span data-ttu-id="aa4b1-125">NuGet UWP uygulaması henüz hello SDK kaynakları otomatik olarak dağıtmaz.</span><span class="sxs-lookup"><span data-stu-id="aa4b1-125">NuGet does not automatically deploy hello SDK resources in your UWP application yet.</span></span> <span data-ttu-id="aa4b1-126">El ile kaynakların dağıtımı kadar NuGet içinde yeniden girmesini toodo vardır:</span><span class="sxs-lookup"><span data-stu-id="aa4b1-126">You have toodo it manually until resources deployment is reintroduced in NuGet:</span></span>

1. <span data-ttu-id="aa4b1-127">Dosya Gezgini'ni açın.</span><span class="sxs-lookup"><span data-stu-id="aa4b1-127">Open your File Explorer.</span></span>
2. <span data-ttu-id="aa4b1-128">Konum aşağıdaki toohello gidin (**x.x.x** yüklemekte katılım hello sürümüdür): *% USERPROFILE %\\.nuget\packages\MicrosoftAzure.MobileEngagement\\ * *x.x.x**\\content\win81*</span><span class="sxs-lookup"><span data-stu-id="aa4b1-128">Navigate toohello following location (**x.x.x** is hello version of Engagement you are installing): *%USERPROFILE%\\.nuget\packages\MicrosoftAzure.MobileEngagement\\**x.x.x**\\content\win81*</span></span>
3. <span data-ttu-id="aa4b1-129">Sürükle ve bırak hello **kaynakları** hello dosya Gezgini toohello kök Visual Studio, projenizin klasöründen.</span><span class="sxs-lookup"><span data-stu-id="aa4b1-129">Drag and drop hello **Resources** folder from hello file explorer toohello root of your project in Visual Studio.</span></span>
4. <span data-ttu-id="aa4b1-130">Visual Studio projenizi seçin ve hello etkinleştirme **tüm dosyaları göster** simgesi hello üstünde **Çözüm Gezgini**.</span><span class="sxs-lookup"><span data-stu-id="aa4b1-130">In Visual Studio select your project and activate hello **Show All files** icon on top of hello **Solution Explorer**.</span></span>
5. <span data-ttu-id="aa4b1-131">Bazı dosyalar hello projeye dahil edilmez.</span><span class="sxs-lookup"><span data-stu-id="aa4b1-131">Some files are not included in hello project.</span></span> <span data-ttu-id="aa4b1-132">bunları aynı anda sağ tıklayın hello üzerinde tooimport **kaynakları** klasörü, **projeden hariç** başka sağ tıklayın ardından hello üzerinde **kaynakları** klasörünü **Ekle Proje** toore-hello tüm klasör içerir.</span><span class="sxs-lookup"><span data-stu-id="aa4b1-132">tooimport them at once right click on hello **Resources** folder, **Exclude from project** then another right click on hello **Resources** folder, **Include in project** toore-include hello whole folder.</span></span> <span data-ttu-id="aa4b1-133">Merhaba tüm dosyaları **kaynakları** klasörü projenizde eklenmiştir.</span><span class="sxs-lookup"><span data-stu-id="aa4b1-133">All files from hello **Resources** folder are now included in your project.</span></span>

## <a name="add-hello-capabilities"></a><span data-ttu-id="aa4b1-134">Merhaba yetenekleri ekleme</span><span class="sxs-lookup"><span data-stu-id="aa4b1-134">Add hello capabilities</span></span>
<span data-ttu-id="aa4b1-135">Merhaba Engagement SDK'sı hello Windows SDK sipariş toowork bazı özellikleri düzgün gerekir.</span><span class="sxs-lookup"><span data-stu-id="aa4b1-135">hello Engagement SDK needs some capabilities of hello Windows SDK in order toowork properly.</span></span>

<span data-ttu-id="aa4b1-136">Açık, `Package.appxmanifest` dosya ve yetenekleri aşağıdaki o hello bildirildiğinden emin olun:</span><span class="sxs-lookup"><span data-stu-id="aa4b1-136">Open your `Package.appxmanifest` file and be sure that hello following capabilities are declared:</span></span>

* `Internet (Client)`

## <a name="initialize-hello-engagement-sdk"></a><span data-ttu-id="aa4b1-137">Merhaba Engagement SDK'yı başlatma</span><span class="sxs-lookup"><span data-stu-id="aa4b1-137">Initialize hello Engagement SDK</span></span>
### <a name="engagement-configuration"></a><span data-ttu-id="aa4b1-138">Katılım yapılandırma</span><span class="sxs-lookup"><span data-stu-id="aa4b1-138">Engagement configuration</span></span>
<span data-ttu-id="aa4b1-139">Merhaba katılım yapılandırma hello Merkezi `Resources\EngagementConfiguration.xml` projenizin dosya.</span><span class="sxs-lookup"><span data-stu-id="aa4b1-139">hello Engagement configuration is centralized in hello `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="aa4b1-140">Bu dosya toospecify düzenleyin:</span><span class="sxs-lookup"><span data-stu-id="aa4b1-140">Edit this file toospecify:</span></span>

* <span data-ttu-id="aa4b1-141">Uygulama bağlantı dizenizi etiketleri arasına `<connectionString>` ve `<\connectionString>`.</span><span class="sxs-lookup"><span data-stu-id="aa4b1-141">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span></span>

<span data-ttu-id="aa4b1-142">Çalışma zamanında, bunun yerine, çağırabilirsiniz hello aşağıdaki toospecify istiyorsanız yöntemi hello katılım aracı başlatmadan önce:</span><span class="sxs-lookup"><span data-stu-id="aa4b1-142">If you want toospecify it at runtime instead, you can call hello following method before hello Engagement agent initialization:</span></span>

          /* Engagement configuration. */
          EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

          /* Set hello Engagement connection string. */
          engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

          /* Initialize Engagement angent with above configuration. */
          EngagementAgent.Instance.Init(e, engagementConfiguration);

<span data-ttu-id="aa4b1-143">Merhaba bağlantı dizesi, uygulamanız için Klasik Azure portalı hello üzerinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="aa4b1-143">hello connection string for your application is displayed on hello Azure Classic Portal.</span></span>

### <a name="engagement-initialization"></a><span data-ttu-id="aa4b1-144">Katılım başlatma</span><span class="sxs-lookup"><span data-stu-id="aa4b1-144">Engagement initialization</span></span>
<span data-ttu-id="aa4b1-145">Yeni bir proje oluşturduğunuzda, bir `App.xaml.cs` dosyası oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="aa4b1-145">When you create a new project, a `App.xaml.cs` file is generated.</span></span> <span data-ttu-id="aa4b1-146">Bu sınıf devraldığı `Application` ve birçok önemli yöntemler içerir.</span><span class="sxs-lookup"><span data-stu-id="aa4b1-146">This class inherits from `Application` and contains many important methods.</span></span> <span data-ttu-id="aa4b1-147">Ayrıca, kullanılan tooinitialize hello Engagement SDK'sı de olur.</span><span class="sxs-lookup"><span data-stu-id="aa4b1-147">It will also be used tooinitialize hello Engagement SDK.</span></span>

<span data-ttu-id="aa4b1-148">Merhaba değiştirme `App.xaml.cs`:</span><span class="sxs-lookup"><span data-stu-id="aa4b1-148">Modify hello `App.xaml.cs`:</span></span>

* <span data-ttu-id="aa4b1-149">Tooyour ekleme `using` deyimleri:</span><span class="sxs-lookup"><span data-stu-id="aa4b1-149">Add tooyour `using` statements:</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="aa4b1-150">Bir yöntem tooshare hello katılım başlatma tüm çağrıları için bir kez tanımlayın:</span><span class="sxs-lookup"><span data-stu-id="aa4b1-150">Define a method tooshare hello Engagement initialization once for all calls:</span></span>
  
      private void InitEngagement(IActivatedEventArgs e)
      {
        EngagementAgent.Instance.Init(e);
  
        // or
  
        EngagementAgent.Instance.Init(e, engagementConfiguration);
      }
* <span data-ttu-id="aa4b1-151">Çağrı `InitEngagement` hello içinde `OnLaunched` yöntemi:</span><span class="sxs-lookup"><span data-stu-id="aa4b1-151">Call `InitEngagement` in hello `OnLaunched` method:</span></span>
  
      protected override void OnLaunched(LaunchActivatedEventArgs e)
      {
        InitEngagement(e);
      }
* <span data-ttu-id="aa4b1-152">Özel bir şema kullanarak uygulamanızı başlatıldığında, başka bir uygulama veya hello komut satırı sonra hello `OnActivated` yöntemi çağrılır.</span><span class="sxs-lookup"><span data-stu-id="aa4b1-152">When your application is launched using a custom scheme, another application or hello command line then hello `OnActivated` method is called.</span></span> <span data-ttu-id="aa4b1-153">Uygulamanızı etkinleştirildiğinde tooinitiate hello Engagement SDK'sı da gerekir.</span><span class="sxs-lookup"><span data-stu-id="aa4b1-153">You also need tooinitiate hello Engagement SDK when your app is activated.</span></span> <span data-ttu-id="aa4b1-154">toodo bu nedenle, geçersiz kılma `OnActivated` yöntemi:</span><span class="sxs-lookup"><span data-stu-id="aa4b1-154">toodo so, override `OnActivated` method:</span></span>
  
      protected override void OnActivated(IActivatedEventArgs args)
      {
        InitEngagement(args);
      }

> [!IMPORTANT]
> <span data-ttu-id="aa4b1-155">Biz, tooadd hello katılım başlatma, uygulamanızın başka bir yerde kesinlikle önerilmemektedir.</span><span class="sxs-lookup"><span data-stu-id="aa4b1-155">We strongly discourage you tooadd hello Engagement initialization in another place of your application.</span></span>
> 
> 

## <a name="basic-reporting"></a><span data-ttu-id="aa4b1-156">Temel raporlama</span><span class="sxs-lookup"><span data-stu-id="aa4b1-156">Basic reporting</span></span>
### <a name="recommended-method-overload-your-page-classes"></a><span data-ttu-id="aa4b1-157">Önerilen yöntem: aşırı yükleme, `Page` sınıfları</span><span class="sxs-lookup"><span data-stu-id="aa4b1-157">Recommended method: overload your `Page` classes</span></span>
<span data-ttu-id="aa4b1-158">Sipariş tooactivate hello raporunda katılım toocompute kullanıcıları, oturumlar, etkinlikleri, kilitlenme ve teknik istatistikleri gerekli tüm hello günlükler, yalnızca tüm yapabileceğiniz, `Page` alt sınıfları devral hello `EngagementPage` sınıfları.</span><span class="sxs-lookup"><span data-stu-id="aa4b1-158">In order tooactivate hello report of all hello logs required by Engagement toocompute Users, Sessions, Activities, Crashes and Technical statistics, you can simply make all your `Page` sub-classes inherit from hello `EngagementPage` classes.</span></span>

<span data-ttu-id="aa4b1-159">Örneği nasıl toodo Bu, uygulamanızın bir sayfa için.</span><span class="sxs-lookup"><span data-stu-id="aa4b1-159">Here is an example of how toodo this for a page of your application.</span></span> <span data-ttu-id="aa4b1-160">Yapabileceğiniz Merhaba, uygulamanızın tüm sayfalar için aynı anlama.</span><span class="sxs-lookup"><span data-stu-id="aa4b1-160">You can do hello same thing for all pages of your application.</span></span>

#### <a name="c-source-file"></a><span data-ttu-id="aa4b1-161">C# kaynak dosyası</span><span class="sxs-lookup"><span data-stu-id="aa4b1-161">C# Source file</span></span>
<span data-ttu-id="aa4b1-162">Sayfanızı değiştirmek `.xaml.cs` dosyası:</span><span class="sxs-lookup"><span data-stu-id="aa4b1-162">Modify your page `.xaml.cs` file:</span></span>

* <span data-ttu-id="aa4b1-163">Tooyour ekleme `using` deyimleri:</span><span class="sxs-lookup"><span data-stu-id="aa4b1-163">Add tooyour `using` statements:</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="aa4b1-164">Değiştir `Page` ile `EngagementPage`:</span><span class="sxs-lookup"><span data-stu-id="aa4b1-164">Replace `Page` with `EngagementPage`:</span></span>

<span data-ttu-id="aa4b1-165">**Katılım:**</span><span class="sxs-lookup"><span data-stu-id="aa4b1-165">**Without Engagement:**</span></span>

        namespace Example
        {
          public sealed partial class ExamplePage : Page
          {
            [...]
          }
        }

<span data-ttu-id="aa4b1-166">**Katılım ile:**</span><span class="sxs-lookup"><span data-stu-id="aa4b1-166">**With Engagement:**</span></span>

        using Microsoft.Azure.Engagement;

        namespace Example
        {
          public sealed partial class ExamplePage : EngagementPage 
          {
            [...]
          }
        }

> [!IMPORTANT]
> <span data-ttu-id="aa4b1-167">Sayfanız hello kılıyorsa `OnNavigatedTo` yöntemi, emin toocall olması `base.OnNavigatedTo(e)`.</span><span class="sxs-lookup"><span data-stu-id="aa4b1-167">If your page overrides hello `OnNavigatedTo` method, be sure toocall `base.OnNavigatedTo(e)`.</span></span> <span data-ttu-id="aa4b1-168">Aksi takdirde hello etkinlik raporlanmayacak (Merhaba `EngagementPage` çağrıları `StartActivity` içinde kendi `OnNavigatedTo` yöntemi).</span><span class="sxs-lookup"><span data-stu-id="aa4b1-168">Otherwise,  hello activity will not be reported (hello `EngagementPage` calls `StartActivity` inside its `OnNavigatedTo` method).</span></span>
> 
> 

#### <a name="xaml-file"></a><span data-ttu-id="aa4b1-169">XAML dosyası</span><span class="sxs-lookup"><span data-stu-id="aa4b1-169">XAML file</span></span>
<span data-ttu-id="aa4b1-170">Sayfanızı değiştirmek `.xaml` dosyası:</span><span class="sxs-lookup"><span data-stu-id="aa4b1-170">Modify your page `.xaml` file:</span></span>

* <span data-ttu-id="aa4b1-171">Tooyour ad alanları bildirimleri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="aa4b1-171">Add tooyour namespaces declarations:</span></span>
  
      xmlns:engagement="using:Microsoft.Azure.Engagement"
* <span data-ttu-id="aa4b1-172">Değiştir `Page` ile `engagement:EngagementPage`:</span><span class="sxs-lookup"><span data-stu-id="aa4b1-172">Replace `Page` with `engagement:EngagementPage`:</span></span>

<span data-ttu-id="aa4b1-173">**Katılım:**</span><span class="sxs-lookup"><span data-stu-id="aa4b1-173">**Without Engagement:**</span></span>

        <Page>
            <!-- layout -->
            ...
        </Page>

<span data-ttu-id="aa4b1-174">**Katılım ile:**</span><span class="sxs-lookup"><span data-stu-id="aa4b1-174">**With Engagement:**</span></span>

        <engagement:EngagementPage 
            xmlns:engagement="using:Microsoft.Azure.Engagement">
            <!-- layout -->
            ...
        </engagement:EngagementPage >

#### <a name="override-hello-default-behaviour"></a><span data-ttu-id="aa4b1-175">Merhaba varsayılan davranışı geçersiz kılma</span><span class="sxs-lookup"><span data-stu-id="aa4b1-175">Override hello default behaviour</span></span>
<span data-ttu-id="aa4b1-176">Varsayılan olarak, hiçbir ek ile Merhaba etkinlik adı olarak hello sınıf adı hello sayfasının bildirilir.</span><span class="sxs-lookup"><span data-stu-id="aa4b1-176">By default, hello class name of hello page is reported as hello activity name, with no extra.</span></span> <span data-ttu-id="aa4b1-177">Merhaba sınıfı hello "Sayfa" soneki kullanıyorsa, katılım bunu de kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="aa4b1-177">If hello class uses hello "Page" suffix, Engagement will also remove it.</span></span>

<span data-ttu-id="aa4b1-178">Merhaba adını toooverride hello varsayılan davranışa istiyorsanız, yalnızca bu tooyour kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="aa4b1-178">If you want toooverride hello default behaviour for hello name, simply add this tooyour code:</span></span>

        // in hello .xaml.cs file
        protected override string GetEngagementPageName()
        {
          /* your code */
          return "new name";
        }

<span data-ttu-id="aa4b1-179">Etkinliği ile bazı ek bilgiler tooreport istiyorsanız, bu tooyour kodu ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="aa4b1-179">If you want tooreport some extra informations with your activity, you can add this tooyour code:</span></span>

        // in hello .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
          /* your code */
          return extra;
        }

<span data-ttu-id="aa4b1-180">Bu yöntemler içinde hello denir `OnNavigatedTo` sayfanızın yöntemi.</span><span class="sxs-lookup"><span data-stu-id="aa4b1-180">These methods are called from within hello `OnNavigatedTo` method of your page.</span></span>

### <a name="alternate-method-call-startactivity-manually"></a><span data-ttu-id="aa4b1-181">Alternatif yöntem: çağrı `StartActivity()` el ile</span><span class="sxs-lookup"><span data-stu-id="aa4b1-181">Alternate method: call `StartActivity()` manually</span></span>
<span data-ttu-id="aa4b1-182">Olamaz ya da toooverload istiyor musunuz, `Page` sınıfları, bunun yerine, çağırarak etkinliklerinizi başlatabilirsiniz `EngagementAgent` doğrudan yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="aa4b1-182">If you cannot or do not want toooverload your `Page` classes, you can instead start your activities by calling `EngagementAgent` methods directly.</span></span>

<span data-ttu-id="aa4b1-183">Toocall öneririz `StartActivity` içinde `OnNavigatedTo` sayfanızın yöntemi.</span><span class="sxs-lookup"><span data-stu-id="aa4b1-183">We recommend toocall `StartActivity` inside your `OnNavigatedTo` method of your Page.</span></span>

            protected override void OnNavigatedTo(NavigationEventArgs e)
            {
              base.OnNavigatedTo(e);
              EngagementAgent.Instance.StartActivity("MyPage");
            }

> [!IMPORTANT]
> <span data-ttu-id="aa4b1-184">Doğru oturumunuzu sonlandırmak emin olun.</span><span class="sxs-lookup"><span data-stu-id="aa4b1-184">Ensure you end your session correctly.</span></span>
> 
> <span data-ttu-id="aa4b1-185">Merhaba Windows Evrensel SDK otomatik olarak çağırır hello `EndActivity` hello uygulama kapatıldığında yöntemi.</span><span class="sxs-lookup"><span data-stu-id="aa4b1-185">hello Windows Universal SDK automatically calls hello `EndActivity` method when hello application is closed.</span></span> <span data-ttu-id="aa4b1-186">Bu nedenle, olan **yüksek oranda** toocall hello önerilen `StartActivity` hello kullanıcının hello etkinliği değiştirdiğinizde, yöntemi ve çok**hiçbir zaman** çağrısı hello `EndActivity` yöntemi, bu yöntem, tooEngagement gönderir Sunucu geçerli kullanıcının bırakın hello uygulama olduğundan, bu işlem tüm uygulama günlüklerini etkiler.</span><span class="sxs-lookup"><span data-stu-id="aa4b1-186">Thus, it is **HIGHLY** recommended toocall hello `StartActivity` method whenever hello activity of hello user change, and too**NEVER** call hello `EndActivity` method, this method sends tooEngagement server that current user has leave hello application, this will impacts all application logs.</span></span>
> 
> 

## <a name="advanced-reporting"></a><span data-ttu-id="aa4b1-187">Gelişmiş raporlama</span><span class="sxs-lookup"><span data-stu-id="aa4b1-187">Advanced reporting</span></span>
<span data-ttu-id="aa4b1-188">İsteğe bağlı olarak, böylece tooreport uygulama belirli olayları, hataları ve işleri, toodo isteyebilirsiniz, kullanım hello diğer yöntemleri bulunanlar hello `EngagementAgent` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="aa4b1-188">Optionally, you may want tooreport application specific events, errors and jobs, toodo so, use hello others methods found in hello `EngagementAgent` class.</span></span> <span data-ttu-id="aa4b1-189">Merhaba katılım API toouse tüm Engagement'ın gelişmiş özelliklerinden sağlar.</span><span class="sxs-lookup"><span data-stu-id="aa4b1-189">hello Engagement API allows toouse all of Engagement's advanced capabilities.</span></span>

<span data-ttu-id="aa4b1-190">Daha fazla bilgi için bkz: [nasıl toouse hello Mobile Engagement Windows Evrensel uygulamanız API etiketleme Gelişmiş](mobile-engagement-windows-store-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="aa4b1-190">For further information, see [How toouse hello advanced Mobile Engagement tagging API in your Windows Universal app](mobile-engagement-windows-store-use-engagement-api.md).</span></span>

## <a name="advanced-configuration"></a><span data-ttu-id="aa4b1-191">Gelişmiş yapılandırma</span><span class="sxs-lookup"><span data-stu-id="aa4b1-191">Advanced configuration</span></span>
### <a name="disable-automatic-crash-reporting"></a><span data-ttu-id="aa4b1-192">Otomatik Kilitlenme bildirimini devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="aa4b1-192">Disable automatic crash reporting</span></span>
<span data-ttu-id="aa4b1-193">Merhaba otomatik kilitlenme raporlama katılım özelliği devre dışı bırakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aa4b1-193">You can disable hello automatic crash reporting feature of Engagement.</span></span> <span data-ttu-id="aa4b1-194">Ardından, işlenmeyen bir özel durum meydana gelir, katılım hiçbir şey olmaz.</span><span class="sxs-lookup"><span data-stu-id="aa4b1-194">Then, when an unhandled exception will occur, Engagement won't do anything.</span></span>

> [!WARNING]
> <span data-ttu-id="aa4b1-195">Bu özellik toodisable planlıyorsanız, uygulamanızda işlenmeyen bir kilitlenme meydana gelir, katılım hello kilitlenme göndermez unutmayın **ve** hello oturum ve işleri kapanmaz.</span><span class="sxs-lookup"><span data-stu-id="aa4b1-195">If you plan toodisable this feature, be aware that when a unhandled crash will occur in your app, Engagement will not send hello crash **AND** will not close hello session and jobs.</span></span>
> 
> 

<span data-ttu-id="aa4b1-196">Raporlama toodisable otomatik kilitlenme yalnızca yapılandırmanıza bağlı olarak, bildirilen hello şekilde özelleştirin:</span><span class="sxs-lookup"><span data-stu-id="aa4b1-196">toodisable automatic crash reporting, just customize your configuration depending on hello way you declared it:</span></span>

#### <a name="from-engagementconfigurationxml-file"></a><span data-ttu-id="aa4b1-197">Gelen `EngagementConfiguration.xml` dosyası</span><span class="sxs-lookup"><span data-stu-id="aa4b1-197">From `EngagementConfiguration.xml` file</span></span>
<span data-ttu-id="aa4b1-198">Raporu çökme çok Ayarla`false` arasında `<reportCrash>` ve `</reportCrash>` etiketler.</span><span class="sxs-lookup"><span data-stu-id="aa4b1-198">Set report crash too`false` between `<reportCrash>` and `</reportCrash>` tags.</span></span>

#### <a name="from-engagementconfiguration-object-at-run-time"></a><span data-ttu-id="aa4b1-199">Gelen `EngagementConfiguration` çalışma zamanında nesne</span><span class="sxs-lookup"><span data-stu-id="aa4b1-199">From `EngagementConfiguration` object at run time</span></span>
<span data-ttu-id="aa4b1-200">EngagementConfiguration nesnesini kullanarak rapor kilitlenme toofalse ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="aa4b1-200">Set report crash toofalse using your EngagementConfiguration object.</span></span>

        /* Engagement configuration. */
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Disable Engagement crash reporting. */
        engagementConfiguration.Agent.ReportCrash = false;

### <a name="burst-mode"></a><span data-ttu-id="aa4b1-201">Veri bloğu modu</span><span class="sxs-lookup"><span data-stu-id="aa4b1-201">Burst mode</span></span>
<span data-ttu-id="aa4b1-202">Varsayılan olarak, hello katılım hizmet raporları gerçek zamanlı olarak günlüğe kaydeder.</span><span class="sxs-lookup"><span data-stu-id="aa4b1-202">By default, hello Engagement service reports logs in real time.</span></span> <span data-ttu-id="aa4b1-203">Uygulamanızı günlükleri çok sık raporları, daha iyi toobuffer hello günlükleri ve tooreport varsa, bunları (Merhaba "veri bloğu modu" denir) tümünü bir defada bir normal zaman temel üzerinde.</span><span class="sxs-lookup"><span data-stu-id="aa4b1-203">If your application reports logs very frequently, it is better toobuffer hello logs and tooreport them all at once on a regular time base (this is called hello “burst mode”).</span></span>

<span data-ttu-id="aa4b1-204">toodo, bu nedenle, hello yöntemi çağırın:</span><span class="sxs-lookup"><span data-stu-id="aa4b1-204">toodo so, call hello method:</span></span>

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

<span data-ttu-id="aa4b1-205">Merhaba bağımsız değişkeni olarak bir değerdir **milisaniye**.</span><span class="sxs-lookup"><span data-stu-id="aa4b1-205">hello argument is a value in **milliseconds**.</span></span> <span data-ttu-id="aa4b1-206">Tooreactivate hello gerçek zamanlı günlük tutma istiyorsanız, herhangi bir zamanda hello yöntemini hello 0 değerine sahip veya herhangi bir parametre olmadan yalnızca çağırın.</span><span class="sxs-lookup"><span data-stu-id="aa4b1-206">At any time, if you want tooreactivate hello real-time logging, just call hello method without any parameter, or with hello 0 value.</span></span>

<span data-ttu-id="aa4b1-207">Merhaba veri bloğu modu biraz artırmak hello pil ömrü ancak Engagement İzleyicisi Merhaba üzerinde bir etkisi vardır: tüm oturumları ve işleri süresi yuvarlak toohello veri bloğu eşiği (Bu nedenle, oturumlar ve işleri hello veri bloğu eşik görünmeyebilir daha kısa) olacaktır.</span><span class="sxs-lookup"><span data-stu-id="aa4b1-207">hello burst mode slightly increase hello battery life but has an impact on hello Engagement Monitor: all sessions and jobs duration will be rounded toohello burst threshold (thus, sessions and jobs shorter than hello burst threshold may not be visible).</span></span> <span data-ttu-id="aa4b1-208">Bu bir veri bloğu eşikten artık 30000 (30s) toouse önerilir.</span><span class="sxs-lookup"><span data-stu-id="aa4b1-208">It is recommended toouse a burst threshold no longer than 30000 (30s).</span></span> <span data-ttu-id="aa4b1-209">Toobe Günlükleri kaydedilen sınırlı too300 öğeleridir farkında olması.</span><span class="sxs-lookup"><span data-stu-id="aa4b1-209">You have toobe aware that saved logs are limited too300 items.</span></span> <span data-ttu-id="aa4b1-210">Gönderme çok uzunsa, bazı günlükleri kaybedebilir.</span><span class="sxs-lookup"><span data-stu-id="aa4b1-210">If sending is too long you can lose some logs.</span></span>

> [!WARNING]
> <span data-ttu-id="aa4b1-211">Merhaba veri bloğu eşik tooa dönemi 1'ler küçüktür yapılandırılamaz.</span><span class="sxs-lookup"><span data-stu-id="aa4b1-211">hello burst threshold cannot be configured tooa period lesser than 1s.</span></span> <span data-ttu-id="aa4b1-212">Toodo şekilde çalışırsanız, SDK izleme hello hatasıyla göstermek ve otomatik olarak hello toohello varsayılan değer, yani, 0s sıfırlayın.</span><span class="sxs-lookup"><span data-stu-id="aa4b1-212">If you try toodo so, hello SDK will show a trace with hello error and will automatically reset toohello default value, i.e., 0s.</span></span> <span data-ttu-id="aa4b1-213">Bu hello SDK tooreport hello günlükler gerçek zamanlı tetikler.</span><span class="sxs-lookup"><span data-stu-id="aa4b1-213">This will trigger hello SDK tooreport hello logs in real-time.</span></span>
> 
> 

[here]:http://www.nuget.org/packages/Capptain.WindowsCS
[NuGet website]:http://docs.nuget.org/docs/start-here/overview

