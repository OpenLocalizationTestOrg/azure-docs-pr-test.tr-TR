---
title: "Windows Evrensel uygulamaları Azure Mobile Engagement ile aaaGet başlatıldı"
description: "Bilgi nasıl toouse Azure Mobile Engagement Windows Evrensel uygulamaları için analizler ve anında iletme bildirimleri ile."
services: mobile-engagement
documentationcenter: windows
author: piyushjo
manager: erikre
editor: 
ms.assetid: 48103867-7f64-4646-b019-42bd797d38e2
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/12/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 8224a6d3789cfe4784bbc9472005f9eddb94a8b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-windows-universal-apps"></a><span data-ttu-id="40a3e-103">Windows Evrensel Uygulamaları için Azure Mobile Engagement kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="40a3e-103">Get started with Azure Mobile Engagement for Windows Universal Apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="40a3e-104">Bu konu, nasıl gösterir toouse Azure Mobile Engagement toounderstand uygulama kullanımı ve gönderme anında iletme bildirimleri toosegmented kullanıcılar Windows Evrensel uygulamasının.</span><span class="sxs-lookup"><span data-stu-id="40a3e-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and send push notifications toosegmented users of a Windows Universal application.</span></span>
<span data-ttu-id="40a3e-105">Bu öğretici, Mobile Engagement kullanarak hello basit yayın senaryosunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="40a3e-105">This tutorial demonstrates hello simple broadcast scenario using Mobile Engagement.</span></span> <span data-ttu-id="40a3e-106">Temel uygulama kullanımı verilerini toplayan ve Windows Bildirim Hizmeti’ni (WNS) kullanarak anında iletme bildirimleri alan boş bir Windows Evrensel Uygulaması oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="40a3e-106">You create a blank Windows Universal App that collects basic app usage data and receives push notifications using Windows Notification Service (WNS).</span></span>

