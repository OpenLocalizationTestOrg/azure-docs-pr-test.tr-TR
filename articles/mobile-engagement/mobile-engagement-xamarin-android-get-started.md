---
title: "aaaGet Xamarin.Android için Azure Mobile Engagement ile başlatıldı"
description: "Bilgi nasıl toouse analizi ve Xamarin.Android uygulamaları için anında iletme bildirimleri ile Azure Mobile Engagement."
services: mobile-engagement
documentationcenter: xamarin
author: piyushjo
manager: erikre
editor: 
ms.assetid: fb68cf98-08a2-41b5-8e59-757469de3fe7
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/16/2016
ms.author: piyushjo
ms.openlocfilehash: 9d584fea8e8153d511258cf9b6f87f31dac6aeca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-xamarinandroid-apps"></a><span data-ttu-id="ec6a0-103">Xamarin.Android Uygulamaları için Azure Mobile Engagement kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="ec6a0-103">Get Started with Azure Mobile Engagement for Xamarin.Android Apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="ec6a0-104">Bu konu, nasıl gösterir toouse Azure Mobile Engagement toounderstand, uygulama kullanımınızı ve toosend bir Xamarin.Android uygulamasının bildirimleri toosegmented kullanıcılarına nasıl anında iletme.</span><span class="sxs-lookup"><span data-stu-id="ec6a0-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and how toosend push notifications toosegmented users of a Xamarin.Android application.</span></span>
<span data-ttu-id="ec6a0-105">Bu öğretici, Mobile Engagement kullanarak hello basit yayın senaryosunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="ec6a0-105">This tutorial demonstrates hello simple broadcast scenario using Mobile Engagement.</span></span> <span data-ttu-id="ec6a0-106">Öğreticide, temel bilgiler toplayan ve Google Cloud Messaging (GCM) kullanarak anında iletme bildirimleri gönderen, boş bir Xamarin.Android uygulaması oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="ec6a0-106">In it, you create a blank Xamarin.Android app that collects basic data and receives push notifications using Google Cloud Messaging (GCM).</span></span>

> [!NOTE]
> <span data-ttu-id="ec6a0-107">Hello Azure Mobile Engagement hizmet Mart 2018 kullanımdan kaldırılır ve şu anda yalnızca kullanılabilir tooexisting müşterileri içindir.</span><span class="sxs-lookup"><span data-stu-id="ec6a0-107">hello Azure Mobile Engagement service will be retired March 2018 and is currently only available tooexisting customers.</span></span> <span data-ttu-id="ec6a0-108">Daha fazla bilgi için bkz. [Mobile Engagement nedir?](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span><span class="sxs-lookup"><span data-stu-id="ec6a0-108">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

<span data-ttu-id="ec6a0-109">Bu öğretici hello aşağıdakileri gerektirir:</span><span class="sxs-lookup"><span data-stu-id="ec6a0-109">This tutorial requires hello following:</span></span>

* <span data-ttu-id="ec6a0-110">[Xamarin Studio](http://xamarin.com/studio).</span><span class="sxs-lookup"><span data-stu-id="ec6a0-110">[Xamarin Studio](http://xamarin.com/studio).</span></span> <span data-ttu-id="ec6a0-111">Xamarin ile Visual Studio’yu da kullanabilirsiniz, ancak bu öğretici Xamarin Studio'yu kullanır.</span><span class="sxs-lookup"><span data-stu-id="ec6a0-111">You can also use Visual Studio with Xamarin but this tutorial uses Xamarin Studio.</span></span> <span data-ttu-id="ec6a0-112">Yükleme yönergeleri için bkz. [Visual Studio ve Xamarin için Kurulum ve Yükleme](https://msdn.microsoft.com/library/mt613162.aspx).</span><span class="sxs-lookup"><span data-stu-id="ec6a0-112">For installation instructions, see [Setup and Install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span></span>
* [<span data-ttu-id="ec6a0-113">Mobile Engagement Xamarin SDK</span><span class="sxs-lookup"><span data-stu-id="ec6a0-113">Mobile Engagement Xamarin SDK</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Engagement.Xamarin/)

> [!NOTE]
> <span data-ttu-id="ec6a0-114">toocomplete Bu öğretici, etkin bir Azure hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ec6a0-114">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="ec6a0-115">Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ec6a0-115">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="ec6a0-116">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-android-get-started).</span><span class="sxs-lookup"><span data-stu-id="ec6a0-116">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-android-get-started).</span></span>
> 
> 

