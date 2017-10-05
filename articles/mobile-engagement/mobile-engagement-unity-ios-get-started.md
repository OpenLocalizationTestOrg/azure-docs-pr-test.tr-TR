---
title: "Unity iOS dağıtımı için Azure Mobile Engagement kullanmaya başlama"
description: "Unity uygulamalarını iOS cihazlarına dağıtmak için Analizler ve Anında İletme Bildirimleri ile Azure Mobile Engagement kullanmayı öğrenin."
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
ms.openlocfilehash: c8f50404771965ec636065346ac04e059d264c3d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-unity-ios-deployment"></a><span data-ttu-id="45034-103">Unity iOS dağıtımı için Azure Mobile Engagement kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="45034-103">Get Started with Azure Mobile Engagement for Unity iOS deployment</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="45034-104">Bu konu size uygulama kullanımınızı anlamak için Azure Mobile Engagement kullanmayı ve iOS cihazına dağıtırken bir Unity uygulamasının kesimli kullanıcılarına anında iletme bildirimleri göndermeyi gösterir.</span><span class="sxs-lookup"><span data-stu-id="45034-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and how to send push notifications to segmented users of a Unity application when deploying to an iOS device.</span></span>
<span data-ttu-id="45034-105">Bu öğretici, başlangıç noktası olarak bir Küre öğretici olarak klasik Unity Roll kullanır.</span><span class="sxs-lookup"><span data-stu-id="45034-105">This tutorial uses the classic Unity Roll a Ball tutorial as the starting point.</span></span> <span data-ttu-id="45034-106">Aşağıdaki öğreticide gösterdiğimiz Mobile Engagement tümleştirmesine geçmeden önce bu [öğreticideki](mobile-engagement-unity-roll-a-ball.md) adımları izlemelisiniz.</span><span class="sxs-lookup"><span data-stu-id="45034-106">You should follow the steps in this [tutorial](mobile-engagement-unity-roll-a-ball.md) before proceeding with the Mobile Engagement integration we showcase in the tutorial below.</span></span> 

<span data-ttu-id="45034-107">Bu öğretici için aşağıdakiler gereklidir:</span><span class="sxs-lookup"><span data-stu-id="45034-107">This tutorial requires the following:</span></span>

