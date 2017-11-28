---
title: "aaaWindows Evrensel uygulamalar Reach SDK tümleştirmesi"
description: "Nasıl tooIntegrate Azure Mobile Engagement Reach ile Windows Evrensel uygulamaları"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a31ca1d6-856f-4aec-898a-07969ae5f7ec
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: af311c65940014083333853875a00173b8d6783e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-universal-apps-reach-sdk-integration"></a><span data-ttu-id="1bf4f-103">Windows Evrensel uygulamaları Reach SDK tümleştirmesi</span><span class="sxs-lookup"><span data-stu-id="1bf4f-103">Windows Universal Apps Reach SDK Integration</span></span>
<span data-ttu-id="1bf4f-104">Merhaba tümleştirme hello yordamını izleyin [Windows Evrensel Engagement SDK tümleştirmesi](mobile-engagement-windows-store-integrate-engagement.md) bu kılavuz aşağıdaki önce.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-104">You must follow hello integration procedure described in hello [Windows Universal Engagement SDK Integration](mobile-engagement-windows-store-integrate-engagement.md) before following this guide.</span></span>

## <a name="embed-hello-engagement-reach-sdk-into-your-windows-universal-project"></a><span data-ttu-id="1bf4f-105">Windows Evrensel projenize Hello Engagement Reach SDK'sı ekleme</span><span class="sxs-lookup"><span data-stu-id="1bf4f-105">Embed hello Engagement Reach SDK into your Windows Universal project</span></span>
<span data-ttu-id="1bf4f-106">Herhangi bir şey yok tooadd.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-106">You do not have anything tooadd.</span></span> <span data-ttu-id="1bf4f-107">`EngagementReach`Projenizde başvuruları ve kaynak zaten var.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-107">`EngagementReach` references and resources are already in your project.</span></span>

> [!TIP]
> <span data-ttu-id="1bf4f-108">Hello bulunan görüntüleri özelleştirebilirsiniz `Resources` klasörü projenizin, özellikle hello marka simgesini (Bu varsayılan toohello katılım simge).</span><span class="sxs-lookup"><span data-stu-id="1bf4f-108">You can customize images located in hello `Resources` folder of your project, especially hello brand icon (that default toohello Engagement icon).</span></span> <span data-ttu-id="1bf4f-109">Evrensel uygulamaları hello de taşıyabilirsiniz `Resources` içeriği uygulamalar, ancak arasında olacaktır, paylaşılan bir proje tooshare klasöründe tookeep hello `Resources\EngagementConfiguration.xml` platform bağımlı olduğu gibi varsayılan konumuna dosya.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-109">On Universal Apps you can also move hello `Resources` folder on your shared project tooshare its content between apps, but you will have tookeep hello `Resources\EngagementConfiguration.xml` file on its default location as it is platform dependent.</span></span>
> 
> 

## <a name="enable-hello-windows-notification-service"></a><span data-ttu-id="1bf4f-110">Merhaba Windows bildirim Hizmeti'ni etkinleştir</span><span class="sxs-lookup"><span data-stu-id="1bf4f-110">Enable hello Windows Notification Service</span></span>
### <a name="windows-8x-and-windows-phone-81-only"></a><span data-ttu-id="1bf4f-111">Windows 8.x ve Windows Phone 8.1 yalnızca</span><span class="sxs-lookup"><span data-stu-id="1bf4f-111">Windows 8.x and Windows Phone 8.1 only</span></span>
<span data-ttu-id="1bf4f-112">Sipariş toouse hello içinde **Windows bildirim hizmeti** (WNS adlandırılır) içinde `Package.appxmanifest` üzerinde dosya `Application UI` tıklayın `All Image Assets` hello sol bot kutusunda.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-112">In order toouse hello **Windows Notification Service** (referred as WNS) in your `Package.appxmanifest` file on `Application UI` click on `All Image Assets` in hello left bot box.</span></span> <span data-ttu-id="1bf4f-113">Merhaba kutusunun sağında hello adresindeki `Notifications`, değiştirme `toast capable` gelen `(not set)` çok`(Yes)`.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-113">At hello right of hello box in `Notifications`, change `toast capable` from `(not set)` too`(Yes)`.</span></span>

