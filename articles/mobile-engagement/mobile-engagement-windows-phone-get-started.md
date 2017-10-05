---
title: "Windows Phone Silverlight uygulamaları için Azure Mobile Engagement kullanmaya başlama"
description: "Windows Phone Silverlight uygulamaları için analizler ve anında iletme bildirimleri ile Azure Mobile Engagement kullanmayı öğrenin."
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
ms.openlocfilehash: d2334a59d83c90bdd02c4fa29261d36aad292892
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-windows-phone-silverlight-apps"></a><span data-ttu-id="99349-103">Windows Phone Silverlight uygulamaları için Azure Mobile Engagement kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="99349-103">Get started with Azure Mobile Engagement for Windows Phone Silverlight apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="99349-104">Bu konuda, uygulama kullanımınızı anlamak ve bir Windows Phone Silverlight uygulamasının segmentli kullanıcılarına anında iletme bildirimleri göndermek için nasıl Azure Mobile Engagement kullanılacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="99349-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and send push notifications to segmented users of a Windows Phone Silverlight application.</span></span>
<span data-ttu-id="99349-105">Bu öğretici, Mobile Engagement kullanarak basit bir yayın senaryosunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="99349-105">This tutorial demonstrates the simple broadcast scenario using Mobile Engagement.</span></span> <span data-ttu-id="99349-106">Temel verileri toplayan ve Microsoft Anında İletme Bildirimi Hizmeti’ni (MPNS) kullanarak anında iletme bildirimleri alan boş bir Windows Phone Silverlight uygulaması oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="99349-106">In it, you create a blank Windows Phone Silverlight app that collects basic data and receives push notifications using Microsoft Push Notification Service (MPNS).</span></span>

> [!NOTE]
> <span data-ttu-id="99349-107">Azure Mobile Engagement hizmeti, Mart 2018’de devre dışı bırakılacaktır. Şu anda yalnızca mevcut müşteriler tarafından kullanılabilmektedir.</span><span class="sxs-lookup"><span data-stu-id="99349-107">The Azure Mobile Engagement service will be retired March 2018 and is currently only available to existing customers.</span></span> <span data-ttu-id="99349-108">Daha fazla bilgi için bkz. [Mobile Engagement nedir?](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span><span class="sxs-lookup"><span data-stu-id="99349-108">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

> [!NOTE]
> <span data-ttu-id="99349-109">Windows Phone 8.1 ve önceki sürümlerde oluşturulmuş projeler Visual Studio 2017’de desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="99349-109">Windows Phone 8.1 and prior version projects are not supported in Visual Studio 2017.</span></span>  <span data-ttu-id="99349-110">Daha fazla bilgi için bkz. [Visual Studio 2017 Platform Desteği ve Uyumluluk](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span><span class="sxs-lookup"><span data-stu-id="99349-110">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span>

> [!NOTE]
> <span data-ttu-id="99349-111">Windows Phone 8.1'i (Silverlight olmayan) hedefliyorsanız [Windows Evrensel öğreticisine](mobile-engagement-windows-store-dotnet-get-started.md) bakın.</span><span class="sxs-lookup"><span data-stu-id="99349-111">If you are targeting Windows Phone 8.1 (non-Silverlight), refer to the [Windows Universal tutorial](mobile-engagement-windows-store-dotnet-get-started.md).</span></span>
> 
> 

<span data-ttu-id="99349-112">Bu öğretici için aşağıdakiler gereklidir:</span><span class="sxs-lookup"><span data-stu-id="99349-112">This tutorial requires the following:</span></span>

* <span data-ttu-id="99349-113">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="99349-113">Visual Studio 2013</span></span>
* <span data-ttu-id="99349-114">[MicrosoftAzure.MobileEngagement] Nuget paketi</span><span class="sxs-lookup"><span data-stu-id="99349-114">[MicrosoftAzure.MobileEngagement] Nuget package</span></span>

> [!NOTE]
> <span data-ttu-id="99349-115">Bu öğreticiyi tamamlamak için etkin bir Azure hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="99349-115">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="99349-116">Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="99349-116">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="99349-117">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-windows-phone-get-started).</span><span class="sxs-lookup"><span data-stu-id="99349-117">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-windows-phone-get-started).</span></span>
> 
> 

