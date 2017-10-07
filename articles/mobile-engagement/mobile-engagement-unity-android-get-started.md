---
title: "Unity Android dağıtımı için aaaGet Azure Mobile Engagement ile başlatıldı"
description: "Bilgi nasıl tooiOS aygıtları dağıtma Unity uygulamaları için analizler ve anında iletme bildirimleri ile Azure Mobile Engagement toouse."
services: mobile-engagement
documentationcenter: unity
author: piyushjo
manager: erikre
editor: 
ms.assetid: d5f0ef79-be00-4cec-97a5-a0b2fdaa380e
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-unity-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: c4d34691daeb7544b11c2d6895b2474af0f902b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-unity-android-deployment"></a><span data-ttu-id="e9fb1-103">Unity Android dağıtımı için Azure Mobile Engagement kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="e9fb1-103">Get Started with Azure Mobile Engagement for Unity Android deployment</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="e9fb1-104">Bu konu, nasıl gösterir toouse Azure Mobile Engagement toounderstand, uygulama kullanımınızı ve nasıl toosend anında iletme bildirimleri toosegmented kullanıcılar bir Unity uygulamasının tooan Android cihazına dağıtırken.</span><span class="sxs-lookup"><span data-stu-id="e9fb1-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and how toosend push notifications toosegmented users of a Unity application when deploying tooan Android device.</span></span>
<span data-ttu-id="e9fb1-105">Bu öğretici kullanır Klasik Unity Roll bir küre öğretici hello başlangıç noktası hello.</span><span class="sxs-lookup"><span data-stu-id="e9fb1-105">This tutorial uses hello classic Unity Roll a Ball tutorial as hello starting point.</span></span> <span data-ttu-id="e9fb1-106">Bu başlangıç adımları izlemelisiniz [öğretici](mobile-engagement-unity-roll-a-ball.md) hello hello aşağıdaki öğreticide gösterdiğimiz Mobile Engagement tümleştirmesi işlemine devam etmeden önce.</span><span class="sxs-lookup"><span data-stu-id="e9fb1-106">You should follow hello steps in this [tutorial](mobile-engagement-unity-roll-a-ball.md) before proceeding with hello Mobile Engagement integration we showcase in hello tutorial below.</span></span> 

<span data-ttu-id="e9fb1-107">Bu öğretici hello aşağıdakileri gerektirir:</span><span class="sxs-lookup"><span data-stu-id="e9fb1-107">This tutorial requires hello following:</span></span>

* [<span data-ttu-id="e9fb1-108">Unity Düzenleyicisi</span><span class="sxs-lookup"><span data-stu-id="e9fb1-108">Unity Editor</span></span>](http://unity3d.com/get-unity)
* [<span data-ttu-id="e9fb1-109">Mobile Engagement Unity SDK</span><span class="sxs-lookup"><span data-stu-id="e9fb1-109">Mobile Engagement Unity SDK</span></span>](https://aka.ms/azmeunitysdk)
* <span data-ttu-id="e9fb1-110">Google Android SDK</span><span class="sxs-lookup"><span data-stu-id="e9fb1-110">Google Android SDK</span></span>

> [!NOTE]
> <span data-ttu-id="e9fb1-111">toocomplete Bu öğretici, etkin bir Azure hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="e9fb1-111">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="e9fb1-112">Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e9fb1-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="e9fb1-113">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-android-get-started).</span><span class="sxs-lookup"><span data-stu-id="e9fb1-113">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-android-get-started).</span></span>
> 
> 