## <span data-ttu-id="ec6a0-117"><a id="setup-azme"></a>Android uygulamanız için Mobile Engagement kurma</span><span class="sxs-lookup"><span data-stu-id="ec6a0-117"><a id="setup-azme"></a>Setup Mobile Engagement for your Android app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="ec6a0-118"><a id="connecting-app"></a>Uygulamanızın toohello Mobile Engagement arka ucuna bağlanmak</span><span class="sxs-lookup"><span data-stu-id="ec6a0-118"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="ec6a0-119">Bu öğreticide "Merhaba en az gerekli toocollect veri kümesi ve bir anında iletme bildirimi gönderme bir"temel tümleştirme"gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="ec6a0-119">This tutorial presents a "basic integration", which is hello minimal set required toocollect data and send a push notification.</span></span> 

<span data-ttu-id="ec6a0-120">Xamarin Studio toodemonstrate hello Tümleştirmesi ile temel bir uygulama oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="ec6a0-120">We will create a basic app with Xamarin Studio toodemonstrate hello integration.</span></span>

### <a name="create-a-new-xamarinandroid-project"></a><span data-ttu-id="ec6a0-121">Yeni bir Xamarin.Android projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="ec6a0-121">Create a new Xamarin.Android project</span></span>
1. <span data-ttu-id="ec6a0-122">Başlatma **Xamarin Studio** çok Git**dosya** -> **yeni** -> **çözümü**</span><span class="sxs-lookup"><span data-stu-id="ec6a0-122">Launch **Xamarin Studio** Go too**File** -> **New** -> **Solution**</span></span> 
   
    ![][1]
2. <span data-ttu-id="ec6a0-123">Seçin **Android uygulaması** seçili hello dilin olduğundan emin olun **C#** tıklatıp **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="ec6a0-123">Select **Android App** then make sure hello selected language is **C#** and click **Next**.</span></span>
   
    ![][2]
3. <span data-ttu-id="ec6a0-124">Hello dolgu **App Name** ve hello **kuruluş tanımlayıcı**.</span><span class="sxs-lookup"><span data-stu-id="ec6a0-124">Fill in hello **App Name** and hello **Organization Identifier**.</span></span> <span data-ttu-id="ec6a0-125">Emin toocheckmark olun **Google Play Hizmetleri** ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="ec6a0-125">Make sure toocheckmark **Google Play Services** and then click **Next**.</span></span> 
   
    ![][3]
4. <span data-ttu-id="ec6a0-126">Güncelleştirme hello **proje adı**, **çözüm adı** ve **konumu** gerekli ve tıklatırsanız **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="ec6a0-126">Update hello **Project Name**, **Solution Name** and **Location** if required and click **Create**.</span></span>
   
    ![][4]

<span data-ttu-id="ec6a0-127">Xamarin Studio biz Mobile Engagement tümleştirecek hello uygulaması oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="ec6a0-127">Xamarin Studio will create hello app in which we will integrate Mobile Engagement.</span></span> 

### <a name="connect-your-app-toomobile-engagement-backend"></a><span data-ttu-id="ec6a0-128">Uygulamanızın tooMobile Engagement arka ucuna bağlanmak</span><span class="sxs-lookup"><span data-stu-id="ec6a0-128">Connect your app tooMobile Engagement backend</span></span>
1. <span data-ttu-id="ec6a0-129">Merhaba sağ tıklayın **paketleri** seçip hello çözüm windows klasörü **paketleri Ekle...**</span><span class="sxs-lookup"><span data-stu-id="ec6a0-129">Right click hello **Packages** folder in hello Solution windows and select **Add Packages...**</span></span>
   
    ![][5]
