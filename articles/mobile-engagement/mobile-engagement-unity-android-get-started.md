---
title: "Unity Android dağıtımı için Azure Mobile Engagement kullanmaya başlama"
description: "Unity uygulamalarını iOS cihazlarına dağıtmak için Analizler ve Anında İletme Bildirimleri ile Azure Mobile Engagement kullanmayı öğrenin."
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
ms.openlocfilehash: bf0b758159d475b4ed7eadb84227e4824e11ba86
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-unity-android-deployment"></a><span data-ttu-id="a2885-103">Unity Android dağıtımı için Azure Mobile Engagement kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="a2885-103">Get Started with Azure Mobile Engagement for Unity Android deployment</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="a2885-104">Bu konu size uygulama kullanımınızı anlamak için Azure Mobile Engagement kullanmayı ve Android cihazına dağıtırken bir Unity uygulamasının kesimli kullanıcılarına anında iletme bildirimleri göndermeyi gösterir.</span><span class="sxs-lookup"><span data-stu-id="a2885-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and how to send push notifications to segmented users of a Unity application when deploying to an Android device.</span></span>
<span data-ttu-id="a2885-105">Bu öğretici, başlangıç noktası olarak bir Küre öğretici olarak klasik Unity Roll kullanır.</span><span class="sxs-lookup"><span data-stu-id="a2885-105">This tutorial uses the classic Unity Roll a Ball tutorial as the starting point.</span></span> <span data-ttu-id="a2885-106">Aşağıdaki öğreticide gösterdiğimiz Mobile Engagement tümleştirmesine geçmeden önce bu [öğreticideki](mobile-engagement-unity-roll-a-ball.md) adımları izlemelisiniz.</span><span class="sxs-lookup"><span data-stu-id="a2885-106">You should follow the steps in this [tutorial](mobile-engagement-unity-roll-a-ball.md) before proceeding with the Mobile Engagement integration we showcase in the tutorial below.</span></span> 

<span data-ttu-id="a2885-107">Bu öğretici için aşağıdakiler gereklidir:</span><span class="sxs-lookup"><span data-stu-id="a2885-107">This tutorial requires the following:</span></span>