## <span data-ttu-id="e9fb1-114"><a id="setup-azme"></a>Android uygulamanız için Mobile Engagement kurma</span><span class="sxs-lookup"><span data-stu-id="e9fb1-114"><a id="setup-azme"></a>Setup Mobile Engagement for your Android app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="e9fb1-115"><a id="connecting-app"></a>Uygulamanızın toohello Mobile Engagement arka ucuna bağlanmak</span><span class="sxs-lookup"><span data-stu-id="e9fb1-115"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
### <a name="import-hello-unity-package"></a><span data-ttu-id="e9fb1-116">Merhaba Unity paketini içeri aktarma</span><span class="sxs-lookup"><span data-stu-id="e9fb1-116">Import hello Unity package</span></span>
1. <span data-ttu-id="e9fb1-117">Merhaba karşıdan [Mobile Engagement Unity paketini](https://aka.ms/azmeunitysdk) ve tooyour yerel makine kaydedin.</span><span class="sxs-lookup"><span data-stu-id="e9fb1-117">Download hello [Mobile Engagement Unity package](https://aka.ms/azmeunitysdk) and save it tooyour local machine.</span></span> 
2. <span data-ttu-id="e9fb1-118">Çok Git**varlıklar -> paketi İçeri Aktar -> özel paket** ve indirilen Yukarıdaki adımı hello içindeki select hello paketi.</span><span class="sxs-lookup"><span data-stu-id="e9fb1-118">Go too**Assets -> Import Package -> Custom Package** and select hello package you downloaded in hello above step.</span></span> 
   
    ![][70] 
3. <span data-ttu-id="e9fb1-119">Tüm dosyaların seçildiğinden emin olun ve **İçeri Aktar** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e9fb1-119">Make sure all files are selected and click **Import** button.</span></span> 
   
    ![][71] 
4. <span data-ttu-id="e9fb1-120">İçeri aktarma başarılı olduktan sonra hello içeri aktarılan SDK dosyalarını projenizde görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="e9fb1-120">Once Import is successful, you will see hello imported SDK files in your project.</span></span>  
   
    ![][72] 

### <a name="update-hello-engagementconfiguration"></a><span data-ttu-id="e9fb1-121">Merhaba EngagementConfiguration güncelleştir</span><span class="sxs-lookup"><span data-stu-id="e9fb1-121">Update hello EngagementConfiguration</span></span>
1. <span data-ttu-id="e9fb1-122">Merhaba açın **EngagementConfiguration** hello SDK klasörü ve güncelleştirme hello betik dosyasından **ANDROID\_bağlantı\_dize** aldığınız hello bağlantı dizesiyle daha önce hello Azure portalı.</span><span class="sxs-lookup"><span data-stu-id="e9fb1-122">Open up hello **EngagementConfiguration** script file from hello SDK folder and update hello **ANDROID\_CONNECTION\_STRING** with hello connection string you obtained earlier from hello Azure portal.</span></span>  
   
    ![][73]
2. <span data-ttu-id="e9fb1-123">Merhaba dosyasını kaydedin</span><span class="sxs-lookup"><span data-stu-id="e9fb1-123">Save hello file</span></span> 
3. <span data-ttu-id="e9fb1-124">**Dosya -> Engagement -> Android Derleme Bildirimi Oluştur**’yürütün.</span><span class="sxs-lookup"><span data-stu-id="e9fb1-124">Execute **File -> Engagement -> Generate Android Manifest**.</span></span> <span data-ttu-id="e9fb1-125">Bu hello Mobile Engagement SDK tarafından eklenen hello eklentidir ve buna tıklamak proje ayarlarınızı otomatik olarak güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="e9fb1-125">This is hello plugin added by hello Mobile Engagement SDK and clicking on it will automatically update your project settings.</span></span> 
   
    ![][74]

> [!IMPORTANT]
> <span data-ttu-id="e9fb1-126">Merhaba güncelleştirdiğiniz her sefer emin tooexecute bunu yap **EngagementConfiguration** dosya Aksi takdirde değişiklikleriniz hello uygulamada yansıtılmaz.</span><span class="sxs-lookup"><span data-stu-id="e9fb1-126">Make sure tooexecute this every time you update hello **EngagementConfiguration** file otherwise your changes will not be reflected in hello app.</span></span> 
> 
> 

### <a name="configure-hello-app-for-basic-tracking"></a><span data-ttu-id="e9fb1-127">Merhaba uygulamayı temel izleme için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="e9fb1-127">Configure hello app for basic tracking</span></span>
1. <span data-ttu-id="e9fb1-128">Merhaba açın **PlayerController** iliştirilmiş düzenlemek için Player nesnesine toohello komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="e9fb1-128">Open up hello **PlayerController** script attached toohello Player object for editing.</span></span> 
2. <span data-ttu-id="e9fb1-129">Merhaba aşağıdaki ekleme deyimini kullanarak:</span><span class="sxs-lookup"><span data-stu-id="e9fb1-129">Add hello following using statement:</span></span>
   
        using Microsoft.Azure.Engagement.Unity;
3. <span data-ttu-id="e9fb1-130">Toohello aşağıdaki hello eklemek `Start()` yöntemi</span><span class="sxs-lookup"><span data-stu-id="e9fb1-130">Add hello following toohello `Start()` method</span></span>
   
        EngagementAgent.Initialize();
        EngagementAgent.StartActivity("Home");

### <a name="deploy-and-run-hello-app"></a><span data-ttu-id="e9fb1-131">Dağıtma ve hello uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="e9fb1-131">Deploy and run hello app</span></span>
<span data-ttu-id="e9fb1-132">Android SDK toodeploy bu Unity uygulamasını tooyour aygıt çalışmadan önce makinenizde yüklü olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="e9fb1-132">Make sure that you have Android SDK installed on your machine before attempting toodeploy this Unity app tooyour device.</span></span> 

1. <span data-ttu-id="e9fb1-133">Bir Android cihaz tooyour makineyi bağlayın.</span><span class="sxs-lookup"><span data-stu-id="e9fb1-133">Connect an Android device tooyour machine.</span></span> 
2. <span data-ttu-id="e9fb1-134">**Dosya -> Yapı Ayarları**’nı açın</span><span class="sxs-lookup"><span data-stu-id="e9fb1-134">Open up **File -> Build Settings**</span></span> 
   
    ![][40]
3. <span data-ttu-id="e9fb1-135">**Android**’i seçin ve ardından **Anahtar Platformu**’na tıklayın</span><span class="sxs-lookup"><span data-stu-id="e9fb1-135">Select **Android** and then click on **Switch Platform**</span></span>
   
    ![][51]
   
    ![][52]
4. <span data-ttu-id="e9fb1-136">**Player ayarları**’na tıklayın ve geçerli bir Paket Tanımlayıcısı girin.</span><span class="sxs-lookup"><span data-stu-id="e9fb1-136">Click on **Player settings** and provide a valid Bundle Identifier.</span></span> 
   
    ![][53]
5. <span data-ttu-id="e9fb1-137">Son olarak, **Derle ve Çalıştır**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e9fb1-137">Finally click on **Build And Run**</span></span>
   
    ![][54]
6. <span data-ttu-id="e9fb1-138">Olabilir bir klasör adı toostore hello Android paketini tooprovide istedi.</span><span class="sxs-lookup"><span data-stu-id="e9fb1-138">You may be asked tooprovide a folder name toostore hello Android package.</span></span> 
7. <span data-ttu-id="e9fb1-139">Merhaba paket bağlı dağıtılan tooyour sonra her şey ince, giderse Unity oyununuzu cihaz ve telefonunuzda görmeniz gerekir!</span><span class="sxs-lookup"><span data-stu-id="e9fb1-139">If everything goes fine, then hello package will be deployed tooyour connected device and you should see your Unity game on your phone!</span></span> 

## <span data-ttu-id="e9fb1-140"><a id="monitor"></a>Uygulamayı gerçek zamanlı izlemeyle bağlama</span><span class="sxs-lookup"><span data-stu-id="e9fb1-140"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="e9fb1-141"><a id="integrate-push"></a>Anında iletme bildirimlerini ve uygulama içi mesajlaşmayı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="e9fb1-141"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

### <a name="update-hello-engagementconfiguration"></a><span data-ttu-id="e9fb1-142">Merhaba EngagementConfiguration güncelleştir</span><span class="sxs-lookup"><span data-stu-id="e9fb1-142">Update hello EngagementConfiguration</span></span>
1. <span data-ttu-id="e9fb1-143">Merhaba açın **EngagementConfiguration** hello SDK klasörü ve güncelleştirme hello betik dosyasından **ANDROID\_GOOGLE\_numarası** hello ile **Google proje Sayı** önceki hello Google Cloud Developer portaldan aldığınız.</span><span class="sxs-lookup"><span data-stu-id="e9fb1-143">Open up hello **EngagementConfiguration** script file from hello SDK folder and update hello **ANDROID\_GOOGLE\_NUMBER** with hello **Google Project Number** you obtained earlier from hello Google Cloud Developer portal.</span></span> <span data-ttu-id="e9fb1-144">Bu bir dizedir değeri nedenle emin tooenclose olun çift tırnak işareti içinde.</span><span class="sxs-lookup"><span data-stu-id="e9fb1-144">This is a string value so make sure tooenclose it in double quotes.</span></span> 
   
    ![][75]
2. <span data-ttu-id="e9fb1-145">Merhaba dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="e9fb1-145">Save hello file.</span></span> 
3. <span data-ttu-id="e9fb1-146">**Dosya -> Engagement -> Android Derleme Bildirimi Oluştur**’yürütün.</span><span class="sxs-lookup"><span data-stu-id="e9fb1-146">Execute **File -> Engagement -> Generate Android Manifest**.</span></span> <span data-ttu-id="e9fb1-147">Bu hello Mobile Engagement SDK tarafından eklenen hello eklentidir ve buna tıklamak proje ayarlarınızı otomatik olarak güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="e9fb1-147">This is hello plugin added by hello Mobile Engagement SDK and clicking on it will automatically update your project settings.</span></span> 
   
    ![][74]

### <a name="configure-hello-app-tooreceive-notifications"></a><span data-ttu-id="e9fb1-148">Merhaba uygulama tooreceive bildirimleri yapılandırma</span><span class="sxs-lookup"><span data-stu-id="e9fb1-148">Configure hello app tooreceive notifications</span></span>
1. <span data-ttu-id="e9fb1-149">Merhaba açın **PlayerController** iliştirilmiş düzenlemek için Player nesnesine toohello komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="e9fb1-149">Open up hello **PlayerController** script attached toohello Player object for editing.</span></span> 
2. <span data-ttu-id="e9fb1-150">Toohello aşağıdaki hello eklemek `Start()` yöntemi</span><span class="sxs-lookup"><span data-stu-id="e9fb1-150">Add hello following toohello `Start()` method</span></span>
   
        EngagementReachAgent.Initialize();
3. <span data-ttu-id="e9fb1-151">Merhaba uygulama güncelleştirildiğine göre dağıtın ve hello yönergeler aşağıda sağlanan her bir cihazda hello uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e9fb1-151">Now that hello app is updated, deploy and run hello app on a device per hello instructions provided below.</span></span> 

[!INCLUDE [Send notification from portal](../../includes/mobile-engagement-android-send-push-from-portal.md)]

<!-- Images -->
[40]: ./media/mobile-engagement-unity-android-get-started/40.png
[70]: ./media/mobile-engagement-unity-android-get-started/70.png
[71]: ./media/mobile-engagement-unity-android-get-started/71.png
[72]: ./media/mobile-engagement-unity-android-get-started/72.png
[73]: ./media/mobile-engagement-unity-android-get-started/73.png
[74]: ./media/mobile-engagement-unity-android-get-started/74.png
[75]: ./media/mobile-engagement-unity-android-get-started/75.png
[51]: ./media/mobile-engagement-unity-android-get-started/51.png
[52]: ./media/mobile-engagement-unity-android-get-started/52.png
[53]: ./media/mobile-engagement-unity-android-get-started/53.png
[54]: ./media/mobile-engagement-unity-android-get-started/54.png
