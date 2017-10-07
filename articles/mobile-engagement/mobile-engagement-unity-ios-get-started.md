---
title: "Unity iOS dağıtımı için aaaGet Azure Mobile Engagement ile başlatıldı"
description: "Bilgi nasıl tooiOS aygıtları dağıtma Unity uygulamaları için analizler ve anında iletme bildirimleri ile Azure Mobile Engagement toouse."
services: mobile-engagement
documentationcenter: unity
author: piyushjo
manager: erikre
editor: 
ms.assetid: 7ddfbac3-8d13-4ebe-b061-c865f357297f
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-unity-ios
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: f4247b0a9240cbe2bf1a6618388919d3554c07fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-unity-ios-deployment"></a><span data-ttu-id="0f5a6-103">Unity iOS dağıtımı için Azure Mobile Engagement kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="0f5a6-103">Get Started with Azure Mobile Engagement for Unity iOS deployment</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="0f5a6-104">Bu konu, nasıl gösterir toouse Azure Mobile Engagement toounderstand, uygulama kullanımınızı ve nasıl toosend anında iletme bildirimleri toosegmented kullanıcılar bir Unity uygulamasının tooan iOS cihazına dağıtırken.</span><span class="sxs-lookup"><span data-stu-id="0f5a6-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and how toosend push notifications toosegmented users of a Unity application when deploying tooan iOS device.</span></span>
<span data-ttu-id="0f5a6-105">Bu öğretici kullanır Klasik Unity Roll bir küre öğretici hello başlangıç noktası hello.</span><span class="sxs-lookup"><span data-stu-id="0f5a6-105">This tutorial uses hello classic Unity Roll a Ball tutorial as hello starting point.</span></span> <span data-ttu-id="0f5a6-106">Bu başlangıç adımları izlemelisiniz [öğretici](mobile-engagement-unity-roll-a-ball.md) hello hello aşağıdaki öğreticide gösterdiğimiz Mobile Engagement tümleştirmesi işlemine devam etmeden önce.</span><span class="sxs-lookup"><span data-stu-id="0f5a6-106">You should follow hello steps in this [tutorial](mobile-engagement-unity-roll-a-ball.md) before proceeding with hello Mobile Engagement integration we showcase in hello tutorial below.</span></span> 

<span data-ttu-id="0f5a6-107">Bu öğretici hello aşağıdakileri gerektirir:</span><span class="sxs-lookup"><span data-stu-id="0f5a6-107">This tutorial requires hello following:</span></span>

* [<span data-ttu-id="0f5a6-108">Unity Düzenleyicisi</span><span class="sxs-lookup"><span data-stu-id="0f5a6-108">Unity Editor</span></span>](http://unity3d.com/get-unity)
* [<span data-ttu-id="0f5a6-109">Mobile Engagement Unity SDK</span><span class="sxs-lookup"><span data-stu-id="0f5a6-109">Mobile Engagement Unity SDK</span></span>](https://aka.ms/azmeunitysdk)
* <span data-ttu-id="0f5a6-110">XCode Düzenleyicisi</span><span class="sxs-lookup"><span data-stu-id="0f5a6-110">XCode Editor</span></span>

> [!NOTE]
> <span data-ttu-id="0f5a6-111">toocomplete Bu öğretici, etkin bir Azure hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="0f5a6-111">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="0f5a6-112">Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0f5a6-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="0f5a6-113">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-ios-get-started).</span><span class="sxs-lookup"><span data-stu-id="0f5a6-113">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-ios-get-started).</span></span>
> 
> 

