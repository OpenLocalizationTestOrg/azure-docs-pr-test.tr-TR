---
title: "Windows Phone Silverlight için Azure Mobile Engagement uygulamalarla aaaGet başlatıldı"
description: "Bilgi nasıl Windows Phone Silverlight uygulamaları için analizler ve anında iletme bildirimleri ile Azure Mobile Engagement toouse."
services: mobile-engagement
documentationcenter: windows
author: piyushjo
manager: erikre
editor: 
ms.assetid: aa34692f-87f7-47c6-a20c-a1972750bc25
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: b39a838ab03217b2dc845cbf59d7bf8b094dac1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-windows-phone-silverlight-apps"></a><span data-ttu-id="292b9-103">Windows Phone Silverlight uygulamaları için Azure Mobile Engagement kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="292b9-103">Get started with Azure Mobile Engagement for Windows Phone Silverlight apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="292b9-104">Bu konu, nasıl gösterir toouse Azure Mobile Engagement toounderstand uygulama kullanımı ve gönderme anında iletme bildirimleri toosegmented kullanıcılar Windows Phone Silverlight uygulaması.</span><span class="sxs-lookup"><span data-stu-id="292b9-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and send push notifications toosegmented users of a Windows Phone Silverlight application.</span></span>
<span data-ttu-id="292b9-105">Bu öğretici, Mobile Engagement kullanarak hello basit yayın senaryosunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="292b9-105">This tutorial demonstrates hello simple broadcast scenario using Mobile Engagement.</span></span> <span data-ttu-id="292b9-106">Temel verileri toplayan ve Microsoft Anında İletme Bildirimi Hizmeti’ni (MPNS) kullanarak anında iletme bildirimleri alan boş bir Windows Phone Silverlight uygulaması oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="292b9-106">In it, you create a blank Windows Phone Silverlight app that collects basic data and receives push notifications using Microsoft Push Notification Service (MPNS).</span></span>