## <span data-ttu-id="99349-118"><a id="setup-azme"></a>Windows Phone uygulamanıza Mobile Engagement’i kurma</span><span class="sxs-lookup"><span data-stu-id="99349-118"><a id="setup-azme"></a>Setup Mobile Engagement for your Windows Phone app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="99349-119"><a id="connecting-app"></a>Uygulamanızı Mobile Engagement arka ucuna bağlama</span><span class="sxs-lookup"><span data-stu-id="99349-119"><a id="connecting-app"></a>Connect your app to the Mobile Engagement backend</span></span>
<span data-ttu-id="99349-120">Bu öğreticide, veri toplamak ve anında iletme bildirimi göndermek için gerekli en küçük grup olan bir "temel tümleştirme" gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="99349-120">This tutorial presents a "basic integration", which is the minimal set required to collect data and send a push notification.</span></span> <span data-ttu-id="99349-121">Tümleştirme belgelerinin tamamı [Mobile Engagement Windows Phone SDK tümleştirmesi](mobile-engagement-windows-phone-sdk-overview.md) makalesinde bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="99349-121">The complete integration documentation can be found in the [Mobile Engagement Windows Phone SDK integration](mobile-engagement-windows-phone-sdk-overview.md)</span></span>

<span data-ttu-id="99349-122">Tümleştirmeyi göstermek için Visual Studio ile temel bir uygulama oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="99349-122">We will create a basic app with Visual Studio to demonstrate the integration.</span></span>

### <a name="create-a-new-windows-phone-silverlight-project"></a><span data-ttu-id="99349-123">Yeni bir Windows Phone Silverlight projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="99349-123">Create a new Windows Phone Silverlight project</span></span>
<span data-ttu-id="99349-124">Aşağıdaki adımlarda Visual Studio 2015 kullanıldığı varsayılmaktadır ancak Visual Studio'nun önceki sürümleri için de benzer adımlar izlenir.</span><span class="sxs-lookup"><span data-stu-id="99349-124">The following steps assume the use of Visual Studio 2015 though the steps are similar in earlier versions of Visual Studio.</span></span> 

1. <span data-ttu-id="99349-125">Visual Studio'yu başlatın ve **Giriş** ekranında **Yeni Proje**’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="99349-125">Start Visual Studio, and in the **Home** screen, select **New Project**.</span></span>
2. <span data-ttu-id="99349-126">Açılır pencerede **Windows 8** -> **Windows Phone** -> **Boş Uygulama (Windows Phone Silverlight)**’yı seçin.</span><span class="sxs-lookup"><span data-stu-id="99349-126">In the pop-up, select **Windows 8** -> **Windows Phone** -> **Blank App (Windows Phone Silverlight)**.</span></span> <span data-ttu-id="99349-127">**Ad** ve **Çözüm adı** alanlarını doldurup **Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="99349-127">Fill in the app **Name** and **Solution name**, and then click **OK**.</span></span>
   
    ![][1]
3. <span data-ttu-id="99349-128">Hedeflemek için **Windows Phone 8.0** veya **Windows Phone 8.1**’i seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="99349-128">You can choose to target either **Windows Phone 8.0** or **Windows Phone 8.1**.</span></span>

<span data-ttu-id="99349-129">Azure Mobile Engagement SDK’sını tümleştireceğimiz yeni bir Windows Phone Silverlight uygulaması oluşturmuş oldunuz.</span><span class="sxs-lookup"><span data-stu-id="99349-129">You have now created a new Windows Phone Silverlight app into which we will integrate the Azure Mobile Engagement SDK.</span></span>

### <a name="connect-your-app-to-the-mobile-engagement-backend"></a><span data-ttu-id="99349-130">Uygulamanızı Mobile Engagement arka ucuna bağlama</span><span class="sxs-lookup"><span data-stu-id="99349-130">Connect your app to the Mobile Engagement backend</span></span>
1. <span data-ttu-id="99349-131">[MicrosoftAzure.MobileEngagement] nuget paketini projenize yükleyin.</span><span class="sxs-lookup"><span data-stu-id="99349-131">Install the [MicrosoftAzure.MobileEngagement] nuget package in your project.</span></span>
2. <span data-ttu-id="99349-132">`WMAppManifest.xml` dosyasını (Özellikler klasörünün altındadır) açıp `<Capabilities />` etiketinde aşağıdakilerin bildirildiğinden emin olun (bildirilmemişlerse bunları ekleyin):</span><span class="sxs-lookup"><span data-stu-id="99349-132">Open `WMAppManifest.xml` (under the Properties folder) and make sure the following are declared (add them if they are not) in the `<Capabilities />` tag:</span></span>
   
        <Capability Name="ID_CAP_NETWORKING" />
        <Capability Name="ID_CAP_IDENTITY_DEVICE" />
   
    ![][2]
3. <span data-ttu-id="99349-133">Daha önce Mobile Engagement uygulamanız için kopyaladığınız bağlantı dizesini kopyalayın ve bu dizeyi `Resources\EngagementConfiguration.xml` dosyasında `<connectionString>` ve `</connectionString>` etiketlerinin arasına yapıştırın:</span><span class="sxs-lookup"><span data-stu-id="99349-133">Now paste the connection string that you copied earlier for your Mobile Engagement app and paste it in the `Resources\EngagementConfiguration.xml` file, between the `<connectionString>` and `</connectionString>` tags:</span></span>
   
    ![][3]