> [!NOTE]
> <span data-ttu-id="40a3e-107">Hello Azure Mobile Engagement hizmet Mart 2018 kullanımdan kaldırılır ve şu anda yalnızca kullanılabilir tooexisting müşterileri içindir.</span><span class="sxs-lookup"><span data-stu-id="40a3e-107">hello Azure Mobile Engagement service will be retired March 2018 and is currently only available tooexisting customers.</span></span> <span data-ttu-id="40a3e-108">Daha fazla bilgi için bkz. [Mobile Engagement nedir?](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span><span class="sxs-lookup"><span data-stu-id="40a3e-108">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="40a3e-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="40a3e-109">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

## <a name="set-up-mobile-engagement-for-your-windows-universal-app"></a><span data-ttu-id="40a3e-110">Windows Evrensel uygulamanız için Mobile Engagement kurma</span><span class="sxs-lookup"><span data-stu-id="40a3e-110">Set up Mobile Engagement for your Windows Universal app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="40a3e-111"><a id="connecting-app"></a>Uygulamanızın toohello Mobile Engagement arka ucuna bağlanmak</span><span class="sxs-lookup"><span data-stu-id="40a3e-111"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="40a3e-112">Bu öğretici "Merhaba en az gerekli toocollect veri kümesi ve bir anında iletme bildirimi gönderme bir temel tümleştirme" gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="40a3e-112">This tutorial presents a "basic integration," which is hello minimal set required toocollect data and send a push notification.</span></span> <span data-ttu-id="40a3e-113">Merhaba tümleştirme belgelerinin tamamı hello bulunabilir [Mobile Engagement Windows Evrensel SDK tümleştirmesi](mobile-engagement-windows-store-sdk-overview.md).</span><span class="sxs-lookup"><span data-stu-id="40a3e-113">hello complete integration documentation can be found in hello [Mobile Engagement Windows Universal SDK integration](mobile-engagement-windows-store-sdk-overview.md).</span></span>

<span data-ttu-id="40a3e-114">Visual Studio toodemonstrate hello Tümleştirmesi ile temel bir uygulama oluşturun.</span><span class="sxs-lookup"><span data-stu-id="40a3e-114">You create a basic app with Visual Studio toodemonstrate hello integration.</span></span>

### <a name="create-a-windows-universal-app-project"></a><span data-ttu-id="40a3e-115">Bir Windows Evrensel Uygulaması projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="40a3e-115">Create a Windows Universal App project</span></span>
<span data-ttu-id="40a3e-116">Visual Studio'nun önceki sürümleri başlangıç adımları benzerdir olsa hello aşağıdaki adımlarda Visual Studio 2015 hello kullanımını varsayılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="40a3e-116">hello following steps assume hello use of Visual Studio 2015 though hello steps are similar in earlier versions of Visual Studio.</span></span>

1. <span data-ttu-id="40a3e-117">Visual Studio'yu başlatın ve hello **giriş** ekran, select **yeni proje**.</span><span class="sxs-lookup"><span data-stu-id="40a3e-117">Start Visual Studio, and in hello **Home** screen, select **New Project**.</span></span>
2. <span data-ttu-id="40a3e-118">Merhaba açılır pencerede seçin **Windows** -> **Evrensel** -> **boş uygulama (Evrensel Windows)**.</span><span class="sxs-lookup"><span data-stu-id="40a3e-118">In hello pop-up, select **Windows** -> **Universal** -> **Blank App (Universal Windows)**.</span></span> <span data-ttu-id="40a3e-119">Merhaba doldurup **adı** ve **çözüm adı**ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="40a3e-119">Fill in hello app **Name** and **Solution name**, and then click **OK**.</span></span>

    ![][1]

<span data-ttu-id="40a3e-120">Bir Windows Evrensel uygulama projesi sonraki hello Azure Mobile Engagement SDK'sını tümleştirmek oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="40a3e-120">You have now created a Windows Universal App project into which you next integrate hello Azure Mobile Engagement SDK.</span></span>

### <a name="connect-your-app-toomobile-engagement-backend"></a><span data-ttu-id="40a3e-121">Uygulamanızın tooMobile Engagement arka ucuna bağlanmak</span><span class="sxs-lookup"><span data-stu-id="40a3e-121">Connect your app tooMobile Engagement backend</span></span>
1. <span data-ttu-id="40a3e-122">Merhaba yüklemek [MicrosoftAzure.MobileEngagement] Nuget paketini projenize.</span><span class="sxs-lookup"><span data-stu-id="40a3e-122">Install hello [MicrosoftAzure.MobileEngagement] Nuget package in your project.</span></span> <span data-ttu-id="40a3e-123">Windows ve Windows Phone platformlarının hedefliyorsanız, toodo bu iki projeleri için gerekir.</span><span class="sxs-lookup"><span data-stu-id="40a3e-123">If you are targeting both Windows and Windows Phone platforms, you need toodo this for both projects.</span></span> <span data-ttu-id="40a3e-124">Windows 8.x ve Windows Phone 8.1, hello aynı Nuget paketi yerler hello doğru platforma özgü ikili dosyalarını her projede.</span><span class="sxs-lookup"><span data-stu-id="40a3e-124">For Windows 8.x and Windows Phone 8.1, hello same Nuget package places hello correct platform-specific binaries in each project.</span></span>
2. <span data-ttu-id="40a3e-125">Açık **Package.appxmanifest** ve yetenek aşağıdaki o hello var. eklendiğinden emin olun:</span><span class="sxs-lookup"><span data-stu-id="40a3e-125">Open **Package.appxmanifest** and make sure that hello following capability is added there:</span></span>

        Internet (Client)

    ![][2]
3. <span data-ttu-id="40a3e-126">Şimdi daha önce Mobile Engagement uygulamanız için kopyaladığınız hello bağlantı dizesini kopyalayın ve hello Yapıştır `Resources\EngagementConfiguration.xml` hello arasında dosya `<connectionString>` ve `</connectionString>` etiketler:</span><span class="sxs-lookup"><span data-stu-id="40a3e-126">Now copy hello connection string that you copied earlier for your Mobile Engagement App and paste it in hello `Resources\EngagementConfiguration.xml` file, between hello `<connectionString>` and `</connectionString>` tags:</span></span>

    ![][3]

    > [!TIP]
    > <span data-ttu-id="40a3e-127">Uygulamanız, Windows ve Windows Phone platformlarının ikisini de hedefliyorsa, desteklenen her platform için birer adet olmak üzere iki adet Mobile Engagement Uygulaması oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="40a3e-127">If your App targets both Windows and Windows Phone platforms, you should still create two Mobile Engagement Applications - one for each supported platform.</span></span> <span data-ttu-id="40a3e-128">İki uygulama sahip hello hedef kitleyi segmentlere doğru oluşturabilirsiniz ve her platform için uygun şekilde hedefe yönelik bildirimler gönderebilirsiniz sağlar.</span><span class="sxs-lookup"><span data-stu-id="40a3e-128">Having two apps ensures that you can create correct segmentation of hello audience and can send appropriately targeted notifications for each platform.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="40a3e-129">NuGet Windows 10 UWP uygulamanızda hello SDK kaynakları otomatik olarak kopyalamaz.</span><span class="sxs-lookup"><span data-stu-id="40a3e-129">NuGet does not automatically copy hello SDK resources in your Windows 10 UWP application.</span></span> <span data-ttu-id="40a3e-130">Bunu el ile Merhaba Nuget paketi yüklendiğinde (readme.txt) göster hello adımları izleyerek toodo sahip.</span><span class="sxs-lookup"><span data-stu-id="40a3e-130">You have toodo it manually following hello steps which show up (readme.txt) when hello Nuget package is installed.</span></span>  

1. <span data-ttu-id="40a3e-131">Merhaba, `App.xaml.cs` dosyası:</span><span class="sxs-lookup"><span data-stu-id="40a3e-131">In hello `App.xaml.cs` file:</span></span>

    <span data-ttu-id="40a3e-132">a.</span><span class="sxs-lookup"><span data-stu-id="40a3e-132">a.</span></span> <span data-ttu-id="40a3e-133">Merhaba eklemek `using` deyimi:</span><span class="sxs-lookup"><span data-stu-id="40a3e-133">Add hello `using` statement:</span></span>

            using Microsoft.Azure.Engagement;

    <span data-ttu-id="40a3e-134">b.</span><span class="sxs-lookup"><span data-stu-id="40a3e-134">b.</span></span> <span data-ttu-id="40a3e-135">Merhaba katılım başlatan bir yöntemi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="40a3e-135">Add a method that initializes hello Engagement:</span></span>

           private void InitEngagement(IActivatedEventArgs e)
           {
             EngagementAgent.Instance.Init(e);

             //... rest of hello code
           }

    <span data-ttu-id="40a3e-136">c.</span><span class="sxs-lookup"><span data-stu-id="40a3e-136">c.</span></span> <span data-ttu-id="40a3e-137">Merhaba Hello SDK başlatma **OnLaunched** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="40a3e-137">Initialize hello SDK in hello **OnLaunched** method:</span></span>

            protected override void OnLaunched(LaunchActivatedEventArgs e)
            {
              InitEngagement(e);

              //... rest of hello code
            }

    <span data-ttu-id="40a3e-138">c.</span><span class="sxs-lookup"><span data-stu-id="40a3e-138">c.</span></span> <span data-ttu-id="40a3e-139">Merhaba aşağıdaki hello Ekle **OnActivated** yöntemi ve zaten mevcut değilse hello yöntemi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="40a3e-139">Insert hello following in hello **OnActivated** method and add hello method if it is not already present:</span></span>

            protected override void OnActivated(IActivatedEventArgs e)
            {
              InitEngagement(e);

              //... rest of hello code
            }

## <span data-ttu-id="40a3e-140"><a id="monitor"></a>Gerçek zamanlı izlemeyi etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="40a3e-140"><a id="monitor"></a>Enable real-time monitoring</span></span>
<span data-ttu-id="40a3e-141">verileri gönderilirken toostart ve hello kullanıcıların etkin olduğundan emin olmak, en az bir ekran (etkinlik) toohello Mobile Engagement arka göndermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="40a3e-141">toostart sending data and ensuring that hello users are active, you must send at least one screen (Activity) toohello Mobile Engagement backend.</span></span>

1. <span data-ttu-id="40a3e-142">Merhaba, **MainPage.xaml.cs**, hello aşağıdakileri ekleyin `using` deyimi:</span><span class="sxs-lookup"><span data-stu-id="40a3e-142">In hello **MainPage.xaml.cs**, add hello following `using` statement:</span></span>

    <span data-ttu-id="40a3e-143">Microsoft.Azure.Engagement.Overlay’i kullanarak</span><span class="sxs-lookup"><span data-stu-id="40a3e-143">using Microsoft.Azure.Engagement.Overlay;</span></span>
2. <span data-ttu-id="40a3e-144">Değiştirme hello temel sınıfını **MainPage** gelen **sayfa** çok**EngagementPageOverlay**:</span><span class="sxs-lookup"><span data-stu-id="40a3e-144">Change hello base class of **MainPage** from **Page** too**EngagementPageOverlay**:</span></span>

        class MainPage : EngagementPageOverlay
3. <span data-ttu-id="40a3e-145">Merhaba, `MainPage.xaml` dosyası:</span><span class="sxs-lookup"><span data-stu-id="40a3e-145">In hello `MainPage.xaml` file:</span></span>

    <span data-ttu-id="40a3e-146">a.</span><span class="sxs-lookup"><span data-stu-id="40a3e-146">a.</span></span> <span data-ttu-id="40a3e-147">Tooyour ad alanları bildirimleri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="40a3e-147">Add tooyour namespaces declarations:</span></span>

        xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"

    <span data-ttu-id="40a3e-148">b.</span><span class="sxs-lookup"><span data-stu-id="40a3e-148">b.</span></span> <span data-ttu-id="40a3e-149">Hello yerine **sayfa** hello XML etiket adı ile **engagement: EngagementPageOverlay**</span><span class="sxs-lookup"><span data-stu-id="40a3e-149">Replace hello **Page** in hello XML tag name with **engagement:EngagementPageOverlay**</span></span>

> [!IMPORTANT]
> <span data-ttu-id="40a3e-150">Sayfanız hello kılıyorsa `OnNavigatedTo` yöntemi, emin toocall olması `base.OnNavigatedTo(e)`.</span><span class="sxs-lookup"><span data-stu-id="40a3e-150">If your page overrides hello `OnNavigatedTo` method, be sure toocall `base.OnNavigatedTo(e)`.</span></span> <span data-ttu-id="40a3e-151">Aksi takdirde hello etkinlik bildirilmedi `EngagementPage` çağrıları `StartActivity` içinde kendi `OnNavigatedTo` yöntemi).</span><span class="sxs-lookup"><span data-stu-id="40a3e-151">Otherwise, hello activity is not reported `EngagementPage` calls `StartActivity` inside its `OnNavigatedTo` method).</span></span> <span data-ttu-id="40a3e-152">Bu hello varsayılan şablonu sahip olduğu bir Windows Phone projesinde özellikle önemlidir bir `OnNavigatedTo` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="40a3e-152">This is especially important in a Windows Phone project where hello default template has an `OnNavigatedTo` method.</span></span>
>
> <span data-ttu-id="40a3e-153">İçin **Windows 10 Universal uygulamalarının**, hello önerilen hello yöntemi kullanın "yöntemi önerilir: sayfa sınıflarınızı aşırı yükleme" kısmında [Gelişmiş raporlama hello Windows Evrensel uygulamaları Engagement SDK'sı ile](mobile-engagement-windows-store-advanced-reporting.md) , hello yerine bir bahsedilen üstünde.</span><span class="sxs-lookup"><span data-stu-id="40a3e-153">For **Windows 10 Universal apps**, use hello method recommended in hello "Recommended method: overload your Page classes" section of [Advanced Reporting with hello Windows Universal Apps Engagement SDK](mobile-engagement-windows-store-advanced-reporting.md), rather than hello one mentioned above.</span></span>

## <span data-ttu-id="40a3e-154"><a id="monitor"></a>Uygulamayı gerçek zamanlı izlemeyle bağlama</span><span class="sxs-lookup"><span data-stu-id="40a3e-154"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="40a3e-155"><a id="integrate-push"></a>Anında iletme bildirimlerini ve uygulama içi mesajlaşmayı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="40a3e-155"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="40a3e-156">Mobile Engagement toointeract sağlar ve kullanıcılarınızın anında iletme bildirimleri ve uygulama içi Mesajlaşma hello Kampanyalar bağlamında ulaşılırsa.</span><span class="sxs-lookup"><span data-stu-id="40a3e-156">Mobile Engagement allows you toointeract and reach your users with push notifications and in-app messaging in hello context of campaigns.</span></span> <span data-ttu-id="40a3e-157">Bu modül hello Mobile Engagement portalında REACH adı verilir.</span><span class="sxs-lookup"><span data-stu-id="40a3e-157">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="40a3e-158">Merhaba aşağıdaki bölümlerde, app tooreceive bunları ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="40a3e-158">hello following sections set up your app tooreceive them.</span></span>

### <a name="enable-your-app-tooreceive-wns-push-notifications"></a><span data-ttu-id="40a3e-159">Uygulama tooreceive WNS anında iletme bildirimlerini etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="40a3e-159">Enable your app tooreceive WNS Push Notifications</span></span>
1. <span data-ttu-id="40a3e-160">Merhaba, `Package.appxmanifest` dosyasında hello **uygulama** sekmesinde, altında **bildirimleri**ayarlayın **bildirim özellikli:** çok**Evet**</span><span class="sxs-lookup"><span data-stu-id="40a3e-160">In hello `Package.appxmanifest` file, in hello **Application** tab, under **Notifications**, set **Toast capable:** too**Yes**</span></span>

    ![][5]

### <a name="initialize-hello-reach-sdk"></a><span data-ttu-id="40a3e-161">Merhaba REACH SDK'yı başlatma</span><span class="sxs-lookup"><span data-stu-id="40a3e-161">Initialize hello REACH SDK</span></span>
<span data-ttu-id="40a3e-162">İçinde `App.xaml.cs`, çağrı **Initengagement** hello içinde **engagementreach.Instance.Init(e);** işlevi hello aracı başlatmadan hemen sonra:</span><span class="sxs-lookup"><span data-stu-id="40a3e-162">In `App.xaml.cs`, call **EngagementReach.Instance.Init(e);** in hello **InitEngagement** function right after hello agent initialization:</span></span>

        private void InitEngagement(IActivatedEventArgs e)
        {
           EngagementAgent.Instance.Init(e);
           EngagementReach.Instance.Init(e);
        }

<span data-ttu-id="40a3e-163">Hazır toosend bir bildirim demektir.</span><span class="sxs-lookup"><span data-stu-id="40a3e-163">You're ready toosend a toast.</span></span> <span data-ttu-id="40a3e-164">Şimdi bu temel tümleştirmeyi doğru bir şekilde gerçekleştirdiğinizi doğrulayacağız.</span><span class="sxs-lookup"><span data-stu-id="40a3e-164">Next we verify that you have correctly carried out this basic integration.</span></span>

### <a name="grant-access-toomobile-engagement-toosend-notifications"></a><span data-ttu-id="40a3e-165">GRANT erişim tooMobile katılım toosend bildirimleri</span><span class="sxs-lookup"><span data-stu-id="40a3e-165">Grant access tooMobile Engagement toosend notifications</span></span>
1. <span data-ttu-id="40a3e-166">Web tarayıcınızda [Windows Mağazası Geliştirme Merkezi]’ni açın, oturum açın ve gerekiyorsa bir hesap oluşturun.</span><span class="sxs-lookup"><span data-stu-id="40a3e-166">Open [Windows Store Dev Center] in your web browser, login, and create an account if necessary.</span></span>
2. <span data-ttu-id="40a3e-167">Tıklatın **Pano** hello sağ üst köşe ve ardından **yeni uygulama oluştur** hello sol panel menüsünde.</span><span class="sxs-lookup"><span data-stu-id="40a3e-167">Click **Dashboard** at hello top right corner and then click **Create a new app** from hello left panel menu.</span></span>

    ![][9]
3. <span data-ttu-id="40a3e-168">Adını ayırarak uygulamanızı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="40a3e-168">Create your app by reserving its name.</span></span>

    ![][10]
4. <span data-ttu-id="40a3e-169">Merhaba uygulama oluşturulduktan sonra çok gidin**Hizmetleri -> anında iletme bildirimleri** hello sol menüden.</span><span class="sxs-lookup"><span data-stu-id="40a3e-169">Once hello app has been created, navigate too**Services -> Push notifications** from hello left menu.</span></span>

    ![][11]
5. <span data-ttu-id="40a3e-170">Bildirimler bölümü Hello itme, hello tıklatın **Live Services sitesi** bağlantı.</span><span class="sxs-lookup"><span data-stu-id="40a3e-170">In hello Push notifications section, click hello **Live Services site** link.</span></span>

    ![][12]
6. <span data-ttu-id="40a3e-171">Toohello gönderim kimlik bilgileri bölümüne gidin.</span><span class="sxs-lookup"><span data-stu-id="40a3e-171">You navigate toohello Push credentials section.</span></span> <span data-ttu-id="40a3e-172">Hello olduğundan emin olun **uygulama ayarları** bölümünde ve ardından kopyalama, **paket SID'si** ve **istemci parolası**</span><span class="sxs-lookup"><span data-stu-id="40a3e-172">Make sure you are in hello **App Settings** section and then copy your **Package SID** and **Client secret**</span></span>

    ![][13]
7. <span data-ttu-id="40a3e-173">Toohello gidin **ayarları** , Mobile Engagement portalının hello tıklatıp **yerel gönderim** hello soldaki bölüm.</span><span class="sxs-lookup"><span data-stu-id="40a3e-173">Navigate toohello **Settings** of your Mobile Engagement portal, and click hello **Native Push** section on hello left.</span></span> <span data-ttu-id="40a3e-174">Merhaba ardından **Düzenle** düğmesini tooenter, **paket güvenlik tanımlayıcısı (SID)** ve **gizli anahtar** gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="40a3e-174">Then, click hello **Edit** button tooenter your **Package security identifier (SID)** and your **Secret Key** as shown:</span></span>

    ![][6]
8. <span data-ttu-id="40a3e-175">Son olarak, Visual Studio uygulamanızı hello uygulama Mağazası'nda oluşturulan bu uygulama ile ilişkilendirdiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="40a3e-175">Finally make sure that you have associated your Visual Studio app with this created app in hello App store.</span></span> <span data-ttu-id="40a3e-176">Visual Studio’da **Uygulamayı Mağaza ile İlişkilendir**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="40a3e-176">Click **Associate App with Store** in Visual Studio.</span></span>

    ![][7]

## <span data-ttu-id="40a3e-177"><a id="send"></a>Bir bildirim tooyour uygulaması Gönder</span><span class="sxs-lookup"><span data-stu-id="40a3e-177"><a id="send"></a>Send a notification tooyour app</span></span>
[!INCLUDE [Create Windows Push campaign](../../includes/mobile-engagement-windows-push-campaign.md)]

<span data-ttu-id="40a3e-178">Merhaba uygulama çalışıyorsa, bir uygulama içi bildirim görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="40a3e-178">If hello app is running, you see an in-app notification.</span></span> <span data-ttu-id="40a3e-179">Aksi takdirde Hello uygulama kapalıysa, bir bildirim görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="40a3e-179">otherwise if hello app is closed, you see a toast notification.</span></span>
<span data-ttu-id="40a3e-180">Bir uygulama bildirimi ancak bildirim bakın ve Visual Studio'da hata ayıklama modunda hello uygulama çalıştırıyorsanız, daha sonra deneyin **yaşam döngüsü olayları -> Askıya Al** hello araç tooensure bu hello uygulama askıya alınır.</span><span class="sxs-lookup"><span data-stu-id="40a3e-180">If you see an in-app notification but not a toast notification, and you are running hello app in debug mode in Visual Studio, then try **Lifecycle events -> Suspend** in hello toolbar tooensure that hello app is suspended.</span></span> <span data-ttu-id="40a3e-181">Merhaba uygulaması Visual Studio'da hata ayıklarken hello giriş düğmesine tıkladıysanız, ardından bu her zaman askıya alınmaz ve uygulama hello bildirim bakın, ancak bunu bir bildirim gösterilmesini.</span><span class="sxs-lookup"><span data-stu-id="40a3e-181">If you clicked hello Home button while debugging hello application in Visual Studio, then it doesn't always get suspended and while you see hello notification as in-app, it doesn't show up as a toast notification.</span></span>  

![][8]

<!-- URLs. -->
[Mobile Engagement Windows Universal SDK documentation]: ../mobile-engagement-windows-store-integrate-engagement/
[MicrosoftAzure.MobileEngagement]: http://go.microsoft.com/?linkid=9864592
[Windows Mağazası Geliştirme Merkezi]: https://dev.windows.com
[Windows Universal Apps - Overlay integration]: ../mobile-engagement-windows-store-integrate-engagement-reach/#overlay-integration

<!-- Images. -->
[1]: ./media/mobile-engagement-windows-store-dotnet-get-started/universal-app-creation.png
[2]: ./media/mobile-engagement-windows-store-dotnet-get-started/manifest-capabilities.png
[3]: ./media/mobile-engagement-windows-store-dotnet-get-started/add-connection-info.png
[5]: ./media/mobile-engagement-windows-store-dotnet-get-started/manifest-toast.png
[6]: ./media/mobile-engagement-windows-store-dotnet-get-started/enter-credentials.png
[7]: ./media/mobile-engagement-windows-store-dotnet-get-started/associate-app-store.png
[8]: ./media/mobile-engagement-windows-store-dotnet-get-started/vs-suspend.png
[9]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_create_app.png
[10]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_app_name.png
[11]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_services_push.png
[12]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_services_push_1.png
[13]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_services_push_creds.png
