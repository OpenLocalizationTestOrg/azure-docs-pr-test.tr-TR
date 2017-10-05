---
title: "Android Uygulamaları Azure Mobile Engagement kullanmaya başlama"
description: "Android uygulamaları için analizler ve anında iletme bildirimleri ile Azure Mobile Engagement kullanmayı öğrenin."
services: mobile-engagement
documentationcenter: android
author: piyushjo
manager: erikre
editor: 
ms.assetid: 3c286c6d-cfef-4e3e-9b2c-715429fe82db
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: hero-article
ms.date: 08/10/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: dc255a930bf71e6ef6d964bc5e3472a38ce4e467
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-android-apps"></a><span data-ttu-id="83a18-103">Android uygulamaları için Azure Mobile Engagement kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="83a18-103">Get started with Azure Mobile Engagement for Android apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="83a18-104">Bu konuda, uygulama kullanımınızı anlamak için nasıl Azure Mobile Engagement kullanılacağı ve bir Android uygulamasının segmentli kullanıcılarına nasıl anında iletme bildirimleri gönderileceği gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="83a18-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and how to send push notifications to segmented users of an Android application.</span></span>
<span data-ttu-id="83a18-105">Bu öğretici, Mobile Engagement kullanarak basit bir yayın senaryosunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="83a18-105">This tutorial demonstrates the simple broadcast scenario using Mobile Engagement.</span></span> <span data-ttu-id="83a18-106">Öğreticide, temel bilgiler toplayan ve Google Cloud Messaging (GCM) kullanarak anında iletme bildirimleri alan, boş bir Android uygulaması oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="83a18-106">In it, you create a blank Android app that collects basic data and receives push notifications using Google Cloud Messaging (GCM).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="83a18-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="83a18-107">Prerequisites</span></span>
<span data-ttu-id="83a18-108">Bu öğreticiyi tamamlamak için Android Studio tümleşik geliştirme ortamını ve en son Android platformunu içeren [Android Geliştirici Araçları](https://developer.android.com/sdk/index.html) gerekir.</span><span class="sxs-lookup"><span data-stu-id="83a18-108">Completing this tutorial requires the [Android Developer Tools](https://developer.android.com/sdk/index.html), which includes the Android Studio integrated development environment, and the latest Android platform.</span></span>

<span data-ttu-id="83a18-109">Ayrıca [Mobile Engagement Android SDK](https://aka.ms/vq9mfn) gereklidir.</span><span class="sxs-lookup"><span data-stu-id="83a18-109">It also requires the [Mobile Engagement Android SDK](https://aka.ms/vq9mfn).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="83a18-110">Bu öğreticiyi tamamlamak için etkin bir Azure hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="83a18-110">To complete this tutorial, you need an active Azure account.</span></span> <span data-ttu-id="83a18-111">Hesabınız yoksa yalnızca birkaç dakika içinde ücretsiz bir deneme sürümü hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="83a18-111">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="83a18-112">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-android-get-started).</span><span class="sxs-lookup"><span data-stu-id="83a18-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-android-get-started).</span></span>
>
>

## <a name="set-up-mobile-engagement-for-your-android-app"></a><span data-ttu-id="83a18-113">Android uygulamanız için Mobile Engagement kurma</span><span class="sxs-lookup"><span data-stu-id="83a18-113">Set up Mobile Engagement for your Android app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a name="connect-your-app-to-the-mobile-engagement-backend"></a><span data-ttu-id="83a18-114">Uygulamanızı Mobile Engagement arka ucuna bağlama</span><span class="sxs-lookup"><span data-stu-id="83a18-114">Connect your app to the Mobile Engagement backend</span></span>
<span data-ttu-id="83a18-115">Bu öğreticide, veri toplamak ve anında iletme bildirimi göndermek için gerekli en küçük grup olan bir "temel tümleştirme" gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="83a18-115">This tutorial presents a "basic integration", which is the minimal set required to collect data and send a push notification.</span></span> <span data-ttu-id="83a18-116">Tümleştirmeyi göstermek için Android Studio ile temel bir uygulama oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="83a18-116">You create a basic app with Android Studio to demonstrate the integration.</span></span>

<span data-ttu-id="83a18-117">Tümleştirme belgelerinin tamamı [Mobile Engagement Android SDK tümleştirmesi](mobile-engagement-android-sdk-overview.md)’nde bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="83a18-117">The complete integration documentation can be found in the [Mobile Engagement Android SDK integration](mobile-engagement-android-sdk-overview.md).</span></span>

### <a name="create-an-android-project"></a><span data-ttu-id="83a18-118">Android projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="83a18-118">Create an Android project</span></span>
1. <span data-ttu-id="83a18-119">**Android Studio**’yu başlatın ve açılır menüde **Yeni bir Android Studio projesi başlat**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="83a18-119">Start **Android Studio**, and in the pop-up, select **Start a new Android Studio project**.</span></span>

    ![][1]
2. <span data-ttu-id="83a18-120">Uygulama adı ve şirket etki alanı belirtin.</span><span class="sxs-lookup"><span data-stu-id="83a18-120">Provide an app name and company domain.</span></span> <span data-ttu-id="83a18-121">Girdiğiniz bilgileri daha sonra kullanmanız gerekeceğinden bunları not edin.</span><span class="sxs-lookup"><span data-stu-id="83a18-121">Make a note of what you are filling, because you need it later.</span></span> <span data-ttu-id="83a18-122">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="83a18-122">Click **Next**.</span></span>

    ![][2]
3. <span data-ttu-id="83a18-123">Hedef form faktörünü ve API düzeyini seçip **İleri**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="83a18-123">Select the target form factor and API level, and click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="83a18-124">Mobile Engagement, en az API düzey 10 (Android 2.3.3) gerektirir.</span><span class="sxs-lookup"><span data-stu-id="83a18-124">Mobile Engagement requires API level 10 minimum (Android 2.3.3).</span></span>
   >
   >

    ![][3]
4. <span data-ttu-id="83a18-125">Burada, bu uygulama için tek ekran olan **Boş Etkinlik**’i seçip **İleri**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="83a18-125">Select **Blank Activity** here, which is the only screen for this app and click **Next**.</span></span>

    ![][4]
5. <span data-ttu-id="83a18-126">Son olarak, varsayılan değerleri olduğu gibi bırakıp **Son**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="83a18-126">Finally, leave the defaults as is and click **Finish**.</span></span>

    ![][5]

<span data-ttu-id="83a18-127">Şimdi Android Studio, Mobile Engagement’ı tümleştirdiğimiz tanıtım uygulamasını oluşturur.</span><span class="sxs-lookup"><span data-stu-id="83a18-127">Android Studio now creates the demo app into which we integrate Mobile Engagement.</span></span>

### <a name="include-the-sdk-library-in-your-project"></a><span data-ttu-id="83a18-128">SDK kitaplığını projenize ekleme</span><span class="sxs-lookup"><span data-stu-id="83a18-128">Include the SDK library in your project</span></span>
1. <span data-ttu-id="83a18-129">[Mobile Engagement Android SDK](https://aka.ms/vq9mfn)’yı indirin.</span><span class="sxs-lookup"><span data-stu-id="83a18-129">Download the [Mobile Engagement Android SDK](https://aka.ms/vq9mfn).</span></span>
2. <span data-ttu-id="83a18-130">Arşiv dosyasını bilgisayarınızdaki bir klasöre ayıklayın.</span><span class="sxs-lookup"><span data-stu-id="83a18-130">Extract the archive file to a folder in your computer.</span></span>
3. <span data-ttu-id="83a18-131">Bu SDK'nın geçerli sürümüne ait .jar kitaplığını belirleyin ve Pano’ya kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="83a18-131">Identify the .jar library for the current version of this SDK and copy it to the Clipboard.</span></span>

      ![][6]
4. <span data-ttu-id="83a18-132">**Proje** bölümüne gidin (1) ve .jar kitaplığını libs klasörüne yapıştırın (2).</span><span class="sxs-lookup"><span data-stu-id="83a18-132">Navigate to the **Project** section (1) and paste the .jar in the libs folder (2).</span></span>

      ![][7]
5. <span data-ttu-id="83a18-133">Kitaplığı yüklemek için projeyi eşitleyin.</span><span class="sxs-lookup"><span data-stu-id="83a18-133">To load the library, sync the project .</span></span>

      ![][8]

### <a name="connect-your-app-to-mobile-engagement-backend-with-the-connection-string"></a><span data-ttu-id="83a18-134">Uygulamanızı Bağlantı Dizesi ile Mobile Engagement arka ucuna bağlama</span><span class="sxs-lookup"><span data-stu-id="83a18-134">Connect your app to Mobile Engagement backend with the Connection String</span></span>
1. <span data-ttu-id="83a18-135">Aşağıdaki kod satırlarını etkinlik oluşturmaya kopyalayın (uygulamanızın tek bir noktasında yapılmalıdır, bu nokta genellikle ana etkinliktir).</span><span class="sxs-lookup"><span data-stu-id="83a18-135">Copy the following lines of code into the activity creation (must be done only in one place of your application, usually the main activity).</span></span> <span data-ttu-id="83a18-136">Bu örnek uygulama için, src -> main -> java klasörü altında MainActivity dosyasını açın ve aşağıdakileri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="83a18-136">For this sample app, open up the MainActivity under src -> main -> java folder and add the following:</span></span>

        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
        EngagementAgent.getInstance(this).init(engagementConfiguration);
2. <span data-ttu-id="83a18-137">Alt + Enter tuşlarına basarak veya aşağıdaki içeri aktarma deyimlerini ekleyerek başvuruları çözümleyin:</span><span class="sxs-lookup"><span data-stu-id="83a18-137">Resolve the references by pressing Alt + Enter or adding the following import statements:</span></span>

        import com.microsoft.azure.engagement.EngagementAgent;
        import com.microsoft.azure.engagement.EngagementConfiguration;
3. <span data-ttu-id="83a18-138">Uygulamanızın**Bağlantı Bilgileri** sayfasında Klasik Azure Portalı’na geri gidin ve **Bağlantı Dizesi**’ni kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="83a18-138">Go back to the Azure Classic Portal in your app's **Connection Info** page and copy the **Connection String**.</span></span>

      ![][9]
4. <span data-ttu-id="83a18-139">`setConnectionString` parametresine yapıştırarak aşağıdaki kodda gösterilen dizenin tamamını değiştirin:</span><span class="sxs-lookup"><span data-stu-id="83a18-139">Paste it into the `setConnectionString` parameter, replacing the entire string shown in the following code:</span></span>

        engagementConfiguration.setConnectionString("Endpoint=my-company-name.device.mobileengagement.windows.net;SdkKey=********************;AppId=*********");

### <a name="add-permissions-and-a-service-declaration"></a><span data-ttu-id="83a18-140">İzinler ve bir hizmet bildirimi ekleme</span><span class="sxs-lookup"><span data-stu-id="83a18-140">Add permissions and a service declaration</span></span>
1. <span data-ttu-id="83a18-141">Bu izinleri, projenizin Manifest.xml dosyasında `<application>` etiketinin hemen önüne ya da arkasına ekleyin:</span><span class="sxs-lookup"><span data-stu-id="83a18-141">Add these permissions to the Manifest.xml of your project immediately before or after the `<application>` tag:</span></span>

        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
        <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
        <uses-permission android:name="android.permission.VIBRATE" />
        <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
2. <span data-ttu-id="83a18-142">Aracı hizmetini bildirmek için `<application>` ve `</application>` etiketleri arasına şu kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="83a18-142">To declare the agent service, add this code between the `<application>` and `</application>` tags:</span></span>

        <service
             android:name="com.microsoft.azure.engagement.service.EngagementService"
             android:exported="false"
             android:label="<Your application name>"
             android:process=":Engagement"/>
3. <span data-ttu-id="83a18-143">Yapıştırdığınız kodda, cihazda çalışmakta olan hizmetleri görebileceğiniz **Ayarlar** menüsünde görüntülenen etiketteki `"<Your application name>"` değerini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="83a18-143">In the code you pasted, replace `"<Your application name>"` in the label, which is displayed in the **Settings** menu where you can see services running on the device.</span></span> <span data-ttu-id="83a18-144">Örneğin bu etikete "Hizmet" sözcüğünü ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="83a18-144">You can add the word "Service" in that label for example.</span></span>

### <a name="send-a-screen-to-mobile-engagement"></a><span data-ttu-id="83a18-145">Bir ekranı Mobile Engagement’a gönderme</span><span class="sxs-lookup"><span data-stu-id="83a18-145">Send a screen to Mobile Engagement</span></span>
<span data-ttu-id="83a18-146">Veri göndermeye başlamak ve kullanıcıların etkin olduğundan emin olmak için, Mobile Engagement arka ucuna en az bir ekran (Etkinlik) göndermelisiniz.</span><span class="sxs-lookup"><span data-stu-id="83a18-146">To start sending data and ensure that the users are active, you must send at least one screen (Activity) to the Mobile Engagement backend.</span></span>

<span data-ttu-id="83a18-147">**MainActivity.java** dosyasına gidip aşağıdakileri ekleyerek **MainActivity** temel sınıfını **EngagementActivity** olarak değiştirin:</span><span class="sxs-lookup"><span data-stu-id="83a18-147">Go to **MainActivity.java** and add the following to replace the base class of **MainActivity** to **EngagementActivity**:</span></span>

    public class MainActivity extends EngagementActivity {

> [!NOTE]
> <span data-ttu-id="83a18-148">Temel sınıfınız *Etkinlik* değilse farklı sınıflardan nasıl devralınacağı konusunda [Gelişmiş Android Raporlama](mobile-engagement-android-advanced-reporting.md)’ya başvurun.</span><span class="sxs-lookup"><span data-stu-id="83a18-148">If your base class is not *Activity*, consult [Advanced Android Reporting](mobile-engagement-android-advanced-reporting.md) for how to inherit from different classes.</span></span>
>
>

<span data-ttu-id="83a18-149">Bu basit örnek senaryo için aşağıdaki satırı açıklama satırı yapın:</span><span class="sxs-lookup"><span data-stu-id="83a18-149">Comment out the following line for this simple sample scenario:</span></span>

    // setSupportActionBar(toolbar);

<span data-ttu-id="83a18-150">Uygulamanızda `ActionBar` öğesini tutmak istiyorsanız [Gelişmiş Android Raporlama](mobile-engagement-android-advanced-reporting.md) konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="83a18-150">If you want to keep the `ActionBar` in your app, see [Advanced Android Reporting](mobile-engagement-android-advanced-reporting.md).</span></span>

## <a name="connect-app-with-real-time-monitoring"></a><span data-ttu-id="83a18-151">Uygulamayı gerçek zamanlı izlemeyle bağlama</span><span class="sxs-lookup"><span data-stu-id="83a18-151">Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a name="enable-push-notifications-and-in-app-messaging"></a><span data-ttu-id="83a18-152">Anında iletme bildirimlerini ve uygulama içi mesajlaşmayı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="83a18-152">Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="83a18-153">Mobile Engagement, bir kampanya sırasında anında iletme bildirimleri ve uygulama içi mesajlaşma ile kullanıcılarınızla etkileşim kurmanızı ve REACH ile kullanıcılarınıza ulaşmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="83a18-153">During a campaign, Mobile Engagement lets you interact with and REACH your users with push notifications and in-app messaging.</span></span> <span data-ttu-id="83a18-154">Mobile Engagement portalında bu modüle REACH adı verilir.</span><span class="sxs-lookup"><span data-stu-id="83a18-154">This module is called REACH in the Mobile Engagement portal.</span></span>
<span data-ttu-id="83a18-155">Aşağıdaki bölüm, uygulamanızı bu bildirim ve mesajları alacak şekilde ayarlar.</span><span class="sxs-lookup"><span data-stu-id="83a18-155">The following section sets up your app to receive them.</span></span>

### <a name="copy-sdk-resources-in-your-project"></a><span data-ttu-id="83a18-156">SDK kaynaklarını projenize kopyalama</span><span class="sxs-lookup"><span data-stu-id="83a18-156">Copy SDK resources in your project</span></span>
1. <span data-ttu-id="83a18-157">İndirilen SDK içeriğinize geri gidip **res** klasörünü kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="83a18-157">Navigate back to your SDK download content and copy the **res** folder.</span></span>

    ![][10]
2. <span data-ttu-id="83a18-158">Android Studio’ya geri gidip proje dosyalarınıza ait **ana** dizini seçin ve kopyaladığınız klasörü buraya yapıştırarak kaynakları projenize ekleyin.</span><span class="sxs-lookup"><span data-stu-id="83a18-158">Go back to Android Studio, select the **main** directory of your project files, and then paste it to add the resources to your project.</span></span>

    ![][11]

[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

[!INCLUDE [Enable in-app messaging](../../includes/mobile-engagement-android-send-push.md)]

[!INCLUDE [Send notification from portal](../../includes/mobile-engagement-android-send-push-from-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="83a18-159">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="83a18-159">Next steps</span></span>
<span data-ttu-id="83a18-160">SDK tümleştirmesi hakkında ayrıntılı bilgi edinmek için [Android SDK](mobile-engagement-android-sdk-overview.md) sayfasına gidin.</span><span class="sxs-lookup"><span data-stu-id="83a18-160">Go to [Android SDK](mobile-engagement-android-sdk-overview.md) to get detailed knowledge about the SDK integration.</span></span>

<!-- Images. -->
[1]: ./media/mobile-engagement-android-get-started/android-studio-new-project.png
[2]: ./media/mobile-engagement-android-get-started/android-studio-project-props.png
[3]: ./media/mobile-engagement-android-get-started/android-studio-project-props2.png
[4]: ./media/mobile-engagement-android-get-started/android-studio-add-activity.png
[5]: ./media/mobile-engagement-android-get-started/android-studio-activity-name.png
[6]: ./media/mobile-engagement-android-get-started/sdk-content.png
[7]: ./media/mobile-engagement-android-get-started/paste-jar.png
[8]: ./media/mobile-engagement-android-get-started/sync-project.png
[9]: ./media/mobile-engagement-android-get-started/app-connection-info-page.png
[10]: ./media/mobile-engagement-android-get-started/copy-resources.png
[11]: ./media/mobile-engagement-android-get-started/paste-resources.png