2. <span data-ttu-id="ec6a0-130">Merhaba Ara **Microsoft Azure Mobile Engagement Xamarin SDK** ve tooyour çözüme ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ec6a0-130">Search for hello **Microsoft Azure Mobile Engagement Xamarin SDK** and add it tooyour solution.</span></span>  
   
    ![][6]
3. <span data-ttu-id="ec6a0-131">Açık **MainActivity.cs** ve hello aşağıdaki using deyimlerini:</span><span class="sxs-lookup"><span data-stu-id="ec6a0-131">Open **MainActivity.cs** and add hello following using statements:</span></span>
   
        using Microsoft.Azure.Engagement;
        using Microsoft.Azure.Engagement.Activity;
4. <span data-ttu-id="ec6a0-132">Merhaba, `OnCreate` yöntemi, Mobile Engagement arka ucuyla tooinitialize hello bağlantıyı izleyerek hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ec6a0-132">In hello `OnCreate` method, add hello following tooinitialize hello connection with Mobile Engagement backend.</span></span> <span data-ttu-id="ec6a0-133">Tooadd emin olun, **ConnectionString**.</span><span class="sxs-lookup"><span data-stu-id="ec6a0-133">Make sure tooadd your **ConnectionString**.</span></span> 
   
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.ConnectionString = "YourConnectionStringFromAzurePortal";
        EngagementAgent.Init(engagementConfiguration);

### <a name="add-permissions-and-a-service-declaration"></a><span data-ttu-id="ec6a0-134">İzinler ve bir hizmet bildirimi ekleme</span><span class="sxs-lookup"><span data-stu-id="ec6a0-134">Add permissions and a service declaration</span></span>
1. <span data-ttu-id="ec6a0-135">Merhaba açın **Manifest.xml** dosya hello özellikleri klasörü altında.</span><span class="sxs-lookup"><span data-stu-id="ec6a0-135">Open up hello **Manifest.xml** file under hello Properties folder.</span></span> <span data-ttu-id="ec6a0-136">Kaynak sekmesini seçin, böylece hello XML kaynağını doğrudan güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="ec6a0-136">Select Source tab so that you directly update hello XML source.</span></span>
2. <span data-ttu-id="ec6a0-137">Bu izinleri toohello Manifest.xml ekleyin (Merhaba altında bulunabilir **özellikleri** klasörü) projenizin hemen önce veya sonra hello `<application>` etiketi:</span><span class="sxs-lookup"><span data-stu-id="ec6a0-137">Add these permissions toohello Manifest.xml (which can be found under hello **Properties** folder) of your project immediately before or after hello `<application>` tag:</span></span>
   
        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
        <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
        <uses-permission android:name="android.permission.VIBRATE" />
        <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
3. <span data-ttu-id="ec6a0-138">Merhaba arasında Hello aşağıdakileri ekleyin `<application>` ve `</application>` toodeclare hello Aracısı hizmeti etiketler:</span><span class="sxs-lookup"><span data-stu-id="ec6a0-138">Add hello following between hello `<application>` and `</application>` tags toodeclare hello agent service:</span></span>
   
        <service
             android:name="com.microsoft.azure.engagement.service.EngagementService"
             android:exported="false"
             android:label="<Your application name>"
             android:process=":Engagement"/>
4. <span data-ttu-id="ec6a0-139">Yapıştırdığınız hello kodla `"<Your application name>"` hello etiketi.</span><span class="sxs-lookup"><span data-stu-id="ec6a0-139">In hello code you just pasted, replace `"<Your application name>"` in hello label.</span></span> <span data-ttu-id="ec6a0-140">Bu hello görüntülenir **ayarları** burada kullanıcılar görebilir hello cihazda çalışan hizmetleri menüsü.</span><span class="sxs-lookup"><span data-stu-id="ec6a0-140">This is displayed in hello **Settings** menu where users can see services running on hello device.</span></span> <span data-ttu-id="ec6a0-141">Örneğin bu etikete "Hizmet" Merhaba sözcüğünü ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ec6a0-141">You can add hello word "Service" in that label for example.</span></span>