> [!NOTE]
> <span data-ttu-id="292b9-107">Hello Azure Mobile Engagement hizmet Mart 2018 kullanımdan kaldırılır ve şu anda yalnızca kullanılabilir tooexisting müşterileri içindir.</span><span class="sxs-lookup"><span data-stu-id="292b9-107">hello Azure Mobile Engagement service will be retired March 2018 and is currently only available tooexisting customers.</span></span> <span data-ttu-id="292b9-108">Daha fazla bilgi için bkz. [Mobile Engagement nedir?](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span><span class="sxs-lookup"><span data-stu-id="292b9-108">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

> [!NOTE]
> <span data-ttu-id="292b9-109">Windows Phone 8.1 ve önceki sürümlerde oluşturulmuş projeler Visual Studio 2017’de desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="292b9-109">Windows Phone 8.1 and prior version projects are not supported in Visual Studio 2017.</span></span>  <span data-ttu-id="292b9-110">Daha fazla bilgi için bkz. [Visual Studio 2017 Platform Desteği ve Uyumluluk](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span><span class="sxs-lookup"><span data-stu-id="292b9-110">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span>

> [!NOTE]
> <span data-ttu-id="292b9-111">Windows Phone 8.1 (Silverlight olmayan) hedefliyorsanız, toohello başvuran [Windows Evrensel Öğreticisine](mobile-engagement-windows-store-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="292b9-111">If you are targeting Windows Phone 8.1 (non-Silverlight), refer toohello [Windows Universal tutorial](mobile-engagement-windows-store-dotnet-get-started.md).</span></span>
> 
> 

<span data-ttu-id="292b9-112">Bu öğretici hello aşağıdakileri gerektirir:</span><span class="sxs-lookup"><span data-stu-id="292b9-112">This tutorial requires hello following:</span></span>

* <span data-ttu-id="292b9-113">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="292b9-113">Visual Studio 2013</span></span>
* <span data-ttu-id="292b9-114">[MicrosoftAzure.MobileEngagement] Nuget paketi</span><span class="sxs-lookup"><span data-stu-id="292b9-114">[MicrosoftAzure.MobileEngagement] Nuget package</span></span>

> [!NOTE]
> <span data-ttu-id="292b9-115">toocomplete Bu öğretici, etkin bir Azure hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="292b9-115">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="292b9-116">Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="292b9-116">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="292b9-117">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-windows-phone-get-started).</span><span class="sxs-lookup"><span data-stu-id="292b9-117">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-windows-phone-get-started).</span></span>
> 
> 

## <span data-ttu-id="292b9-118"><a id="setup-azme"></a>Windows Phone uygulamanıza Mobile Engagement’i kurma</span><span class="sxs-lookup"><span data-stu-id="292b9-118"><a id="setup-azme"></a>Setup Mobile Engagement for your Windows Phone app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="292b9-119"><a id="connecting-app"></a>Uygulamanızın toohello Mobile Engagement arka ucuna bağlanmak</span><span class="sxs-lookup"><span data-stu-id="292b9-119"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="292b9-120">Bu öğreticide "Merhaba en az gerekli toocollect veri kümesi ve bir anında iletme bildirimi gönderme bir"temel tümleştirme"gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="292b9-120">This tutorial presents a "basic integration", which is hello minimal set required toocollect data and send a push notification.</span></span> <span data-ttu-id="292b9-121">Merhaba tümleştirme belgelerinin tamamı hello bulunabilir [Mobile Engagement Windows Phone SDK tümleştirmesi](mobile-engagement-windows-phone-sdk-overview.md)</span><span class="sxs-lookup"><span data-stu-id="292b9-121">hello complete integration documentation can be found in hello [Mobile Engagement Windows Phone SDK integration](mobile-engagement-windows-phone-sdk-overview.md)</span></span>

<span data-ttu-id="292b9-122">Visual Studio toodemonstrate hello Tümleştirmesi ile temel bir uygulama oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="292b9-122">We will create a basic app with Visual Studio toodemonstrate hello integration.</span></span>

### <a name="create-a-new-windows-phone-silverlight-project"></a><span data-ttu-id="292b9-123">Yeni bir Windows Phone Silverlight projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="292b9-123">Create a new Windows Phone Silverlight project</span></span>
<span data-ttu-id="292b9-124">Visual Studio'nun önceki sürümleri başlangıç adımları benzerdir olsa hello aşağıdaki adımlarda Visual Studio 2015 hello kullanımını varsayılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="292b9-124">hello following steps assume hello use of Visual Studio 2015 though hello steps are similar in earlier versions of Visual Studio.</span></span> 

1. <span data-ttu-id="292b9-125">Visual Studio'yu başlatın ve hello **giriş** ekran, select **yeni proje**.</span><span class="sxs-lookup"><span data-stu-id="292b9-125">Start Visual Studio, and in hello **Home** screen, select **New Project**.</span></span>
2. <span data-ttu-id="292b9-126">Merhaba açılır pencerede seçin **Windows 8** -> **Windows Phone** -> **boş uygulama (Windows Phone Silverlight)**.</span><span class="sxs-lookup"><span data-stu-id="292b9-126">In hello pop-up, select **Windows 8** -> **Windows Phone** -> **Blank App (Windows Phone Silverlight)**.</span></span> <span data-ttu-id="292b9-127">Merhaba doldurup **adı** ve **çözüm adı**ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="292b9-127">Fill in hello app **Name** and **Solution name**, and then click **OK**.</span></span>
   
    ![][1]
3. <span data-ttu-id="292b9-128">Tootarget ya da seçebilirsiniz **Windows Phone 8.0** veya **Windows Phone 8.1**.</span><span class="sxs-lookup"><span data-stu-id="292b9-128">You can choose tootarget either **Windows Phone 8.0** or **Windows Phone 8.1**.</span></span>

<span data-ttu-id="292b9-129">İçine biz hello Azure Mobile Engagement SDK'sı tümleştirecek yeni bir Windows Phone Silverlight uygulaması oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="292b9-129">You have now created a new Windows Phone Silverlight app into which we will integrate hello Azure Mobile Engagement SDK.</span></span>

### <a name="connect-your-app-toohello-mobile-engagement-backend"></a><span data-ttu-id="292b9-130">Uygulamanızın toohello Mobile Engagement arka ucuna bağlanmak</span><span class="sxs-lookup"><span data-stu-id="292b9-130">Connect your app toohello Mobile Engagement backend</span></span>
1. <span data-ttu-id="292b9-131">Merhaba yüklemek [MicrosoftAzure.MobileEngagement] nuget paketini projenize.</span><span class="sxs-lookup"><span data-stu-id="292b9-131">Install hello [MicrosoftAzure.MobileEngagement] nuget package in your project.</span></span>
2. <span data-ttu-id="292b9-132">Açık `WMAppManifest.xml` (Merhaba özellikler klasörünün altında) ve hello aşağıdakilerin bildirildiğinden emin olun (bunları değillerse ekleyin) hello içinde `<Capabilities />` etiketi:</span><span class="sxs-lookup"><span data-stu-id="292b9-132">Open `WMAppManifest.xml` (under hello Properties folder) and make sure hello following are declared (add them if they are not) in hello `<Capabilities />` tag:</span></span>
   
        <Capability Name="ID_CAP_NETWORKING" />
        <Capability Name="ID_CAP_IDENTITY_DEVICE" />
   
    ![][2]
3. <span data-ttu-id="292b9-133">Şimdi daha önce Mobile Engagement uygulamanız için kopyaladığınız hello bağlantı dizesini yapıştırın ve hello Yapıştır `Resources\EngagementConfiguration.xml` hello arasında dosya `<connectionString>` ve `</connectionString>` etiketler:</span><span class="sxs-lookup"><span data-stu-id="292b9-133">Now paste hello connection string that you copied earlier for your Mobile Engagement app and paste it in hello `Resources\EngagementConfiguration.xml` file, between hello `<connectionString>` and `</connectionString>` tags:</span></span>
   
    ![][3]
4. <span data-ttu-id="292b9-134">Merhaba, `App.xaml.cs` dosyası:</span><span class="sxs-lookup"><span data-stu-id="292b9-134">In hello `App.xaml.cs` file:</span></span>
   
    <span data-ttu-id="292b9-135">a.</span><span class="sxs-lookup"><span data-stu-id="292b9-135">a.</span></span> <span data-ttu-id="292b9-136">Merhaba eklemek `using` deyimi:</span><span class="sxs-lookup"><span data-stu-id="292b9-136">Add hello `using` statement:</span></span>
   
            using Microsoft.Azure.Engagement;
   
    <span data-ttu-id="292b9-137">b.</span><span class="sxs-lookup"><span data-stu-id="292b9-137">b.</span></span> <span data-ttu-id="292b9-138">Merhaba Hello SDK başlatma `Application_Launching` yöntemi:</span><span class="sxs-lookup"><span data-stu-id="292b9-138">Initialize hello SDK in hello `Application_Launching` method:</span></span>
   
            private void Application_Launching(object sender, LaunchingEventArgs e)
            {
              EngagementAgent.Instance.Init();
            }
   
    <span data-ttu-id="292b9-139">c.</span><span class="sxs-lookup"><span data-stu-id="292b9-139">c.</span></span> <span data-ttu-id="292b9-140">Merhaba aşağıdaki hello Ekle `Application_Activated`:</span><span class="sxs-lookup"><span data-stu-id="292b9-140">Insert hello following in hello `Application_Activated`:</span></span>
   
            private void Application_Activated(object sender, ActivatedEventArgs e)
            {
               EngagementAgent.Instance.OnActivated(e);
            }

## <span data-ttu-id="292b9-141"><a id="monitor"></a>Gerçek zamanlı izlemeyi etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="292b9-141"><a id="monitor"></a>Enable real-time monitoring</span></span>
<span data-ttu-id="292b9-142">Verileri gönderme ve hello kullanıcıların etkin olduğundan emin olmak sipariş toostart içinde en az bir ekran (etkinlik) toohello Mobile Engagement arka göndermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="292b9-142">In order toostart sending data and ensuring that hello users are active, you must send at least one screen (Activity) toohello Mobile Engagement backend.</span></span>

1. <span data-ttu-id="292b9-143">Hello MainPage.xaml.cs, hello eklemek `using` deyimi:</span><span class="sxs-lookup"><span data-stu-id="292b9-143">In hello MainPage.xaml.cs, add hello `using` statement:</span></span>
   
        using Microsoft.Azure.Engagement;
2. <span data-ttu-id="292b9-144">Merhaba temel sınıfını değiştirme **MainPage**, önce olduğu **mainpage**, ile **EngagementPage**.</span><span class="sxs-lookup"><span data-stu-id="292b9-144">Replace hello base class of **MainPage**, which is before **PhoneApplicationPage**, with **EngagementPage**.</span></span>
   
        class MainPage : EngagementPage 
3. <span data-ttu-id="292b9-145">`MainPage.xml` dosyanızda:</span><span class="sxs-lookup"><span data-stu-id="292b9-145">In your `MainPage.xml` file:</span></span>
   
    <span data-ttu-id="292b9-146">a.</span><span class="sxs-lookup"><span data-stu-id="292b9-146">a.</span></span> <span data-ttu-id="292b9-147">Tooyour ad alanları bildirimleri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="292b9-147">Add tooyour namespaces declarations:</span></span>
   
            xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
   
    <span data-ttu-id="292b9-148">b.</span><span class="sxs-lookup"><span data-stu-id="292b9-148">b.</span></span> <span data-ttu-id="292b9-149">Değiştir `phone:PhoneApplicationPage` hello XML etiket adı ile `engagement:EngagementPage`.</span><span class="sxs-lookup"><span data-stu-id="292b9-149">Replace `phone:PhoneApplicationPage` in hello XML tag name with `engagement:EngagementPage`.</span></span>

## <span data-ttu-id="292b9-150"><a id="monitor"></a>Uygulamayı gerçek zamanlı izlemeyle bağlama</span><span class="sxs-lookup"><span data-stu-id="292b9-150"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="292b9-151"><a id="integrate-push"></a>Anında iletme bildirimlerini ve uygulama içi mesajlaşmayı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="292b9-151"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="292b9-152">Mobile Engagement toointeract sağlar ve anında iletme bildirimleri ve uygulama içi Mesajlaşma Kampanyalar hello bağlamda Kullanıcılarınızla ulaşılırsa.</span><span class="sxs-lookup"><span data-stu-id="292b9-152">Mobile Engagement allows you toointeract and reach your users with Push Notifications and in-app Messaging in hello context of campaigns.</span></span> <span data-ttu-id="292b9-153">Bu modül hello Mobile Engagement portalında REACH adı verilir.</span><span class="sxs-lookup"><span data-stu-id="292b9-153">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="292b9-154">Merhaba aşağıdaki bölümlerde, app tooreceive bunları ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="292b9-154">hello following sections set up your app tooreceive them.</span></span>

### <a name="enable-your-app-tooreceive-mpns-push-notifications"></a><span data-ttu-id="292b9-155">Uygulama tooreceive MPNS anında iletme bildirimlerini etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="292b9-155">Enable your app tooreceive MPNS Push Notifications</span></span>
<span data-ttu-id="292b9-156">Yeni özellikleri tooyour ekleme `WMAppManifest.xml` dosyası:</span><span class="sxs-lookup"><span data-stu-id="292b9-156">Add new Capabilities tooyour `WMAppManifest.xml` file:</span></span>

        ID_CAP_PUSH_NOTIFICATION
        ID_CAP_WEBBROWSERCOMPONENT

   ![][5]

### <a name="initialize-hello-reach-sdk"></a><span data-ttu-id="292b9-157">Merhaba REACH SDK'yı başlatma</span><span class="sxs-lookup"><span data-stu-id="292b9-157">Initialize hello REACH SDK</span></span>
1. <span data-ttu-id="292b9-158">İçinde `App.xaml.cs`, çağrı `EngagementReach.Instance.Init();` hello içinde **Application_Launching** hello aracı başlatmadan hemen sonra işlevi:</span><span class="sxs-lookup"><span data-stu-id="292b9-158">In `App.xaml.cs`, call `EngagementReach.Instance.Init();` in hello **Application_Launching** function, right after hello agent initialization:</span></span>
   
        private void Application_Launching(object sender, LaunchingEventArgs e)
        {
           EngagementAgent.Instance.Init();
           EngagementReach.Instance.Init();
        }
2. <span data-ttu-id="292b9-159">İçinde `App.xaml.cs`, çağrı `EngagementReach.Instance.OnActivated(e);` hello içinde **Application_Activated** hello aracı başlatmadan hemen sonra işlevi:</span><span class="sxs-lookup"><span data-stu-id="292b9-159">In `App.xaml.cs`, call `EngagementReach.Instance.OnActivated(e);` in hello **Application_Activated** function, right after hello agent initialization:</span></span>
   
        private void Application_Activated(object sender, ActivatedEventArgs e)
        {
           EngagementAgent.Instance.OnActivated(e);
           EngagementReach.Instance.OnActivated(e);
        }

<span data-ttu-id="292b9-160">İşinizi tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="292b9-160">You're all set.</span></span> <span data-ttu-id="292b9-161">Şimdi bu temel tümleştirmeyi doğru bir şekilde gerçekleştirdiğinizi onaylayacağız.</span><span class="sxs-lookup"><span data-stu-id="292b9-161">Now we will verify that you have correctly cried out this basic integration.</span></span>

## <span data-ttu-id="292b9-162"><a id="send"></a>Bir bildirim tooyour uygulaması Gönder</span><span class="sxs-lookup"><span data-stu-id="292b9-162"><a id="send"></a>Send a notification tooyour app</span></span>
[!INCLUDE [Create Windows Push campaign](../../includes/mobile-engagement-windows-push-campaign.md)]

<span data-ttu-id="292b9-163">Hello uygulama, aksi takdirde bildirim hello aşağıdaki gibi açıksa şimdi bir bildirim gösterilir, Cihazınızda bir uygulama içi bildirim olarak görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="292b9-163">You should now see a notification on your device which will show up as an in-app notification if hello app is open otherwise as a toast notification like hello following:</span></span> 

![][6]

<!-- URLs. -->
[MicrosoftAzure.MobileEngagement]: http://go.microsoft.com/?linkid=9874664
[Mobile Engagement Windows Phone SDK documentation]: ../mobile-engagement-windows-phone-integrate-engagement/

<!-- Images. -->
[1]: ./media/mobile-engagement-windows-phone-get-started/project-properties.png
[2]: ./media/mobile-engagement-windows-phone-get-started/wmappmanifest-capabilities.png
[3]: ./media/mobile-engagement-windows-phone-get-started/add-connection-string.png
[5]: ./media/mobile-engagement-windows-phone-get-started/reach-capabilities.png
[6]: ./media/mobile-engagement-windows-phone-get-started/push-screenshot.png