4. <span data-ttu-id="99349-134">`App.xaml.cs` dosyasında:</span><span class="sxs-lookup"><span data-stu-id="99349-134">In the `App.xaml.cs` file:</span></span>
   
    <span data-ttu-id="99349-135">a.</span><span class="sxs-lookup"><span data-stu-id="99349-135">a.</span></span> <span data-ttu-id="99349-136">`using` deyimini ekleyin:</span><span class="sxs-lookup"><span data-stu-id="99349-136">Add the `using` statement:</span></span>
   
            using Microsoft.Azure.Engagement;
   
    <span data-ttu-id="99349-137">b.</span><span class="sxs-lookup"><span data-stu-id="99349-137">b.</span></span> <span data-ttu-id="99349-138">`Application_Launching` yönteminde SDK’yı başlatın:</span><span class="sxs-lookup"><span data-stu-id="99349-138">Initialize the SDK in the `Application_Launching` method:</span></span>
   
            private void Application_Launching(object sender, LaunchingEventArgs e)
            {
              EngagementAgent.Instance.Init();
            }
   
    <span data-ttu-id="99349-139">c.</span><span class="sxs-lookup"><span data-stu-id="99349-139">c.</span></span> <span data-ttu-id="99349-140">`Application_Activated` bölümüne aşağıdakileri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="99349-140">Insert the following in the `Application_Activated`:</span></span>
   
            private void Application_Activated(object sender, ActivatedEventArgs e)
            {
               EngagementAgent.Instance.OnActivated(e);
            }

## <span data-ttu-id="99349-141"><a id="monitor"></a>Gerçek zamanlı izlemeyi etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="99349-141"><a id="monitor"></a>Enable real-time monitoring</span></span>
<span data-ttu-id="99349-142">Veri göndermeye başlamak ve kullanıcıların etkin olduğundan emin olmak için, Mobile Engagement arka ucuna en az bir ekran (Etkinlik) göndermelisiniz.</span><span class="sxs-lookup"><span data-stu-id="99349-142">In order to start sending data and ensuring that the users are active, you must send at least one screen (Activity) to the Mobile Engagement backend.</span></span>

1. <span data-ttu-id="99349-143">MainPage.xaml.cs dosyasında, `using` deyimini ekleyin:</span><span class="sxs-lookup"><span data-stu-id="99349-143">In the MainPage.xaml.cs, add the `using` statement:</span></span>
   
        using Microsoft.Azure.Engagement;
2. <span data-ttu-id="99349-144">**PhoneApplicationPage** olan **MainPage** temel sınıfını **EngagementPage** olarak değiştirin.</span><span class="sxs-lookup"><span data-stu-id="99349-144">Replace the base class of **MainPage**, which is before **PhoneApplicationPage**, with **EngagementPage**.</span></span>
   
        class MainPage : EngagementPage 
3. <span data-ttu-id="99349-145">`MainPage.xml` dosyanızda:</span><span class="sxs-lookup"><span data-stu-id="99349-145">In your `MainPage.xml` file:</span></span>
   
    <span data-ttu-id="99349-146">a.</span><span class="sxs-lookup"><span data-stu-id="99349-146">a.</span></span> <span data-ttu-id="99349-147">Ad alanı bildirimlerinize aşağıdakini ekleyin:</span><span class="sxs-lookup"><span data-stu-id="99349-147">Add to your namespaces declarations:</span></span>
   
            xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
   
    <span data-ttu-id="99349-148">b.</span><span class="sxs-lookup"><span data-stu-id="99349-148">b.</span></span> <span data-ttu-id="99349-149">XML etiket adında `phone:PhoneApplicationPage` yerine `engagement:EngagementPage` koyun.</span><span class="sxs-lookup"><span data-stu-id="99349-149">Replace `phone:PhoneApplicationPage` in the XML tag name with `engagement:EngagementPage`.</span></span>

## <span data-ttu-id="99349-150"><a id="monitor"></a>Uygulamayı gerçek zamanlı izlemeyle bağlama</span><span class="sxs-lookup"><span data-stu-id="99349-150"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="99349-151"><a id="integrate-push"></a>Anında iletme bildirimlerini ve uygulama içi mesajlaşmayı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="99349-151"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="99349-152">Mobile Engagement, kampanyalar bağlamında Anında İletme Bildirimleri ve uygulama içi Mesajlaşma aracılığıyla kullanıcılarınız ile etkileşim kurmanızı ve onlara erişmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="99349-152">Mobile Engagement allows you to interact and reach your users with Push Notifications and in-app Messaging in the context of campaigns.</span></span> <span data-ttu-id="99349-153">Mobile Engagement portalında bu modüle REACH adı verilir.</span><span class="sxs-lookup"><span data-stu-id="99349-153">This module is called REACH in the Mobile Engagement portal.</span></span>
<span data-ttu-id="99349-154">Aşağıdaki bölümler bunları almak için uygulamanızı ayarlar.</span><span class="sxs-lookup"><span data-stu-id="99349-154">The following sections set up your app to receive them.</span></span>