### <a name="all-platforms"></a><span data-ttu-id="1bf4f-114">Tüm platformlar</span><span class="sxs-lookup"><span data-stu-id="1bf4f-114">All platforms</span></span>
<span data-ttu-id="1bf4f-115">Uygulama tooyour Microsoft hesabı ve toohello katılım platformunuz toosynchronize gerekir.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-115">You need toosynchronize your app tooyour Microsoft account and toohello engagement platform.</span></span> <span data-ttu-id="1bf4f-116">Bu toocreate bir hesap gerekir veya oturum açma [windows Geliştirme Merkezi](https://dev.windows.com).</span><span class="sxs-lookup"><span data-stu-id="1bf4f-116">For this you need toocreate an account or log on [windows dev center](https://dev.windows.com).</span></span> <span data-ttu-id="1bf4f-117">Sonra yeni bir uygulama oluşturun ve Bul SID'sini ve gizli anahtarını hello.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-117">After that create a new application and find hello SID and secret key.</span></span> <span data-ttu-id="1bf4f-118">Uygulama ayarınız Hello katılım ön uçta gidin `native push` ve kimlik bilgilerinizi yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-118">On hello engagement frontend, go on your app setting in `native push` and paste your credentials.</span></span> <span data-ttu-id="1bf4f-119">Bundan sonra projenize sağ üzerinde select tıklayın `store` ve `Associate App with hello Store...`.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-119">After that, right click on your project, select `store` and `Associate App with hello Store...`.</span></span> <span data-ttu-id="1bf4f-120">Tooselect Merhaba uygulaması yeterlidir, oluşturduğunuz toosynchronize önce onu.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-120">You just need tooselect hello application you have create before toosynchronize it.</span></span>

## <a name="initialize-hello-engagement-reach-sdk"></a><span data-ttu-id="1bf4f-121">Merhaba Engagement Reach SDK'sını başlatma</span><span class="sxs-lookup"><span data-stu-id="1bf4f-121">Initialize hello Engagement Reach SDK</span></span>
<span data-ttu-id="1bf4f-122">Merhaba değiştirme `App.xaml.cs`:</span><span class="sxs-lookup"><span data-stu-id="1bf4f-122">Modify hello `App.xaml.cs`:</span></span>

* <span data-ttu-id="1bf4f-123">INSERT `EngagementReach.Instance.Init` hemen sonra `EngagementAgent.Instance.Init` içinde `InitEngagement` yöntemi:</span><span class="sxs-lookup"><span data-stu-id="1bf4f-123">Insert `EngagementReach.Instance.Init` just after `EngagementAgent.Instance.Init` in your `InitEngagement` method:</span></span>
  
      private void InitEngagement(IActivatedEventArgs e)
      {
        EngagementAgent.Instance.Init(e);
        EngagementReach.Instance.Init(e);
      }
  
  <span data-ttu-id="1bf4f-124">Merhaba `EngagementReach.Instance.Init` adanmış bir iş parçacığı çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-124">hello `EngagementReach.Instance.Init` runs in a dedicated thread.</span></span> <span data-ttu-id="1bf4f-125">Toodo sahip değil, kendiniz.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-125">You do not have toodo it yourself.</span></span>