* [<span data-ttu-id="a2885-108">Unity Düzenleyicisi</span><span class="sxs-lookup"><span data-stu-id="a2885-108">Unity Editor</span></span>](http://unity3d.com/get-unity)
* [<span data-ttu-id="a2885-109">Mobile Engagement Unity SDK</span><span class="sxs-lookup"><span data-stu-id="a2885-109">Mobile Engagement Unity SDK</span></span>](https://aka.ms/azmeunitysdk)
* <span data-ttu-id="a2885-110">Google Android SDK</span><span class="sxs-lookup"><span data-stu-id="a2885-110">Google Android SDK</span></span>

> [!NOTE]
> <span data-ttu-id="a2885-111">Bu öğreticiyi tamamlamak için etkin bir Azure hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a2885-111">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="a2885-112">Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a2885-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="a2885-113">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-android-get-started).</span><span class="sxs-lookup"><span data-stu-id="a2885-113">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-android-get-started).</span></span>
> 
> 

## <span data-ttu-id="a2885-114"><a id="setup-azme"></a>Android uygulamanız için Mobile Engagement kurma</span><span class="sxs-lookup"><span data-stu-id="a2885-114"><a id="setup-azme"></a>Setup Mobile Engagement for your Android app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="a2885-115"><a id="connecting-app"></a>Uygulamanızı Mobile Engagement arka ucuna bağlama</span><span class="sxs-lookup"><span data-stu-id="a2885-115"><a id="connecting-app"></a>Connect your app to the Mobile Engagement backend</span></span>
### <a name="import-the-unity-package"></a><span data-ttu-id="a2885-116">Unity paketini içeri aktarma</span><span class="sxs-lookup"><span data-stu-id="a2885-116">Import the Unity package</span></span>
1. <span data-ttu-id="a2885-117">[Mobile Engagement Unity paketini](https://aka.ms/azmeunitysdk) indirin ve yerel makinenize kaydedin.</span><span class="sxs-lookup"><span data-stu-id="a2885-117">Download the [Mobile Engagement Unity package](https://aka.ms/azmeunitysdk) and save it to your local machine.</span></span> 
2. <span data-ttu-id="a2885-118">**Varlıklar -> Paketi İçeri Aktar -> Özel Paket**’e gidin ve yukarıdaki adımda indirdiğiniz paketi seçin.</span><span class="sxs-lookup"><span data-stu-id="a2885-118">Go to **Assets -> Import Package -> Custom Package** and select the package you downloaded in the above step.</span></span> 
   
    ![][70] 
3. <span data-ttu-id="a2885-119">Tüm dosyaların seçildiğinden emin olun ve **İçeri Aktar** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a2885-119">Make sure all files are selected and click **Import** button.</span></span> 
   
    ![][71] 
4. <span data-ttu-id="a2885-120">İçeri aktarma başarılı olduktan sonra, içeri aktarılan SDK dosyalarını projenizde görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="a2885-120">Once Import is successful, you will see the imported SDK files in your project.</span></span>  
   
    ![][72] 

### <a name="update-the-engagementconfiguration"></a><span data-ttu-id="a2885-121">EngagementConfiguration’ı güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="a2885-121">Update the EngagementConfiguration</span></span>
1. <span data-ttu-id="a2885-122">SDK klasöründe **EngagementConfiguration** betik dosyasını açın ve daha önce Azure portaldan aldığınız bağlantı dizesiyle **ANDROID\_CONNECTION\_STRING**’i güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="a2885-122">Open up the **EngagementConfiguration** script file from the SDK folder and update the **ANDROID\_CONNECTION\_STRING** with the connection string you obtained earlier from the Azure portal.</span></span>  
   
    ![][73]
2. <span data-ttu-id="a2885-123">Dosyayı kaydetme</span><span class="sxs-lookup"><span data-stu-id="a2885-123">Save the file</span></span> 
3. <span data-ttu-id="a2885-124">**Dosya -> Engagement -> Android Derleme Bildirimi Oluştur**’yürütün.</span><span class="sxs-lookup"><span data-stu-id="a2885-124">Execute **File -> Engagement -> Generate Android Manifest**.</span></span> <span data-ttu-id="a2885-125">Bu, Mobile Engagement SDK tarafından eklenen eklentidir ve buna tıklamak proje ayarlarınızı otomatik olarak güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="a2885-125">This is the plugin added by the Mobile Engagement SDK and clicking on it will automatically update your project settings.</span></span> 
   
    ![][74]

> [!IMPORTANT]
> <span data-ttu-id="a2885-126">**EngagementConfiguration** dosyasını güncelleştirdiğiniz her sefer bunu yürüttüğünüzden emin olun, aksi takdirde değişiklikleriniz uygulamada yansıtılmaz.</span><span class="sxs-lookup"><span data-stu-id="a2885-126">Make sure to execute this every time you update the **EngagementConfiguration** file otherwise your changes will not be reflected in the app.</span></span> 
> 
> 

### <a name="configure-the-app-for-basic-tracking"></a><span data-ttu-id="a2885-127">Uygulamayı temel izleme için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a2885-127">Configure the app for basic tracking</span></span>
1. <span data-ttu-id="a2885-128">Düzenlemek için Player nesnesine ekli olan **PlayerController** betiğini açın.</span><span class="sxs-lookup"><span data-stu-id="a2885-128">Open up the **PlayerController** script attached to the Player object for editing.</span></span> 
2. <span data-ttu-id="a2885-129">Şu deyimi kullanarak aşağıdakileri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="a2885-129">Add the following using statement:</span></span>
   
        using Microsoft.Azure.Engagement.Unity;
3. <span data-ttu-id="a2885-130">Aşağıdakileri `Start()` yöntemine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a2885-130">Add the following to the `Start()` method</span></span>
   
        EngagementAgent.Initialize();
        EngagementAgent.StartActivity("Home");

### <a name="deploy-and-run-the-app"></a><span data-ttu-id="a2885-131">Uygulamayı dağıtma ve çalıştırma</span><span class="sxs-lookup"><span data-stu-id="a2885-131">Deploy and run the app</span></span>
<span data-ttu-id="a2885-132">Bu Unity uygulamasını cihazınıza dağıtmaya çalışmadan önce makinenizde Android SDK yüklü olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="a2885-132">Make sure that you have Android SDK installed on your machine before attempting to deploy this Unity app to your device.</span></span> 

1. <span data-ttu-id="a2885-133">Bir Android cihazı makinenize bağlayın.</span><span class="sxs-lookup"><span data-stu-id="a2885-133">Connect an Android device to your machine.</span></span> 
2. <span data-ttu-id="a2885-134">**Dosya -> Yapı Ayarları**’nı açın</span><span class="sxs-lookup"><span data-stu-id="a2885-134">Open up **File -> Build Settings**</span></span> 
   
    ![][40]
3. <span data-ttu-id="a2885-135">**Android**’i seçin ve ardından **Anahtar Platformu**’na tıklayın</span><span class="sxs-lookup"><span data-stu-id="a2885-135">Select **Android** and then click on **Switch Platform**</span></span>
   
    ![][51]
   
    ![][52]
4. <span data-ttu-id="a2885-136">**Player ayarları**’na tıklayın ve geçerli bir Paket Tanımlayıcısı girin.</span><span class="sxs-lookup"><span data-stu-id="a2885-136">Click on **Player settings** and provide a valid Bundle Identifier.</span></span> 
   
    ![][53]
5. <span data-ttu-id="a2885-137">Son olarak, **Derle ve Çalıştır**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a2885-137">Finally click on **Build And Run**</span></span>
   
    ![][54]
6. <span data-ttu-id="a2885-138">Android paketini depolamak için bir klasör adı sağlamanız istenebilir.</span><span class="sxs-lookup"><span data-stu-id="a2885-138">You may be asked to provide a folder name to store the Android package.</span></span> 
7. <span data-ttu-id="a2885-139">Her şey yolunda giderse, paket bağlı cihazınıza dağıtılır ve telefonunuzda Unity oyununuzu görmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="a2885-139">If everything goes fine, then the package will be deployed to your connected device and you should see your Unity game on your phone!</span></span> 

## <span data-ttu-id="a2885-140"><a id="monitor"></a>Uygulamayı gerçek zamanlı izlemeyle bağlama</span><span class="sxs-lookup"><span data-stu-id="a2885-140"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="a2885-141"><a id="integrate-push"></a>Anında iletme bildirimlerini ve uygulama içi mesajlaşmayı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="a2885-141"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

### <a name="update-the-engagementconfiguration"></a><span data-ttu-id="a2885-142">EngagementConfiguration’ı güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="a2885-142">Update the EngagementConfiguration</span></span>
1. <span data-ttu-id="a2885-143">SDK klasöründe **EngagementConfiguration** betik dosyasını açın ve daha önce Google Cloud Developer portaldan aldığınız **Google Project Number** ile **ANDROID\_GOOGLE\_NUMBER**’i güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="a2885-143">Open up the **EngagementConfiguration** script file from the SDK folder and update the **ANDROID\_GOOGLE\_NUMBER** with the **Google Project Number** you obtained earlier from the Google Cloud Developer portal.</span></span> <span data-ttu-id="a2885-144">Bu bir dize değeridir, bu nedenle çift tırnak içine aldığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="a2885-144">This is a string value so make sure to enclose it in double quotes.</span></span> 
   
    ![][75]
2. <span data-ttu-id="a2885-145">Dosyayı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="a2885-145">Save the file.</span></span> 
3. <span data-ttu-id="a2885-146">**Dosya -> Engagement -> Android Derleme Bildirimi Oluştur**’yürütün.</span><span class="sxs-lookup"><span data-stu-id="a2885-146">Execute **File -> Engagement -> Generate Android Manifest**.</span></span> <span data-ttu-id="a2885-147">Bu, Mobile Engagement SDK tarafından eklenen eklentidir ve buna tıklamak proje ayarlarınızı otomatik olarak güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="a2885-147">This is the plugin added by the Mobile Engagement SDK and clicking on it will automatically update your project settings.</span></span> 
   
    ![][74]

### <a name="configure-the-app-to-receive-notifications"></a><span data-ttu-id="a2885-148">Bildirimleri almak üzere uygulamayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a2885-148">Configure the app to receive notifications</span></span>
1. <span data-ttu-id="a2885-149">Düzenlemek için Player nesnesine ekli olan **PlayerController** betiğini açın.</span><span class="sxs-lookup"><span data-stu-id="a2885-149">Open up the **PlayerController** script attached to the Player object for editing.</span></span> 
2. <span data-ttu-id="a2885-150">Aşağıdakileri `Start()` yöntemine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a2885-150">Add the following to the `Start()` method</span></span>
   
        EngagementReachAgent.Initialize();
3. <span data-ttu-id="a2885-151">Artık uygulama güncelleştirildiğine göre, uygulamayı aşağıda verilen yönergelere göre bir cihaza dağıtın ve çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="a2885-151">Now that the app is updated, deploy and run the app on a device per the instructions provided below.</span></span> 

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