### <a name="enable-your-app-to-receive-mpns-push-notifications"></a><span data-ttu-id="99349-155">MPNS Anında İletme Bildirimlerini almak üzere uygulamanızı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="99349-155">Enable your app to receive MPNS Push Notifications</span></span>
<span data-ttu-id="99349-156">`WMAppManifest.xml` dosyanıza yeni Capabilities (Özellikler) ekleyin:</span><span class="sxs-lookup"><span data-stu-id="99349-156">Add new Capabilities to your `WMAppManifest.xml` file:</span></span>

        ID_CAP_PUSH_NOTIFICATION
        ID_CAP_WEBBROWSERCOMPONENT

   ![][5]

### <a name="initialize-the-reach-sdk"></a><span data-ttu-id="99349-157">REACH SDK'sını başlatma</span><span class="sxs-lookup"><span data-stu-id="99349-157">Initialize the REACH SDK</span></span>
1. <span data-ttu-id="99349-158">`App.xaml.cs` dosyasındaki **Application_Launching** işlevinde, aracı başlatmadan hemen sonra `EngagementReach.Instance.Init();` öğesini çağırın:</span><span class="sxs-lookup"><span data-stu-id="99349-158">In `App.xaml.cs`, call `EngagementReach.Instance.Init();` in the **Application_Launching** function, right after the agent initialization:</span></span>
   
        private void Application_Launching(object sender, LaunchingEventArgs e)
        {
           EngagementAgent.Instance.Init();
           EngagementReach.Instance.Init();
        }
2. <span data-ttu-id="99349-159">`App.xaml.cs` dosyasındaki **Application_Activated** işlevinde, aracı başlatmadan hemen sonra `EngagementReach.Instance.OnActivated(e);` öğesini çağırın:</span><span class="sxs-lookup"><span data-stu-id="99349-159">In `App.xaml.cs`, call `EngagementReach.Instance.OnActivated(e);` in the **Application_Activated** function, right after the agent initialization:</span></span>
   
        private void Application_Activated(object sender, ActivatedEventArgs e)
        {
           EngagementAgent.Instance.OnActivated(e);
           EngagementReach.Instance.OnActivated(e);
        }

<span data-ttu-id="99349-160">İşinizi tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="99349-160">You're all set.</span></span> <span data-ttu-id="99349-161">Şimdi bu temel tümleştirmeyi doğru bir şekilde gerçekleştirdiğinizi onaylayacağız.</span><span class="sxs-lookup"><span data-stu-id="99349-161">Now we will verify that you have correctly cried out this basic integration.</span></span>

## <span data-ttu-id="99349-162"><a id="send"></a>Uygulamanıza bildirim gönderme</span><span class="sxs-lookup"><span data-stu-id="99349-162"><a id="send"></a>Send a notification to your app</span></span>
[!INCLUDE [Create Windows Push campaign](../../includes/mobile-engagement-windows-push-campaign.md)]

<span data-ttu-id="99349-163">Şimdi cihazınızda, uygulama açıksa bir uygulama içi bildirim, aksi takdirde aşağıdaki gibi bir bildirim görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="99349-163">You should now see a notification on your device which will show up as an in-app notification if the app is open otherwise as a toast notification like the following:</span></span> 

![][6]

<!-- URLs. -->
<span data-ttu-id="99349-164">[MicrosoftAzure.MobileEngagement]: http://go.microsoft.com/?linkid=9874664</span><span class="sxs-lookup"><span data-stu-id="99349-164">[MicrosoftAzure.MobileEngagement]: http://go.microsoft.com/?linkid=9874664</span></span>
[Mobile Engagement Windows Phone SDK documentation]: ../mobile-engagement-windows-phone-integrate-engagement/

<!-- Images. -->
[1]: ./media/mobile-engagement-windows-phone-get-started/project-properties.png
[2]: ./media/mobile-engagement-windows-phone-get-started/wmappmanifest-capabilities.png
[3]: ./media/mobile-engagement-windows-phone-get-started/add-connection-string.png
[5]: ./media/mobile-engagement-windows-phone-get-started/reach-capabilities.png
[6]: ./media/mobile-engagement-windows-phone-get-started/push-screenshot.png