> [!NOTE]
> <span data-ttu-id="1bf4f-126">Anında iletme bildirimleri, uygulamanızda başka bir yerde kullanıyorsanız sonra çok sahip[itme kanalını paylaşan](#push-channel-sharing) Engagement Reach ile.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-126">If you are using push notifications elsewhere in your application then you have too[share your push channel](#push-channel-sharing) with Engagement Reach.</span></span>
> 
> 

## <a name="integration"></a><span data-ttu-id="1bf4f-127">Tümleştirme</span><span class="sxs-lookup"><span data-stu-id="1bf4f-127">Integration</span></span>
<span data-ttu-id="1bf4f-128">Duyuruları ve yoklamaları uygulamanızda katılım sağlayan iki yolla tooadd hello ulaşma uygulama başlıkları ve Interstitial görünümleri: hello kaplama tümleştirme ve hello web görünümleri el ile tümleştirme.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-128">Engagement provides two ways tooadd hello Reach in-app banners and interstitial views for announcements and polls in your application: hello overlay integration and hello web views manual integration.</span></span> <span data-ttu-id="1bf4f-129">Her iki yaklaşım hello üzerinde birleştirmelisiniz değil aynı sayfa.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-129">You should not combine both approach on hello same page.</span></span>

<span data-ttu-id="1bf4f-130">Bu şekilde hello iki tümleştirme arasında seçim Hello özetlenen:</span><span class="sxs-lookup"><span data-stu-id="1bf4f-130">hello choice between hello two integration could be summarized this way:</span></span>

* <span data-ttu-id="1bf4f-131">Sayfalarınızın zaten devralıyorsa hello Aracısı ' hello yer paylaşımlı tümleştirme seçebilirsiniz `EngagementPage`, onu değiştirme yalnızca bir konudur `EngagementPage` tarafından `EngagementPageOverlay` ve `xmlns:engagement="using:Microsoft.Azure.Engagement"` tarafından `xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"` sayfalarınızı içinde.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-131">You may choose hello overlay integration if your pages already inherits from hello Agent `EngagementPage`, it's just a matter of replacing `EngagementPage` by `EngagementPageOverlay` and `xmlns:engagement="using:Microsoft.Azure.Engagement"` by `xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"` in your pages.</span></span>
* <span data-ttu-id="1bf4f-132">Başka bir devralma düzeyi tooyour sayfaları içindeki sayfalarınızı tooprecisely yer hello UI erişmek isterseniz veya tooadd istemiyorsanız hello web görünümleri el ile tümleştirme'yı seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-132">You may choose hello web views manual integration if you want tooprecisely place hello Reach UI within your pages or if you don't want tooadd another inheritance level tooyour pages.</span></span> 

### <a name="overlay-integration"></a><span data-ttu-id="1bf4f-133">Yer paylaşımlı tümleştirme</span><span class="sxs-lookup"><span data-stu-id="1bf4f-133">Overlay integration</span></span>
<span data-ttu-id="1bf4f-134">Merhaba katılım katmana hello kullanıcı Arabirimi öğeleri toodisplay Reach kampanyaları sayfanızda kullanılan dinamik olarak ekler.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-134">hello Engagement overlay dynamically adds hello UI elements used toodisplay Reach campaigns in your page.</span></span> <span data-ttu-id="1bf4f-135">Merhaba katmana düzeninize uyacak değil, el ile tümleştirme hello web görünümleri yerine dikkate almalısınız.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-135">If hello overlay doesn't suit your layout you should consider hello web views manual integration instead.</span></span>

<span data-ttu-id="1bf4f-136">.Xaml dosya değişikliği `EngagementPage` çok başvurusu`EngagementPageOverlay`</span><span class="sxs-lookup"><span data-stu-id="1bf4f-136">In your .xaml file change `EngagementPage` reference too`EngagementPageOverlay`</span></span>

* <span data-ttu-id="1bf4f-137">Tooyour ad alanları bildirimleri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="1bf4f-137">Add tooyour namespaces declarations:</span></span>
  
      xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"
* <span data-ttu-id="1bf4f-138">Değiştir `engagement:EngagementPage` ile `engagement:EngagementPageOverlay`:</span><span class="sxs-lookup"><span data-stu-id="1bf4f-138">Replace `engagement:EngagementPage` with `engagement:EngagementPageOverlay`:</span></span>

<span data-ttu-id="1bf4f-139">**EngagementPage ile:**</span><span class="sxs-lookup"><span data-stu-id="1bf4f-139">**With EngagementPage:**</span></span>

        <engagement:EngagementPage 
            xmlns:engagement="using:Microsoft.Azure.Engagement">

            <!-- Your layout -->
        </engagement:EngagementPage>

<span data-ttu-id="1bf4f-140">**EngagementPageOverlay ile:**</span><span class="sxs-lookup"><span data-stu-id="1bf4f-140">**With EngagementPageOverlay:**</span></span>

        <engagement:EngagementPageOverlay 
            xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay">

            <!-- Your layout -->
        </engagement:EngagementPageOverlay>

<span data-ttu-id="1bf4f-141">Ardından .cs dosyanızda sayfanızda etiketi `EngagementPageOverlay` yerine `EngagementPage` ve içeri aktarma `Microsoft.Azure.Engagement.Overlay`.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-141">Then in your .cs file tag your page in `EngagementPageOverlay` instead of `EngagementPage` and import `Microsoft.Azure.Engagement.Overlay`.</span></span>

            using Microsoft.Azure.Engagement.Overlay;

* <span data-ttu-id="1bf4f-142">Değiştir `EngagementPage` ile `EngagementPageOverlay`:</span><span class="sxs-lookup"><span data-stu-id="1bf4f-142">Replace `EngagementPage` with `EngagementPageOverlay`:</span></span>

<span data-ttu-id="1bf4f-143">**EngagementPage ile:**</span><span class="sxs-lookup"><span data-stu-id="1bf4f-143">**With EngagementPage:**</span></span>

            using Microsoft.Azure.Engagement;

            namespace Example
            {
              public sealed partial class ExamplePage : EngagementPage
              {
                [...]
              }
            }

<span data-ttu-id="1bf4f-144">**EngagementPageOverlay ile:**</span><span class="sxs-lookup"><span data-stu-id="1bf4f-144">**With EngagementPageOverlay:**</span></span>

            using Microsoft.Azure.Engagement.Overlay;

            namespace Example
            {
              public sealed partial class ExamplePage : EngagementPageOverlay 
              {
                [...]
              }
            }


<span data-ttu-id="1bf4f-145">Merhaba katılım katmana ekler bir `Grid` öğesi, sayfanın en üstünde oluşur, Düzen ve hello iki `WebView` hello için öğeleri bir kapak sayfası ve hello Interstitial görünüm için başka bir hello.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-145">hello Engagement overlay adds a `Grid` element on top of your page composed of your layout and hello two `WebView` elements one for hello banner and hello other one for hello interstitial view.</span></span>

<span data-ttu-id="1bf4f-146">Merhaba katmana öğelerinde doğrudan hello özelleştirebilirsiniz `EngagementPageOverlay.cs` dosya.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-146">You can customize hello overlay elements directly in hello `EngagementPageOverlay.cs` file.</span></span>

### <a name="web-views-manual-integration"></a><span data-ttu-id="1bf4f-147">Web görünümleri el ile tümleştirme</span><span class="sxs-lookup"><span data-stu-id="1bf4f-147">Web views manual integration</span></span>
<span data-ttu-id="1bf4f-148">Reach sayfalarınızın hello iki arama `WebView` öğeleri hello başlık ve hello Interstitial görünümü görüntülemek için sorumlu.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-148">Reach will be searching your pages for hello two `WebView` elements responsible for displaying hello banner and hello interstitial view.</span></span> <span data-ttu-id="1bf4f-149">yalnızca bir şey toodo sahip tooadd hello bu iki `WebView` öğeleri yere sayfalarınızda, örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="1bf4f-149">hello only thing you have toodo is tooadd those two `WebView` elements somewhere in your pages, here is an example:</span></span>

    <Grid x:Name="engagementGrid">

      <!-- Your layout -->

      <WebView x:Name="engagement_notification_content" Visibility="Collapsed" Height="80" HorizontalAlignment="Stretch" VerticalAlignment="Top"/>
      <WebView x:Name="engagement_announcement_content" Visibility="Collapsed"  HorizontalAlignment="Stretch"  VerticalAlignment="Stretch"/>
    </Grid>


<span data-ttu-id="1bf4f-150">Bu örnek hello içinde `WebView` öğeler otomatik olarak onları ekran döndürme veya pencere boyutu değişikliği durumunda yeniden boyutlandırır kendi kapsayıcı esnetilen toofit olan.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-150">In this example hello `WebView` elements are stretched toofit their container which automatically re-sizes them in case of screen rotation or window size change.</span></span>

> [!WARNING]
> <span data-ttu-id="1bf4f-151">Tookeep hello aynı adlandırma önemlidir `engagement_notification_content` ve `engagement_announcement_content` hello için `WebView` öğeleri.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-151">It is important tookeep hello same naming `engagement_notification_content` and `engagement_announcement_content` for hello `WebView` elements.</span></span> <span data-ttu-id="1bf4f-152">Reach bunları adına göre tanımlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-152">Reach is identifying them by their name.</span></span> 
> 
> 

## <a name="handle-datapush-optional"></a><span data-ttu-id="1bf4f-153">Tanıtıcı datapush (isteğe bağlı)</span><span class="sxs-lookup"><span data-stu-id="1bf4f-153">Handle datapush (optional)</span></span>
<span data-ttu-id="1bf4f-154">Uygulama toobe mümkün tooreceive ulaşma veri gönderimleri isterseniz, iki olayları hello EngagementReach sınıfı tooimplement vardır:</span><span class="sxs-lookup"><span data-stu-id="1bf4f-154">If you want your application toobe able tooreceive Reach data pushes, you have tooimplement two events of hello EngagementReach class:</span></span>

<span data-ttu-id="1bf4f-155">App.xaml.cs hello App() oluşturucuda ekleyin:</span><span class="sxs-lookup"><span data-stu-id="1bf4f-155">In App.xaml.cs in hello App() constructor add:</span></span>

            EngagementReach.Instance.DataPushStringReceived += (body) =>
            {
              Debug.WriteLine("String data push message received: " + body);
              return true;
            };

            EngagementReach.Instance.DataPushBase64Received += (decodedBody, encodedBody) =>
            {
              Debug.WriteLine("Base64 data push message received: " + encodedBody);
              // Do something useful with decodedBody like updating an image view
              return true;
            };

<span data-ttu-id="1bf4f-156">Her yöntem döndürür bir Boole değeri, bu hello geri çağırma görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-156">You can see that hello callback of each method returns a boolean.</span></span> <span data-ttu-id="1bf4f-157">Katılım hello veri gönderimi gönderdikten sonra bir geri bildirim tooits arka uç gönderir.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-157">Engagement sends a feedback tooits back-end after dispatching hello data push.</span></span> <span data-ttu-id="1bf4f-158">Merhaba geri çağırma false değeri döndürülürse, hello `exit` geri bildirim gönder olacaktır.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-158">If hello callback returns false, hello `exit` feedback will be send.</span></span> <span data-ttu-id="1bf4f-159">Aksi durumda olur `action`.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-159">Otherwise, it will be `action`.</span></span> <span data-ttu-id="1bf4f-160">Geri arama yok hello olaylarını ayarlarsanız hello `drop` geri bildirim tooEngagement döndürülecek.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-160">If no callback is set for hello events, hello `drop` feedback will be returned tooEngagement.</span></span>

> [!WARNING]
> <span data-ttu-id="1bf4f-161">Katılım mümkün tooreceive katları geribildirimler veri gönderimi için değil.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-161">Engagement is not able tooreceive multiples feedbacks for a data push.</span></span> <span data-ttu-id="1bf4f-162">Bir olayda birçok işleyicileri tooset planlıyorsanız, hello geri bildirim sonuncu gönderilen toohello karşılık unutmayın.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-162">If you plan tooset several handlers on an event, be aware that hello feedback will correspond toohello last one sent.</span></span> <span data-ttu-id="1bf4f-163">Bu durumda, tooalways öneririz hello kafa karıştırıcı geri bildirim hello ön uç sahip aynı değeri tooavoid döndürür.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-163">In this case, we recommend tooalways returns hello same value tooavoid having confusing feedback on hello front-end.</span></span>
> 
> 

## <a name="customize-ui-optional"></a><span data-ttu-id="1bf4f-164">(İsteğe bağlı) kullanıcı arabirimini özelleştirme</span><span class="sxs-lookup"><span data-stu-id="1bf4f-164">Customize UI (optional)</span></span>
### <a name="first-step"></a><span data-ttu-id="1bf4f-165">İlk adım</span><span class="sxs-lookup"><span data-stu-id="1bf4f-165">First step</span></span>
<span data-ttu-id="1bf4f-166">Biz toocustomize hello ulaşma kullanıcı Arabirimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-166">We allow you toocustomize hello reach UI.</span></span>

<span data-ttu-id="1bf4f-167">toodo bu nedenle, toocreate hello öğesinin bir alt kümesi olan `EngagementReachHandler` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-167">toodo so, you have toocreate a subclass of hello `EngagementReachHandler` class.</span></span>

<span data-ttu-id="1bf4f-168">**Örnek kod:**</span><span class="sxs-lookup"><span data-stu-id="1bf4f-168">**Sample Code :**</span></span>

            using Microsoft.Azure.Engagement;

            namespace Example
            {
              internal class ExampleReachHandler : EngagementReachHandler
              {
               // Override EngagementReachHandler methods depending on your needs
              }
            }

<span data-ttu-id="1bf4f-169">Sonra hello Merhaba içeriğine ayarlayın `EngagementReach.Instance.Handler` özel nesnesinde ile alan, `App.xaml.cs` hello sınıfında `App()` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-169">Then, set hello content of hello `EngagementReach.Instance.Handler` field with your custom object in your `App.xaml.cs` class within hello `App()` method.</span></span>

<span data-ttu-id="1bf4f-170">**Örnek kod:**</span><span class="sxs-lookup"><span data-stu-id="1bf4f-170">**Sample Code :**</span></span>

            protected override void OnLaunched(LaunchActivatedEventArgs args)
            {
              // your app initialization 
              EngagementReach.Instance.Handler = new ExampleReachHandler();
              // Engagement Agent and Reach initialization
            }

> [!NOTE]
> <span data-ttu-id="1bf4f-171">Varsayılan olarak, kendi uyarlamasını katılım kullanır `EngagementReachHandler`.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-171">By default, Engagement uses its own implementation of `EngagementReachHandler`.</span></span>
> <span data-ttu-id="1bf4f-172">Toocreate yoksa, kendi ve bunu yaparsanız, her yöntemi toooverride yok.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-172">You don't have toocreate your own, and if you do so, you don't have toooverride every method.</span></span> <span data-ttu-id="1bf4f-173">tooselect hello katılım temel nesne Hello varsayılan davranıştır.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-173">hello default behavior is tooselect hello Engagement base object.</span></span>
> 
> 

### <a name="web-view"></a><span data-ttu-id="1bf4f-174">Web görünümü</span><span class="sxs-lookup"><span data-stu-id="1bf4f-174">Web View</span></span>
<span data-ttu-id="1bf4f-175">Varsayılan olarak, ulaşma hello DLL toodisplay hello bildirimleri ve sayfalarının katıştırılmış hello kaynakları kullanır.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-175">By default, Reach will use hello embedded resources of hello DLL toodisplay hello notifications and pages.</span></span>

<span data-ttu-id="1bf4f-176">tooprovide tam özelleştirme olanakları yalnızca kullanırız web görünümü.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-176">tooprovide a full customization possibilities we only use web view.</span></span> <span data-ttu-id="1bf4f-177">Doğrudan toocustomize düzenleri istiyorsanız hello kaynaklar dosyaları geçersiz kılma `EngagementAnnouncement.html` ve `EngagementNotification.html`.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-177">If you want toocustomize layouts, override directly hello resources files `EngagementAnnouncement.html` and `EngagementNotification.html`.</span></span> <span data-ttu-id="1bf4f-178">Katılım gereken tüm kodda `<body></body>` toorun doğru.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-178">Engagement needs all code in `<body></body>` toorun correctly.</span></span> <span data-ttu-id="1bf4f-179">Ancak, dış etiket ekleyebilirsiniz `engagement_webview_area`.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-179">But you can add tag outer `engagement_webview_area`.</span></span>

<span data-ttu-id="1bf4f-180">Ancak, kendi kaynaklarını toouse karar verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-180">However, you can decide toouse your own resources.</span></span>

<span data-ttu-id="1bf4f-181">Geçersiz kılabilirsiniz `EngagementReachHandler` alt tootell katılım toouse yöntemleri, düzenler ancak dikkatli tooembedded hello katılım mekanizması alın:</span><span class="sxs-lookup"><span data-stu-id="1bf4f-181">You can override `EngagementReachHandler` methods in your subclass tootell Engagement toouse your layouts, but take care tooembedded hello engagement mechanism:</span></span>

<span data-ttu-id="1bf4f-182">**Örnek kod:**</span><span class="sxs-lookup"><span data-stu-id="1bf4f-182">**Sample Code :**</span></span>

            // In your subclass of EngagementReachHandler

            public override string GetAnnouncementHTML()
            {
              return base.GetAnnouncementHTML();
            }
            public override string GetAnnouncementName()
            {
              return base.GetAnnouncementName();
            }
            public override string GetNotfificationHTML()
            {
              return base.GetNotfificationHTML();
            }
            public override string GetNotfificationName()
            {
              return base.GetNotfificationName();
            }


<span data-ttu-id="1bf4f-183">Varsayılan olarak, AnnouncementHTML olan `ms-appx-web:///Resources/EngagementAnnouncement.html`.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-183">By default, AnnouncementHTML is `ms-appx-web:///Resources/EngagementAnnouncement.html`.</span></span> <span data-ttu-id="1bf4f-184">Anında iletme iletisi (metin Duyurusu, Web anoucement ve yoklama duyuru) Merhaba içeriğine tasarım hello html dosyası temsil eder.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-184">It represents hello html file that design hello content of a push message (Text announcement, Web anoucement and Poll announcement).</span></span> <span data-ttu-id="1bf4f-185">AnnouncementName olan `engagement_announcement_content`.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-185">AnnouncementName is `engagement_announcement_content`.</span></span> <span data-ttu-id="1bf4f-186">Bunu hello hello webview xaml sayfası tasarımında adıdır.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-186">It is hello name of hello webview design in your xaml page.</span></span>

<span data-ttu-id="1bf4f-187">NotfificationHTML olan `ms-appx-web:///Resources/EngagementNotification.html`.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-187">NotfificationHTML is `ms-appx-web:///Resources/EngagementNotification.html`.</span></span> <span data-ttu-id="1bf4f-188">Anında iletme iletisi hello bildirim tasarım hello html dosyası temsil eder.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-188">It represents hello html file that design hello notification of a push message.</span></span> <span data-ttu-id="1bf4f-189">NotfificationName olan `engagement_notification_content`.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-189">NotfificationName is `engagement_notification_content`.</span></span> <span data-ttu-id="1bf4f-190">Bunu hello hello webview xaml sayfası tasarımında adıdır.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-190">It is hello name of hello webview design in your xaml page.</span></span>

### <a name="customization"></a><span data-ttu-id="1bf4f-191">Özelleştirme</span><span class="sxs-lookup"><span data-stu-id="1bf4f-191">Customization</span></span>
<span data-ttu-id="1bf4f-192">Bildirim ve web görünümü, katılım nesne korumak istiyorsanız sahip duyuru özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-192">You can customize notification and announcement web view has you want if you preserve Engagement object.</span></span> <span data-ttu-id="1bf4f-193">Dikkatli olun webview nesnesi üç kez açıklanan - Merhaba, xaml ilk kez ikinci hello "setwebview()" yönteminde .cs dosyanızdaki ve saat üçüncü hello html dosyasında zaman.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-193">Take care that webview object is described three times - hello first time in your xaml, second time in your .cs file in hello "setwebview()" method, and third time in hello html file.</span></span>

* <span data-ttu-id="1bf4f-194">Xaml içinde hello geçerli grafik düzenini webview bileşeni açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-194">In your xaml you describe hello current graphical layout webview component.</span></span>
* <span data-ttu-id="1bf4f-195">.Cs dosyanızda "Merhaba iki webview (bildirim, duyuru) hello boyutunu Ayarla setwebview()" tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-195">In your .cs file you can define "setwebview()" in which you set hello dimension of hello two webview (notification, announcement).</span></span> <span data-ttu-id="1bf4f-196">Merhaba uygulaması yeniden boyutlandırılırken çok etkili olur.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-196">It is very effective when hello application is resizing.</span></span>
* <span data-ttu-id="1bf4f-197">Merhaba katılım html dosyasındaki hello webview içerik, tasarım açıklamakta ve birbirleri arasındaki öğeleri konum hello.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-197">In hello Engagement html file we describe hello webview content, design and hello elements positions between each other.</span></span>

### <a name="launch-message"></a><span data-ttu-id="1bf4f-198">İleti Başlatma</span><span class="sxs-lookup"><span data-stu-id="1bf4f-198">Launch message</span></span>
<span data-ttu-id="1bf4f-199">Bir kullanıcı bir sistem bildirimi (bildirim) tıkladığında, katılım Merhaba uygulaması başlatır, yük hello Merhaba içeriğine iletileri gönderme ve hello ilgili kampanya hello sayfayı görüntüleme.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-199">When a user clicks on a system notification (a toast), Engagement launches hello application, load hello content of hello push messages, and display hello page for hello corresponding campaign.</span></span>

<span data-ttu-id="1bf4f-200">Merhaba başlatma (bağlı olarak, ağ hızına hello) hello sayfasının hello uygulama ve hello görüntüsünün arasında bir gecikme yoktur.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-200">There is a delay between hello launch of hello application and hello display of hello page (depending on hello speed of your network).</span></span>

<span data-ttu-id="1bf4f-201">bir şey yüklüyor tooindicate toohello kullanıcı, bir ilerleme çubuğu veya bir İlerleme göstergesi gibi görsel bir bilgi sağlamalıdır.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-201">tooindicate toohello user that something is loading, you should provide a visual information, like a progress bar or a progress indicator.</span></span> <span data-ttu-id="1bf4f-202">Katılım kendisi, ancak sağladığı birkaç işleyicileri sizin için işleyemez.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-202">Engagement cannot handle that itself, but provides a few handlers for you.</span></span>

<span data-ttu-id="1bf4f-203">"Genel App() {}" App.xaml.cs dosyasında tooimplement hello geri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="1bf4f-203">tooimplement hello callback, in App.xaml.cs in "Public App(){}" add:</span></span>

            /* hello application has launched and hello content is loading.
             * You should display an indicator here.
             */
            EngagementReach.Instance.RetrieveLaunchMessageStarted += () => { [...] };

            /* hello application has finished loading hello content and hello page
             * is about toobe displayed.
             * You should hide hello indicator here.
             */
            EngagementReach.Instance.RetrieveLaunchMessageCompleted += () => { [...] };

            /* hello content has been loaded, but an error has occurred.
             * You can provide an information toohello user.
             * You should hide hello indicator here.
             */
            EngagementReach.Instance.RetrieveLaunchMessageFailed += () => { [...] };

<span data-ttu-id="1bf4f-204">Merhaba geri çağırma "Ortak App() {}" yönteminizi ayarlayabilirsiniz, `App.xaml.cs` dosya, tercihen hello önce `EngagementReach.Instance.Init()` çağırın.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-204">You can set hello callback in your "Public App(){}" method of your `App.xaml.cs` file, preferably before hello `EngagementReach.Instance.Init()` call.</span></span>

> [!TIP]
> <span data-ttu-id="1bf4f-205">Her işleyici hello tarafından kullanıcı Arabirimi iş parçacığı denir.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-205">Each handler is called by hello UI Thread.</span></span> <span data-ttu-id="1bf4f-206">MessageBox veya bir şey UI ilgili kullanırken tooworry yok.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-206">You do not have tooworry when using a MessageBox or something UI-related.</span></span>
> 
> 

## <span data-ttu-id="1bf4f-207"><a id="push-channel-sharing"></a>Kanal paylaşımı gönderme</span><span class="sxs-lookup"><span data-stu-id="1bf4f-207"><a id="push-channel-sharing"></a> Push channel sharing</span></span>
<span data-ttu-id="1bf4f-208">Ardından, uygulamanızda anında iletme bildirimleri başka bir amaç için kullanıyorsanız, hello Engagement SDK'sı özelliği paylaşımı toouse hello itme kanal sahip.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-208">If you are using push notifications for another purpose in your application then you have toouse hello push channel sharing feature of hello Engagement SDK.</span></span> <span data-ttu-id="1bf4f-209">Eksik tooavoid itme budur.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-209">This is tooavoid missed push.</span></span>

* <span data-ttu-id="1bf4f-210">Engagement Reach kendi itme kanal toohello başlatma sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-210">You can provide your own push channel toohello Engagement Reach initialization.</span></span> <span data-ttu-id="1bf4f-211">Merhaba SDK yeni bir tane isteyen yerine kullanır.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-211">hello SDK will use it instead of requesting a new one.</span></span>

<span data-ttu-id="1bf4f-212">Merhaba, anında iletme kanalda ile Merhaba Engagement Reach başlatma güncelleştirme `InitEngagement` hello yönteminden `App.xaml.cs` dosyası:</span><span class="sxs-lookup"><span data-stu-id="1bf4f-212">Update hello Engagement Reach initialization with your push channel in hello `InitEngagement` method from hello `App.xaml.cs` file:</span></span>

    /* Your own push channel logic... */
    var pushChannel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    /*...Engagement initialization */
    EngagementAgent.Instance.Init(e);
    EngagementReach.Instance.Init(e,pushChannel);

* <span data-ttu-id="1bf4f-213">Alternatif olarak, yalnızca istiyorsanız tooconsume hello anında kanal hello ulaşma başlattıktan sonra hello SDK tarafından oluşturulduktan sonra bir geri çağırma Engagement Reach tooget hello itme kanalda ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-213">Alternatively, if you just want tooconsume hello push channel after hello Reach initialization then you can set a callback on Engagement Reach tooget hello push channel once it is created by hello SDK.</span></span>

<span data-ttu-id="1bf4f-214">Herhangi bir noktada, geri aramasını ayarlamasını **sonra** ulaşma başlatma hello:</span><span class="sxs-lookup"><span data-stu-id="1bf4f-214">Set your callback at any place **after** hello Reach initialization :</span></span>

    /* Set action on hello SDK push channel. */
    EngagementReach.Instance.SetActionOnPushChannel((PushNotificationChannel channel) => 
    {
      /* hello forwarded channel can be null if its creation fails for any reason. */
      if (channel != null)
      {
        /* Your own push channel logic... */
      });
    }

## <a name="custom-scheme-tip"></a><span data-ttu-id="1bf4f-215">Özel şema İpucu</span><span class="sxs-lookup"><span data-stu-id="1bf4f-215">Custom scheme tip</span></span>
<span data-ttu-id="1bf4f-216">Özel şema kullanım sunuyoruz.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-216">We provide custom scheme use.</span></span> <span data-ttu-id="1bf4f-217">Katılım uygulamanızda kullanılan katılım ön uç toobe öğesinden farklı türde bir URI gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-217">You can send different type of URI from engagement frontend toobe used in your engagement application.</span></span> <span data-ttu-id="1bf4f-218">Varsayılan şema gibi `http, ftp, ...` olan yönetmek penceresi olacak Windows komut isteminde bir varsayılan uygulama cihazda yüklü olmaları durumunda.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-218">Default scheme like `http, ftp, ...` are manage by Windows, a window will prompt if they are no default application installed on device.</span></span> <span data-ttu-id="1bf4f-219">Ayrıca, uygulamanız için kendi özel şema oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-219">You can also create your own custom scheme for your application.</span></span>

<span data-ttu-id="1bf4f-220">Merhaba basit yol tooset uygulamanızda özel bir düzeni olduğunu tooopen, `Package.appxmanifest` içinde gidin `Declarations` paneli.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-220">hello simple way tooset a custom scheme in your application is tooopen your `Package.appxmanifest` go in `Declarations` panel.</span></span> <span data-ttu-id="1bf4f-221">Seçin `Protocol` hello kullanılabilir bildirimleri Kaydırma kutusu ve ekleyin.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-221">Select `Protocol` in hello Available Declarations scroll box and add it.</span></span> <span data-ttu-id="1bf4f-222">Merhaba Düzenle `Name` yeni Protokolü alanıyla istenen adı.</span><span class="sxs-lookup"><span data-stu-id="1bf4f-222">Edit hello `Name` field with your new protocol desired name.</span></span>

<span data-ttu-id="1bf4f-223">Şimdi toouse bu protokolü düzenlemek, `App.xaml.cs` hello ile `OnActivated` yöntemi ve burada tooinitialize katılım de unutmayın:</span><span class="sxs-lookup"><span data-stu-id="1bf4f-223">Now toouse this protocol, edit your `App.xaml.cs` with hello `OnActivated` method, and don't forget tooinitialize engagement here also:</span></span>

            /// <summary>
            /// Enter point when app his called by another way than user click
            /// </summary>
            /// <param name="args">Activation args</param>
            protected override void OnActivated(IActivatedEventArgs args)
            {
              /* Init engagement like it was launch by a custom uri scheme */
              EngagementAgent.Instance.Init(args);
              EngagementReach.Instance.Init(args);

              //TODO design action toodo when app is launch

              #region Custom scheme use
              if (args.Kind == ActivationKind.Protocol)
              {
                ProtocolActivatedEventArgs myProtocol = (ProtocolActivatedEventArgs)args;

                if (myProtocol.Uri.Scheme.Equals("protocolName"))
                {
                  string path = myProtocol.Uri.AbsolutePath;
                }
              }
              #endregion

