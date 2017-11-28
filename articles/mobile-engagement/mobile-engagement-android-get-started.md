---
title: "Android uygulamaları Azure Mobile Engagement ile aaaGet başlatıldı"
description: "Bilgi nasıl Android uygulamaları için analizler ve anında iletme bildirimleri ile Azure Mobile Engagement toouse."
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
ms.openlocfilehash: e8c92607691104750cdf1c4f7639a041d8a7bcd5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-android-apps"></a><span data-ttu-id="d65b6-103">Android uygulamaları için Azure Mobile Engagement kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="d65b6-103">Get started with Azure Mobile Engagement for Android apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="d65b6-104">Bu konu, nasıl gösterir toouse Azure Mobile Engagement toounderstand, uygulama kullanımınızı ve toosend bir Android uygulamasının bildirimleri toosegmented kullanıcılarına nasıl anında iletme.</span><span class="sxs-lookup"><span data-stu-id="d65b6-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and how toosend push notifications toosegmented users of an Android application.</span></span>
<span data-ttu-id="d65b6-105">Bu öğretici, Mobile Engagement kullanarak hello basit yayın senaryosunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="d65b6-105">This tutorial demonstrates hello simple broadcast scenario using Mobile Engagement.</span></span> <span data-ttu-id="d65b6-106">Öğreticide, temel bilgiler toplayan ve Google Cloud Messaging (GCM) kullanarak anında iletme bildirimleri alan, boş bir Android uygulaması oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="d65b6-106">In it, you create a blank Android app that collects basic data and receives push notifications using Google Cloud Messaging (GCM).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d65b6-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="d65b6-107">Prerequisites</span></span>
<span data-ttu-id="d65b6-108">Bu öğreticiyi tamamlamak gerektirir hello [Android Geliştirici Araçları](https://developer.android.com/sdk/index.html), hello Android Studio tümleşik geliştirme ortamını ve en son Android platformunu hello içerir.</span><span class="sxs-lookup"><span data-stu-id="d65b6-108">Completing this tutorial requires hello [Android Developer Tools](https://developer.android.com/sdk/index.html), which includes hello Android Studio integrated development environment, and hello latest Android platform.</span></span>

<span data-ttu-id="d65b6-109">Ayrıca hello gerektirir [Mobile Engagement Android SDK](https://aka.ms/vq9mfn).</span><span class="sxs-lookup"><span data-stu-id="d65b6-109">It also requires hello [Mobile Engagement Android SDK](https://aka.ms/vq9mfn).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d65b6-110">toocomplete Bu öğretici, etkin bir Azure hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d65b6-110">toocomplete this tutorial, you need an active Azure account.</span></span> <span data-ttu-id="d65b6-111">Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d65b6-111">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="d65b6-112">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-android-get-started).</span><span class="sxs-lookup"><span data-stu-id="d65b6-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-android-get-started).</span></span>
>
>

## <a name="set-up-mobile-engagement-for-your-android-app"></a><span data-ttu-id="d65b6-113">Android uygulamanız için Mobile Engagement kurma</span><span class="sxs-lookup"><span data-stu-id="d65b6-113">Set up Mobile Engagement for your Android app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a name="connect-your-app-toohello-mobile-engagement-backend"></a><span data-ttu-id="d65b6-114">Uygulamanızın toohello Mobile Engagement arka ucuna bağlanmak</span><span class="sxs-lookup"><span data-stu-id="d65b6-114">Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="d65b6-115">Bu öğreticide "Merhaba en az gerekli toocollect veri kümesi ve bir anında iletme bildirimi gönderme bir"temel tümleştirme"gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="d65b6-115">This tutorial presents a "basic integration", which is hello minimal set required toocollect data and send a push notification.</span></span> <span data-ttu-id="d65b6-116">Android Studio toodemonstrate hello Tümleştirmesi ile temel bir uygulama oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d65b6-116">You create a basic app with Android Studio toodemonstrate hello integration.</span></span>

<span data-ttu-id="d65b6-117">Merhaba tümleştirme belgelerinin tamamı hello bulunabilir [Mobile Engagement Android SDK tümleştirmesi](mobile-engagement-android-sdk-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d65b6-117">hello complete integration documentation can be found in hello [Mobile Engagement Android SDK integration](mobile-engagement-android-sdk-overview.md).</span></span>

### <a name="create-an-android-project"></a><span data-ttu-id="d65b6-118">Android projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="d65b6-118">Create an Android project</span></span>
1. <span data-ttu-id="d65b6-119">Başlat **Android Studio**, hello açılır pencerede seçip **yeni bir Android Studio projesi Başlat**.</span><span class="sxs-lookup"><span data-stu-id="d65b6-119">Start **Android Studio**, and in hello pop-up, select **Start a new Android Studio project**.</span></span>

    ![][1]
2. <span data-ttu-id="d65b6-120">Uygulama adı ve şirket etki alanı belirtin.</span><span class="sxs-lookup"><span data-stu-id="d65b6-120">Provide an app name and company domain.</span></span> <span data-ttu-id="d65b6-121">Girdiğiniz bilgileri daha sonra kullanmanız gerekeceğinden bunları not edin.</span><span class="sxs-lookup"><span data-stu-id="d65b6-121">Make a note of what you are filling, because you need it later.</span></span> <span data-ttu-id="d65b6-122">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d65b6-122">Click **Next**.</span></span>

    ![][2]
3. <span data-ttu-id="d65b6-123">Merhaba hedef form faktörünü ve API düzeyini seçin ve tıklayın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="d65b6-123">Select hello target form factor and API level, and click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="d65b6-124">Mobile Engagement, en az API düzey 10 (Android 2.3.3) gerektirir.</span><span class="sxs-lookup"><span data-stu-id="d65b6-124">Mobile Engagement requires API level 10 minimum (Android 2.3.3).</span></span>
   >
   >

    ![][3]
4. <span data-ttu-id="d65b6-125">Seçin **boş etkinlik** hello yalnızca ekran bu uygulama ve tıklatın burada **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="d65b6-125">Select **Blank Activity** here, which is hello only screen for this app and click **Next**.</span></span>

    ![][4]
5. <span data-ttu-id="d65b6-126">Son olarak, olan ve'ı tıklatın hello Varsayılanları bırakabilir **son**.</span><span class="sxs-lookup"><span data-stu-id="d65b6-126">Finally, leave hello defaults as is and click **Finish**.</span></span>

    ![][5]

<span data-ttu-id="d65b6-127">Android Studio şimdi içine biz Mobile Engagement tümleştirmek hello tanıtım uygulamasını oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d65b6-127">Android Studio now creates hello demo app into which we integrate Mobile Engagement.</span></span>

### <a name="include-hello-sdk-library-in-your-project"></a><span data-ttu-id="d65b6-128">Merhaba SDK kitaplığını projenize ekleme</span><span class="sxs-lookup"><span data-stu-id="d65b6-128">Include hello SDK library in your project</span></span>
1. <span data-ttu-id="d65b6-129">Merhaba karşıdan [Mobile Engagement Android SDK](https://aka.ms/vq9mfn).</span><span class="sxs-lookup"><span data-stu-id="d65b6-129">Download hello [Mobile Engagement Android SDK](https://aka.ms/vq9mfn).</span></span>
2. <span data-ttu-id="d65b6-130">Bilgisayarınızdaki Hello arşiv dosyasını tooa klasöre ayıklayın.</span><span class="sxs-lookup"><span data-stu-id="d65b6-130">Extract hello archive file tooa folder in your computer.</span></span>
3. <span data-ttu-id="d65b6-131">Bu SDK'ın geçerli sürümü hello Hello .jar kitaplığını belirleyin ve toohello panoya kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="d65b6-131">Identify hello .jar library for hello current version of this SDK and copy it toohello Clipboard.</span></span>

      ![][6]
4. <span data-ttu-id="d65b6-132">Toohello gidin **proje** bölümünde (1) ve hello .jar (2) hello libs klasörüne yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="d65b6-132">Navigate toohello **Project** section (1) and paste hello .jar in hello libs folder (2).</span></span>

      ![][7]
5. <span data-ttu-id="d65b6-133">tooload hello kitaplığı, Merhaba projeyi Eşitle.</span><span class="sxs-lookup"><span data-stu-id="d65b6-133">tooload hello library, sync hello project .</span></span>

      ![][8]

### <a name="connect-your-app-toomobile-engagement-backend-with-hello-connection-string"></a><span data-ttu-id="d65b6-134">Bağlantı dizesi hello ile uygulamanızın tooMobile Engagement arka ucuna bağlanmak</span><span class="sxs-lookup"><span data-stu-id="d65b6-134">Connect your app tooMobile Engagement backend with hello Connection String</span></span>
1. <span data-ttu-id="d65b6-135">(Yalnızca tek bir yerde genellikle hello Ana faaliyet, uygulamanızın yapılmalıdır) hello etkinlik oluşturma içine kod satırı aşağıdaki hello kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="d65b6-135">Copy hello following lines of code into hello activity creation (must be done only in one place of your application, usually hello main activity).</span></span> <span data-ttu-id="d65b6-136">Bu örnek uygulama için src altında MainActivity hello açın main -> java klasörü ve hello aşağıdakileri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="d65b6-136">For this sample app, open up hello MainActivity under src -> main -> java folder and add hello following:</span></span>

        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
        EngagementAgent.getInstance(this).init(engagementConfiguration);
2. <span data-ttu-id="d65b6-137">Alt + Enter tuşuna basarak veya içeri aktarma deyimlerini aşağıdaki hello ekleyerek Hello başvuruları çözümlenemedi:</span><span class="sxs-lookup"><span data-stu-id="d65b6-137">Resolve hello references by pressing Alt + Enter or adding hello following import statements:</span></span>

        import com.microsoft.azure.engagement.EngagementAgent;
        import com.microsoft.azure.engagement.EngagementConfiguration;
3. <span data-ttu-id="d65b6-138">Toohello Azure Klasik Portalı'nda, uygulamanızın dön **bağlantı bilgisi** sayfası ve kopyalama hello **bağlantı dizesi**.</span><span class="sxs-lookup"><span data-stu-id="d65b6-138">Go back toohello Azure Classic Portal in your app's **Connection Info** page and copy hello **Connection String**.</span></span>

      ![][9]
4. <span data-ttu-id="d65b6-139">Merhaba yapıştırma `setConnectionString` hello tüm dizeyi koddan hello gösterilen değiştirme parametresi:</span><span class="sxs-lookup"><span data-stu-id="d65b6-139">Paste it into hello `setConnectionString` parameter, replacing hello entire string shown in hello following code:</span></span>

        engagementConfiguration.setConnectionString("Endpoint=my-company-name.device.mobileengagement.windows.net;SdkKey=********************;AppId=*********");

### <a name="add-permissions-and-a-service-declaration"></a><span data-ttu-id="d65b6-140">İzinler ve bir hizmet bildirimi ekleme</span><span class="sxs-lookup"><span data-stu-id="d65b6-140">Add permissions and a service declaration</span></span>
1. <span data-ttu-id="d65b6-141">Bu izinleri toohello projenizin manifest.xml dosyasında hemen önce veya sonra hello eklemek `<application>` etiketi:</span><span class="sxs-lookup"><span data-stu-id="d65b6-141">Add these permissions toohello Manifest.xml of your project immediately before or after hello `<application>` tag:</span></span>

        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
        <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
        <uses-permission android:name="android.permission.VIBRATE" />
        <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
2. <span data-ttu-id="d65b6-142">toodeclare Merhaba Aracısı hizmeti, bu kod hello arasında eklemek `<application>` ve `</application>` etiketler:</span><span class="sxs-lookup"><span data-stu-id="d65b6-142">toodeclare hello agent service, add this code between hello `<application>` and `</application>` tags:</span></span>

        <service
             android:name="com.microsoft.azure.engagement.service.EngagementService"
             android:exported="false"
             android:label="<Your application name>"
             android:process=":Engagement"/>
3. <span data-ttu-id="d65b6-143">Yapıştırdığınız hello kodla `"<Your application name>"` hello etiketinde görüntülendiği hello **ayarları** burada görebilirsiniz hello cihazda çalışan hizmetleri menüsü.</span><span class="sxs-lookup"><span data-stu-id="d65b6-143">In hello code you pasted, replace `"<Your application name>"` in hello label, which is displayed in hello **Settings** menu where you can see services running on hello device.</span></span> <span data-ttu-id="d65b6-144">Örneğin bu etikete "Hizmet" Merhaba sözcüğünü ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d65b6-144">You can add hello word "Service" in that label for example.</span></span>

### <a name="send-a-screen-toomobile-engagement"></a><span data-ttu-id="d65b6-145">Ekran tooMobile katılım Gönder</span><span class="sxs-lookup"><span data-stu-id="d65b6-145">Send a screen tooMobile Engagement</span></span>
<span data-ttu-id="d65b6-146">verileri gönderme toostart ve olun hello kullanıcıların etkin olduğundan, en az bir ekran (etkinlik) toohello Mobile Engagement arka göndermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="d65b6-146">toostart sending data and ensure that hello users are active, you must send at least one screen (Activity) toohello Mobile Engagement backend.</span></span>

<span data-ttu-id="d65b6-147">Çok Git**MainActivity.java** ve tooreplace hello temel sınıfını aşağıdaki hello ekleyin **MainActivity** çok**EngagementActivity**:</span><span class="sxs-lookup"><span data-stu-id="d65b6-147">Go too**MainActivity.java** and add hello following tooreplace hello base class of **MainActivity** too**EngagementActivity**:</span></span>

    public class MainActivity extends EngagementActivity {

> [!NOTE]
> <span data-ttu-id="d65b6-148">Temel sınıfınız değilse *etkinlik*, başvurun [Gelişmiş Android raporlama](mobile-engagement-android-advanced-reporting.md) nasıl tooinherit farklı sınıflardan.</span><span class="sxs-lookup"><span data-stu-id="d65b6-148">If your base class is not *Activity*, consult [Advanced Android Reporting](mobile-engagement-android-advanced-reporting.md) for how tooinherit from different classes.</span></span>
>
>

<span data-ttu-id="d65b6-149">Bu basit Örnek senaryo için satır aşağıdaki hello çıkışı Açıklama:</span><span class="sxs-lookup"><span data-stu-id="d65b6-149">Comment out hello following line for this simple sample scenario:</span></span>

    // setSupportActionBar(toolbar);

<span data-ttu-id="d65b6-150">Tookeep hello istiyorsanız `ActionBar` , uygulamanızda bkz [Gelişmiş Android raporlama](mobile-engagement-android-advanced-reporting.md).</span><span class="sxs-lookup"><span data-stu-id="d65b6-150">If you want tookeep hello `ActionBar` in your app, see [Advanced Android Reporting](mobile-engagement-android-advanced-reporting.md).</span></span>

## <a name="connect-app-with-real-time-monitoring"></a><span data-ttu-id="d65b6-151">Uygulamayı gerçek zamanlı izlemeyle bağlama</span><span class="sxs-lookup"><span data-stu-id="d65b6-151">Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a name="enable-push-notifications-and-in-app-messaging"></a><span data-ttu-id="d65b6-152">Anında iletme bildirimlerini ve uygulama içi mesajlaşmayı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="d65b6-152">Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="d65b6-153">Mobile Engagement, bir kampanya sırasında anında iletme bildirimleri ve uygulama içi mesajlaşma ile kullanıcılarınızla etkileşim kurmanızı ve REACH ile kullanıcılarınıza ulaşmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="d65b6-153">During a campaign, Mobile Engagement lets you interact with and REACH your users with push notifications and in-app messaging.</span></span> <span data-ttu-id="d65b6-154">Bu modül hello Mobile Engagement portalında REACH adı verilir.</span><span class="sxs-lookup"><span data-stu-id="d65b6-154">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="d65b6-155">bölümden Merhaba, uygulama tooreceive bunları ayarlar.</span><span class="sxs-lookup"><span data-stu-id="d65b6-155">hello following section sets up your app tooreceive them.</span></span>

### <a name="copy-sdk-resources-in-your-project"></a><span data-ttu-id="d65b6-156">SDK kaynaklarını projenize kopyalama</span><span class="sxs-lookup"><span data-stu-id="d65b6-156">Copy SDK resources in your project</span></span>
1. <span data-ttu-id="d65b6-157">İçerik ve kopyalama geri tooyour SDK yükleme hello gidin **res** klasör.</span><span class="sxs-lookup"><span data-stu-id="d65b6-157">Navigate back tooyour SDK download content and copy hello **res** folder.</span></span>

    ![][10]
2. <span data-ttu-id="d65b6-158">TooAndroid Studio, select hello dön **ana** proje dosyalarınıza dizin ve tooadd hello kaynakları tooyour proje yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="d65b6-158">Go back tooAndroid Studio, select hello **main** directory of your project files, and then paste it tooadd hello resources tooyour project.</span></span>

    ![][11]

[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

[!INCLUDE [Enable in-app messaging](../../includes/mobile-engagement-android-send-push.md)]

[!INCLUDE [Send notification from portal](../../includes/mobile-engagement-android-send-push-from-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="d65b6-159">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d65b6-159">Next steps</span></span>
<span data-ttu-id="d65b6-160">Çok Git[Android SDK](mobile-engagement-android-sdk-overview.md) tooget ayrıntılı hello SDK tümleştirmesi hakkında bilgi.</span><span class="sxs-lookup"><span data-stu-id="d65b6-160">Go too[Android SDK](mobile-engagement-android-sdk-overview.md) tooget detailed knowledge about hello SDK integration.</span></span>

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