## <span data-ttu-id="0f5a6-114"><a id="setup-azme"></a>iOS uygulamanız için Mobile Engagement kurma</span><span class="sxs-lookup"><span data-stu-id="0f5a6-114"><a id="setup-azme"></a>Setup Mobile Engagement for your iOS app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="0f5a6-115"><a id="connecting-app"></a>Uygulamanızın toohello Mobile Engagement arka ucuna bağlanmak</span><span class="sxs-lookup"><span data-stu-id="0f5a6-115"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
### <a name="import-hello-unity-package"></a><span data-ttu-id="0f5a6-116">Merhaba Unity paketini içeri aktarma</span><span class="sxs-lookup"><span data-stu-id="0f5a6-116">Import hello Unity package</span></span>
1. <span data-ttu-id="0f5a6-117">Merhaba karşıdan [Mobile Engagement Unity paketini](https://aka.ms/azmeunitysdk) ve tooyour yerel makine kaydedin.</span><span class="sxs-lookup"><span data-stu-id="0f5a6-117">Download hello [Mobile Engagement Unity package](https://aka.ms/azmeunitysdk) and save it tooyour local machine.</span></span> 
2. <span data-ttu-id="0f5a6-118">Çok Git**varlıklar -> paketi İçeri Aktar -> özel paket** ve indirilen Yukarıdaki adımı hello içindeki select hello paketi.</span><span class="sxs-lookup"><span data-stu-id="0f5a6-118">Go too**Assets -> Import Package -> Custom Package** and select hello package you downloaded in hello above step.</span></span> 
   
    ![][70] 
3. <span data-ttu-id="0f5a6-119">Tüm dosyaların seçildiğinden emin olun ve **İçeri Aktar** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0f5a6-119">Make sure all files are selected and click **Import** button.</span></span> 
   
    ![][71] 
4. <span data-ttu-id="0f5a6-120">İçeri aktarma başarılı olduktan sonra hello içeri aktarılan SDK dosyalarını projenizde görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="0f5a6-120">Once Import is successful, you will see hello imported SDK files in your project.</span></span>  
   
    ![][72] 

### <a name="update-hello-engagementconfiguration"></a><span data-ttu-id="0f5a6-121">Merhaba EngagementConfiguration güncelleştir</span><span class="sxs-lookup"><span data-stu-id="0f5a6-121">Update hello EngagementConfiguration</span></span>
1. <span data-ttu-id="0f5a6-122">Merhaba açın **EngagementConfiguration** hello SDK klasörü ve güncelleştirme hello betik dosyasından **IOS\_bağlantı\_dize** daha önce aldığınız hello bağlantı dizesiyle Azure portal Hello.</span><span class="sxs-lookup"><span data-stu-id="0f5a6-122">Open up hello **EngagementConfiguration** script file from hello SDK folder and update hello **IOS\_CONNECTION\_STRING** with hello connection string you obtained earlier from hello Azure portal.</span></span>  
   
    ![][73]
2. <span data-ttu-id="0f5a6-123">Merhaba dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="0f5a6-123">Save hello file.</span></span> 

### <a name="configure-hello-app-for-basic-tracking"></a><span data-ttu-id="0f5a6-124">Merhaba uygulamayı temel izleme için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="0f5a6-124">Configure hello app for basic tracking</span></span>
1. <span data-ttu-id="0f5a6-125">Merhaba açın **PlayerController** iliştirilmiş düzenlemek için Player nesnesine toohello komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="0f5a6-125">Open up hello **PlayerController** script attached toohello Player object for editing.</span></span> 
2. <span data-ttu-id="0f5a6-126">Merhaba aşağıdaki ekleme deyimini kullanarak:</span><span class="sxs-lookup"><span data-stu-id="0f5a6-126">Add hello following using statement:</span></span>
   
        using Microsoft.Azure.Engagement.Unity;
3. <span data-ttu-id="0f5a6-127">Toohello aşağıdaki hello eklemek `Start()` yöntemi</span><span class="sxs-lookup"><span data-stu-id="0f5a6-127">Add hello following toohello `Start()` method</span></span>
   
        EngagementAgent.Initialize();
        EngagementAgent.StartActivity("Home");

### <a name="deploy-and-run-hello-app"></a><span data-ttu-id="0f5a6-128">Dağıtma ve hello uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="0f5a6-128">Deploy and run hello app</span></span>
1. <span data-ttu-id="0f5a6-129">Bir iOS aygıtı tooyour makineyi bağlayın.</span><span class="sxs-lookup"><span data-stu-id="0f5a6-129">Connect an iOS device tooyour machine.</span></span> 
2. <span data-ttu-id="0f5a6-130">**Dosya -> Yapı Ayarları**’nı açın</span><span class="sxs-lookup"><span data-stu-id="0f5a6-130">Open up **File -> Build Settings**</span></span> 
   
    ![][40]
3. <span data-ttu-id="0f5a6-131">**iOS**’u seçin ve ardından **Anahtar Platformu**’na tıklayın</span><span class="sxs-lookup"><span data-stu-id="0f5a6-131">Select **iOS** and then click on **Switch Platform**</span></span>
   
    ![][41]
   
    ![][42]
4. <span data-ttu-id="0f5a6-132">**Player ayarları**’na tıklayın ve geçerli bir Paket Tanımlayıcısı girin.</span><span class="sxs-lookup"><span data-stu-id="0f5a6-132">Click on **Player settings** and provide a valid Bundle Identifier.</span></span> 
   
    ![][53]
5. <span data-ttu-id="0f5a6-133">Son olarak, **Derle ve Çalıştır**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0f5a6-133">Finally click on **Build And Run**</span></span>
   
    ![][54]
6. <span data-ttu-id="0f5a6-134">Olabilir bir klasör adı toostore hello iOS paketini tooprovide istedi.</span><span class="sxs-lookup"><span data-stu-id="0f5a6-134">You may be asked tooprovide a folder name toostore hello iOS package.</span></span> 
   
    ![][43]
7. <span data-ttu-id="0f5a6-135">Her şey yolunda giderse, hello Proje derlenir ve XCode uygulamanızda açmanız.</span><span class="sxs-lookup"><span data-stu-id="0f5a6-135">If everything goes fine, then hello project will be compiled and you should open it up on your XCode application.</span></span> 
8. <span data-ttu-id="0f5a6-136">Bu hello emin olun **paket tanımlayıcı** hello projede doğru olduğundan.</span><span class="sxs-lookup"><span data-stu-id="0f5a6-136">Make sure that hello **Bundle identifier** is correct in hello project.</span></span>  
   
    ![][75]
9. <span data-ttu-id="0f5a6-137">Şimdi hello uygulama hello paketi dağıtılan tooyour bağlı cihaz ve telefonunuzda Unity oyununuzu görmelisiniz böylece Xcode'da çalıştırın!</span><span class="sxs-lookup"><span data-stu-id="0f5a6-137">Now run hello app in XCode so that hello package is deployed tooyour connected device and you should see your Unity game on your phone!</span></span> 

## <span data-ttu-id="0f5a6-138"><a id="monitor"></a>Uygulamayı gerçek zamanlı izlemeyle bağlama</span><span class="sxs-lookup"><span data-stu-id="0f5a6-138"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="0f5a6-139"><a id="integrate-push"></a>Anında iletme bildirimlerini ve uygulama içi mesajlaşmayı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="0f5a6-139"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="0f5a6-140">Mobile Engagement anında iletme bildirimleri ve uygulama içi Mesajlaşma hello Kampanyalar bağlamında toointeract kullanıcılarınız ve REACH sağlar.</span><span class="sxs-lookup"><span data-stu-id="0f5a6-140">Mobile Engagement allows you toointeract with your users and REACH with push notifications and in-app messaging in hello context of campaigns.</span></span> <span data-ttu-id="0f5a6-141">Bu modül hello Mobile Engagement portalında REACH adı verilir.</span><span class="sxs-lookup"><span data-stu-id="0f5a6-141">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="0f5a6-142">Toodo uygulama tooreceive bildirimlerinizi herhangi bir ek yapılandırma yoktur ve onu zaten ayarlıdır.</span><span class="sxs-lookup"><span data-stu-id="0f5a6-142">You don't have toodo any additional configuration in your app tooreceive notifications and it is already setup for it.</span></span>

[!INCLUDE [mobile-engagement-ios-send-push-push](../../includes/mobile-engagement-ios-send-push.md)]

<!-- Images. -->
[40]: ./media/mobile-engagement-unity-ios-get-started/40.png
[41]: ./media/mobile-engagement-unity-ios-get-started/41.png
[42]: ./media/mobile-engagement-unity-ios-get-started/42.png
[43]: ./media/mobile-engagement-unity-ios-get-started/43.png
[53]: ./media/mobile-engagement-unity-ios-get-started/53.png
[54]: ./media/mobile-engagement-unity-ios-get-started/54.png
[70]: ./media/mobile-engagement-unity-ios-get-started/70.png
[71]: ./media/mobile-engagement-unity-ios-get-started/71.png
[72]: ./media/mobile-engagement-unity-ios-get-started/72.png
[73]: ./media/mobile-engagement-unity-ios-get-started/73.png
[74]: ./media/mobile-engagement-unity-ios-get-started/74.png
[75]: ./media/mobile-engagement-unity-ios-get-started/75.png