* [<span data-ttu-id="45034-108">Unity Düzenleyicisi</span><span class="sxs-lookup"><span data-stu-id="45034-108">Unity Editor</span></span>](http://unity3d.com/get-unity)
* [<span data-ttu-id="45034-109">Mobile Engagement Unity SDK</span><span class="sxs-lookup"><span data-stu-id="45034-109">Mobile Engagement Unity SDK</span></span>](https://aka.ms/azmeunitysdk)
* <span data-ttu-id="45034-110">XCode Düzenleyicisi</span><span class="sxs-lookup"><span data-stu-id="45034-110">XCode Editor</span></span>

> [!NOTE]
> <span data-ttu-id="45034-111">Bu öğreticiyi tamamlamak için etkin bir Azure hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="45034-111">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="45034-112">Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="45034-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="45034-113">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-ios-get-started).</span><span class="sxs-lookup"><span data-stu-id="45034-113">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-ios-get-started).</span></span>
> 
> 

## <span data-ttu-id="45034-114"><a id="setup-azme"></a>iOS uygulamanız için Mobile Engagement kurma</span><span class="sxs-lookup"><span data-stu-id="45034-114"><a id="setup-azme"></a>Setup Mobile Engagement for your iOS app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="45034-115"><a id="connecting-app"></a>Uygulamanızı Mobile Engagement arka ucuna bağlama</span><span class="sxs-lookup"><span data-stu-id="45034-115"><a id="connecting-app"></a>Connect your app to the Mobile Engagement backend</span></span>
### <a name="import-the-unity-package"></a><span data-ttu-id="45034-116">Unity paketini içeri aktarma</span><span class="sxs-lookup"><span data-stu-id="45034-116">Import the Unity package</span></span>
1. <span data-ttu-id="45034-117">[Mobile Engagement Unity paketini](https://aka.ms/azmeunitysdk) indirin ve yerel makinenize kaydedin.</span><span class="sxs-lookup"><span data-stu-id="45034-117">Download the [Mobile Engagement Unity package](https://aka.ms/azmeunitysdk) and save it to your local machine.</span></span> 
2. <span data-ttu-id="45034-118">**Varlıklar -> Paketi İçeri Aktar -> Özel Paket**’e gidin ve yukarıdaki adımda indirdiğiniz paketi seçin.</span><span class="sxs-lookup"><span data-stu-id="45034-118">Go to **Assets -> Import Package -> Custom Package** and select the package you downloaded in the above step.</span></span> 
   
    ![][70] 
3. <span data-ttu-id="45034-119">Tüm dosyaların seçildiğinden emin olun ve **İçeri Aktar** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="45034-119">Make sure all files are selected and click **Import** button.</span></span> 
   
    ![][71] 
4. <span data-ttu-id="45034-120">İçeri aktarma başarılı olduktan sonra, içeri aktarılan SDK dosyalarını projenizde görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="45034-120">Once Import is successful, you will see the imported SDK files in your project.</span></span>  
   
    ![][72] 

### <a name="update-the-engagementconfiguration"></a><span data-ttu-id="45034-121">EngagementConfiguration’ı güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="45034-121">Update the EngagementConfiguration</span></span>
1. <span data-ttu-id="45034-122">SDK klasöründe **EngagementConfiguration** betik dosyasını açın ve daha önce Azure portaldan aldığınız bağlantı dizesiyle **IOS\_CONNECTION\_STRING**’i güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="45034-122">Open up the **EngagementConfiguration** script file from the SDK folder and update the **IOS\_CONNECTION\_STRING** with the connection string you obtained earlier from the Azure portal.</span></span>  
   
    ![][73]
2. <span data-ttu-id="45034-123">Dosyayı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="45034-123">Save the file.</span></span> 

### <a name="configure-the-app-for-basic-tracking"></a><span data-ttu-id="45034-124">Uygulamayı temel izleme için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="45034-124">Configure the app for basic tracking</span></span>
1. <span data-ttu-id="45034-125">Düzenlemek için Player nesnesine ekli olan **PlayerController** betiğini açın.</span><span class="sxs-lookup"><span data-stu-id="45034-125">Open up the **PlayerController** script attached to the Player object for editing.</span></span> 
2. <span data-ttu-id="45034-126">Şu deyimi kullanarak aşağıdakileri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="45034-126">Add the following using statement:</span></span>
   
        using Microsoft.Azure.Engagement.Unity;
3. <span data-ttu-id="45034-127">Aşağıdakileri `Start()` yöntemine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="45034-127">Add the following to the `Start()` method</span></span>
   
        EngagementAgent.Initialize();
        EngagementAgent.StartActivity("Home");

### <a name="deploy-and-run-the-app"></a><span data-ttu-id="45034-128">Uygulamayı dağıtma ve çalıştırma</span><span class="sxs-lookup"><span data-stu-id="45034-128">Deploy and run the app</span></span>
1. <span data-ttu-id="45034-129">Bir iOS cihazı makinenize bağlayın.</span><span class="sxs-lookup"><span data-stu-id="45034-129">Connect an iOS device to your machine.</span></span> 
2. <span data-ttu-id="45034-130">**Dosya -> Yapı Ayarları**’nı açın</span><span class="sxs-lookup"><span data-stu-id="45034-130">Open up **File -> Build Settings**</span></span> 
   
    ![][40]
3. <span data-ttu-id="45034-131">**iOS**’u seçin ve ardından **Anahtar Platformu**’na tıklayın</span><span class="sxs-lookup"><span data-stu-id="45034-131">Select **iOS** and then click on **Switch Platform**</span></span>
   
    ![][41]
   
    ![][42]
4. <span data-ttu-id="45034-132">**Player ayarları**’na tıklayın ve geçerli bir Paket Tanımlayıcısı girin.</span><span class="sxs-lookup"><span data-stu-id="45034-132">Click on **Player settings** and provide a valid Bundle Identifier.</span></span> 
   
    ![][53]
5. <span data-ttu-id="45034-133">Son olarak, **Derle ve Çalıştır**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="45034-133">Finally click on **Build And Run**</span></span>
   
    ![][54]
6. <span data-ttu-id="45034-134">iOS paketini depolamak için bir klasör adı sağlamanız istenebilir.</span><span class="sxs-lookup"><span data-stu-id="45034-134">You may be asked to provide a folder name to store the iOS package.</span></span> 
   
    ![][43]
7. <span data-ttu-id="45034-135">Her şey yolunda giderse, proje derlenir ve XCode uygulamanızda açabilmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="45034-135">If everything goes fine, then the project will be compiled and you should open it up on your XCode application.</span></span> 
8. <span data-ttu-id="45034-136">**Paket Tanımlayıcısı**’nın projede doğru olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="45034-136">Make sure that the **Bundle identifier** is correct in the project.</span></span>  
   
    ![][75]
9. <span data-ttu-id="45034-137">Şimdi uygulamayı XCode’^da çalıştırın, böylece paket bağlı cihazınıza dağıtılır ve telefonunuzda Unity oyununuzu görmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="45034-137">Now run the app in XCode so that the package is deployed to your connected device and you should see your Unity game on your phone!</span></span> 

## <span data-ttu-id="45034-138"><a id="monitor"></a>Uygulamayı gerçek zamanlı izlemeyle bağlama</span><span class="sxs-lookup"><span data-stu-id="45034-138"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="45034-139"><a id="integrate-push"></a>Anında iletme bildirimlerini ve uygulama içi mesajlaşmayı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="45034-139"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="45034-140">Mobile Engagement, kullanıcılarınız ile etkileşim kurmanızı ve onlara kampanyalar bağlamında anında iletme bildirimleri ve uygulama içi mesajlaşma aracılığıyla erişmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="45034-140">Mobile Engagement allows you to interact with your users and REACH with push notifications and in-app messaging in the context of campaigns.</span></span> <span data-ttu-id="45034-141">Mobile Engagement portalında bu modüle REACH adı verilir.</span><span class="sxs-lookup"><span data-stu-id="45034-141">This module is called REACH in the Mobile Engagement portal.</span></span>
<span data-ttu-id="45034-142">Bildirimleri almak için uygulamanızda herhangi bir ek yapılandırma yapmanız gerekmez ve zaten ayarlıdır.</span><span class="sxs-lookup"><span data-stu-id="45034-142">You don't have to do any additional configuration in your app to receive notifications and it is already setup for it.</span></span>

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