### <a name="send-a-screen-toomobile-engagement"></a><span data-ttu-id="ec6a0-142">Ekran tooMobile katılım Gönder</span><span class="sxs-lookup"><span data-stu-id="ec6a0-142">Send a screen tooMobile Engagement</span></span>
<span data-ttu-id="ec6a0-143">Verileri gönderme ve hello kullanıcıların etkin olduğundan emin olmak sipariş toostart içinde en az bir ekran toohello Mobile Engagement arka göndermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ec6a0-143">In order toostart sending data and ensuring hello users are active, you must send at least one screen toohello Mobile Engagement backend.</span></span> <span data-ttu-id="ec6a0-144">Bunu yapmak için-o hello olun `MainActivity` devraldığı `EngagementActivity` yerine `Activity`.</span><span class="sxs-lookup"><span data-stu-id="ec6a0-144">For doing this - ensure that hello `MainActivity` inherits from `EngagementActivity` instead of `Activity`.</span></span>

    public class MainActivity : EngagementActivity

<span data-ttu-id="ec6a0-145">Alternatif olarak, `EngagementActivity` konumundan devralamıyorsanız `.StartActivity` ve `.EndActivity` yöntemlerini sırasıyla `OnResume` ve `OnPause` içine eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ec6a0-145">Alternatively, if you cannot inherit from `EngagementActivity` then you must add `.StartActivity` and `.EndActivity` methods in `OnResume` and `OnPause` respectively.</span></span>  

        protected override void OnResume()
            {
                EngagementAgent.StartActivity(EngagementAgentUtils.BuildEngagementActivityName(Java.Lang.Class.FromType(this.GetType())), null);
                base.OnResume();             
            }

            protected override void OnPause()
            {
                EngagementAgent.EndActivity();
                base.OnPause();            
            }

## <span data-ttu-id="ec6a0-146"><a id="monitor"></a>Uygulamayı gerçek zamanlı izlemeyle bağlama</span><span class="sxs-lookup"><span data-stu-id="ec6a0-146"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="ec6a0-147"><a id="integrate-push"></a>Anında iletme bildirimlerini ve uygulama içi mesajlaşmayı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="ec6a0-147"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="ec6a0-148">Mobile Engagement ile toointeract sağlar ve kullanıcılarınızın anında iletme bildirimleri ve uygulama içi Mesajlaşma hello Kampanyalar bağlamında ULAŞILIRSA.</span><span class="sxs-lookup"><span data-stu-id="ec6a0-148">Mobile Engagement allows you toointeract with and REACH your users with push notifications and in-app messaging in hello context of campaigns.</span></span> <span data-ttu-id="ec6a0-149">Bu modül hello Mobile Engagement portalında REACH adı verilir.</span><span class="sxs-lookup"><span data-stu-id="ec6a0-149">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="ec6a0-150">Aşağıdaki bölümlerde Merhaba, uygulama tooreceive bunları ayarlar.</span><span class="sxs-lookup"><span data-stu-id="ec6a0-150">hello following sections sets up your app tooreceive them.</span></span>

[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

[!INCLUDE [Enable in-app messaging](../../includes/mobile-engagement-android-send-push.md)]

[!INCLUDE [Send notification from portal](../../includes/mobile-engagement-android-send-push-from-portal.md)]

<!-- Images -->
[1]: ./media/mobile-engagement-xamarin-android-get-started/1.png
[2]: ./media/mobile-engagement-xamarin-android-get-started/2.png
[3]: ./media/mobile-engagement-xamarin-android-get-started/3.png
[4]: ./media/mobile-engagement-xamarin-android-get-started/4.png
[5]: ./media/mobile-engagement-xamarin-android-get-started/5.png
[6]: ./media/mobile-engagement-xamarin-android-get-started/6.png
